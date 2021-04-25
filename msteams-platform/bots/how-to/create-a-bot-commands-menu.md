---
title: Crear un menú de comandos para el bot
author: clearab
description: Cómo crear un menú de comandos para el bot de Microsoft Teams
ms.topic: how-to
ms.author: anclear
ms.openlocfilehash: a4d53d8287d425120d24f559b8ffffabebdbcfb4
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2021
ms.locfileid: "51995900"
---
# <a name="bot-command-menus"></a>Menús de comandos bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> Los menús bot no aparecen en clientes móviles.

Para definir un conjunto de comandos principales a los que el bot puede responder, puede agregar un menú de comandos con una lista desplegable de comandos para el bot. La lista de comandos se presenta a los usuarios en el área del mensaje de redacción cuando están en conversación con el bot. Seleccione un comando de la lista para insertar la cadena de comandos en el cuadro de mensaje de redacción y seleccione **Enviar**.

![Menú de comandos Bot](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a>Crear un menú de comandos para el bot

Los menús de comandos se definen en el manifiesto de la aplicación. Puedes usar **App Studio** para crearlos o agregarlos manualmente en el manifiesto de la aplicación.

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>Crear un menú de comandos para el bot con App Studio

Un requisito previo para crear un menú de comandos para el bot es que debes editar un manifiesto de aplicación existente. Los pasos para agregar un menú de comandos son los mismos, ya sea que cree un nuevo manifiesto o edite uno existente.

**Para crear un menú de comandos para el bot con App Studio**

1. Abra Teams y seleccione **Aplicaciones** en el panel izquierdo. En la **página Aplicaciones,** busque **App Studio** y seleccione **Abrir**. 
   > [!NOTE]
   > Si no tienes **App Studio,** puedes descargarlo. Para obtener más información, consulta [instalación de App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).

    ![App Studio](./conversations/media/AppStudio.png)

2. En **App Studio,** seleccione la **pestaña Editor de manifiestos.** Si no tienes un paquete de aplicación existente, puedes crear o importar una aplicación existente. Para obtener más información, [consulta Actualizar un paquete de la aplicación](~/tutorials/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package).

3. En el panel izquierdo del **editor de manifiestos** y en la sección **Funcionalidades,** seleccione **Bots**.

4. En el panel derecho del **editor de manifiestos** y en la **sección Comandos,** seleccione **Agregar**. Aparecerá **la pantalla Nuevo** comando.

    ![Menú Comandos de App Studio Botón Agregar](./conversations/media/AppStudio-CommandMenu-Add.png)

5. Escriba el **texto comando** que debe aparecer como el menú de comandos del bot.

6. Escriba el **texto de ayuda** que debe aparecer debajo del texto del comando en el menú. **El texto de** la ayuda debe ser una breve explicación del propósito del comando.

7. Active las **casillas** Ámbito para seleccionar dónde debe aparecer este menú de comandos y **seleccione Guardar**.

    ![Botón de menú Nuevos comandos de App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Crear un menú de comandos para el bot editando Manifest.js

Otra forma de crear un menú de comandos es crearlo directamente en el archivo de manifiesto mientras se desarrolla el código fuente del bot. Para usar este método, siga estos puntos:

* Cada menú admite hasta diez comandos.
* Cree un menú de comandos único que funcione en todos los ámbitos.
* Cree un menú de comandos diferente para cada ámbito.

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>Ejemplo de manifiesto para un solo menú para ambos ámbitos

El código de ejemplo de manifiesto para un solo menú para ambos ámbitos es el siguiente:

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

El código de ejemplo del manifiesto para el menú de cada ámbito es el siguiente:

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

Debes controlar los comandos de menú en el código del bot mientras controlas cualquier mensaje de los usuarios. Puede controlar los comandos de menú en el código del bot analizando la parte **\@ Mención** del texto del mensaje.

## <a name="handle-menu-commands-in-your-bot-code"></a>Controlar comandos de menú en el código del bot

Los bots de un grupo o canal responden solo cuando se `@botname` mencionan en un mensaje. Cada mensaje recibido por un bot cuando se encuentra en un ámbito de grupo o canal contiene su nombre en el texto del mensaje devuelto. Antes de controlar el comando que se devuelve, el análisis de mensajes debe controlar el mensaje recibido por un bot con su nombre.

> [!NOTE]
> Para controlar los comandos en el código, se envían al bot como un mensaje normal. Debe controlarlos como controlaría cualquier otro mensaje de los usuarios. Los comandos del código insertan texto preconfigurado en el cuadro de texto. A continuación, el usuario debe enviar ese texto como lo hace con cualquier otro mensaje.

# <a name="c"></a>[C#](#tab/dotnet)

Puede analizar la parte **\@ Mención** del texto del mensaje mediante un método estático proporcionado con Microsoft Bot Framework. Es un método de la `Activity` clase denominada `RemoveRecipientMention` .

El C# código para analizar la parte de **\@ mención** del texto del mensaje es la siguiente:

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Puede analizar la parte **\@ Mención** del texto del mensaje mediante un método estático proporcionado con Bot Framework. Es un método de la `TurnContext` clase denominada `removeMentionText` .

El código JavaScript para analizar la parte **\@ de** mención del texto del mensaje es el siguiente:

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

Puede analizar la parte **@Mention** del texto del mensaje mediante un método estático proporcionado con Bot Framework. Es un método de la `TurnContext` clase denominada `remove_recipient_mention` .

El código de Python para analizar la parte **\@ de** mención del texto del mensaje es el siguiente:

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

Para que el código del bot funcione correctamente, hay pocos procedimientos recomendados que debe seguir.

## <a name="command-menu-best-practices"></a>Procedimientos recomendados del menú de comandos

Estos son los procedimientos recomendados del menú de comandos:

* Mantenlo sencillo: el menú del bot está diseñado para presentar las funciones clave del bot.
* Tenga en cuenta que las opciones de menú no deben ser largas y no deben ser instrucciones complejas de lenguaje natural. Deben ser comandos simples.
* Mantenerlo invokable: las acciones o comandos del menú Bot siempre deben estar disponibles, independientemente del estado de la conversación o del cuadro de diálogo en el que se encuentra el bot.

> [!NOTE]
> Si quitas cualquier comando del manifiesto, debes volver a implementar la aplicación para implementar los cambios. En general, cualquier cambio en el manifiesto requiere que vuelvas a implementar la aplicación.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Conversaciones de canal y grupo](~/bots/how-to/conversations/channel-and-group-conversations.md)
