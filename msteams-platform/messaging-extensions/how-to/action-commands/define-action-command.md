---
title: Definir comandos de acción de extensión de mensajería
author: surbhigupta
description: En este módulo, aprenderá a definir comandos de acción de extensión de mensajería con el ejemplo de manifiesto de aplicación en Microsoft Teams.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 45dbdabc744a58eb031c6e9a9f7415ecdf18cdcb
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2022
ms.locfileid: "67604860"
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

* [Creación de un comando de acción mediante el Portal para desarrolladores](#create-an-action-command-using-developer-portal)
* [Crear un comando de acción manualmente](#create-an-action-command-manually)

### <a name="create-an-action-command-using-developer-portal"></a>Creación de un comando de acción mediante el Portal para desarrolladores

Puede crear un comando de acción mediante **el Portal para desarrolladores**.

> [!NOTE]
> El requisito previo para crear un comando de acción es que ya haya creado una extensión de mensaje. Para obtener información sobre cómo crear una extensión de mensaje, vea [crear una extensión de mensaje](~/messaging-extensions/how-to/create-messaging-extension.md).

Para crear un comando de acción:

1. Abra **el Portal para desarrolladores** en el cliente de Microsoft Teams y seleccione la pestaña **Aplicaciones** . Si ya ha creado el paquete de la aplicación en **el Portal para desarrolladores**, seleccione en la lista. Si no ha creado un paquete de aplicación, importe uno existente.
1. Después de importar un paquete de aplicación, seleccione **Extensiones de mensaje** en **Características de la aplicación**.
1. Para crear una extensión de mensaje, necesita un bot registrado de Microsoft. Puede usar un bot existente o crear uno nuevo. Seleccione **la opción Crear nuevo bot** , asigne un nombre al nuevo bot y, a continuación, seleccione **Crear**.

   :::image type="content" source="../../../assets/images/tdp/bot-page.png" alt-text="En la captura de pantalla se muestra cómo crear un bot en el Portal para desarrolladores.":::

1. Para usar un bot existente, seleccione **Seleccionar un bot existente** y elija los bots existentes en la lista desplegable o seleccione **Escribir un identificador de bot** si ya ha creado un identificador de bot.

1. Seleccione el ámbito de la extensión de mensajería y seleccione **Guardar**.

1. Seleccione **Agregar un comando** en la sección **Comando** para incluir los comandos, que decide el comportamiento de la extensión de mensaje.

   :::image type="content" source="../../../assets/images/tdp/add-a-command.PNG" alt-text="Captura de pantalla que muestra cómo agregar un comando para definir el comportamiento de la extensión de mensaje.":::

1. Seleccione **Acción** y, a continuación, seleccione Tipo de parámetro.

1. Escriba **Id. de comando**, **Título de comando** y **Descripción del comando**.

1. Escriba todos los parámetros y seleccione el tipo de entrada en la lista desplegable.

   :::image type="content" source="../../../assets/images/tdp/add-a-command-parameter.PNG" alt-text="Captura de pantalla que muestra cómo agregar parámetros para definir el comando para la extensión de mensaje.":::

1. Seleccione **Agregar un dominio** en **Vínculos de vista previa**.

1. Escriba dominio válido y, a continuación, seleccione **Agregar**.

   :::image type="content" source="../../../assets/images/tdp/add-domain.PNG" alt-text="Captura de pantalla que muestra cómo agregar un dominio válido a la extensión de mensajería para las desplegadas de vínculos.":::

1. Haga clic en **Guardar**.

   :::image type="content" source="../../../assets/images/tdp/add-a-command-save.PNG" alt-text="Captura de pantalla que muestra cómo guardar toda la configuración y los parámetros de la extensión de mensaje.":::

**Para agregar parámetros adicionales**

1. Seleccione elipse en la sección de comandos y, a continuación, seleccione **Editar parámetro**.

   :::image type="content" source="../../../assets/images/tdp/edit-parameters.PNG" alt-text="Capturas de pantalla que muestran cómo agregar parámetros adicionales para la extensión de mensaje.":::

1. Seleccione **Agregar parámetros** y escriba todos los parámetros.

   :::image type="content" source="../../../assets/images/tdp/add-parameter.PNG" alt-text="Captura de pantalla que muestra cómo agregar parámetros adicionales para la extensión de mensaje."lightbox="../../../assets/images/tdp/add-a-parameters.PNG":::

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
    "botId": "c8fa3cf6-b1f0-4ba8-a5bf-a241bc29adf3",
    "scopes": [
      "personal",
      "groupchat"
    ],
    "commands": [
      {
        "id": "To do",
        "type": "action",
        "title": "Create To do",
        "description": "Create a To do",
        "initialRun": true,
        "fetchTask": false,
        "context": [
          "commandBox",
          "compose"
        ],
        "parameters": [
          {
            "name": "Name",
            "title": "Title",
            "description": "To do Title",
            "inputType": "text"
          },
          {
            "name": "Description",
            "title": "Description",
            "description": "Description of the task",
            "inputType": "textarea"
          },
          {
            "name": "Date",
            "title": "Date",
            "description": "Due date for the task",
            "inputType": "date"
          }
        ]
      }
    ],
    "canUpdateConfiguration": true,
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "yourapp.onmicrosoft.com"
          ]
        }
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
