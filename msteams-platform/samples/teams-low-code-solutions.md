---
title: Creación de aplicaciones personalizadas de código bajo para Microsoft Teams
author: surbhigupta
description: Obtenga información sobre las soluciones de código bajo y sin código de Microsoft disponibles con Teams, una plataforma de Microsoft Power.
ms.localizationpriority: medium
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 74dd4eb094c31510319932ec96cbb0db34a1fca5
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503315"
---
# <a name="create-low-code-custom-apps-for-teams"></a>Creación de aplicaciones personalizadas de código bajo para Teams

Microsoft Teams es extensible y adaptable. Esto significa que puede crear aplicaciones personalizadas para Teams que satisfagan las distintas necesidades de los usuarios. Las aplicaciones personalizadas de código bajo ahorran tiempo, proporcionan soluciones rápidas y satisfacen la misma demanda que las aplicaciones creadas desde cero. En este documento se proporciona información general sobre Microsoft Power Platform, el bot de chat de Power Virtual Agents y Virtual Assistant.

Las plataformas de código bajo proporcionan un enfoque intuitivo para el desarrollo de software con codificación mínima o nula para compilar aplicaciones y procesos. Permiten a los desarrolladores sin experiencia crear aplicaciones personalizadas fácilmente con poca o ninguna codificación, y a desarrolladores profesionales desarrollar e implementar la aplicación rápidamente. Estas plataformas constan de una interfaz visual, conectores para servicios back-end y un sistema integrado de administración del ciclo de vida de aplicaciones para compilar, depurar, implementar y mantener aplicaciones. Microsoft Power Platform es la puerta de enlace innovadora para crear rápidamente aplicaciones compatibles con Teams mediante atributos de código bajo.

## <a name="teams-and-microsoft-power-platform"></a>Teams y Microsoft Power Platform

Microsoft Power Platform combina cuatro tecnologías sólidas de Microsoft, como Power BI, Power Apps, Power Automate, anteriormente Microsoft Flow y Power Virtual Agents en una potente plataforma de aplicaciones. Estas tecnologías le permiten crear soluciones, automatizar procesos, analizar datos y crear agentes virtuales dentro de un entorno unificado e integrado:

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="Servicios de Power Platform":::

> [!NOTE]
> No debe usar Microsoft Power Platform para crear aplicaciones que se van a publicar en la tienda de aplicaciones de Teams. Las aplicaciones de Microsoft Power Platform solo se pueden publicar en la tienda de aplicaciones de una organización.

### <a name="-teams-and-power-bi"></a>✔ Teams y Power BI

La [pestaña Power BI de Microsoft Teams](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/) agrega compatibilidad con informes en el área de trabajo de Teams y permite a los usuarios [compartir contenido interactivo Power BI](/power-bi/collaborate-share/service-embed-report-microsoft-teams) y [colaborar con otros usuarios en canales y chats de Teams](/power-bi/collaborate-share/service-collaborate-microsoft-teams). Puede crear contenido empaquetado en la [aplicación de Power BI](/power-bi/collaborate-share/service-create-distribute-apps) desde cero y distribuirlo como una aplicación o [crear una aplicación de plantilla en Power BI](/power-bi/connect-data/service-template-apps-create). Además, usa la nueva [aplicación de Power BI en Teams](https://go.microsoft.com/fwlink/?linkid=2143643) para incorporar toda tu experiencia básica en el servicio Power BI a Teams.

### <a name="-teams-and-power-apps"></a>✔ Teams y Power Apps

Con [Power Apps](/powerapps/powerapps-overview), puede crear aplicaciones empresariales que se conecten a los datos empresariales y se adapten a las necesidades de su organización.  Power Apps habilitar una amplia gama de escenarios de aplicaciones para resolver los desafíos empresariales a través de [aplicaciones de lienzo](/powerapps/maker/#canvas-apps). Después de la compilación, puede exportar la aplicación desde el portal del creador de Power Apps e [insertarla en Microsoft Teams](/power-platform/admin/embed-app-teams).

La nueva [aplicación Power Apps](https://go.microsoft.com/fwlink/?linkid=2143374) de Teams proporciona una experiencia integrada para que los creadores de aplicaciones creen y editen aplicaciones y flujos de trabajo dentro de Teams. Pueden publicar y compartir rápidamente las aplicaciones con los miembros del equipo. Los miembros pueden usar las aplicaciones sin tener que cambiar entre varias aplicaciones y servicios.

### <a name="-teams-and-power-automate"></a>✔ Teams y Power Automate

Puede [crear flujos para automatizar tareas de trabajo repetitivas](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/) directamente en el entorno de Teams con la [aplicación Power Automate en Teams](/power-automate/flows-teams). Puede [desencadenar un flujo desde cualquier mensaje de Microsoft Teams](/power-automate/trigger-flow-teams-message) y [usar tarjetas adaptables dentro de Power Automate](/power-automate/create-adaptive-cards). Además, puede crear flujos para personalizar y agregar más valor a Microsoft Teams desde la nueva [aplicación de Power Apps](https://go.microsoft.com/fwlink/?linkid=2143539) en Teams.

### <a name="-teams-and-power-virtual-agents"></a>✔ Teams y Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) es una solución de interfaz gráfica guiada sin código, basada en Microsoft Power Platform y Bot Framework. Una solución de interfaz gráfica guiada sin código que permite a todos los miembros de su equipo crear bots de chat enriquecidos y conversacionales que se integren fácilmente con la plataforma de Teams. Todo el contenido creado en Power Virtual Agents se representa de forma natural en Teams y los bots de Power Virtual Agents interactúan con los usuarios en el lienzo de chat nativo de Teams. Puede [integrar el bot de chat de Power Virtual Agents](/power-virtual-agents/publication-add-bot-to-microsoft-teams) para Teams a través del [portal de Power Virtual Agents](https://powervirtualagents.microsoft.com).

Use la nueva [aplicación Power Virtual Agents](https://aka.ms/pva-teams-docs) en Teams para crear, administrar y publicar bots de chat conversacionales fácilmente desde Teams. Puede compartir los bots con otras personas de su organización para chatear y obtener respuestas a sus preguntas.

### <a name="-virtual-assistant-for-teams"></a>✔ Asistente virtual para Teams

Un asistente virtual es un modelo de código abierto de Microsoft que permite crear una solución conversacional sólida a la vez que mantiene el control total de la experiencia del usuario, la marca de la organización y los datos necesarios. Puede configurar el asistente virtual para la [integración en el entorno de Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro).

### <a name="-power-platform-learn-modules"></a>✔ Módulos de Power Platform Learn

|  Tema  |  Vínculos  |
|:---------|:----------------------|
|Power BI|[Power BI para creadores de aplicaciones](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)</br>[Power BI para desarrolladores](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|Power Apps|[Power Apps para creadores de aplicaciones](/learn/browse/?products=power-apps&roles=maker)</br>[Power Apps para desarrolladores](/learn/browse/?products=power-apps)|
|Power Automate|[Power Automate para creadores de aplicaciones](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)</br>[Power Automate para desarrolladores](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|Power Virtual Agents|[Power Virtual Agents para creadores y desarrolladores de aplicaciones](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)|

### <a name="-project-oakdale-preview"></a>✔ Project Oakdale (versión preliminar)

> [!NOTE]
> Se ha cambiado el nombre de Project **Oakdale** al proyecto **Dataverse para Teams**.

[Project Oakdale](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) es una nueva plataforma de datos de código bajo que próximamente Microsoft Teams. Permite a los desarrolladores crear soluciones de Power Platform en Teams directamente dentro de Teams. Para obtener más información sobre Project Oakdale, consulte [Blog de Teams Microsoft Project Oakdale](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams).

### <a name="-microsoft-blog-insights"></a>✔ Conclusiones del blog de Microsoft

[Más información sobre las capacidades de la plataforma de datos en Project Oakdale](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[Anuncio de actualizaciones de Power Platform y Teams para ayudar a los clientes a adaptarse al trabajo remoto](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teams está dando forma al futuro del trabajo con características de código bajo para mejorar el área de trabajo digital](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>✔ Administración de aplicaciones de Power Platform

> [!div class="nextstepaction"]
> [Administrar aplicaciones de Power Platform en el centro de administración de Microsoft Teams](/microsoftteams/manage-power-platform-apps)

## <a name="see-also"></a>Consulte también

[Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
