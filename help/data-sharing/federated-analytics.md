---
seo-title: Federated Analytics
title: Federated Analytics
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
translation-type: tm+mt
source-git-commit: 3ca6743e34d40e5826dbe50edcbec6aa77ef66f4

---


# Federated Analytics{#federated-analytics}

El servicio de Federated Analytics ofrece un sistema para compartir datos de Adobe Media Analytics (audio y vídeo) entre dos socios. Los datos estandarizados de medición creados por Media Analytics son la seña de identidad de Federated Analytics, y permiten que los datos aparezcan en un único informe de múltiples fuentes. A través de las reglas y lógica que rigen Federated Analytics, los datos se controlan y se personalizan para satisfacer las necesidades de cada sociedad. Federated Analytics hace que la medición de audio y vídeo sea más eficaz, ágil y procesable.

## Ventajas {#section_804FFE8671594A6FB769CBE79EF9D627}

* **Transparencia:** elimine la caja negra de la creación de datos utilizando la misma lógica en diferentes empresas.
* **Amplitud:** conozca el alcance completo y el impacto del consumo de audio y vídeo en distintas sociedades, plataformas y dispositivos.
* **Protección:** controle el uso compartido de datos en el servidor mediante reglas y lógica.
* **Estandarización:** hable el mismo idioma de datos que sus socios.
* **Procesamiento:** calcule los datos de audio y vídeo para monitorizar reproductores, tendencias y detectar anomalías con Adobe Analytics.
* **Centralización:** recopile datos de medición de audio y vídeo en una sola ubicación de Adobe.
* **Cumplimiento legal:** cumpla los requisitos de uso compartido de datos legales fácilmente.
* **Siempre a tiempo:** envío y recepción de datos en tiempo real.
* **Sencillez:** marque los reproductores solo una vez con los kits de desarrollo de software de Adobe y comparta los datos con varios socios

## Definiciones {#section_ypl_mb3_vbb}

* **Remitente:** el cliente que genera datos de análisis de audio y vídeo en sus reproductores.
* **Receptor:** el cliente que recibe los datos de análisis de audio y vídeo del remitente.

## Requisitos {#section_4758843A8941441B9A4D0D7A61077A6E}

* **Contrato de emisiones de medios:** el receptor y el remitente deben tener contratado Adobe Analytics para emisiones de medios para tener acceso a los datos de audio y vídeo en Adobe Analytics. Póngase en contacto con su equipo de cuentas para obtener más detalles.
* **Apéndice federado:** cada remitente y receptor deben tener un apéndice firmado con Adobe antes de enviar o recibir datos. Es necesario un apéndice por cliente, no por sociedad. Póngase en contacto con su equipo de cuentas para obtener más detalles.
* **Implementación de Media Analytics:** el remitente debe tener Media Analytics en todos los reproductores que formarán parte del conjunto de datos federados. Solo se pueden federar los datos de Media Analytics. See documentation: [Measuring audio and video in Adobe Analytics](/help/media-overview.md)

* **Contrato de consultoría de Adobe:** para la configuración inicial de reglas federadas entre el receptor y el remitente, es importante trabajar con los servicios de consultoría para revisar los datos y crear el acuerdo de uso compartido de datos.

## Download the Federated Analytics Form

**`===>`Descargue la versión actual del formulario aquí: Formulario**[ de acuerdo de reglas de](/assets/federated_analytics_form.pdf)federación. **`<===`**

## Proceso {#section_byb_kb3_vbb}

1. El remitente y el receptor colaboran para completar el formulario del acuerdo de reglas de federación. The Federated Rules Agreement form contains special fields for our engineering team and should ONLY be edited using Adobe Acrobat. [Descargue Acrobat de forma gratuita.](https://get.adobe.com/reader/)
1. Los servicios de consultoría proporcionan un archivo de datos de muestra al receptor con datos reales de reproductores del remitente para confirmar que se definen las reglas adecuadas de uso compartido de datos, siempre que haya archivos de datos disponibles.
1. El remitente y el receptor garantizan que el acuerdo de uso compartido de datos cumplirá todos los requisitos contractuales entre las dos partes.
1. Los servicios de consultoría enviarán el formulario completado a Adobe Engineering para definir las reglas de uso compartido de datos.
1. Los datos se comparten en el grupo de informes de desarrollo donde el receptor revisará y validará los datos.
1. Cuando el receptor confirme que los datos son correctos, Adobe Engineering actualizará las reglas para asignar un grupo de informes de producción.
1. El receptor revisará y validará los datos en el grupo de informes de producción.
1. Si en el futuro se hacen cambios en el conjunto de datos, el remitente o el receptor podrán solicitar asistencia del Servicio de atención al cliente.

