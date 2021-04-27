---
title: Diseño de módulos de tareas
author: heath-hamilton
description: Aprende a diseñar módulos de tareas para aplicaciones de Teams y a obtener el Kit de interfaz de usuario de Microsoft Teams.
localization_priority: Normal
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 3502a705bfe1bf99a5dc0edff5c5a54265cc6ca1
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019548"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>Diseño de módulos de tareas para la aplicación de Microsoft Teams

Puedes crear experiencias emergentes modales en tu aplicación de Teams con módulos de tareas. Use esta funcionalidad para mostrar medios enriquecidos e información o completar una tarea compleja.

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="En el ejemplo se muestra un módulo de tareas." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Puedes encontrar instrucciones de diseño de módulos de tareas más completas, incluidos los elementos que puedes agarrar y modificar según sea necesario, en el Kit de interfaz de usuario de Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtener el Kit de UI de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>Abrir un módulo de tareas

Los módulos de tareas se pueden iniciar desde casi cualquier lugar de la aplicación.

* **Tab:** se puede iniciar un módulo de tareas desde cualquier vínculo dentro de una pestaña. Se usa en escenarios en los que desea que el usuario se centre en una interacción.
* **Bot:** se puede iniciar un módulo de tareas desde un vínculo dentro de un mensaje de bot.
* **Tarjeta adaptable:** se puede iniciar un módulo de tareas desde una tarjeta adaptable (enviada con una extensión de mensajería o por un bot) cuando un usuario selecciona un botón.
* **Extensión de mensajería (comandos de acción):** las extensiones de mensajería permiten realizar una acción determinada en el contenido del mensaje. Al seleccionar una acción, se abre un módulo de tareas.
* **Extensión de mensajería (contexto del** cuadro de redacción): en el cuadro de redacción, puede diseñar una extensión de mensajería para abrir un módulo de tareas en lugar del control desplegable típico. Reserve módulos de tareas para interacciones complejas, como completar un formulario.

## <a name="anatomy"></a>Anatomía

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un módulo de tareas." border="false":::

Los módulos de tareas son superficies muy flexibles. Se pueden crear con iframes, lo que hace que se usen otras plantillas de interfaz de usuario para hospedar experiencias creadas por asociados. Esto es preferible para la experiencia más pulida.

También se pueden crear con el marco [de](../../task-modules-and-cards/cards/design-effective-cards.md) tarjeta adaptable, que puede ser una forma más sencilla y rápida de ejecutar escenarios comunes (como formularios).

|Contador|Descripción|
|----------|-----------|
|1|**Icono de aplicación**|
|2|**Nombre de la** aplicación: nombre completo de la aplicación.|
|3|**Encabezado:** haga que los encabezados sea claros y concisos. Describa la tarea que desea que los usuarios completen.
|4 |**Botón Cerrar:** permite a los usuarios encontrar el contenido de la aplicación que desean insertar.|
|5 |**iframe:** espacio dinámico que hospeda el contenido de la aplicación.|
|6 |**Acciones (opcional):** botones relacionados con el contenido de la aplicación.|

## <a name="designing-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Considere la posibilidad de usar plantillas para diseños comunes dentro de los módulos de tareas. Cada uno de ellos está hecho de componentes más pequeños para crear un diseño elegante y con capacidad de respuesta que se puede usar de forma personalizada para el escenario o con la apariencia de la marca.

* [Lista:](../../concepts/design/design-teams-app-ui-templates.md#list)las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.
* [Formulario:](../../concepts/design/design-teams-app-ui-templates.md#form)los formularios son para recopilar, validar y enviar la entrada del usuario de forma estructurada.
* [Estado vacío:](../../concepts/design/design-teams-app-ui-templates.md#empty-state)la plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.

## <a name="examples"></a>Ejemplos

### <a name="list"></a>Lista

Las listas funcionan bien en un módulo de tareas porque son fáciles de examinar.

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Lista de ejemplos en un módulo de tareas." border="false":::

### <a name="form"></a>Form

Los módulos de tareas son un excelente lugar para superficier formularios con entradas de usuario secuenciales y validación en línea. Puedes aprovechar las tarjetas adaptables como una forma de insertar elementos de formulario.

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Formulario de ejemplo en un módulo de tareas." border="false":::

### <a name="sign-in"></a>Iniciar sesión

Cree un flujo de inicio de sesión o registro centrado con una serie de módulos de tareas, lo que permite a los usuarios moverse fácilmente a través de pasos secuenciales.

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Ejemplo de experiencia de inicio de sesión en un módulo de tareas." border="false":::

### <a name="media"></a>Elementos multimedia

Insertar contenido multimedia en un módulo de tareas para una experiencia de visualización centrada.

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Ejemplo de contenido multimedia en un módulo de tareas." border="false":::

### <a name="empty-state"></a>Estado vacío

Se usa para los mensajes de bienvenida, error y éxito.

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Estado vacío de ejemplo en un módulo de tareas." border="false":::

### <a name="image-gallery"></a>Galería de imágenes

Inserte un carrusel de galería en un iframe.

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Galería de imágenes de ejemplo en un módulo de tareas." border="false":::

### <a name="poll"></a>Sondeo

En este ejemplo se muestran los resultados del sondeo iniciados desde una tarjeta adaptable. El sondeo también se puede colocar dentro de un módulo de tareas.

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Sondeo de ejemplo en un módulo de tareas." border="false":::

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="usability"></a>Facilidad de uso

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a>Hacer: Usar un módulo de tareas a la vez

El objetivo es centrar al usuario en completar una tarea después de todo.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="En el ejemplo se muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>Don't: Pop a dialog on top of a task module

Esto crea una experiencia de usuario confusa y desenfoque.

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>Respuesta correcta

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="En el ejemplo se muestra el procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a>Do: Make sure the content is responsive

Aunque las tarjetas adaptables hospedadas en un módulo de tareas se representan correctamente en dispositivos móviles, si eliges usar un iframe para hospedar contenido de la aplicación, asegúrate de que la interfaz de usuario responda y funcione bien en todos los dispositivos.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="En el ejemplo se muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a>No usar: Usar barras de desplazamiento horizontales

Es un procedimiento recomendado mantener el contenido centrado y no demasiado largo. Si es necesario un desplazamiento, desplácese verticalmente y no horizontalmente.

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>Simplicidad

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="En el ejemplo se muestra el procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="do-keep-it-short"></a>Do: Keep it short

Puedes crear fácilmente un asistente para varios pasos, pero eso no significa necesariamente que debas hacerlo. Un módulo de tareas de varias pantallas puede ser problemático porque los mensajes entrantes distraen y tenta a los usuarios a salir. Si la tarea está realmente implicada, abre una página web completa en lugar de un módulo de tareas.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Ilustración que muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="dont-do-long-interactions"></a>No hacer: realizar interacciones largas

Intenta mantener tus interacciones cortas y hasta el punto.

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>Mensajes de error

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="La ilustración muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="do-use-inline-error-messages"></a>Hacer: usar mensajes de error en línea

Consulta la plantilla de interfaz de usuario de formularios para obtener instrucciones sobre el control de errores en línea.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="La ilustración muestra un procedimiento recomendado del módulo de tareas." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a>No: poner mensajes de error en cuadros de diálogo

No aparece un mensaje de error en un cuadro de diálogo encima de los módulos de tareas. Crea una experiencia de usuario confusa.

   :::column-end:::
:::row-end:::
