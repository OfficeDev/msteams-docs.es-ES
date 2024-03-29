---
title: Definición de comandos de búsqueda de extensión de mensaje
author: surbhigupta
description: Obtenga información sobre los comandos de búsqueda de extensión de mensaje para aplicaciones de Teams, para crear un comando de búsqueda a través del manifiesto de la aplicación y manualmente.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 9ec7ea734e331fcfb563702d18284f4831c369f6
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820181"
---
# <a name="define-message-extension-search-commands"></a>Definición de comandos de búsqueda de extensión de mensaje

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Los comandos de búsqueda de extensión de mensaje permiten a los usuarios buscar sistemas externos e insertar los resultados de esa búsqueda en un mensaje en forma de tarjeta. Este documento le guía sobre cómo seleccionar ubicaciones de invocación de comandos de búsqueda y agregar el comando de búsqueda al manifiesto de la aplicación.

> [!NOTE]
> El límite de tamaño de la tarjeta de resultados es de 28 KB. La tarjeta no se envía si su tamaño supera los 28 KB.

Vea el siguiente vídeo para obtener información sobre cómo definir comandos de búsqueda de extensión de mensaje:
<br>

> [!VIDEO <https://www.microsoft.com/en-us/videoplayer/embed/RE4OIvK>]
<br>

## <a name="select-search-command-invoke-locations"></a>Selección de ubicaciones de invocación de comandos de búsqueda

El comando de búsqueda se invoca desde cualquiera de las siguientes ubicaciones o desde ambas:

* Área redactar mensaje: los botones de la parte inferior del área de redacción del mensaje.
* Cuadro de comandos: por @mentioning en el cuadro de comandos.

Cuando se invoca un comando de búsqueda desde el área del mensaje de redacción, el usuario envía los resultados a la conversación. Cuando se invoca desde el cuadro de comandos, el usuario interactúa con la tarjeta resultante o la copia para usarla en otro lugar.

En la imagen siguiente se muestran las ubicaciones de invocación del comando de búsqueda:

:::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-locations.png" alt-text="Captura de pantalla que muestra las ubicaciones de invocación de un comando de búsqueda en un canal de Teams.":::

## <a name="add-the-search-command-to-your-app-manifest"></a>Agregar el comando de búsqueda al manifiesto de la aplicación

Para agregar el comando de búsqueda al manifiesto de la aplicación, debe agregar un nuevo `composeExtension` objeto al nivel superior del JSON del manifiesto de la aplicación. Puede agregar el comando de búsqueda con la ayuda del Portal para desarrolladores o manualmente.

### <a name="create-a-search-command-using-developer-portal"></a>Creación de un comando de búsqueda mediante el Portal para desarrolladores

El requisito previo para crear un comando de búsqueda es que ya debe haber creado una extensión de mensaje. Para obtener información sobre cómo crear una extensión de mensaje, vea [crear una extensión de mensaje](~/messaging-extensions/how-to/create-messaging-extension.md).

**Para crear un comando de acción**

1. Abra **el Portal para desarrolladores** en el cliente de Microsoft Teams y seleccione la pestaña **Aplicaciones** . Si ya ha creado el paquete de la aplicación en **el Portal para desarrolladores**, seleccione en la lista. Si no ha creado un paquete de aplicación, importe uno existente.
1. Después de importar un paquete de aplicación, seleccione **Extensiones de mensaje** en **Características de la aplicación**.
1. Para crear una extensión de mensaje, necesita un bot registrado de Microsoft. Puede usar un bot existente o crear uno nuevo. Seleccione **la opción Crear nuevo bot** , asigne un nombre al nuevo bot y, a continuación, seleccione **Crear**.

   :::image type="content" source="../../../assets/images/tdp/bot-page.png" alt-text="Captura de pantalla que muestra las opciones para configurar un bot para una aplicación en el Portal para desarrolladores de Teams.":::

1. Para usar un bot existente, seleccione **Seleccionar un bot existente** y elija los bots existentes en la lista desplegable o escriba **un identificador de bot** si ya tiene un identificador de bot creado.

1. Seleccione el ámbito de la extensión de mensajería y seleccione **Guardar**.

1. Seleccione **Agregar un comando** en la sección **Comando** para incluir los comandos, que deciden el comportamiento de la extensión de mensaje.
En la imagen siguiente se muestra la adición de comandos para la extensión de mensaje:

   :::image type="content" source="../../../assets/images/tdp/add-a-command.PNG" alt-text="Captura de pantalla que muestra cómo agregar un comando en el Portal para desarrolladores de Teams para definir el comportamiento de la extensión de mensaje.":::

1. Seleccione **Buscar** y escriba **Id. de comando**, **Título de comando** y **Descripción del comando**.

1. Escriba todos los parámetros y seleccione el tipo de entrada en la lista desplegable.

   :::image type="content" source="../../../assets/images/tdp/add-a-command-parameter.PNG" alt-text="Captura de pantalla que muestra cómo agregar un parámetro para definir el comando en el Portal para desarrolladores de Teams para una extensión de mensaje.":::

1. Seleccione **Agregar un dominio** en **Vínculos de vista previa**.

1. Escriba dominio válido y, a continuación, seleccione **Agregar**.

   :::image type="content" source="../../../assets/images/tdp/add-domain.PNG" alt-text="Captura de pantalla que muestra cómo agregar un dominio válido a la extensión de mensajería para la desplegamiento de vínculos.":::

1. Seleccione **Guardar**.

   :::image type="content" source="../../../assets/images/tdp/add-a-command-save.PNG" alt-text="Captura de pantalla que muestra cómo guardar toda la configuración y los parámetros de la extensión de mensaje.":::

**Para agregar parámetros adicionales**

1. Seleccione elipse en la sección de comandos y, a continuación, seleccione **Editar parámetro**.

   :::image type="content" source="../../../assets/images/tdp/edit-parameters.PNG" alt-text="Capturas de pantalla que muestran cómo editar parámetros para la extensión de mensaje.":::

1. Seleccione **Agregar parámetros** y escriba todos los parámetros.

   :::image type="content" source="../../../assets/images/tdp/add-parameter.PNG" alt-text="Captura de pantalla que muestra cómo agregar parámetros adicionales para la extensión de mensaje."lightbox="../../../assets/images/tdp/add-a-parameters.PNG":::

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

Debe agregar los detalles del parámetro de búsqueda que define el texto visible para el usuario en el cliente de Teams.

| Nombre de propiedad | Objetivo | ¿Es obligatoria? | Versión mínima del manifiesto |
|---|---|---|---|
| `parameters` | Esta propiedad define una lista estática de parámetros para el comando. | No | 1.0 |
| `parameter.name` | Esta propiedad describe el nombre del parámetro. `parameter.name` se envía al servicio en la solicitud del usuario. | Sí | 1.0 |
| `parameter.description` | Esta propiedad describe los propósitos del parámetro o el ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Esta propiedad es un título o etiqueta de parámetro descriptivo corto. | Sí | 1.0 |
| `parameter.inputType` | Esta propiedad se establece en el tipo de entrada necesaria. Entre los valores posibles se incluyen , , , , , `toggle``time`. `date``number``textarea``text` El valor predeterminado está establecido en `text`. | No | 1.4 |
| `parameters.value` | Valor inicial del parámetro. Actualmente no se admite el valor | No | 1,5 |

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

## <a name="see-also"></a>Vea también

* [Tarjetas](../../../task-modules-and-cards/what-are-cards.md)
* [Módulos de tareas](../../../task-modules-and-cards/what-are-task-modules.md)
* [Esquema del manifiesto de la aplicación de Teams](../../../resources/schema/manifest-schema.md)
* [Portal para desarrolladores de Teams](../../../concepts/build-and-test/teams-developer-portal.md)
* [Extensiones de mensajes](../../what-are-messaging-extensions.md)
