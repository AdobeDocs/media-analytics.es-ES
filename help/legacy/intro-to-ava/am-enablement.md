---
title: ¿Qué es la habilitación de Adobe Audience Manager?
description: Esta función le permite vincular acciones de aplicación a datos de seguimiento de medios sin necesidad de reglas de procesamiento ni variables personalizadas adicionales.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oInE3GwgI1k5-UbqMUm9yvjXfIF0SsRXPrnUWmWT9Ww
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 100%

---

# Habilitación de Audience Manager{#audience-manager-enablement}

Adobe Audience Manager (AAM), una plataforma de Gestión de datos (DMP), le ayuda a reunir los recursos de datos de su audiencia, lo que facilita la recopilación de información relevante desde el punto de vista comercial sobre los visitantes del sitio, la creación de segmentos comercializables y la distribución de contenido y publicidad dirigidos a la audiencia correcta.

Con AAM, no dependerá de un vendedor de datos, un intercambio o una plataforma de demanda. Además, AAM es completamente agnóstico cuando se trata de los recursos de datos de sus socios. Con acceso a múltiples fuentes de datos, AAM permite a los editores digitales utilizar una amplia variedad de datos de terceros. Para obtener más información sobre AAM, consulte la documentación de AAM sobre la [Documentación del producto de Audience Manager](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.html).

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

  Envía una señal con rasgos a la gestión de públicos.

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

  Envía una señal con rasgos a la gestión de públicos.

  ```js
  traitData = {}
  traitData["sampleTrait"] = "sampleValue"
  ADBMobile().audienceSubmitSignal(traitData)
  ```
