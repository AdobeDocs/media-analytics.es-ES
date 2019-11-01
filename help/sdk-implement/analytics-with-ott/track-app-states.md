---
title: Seguimiento de estados de aplicaciones
description: 'Los estados de la aplicación son las diferentes pantallas o vistas de la aplicación, que cuando se muestran deben resultar en una llamada a trackState. '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Seguimiento de estados de aplicaciones{#track-app-states}

Los estados son las distintas pantallas o vistas de su aplicación. Cada vez que se muestra un nuevo estado en la aplicación, debe enviar una `trackState` llamada. Por ejemplo, cuando un usuario navega de la página principal a la pantalla de detalles del vídeo, envía una `trackState` llamada. Los estados suelen verse mediante un informe de ruta, y así se puede ver cuántos usuarios navegan por la aplicación y qué estados se ven más.

## Llamadas trackState

Normalmente, llama `trackState` cada vez que la aplicación carga una nueva pantalla.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. En otras interfaces de Analytics, "Ver estado" se notifica como "Nombre de página"; "Vistas de estado" se informa como "Vistas de página".

## Enviar datos de contexto

Además de "Nombre de estado", puede enviar datos de contexto adicionales con cada llamada de estado de seguimiento.

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

