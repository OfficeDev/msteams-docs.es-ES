---
title: Creación de un menú de comandos para el bot
author: surbhigupta
description: Obtenga información sobre cómo crear un menú de comandos para el bot de Microsoft Teams con ejemplos de código.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
keywords: menú de comandos redactar la conversación del mensaje @mention
ms.openlocfilehash: 6f4b9cdac76fc9beb42a39dde3b320036ea580b5
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102559"
---
# <a name="bot-command-menus"></a>Menús de comandos del bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Para definir un conjunto de comandos principales a los que el bot puede responder, puede agregar un menú de comandos con una lista desplegable de comandos para el bot. La lista de comandos se presenta a los usuarios en el área del mensaje de redacción cuando están en conversación con el bot. Seleccione un comando de la lista para insertar la cadena de comando en el cuadro de mensaje de redacción y seleccione **Enviar**.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

![Menú de comandos del bot](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

![Menú de comandos de bot móvil](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a>Creación de un menú de comandos para el bot

Los menús de comandos se definen en el manifiesto de la aplicación. Puede usar **App Studio** para crearlos o agregarlos manualmente en el manifiesto de la aplicación.

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>Creación de un menú de comandos para el bot mediante App Studio

Un requisito previo para crear un menú de comandos para el bot es que debe editar un manifiesto de aplicación existente. Los pasos para agregar un menú de comandos son los mismos, tanto si crea un nuevo manifiesto como si edita uno existente.

**Para crear un menú de comandos para el bot mediante App Studio**

1. Abra Teams y seleccione **Aplicaciones** en el panel izquierdo. En la página **Aplicaciones** , busque **App Studio** y seleccione **Abrir**.
   > [!NOTE]
   > Si no tiene **App Studio**, puede descargarlo. Para obtener más información, consulte [Instalación de App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).

    :::image type="content" source="/media/AppStudio.png" alt-text="Instalación de App Studio"lightbox="media/AppStudio.png"border="true":::

2. En **App Studio**, seleccione la pestaña **Editor de manifiestos** . Si no tiene un paquete de aplicación existente, puede crear o importar una aplicación existente. Para obtener más información, consulte [Actualización de un paquete de aplicación](~/get-started/deploy-csharp-app-studio.md).

3. En el panel izquierdo del **editor de manifiestos** y en la sección **Funcionalidades** , seleccione **Bots**.

4. En el panel derecho del **editor de manifiestos** y en la sección **Comandos** , seleccione **Agregar**. Aparece **la pantalla Nuevo comando** .

    :::image type="content" source="/media/AppStudio-CommandMenu-Add.png" alt-text="Seleccionar el paquete de la aplicación"lightbox="/media/AppStudio-CommandMenu-Add.png"border="true":::

5. Escriba el **texto comando** que debe aparecer como el menú de comandos del bot.

6. Escriba el **texto de ayuda** que debe aparecer bajo el texto del comando en el menú. **El texto de ayuda** debe ser una breve explicación del propósito del comando.

7. Active las casillas **Ámbito** para seleccionar dónde debe aparecer este menú de comandos y seleccione **Guardar**.

:::image type="content" source="/media/AppStudio-NewCommandMenu.png" alt-text="Botón de menú nuevos comandos de App Studio"lightbox="/media/AppStudio-NewCommandMenu.png"border="true":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Cree un menú de comandos para el bot editando Manifest.json.

Otra manera de crear un menú de comandos es crearlo directamente en el archivo de manifiesto al desarrollar el código fuente del bot. Para usar este método, siga estos puntos:

* Cada menú admite hasta diez comandos.
* Cree un único menú de comandos que funcione en todos los ámbitos.
* Cree un menú de comandos diferente para cada ámbito.

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>Ejemplo de manifiesto para un solo menú para ambos ámbitos

El código de ejemplo de manifiesto del menú único para ambos ámbitos es el siguiente:

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

El código de ejemplo de manifiesto para el menú de cada ámbito es el siguiente:

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

Debe controlar los comandos de menú en el código del bot a medida que controla cualquier mensaje de los usuarios. Para controlar los comandos de menú en el código del bot, analice la **\@parte Mención** del texto del mensaje.

## <a name="handle-menu-commands-in-your-bot-code"></a>Control de comandos de menú en el código del bot

Los bots de un grupo o canal solo responden cuando se mencionan `@botname` en un mensaje. Cada mensaje recibido por un bot cuando se encuentra en un ámbito de grupo o canal contiene su nombre en el texto del mensaje. Antes de controlar el comando que se devuelve, el análisis de mensajes debe controlar el mensaje recibido por un bot con su nombre.

> [!NOTE]
> Para controlar los comandos en el código, se envían al bot como un mensaje normal. Debe controlarlos como controlaría cualquier otro mensaje de los usuarios. Los comandos del código insertan texto preconfigurado en el cuadro de texto. A continuación, el usuario debe enviar ese texto como lo hace para cualquier otro mensaje.

# <a name="c"></a>[C#](#tab/dotnet)

Puede analizar la **\@parte Mention** del texto del mensaje mediante un método estático proporcionado con el Microsoft Bot Framework. Es un método de la `Activity` clase denominada `RemoveRecipientMention`.

El código de C# para analizar la **\@parte Mención** del texto del mensaje es el siguiente:

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Puede analizar la **\@parte Mención** del texto del mensaje mediante un método estático proporcionado con Bot Framework. Es un método de la `TurnContext` clase denominada `removeMentionText`.

El código JavaScript para analizar la **\@parte Mención** del texto del mensaje es el siguiente:

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

Puede analizar la **parte @Mention** del texto del mensaje mediante un método estático proporcionado con Bot Framework. Es un método de la `TurnContext` clase denominada `remove_recipient_mention`.

El código de Python para analizar la **\@parte Mención** del texto del mensaje es el siguiente:

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

Para habilitar el funcionamiento sin problemas del código del bot, hay algunos procedimientos recomendados que debe seguir.

## <a name="command-menu-best-practices"></a>Procedimientos recomendados del menú de comandos

A continuación se muestran los procedimientos recomendados del menú de comandos:

* Mantenlo sencillo: el menú del bot está diseñado para presentar las funcionalidades clave del bot.
* Manténgalo corto: las opciones de menú no deben ser largas y no deben ser instrucciones de lenguaje natural complejas. Deben ser comandos simples.
* Mantenerlo invocable: las acciones o comandos del menú bot siempre deben estar disponibles, independientemente del estado de la conversación o del cuadro de diálogo en el que se encuentra el bot.

> [!NOTE]
> Si quitas los comandos del manifiesto, debes volver a implementar la aplicación para implementar los cambios. En general, cualquier cambio en el manifiesto requiere que vuelva a implementar la aplicación.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Conversaciones de canal y grupo](~/bots/how-to/conversations/channel-and-group-conversations.md)
