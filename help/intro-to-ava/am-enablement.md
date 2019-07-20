---
seo-title: Habilitación de Audience Manager
title: Habilitación de Audience Manager
uuid: 8 a 7 f 9343-ebc 3-4087-9 d 7 e -5972640 d 2455
translation-type: tm+mt
source-git-commit: 8ae15f1e14731a97d212ab66816a777b4dcc897e

---


# Habilitación de Audience Manager{#audience-manager-enablement}

Adobe Audience Manager (AAM), una plataforma de gestión de datos (DMP), le ayuda a agrupar los activos de datos de audiencia, lo cual facilita la recopilación de información relevante para el comercio acerca de los visitantes del sitio, la creación de segmentos comercializables y el envío de contenido y publicidad a la audiencia adecuada.

Con AAM, no está ligado a un proveedor de datos, un intercambio o una plataforma de demanda. Además, AAM no trata con los recursos de datos de sus socios. Gracias al acceso a múltiples fuentes de datos, AAM ofrece a los editores digitales la capacidad de utilizar una amplia variedad de datos de terceros y nuestros datos privados. To learn more about AAM, see the AAM documentation [Audience Manager Product Documentation.](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html)

**Transferencia de datos de VA a AAM**: las métricas y los metadatos recopilados mediante las variables de solución (reservadas) se pueden enviar automáticamente a AAM tanto para el contenido de vídeo como para las publicidades de vídeo. La transferencia de datos está disponible en todas las plataformas, entre las que se incluyen escritorio, móvil y OTT. Para activar esta transferencia de datos desde el servidor, debe acceder al servicio de atención al cliente de Adobe y solicitar su habilitación.

>[!IMPORTANT]
>
>Para garantizar la transferencia suave de datos a AAM, debe estar en las versiones más recientes de las bibliotecas de SDK de medios.

Los datos federados admiten totalmente el uso compartido de datos en AAM. Colabore con su equipo de Adobe para confirmar la configuración de los datos federados.

## Métodos OTT/AAM {#section_yqq_5br_v2b}

Puede utilizar estos métodos para enviar señales y recuperar segmentos de visitantes de Audience Manager:

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   Devuelve el perfil del visitante que se haya obtenido más recientemente. Devuelve un objeto vacío si aún no se ha enviado una señal.

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   Devuelve el perfil del visitante que se haya obtenido más recientemente. Devuelve un objeto vacío si aún no se ha enviado una señal.

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   Devuelve el DPUUID actual.

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   Establece el DPID y el DPUUID. Si DPID y DPUUID se han establecido, se envían con cada señal.

   ```js
   ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   Envía una señal con rasgos a la gestión de público.

   ```js
   ADBMobile.audienceManager.SubmitSignal();
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   Devuelve el perfil del visitante que se haya obtenido más recientemente. Devuelve un objeto vacío si aún no se ha enviado una señal.

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   Devuelve el perfil del visitante que se haya obtenido más recientemente. Devuelve un objeto vacío si aún no se ha enviado una señal.

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   Devuelve el DPUUID actual.

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   Establece el DPID y el DPUUID. Si DPID y DPUUID se han establecido, se envían con cada señal.

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   Envía una señal con rasgos a la gestión de público.

   ```js
   ADBMobile().audienceSubmitSignal()
   ```

