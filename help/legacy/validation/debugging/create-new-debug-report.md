---
title: Crear un nuevo informe de Debug
description: Aprenda a crear un nuevo informe Debug.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 44%

---

# Crear un nuevo informe de Debug{#create-a-new-debug-report}

Para crear un nuevo informe de Debug:

1. En [!UICONTROL Crear nuevo informe de Debug], seleccione lo siguiente:

   ![](assets/create-new-debug-report.png)

1. Rellene los campos con la siguiente información:

   * **Asigne un nombre al informe**. Escriba el nombre y la fecha del reproductor para que pueda rastrear fácilmente al reproductor durante la certificación y mantener las marcas y las plataformas separadas.
   * **Adobe Analytics**

      * [!UICONTROL Nombre de usuario] y [!UICONTROL Secreto compartido]: estos campos son opcionales, pero puede agregar sus credenciales de API de servicios web a Adobe Debug para mostrar los nombres de las variables y la configuración de las variables para el grupo de informes.

        Puede acceder a de una de las siguientes maneras:

         * [!UICONTROL Analytics > Administración > Configuración de la empresa > Servicios web]
         * [!UICONTROL Analytics > Administración > Administración de usuarios > Usuarios > Configuración de usuario individual] Para crear una credencial de API de servicios web para un nuevo usuario, en [!UICONTROL Administración de usuarios], agregue el usuario al grupo de usuarios **Acceso a servicio web**.

      * [!UICONTROL Punto final por defecto]: Adobe proporciona los datos de este campo y no se pueden cambiar.
      * [!UICONTROL Punto final extra]: Añada `CNAMES` como servidor de seguimiento, si los usa, como `metrics.companyname.com`

   * **Video Heartbeats (Media Analytics)**

      * [!UICONTROL Punto final por defecto]: Adobe proporciona los datos de este campo y no se pueden cambiar.
      * [!UICONTROL Punto final extra]: Añada `CNAMES`, si los usa, para su servidor de seguimiento, es decir, `metrics.companyname.com`.
