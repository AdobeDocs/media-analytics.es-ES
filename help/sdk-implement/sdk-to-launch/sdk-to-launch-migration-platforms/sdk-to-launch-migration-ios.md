---
seo-title: Migración del SDK de medios independiente a Adobe Launch - iOS
title: Migración del SDK de medios independiente a Adobe Launch - iOS
seo-description: Instrucciones y ejemplos de código para ayudarle a migrar del SDK de medios a Launch for iOS.
description: Instrucciones y ejemplos de código para ayudarle a migrar del SDK de medios a Launch for iOS.
translation-type: tm+mt
source-git-commit: b479f6623566b6a6989f625b757a97bba5f6aafd

---


# Migración del SDK de medios independiente a Adobe Launch - iOS

## Configuración

### Iniciar extensión

1. En Inicio de plataforma de experiencia, haga clic en la ficha [!UICONTROL Extensiones] de su propiedad móvil
1. En la ficha [!UICONTROL Catálogo] , ubique la extensión Adobe Media Analytics para audio y vídeo y haga clic en [!UICONTROL Instalar].
1. En la página de configuración de la extensión, configure los parámetros de seguimiento.
La extensión Media utilizará los parámetros configurados para el seguimiento.

[Configurar la extensión de Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

### SDK de medios independiente

En el SDK de medios independiente, puede configurar la configuración de seguimiento en la aplicación y pasarla al SDK cuando cree el rastreador.

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

## Creación de rastreadores

### Iniciar extensión

[Referencia de API de medios: Crear rastreador de medios](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

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
El rastreador selecciona automáticamente la configuración de la propiedad de inicio configurada.

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

### SDK de medios independiente

En el SDK de medios independiente, cree manualmente el objeto `ADBMediaHeartbeatConfig` y configure los parámetros de seguimiento. Implementar la interfaz delegada que expone los`getQoSObject()` y `getCurrentPlaybackTime()functions.`

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

## Actualización de los valores de cabeza lectora y calidad de experiencia.

### Iniciar extensión

La implementación debe actualizar el cursor de reproducción del reproductor actual mediante el método denominado`updateCurrentPlayhead` expuesto por el rastreador. Para un seguimiento preciso, debe llamar a este método al menos una vez por segundo.

[Referencia de la API de medios: Actualizar cabeza lectora actual](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

La implementación debe actualizar la información de QoE llamando al método expuesto por`updateQoEObject` el rastreador. Debe llamar a este método siempre que haya un cambio en las métricas de calidad.

[Referencia de API de medios - Actualizar objeto QoE](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

### SDK de medios independiente

En el SDK de medios independiente, se pasa un objeto delegado que implementa el`ADBMediaHeartbeartDelegate` protocolo durante la creación del rastreador.
La implementación debe devolver el último QoE y cursor de reproducción cada vez que el rastreador llame a los métodos `getQoSObject()` e interfacemática `getCurrentPlaybackTime()` .

## Transmisión de metadatos de anuncio/medios estándar

### Iniciar extensión

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

