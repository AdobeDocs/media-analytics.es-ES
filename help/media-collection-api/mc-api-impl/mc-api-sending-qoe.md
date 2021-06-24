---
title: Envío de datos de la nube
description: Obtenga información sobre el envío de eventos con una clave qoeData JSON.
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '57'
ht-degree: 84%

---

# Envío de datos de QoE{#sending-qoe-data}

Cada evento puede estar acompañado por una clave JSON adicional denominada `qoeData`, que se coloca junto a la clave `params` en el cuerpo de la solicitud JSON.

>[!NOTE]
>
>Debe comprobar los [esquemas de validación de JSON](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md) para verificar los tipos de parámetros y si estos son obligatorios o opcionales.
