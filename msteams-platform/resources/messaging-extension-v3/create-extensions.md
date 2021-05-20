---
title: Inician acciones con extensiones de mensajería
description: Crear extensiones de mensajería basadas en acciones para permitir a los usuarios activar servicios externos
localization_priority: Normal
ms.topic: how-to
keywords: equipos de mensajería extensiones de mensajería extensiones de mensajería buscar
ms.openlocfilehash: bfb3295726c355164f080c15e3759ea36a99d914
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566743"
---
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="b4a3e-104">Inician acciones con extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="b4a3e-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="b4a3e-105">Las extensiones de mensajería basadas en acciones permiten a los usuarios desencadenar acciones en servicios externos mientras están dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![Ejemplo de tarjeta de extensión de mensajería](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="b4a3e-107">En las secciones siguientes se describe cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="b4a3e-108">Extensiones de mensaje de tipo de acción</span><span class="sxs-lookup"><span data-stu-id="b4a3e-108">Action type message extensions</span></span>

<span data-ttu-id="b4a3e-109">Para iniciar acciones desde una extensión de mensajería, establezca el `type` parámetro en `action` .</span><span class="sxs-lookup"><span data-stu-id="b4a3e-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="b4a3e-110">A continuación se muestra un ejemplo de un manifiesto con una búsqueda y un comando create.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="b4a3e-111">Una sola extensión de mensajería puede tener hasta 10 comandos diferentes.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="b4a3e-112">Esto puede incluir varios comandos basados en la búsqueda y múltiples acciones.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="b4a3e-113">Ejemplo completo del manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b4a3e-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="b4a3e-114">Iniciar acciones desde mensajes</span><span class="sxs-lookup"><span data-stu-id="b4a3e-114">Initiate actions from messages</span></span>

<span data-ttu-id="b4a3e-115">Además de iniciar acciones desde el área de mensaje de composición, también puede usar la extensión de mensajería para iniciar una acción desde un mensaje.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="b4a3e-116">Esto le permitirá enviar el contenido del mensaje al bot para su procesamiento y, opcionalmente, responder a ese mensaje con una respuesta mediante el método descrito en [Responder para enviar](#responding-to-submit).</span><span class="sxs-lookup"><span data-stu-id="b4a3e-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="b4a3e-117">La respuesta se insertará como respuesta al mensaje que los usuarios pueden editar antes de enviar.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="b4a3e-118">Los usuarios pueden acceder a la extensión de mensajería desde el menú de desbordamiento `...` y, a continuación, seleccionar `Take action` como en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="b4a3e-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the following image:</span></span>

![Ejemplo de iniciar una acción desde un mensaje](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="b4a3e-120">Para permitir que la extensión de mensajería funcione desde un mensaje, deberá agregar el `context` parámetro al objeto de la extensión de mensajería en el manifiesto de la aplicación como en el ejemplo `commands` siguiente.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="b4a3e-121">Las cadenas válidas para la `context` matriz son , y `"message"` `"commandBox"` `"compose"` .</span><span class="sxs-lookup"><span data-stu-id="b4a3e-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="b4a3e-122">El valor predeterminado es `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="b4a3e-123">Consulte la sección [definir comandos](#define-commands) para obtener más detalles sobre el `context` parámetro.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

```json
"composeExtensions": [
  {
    "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Create To Do",
        "type": "Action",
        "context": ["message"],
        "fetchTask": true
    }]
    ...

```

<span data-ttu-id="b4a3e-124">A continuación se muestra un ejemplo del `value` objeto que contiene los detalles del mensaje que se enviarán como parte de la `composeExtension` solicitud que se enviará al bot.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "this is the message"
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

### <a name="test-via-uploading"></a><span data-ttu-id="b4a3e-125">Prueba a través de la carga</span><span class="sxs-lookup"><span data-stu-id="b4a3e-125">Test via uploading</span></span>

<span data-ttu-id="b4a3e-126">Puedes probar la extensión de mensajería subiendo la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="b4a3e-127">Para obtener más información, consulta [Carga de la aplicación en un equipo.](~/concepts/deploy-and-publish/apps-upload.md)</span><span class="sxs-lookup"><span data-stu-id="b4a3e-127">For more information, see [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md).</span></span>

<span data-ttu-id="b4a3e-128">Para abrir la extensión de mensajería, vaya a cualquiera de sus chats o canales.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="b4a3e-129">Elija el botón **Más opciones** (**&#8943;**) en el cuadro de composición y elija la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="b4a3e-130">Recopilación de entradas de los usuarios</span><span class="sxs-lookup"><span data-stu-id="b4a3e-130">Collecting input from users</span></span>

<span data-ttu-id="b4a3e-131">Hay tres maneras de recopilar información de un usuario final en Teams.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="b4a3e-132">Lista de parámetros estáticos</span><span class="sxs-lookup"><span data-stu-id="b4a3e-132">Static parameter list</span></span>

<span data-ttu-id="b4a3e-133">En este método, todo lo que necesita hacer es definir una lista estática de parámetros en el manifiesto como se muestra arriba en el comando "Crear To Do".</span><span class="sxs-lookup"><span data-stu-id="b4a3e-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="b4a3e-134">Para utilizar este método asegúrese `fetchTask` de que está establecido en y que se definen los parámetros en el `false` manifiesto.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="b4a3e-135">Cuando un usuario elige un comando con parámetros estáticos, Teams generará un formulario en un módulo de tareas con los parámetros definidos en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="b4a3e-136">Al pulsar Enviar a `composeExtension/submitAction` se envía al bot.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="b4a3e-137">Para obtener más información sobre el conjunto esperado de respuestas, consulte [Responder para enviar](#responding-to-submit).</span><span class="sxs-lookup"><span data-stu-id="b4a3e-137">For more information on the expected set of responses, see [Responding to submit](#responding-to-submit).</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="b4a3e-138">Entrada dinámica mediante una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="b4a3e-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="b4a3e-139">En este método, el servicio puede definir una tarjeta adaptable personalizada para recopilar la entrada del usuario final.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="b4a3e-140">Para este enfoque, establezca el `fetchTask` parámetro en en el `true` manifiesto.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="b4a3e-141">Tenga en cuenta que si establece `fetchTask` `true` en cualquier parámetro estático definido para el comando se omitirá.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="b4a3e-142">En este método, el servicio recibirá un `composeExtension/fetchTask` evento y deberá responder con una respuesta de módulo de [tareas](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)basada en tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-142">In this method your service will receive a `composeExtension/fetchTask` event and needs to respond with an adaptive card based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="b4a3e-143">A continuación se muestra una respuesta de muestra con una tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="b4a3e-143">Following is a sample response with an adaptive card:</span></span>

```json
{
    "task": {
        "type": "continue",
        "value": {
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": {
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Please enter the following information:"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Name"
                        },
                        {
                            "type": "Input.Text",
                            "spacing": "None",
                            "title": "New Input.Toggle",
                            "placeholder": "Placeholder text"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Date of birth"
                        },
                        {
                            "type": "Input.Date",
                            "spacing": "None",
                            "title": "New Input.Toggle"
                        }
                    ],
                    "type": "AdaptiveCard",
                    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
                    "version": "1.0"
                }
            }
        }
    }
}
```

<span data-ttu-id="b4a3e-144">El bot también puede responder con una respuesta de autenticación/configuración si el usuario necesita autenticar o configurar la extensión antes de obtener la entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="b4a3e-145">Entrada dinámica mediante una vista web</span><span class="sxs-lookup"><span data-stu-id="b4a3e-145">Dynamic input using a web view</span></span>

<span data-ttu-id="b4a3e-146">En este método, el servicio puede mostrar un `<iframe>` widget basado para mostrar cualquier interfaz de usuario personalizada y recopilar la entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="b4a3e-147">Para este enfoque, establezca el `fetchTask` parámetro en en el `true` manifiesto.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="b4a3e-148">Al igual que en el flujo de tarjeta adaptable, su servicio enviará un `fetchTask` evento y debe responder con una respuesta del módulo de [tareas](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)basada en URL.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-148">Just like in the adaptive card flow your service will be send a `fetchTask` event and needs to respond with a URL based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="b4a3e-149">A continuación se muestra una respuesta de ejemplo con una tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="b4a3e-149">Following is a sample response with an Adaptive card:</span></span>

```json
{
    "task": {
        "value": {
            "url": "http://mywebapp.com/input"
        },
        "type": "continue"
    }
}
```

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="b4a3e-150">Solicitud para instalar su bot conversacional</span><span class="sxs-lookup"><span data-stu-id="b4a3e-150">Request to install your conversational bot</span></span>

<span data-ttu-id="b4a3e-151">Si la aplicación también contiene un bot conversacional, puede ser necesario asegurarse de que el bot está instalado en la conversación antes de cargar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="b4a3e-152">Esto puede ser útil en situaciones en las que necesita obtener contexto adicional para el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="b4a3e-153">Por ejemplo, es posible que deba buscar la lista para rellenar un control de selector de personas o la lista de canales de un equipo.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="b4a3e-154">Para facilitar este flujo, cuando la extensión de mensajería recibe por primera vez la `composeExtension/fetchTask` comprobación de invocación para ver si el bot está instalado en el contexto actual.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context.</span></span> <span data-ttu-id="b4a3e-155">Podría lograr esto intentando la llamada a la lista get, por ejemplo, Si el bot no está instalado, devuelve una tarjeta adaptable con una acción que solicita al usuario que instale el bot Vea el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-155">You could accomplish this by attempting the get roster call, for example, If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="b4a3e-156">Tenga en cuenta que esto requiere que el usuario tenga permiso para instalar aplicaciones en esa ubicación; si no pueden, se les presentará un mensaje pidiéndoles que se pongan en contacto con su administrador.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="b4a3e-157">Este es un ejemplo de la respuesta:</span><span class="sxs-lookup"><span data-stu-id="b4a3e-157">Here's an example of the response:</span></span>

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

<span data-ttu-id="b4a3e-158">Una vez que el usuario complete la instalación, el bot recibirá otro mensaje de invocación con `name = composeExtension/submitAction` y `value.data.msteams.justInTimeInstall = true` .</span><span class="sxs-lookup"><span data-stu-id="b4a3e-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="b4a3e-159">Este es un ejemplo de la invocación:</span><span class="sxs-lookup"><span data-stu-id="b4a3e-159">Here's an example of the invoke:</span></span>

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

<span data-ttu-id="b4a3e-160">Debe responder a esta invocación con la misma respuesta de tarea con la que habría respondido si el bot ya estaba instalado.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="b4a3e-161">Responder para enviar</span><span class="sxs-lookup"><span data-stu-id="b4a3e-161">Responding to submit</span></span>

<span data-ttu-id="b4a3e-162">Una vez que un usuario complete la introducción de su entrada, el bot recibirá un `composeExtension/submitAction` evento con el id del comando y los valores de parámetro establecidos.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="b4a3e-163">Estas son las diferentes respuestas esperadas a un `submitAction` .</span><span class="sxs-lookup"><span data-stu-id="b4a3e-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="b4a3e-164">Respuesta del módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="b4a3e-164">Task Module response</span></span>

<span data-ttu-id="b4a3e-165">Esto se utiliza cuando la extensión necesita encadenar cuadros de diálogo juntos para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="b4a3e-166">La respuesta es exactamente la misma que `fetchTask` se mencionó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="b4a3e-167">Respuesta de autenticación/configuración de extensión de composición</span><span class="sxs-lookup"><span data-stu-id="b4a3e-167">Compose extension auth/config response</span></span>

<span data-ttu-id="b4a3e-168">Esto se utiliza cuando su extensión necesita autenticar o configurar para continuar.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="b4a3e-169">Para obtener más información, consulte la [sección de autenticación](~/resources/messaging-extension-v3/search-extensions.md#authentication) en la sección de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-169">For more information, see [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="b4a3e-170">Respuesta del resultado de la extensión de composaje</span><span class="sxs-lookup"><span data-stu-id="b4a3e-170">Compose extension result response</span></span>

<span data-ttu-id="b4a3e-171">Esto se utiliza para insertar una tarjeta en el cuadro de composición como resultado de un comando.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="b4a3e-172">Es la misma respuesta que se usa en el comando de búsqueda, pero se limita a una tarjeta o un resultado en la matriz.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        },
    "attachments": [
      {  
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="b4a3e-173">Responder con un mensaje de tarjeta adaptable enviado desde un bot</span><span class="sxs-lookup"><span data-stu-id="b4a3e-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="b4a3e-174">También puede responder a la acción enviar insertando un mensaje con una tarjeta adaptable en el canal con un bot.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="b4a3e-175">El usuario podrá obtener una vista previa del mensaje antes de enviarlo y, potencialmente, editarlo o interactuar con él también.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="b4a3e-176">Esto puede ser muy útil en escenarios en los que necesita recopilar información de los usuarios antes de crear una respuesta de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="b4a3e-177">En el siguiente escenario se muestra cómo puede usar este flujo para configurar una encuesta sin incluir los pasos de configuración en el mensaje de canal.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="b4a3e-178">El usuario hace clic en la extensión de mensajería para desencadenar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="b4a3e-179">El usuario utiliza el módulo de tareas para configurar la encuesta.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="b4a3e-180">Después de enviar el módulo de tareas de configuración, la aplicación utiliza la información proporcionada en el módulo de tareas para crear una tarjeta adaptable y la envía como `botMessagePreview` respuesta al cliente.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="b4a3e-181">A continuación, el usuario puede obtener una vista previa del mensaje de tarjeta adaptable antes de que el bot lo inserte en el canal.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="b4a3e-182">Si el bot aún no es miembro del canal, al hacer clic en `Send` se agregará el bot.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="b4a3e-183">Interactuar con la tarjeta adaptable cambiará el mensaje antes de enviarlo.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="b4a3e-184">Una vez que el usuario haga clic en `Send` el bot publicará el mensaje en el canal.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="b4a3e-185">Para habilitar este flujo, el módulo de tareas debe responder como en el ejemplo siguiente, que presentará el mensaje de vista previa al usuario.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="b4a3e-186">El `activityPreview` must contendrá una `message` actividad con exactamente 1 accesorio de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

```json
{
  "composeExtension": {
    "type": "botMessagePreview",
    "activityPreview": {
      "type": "message",
      "attachments":  [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": << Card Payload >>
        }
      ]
    }
  }
}
```

<span data-ttu-id="b4a3e-187">La extensión del mensaje ahora tendrá que responder a dos nuevos tipos de interacciones `value.botMessagePreviewAction = "send"` y `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="b4a3e-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="b4a3e-188">A continuación se muestra un ejemplo del `value` objeto que tendrá que procesar:</span><span class="sxs-lookup"><span data-stu-id="b4a3e-188">Below is an example of the `value` object you will need to process:</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send" | "edit",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

<span data-ttu-id="b4a3e-189">Al responder a la `edit` solicitud debe responder con una respuesta con los valores `task` rellenados con la información que el usuario ya ha enviado.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="b4a3e-190">Al responder a la `send` solicitud, debe enviar un mensaje al canal que contiene la tarjeta adaptable finalizada.</span><span class="sxs-lookup"><span data-stu-id="b4a3e-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejs"></a>[<span data-ttu-id="b4a3e-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="b4a3e-191">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
teamChatConnector.onComposeExtensionSubmitAction((
    event: builder.IEvent,
    request: teamBuilder.IComposeExtensionActionCommandRequest,
    callback: (err: Error, result: any, statusCode: number) => void) => {
        let invokeValue = (<any> event).value;

        if (invokeValue.botMessagePreviewAction ) {
            let attachment = invokeValue.botActivityPreview[0].attachments[0];

            if (invokeValue.botMessagePreviewAction === 'send') {
                let msg = new builder.Message()
                    .address(event.address)
                    .addAttachment(attachment);
                teamChatConnector.send([msg.toMessage()],
                    (error) => {
                        if(error){
                            //TODO: Handle error and callback
                        }
                        else {
                            callback(null, null, 200);
                        }
                    }
                );
            }

            else if (invokeValue.botMessagePreviewAction === 'edit') {
              // Create the card and populate with user-inputted information
              let card = { ... }

              let taskResponse = {
                task: {
                  type: "continue",
                  value: {
                    title: "Card Preview",
                    card: {
                      contentType: 'application/vnd.microsoft.card.adaptive',
                      content: card
                    }
                  }
                }
              }
              callback(null, taskResponse, 200);
            }

        else {
            let attachment = {
                  //create adaptive card
                };
            let activity = new builder.Message().addAttachment(attachment).toMessage();
            let response = teamBuilder.ComposeExtensionResponse.messagePreview()
                .preview(activity)
                .toResponse();
            callback(null, response, 200);
        }
    });
```

# <a name="cnet"></a>[<span data-ttu-id="b4a3e-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b4a3e-192">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="b4a3e-193">En este ejemplo se muestra este flujo mediante el [SDK de Microsoft.Bot.Connector.Teams (v3).](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="b4a3e-193">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

```csharp
public class MessagesController : ApiController
{

    [BotAuthentication]
    public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
    {
        MicrosoftAppCredentials.TrustServiceUrl(activity.ServiceUrl, DateTime.MaxValue);
        ConnectorClient connectorClient = new ConnectorClient(
            new Uri(activity.ServiceUrl),
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppIdKey],
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppPasswordKey]);

        if (activity.Type == ActivityTypes.Invoke)
        {
            // Initial task module presented to the user
            if (activity.Name == "composeExtension/fetchTask")
            {
                string task = GetTaskModule();

                return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
            }
            else if (activity.Name == "composeExtension/submitAction")
            {
                dynamic activityValue = JObject.FromObject(activity.Value);
                string botMessagePreviewAction = activityValue["botMessagePreviewAction"];

                //This is the initial card response sent after the task module is submitted
                if (botMessagePreviewAction is null)
                {
                    string text = activityValue.data.cardMessage;

                    AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "This card will be inserted into the conversation by the bot.",
                        Size = AdaptiveTextSize.Large,
                        Wrap = true
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "The text below is what you provided."
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = text,
                    });

                    string cardJson = card.ToJson();

                    string cardMessage = $@"{{
                        'composeExtension': {{
                        'type': 'botMessagePreview',
                        'activityPreview': {{
                            'type': 'message',
                            'attachments': [{{
                                'contentType': 'application/vnd.microsoft.card.adaptive',
                                'content': {cardJson}
                            }}]
                        }}
                        }}
                    }}";

                    JObject res = JObject.Parse(cardMessage);
                    return Request.CreateResponse(HttpStatusCode.OK, res);

                }
                else
                {
                    //This is the "send the card to the channel" event
                    if (botMessagePreviewAction.Equals("send"))
                    {
                        string cardJson = JsonConvert.SerializeObject(activityValue.botActivityPreview[0].attachments[0].content);

                        AdaptiveCardParseResult cardResult = AdaptiveCard.FromJson(cardJson);
                        AdaptiveCard card = cardResult.Card;
                        Attachment cardAttachment = new Attachment
                        {
                            ContentType = AdaptiveCard.ContentType,
                            Content = card
                        };


                        Activity response = activity.CreateReply();
                        response.Attachments.Add(cardAttachment);

                        var result = await connectorClient.Conversations.SendToConversationAsync(response);
                    }
                    //This is fired if the user edits the card before sending it
                    else if (botMessagePreviewAction.Equals("edit"))
                    {
                        string task = GetTaskModule();

                        return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
                    }
                    else
                    {
                        return Request.CreateResponse(HttpStatusCode.NotImplemented);
                    }
                }
            }
        }

        return Request.CreateResponse(HttpStatusCode.NotImplemented);

    }

    private static string GetTaskModule()
    {
        AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Please enter the following information:",
            Size = AdaptiveTextSize.Large
        });
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Card Message:"
        });
        card.Body.Add(new AdaptiveTextInput()
        {
            Id = "cardMessage",
            Spacing = AdaptiveSpacing.None,
            Placeholder = "Card message goes here."
        });
        card.Actions.Add(new AdaptiveSubmitAction()
        {
            Title = "Submit"
        });

        string cardJson = card.ToJson();

        //Create the task module response
        string task = $@"{{
                            'task': {{
                                'type': 'continue',
                                'value': {{
                                    'card': {{
                                        'contentType': 'application/vnd.microsoft.card.adaptive',
                                        'content': {cardJson}
                                        }}
                                    }}
                                }}
                            }}";
        return task;
    }

}
```

## <a name="see-also"></a><span data-ttu-id="b4a3e-194">Vea también</span><span class="sxs-lookup"><span data-stu-id="b4a3e-194">See also</span></span>

[<span data-ttu-id="b4a3e-195">Muestras de Bot Framework</span><span class="sxs-lookup"><span data-stu-id="b4a3e-195">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)