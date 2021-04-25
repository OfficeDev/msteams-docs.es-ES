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
# <a name="bot-command-menus"></a><span data-ttu-id="e48ee-103">Menús de comandos bot</span><span class="sxs-lookup"><span data-stu-id="e48ee-103">Bot command menus</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> <span data-ttu-id="e48ee-104">Los menús bot no aparecen en clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="e48ee-104">Bot menus do not appear on mobile clients.</span></span>

<span data-ttu-id="e48ee-105">Para definir un conjunto de comandos principales a los que el bot puede responder, puede agregar un menú de comandos con una lista desplegable de comandos para el bot.</span><span class="sxs-lookup"><span data-stu-id="e48ee-105">To define a set of core commands that your bot can respond to, you can add a command menu with a drop-down list of commands for your bot.</span></span> <span data-ttu-id="e48ee-106">La lista de comandos se presenta a los usuarios en el área del mensaje de redacción cuando están en conversación con el bot.</span><span class="sxs-lookup"><span data-stu-id="e48ee-106">The list of commands is presented to the users in the compose message area when they are in conversation with your bot.</span></span> <span data-ttu-id="e48ee-107">Seleccione un comando de la lista para insertar la cadena de comandos en el cuadro de mensaje de redacción y seleccione **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="e48ee-107">Select a command from the list to insert the command string into the compose message box and select **Send**.</span></span>

![Menú de comandos Bot](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a><span data-ttu-id="e48ee-109">Crear un menú de comandos para el bot</span><span class="sxs-lookup"><span data-stu-id="e48ee-109">Create a command menu for your bot</span></span>

<span data-ttu-id="e48ee-110">Los menús de comandos se definen en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e48ee-110">Command menus are defined in your app manifest.</span></span> <span data-ttu-id="e48ee-111">Puedes usar **App Studio** para crearlos o agregarlos manualmente en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e48ee-111">You can either use **App Studio** to create them or add them manually in the app manifest.</span></span>

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a><span data-ttu-id="e48ee-112">Crear un menú de comandos para el bot con App Studio</span><span class="sxs-lookup"><span data-stu-id="e48ee-112">Create a command menu for your bot using App Studio</span></span>

<span data-ttu-id="e48ee-113">Un requisito previo para crear un menú de comandos para el bot es que debes editar un manifiesto de aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="e48ee-113">A prerequisite to create a command menu for your bot is that you must edit an existing app manifest.</span></span> <span data-ttu-id="e48ee-114">Los pasos para agregar un menú de comandos son los mismos, ya sea que cree un nuevo manifiesto o edite uno existente.</span><span class="sxs-lookup"><span data-stu-id="e48ee-114">The steps to add a command menu are the same, whether you create a new manifest or edit an existing one.</span></span>

<span data-ttu-id="e48ee-115">**Para crear un menú de comandos para el bot con App Studio**</span><span class="sxs-lookup"><span data-stu-id="e48ee-115">**To create a command menu for your bot using App Studio**</span></span>

1. <span data-ttu-id="e48ee-116">Abra Teams y seleccione **Aplicaciones** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="e48ee-116">Open Teams and select **Apps** from the left pane.</span></span> <span data-ttu-id="e48ee-117">En la **página Aplicaciones,** busque **App Studio** y seleccione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="e48ee-117">In the **Apps** page, search for **App Studio**, and select **Open**.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="e48ee-118">Si no tienes **App Studio,** puedes descargarlo.</span><span class="sxs-lookup"><span data-stu-id="e48ee-118">If you do not have **App Studio**, you can download it.</span></span> <span data-ttu-id="e48ee-119">Para obtener más información, consulta [instalación de App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).</span><span class="sxs-lookup"><span data-stu-id="e48ee-119">For more information, see [installing App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).</span></span>

    ![App Studio](./conversations/media/AppStudio.png)

2. <span data-ttu-id="e48ee-121">En **App Studio,** seleccione la **pestaña Editor de manifiestos.** Si no tienes un paquete de aplicación existente, puedes crear o importar una aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="e48ee-121">In **App Studio**, select the **Manifest editor** tab. If you do not have an existing app package, you can create or import an existing app.</span></span> <span data-ttu-id="e48ee-122">Para obtener más información, [consulta Actualizar un paquete de la aplicación](~/tutorials/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package).</span><span class="sxs-lookup"><span data-stu-id="e48ee-122">For more information, see [update an app package](~/tutorials/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package).</span></span>

3. <span data-ttu-id="e48ee-123">En el panel izquierdo del **editor de manifiestos** y en la sección **Funcionalidades,** seleccione **Bots**.</span><span class="sxs-lookup"><span data-stu-id="e48ee-123">In the left pane of the **Manifest editor** and in the **Capabilities** section, select **Bots**.</span></span>

4. <span data-ttu-id="e48ee-124">En el panel derecho del **editor de manifiestos** y en la **sección Comandos,** seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e48ee-124">In the right pane of the **Manifest editor** and in the **Commands** section, select **Add**.</span></span> <span data-ttu-id="e48ee-125">Aparecerá **la pantalla Nuevo** comando.</span><span class="sxs-lookup"><span data-stu-id="e48ee-125">The **New Command** screen appears.</span></span>

    ![Menú Comandos de App Studio Botón Agregar](./conversations/media/AppStudio-CommandMenu-Add.png)

5. <span data-ttu-id="e48ee-127">Escriba el **texto comando** que debe aparecer como el menú de comandos del bot.</span><span class="sxs-lookup"><span data-stu-id="e48ee-127">Enter the **Command text** that must appear as the command menu for your bot.</span></span>

6. <span data-ttu-id="e48ee-128">Escriba el **texto de ayuda** que debe aparecer debajo del texto del comando en el menú.</span><span class="sxs-lookup"><span data-stu-id="e48ee-128">Enter the **Help text** that must appear under the command text in the menu.</span></span> <span data-ttu-id="e48ee-129">**El texto de** la ayuda debe ser una breve explicación del propósito del comando.</span><span class="sxs-lookup"><span data-stu-id="e48ee-129">**Help text** must be a brief explanation of the purpose of the command.</span></span>

7. <span data-ttu-id="e48ee-130">Active las **casillas** Ámbito para seleccionar dónde debe aparecer este menú de comandos y **seleccione Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e48ee-130">Select the **Scope** check boxes to select where this command menu must appear, and select **Save**.</span></span>

    ![Botón de menú Nuevos comandos de App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a><span data-ttu-id="e48ee-132">Crear un menú de comandos para el bot editando Manifest.js</span><span class="sxs-lookup"><span data-stu-id="e48ee-132">Create a command menu for your bot by editing Manifest.json</span></span>

<span data-ttu-id="e48ee-133">Otra forma de crear un menú de comandos es crearlo directamente en el archivo de manifiesto mientras se desarrolla el código fuente del bot.</span><span class="sxs-lookup"><span data-stu-id="e48ee-133">Another way to create a command menu is to create it directly in the manifest file while developing your bot source code.</span></span> <span data-ttu-id="e48ee-134">Para usar este método, siga estos puntos:</span><span class="sxs-lookup"><span data-stu-id="e48ee-134">To use this method, follow these points:</span></span>

* <span data-ttu-id="e48ee-135">Cada menú admite hasta diez comandos.</span><span class="sxs-lookup"><span data-stu-id="e48ee-135">Each menu supports up to ten commands.</span></span>
* <span data-ttu-id="e48ee-136">Cree un menú de comandos único que funcione en todos los ámbitos.</span><span class="sxs-lookup"><span data-stu-id="e48ee-136">Create a single command menu that works in all scopes.</span></span>
* <span data-ttu-id="e48ee-137">Cree un menú de comandos diferente para cada ámbito.</span><span class="sxs-lookup"><span data-stu-id="e48ee-137">Create a different command menu for each scope.</span></span>

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a><span data-ttu-id="e48ee-138">Ejemplo de manifiesto para un solo menú para ambos ámbitos</span><span class="sxs-lookup"><span data-stu-id="e48ee-138">Manifest example for single menu for both scopes</span></span>

<span data-ttu-id="e48ee-139">El código de ejemplo de manifiesto para un solo menú para ambos ámbitos es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="e48ee-139">The manifest example code for single menu for both scopes is as follows:</span></span>

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

#### <a name="manifest-example-for-the-menu-for-each-scope"></a><span data-ttu-id="e48ee-140">Ejemplo de manifiesto para el menú de cada ámbito</span><span class="sxs-lookup"><span data-stu-id="e48ee-140">Manifest example for the menu for each scope</span></span>

<span data-ttu-id="e48ee-141">El código de ejemplo del manifiesto para el menú de cada ámbito es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="e48ee-141">The manifest example code for the menu for each scope is as follows:</span></span>

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

<span data-ttu-id="e48ee-142">Debes controlar los comandos de menú en el código del bot mientras controlas cualquier mensaje de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e48ee-142">You must handle menu commands in your bot code as you handle any message from users.</span></span> <span data-ttu-id="e48ee-143">Puede controlar los comandos de menú en el código del bot analizando la parte **\@ Mención** del texto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="e48ee-143">You can handle menu commands in your bot code by parsing out the **\@Mention** portion of the message text.</span></span>

## <a name="handle-menu-commands-in-your-bot-code"></a><span data-ttu-id="e48ee-144">Controlar comandos de menú en el código del bot</span><span class="sxs-lookup"><span data-stu-id="e48ee-144">Handle menu commands in your bot code</span></span>

<span data-ttu-id="e48ee-145">Los bots de un grupo o canal responden solo cuando se `@botname` mencionan en un mensaje.</span><span class="sxs-lookup"><span data-stu-id="e48ee-145">Bots in a group or channel respond only when they are mentioned `@botname` in a message.</span></span> <span data-ttu-id="e48ee-146">Cada mensaje recibido por un bot cuando se encuentra en un ámbito de grupo o canal contiene su nombre en el texto del mensaje devuelto.</span><span class="sxs-lookup"><span data-stu-id="e48ee-146">Every message received by a bot when in a group or channel scope contains its name in the message text returned.</span></span> <span data-ttu-id="e48ee-147">Antes de controlar el comando que se devuelve, el análisis de mensajes debe controlar el mensaje recibido por un bot con su nombre.</span><span class="sxs-lookup"><span data-stu-id="e48ee-147">Before handling the command being returned, your message parsing must handle the message received by a bot with its name.</span></span>

> [!NOTE]
> <span data-ttu-id="e48ee-148">Para controlar los comandos en el código, se envían al bot como un mensaje normal.</span><span class="sxs-lookup"><span data-stu-id="e48ee-148">To handle the commands in code, they are sent to your bot as a regular message.</span></span> <span data-ttu-id="e48ee-149">Debe controlarlos como controlaría cualquier otro mensaje de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e48ee-149">You must handle them as you would handle any other message from your users.</span></span> <span data-ttu-id="e48ee-150">Los comandos del código insertan texto preconfigurado en el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="e48ee-150">The commands in code insert pre-configured text into the text box.</span></span> <span data-ttu-id="e48ee-151">A continuación, el usuario debe enviar ese texto como lo hace con cualquier otro mensaje.</span><span class="sxs-lookup"><span data-stu-id="e48ee-151">The user must then send that text as they do for any other message.</span></span>

# <a name="c"></a>[<span data-ttu-id="e48ee-152">C#</span><span class="sxs-lookup"><span data-stu-id="e48ee-152">C#</span></span>](#tab/dotnet)

<span data-ttu-id="e48ee-153">Puede analizar la parte **\@ Mención** del texto del mensaje mediante un método estático proporcionado con Microsoft Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e48ee-153">You can parse out the **\@Mention** portion of the message text using a static method provided with the Microsoft Bot Framework.</span></span> <span data-ttu-id="e48ee-154">Es un método de la `Activity` clase denominada `RemoveRecipientMention` .</span><span class="sxs-lookup"><span data-stu-id="e48ee-154">It is a method of the `Activity` class named `RemoveRecipientMention`.</span></span>

<span data-ttu-id="e48ee-155">El C# código para analizar la parte de **\@ mención** del texto del mensaje es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="e48ee-155">The C# code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[<span data-ttu-id="e48ee-156">JavaScript</span><span class="sxs-lookup"><span data-stu-id="e48ee-156">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="e48ee-157">Puede analizar la parte **\@ Mención** del texto del mensaje mediante un método estático proporcionado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e48ee-157">You can parse out the **\@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="e48ee-158">Es un método de la `TurnContext` clase denominada `removeMentionText` .</span><span class="sxs-lookup"><span data-stu-id="e48ee-158">It is a method of the `TurnContext` class named `removeMentionText`.</span></span>

<span data-ttu-id="e48ee-159">El código JavaScript para analizar la parte **\@ de** mención del texto del mensaje es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="e48ee-159">The JavaScript code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[<span data-ttu-id="e48ee-160">Python</span><span class="sxs-lookup"><span data-stu-id="e48ee-160">Python</span></span>](#tab/python)

<span data-ttu-id="e48ee-161">Puede analizar la parte **@Mention** del texto del mensaje mediante un método estático proporcionado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="e48ee-161">You can parse out the **@Mention** portion of the message text using a static method provided with the Bot Framework.</span></span> <span data-ttu-id="e48ee-162">Es un método de la `TurnContext` clase denominada `remove_recipient_mention` .</span><span class="sxs-lookup"><span data-stu-id="e48ee-162">It is a method of the `TurnContext` class named `remove_recipient_mention`.</span></span>

<span data-ttu-id="e48ee-163">El código de Python para analizar la parte **\@ de** mención del texto del mensaje es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="e48ee-163">The Python code to parse out the **\@Mention** portion of the message text is as follows:</span></span>

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

<span data-ttu-id="e48ee-164">Para que el código del bot funcione correctamente, hay pocos procedimientos recomendados que debe seguir.</span><span class="sxs-lookup"><span data-stu-id="e48ee-164">To enable smooth functioning of your bot code, there are few best practices that you must follow.</span></span>

## <a name="command-menu-best-practices"></a><span data-ttu-id="e48ee-165">Procedimientos recomendados del menú de comandos</span><span class="sxs-lookup"><span data-stu-id="e48ee-165">Command menu best practices</span></span>

<span data-ttu-id="e48ee-166">Estos son los procedimientos recomendados del menú de comandos:</span><span class="sxs-lookup"><span data-stu-id="e48ee-166">Following are the command menu best practices:</span></span>

* <span data-ttu-id="e48ee-167">Mantenlo sencillo: el menú del bot está diseñado para presentar las funciones clave del bot.</span><span class="sxs-lookup"><span data-stu-id="e48ee-167">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="e48ee-168">Tenga en cuenta que las opciones de menú no deben ser largas y no deben ser instrucciones complejas de lenguaje natural.</span><span class="sxs-lookup"><span data-stu-id="e48ee-168">Keep it short: Menu options must not be long and must not be complex natural language statements.</span></span> <span data-ttu-id="e48ee-169">Deben ser comandos simples.</span><span class="sxs-lookup"><span data-stu-id="e48ee-169">They must be simple commands.</span></span>
* <span data-ttu-id="e48ee-170">Mantenerlo invokable: las acciones o comandos del menú Bot siempre deben estar disponibles, independientemente del estado de la conversación o del cuadro de diálogo en el que se encuentra el bot.</span><span class="sxs-lookup"><span data-stu-id="e48ee-170">Keep it invokable: Bot menu actions or commands must always be available, regardless of the state of the conversation or the dialog the bot is in.</span></span>

> [!NOTE]
> <span data-ttu-id="e48ee-171">Si quitas cualquier comando del manifiesto, debes volver a implementar la aplicación para implementar los cambios.</span><span class="sxs-lookup"><span data-stu-id="e48ee-171">If you remove any commands from your manifest, you must redeploy your app to implement the changes.</span></span> <span data-ttu-id="e48ee-172">En general, cualquier cambio en el manifiesto requiere que vuelvas a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e48ee-172">In general, any changes to the manifest require you to redeploy your app.</span></span>

## <a name="next-step"></a><span data-ttu-id="e48ee-173">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="e48ee-173">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e48ee-174">Conversaciones de canal y grupo</span><span class="sxs-lookup"><span data-stu-id="e48ee-174">Channel and group conversations</span></span>](~/bots/how-to/conversations/channel-and-group-conversations.md)
