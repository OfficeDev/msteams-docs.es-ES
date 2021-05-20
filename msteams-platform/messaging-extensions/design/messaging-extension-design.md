---
title: Diseño de la extensión de mensajería
description: Obtén información sobre cómo diseñar una extensión de mensajería Teams y obtener el kit de interfaz de usuario de Microsoft Teams.
keywords: directrices de diseño de equipos de referencia extensiones de mensajería consejos mejores prácticas
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ed1f0f2eb2ce8d429a8a780bd2c4c4eb421d6d54
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566218"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>Diseño de la extensión de mensajería Microsoft Teams

Las extensiones de mensajería son accesos directos para insertar contenido de la aplicación o actuar en un mensaje sin navegar lejos de la conversación.
Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo las personas pueden agregar, usar y administrar extensiones de mensajería en Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Puede encontrar directrices completas de diseño de extensiones de mensajería, incluidos los elementos que puede capturar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>Añadir una extensión de mensajería

Puede agregar una extensión de mensajería en los siguientes contextos de Teams:

* En la tienda de Teams (AppSource)
* En un canal, chatea o reúne (antes, durante y después) cerca del cuadro de composición. Vale la pena señalar si agrega una extensión de mensajería en uno de estos lugares, solo usted puede usarlo en ese contexto.

En el ejemplo siguiente se muestra cómo agregar una extensión de mensajería en un canal:

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="En el ejemplo se muestra cómo agregar una extensión de mensajería cerca del cuadro de composición en un canal." border="false":::

## <a name="set-up-a-messaging-extension"></a>Configurar una extensión de mensajería

La autenticación no es obligatoria, pero si la aplicación es algo así como una herramienta de seguimiento de vales, es posible que necesite que las personas inicien sesión para usar la extensión de mensajería.

Para obtener coherencia entre Teams aplicaciones, no puede personalizar la pantalla de inicio de sesión. Si utiliza la autenticación de inicio de sesión único (SSO), los usuarios inician sesión automáticamente.

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="En el ejemplo se muestra la pantalla de configuración de la extensión de mensajería con un botón de inicio de sesión." border="false":::

## <a name="types-of-messaging-extensions"></a>Tipos de extensiones de mensajería

Las extensiones de mensajería pueden tener comandos de búsqueda, comandos de acción o ambos. Los comandos dependen de las características de la aplicación y de cómo se ajusten en Teams casos de uso.

### <a name="search-commands"></a>Comandos de búsqueda

Con los comandos de búsqueda, las personas pueden usar la extensión de mensajería para encontrar rápidamente contenido externo e insertarlo en un mensaje. Los comandos de búsqueda suelen estar disponibles en el cuadro de composición. Por ejemplo, puede iniciar o agregar a una discusión compartiendo un fragmento de contenido, sin salir nunca de Teams.

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="En el ejemplo se muestra una extensión de mensajería basada en búsqueda iniciada desde el cuadro de composición." border="false":::

#### <a name="compose-box-layout-options"></a>Opciones de diseño de cuadro de composición

Tiene algunas opciones para mostrar los resultados de búsqueda de extensiones de mensajería, incluidas [las vistas de lista y cuadrícula.](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="Ilustraciones que muestran opciones de diseño para los resultados de búsqueda de extensiones de mensajería." border="false":::

### <a name="action-commands"></a>Comandos de acción

Los comandos de acción permiten a las personas desencadenar acciones y procesar solicitudes en servicios externos dentro de Teams. Por ejemplo, si la aplicación realiza un seguimiento de los pedidos, un usuario podría crear un nuevo pedido utilizando el contenido del mensaje de un colega desde el interior de su chat.

Las extensiones de mensajería basadas en acciones con frecuencia requieren que los usuarios completen un formulario o algún otro tipo de configuración dentro de un modal. Puede crear estas experiencias con [módulos de tareas.](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="open-a-messaging-extension"></a>Abrir una extensión de mensajería

El cuadro de composición y los mensajes o publicaciones son los contextos principales donde las personas usan extensiones de mensajería.

### <a name="from-the-compose-box"></a>Desde la caja de composa

Una vez agregado, los usuarios pueden abrir la extensión de mensajería seleccionando el icono de la aplicación debajo del cuadro de composición. En este ejemplo, la extensión tiene comandos de búsqueda y acción:

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde el cuadro de composición." border="false":::

### <a name="from-a-chat-message-or-channel-post"></a>Desde un mensaje de chat o una publicación de canal

Una vez agregado, los usuarios pueden seleccionar el icono **Más** en el mensaje de chat o la publicación de canal para encontrar los :::image type="icon" source="../../assets/icons/teams-client-more.png"::: comandos de acción de la extensión. Su extensión puede aparecer en **Más acciones** basadas en el uso.

> [!NOTE]
> El soporte para más acciones de un mensaje de chat o una publicación de canal no está disponible en Microsoft Teams plataforma móvil. 

#### <a name="chat-message"></a>Mensaje de chat

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde un mensaje de chat." border="false":::

#### <a name="channel-post"></a>Publicación de canal

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="En el ejemplo se muestra cómo abrir una extensión de mensajería desde una publicación de canal." border="false":::

## <a name="use-a-messaging-extension"></a>Usar una extensión de mensajería

Los siguientes escenarios muestran las formas principales en que las personas usan extensiones de mensajería.

### <a name="insert-content-into-a-message"></a>Insertar contenido en un mensaje

**1. Seleccione una extensión de mensajería**. Los usuarios pueden buscar el contenido que desean compartir desde el cuadro de composición.

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="En el ejemplo se muestra a un usuario que busca contenido para insertar desde el cuadro de composición." border="false":::

**2. Inserte contenido**. Una vez publicado, otros pueden responder o seleccionar el contenido para ver más información en la aplicación.

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="En el ejemplo se muestra un usuario que publica contenido en una conversación de canal." border="false":::

### <a name="take-action-on-a-message"></a>Tomar medidas en un mensaje

**1. Seleccione una extensión de mensajería**. La aplicación puede incluir uno o varios comandos de acción.

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="En el ejemplo se muestra a un usuario que selecciona un comando de acción de extensión de mensajería." border="false":::

**2. Complete la acción**. La aplicación puede recibir y procesar cualquier contenido o datos enviados por la acción del mensaje. Esto permite a los usuarios permanecer en su conversación y, en el siguiente ejemplo, no preocuparse por introducir información directamente en la aplicación.

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="Ejemplo sobre cómo tomar medidas en un mensaje." border="false":::

### <a name="preview-links"></a>Enlaces de vista previa

Las extensiones de mensajería también le permiten insertar vínculos enriquecidos desde una dirección URL reconocida en un mensaje (esta funcionalidad se denomina [despliegue de vínculos](../../messaging-extensions/how-to/link-unfurling.md).)

**1. Pegue un enlace reconocido** en el cuadro de composición.

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="En el ejemplo se muestra a un usuario pegando un vínculo en el cuadro de compost." border="false":::

**2. Inserte contenido**. Si la aplicación reconoce la dirección URL en el cuadro de composición, representa el vínculo como una tarjeta que proporciona una vista previa enriquecida con contenido del contenido web. (Consulte [directrices de diseño de tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md) para obtener más información.)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="En el ejemplo se muestra cómo la dirección URL, ya que la reconoce la aplicación, incluye contenido enriquecido en el cuadro de composición." border="false":::

## <a name="manage-a-messaging-extension"></a>Administrar una extensión de mensajería

Al hacer clic con el botón derecho en el icono, los usuarios pueden anclar, quitar o configurar la extensión de mensajería.

## <a name="anatomy"></a>Anatomía

### <a name="messaging-extension-in-the-compose-box"></a>Extensión de mensajería en el cuadro de composición

En el ejemplo siguiente se abre una extensión de mensajería desde el cuadro de composición.

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una extensión de mensajería en el cuadro de composición." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Logotipo de la aplicación**: Icono de color del logotipo de la aplicación.|
|2|**Nombre de la aplicación**: Nombre completo de la aplicación.|
|3|Icono de menú comandos de **acción (opcional):** abre una lista de comandos de acción para la extensión de mensajería (si especifica alguno).
|4 |**Cuadro de búsqueda**: Permite a los usuarios encontrar el contenido de la aplicación que desean insertar.|
|5 |**Menú de pestañas (opcional):** proporciona varias categorías de contenido.|
|6 |**Menú comandos de acción (opcional):** muestra la lista de comandos de acción (si especifica alguno).|
|7 |**Contenido de la aplicación:** principalmente para mostrar los resultados de búsqueda. El ejemplo aquí es el uso del diseño de lista (el diseño de cuadrícula es otra opción).|
|8 |**Logotipo de la aplicación**: Icono de contorno del logotipo de la aplicación.|

### <a name="messaging-extension-management-menu"></a>Menú de gestión de extensiones de mensajería

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de administración de extensiones de mensajería." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Unpin**: Disponible si el usuario ha anclado la aplicación.|
|2|**Eliminar**: Elimina la extensión de mensajería del canal, chat o reunión.|

## <a name="best-practices"></a>Procedimientos recomendados

Utilice estas recomendaciones para crear una experiencia de aplicación de calidad.

### <a name="setup-and-general-usage"></a>Configuración y uso general

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="Ejemplo sobre la configuración y el uso general." border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>Hacer: Integre con el inicio de sesión único

SSO hace que el proceso de inicio de sesión sea más fácil, rápido y seguro. Además, si un usuario ya ha iniciado sesión en su aplicación personal, no tiene que volver a iniciar sesión para acceder a la extensión de mensajería.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="Ejemplo sobre la integración con el inicio de sesión único." border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>No: Alejar a los usuarios de la conversación

Las extensiones de mensajería son accesos directos que se supone reducen el cambio de contexto. La extensión no debe, por ejemplo, dirigir a los usuarios a una página web fuera de Teams.

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>Hacer: Resalte su extensión de mensajería

Las extensiones de mensajería no siempre son fáciles de encontrar. Incluya capturas de pantalla de cómo usarlo en la página de detalles de la aplicación. Si la aplicación también incluye un bot, puede incluir documentación de ayuda de extensión de mensajería en un recorrido de bienvenida a bots.

### <a name="templating"></a>Tentador

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="Ejemplo sobre la templación." border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>Hacer: Deje que Teams maneje parte del trabajo de diseño si es posible

Si tiene sentido para los casos de uso, considere la posibilidad de crear una extensión de mensajería basada en búsqueda. Teams representa estos tipos de extensiones con temática y accesibilidad integradas.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="Ejemplo sobre el trabajo de diseño de manipulación." border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>No: Incrusta toda la aplicación en un módulo de tareas

Si la extensión de mensajería requiere comandos de acción, mantenga el módulo de tareas simple y muestre solo los componentes necesarios para completar la acción.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Creación de temas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="Ejemplo sobre el uso de temática." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Hacer: Aproveche Teams tokens de color

Cada tema Teams tiene su propio esquema de color. Para controlar los cambios de tema automáticamente, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (interfaz de usuario fluida)</a> en el diseño.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="Ejemplo sobre tokens de color." border="false":::

#### <a name="dont-hard-code-color-values"></a>No: Valores de color de código duro

Si no usa tokens de color Teams, sus diseños serán menos escalables y tardarán más tiempo en administrarse.

   :::column-end:::
:::row-end:::

### <a name="actions"></a>Acciones

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="Ejemplo sobre acciones." border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>Hacer: Incluya comandos de acción que tienen sentido en contexto

Las acciones de mensaje deben relacionarse con lo que un usuario está mirando. Por ejemplo, proporcione a los usuarios un acceso directo para crear un problema o elemento de trabajo mediante el texto de la publicación de alguien.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="Ejemplo sobre comandos de acción." border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>No: incluya comandos de acciones que no sean contextuales

Una acción de mensaje para **Ver el panel** probablemente parecería desconectada de la mayoría de las conversaciones.

   :::column-end:::
:::row-end:::

### <a name="searches"></a>Búsquedas

#### <a name="do-show-search-results-while-typing"></a>Hacer: Mostrar los resultados de búsqueda mientras escribe

Proporcione los resultados de búsqueda sugeridos mientras los usuarios escriben. Pueden encontrar el contenido que necesitan más rápido con una cantidad mínima de caracteres.

#### <a name="dont-require-users-to-submit-a-query"></a>No: requiere que los usuarios envíen una consulta

Puede hacer que los usuarios presionen una tecla o seleccionen un botón para enviar consultas a la aplicación. Aunque eso puede ser más fácil en el servicio de servicios de aplicaciones, es posible que las personas se confundan con que no están viendo los resultados de búsqueda en tiempo real a medida que escriben.

#### <a name="do-consider-zero-term-queries"></a>Hacer: Considere consultas de términos cero

Por ejemplo, antes de que un usuario escriba algo en el cuadro de búsqueda, muestra lo que vio por última vez en la aplicación. Es posible que quieran insertar ese contenido en su conversación.
