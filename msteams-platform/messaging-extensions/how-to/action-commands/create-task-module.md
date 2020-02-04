---
title: Crear y enviar el módulo de tareas
author: clearab
description: Cómo controlar la acción de invocación inicial y responder con un módulo de tareas desde un comando de extensión de mensajería de acción
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f5f96e71517d45f52d17d2d70c583ec1eec3babd
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676027"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="d49ae-103">Crear y enviar el módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="d49ae-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="d49ae-104">Si no va a rellenar el módulo de tareas con los parámetros definidos en el manifiesto de la aplicación, deberá crear el módulo de tarea que se va a presentar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d49ae-104">If you are not populating your task module with parameters defined in your app manifest, you'll need to create the task module to be presented to your users.</span></span> <span data-ttu-id="d49ae-105">Puede usar tanto una tarjeta adaptable como una vista Web incrustada.</span><span class="sxs-lookup"><span data-stu-id="d49ae-105">You can use either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="d49ae-106">La solicitud de invocación inicial</span><span class="sxs-lookup"><span data-stu-id="d49ae-106">The initial invoke request</span></span>

<span data-ttu-id="d49ae-107">Con este método, el servicio recibirá `Activity` un objeto de `composeExtension/fetchTask`tipo y tendrá que responder con un `task` objeto que contenga la tarjeta adaptable o una dirección URL a la vista Web incrustada.</span><span class="sxs-lookup"><span data-stu-id="d49ae-107">Using this method you service will receive an `Activity` object of type `composeExtension/fetchTask`, and you'll need to respond with a `task` object containing either the adaptive card or a URL to the embedded web view.</span></span> <span data-ttu-id="d49ae-108">Además de las propiedades de actividad de bot estándar, la carga de invocación inicial contiene los siguientes metadatos de solicitud:</span><span class="sxs-lookup"><span data-stu-id="d49ae-108">In addition to the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="d49ae-109">Nombre de la propiedad</span><span class="sxs-lookup"><span data-stu-id="d49ae-109">Property name</span></span>|<span data-ttu-id="d49ae-110">Objetivo</span><span class="sxs-lookup"><span data-stu-id="d49ae-110">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="d49ae-111">Tipo de solicitud; debe ser `invoke`.</span><span class="sxs-lookup"><span data-stu-id="d49ae-111">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="d49ae-112">Tipo de comando que se emite para el servicio.</span><span class="sxs-lookup"><span data-stu-id="d49ae-112">Type of command that is issued to your service.</span></span> <span data-ttu-id="d49ae-113">Será `composeExtension/fetchTask`.</span><span class="sxs-lookup"><span data-stu-id="d49ae-113">Will be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="d49ae-114">IDENTIFICADOR del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="d49ae-114">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="d49ae-115">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="d49ae-115">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="d49ae-116">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="d49ae-116">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="d49ae-117">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d49ae-117">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="d49ae-118">IDENTIFICADOR de canal (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="d49ae-118">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="d49ae-119">IDENTIFICADOR del equipo (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="d49ae-119">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="d49ae-120">Contiene el identificador del comando que se ha invocado.</span><span class="sxs-lookup"><span data-stu-id="d49ae-120">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="d49ae-121">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="d49ae-121">The context that triggered the event.</span></span> <span data-ttu-id="d49ae-122">Será `compose`.</span><span class="sxs-lookup"><span data-stu-id="d49ae-122">Will be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="d49ae-123">El tema del cliente del usuario, útil para el formato de vista Web incrustado.</span><span class="sxs-lookup"><span data-stu-id="d49ae-123">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="d49ae-124">`default`Será `contrast` o `dark`.</span><span class="sxs-lookup"><span data-stu-id="d49ae-124">Will be `default`, `contrast` or `dark`.</span></span> |

### <a name="example-fetchtask-request"></a><span data-ttu-id="d49ae-125">Ejemplo de solicitud fetchTask</span><span class="sxs-lookup"><span data-stu-id="d49ae-125">Example fetchTask request</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="d49ae-126">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d49ae-126">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="d49ae-127">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="d49ae-127">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="d49ae-128">JSON</span><span class="sxs-lookup"><span data-stu-id="d49ae-128">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="d49ae-129">Solicitud de invocación inicial de un mensaje</span><span class="sxs-lookup"><span data-stu-id="d49ae-129">Initial invoke request from a message</span></span>

<span data-ttu-id="d49ae-130">Cuando se invoca el bot desde un mensaje en lugar de desde el área de redacción o la barra de `value` comandos, el objeto en la solicitud inicial contendrá los detalles del mensaje desde el que se invocó a la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="d49ae-130">When your bot is invoked from a message rather than the compose area or the command bar, the `value` object in the initial request will contain the details of the message your messaging extension was invoked from.</span></span> <span data-ttu-id="d49ae-131">A continuación se muestra un ejemplo de este objeto.</span><span class="sxs-lookup"><span data-stu-id="d49ae-131">An example of this object is below.</span></span> <span data-ttu-id="d49ae-132">Las `reactions` matrices `mentions` y son opcionales, y no estarán presentes si no hay reacciones o menciones en el mensaje original.</span><span class="sxs-lookup"><span data-stu-id="d49ae-132">The `reactions` and `mentions` arrays are optional, and will not be present if there are no reactions or mentions in the original message.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="d49ae-133">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d49ae-133">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="d49ae-134">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="d49ae-134">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="d49ae-135">JSON</span><span class="sxs-lookup"><span data-stu-id="d49ae-135">JSON</span></span>](#tab/json)

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
        "content": "This is the message the messaging extension was invoked from."
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

* * *

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="d49ae-136">Responder a la fetchTask</span><span class="sxs-lookup"><span data-stu-id="d49ae-136">Respond to the fetchTask</span></span>

<span data-ttu-id="d49ae-137">Responda a la solicitud de invocación `task` con un objeto que contenga un `taskInfo` objeto con la tarjeta adaptable o la dirección URL de la web, o bien un mensaje de cadena simple.</span><span class="sxs-lookup"><span data-stu-id="d49ae-137">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the adaptive card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="d49ae-138">Nombre de la propiedad</span><span class="sxs-lookup"><span data-stu-id="d49ae-138">Property name</span></span>|<span data-ttu-id="d49ae-139">Objetivo</span><span class="sxs-lookup"><span data-stu-id="d49ae-139">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="d49ae-140">Puede ser `continue` para presentar un formulario o `message` para un elemento emergente sencillo.</span><span class="sxs-lookup"><span data-stu-id="d49ae-140">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="d49ae-141">Un `taskInfo` objeto para un formulario o un `string` para un mensaje.</span><span class="sxs-lookup"><span data-stu-id="d49ae-141">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="d49ae-142">El esquema del objeto taskInfo es:</span><span class="sxs-lookup"><span data-stu-id="d49ae-142">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="d49ae-143">Nombre de la propiedad</span><span class="sxs-lookup"><span data-stu-id="d49ae-143">Property name</span></span>|<span data-ttu-id="d49ae-144">Objetivo</span><span class="sxs-lookup"><span data-stu-id="d49ae-144">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="d49ae-145">Título del módulo de tarea.</span><span class="sxs-lookup"><span data-stu-id="d49ae-145">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="d49ae-146">Puede ser un número entero (en píxeles), o `small`bien, `medium` `large`.</span><span class="sxs-lookup"><span data-stu-id="d49ae-146">Can be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="d49ae-147">Puede ser un número entero (en píxeles), o `small`bien, `medium` `large`.</span><span class="sxs-lookup"><span data-stu-id="d49ae-147">Can be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="d49ae-148">Tarjeta adaptable que define el formulario (si se usa uno).</span><span class="sxs-lookup"><span data-stu-id="d49ae-148">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="d49ae-149">Dirección URL que se va a abrir dentro del módulo de tarea como una vista Web incrustada.</span><span class="sxs-lookup"><span data-stu-id="d49ae-149">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="d49ae-150">Si un cliente no admite la característica de módulo de tareas, esta dirección URL se abre en una pestaña del explorador.</span><span class="sxs-lookup"><span data-stu-id="d49ae-150">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="with-an-adaptive-card"></a><span data-ttu-id="d49ae-151">Con una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="d49ae-151">With an adaptive card</span></span>

<span data-ttu-id="d49ae-152">Cuando use una tarjeta adaptable, deberá responder con un `task` objeto con el `value` objeto que contiene una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="d49ae-152">When using an adaptive card, you'll need to respond with a `task` object with the `value` object containing an adaptive card.</span></span>

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a><span data-ttu-id="d49ae-153">Respuesta de ejemplo fetchTask con una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="d49ae-153">Example fetchTask response with an adaptive card</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="d49ae-154">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d49ae-154">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="d49ae-155">En este ejemplo se usa el [paquete de NuGet AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards) además del SDK de bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d49ae-155">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="d49ae-156">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="d49ae-156">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="d49ae-157">JSON</span><span class="sxs-lookup"><span data-stu-id="d49ae-157">JSON</span></span>](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "card":
      {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ],
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json"
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a><span data-ttu-id="d49ae-158">Con una vista Web incrustada</span><span class="sxs-lookup"><span data-stu-id="d49ae-158">With an embedded web view</span></span>

<span data-ttu-id="d49ae-159">Cuando se usa una vista Web incrustada, es necesario responder con un `task` objeto con el `value` objeto que contiene la dirección URL al formulario web que se desea cargar.</span><span class="sxs-lookup"><span data-stu-id="d49ae-159">When using an embedded web view, you'll need to respond with a `task` object with the `value` object containing the URL to the web form you'd like to load.</span></span> <span data-ttu-id="d49ae-160">Los dominios de cualquier dirección URL que desee cargar deben incluirse en la `validDomains` matriz del manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d49ae-160">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="d49ae-161">Consulte la [documentación del módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md) para obtener información completa sobre cómo crear la vista Web incrustada.</span><span class="sxs-lookup"><span data-stu-id="d49ae-161">See the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md) for complete information on building your embedded web view.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="d49ae-162">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="d49ae-162">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="d49ae-163">JavaScript/node. js</span><span class="sxs-lookup"><span data-stu-id="d49ae-163">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="d49ae-164">JSON</span><span class="sxs-lookup"><span data-stu-id="d49ae-164">JSON</span></span>](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

## <a name="next-steps"></a><span data-ttu-id="d49ae-165">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="d49ae-165">Next steps</span></span>

<span data-ttu-id="d49ae-166">Si permite que los usuarios envíen una respuesta de vuelta desde el módulo de tareas, deberá controlar la acción de envío.</span><span class="sxs-lookup"><span data-stu-id="d49ae-166">If you allow your users to send a response back from the task module, you'll need to handle the submit action.</span></span>

* [<span data-ttu-id="d49ae-167">Crear y responder con un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="d49ae-167">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
