---
title: Habilitación de informes de contenidos
description: null
uuid: d306068d-a308-4b6e-8a72-742dda0de428
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Habilitación de informes de contenidos {#media-reports-enablement}

Para enviar datos sobre los contenidos, es necesario configurar todos los grupos de informes que recopilan métricas de contenidos.

>[!TIP]
>
>Para aprovechar las nuevas capacidades, los clientes de Media Analytics deben volver a habilitar el seguimiento de contenidos para sus RSID.

1. En [Reports &amp; Analytics](https://my.omniture.com/login/) haga clic en **[!UICONTROL Administración &gt; Grupos de informes].**
1. Seleccione los grupos de informes donde desee recopilar los datos de contenidos y haga clic en **[!UICONTROL Editar configuración &gt; Gestión de contenidos &gt; Informes de contenidos].**

   ![](assets/media-reporting.png){width="400px"}

1. En la página **[!UICONTROL Informes de contenidos]**, habilite **[!UICONTROL Componentes básicos de contenidos],** y, opcionalmente, también **[!UICONTROL Anuncios de contenidos],** **[!UICONTROL Capítulos de contenidos]** y **[!UICONTROL Calidad de contenidos].**

   La medición de contenidos incluye los siguientes módulos:

   * **Componentes básicos de contenidos**

      La medición de componentes básicos de contenidos se utiliza para el contenido multimedia. Esta usa eVars de solución (o personalizadas) para realizar un seguimiento del Contenido, el Tipo de contenido, el Nombre del reproductor de contenido y el Canal de contenido. Los eventos de solución (o personalizados) se utilizarán para contenidos iniciados, Contenido iniciado, Contenido finalizado y Tiempo invertido en contenido.

   * **Anuncios multimedia**

      La medición de anuncios de contenidos se usa para medir anuncios dentro del contenido de contenidos. Se utilizará el conmutador de soluciones eVars para medir la publicidad, el nombre del reproductor de publicidad, el pod de anuncios y la publicidad en la posición del pod. Se utilizarán eventos de solución para inicios de anuncios, finalización de anuncios, tiempo invertido en publicidad y tiempo de vídeo transcurrido.

   * **Capítulos multimedia**

      La medición de capítulos del vídeo se usa para medir capítulos. Un capítulo es una subdivisión de contenido dentro de los contenidos. Se utilizará una eVar de solución para almacenar el ID del capítulo. Se utilizarán eventos de solución para el inicio de capítulos, la finalización de capítulos y el tiempo del capítulo consumido. Los metadatos adicionales del nombre del capítulo y de posición se proporcionarán como clasificaciones del ID del capítulo.

   * **Calidad multimedia**

      La medición de la calidad del vídeo se utiliza para medir la calidad de la reproducción del contenido. Se utilizarán eVars de solución para almacenar el tiempo de inicio, eventos de búfer, duración total del almacenamiento en búfer, cambios en la velocidad de bits, velocidad de bits media, errores y fotogramas perdidos. Los eventos de solución se utilizarán para el momento del inicio, fotogramas perdidos antes del inicio, emisiones afectadas por búfer, eventos de búfer, duración total del almacenamiento en búfer, emisiones afectadas por cambios de velocidad de bits, cambios en la velocidad de bits, velocidad de bits media, Emisiones afectadas por fotogramas perdidos y fotogramas perdidos.

   * **Metadatos de vídeo y anuncios de vídeo**

      Se pueden adjuntar metadatos a un contenido o a un anuncio para describir y categorizar más ese contenido o anuncio. Los metadatos estandarizados de contenidos o de publicidad se recopilarán mediante variables y clasificaciones de soluciones. Los valores incluyen: Programa, Temporada, Episodio, ID de recurso, Género, Fecha de primera publicación, Fecha del primer uso digital, Valoración del contenido, Creador, Red, Tipo de programa, Cargas publicitarias, MVPD, Con autorización, Partición de días, ID de sesión de contenido, Anunciante, ID de campaña e ID creativo.

   * **Metadatos de anuncios de audio y audio**

      Los metadatos se pueden adjuntar al audio o anuncio para describirlo o categorizarlo con más precisión. Los metadatos estandarizados de los anuncios y el audio se recopilan a través de las variables y las clasificaciones de la solución. Los valores disponibles son los siguientes: artista, álbum, discográfica, autor, editor, canal, programa, temporada, episodio, ID de activo, género, fecha de la primera emisión, fecha del primer uso digital, valoración del contenido, creador, tipo de programa, cargas del anuncio, plantilla de programación, ID de sesión de contenido, anunciante, ID de campaña e ID de creativo.
   Al habilitar cada módulo, se reserva un conjunto de variables y se crea un nuevo conjunto de informes. A excepción de Calidad, no habrá datos en los informes a menos que se haya completado la implementación correspondiente. Al implementar el módulo Core, también se implementa el módulo Calidad si lo habilita.

   Si todavía no rastrea anuncios, capítulos o la calidad de la reproducción, puede habilitar opciones adicionales en cualquier momento.

1. Haga clic en **[!UICONTROL Guardar].**

   Si este grupo de informes ya está configurado para recopilar datos de contenidos, después de hacer clic en **[!UICONTROL Guardar]**, aparecerá una página de configuración adicional. Si ve la página **[!UICONTROL Medición de Componentes básicos de contenidos]**, continúe con el siguiente paso.

1. (Condicional) En la página **[!UICONTROL medición del Componentes básicos de contenidos]**, seleccione continuar usando las variables personalizadas o usar variables de solución.

   | Opción | Notas |
   | --- | --- |
   | Continuar usando variables personalizadas | Ventajas e inconvenientes:<ul> <li> **Profesionales:** las tendencias de contenidos siguen funcionando después de la migración. </li> <li> **Inconvenientes:** Requiere que mantenga dos eVars personalizadas y tres eventos personalizados asignados a contenidos. Recupera el uso de una eVar personalizada y un evento personalizado. </li> </ul> Para continuar usando variables personalizadas: <ol> <li>Seleccione **[!UICONTROL Usar variables personalizadas]** y luego haga clic en **[!UICONTROL Guardar]**. </li> <li>Cuando se le solicite, asigne sus eVars y eventos personalizados actuales y luego haga clic en **[!UICONTROL Guardar:]** </li> </ol> |
   | Migrar a variables de solución | Ventajas e inconvenientes:<ul> <li> **Profesionales:** se puede utilizar tres eVars personalizadas y cuatro eventos personalizados. </li> <li> **Desventajas:** pierde **todas** las tendencias y comparativas históricas para los informes de contenidos. Esto significa que no puede ver la tendencia de las visualizaciones de contenido ni el tiempo de contenido reproducido en cualquier fecha antes de realizar la migración a Heartbeat. </li> </ul> **Restricción:** no migre a las variables de solución a menos que esté seguro de que no desea conservar esta tendencia. Todos los clientes deben utilizar variables de solución y reglas de procesamiento para incluir datos de contenidos en las props y eVars existentes, solo si necesitan conservar la continuidad histórica. Para migrar a variables de solución: Seleccione **[!UICONTROL Usar variables de solución]** y haga clic en **[!UICONTROL Guardar].** <br><br> IMPORTANTE: La migración a las variables de solución hace que se pierdan **todas** las tendencias y comparativas históricas para los informes de contenidos. |

>[!IMPORTANT]
>
>No cambie los nombres de clasificación de ninguna variable enumerada en las tablas de métricas y metadatos (por ejemplo, [Parámetros de audio y vídeo](/help/metrics-and-metadata/audio-video-parameters.md)) que se describen en Informes/Variables reservadas como “clasificación”. Las clasificaciones de contenidos se definen cuando se habilita un grupo de informes para el seguimiento de contenidos. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede, los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las propiedades de los nuevos contenidos. Durante el proceso de actualización, Adobe determina si las clasificaciones están habilitadas mediante la comprobación de los nombres de las variables. Si falta alguno de ellos, Adobe agrega los que faltan de nuevo.
