---
title: Definir comandos de acción de extensión de mensajería
author: clearab
description: Información general sobre los comandos de acción de extensión de mensajería
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 51c2ce5ac3b8ab265d9bec0b1101ba18138a9365
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696948"
---
# <a name="define-messaging-extension-action-commands"></a>Definir comandos de acción de extensión de mensajería

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Los comandos de acción permiten presentar a los usuarios un elemento emergente modal denominado módulo de tareas en Teams. El módulo de tareas recopila o muestra información, procesa la interacción y envía la información de vuelta a Teams. Este documento le guía sobre cómo seleccionar ubicaciones de invocación de comandos de acción, crear el módulo de tareas, enviar el mensaje final o la tarjeta, crear un comando de acción con app studio o crearlo manualmente. 

Antes de crear el comando de acción, debe decidir los siguientes factores:

1. [¿Desde dónde se puede desencadenar el comando de acción?](#select-action-command-invoke-locations)
1. [¿Cómo se creará el módulo de tareas?](#select-how-to-create-your-task-module)
1. [¿Se enviará el mensaje final o la tarjeta al canal desde un bot o se insertará el mensaje o la tarjeta en el área del mensaje de redacción para que el usuario envíe?](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a>Seleccionar ubicaciones de invocación de comandos de acción

En primer lugar, debe decidir la ubicación desde la que se debe invocar el comando de acción. Al especificar el manifiesto de la aplicación, se puede invocar el comando `context` desde una o varias de las siguientes ubicaciones:

* Área de redacción de mensajes: los botones situados en la parte inferior del área del mensaje de redacción.
* Cuadro de comando: @mentioning la aplicación en el cuadro de comandos. 
   > [!NOTE]
   > Si se invoca la extensión de mensajería desde el cuadro de comandos, no puede responder con un mensaje de bot insertado directamente en la conversación.

* Mensaje: directamente desde un mensaje existente a través del `...` menú de desbordamiento de un mensaje. 
    > [!NOTE] 
    > La invocación inicial al bot incluye un objeto JSON que contiene el mensaje desde el que se invocó. Puede procesar el mensaje antes de presentarlo con un módulo de tareas.

La siguiente imagen muestra las ubicaciones desde las que se invoca el comando action:

![ubicaciones de invocación de comandos de acción](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a>Seleccionar cómo crear el módulo de tareas

Además de seleccionar desde dónde se puede invocar el comando, también debe seleccionar cómo rellenar el formulario en el módulo de tareas para los usuarios. Tiene las tres opciones siguientes para crear el formulario que se representa dentro del módulo de tareas:   

* **Lista estática de parámetros:** este es el método más sencillo. Puedes definir una lista de parámetros en el manifiesto de la aplicación que representa el cliente de Teams, pero no puedes controlar el formato en este caso.
* **Tarjeta adaptable:** puedes seleccionar usar una tarjeta adaptable, que proporciona un mayor control sobre la interfaz de usuario, pero aún te limita a los controles y opciones de formato disponibles.
* **Vista web incrustada:** puede seleccionar insertar una vista web personalizada en el módulo de tareas para tener un control completo sobre la interfaz de usuario y los controles. 

Si selecciona crear el módulo de tareas con una lista estática de parámetros y cuando el usuario envía el módulo de tareas, se llama a la extensión de mensajería. Al usar una vista web incrustada o una tarjeta adaptable, la extensión de mensajería debe controlar un evento de invocación inicial del usuario, crear el módulo de tareas y devolverlo al cliente.

## <a name="select-how-the-final-message-is-sent"></a>Seleccionar cómo se envía el mensaje final

En la mayoría de los casos, el comando action da como resultado una tarjeta insertada en el cuadro de mensaje de redacción. El usuario puede enviarlo al canal o chat. En este caso, el mensaje proviene del usuario y el bot no puede editar ni actualizar aún más la tarjeta.

Si la extensión de mensajería se invoca desde el cuadro de redacción o directamente desde un mensaje, el servicio web puede insertar la respuesta final directamente en el canal o chat. En este caso, la tarjeta adaptable proviene del bot, el bot la actualiza y responde al hilo de conversación si es necesario. Debes agregar el objeto al manifiesto de la aplicación `bot` con el mismo identificador y definir los ámbitos adecuados.

## <a name="add-the-action-command-to-your-app-manifest"></a>Agregar el comando action al manifiesto de la aplicación

Para agregar el comando action al manifiesto de la aplicación, debes agregar un nuevo objeto al `composeExtension` nivel superior del JSON del manifiesto de la aplicación. Puede usar una de las siguientes maneras de hacerlo:

* [Crear un comando de acción con App Studio](#create-an-action-command-using-app-studio)
* [Crear un comando de acción manualmente](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a>Crear un comando de acción con App Studio

> [!NOTE]
> El requisito previo para crear un comando de acción es que ya ha creado una extensión de mensajería. Para obtener información sobre cómo crear una extensión de mensajería, vea [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).

**Para crear un comando de acción**

1. Abre **App Studio** desde el cliente de Microsoft Teams y selecciona la pestaña Editor de **manifiestos.**
1. Si ya creaste el paquete de la aplicación en **App Studio,** selecciónelo en la lista. Si no has creado un paquete de aplicación, importa uno existente.
1. Después de importar un paquete de aplicación, selecciona **Extensiones de mensajería en** **Funcionalidades**. Obtiene una ventana emergente para configurar la extensión de mensajería.
1. Selecciona **Configurar en la** ventana para incluir la extensión de mensajería en la experiencia de la aplicación. En la siguiente imagen se muestra la ventana de configuración de la extensión de mensajería:

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>
    
1. Para crear una extensión de mensajería, necesita un bot registrado de Microsoft. Puede usar un bot existente o crear un bot nuevo. Seleccione **Crear nueva opción de bot,** asigne un nombre al nuevo bot y seleccione **Crear**. En la siguiente imagen se muestra la creación de bots para la extensión de mensajería:

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. Seleccione **Agregar** en la **sección Comando** de la página extensiones de mensajería para incluir los comandos que deciden el comportamiento de la extensión de mensajería.   
La siguiente imagen muestra la adición de comandos para la extensión de mensajería:

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. Seleccione **Permitir que los usuarios desencadene acciones en servicios externos mientras están dentro de Teams**. En la siguiente imagen se muestra la selección de comandos de acción:

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>
    
1. Para usar un conjunto estático de parámetros para crear el módulo de tareas, seleccione Definir un conjunto de parámetros **estáticos para el comando**. 

    En la imagen siguiente se muestra la selección del parámetro estático del comando de acción:

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/> 
   
    La siguiente imagen muestra un ejemplo de configuración de parámetros estáticos: 

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    En la siguiente imagen se muestra un ejemplo de pruebas de parámetros estáticos:

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. Para usar parámetros dinámicos, seleccione **Capturar un conjunto dinámico de parámetros del bot**. En la siguiente imagen se muestra la selección del parámetro de comando de acción:

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>
    
1. Agregue un **identificador de comando** y un **título**.
1. Seleccione la ubicación desde la que desea invocar el comando de acción. La siguiente imagen muestra la ubicación de invocación del comando de acción:

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. Seleccione **Guardar**.
1. Para agregar más parámetros, seleccione el **botón Agregar** en la **sección Parámetros.**

### <a name="create-an-action-command-manually"></a>Crear un comando de acción manualmente

Para agregar manualmente el comando de extensión de mensajería basada en acciones al manifiesto de la aplicación, debe agregar los siguientes parámetros a la `composeExtension.commands` matriz de objetos:

| Nombre de propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | Esta propiedad es un identificador único que se asigna a este comando. La solicitud de usuario incluye este identificador. | Sí | 1.0 |
| `title` | Esta propiedad es un nombre de comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Esta propiedad debe ser `action` un . | No | 1.4 |
| `fetchTask` | Esta propiedad se establece en para una tarjeta adaptable o una vista web incrustada para el módulo de tareas, y para una lista estática de parámetros o al cargar la vista `true` `false` web mediante un `taskInfo` . | No | 1.4 |
| `context` | Esta propiedad es una matriz opcional de valores que define desde dónde se invoca la extensión de mensajería. Los valores posibles son`message`, `compose` o `commandBox`. El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |

Si usa una lista estática de parámetros, también debe agregar los siguientes parámetros:

| Nombre de propiedad | Objetivo | ¿Es necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `parameters` | Esta propiedad describe la lista estática de parámetros para el comando. Solo se usa cuando `fetchTask` es `false` . | No | 1.0 |
| `parameter.name` | Esta propiedad describe el nombre del parámetro. Esto se envía al servicio en la solicitud de usuario. | Sí | 1.0 |
| `parameter.description` | Esta propiedad describe los propósitos del parámetro o el ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Esta propiedad es un título o etiqueta de parámetros fáciles de usar. | Sí | 1.0 |
| `parameter.inputType` | Esta propiedad se establece en el tipo de entrada necesario. Los valores posibles `text` incluyen , , , , , `textarea` `number` `date` `time` `toggle` . El valor predeterminado se establece en `text` . | No | 1.4 |

Si usa una vista web incrustada, opcionalmente puede agregar el objeto para capturar la vista `taskInfo` web sin llamar directamente al bot. Si selecciona esta opción, el comportamiento es similar al de usar una lista estática de parámetros. En el caso de que la primera interacción con el bot [responde al módulo de tareas enviar acción](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md). Si usa un `taskInfo` objeto, debe establecer el `fetchTask` parámetro en `false` .

| Nombre de propiedad | Objetivo | ¿Es necesario? | Versión mínima del manifiesto |
|---|---|---|---|
|`taskInfo`|Especifique el módulo de tareas que se debe precargar al usar un comando de extensión de mensajería. | No | 1.4 |
|`taskInfo.title`|Título del módulo de tareas inicial. |No | 1.4 |
|`taskInfo.width`|Ancho del módulo de tareas, ya sea un número en píxeles o un diseño predeterminado como `large` , `medium` o `small` . |No | 1.4 |
|`taskInfo.height`|Alto del módulo de tareas, ya sea un número en píxeles o un diseño predeterminado como `large` , `medium` o `small` .|No | 1.4 |
|`taskInfo.url`|Dirección URL de vista web inicial.|No | 1.4 | 

#### <a name="app-manifest-example"></a>Ejemplo de manifiesto de la aplicación

La siguiente sección es un ejemplo de un `composeExtensions` objeto que define dos comandos de acción. No es un ejemplo del manifiesto completo. Para ver el esquema de manifiesto de aplicación completo, consulta [Esquema de manifiesto de la aplicación:](~/resources/schema/manifest-schema.md)

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
        "fetchTask": true,
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
        "fetchTask": true,
      }
    ]
  }
]
...
```

## <a name="code-sample"></a>Ejemplo de código

| Nombre de ejemplo           | Descripción | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Acción de extensión de mensajería de Teams| Describe cómo definir comandos de acción, crear módulo de tareas y responder a la acción de envío del módulo de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Búsqueda de extensión de mensajería de Teams   |  Describe cómo definir comandos de búsqueda y responder a las búsquedas.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Paso siguiente

Si usa una tarjeta adaptable o una vista web incrustada sin un objeto, el `taskInfo` siguiente paso es:

> [!div class="nextstepaction"]
> [Crear y responder con un módulo de tareas](~/messaging-extensions/how-to/action-commands/create-task-module.md)

Si usa los parámetros o una vista web incrustada con un `taskInfo` objeto, el siguiente paso es:

> [!div class="nextstepaction"]
> [Responder al envío del módulo de tareas](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

