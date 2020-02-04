---
title: Iniciar acciones con extensiones de mensajería
description: Crear extensiones de mensajería basadas en acciones para permitir que los usuarios desencadenen servicios externos
keywords: búsqueda de extensiones de mensajería de Team Extensions
ms.openlocfilehash: 9b7d3bd53ba45d55e80f858a3c89be265c13482b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676000"
---
# <a name="initiate-actions-with-messaging-extensions"></a><span data-ttu-id="b6b7b-104">Iniciar acciones con extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="b6b7b-104">Initiate actions with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="b6b7b-105">Las extensiones de mensajería basadas en acciones permiten a los usuarios desencadenar acciones en servicios externos mientras se encuentran dentro de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-105">Action-based messaging extensions allow your users to trigger actions in external services while inside of Teams.</span></span>

![Ejemplo de tarjeta de extensión de mensajería](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="b6b7b-107">En las secciones siguientes se describe cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-107">The following sections describe how to do this.</span></span>

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a><span data-ttu-id="b6b7b-108">Tipo de acción extensiones de mensajes</span><span class="sxs-lookup"><span data-stu-id="b6b7b-108">Action type message extensions</span></span>

<span data-ttu-id="b6b7b-109">Para iniciar acciones desde una extensión de mensajería, `type` establezca el `action`parámetro en.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-109">To initiate actions from a  messaging extension set the `type` parameter to `action`.</span></span> <span data-ttu-id="b6b7b-110">A continuación se muestra un ejemplo de un manifiesto con una búsqueda y un comando crear.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-110">Below is an example of a manifest with a search and a create command.</span></span> <span data-ttu-id="b6b7b-111">Una sola extensión de mensajería puede tener hasta 10 comandos diferentes.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-111">A single messaging extension can have up to 10 different commands.</span></span> <span data-ttu-id="b6b7b-112">Esto puede incluir varios comandos de búsqueda y varios basados en acciones.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-112">This can include both multiple search and multiple action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="b6b7b-113">Ejemplo de manifiesto de aplicación completo</span><span class="sxs-lookup"><span data-stu-id="b6b7b-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

### <a name="initiate-actions-from-messages"></a><span data-ttu-id="b6b7b-114">Iniciar acciones desde mensajes</span><span class="sxs-lookup"><span data-stu-id="b6b7b-114">Initiate actions from messages</span></span>

<span data-ttu-id="b6b7b-115">Además de iniciar acciones desde el área de mensaje de redacción, también puede usar la extensión de mensajería para iniciar una acción desde un mensaje.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-115">In addition to initiating actions from the compose message area, you can also use your messaging extension to initiate an action from a message.</span></span> <span data-ttu-id="b6b7b-116">Esto le permitirá enviar el contenido del mensaje a su bot para su procesamiento y, opcionalmente, responder a ese mensaje con una respuesta mediante el método que se describe en [responder a envío](#responding-to-submit).</span><span class="sxs-lookup"><span data-stu-id="b6b7b-116">This will allow you to send the contents of the message to your bot for processing, and optionally reply to that message with a response using the method described in [Responding to submit](#responding-to-submit).</span></span> <span data-ttu-id="b6b7b-117">La respuesta se insertará como respuesta al mensaje que los usuarios pueden editar antes de enviarlo.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-117">The response will be inserted as a reply to the message that your users can edit before submitting.</span></span> <span data-ttu-id="b6b7b-118">Los usuarios pueden acceder a la extensión de mensajería desde `...` el menú de desbordamiento `Take action` y, a continuación, seleccionar como en la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-118">Your users can access your messaging extension from the overflow `...` menu and then selecting `Take action` as in the image below.</span></span>

![Ejemplo de inicio de una acción desde un mensaje](~/assets/images/compose-extensions/messageextensions_messageaction.png)

<span data-ttu-id="b6b7b-120">Para habilitar la extensión de mensajería para que funcione desde un mensaje, deberá agregar el `context` parámetro al `commands` objeto de la extensión de mensajería en el manifiesto de la aplicación, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-120">To enable your messaging extension to work from a message you'll need to add the `context` parameter to your messaging extension's `commands` object in your app manifest as in the example below.</span></span> <span data-ttu-id="b6b7b-121">Las cadenas válidas `context` para la `"message"`matriz `"commandBox"`son, `"compose"`y.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-121">Valid strings for the `context` array are `"message"`, `"commandBox"`, and `"compose"`.</span></span> <span data-ttu-id="b6b7b-122">El valor predeterminado es `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-122">The default value is `["compose", "commandBox"]`.</span></span> <span data-ttu-id="b6b7b-123">Consulte la sección [definir comandos](#define-commands) para obtener detalles completos del `context` parámetro.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-123">See the [define commands](#define-commands) section for complete details on the `context` parameter.</span></span>

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

<span data-ttu-id="b6b7b-124">A continuación se muestra un ejemplo `value` del objeto que contiene los detalles del mensaje que se enviará como `composeExtension` parte de la solicitud que se enviará a su bot.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-124">Below is an example of the `value` object containing the message details that will be sent as part of the `composeExtension` request be sent to your bot.</span></span>

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

### <a name="test-via-uploading"></a><span data-ttu-id="b6b7b-125">Prueba mediante carga</span><span class="sxs-lookup"><span data-stu-id="b6b7b-125">Test via uploading</span></span>

<span data-ttu-id="b6b7b-126">Puede probar la extensión de mensajería cargando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-126">You can test your messaging extension by uploading your app.</span></span> <span data-ttu-id="b6b7b-127">Consulte [cargar la aplicación en un equipo](~/concepts/deploy-and-publish/apps-upload.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-127">See [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md) for details.</span></span>

<span data-ttu-id="b6b7b-128">Para abrir la extensión de mensajería, navegue a cualquiera de sus chats o canales.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-128">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="b6b7b-129">Elija el botón **más opciones** (**&#8943;**) en el cuadro de redacción y elija su extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-129">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="collecting-input-from-users"></a><span data-ttu-id="b6b7b-130">Recopilar la entrada de los usuarios</span><span class="sxs-lookup"><span data-stu-id="b6b7b-130">Collecting input from users</span></span>

<span data-ttu-id="b6b7b-131">Hay tres formas de recopilar información de un usuario final en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-131">There are three ways to collect information from an end user in Teams.</span></span>

### <a name="static-parameter-list"></a><span data-ttu-id="b6b7b-132">Lista de parámetros estáticos</span><span class="sxs-lookup"><span data-stu-id="b6b7b-132">Static parameter list</span></span>

<span data-ttu-id="b6b7b-133">En este método, todo lo que debe hacer es definir una lista estática de parámetros en el manifiesto, tal como se muestra más arriba en el comando "crear tarea".</span><span class="sxs-lookup"><span data-stu-id="b6b7b-133">In this method, all you need to do is define a static list of parameters in the manifest as shown above in the "Create To Do" command.</span></span> <span data-ttu-id="b6b7b-134">Para usar este método, `fetchTask` Asegúrese de que `false` se establece en y de que define los parámetros en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-134">To use this method ensure `fetchTask` is set to `false` and that you define your parameters in the manifest.</span></span>

<span data-ttu-id="b6b7b-135">Cuando un usuario elige un comando con parámetros estáticos, Microsoft Teams generará un formulario en un módulo de tareas con los parámetros definidos en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-135">When a user chooses a command with static parameters, Teams will generate a form in a Task Module with the parameters defined in the manifest.</span></span> <span data-ttu-id="b6b7b-136">Al presionar enviar, `composeExtension/submitAction` se envía al bot.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-136">On hitting Submit a `composeExtension/submitAction` is sent to the bot.</span></span> <span data-ttu-id="b6b7b-137">Consulte el tema [respuesta a envío](#responding-to-submit) para obtener más información sobre el conjunto de respuestas esperado.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-137">See the topic [Responding to submit](#responding-to-submit) for more information on the expected set of responses.</span></span>

### <a name="dynamic-input-using-an-adaptive-card"></a><span data-ttu-id="b6b7b-138">Entrada dinámica con una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="b6b7b-138">Dynamic input using an adaptive card</span></span>

<span data-ttu-id="b6b7b-139">En este método, el servicio puede definir una tarjeta adaptable personalizada para recopilar la entrada del usuario final.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-139">In this method, your service can define a custom adaptive card to collect the end user input.</span></span> <span data-ttu-id="b6b7b-140">Para este enfoque, establezca el `fetchTask` parámetro `true` en en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-140">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span> <span data-ttu-id="b6b7b-141">Tenga en cuenta que si `fetchTask` establece `true` en cualquier parámetro estático definido para el comando, se omitirá.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-141">Note that if you set `fetchTask` to `true` any static parameters defined for the command will be ignored.</span></span>

<span data-ttu-id="b6b7b-142">En este método, el servicio recibirá `composeExtension/fetchTask` un evento y debe responder con una [respuesta del módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-142">In this method your service will receive a `composeExtension/fetchTask` event and needs to respond with an adaptive card based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="b6b7b-143">A continuación se muestra una respuesta de ejemplo con una tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="b6b7b-143">Below is an sample response with an adaptive card:</span></span>

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

<span data-ttu-id="b6b7b-144">El bot también puede responder con una respuesta de auth/config si el usuario necesita autenticar o configurar la extensión antes de obtener la entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-144">The bot can also respond with an auth/config response if the user needs to authenticate or configure the extension before getting the user input.</span></span>

### <a name="dynamic-input-using-a-web-view"></a><span data-ttu-id="b6b7b-145">Entrada dinámica con una vista Web</span><span class="sxs-lookup"><span data-stu-id="b6b7b-145">Dynamic input using a web view</span></span>

<span data-ttu-id="b6b7b-146">En este método, el servicio puede mostrar `<iframe>` un widget basado en para mostrar una interfaz de usuario personalizada y recopilar entradas de usuario.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-146">In this method your service can show an `<iframe>` based widget to show any custom UI and collect user input.</span></span> <span data-ttu-id="b6b7b-147">Para este enfoque, establezca el `fetchTask` parámetro `true` en en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-147">For this approach, set the `fetchTask` parameter to `true` in the manifest.</span></span>

<span data-ttu-id="b6b7b-148">Al igual que en el flujo de tarjeta adaptable, el servicio `fetchTask` enviará un evento y debe responder con una [respuesta del módulo de tarea](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)basada en URL.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-148">Just like in the adaptive card flow your service will be send a `fetchTask` event and needs to respond with a URL based [task module response](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object).</span></span> <span data-ttu-id="b6b7b-149">A continuación se muestra una respuesta de ejemplo con una tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="b6b7b-149">Below is an sample response with an Adaptive card:</span></span>

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="b6b7b-150">Solicitud para instalar el bot Conversation</span><span class="sxs-lookup"><span data-stu-id="b6b7b-150">Request to install your conversational bot</span></span>

<span data-ttu-id="b6b7b-151">Si la aplicación también contiene un bot Conversation, puede que sea necesario asegurarse de que el bot está instalado en la conversación antes de cargar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-151">If your app also contains a conversational bot, it may be necessary to ensure that your bot is installed in the conversation before loading your task module.</span></span> <span data-ttu-id="b6b7b-152">Esto puede ser útil en situaciones en las que necesita obtener contexto adicional para el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-152">This can be useful in situations where you need to get additional context for you task module.</span></span> <span data-ttu-id="b6b7b-153">Por ejemplo, puede que necesite recuperar la lista para rellenar un control de selector de personas o la lista de canales en un equipo.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-153">For example, you may need to fetch the roster to populate a people picker control, or the list of channels in a team.</span></span>

<span data-ttu-id="b6b7b-154">Para facilitar este flujo, cuando la extensión de mensajería recibe primero `composeExtension/fetchTask` la comprobación de la invocación para ver si el bot está instalado en el contexto actual (para ello, puede intentar la llamada obtener lista, por ejemplo).</span><span class="sxs-lookup"><span data-stu-id="b6b7b-154">To facilitate this flow, when your messaging extension first receives the `composeExtension/fetchTask` invoke check to see if your bot is installed in the current context (you could accomplish this by attempting the get roster call, for example).</span></span> <span data-ttu-id="b6b7b-155">Si el bot no está instalado, se devuelve una tarjeta adaptable con una acción que solicita al usuario que instale el bot. Consulte el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-155">If your bot is not installed, you return an Adaptive Card with an action that requests the user to install your bot See the example below.</span></span> <span data-ttu-id="b6b7b-156">Tenga en cuenta que esto requiere que el usuario tenga permiso para instalar aplicaciones en esa ubicación; Si no se pueden presentar con un mensaje que les pide que se ponga en contacto con el administrador.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-156">Note that this requires the user to have permission to install apps in that location; if they cannot they will be presented with a message asking them to contact their administrator.</span></span>

<span data-ttu-id="b6b7b-157">Este es un ejemplo de la respuesta:</span><span class="sxs-lookup"><span data-stu-id="b6b7b-157">Here's an example of the response:</span></span>

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

<span data-ttu-id="b6b7b-158">Una vez que el usuario completa la instalación, el bot recibirá otro mensaje de `name = composeExtension/submitAction`llamada con `value.data.msteams.justInTimeInstall = true`y.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-158">Once the user completes the installation, your bot will receive another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

<span data-ttu-id="b6b7b-159">A continuación, se muestra un ejemplo de Invoke:</span><span class="sxs-lookup"><span data-stu-id="b6b7b-159">Here's an example of the invoke:</span></span>

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

<span data-ttu-id="b6b7b-160">Debe responder a esta Invocación con la misma respuesta de tarea que habría respondido si el bot ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-160">You should respond to this invoke with the same task response you would have responded with if the bot was already installed.</span></span>

## <a name="responding-to-submit"></a><span data-ttu-id="b6b7b-161">Responder al envío</span><span class="sxs-lookup"><span data-stu-id="b6b7b-161">Responding to submit</span></span>

<span data-ttu-id="b6b7b-162">Una vez que un usuario termina de escribir su entrada, el bot `composeExtension/submitAction` recibirá un evento con el identificador de comando y los valores de parámetro establecidos.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-162">Once a user completes entering their input your bot will receive a `composeExtension/submitAction` event with the command id and parameter values set.</span></span>

<span data-ttu-id="b6b7b-163">Estas son las diferentes respuestas esperadas a `submitAction`un.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-163">These are the different expected responses to a `submitAction`.</span></span>

### <a name="task-module-response"></a><span data-ttu-id="b6b7b-164">Respuesta del módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="b6b7b-164">Task Module response</span></span>

<span data-ttu-id="b6b7b-165">Se usa cuando la extensión tiene que encadenar cuadros de diálogo juntos para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-165">This is used when your extension needs to chain dialogs together to get more information.</span></span> <span data-ttu-id="b6b7b-166">La respuesta es exactamente la misma que `fetchTask` se mencionó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-166">The response is exactly the same as `fetchTask` mentioned earlier.</span></span>

### <a name="compose-extension-authconfig-response"></a><span data-ttu-id="b6b7b-167">Escribir respuesta de autenticación/configuración de extensión</span><span class="sxs-lookup"><span data-stu-id="b6b7b-167">Compose extension auth/config response</span></span>

<span data-ttu-id="b6b7b-168">Se usa cuando la extensión debe ser autenticada o configurada para continuar.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-168">This is used when your extension needs to either authenticate or configure in order to continue.</span></span> <span data-ttu-id="b6b7b-169">Consulte la [sección autenticación](~/resources/messaging-extension-v3/search-extensions.md#authentication) en la sección Buscar para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-169">See [authentication section](~/resources/messaging-extension-v3/search-extensions.md#authentication) in the search section for more details.</span></span>

### <a name="compose-extension-result-response"></a><span data-ttu-id="b6b7b-170">Respuesta de resultado de la extensión de redacción</span><span class="sxs-lookup"><span data-stu-id="b6b7b-170">Compose extension result response</span></span>

<span data-ttu-id="b6b7b-171">Esto se usa para insertar una tarjeta en el cuadro de redacción como resultado de un comando.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-171">This used to insert a card into the compose box as a result of a the command.</span></span> <span data-ttu-id="b6b7b-172">Se trata de la misma respuesta que se usa en el comando de búsqueda, pero está limitada a una tarjeta o a un resultado de la matriz.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-172">It's the same response that's used in the search command, but it's limited to one card or one result in the array.</span></span>

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
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a><span data-ttu-id="b6b7b-173">Responder con un mensaje de tarjeta adaptable enviado desde un bot</span><span class="sxs-lookup"><span data-stu-id="b6b7b-173">Respond with an adaptive card message sent from a bot</span></span>

<span data-ttu-id="b6b7b-174">También puede responder a la acción de envío Insertando un mensaje con una tarjeta adaptable en el canal con un bot.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-174">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="b6b7b-175">El usuario podrá obtener una vista previa del mensaje antes de enviarlo y, potencialmente, editarlo o interactuar con él.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-175">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="b6b7b-176">Esto puede ser muy útil en escenarios en los que es necesario recopilar información de los usuarios antes de crear una respuesta de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-176">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response.</span></span> <span data-ttu-id="b6b7b-177">El siguiente escenario muestra cómo se puede usar este flujo para configurar un sondeo sin incluir los pasos de configuración en el mensaje de canal.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-177">The following scenario shows how you can use this flow to configure a poll without including the configuration steps in the channel message.</span></span>

1. <span data-ttu-id="b6b7b-178">El usuario hace clic en la extensión de mensajería para desencadenar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-178">The user clicks the messaging extension to trigger the task module.</span></span>
1. <span data-ttu-id="b6b7b-179">El usuario usa el módulo de tareas para configurar el sondeo.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-179">The user uses the task module to configure the poll.</span></span>
1. <span data-ttu-id="b6b7b-180">Después de enviar el módulo de tareas de configuración, la aplicación usa la información proporcionada en el módulo de tareas para diseñar una tarjeta adaptable `botMessagePreview` y enviarla como respuesta al cliente.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-180">After submitting the configuration task module the app uses the information provided in the task module to craft an adaptive card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="b6b7b-181">A continuación, el usuario puede obtener una vista previa del mensaje de tarjeta adaptable antes de que el bot lo inserte en el canal.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-181">The user can then preview the adaptive card message before the bot will inserts it into the channel.</span></span> <span data-ttu-id="b6b7b-182">Si el bot todavía no es miembro del canal, al hacer clic `Send` se agregará el bot.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-182">If the bot is not already a member of the channel, clicking `Send` will add the bot.</span></span>
1. <span data-ttu-id="b6b7b-183">La interacción con la tarjeta adaptable modificará el mensaje antes de enviarlo.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-183">Interacting with the adaptive card will change the message before sending it.</span></span>
1. <span data-ttu-id="b6b7b-184">Una vez que el usuario `Send` hace clic en el bot, el mensaje se enviará al canal.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-184">Once the user clicks `Send` the bot will post the message to the channel.</span></span>

<span data-ttu-id="b6b7b-185">Para habilitar este flujo, el módulo de tareas debe responder como se muestra en el ejemplo siguiente, que presentará el mensaje de vista previa al usuario.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-185">To enable this flow your task module should respond as in the example below, which will present the preview message to the user.</span></span>

>[!Note]
><span data-ttu-id="b6b7b-186">El `activityPreview` debe contener una `message` actividad con exactamente 1 archivo adjunto de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-186">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span>

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

<span data-ttu-id="b6b7b-187">La extensión de mensajes ahora tendrá que responder a dos nuevos tipos de interacciones `value.botMessagePreviewAction = "send"` y `value.botMessagePreviewAction = "edit"`.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-187">Your message extension will now need to respond to two new types of interactions, `value.botMessagePreviewAction = "send"` and `value.botMessagePreviewAction = "edit"`.</span></span> <span data-ttu-id="b6b7b-188">A continuación se muestra un ejemplo `value` del objeto que tendrá que procesar:</span><span class="sxs-lookup"><span data-stu-id="b6b7b-188">Below is an example of the `value` object you will need to process:</span></span>

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

<span data-ttu-id="b6b7b-189">Al responder a la `edit` solicitud, debe responder con una `task` respuesta con los valores que se han rellenado con la información que el usuario ya ha enviado.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-189">When responding to the `edit` request you should respond with a `task` response with the values populated with the information the user has already submitted.</span></span> <span data-ttu-id="b6b7b-190">Al responder a la `send` solicitud, debe enviar un mensaje al canal que contiene la tarjeta adaptable que ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="b6b7b-190">When responding to the `send` request you should send a message to the channel containing the finalized adaptive card.</span></span>

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="b6b7b-191">TypeScript/node. js</span><span class="sxs-lookup"><span data-stu-id="b6b7b-191">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="b6b7b-192">En el ejemplo siguiente, se muestra cómo hacerlo con el [SDK de Team. js para Teams Builder](https://www.npmjs.com/package/botbuilder-teams).</span><span class="sxs-lookup"><span data-stu-id="b6b7b-192">The example below shows how to do this using the [Node.js Teams Bot Builder SDK](https://www.npmjs.com/package/botbuilder-teams).</span></span>

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

# <a name="cnettabdotnet"></a>[<span data-ttu-id="b6b7b-193">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b6b7b-193">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="b6b7b-194">En este ejemplo se muestra este flujo mediante el [SDK de Microsoft. bot. Connector. Teams (V3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span><span class="sxs-lookup"><span data-stu-id="b6b7b-194">This sample shows this flow using the [Microsoft.Bot.Connector.Teams SDK (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).</span></span>

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
