---
title: Definición de comandos de búsqueda de extensión de mensaje
author: surbhigupta
description: En este módulo, obtenga información sobre los comandos de búsqueda de extensión de mensaje para aplicaciones Teams, para crear un comando de búsqueda a través del manifiesto de la aplicación y manualmente.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: e71e83f8fbd6b0d44257a2d38fd13486b087bc5e
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142811"
---
# <a name="define-message-extension-search-commands"></a>Definición de comandos de búsqueda de extensión de mensaje

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Los comandos de búsqueda de extensión de mensaje permiten a los usuarios buscar sistemas externos e insertar los resultados de esa búsqueda en un mensaje en forma de tarjeta. Este documento le guía sobre cómo seleccionar ubicaciones de invocación de comandos de búsqueda y agregar el comando de búsqueda al manifiesto de la aplicación.

> [!NOTE]
> El límite de tamaño de la tarjeta de resultados es de 28 KB. La tarjeta no se envía si su tamaño supera los 28 KB.

## <a name="select-search-command-invoke-locations"></a>Selección de ubicaciones de invocación de comandos de búsqueda

El comando de búsqueda se invoca desde cualquiera de las siguientes ubicaciones o desde ambas:

* Área redactar mensaje: los botones de la parte inferior del área de redacción del mensaje.
* Cuadro de comandos: por @mentioning en el cuadro de comandos.

  Cuando se invoca el comando de búsqueda desde el área del mensaje de redacción, el usuario envía los resultados a la conversación. Cuando se invoca desde el cuadro de comandos, el usuario interactúa con la tarjeta resultante o la copia para usarla en otro lugar.

En la imagen siguiente se muestran las ubicaciones de invocación del comando de búsqueda:

:::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-locations.png" alt-text="Ubicaciones de invocación de comandos de búsqueda":::

## <a name="add-the-search-command-to-your-app-manifest"></a>Agregar el comando de búsqueda al manifiesto de la aplicación

Para agregar el comando de búsqueda al manifiesto de la aplicación, debe agregar un nuevo `composeExtension` objeto al nivel superior del JSON del manifiesto de la aplicación. Puede agregar el comando de búsqueda con la ayuda de App Studio o manualmente.

### <a name="create-a-search-command-using-app-studio"></a>Creación de un comando de búsqueda mediante App Studio

El requisito previo para crear un comando de búsqueda es que ya debe haber creado una extensión de mensaje. Para obtener información sobre cómo crear una extensión de mensaje, vea [crear una extensión de mensaje](~/messaging-extensions/how-to/create-messaging-extension.md).

Para crear un comando de búsqueda:

1. Abra **App Studio** en el cliente Microsoft Teams y seleccione la pestaña **Editor de manifiestos**.
1. Si ya ha creado el paquete de la aplicación en **App Studio**, seleccione en la lista. Si no ha creado un paquete de aplicación, importe uno existente.
1. Después de importar el paquete de la aplicación, seleccione **Extensiones de mensaje** en **Funcionalidades**. Se mostrará una ventana emergente para configurar la extensión de mensaje.
1. Seleccione **Configurar** en la ventana para incluir la extensión de mensaje en la experiencia de la aplicación. En la imagen siguiente se muestra la página de configuración de la extensión de mensaje:

    :::image type="content" source="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt-text="Configuración de la extensión de mensajería":::

1. Para crear la extensión de mensaje, necesita un bot registrado por Microsoft. Puede usar un bot existente o crear uno nuevo. Seleccione la opción **Crear nuevo bot**, asigne un nombre al nuevo bot y seleccione **Crear**. En la imagen siguiente se muestra la creación de bots para la extensión de mensaje:

    :::image type="content" source="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt-text="Creación de un bot para la extensión de mensajería":::

1. Para usar un bot existente, seleccione **Usar bot existente** y seleccione **Seleccionar de uno de mis bots existentes** para elegir los bots existentes de la lista desplegable, proporcione un **Nombre de bot** y seleccione **Guardar**, o seleccione **Conectar a un identificador de bot diferente** si ya tiene un identificador de bot creado, asigne un **Nombre de bot** y seleccione **Guardar**.

    :::image type="content" source="~/assets/images/messaging-extension/use-existing-bot.png" alt-text="Uso del bot existente para la extensión de mensajería":::

1. Seleccione **Agregar** en la **sección Comando** de la página extensiones de mensaje para incluir los comandos, que deciden el comportamiento de la extensión de mensaje.
En la imagen siguiente se muestra la adición de comandos para la extensión de mensaje:

    :::image type="content" source="~/assets/images/messaging-extension/include-command.png" alt-text="Incluir comandos":::

1. Seleccione **Permitir que los usuarios consulten el servicio para obtener información e insertarla en un mensaje**. En la imagen siguiente se muestra la selección del parámetro de comando de búsqueda:

    :::image type="content" source="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt-text="Selección de parámetros de comando de búsqueda":::

1. Agregue un **Id. de comando** y un **Título**.
1. Seleccione la ubicación desde la que se debe invocar el comando de búsqueda. En la imagen siguiente se muestra la ubicación de invocación del comando de búsqueda:

    :::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt-text="Selección de ubicación de invocación de comandos de búsqueda":::

1. Agregue el parámetro de búsqueda y seleccione **Guardar**.

### <a name="create-a-search-command-manually"></a>Creación manual de un comando de búsqueda

Para agregar manualmente el comando de búsqueda de extensión de mensaje al manifiesto de la aplicación, debe agregar los parámetros siguientes a `composeExtension.commands` la matriz de objetos:

| Nombre de propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | Esta propiedad es un identificador único que se asigna al comando de búsqueda. La solicitud de usuario incluye este id. | Sí | 1.0 |
| `title` | Esta propiedad es un nombre de comando. Este valor aparece en la interfaz de usuario (UI). | Sí | 1.0 |
| `description` | Esta propiedad es un texto de ayuda que indica lo que hace este comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Esta propiedad debe ser .`query` | No | 1.4 |
|`initialRun` | Si esta propiedad se establece en **true**, indica que este comando debe ejecutarse en cuanto el usuario seleccione este comando en la interfaz de usuario. | No | 1.0 |
| `context` | Esta propiedad es una matriz opcional de valores que define el contexto en el que está disponible la acción de búsqueda. Los valores posibles son`message`, `compose` o `commandBox`. El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |

Debe agregar los detalles del parámetro de búsqueda, que define el texto visible para el usuario en el cliente de Teams.

| Nombre de propiedad | Objetivo | ¿Es obligatoria? | Versión mínima del manifiesto |
|---|---|---|---|
| `parameters` | Esta propiedad define una lista estática de parámetros para el comando. | No | 1.0 |
| `parameter.name` | Esta propiedad describe el nombre del parámetro. Esto se envía al servicio en la solicitud del usuario. | Sí | 1.0 |
| `parameter.description` | Esta propiedad describe los propósitos del parámetro o el ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Esta propiedad es un título o etiqueta de parámetro descriptivo corto. | Sí | 1.0 |
| `parameter.inputType` | Esta propiedad se establece en el tipo de entrada necesaria. Entre los valores posibles se incluyen , , , , , `toggle``time`. `date``number``textarea``text` El valor predeterminado está establecido en `text`. | No | 1.4 |

#### <a name="example"></a>Ejemplo

En la sección siguiente se muestra un ejemplo del manifiesto de aplicación simple del `composeExtensions` objeto que define un comando de búsqueda:

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

Para ver el manifiesto de aplicación completo, consulte [Esquema de manifiesto de aplicación](~/resources/schema/manifest-schema.md).

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre           | Descripción | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Búsqueda de extensión de mensaje de Teams   |  Describe cómo definir comandos de búsqueda y responder a búsquedas.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../../../sbs-messagingextension-searchcommand.yml) para crear una extensión de mensaje basada en búsquedas.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Responda a los comandos de búsqueda](~/messaging-extensions/how-to/search-commands/respond-to-search.md).
