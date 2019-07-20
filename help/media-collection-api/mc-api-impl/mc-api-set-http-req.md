---
seo-title: Configuración del tipo de solicitud HTTP en el reproductor
title: Configuración del tipo de solicitud HTTP en el reproductor
uuid: b 8 fa 7233-e 654-4 acf-a 9 d 7-14158 cded 13 e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# Setting the HTTP request type {#setting-the-http-request-type}

El cuerpo de la solicitud de todas las solicitudes de API de Media Collection debe estar en formato JSON, por lo que debe establecer el tipo de solicitud de contenido en el reproductor. Por ejemplo, en JavaScript se establecería el encabezado de solicitud `Content-Type` como se indica a continuación:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

