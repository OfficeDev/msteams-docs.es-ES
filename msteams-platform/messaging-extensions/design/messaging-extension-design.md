---
title: Diseño de la extensión de mensajería
description: Obtén información sobre cómo diseñar una Teams de mensajería y obtener el kit Microsoft Teams interfaz de usuario.
keywords: Recomendaciones sobre extensiones de mensajería de referencia de directrices de diseño de teams
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: fd870d8e10ef74c36f8f6d145d48980f53e9303c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631075"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>Diseño de la extensión Microsoft Teams de mensajería

Las extensiones de mensajería son métodos abreviados para insertar contenido de la aplicación o actuar en un mensaje sin salir de la conversación.
Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar extensiones de mensajería en Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Puedes encontrar instrucciones completas de diseño de extensión de mensajería, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams de usuario.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>Agregar una extensión de mensajería

Puede agregar una extensión de mensajería en los siguientes Teams contextos:

* Desde el Teams almacén.
* En un canal, chat o reunión (antes, durante y después) cerca del cuadro de redacción. Vale la pena tener en cuenta que si agregas una extensión de mensajería en uno de estos lugares, solo puedes usarla en ese contexto.

En el ejemplo siguiente se muestra cómo agregar una extensión de mensajería en un canal:

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de mensajería cerca del cuadro de redacción de un canal." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de mensajería cerca del cuadro de redacción en un canal en el móvil." border="false":::

---

## <a name="set-up-a-messaging-extension"></a>Configurar una extensión de mensajería

La autenticación no es obligatoria, pero si la aplicación es algo parecido a una herramienta de seguimiento de vales, es posible que necesites que las personas inicien sesión para usar la extensión de mensajería.

Para obtener coherencia Teams aplicaciones, no puedes personalizar la pantalla de inicio de sesión. Si usa la autenticación de inicio de sesión único (SSO), los usuarios iniciarán sesión automáticamente.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="En el ejemplo se muestra la pantalla de configuración de extensión de mensajería con un botón de inicio de sesión." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="En el ejemplo se muestra la pantalla de configuración de extensión de mensajería con un botón de inicio de sesión en el móvil." border="false":::

---

## <a name="types-of-messaging-extensions"></a>Tipos de extensiones de mensajería

Las extensiones de mensajería pueden tener comandos de búsqueda, comandos de acción o ambos. Los comandos dependen de las características de la aplicación y de cómo se ajustan a Teams casos de uso.

### <a name="search-commands"></a>Comandos de búsqueda

Con los comandos de búsqueda, los usuarios pueden usar la extensión de mensajería para buscar rápidamente contenido externo e insertarlo en un mensaje. Los comandos de búsqueda normalmente están disponibles en el cuadro de redacción. Por ejemplo, puede iniciar o agregar a una discusión compartiendo un fragmento de contenido, sin salir de Teams.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="En el ejemplo se muestra una extensión de mensajería basada en búsqueda iniciada desde el cuadro de redacción." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="En el ejemplo se muestra una extensión de mensajería basada en búsqueda iniciada desde el cuadro de redacción en el móvil." border="false":::

---

#### <a name="compose-box-layout-options"></a>Opciones de diseño de cuadro de redacción

Tiene algunas opciones para mostrar los resultados de búsqueda de extensión de mensajería, incluidas [las vistas de lista y cuadrícula.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Ilustraciones que muestran las opciones de diseño para los resultados de búsqueda de extensión de mensajería." border="false":::

### <a name="action-commands"></a>Comandos de acción

Los comandos action permiten a los usuarios desencadenar acciones y procesar solicitudes en servicios externos dentro de Teams. Por ejemplo, si la aplicación realiza un seguimiento de los pedidos, un usuario podría crear un nuevo pedido con el contenido del mensaje de un compañero desde el chat.

Con frecuencia, las extensiones de mensajería basadas en acciones requieren que los usuarios completen un formulario o algún otro tipo de configuración dentro de un modal. Puede crear estas experiencias con [módulos de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).

## <a name="open-a-messaging-extension"></a>Abrir una extensión de mensajería

El cuadro de redacción y los mensajes o publicaciones son los contextos principales donde los usuarios usan extensiones de mensajería.

### <a name="from-the-compose-box"></a>Desde el cuadro de redacción

Una vez agregado, los usuarios pueden abrir la extensión de mensajería seleccionando el icono de la aplicación debajo del cuadro de redacción. En estos ejemplos, la extensión tiene comandos de búsqueda y acción.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde el cuadro de redacción." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde el cuadro de redacción en el móvil." border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a>Desde un mensaje de chat o una publicación de canal

Una vez agregado, los usuarios pueden seleccionar el icono **Más** en el mensaje de chat o la publicación del canal para buscar los comandos de acción :::image type="icon" source="../../assets/icons/teams-client-more.png"::: de la extensión. La extensión puede aparecer en **Más acciones basadas** en el uso.

> [!NOTE]
> La compatibilidad con más acciones de un mensaje de chat o una publicación de canal no está disponible en Microsoft Teams plataforma móvil. 

#### <a name="chat-message"></a>Mensaje de chat

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde un mensaje de chat." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde una publicación de chat en el móvil." border="false":::

---
':::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
':::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
---

## <a name="use-a-messaging-extension"></a>Usar una extensión de mensajería

En los siguientes escenarios se muestran las formas principales en que los usuarios usan extensiones de mensajería.

### <a name="insert-content-into-a-message"></a>Insertar contenido en un mensaje

**1. Seleccione una extensión de mensajería**. Los usuarios pueden buscar el contenido que desean compartir desde el cuadro de redacción.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="En el ejemplo se muestra un usuario que busca contenido para insertar desde el cuadro de redacción." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="En el ejemplo se muestra un usuario que busca contenido para insertar desde el cuadro de redacción en el móvil." border="false":::

---

**2. Insertar contenido**. Una vez publicado, otros usuarios pueden responder o seleccionar el contenido para ver más información en la aplicación.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="En el ejemplo se muestra un usuario que publica contenido en una conversación de canal." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="En el ejemplo se muestra un usuario que publica contenido en una conversación de canal en el móvil." border="false":::

---

### <a name="take-action-on-a-message"></a>Realizar acciones en un mensaje

**1. Seleccione una extensión de mensajería**. La aplicación puede incluir uno o varios comandos de acción.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="En el ejemplo se muestra un usuario que selecciona un comando de acción de extensión de mensajería." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="En el ejemplo se muestra un usuario que selecciona un comando de acción de extensión de mensajería en el móvil." border="false":::

---

**2. Complete la acción**. La aplicación puede recibir y procesar cualquier contenido o datos enviados por la acción del mensaje. Esto permite a los usuarios permanecer en su conversación y, en el ejemplo siguiente, no preocuparse por escribir información directamente en la aplicación.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Ejemplo sobre cómo realizar acciones en un mensaje." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="Ejemplo sobre cómo realizar acciones en un mensaje en el móvil." border="false":::

---

### <a name="preview-links"></a>Vínculos de vista previa

Las extensiones de mensajería también permiten insertar vínculos enriquecidos desde una dirección URL reconocida en un mensaje (esta funcionalidad se denomina desafugüe [de vínculos](../../messaging-extensions/how-to/link-unfurling.md)).)

**1. Pegue un vínculo reconocido en** el cuadro de redacción.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="En el ejemplo se muestra a un usuario pegando un vínculo en el cuadro de compost." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="En el ejemplo se muestra a un usuario pegando un vínculo en el cuadro de compost en el móvil." border="false":::

---

**2. Insertar contenido**. Si la aplicación reconoce la dirección URL en el cuadro de redacción, representa el vínculo como una tarjeta que proporciona una vista previa con contenido enriquecido del contenido web. (Vea [Directrices de diseño de tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md) para obtener más información).

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="En un ejemplo se muestra cómo la dirección URL, ya que la reconoce la aplicación, incluye contenido enriquecido en el cuadro de redacción." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="En un ejemplo se muestra cómo la dirección URL, ya que la reconoce la aplicación, incluye contenido enriquecido en el cuadro de redacción en el móvil." border="false":::

---

## <a name="manage-a-messaging-extension"></a>Administrar una extensión de mensajería

Al hacer clic con el botón secundario en el icono, los usuarios pueden anclar, quitar o configurar la extensión de mensajería.

## <a name="anatomy"></a>Anatomía

### <a name="messaging-extension-in-the-compose-box"></a>Extensión de mensajería en el cuadro de redacción

El siguiente ejemplo es una extensión de mensajería abierta desde el cuadro de redacción.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una extensión de mensajería en el cuadro de redacción." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Logotipo de la aplicación:** icono de color del logotipo de la aplicación.|
|2|**Nombre de la** aplicación: nombre completo de la aplicación.|
|3|**Icono de menú Comandos de acción (opcional):** abre una lista de comandos de acción para la extensión de mensajería (si especifica alguno).
|4 |**Cuadro de búsqueda:** permite a los usuarios encontrar el contenido de la aplicación que desean insertar.|
|5 |**Menú Tab (opcional):** proporciona varias categorías de contenido.|
|6 |**Menú Comandos de acción (opcional):** muestra una lista de comandos de acción (si especifica alguno).|
|7 |**Contenido de la** aplicación: principalmente para mostrar los resultados de la búsqueda. El ejemplo aquí es usar el diseño de lista (el diseño de cuadrícula es otra opción).|
|8 |**Logotipo de la** aplicación: icono de esquema del logotipo de la aplicación.|

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una extensión de mensajería en el cuadro de redacción del móvil." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Nombre de la** aplicación: nombre completo de la aplicación.|
|2|**Icono de menú Comandos de acción (opcional):** abre una lista de comandos de acción para la extensión de mensajería (si especifica alguno).
|3|**Cuadro de búsqueda:** permite a los usuarios encontrar el contenido de la aplicación que desean insertar.|
|4 |**Menú Tab (opcional):** proporciona varias categorías de contenido.|
|5 |**Menú Comandos de acción (opcional):** muestra una lista de comandos de acción (si especifica alguno).|
|6 |**Contenido de la** aplicación: principalmente para mostrar los resultados de la búsqueda.|

---

### <a name="messaging-extension-management-menu"></a>Menú administración de extensiones de mensajería

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de administración de extensiones de mensajería." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Desanclar:** disponible si el usuario ha anclado la aplicación.|
|2|**Quitar:** quita la extensión de mensajería del canal, chat o reunión.|

## <a name="best-practices"></a>Procedimientos recomendados

Usa estas recomendaciones para crear una experiencia de aplicación de calidad.

### <a name="setup-and-general-usage"></a>Configuración y uso general

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Ejemplo sobre configuración y uso general." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>Hacer: integrar con el inicio de sesión único

SSO hace que el proceso de inicio de sesión sea más fácil, rápido y seguro. Además, si un usuario ya ha iniciado sesión en la aplicación personal, no tiene que volver a iniciar sesión para tener acceso a la extensión de mensajería.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Ejemplo de integración con inicio de sesión único." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>No: alejar a los usuarios de la conversación

Las extensiones de mensajería son métodos abreviados que se supone reducen el cambio de contexto. La extensión no debe, por ejemplo, dirigir a los usuarios a una página web fuera de Teams.

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>Hacer: Resaltar la extensión de mensajería

Las extensiones de mensajería no siempre son fáciles de encontrar. Incluye capturas de pantalla de cómo usarlo en la página de detalles de la aplicación. Si la aplicación también incluye un bot, puedes incluir documentación de ayuda de extensión de mensajería en un recorrido de bienvenida del bot.

### <a name="templating"></a>Templating

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Ejemplo de templating." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>Do: Let Teams handle some of the design work if possible

Si tiene sentido para los casos de uso, considere la posibilidad de crear una extensión de mensajería basada en búsquedas. Teams representa estos tipos de extensiones con tema y accesibilidad integrados.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Ejemplo sobre cómo controlar el trabajo de diseño." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>No: insertar toda la aplicación en un módulo de tareas

Si la extensión de mensajería requiere comandos de acción, mantenga el módulo de tareas sencillo y muestre solo los componentes necesarios para completar la acción.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Creación de temas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Ejemplo en el uso de los mismos." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Hacer: aprovechar las ventajas de Teams de color

Cada Teams tema tiene su propia combinación de colores. Para controlar los cambios de tema automáticamente, usa <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (Fluent UI)</a> en el diseño.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Ejemplo en tokens de color." border="false":::

#### <a name="dont-hard-code-color-values"></a>No: valores de color de código duro

Si no usas tokens Teams de color, tus diseños serán menos escalables y tendrán más tiempo para administrar.

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Acciones

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Ejemplo de acciones." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>Hacer: incluir comandos de acción que tienen sentido en contexto

Las acciones del mensaje deben estar relacionadas con lo que un usuario está viendo. Por ejemplo, proporcione a los usuarios un acceso directo para crear un problema o elemento de trabajo con el texto de la publicación de alguien.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Ejemplo de comandos de acción." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>No: incluir comandos de acciones que no son contextuales

Una acción de mensaje **para ver el panel** probablemente parecería desconectada de la mayoría de las conversaciones.

   :::column-end:::
:::row-end:::

### <a name="searches"></a>Búsquedas

#### <a name="do-show-search-results-while-typing"></a>Hacer: mostrar resultados de búsqueda al escribir

Proporcionar resultados de búsqueda sugeridos mientras los usuarios escriben. Es posible que encuentren el contenido que necesitan más rápido con una cantidad mínima de caracteres.

#### <a name="dont-require-users-to-submit-a-query"></a>No: requerir que los usuarios envíen una consulta

Puedes hacer que los usuarios presionen una tecla o seleccione un botón para enviar consultas a la aplicación. Aunque esto puede ser más fácil en el servicio de servicios de aplicaciones, es posible que los usuarios se confundan de que no ven resultados de búsqueda en tiempo real mientras escriben.

#### <a name="do-consider-zero-term-queries"></a>Do: Consider zero-term queries

Por ejemplo, antes de que un usuario escriba algo en el cuadro de búsqueda, muestre lo que ha visto por última vez en la aplicación. Es posible que quieran insertar ese contenido en su conversación.
