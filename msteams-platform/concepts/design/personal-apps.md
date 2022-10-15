---
title: Diseño de su aplicación personal
description: Obtenga información sobre cómo implementar las directrices de diseño, incluidos los elementos de la interfaz de usuario para diseñar una aplicación personal mediante el kit de interfaz de usuario de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: 4646d47c5aa325291f060ea192dcc1705b414ac7
ms.sourcegitcommit: bd96080c78f25eb0a67ce176df5e255be348f7b1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2022
ms.locfileid: "68575799"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Diseñe la aplicación personal para Microsoft Teams

Una aplicación personal puede ser un bot, un área de trabajo privada o ambas. A veces funciona como un lugar para crear o ver contenido. Otras veces, ofrece al usuario una vista general de todo lo que es suyo cuando la aplicación se ha configurado como una pestaña en varios canales.

A modo de guía en el diseño de su aplicación, a continuación se describe e ilustra cómo pueden los usuarios agregar, usar y administrar bots en Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

En el kit de interfaz de usuario de Microsoft Teams, encontrará instrucciones completas de diseño de pestaña, que incluyen elementos que puede usar y modificar como quiera. El kit de interfaz de usuario también tiene temas esenciales, como la accesibilidad y el tamaño dinámico que no se tratan aquí.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Agregar una aplicación personal

Los usuarios pueden agregar una aplicación personal desde el control flotante de la tienda o la aplicación de Teams seleccionando el icono **Más** en el lado izquierdo de Teams (que se muestra en el ejemplo siguiente).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="En el ejemplo se muestra cómo agregar una aplicación personal desde el control flotante de la aplicación.":::

## <a name="use-a-personal-app-private-workspace"></a>Uso de una aplicación personal (área de trabajo privada)

Con un área de trabajo privada, los usuarios pueden ver el contenido de la aplicación que es importante para ellos en una ubicación central sin salir de Teams.

(Nota de implementación: el área de trabajo privada se basa en la funcionalidad de [*pestaña personal*](../../tabs/how-to/create-personal-tab.md)).

### <a name="anatomy-personal-app-private-workspace"></a>Anatomía: Aplicación personal (área de trabajo privada)

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de la pestaña personal.":::

|Contador|Descripción|
|----------|-----------|
|A|**Atribución de la aplicación**: nombre de la aplicación.|
|N|**Pestañas**: navegación en la aplicación personal.|
|C|**Más menú**: incluye otras opciones e información de la aplicación.|
|D|**Navegación principal**: proporciona navegación a otras características principales de la aplicación de Teams.|

#### <a name="configure-and-add-multiple-actions-in-navbar"></a>**Configuración y adición de varias acciones en NavBar**

Puede agregar varias acciones a la barra de navegación superior derecha y crear un menú de desbordamiento para acciones adicionales en una aplicación.

>[!NOTE]
> Se pueden agregar un máximo de cinco acciones en la barra de navegación, incluido el menú de desbordamiento.

:::image type="content" source="../../assets/images/overflow-menu-and-multiple-actionsoptions.png" alt-text="La captura de pantalla es un ejemplo que describe el menú NavBar y Overflow.":::

Para **configurar y agregar varias acciones en NavBar**, llame a [setNavBarMenu](/javascript/api/@microsoft/teams-js/microsoftteams.menus?view=msteams-client-js-1.12.1&preserve-view=true) API. y agregue la `displayMode enum` propiedad a `MenuItem`. `displayMode enum` define cómo aparece un menú en la barra de navegación. El valor predeterminado de `displayMode enum` se establece en `ifRoom`.

En función de los requisitos y el espacio disponible en la barra de navegación, establezca `displayMode enum` teniendo en cuenta uno de los siguientes.

* Si hay espacio, establezca `ifRoom = 0` para colocar un elemento en la barra de navegación.
* Si no hay espacio, establezca `overflowOnly = 1`, para que ese elemento siempre se coloque en el menú de desbordamiento de la barra de navegación, pero no en la barra de navegación.

A continuación se muestra un ejemplo de configuración de la barra de navegación con un menú de desbordamiento para varias acciones:

```typescript
const menuItems = [item1, item2, item3, item4, item5]
microsoftTeams.menus.setNavBarMenu(menuItems, (id: string) => {
  output(`Clicked ${id}`)
  return true;
})
```

> [!NOTE]
> La `setNavBarMenu` API no controla el botón **Actualizar** . Aparece de forma predeterminada.

:::image type="content" source="../../assets/images/overflow-menu-and-multple-actions.png" alt-text="La captura de pantalla es un ejemplo que muestra la barra de navegación y varias acciones en un menú de desbordamiento.":::

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de la pestaña personal.":::

|Contador|Descripción|
|----------|-----------|
|A|**Pestañas**: navegación en la aplicación personal.|
|1|**webview**: muestra el contenido de la aplicación.|

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="En este ejemplo se muestra la anatomía del componente de la pestaña personal.":::

|Contador|Descripción|
|----------|-----------|
|A|**Atribución de aplicaciones**: el logotipo y el nombre de la aplicación.|
|N|**Pestañas**: navegación en la aplicación personal.|
|C|**Vista emergente**: inserta el contenido de la aplicación desde una ventana primaria en una ventana secundaria independiente.|
|D|**Más menú**: incluye otras opciones e información de la aplicación. (También puede convertir **Configuración** en una pestaña).|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="En este ejemplo se muestra la anatomía estructural de la pestaña personal.":::

|Contador|Descripción|
|----------|-----------|
|A|**Pestañas**: navegación en la aplicación personal.|
|1|**iframe**: muestra el contenido de la aplicación.|

### <a name="design-with-ui-templates-and-advanced-components"></a>Diseñar una pestaña con plantillas de interfaz de usuario y componentes avanzados

Use una de las siguientes plantillas y componentes de Teams para ayudar a diseñar la experiencia de la pestaña:

* [Lista](../../concepts/design/design-teams-app-ui-templates.md#list): Las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o en elementos individuales.
* [Panel de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): un panel de tareas, a veces denominado panel kanban o carril, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.
* [Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.
* [Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): Los formularios son para recopilar, validar y enviar el input del usuario de forma estructurada.
* [Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): La plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.
* [Navegación izquierda](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav): el componente de navegación izquierda puede ayudar si la pestaña requiere algo de navegación. En general, debe usar lo mínimo posible la navegación por pestañas.

## <a name="use-a-personal-app-bot"></a>Uso de una aplicación personal (bot)

Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on artboard). Users interact with the bot in a tab you specify.

### <a name="anatomy-personal-app-bot"></a>Anatomía: Aplicación personal (bot)

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de bot personal.":::

|Contador|Descripción|
|----------|-----------|
|A|**Punto de entrada del bot**: punto de entrada para que los usuarios accedan a la característica de bot en la aplicación personal.|
|N|**Botón Atrás**: devuelve a los usuarios al área de trabajo privada.|
|C|**Mensaje del bot**: los bots suelen enviar mensajes y notificaciones en forma de tarjeta (por ejemplo, una tarjeta adaptable).|
|D|**Cuadro Redactar**: campo de entrada para enviar mensajes al bot.|

#### <a name="configure-back-button"></a>Botón Configurar atrás

Al seleccionar el botón Atrás en una aplicación de Teams, volverá a la plataforma teams sin navegar dentro de la aplicación.

Para navegar dentro de la aplicación, configure el botón Atrás para que, al seleccionar el botón Atrás, pueda volver a los pasos anteriores y navegar dentro de la aplicación.

Para **configurar el botón Atrás**, llame a [registerBackButtonHandler](/javascript/api/@microsoft/teams-js/pages.backstack?view=msteams-client-js-latest&preserve-view=true&branch=pr-en-us-6801&preserve-view=true) API, que controla la funcionalidad del botón Atrás en función de una de las condiciones siguientes:

* Cuando `registerBackButtonHandler` se establece en `false`, el SDK de JavaScript llama a la `navigateBack` API y la plataforma teams controla el botón Atrás.
* Cuando `registerBackButtonHandler` se establece en `true`, la aplicación controla la funcionalidad del botón Atrás (puede volver a los pasos anteriores y navegar dentro de la aplicación) y la plataforma Teams no realiza ninguna acción adicional.

A continuación se muestra un ejemplo de configuración del botón Atrás:

```typescript
microsoftTeams.registerBackButtonHandler(() => {
  const selectOption = registerBackReturn.options[registerBackReturn.selectedIndex].value
  var isHandled = false
  if (selectOption == 'true') 
    isHandled = true;
  output(`onBack isHandled ${isHandled}`)
  return isHandled;
})
```

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de bot personal.":::

|Contador|Descripción|
|----------|-----------|
|A|**Pestaña Bot**: por ejemplo, incluya una pestaña **Chat** para acceder a las conversaciones y notificaciones del bot.|
|N|**Mensaje del bot**: los bots suelen enviar mensajes y notificaciones en forma de tarjeta (por ejemplo, una tarjeta adaptable).|
|C|**Cuadro Redactar**: campo de entrada para enviar mensajes al bot.|

## <a name="manage-a-personal-tab"></a>Administrar una pestaña personal

En el lado izquierdo de Teams, los usuarios pueden hacer clic con el botón derecho en la aplicación personal para anclar, quitar y configurar otras opciones de aplicación.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="En el ejemplo se muestran las opciones para administrar una aplicación personal.":::

## <a name="best-practices"></a>Procedimientos recomendados

Use estas recomendaciones para crear una experiencia de aplicación de calidad.

### <a name="tab-priority"></a>Prioridad de pestaña

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>Qué sí hacer: mostrar el contenido más relevante en la primera pestaña

Con el tamaño dinámico, las pestañas de la derecha pueden truncarse u ocultarse.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="En el ejemplo se muestra una aplicación personal que muestra el contenido más relevante de la primera pestaña.":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>Qué no hacer: comenzar con contenido o metadatos secundarios

Al igual que una aplicación web estándar, la navegación por pestañas debe progresar en un orden que ayude a dar sentido a las características principales de la aplicación.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="En el ejemplo se muestra una aplicación personal a la izquierda con contenido secundario o metadatos.":::

### <a name="tab-hierarchy"></a>Jerarquía de pestañas

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>Qué sí hacer: las pestañas deben ser de la misma jerarquía y representar las páginas clave de la aplicación

Las pestañas deben clasificar las características principales y el contenido de la aplicación. Con el tamaño dinámico, el contenido de la derecha pueden truncarse u ocultarse.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="En el ejemplo se muestra una aplicación personal con pestañas de la misma jerarquía.":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>Qué no hacer: incluir distintos niveles de jerarquía

El contenido debe progresar en un orden lógico que ayude a los usuarios a entenderlo. Si tiene dos pestañas estrechamente relacionadas, considere la posibilidad de combinarlas en una sola pestaña.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="En el ejemplo se muestra una aplicación personal con distintos niveles de jerarquía.":::

### <a name="first-run-experience"></a>Experiencia de primera ejecución

#### <a name="do-include-a-first-run-experience"></a>Qué sí hacer: incluir una experiencia de primera ejecución

Debería haber al menos una pantalla de bienvenida la primera vez que use una aplicación personal. En el caso de los bots, describa lo que el bot puede hacer y proporcione acciones rápidas, como un botón de inicio de sesión.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="En el ejemplo se muestra qué hacer durante una experiencia de primera ejecución de una aplicación personal.":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Otro ejemplo muestra qué hacer durante una experiencia de primera ejecución de una aplicación personal.":::

#### <a name="dont-start-with-a-blank-screen"></a>Qué no hacer: comenzar con la pantalla en blanco

Es posible que los usuarios se confundan si no se muestra nada la primera vez que ejecutan la aplicación.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="En el ejemplo se muestra lo que no se debe hacer durante una experiencia de primera ejecución de una aplicación personal.":::

### <a name="personalized-content"></a>Contenido personalizado

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>Qué sí hacer: agregar contenido de la aplicación relevante para un usuario

Tanto si se trata de una pestaña personal como de un bot, muestre contenido relacionado solo con la actividad de un usuario en la aplicación.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="Ejemplo que muestra qué hacer con una aplicación personal y contenido personalizado.":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Otro ejemplo que muestra qué hacer con una aplicación personal y contenido personalizado.":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>Qué no hacer: mostrar contenido no relacionado o demasiado amplio

En contextos personales, no muestre contenido para los equipos de los que un usuario no forma parte. El contenido del bot personal debe centrarse en la persona, no en un grupo.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="En el ejemplo se muestra lo que no se debe hacer con una aplicación personal y contenido personalizado.":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Otro ejemplo que muestra qué no hacer con una aplicación personal y contenido personalizado.":::

### <a name="complex-app-features"></a>Características complejas de la aplicación

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>Qué sí hacer: permitir que los usuarios accedan a características complejas en un explorador

La aplicación debe centrarse en las tareas principales de Teams, pero puede ver la aplicación completa e independiente en un explorador.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="En el ejemplo se muestra cómo controlar características de aplicaciones complejas con una aplicación personal.":::

#### <a name="dont-include-your-entire-app"></a>Qué no hacer: incluir toda la aplicación

A menos que haya creado la aplicación específicamente para Teams, probablemente tenga características que no tienen sentido en una herramienta de colaboración.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="En el ejemplo se muestra cómo no controlar características de aplicaciones complejas con una aplicación personal.":::

## <a name="see-also"></a>Consulte también

Estas otras directrices de diseño pueden ayudar en función del ámbito de la aplicación personal:

* [Diseño de la pestaña](../../tabs/design/tabs.md)
* [Cómo diseñar su bot](../../bots/design/bots.md)
* [registerBackButtonHandler](/javascript/api/@microsoft/teams-js/pages.backstack?view=msteams-client-js-latest&preserve-view=true&branch=pr-en-us-6801&preserve-view=true)
* [Enumeración DisplayMode](/javascript/api/@microsoft/teams-js/menus.displaymode?view=msteams-client-js-latest&preserve-view=true)
