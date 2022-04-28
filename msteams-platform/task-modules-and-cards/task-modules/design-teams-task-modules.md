---
title: Diseño de módulos de tareas
author: heath-hamilton
description: Obtenga información sobre cómo diseñar módulos de tareas para aplicaciones de Teams y obtener el Kit de interfaz de usuario de Microsoft Teams.
ms.localizationpriority: high
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 1514ed8e3101065efd482ced45de98b8b0f58ab8
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104136"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>Diseño de módulos de tareas para la aplicación de Microsoft Teams

Puede crear experiencias emergentes modales en la aplicación de Teams con módulos de tareas. Use esta funcionalidad para mostrar medios enriquecidos e información o completar una tarea compleja.

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="En el ejemplo se muestra un módulo de tareas." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit de interfaz de usuario de Microsoft Teams

En el kit de interfaz de usuario de Microsoft Teams, encontrará instrucciones completas de diseño de módulos de tareas que incluyen elementos que puede usar y modificar como quiera.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>Abrir un módulo de tareas

Los módulos de tareas se pueden iniciar desde casi cualquier lugar de la aplicación.

* **Pestaña**: Se puede iniciar un módulo de tareas desde cualquier vínculo dentro de una pestaña. Se usa en escenarios en los que desea que el usuario se centre en una interacción.
* **Bot**: Se puede iniciar un módulo de tareas desde un vínculo dentro de un mensaje de bot.
* **Tarjeta adaptable**: Se puede iniciar un módulo de tareas desde una tarjeta adaptable (enviada con una extensión de mensaje o por un bot) cuando un usuario selecciona un botón.
* **Extensión de mensaje (comandos de acción)**: Las extensiones de mensaje permiten realizar una acción determinada en el contenido del mensaje. Al seleccionar una acción, se abre un módulo de tareas.
* **Extensión de mensaje (contexto del cuadro de redacción)**: En el cuadro de redacción, puede diseñar una extensión de mensaje para abrir un módulo de tareas en lugar del control flotante característico. Reserve módulos de tareas para interacciones complejas, como completar un formulario.

## <a name="anatomy"></a>Anatomía

Los módulos de tareas proporcionan una superficie flexible para experiencias de aplicaciones alojadas. Se han creado con un iframe (escritorio) o una vista web (móvil), por lo que puedes diseñar módulos de tareas con nuestras plantillas de interfaz de usuario (recomendadas) o desde cero.

También se pueden crear con el marco [de tarjetas adaptables](../../task-modules-and-cards/cards/design-effective-cards.md), que puede ser una forma más sencilla y rápida de facilitar escenarios comunes (como formularios).

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/task-module/mobile-task-module-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un módulo de tareas en el móvil." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Encabezado**: Haga que los encabezados sean claros y concisos. Describa la tarea que desea que los usuarios completen.
|2|**Nombre de la aplicación**: nombre completo de la aplicación.|
|3|**Botón Cerrar**: Cierra el módulo de tareas. No aplica cambios no guardados en el contenido de la aplicación.|
|4|**Vista Web**: Espacio dinámico que hospeda el contenido de la aplicación.|
|5|**Acciones (opcional)**: Botones relacionados con el contenido de la aplicación.|

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="Ilustración que muestra la anatomía de la interfaz de usuario de un módulo de tareas." border="false":::

|Contador|Descripción|
|----------|-----------|
|1|**Icono de aplicación**|
|2|**Nombre de la aplicación**: nombre completo de la aplicación.|
|3|**Encabezado**: Haga que los encabezados sean claros y concisos. Describa la tarea que desea que los usuarios completen.
|4|**Botón Cerrar**: Cierra el módulo de tareas. No aplica cambios no guardados en el contenido de la aplicación.|
|5|**iframe**: Espacio dinámico que hospeda el contenido de la aplicación.|
|6 |**Acciones (opcional)**: Botones relacionados con el contenido de la aplicación.|

## <a name="designing-with-ui-templates"></a>Diseño con plantillas de interfaz de usuario

Considere usar plantillas para diseños comunes dentro de sus módulos de tareas. Cada una de ellas se compone de elementos más pequeños para crear un diseño elegante y dinámico que se puede usar de forma predeterminada o personalizarse para su escenario o con su apariencia de marca.

* [Lista](../../concepts/design/design-teams-app-ui-templates.md#list): Las listas pueden mostrar elementos relacionados en un formato digitalizado y permitir a los usuarios realizar acciones en una lista completa o en elementos individuales.
* [Formulario](../../concepts/design/design-teams-app-ui-templates.md#form): Los formularios son para recopilar, validar y enviar el input del usuario de forma estructurada.
* [Estado vacío](../../concepts/design/design-teams-app-ui-templates.md#empty-state): La plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más.

## <a name="examples"></a>Ejemplos

### <a name="list"></a>Lista

Las listas funcionan bien en un módulo de tareas porque son fáciles de digitalizar.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/task-module/mobile-list.png" alt-text="Lista de ejemplos en un módulo de tareas en el móvil." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="Lista de ejemplos en un módulo de tareas." border="false":::

### <a name="form"></a>Formulario

Los módulos de tareas son un excelente lugar para mostrar formularios con entradas de usuario secuenciales y validación en línea. Puede aprovechar las tarjetas adaptables como una forma de insertar elementos del formulario.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/task-module/mobile-form.png" alt-text="Formulario de ejemplo en un módulo de tareas en el móvil." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/form.png" alt-text="Formulario de ejemplo en un módulo de tareas." border="false":::

### <a name="sign-in"></a>Iniciar sesión

Cree un flujo de inicio de sesión o registro centrado con una serie de módulos de tareas, lo que permite a los usuarios moverse fácilmente a través de pasos secuenciales.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/task-module/mobile-sign-in.png" alt-text="Ejemplo de experiencia de inicio de sesión en un módulo de tareas en el móvil." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="Ejemplo de experiencia de inicio de sesión en un módulo de tareas." border="false":::

### <a name="media"></a>Multimedia

Insertar contenido multimedia en un módulo de tareas para una experiencia de visualización prioritaria.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/task-module/mobile-media.png" alt-text="Ejemplo de contenido multimedia en un módulo de tareas en el móvil." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="Ejemplo de contenido multimedia en un módulo de tareas." border="false":::

### <a name="empty-state"></a>Estado vacío

Se usa para los mensajes de bienvenida, error y éxito.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/task-module/mobile-empty-state.png" alt-text="Estado vacío de ejemplo en un módulo de tareas en el móvil." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="Estado vacío de ejemplo en un módulo de tareas." border="false":::

### <a name="image-gallery"></a>Galería de imágenes

Insertar un carrusel de galería en un iframe (escritorio) o vista web (móvil).

##### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/task-module/mobile-image-gallery.png" alt-text="Galería de imágenes de ejemplo en un módulo de tareas en el móvil." border="false":::

##### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="Galería de imágenes de ejemplo en un módulo de tareas." border="false":::

### <a name="poll"></a>Sondeo

En este ejemplo se muestran los resultados del sondeo iniciados desde una tarjeta adaptable. El sondeo también se puede colocar dentro de un módulo de tareas.

#### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/task-module/mobile-poll.png" alt-text="Sondeo de ejemplo en un módulo de tareas en el móvil." border="false":::

#### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="Sondeo de ejemplo en un módulo de tareas." border="false":::

## <a name="best-practices"></a>Procedimientos recomendados

Use estas recomendaciones para crear una experiencia de aplicación de calidad.

### <a name="usability"></a>Usabilidad

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado del módulo de tareas (un módulo de tareas cada vez)." border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a>Hacer: Usar un módulo de tareas cada vez

¡El objetivo es centrar al usuario en completar una tarea después de todo!

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="Ejemplo en el que se muestra un procedimiento recomendado del módulo de tareas (mostrar un cuadro de diálogo encima de un módulo de tareas)." border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>No hacer: Mostrar un cuadro de diálogo encima de un módulo de tareas

Esto crea una experiencia de usuario confusa y descentrada.

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>Capacidad de respuesta

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado del módulo de tareas (asegúrese de que el contenido responde)." border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a>Hacer: Asegúrese de que el contenido responde

Aunque las tarjetas adaptables hospedadas en un módulo de tareas se representan correctamente en dispositivos móviles, si eliges usar un iframe para hospedar contenido de la aplicación, asegúrate de que la interfaz de usuario responda y funcione bien en todos los dispositivos.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado del módulo de tareas (no use barras de desplazamiento horizontales)." border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a>No: Usar barras de desplazamiento horizontales

Es un procedimiento recomendado mantener el contenido centrado y no demasiado largo. Si es necesario un desplazamiento, desplácese verticalmente y no horizontalmente.

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>Sencillez

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="Ejemplo en el que se muestra un procedimiento recomendado del módulo de tareas (que sea breve)." border="false":::

#### <a name="do-keep-it-short"></a>Sí: Sea breve.

Puede crear fácilmente un asistente para varios pasos, ¡pero eso no significa necesariamente que deba hacerlo! Un módulo de tareas de varias pantallas puede ser problemático porque los mensajes entrantes distraen y tientan a los usuarios a salir. Si la tarea está realmente implicada, abre una página web completa en lugar de un módulo de tareas.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado del módulo de tareas (no tiene interacciones largas)." border="false":::

#### <a name="dont-have-long-interactions"></a>No: Tener interacciones largas

Intente mantener sus interacciones cortas y concretas.

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>Mensajes de error

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="Ejemplo que muestra un procedimiento recomendado del módulo de tareas (usar mensajes de error en línea)." border="false":::

#### <a name="do-use-inline-error-messages"></a>Hacer: Usar mensajes de error en línea

Consulte la plantilla de interfaz de usuario de formularios para obtener instrucciones sobre el control de errores en línea.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="Ejemplo que muestra un procedimiento recomendado del módulo de tareas (colocar mensajes de error en cuadros de diálogo)." border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a>No: Poner mensajes de error en cuadros de diálogo

No aparece un mensaje de error en un cuadro de diálogo encima de un módulo de tareas. Crea una experiencia de usuario confusa.

   :::column-end:::
:::row-end:::
