---
title: Seguimiento de estados de aplicaciones
description: Los estados de la aplicación son las diferentes pantallas o vistas de su aplicación. Obtenga información sobre cómo rastrear el estado de la aplicación en la aplicación mediante la llamada trackState.
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/fVNQ4CIqXbSYyi32rBlB2B9S6YTsBwxJhD3XaeDcDIE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 188
ht-degree: 100%

---

# Seguimiento de estados de aplicaciones{#track-app-states}

Los estados son las distintas pantallas o vistas de su aplicación. Cada vez que se muestra un nuevo estado en la aplicación, debe enviar una llamada `trackState`. Por ejemplo, cuando un usuario navega de la página principal a la pantalla de detalles del vídeo, envía una llamada `trackState`. Los estados suelen verse mediante un informe de ruta, y así se puede ver cuántos usuarios navegan por la aplicación y qué estados se ven más.

## llamadas trackState

Normalmente, llama `trackState` cada vez que la aplicación carga una nueva pantalla.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

El nombre del estado se recoge en la variable “Ver estado” de Adobe Mobile Services y se registra una vista para cada llamada `trackState`. En otras interfaces de Analytics, “Ver estado” aparece como “Nombre de página” y “Vistas de estado” aparece como “Vistas de página”.

## Enviar datos de contexto

Además del “Nombre de estado”, puede enviar datos de contexto adicionales con cada llamada de seguimiento de estado.

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Chromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>El valor de los datos de contexto debe asignarse a variables personalizadas de Adobe Mobile Services.
