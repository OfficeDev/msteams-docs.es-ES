---
title: Diseño de la pestaña para escritorio y Web
description: Obtenga información sobre cómo diseñar una pestaña de Microsoft Teams (escritorio y Web) y obtener el kit de interfaz de usuario de Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 692a21c78dc86cbca5bf248e55d0332bd71c6b92
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604704"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a>Diseño de la pestaña para escritorio y Web de Microsoft Teams

Una pestaña es un gran lienzo para contenido que facilita la colaboración. Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar pestañas en Microsoft Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit de IU de Microsoft Teams

Puede encontrar instrucciones detalladas para el diseño de pestañas, incluidos los elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams. El kit de UI también tiene temas esenciales, como la accesibilidad y el tamaño de respuesta, que no se cubren aquí.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>Agregar una pestaña

Puede Agregar una pestaña desde el almacén de Microsoft Teams (AppSource) o en uno de los siguientes contextos:

* Chat
* Canal
* Reunión (antes, durante o después de la reunión)

En el siguiente ejemplo se muestra cómo se agrega una pestaña en un canal.

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="Ejemplo muestra una pestaña agregada en un canal." border="false":::

## <a name="set-up-a-tab"></a>Configurar una pestaña

Hay un proceso de instalación breve para agregar una aplicación como una pestaña de canal, chat o reunión. La experiencia depende en gran medida del usuario. Por ejemplo, puede tener una descripción de cómo usar la aplicación y algunos parámetros opcionales. Incluya un paso de inicio de sesión aquí si necesita autenticar usuarios.

### <a name="tab-configuration-modal"></a>Ficha modal de configuración

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="Ejemplo muestra un modal de configuración de ficha." border="false":::

### <a name="anatomy-tab-configuration-modal"></a>Anatomía: configuración de pestaña modal

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un modal de configuración de ficha." border="false":::

|Counter|Descripción|
|----------|-----------|
|1|**Logotipo** de la aplicación: logotipo de aplicación a todo color de la aplicación.|
|2 |**Nombre** de la aplicación: nombre completo de la aplicación.|
|3 |**iframe**: espacio de respuesta para el contenido de la aplicación (por ejemplo, la configuración de la pestaña o la autenticación).|
|4 |**Acerca del vínculo**: abre un cuadro de diálogo que muestra más información sobre la aplicación, como una descripción completa, los permisos requeridos por la aplicación y los vínculos a la Directiva de privacidad y los términos de servicio.
|5 |**Botón Cerrar**: cierra el modal.|
|6 |**Opción notificar a los integrantes del equipo**: el modal le preguntará si desea crear una publicación que permita a otros usuarios saber que ha agregado una pestaña.|
|7 |**Botón atrás**: se dirige al paso anterior en función de dónde se abrió el cuadro de diálogo.|
|8 |**Botón Guardar**: completa la configuración de la pestaña.|

### <a name="tab-authentication-with-single-sign-on"></a>Autenticación de pestaña con inicio de sesión único

Puede Agregar un paso en el que los usuarios primero deban iniciar sesión con sus credenciales de Microsoft. Este método de autenticación se denomina inicio de sesión único (SSO).

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="Ejemplo muestra una pantalla de autenticación de pestañas." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a>Diseño de una configuración de pestaña con plantillas de interfaz de usuario

Use una de las siguientes plantillas de interfaz de usuario de Microsoft Teams para ayudar a diseñar su experiencia de configuración de pestañas:

* [List](../../concepts/design/design-teams-app-ui-templates.md#list): lists puede mostrar elementos relacionados en un formato que se pueda analizar y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.
* [Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.
* [Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc.

## <a name="view-a-tab"></a>Ver una pestaña

Las pestañas proporcionan una experiencia web de pantalla completa en Teams donde puede mostrar contenido de colaboración (como paneles y paneles de tareas) e información importante.

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="Ejemplo muestra una pestaña con un panel de tareas." border="false":::

### <a name="anatomy-tab"></a>Anatomía: pestaña

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una pestaña." border="false":::

|Counter|Descripción|
|----------|-----------|
|1|**Nombre de ficha**: etiqueta de navegación de la pestaña.|
|2 |**Desbordamiento de tabulación**: abre acciones de pestaña, como cambiar nombre y quitar.|
|3 |**Chat de pestañas**: abre un hilo de chat a la derecha, lo que permite a los usuarios tener una conversación junto al contenido.|
|4 |**iframe**: muestra el contenido de la pestaña.

### <a name="designing-a-tab-with-ui-templates"></a>Diseño de una pestaña con plantillas de interfaz de usuario

Use una de las siguientes plantillas de interfaz de usuario de Microsoft Teams para ayudar a diseñar su experiencia de pestañas:

* [List](../../concepts/design/design-teams-app-ui-templates.md#list): lists puede mostrar elementos relacionados en un formato que se pueda analizar y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.
* [Panel de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): un panel de tareas, a veces denominado tablero Kanban o carriles de nadar, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o vales.
* [Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre datos o contenido.
* [Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.
* [Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc.
* Panel de [navegación izquierdo](../../concepts/design/design-teams-app-ui-templates.md#left-nav): la plantilla de navegación izquierda puede servir de ayuda si la pestaña requiere la navegación. En general, debe mantener al mínimo la navegación por tabulaciones.

## <a name="use-a-tab-to-collaborate"></a>Usar una pestaña para colaborar

Las pestañas ayudan a facilitar las conversaciones sobre el contenido en una ubicación central.

### <a name="thread-discussion"></a>Discusión de subprocesos

Los usuarios pueden publicar automáticamente en un canal o un chat una vez que haya agregado una nueva pestaña. Esto no solo notifica a los miembros del equipo el contenido nuevo y proporciona un vínculo a la pestaña, permite a los usuarios empezar a hablar sobre la ficha.

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="Ejemplo muestra una pestaña que se está discutiendo en un subproceso de canal." border="false":::

### <a name="side-by-side-discussion"></a>Discusión en paralelo

Los usuarios pueden tener una conversación junto al ver el contenido de la pestaña.

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="Ejemplo muestra una pestaña con un chat abierto en el lado derecho." border="false":::

### <a name="permissions-and-role-based-views"></a>Permisos y vistas basadas en roles

La experiencia de la pestaña puede ser diferente para los usuarios en función de sus permisos. Por ejemplo, un usuario puede tener acceso a la pestaña sin tener que iniciar sesión. Sin embargo, otro usuario debe firmar y verá contenido ligeramente distinto.

## <a name="manage-a-tab"></a>Administrar una pestaña

Puede incluir opciones para cambiar el nombre de una pestaña, quitarla o modificarla.

### <a name="anatomy-tab-menu"></a>Anatomía: menú de pestañas

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de pestañas." border="false":::

|Counter|Descripción|
|----------|-----------|
|1|**Settings**: (opcional) permite a los usuarios modificar la configuración de una pestaña una vez que se ha agregado.|
|2 |**Rename**: permite a los usuarios asignar a la ficha un nombre que sea más significativo para el equipo.|
|3 |**Quitar**: quita la pestaña del canal, el chat o la reunión.|

## <a name="tab-notifications-and-deep-linking"></a>Notificaciones de tabulación y vínculos profundos

Puede enviar un mensaje con un vínculo profundo a su ficha. Por ejemplo, una tarjeta muestra un resumen de los datos de los errores que un usuario puede seleccionar para ver el error completo en una ficha. El envío de mensajes sobre la actividad de la pestaña aumenta el conocimiento sin notificar explícitamente a todos los usuarios (es decir, actividades sin ruido). También puede @mention usuarios específicos si es necesario.

Notifique a los usuarios la actividad de tabulación de una de las siguientes maneras:

* **Bot**: este método es preferible especialmente si el subproceso de la pestaña es de destino. La conversación encadenada de la pestaña se mueve a la vista como activa recientemente. Este método también permite una sofisticación en el modo en que se envía la notificación.
* **Mensaje**: un mensaje se muestra en la fuente de actividades del usuario con un [vínculo profundo a la ficha](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="collaboration"></a>Colaboración

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="Ilustración que muestra qué se debe hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-facilitate-conversation"></a>Hacer: facilitar la conversación

Incluir contenido y componentes sobre los que pueden hablar los usuarios. Si no encaja en el contexto de un chat, canal o reunión, no pertenece a la pestaña.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="Ilustración que muestra lo que no se hace con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>No: tratar la pestaña como cualquier otra página web

Una pestaña no es una página web que alguien pueda ver una vez. Una pestaña debe mostrar su contenido más importante y relevante que los usuarios necesitan para realizar algo juntos.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navegación

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Ilustración que muestra qué se debe hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-limit-tasks-and-data"></a>Do: limitar tareas y datos

Las pestañas funcionan mejor cuando se redireccionan a necesidades específicas. Incluya un conjunto limitado de tareas y datos relevantes para el equipo o grupo.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Ilustración que muestra lo que no se hace con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-embed-your-entire-app"></a>No: incruste la aplicación completa

Usar una pestaña para mostrar una aplicación completa con navegación de varios niveles y interacciones complejas conduce a la sobrecarga de información.

   :::column-end:::
:::row-end:::

### <a name="setup"></a>Instalación

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Ilustración que muestra qué se debe hacer con el diseño de la configuración de pestañas." border="false":::

#### <a name="do-keep-it-simple"></a>Do: simple

Si la aplicación requiere autenticación, intente integrar el inicio de sesión único (SSO) de Microsoft para obtener una experiencia de inicio de sesión más fluida. Además, solo incluya información esencial y pasos para agregar la pestaña.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Ilustración que muestra lo que no se hace con el diseño de la configuración de pestañas." border="false":::

#### <a name="dont-have-too-many-steps"></a>No: tener demasiados pasos

Quite los pasos innecesarios para agregar una tabulación.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Creación de temas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Ilustración que muestra qué se debe hacer con los temas de la ficha." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Do: aprovechar las ventajas de los tokens de color de Microsoft Teams

Cada tema de Teams tiene su propia combinación de colores. Para controlar automáticamente los cambios de tema, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (interfaz de usuario de Fluent)</a> en el diseño.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Ilustración que muestra lo que no se hace con el tabulador." border="false":::

#### <a name="dont-hard-code-color-values"></a>No: valores de color de código duro

Si no usa los tokens de color de Teams, los diseños serán menos escalables y tendrán más tiempo para administrarlos.

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>Validar el diseño

Si planea publicar la aplicación en AppSource, debe comprender los problemas de diseño que suelen hacer que las aplicaciones fallen durante el envío.

> [!div class="nextstepaction"]
> [Comprobar las instrucciones de validación del diseño](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
