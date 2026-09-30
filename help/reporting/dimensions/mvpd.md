---
title: MVPD
description: Informa del proveedor de cable, satélite o virtual a través del cual se autenticó el usuario.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%
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
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.pass.mvpd` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videomvpd`, `post_videomvpd` |
| Audience Manager | `c_contextdata.a.media.pass.mvpd` |

## Elementos de dimensión

Cada elemento es el nombre literal de MVPD registrado al inicio de la sesión. Utilice el identificador canónico de Adobe Pass MVPD por proveedor para que los datos se acumulen en un solo elemento de línea por proveedor.
