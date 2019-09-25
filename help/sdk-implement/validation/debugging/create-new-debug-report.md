---
seo-title: Creación de un nuevo informe de Debug
title: Creación de un nuevo informe de Debug
uuid: 438fde3d-98f9-46d1-9672-75d204361568
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

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
      * [!UICONTROL Default Endpoint] - The data in this field is provided by Adobe and cannot be changed.
      * [!UICONTROL Extremo] extra: agregue `CNAMES`, si los utiliza, para el servidor de seguimiento como `metrics.companyname.com`
   * **Latidos de vídeo (Media Analytics)**

      * [!UICONTROL Extremo] predeterminado: Adobe proporciona los datos de este campo y no se pueden cambiar.
      * [!UICONTROL Extra Endpoint - Add , if you use them, for your tracking server, e.g., .]`CNAMES``metrics.companyname.com`



