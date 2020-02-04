---
title: Crear un menú de comandos para el bot
author: clearab
description: Cómo crear un menú de comandos para su bot de Microsoft Teams
ms.topic: overview, command menu
ms.author: anclear
ms.openlocfilehash: 81efb94fc882aa4653ab162863d5d973aeae87b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675850"
---
# <a name="bot-command-menus"></a>Menús de comandos de bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> Los menús de bot no aparecerán en los clientes móviles.

Add Command menu for your bot permite definir un conjunto de comandos básicos a los que siempre puede responder el bot. La lista de comandos se presenta al usuario encima del área de mensaje de redacción cuando se trata con el bot. Al seleccionar un comando de la lista, se insertará la cadena de comandos en el cuadro de mensaje de redacción y, a continuación, todos los usuarios tendrán que hacer clic en **Enviar**.

![Menú de comandos de bot](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a>Crear un menú de comandos para el bot

Los menús de comandos se definen en el manifiesto de la aplicación. Puede usar App Studio para ayudarle a crearlos, o bien agregarlos de forma manual.

### <a name="creating-a-command-menu-for-your-bot-using-app-studio"></a>Crear un menú de comandos para el bot con App Studio

En estas instrucciones se da por sentado que va a editar un manifiesto de aplicación existente. Los pasos para agregar un menú de comandos son los mismos, tanto si está creando un manifiesto nuevo o editando uno existente.

1. Abra App Studio desde el... menú de desbordamiento en el raíl de navegación izquierdo. Si no tiene App Studio disponible, puede descargarlo. Vea [Installing App Studio](https://aka.ms/teams-app-studio#installing-app-studio) para obtener más información sobre el uso de App Studio.

    ![App Studio](./conversations/media/AppStudio.png)

2. Una vez en App Studio, seleccione la pestaña **Editor de manifiestos** .

3. En la columna izquierda de la vista editor de manifiestos, en la sección **capacidades** , seleccione **bots**.

4. En la columna derecha de la vista editor de manifiestos, en la sección **comandos** , seleccione el botón **Agregar** .

    ![Botón Agregar del menú de comandos de App Studio](./conversations/media/AppStudio-CommandMenu-Add.png)

5. Aparece la pantalla **nuevo comando** . Escriba el **texto del comando** que desea que aparezca como comando de menú y el texto de **ayuda** que desea que aparezca directamente debajo del texto del comando en el menú. Esta debe ser una breve explicación del propósito del comando.

6. A continuación, seleccione el ámbito o ámbitos donde desea que aparezca este menú de comandos y, a continuación, seleccione el botón **Guardar** .

    ![Botón Agregar del menú de comandos de App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="creating-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Crear un menú de comandos para el bot editando **manifest. JSON**

Otro enfoque válido para crear un menú de comandos es crearlo directamente en el archivo de manifiesto mientras se desarrolla el código fuente de bot. Estas son algunas de las cosas que debe tener en cuenta al usar este enfoque:

1. Cada menú admite hasta 10 comandos.

2. Se puede crear un solo menú de comandos que funcione en todos los ámbitos.

3. Puede crear un menú de comandos diferente para cada ámbito

#### <a name="manifest-example---single-menu-for-both-scopes"></a>Ejemplo de manifiesto: menú único para ambos ámbitos

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

#### <a name="manifest-example---menu-for-each-scope"></a>Ejemplo de manifiesto: menú para cada ámbito

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

## <a name="handling-menu-commands-in-your-bot-code"></a>Control de comandos de menú en el código de bot

Los bots de un grupo o canal solo responden cuando se mencionan ("@botname") en un mensaje. Como resultado, cada mensaje recibido por un bot cuando se encuentre en un ámbito de grupo o de canal contendrá su propio nombre en el texto del mensaje devuelto. Debe asegurarse de que los controladores de análisis de mensajes antes de controlar el comando que se devuelve.

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

Puede analizar la `Activity` `RemoveRecipientMention` ** \@parte de menciones** del texto del mensaje usando un método estático proporcionado con Microsoft bot Framework, un método de la clase denominada.

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node. js](#tab/javascript)

Puede analizar la `TurnContext` `removeMentionText` ** \@parte de menciones** del texto del mensaje usando un método estático proporcionado con Microsoft bot Framework, un método de la clase denominada.

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="pythontabpython"></a>[Python](#tab/python)


Puede analizar la parte **@Mention** del texto del mensaje usando un método estático proporcionado con Microsoft bot Framework, un método de la `TurnContext` clase denominada. `remove_recipient_mention`

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

## <a name="command-menu-best-practices"></a>Procedimientos recomendados de menús de comandos

* **Manténgase sencillo**: el menú bot tiene como objetivo presentar las capacidades clave de su bot.
* **Tenga en Resumen**: las opciones de menú no deben ser muy largas y complejas con instrucciones de lenguaje natural, sino que deben ser comandos simples.
* **Guardar invokable**: los comandos o acciones del menú bot siempre deben estar disponibles, independientemente del estado de la conversación o el cuadro de diálogo en el que se encuentra el bot.
