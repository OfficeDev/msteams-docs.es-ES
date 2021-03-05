---
title: Definir comandos de búsqueda de extensión de mensajería
author: clearab
description: Definir comandos de búsqueda de extensión de mensajería para aplicaciones de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 18bac3049fec8fead168c12f2832bfbbb72cf609
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449272"
---
# <a name="define-messaging-extension-search-commands"></a>Definir comandos de búsqueda de extensión de mensajería

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Los comandos de búsqueda de extensión de mensajería permiten a los usuarios buscar en sistemas externos e insertar los resultados de esa búsqueda en un mensaje en forma de tarjeta.

> [!NOTE]
> El límite de tamaño de la tarjeta de resultados es de 28 KB. La tarjeta no se envía si su tamaño supera los 28 KB. 

## <a name="choose-messaging-extension-invoke-locations"></a>Elegir ubicaciones de invocación de extensión de mensajería

Lo primero que debe decidir es desde dónde se puede desencadenar el comando de búsqueda (o, específicamente, *invocarlo).* El comando de búsqueda se puede invocar desde una o ambas de las siguientes ubicaciones:

* Los botones de la parte inferior del área del mensaje de redacción
* Por @mentioning en el cuadro de comandos

Cuando se invoca desde el área del mensaje de redacción, el usuario tendrá la opción de enviar los resultados a la conversación. Cuando se invoca desde el cuadro de comandos, el usuario puede interactuar con la tarjeta resultante o copiarla para usarla en otro lugar.

## <a name="add-the-command-to-your-app-manifest"></a>Agregar el comando al manifiesto de la aplicación

Ahora que has decidido cómo interactuarán los usuarios con el comando de búsqueda, es el momento de agregarlo al manifiesto de la aplicación. Para ello, agregarás un nuevo objeto al nivel superior del JSON del `composeExtension` manifiesto de la aplicación. Puedes hacerlo con la ayuda de App Studio o manualmente.

### <a name="create-a-command-using-app-studio"></a>Crear un comando con App Studio

El requisito previo para crear un comando de búsqueda es que ya debe crear una extensión de mensajería. Para obtener información sobre cómo crear una extensión de mensajería, vea [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).

**Para crear un comando de búsqueda**

1. En el cliente de Microsoft Teams, abra **App Studio** y seleccione la pestaña Editor **de manifiestos.**
1. Si ya creaste un paquete de aplicación en **App Studio,** eligelo en la lista. Si no has creado un paquete de aplicación, importa uno existente.
1. Después de importar un paquete de aplicación, selecciona **Extensiones de mensajería en** **Funcionalidades**.
1. Seleccione **Agregar** en la **sección Comando** de la página extensiones de mensajería.
1. Elija **Permitir que los usuarios consulten su servicio para** obtener información e insertarla en un mensaje .
1. Agregue un **identificador de comando** y un **título**.
1. Seleccione la ubicación desde la que se debe desencadenar el comando de búsqueda. Seleccionar mensaje **no** modifica actualmente el comportamiento del comando de búsqueda.
1. Agregue el parámetro de búsqueda y **seleccione Guardar**.
 
### <a name="manually-create-a-command"></a>Crear manualmente un comando

Para agregar manualmente el comando de búsqueda de extensión de mensajería al manifiesto de la aplicación, tendrás que agregar los siguientes parámetros a la `composeExtension.commands` matriz de objetos.

| Nombre de propiedad | Finalidad | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | Identificador único que se asigna a este comando. La solicitud de usuario incluirá este identificador. | Sí | 1.0 |
| `title` | Nombre del comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `description` | Texto de ayuda que indica lo que hace este comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Debe ser `query` | No | 1.4 |
|`initialRun` | Si se establece en **true,** indica que este comando debe ejecutarse tan pronto como el usuario elija este comando en la interfaz de usuario. | No | 1.0 |
| `context` | Matriz opcional de valores que define el contexto en el que está disponible la acción de búsqueda. Los valores posibles `message` `compose` son , o `commandBox` . El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |

También tendrás que agregar los detalles del parámetro de búsqueda, que definirá el texto visible para el usuario en el cliente de Teams.

| Nombre de propiedad | Finalidad | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `parameters` | Lista estática de parámetros para el comando. | No | 1.0 |
| `parameter.name` | Nombre del parámetro. Esto se envía al servicio en la solicitud de usuario. | Sí | 1.0 |
| `parameter.description` | Describe los propósitos de este parámetro o un ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Título o etiqueta de parámetros fáciles de usar cortos. | Sí | 1.0 |
| `parameter.inputType` | Se establece en el tipo de entrada necesario. Los valores posibles `text` incluyen , , , , , `textarea` `number` `date` `time` `toggle` . El valor predeterminado está establecido en `text` | No | 1.4 |

#### <a name="app-manifest-example"></a>Ejemplo de manifiesto de la aplicación

A continuación se muestra un ejemplo `composeExtensions` de un objeto que define un comando de búsqueda. No es un ejemplo del manifiesto completo, para el esquema de manifiesto de aplicación completo vea: [Esquema de manifiesto de aplicación](~/resources/schema/manifest-schema.md).

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

Ahora que ha agregado el comando de búsqueda, tendrá que controlar [la solicitud de búsqueda](~/messaging-extensions/how-to/search-commands/respond-to-search.md).

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
