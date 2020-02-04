---
title: Definir comandos de acción de la extensión de mensajería
author: clearab
description: Información general sobre las extensiones de mensajería en la plataforma de Microsoft Teams
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 7eb734258aa34c69fa34d1413b2d3dab88e0113a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675770"
---
# <a name="define-messaging-extension-action-commands"></a>Definir comandos de acción de la extensión de mensajería

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Los comandos de acción permiten presentar a los usuarios un elemento emergente modal (denominado módulo de tareas en Microsoft Teams) para recopilar o Mostrar información, luego procesar su interacción y enviar información de vuelta a teams. Antes de crear el comando tendrá que decidir:

1. ¿Desde dónde se puede activar el comando de acción?
1. ¿Cómo se creará el módulo de tareas?
1. ¿Se enviará el mensaje final o la tarjeta al canal desde un bot, o bien se insertará el mensaje o la tarjeta en el área de mensaje de redacción para que el usuario lo envíe?

## <a name="choose-action-command-invoke-locations"></a>Comando elegir acción invocar ubicaciones

Lo primero que debe decidir es donde se puede desencadenar el comando de acción (o más concretamente, *invocado*) desde. Al especificar el `context` en el manifiesto de la aplicación, se puede invocar al comando desde una o varias de las siguientes ubicaciones:

* Botones de la parte inferior del área de mensaje de redacción.
* @Mentioning la aplicación en el cuadro comando. Nota: no puede responder con un mensaje de bot insertado directamente en la conversación si la extensión de mensajería se invoca desde el cuadro de comandos.
* Directamente desde un mensaje existente a través del... menú de desbordamiento en un mensaje. Nota: la invocación inicial a su bot incluirá un objeto JSON que contiene el mensaje desde el que se invocó, que puede procesar antes de presentarlo con un módulo de tareas.

## <a name="choose-how-to-build-your-task-module"></a>Elegir cómo crear el módulo de tareas

Además de elegir desde dónde se puede invocar el comando, también debe elegir cómo rellenar el formulario en el módulo de tareas para los usuarios. Tiene tres opciones para crear el formulario que se representa en el módulo de tareas:

* **Lista estática de parámetros** : es la opción más sencilla. Puede definir una lista de parámetros (campos de entrada) en el manifiesto de la aplicación que se representará en el cliente de Microsoft Teams. No se puede controlar el formato con esta opción.
* **Tarjeta adaptable** : puede elegir usar una tarjeta adaptable, que proporciona un mayor control sobre la interfaz de usuario, pero sigue limitando los controles y las opciones de formato disponibles.
* **Vista Web incrustada** : Si necesita controlar completamente la interfaz de usuario y los controles, puede optar por incrustar una vista web personalizada en el módulo de tareas.

Si elige crear el módulo de tareas con una lista estática de parámetros, la primera llamada a la extensión de mensajería será cuando un usuario envíe el módulo de tareas. Cuando se usa una vista Web incrustada o una tarjeta adaptable, la extensión de mensajería debe controlar un evento de invocación inicial del usuario, crear el módulo de tarea y devolverlo al cliente.

## <a name="choose-how-the-final-message-will-be-sent"></a>Elegir cómo se enviará el mensaje final

En la mayoría de los casos, el comando de acción dará como resultado una tarjeta insertada en el cuadro de mensaje de redacción. A continuación, el usuario puede decidir enviarlo al canal o al chat. El mensaje en este caso procede del usuario y el bot no podrá editar ni actualizar la tarjeta.

Si la extensión de mensajería se desencadena desde el cuadro de redacción o directamente desde un mensaje, el servicio web puede insertar la respuesta final directamente en el canal o el chat. En este caso, la tarjeta adaptable procede del bot, el bot podrá actualizarlo y el bot también puede responder al hilo de conversación si es necesario. Tendrá que agregar el `bot` objeto al manifiesto de la aplicación con el mismo identificador y definir los ámbitos apropiados.

## <a name="add-the-command-to-your-app-manifest"></a>Agregar el comando al manifiesto de la aplicación

Ahora que ha decidido cómo interactúan los usuarios con el comando de acción, es el momento de agregarlo al manifiesto de la aplicación. Para ello, agregará un nuevo `composeExtension` objeto al nivel superior del JSON del manifiesto de la aplicación. Puede hacerlo con la ayuda de App Studio, o bien manualmente.

### <a name="create-a-command-using-app-studio"></a>Crear un comando con App Studio

En los pasos siguientes se da por sentado que ya ha [creado una extensión de mensajería](~/messaging-extensions/how-to/create-messaging-extension.md).

1. En el cliente de Microsoft Teams, Abra **App Studio** y seleccione la pestaña **Editor de manifiestos** .
2. Si ya ha creado el paquete de la aplicación en App Studio, elija en la lista. Si no es así, puedes importar un paquete de aplicación existente.
3. Haga clic en el botón **Agregar** en la sección comando.
4. Elija **permitir que los usuarios desencadenen acciones en servicios externos mientras se encuentra dentro de Microsoft Teams**.
5. Si desea usar un conjunto estático de parámetros para crear el módulo de tareas, seleccione esa opción. De lo contrario, elija **recuperar un conjunto dinámico de parámetros de su bot**.
6. Agregue un **identificador de comando** y un **título**.
7. Seleccione el lugar desde el que desea que se desencadene el comando de acción.
8. Si está usando parámetros para el módulo de tareas, agregue el primero.
9. Click Save
10. Si necesita agregar más parámetros, haga clic en el botón **Agregar** de la sección **parámetros** para agregarlos.

### <a name="manually-create-a-command"></a>Crear manualmente un comando

Para agregar manualmente el comando de extensión de mensajería basada en acciones al manifiesto de la aplicación, deberá agregar los siguientes parámetros a la `composeExtension.commands` matriz de objetos.

| Nombre de la propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | IDENTIFICADOR único que asigna a este comando. La solicitud del usuario incluirá este identificador. | Sí | 1.0 |
| `title` | Nombre del comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Debe ser`action` | No | 1.4 |
| `fetchTask` | `true`para una tarjeta adaptable o una vista Web incrustada para el `false` módulo de tareas, para una lista estática de parámetros o cuando se carga la vista Web mediante un`taskInfo` | No | 1.4 |
| `context` | Matriz opcional de valores que define dónde se puede invocar la extensión de mensajería. Los valores posibles `message`son `compose`, o `commandBox`. El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |

Si usa una lista de parámetros estática, también los agregará.

| Nombre de la propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `parameters` | Lista estática de parámetros para el comando. Usar solo cuando `fetchTask` es`false` | No | 1.0 |
| `parameter.name` | Nombre del parámetro. Se envía al servicio en la solicitud del usuario. | Sí | 1.0 |
| `parameter.description` | Describe los propósitos de este parámetro o el ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Nombre corto o etiqueta del parámetro sencillo para el usuario. | Sí | 1.0 |
| `parameter.inputType` | Se establece en el tipo de entrada requerido. Los valores posibles `text`son `textarea`: `number`, `date`, `time`, `toggle`,. El valor predeterminado está establecido en`text` | No | 1.4 |

Si usa una vista Web incrustada, puede agregar opcionalmente el `taskInfo` objeto para recuperar la vista Web sin llamar a su bot directamente. Si decide usar esta opción, el comportamiento es similar al uso de una lista estática de parámetros en que la primera interacción con el bot [responderá a la acción de envío del módulo de tarea](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md). Si usa un `taskInfo` objeto, asegúrese de establecer también el `fetchTask` parámetro en. `false`

| Nombre de la propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
|`taskInfo`|Especificar el módulo de tarea para cargar previamente cuando se usa un comando de extensión de mensajería| No | 1.4 |
|`taskInfo.title`|Título del módulo de tarea inicial|No | 1.4 |
|`taskInfo.width`|Ancho del módulo de tareas, ya sea un número en píxeles o un diseño predeterminado, como "Large", "Medium" o "Small"|No | 1.4 |
|`taskInfo.height`|Alto del módulo de tareas: número en píxeles o diseño predeterminado, como "Large", "Medium" o "Small"|No | 1.4 |
|`taskInfo.url`|Dirección URL de vista Web inicial|No | 1.4 |

#### <a name="app-manifest-example"></a>Ejemplo de manifiesto de la aplicación

A continuación, se muestra un ejemplo `composeExtensions` de un objeto que define dos comandos de acción. No es un ejemplo del manifiesto completo, para el esquema completo del manifiesto de la aplicación, vea: [esquema del manifiesto](~/resources/schema/manifest-schema.md)de la aplicación.

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
        "fetchTask": true,
      }
    ]
  }
]
...
```

## <a name="next-steps"></a>Siguientes pasos

Si usa una tarjeta adaptable o una vista Web incrustada sin un `taskInfo` objeto, querrá:

* [Crear y responder con un módulo de tareas](~/messaging-extensions/how-to/action-commands/create-task-module.md)

Si usa parámetros o una vista Web incrustada con un `taskInfo` objeto, el siguiente paso es:

* [Responder al envío del módulo de tareas](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
