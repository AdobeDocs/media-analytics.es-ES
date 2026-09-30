---
title: Versión de aplicación
description: Informa de la versión de la aplicación de reproducción de contenido utilizada en cada sesión de flujo continuo.
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
source-wordcount: '252'
ht-degree: 4%
---

# Versión de aplicación

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Versión de la aplicación**. Consulte [Versión de aplicación](/help/implementation/variables/core/app-version.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Versión de la aplicación** indica la cadena de versión de la aplicación del reproductor de medios configurada durante la inicialización de SDK. Utilícelo para identificar qué versiones del reproductor están en uso activo, correlacionar los cambios de calidad o comportamiento con versiones específicas y priorizar la compatibilidad con versiones ampliamente utilizadas.

>[!NOTE]
>
>Esta dimensión captura la versión de su **aplicación de reproducción multimedia**, no la biblioteca SDK de Adobe. La versión de la biblioteca SDK de Adobe se recopila automáticamente como un campo interno independiente.

## Cómo se rellena esta dimensión

La versión de la aplicación se establece una vez al inicializar SDK y se incluye automáticamente en cada solicitud de inicio de sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente mediante la asignación de campos XDM al utilizar implementaciones de Edge. Para implementaciones solo de Analytics, asigne los datos de contexto `media.sdkVersion` a un eVar personalizado mediante una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.md). |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.appVersion`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | No hay ninguna columna de fuente de datos dedicada. Para implementaciones solo de Analytics, utilice la columna de fuente de datos del eVar personalizado configurado mediante una regla de procesamiento. |
| Audience Manager | `c_contextdata.media.sdkVersion` (implementaciones solo de Analytics) |

## Elementos de dimensión

Cada elemento es la cadena de versión literal configurada en la inicialización de SDK. Utilice un esquema de versiones coherente en todas las implementaciones de modo que las cadenas de versión se acumulen de forma predecible en los informes.
