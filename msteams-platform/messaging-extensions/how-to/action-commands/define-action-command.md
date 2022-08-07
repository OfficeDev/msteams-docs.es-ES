---
title: Definir comandos de acción de extensión de mensajería
author: surbhigupta
description: En este módulo, aprenderá a definir comandos de acción de extensión de mensajería con el ejemplo de manifiesto de aplicación en Microsoft Teams.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 2769dc4d76f6b417f3264dd321b0d5c5e794c9f8
ms.sourcegitcommit: fb0942afb8be32d92df282dec03fbb3b13f8f303
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2022
ms.locfileid: "67264186"
---
# <a name="define-message-extension-action-commands"></a>Definir comandos de acción de extensión de mensajería

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> Cuando se inicia una acción de mensaje, los detalles de los datos adjuntos no se envían como parte de la `turncontext` actividad de invocación.

Los comandos de acción permiten presentar a los usuarios un elemento emergente modal denominado módulo de tareas en Teams. El módulo de tareas recopila o muestra información, procesa la interacción y envía la información de vuelta a Teams. Este documento le guía sobre cómo seleccionar ubicaciones de invocación de los comandos de acción, crear el módulo de tareas, enviar el mensaje final o tarjeta, crear un comando de acción mediante App Studio o crearlo manualmente.

Antes de crear el comando de acción, debe decidir los siguientes factores:

1. [¿Desde dónde se puede desencadenar el comando de acción?](#select-action-command-invoke-locations)
1. [¿Cómo se creará el módulo de tareas?](#select-how-to-create-your-task-module)
1. [¿Se enviará el mensaje final o la tarjeta al canal desde un bot, o se insertará el mensaje o la tarjeta en el área de redacción del mensaje para que el usuario lo envíe?](#select-how-the-final-message-is-sent)

Vea el siguiente vídeo para obtener información sobre cómo definir comandos de acción de extensión de mensaje:
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OANG]
<br>

## <a name="select-action-command-invoke-locations"></a>Seleccionar ubicaciones de invocación de comando de acción

En primer lugar, debe decidir la ubicación desde la que se debe invocar el comando de acción. Al especificar `context` en el manifiesto de la aplicación, el comando se puede invocar desde una o varias de las siguientes ubicaciones:

* Área redactar mensaje: los botones de la parte inferior del área de redacción del mensaje.

    Contexto de comando = redacción

* Cuadro de comandos: al @mencionar la aplicación en el cuadro de comandos.

    Contexto de comandos = commandBox

   > [!NOTE]
   > Si se invoca la extensión de mensaje desde el cuadro de comandos, no puede responder con un mensaje de bot insertado directamente en la conversación.

* Mensaje: directamente desde un mensaje existente a través del menú de desbordamiento `...` en un mensaje.

    Contexto de comandos = mensaje

    > [!NOTE]
    > La invocación inicial al bot incluye un objeto JSON que contiene el mensaje desde el que se invocó. Puede procesar el mensaje antes de presentarlo con un módulo de tareas.

En la imagen siguiente se muestran las ubicaciones desde las que se invoca el comando de acción:

:::image type="content" source="~/assets/images/messaging-extension-invoke-locations.png" alt-text="Ubicaciones de invocación de comandos de acción":::

## <a name="select-how-to-create-your-task-module"></a>Seleccione cómo crear el módulo de tareas

Además de seleccionar desde dónde se puede invocar el comando, también debe seleccionar cómo rellenar el formulario en el módulo de tareas para los usuarios. Tiene las tres opciones siguientes para crear el formulario que se representará dentro del módulo de tareas:

* **Lista estática de parámetros**: este es el método más sencillo. Puede definir una lista de parámetros en el manifiesto de la aplicación que representa el cliente de Teams, pero no puede controlar el formato en este caso.
* **Tarjeta adaptable**: puede seleccionar usar una tarjeta adaptable, que proporciona un mayor control sobre la interfaz de usuario, pero le sigue limitando en cuanto a los controles disponibles y las opciones de formato.
* **Vista web incrustada**: puede seleccionar insertar una vista web personalizada en el módulo de tareas para tener un control completo sobre la interfaz de usuario y los controles.

Si selecciona crear el módulo de tareas con una lista estática de parámetros y cuando el usuario envía el módulo de tareas, se llamará a la extensión de mensaje. Cuando se usa una vista web incrustada o una tarjeta adaptable, la extensión de mensaje debe controlar un evento de invocación inicial del usuario, crear el módulo de tareas y devolverlo al cliente.

## <a name="select-how-the-final-message-is-sent"></a>Seleccionar cómo se envía el mensaje final

En la mayoría de los casos, el comando de acción da como resultado una tarjeta insertada en el cuadro de redacción del mensaje. El usuario puede enviarlo al canal o chat. En este caso, el mensaje procede del usuario y el bot no puede editar ni actualizar aún más la tarjeta.

Si la extensión de mensaje se invoca desde el cuadro de redacción o directamente desde un mensaje, el servicio web puede insertar la respuesta final directamente en el canal o chat. En este caso, la tarjeta adaptable procede del bot, el bot la actualiza y responde al hilo de conversación si es necesario. Debe agregar el objeto `bot` al manifiesto de aplicación con el mismo identificador y definiendo los ámbitos adecuados.

## <a name="add-the-action-command-to-your-app-manifest"></a>Agregar el comando de acción al manifiesto de la aplicación

Para agregar el comando de acción al manifiesto de la aplicación, debe agregar un nuevo objeto `composeExtension` al nivel superior del JSON del manifiesto de aplicación. Puede hacerlo de una de las siguientes formas:

* [Crear un comando de acción con App Studio](#create-an-action-command-using-app-studio)
* [Crear un comando de acción manualmente](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a>Creación de un comando de acción mediante App Studio

Puede crear un comando de acción mediante **App Studio** o **Portal para desarrolladores**.

> [!WARNING]
 > Si ha estado usando App Studio, le recomendamos que pruebe el portal para desarrolladores [Portal para desarrolladores](https://dev.teams.microsoft.com/) para configurar, distribuir y administrar las aplicaciones de Teams. App Studio está en desuso el 01 de agosto de 2022.

# <a name="app-studio"></a>[App Studio](#tab/AS)

> [!NOTE]
> El requisito previo para crear un comando de acción es que ya haya creado una extensión de mensaje. Para obtener información sobre cómo crear una extensión de mensaje, vea [crear una extensión de mensaje](~/messaging-extensions/how-to/create-messaging-extension.md).

**Para crear un comando de acción**

1. Abra **App Studio** en el cliente Microsoft Teams y seleccione la pestaña **Editor de manifiestos**.
1. Si ya ha creado el paquete de la aplicación en **App Studio**, selecciónelo en la lista. Si no ha creado un paquete de aplicación, importe uno existente.
1. Después de importar un paquete de aplicación, seleccione **Extensiones de mensaje** en **Funcionalidades**. Se mostrará una ventana emergente para configurar la extensión de mensaje.
1. Seleccione **Configurar** en la ventana para incluir la extensión de mensaje en la experiencia de la aplicación. En la imagen siguiente se muestra la ventana de configuración de la extensión de mensaje:

    :::image type="content" source="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt-text="Configuración de la extensión de mensajería":::

1. Para crear una extensión de mensaje, necesita un bot registrado de Microsoft. Puede usar un bot existente o crear uno nuevo. Seleccione la opción **Crear nuevo bot**, asigne un nombre al nuevo bot y seleccione **Crear**. En la imagen siguiente se muestra la creación de bots para la extensión de mensaje:

    :::image type="content" source="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt-text="Creación de un bot para la extensión de mensajería":::

1. Para usar un bot existente, seleccione **Usar bot existente** y seleccione **Seleccionar de uno de mis bots existentes** para elegir los bots existentes de la lista desplegable, proporcione un **Nombre de bot** y seleccione **Guardar**, o seleccione **Conectar a un identificador de bot diferente** si ya tiene un identificador de bot creado, asigne un **Nombre de bot** y seleccione **Guardar**.

    :::image type="content" source="~/assets/images/messaging-extension/use-existing-bot.png" alt-text="Uso del bot existente para la extensión de mensajería":::

1. Seleccione **Agregar** en la **Sección de comandos** de la página de extensión de mensajería para incluir los comandos que deciden el comportamiento de la extensión de mensajería. La siguiente imagen muestra la adicción de comandos para la extensión de mensajería:

    :::image type="content" source="~/assets/images/messaging-extension/include-command.png" alt-text="Incluir comandos":::

1. Seleccione **Permitir que los usuarios desencadenen acciones en servicios externos dentro de Teams**. En la imagen siguiente se muestra la selección del comando de acción:

    :::image type="content" source="~/assets/images/messaging-extension/action-command-selection.png" alt-text="Selección de comandos de acción":::

1. Para usar un conjunto estático de parámetros para crear el módulo de tareas, seleccione **Definir un conjunto de parámetros estáticos para el comando**.

    En la imagen siguiente se muestra la selección de parámetros estáticos del comando de acción:

    :::image type="content" source="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt-text="Selección de parámetros estáticos del comando de acción":::

    En la imagen siguiente se muestra un ejemplo de configuración de parámetros estáticos:

    :::image type="content" source="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt-text="Configuración de parámetros estáticos del comando de acción":::

    En la imagen siguiente se muestra un ejemplo de pruebas de parámetros estáticos:

    :::image type="content" source="~/assets/images/messaging-extension/static-parameter-testing.png" alt-text="Pruebas de parámetros estáticos del comando de acción":::

1. Para usar parámetros dinámicos, seleccione **Capturar un conjunto dinámico de parámetros del bot**. En la imagen siguiente se muestra la selección del parámetro de comando de acción:

    :::image type="content" source="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt-text="Selección de parámetros dinámicos de comandos de acción":::

1. Agregue un **Id. de comando** y un **Título**.
1. Seleccione la ubicación desde la que desea invocar el comando de acción. En la imagen siguiente se muestra la ubicación de invocación del comando de acción:

    :::image type="content" source="~/assets/images/messaging-extension/action-command-invoke-location.png" alt-text="Ubicación de invocación de comandos de acción":::

1. Seleccione **Guardar**.
1. Para agregar más parámetros, seleccione el botón **Agregar** en la sección **Parámetros**.

### <a name="create-an-action-command-manually"></a>Creación manual de un comando de acción

Para agregar manualmente el comando de extensión de mensaje basado en acciones al manifiesto de la aplicación, debe agregar los siguientes parámetros a la matriz de objetos `composeExtension.commands` :

| Nombre de propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | Esta propiedad es un identificador único que se asigna a este comando. La solicitud de usuario incluye este id. | Sí | 1.0 |
| `title` | Esta propiedad es un nombre de comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Esta propiedad debe ser una `action`. | No | 1.4 |
| `fetchTask` | Esta propiedad se establece en `true` para una tarjeta adaptable o una vista web insertada para el módulo de tareas, y`false` para una lista estática de parámetros o al cargar la vista web mediante un `taskInfo`. | No | 1.4 |
| `context` | Esta propiedad es una matriz opcional de valores que define desde dónde se invoca la extensión de mensaje. Los valores posibles son`message`, `compose` o `commandBox`. El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |

Si usa una lista estática de parámetros, también debe agregar los parámetros siguientes:

| Nombre de propiedad | Objetivo | ¿Es obligatoria? | Versión mínima del manifiesto |
|---|---|---|---|
| `parameters` | Esta propiedad describe la lista estática de parámetros para el comando. Usar solo cuando `fetchTask` es `false`. | No | 1.0 |
| `parameter.name` | Esta propiedad describe el nombre del parámetro. Esto se envía al servicio en la solicitud del usuario. | Sí | 1.0 |
| `parameter.description` | Esta propiedad describe los propósitos del parámetro o el ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Esta propiedad es un título o etiqueta de parámetro descriptivo corto. | Sí | 1.0 |
| `parameter.inputType` | Esta propiedad se establece en el tipo de entrada requerido. Los valores posibles incluyen `text`, `textarea`, `number`, `date`, `time`, `toggle`. El valor predeterminado se establece en `text`. | No | 1.4 |

Si usa una vista web incrustada, opcionalmente puede agregar el objeto para capturar la `taskInfo` vista web sin llamar directamente al bot. Si selecciona esta opción, el comportamiento es similar al del uso de una lista estática de parámetros. En que la primera interacción con el bot es [responder a la acción de envío del módulo de tareas](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md). Si usa un `taskInfo` objeto , debe establecer el `fetchTask` parámetro en `false`.

| Nombre de propiedad | Objetivo | ¿Es obligatoria? | Versión mínima del manifiesto |
|---|---|---|---|
|`taskInfo`|Especifique el módulo de tareas que se va a cargar previamente al usar un comando de extensión de mensajería. | No | 1.4 |
|`taskInfo.title`|Título del módulo de tareas inicial. |No | 1.4 |
|`taskInfo.width`|Ancho del módulo de tareas, ya sea un número en píxeles o un diseño predeterminado, como `large`, `medium` o `small`. |No | 1.4 |
|`taskInfo.height`|Alto del módulo de tareas, ya sea un número en píxeles o un diseño predeterminado, como `large`, `medium` o `small`.|No | 1.4 |
|`taskInfo.url`|Dirección URL inicial de la vista web.|No | 1.4 |

#### <a name="app-manifest-example"></a>Ejemplo de manifiesto de aplicación

La siguiente sección es un ejemplo de un objeto `composeExtensions` que define dos comandos de acción. No es un ejemplo del manifiesto completo. Para obtener el esquema completo del manifiesto de aplicación, consulte [esquema de manifiesto de aplicación](~/resources/schema/manifest-schema.md):

```json
...
"composeExtensions": [
  {
    "botId": "12a3c29f-1fc5-4d97-a142-12bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "addTodo",
        "description": "Create a To Do item",
        "title": "Create To Do",
        "type": "action",
        "context": ["commandBox", "message", "compose"],
        "fetchTask": false,
        "parameters": [
          {
            "name": "Name",
            "description": "To Do Title",
            "title": "Title",
            "inputType": "text"
          },
          {
            "name": "Description",
            "description": "Description of the task",
            "title": "Description",
            "inputType": "textarea"
          },
          {
            "name": "Date",
            "description": "Due date for the task",
            "title": "Date",
            "inputType": "date"
          }
        ]
      },
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Reassign a todo item",
        "type": "action",
        "fetchTask": false,
      }
    ]
  }
]
...
```

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre           | Descripción | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Acción de extensión de mensaje de Teams| Describe cómo definir comandos de acción, crear un módulo de tareas y responder a la acción de envío del módulo de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [ guía paso a paso](../../../sbs-meetingextension-action.yml) para crear la extensión de mensajería basada en acciones de Teams.

## <a name="next-step"></a>Paso siguiente

Si usa una tarjeta adaptable o una vista web incrustada sin un `taskInfo` objeto, el siguiente paso es:

> [!div class="nextstepaction"]
> [Crear y responder con un módulo de tareas](~/messaging-extensions/how-to/action-commands/create-task-module.md)

Si usa los parámetros o una vista web incrustada con un `taskInfo` objeto , el siguiente paso es:

> [!div class="nextstepaction"]
> [Responde al envío del módulo de tareas](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
