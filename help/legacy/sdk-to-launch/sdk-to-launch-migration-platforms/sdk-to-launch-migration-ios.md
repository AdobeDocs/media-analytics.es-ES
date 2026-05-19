---
title: 'Migración de Media SDK independiente a Adobe Launch: iOS'
description: Obtenga información acerca de cómo migrar del SDK de medios a Launch para iOS.
exl-id: f70b8e1b-cb9f-4230-86b2-171bdaed4615
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/drdnQd83UXJkMKj-isUKPeIHe9xGetwY31HzHf37IEo
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 429
ht-degree: 60%

---

# Migración del SDK de medios independiente a Adobe Launch: iOS

>[!NOTE]
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=es) para obtener una referencia consolidada de los cambios terminológicos.

## Configuración

### SDK de medios independiente

En Media SDK independiente se establece la configuración de seguimiento en la aplicación,
y pasarlo al SDK cuando cree el rastreador.

```objective-c
ADBMediaHeartbeatConfig *config =
  [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"v2.0.0";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### Extensión de Launch

1. En Experience Platform Launch, haga clic en la pestaña [!UICONTROL Extensiones] de su propiedad móvil
1. En la pestaña [!UICONTROL Catálogo], busque la extensión Adobe Media Analytics para audio y vídeo y haga clic en [!UICONTROL Instalar].
1. En la página de configuración de la extensión, configure los parámetros de seguimiento.
La extensión de medios utilizará los parámetros configurados para el seguimiento.

   ![](assets/launch_config_mobile.png)

[Configurar la extensión de Media Analytics](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

## Creación de rastreadores

### SDK de medios independiente

En Media SDK independiente, cree manualmente el objeto `ADBMediaHeartbeatConfig`
y configure los parámetros de seguimiento. Implementar la interfaz delegada que expone el
`getQoSObject()` y `getCurrentPlaybackTime()functions.`

Cree una instancia de MediaHeartbeat para el seguimiento:

```objective-c
@interface PlayerDelegate : NSObject<ADBMediaHeartbeatDelegate>
@end

@implementation PlayerDelegate {
}

- (NSTimeInterval) getCurrentPlaybackTime {
    // When called should return the current player time in seconds.
    return playhead_;
}

- (nonnull ADBMediaObject*) getQoSObject {
    // When called should return the latest qos values.
    return qosObject_;
}
@end

ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"app-version";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;
ADBMediaHeartbeatDelegate* delegate = [[PlayerDelegate alloc] init];

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:delegate config:config];
```

### Extensión de Launch

[Referencia de API de medios: Crear un rastreador de medios](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createtracker)

Antes de crear el rastreador, registre la extensión multimedia y las extensiones dependientes con el núcleo móvil.

```objective-c
// Register the extension once during app launch
#import <ACPCore.h>
#import <ACPAnalytics.h>
#import <ACPMedia.h>
#import <ACPIdentity.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"your-launch-app-id"];
    [ACPMedia registerExtension];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    [ACPCore start:nil];
    return YES;
}
```

Una vez registrada la extensión de medios, se puede crear el rastreador con la siguiente API.
El rastreador selecciona automáticamente la configuración de la propiedad configurada de Launch.

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

## Actualización de los valores de experiencia del cabezal de reproducción y de la calidad.

### SDK de medios independiente

En Media SDK independiente, un objeto delegado que implementa la variable
Se pasó el protocolo `ADBMediaHeartbeartDelegate` durante la creación del rastreador.
La implementación debe devolver el último QoE y cabezal de reproducción cada vez que se ejecute el
el rastreador llama a la interfaz `getQoSObject()` y `getCurrentPlaybackTime()`
métodos.

### Extensión de Launch

La implementación debe actualizar el cabezal de reproducción actual mediante el nombre
El rastreador expuso el método `updateCurrentPlayhead`. Para un seguimiento preciso
debe llamar a este método al menos una vez por segundo.

[Referencia de API de medios: Actualizar cabezal de reproducción actual](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#updatecurrentplayhead)

La implementación debe actualizar la información de QoE llamando a la función
El rastreador expuso el método `updateQoEObject`. Debe llamar a este método
siempre que haya un cambio en las métricas de calidad.

[Referencia de API de medios: Actualizar objeto de QoE](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createqoeobject)

## Transmisión de metadatos estándar/metadatos publicitarios

### SDK de medios independiente

* Metadatos de medios estándar:

  ```objective-c
  ADBMediaObject *mediaObject =
    [ADBMediaHeartbeat createMediaObjectWithName:@"media-name"
                       mediaId:@"media-id"
                       length:60
                       streamType:ADBMediaHeartbeatStreamTypeVod
                       mediaType:ADBMediaTypeVideo];
  
  // Standard metadata keys provided by adobe.
  NSMutableDictionary *standardMetadata = [[NSMutableDictionary alloc] init];
  [standardMetadata setObject:@"Sample show" forKey:ADBVideoMetadataKeySHOW];
  [standardMetadata setObject:@"Sample season" forKey:ADBVideoMetadataKeySEASON];
  [mediaObject setValue:standardMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
  
  //Attaching custom metadata
  NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
  [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
  [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
  
  [tracker trackSessionStart:mediaObject data:mediaMetadata];
  ```

* Metadatos de anuncio estándar:

  ```objective-c
  ADBMediaObject* adObject =
    [ADBMediaHeartbeat createAdObjectWithName:[adData objectForKey:@"name"]
                       adId:[adData objectForKey:@"id"]
                       position:[[adData objectForKey:@"position"] doubleValue]
                       length:[[adData objectForKey:@"length"] doubleValue]];
  
  // Standard metadata keys provided by adobe.
  NSMutableDictionary *standardMetadata =
    [[NSMutableDictionary alloc] init];
  [standardMetadata setObject:@"Sample Advertiser"
                    forKey:ADBAdMetadataKeyADVERTISER];
  [standardMetadata setObject:@"Sample Campaign"
                    forKey:ADBAdMetadataKeyCAMPAIGN_ID];
  [adObject setValue:standardMetadata
                    forKey:ADBMediaObjectKeyStandardAdMetadata];
  
  //Attaching custom metadata
  NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
  [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
  
  [tracker trackEvent:ADBMediaHeartbeatEventAdStart
           mediaObject:adObject
           data:adDictionary];
  ```

### Extensión de Launch

* Metadatos de medios estándar:

  ```objective-c
  NSDictionary *mediaObject =
    [ACPMedia createMediaObjectWithName:@"media-name"
              mediaId:@"media-id"
              length:60
              streamType:ACPMediaStreamTypeVod
              mediaType:ACPMediaTypeVideo];
  
  NSMutableDictionary *mediaMetadata =
    [[NSMutableDictionary alloc] init];
  
  // Standard metadata keys provided by adobe.
  [mediaMetadata setObject:@"Sample show" forKey:ACPVideoMetadataKeyShow];
  [mediaMetadata setObject:@"Sample season" forKey:ACPVideoMetadataKeySeason];
  
  // Custom metadata keys
  [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
  [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
  [_tracker trackSessionStart:mediaObject data:mediaMetadata];
  ```

* Metadatos de anuncio estándar:

  ```objective-c
  NSDictionary* adObject =
    [ACPMedia createAdObjectWithName:@"ad-name"
              adId:@"ad-id"
              position:1
              length:15];
  
  NSMutableDictionary* adMetadata =
    [[NSMutableDictionary alloc] init];
  
  // Standard metadata keys provided by adobe.
  [adMetadata setObject:@"Sample Advertiser" forKey:ACPAdMetadataKeyAdvertiser];
  [adMetadata setObject:@"Sample Campaign" forKey:ACPAdMetadataKeyCampaignId];
  
  // Custom metadata keys
  [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];
  
  [tracker trackEvent:ACPMediaEventAdStart mediaObject:adObject data:adMetadata];
  ```
