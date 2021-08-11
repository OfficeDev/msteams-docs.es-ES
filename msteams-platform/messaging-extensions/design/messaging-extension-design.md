---
title: Diseño de la extensión de mensajería
description: Obtenga información sobre cómo diseñar una extensión de mensajería de Teams y obtener el kit de interfaz de usuario de Microsoft Teams.
keywords: teams diseño instrucciones referencia extensiones de mensajería sugerencias procedimientos recomendados
author: heath-hamilton
localization_priority: Priority
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: 63bdbd0afbf2d0c4a3b7506330fb56e463a10169379c0674dd68496e3cc8de19
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57703376"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>Diseño de la extensión de mensajería de Microsoft Teams

Las extensiones de mensajería son métodos abreviados para insertar contenido de la aplicación o realizar una acción en un mensaje sin salir de la conversación.
A modo de guía en el diseño de su aplicación, a continuación, se describe e ilustra cómo pueden los usuarios agregar, usar y administrar las extensiones de mensajería en Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit de interfaz de usuario de Microsoft Teams

En el kit de interfaz de usuario de Microsoft Teams, encontrará instrucciones completas de diseño para la extensión de mensajería, que incluyen elementos que puede usar y modificar como quiera.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>Agregar una extensión de mensajería

Puede agregar una extensión de mensajería en los siguientes contextos de Teams:

* Desde la tienda de Teams.
* En un canal, chat o reunión (antes, durante y después) cerca del cuadro de redacción. Vale la pena recalcar que, si agrega una extensión de mensajería en uno de estos lugares, solo usted podrá usarla en ese contexto.

En el ejemplo siguiente, se muestra cómo agregar una extensión de mensajería en un canal:

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="En el ejemplo, se muestra cómo agregar una extensión de mensajería cerca del cuadro de redacción en un canal." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="En el ejemplo, se muestra cómo agregar una extensión de mensajería cerca del cuadro de redacción en un dispositivo móvil." border="false":::

---

## <a name="set-up-a-messaging-extension"></a>Configurar una extensión de mensajería

La autenticación no es obligatoria, pero si la aplicación es algo parecida a una herramienta de seguimiento de vales, es posible que necesite que los usuarios inicien sesión para usar la extensión de mensajería.

Con el fin de mantener la coherencia entre las aplicaciones de Teams, no es posible personalizar la pantalla de inicio de sesión. Si usa la autenticación de inicio de sesión único (SSO), los usuarios iniciarán sesión automáticamente.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="En el ejemplo, se muestra la pantalla de configuración de la extensión de mensajería con un botón de inicio de sesión." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="En el ejemplo, se muestra la pantalla de configuración de la extensión de mensajería con un botón de inicio de sesión en dispositivos móviles." border="false":::

---

## <a name="types-of-messaging-extensions"></a>Tipos de extensiones de mensajería

Las extensiones de mensajería pueden tener comandos de búsqueda, comandos de acción o ambos. Los comandos dependen de las características de su aplicación y de cómo encajan en los casos de uso de Teams.

### <a name="search-commands"></a>Comandos de búsqueda

Con los comandos de búsqueda, los usuarios pueden usar la extensión de mensajería para buscar rápidamente contenido externo e insertarlo en un mensaje. Los comandos de búsqueda suelen estar disponibles en el cuadro de redacción. Por ejemplo, puede iniciar o agregar contenido a una discusión al compartir algún contenido sin necesidad de salir de Teams.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="En el ejemplo, se muestra una extensión de mensajería basada en la búsqueda que se ha iniciado desde el cuadro de redacción." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="En el ejemplo, se muestra una extensión de mensajería basada en la búsqueda que se ha iniciado desde el cuadro de redacción en dispositivos móviles." border="false":::

---

#### <a name="compose-box-layout-options"></a>Opciones de diseño del cuadro de redacción

Tiene algunas opciones para mostrar los resultados de la búsqueda de la extensión de mensajería, incluidas las[vistas de lista y cuadrícula](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Ilustraciones que muestran las opciones de diseño para los resultados de la búsqueda de la extensión de mensajería." border="false":::

### <a name="action-commands"></a>Comandos de acción

Los comandos de acción permiten que los usuarios desencadenen acciones y procesen solicitudes en servicios externos dentro de Teams. Por ejemplo, si su aplicación realiza un seguimiento de pedidos, un usuario podría crear un nuevo pedido utilizando el contenido del mensaje de un compañero directamente desde su chat.

Las extensiones de mensajería basadas en acciones suelen requerir que los usuarios completen un formulario o algún otro tipo de configuración dentro de una ventana modal. Puede crear estas experiencias con los [módulos de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).

## <a name="open-a-messaging-extension"></a>Abrir una extensión de mensajería

El cuadro de redacción y los mensajes o publicaciones son los contextos principales en los que los usuarios usan extensiones de mensajería.

### <a name="from-the-compose-box"></a>Desde el cuadro de redacción

Una vez agregada, los usuarios pueden abrir la extensión de mensajería seleccionando el icono de la aplicación debajo del cuadro de redacción. En estos ejemplos, la extensión tiene comandos de búsqueda y acción.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="En el ejemplo, se muestra cómo abrir una extensión de mensajería desde el cuadro de redacción." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="En el ejemplo, se muestra cómo abrir una extensión de mensajería desde el cuadro de redacción en un dispositivo móvil." border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a>Desde un mensaje de chat o publicación de canal

Una vez agregado, los usuarios pueden seleccionar el icono **Más** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: en el mensaje de chat o en la publicación del canal para buscar los comandos de acción de la extensión. La extensión puede aparecer en **Más acciones** en función de su uso.

> [!NOTE]
> La compatibilidad con más acciones desde un mensaje de chat o publicación del canal no está disponible en la plataforma móvil de Microsoft Teams. 

#### <a name="chat-message"></a>Mensaje de chat

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="En el ejemplo, se muestra cómo abrir una extensión de mensajería desde un mensaje de chat." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="En el ejemplo, se muestra cómo abrir una extensión de mensajería desde una publicación de chat en dispositivos móviles." border="false":::

---
':::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
':::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
---

## <a name="use-a-messaging-extension"></a>Usar una extensión de mensajería

En los escenarios siguientes, se muestran las principales formas en que los usuarios usan las extensiones de mensajería.

### <a name="insert-content-into-a-message"></a>Insertar contenido en un mensaje

**1. Seleccione una extensión de mensajería**. Los usuarios pueden buscar el contenido que quieran compartir desde el cuadro de redacción.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="En el ejemplo, se muestra un usuario que busca contenido para insertar desde el cuadro de redacción." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="En el ejemplo, se muestra un usuario que busca contenido para insertar desde el cuadro de redacción en dispositivos móviles." border="false":::

---

**2. Inserte el contenido**. Una vez publicado, otros usuarios pueden responder o seleccionar el contenido para ver más información en la aplicación.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="En el ejemplo, se muestra un usuario publicando contenido en una conversación de canal." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="En el ejemplo, se muestra un usuario publicando contenido en una conversación de canal en un dispositivo móvil." border="false":::

---

### <a name="take-action-on-a-message"></a>Realizar una acción en un mensaje

**1. Seleccione una extensión de mensajería**. La aplicación puede incluir uno o varios comandos de acción.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="En el ejemplo, se muestra un usuario que selecciona un comando de acción de la extensión de mensajería." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="En el ejemplo, se muestra un usuario que selecciona un comando de acción de la extensión de mensajería en un dispositivo móvil." border="false":::

---

**2. Complete la acción**. Su aplicación puede recibir y procesar cualquier contenido o dato enviado por la acción del mensaje. Esto permite que los usuarios permanezcan en su conversación y, en el ejemplo siguiente, que no se preocupen por tener que escribir información directamente en la aplicación.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Ejemplo sobre cómo realizar acciones en un mensaje." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="Ejemplo sobre cómo realizar acciones en un mensaje en dispositivos móviles." border="false":::

---

### <a name="preview-links"></a>Vínculos de vista previa

Las extensiones de mensajería también permiten insertar "rich links" desde una dirección URL reconocida en un mensaje (esta funcionalidad se denomina ["link unfurling"](../../messaging-extensions/how-to/link-unfurling.md)).

**1. Pegue un vínculo reconocido** en el cuadro de redacción.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="En el ejemplo, se muestra un usuario pegando un vínculo en el cuadro de diálogo." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="En el ejemplo, se muestra un usuario pegando un vínculo en el cuadro de texto en un dispositivo móvil." border="false":::

---

**2. Inserte el contenido**. Si la aplicación reconoce la dirección URL en el cuadro de redacción, esta representará el vínculo como una tarjeta que proporciona una vista previa completa del contenido web. (Consulte [Instrucciones de diseño de tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md) para obtener más información).

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="En el ejemplo, se muestra cómo la dirección URL, desde su reconocimiento por parte de la aplicación, incluye contenido enriquecido en el cuadro de redacción." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="En el ejemplo, se muestra cómo la dirección URL, desde su reconocimiento por parte de la aplicación, incluye contenido enriquecido en el cuadro de redacción en un dispositivo móvil." border="false":::

---

## <a name="manage-a-messaging-extension"></a>Administrar una extensión de mensajería

Al hacer clic con el botón derecho en su icono, los usuarios pueden anclar, quitar o configurar la extensión de mensajería.

## <a name="anatomy"></a>Anatomía

### <a name="messaging-extension-in-the-compose-box"></a>Extensión de mensajería en el cuadro de redacción

El ejemplo siguiente es una extensión de mensajería abierta desde el cuadro de redacción.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una extensión de mensajería en el cuadro de redacción." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Logotipo de la aplicación**: icono de color del logotipo de la aplicación.|
|2|**Nombre de la aplicación**: nombre completo de la aplicación.|
|3|**Icono del menú de comandos de acción (opcional)**: abre una lista de comandos de acción para la extensión de mensajería (si especifica alguno).
|4|**Cuadro de búsqueda**: permite que los usuarios busquen contenido de la aplicación que quieran insertar.|
|5|**Menú de pestaña (opcional)**: proporciona varias categorías de contenido.|
|6|**Menú de comandos de acción (opcional)**: muestra la lista de comandos de acción (si especifica alguno).|
|7|**Contenido de la aplicación**: principalmente para mostrar los resultados de la búsqueda. El ejemplo siguiente usa el diseño de lista (el diseño de cuadrícula es otra opción).|
|8|**Logotipo de la aplicación**: icono de esquema del logotipo de la aplicación.|

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="Ilustración en la que se muestra la anatomía de la interfaz de usuario de una extensión de mensajería en el cuadro de redacción en un dispositivo móvil." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Nombre de la aplicación**: nombre completo de la aplicación.|
|2|**Icono del menú de comandos de acción (opcional)**: abre una lista de comandos de acción para la extensión de mensajería (si especifica alguno).
|3|**Cuadro de búsqueda**: permite que los usuarios busquen contenido de la aplicación que quieran insertar.|
|4|**Menú de pestaña (opcional)**: proporciona varias categorías de contenido.|
|5|**Menú de comandos de acción (opcional)**: muestra la lista de comandos de acción (si especifica alguno).|
|6|**Contenido de la aplicación**: principalmente para mostrar los resultados de la búsqueda.|

---

### <a name="messaging-extension-management-menu"></a>Menú de administración de extensiones de mensajería

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de administración de extensiones de mensajería." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Desanclar**: disponible si el usuario ha anclado la aplicación.|
|2|**Quitar**: quita la extensión de mensajería del canal, chat o reunión.|

## <a name="best-practices"></a>Procedimientos recomendados

Use estas recomendaciones para crear una experiencia de aplicación de calidad.

### <a name="setup-and-general-usage"></a>Configuración y uso general

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Ejemplo de configuración y uso general." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>Qué hacer: Integración con el inicio de sesión único

SSO hace que el proceso de inicio de sesión sea más fácil, rápido y seguro. Además, si un usuario ya ha iniciado sesión en su aplicación personal, no tendrá que volver a iniciar sesión para acceder a la extensión de mensajería.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Ejemplo de integración con inicio de sesión único." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>Qué no hacer: Sacar a los usuarios de la conversación

Las extensiones de mensajería son accesos directos que suponen una reducción del cambio de contexto. Por ejemplo, su extensión no debería dirigir a los usuarios a una página web fuera de Teams.

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>Qué hacer: Hacer notar la extensión de mensajería

Las extensiones de mensajería no siempre son fáciles de encontrar. Incluya capturas de pantalla de cómo usarla en la página de detalles de la aplicación. Si la aplicación también incluye un bot, puede incluir la documentación de ayuda de la extensión de mensajería en un paseo de bienvenida del bot.

### <a name="templating"></a>Plantillas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Ejemplo de plantillas." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>Qué hacer: Permitir que Teams controle parte del trabajo de diseño si es posible

Si es útil para sus casos de uso, considere la posibilidad de crear una extensión de mensajería basada en la búsqueda. Teams representa estos tipos de extensiones con elementos de creación de temas y accesibilidad integrados.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Ejemplo sobre cómo controlar el trabajo de diseño." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>Qué no hacer: Insertar toda la aplicación en un módulo de tareas

Si la extensión de mensajería requiere comandos de acción, no dificulte la comprensión de su módulo de tareas permanezca y muestre solo los componentes necesarios para completar la acción.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Creación de temas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Ejemplo de creación de temas." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Qué hacer: Aprovechar los tokens de color de Teams

Cada tema de Teams tiene su propia combinación de colores. Para controlar los cambios de tema de forma automática, use los <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (Fluent UI)</a> en su diseño.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Ejemplo de tokens de color." border="false":::

#### <a name="dont-hard-code-color-values"></a>Qué no hacer: Valores complicados de código de color

Si no usa los tokens de color de Teams, sus diseños serán menos escalables y administrarlos tomará más tiempo.

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Acciones

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Ejemplo de acciones." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>Qué hacer: Incluir comandos de acción que sean útiles en el contexto

Las acciones de mensaje deben relacionarse con lo que un usuario está mirando. Por ejemplo, proporcione a los usuarios un acceso directo para crear una incidencia o elemento de trabajo usando el texto de la publicación de un usuario.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Ejemplo de comandos de acción." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>Qué no hacer: Incluir comandos de acciones que no son contextuales

Probablemente, una acción de mensaje para **Ver el panel** sería considerada no coherente en la mayoría de las conversaciones.

   :::column-end:::
:::row-end:::

### <a name="searches"></a>Búsquedas

#### <a name="do-show-search-results-while-typing"></a>Qué hacer: Mostrar los resultados de la búsqueda al escribir

Proporcione resultados de la búsqueda sugeridos mientras los usuarios escriben. Es posible que encuentren el contenido que necesitan más rápido con una cantidad mínima de caracteres.

#### <a name="dont-require-users-to-submit-a-query"></a>Qué no hacer: Requerir que los usuarios envíen una consulta

Puede hacer que los usuarios presionen una tecla o seleccionen un botón para enviar consultas a la aplicación. Aunque esto puede resultar más fácil en el servicio "Servicios de aplicaciones", es posible que a los usuarios les confunda no ver los resultados de la búsqueda en tiempo real a medida que escriben su consulta.

#### <a name="do-consider-zero-term-queries"></a>Qué hacer: Considerar la posibilidad de realizar consultas sin utilizar términos

Por ejemplo, antes de que un usuario escriba algo en el cuadro de búsqueda, muestre lo que vio por última vez en la aplicación. Es posible que quieran insertar ese contenido en su conversación.
