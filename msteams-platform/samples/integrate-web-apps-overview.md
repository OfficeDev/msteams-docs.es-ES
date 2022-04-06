---
title: Integrar aplicaciones web
author: Rajeshwari-v
description: Información general sobre la integración de aplicaciones web y funcionalidades de dispositivo con Microsoft Teams aplicación.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: power apps power apps selector de personas deep link virtual agent assistant share-to-Teams
ms.openlocfilehash: 8fe6b41f129497d439d9cf5ef391c800d6ddea0e
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685593"
---
# <a name="integrate-web-apps"></a>Integrar aplicaciones web

Puede proporcionar una experiencia de usuario enriquecida mediante la integración de las características de una aplicación web existente en Microsoft Teams plataforma. Asegúrese de seguir [Teams directrices de diseño](~/concepts/design/understand-use-cases.md) para que la aplicación sea nativa para Teams.
En este documento se proporciona información general sobre los requisitos previos para integrar aplicaciones web con Teams, power platform para crear power apps, Power Virtual Agents, Virtual Assistant, plantillas de aplicación, conectores shift, Moodle LMS, creación de un botón Compartir a Teams para su sitio web, agregar un Microsoft Teams  pestaña en SharePoint, creando vínculos profundos e integrando funcionalidades de dispositivo.

## <a name="prerequisites"></a>Requisitos previos

Para una integración eficaz, asegúrese de comprender mejor los siguientes requisitos previos:

* capacidades de Teams.
* SharePoint requisitos para el almacenamiento de archivos y datos.
* Requisitos de API.
* Autenticación.
* Vinculación profunda de la aplicación con Teams.
* Asigne los casos de uso de la aplicación a las funcionalidades de la plataforma de Teams.
* Determine los puntos de entrada de la aplicación, como el uso personal, la colaboración o ambos.

## <a name="low-code-platforms"></a>Plataformas de código bajo

Las plataformas de código bajo proporcionan un enfoque intuitivo para el desarrollo de software y requieren poca o ninguna codificación para compilar aplicaciones y procesos. Puede crear aplicaciones personalizadas fácilmente con plataformas de código bajo. Estas plataformas constan de una interfaz visual, conectores a servicios back-end y un sistema integrado de administración del ciclo de vida de aplicaciones para compilar, depurar, implementar y mantener aplicaciones. Microsoft proporciona las siguientes puertas de enlace innovadoras para crear rápidamente aplicaciones compatibles con Teams mediante atributos de código bajo:

* Plataforma Microsoft Power
* plantillas de aplicación de Microsoft Teams

## <a name="microsoft-power-platform"></a>Plataforma Microsoft Power

La plataforma Microsoft Power combina cuatro tecnologías sólidas de Microsoft, como Power BI, Power Apps, Power Automate y Power Virtual Agents en una potente plataforma de aplicaciones. Estas tecnologías le permiten crear soluciones, automatizar procesos, analizar datos y crear agentes virtuales dentro de un entorno unificado e integrado.

>[!NOTE]
>No debe usar Microsoft Power Platform para crear aplicaciones que se van a publicar en la tienda de aplicaciones de Teams. Las aplicaciones de Microsoft Power Platform solo se pueden publicar en la tienda de aplicaciones de una organización.

### <a name="power-apps"></a>Power Apps

Con Power Apps, puede crear aplicaciones empresariales que se conecten a los datos empresariales y se adapten a las necesidades de su organización. Power Apps habilitar una amplia gama de escenarios de aplicaciones para resolver los desafíos empresariales a través de aplicaciones de lienzo. Después de compilar la aplicación, puede exportarla desde el portal del creador de Power Apps e insertarla en Microsoft Teams.

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent es una solución de interfaz gráfica guiada sin código. Se basa en Microsoft Power Platform y Bot Framework. Permite a todos los miembros de su equipo crear y mantener completos bots de chat conversacionales que se integran fácilmente con la plataforma de Teams. Puede diseñar, desarrollar y publicar agentes virtuales inteligentes para Teams sin tener que configurar un entorno de desarrollo, crear un servicio web o registrarse directamente en Bot Framework.

### <a name="create-virtual-assistant"></a>Crear un asistente virtual

Virtual Assistant es una plantilla de código abierto de Microsoft que le permite crear una solución conversacional sólida y mantener el control total de la experiencia del usuario, la personalización de marca de la organización y los datos necesarios.

## <a name="app-templates"></a>Plantillas de aplicación

Puede usar la plantilla de aplicación para crear aplicaciones personalizadas que se adapten a sus necesidades organizativas. Se trata de aplicaciones listas para producción para Microsoft Teams controladas por la comunidad, de código abierto y disponibles en GitHub. Cada plantilla contiene instrucciones detalladas para implementar e instalar la aplicación para su organización. Proporciona una aplicación lista para usar que puede instalar y empezar a usar inmediatamente.

## <a name="teams-shifts-work-force-management-connectors"></a>conectores de administración de Teams Shifts Work Force Management

Teams los conectores de Administración de turnos de Work Force son integraciones preparadas para producción, de código abierto y controladas por la comunidad. Ofrecen una experiencia perfecta y un proceso rápido para la transformación digital de los trabajadores de primera línea con turnos de Teams.

## <a name="install-moodle-lms"></a>Instalar Moodle LMS

Moodle es un popular sistema de administración de Learning de código abierto (LMS). Ahora se integra con Microsoft Teams. Esta integración ayuda a los educadores y profesores a colaborar en torno a los cursos de Moodle, a formular preguntas sobre calificaciones y asignaciones, y a mantenerse actualizados con las notificaciones directamente dentro de Teams.

## <a name="create-a-share-to-teams-button-for-your-website"></a>Creación de un botón Compartir en Teams para el sitio web

Los sitios web de terceros pueden usar el script del iniciador para insertar Share para Teams botones en sus páginas web. Al seleccionar el botón, se inicia la experiencia Compartir en Teams en una ventana emergente. Esto le permite compartir un vínculo directamente con cualquier persona o canal Microsoft Teams sin cambiar de contexto.

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>Agregar una pestaña de Microsoft Teams en SharePoint

Para obtener una experiencia de integración enriquecida entre Microsoft Teams y SharePoint, agregue una pestaña de Microsoft Teams en SharePoint como elemento web SPFx.

## <a name="create-deep-link"></a>Crear vínculo profundo

Puede crear vínculos profundos a las entidades de Teams. Puede crear vínculos a información y características en Teams. Estos vínculos profundos se desplazan al contenido y a la información de la pestaña. Puedes usar vínculos profundos para vincular la aplicación con Teams, ya que unen varias partes de una aplicación para una experiencia de Teams más nativa.

## <a name="integrate-device-capabilities"></a>Integrar las funcionalidades del dispositivo

Microsoft Teams plataforma mejora continuamente las capacidades de los desarrolladores en consonancia con las experiencias integradas de primera persona. La plataforma de Teams mejorada permite a los asociados acceder e integrar las funcionalidades nativas del dispositivo, como cámara, escáner qr o código de barras, galería de fotos, micrófono y ubicación mediante API dedicadas disponibles en Microsoft Teams SDK de cliente de JavaScript.

## <a name="integrate-people-picker"></a>Integrar Selector de personas

Puede integrar el Teams control de selector de personas nativas que permite a los usuarios buscar y seleccionar personas en la experiencia de la aplicación web.

## <a name="integrate-teams-in-your-external-app"></a>Integración de Teams en la aplicación externa

Puede insertar sus propias experiencias en Microsoft Teams mediante la creación de aplicaciones Teams. Si desea *invertir* este modelo e integrar Teams u otras funcionalidades de comunicación en su propia experiencia de aplicación externa, consulte [Azure Communication Services](/azure/communication-services/overview). Azure Communication Services son servicios basados en la nube con API REST y SDK de biblioteca cliente para ayudarle a integrar la comunicación en sus propias aplicaciones personalizadas. Puede insertar componentes web de React genéricos o con estilo Teams para llamar y chatear con la ayuda de la biblioteca de interfaz de [usuario](https://azure.github.io/communication-ui-library/).

Azure Communication Services aplicaciones pueden usar la funcionalidad de versión preliminar pública para [interoperar con Teams](/azure/communication-services/concepts/teams-interop) y permitir que la aplicación personalizada se una a Teams reuniones de forma anónima. Por ejemplo, puede integrar las videollamadas en una aplicación de banca móvil y permitir que los usuarios finales se reúnan virtualmente con los empleados del banco mediante Microsoft Teams.

También puede integrar Microsoft 365 identidad para compilar aplicaciones externas que insertan vídeo y llamadas RTC en nombre de un usuario Teams. Si ha usado [Skype Empresarial SDK](/skype-sdk/appsdk/skypeappsdk) en el pasado, estas funcionalidades como parte de Azure Communication Services se recomiendan como reemplazo.

## <a name="see-also"></a>Vea también

* [Asignar los casos de uso de la aplicación a las funcionalidades de la plataforma Teams](~/concepts/design/map-use-cases.md)
* [Determinación de los puntos de entrada de la aplicación](~/concepts/extensibility-points.md)
* [Consideraciones para la integración de Teams](~/samples/integrating-web-apps.md)
* [Creación de aplicaciones personalizadas de código bajo para Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [Añadir un bot de chat de Power Virtual Agents](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [Creación de un asistente virtual](~/samples/virtual-assistant.md)
* [Plantillas de aplicaciones para Microsoft Teams](~/samples/app-templates.md)
* [Conectores shift listos para producción](~/samples/shifts-wfm-connectors.md)
* [Instalar Moodle LMS](~/resources/moodleinstructions.md)
* [Uso compartido en Teams desde aplicaciones web](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [Añadir una pestaña de Teams a SharePoint](~/tabs/how-to/tabs-in-sharepoint.md)
* [Crear vínculos profundos](~/concepts/build-and-test/deep-links.md)
* [Funciones del dispositivo](~/concepts/device-capabilities/device-capabilities-overview.md)
* [Control Selector de personas](~/concepts/device-capabilities/people-picker-capability.md)
