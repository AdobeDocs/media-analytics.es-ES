---
title: Medios federados
description: El servicio Federated Media proporciona un sistema para compartir datos de medios de streaming entre dos socios.
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
exl-id: 81970370-663c-49d5-b13c-628d294be178
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 61%

---

# Medios federados{#federated-media}

El servicio Federated Media proporciona un sistema para compartir datos de medios de streaming (audio y vídeo) entre dos socios.
Los datos estandarizados de medición creados por la recopilación de medios de streaming son la seña de identidad de Federated Media, ya que permiten que los mismos datos fluyan en un único informe de múltiples fuentes.
A través de las reglas y la lógica que rigen Federated Media, los datos se controlan y se personalizan para satisfacer las necesidades de cada sociedad.
Federated Media hace que la medición de audio y vídeo sea más eficiente, ágil y procesable.


![](assets/media-federated.png)

## Beneficios {#benefits}

* **Transparencia:** Elimine la caja negra de la creación de datos utilizando la misma lógica en todas las compañías
* **Amplitud:** Comprenda el alcance y el impacto totales del consumo de audio y vídeo en asociaciones, plataformas y dispositivos
* **Seguridad:** Controle el uso compartido de datos del lado del servidor mediante reglas y lógicas
* **Estandarización:** Hable el mismo idioma de datos que sus socios
* **Útil:** Cuantifique los datos de audio y vídeo para comparar reproductores, monitorizar tendencias y detectar anomalías a través de Adobe Analytics
* **Gestión centralizada:** Recopilación de datos de medición de audio y vídeo en una ubicación de Adobe
* **Contractual:** Puede cumplir con los requisitos legales de uso compartido de datos
* **Siempre a tiempo:** Envíe y reciba datos en tiempo casi real
* **Fácil:** Etiquete reproductores solo una vez con los SDK de Adobe, comparta datos con muchos socios

## Definiciones {#definitions}

* **Remitente:** Generación por parte del cliente de datos de análisis de audio y vídeo en reproductores propios
* **Receptor:** Cliente que recibe datos de análisis de audio y vídeo del remitente

## Requisitos {#requirements}

* **Contrato de emisiones de contenidos:** el receptor y el remitente deben tener contratado Adobe Analytics para emisiones de contenidos para tener acceso a los datos de audio y vídeo en Adobe Analytics. Póngase en contacto con el equipo de su cuenta para obtener más detalles.
* **Anexo federado:** Cada remitente y receptor debe tener un anexo firmado con Adobe antes de enviar o recibir datos. Se requiere un anexo por cliente, no uno por sociedad. Póngase en contacto con el equipo de su cuenta para obtener más detalles.

* **Implementación de recopilación de medios de transmisión:** El remitente debe tener implementada la recopilación de medios de transmisión en todos los reproductores que formarán parte del conjunto de datos federado. Solo los datos de medios de streaming están disponibles para la federación. Para obtener más información, consulte [Información general sobre la recopilación de medios de streaming de Adobe](/help/media-overview.md).

* **Contrato de consultoría de Adobe:** para la configuración inicial de reglas federadas entre el receptor y el remitente, es importante trabajar con los servicios de consultoría para revisar los datos y crear el acuerdo de uso compartido de datos.

## Descargar el formulario de medios federados

Para participar en Federated Media, descargue y complete el formulario [Acuerdo de reglas de federación](assets/federated_analytics_form.pdf).

## Proceso {#process}

1. El remitente y el receptor colaboran para completar el formulario del acuerdo de reglas de federación. El formulario de acuerdo de reglas de federación contiene campos especiales para el equipo de ingeniería y SOLO debe editarse mediante el uso de Adobe Acrobat. [Descargue Acrobat de forma gratuita.](https://get.adobe.com/es/reader/)
1. Los servicios de consultoría proporcionan un archivo de datos de muestra al receptor con datos reales de los reproductores del remitente, para confirmar aún más que se han definido las reglas correctas de uso compartido de datos, siempre que haya archivos de datos disponibles.
1. El remitente y el receptor se aseguran de que el acuerdo de intercambio de datos cumpla todos los requisitos contractuales entre las dos partes.
1. Los servicios de consultoría envían el formulario completado a Adobe Engineering para configurar las reglas de uso compartido de datos.
1. Los datos se comparten con el grupo de informes de desarrollo de Adobe Analytics o el conjunto de datos de Adobe Experience Platform, donde el receptor revisará y validará los datos.
1. Una vez que el receptor confirma que los datos son correctos, Adobe Engineering actualiza las reglas para que indiquen un grupo de informes de producción de Analytics o un conjunto de datos de Adobe Experience Platform.
1. El receptor revisará y validará los datos en el grupo de informes de producción de Analytics o en el conjunto de datos de Adobe Experience Platform.
1. Si se producen cambios en el conjunto de datos en el futuro, el remitente o el receptor pueden enviar un ticket de atención al cliente para recibir asistencia.
