---
title: Obtención de un ID de sesión
description: Aprenda a codificar una solicitud de sesiones para obtener el ID de sesión del encabezado Ubicación en una respuesta.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 69%

---

# Obtención de un ID de sesión{#obtaining-a-session-id}

Este fragmento de código del reproductor de referencia muestra una forma de codificar una [solicitud de sesiones](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) junto con la extracción del ID de sesión (y la versión de la API de recopilación de contenido) en el encabezado Ubicación en la respuesta:

```js
var  
sessionData = { 
        ... 
        "media.contentType": "VOD", 
        "media.channel": "sample-channel", 
        ... 
    } 
}; 
...

const SESSION_ID_EXTRACTOR = /^\/api\/(.*)\/sessions\/(.*)/; 
    ...
    apiClient.request({ 
        "baseUrl": config.apiBaseUrl,   // The endpoint 
        "path": config.apiSessionsPath, // api/v1/sessions/ 
        "method": "POST",               // (Always POST) 
        "data": sessionData             // Mandatory params 
     }).then((response) => { 
        // Extract Session ID (and API version) 
        const [, apiVersion, sessionId] =  response.headers.Location.match(SESSION_ID_EXTRACTOR);  
        this.sessionId = sessionId;     // Session ID obtained 
        this._sessionStarted = true;    // Session started. 
    ...
```
