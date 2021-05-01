---
title: Diseño de su aplicación personal
description: Aprende a diseñar una aplicación Teams personal y obtener el kit Microsoft Teams interfaz de usuario.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: b3f08c39a7900b80fb46d167fae8d9e8bdbcc574
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101558"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Diseñar tu aplicación personal para Microsoft Teams

Una aplicación personal puede ser un bot, un área de trabajo privada o ambos. A veces funciona como un lugar para crear o ver contenido, otras veces ofrece al usuario una vista visual de todo lo que es suyo cuando la aplicación se ha configurado como una pestaña en varios canales.

Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo las personas pueden agregar, usar y administrar aplicaciones personales en Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Puedes encontrar instrucciones completas de diseño de aplicaciones personales, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario. El kit de interfaz de usuario también tiene temas esenciales, como la accesibilidad y el tamaño dinámico que no se tratan aquí.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Agregar una aplicación personal

Puedes agregar una aplicación personal desde la tienda Teams (AppSource) o el  menú desplegable de la aplicación seleccionando el icono Más en el lado izquierdo de Teams (que se muestra en el ejemplo siguiente).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="En el ejemplo se muestra cómo agregar una aplicación personal desde el menú desplegable de la aplicación." border="false":::

## <a name="use-a-personal-app-private-workspace"></a>Usar una aplicación personal (área de trabajo privada)

Con un área de trabajo privada, puedes ver contenido de la aplicación que sea significativo para ti en una ubicación central sin salir de Teams.

(Nota de implementación: el área de trabajo privada se basa en la funcionalidad [*de tabulación*](../../build-your-first-app/build-personal-tab.md) personal).

### <a name="anatomy-personal-app-private-workspace"></a>Anatomía: aplicación personal (área de trabajo privada)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de la pestaña personal." border="false":::

|Contador|Descripción|
|----------|-----------|
|A|**Atribución de la aplicación:** el logotipo y el nombre de la aplicación.|
|B|**Pestañas:** proporciona navegación para tu aplicación personal. Por ejemplo, incluya una **pestaña Acerca o** **Ayuda.**|
|C|**Vista emergente:** inserta el contenido de la aplicación desde una ventana primaria a una ventana secundaria independiente.|
|D|**Más menú:** incluye información y opciones adicionales de la aplicación. (También puede crear una **Configuración** una pestaña).|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="En el ejemplo se muestra la anatomía estructural de la pestaña personal." border="false":::

|Contador|Descripción|
|----------|-----------|
|A|**Pestañas:** proporciona navegación para tu aplicación personal.|
|1|**iframe:** muestra el contenido de la aplicación.|

### <a name="designing-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Usa una de las siguientes plantillas Teams interfaz de usuario para ayudar a diseñar tu pestaña personal:

* [Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.
* [Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.
* [Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.
* [Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.
* [Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.
* [Navegación izquierda:](../../concepts/design/design-teams-app-ui-templates.md#left-nav)la plantilla de navegación izquierda puede ayudar si la pestaña requiere algo de navegación. En general, debe mantener la navegación por pestañas al mínimo.

## <a name="use-a-personal-app-bot"></a>Usar una aplicación personal (bot)

Las aplicaciones personales pueden incluir un bot para conversaciones uno a uno y notificaciones privadas (por ejemplo, cuando un compañero publica un comentario en la mesa de trabajo). El bot está disponible en una pestaña especificada.

### <a name="anatomy-personal-app-bot"></a>Anatomía: aplicación personal (bot)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="En el ejemplo se muestra la anatomía del componente de bot personal." border="false":::

|Contador|Descripción|
|----------|-----------|
|A|**Ficha Bot:** Por ejemplo, incluya una **pestaña Chat** para obtener acceso a las conversaciones y notificaciones del bot.|
|B|**Mensaje de bot:** los bots suelen enviar mensajes y notificaciones en forma de tarjeta (como una tarjeta adaptable).|
|C|**Cuadro Redacción:** campo de entrada para enviar mensajes al bot.|

## <a name="manage-a-personal-tab"></a>Administrar una pestaña personal

En el lado izquierdo de Teams, los usuarios pueden hacer clic con el botón secundario en la aplicación personal para anclar, quitar y configurar otras opciones de la aplicación.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="En el ejemplo se muestran las opciones para administrar una aplicación personal." border="false":::

## <a name="best-practices"></a>Procedimientos recomendados

Usa estas recomendaciones para crear una experiencia de aplicación de calidad.

### <a name="tab-priority"></a>Prioridad de tabulación

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>Hacer: mostrar el contenido más relevante en la primera pestaña

Con el tamaño dinámico, las pestañas de la derecha pueden truncarse o quedar fuera de la vista.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="En el ejemplo se muestra una aplicación personal que muestra el contenido más relevante en la primera pestaña." border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>Don't: Lead with secondary content or metadata

Al igual que una aplicación web estándar, la navegación por pestañas debe avanzar en un orden que ayude a dar sentido a las características principales de la aplicación.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="En el ejemplo se muestra una aplicación personal que lleva contenido o metadatos secundarios." border="false":::

### <a name="tab-hierarchy"></a>Jerarquía de tabulaciones

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>Hacer: las pestañas deben ser de igual jerarquía y representar páginas clave de la aplicación

Las pestañas deben clasificar las características y el contenido principales de la aplicación. Con el tamaño dinámico, el contenido de la derecha puede truncarse o quedar fuera de la vista.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="En el ejemplo se muestra una aplicación personal con pestañas de igual jerarquía." border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>No: incluir diferentes niveles de jerarquía

El contenido debe avanzar en un orden lógico que ayude a los usuarios a entenderlo. Si tiene dos pestañas estrechamente relacionadas, considere la posibilidad de combinarlas en una pestaña.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="En el ejemplo se muestra una aplicación personal con diferentes niveles de jerarquía." border="false":::

### <a name="first-run-experience"></a>Experiencia de primera ejecución

#### <a name="do-include-a-first-run-experience"></a>Do: Include a first-run experience

Debería haber al menos una pantalla de bienvenida la primera vez que uses una aplicación personal. En el caso de los bots, describa lo que el bot puede hacer y proporcione acciones rápidas, como un botón de inicio de sesión.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="En el ejemplo se muestra qué hacer durante la primera ejecución de una aplicación personal." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Otro ejemplo muestra qué hacer durante la primera ejecución de una aplicación personal." border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>Don't: Start with a blank screen

Es posible que los usuarios se confundan si no se muestra nada la primera vez que ejecutan la aplicación.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="En el ejemplo se muestra lo que no se debe hacer durante la primera ejecución de una aplicación personal." border="false":::

### <a name="personalized-content"></a>Contenido personalizado

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>Hacer: agregar contenido de aplicación relevante para un usuario

Tanto si se trata de una pestaña personal como de un bot, muestra contenido relacionado solo con la actividad de un usuario en la aplicación.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="En el ejemplo se muestra qué hacer con una aplicación personal y contenido personalizado." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Otro ejemplo muestra qué hacer con una aplicación personal y contenido personalizado." border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>No: mostrar contenido demasiado amplio o no relacionado

En contextos personales, no muestre contenido para equipos de los que un usuario no forma parte. El contenido del bot personal debe centrarse en el individuo, no en un grupo.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="En el ejemplo se muestra qué no hacer con una aplicación personal y contenido personalizado." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Otro ejemplo muestra qué no hacer con una aplicación personal y contenido personalizado." border="false":::

### <a name="complex-app-features"></a>Características complejas de la aplicación

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>Hacer: permitir que los usuarios accedan a características complejas en un explorador

La aplicación debe centrarse en las tareas principales Teams, pero aún puedes ver la aplicación completa e independiente en un explorador.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="En el ejemplo se muestra cómo controlar las características complejas de la aplicación con una aplicación personal." border="false":::

#### <a name="dont-include-your-entire-app"></a>No: incluir toda la aplicación

A menos que creaste la aplicación específicamente para Teams, probablemente tienes características que no tienen sentido en una herramienta de colaboración.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="En el ejemplo se muestra cómo no controlar las características complejas de la aplicación con una aplicación personal." border="false":::

## <a name="see-also"></a>Vea también

Estas otras directrices de diseño pueden ayudar en función del ámbito de la aplicación personal:

* [Diseño de la pestaña](../../tabs/design/tabs.md)
* [Diseño del bot](../../bots/design/bots.md)
