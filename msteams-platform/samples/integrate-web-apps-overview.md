---
title: Integrar aplicaciones web
author: Rajeshwari-v
description: Una introducción a la integración de aplicaciones web y capacidades de dispositivo con Microsoft Teams aplicación.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: El selector de personas de power platform power apps vincula profundamente el recurso compartido con el asistente de agente virtual Teams
ms.openlocfilehash: 54f5345f44c35abbefabba642899a92d515e0aa2
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889219"
---
# <a name="integrate-web-apps"></a>Integrar aplicaciones web

Puede proporcionar una experiencia de usuario enriquecida integrando las características de una aplicación web existente en Microsoft Teams plataforma. Asegúrate de seguir [las Teams de diseño para](~/concepts/design/understand-use-cases.md) que tu aplicación sea nativa de Teams.
En este documento se proporciona información general sobre los requisitos previos para integrar aplicaciones web con Teams, power platform para crear aplicaciones de Power, Power Virtual Agents, Virtual Assistant, plantillas de aplicaciones, conectores de turnos, LMS de Moodle, creación de un botón compartir a Teams para el sitio web, agregar una pestaña Microsoft Teams en SharePoint, crear vínculos profundos e integrar las capacidades del dispositivo.

## <a name="prerequisites"></a>Requisitos previos   

Para una integración eficaz, asegúrese de comprender mejor los siguientes requisitos previos:
* Teams funcionalidades. 
* SharePoint requisitos de almacenamiento de archivos y datos.
* Requisitos de api.
* Autenticación.
* Vinculación profunda de la aplicación con Teams.
* Asigna los casos de uso de la aplicación a Teams funcionalidades de la plataforma.
* Determina los puntos de entrada de la aplicación, como el uso personal, la colaboración o ambos.

## <a name="low-code-platforms"></a>Plataformas de código bajo

Las plataformas de código bajos proporcionan un enfoque intuitivo para el desarrollo de software y requieren poca o ninguna codificación para crear aplicaciones y procesos. Puedes crear aplicaciones personalizadas fácilmente con plataformas de código bajo. Estas plataformas constan de una interfaz visual, conectores para servicios back-end y un sistema integrado de administración del ciclo de vida de aplicaciones para crear, depurar, implementar y mantener aplicaciones. Microsoft proporciona las siguientes puertas de enlace innovadoras para crear rápidamente aplicaciones compatibles Teams con atributos de código bajos:
* Plataforma de Microsoft Power
* Microsoft Teams de aplicación

## <a name="microsoft-power-platform"></a>Plataforma de Microsoft Power

La plataforma Microsoft Power combina cuatro tecnologías sólidas de Microsoft, como Power BI, Power Apps, Power Automate y Power Virtual Agents una plataforma de aplicaciones eficaz. Estas tecnologías le permiten crear soluciones, automatizar procesos, analizar datos y crear agentes virtuales en un entorno unificado e integrado.

### <a name="power-apps"></a>Power Apps

Con Power Apps, puede crear aplicaciones empresariales que se conecten a sus datos empresariales y se adapten a las necesidades de su organización. Power Apps una amplia variedad de escenarios de aplicaciones para resolver los desafíos empresariales a través de aplicaciones de lienzo. Después de crear la aplicación, puedes exportarla desde el portal Power Apps creador e insertarla en Microsoft Teams.

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent es una solución de interfaz gráfica guiada sin código. Se basa en Microsoft Power Platform y bot Framework. Permite a todos los miembros del equipo crear y mantener bots de chat conversacionales enriquecidos que se integran fácilmente con la Teams web. Puede diseñar, desarrollar y publicar agentes virtuales inteligentes para Teams sin tener que configurar un entorno de desarrollo, crear un servicio web o registrarse directamente con Bot Framework.

### <a name="create-virtual-assistant"></a>Crear un asistente virtual

Virtual Assistant es una plantilla de código abierto de Microsoft que le permite crear una solución conversacional sólida y mantener el control total de la experiencia del usuario, la personalidad de marca de la organización y los datos necesarios. 

## <a name="app-templates"></a>Plantillas de aplicación

Puedes usar la plantilla de aplicación para crear aplicaciones personalizadas que se adapten a tus necesidades organizativas. Se trata de aplicaciones preparadas para producción Microsoft Teams que están controladas por la comunidad, de código abierto y disponibles en GitHub. Cada plantilla contiene instrucciones detalladas para implementar e instalar la aplicación para su organización. Proporciona una aplicación lista para usar que puede instalar y empezar a usar inmediatamente. 

## <a name="teams-shifts-work-force-management-connectors"></a>Teams Conectores de administración de fuerza de trabajo de turnos

Teams Los conectores de administración de fuerza de trabajo de turnos son integraciones basadas en la producción, de código abierto y basadas en la comunidad. Ofrecen una experiencia perfecta y un proceso rápido para la transformación digital de trabajadores de primera línea con Teams Shifts.

## <a name="install-moodle-lms"></a>Instalar Moodle LMS

Moodle es un popular sistema de administración Learning de código abierto (LMS). Ahora está integrado con Microsoft Teams. Esta integración ayuda a los formadores y profesores a colaborar en torno a los cursos de Moodle, hacer preguntas sobre calificaciones y asignaciones y mantenerse actualizados con las notificaciones directamente dentro de Teams.

## <a name="create-a-share-to-teams-button-for-your-website"></a>Creación de un botón Compartir en Teams para el sitio web

Los sitios web de terceros pueden usar el script del iniciador para insertar Share en Teams botones en sus páginas web. Cuando selecciona el botón, inicia la experiencia Compartir Teams en una ventana emergente. Esto le permite compartir un vínculo directamente con cualquier persona o canal Microsoft Teams sin cambiar de contexto.

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>Agregar una Microsoft Teams pestaña en SharePoint

Puede obtener una experiencia de integración enriquecida entre Microsoft Teams y SharePoint agregando una pestaña Microsoft Teams en SharePoint como elemento web SPFx web. 

## <a name="create-deep-link"></a>Crear vínculo profundo

Puede crear vínculos profundos a las entidades de Teams. Puede crear vínculos a información y características dentro de Teams. Estos vínculos profundos navegan al contenido y a la información de la pestaña. Puedes usar vínculos profundos para vincular la aplicación con Teams a medida que enlazan varias partes de una aplicación para una experiencia Teams nativa.

## <a name="integrate-device-capabilities"></a>Integrar funcionalidades de dispositivos

Microsoft Teams plataforma está mejorando continuamente las capacidades de los desarrolladores que se alinean con las experiencias integradas de primera persona. La plataforma de Teams mejorada permite a los asociados acceder e integrar las capacidades de dispositivo nativo, como cámara, escáner qr o código de barras, galería de fotos, micrófono y ubicación mediante API dedicadas disponibles en el SDK de cliente de JavaScript de Microsoft Teams. 

## <a name="integrate-people-picker"></a>Integrar Selector de personas

Puedes integrar el control Teams selector de personas nativas que permite a los usuarios buscar y seleccionar personas en la experiencia de la aplicación web.

## <a name="integrate-teams-in-your-external-app"></a>Integrar Teams en la aplicación externa
Puedes insertar tus propias experiencias en Microsoft Teams creando Teams aplicaciones. Si desea invertir  este modelo e integrar Teams u otras capacidades de comunicación en su propia experiencia de aplicación [externa,](/azure/communication-services/overview)consulte Azure Communication Services . Azure Communication Services son servicios basados en la nube con API de REST y SDK de biblioteca de cliente para ayudarle a integrar la comunicación en sus propias aplicaciones personalizadas. Puedes insertar componentes web genéricos Teams estilo React para llamar y chatear con la ayuda de la biblioteca [de interfaz de usuario.](https://azure.github.io/communication-ui-library/)

Las aplicaciones de Azure Communication Services pueden usar la funcionalidad de vista previa pública para [interoperar](/azure/communication-services/concepts/teams-interop) con Teams y permitir que la aplicación personalizada se una Teams reuniones de forma anónima. Por ejemplo, puede integrar videollamadas en una aplicación bancaria móvil y permitir que los usuarios finales se reúnan virtualmente con los empleados del banco mediante Microsoft Teams. 

También puede integrar una identidad Microsoft 365 para crear aplicaciones externas que inserten vídeo y llamadas RTC en nombre de un Teams usuario. Si ha usado [sdk](/skype-sdk/appsdk/skypeappsdk) Skype Empresarial en el pasado, estas funcionalidades como parte de Azure Communication Services se recomiendan como reemplazo.

## <a name="see-also"></a>Consulte también

* [Asignar los casos de uso de la aplicación a Teams funcionalidades de plataforma](~/concepts/design/map-use-cases.md)
* [Determinar los puntos de entrada de la aplicación](~/concepts/extensibility-points.md)
* [Integrar aplicaciones web](~/samples/integrating-web-apps.md)
* [Crear aplicaciones personalizadas de código bajo para Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [Añadir un bot de chat de Power Virtual Agents](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [Crear asistente virtual](~/samples/virtual-assistant.md)
* [Plantillas de aplicaciones para Microsoft Teams](~/samples/app-templates.md)
* [Conectores de turnos listos para producción](~/samples/shifts-wfm-connectors.md)
* [Instalar Moodle LMS](~/resources/moodleinstructions.md)
* [Crear un botón de Compartir en Teams](~/concepts/build-and-test/share-to-teams.md)
* [Añadir una pestaña de Teams a SharePoint](~/tabs/how-to/tabs-in-sharepoint.md)
* [Crear vínculos profundos](~/concepts/build-and-test/deep-links.md)
* [Funciones del dispositivo](~/concepts/device-capabilities/device-capabilities-overview.md)
* [control de selector de personas](~/concepts/device-capabilities/people-picker-capability.md)
