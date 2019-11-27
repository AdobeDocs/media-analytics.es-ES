---
title: Configuración del tipo de solicitud HTTP en el reproductor
description: null
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Configuración del tipo de solicitud HTTP {#setting-the-http-request-type}

El cuerpo de la solicitud de todas las solicitudes de API de Media Collection debe estar en formato JSON, por lo que debe establecer el tipo de solicitud de contenido en el reproductor. Por ejemplo, en JavaScript se establecería el encabezado de solicitud `Content-Type` como se indica a continuación:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

