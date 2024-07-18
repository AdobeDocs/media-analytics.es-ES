---
title: "Streaming Media Collection API - Inicio rápido"
description: Introducción a la API de medios de streaming. Aprenda a verificar rápidamente los datos de su solicitud.
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 100%

---

# Inicio rápido{#quick-start}

>[!TIP]
>
>Recopile los datos de solicitud necesarios para completar una solicitud de [sesión correcta](../mc-api-ref/mc-api-sessions-req.md) en el servidor back-end de la API de recopilación de Media Analytics (MA). Puede verificar rápidamente los datos de solicitud enviando solicitudes manualmente (con `curl` o Postman, etc.). Esto le proporcionará información inmediata sobre si tiene problemas con tipos de datos incorrectos o con información incorrecta en la solicitud. Utilice los [esquemas de validación JSON](../mc-api-ref/mc-api-json-validation.md) para comprobar que está suministrando los datos de solicitud adecuados.

1. Reúna los datos estándar y requeridos de Adobe Analytics y Visitante que debe proporcionar para ejecutar cualquiera de las aplicaciones de Experience Cloud:

   * ID de organización para visitantes en Experience Cloud
   * ID de usuario para visitantes en Experience Cloud
   * ID de grupo de informes de Analytics
   * URL de servidor de seguimiento de Analytics

1. Cree un objeto JSON para su solicitud de `sessions` que contenga los datos mínimos necesarios para una llamada correcta. Por ejemplo:

   ```json
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
   >Debe utilizar los tipos de datos correctos en el cuerpo de la solicitud JSON. Por ejemplo, `analytics.enableSSL` requiere un booleano, `media.length` es numérico, etc. Puede comprobar los tipos de parámetros y los requisitos obligatorios frente a los requisitos opcionales comprobando los [esquemas de validación de JSON.](mc-api-validate-reqs.md)

1. Envíe solicitudes de sesiones al punto final de la API de recopilación de MA. Si la carga de la solicitud no es válida, identifique el problema y vuelva a intentarlo hasta que obtenga una respuesta de `201 Created`. En este ejemplo de `curl`, el cuerpo de la solicitud JSON se encuentra en un archivo denominado `sample_data_session`:

   ```sh
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

Si la [solicitud de sesiones](../mc-api-ref/mc-api-sessions-req.md) se realiza correctamente, recibirá una respuesta de `201 Created` similar a la anterior. La respuesta incluye un ID de sesión en el encabezado Ubicación. El ID de sesión es la información crucial de la respuesta, ya que es necesaria para todas las llamadas de seguimiento subsiguientes. Una vez que se haya devuelto correctamente una [solicitud de sesiones](../mc-api-ref/mc-api-sessions-req.md), puede continuar con la implementación del seguimiento de vídeo con la API de MA en su reproductor de vídeo.
