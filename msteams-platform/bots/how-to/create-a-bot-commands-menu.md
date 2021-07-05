---
title: Crear un menú de comandos para el bot
author: surbhigupta
description: Cómo crear un menú de comandos para el Microsoft Teams bot
ms.topic: how-to
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 4ee8c48b2f3b10c8924b0e81dae0a0c1f6014414
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254317"
---
# <a name="bot-command-menus"></a><span data-ttu-id="f9af9-103">Menús de comandos bot</span><span class="sxs-lookup"><span data-stu-id="f9af9-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="f9af9-104">Para definir un conjunto de comandos principales a los que el bot puede responder, puede agregar un menú de comandos con una lista desplegable de comandos para el bot.</span><span class="sxs-lookup"><span data-stu-id="f9af9-104">To define a set of core commands that your bot can respond to, you can add a command menu with a drop-down list of commands for your bot.</span></span> <span data-ttu-id="f9af9-105">La lista de comandos se presenta a los usuarios en el área del mensaje de redacción cuando están en conversación con el bot.</span><span class="sxs-lookup"><span data-stu-id="f9af9-105">The list of commands is presented to the users in the compose message area when they are in conversation with your bot.</span></span> <span data-ttu-id="f9af9-106">Seleccione un comando de la lista para insertar la cadena de comandos en el cuadro de mensaje de redacción y seleccione **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="f9af9-106">Select a command from the list to insert the command string into the compose message box and select **Send**.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f9af9-107">Escritorio</span><span class="sxs-lookup"><span data-stu-id="f9af9-107">Desktop</span></span>](#tab/desktop)

![Menú de comandos Bot](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[<span data-ttu-id="f9af9-109">Móvil</span><span class="sxs-lookup"><span data-stu-id="f9af9-109">Mobile</span></span>](#tab/mobile)

![Menú de comandos del bot móvil](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="f9af9-111">Crear un menú de comandos para el bot</span><span class="sxs-lookup"><span data-stu-id="f9af9-111">Create a command menu for your bot</span></span>

<span data-ttu-id="f9af9-112">Los menús de comandos se definen en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9af9-112">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="f9af9-113">Puedes usar **App Studio** para crearlos o agregarlos manualmente en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9af9-113">You can either use **App Studio** to create them or add them manually in the app manifest.</span></span>

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="f9af9-114">Crear un menú de comandos para el bot con App Studio</span><span class="sxs-lookup"><span data-stu-id="f9af9-114">Create a command menu for your bot using App Studio</span></span>

<span data-ttu-id="f9af9-115">Un requisito previo para crear un menú de comandos para el bot es que debes editar un manifiesto de aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="f9af9-115">A prerequisite to create a command menu for your bot is that you must edit an existing app manifest.</span></span> <span data-ttu-id="f9af9-116">Los pasos para agregar un menú de comandos son los mismos, ya sea que cree un nuevo manifiesto o edite uno existente.</span><span class="sxs-lookup"><span data-stu-id="f9af9-116">The steps to add a command menu are the same, whether you create a new manifest or edit an existing one.</span></span>

<span data-ttu-id="f9af9-117">**Para crear un menú de comandos para el bot con App Studio**</span><span class="sxs-lookup"><span data-stu-id="f9af9-117">**To create a command menu for your bot using App Studio**</span></span>

1. <span data-ttu-id="f9af9-118">Abre Teams y selecciona **Aplicaciones** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="f9af9-118">Open Teams and select **Apps** from the left pane.</span></span> <span data-ttu-id="f9af9-119">En la **página Aplicaciones,** busque **App Studio** y seleccione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="f9af9-119">In the **Apps** page, search for **App Studio**, and select **Open**.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="f9af9-120">Si no tienes **App Studio,** puedes descargarlo.</span><span class="sxs-lookup"><span data-stu-id="f9af9-120">If you do not have **App Studio**, you can download it.</span></span> <span data-ttu-id="f9af9-121">Para obtener más información, consulta [instalación de App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).</span><span class="sxs-lookup"><span data-stu-id="f9af9-121">For more information, see [installing App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).</span></span>

    ![App Studio](./conversations/media/AppStudio.png)

2. <span data-ttu-id="f9af9-123">En **App Studio,** seleccione la **pestaña Editor de manifiestos.** Si no tienes un paquete de aplicación existente, puedes crear o importar una aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="f9af9-123">In **App Studio**, select the **Manifest editor** tab. If you do not have an existing app package, you can create or import an existing app.</span></span> <span data-ttu-id="f9af9-124">Para obtener más información, [consulta Actualizar un paquete de la aplicación](~/get-started/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package).</span><span class="sxs-lookup"><span data-stu-id="f9af9-124">For more information, see [update an app package](~/get-started/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package).</span></span>

3. <span data-ttu-id="f9af9-125">En el panel izquierdo del **editor de manifiestos** y en la sección **Funcionalidades,** seleccione **Bots**.</span><span class="sxs-lookup"><span data-stu-id="f9af9-125">In the left pane of the **Manifest editor** and in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="f9af9-126">En el panel derecho del **editor de manifiestos** y en la **sección Comandos,** seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f9af9-126">In the right pane of the **Manifest editor** and in the **Commands** section, select **Add**.</span></span> <span data-ttu-id="f9af9-127">Aparecerá **la pantalla Nuevo** comando.</span><span class="sxs-lookup"><span data-stu-id="f9af9-127">The **New Command** screen appears.</span></span>

    ![Menú Comandos de App Studio Botón Agregar](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="f9af9-129">Escriba el **texto comando** que debe aparecer como el menú de comandos del bot.</span><span class="sxs-lookup"><span data-stu-id="f9af9-129">Enter the **Command text** that must appear as the command menu for your bot.</span></span>

6. <span data-ttu-id="f9af9-130">Escriba el **texto de ayuda** que debe aparecer debajo del texto del comando en el menú.</span><span class="sxs-lookup"><span data-stu-id="f9af9-130">Enter the **Help text** that must appear under the command text in the menu.</span></span> <span data-ttu-id="f9af9-131">**El texto de** la ayuda debe ser una breve explicación del propósito del comando.</span><span class="sxs-lookup"><span data-stu-id="f9af9-131">**Help text** must be a brief explanation of the purpose of the command.</span></span>

7. <span data-ttu-id="f9af9-132">Active las **casillas** Ámbito para seleccionar dónde debe aparecer este menú de comandos y **seleccione Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f9af9-132">Select the **Scope** check boxes to select where this command menu must appear, and select **Save**.</span></span>

    ![Botón de menú Nuevos comandos de App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="f9af9-134">Crear un menú de comandos para el bot editando Manifest.js</span><span class="sxs-lookup"><span data-stu-id="f9af9-134">Create a command menu for your bot by editing Manifest.json</span></span>

<span data-ttu-id="f9af9-135">Otra forma de crear un menú de comandos es crearlo directamente en el archivo de manifiesto mientras se desarrolla el código fuente del bot.</span><span class="sxs-lookup"><span data-stu-id="f9af9-135">Another way to create a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="f9af9-136">Para usar este método, siga estos puntos:</span><span class="sxs-lookup"><span data-stu-id="f9af9-136">To use this method, follow these points:</span></span>

* <span data-ttu-id="f9af9-137">Cada menú admite hasta diez comandos.</span><span class="sxs-lookup"><span data-stu-id="f9af9-137">Each menu supports up to ten commands.</span></span>
* <span data-ttu-id="f9af9-138">Cree un menú de comandos único que funcione en todos los ámbitos.</span><span class="sxs-lookup"><span data-stu-id="f9af9-138">Create a single command menu that works in all scopes.</span></span>
* <span data-ttu-id="f9af9-139">Cree un menú de comandos diferente para cada ámbito.</span><span class="sxs-lookup"><span data-stu-id="f9af9-139">Create a different command menu for each scope.</span></span>

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a><span data-ttu-id="f9af9-140">Ejemplo de manifiesto para un solo menú para ambos ámbitos</span><span class="sxs-lookup"><span data-stu-id="f9af9-140">Manifest example for single menu for both scopes</span></span>

<span data-ttu-id="f9af9-141">El código de ejemplo de manifiesto para un solo menú para ambos ámbitos es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9af9-141">The manifest example code for single menu for both scopes is as follows:</span></span>

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

#### <a name="manifest-example-for-the-menu-for-each-scope"></a><span data-ttu-id="f9af9-142">Ejemplo de manifiesto para el menú de cada ámbito</span><span class="sxs-lookup"><span data-stu-id="f9af9-142">Manifest example for the menu for each scope</span></span>

<span data-ttu-id="f9af9-143">El código de ejemplo del manifiesto para el menú de cada ámbito es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9af9-143">The manifest example code for the menu for each scope is as follows:</span></span>

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

<span data-ttu-id="f9af9-144">Debes controlar los comandos de menú en el código del bot mientras controlas cualquier mensaje de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="f9af9-144">You must handle menu commands in your bot code as you handle any message from users.</span></span> <span data-ttu-id="f9af9-145">Puede controlar los comandos de menú en el código del bot analizando la parte **\@ Mención** del texto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="f9af9-145">You can handle menu commands in your bot code by parsing out the **\@Mention** portion of the message text.</span></span>

## <a name="handle-menu-commands-in-your-bot-code"></a><span data-ttu-id="f9af9-146">Controlar comandos de menú en el código del bot</span><span class="sxs-lookup"><span data-stu-id="f9af9-146">Handle menu commands in your bot code</span></span>

<span data-ttu-id="f9af9-147">Los bots de un grupo o canal responden solo cuando se `@botname` mencionan en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="f9af9-147">Bots in a group or channel respond only when they are mentioned `@botname` in a message.</span></span> <span data-ttu-id="f9af9-148">Cada mensaje recibido por un bot cuando se encuentra en un ámbito de grupo o canal contiene su nombre en el texto del mensaje devuelto.</span><span class="sxs-lookup"><span data-stu-id="f9af9-148">Every message received by a bot when in a group or channel scope contains its name in the message text returned.</span></span> <span data-ttu-id="f9af9-149">Antes de controlar el comando que se devuelve, el análisis de mensajes debe controlar el mensaje recibido por un bot con su nombre.</span><span class="sxs-lookup"><span data-stu-id="f9af9-149">Before handling the command being returned, your message parsing must handle the message received by a bot with its name.</span></span>

> [!NOTE]
> <span data-ttu-id="f9af9-150">Para controlar los comandos en el código, se envían al bot como un mensaje normal.</span><span class="sxs-lookup"><span data-stu-id="f9af9-150">To handle the commands in code, they are sent to your bot as a regular message.</span></span> <span data-ttu-id="f9af9-151">Debe controlarlos como controlaría cualquier otro mensaje de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="f9af9-151">You must handle them as you would handle any other message from your users.</span></span> <span data-ttu-id="f9af9-152">Los comandos del código insertan texto preconfigurado en el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="f9af9-152">The commands in code insert pre-configured text into the text box.</span></span> <span data-ttu-id="f9af9-153">A continuación, el usuario debe enviar ese texto como lo hace con cualquier otro mensaje.</span><span class="sxs-lookup"><span data-stu-id="f9af9-153">The user must then send that text as they do for any other message.</span></span>

# <a name="c"></a>[<span data-ttu-id="f9af9-154">C#</span><span class="sxs-lookup"><span data-stu-id="f9af9-154">C#</span></span>](#tab/dotnet)

<span data-ttu-id="f9af9-155">Puede analizar la parte **\@ Mención** del texto del mensaje mediante un método estático proporcionado con el Microsoft Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="f9af9-155">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework.</span></span> <span data-ttu-id="f9af9-156">Es un método de la `Activity` clase denominada `RemoveRecipientMention` .</span><span class="sxs-lookup"><span data-stu-id="f9af9-156">It is a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

<span data-ttu-id="f9af9-157">El C# código para analizar la parte de **\@ mención** del texto del mensaje es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9af9-157">The C# code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[<span data-ttu-id="f9af9-158">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f9af9-158">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="f9af9-159">Puede analizar la parte **\@ Mención** del texto del mensaje mediante un método estático proporcionado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="f9af9-159">You can parse out the **\@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="f9af9-160">Es un método de la `TurnContext` clase denominada `removeMentionText` .</span><span class="sxs-lookup"><span data-stu-id="f9af9-160">It is a method of the `TurnContext` class named `removeMentionText`.</span></span>

<span data-ttu-id="f9af9-161">El código JavaScript para analizar la parte **\@ de** mención del texto del mensaje es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9af9-161">The JavaScript code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[<span data-ttu-id="f9af9-162">Python</span><span class="sxs-lookup"><span data-stu-id="f9af9-162">Python</span></span>](#tab/python)

<span data-ttu-id="f9af9-163">Puede analizar la parte **@Mention** del texto del mensaje mediante un método estático proporcionado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="f9af9-163">You can parse out the **@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="f9af9-164">Es un método de la `TurnContext` clase denominada `remove_recipient_mention` .</span><span class="sxs-lookup"><span data-stu-id="f9af9-164">It is a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

<span data-ttu-id="f9af9-165">El código de Python para analizar la parte **\@ de** mención del texto del mensaje es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9af9-165">The Python code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

<span data-ttu-id="f9af9-166">Para que el código del bot funcione correctamente, hay pocos procedimientos recomendados que debe seguir.</span><span class="sxs-lookup"><span data-stu-id="f9af9-166">To enable smooth functioning of your bot code, there are few best practices that you must follow.</span></span>

## <a name="command-menu-best-practices"></a><span data-ttu-id="f9af9-167">Procedimientos recomendados del menú de comandos</span><span class="sxs-lookup"><span data-stu-id="f9af9-167">Command menu best practices</span></span>

<span data-ttu-id="f9af9-168">Estos son los procedimientos recomendados del menú de comandos:</span><span class="sxs-lookup"><span data-stu-id="f9af9-168">Following are the command menu best practices:</span></span>

* <span data-ttu-id="f9af9-169">Mantenlo sencillo: el menú del bot está diseñado para presentar las funciones clave del bot.</span><span class="sxs-lookup"><span data-stu-id="f9af9-169">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="f9af9-170">Tenga en cuenta que las opciones de menú no deben ser largas y no deben ser instrucciones complejas de lenguaje natural.</span><span class="sxs-lookup"><span data-stu-id="f9af9-170">Keep it short: Menu options must not be long and must not be complex natural language statements.</span></span> <span data-ttu-id="f9af9-171">Deben ser comandos simples.</span><span class="sxs-lookup"><span data-stu-id="f9af9-171">They must be simple commands.</span></span>
* <span data-ttu-id="f9af9-172">Mantenerlo invokable: las acciones o comandos del menú Bot siempre deben estar disponibles, independientemente del estado de la conversación o del cuadro de diálogo en el que se encuentra el bot.</span><span class="sxs-lookup"><span data-stu-id="f9af9-172">Keep it invokable: Bot menu actions or commands must always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>

> [!NOTE]
> <span data-ttu-id="f9af9-173">Si quitas cualquier comando del manifiesto, debes volver a implementar la aplicación para implementar los cambios.</span><span class="sxs-lookup"><span data-stu-id="f9af9-173">If you remove any commands from your manifest, you must redeploy your app to implement the changes.</span></span> <span data-ttu-id="f9af9-174">En general, cualquier cambio en el manifiesto requiere que vuelvas a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9af9-174">In general, any changes to the manifest require you to redeploy your app.</span></span>

## <a name="next-step"></a><span data-ttu-id="f9af9-175">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="f9af9-175">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9af9-176">Conversaciones de canal y grupo</span><span class="sxs-lookup"><span data-stu-id="f9af9-176">Channel and group conversations</span></span>](~/bots/how-to/conversations/channel-and-group-conversations.md)
