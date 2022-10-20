---
title: ¿Qué es la habilitación de Adobe Audience Manager?
description: Esta función le permite vincular acciones de aplicación a datos de seguimiento de medios sin necesidad de reglas de procesamiento ni variables personalizadas adicionales.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 3e996d243d060a6fd07d2ddbabf05e39eca40758
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 95%

---

# Habilitación de Audience Manager{#audience-manager-enablement}

Adobe Audience Manager (AAM), una plataforma de Gestión de datos (DMP), le ayuda a reunir los recursos de datos de su audiencia, lo que facilita la recopilación de información relevante desde el punto de vista comercial sobre los visitantes del sitio, la creación de segmentos comercializables y la distribución de contenido y publicidad dirigidos a la audiencia correcta.

Con AAM, no dependerá de un vendedor de datos, un intercambio o una plataforma de demanda. Además, AAM es completamente agnóstico cuando se trata de los recursos de datos de sus socios. Con acceso a múltiples fuentes de datos, AAM ofrece a los editores digitales la capacidad de usar una amplia variedad de datos de terceros. Para obtener más información sobre AAM, consulte la documentación de AAM sobre la [Documentación del producto de Audience Manager](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.html).

**Transferencia de datos de VA a AAM:** Tanto para el contenido de vídeo como para los anuncios de vídeo, las métricas y los metadatos recopilados mediante variables de solución (reservadas) se pueden enviar automáticamente a AAM. La transferencia de datos está disponible en todas las plataformas, incluidos equipos de escritorio, dispositivos móviles y OTT. Para habilitar esta transferencia de datos del lado del servidor, debe ponerse en contacto con el equipo de Atención al cliente de Adobe y solicitar que se habilite esta fuente.

>[!IMPORTANT]
>
>Para garantizar la transferencia perfecta de datos en AAM, debe contar con las últimas versiones de las bibliotecas de Media SDK.

Los datos federados admiten totalmente el uso compartido de datos con AAM. Contacte con su equipo de Adobe para confirmar la configuración de Datos federados.

## Métodos OTT/AAM {#ott-aam-methods}

Puede utilizar estos métodos para enviar señales y recuperar segmentos de visitantes de Audience Manager:

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   Devuelve el perfil del visitante que se haya obtenido más recientemente. Devuelve un objeto vacío si todavía no se ha enviado ninguna señal.

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   Devuelve el perfil del visitante que se haya obtenido más recientemente. Devuelve un objeto vacío si todavía no se ha enviado ninguna señal.

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   Devuelve el DPUUID actual.

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   Establece el DPID y el DPUUID. Si se establecen DPID y DPUUID, se enviarán con cada señal.

   ```js
   ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   Envía una señal con rasgos a la gestión de audiencias.

   ```js
   ADBMobile.audienceManager.submitSignal({"sampleTrait":"sampleValue"});
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   Devuelve el perfil del visitante que se haya obtenido más recientemente. Devuelve un objeto vacío si todavía no se ha enviado ninguna señal.

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   Devuelve el perfil del visitante que se haya obtenido más recientemente. Devuelve un objeto vacío si todavía no se ha enviado ninguna señal.

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   Devuelve el DPUUID actual.

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   Establece el DPID y el DPUUID. Si se establecen DPID y DPUUID, se enviarán con cada señal.

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   Envía una señal con rasgos a la gestión de audiencias.

   ```js
   traitData = {}
   traitData["sampleTrait"] = "sampleValue"
   ADBMobile().audienceSubmitSignal(traitData)
   ```
