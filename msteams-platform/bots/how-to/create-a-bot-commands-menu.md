---
title: Crear un menú de comandos para el bot
author: surbhigupta
description: Obtenga información sobre cómo crear y controlar un menú de comandos para el bot de Microsoft Teams y procedimientos recomendados. Sepa cómo quitar comandos del manifiesto.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 0e0f9ce9ada0cde0aa6f7b6b29c7badb07dd7db9
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100906"
---
# <a name="create-a-commands-menu"></a>Crear un menú de comandos

> [!NOTE]
> Se recomienda crear un bot de comandos siguiendo la guía paso a paso [de Compilación del bot de comandos con JavaScript](../../sbs-gs-commandbot.yml) mediante la herramienta de desarrollo de nueva generación para Teams. Para obtener más información sobre el kit de herramientas de Teams, consulte [Introducción al kit de herramientas de Teams para Visual Studio Code](../../toolkit/teams-toolkit-fundamentals.md) y [Información general del kit de herramientas de Teams para Visual Studio](../../toolkit/teams-toolkit-overview-visual-studio.md).

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Para definir un conjunto de comandos principales a los que el bot pueda responder, puede agregar un menú de comandos con una lista desplegable para el bot. La lista de comandos se presenta a los usuarios en el área del redacción del mensaje cuando están en una conversación con el bot. Seleccione un comando de la lista para insertar la cadena de comando en el cuadro de mensaje de redacción y seleccione **Enviar**.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="conversations/Media/bot-menu-sample.png" alt-text="Bot-command-menu":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="conversations/Media/mobile-bot-menu-sample.png" alt-text="Mobile-bot-command-menu":::

* * *

## <a name="create-a-command-menu-for-your-bot"></a>Crear un menú de comandos para el bot

Los menús de comandos se definen en el manifiesto de la aplicación. Puede usar **el Portal para desarrolladores** para crearlos o agregarlos manualmente en el manifiesto de la aplicación.

### <a name="create-a-command-menu-for-your-bot-using-developer-portal"></a>Creación de un menú de comandos para el bot mediante el Portal para desarrolladores

Un requisito previo para crear un menú de comandos para el bot es que debe editar un manifiesto de aplicación existente. Los pasos para agregar un menú de comandos son los mismos, sin importar si crea un nuevo manifiesto o si edita uno existente.

Para crear un menú de comandos para el bot mediante el Portal para desarrolladores:

1. Abra Teams y seleccione **Aplicaciones** en el panel izquierdo. En la página **Aplicaciones** , busque **Portal para desarrolladores** y, a continuación, seleccione **Abrir**.

   :::image type="content" source="../../assets/images/tdp/add-dev-portal.png" alt-text="Captura de pantalla que muestra cómo agregar portal para desarrolladores en el cliente de Teams.":::
  
1. En **Portal para desarrolladores**, seleccione la pestaña **Aplicaciones** . Si no tiene un paquete de aplicación existente, puede crear o importar una aplicación existente. Para obtener más información, consulte [Portal para desarrolladores para Teams](../../concepts/build-and-test/teams-developer-portal.md).

1. Seleccione **la pestaña Aplicaciones** , seleccione Características de la **aplicación** en el panel izquierdo y, a continuación, **bots**.

1. Seleccione **Agregar un comando** en la sección **Comandos** .

   :::image type="content" source="../../assets/images/tdp/add-a-bot-command.png" alt-text="Captura de pantalla que muestra cómo agregar un comando para el bot en el Portal para desarrolladores.":::

1. Escriba el **comando** que aparece como el menú de comandos del bot.

1. Escriba la **descripción** que aparece bajo el texto del comando en el menú. **Descripción** debe ser una breve explicación del propósito del comando.

1. Active la casilla **Ámbito** y, a continuación, seleccione **Agregar**.
   Esto define dónde debe aparecer el menú de comandos.

   :::image type="content" source="../../assets/images/tdp/bot-command.png" alt-text="Captura de pantalla que muestra cómo agregar un comando, una descripción y ámbitos para el bot.":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Edite Manifest.json para crear un menú de comandos para el bot

Another way to create a command menu is to create it directly in the manifest file while developing your bot source code. To use this method, follow these points:

* Cada menú admite hasta diez comandos.
* Cree un único menú de comandos que funcione en todos los ámbitos.
* Cree un menú de comandos diferente para cada ámbito.

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>Ejemplo de manifiesto para un solo menú para ambos ámbitos

El código de ejemplo del manifiesto para un menú único para ambos ámbitos es el siguiente:

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "scopes": [
        "personal",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team",
            "personal"
          ],
          "commands":[
            {
              "title":"Help",
              "description":"Displays this help message"
            },
            {
              "title":"Search Flights",
              "description":"Search flights from Seattle to Phoenix May 2-5 departing after 3pm"
            },
            {
              "title":"Search Hotels",
              "description":"Search hotels in Portland tonight"
            },
            {
              "title":"Best Time to Fly",
              "description":"Best time to fly to London for a 5 day trip this summer"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

#### <a name="manifest-example-for-the-menu-for-each-scope"></a>Ejemplo de manifiesto para el menú de cada ámbito

El código de ejemplo del manifiesto para el menú para cada ámbito es el siguiente:

```json
{
  ...
  "bots":[
    {
      "botId":"<Microsoft app ID for your bot>",
      "scopes": [
        "groupChat",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for channels"
            }
          ]
        },
        {
          "scopes":[
            "groupChat"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for group chat"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

Debe controlar los comandos del menú en el código del bot del mismo modo que controla cualquier mensaje de los usuarios. Para controlar los comandos de menú en el código del bot, analice la parte **\@Mención** del texto del mensaje.

## <a name="handle-menu-commands-in-your-bot-code"></a>Control de comandos de menú en el código del bot

Los bots de un grupo o canal solo responden cuando se menciona `@botname` en un mensaje. Cada mensaje recibido por un bot cuando se encuentra en un ámbito de grupo o canal contiene su nombre en el texto del mensaje. Antes de controlar el comando que se devuelve, el análisis de mensajes debe controlar el mensaje recibido por un bot con su nombre.

> [!NOTE]
> Para controlar los comandos en el código, se envían al bot como un mensaje normal. Debe controlarlos como controlaría cualquier otro mensaje de los usuarios. Los comandos en el código insertan texto preconfigurado en el cuadro de texto. A continuación, el usuario debe enviar ese texto como lo hace con cualquier otro mensaje.

# <a name="c"></a>[C#](#tab/dotnet)

Puede analizar la parte **\@Mención** del texto del mensaje mediante un método estático proporcionado con el Microsoft Bot Framework. Es un método de la clase `Activity` denominada `RemoveRecipientMention`.

El código de C# para analizar la parte **\@Mención** del texto del mensaje es el siguiente:

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Puede analizar la parte **\@Mención** del texto del mensaje mediante un método estático proporcionado con Bot Framework. Es un método de la clase `TurnContext` denominada `removeMentionText`.

El código JavaScript para analizar la parte **\@Mención** del texto del mensaje es el siguiente:

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

You can parse out the **@Mention** portion of the message text using a static method provided with the Bot Framework. It is a method of the `TurnContext` class named `remove_recipient_mention`.

El código de Python para analizar la parte **\@Mención** del texto del mensaje es el siguiente:

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

Para habilitar el funcionamiento sin problemas del código del bot, hay algunos procedimientos recomendados que debe seguir.

## <a name="command-menu-best-practices"></a>Procedimientos recomendados para eel menú de comandos

A continuación, se describen los procedimientos recomendados para el menú de comandos:

* Mantenga la simplicidad: el menú del bot está diseñado para presentar las funcionalidades clave del bot.
* Keep it short: Menu options must not be long and must not be complex natural language statements. They must be simple commands.
* Mantenga la invocabilidad: las acciones o comandos del menú del bot siempre deben estar disponibles, independientemente del estado de la conversación o del cuadro de diálogo en el que se encuentra el bot.

> [!NOTE]
> Si quita los comandos del manifiesto, debe volver a implementar la aplicación para actualizar los cambios. En general, cualquier cambio en el manifiesto requiere que vuelva a implementar la aplicación.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Conversaciones de canal y grupo](~/bots/how-to/conversations/channel-and-group-conversations.md)
