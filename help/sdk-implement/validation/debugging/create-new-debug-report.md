---
seo-title: Creación de un nuevo informe de Debug
title: Creación de un nuevo informe de Debug
uuid: 438 fde 3 d -98 f 9-46 d 1-9672-75 d 204361568
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

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
      * [!UICONTROL Extremo] predeterminado: los datos de este campo son proporcionados por Adobe y no se pueden cambiar.
      * [!UICONTROL Extremo adicional] - Agregar `CNAMES`, si los utiliza, para el servidor de seguimiento como `metrics.companyname.com`
   * **Latidos de medios**

      * [!UICONTROL Extremo] predeterminado: los datos de este campo son proporcionados por Adobe y no se pueden cambiar.
      * [!UICONTROL Extremo] adicional: agregue `CNAMES`, si los utiliza, para su servidor de seguimiento, por ejemplo `metrics.companyname.com`.



