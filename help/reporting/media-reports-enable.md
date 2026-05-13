---
title: Habilitación de informes de contenidos
description: Obtenga información acerca del grupo de informes multimedia que recopila métricas de medios.  Siga estos pasos para configurar los informes de medios antes de enviar los datos de medios.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/2nLLlF-rFJUR3t-OMbcy5iqF42l-O7oLybXFGhdPyhU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559id: e38cbddc-1633-4cd5-bed5-9f289f2a6029id: ef60b66e-5984-4336-ba72-6d978b1b6f87id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 945
ht-degree: 81%

---

# Habilitación de informes de contenidos{#media-reports-enablement}

Para enviar datos sobre los contenidos, es necesario configurar todos los grupos de informes que recopilan métricas de contenidos.

Los clientes avanzados solo pueden usar los paneles de medios en Analysis Workspace una vez que Media Core esté habilitado y el seguimiento esté habilitado para [Calidad de la experiencia](/help/use-cases/track-qos/track-qos-overview.md).

>[!TIP]
>
>Para aprovechar las nuevas funciones, los clientes de medios de streaming existentes deben volver a habilitar el seguimiento de medios para sus RSID.

1. En [Reports &amp; Analytics](https://my.omniture.com/login/) haga clic en **[!UICONTROL Administración > Grupos de informes].**
1. Seleccione los grupos de informes donde desee recopilar los datos de contenidos y haga clic en **[!UICONTROL Editar configuración > Gestión de contenidos > Informes de contenidos].**

   ![](assets/media-reporting.png)

1. En la página **[!UICONTROL Informes de contenidos]**, habilite **[!UICONTROL Componentes básicos de contenidos],** y, opcionalmente, también **[!UICONTROL Anuncios de contenidos],** **[!UICONTROL Capítulos de contenidos],** y **[!UICONTROL Calidad de contenidos].**

   La medición de contenidos incluye los siguientes módulos:

   * **Componentes básicos de contenidos**

     La medición de contenidos principales se utiliza para el contenido multimedia. Se utilizarán las eVars de solución (o personalizadas) para realizar un seguimiento del contenido, el tipo de contenido, el nombre del reproductor de contenido y el canal de contenido. Los eventos de solución (o personalizados) se utilizarán para contenidos iniciados, Contenido iniciado, Contenido finalizado y Tiempo invertido en contenido.

   * **Anuncios multimedia**

     La medición de anuncios de contenidos se usa para medir anuncios dentro del contenido de contenidos. Se usan las eVars de solución para medir la publicidad, el nombre del reproductor de publicidad, el pod de anuncios y la posición del anuncio en el pod. Los eventos de solución se utilizarán para Inicios de publicidad, finalizaciones de publicidad, tiempo invertido en publicidad y tiempo invertido en vídeo.

   * **Capítulos multimedia**

     La medición de capítulos del vídeo se usa para medir capítulos. Un capítulo es una subdivisión de contenido dentro de los contenidos. Se utilizará una eVar de solución para almacenar el ID del capítulo. Los eventos de solución se utilizarán para los Inicios de capítulo, las finalizaciones de capítulo y el tiempo invertido en el capítulo. Se proporcionarán metadatos de capítulo adicionales del nombre y la posición del capítulo como clasificaciones del ID del capítulo.

   * **Calidad multimedia**

     La medición de la calidad del vídeo se utiliza para medir la calidad de la reproducción del contenido. Se utilizarán las eVars de solución para almacenar el tiempo de Inicio, los Eventos de búfer, la duración total del búfer, los conmutadores de velocidad de bits, la velocidad de bits media, los errores y los fotogramas perdidos. Se utilizarán eventos de solución para el tiempo para el inicio, rechazos antes del inicio, flujos incrustados en el búfer, eventos de búfer, duración total del búfer, flujos incrustados en el cambio de tasa de bits, cambios de tasa de bits, tasa de bits media, flujos incrustados en error, eventos de error, flujos incrustados en fotogramas rechazados y fotogramas rechazados.

   * **Metadatos de vídeo y anuncios de vídeo**

     Se pueden adjuntar metadatos a un contenido o a un anuncio para describir y categorizar más ese contenido o anuncio. Los metadatos estandarizados de contenidos o de publicidad se recopilarán mediante variables y clasificaciones de soluciones. Los valores incluyen: Programa, Temporada, Episodio, ID de recurso, Género, Fecha de primera publicación, Fecha del primer uso digital, Valoración del contenido, Creador, Red, Tipo de programa, Cargas publicitarias, MVPD, Con autorización, Partición de días, ID de sesión de contenido, Anunciante, ID de campaña e ID creativo.

   * **Metadatos de anuncios de audio y audio**

     Se pueden adjuntar metadatos al audio o anuncio para describir y categorizar más ese audio o anuncio. Los metadatos estandarizados de audio y publicidad se recopilarán mediante variables y clasificaciones de soluciones. Los valores incluyen: artista, álbum, discográfica, autor, editor, canal, programa, temporada, episodio, ID de recurso, género, fecha de la primera publicación, fecha del primer uso digital, valoración del contenido, creador, tipo de programa, cargas del anuncio, plantilla de programación, ID de sesión de contenido, anunciante, ID de campaña e ID de Creative.

   Al habilitar cada módulo, se reserva un conjunto de variables y se crea un nuevo conjunto de informes. A excepción de Calidad, no habrá datos en los informes a menos que se haya completado la implementación correspondiente. La implementación del módulo Principal también implementa el módulo Calidad si lo habilita.

   Si todavía no está monitorizando anuncios, capítulos o la calidad de reproducción, puede habilitar opciones adicionales en cualquier momento.

1. Haga clic en **[!UICONTROL Guardar].**

   Si este grupo de informes ya está configurado para recopilar datos de contenidos, después de hacer clic en **[!UICONTROL Guardar]**, aparecerá una página de configuración adicional. Si ve la página **[!UICONTROL Medición de Componentes básicos de contenidos]**, continúe con el siguiente paso.

1. (Condicional) En la página **[!UICONTROL medición del Componentes básicos de contenidos]**, seleccione continuar usando las variables personalizadas o usar variables de solución.

   | Opción | Notas |
   | --- | --- |
   | Continuar usando variables personalizadas | Ventajas e inconvenientes:<ul> <li> **Profesionales:** las tendencias de contenidos siguen funcionando después de la migración. </li> <li> **Inconvenientes:** Requiere que mantenga dos eVars personalizadas y tres eventos personalizados asignados a contenidos. Recuperará el uso de una eVar personalizada y un evento personalizado. </li> </ul> Para seguir usando variables personalizadas: <ol> <li>Seleccione **[!UICONTROL Usar variables personalizadas]** y luego haga clic en **[!UICONTROL Guardar]**. </li> <li>Cuando se le solicite, asigne sus eVars y eventos personalizados actuales y luego haga clic en **[!UICONTROL Guardar:]** </li> </ol> |
   | Migrar a variables de solución | Ventajas e inconvenientes:<ul> <li> **Ventajas:** Recuperará el uso de tres eVars personalizadas y cuatro eventos personalizados. </li> <li> **Desventajas:** pierde **todas** las tendencias y comparativas históricas para los informes de contenidos. Esto significa que no puede aplicar tendencias a las vistas de contenido ni al tiempo de contenido reproducido para ninguna fecha antes de migrar a latidos. </li> </ul> **Restricción:** no migre a las variables de solución a menos que esté seguro de que no desea conservar esta tendencia. Todos los clientes deben utilizar variables de solución y reglas de procesamiento para incluir datos de contenidos en las props y eVars existentes, solo si necesitan conservar la continuidad histórica. Para migrar a variables de solución: Seleccione **[!UICONTROL Usar variables de solución]** y haga clic en **[!UICONTROL Guardar].** <br><br> IMPORTANTE: La migración a las variables de solución hace que se pierdan **todas** las tendencias y comparativas históricas para los informes multimedia. |

>[!IMPORTANT]
>
>No cambie los nombres de clasificación de ninguna variable enumerada en la documentación de variables de medios de streaming (enlazada desde la [descripción general de los servicios de medios de streaming](/help/media-overview.md)) que se describen en Informes/Variables reservadas como &quot;clasificación&quot;. Las clasificaciones de contenidos se definen cuando se habilita un grupo de informes para el seguimiento de contenidos. De vez en cuando, Adobe agrega nuevas propiedades y, cuando esto sucede, los clientes deben volver a habilitar sus grupos de informes para obtener acceso a las propiedades de los nuevos contenidos. Durante el proceso de actualización, Adobe determina si las clasificaciones están habilitadas mediante la comprobación de los nombres de las variables. Si falta alguno de ellos, Adobe agrega los que faltan de nuevo.
