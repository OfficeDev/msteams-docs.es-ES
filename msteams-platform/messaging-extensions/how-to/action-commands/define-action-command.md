---
title: Definir comandos de acción de extensión de mensajería
author: clearab
description: Información general sobre los comandos de acción de extensión de mensajería
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: be2135477c4234187f374aef215f90e8329fb74e
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778404"
---
# <a name="define-messaging-extension-action-commands"></a>Definir comandos de acción de extensión de mensajería

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Los comandos de acción le permiten presentar a los usuarios un elemento emergente modal (denominado módulo de tareas en Teams) para recopilar o mostrar información y, a continuación, procesar su interacción y enviar información a Teams. Antes de crear el comando, tendrás que decidir:

1. ¿Desde dónde se puede desencadenar el comando de acción?
1. ¿Cómo se creará el módulo de tareas?
1. ¿Se enviará el mensaje o la tarjeta final al canal desde un bot o se insertará el mensaje o la tarjeta en el área de redacción del mensaje para que el usuario la envíe?

## <a name="choose-action-command-invoke-locations"></a>Elegir ubicaciones de invocación de comando de acción

Lo primero que debes decidir es desde dónde se puede desencadenar el comando de acción (o más específicamente, *invocarlo).* Al especificar el manifiesto de la aplicación, el comando se puede invocar desde una o `context` varias de las siguientes ubicaciones:

* Los botones situados en la parte inferior del área de redacción de mensajes.
* Al @mentioning la aplicación en el cuadro de comando. Nota: No puede responder con un mensaje de bot insertado directamente en la conversación si la extensión de mensajería se invoca desde el cuadro de comando.
* Directamente desde un mensaje existente a través de ... menú de desbordamiento de un mensaje. Nota: La invocación inicial al bot incluirá un objeto JSON que contiene el mensaje desde el que se invocó, que puede procesar antes de presentarlos con un módulo de tareas.

## <a name="choose-how-to-build-your-task-module"></a>Elegir cómo crear el módulo de tareas

Además de elegir desde dónde se puede invocar el comando, también debe elegir cómo rellenar el formulario en el módulo de tareas para los usuarios. Tiene tres opciones para crear el formulario que se representa dentro del módulo de tareas:

* **Lista estática de parámetros:** esta es la opción más sencilla. Puede definir una lista de parámetros (campos de entrada) en el manifiesto de la aplicación que representará el cliente de Teams. No puede controlar el formato con esta opción.
* **Tarjeta adaptable:** puedes elegir usar una tarjeta adaptable, lo que proporciona un mayor control sobre la interfaz de usuario, pero sigue limitando los controles disponibles y las opciones de formato.
* **Vista web incrustada:** si necesita un control total sobre la interfaz de usuario y los controles, puede elegir insertar una vista web personalizada en el módulo de tareas.

Si decide crear el módulo de tareas con una lista estática de parámetros, la primera llamada a la extensión de mensajería será cuando un usuario envíe el módulo de tareas. Al usar una vista web incrustada o una tarjeta adaptable, la extensión de mensajería tendrá que controlar un evento de invocación inicial del usuario, crear el módulo de tareas y devolverlo al cliente.

## <a name="choose-how-the-final-message-will-be-sent"></a>Elegir cómo se enviará el mensaje final

En la mayoría de los casos, el comando de acción dará como resultado una tarjeta insertada en el cuadro de mensaje de redacción. A continuación, el usuario puede decidir enviarlo al canal o chat. En este caso, el mensaje proviene del usuario y el bot no podrá editar ni actualizar aún más la tarjeta.

Si la extensión de mensajería se desencadena desde el cuadro de redacción o directamente desde un mensaje, el servicio web puede insertar la respuesta final directamente en el canal o chat. En este caso, la tarjeta adaptable proviene del bot, el bot podrá actualizarlo y el bot también puede responder al hilo de conversación si es necesario. Deberás agregar el objeto al manifiesto de la aplicación con el mismo identificador y `bot` definir los ámbitos adecuados.

## <a name="add-the-command-to-your-app-manifest"></a>Agregar el comando al manifiesto de la aplicación

Ahora que has decidido cómo interactuarán los usuarios con el comando de acción, es el momento de agregarlo al manifiesto de la aplicación. Para ello, agregará un nuevo objeto al nivel superior del JSON del `composeExtension` manifiesto de la aplicación. Puedes hacerlo con la ayuda de App Studio o manualmente.

### <a name="create-a-command-using-app-studio"></a>Crear un comando con App Studio

En los pasos siguientes se supone que ya ha [creado una extensión de mensajería.](~/messaging-extensions/how-to/create-messaging-extension.md)

1. En el cliente de Microsoft Teams, abra **App Studio** y seleccione la pestaña **Editor de** manifiestos.
2. Si ya has creado el paquete de la aplicación en App Studio, elíbalo de la lista. Si no es así, puedes importar un paquete de aplicación existente.
3. Haga clic **en el botón** Agregar de la sección Comando.
4. Elija **Permitir que los usuarios desencadene acciones en servicios externos dentro de Teams.**
5. Si desea usar un conjunto estático de parámetros para crear el módulo de tareas, seleccione esa opción. De lo contrario, **elija capturar un conjunto dinámico de parámetros del bot.**
6. Agregue un **identificador de comando** y un **título.**
7. Selecciona desde dónde quieres que se desencadene el comando de acción.
8. Si usa parámetros para el módulo de tareas, agregue el primero.
9. Click Save
10. Si necesita agregar más parámetros, haga clic en el **botón** Agregar de la **sección Parámetros** para agregarlos.

### <a name="manually-create-a-command"></a>Crear manualmente un comando

Para agregar manualmente el comando de extensión de mensajería basada en acciones al manifiesto de la aplicación, deberá agregar los siguientes parámetros a la `composeExtension.commands` matriz de objetos.

| Nombre de propiedad | Finalidad | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | Identificador único que se asigna a este comando. La solicitud de usuario incluirá este identificador. | Sí | 1.0 |
| `title` | Nombre del comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Debe ser `action` | No | 1.4 |
| `fetchTask` | `true` para una tarjeta adaptable o una vista web incrustada para el módulo de tareas, para una lista estática de parámetros o al cargar la vista `false` web por un `taskInfo` | No | 1.4 |
| `context` | Matriz opcional de valores que define desde dónde se puede invocar la extensión de mensajería. Los valores posibles `message` son `compose` , o `commandBox` . El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |

Si usa una lista estática de parámetros, también los agregará.

| Nombre de propiedad | Finalidad | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `parameters` | Lista estática de parámetros para el comando. Solo se usa cuando `fetchTask` está `false` | No | 1.0 |
| `parameter.name` | Nombre del parámetro. Esto se envía a su servicio en la solicitud de usuario. | Sí | 1.0 |
| `parameter.description` | Describe los propósitos de este parámetro o un ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Título o etiqueta de parámetros descriptivos cortos. | Sí | 1.0 |
| `parameter.inputType` | Se establece en el tipo de entrada necesario. Los valores posibles `text` son , , , , `textarea` `number` `date` `time` `toggle` . El valor predeterminado está establecido en `text` | No | 1.4 |

Si usa una vista web incrustada, opcionalmente puede agregar el objeto para capturar la vista web sin llamar `taskInfo` al bot directamente. Si decide usar esta opción, el comportamiento es similar al uso de una lista estática de parámetros en que la primera interacción con el bot responderá a la acción de envío del módulo [de tareas.](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md) Si usa un `taskInfo` objeto, asegúrese de establecer también `fetchTask` el parámetro en `false` .

| Nombre de propiedad | Finalidad | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
|`taskInfo`|Especificar el módulo de tareas que se debe precargar al usar un comando de extensión de mensajería| No | 1.4 |
|`taskInfo.title`|Título inicial del módulo de tareas|No | 1.4 |
|`taskInfo.width`|Ancho del módulo de tareas: un número en píxeles o un diseño predeterminado, como "grande", "mediano" o "pequeño".|No | 1.4 |
|`taskInfo.height`|Alto del módulo de tareas: un número en píxeles o un diseño predeterminado, como "grande", "mediano" o "pequeño".|No | 1.4 |
|`taskInfo.url`|Dirección URL inicial de la vista web|No | 1.4 |

#### <a name="app-manifest-example"></a>Ejemplo de manifiesto de la aplicación

A continuación se muestra un ejemplo de `composeExtensions` un objeto que define dos comandos de acción. No es un ejemplo del manifiesto completo, para ver el esquema de manifiesto completo de la aplicación, vea: [Esquema del manifiesto de la aplicación.](~/resources/schema/manifest-schema.md)

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

## <a name="next-steps"></a>Siguientes pasos

Si usas una tarjeta adaptable o una vista web incrustada sin un `taskInfo` objeto, querrás:

* [Crear y responder con un módulo de tareas](~/messaging-extensions/how-to/action-commands/create-task-module.md)

Si usa parámetros o una vista web incrustada con un objeto, el `taskInfo` siguiente paso es:

* [Responder al envío del módulo de tareas](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
