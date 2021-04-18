---
title: Configuración del tipo de solicitud HTTP en el reproductor
description: Configuración del tipo de solicitud HTTP en el reproductor
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 100%

---

# Configuración del tipo de solicitud HTTP {#setting-the-http-request-type}

El cuerpo de la solicitud de todas las solicitudes de API de Media Collection debe estar en formato JSON, por lo que debe establecer el tipo de solicitud de contenido en el reproductor. Por ejemplo, en JavaScript se establecería el encabezado de solicitud `Content-Type` como se indica a continuación:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
