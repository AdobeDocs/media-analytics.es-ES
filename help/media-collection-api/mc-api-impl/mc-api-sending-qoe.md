---
title: Envío de datos de QoE
description: Envío de datos de QoE
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 100%

---

# Envío de datos de QoE {#sending-qoe-data}

Cada evento puede estar acompañado por una clave JSON adicional denominada `qoeData`, que se coloca junto a la clave `params` en el cuerpo de la solicitud JSON.

>[!NOTE]
>
>Debe comprobar los [esquemas de validación de JSON](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md) para verificar los tipos de parámetros y si estos son obligatorios o opcionales.
