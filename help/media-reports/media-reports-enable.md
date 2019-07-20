---
seo-title: Habilitación de informes de medios
title: Habilitación de informes de medios
uuid: d 306068 d-a 308-4 b 6 e -8 a 72-742 dda 0 de 428
translation-type: tm+mt
source-git-commit: 3fed0736b673d024b7a4b07d8324bfc62f747ed7

---


# Habilitación de informes de medios{#media-reports-enablement}

Cada grupo de informes que recopile métricas de medios debe configurarse antes de que se envíen los datos de medios.

>[!TIP]
>
>Para aprovechar las nuevas capacidades, los actuales clientes de Media Analytics deben volver a habilitar el seguimiento de medios para sus RSID.

1. In [Reports &amp; Analytics](https://my.omniture.com/login/) click [!UICONTROL Admin] &gt; [!UICONTROL Report Suites].
1. Select the report suite(s) where you are collecting media data and click [!UICONTROL Edit Settings] &gt; [!UICONTROL Media Management] &gt; [!UICONTROL Media Reporting].
   ![](assets/media-reporting.png){width = "400 px"}

1. On the **[!UICONTROL Media Reporting]** page, enable **[!UICONTROL Media Core]**, and optionally enable **[!UICONTROL Media Ads]**, **[!UICONTROL Media Chapters]**, and **[!UICONTROL Media Quality]**.

   La medición de medios incluye los siguientes módulos:

   * **Componentes básicos de medios:**

      La medición de medios principales se utiliza para contenido multimedia. Esto usará evars de solución (o personalizadas) para rastrear el contenido, el tipo de contenido, el nombre del reproductor de contenido y el canal de contenido. Los eventos de solución (o personalizados) se utilizarán para los inicios de medios, los inicios de contenido, las finalizaciones de contenido y el tiempo invertido en contenido.

   * **Publicidades de medios:** La medición de publicidad de medios se utiliza para medir anuncios dentro del contenido multimedia. Se utilizará el conmutador de soluciones eVars para medir la publicidad, el nombre del reproductor de publicidad, el pod de anuncios y la publicidad en la posición del pod. Se utilizarán eventos de solución para inicios de anuncios, finalización de anuncios, tiempo invertido en publicidad y tiempo de vídeo transcurrido.
   * **Capítulos multimedia:**

      La medición de capítulos de vídeo se utiliza para medir capítulos. Un capítulo es una subdivisión de contenido dentro de un solo medio. Se utilizará una eVar de solución para almacenar el ID del capítulo. Se utilizarán eventos de solución para el inicio de capítulos, la finalización de capítulos y el tiempo del capítulo consumido. Los metadatos adicionales del nombre del capítulo y de posición se proporcionarán como clasificaciones del ID del capítulo.

   * **Calidad multimedia:**

      La medición de calidad de vídeo se utiliza para medir la calidad de la reproducción del contenido. Se utilizarán eVars de solución para almacenar el tiempo de inicio, eventos de búfer, duración total del almacenamiento en búfer, cambios en la velocidad de bits, velocidad de bits media, errores y fotogramas perdidos. Los eventos de solución se utilizarán para el momento del inicio, fotogramas perdidos antes del inicio, emisiones afectadas por búfer, eventos de búfer, duración total del almacenamiento en búfer, emisiones afectadas por cambios de velocidad de bits, cambios en la velocidad de bits, velocidad de bits media, Emisiones afectadas por fotogramas perdidos y fotogramas perdidos.

   * **Metadatos de vídeo y anuncios de vídeo:**

      Los metadatos se pueden adjuntar a un medio o una publicidad para describir y categorizar más ese medio o anuncio. Los metadatos estandarizados y los metadatos de anuncios se recopilarán mediante variables y clasificaciones de soluciones. Los valores incluyen: Programa, Temporada, Episodio, ID de recurso, Género, Fecha de primera publicación, Fecha del primer uso digital, Valoración del contenido, Creador, Red, Tipo de programa, Cargas publicitarias, MVPD, Con autorización, Partición de días, ID de sesión de medio, Anunciante, ID de campaña e ID creativo.

   * **Metadatos de anuncios de audio y audio:**

      Los metadatos se pueden adjuntar al audio o anuncio para describirlo o categorizarlo con más precisión. Los metadatos estandarizados de los anuncios y el audio se recopilan a través de las variables y las clasificaciones de la solución. Los valores disponibles son los siguientes: artista, álbum, discográfica, autor, editor, canal, programa, temporada, episodio, ID de activo, género, fecha de la primera emisión, fecha del primer uso digital, valoración del contenido, creador, tipo de programa, cargas del anuncio, plantilla de programación, ID de sesión de medio, anunciante, ID de campaña e ID de creativo.
   Al habilitar cada módulo, se reserva un conjunto de variables y se crea un nuevo conjunto de informes. A excepción de Calidad, no habrá datos en los informes a menos que se haya completado la implementación correspondiente. Al implementar el módulo Core, también se implementa el módulo Calidad si lo habilita.

   Si todavía no rastrea anuncios, capítulos o la calidad de la reproducción, puede habilitar opciones adicionales en cualquier momento.

1. Haga clic en **[!UICONTROL Guardar]**.

   If this report suite is already configured to collect media data, after you click **[!UICONTROL Save]**, an additional configuration page is displayed. Si ve la página [!UICONTROL Medición de Media Core], continúe con el siguiente paso.

1. (Condicional) En la página [!UICONTROL Medición de Media Core], elija continuar usando variables personalizadas o usar variables de solución.

   | Opción | Descripción |
   | --- | --- |
   | Continuar usando variables personalizadas | <ul> <li> **Profesionales:** las tendencias de medios siguen funcionando después de la migración. </li> <li> **Inconvenientes:** Requiere que mantenga dos evars personalizadas y tres eventos personalizados asignados a los medios. Recupera el uso de una eVar personalizada y un evento personalizado. </li> </ul> Para continuar usando variables personalizadas: <ol> <li>Seleccione Usar variables personalizadas y luego haga clic en Guardar. </li> <li>Cuando se le solicite, asigne sus eVars y eventos personalizados actuales y luego haga clic en Guardar: </li> </ol> |
   | Migrar a variables de solución | <ul> <li> **Profesionales:** se puede utilizar tres eVars personalizadas y cuatro eventos personalizados. </li> <li> **Desventajas:** pierde **todas** las tendencias y comparativas históricas para los informes de medios. Esto significa que no puede ver la tendencia de las visualizaciones de contenido ni el tiempo de contenido reproducido en cualquier fecha antes de realizar la migración a Heartbeat. </li> </ul> **Restricción:** no migre a las variables de solución a menos que esté seguro de que no desea conservar esta tendencia. Todos los clientes deben utilizar variables de solución y reglas de procesamiento para incluir datos de medios en las props y eVars existentes, solo si necesitan conservar la continuidad histórica. Para migrar a variables de solución: Seleccione Utilizar variables de solución y haga clic en Guardar. |

   >[!IMPORTANT]
   >
   >Migrating to solution variables causes you to lose **all** historical trending and comparison for media reports.

>[!IMPORTANT]
>
>Do not change the classification names for any variables listed in the Metrics and metadata tables (e.g., [Audio and video parameters](../metrics-and-metadata/audio-video-parameters.md)) that are described there under Reporting/Reserved Variable as "classification". Las clasificaciones de medios se definen cuando un grupo de informes está habilitado para el seguimiento de medios. Cada cierto tiempo, Adobe agrega nuevas propiedades y, cuando esto sucede, los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las nuevas propiedades de medios. Durante el proceso de actualización, Adobe determina si las clasificaciones están habilitadas marcando los nombres de las variables. Si falta alguno, Adobe agrega los que faltan.
