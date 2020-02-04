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
# <a name="bot-command-menus"></a><span data-ttu-id="9fe82-103">Menús de comandos de bot</span><span class="sxs-lookup"><span data-stu-id="9fe82-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> <span data-ttu-id="9fe82-104">Los menús de bot no aparecerán en los clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="9fe82-104">Bot menus won't appear on mobile clients.</span></span>

<span data-ttu-id="9fe82-105">Add Command menu for your bot permite definir un conjunto de comandos básicos a los que siempre puede responder el bot.</span><span class="sxs-lookup"><span data-stu-id="9fe82-105">Add command menu for your bot allows you to define a set of core commands your bot can always respond to.</span></span> <span data-ttu-id="9fe82-106">La lista de comandos se presenta al usuario encima del área de mensaje de redacción cuando se trata con el bot.</span><span class="sxs-lookup"><span data-stu-id="9fe82-106">The list of commands is presented to the user above the compose message area when they are conversing with your bot.</span></span> <span data-ttu-id="9fe82-107">Al seleccionar un comando de la lista, se insertará la cadena de comandos en el cuadro de mensaje de redacción y, a continuación, todos los usuarios tendrán que hacer clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="9fe82-107">Selecting a command from the list will insert the command string into the compose message box, then all users need to do is select **Send**.</span></span>

![Menú de comandos de bot](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="9fe82-109">Crear un menú de comandos para el bot</span><span class="sxs-lookup"><span data-stu-id="9fe82-109">Create a command menu for your bot</span></span>

<span data-ttu-id="9fe82-110">Los menús de comandos se definen en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fe82-110">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="9fe82-111">Puede usar App Studio para ayudarle a crearlos, o bien agregarlos de forma manual.</span><span class="sxs-lookup"><span data-stu-id="9fe82-111">You can either use App Studio to help you create them, or add them manually.</span></span>

### <a name="creating-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="9fe82-112">Crear un menú de comandos para el bot con App Studio</span><span class="sxs-lookup"><span data-stu-id="9fe82-112">Creating a command menu for your bot using App Studio</span></span>

<span data-ttu-id="9fe82-113">En estas instrucciones se da por sentado que va a editar un manifiesto de aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="9fe82-113">The instructions here assume that you'll be editing an existing app manifest.</span></span> <span data-ttu-id="9fe82-114">Los pasos para agregar un menú de comandos son los mismos, tanto si está creando un manifiesto nuevo o editando uno existente.</span><span class="sxs-lookup"><span data-stu-id="9fe82-114">The steps for adding a command menu are the same, whether you're creating a new manifest or editing an existing one.</span></span>

1. <span data-ttu-id="9fe82-115">Abra App Studio desde el... menú de desbordamiento en el raíl de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="9fe82-115">Open App Studio from the ... overflow menu on the left navigation rail.</span></span> <span data-ttu-id="9fe82-116">Si no tiene App Studio disponible, puede descargarlo.</span><span class="sxs-lookup"><span data-stu-id="9fe82-116">If you don't have App Studio available you can download it.</span></span> <span data-ttu-id="9fe82-117">Vea [Installing App Studio](https://aka.ms/teams-app-studio#installing-app-studio) para obtener más información sobre el uso de App Studio.</span><span class="sxs-lookup"><span data-stu-id="9fe82-117">See [Installing App Studio](https://aka.ms/teams-app-studio#installing-app-studio) for more information on using App Studio.</span></span>

    ![App Studio](./conversations/media/AppStudio.png)

2. <span data-ttu-id="9fe82-119">Una vez en App Studio, seleccione la pestaña **Editor de manifiestos** .</span><span class="sxs-lookup"><span data-stu-id="9fe82-119">Once in App Studio, select the **Manifest editor** tab.</span></span>

3. <span data-ttu-id="9fe82-120">En la columna izquierda de la vista editor de manifiestos, en la sección **capacidades** , seleccione **bots**.</span><span class="sxs-lookup"><span data-stu-id="9fe82-120">In the left column of the manifest editor view in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="9fe82-121">En la columna derecha de la vista editor de manifiestos, en la sección **comandos** , seleccione el botón **Agregar** .</span><span class="sxs-lookup"><span data-stu-id="9fe82-121">In the right column of the manifest editor view in the **Commands** section, select the **Add** button.</span></span>

    ![Botón Agregar del menú de comandos de App Studio](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="9fe82-123">Aparece la pantalla **nuevo comando** .</span><span class="sxs-lookup"><span data-stu-id="9fe82-123">The **New Command** screen appears.</span></span> <span data-ttu-id="9fe82-124">Escriba el **texto del comando** que desea que aparezca como comando de menú y el texto de **ayuda** que desea que aparezca directamente debajo del texto del comando en el menú.</span><span class="sxs-lookup"><span data-stu-id="9fe82-124">Enter the **Command text** that you want to have appear as the menu command, and the **Help text** that you want to have appear directly under the command text in the menu.</span></span> <span data-ttu-id="9fe82-125">Esta debe ser una breve explicación del propósito del comando.</span><span class="sxs-lookup"><span data-stu-id="9fe82-125">This should be a brief explanation of the purpose of the command.</span></span>

6. <span data-ttu-id="9fe82-126">A continuación, seleccione el ámbito o ámbitos donde desea que aparezca este menú de comandos y, a continuación, seleccione el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9fe82-126">Next, select the scope(s) where you want this command menu to appear, then select the **Save** button.</span></span>

    ![Botón Agregar del menú de comandos de App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="creating-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="9fe82-128">Crear un menú de comandos para el bot editando **manifest. JSON**</span><span class="sxs-lookup"><span data-stu-id="9fe82-128">Creating a command menu for your bot by editing **Manifest.json**</span></span>

<span data-ttu-id="9fe82-129">Otro enfoque válido para crear un menú de comandos es crearlo directamente en el archivo de manifiesto mientras se desarrolla el código fuente de bot.</span><span class="sxs-lookup"><span data-stu-id="9fe82-129">Another valid approach for creating a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="9fe82-130">Estas son algunas de las cosas que debe tener en cuenta al usar este enfoque:</span><span class="sxs-lookup"><span data-stu-id="9fe82-130">Here are a few things to keep in mind when using this approach:</span></span>

1. <span data-ttu-id="9fe82-131">Cada menú admite hasta 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="9fe82-131">Each menu supports up to 10 commands.</span></span>

2. <span data-ttu-id="9fe82-132">Se puede crear un solo menú de comandos que funcione en todos los ámbitos.</span><span class="sxs-lookup"><span data-stu-id="9fe82-132">You can create a single command menu that will work in all scopes.</span></span>

3. <span data-ttu-id="9fe82-133">Puede crear un menú de comandos diferente para cada ámbito</span><span class="sxs-lookup"><span data-stu-id="9fe82-133">You can create a different command menu for each scope</span></span>

#### <a name="manifest-example---single-menu-for-both-scopes"></a><span data-ttu-id="9fe82-134">Ejemplo de manifiesto: menú único para ambos ámbitos</span><span class="sxs-lookup"><span data-stu-id="9fe82-134">Manifest example - single menu for both scopes</span></span>

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

#### <a name="manifest-example---menu-for-each-scope"></a><span data-ttu-id="9fe82-135">Ejemplo de manifiesto: menú para cada ámbito</span><span class="sxs-lookup"><span data-stu-id="9fe82-135">Manifest example - menu for each scope</span></span>

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

## <a name="handling-menu-commands-in-your-bot-code"></a><span data-ttu-id="9fe82-136">Control de comandos de menú en el código de bot</span><span class="sxs-lookup"><span data-stu-id="9fe82-136">Handling menu commands in your bot code</span></span>

<span data-ttu-id="9fe82-137">Los bots de un grupo o canal solo responden cuando se mencionan ("@botname") en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="9fe82-137">Bots in a group or channel respond only when they are mentioned ("@botname") in a message.</span></span> <span data-ttu-id="9fe82-138">Como resultado, cada mensaje recibido por un bot cuando se encuentre en un ámbito de grupo o de canal contendrá su propio nombre en el texto del mensaje devuelto.</span><span class="sxs-lookup"><span data-stu-id="9fe82-138">As a result, every message received by a bot when in a group or channel scope will contain its own name in the message text returned.</span></span> <span data-ttu-id="9fe82-139">Debe asegurarse de que los controladores de análisis de mensajes antes de controlar el comando que se devuelve.</span><span class="sxs-lookup"><span data-stu-id="9fe82-139">You need to ensure your message parsing handles that before handling the command being returned.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9fe82-140">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9fe82-140">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="9fe82-141">Puede analizar la `Activity` `RemoveRecipientMention` \*\* \@parte de menciones\*\* del texto del mensaje usando un método estático proporcionado con Microsoft bot Framework, un método de la clase denominada.</span><span class="sxs-lookup"><span data-stu-id="9fe82-141">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="9fe82-142">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="9fe82-142">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="9fe82-143">Puede analizar la `TurnContext` `removeMentionText` \*\* \@parte de menciones\*\* del texto del mensaje usando un método estático proporcionado con Microsoft bot Framework, un método de la clase denominada.</span><span class="sxs-lookup"><span data-stu-id="9fe82-143">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `removeMentionText`.</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="pythontabpython"></a>[<span data-ttu-id="9fe82-144">Python</span><span class="sxs-lookup"><span data-stu-id="9fe82-144">Python</span></span>](#tab/python)


<span data-ttu-id="9fe82-145">Puede analizar la parte **@Mention** del texto del mensaje usando un método estático proporcionado con Microsoft bot Framework, un método de la `TurnContext` clase denominada. `remove_recipient_mention`</span><span class="sxs-lookup"><span data-stu-id="9fe82-145">You can parse out the **@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework — a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

## <a name="command-menu-best-practices"></a><span data-ttu-id="9fe82-146">Procedimientos recomendados de menús de comandos</span><span class="sxs-lookup"><span data-stu-id="9fe82-146">Command menu best practices</span></span>

* <span data-ttu-id="9fe82-147">**Manténgase sencillo**: el menú bot tiene como objetivo presentar las capacidades clave de su bot.</span><span class="sxs-lookup"><span data-stu-id="9fe82-147">**Keep it simple**: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="9fe82-148">**Tenga en Resumen**: las opciones de menú no deben ser muy largas y complejas con instrucciones de lenguaje natural, sino que deben ser comandos simples.</span><span class="sxs-lookup"><span data-stu-id="9fe82-148">**Keep it short**: Menu options shouldn’t be extremely long and complex natural language statements — they should be simple commands.</span></span>
* <span data-ttu-id="9fe82-149">**Guardar invokable**: los comandos o acciones del menú bot siempre deben estar disponibles, independientemente del estado de la conversación o el cuadro de diálogo en el que se encuentra el bot.</span><span class="sxs-lookup"><span data-stu-id="9fe82-149">**Keep it invokable**: Bot menu actions/commands should always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>
