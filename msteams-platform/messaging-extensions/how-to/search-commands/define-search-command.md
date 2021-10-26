---
title: Definir comandos de búsqueda de extensión de mensajería
author: surbhigupta
description: Definir comandos de búsqueda de extensión de mensajería para Microsoft Teams aplicaciones.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: none
ms.openlocfilehash: aaea89aa14e556dfa00e81e8ec72fe5fb4bbe744
ms.sourcegitcommit: 781e7b82240075e9d1f55e97f3f1dcbba82a5e4d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2021
ms.locfileid: "60566368"
---
# <a name="define-messaging-extension-search-commands"></a>Definir comandos de búsqueda de extensión de mensajería

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Los comandos de búsqueda de extensión de mensajería permiten a los usuarios buscar sistemas externos e insertar los resultados de esa búsqueda en un mensaje en forma de tarjeta. Este documento le guía sobre cómo seleccionar ubicaciones de invocar comandos de búsqueda y agregar el comando de búsqueda al manifiesto de la aplicación.

> [!NOTE]
> El límite de tamaño de la tarjeta de resultados es de 28 KB. La tarjeta no se envía si su tamaño supera los 28 KB.

## <a name="select-search-command-invoke-locations"></a>Seleccionar ubicaciones de invocación de comandos de búsqueda

El comando de búsqueda se invoca desde una o ambas de las siguientes ubicaciones:

* Área de redacción de mensajes: los botones situados en la parte inferior del área del mensaje de redacción.
* Cuadro de comando: @mentioning en el cuadro de comandos.

  Cuando se invoca el comando de búsqueda desde el área del mensaje de redacción, el usuario envía los resultados a la conversación. Cuando se invoca desde el cuadro de comandos, el usuario interactúa con la tarjeta resultante o la copia para su uso en otro lugar.

En la siguiente imagen se muestran las ubicaciones de invocación del comando de búsqueda:

![Ubicaciones de invocar comandos de búsqueda](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## <a name="add-the-search-command-to-your-app-manifest"></a>Agregar el comando de búsqueda al manifiesto de la aplicación

Para agregar el comando de búsqueda al manifiesto de la aplicación, debes agregar un nuevo objeto al nivel superior del JSON del `composeExtension` manifiesto de la aplicación. Puedes agregar el comando de búsqueda con la ayuda de App Studio o manualmente.

### <a name="create-a-search-command"></a>Crear un comando de búsqueda 

Puede crear un comando de búsqueda mediante ** App Studio** o **Developer Portal**.

> [!NOTE]
>  App Studio pronto se depricará. Configure, distribuya y administre las aplicaciones Teams con el nuevo [Portal de desarrolladores.](https://dev.teams.microsoft.com/)

# <a name="app-studio"></a>[App Studio](#tab/AS)

> [!NOTE]
> El requisito previo para crear un comando de búsqueda es que ya debe haber creado una extensión de mensajería. Para obtener información sobre cómo crear una extensión de mensajería, vea [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).

**Para crear un comando de búsqueda**

1. Abre **App Studio** desde el Microsoft Teams y selecciona la pestaña Editor **de** manifiestos.
1.  Si ya creaste el paquete de la aplicación **en App Studio,** selecciona de la lista. Si no has creado un paquete de aplicación, importa uno existente.
1. Después de importar el paquete de la aplicación, selecciona **Extensiones de mensajería en** **Funcionalidades**. Obtiene una ventana emergente para configurar la extensión de mensajería.
1. Selecciona **Configurar en la** ventana para incluir la extensión de mensajería en la experiencia de la aplicación. En la siguiente imagen se muestra la página de configuración de extensión de mensajería: 

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. Para crear la extensión de mensajería, necesita un bot registrado de Microsoft. Puede usar un bot existente o crear un bot nuevo. Seleccione **Crear nueva opción de bot,** asigne un nombre al nuevo bot y seleccione **Crear**. En la siguiente imagen se muestra la creación de bots para la extensión de mensajería:

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. Seleccione **Agregar** en la **sección Comando** de la página extensiones de mensajería para incluir los comandos que deciden el comportamiento de la extensión de mensajería.   
La siguiente imagen muestra la adición de comandos para la extensión de mensajería:

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. Seleccione **Permitir que los usuarios consulten su servicio para obtener información e insertarla en un mensaje**. La siguiente imagen muestra la selección del parámetro de comando de búsqueda:

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. Agregue un **identificador de comando** y un **título**.
1. Seleccione la ubicación desde la que se debe invocar el comando de búsqueda. Seleccionar mensaje **no** modifica actualmente el comportamiento del comando de búsqueda. La siguiente imagen muestra la ubicación de invocación del comando de búsqueda:

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. Agregue el parámetro de búsqueda y **seleccione Guardar**.

# <a name="developer-portal"></a>[Portal para desarrolladores](#tab/DP)

**Para crear un comando de búsqueda con Portal de desarrolladores**

1. Vaya a **[Portal para desarrolladores.](https://dev.teams.microsoft.com/)**
    
   <img src="~/assets/images/tdp/tdp_home_1.png" alt="Screenshot of TDP" width="500"/>
    
1. Vaya a **Aplicaciones**.
    
    <img width="500px" alt="Screenshot of TDP Open" src="~/assets/images/tdp/screen2.png"/>
    
1. Si ya creaste el paquete de la aplicación en **el Portal de desarrolladores,** selecciónelo en la lista. Si no has creado un paquete de aplicación, selecciona **Importar una aplicación existente.**

    <img width="500px" alt="Screenshot of import app in tdp" src="~/assets/images/tdp/screen3.png"/>

1. Vaya a **Características de la aplicación**.  

    <img width="500px" alt="TDP messaging extension" src="~/assets/images/tdp/tdp-me.png"/>

1. Seleccione **Extensiones de mensajería de** las características de la **aplicación**. Aparece una ventana emergente para configurar la extensión de mensajería.
    
   <img width="500px" alt="TDP messaging extension set up" src="~/assets/images/tdp/tdp-app-me.png"/>

1. Seleccione **un bot de extensión de** mensaje de la lista desplegable en **Id. de extensiones de mensaje** y seleccione **Guardar**.

    <img width="500px" alt="TDP messaging extension bot" src="~/assets/images/tdp/tdp-me-bot.png"/>

1. Seleccione **Agregar un comando**. Aparece una ventana emergente para agregar un comando.

    <img width="500px" alt="TDP messaging extension command" src="~/assets/images/tdp/tdp-me-add-command.png"/>

1. Seleccione **basado en búsqueda para** buscar el comando y escriba campos de comando.

    <img width="500px" alt="TDP messaging extension search command" src="~/assets/images/tdp/tdp-me-search-command.png"/>

1. Escriba campos de parámetro y **seleccione Guardar**.

    <img width="500px" alt="TDP messaging extension search parameter" src="~/assets/images/tdp/tdp-me-search-parameter.png"/>

---


### <a name="create-a-search-command-manually"></a>Crear un comando de búsqueda manualmente 

Para agregar manualmente el comando de búsqueda de extensión de mensajería al manifiesto de la aplicación, debes agregar los siguientes parámetros a la `composeExtension.commands` matriz de objetos:

| Nombre de la propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | Esta propiedad es un identificador único que se asigna al comando de búsqueda. La solicitud de usuario incluye este identificador. | Sí | 1.0 |
| `title` | Esta propiedad es un nombre de comando. Este valor aparece en la interfaz de usuario (UI). | Sí | 1.0 |
| `description` | Esta propiedad es un texto de ayuda que indica lo que hace este comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Esta propiedad debe ser `query` un . | No | 1.4 |
|`initialRun` | Si esta propiedad se establece en **true,** indica que este comando debe ejecutarse tan pronto como el usuario seleccione este comando en la interfaz de usuario. | No | 1.0 |
| `context` | Esta propiedad es una matriz opcional de valores que define el contexto en el que está disponible la acción de búsqueda. Los valores posibles son`message`, `compose` o `commandBox`. El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |

Debe agregar los detalles del parámetro de búsqueda, que define el texto visible para el usuario en el Teams cliente.

| Nombre de la propiedad | Objetivo | ¿Es necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `parameters` | Esta propiedad define una lista estática de parámetros para el comando. | No | 1.0 |
| `parameter.name` | Esta propiedad describe el nombre del parámetro. Esto se envía al servicio en la solicitud de usuario. | Sí | 1.0 |
| `parameter.description` | Esta propiedad describe los propósitos del parámetro o el ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Esta propiedad es un título o etiqueta de parámetros fáciles de usar. | Sí | 1.0 |
| `parameter.inputType` | Esta propiedad se establece en el tipo de entrada necesaria. Los valores posibles `text` incluyen , , , , , `textarea` `number` `date` `time` `toggle` . El valor predeterminado se establece en `text` . | No | 1.4 |

#### <a name="example"></a>Ejemplo

En la siguiente sección se muestra un ejemplo del manifiesto de aplicación simple del `composeExtensions` objeto que define un comando de búsqueda: 

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
Para ver el manifiesto completo de la aplicación, consulta [Esquema de manifiesto de la aplicación](~/resources/schema/manifest-schema.md).

## <a name="code-sample"></a>Ejemplo de código

| Nombre de ejemplo           | Descripción | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Teams extensión de mensajería| Describe cómo definir comandos de acción, crear módulo de tareas y responder a la acción de envío del módulo de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams de extensión de mensajería   |  Describe cómo definir comandos de búsqueda y responder a las búsquedas.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Responder a los comandos de búsqueda](~/messaging-extensions/how-to/search-commands/respond-to-search.md).

