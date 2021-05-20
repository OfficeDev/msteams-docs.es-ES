---
title: Diseño de la aplicación personalizada
author: heath-hamilton
description: Obtén información sobre cómo diseñar aplicaciones Microsoft Teams. Los recursos incluyen el kit de interfaz de usuario Microsoft Teams, procedimientos recomendados, ejemplos y mucho más.
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 2f21872bd8c37026528ff6fde282e8c433d5e052
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565119"
---
# <a name="designing-your-microsoft-teams-app"></a>Diseño de la aplicación Microsoft Teams

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Imagen conceptual que introduce las directrices de diseño Microsoft Teams.":::

Ya sea que sea diseñador, administrador de productos, desarrollador o creador que utilice herramientas de código bajo, estas directrices pueden ayudarle a tomar rápidamente las decisiones de diseño correctas para su aplicación Microsoft Teams.

## <a name="teams-app-design-principles"></a>Teams principios de diseño de aplicaciones

Teams aplicaciones ayudan a las personas a lograr más juntos. Utilice estos principios para guiar su diseño.

:::row:::
   :::column span="":::

### <a name="collaborative"></a>colaborativo

Teams aplicaciones ayudan a las personas a lograr más juntos. Utilice estos principios para guiar su diseño.

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>fidedigno

La aplicación es segura y compatible. Los usuarios pueden encontrar fácilmente información sobre la privacidad.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>Globalmente inclusivo

Personas de todos los orígenes, conjuntos de habilidades y disciplinas pueden usar la aplicación. Es cultural, racial y socialmente consciente.

   :::column-end:::
   :::column span="":::

### <a name="light"></a>Leve

La aplicación se centra en escenarios principales que se mezclan con flujos de trabajo Teams.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>Nativo o distinto

La aplicación utiliza componentes de diseño Teams nativos o los suyos propios. No hay una mezcla de esquemas de color, controles, etc.

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>útil

La aplicación se basa en un escenario que las personas deben hacer en Teams.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>Fácil de usar

La interfaz de usuario es fácil de entender, agradable en apariencia y tono, y hace que la gente sea más productiva.

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>Respuesta correcta

La aplicación es independiente del dispositivo y la pantalla.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>Accesible

La aplicación cumple Teams requisitos de accesibilidad en términos de contraste de color, alternativas de navegación y más.

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>Bien descrito

El texto, los iconos y las imágenes dejan claro para qué sirve la aplicación y cómo usarla.

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a>Creación de una experiencia cohesiva

Diseñar una aplicación Teams es como diseñar una aplicación web convencional, pero también un poco diferente. Un diseño eficaz resalta los atributos únicos de la aplicación mientras se ajusta de forma natural con Teams características y contextos.

Estas directrices y recursos pueden ayudarle a lograr ese equilibrio. Sabrás qué hacer y qué evitar al diseñar tu aplicación de Teams (como la navegación de varios niveles en una pestaña).

## <a name="planning-your-app"></a>Planificación de la aplicación

Para diseñar una aplicación de Teams de alta calidad, primero debe comprender lo que desea que haga la aplicación y cómo cree que la gente la usará. Si aún no lo has hecho, tómate un tiempo para planificar correctamente [la aplicación.](../../concepts/extensibility-points.md)

## <a name="design-fundamentals"></a>Conceptos básicos de diseño

Aprenda los [fundamentos del diseño de Teams aplicación,](design-teams-app-fundamentals.md)incluidos el diseño, los esquemas de color y mucho más.

## <a name="basic-fluent-ui-components-for-teams"></a>Componentes básicos de la interfaz de usuario fluida para Teams

En función de fluent UI, estos son los [elementos principales para crear interfaces de Teams conocidas.](design-teams-app-basic-ui-components.md)

## <a name="ui-templates"></a>Plantillas de la interfaz de usuario

Cree rápidamente diseños complejos y de alta fidelidad con [plantillas para casos de uso y flujos de trabajo comunes Teams.](design-teams-app-ui-templates.md)

## <a name="app-capabilities"></a>Capacidades de la aplicación

Comprenda cómo las personas agregan, usan y administran aplicaciones Teams para aprovechar al máximo cada capacidad en su diseño.

* [Aplicaciones personales](../../concepts/design/personal-apps.md)
* [Pestañas](../../tabs/design/tabs.md)
* [Extensiones de mensajería](../../messaging-extensions/design/messaging-extension-design.md)
* [Bots](../../bots/design/bots.md)
* [Extensiones de reunión](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Módulos de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [Tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a>Personalización de aplicaciones

Comprender cómo el administrador de Teams puede personalizar o cambiar el nombre de la aplicación en función de la necesidad de la organización. Esta personalización está habilitada si define el `configurableProperties` esquema de manifiesto. Para obtener más información, consulte [Personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).

> [!NOTE]
> La personalización de la aplicación permite a los administradores cambiar la apariencia de las aplicaciones cargadas a través de bots, extensiones de mensajería, pestañas y conectores. Por ejemplo, si el administrador de Teams personaliza el nombre de una aplicación de *Contoso* al *Agente de Contoso,* la aplicación aparecerá con el nuevo nombre *Contoso Agent* para los usuarios. Sin embargo, al agregar un conector a un chat, en la lista los conectores seguirán mostrando el nombre de la aplicación como *Contoso*.
> 
> Como práctica recomendada, debe proporcionar directrices de personalización para que los usuarios y clientes de la aplicación las sigan al personalizar la aplicación. Para obtener más información, consulte [personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).

## <a name="tools-and-samples"></a>Herramientas y ejemplos

Las siguientes herramientas pueden ayudar a los diseñadores y desarrolladores a empezar:

### <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Diseñe una aplicación Teams con componentes de interfaz de usuario, plantillas y ejemplos que pueda arrastrar, soltar y modificar según sea necesario. El kit de interfaz de usuario también incluye información completa sobre cómo deben verse y comportarse las aplicaciones en diferentes escenarios Teams.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams Biblioteca de IU

Vea y pruebe plantillas de interfaz de usuario Teams individuales y componentes relacionados en el explorador.

> [!div class="nextstepaction"]
> [Pruebe la biblioteca de interfaz de usuario (área de juegos)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importe estas plantillas y componentes relacionados directamente en el proyecto de aplicación Teams.

> [!div class="nextstepaction"]
> [Obtener la biblioteca de interfaz de usuario (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Aplicación de ejemplo

Instale una aplicación de ejemplo para ver cómo se ven y se comportan las plantillas de interfaz de usuario en contextos Teams.

> [!div class="nextstepaction"]
> [Obtener la aplicación de ejemplo (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>Otros recursos

Para obtener más información, pruebe uno de los siguientes recursos:

### <a name="fluent-ui-documentation"></a>Documentación fluida de IU

Obtenga ejemplos de código y detalles de implementación para los componentes basados en la interfaz de usuario de Fluent que se usan para crear experiencias Teams.

> [!div class="nextstepaction"]
> [Probar componentes de interfaz de usuario Teams (INTERFAZ de usuario fluida)](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>Diseñador de tarjetas adaptables

Diseña tarjetas adaptables en nuestra herramienta basada en web.

> [!div class="nextstepaction"]
> [Pruebe el diseñador de tarjetas adaptables](https://adaptivecards.io/designer/)
