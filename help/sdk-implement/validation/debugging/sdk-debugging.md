---
title: Depuración de SDK
description: En este tema se describe el seguimiento/registro disponible en el SDK de medios.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Depuración de SDK{#sdk-debugging}

Puede habilitar y deshabilitar el registro. El SDK de medios proporciona un amplio mecanismo de seguimiento/registro en toda la pila de seguimiento de medios. You can enable or disable logging by setting the `debugLogging` flag on the Config object.

## Código de muestra para el registro de depuración

### Android

```java
// Media Heartbeat initialization 
MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
config.debugLogging = true; 

// Use this space for setting other config values 
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config); 
```

### iOS

```
// Media Heartbeat Initialization 
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
config.debugLogging = YES; 

// Use this space for setting other config values 
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
```

### JavaScript

```js
// Media Heartbeat initialization 
var mediaConfig = new MediaHeartbeatConfig(); 
mediaConfig.debugLogging = true; 
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
```

### OTT (Chromecast, Roku)

La biblioteca ADBMobile proporciona un registro de depuración a través del método `setDebugLogging`. El registro de depuración se debe establecer en `false` para todas las aplicaciones de producción.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Uso de Adobe Bloodhound para probar aplicaciones Chromecast

Durante el desarrollo de la aplicación, Bloodhound permite ver llamadas de servidor localmente y permite la opción reenviar los datos a los servidores de recopilación de Adobe. Para obtener más información acerca de Bloodhound, consulte las siguientes guías:

* [Bloodhound 3.x para Mac](https://marketing.adobe.com/resources/help/en_US/mobile/bloodhound/)
* [Bloodhound 2.2 para Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)

>[!IMPORTANT]
>
>Adobe Bloodhound expiró el 30 de abril de 2017. Desde el 1 de mayo de 2017 no se proporcionarán nuevas mejoras ni se ofrecerá más soporte técnico de ingeniería o Adobe Expert Care.

## Mensajes de registro

Los mensajes de registro siguen este formato:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp:** es la hora CPU actual (según el huso horario GMT)
* **level:** existen 4 niveles de mensaje definidos:
   * INFO: Por lo general son los datos de entrada de la aplicación (validar nombre del reproductor, ID de vídeo, etc.)
   * DEBUG: registros de depuración que usan los desarrolladores para depurar problemas más complejos
   * WARN: Indica posibles errores de integración o configuración, o errores de SDK de Heartbeats
   * ERROR: Indica errores de integración importantes o errores de SDK de Heartbeats
* **tag:** el nombre del subcomponente que generó el mensaje de registro (suele ser el nombre de la clase)
* **message:** el mensaje de rastreo

Puede utilizar el resultado de los registros de la biblioteca del SDK de medios para comprobar la implementación. Una buena estrategia es buscar en los registros la cadena `#track`. This will highlight all the `track*()` calls made by your application.

For instance, this is what the logs filtered for `#track` could look like:

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad() 
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart() 
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay() 
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart() 
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart() 
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete() 
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart() 
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause() 
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete() 
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```

