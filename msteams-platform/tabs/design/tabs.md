---
title: Diseño de su pestaña para escritorio y web
description: Obtén información sobre cómo diseñar una pestaña de Teams (escritorio y web) y obtener el Kit de interfaz de usuario Microsoft Teams.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: baa17cd97ff4e2cad91615dced5c4e4cf5e533c8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566883"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a>Diseñar su pestaña para Microsoft Teams escritorio y web

Una pestaña es un lienzo grande para su contenido. Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo las personas pueden agregar, usar y administrar pestañas en Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Puede encontrar directrices completas de diseño de pestañas, incluidos los elementos que puede capturar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams. El kit de interfaz de usuario también tiene temas esenciales como la accesibilidad y el tamaño adaptable que no se tratan aquí.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>Agregar una pestaña

Puede agregar una pestaña desde la tienda de Teams (AppSource) o en uno de los contextos siguientes:

* Chat
* Canal
* Reunión (antes, durante o después de la reunión)

En el ejemplo siguiente se muestra cómo se agrega una pestaña en un canal:

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="En el ejemplo se muestra una pestaña que se agrega en un canal." border="false":::

## <a name="set-up-a-tab"></a>Configurar una pestaña

Hay un proceso de configuración corto para agregar una aplicación como canal, chat o pestaña de reunión. La experiencia depende en gran medida de usted. Por ejemplo, podría tener una descripción de cómo usar la aplicación y alguna configuración opcional. Incluya un paso de inicio de sesión aquí si necesita autenticar usuarios.

### <a name="tab-configuration-modal"></a>Configuración de pestañas modal

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="El ejemplo muestra una configuración de tabulación modal." border="false":::

### <a name="anatomy-tab-configuration-modal"></a>Anatomía: Configuración de pestañas modal

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una configuración de pestaña modal." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Logotipo de la aplicación**: Logotipo de la aplicación a todo color de su aplicación.|
|2|**Nombre de la aplicación**: Nombre completo de la aplicación.|
|3|**iframe**: Espacio responsivo para el contenido de la aplicación. Por ejemplo, la configuración de la pestaña o la autenticación.|
|4 |**Acerca del vínculo:** abre un cuadro de diálogo que muestra más información sobre la aplicación, como una descripción completa, los permisos requeridos por la aplicación y los vínculos a su política de privacidad y términos de servicio.
|5 |**Botón Cerrar**: Cierra el modal.|
|6 |**Notificar a los miembros** del equipo opción : El modal pregunta si desea crear una publicación que informe a otros de que agregó una pestaña.|
|7 |**Botón Atrás**: Va al paso anterior en función de dónde se abrió el cuadro de diálogo.|
|8 |**Botón Guardar**: Completa la configuración de la pestaña.|

### <a name="tab-authentication-with-single-sign-on"></a>Autenticación de pestañas con inicio de sesión único

Puede agregar un paso en el que los usuarios primero deben iniciar sesión con sus credenciales de Microsoft. Este método de autenticación se denomina inicio de sesión único (SSO).

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="El ejemplo muestra una pantalla de autenticación de pestañas." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a>Diseño de una configuración de pestañas con plantillas de interfaz de usuario

Utilice una de las siguientes plantillas de interfaz de usuario Teams para ayudar a diseñar la experiencia de configuración de la pestaña:

* [Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato escaneable y permitir a los usuarios realizar acciones en una lista completa o en elementos individuales.
* [Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): Los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.
* [Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.

## <a name="view-a-tab"></a>Ver una pestaña

Las pestañas proporcionan una experiencia web a pantalla completa en Teams donde puede mostrar contenido colaborativo ,como tableros de tareas y paneles, e información importante.

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="En el ejemplo se muestra una pestaña con un tablero de tareas." border="false":::

### <a name="anatomy-tab"></a>Anatomía: Pestaña

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una pestaña." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Nombre de la pestaña**: Etiqueta de navegación para la pestaña.|
|2|**Desbordamiento de tabulación:** abre acciones de tabulación, como cambiar el nombre y quitar.|
|3|**Chat de pestañas**: Abre un hilo de chat a la derecha, lo que permite a los usuarios tener una conversación junto al contenido.|
|4 |**iframe**: Muestra el contenido de tu pestaña.

### <a name="designing-a-tab-with-ui-templates"></a>Diseño de una pestaña con plantillas de interfaz de usuario

Utilice una de las siguientes plantillas de interfaz de usuario Teams para ayudar a diseñar la experiencia de la pestaña:

* [Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato escaneable y permitir a los usuarios realizar acciones en una lista completa o en elementos individuales.
* [Tablero de tareas](../../concepts/design/design-teams-app-ui-templates.md#task-board): Un tablero de tareas, a veces llamado tablero kanban o carriles de natación, es una colección de tarjetas que se utilizan a menudo para rastrear el estado de los artículos de trabajo o boletos.
* [Panel](../../concepts/design/design-teams-app-ui-templates.md#dashboard): Un panel es un lienzo que contiene varias tarjetas que proporcionan una visión general de los datos o el contenido.
* [Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): Los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.
* [Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.
* [Navegador izquierdo](../../concepts/design/design-teams-app-ui-templates.md#left-nav): La plantilla de navegación izquierda puede ayudar si la pestaña requiere un poco de navegación. En general, debe mantener la navegación de la pestaña al mínimo.

## <a name="use-a-tab-to-collaborate"></a>Utilice una pestaña para colaborar

Las pestañas ayudan a facilitar las conversaciones sobre el contenido en una ubicación central.

### <a name="thread-discussion"></a>Discusión de hilos

Los usuarios pueden publicar automáticamente en un canal o chat una vez que hayan agregado una nueva pestaña. Esto no solo notifica a los miembros del equipo del nuevo contenido y proporciona un enlace a la pestaña, sino que permite a las personas empezar a hablar de la pestaña.

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="En el ejemplo se muestra una pestaña que se describe en un subproceso de canal." border="false":::

### <a name="side-by-side-discussion"></a>Discusión en paralelo

Los usuarios pueden tener una conversación a continuación mientras ven el contenido de la pestaña.

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="El ejemplo muestra una pestaña con un chat abierto en el lado derecho." border="false":::

### <a name="permissions-and-role-based-views"></a>Permisos y vistas basadas en roles

La experiencia de la pestaña puede ser diferente para los usuarios en función de sus permisos. Por ejemplo, un usuario puede acceder a la pestaña sin tener que iniciar sesión. Otro usuario, sin embargo, debe firmar y verá contenido ligeramente diferente.

## <a name="manage-a-tab"></a>Administrar una pestaña

Puede incluir opciones para cambiar el nombre, quitar o modificar una pestaña.

### <a name="anatomy-tab-menu"></a>Anatomía: Menú tabulador

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de pestañas." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Configuración:**(Opcional) Permite a los usuarios modificar la configuración de una pestaña después de agregarla.|
|2|**Cambiar nombre:** permite a los usuarios dar a la pestaña un nombre más significativo para el equipo.|
|3|**Eliminar**: Elimina la pestaña del canal, chat o reunión.|

## <a name="tab-notifications-and-deep-linking"></a>Notificaciones de pestañas y vinculación profunda

Puede enviar un mensaje con un vínculo profundo a su pestaña. Por ejemplo, una tarjeta muestra un resumen de los datos de error que un usuario puede seleccionar para ver todo el error en una pestaña. Enviar mensajes sobre la actividad de las pestañas aumenta el conocimiento sin notificar explícitamente a todos (es decir, la actividad sin ruido). También puede @mention usuarios específicos si es necesario.

Notifique a los usuarios de la actividad de la pestaña de una de las siguientes maneras:

* **Bot**: Este método es preferido especialmente si el subproceso de tabulación está dirigido. La conversación enhebrada de la pestaña se mueve a la vista como recientemente activa. Este método también permite cierta sofisticación en la forma en que se envía la notificación.
* **Mensaje**: Aparece un mensaje en la fuente de actividad del usuario con un [vínculo profundo a la pestaña](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).

## <a name="best-practices"></a>Procedimientos recomendados

Utilice estas recomendaciones para crear una experiencia de aplicación de calidad:

### <a name="collaboration"></a>Colaboración

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="La ilustración muestra qué hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-facilitate-conversation"></a>Hacer: Facilitar la conversación

Incluya contenido y componentes de los que las personas puedan hablar. Si no encaja en el contexto de un chat, canal o reunión, no pertenece a tu pestaña.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="En el ejemplo se muestra qué no hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>No: Trata tu pestaña como cualquier otra página web

Una pestaña no es una página web que alguien pueda ver una vez. Una pestaña debe mostrar su contenido más importante y relevante que las personas necesitan para lograr algo juntos.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navegación

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Ejemplo que muestra qué hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-limit-tasks-and-data"></a>Hacer: Limitar tareas y datos

Las pestañas funcionan mejor cuando abordan necesidades específicas. Incluya un conjunto limitado de tareas y datos relevantes para el equipo o grupo.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Ilustración que muestra qué no hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-embed-your-entire-app"></a>No: Incrustar toda la aplicación

El uso de una pestaña para mostrar una aplicación completa con navegación de varios niveles e interacciones complejas conduce a la sobrecarga de información.

   :::column-end:::
:::row-end:::

### <a name="setup"></a>Instalación

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Ilustración que muestra qué hacer con el diseño de configuración de pestañas." border="false":::

#### <a name="do-keep-it-simple"></a>Hacer: Mantenlo simple

Si la aplicación requiere autenticación, intente integrar el inicio de sesión único (SSO) de Microsoft para obtener una experiencia de inicio de sesión más fluida. Además, solo incluya información esencial y pasos para agregar la pestaña.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Ilustración que muestra qué no hacer con el diseño de configuración de pestañas." border="false":::

#### <a name="dont-have-too-many-steps"></a>No: Tener demasiados pasos

Elimine los pasos innecesarios para agregar una pestaña.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Creación de temas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Ilustración que muestra qué hacer con el temática de pestañas." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Hacer: Aproveche Teams tokens de color

Cada tema Teams tiene su propio esquema de color. Para controlar los cambios de tema automáticamente, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (interfaz de usuario fluida)</a> en el diseño.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Ilustración que muestra qué no hacer con el temática de pestañas." border="false":::

#### <a name="dont-hard-code-color-values"></a>No: Valores de color de código duro

Si no usa tokens de color Teams, sus diseños serán menos escalables y tardarán más tiempo en administrarse.

   :::column-end:::
:::row-end:::
