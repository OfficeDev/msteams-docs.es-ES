---
title: Integrar aplicaciones web
author: Rajeshwari-v
description: Una introducción a la integración de aplicaciones web y funcionalidades de dispositivos con la aplicación de Microsoft Teams.
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 01977e22d79f7e39986367e647a2d48ea9b2905c
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058659"
---
# <a name="integrate-web-apps"></a>Integrar aplicaciones web

Puede proporcionar una experiencia de usuario enriquecida integrando las características de una aplicación web existente en la plataforma de Microsoft Teams. Asegúrate de seguir las [instrucciones de diseño de Teams](~/concepts/design/understand-use-cases.md) para que tu aplicación sea nativa de Teams.
En este documento se proporciona información general sobre los requisitos previos para integrar aplicaciones web con Teams, la plataforma Power para crear power apps, agentes virtuales, asistente virtual, plantillas de aplicaciones, conectores de turnos, LMS de Moodle, creación de un botón Compartir con Teams para su sitio web, agregar una pestaña de Microsoft Teams en SharePoint, crear vínculos profundos e integrar las capacidades del dispositivo.

## <a name="prerequisites"></a>Requisitos previos   

Para una integración eficaz, asegúrese de comprender mejor los siguientes requisitos previos:
* Capacidades de Teams. 
* Requisitos de SharePoint para el almacenamiento de archivos y datos.
* Requisitos de api.
* Autenticación.
* Vinculación profunda de la aplicación con Teams.
* Asigna los casos de uso de la aplicación a las funcionalidades de la plataforma de Teams.
* Determina los puntos de entrada de la aplicación, como el uso personal, la colaboración o ambos.

## <a name="low-code-platforms"></a>Plataformas de código bajo

Las plataformas de código bajos proporcionan un enfoque intuitivo para el desarrollo de software y requieren poca o ninguna codificación para crear aplicaciones y procesos. Puedes crear aplicaciones personalizadas fácilmente con plataformas de código bajo. Estas plataformas constan de una interfaz visual, conectores para servicios back-end y un sistema integrado de administración del ciclo de vida de aplicaciones para crear, depurar, implementar y mantener aplicaciones. Microsoft proporciona las siguientes puertas de enlace innovadoras para crear rápidamente aplicaciones compatibles con Teams con atributos de código bajos:
* Plataforma de Microsoft Power
* Plantillas de aplicación de Microsoft Teams

## <a name="microsoft-power-platform"></a>Plataforma de Microsoft Power

La plataforma Microsoft Power combina cuatro tecnologías sólidas de Microsoft, como Power BI, Power Apps, Power Automate y Power Virtual Agents en una plataforma de aplicaciones eficaz. Estas tecnologías le permiten crear soluciones, automatizar procesos, analizar datos y crear agentes virtuales en un entorno unificado e integrado.

### <a name="power-apps"></a>Power Apps

Con Power Apps, puedes crear aplicaciones empresariales que se conecten a los datos de tu empresa y se adapten a las necesidades de tu organización. Power Apps permite una amplia variedad de escenarios de aplicaciones para resolver desafíos empresariales a través de aplicaciones de lienzo. Después de crear la aplicación, puedes exportarla desde el portal del fabricante de Power Apps e insertarla en Microsoft Teams.

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent es una solución de interfaz gráfica guiada sin código. Se basa en Microsoft Power Platform y bot Framework. Permite a todos los miembros del equipo crear y mantener bots de chat conversacionales enriquecidos que se integran fácilmente con la plataforma de Teams. Puede diseñar, desarrollar y publicar agentes virtuales inteligentes para Teams sin tener que configurar un entorno de desarrollo, crear un servicio web o registrarse directamente con Bot Framework.

### <a name="create-virtual-assistant"></a>Crear un asistente virtual

Virtual Assistant es una plantilla de código abierto de Microsoft que le permite crear una solución conversacional sólida y mantener el control total de la experiencia del usuario, la personalidad de marca de la organización y los datos necesarios. 

## <a name="app-templates"></a>Plantillas de aplicación

Puedes usar la plantilla de aplicación para crear aplicaciones personalizadas que se adapten a tus necesidades organizativas. Se trata de aplicaciones preparadas para producción para Microsoft Teams que están controladas por la comunidad, de código abierto y disponibles en GitHub. Cada plantilla contiene instrucciones detalladas para implementar e instalar la aplicación para su organización. Proporciona una aplicación lista para usar que puede instalar y empezar a usar inmediatamente. 

## <a name="teams-shifts-work-force-management-connectors"></a>Conectores de administración de fuerza de trabajo de turnos de Teams

Los conectores de administración de fuerza de trabajo de Teams Shifts son integraciones preparadas para producción, de código abierto e impulsadas por la comunidad. Ofrecen una experiencia perfecta y un proceso rápido para la transformación digital de los trabajadores de primera línea con Teams Shifts.

## <a name="install-moodle-lms"></a>Instalar Moodle LMS

Moodle es un popular sistema de administración de aprendizaje de código abierto (LMS). Ahora está integrado con Microsoft Teams. Esta integración ayuda a los formadores y profesores a colaborar en torno a los cursos de Moodle, hacer preguntas sobre calificaciones y asignaciones y mantenerse actualizados con las notificaciones directamente en Teams.

## <a name="create-a-share-to-teams-button-for-your-website"></a>Creación de un botón Compartir en Teams para el sitio web

Los sitios web de terceros pueden usar el script del iniciador para insertar los botones Compartir en Teams en sus páginas web. Al seleccionar el botón, se inicia la experiencia Compartir en Teams en una ventana emergente. Esto le permite compartir un vínculo directamente con cualquier persona o canal de Microsoft Teams sin cambiar de contexto.

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>Agregar una pestaña de Microsoft Teams en SharePoint

Puede obtener una amplia experiencia de integración entre Microsoft Teams y SharePoint agregando una pestaña de Microsoft Teams en SharePoint como un elemento web de SPFx. 

## <a name="create-deep-link"></a>Crear vínculo profundo

Puede crear vínculos profundos a las entidades de Teams. Puede crear vínculos a información y características dentro de Teams. Estos vínculos profundos navegan al contenido y a la información de la pestaña. Puedes usar vínculos profundos para vincular la aplicación con Teams a medida que unen varias partes de una aplicación para una experiencia de Teams más nativa.

## <a name="integrate-device-capabilities"></a>Integrar funcionalidades de dispositivos

La plataforma de Microsoft Teams mejora continuamente las capacidades de los desarrolladores y se alinea con experiencias integradas de primera persona. La plataforma mejorada de Teams permite a los asociados acceder e integrar las capacidades de dispositivo nativo, como cámara, escáner qr o código de barras, galería de fotos, micrófono y ubicación mediante API dedicadas disponibles en el SDK de cliente javaScript de Microsoft Teams. 

## <a name="see-also"></a>Vea también

- [Asignar los casos de uso de la aplicación a las funcionalidades de la plataforma teams](~/concepts/design/map-use-cases.md)

- [Determinar los puntos de entrada de la aplicación](~/concepts/extensibility-points.md)

- [Integrar aplicaciones web](~/samples/integrating-web-apps.md)

- [Crear aplicaciones personalizadas de código bajo para Microsoft Teams](~/samples/teams-low-code-solutions.md)

- [Añadir un bot de chat de Power Virtual Agents](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)

- [Crear asistente virtual](~/samples/virtual-assistant.md)

- [Plantillas de aplicaciones para Microsoft Teams](~/samples/app-templates.md)

- [Conectores de turnos listos para producción](~/samples/shifts-wfm-connectors.md)

- [Instalar Moodle LMS](~/resources/moodleinstructions.md)

- [Crear un botón de Compartir en Teams](~/concepts/build-and-test/share-to-teams.md)

- [Añadir una pestaña de Teams a SharePoint](~/tabs/how-to/tabs-in-sharepoint.md)

- [Crear vínculos profundos](~/concepts/build-and-test/deep-links.md)

- [Funciones del dispositivo](~/concepts/device-capabilities/device-capabilities-overview.md)
