---
title: Diseño de la aplicación personalizada
author: heath-hamilton
description: Aprende a diseñar aplicaciones de Microsoft Teams. Los recursos incluyen el Kit de interfaz de usuario de Microsoft Teams, procedimientos recomendados, ejemplos y mucho más.
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: d7f3e89ce5ad51fb1a8cecddf0b22d59544ecc09
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019884"
---
# <a name="designing-your-microsoft-teams-app"></a>Diseño de la aplicación de Microsoft Teams

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Imagen conceptual que presenta las directrices de diseño de Microsoft Teams.":::

Tanto si eres diseñador, jefe de producto, desarrollador o creador con herramientas de código bajo, estas directrices pueden ayudarte a tomar rápidamente las decisiones de diseño adecuadas para tu aplicación de Microsoft Teams.

## <a name="teams-app-design-principles"></a>Principios de diseño de aplicaciones de Teams

Las aplicaciones de Teams ayudan a los usuarios a lograr más juntos. Use estos principios para guiar el diseño.

:::row:::
   :::column span="":::

### <a name="collaborative"></a>Colaboración

Las aplicaciones de Teams ayudan a los usuarios a lograr más juntos. Use estos principios para guiar el diseño.

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>Confiable

La aplicación es segura y compatible. Los usuarios pueden encontrar fácilmente información sobre privacidad.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>Globalmente inclusiva

Las personas de todos los orígenes, conjuntos de aptitudes y disciplinas pueden usar la aplicación. Es cultural, racial y socialmente consciente.

   :::column-end:::
   :::column span="":::

### <a name="light"></a>Leve

La aplicación se centra en escenarios principales que se combinan con flujos de trabajo de Teams.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>Nativo o distinto

La aplicación usa componentes de diseño nativos de Teams o los tuyos propios. No hay combinación de esquemas de color, controles, etc.

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>Útil

La aplicación se basa en un escenario que los usuarios deben hacer en Teams.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>Fácil de usar

La interfaz de usuario es fácil de entender, agradable en apariencia y tono, y hace que las personas sean más productivas.

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>Respuesta correcta

La aplicación es independiente del dispositivo y la pantalla.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>Accesible

La aplicación cumple los requisitos de accesibilidad de Teams en términos de contraste de color, alternativas de navegación y mucho más.

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>Bien descrito

El texto, los iconos y las imágenes hacen que se aclare para qué está la aplicación y cómo usarla.

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a>Creación de una experiencia cohesiva

Diseñar una aplicación de Teams es como diseñar una aplicación web convencional, pero también un poco diferente. Un diseño eficaz resalta los atributos únicos de la aplicación a la vez que se adapta de forma natural a las características y contextos de Teams.

Estas directrices y recursos pueden ayudarle a encontrar ese equilibrio. Sabrás qué hacer y qué evitar al diseñar la aplicación de Teams (como la navegación de varios niveles en una pestaña).

## <a name="planning-your-app"></a>Planeación de la aplicación

Para diseñar una aplicación de Teams de alta calidad, primero debes comprender lo que quieres que haga tu aplicación y cómo crees que la usarán las personas. Si aún no lo has hecho, tómese un tiempo para [planear correctamente la aplicación](../../concepts/extensibility-points.md).

## <a name="design-fundamentals"></a>Conceptos básicos de diseño

Obtén información [sobre los conceptos básicos del diseño de la](design-teams-app-fundamentals.md)aplicación de Teams, incluido el diseño, las esquemas de color y mucho más.

## <a name="basic-fluent-ui-components-for-teams"></a>Componentes básicos de la interfaz de usuario fluent para Teams

Basados en la interfaz de usuario de Fluent, estos son los [elementos principales para crear interfaces familiares de Teams.](design-teams-app-basic-ui-components.md)

## <a name="ui-templates"></a>Plantillas de la interfaz de usuario

Cree rápidamente diseños complejos y de alta fidelidad con plantillas para casos de uso y flujos de trabajo [comunes de Teams.](design-teams-app-ui-templates.md)

## <a name="app-capabilities"></a>Capacidades de la aplicación

Comprender cómo las personas agregan, usan y administran aplicaciones de Teams para aprovechar al máximo cada funcionalidad del diseño.

* [Aplicaciones personales](../../concepts/design/personal-apps.md)
* [Pestañas](../../tabs/design/tabs.md)
* [Extensiones de mensajería](../../messaging-extensions/design/messaging-extension-design.md)
* [Bots](../../bots/design/bots.md)
* [Extensiones de reunión](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Módulos de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [Tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a>Personalización de aplicaciones

Comprender cómo el administrador de Teams puede personalizar o cambiar el nombre de la aplicación en función de las necesidades de la organización. Esta personalización se habilita si se define en `configurableProperties` el esquema de manifiesto. Para obtener más información, consulta [Personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).

> [!NOTE]
> Esta característica está disponible actualmente solo en la versión preliminar del desarrollador.
> 
> La personalización de aplicaciones permite a los administradores cambiar la apariencia de las aplicaciones cargadas a través de bots, extensiones de mensajería, pestañas y conectores. Por ejemplo, si el administrador de Teams personaliza el nombre de una aplicación de *Contoso* a *Contoso Agent,* la aplicación aparecerá con el nuevo nombre *Agente Contoso* para los usuarios. Sin embargo, al agregar un conector a un chat, en la lista los conectores seguirán mostrándole el nombre de la aplicación como *Contoso*.
> 
> Como práctica recomendada, debes proporcionar directrices de personalización para que los usuarios de la aplicación y los clientes puedan seguir al personalizar la aplicación. Para obtener más información, consulta [Personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).

## <a name="tools-and-samples"></a>Herramientas y ejemplos

Las siguientes herramientas pueden ayudar a los diseñadores y desarrolladores a empezar:

### <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Diseña una aplicación de Teams con componentes de interfaz de usuario, plantillas y ejemplos que puedas arrastrar, colocar y modificar según sea necesario. El kit de interfaz de usuario también incluye información completa sobre cómo deben verse y comportarse las aplicaciones en diferentes escenarios de Teams.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Biblioteca de interfaz de usuario de Microsoft Teams

Ver y probar plantillas de interfaz de usuario individuales de Teams y componentes relacionados en el explorador.

> [!div class="nextstepaction"]
> [Pruebe la biblioteca de interfaz de usuario (área de juegos)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importe estas plantillas y componentes relacionados directamente en el proyecto de la aplicación de Teams.

> [!div class="nextstepaction"]
> [Obtener la biblioteca de interfaz de usuario (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Aplicación de ejemplo

Instala una aplicación de ejemplo para ver cómo se ven y se comportan las plantillas de interfaz de usuario en contextos de Teams.

> [!div class="nextstepaction"]
> [Obtener la aplicación de ejemplo (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>Otros recursos

Para obtener más información, pruebe uno de los siguientes recursos.

### <a name="fluent-ui-documentation"></a>Documentación de la interfaz de usuario fluent

Obtenga ejemplos de código y detalles de implementación para los componentes basados en fluent ui que se usan para crear experiencias de Teams.

> [!div class="nextstepaction"]
> [Probar componentes de la interfaz de usuario de Teams (Fluent UI)](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>Diseñador de tarjetas adaptables

Diseñar tarjetas adaptables en nuestra herramienta basada en web.

> [!div class="nextstepaction"]
> [Probar el diseñador de tarjetas adaptables](https://adaptivecards.io/designer/)
