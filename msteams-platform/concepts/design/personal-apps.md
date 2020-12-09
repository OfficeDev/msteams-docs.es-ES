---
title: Diseño de la aplicación personal
description: Obtenga información sobre cómo diseñar una aplicación personal de Microsoft Teams y obtener el kit de interfaz de usuario de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 971071be9f345815f5461646d7970efdf05fd5c4
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605023"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Diseño de la aplicación personal para Microsoft Teams

Una aplicación personal puede ser un bot, un área de trabajo privada o ambos. A veces, funciona como un espacio para crear o ver contenido, otras veces ofrece al usuario una vista de pájaro de todo lo que es cuando la aplicación se ha configurado como una pestaña en varios canales.

Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar aplicaciones personales en Microsoft Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit de IU de Microsoft Teams

Puede encontrar instrucciones completas para el diseño de aplicaciones personales, incluidos los elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams. El kit de UI también tiene temas esenciales, como la accesibilidad y el tamaño de respuesta, que no se cubren aquí.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Agregar una aplicación personal

Puede Agregar una aplicación personal desde el almacén de Microsoft Teams (AppSource) o desde el flotante de aplicaciones seleccionando el icono **más** en el lado izquierdo de Teams (que se muestra en el ejemplo siguiente).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="En el ejemplo se muestra cómo agregar una aplicación personal desde el control flotante de la aplicación." border="false":::

## <a name="use-a-personal-app-private-workspace"></a>Usar una aplicación personal (área de trabajo privada)

Con un área de trabajo privada, puede ver el contenido de la aplicación que es significativo para usted en una ubicación central sin salir de Microsoft Teams.

(Nota de implementación: el área de trabajo privada se basa en la capacidad de la [*pestaña personal*](../../build-your-first-app/build-personal-tab.md) ).

### <a name="anatomy-personal-app-private-workspace"></a>Anatomía: aplicación personal (área de trabajo privada)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="Ejemplo muestra anatomía de componentes de la pestaña personal." border="false":::

|Counter|Descripción|
|----------|-----------|
|A|**Atribución de aplicaciones**: el logotipo y el nombre de la aplicación.|
|B|**Pestañas**: proporciona navegación para su aplicación personal. Por ejemplo, incluya una ficha **acerca de** o **ayuda** .|
|C|**Vista emergente**: inserta el contenido de la aplicación desde una ventana primaria en una ventana secundaria independiente.|
|D|**Menú más**: incluye información adicional de la aplicación y opciones. (También puede hacer que la **configuración** sea una pestaña.)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="Ejemplo muestra anatomía estructural de la pestaña personal." border="false":::

|Counter|Descripción|
|----------|-----------|
|A|**Pestañas**: proporciona navegación para su aplicación personal.|
|1 |**iframe**: muestra el contenido de la aplicación.|

### <a name="designing-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Use una de las siguientes plantillas de interfaz de usuario de Microsoft Teams para ayudar a diseñar su pestaña personal:

* [List](../../concepts/design/design-teams-app-ui-templates.md#list): lists puede mostrar elementos relacionados en un formato que se pueda analizar y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.
* [Panel de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): un panel de tareas, a veces denominado tablero Kanban o carriles de nadar, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o vales.
* [Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre datos o contenido.
* [Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.
* [Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc.
* Panel de [navegación izquierdo](../../concepts/design/design-teams-app-ui-templates.md#left-nav): la plantilla de navegación izquierda puede servir de ayuda si la pestaña requiere la navegación. En general, debe mantener al mínimo la navegación por tabulaciones.

## <a name="use-a-personal-app-bot"></a>Usar una aplicación personal (bot)

Las aplicaciones personales pueden incluir un bot para las conversaciones de uno en uno y las notificaciones privadas (por ejemplo, cuando un compañero publica un Comentario en la mesa de mesas). El bot está disponible en la ficha que especifique.

### <a name="anatomy-personal-app-bot"></a>Anatomía: aplicación personal (bot)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="Ejemplo que muestra la anatomía del componente de bot personal." border="false":::

|Counter|Descripción|
|----------|-----------|
|A|**Ficha bot**: por ejemplo, incluye una ficha **chat** para tener acceso a conversaciones y notificaciones de bot.|
|B|**Mensaje de bot**: los bots suelen enviar mensajes y notificaciones en forma de una tarjeta (como una tarjeta adaptable).|
|C|**Cuadro de redacción**: campo de entrada para enviar mensajes al bot.|

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="tab-priority"></a>Prioridad de la pestaña

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>Do: mostrar el contenido más relevante en la primera pestaña

Con el tamaño de capacidad de respuesta, las pestañas de la derecha se truncan o desaesn.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>No: lidere con contenido o metadatos secundarios

Al igual que una aplicación web estándar, la navegación por pestaña debe progresar en un orden que ayude a comprender las características principales de la aplicación.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

### <a name="tab-hierarchy"></a>Jerarquía de pestañas

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>Do: las pestañas deben ser de la misma jerarquía y representan páginas de aplicaciones clave

Las pestañas deben categorizar el contenido y las características principales de la aplicación. Con el tamaño de capacidad de respuesta, el contenido de la derecha puede truncarse o quedar fuera de la vista.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>No: incluir distintos niveles de jerarquía

El contenido debe progresar en un orden lógico que ayude a los usuarios a tener sentido. Si tiene dos pestañas estrechamente relacionadas, considere la posibilidad de combinarlas en una pestaña.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

### <a name="first-run-experience"></a>Experiencia de primera ejecución

#### <a name="do-include-a-first-run-experience"></a>Do: incluir una experiencia de primera ejecución

Debe haber al menos una pantalla de bienvenida la primera vez que use una aplicación personal. Para los bots, describa lo que puede hacer el bot y proporcione acciones rápidas, como un botón de inicio de sesión.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>No: empezar con una pantalla en blanco

Los usuarios podrían confundirse si no aparece nada la primera vez que ejecutan la aplicación.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

### <a name="personalized-content"></a>Contenido personalizado

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>Hacer: agregar contenido de aplicaciones relevante para un usuario

Ya sea una pestaña personal o un bot, mostrar contenido relacionado solo con la actividad del usuario en la aplicación.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>No: mostrar contenido no relacionado o demasiado amplio

En los contextos personales, no se muestra el contenido de los equipos de los que no forma parte el usuario. El contenido del bot personal debe centrarse en el individuo (no en un grupo).

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

### <a name="complex-app-features"></a>Características complejas de la aplicación

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>Do: permitir a los usuarios el acceso a características complejas en un explorador

La aplicación debe centrarse en las tareas principales de Microsoft Teams, pero todavía puede ver la aplicación independiente completa en un explorador.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

#### <a name="dont-include-your-entire-app"></a>No: incluir toda la aplicación

A menos que haya creado la aplicación específicamente para Teams, probablemente tiene características que no tienen sentido en una herramienta de colaboración.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="El ejemplo muestra una práctica recomendada de la aplicación personal." border="false":::

## <a name="manage-a-personal-tab"></a>Administrar una pestaña personal

En la parte izquierda de Microsoft Teams, los usuarios pueden hacer clic con el botón derecho en la aplicación personal para anclar, quitar y configurar otras opciones de la aplicación.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="Ejemplo muestra opciones para administrar una aplicación personal." border="false":::

## <a name="learn-more"></a>Más información

Estas otras instrucciones de diseño pueden ayudarle en función del ámbito de su aplicación personal:

* [Diseño de la pestaña](../../tabs/design/tabs.md)
* [Diseño de bot](../../bots/design/bots.md)

## <a name="validate-your-design"></a>Validar el diseño

Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.

> [!div class="nextstepaction"]
> [Comprobar las instrucciones de validación del diseño](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
