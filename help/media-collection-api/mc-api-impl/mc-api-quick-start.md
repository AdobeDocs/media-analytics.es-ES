---
seo-title: Inicio rápido
title: Inicio rápido
uuid: ca 20 bad 4-2 c 8 f -406 b -833 e-b 4883 a 9 aa 534
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Inicio rápido{#quick-start}

>[!TIP]
>
>Gather the request data necessary for completing a successful [Session request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) to the Media Analytics (MA) Collection API back-end server. Puede verificar rápidamente los datos de solicitud enviando solicitudes manualmente (con `curl` o Postman, etc.). Esto le indicará de inmediato si en su solicitud hay problemas con tipos de datos incorrectos o información incorrecta. Utilice los [esquemas de validación de JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) para verificar que está suministrando los datos de solicitud adecuados.

1. Recopile los datos estándar de Adobe Analytics y del visitante que debe proporcionar para ejecutar cualquiera de las aplicaciones de Experience Cloud:

   * ID de organización para visitantes en Experience Cloud
   * ID de usuario de Experience Cloud
   * ID de informes de Analytics
   * URL del servidor de seguimiento de análisis

1. Create a JSON object for your `sessions` request body, containing the minimum data required for a successful call. Por ejemplo:

   ```
   { 
       "playerTime": { 
           "playhead": 0, 
           "ts": 1234560890123 
       }, 
       "eventType": "sessionStart", 
       "params": { 
           "media.playerName": "sample-html5-api-player", 
           "analytics.trackingServer": "[YOUR_TS]", 
           "analytics.reportSuite": "[YOUR_RSID]", 
           "media.contentType": "VOD", 
           "media.length": 60.39333333333333, 
           "media.id": "MA Collection API Sample Player", 
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]", 
           "visitor.marketingCloudUserId": "[YOUR_ECID]",
           "media.name": "ClickMe", 
           "media.channel": "sample-channel", 
           "media.sdkVersion": "va-api-0.0.0", 
           "analytics.enableSSL": false 
       } 
   }
   ```

   >[!NOTE]
   >
   >Debe utilizar los tipos de datos correctos en el cuerpo de solicitud JSON. E.g., `analytics.enableSSL` requires a boolean, `media.length` is numeric, etc. Puede comprobar los tipos de parámetros y los requisitos obligatorios frente a los requisitos opcionales comprobando los [esquemas de validación de JSON.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. Envíe solicitudes de sesiones al extremo de API de recopilación de MA Collection. Si la carga de la solicitud no es válida, identifique el problema y vuelva a intentarlo hasta que obtenga una respuesta de `201 Created`. In this `curl` example, the JSON request body is in a file named `sample_data_session`:

   ```
   $ curl -i -d \ 
     @sample_data_session https://{uri}/api/v1/sessions \ 
     > curl.sessions.out 
   
   $ cat curl.sessions.out 
   HTTP/1.1 201 Created 
   Server: nginx/1.13.5 
   Date: Mon, 18 Dec 2017 22:34:12 GMT 
   Content-Type: application/octet-stream 
   Content-Length: 0 
   Connection: keep-alive 
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: * 
   Access-Control-Allow-Methods: OPTIONS,POST,PUT 
   Access-Control-Allow-Headers: Content-Type 
   Access-Control-Expose-Headers: Location
   ```

Si la [solicitud de sesiones](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) se realiza correctamente, recibirá una respuesta de `201 Created` similar a la anterior. La respuesta incluye un ID de sesión en el encabezado Ubicación. El ID de sesión es información fundamental en la respuesta, ya que es necesaria para todas las llamadas de seguimiento subsiguientes. After a successful return of a [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md), you can confidently proceed with implementing video tracking using the MA API in your video player.
