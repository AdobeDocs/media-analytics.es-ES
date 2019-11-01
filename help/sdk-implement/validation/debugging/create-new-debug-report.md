---
title: Creación de un nuevo informe de Debug
description: En este tema se describe cómo crear un nuevo informe de depuración.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Creación de un nuevo informe de Debug{#create-a-new-debug-report}

Para crear un nuevo informe de Debug:

1. In [!UICONTROL Create New Debug Report] select the following:

   ![](assets/create-new-debug-report.png)

1. Complete los campos con la siguiente información:

   * **Asignar un nombre al informe**: Introduzca el nombre y la fecha del reproductor para poder realizar un seguimiento durante la certificación y mantener las marcas y plataformas por separado.
   * **Adobe Analytics**

      * [!UICONTROL Nombre de usuario] y [!UICONTROL Secreto compartido]: Estos campos son opcionales, pero puede agregar sus credenciales de API de servicios web a Adobe Debug para mostrar los nombres de las variables y las configuraciones de variables del grupo de informes.

         Puede acceder de las siguientes maneras:

         * [!UICONTROL Analytics &gt; Administrador &gt; Configuración de la empresa &gt; Servicios web]
         * [!UICONTROL Analytics &gt; Administrador &gt; Administración de usuarios &gt; Usuarios &gt; Configuración de usuario individual] Para crear una credencial de API de servicios web para un nuevo usuario, en [!UICONTROL Administración de usuarios], agregue el usuario al grupo de usuarios **Acceso al servicio web**.
      * [!UICONTROL Extremo] predeterminado: Adobe proporciona los datos de este campo y no se pueden cambiar.
      * [!UICONTROL Extremo] extra: agregue `CNAMES`, si los utiliza, para el servidor de seguimiento como `metrics.companyname.com`
   * **Latidos de vídeo (Media Analytics)**

      * [!UICONTROL Extremo] predeterminado: Adobe proporciona los datos de este campo y no se pueden cambiar.
      * [!UICONTROL Extremo] adicional: agregue `CNAMES`, si los utiliza, para el servidor de seguimiento, por ejemplo, `metrics.companyname.com`.



