---
title: Diseño de módulos de tareas
author: heath-hamilton
description: Obtenga información sobre cómo diseñar módulos de tareas para las aplicaciones de Teams y obtener el kit de IU de Microsoft Teams.
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 41584ecf58ca7718290e58e5845549e4579dac64
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606416"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>Diseño de módulos de tareas para su aplicación de Microsoft Teams

Puede crear experiencias de elemento emergente modal en la aplicación de Microsoft Teams con módulos de tareas. Use esta funcionalidad para mostrar información y medios enriquecidos o para completar una tarea compleja.

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="Ejemplo muestra un módulo de tarea." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit de IU de Microsoft Teams

Puede encontrar instrucciones de diseño de módulos de tareas más completas, incluidos elementos que puede captar y modificar según sea necesario, en el kit de interfaz de usuario de Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>Abrir un módulo de tareas

Los módulos de tareas se pueden iniciar casi en cualquier lugar de la aplicación.

* **Tab**: se puede iniciar un módulo de tareas desde cualquier vínculo dentro de una pestaña o iframe. Úsela en escenarios en los que desea que el usuario se Centre en una interacción.
* **Bot**: un módulo de tarea puede iniciarse desde un vínculo dentro de un mensaje de bot.
* **Tarjeta adaptable**: un módulo de tarea se puede iniciar desde una tarjeta adaptable (enviada con una extensión de mensajería o mediante un bot) cuando un usuario selecciona un botón.
* **Extensión de mensajería (comandos de acción)**: extensiones de mensajería le permite realizar una acción concreta en el contenido del mensaje. Al seleccionar una acción se abre un módulo de tareas.
* **Extensión de mensajería (contexto de cuadro de redacción)**: en el cuadro de redacción, puede diseñar una extensión de mensajería para abrir un módulo de tareas en lugar del flotante normal. Reserve módulos de tareas para interacciones complejas, como rellenar un formulario.

## <a name="anatomy"></a>Anatomía

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un módulo de tareas." border="false":::

Los módulos de tareas son superficies muy flexibles. Se pueden crear con iframes, al extraer en otras plantillas de interfaz de usuario, para hospedar experiencias creadas por asociados. Esta es la preferida para la experiencia más pulida.

También se pueden crear con el marco de [tarjeta adaptable](../../task-modules-and-cards/cards/design-effective-cards.md) , que puede ser una forma más sencilla y rápida de ejecutar escenarios comunes (como formularios).

|Counter|Descripción|
|----------|-----------|
|1|**Icono de aplicación**|
|2 |**Nombre** de la aplicación: nombre completo de la aplicación.|
|3 |**Encabezado**: hacer que los encabezados sean claros y concisos. Describa la tarea que desea que completen los usuarios.
|4 |**Botón Cerrar**: permite a los usuarios buscar el contenido de la aplicación que quiera insertar.|
|5 |**iframe**: espacio de respuesta que hospeda el contenido de la aplicación.|
|6 |**Acciones (opcional)**: botones relacionados con el contenido de la aplicación.|

## <a name="designing-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Considere la posibilidad de usar plantillas para los diseños comunes dentro de los módulos de tareas. Cada uno de ellos consta de componentes más pequeños para crear un diseño elegante y dinámico que se puede usar de forma rápida o personalizada para su escenario o con la apariencia de la marca.

* [List](../../concepts/design/design-teams-app-ui-templates.md#list): lists puede mostrar elementos relacionados en un formato que se pueda analizar y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.
* [Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): los formularios son para recopilar, validar y enviar entradas de usuario de forma estructurada.
* [Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): la plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc.

## <a name="examples"></a>Ejemplos

### <a name="list"></a>Lista

Las listas funcionan bien en un módulo de tareas porque son fáciles de analizar.

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Lista de ejemplo de un módulo de tareas." border="false":::

### <a name="form"></a>Form

Los módulos de tareas son un buen punto de partida para exponer formularios con entradas de usuario secuenciales y validación en línea. Puede aprovechar las tarjetas adaptables como una forma de incrustar los elementos del formulario.

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="Formulario de ejemplo en un módulo de tareas." border="false":::

### <a name="sign-in"></a>Iniciar sesión

Crear un flujo de inicio de sesión o de inicio de sesión prioritarios con una serie de módulos de tareas, lo que permite a los usuarios desplazarse fácilmente a través de pasos secuenciales.

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Ejemplo de experiencia de inicio de sesión en un módulo de tareas." border="false":::

### <a name="media"></a>Audiovisual

Insertar contenido multimedia en un módulo de tareas para una experiencia de visualización específica.

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Contenido multimedia de ejemplo en un módulo de tareas." border="false":::

### <a name="empty-state"></a>Estado vacío

Usar para los mensajes de bienvenida, error y operación correcta.

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Ejemplo de estado vacío en un módulo de tareas." border="false":::

### <a name="image-gallery"></a>Galería de imágenes

Inserta un carrusel de Galería dentro de un iframe.

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Galería de imágenes de ejemplo en un módulo de tareas." border="false":::

### <a name="poll"></a>Buscar

En este ejemplo se muestran los resultados de sondeo iniciados desde una tarjeta adaptable.

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Ejemplo de sondeo en un módulo de tareas." border="false":::

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="usability"></a>Mejoras

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a>Do: usar un módulo de tareas a la vez

El objetivo es centrar al usuario en la finalización de una tarea después de todo.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>No: mostrar un cuadro de diálogo en la parte superior de un módulo de tareas

Esto crea una experiencia de usuario confusa y no enfocada.

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>Respuesta correcta

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a>Haga lo siguiente: Asegúrese de que el contenido está respondiendo

Aunque las tarjetas adaptables hospedadas en un módulo de tareas se presentan correctamente en dispositivos móviles, si decide usar un iframe para hospedar el contenido de la aplicación, asegúrese de que la interfaz de usuario responda correctamente y de que funcione en todos los dispositivos.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="dont-use-horizontal-scrollbars"></a>No: usar barras de desplazamiento horizontales

Se recomienda mantener el contenido enfocado y no demasiado largo. Si es necesario un desplazamiento, desplácese verticalmente y no horizontalmente.

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>Simple

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="do-keep-it-short"></a>Do: Keep it Short

Puede crear fácilmente un asistente de varios pasos, pero esto no significa necesariamente que debería. Un módulo de tarea de varias pantallas puede ser problemático porque los mensajes entrantes distraen y tentan a los usuarios a salir. Si su tarea realmente está implicada, salga a una página web completa en lugar de a un módulo de tareas.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="dont-do-long-interactions"></a>No: realizar acciones largas

Intente mantener sus interacciones cortas y en el punto.

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>Mensajes de error

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="do-use-inline-error-messages"></a>Do: usar mensajes de error en línea

Vea la plantilla de interfaz de usuario de formularios para obtener instrucciones sobre el tratamiento de errores en línea.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado de módulo de tareas." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a>No: colocar mensajes de error en los cuadros de diálogo

No mostrar un mensaje de error en un cuadro de diálogo encima de los módulos de tareas. Crea una experiencia de usuario confusa.

   :::column-end:::
:::row-end:::
