---
title: MVPD
description: Informa del proveedor de cable, satélite o virtual a través del cual se autenticó el usuario.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 9%

---


# MVPD

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **MVPD**. Consulte [MVPD](/help/implementation/variables/standard-metadata/mvpd.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **MVPD** (distribuidor de programación de vídeo multicanal) informa del proveedor a través del cual el usuario se autenticó mediante Adobe Pass (por ejemplo, `"Comcast"` o `"DirecTV"`). Utilícelo para desglosar la participación del proveedor de autenticación.

## Cómo se rellena esta dimensión

El reproductor establece MVPD al principio de la sesión cuando el contenido se cierra detrás de Adobe Pass.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.pass.mvpd` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videomvpd`, `post_videomvpd` |
| Audience Manager | `c_contextdata.a.media.pass.mvpd` |

## Elementos de dimensión

Cada elemento es el nombre literal de MVPD registrado al inicio de la sesión. Utilice el identificador canónico de Adobe Pass MVPD por proveedor para que los datos se acumulen en un solo elemento de línea por proveedor.
