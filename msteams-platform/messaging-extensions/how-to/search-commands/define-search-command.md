---
title: Definir comandos de búsqueda de extensiones de mensajería
author: clearab
description: Definir comandos de búsqueda de extensiones de mensajería para las aplicaciones de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b6837fb8a131d8ce3e2bbd0c51c2861dbffda2bc
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676020"
---
# <a name="define-messaging-extension-search-commands"></a>Definir comandos de búsqueda de extensiones de mensajería

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Los comandos de búsqueda de extensiones de mensajería permiten a los usuarios buscar en sistemas externos e insertar los resultados de la búsqueda en un mensaje en forma de una tarjeta.

## <a name="choose-messaging-extension-invoke-locations"></a>Elegir ubicaciones de invocación de extensiones de mensajería

Lo primero que debe decidir es donde se puede desencadenar el comando de búsqueda (o más concretamente, *invocado*) desde. Se puede invocar el comando de búsqueda desde una o ambas de las siguientes ubicaciones:

* Botones en la parte inferior del área de mensaje de redacción
* Por @mentioning en el cuadro comando

Cuando se invoca desde el área de mensaje de redacción, el usuario tiene la opción de enviar los resultados a la conversación. Cuando se invoca desde el cuadro comando, el usuario puede interactuar con la tarjeta resultante o copiarla para usarla en otro lugar.

## <a name="add-the-command-to-your-app-manifest"></a>Agregar el comando al manifiesto de la aplicación

Ahora que ha decidido cómo interactúan los usuarios con el comando de búsqueda, es el momento de agregarlo al manifiesto de la aplicación. Para ello, agregará un nuevo `composeExtension` objeto al nivel superior del JSON del manifiesto de la aplicación. Puede hacerlo con la ayuda de App Studio, o bien manualmente.

### <a name="create-a-command-using-app-studio"></a>Crear un comando con App Studio

En los pasos siguientes se da por sentado que ya ha [creado una extensión de mensajería](~/messaging-extensions/how-to/create-messaging-extension.md).

1. En el cliente de Microsoft Teams, Abra **App Studio** y seleccione la pestaña **Editor de manifiestos** .
2. Si ya ha creado el paquete de la aplicación en App Studio, elija en la lista. Si no es así, puedes importar un paquete de aplicación existente.
3. Haga clic en el botón **Agregar** en la sección comando.
4. Elija **permitir que los usuarios consulten la información del servicio e insértela en un mensaje**.
5. Agregue un **identificador de comando** y un **título**.
6. Seleccione el lugar desde el que desea que se desencadene el comando de búsqueda. La selección de un **mensaje** no altera actualmente el comportamiento del comando de búsqueda.
7. Agregue el parámetro de búsqueda.
8. Haga clic en Guardar.

### <a name="manually-create-a-command"></a>Crear manualmente un comando

Para agregar manualmente el comando de búsqueda de extensiones de mensajería al manifiesto de la aplicación, deberá agregar los siguientes parámetros a `composeExtension.commands` la matriz de objetos.

| Nombre de la propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | IDENTIFICADOR único que asigna a este comando. La solicitud del usuario incluirá este identificador. | Sí | 1.0 |
| `title` | Nombre del comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `description` | Texto de ayuda que indica lo que hace este comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Debe ser`query` | No | 1.4 |
|`initialRun` | Si se establece en **true**, indica que este comando debe ejecutarse en cuanto el usuario seleccione este comando en la interfaz de usuario. | No | 1.0 |
| `context` | Matriz opcional de valores que define el contexto en el que está disponible la acción de búsqueda. Los valores posibles `message`son `compose`, o `commandBox`. El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |

También necesitará agregar los detalles del parámetro de búsqueda, que definirán el texto visible para el usuario en el cliente de Microsoft Teams.

| Nombre de la propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `parameters` | Lista estática de parámetros para el comando. | No | 1.0 |
| `parameter.name` | Nombre del parámetro. Se envía al servicio en la solicitud del usuario. | Sí | 1.0 |
| `parameter.description` | Describe los propósitos de este parámetro o el ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Nombre corto o etiqueta del parámetro sencillo para el usuario. | Sí | 1.0 |
| `parameter.inputType` | Se establece en el tipo de entrada requerido. Los valores posibles `text`son `textarea`: `number`, `date`, `time`, `toggle`,. El valor predeterminado está establecido en`text` | No | 1.4 |

#### <a name="app-manifest-example"></a>Ejemplo de manifiesto de la aplicación

A continuación, se muestra un ejemplo `composeExtensions` de un objeto que define un comando de búsqueda. No es un ejemplo del manifiesto completo, para el esquema completo del manifiesto de la aplicación, vea: [esquema del manifiesto](~/resources/schema/manifest-schema.md)de la aplicación.

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}
```

## <a name="next-steps"></a>Siguientes pasos

Ahora que ha agregado el comando de búsqueda, deberá [controlar la solicitud de búsqueda](~/messaging-extensions/how-to/search-commands/respond-to-search.md).

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]