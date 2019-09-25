---
seo-title: Configuración del tipo de solicitud HTTP en el reproductor
title: Configuración del tipo de solicitud HTTP en el reproductor
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# Configuración del tipo de solicitud HTTP {#setting-the-http-request-type}

El cuerpo de la solicitud de todas las solicitudes de API de Media Collection debe estar en formato JSON, por lo que debe establecer el tipo de solicitud de contenido en el reproductor. Por ejemplo, en JavaScript se establecería el encabezado de solicitud `Content-Type` como se indica a continuación:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

