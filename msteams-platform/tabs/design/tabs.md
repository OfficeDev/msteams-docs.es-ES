---
title: Diseño de la pestaña para escritorio y web
description: Obtén información sobre cómo diseñar una Teams (escritorio y web) y obtener el kit Microsoft Teams interfaz de usuario.
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 38eb7e400de63beb0d2840ee573bbfd16299cfbd
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644744"
---
# <a name="designing-your-tab-for-microsoft-teams"></a>Diseñar la pestaña para Microsoft Teams

Una pestaña es un lienzo grande para el contenido de la aplicación. Para guiar el diseño de la aplicación, la siguiente información describe e ilustra cómo los usuarios pueden agregar, usar y administrar pestañas en Teams.

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Puedes encontrar instrucciones completas de diseño de pestañas, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el kit de interfaz Microsoft Teams usuario. El kit de interfaz de usuario también tiene temas esenciales, como la accesibilidad y el tamaño dinámico que no se tratan aquí.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>Agregar una pestaña

Puedes agregar una pestaña desde el almacén Teams (AppSource) o en uno de los siguientes contextos:

* Chat
* Canal
* Reunión (antes, durante o después de la reunión)

# <a name="desktop"></a>[Escritorio](#tab/desktop)

En el ejemplo siguiente se muestra cómo los usuarios pueden agregar una pestaña en un canal.

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="En el ejemplo se muestra una pestaña que se agrega en un canal." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

Los usuarios pueden acceder a  las pestañas seleccionando el botón Más en el canal (ejemplo a continuación) o chat en el que se han agregado.

:::image type="content" source="../../assets/images/tabs/mobile-design-access-tab.png" alt-text="En el ejemplo se muestra una pestaña móvil que se agrega en un canal." border="false":::

---

## <a name="set-up-a-tab"></a>Configurar una pestaña

Hay un breve proceso de configuración para agregar una aplicación como un canal, chat o pestaña de reunión. La experiencia está en gran medida a su medida. Por ejemplo, podrías tener una descripción de cómo usar la aplicación y algunas opciones de configuración opcionales. Incluye un paso de inicio de sesión aquí si necesitas autenticar usuarios.

### <a name="tab-configuration-dialog"></a>Cuadro de diálogo de configuración de tabulación

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="En el ejemplo se muestra un modal de configuración de tabulación." border="false":::

### <a name="anatomy-tab-configuration-dialog"></a>Anatomía: cuadro de diálogo de configuración de tabulación

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un modal de configuración de tabulación." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Logotipo de la** aplicación: logotipo de aplicación a todo color de la aplicación.|
|2|**Nombre de la** aplicación: nombre completo de la aplicación.|
|3|**iframe:** espacio dinámico para el contenido de la aplicación (por ejemplo, configuración de pestañas o autenticación).|
|4 |**Acerca del vínculo:** abre un cuadro de diálogo que muestra más información sobre la aplicación, como una descripción completa, los permisos requeridos por la aplicación y los vínculos a la directiva de privacidad y los términos de servicio.|
|5 |**Botón Cerrar:** cierra el cuadro de diálogo.|
|6 |**Opción Notificar a los miembros del** equipo: el cuadro de diálogo pregunta a los usuarios si quieren crear una publicación para que otros sepan que agregaron una pestaña.|
|7 |**Botón Atrás:** va al paso anterior en función de dónde se abrió el cuadro de diálogo.|
|8 |**Botón Guardar:** completa la configuración de la pestaña.|

### <a name="tab-authentication-with-single-sign-on"></a>Autenticación de tabulación con inicio de sesión único

Puede agregar un paso en el que los usuarios primero deben iniciar sesión con sus credenciales de Microsoft. Este método de autenticación se denomina inicio de sesión único (SSO).

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="En el ejemplo se muestra una pantalla de autenticación de tabulación." border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a>Diseño de una configuración de pestaña con plantillas de interfaz de usuario

Usa una de las siguientes plantillas Teams interfaz de usuario para ayudar a diseñar la experiencia de configuración de pestañas:

* [Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.
* [Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.
* [Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.

## <a name="view-a-tab"></a>Ver una pestaña

Las pestañas proporcionan una experiencia web a pantalla completa en Teams donde puede mostrar contenido de colaboración (como paneles de tareas y paneles) e información importante.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="En el ejemplo se muestra una pestaña con un panel de tareas." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab.png" alt-text="En el ejemplo se muestra una pestaña móvil con un panel de tareas." border="false":::

---

### <a name="anatomy-tab"></a>Anatomía: Ficha

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una pestaña." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Nombre de la pestaña:** etiqueta de navegación para la pestaña.|
|2|**Desbordamiento de** tabulación: abre acciones de tabulación, como cambiar el nombre y quitar.|
|3|**Chat de pestañas:** abre un chat a la derecha, lo que permite a los usuarios tener una conversación junto al contenido.|
|4 |**iframe:** muestra el contenido de la aplicación.|

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de una pestaña." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Nombre de la pestaña:** etiqueta de navegación para la pestaña.|
|2|**Chat de pestaña:** abre un chat que permite a los usuarios tener una conversación junto al contenido.|
|3|**webview:** muestra el contenido de la aplicación.|

---

### <a name="designing-a-tab-with-ui-templates-and-advanced-components"></a>Diseño de una pestaña con plantillas de interfaz de usuario y componentes avanzados

Use una de las siguientes plantillas Teams y componentes para ayudar a diseñar la experiencia de pestaña:

* [Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.
* [Panel de](../../concepts/design/design-teams-app-ui-templates.md#task-board)tareas: un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales.
* [Panel:](../../concepts/design/design-teams-app-ui-templates.md#dashboard)un panel es un lienzo que contiene varias tarjetas que proporcionan información general sobre los datos o el contenido.
* [Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.
* [Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.
* [Navegación izquierda:](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)el componente de navegación izquierdo puede ayudar si la pestaña requiere algo de navegación. En general, debe mantener la navegación por pestañas al mínimo.

## <a name="use-a-tab-to-collaborate"></a>Usar una pestaña para colaborar

Las pestañas ayudan a facilitar las conversaciones sobre el contenido en una ubicación central.

### <a name="thread-discussion"></a>Discusión de subprocesos

Los usuarios pueden publicar automáticamente en un canal o chat una vez que han agregado una nueva pestaña. Esto no solo notifica a los miembros del equipo del nuevo contenido y proporciona un vínculo a la pestaña, sino que permite a los usuarios empezar a hablar sobre la pestaña.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="En el ejemplo se muestra una pestaña que se está analizando en un subproceso de canal." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-channel.png" alt-text="En el ejemplo se muestra una pestaña móvil que se está analizando en un subproceso de canal." border="false":::

---

### <a name="tab-chat"></a>Chat de pestañas

Los usuarios pueden tener una conversación junto al contenido de la pestaña que están viendo. En el escritorio, el chat se abre al lado del contenido de la aplicación.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="En el ejemplo se muestra una pestaña con un chat abierto en el lado derecho." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-side-chat.png" alt-text="En el ejemplo se muestra una pestaña móvil con un área de chat en contexto." border="false":::

---

### <a name="permissions-and-role-based-views"></a>Permisos y vistas basadas en roles

La experiencia de pestaña puede ser diferente para los usuarios en función de sus permisos. Por ejemplo, un usuario puede tener acceso a la pestaña sin tener que iniciar sesión. Sin embargo, otro usuario debe firmar y verá contenido ligeramente diferente.

## <a name="manage-a-tab"></a>Administrar una pestaña

Puede incluir opciones para cambiar el nombre, quitar o modificar una pestaña.

### <a name="anatomy-tab-menu"></a>Anatomía: menú De pestaña

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de pestaña." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Configuración**: (opcional) Permite a los usuarios modificar la configuración de una pestaña después de agregarla.|
|2|**Cambiar** nombre: los usuarios pueden dar a la pestaña un nombre que sea significativo para el canal, chat o reunión.|
|3|**Quitar:** quita la pestaña del canal, chat o reunión.|

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-manage-tab-menu-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un menú de pestaña móvil." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Abrir en el explorador:** abre la aplicación en el explorador predeterminado del dispositivo.|
|2|**Vínculo Copiar:** los usuarios pueden copiar y compartir un vínculo a la pestaña.|
|3|**Configuración**: (opcional) Modificar la configuración de una pestaña después de agregarla.|
|4 |**Cambiar** nombre: los usuarios pueden dar a la pestaña un nombre que sea significativo para el canal, chat o reunión.|
|5 |**Eliminar:** quita la pestaña del canal, chat o reunión.|

---

## <a name="tab-notifications-and-deep-linking"></a>Notificaciones de tabulación y vinculación profunda

Puede enviar un mensaje con un vínculo profundo a la pestaña. Por ejemplo, una tarjeta muestra un resumen de los datos de errores que un usuario puede seleccionar para ver el error completo en una pestaña. El envío de mensajes sobre la actividad de tabulación aumenta el conocimiento sin notificar explícitamente a todos (es decir, actividad sin ruido). También puede usar @mention usuarios específicos si es necesario.

Notificar a los usuarios sobre la actividad de tabulación de una de las siguientes maneras:

* **Bot:** este método se prefiere especialmente si el subproceso de tabulación está dirigido. La conversación enhebrada de la pestaña se mueve a la vista como activa recientemente. Este método también permite cierta sofisticación en la forma en que se envía la notificación.
* **Mensaje:** aparece un mensaje en la fuente de actividad del usuario con un vínculo profundo a [la pestaña](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).

## <a name="best-practices"></a>Procedimientos recomendados

Usa estas recomendaciones para crear una experiencia de aplicación de calidad:

### <a name="collaboration"></a>Colaboración

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="La ilustración muestra qué hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-facilitate-conversation"></a>Hacer: facilitar la conversación

Incluir contenido y componentes de los que los usuarios puedan hablar. Si no cabe en el contexto de un chat, canal o reunión, no pertenece a la pestaña.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="En el ejemplo se muestra lo que no se debe hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>No: trate la pestaña como cualquier otra página web

Una pestaña no es una página web que alguien pueda ver una vez. Una pestaña debe mostrar el contenido más importante y relevante que los usuarios necesitan para lograr algo juntos.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navegación

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="Ejemplo que muestra qué hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="do-limit-tasks-and-data"></a>Hacer: limitar tareas y datos

Las pestañas funcionan mejor cuando se abordan necesidades específicas. Incluya un conjunto limitado de tareas y datos relevantes para el equipo o grupo.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="Ilustración que muestra qué no hacer con el diseño de navegación de pestañas." border="false":::

#### <a name="dont-embed-your-entire-app"></a>No: insertar toda la aplicación

El uso de una pestaña para mostrar una aplicación completa con navegación de varios niveles e interacciones complejas conduce a una sobrecarga de información.

   :::column-end:::
:::row-end:::

### <a name="setup"></a>Instalación

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="Ilustración que muestra qué hacer con el diseño de configuración de pestañas." border="false":::

#### <a name="do-keep-it-simple"></a>Do: Keep it simple

Si la aplicación requiere autenticación, intenta integrar el inicio de sesión único (SSO) de Microsoft para una experiencia de inicio de sesión más fluida. Además, solo incluya información esencial y pasos para agregar la pestaña.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="Ilustración que muestra qué no hacer con el diseño de configuración de pestañas." border="false":::

#### <a name="dont-have-too-many-steps"></a>No: tener demasiados pasos

Quite los pasos innecesarios para agregar una pestaña.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Creación de temas

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="Ilustración que muestra qué hacer con el tema de tabulación." border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Hacer: aprovechar las ventajas de Teams de color

Cada Teams tema tiene su propia combinación de colores. Para controlar los cambios de tema automáticamente, usa <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">tokens de color (Fluent UI)</a> en el diseño.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="Ilustración que muestra lo que no se debe hacer con el tema de tabulación." border="false":::

#### <a name="dont-hard-code-color-values"></a>No: valores de color de código duro

Si no usas tokens Teams de color, tus diseños serán menos escalables y tendrán más tiempo para administrar.

   :::column-end:::
:::row-end:::
