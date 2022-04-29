---
title: Crear un menú de comandos para el bot
author: surbhigupta
description: Obtenga información sobre cómo crear un menú de comandos para el bot de Microsoft Teams con ejemplos de código.
ms.topic: how-to
ms.localizationpriority: high
ms.author: anclear
keywords: comando menú redactar mensaje conversación@mención
ms.openlocfilehash: 37d4c5f451efe9fe2caf137a89d12cdbbdb178d1
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111846"
---
# <a name="bot-command-menus"></a>Menús de comandos de bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Para definir un conjunto de comandos principales a los que el bot pueda responder, puede agregar un menú de comandos con una lista desplegable para el bot. La lista de comandos se presenta a los usuarios en el área del redacción del mensaje cuando están en una conversación con el bot. Seleccione un comando de la lista para insertar la cadena de comando en el cuadro de mensaje de redacción y seleccione **Enviar**.

# <a name="desktop"></a>[Escritorio](#tab/desktop)

![Menú de comandos de bot](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

![Menú de comandos de bot móvil](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a>Crear un menú de comandos para el bot

Los menús de comandos se definen en el manifiesto de la aplicación. Puede usar **App Studio** para crearlos o agregarlos manualmente al manifiesto de la aplicación.

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>Crear un menú de comandos para el bot mediante App Studio

Un requisito previo para crear un menú de comandos para el bot es que debe editar un manifiesto de aplicación existente. Los pasos para agregar un menú de comandos son los mismos, sin importar si crea un nuevo manifiesto o si edita uno existente.

**Para crear un menú de comandos para el bot mediante App Studio**

1. Abra Teams y seleccione **Aplicaciones** en el panel izquierdo. En la página **Aplicaciones**, busque **App Studio** y seleccione **Abrir**.
   > [!NOTE]
   > Si no tiene **App Studio**, puede descargarlo. Para obtener más información, consulte [Instalación de App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).

    :::image type="content" source="/media/AppStudio.png" alt-text="Instalación de App Studio"lightbox="media/AppStudio.png"border="true":::

2. En **App Studio**, seleccione la pestaña **Editor de manifiestos**. Si no tiene un paquete de aplicación, puede crear o importar una aplicación existente. Para obtener más información, consulte [Actualización de un paquete de aplicación](~/get-started/deploy-csharp-app-studio.md).

3. En el panel izquierdo del **Editor de manifiestos**, en la sección **Funcionalidades**, seleccione **Bots**.

4. En el panel derecho del **Editor de manifiestos**, en la sección **Comandos**, seleccione **Agregar**. Aparece la pantalla **Nuevo comando**.

    :::image type="content" source="/media/AppStudio-CommandMenu-Add.png" alt-text="Seleccione el paquete de la aplicación"lightbox="/media/AppStudio-CommandMenu-Add.png"border="true":::

5. Escriba el **texto del comando** que debe aparecer como el menú de comandos del bot.

6. Escriba el **texto de ayuda** que debe aparecer bajo el texto del comando en el menú. **El texto de ayuda** debe ser una explicación breve del propósito del comando.

7. Active las casillas **Ámbito** para seleccionar dónde debe aparecer este menú de comandos y seleccione **Guardar**.

:::image type="content" source="/media/AppStudio-NewCommandMenu.png" alt-text="Botón de menú de nuevos comandos de App Studio"lightbox="/media/AppStudio-NewCommandMenu.png"border="true":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Edite Manifest.json para crear un menú de comandos para el bot

Otra manera de crear un menú de comandos es crearlo directamente en el archivo de manifiesto mientras desarrolla el código fuente del bot. Para usar este método, siga estos puntos:

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

Puede analizar la parte **@Mención** del texto del mensaje mediante un método estático proporcionado con Bot Framework. Es un método de la clase `TurnContext` denominada `remove_recipient_mention`.

El código de Python para analizar la parte **\@Mención** del texto del mensaje es el siguiente:

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

Para habilitar el funcionamiento sin problemas del código del bot, hay algunos procedimientos recomendados que debe seguir.

## <a name="command-menu-best-practices"></a>Procedimientos recomendados para eel menú de comandos

A continuación, se describen los procedimientos recomendados para el menú de comandos:

* Mantenga la simplicidad: el menú del bot está diseñado para presentar las funcionalidades clave del bot.
* Sea breve: las opciones de menú no deben ser largas y no deben ser instrucciones de lenguaje natural complejas. Deben ser comandos simples.
* Mantenga la invocabilidad: las acciones o comandos del menú del bot siempre deben estar disponibles, independientemente del estado de la conversación o del cuadro de diálogo en el que se encuentra el bot.

> [!NOTE]
> Si quita los comandos del manifiesto, debe volver a implementar la aplicación para actualizar los cambios. En general, cualquier cambio en el manifiesto requiere que vuelva a implementar la aplicación.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Conversaciones de canal y grupo](~/bots/how-to/conversations/channel-and-group-conversations.md)
