---
title: Envío de datos de QoE
description: Más información sobre el envío de eventos con una clave qoeData JSON.
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 100%

---

# Envío de datos de QoE{#sending-qoe-data}

Cada evento puede estar acompañado por una clave JSON adicional denominada `qoeData`, que se coloca junto a la clave `params` en el cuerpo de la solicitud JSON.

>[!NOTE]
>
>Debe comprobar los [esquemas de validación de JSON](mc-api-validate-reqs.md) para verificar los tipos de parámetros y si estos son obligatorios o opcionales.
