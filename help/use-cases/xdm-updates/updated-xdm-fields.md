---
title: Actualizar una implementación de conector de origen de Analytics a nuevos campos XDM para los servicios de medios de streaming
description: Obtenga información acerca de la migración de una implementación de conector de origen de Analytics a campos de medios de streaming XDM actualizados
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: d239b203-71ce-4307-884f-9d11cc623d04
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Actualizar una implementación de conector de origen de Analytics a nuevos campos XDM para los servicios de medios de streaming

>[!NOTE]
>
>Esta información está destinada a organizaciones que utilizan el [conector de origen de Analytics](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/adobe-applications/analytics) para traer datos de medios de streaming de Adobe Analytics a Adobe Experience Platform para usarlos con los informes de Customer Journey Analytics o con cualquier otro servicio de Platform.
>
>Los cambios no afectan a Adobe Analytics como aplicación independiente, incluida la recopilación de datos, el procesamiento y la creación de informes. Las herramientas como Fuentes de datos y Reglas de procesamiento no se ven afectadas, por lo que no se requieren actualizaciones en la implementación de Analytics.

Ya está disponible una nueva implementación de recopilación de datos de Adobe (conector de origen de Analytics) para el servicio de medios de streaming que migra de un conjunto de campos XDM a otro.

## Nueva ruta de campo XDM

Como parte de esta migración, la ruta de campo XDM `mediaReporting` se añadió a los esquemas XDM utilizados en flujos de recopilación de datos de Adobe (conector de origen de Analytics). Cualquier esquema de recopilación de datos de Adobe existente y recién generado incluirá automáticamente este nuevo campo.

## Reemplazo de la ruta de campo XDM antigua

Todos los flujos de recopilación de datos de Adobe (conector de origen de Analytics) que transfieren datos de medios de streaming de Adobe Analytics a Adobe Experience Platform están enviando datos actualmente en la nueva ruta de campo XDM `mediaReporting` y en la antigua ruta de campo XDM `media.mediaTimed`. Ambas rutas de campo estarán disponibles durante tres meses, hasta finales de octubre de 2025. A partir de octubre, los campos `media.mediaTimed` quedarán totalmente obsoletos y los datos introducidos después de octubre solo incluirán `mediaReporting`. Después de la desuso, los campos `media.mediaTimed` dejarán de ser visibles en la interfaz de usuario del esquema de Adobe Experience Platform y se detendrá la ingesta de datos en estos campos. Por lo tanto, estos campos ya no estarán disponibles para su uso en ningún servicio de Adobe Experience Platform.

Los datos introducidos antes de esta fecha permanecerán disponibles para la creación de informes.

## Diferencias adicionales con la nueva ruta del campo XDM

Con la nueva implementación del conector de origen de Adobe para los medios de streaming, las llamadas de conexión persistente de Adobe Analytics ahora se incorporan en Adobe Experience Platform.

Anteriormente, estas llamadas no se reflejaban en aplicaciones de Platform como Customer Journey Analytics. Como resultado, su organización podría observar las siguientes diferencias en la creación de informes:

* **Recuentos precisos de sesiones**: En algunos casos, esto podría significar una deflación en los recuentos de sesiones, porque las llamadas de mantenimiento ayudan a mantener sesiones de usuarios activas incluso en ausencia de interacciones de medios directas. Estas llamadas de conexión persistente se generan cada 20 minutos después del último evento, por reproducción de contenido, con la intención de mantener la visita abierta. Para garantizar un seguimiento de sesión óptimo en Customer Journey Analytics, se recomienda configurar la caducidad de la visita a 30 minutos en la vista de datos.

* **Aumento en el número de eventos**: Debido a que las llamadas de conexión persistente ahora se cuentan en la métrica Eventos de Customer Journey Analytics. Si desea excluir las llamadas de conexión persistente de los informes, puede crear un filtro que excluya los eventos que tienen un tipo de evento de `media.keepalive`.

Este cambio garantiza una mayor alineación entre los informes de Analytics y CJA.

## Migre su configuración existente

Para garantizar una transición sin problemas, todos los clientes deben migrar las configuraciones existentes de `media.mediaTimed` campos a `mediaReporting` campos antes de finales de octubre de 2025. Las áreas afectadas son las que dependen del uso de `media.mediaTimed` y deben migrarse como se describe en las secciones siguientes.

### Customer Journey Analytics**

Los informes de CJA se pueden migrar de dos formas:

>[!NOTE]
>
>Después de elegir una de las siguientes opciones, debe reemplazar manualmente cada campo `media.mediaTimed` utilizado en los informes de Customer Journey Analytics con su campo derivado correspondiente o ruta del campo XDM de creación de informes.

* **Para conservar datos históricos**: los equipos de Adobe han desarrollado una plantilla predefinida de Customer Journey Analytics que introduce un conjunto de campos derivados que combinan los campos XDM antiguos y nuevos en un único campo. Esta plantilla se puede habilitar para cada conexión de Customer Journey Analytics si se solicita. Póngase en contacto con el equipo de soporte de Adobe para que le ayude a habilitar los nuevos campos. Estos campos derivados no se contabilizan en el límite de campos derivados de su organización.

  Para ver una lista de asignaciones, consulte [Asignación de parámetros de Media Analytics para Adobe Experience Platform y Customer Journey Analytics](/help/use-cases/xdm-updates/parameters-mapping.md).

* **Si no se requieren datos históricos**: es suficiente usar la ruta del campo XDM de creación de informes en el momento de la creación de informes. Para obtener más información, consulte [Migrar Customer Journey Analytics para usar los nuevos campos de medios de transmisión](/help/use-cases/xdm-updates/migrate-cja-setup.md).

### Real-Time CDP

Todas las audiencias y perfiles deben estar basados en `mediaReporting`. Para obtener más información, consulte [Migrar perfiles a los nuevos campos de medios de transmisión](/help/use-cases/xdm-updates/migrate-profiles.md).

### Flujo de datos y recopilación de datos

Las configuraciones dinámicas y la asignación de datos deben utilizar `mediaReporting`. Para obtener más información, consulte [Migrar preparación de datos para campos personalizados a los nuevos campos de medios de streaming](/help/use-cases/xdm-updates/migrate-dataprep.md).

### Otros servicios que deben migrarse

* Adobe Journey Optimizer: las configuraciones de campaña y recorrido deben incorporar `mediaReporting`.

* Reenvío de eventos: en las configuraciones solo se deben incluir `mediaReporting` campos.

* Servicios de consulta: las consultas deben hacer referencia a `mediaReporting` campos.

* Configuraciones de etiquetas: cualquier configuración de etiquetado debe hacer referencia a `mediaReporting` campos.

* Conexiones y destinos: los flujos de datos de importación y exportación deben estructurarse en torno a `mediaReporting` campos.

Tenga en cuenta que cualquier otro flujo que dependa de `media.mediaTimed` campos se ve afectado y requiere actualizaciones lógicas.

## Próximos pasos y asistencia

Todos los clientes que utilicen la recopilación de datos de Adobe para medios de streaming deben completar sus migraciones dentro del periodo de transición designado.

Si tiene alguna pregunta o necesita asistencia, no dude en ponerse en contacto con el equipo de asistencia de Adobe.
