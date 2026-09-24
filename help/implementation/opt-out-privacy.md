---
title: Configuración de privacidad y exclusión
description: Cómo gestionar la inclusión, la exclusión y la privacidad.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 3%
---
# Configuración de privacidad y exclusión

Cuando un usuario se excluye del seguimiento, la biblioteca de medios de streaming detiene inmediatamente toda la actividad de recopilación de datos. No se envían llamadas de inicio de sesión, ni pings de latidos ni datos de seguimiento de eventos a los servidores de recopilación de datos de Adobe para ese usuario.

## Inclusión/Exclusión

Los controles de exclusión funcionan por dispositivo o explorador. El respeto del consentimiento del usuario es responsabilidad de la organización de implementación. Para obtener una descripción general de las prácticas de privacidad de Adobe, consulte [Centro de privacidad de Adobe](https://www.adobe.com/es/privacy.html).

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Web SDK respeta las preferencias de consentimiento establecidas mediante el comando `setConsent`. Cuando el consentimiento se establece en `"out"`, Web SDK deja de reenviar todos los eventos, incluidas las llamadas de seguimiento de medios de streaming, a Edge Network. El estado de consentimiento persiste en el almacenamiento del explorador entre sesiones.

Antes de implementar la exclusión, asegúrese de que Web SDK esté configurado con el componente de medios de streaming. Para obtener más información, consulte [Configurar Web SDK](../implementation/edge/web-sdk.md).

Establezca el consentimiento en Opted out con el estándar de consentimiento de Adobe 2.0:

```javascript
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: { val: "n" }
    }
  }]
});
```

Valores de consentimiento:

* `"y"`: Incluido (se permite la recopilación de datos)
* `"n"`: exclusión (recopilación de datos suprimida)
* `"p"`: pendiente (a la espera de una decisión del usuario; no se recopilarán datos hasta que se resuelva)

Para restaurar el seguimiento, vuelva a llamar a `setConsent` con `"y"` como valor de `collect.val`.

Consulte el [comando setConsent](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/setconsent) en la documentación de Web SDK para otros formatos, como IAB TCF 2.0.

>[!TAB iOS]

Adobe Experience Platform Mobile SDK respeta el estado de privacidad establecido mediante `MobileCore.setPrivacyStatus()`. Si se establece el estado en `.optedOut`, se suprime toda la recopilación de datos en todas las extensiones de AEP, incluidos los medios de streaming. El estado persiste entre sesiones de aplicación.

```swift
MobileCore.setPrivacyStatus(.optedOut)
```

Para restaurar el seguimiento, restablezca el estado de privacidad en `.optedIn`:

```swift
MobileCore.setPrivacyStatus(.optedIn)
```

Para obtener más información, consulte [Privacidad y RGPD](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus) en la documentación de AEP Mobile SDK.

>[!TAB Android]

Adobe Experience Platform Mobile SDK respeta el estado de privacidad establecido mediante `MobileCore.setPrivacyStatus()`. Si se establece el estado en `MobilePrivacyStatus.OPT_OUT`, se suprime toda la recopilación de datos en todas las extensiones de AEP, incluidos los medios de streaming. El estado persiste entre sesiones de aplicación.

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT)
```

Para restaurar el seguimiento, restablezca el estado de privacidad en `MobilePrivacyStatus.OPT_IN`:

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_IN)
```

Para obtener más información, consulte [Privacidad y RGPD](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus) en la documentación de AEP Mobile SDK.

>[!TAB Roku Edge]

La SDK de Roku Edge usa `setConsent()` con el estándar de consentimiento de Adobe 2.0. Si se establece `collect.val` en `"n"`, se detendrán inmediatamente todas las recopilaciones de datos, incluidos los eventos de medios de transmisión.

Valores de consentimiento:

* `"y"`: Incluido (se permite la recopilación de datos)
* `"n"`: exclusión (recopilación de datos suprimida)
* `"p"`: pendiente (a la espera de una decisión del usuario; no se recopilarán datos hasta que se resuelva)

```brightscript
currentDate = CreateObject("roDateTime")
timestampInISO8601 = currentDate.ToISOString("milliseconds")

collectConsentNo = {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "metadata": { "time": timestampInISO8601 },
      "collect": { "val": "n" }
    }
  }]
}

m.aepSdk.setConsent(collectConsentNo)
```

Para restaurar el seguimiento, establezca `collect.val` en `"y"` y vuelva a llamar a `setConsent()`.

También puede establecer un valor de consentimiento predeterminado en la inicialización de SDK usando `updateConfiguration()` con la clave `ADB_CONSTANTS.CONFIGURATION.CONSENT_DEFAULT`. Para obtener más información, consulte la [Documentación de Roku Edge SDK](https://github.com/adobe/aepsdk-roku).

>[!TAB API de Media Edge]

La API de Media Edge es una implementación del lado del servidor. Ninguna capa de SDK aplica el consentimiento automáticamente: su aplicación debe comprobar el estado del consentimiento del usuario antes de realizar cualquier llamada de API y suprimir las solicitudes de los usuarios excluidos.

Para la exclusión completa, no PUBLIQUE en el extremo `/va/v2/sessions` (ni en ningún extremo de evento posterior) para los usuarios que han optado por la exclusión:

```javascript
// Check consent status before initiating a media session
if (userHasOptedOut) {
  // Do not call the Media Edge API
  return;
}

// Only call the API for users who have not opted out
fetch("https://edge.adobedc.net/va/v2/sessions", {
  method: "POST",
  body: JSON.stringify(sessionStartPayload)
});
```

Para obtener más información, consulte la [Referencia de la API de Media Edge](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/).

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

La biblioteca Media SDK JS 3.x respeta el estado de exclusión del servicio de ID de visitante de Adobe. Cuando un usuario se excluye mediante el servicio de ID, Media SDK suprime automáticamente todas las llamadas de seguimiento.

```javascript
var visitor = Visitor.getInstance("YOUR_ORG_ID@AdobeOrg");
visitor.setOptOut(true);
```

Reemplace `YOUR_ORG_ID@AdobeOrg` con su ID de organización de Adobe Admin Console.

Para restaurar el seguimiento, pase `false` a `setOptOut()`.

Para obtener más información, consulte [Servicio de ID de visitante de Adobe](https://experienceleague.adobe.com/es/docs/id-service/using/home).

>[!TAB Chromecast]

Chromecast Media SDK 3.x respeta el estado de privacidad establecido mediante `ADBMobile.config.setPrivacyStatus()`. Si se establece el estado en `PRIVACY_STATUS_OPT_OUT`, se suprime toda la recopilación de datos.

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT);
```

Para restaurar el seguimiento, vuelva a establecer el estado en Opted in:

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN);
```

También puede establecer el estado de privacidad predeterminado en la inicialización de SDK en su objeto `ADBMobileConfig`:

```javascript
var ADBMobileConfig = {
  "analytics": {
    "privacyDefault": "optedout"
  }
};
```

>[!TAB Roku 2.x]

La SDK de Roku 2.x respeta el estado de privacidad establecido mediante `setPrivacyStatus`. Si se establece el estado en `PRIVACY_STATUS_OPT_OUT`, se suprime toda la recopilación de datos.

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_OUT)
```

Para restaurar el seguimiento, vuelva a establecer el estado en Opted in:

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_IN)
```

También puede establecer el estado de privacidad predeterminado en la inicialización de SDK en el archivo `ADBMobileConfig.json`:

```json
"analytics": {
  "privacyDefault": "optedout"
}
```

>[!TAB API de recopilación de medios]

La API de recopilación de medios es una implementación del lado del servidor. La aplicación debe comprobar el estado del consentimiento del usuario antes de realizar llamadas a la API y suprimir solicitudes para usuarios excluidos.

Para la exclusión completa, no publique en el punto final de las sesiones para los usuarios que hayan optado por la exclusión.

Para las exclusiones parciales según CCPA, incluya indicadores de exclusión en el objeto `params` de su solicitud `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "analytics.optOutServerSideForwarding": true,
    "analytics.optOutShare": true
  }
}
```

* `analytics.optOutServerSideForwarding`: establezca este valor en `true` para impedir que los datos se compartan entre Adobe Analytics y otras soluciones de Experience Cloud (como Audience Manager).
* `analytics.optOutShare`: se establece en `true` para evitar que se compartan datos federados con otros clientes de Adobe Analytics.

Para obtener una lista completa de los parámetros disponibles, consulte la [referencia de parámetros de solicitud de API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/parameters).

>[!ENDTABS]

