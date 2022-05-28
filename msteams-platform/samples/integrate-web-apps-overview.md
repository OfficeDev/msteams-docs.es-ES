---
title: Integrar aplicaciones web
author: Rajeshwari-v
description: Información general sobre la integración de aplicaciones web y funcionalidades de dispositivo con la aplicación de Microsoft Teams.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
keywords: power platform power apps, selector de vínculos profundos del asistente de agente virtual, compartir con Teams
ms.openlocfilehash: dc31644fca25aeca12b7e5f3095ebae53a3c02ac
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757671"
---
# <a name="integrate-web-apps"></a>Integrar aplicaciones web

Puede proporcionar una experiencia de usuario enriquecida mediante la integración de las características de una aplicación web existente en la plataforma Microsoft Teams. Asegúrese de seguir las [directrices de diseño de Teams](~/concepts/design/understand-use-cases.md) para que la aplicación sea nativa para Teams.
En este documento se proporciona información general sobre los requisitos previos para integrar aplicaciones web con Teams, Power Platform para crear Power apps, Power Virtual Agents, Virtual Assistant, plantillas de aplicación, conectores shift, Moodle LMS, creación de un botón Compartir a Teams para su sitio web, agregar una pestaña Microsoft Teams en SharePoint, creando vínculos profundos e integrando funcionalidades de dispositivo.

## <a name="prerequisites"></a>Requisitos previos

Para una integración eficaz, asegúrese de comprender mejor los siguientes requisitos previos:

* Capacidades de Teams.
* Requisitos de SharePoint para el almacenamiento de archivos y datos.
* Requisitos de API.
* Autenticación.
* Vinculación profunda de la aplicación con Teams.
* Asignar los casos de uso a las funcionalidades de la aplicación de Teams.
* Determine los puntos de entrada de la aplicación, como el uso personal, la colaboración o ambos.

## <a name="low-code-platforms"></a>Plataformas de código bajo

Las plataformas de código bajo proporcionan un enfoque intuitivo para el desarrollo de software y requieren poca o ninguna codificación para compilar aplicaciones y procesos. Puede crear aplicaciones personalizadas fácilmente con plataformas de código bajo. Estas plataformas constan de una interfaz visual, conectores a servicios back-end y un sistema integrado de administración del ciclo de vida de aplicaciones para compilar, depurar, implementar y mantener aplicaciones. Microsoft proporciona las siguientes puertas de enlace innovadoras para crear rápidamente aplicaciones compatibles con Teams mediante atributos de código bajo:

* Microsoft Power Platform
* Plantillas de aplicación de Microsoft Teams

## <a name="microsoft-power-platform"></a>Microsoft Power Platform

La plataforma Microsoft Power combina cuatro tecnologías sólidas de Microsoft, como Power BI, Power Apps, Power Automate y Power Virtual Agents en una potente plataforma de aplicaciones. Estas tecnologías le permiten crear soluciones, automatizar procesos, analizar datos y crear agentes virtuales dentro de un entorno unificado e integrado.

>[!NOTE]
>No debe usar Microsoft Power Platform para crear aplicaciones que se van a publicar en la tienda de aplicaciones de Teams. Las aplicaciones de Microsoft Power Platform solo se pueden publicar en la tienda de aplicaciones de una organización.

### <a name="power-apps"></a>Power Apps

Con Power Apps, puede crear aplicaciones empresariales que se conecten a los datos empresariales y se adapten a las necesidades de su organización. Power Apps habilitar una amplia gama de escenarios de aplicaciones para resolver los desafíos empresariales a través de aplicaciones de lienzo. Después de compilar la aplicación, puede exportarla desde el portal del creador de Power Apps e insertarla en Microsoft Teams.

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent es una solución de interfaz gráfica guiada sin código. Se basa en Microsoft Power Platform y Bot Framework. Una solución de interfaz gráfica guiada sin código que permite a todos los miembros de su equipo crear bots de chat enriquecidos y conversacionales que se integren fácilmente con la plataforma de Teams. Puede diseñar, desarrollar y publicar agentes virtuales inteligentes para Teams sin tener que configurar un entorno de desarrollo, crear un servicio web o registrarse directamente en Bot Framework.

### <a name="create-virtual-assistant"></a>Crear un asistente virtual

Un asistente virtual es un modelo de código abierto de Microsoft que permite crear una solución conversacional sólida a la vez que mantiene el control total de la experiencia del usuario, la marca de la organización y los datos necesarios.

## <a name="app-templates"></a>Plantillas de aplicaciones

Puede usar la plantilla de aplicación para crear aplicaciones personalizadas que se adapten a sus necesidades organizativas. Las plantillas de aplicaciones son aplicaciones listas para la producción en Microsoft Teams que están controladas por la comunidad, son de código abierto y están disponibles en GitHub. Cada plantilla contiene instrucciones detalladas para implementar e instalar la aplicación para su organización. Proporciona una aplicación lista para usar que puede instalar y empezar a usar inmediatamente.

## <a name="install-moodle-lms"></a>Instalar Moodle LMS

Moodle es un popular sistema de administración de aprendizaje (LMS) de código abierto. Ahora se integra con Microsoft Teams. Esta integración ayuda a los educadores y profesores a colaborar en torno a los cursos de Moodle, a formular preguntas sobre calificaciones y tareas y a mantenerse actualizados con las notificaciones directamente dentro de Teams.

## <a name="create-a-share-to-teams-button-for-your-website"></a>Creación de un botón Compartir en Teams para el sitio web

Los sitios web de terceros pueden usar el script del iniciador para insertar Compartir a Teams en los botones de sus páginas web. Al seleccionar el botón, se inicia la experiencia Compartir a Teams en una ventana emergente. Esto le permite compartir un vínculo directamente con cualquier persona o canal de Microsoft Teams sin cambiar de contexto.

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>Añadir una pestaña de Microsoft Teams a SharePoint

Puede obtener una experiencia de integración enriquecida entre Microsoft Teams y SharePoint agregando una pestaña de Microsoft Teams en SharePoint como un elemento web SPFx.

## <a name="create-deep-link"></a>Crear un vínculo profundo

Puede crear vínculos profundos a entidades en Teams. Puede crear vínculos a información y características en Teams. Estos vínculos profundos se desplazan al contenido y a la información de la pestaña. Puedes usar vínculos profundos para vincular la aplicación con Teams, ya que unen varias partes de una aplicación para una experiencia de Teams más nativa.

## <a name="integrate-device-capabilities"></a>Integrar las funcionalidades del dispositivo

La plataforma Microsoft Teams mejora continuamente las capacidades de los desarrolladores en consonancia con las experiencias integradas. La plataforma mejorada de Teams permite a los partners acceder e integrar las funcionalidades nativas del dispositivo, como la cámara, el escáner QR o de código de barras, la galería de fotos, el micrófono y la ubicación mediante las API dedicadas disponibles en el SDK de cliente de JavaScript de Microsoft Teams.

## <a name="integrate-people-picker"></a>Integrar Selector de personas

Puede integrar el control de selector de personas nativas de Teams, que permite a los usuarios buscar y seleccionar personas en la experiencia de la aplicación web.

## <a name="integrate-teams-in-your-external-app"></a>Integración de Teams en la aplicación externa

Puede insertar sus propias experiencias en Microsoft Teams mediante la creación de aplicaciones Teams. Si desea *invertir* este modelo e integrar Teams u otras funcionalidades de comunicación en su propia experiencia de aplicación externa, consulte [Azure Communication Services](/azure/communication-services/overview). Azure Communication Services son servicios basados en la nube con API REST y SDK de biblioteca cliente para ayudarle a integrar la comunicación en sus propias aplicaciones personalizadas. Puede insertar componentes web de React genéricos o con estilo Teams para llamar y chatear con la ayuda de la [biblioteca de interfaz de usuario](https://azure.github.io/communication-ui-library/).

Las aplicación de Azure Communication Services pueden usar la funcionalidad de versión preliminar pública para [interoperar con Teams](/azure/communication-services/concepts/teams-interop) y permitir que la aplicación personalizada se una a reuniones de Teams de forma anónima. Por ejemplo, puede integrar las videollamadas en una aplicación de banca móvil y permitir que los usuarios finales se reúnan virtualmente con los empleados del banco mediante Microsoft Teams.

También puede integrar la identidad de Microsoft 365 para compilar aplicaciones externas que insertan vídeo y llamadas RTC en nombre de un usuario de Teams. Si ha usado [Skype Empresarial SDK](/skype-sdk/appsdk/skypeappsdk) en el pasado, estas funcionalidades como parte de Azure Communication Services se recomiendan como reemplazo.

## <a name="see-also"></a>Vea también

* [Asignar los casos de uso a las funcionalidades de la aplicación de Teams](~/concepts/design/map-use-cases.md)
* [Determinar los puntos de entrada de la aplicación](~/concepts/extensibility-points.md)
* [Consideraciones para la integración de Teams](~/samples/integrating-web-apps.md)
* [Crear aplicaciones personalizadas de código bajo para Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [Añadir un bot de chat de Power Virtual Agents](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [Crear un asistente virtual](~/samples/virtual-assistant.md)
* [Plantillas de aplicaciones para Microsoft Teams](~/samples/app-templates.md)
* [Conectores shift listos para producción](~/samples/shifts-wfm-connectors.md)
* [Instalar Moodle LMS](~/resources/moodleinstructions.md)
* [Compartir en Teams desde aplicaciones web](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [Añadir una pestaña de Teams a SharePoint](~/tabs/how-to/tabs-in-sharepoint.md)
* [Crear vínculos profundos](~/concepts/build-and-test/deep-links.md)
* [Funciones del dispositivo](~/concepts/device-capabilities/device-capabilities-overview.md)
* [Control Selector de personas](~/concepts/device-capabilities/people-picker-capability.md)
