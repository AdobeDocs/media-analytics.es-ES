---
seo-title: Información general
title: Información general
uuid: d 71429 e 6-ef 8 b -4 ea 2-8491-ff 3 cdbf 4357 f
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Información general{#overview}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](../../sdk-implement/download-sdks.md)

## Implementación del seguimiento de errores

1. Rastree los errores del reproductor de medios.

   En los eventos de error, invoque `trackError` con la información del error.

>[!NOTE]
>
>El seguimiento de los errores del reproductor de medios no detendrá la sesión de seguimiento de medios. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

