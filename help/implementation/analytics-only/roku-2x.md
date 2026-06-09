---
title: Configuración de Roku 2.x para medios de streaming
description: Instale y configure Adobe Media SDK 2.x para Roku para implementaciones de medios de streaming solo de Analytics, incluidos los canales de SceneGraph.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---

# Configuración de Roku 2.x para medios de streaming

Adobe Media SDK 2.x para Roku (`adbmobile.brs`) envía datos de medios de transmisión de canales Roku escritos en BrightScript directamente a Adobe Analytics. También recopila datos de audiencia a través de Audience Manager y mide la participación a través de eventos de medios.

>[!NOTE]
>
>Esta página cubre Media SDK 2.x solo para Analytics para Roku. Para nuevas implementaciones, Adobe recomienda [Roku Edge SDK](/help/implementation/edge/roku.md), que pone los datos a disposición de Customer Journey Analytics, Adobe Journey Optimizer y Real-Time CDP además de Adobe Analytics.

* **Requisitos previos**:
   * Complete la [descripción general de la implementación solo de Analytics](overview.md).
   * [Descargar Media SDK para Roku](/help/getting-started/download-sdks.md).
   * Incluya una API en el reproductor de contenido para suscribirse a eventos del reproductor y una API que proporcione información del reproductor, como el nombre del contenido y la posición del cabezal de reproducción.

## Instalación de SDK

La descarga de `AdobeMobileLibrary-2.*-Roku.zip` contiene dos componentes:

* `adbmobile.brs`: el archivo de biblioteca. Cópielo en el directorio `pkg:/source/` del canal.
* `ADBMobileConfig.json`: el archivo de configuración de SDK, personalizado para su aplicación.

Para los canales de SceneGraph, copie también `adbmobileTask.brs` y `adbmobileTask.xml` en el directorio `pkg:/components/`. Consulte [Compatibilidad con SceneGraph](#scenegraph).

## Configurar ADBMobileConfig.json

El JSON de configuración tiene una clave `mediaHeartbeat` exclusiva para los medios de transmisión. Agregue `ADBMobileConfig.json` al origen del proyecto y establezca los valores `mediaHeartbeat`, `marketingCloud` y `analytics`:

```json
{
  "analytics": {
    "rsids": "your-report-suite-id",
    "server": "your-analytics-server"
  },
  "marketingCloud": {
    "org": "YOUR-MCORG-ID@AdobeOrg"
  },
  "mediaHeartbeat": {
    "server": "your-namespace.hb-api.omtrdc.net",
    "publisher": "your-publisher-id",
    "channel": "sample-channel",
    "ssl": true,
    "ovp": "sample-ovp",
    "sdkVersion": "sample-sdk",
    "playerName": "Roku Player"
  }
}
```

| Parámetro de configuración | Descripción |
| --- | --- |
| `server` | URL del extremo de seguimiento de medios. Consulte la [descripción general de la implementación solo de Analytics](overview.md). |
| `publisher` | Identificador único del editor de contenido. |
| `channel` | Nombre del canal de distribución de contenido. Notificado como [Canal de contenido](/help/implementation/variables/core/content-channel.md). |
| `ssl` | Si SSL se utiliza para rastrear llamadas. |
| `ovp` | Nombre del proveedor de la plataforma de vídeo en línea. |
| `sdkVersion` | Versión actual de su aplicación o SDK. |
| `playerName` | Nombre del reproductor. Notificado como [Nombre del reproductor de contenido](/help/implementation/variables/core/content-player-name.md). |

>[!IMPORTANT]
>
>Si `mediaHeartbeat` está configurado incorrectamente, el módulo multimedia entrará en un estado de error y dejará de enviar llamadas de seguimiento. Asegúrese de que su valor `marketingCloud.org` incluya `@AdobeOrg`.

## Inicialización de SDK y procesamiento de mensajes

Obtenga una instancia de SDK con `ADBMobile()`. El servicio de ID de visitante de Experience Cloud genera un ID de visitante que se incluye en todas las visitas.

>[!IMPORTANT]
>
>Llame a `processMessages` y a `processMediaMessages` en el bucle de evento principal cada 250 ms para que SDK envíe los pings correctamente.

```brightscript
adb = ADBMobile()

' In your main event loop, every ~250 ms:
adb.processMessages()
adb.processMediaMessages()
```

| Método | Descripción |
| --- | --- |
| `processMessages` | Pasa eventos de Analytics en cola a SDK. |
| `processMediaMessages` | Pasa eventos de medios en cola a SDK, incluidos los pings automáticos. |

## Seguimiento de eventos de medios

Rastree cada evento multimedia llamando a su método SDK. Consulte la pestaña **Roku 2.x** en cada página de [evento](/help/implementation/events/overview.md) y [variable](/help/implementation/variables/overview.md) para ver las llamadas, los generadores y las constantes exactos.

Una sesión típica comienza con la creación de un objeto multimedia y la llamada a `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Mr. Robot", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

contextData = { "a.media.show": "Mr. Robot" }

adb.mediaTrackSessionStart(mediaInfo, contextData)
```

Los generadores globales de `adb_media_init_*` crean los objetos de medios, publicidad, pausa publicitaria, capítulo y QoS utilizados por las llamadas de seguimiento:

| Generador | Firma |
| --- | --- |
| Medios | `adb_media_init_mediainfo(name, id, length, streamType, mediaType)` |
| Publicidad | `adb_media_init_adinfo(name, id, position, length)` |
| Desglose de anuncios | `adb_media_init_adbreakinfo(name, startTime, position)` |
| Capítulo | `adb_media_init_chapterinfo(name, position, length, startTime)` |
| QoS | `adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)` |

Los metadatos estándar se pasan como una matriz asociativa de claves `a.media.*` (SDK también define constantes con nombre como `MEDIA_VideoMetadataKeySHOW` para estas claves). Consulte las páginas de [Variables](/help/implementation/variables/overview.md) para ver la clave que corresponde a cada dimensión.

## Configure el ID de visitante de Experience Cloud, la privacidad y el registro

Los siguientes métodos de la instancia `ADBMobile()` administran la identidad, la privacidad y la depuración:

| Método | Descripción |
| --- | --- |
| `visitorMarketingCloudID()` | Recupera el Experience Cloud ID (ECID). |
| `visitorSyncIdentifiers(identifiers)` | Establece ID de cliente adicionales para el mismo visitante. |
| `setAdvertisingIdentifier(rida)` | Establece el ID de Roku para Advertising (RIDA). Consíguelo con la API Roku [`getRIDA()`](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic). |
| `getAllIdentifiers()` | Devuelve todos los identificadores almacenados por SDK, incluidos los de Analytics, Visitante, Audience Manager y personalizados. |
| `setPrivacyStatus(status)` | Establece el estado de privacidad. Pase `adb.PRIVACY_STATUS_OPT_IN` o `adb.PRIVACY_STATUS_OPT_OUT`. Consulte [Privacidad](/help/implementation/opt-out-privacy.md). |
| `getPrivacyStatus()` | Devuelve el estado de privacidad actual. |
| `setDebugLogging(flag)` | Habilita o deshabilita el registro de depuración. |
| `getDebugLogging()` | Devuelve `true` si el registro de depuración está habilitado. |

## Compatibilidad con SceneGraph {#scenegraph}

El marco XML de Roku SceneGraph no puede llamar directamente a las API heredadas de BrightScript SDK, ya que SDK utiliza componentes (como subprocesos) que no están disponibles para una aplicación SceneGraph. Para reducir esta brecha, SDK proporciona un conector que devuelve una instancia compatible con SceneGraph que expone las mismas API, además de un mecanismo de llamada de retorno para las API que devuelven datos.

El puente consta de tres partes:

* **`adbmobileTask`nodo**: un nodo de tareas de SceneGraph que ejecuta las API de SDK en un subproceso en segundo plano y devuelve datos a las escenas.
* **Instancia del conector**: envuelve todas las API públicas heredadas y se comunica con el nodo `adbmobileTask`.
* **`API_RESPONSE`llamada de retorno**: el campo que observa su aplicación para recibir valores devueltos por las API de captador.

Para inicializar SDK en un canal de SceneGraph:

1. Importar `adbmobile.brs` en su escena:

   ```brightscript
   <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
   ```

1. Cree el nodo `adbmobileTask`, obtenga la instancia del conector y cargue las constantes de SceneGraph:

   ```brightscript
   m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
   m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
   m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
   ```

1. Registre una llamada de retorno para recibir objetos de respuesta para API que devuelvan datos:

   ```brightscript
   m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE, "onAdbmobileApiResponse")
   
   function onAdbmobileApiResponse() as void
       responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
       if responseObject <> invalid
           methodName = responseObject.apiName
           retVal = responseObject.returnValue
           if methodName = m.adbmobileConstants.PRIVACY_STATUS
               print "Privacy status: " + retVal
           end if
       end if
   end function
   ```

La instancia del conector (`m.adbmobile`) expone los mismos métodos multimedia que el SDK heredado (`mediaTrackSessionStart`, `mediaTrackPlay`, `mediaTrackPause`, `mediaTrackComplete`, `mediaTrackSessionEnd`, `mediaTrackError`, `mediaTrackEvent`, `mediaUpdatePlayhead` y `mediaUpdateQoS`), de modo que las llamadas que se muestran en las páginas de evento y de variable funcionan de la misma manera. Las API de establecimiento se llaman directamente; las API de captador devuelven sus valores mediante la llamada de retorno `API_RESPONSE`.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones solo de Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Resumen de eventos](/help/implementation/events/overview.md)
>* [Resumen de variables](/help/implementation/variables/overview.md)
>* [Roku Edge SDK](/help/implementation/edge/roku.md)
