---
title: Configurar Adobe Debug
description: En este tema se describe cómo configurar Adobe Debug, que puede utilizar para solucionar problemas con las implementaciones de Media SDK.
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Configuración de Adobe Debug {#configure-adobe-debug}

## Acceso a Adobe Debug {#accessing-adobe-debug}

Para acceder a Adobe Debug:

1. Vaya a [Experience Cloud](https://www.marketing.adobe.com) y cree un nuevo usuario de Adobe Experience Cloud.

   >[!TIP]
   >
   >Este inicio de sesión no es el mismo nombre de usuario o contraseña que se utiliza para iniciar sesión en Adobe Analytics.

1. Una vez tenga una cuenta de Experience Cloud, póngase en contacto con su representante de Adobe para solicitar acceso a Adobe Debug.
1. Una vez concedido el acceso, vaya a [https://debug.adobe.com](https://debug.adobe.com) y utilice sus credenciales de Experience Cloud para iniciar sesión.

   ![](assets/adobe-debug-login.png)

   Los navegadores admitidos para esta herramienta son:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer versiones 9-11

Los navegadores recomendados son las versiones más recientes de Chrome y Firefox.

## Depurar proxy {#debug-proxy}

Descargar y configurar el proxy de depuración:

1. Descargue la aplicación proxy de depuración en [Descargas de aplicaciones.](https://debug.adobe.com/#/downloads)

   Los sistemas operativos compatibles son:
   * OS X 10.7 de 64 bits o superior
   * Windows 7.1 de 64 bits o superior
   ![](assets/debug-proxy-app.png)

1. El servidor proxy de depuración se ejecutará en el equipo local en el puerto 33284 y se establecerá como proxy del sistema.

   Es posible que necesite ajustar la configuración del navegador en función del sistema operativo y del navegador.

## Descargar e instalar el certificado SSL en el escritorio o las aplicaciones {#download-and-install-sSL-desktop}

La primera vez que ejecute Adobe Debug, se generará un certificado SSL único. Si su dispositivo de escritorio y/o aplicaciones funcionan con tráfico HTTPS, debe descargar e instalar el certificado SSL.

Descargue e instale el certificado SSL:

1. Después de instalar y iniciar Adobe Debug, vaya a [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) y descargue la certificación.
1. Importe el certificado

   **Mac OS**
   1. Haga doble clic en el certificado raíz de CA para abrirlo en Acceso a Llaveros.
   1. El certificado raíz de CA aparecerá en el inicio de sesión.
   1. Mueva (arrastre) el certificado raíz de CA al sistema.
   1. Debe copiar el certificado en el sistema para garantizar que es de confianza para todos los usuarios y los procesos del sistema local.
   1. Abra el certificado raíz de CA, expanda Confiar, seleccione Confiar siempre y guarde los cambios.
   **Windows**
   1. Realice uno de los siguientes procedimientos:

      * [Adición de certificados al almacén de Entidades de certificación raíz de confianza para un equipo local](https://technet.microsoft.com/es-es/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1. Para Firefox, complete el procedimiento de [Instalación del certificado raíz en Mozilla Firefox.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)
    
    Es posible que tenga que salir y volver a abrir Firefox para ver el cambio.
    
    **Dispositivos iOS**
    1. Configure su dispositivo iOS para que utilice Adobe Debug como proxy HTTP haciendo clic en **[!UICONTROL Configuración de la aplicación]** **&gt;** **[!UICONTROL Configuración de Wi-Fi]**.
    
    1. En Safari, vaya a [Debug.](https://proxy.debug.adobe.com/ssl)
    
    Safari le pedirá que instale el certificado SSL.

## Instalación del certificado SSL para su dispositivo móvil {#install-sSL-for-mobile-device}

Si no tiene las llamadas HTTPS en Adobe Debug, debe instalar el certificado SSL para Adobe Debug en el dispositivo móvil.

### iOS

Para instalar el certificado SSL en un dispositivo iOS:

1. En el equipo portátil, active el proxy de depuración y vaya a [Adobe Debug.](https://debug.adobe.com)
1. Siga estos pasos en su dispositivo iOS:
   1. Ponga el dispositivo en modo avión.
   1. Seleccione la misma señal Wi-Fi que utiliza el equipo portátil.
   1. En el equipo portátil, establezca manualmente la IP y el puerto que se muestran en la aplicación proxy de depuración.
   1. Abra una ventana de navegador de Apple Safari.
   1. Vaya a [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Descargue e instale el certificado SSL.

1. En el equipo portátil, inicie sesión en Adobe Debug.
1. Inicie la prueba en el dispositivo iOS.

### Android

Para instalar el certificado SSL en un dispositivo Android:

1. En su portátil, active Debug Proxy y vaya a [Adobe Debug.](https://debug.adobe.com)
1. Siga estos pasos en su dispositivo Android:
   1. Ponga el dispositivo en modo avión.
   1. Seleccione la misma señal Wi-Fi que utiliza el equipo portátil.
   1. En el equipo portátil, establezca manualmente la IP y el puerto que se muestran en la aplicación proxy de depuración.
   1. Abra una ventana del navegador.
   1. Vaya a [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Descargue e instale el certificado SSL.

1. En el equipo portátil, inicie sesión en Adobe Debug.
1. Inicie la prueba en el dispositivo Android.

