---
title: Envío de mensajes a conectores y webhooks
description: Describe cómo usar los Conectores de Office 365 en Microsoft Teams
localization_priority: Priority
keywords: teams o365 conector
ms.openlocfilehash: 55cfbc870ed8b04a8fbac58fdfa9b40110410ad7
ms.sourcegitcommit: 5e1300d6f4f2ea23beb3cdbbf4bd46999eef4e87
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/15/2021
ms.locfileid: "49875017"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a><span data-ttu-id="c7c6b-104">Envío de mensajes a conectores y webhooks</span><span class="sxs-lookup"><span data-stu-id="c7c6b-104">Sending messages to connectors and webhooks</span></span>

<span data-ttu-id="c7c6b-105">Para enviar un mensaje a través del conector de Office 365 o el webhook de entrada, debe publicar una carga JSON en la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-105">To send a message through your Office 365 Connector or incoming webhook, you post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="c7c6b-106">Por lo general, esta carga será una [tarjeta de conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="c7c6b-106">Typically this payload will be in the form of an [Office 365 Connector Card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="c7c6b-107">También puede usar este JSON para crear tarjetas que contengan entradas enriquecidas, como entrada de texto, selección múltiple o selección de una fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-107">You can also use this JSON to create cards containing rich inputs, such as text entry, multi-select, or picking a date and time.</span></span> <span data-ttu-id="c7c6b-108">El código que genera la tarjeta y publica en la dirección URL de webhook se puede ejecutar en cualquier servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-108">The code that generates the card and posts to the webhook URL can be running on any hosted service.</span></span> <span data-ttu-id="c7c6b-109">Estas tarjetas se definen como parte de mensajes accionables, y también se admiten en las [tarjetas](~/task-modules-and-cards/what-are-cards.md) que se usan en los bots de Teams y las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-109">These cards are defined as part of actionable messages, and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md) used in Teams bots and Messaging extensions.</span></span>

### <a name="example-connector-message"></a><span data-ttu-id="c7c6b-110">Ejemplo de mensaje de conector</span><span class="sxs-lookup"><span data-stu-id="c7c6b-110">Example connector message</span></span>

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "Larry Bryant created a new task",
        "activitySubtitle": "On Project Tango",
        "activityImage": "https://teamsnodesample.azurewebsites.net/static/img/image5.png",
        "facts": [{
            "name": "Assigned to",
            "value": "Unassigned"
        }, {
            "name": "Due date",
            "value": "Mon May 01 2017 17:07:18 GMT-0700 (Pacific Daylight Time)"
        }, {
            "name": "Status",
            "value": "Not started"
        }],
        "markdown": true
    }],
    "potentialAction": [{
        "@type": "ActionCard",
        "name": "Add a comment",
        "inputs": [{
            "@type": "TextInput",
            "id": "comment",
            "isMultiline": false,
            "title": "Add a comment here for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Add comment",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Set due date",
        "inputs": [{
            "@type": "DateInput",
            "id": "dueDate",
            "title": "Enter a due date for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "OpenUri",
        "name": "Learn More",
        "targets": [{
            "os": "default",
            "uri": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Change status",
        "inputs": [{
            "@type": "MultichoiceInput",
            "id": "list",
            "title": "Select a status",
            "isMultiSelect": "false",
            "choices": [{
                "display": "In Progress",
                "value": "1"
            }, {
                "display": "Active",
                "value": "2"
            }, {
                "display": "Closed",
                "value": "3"
            }]
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }]
}
```

<span data-ttu-id="c7c6b-111">Este mensaje produce la siguiente tarjeta en el canal.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-111">This message produces the following card in the channel.</span></span>

![Captura de pantalla de una tarjeta de conector](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a><span data-ttu-id="c7c6b-113">Creación de mensajes que requieren acción</span><span class="sxs-lookup"><span data-stu-id="c7c6b-113">Creating actionable messages</span></span>

<span data-ttu-id="c7c6b-114">En el ejemplo de la sección anterior se incluyen tres botones visibles en la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-114">The example in the preceding section includes three visible buttons on the card.</span></span> <span data-ttu-id="c7c6b-115">Cada botón se define en la propiedad `potentialAction` del mensaje mediante acciones `ActionCard`, cada una de las cuales contiene un tipo de entrada: un campo de texto, un selector de fecha o una lista de opciones múltiples.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-115">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each containing an input type: a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="c7c6b-116">Cada acción `ActionCard` tiene asociada una acción, por ejemplo `HttpPOST`.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-116">Each `ActionCard` action has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="c7c6b-117">Las tarjetas de conector admiten tres tipos de acciones:</span><span class="sxs-lookup"><span data-stu-id="c7c6b-117">Connector cards support three types of actions:</span></span>

- <span data-ttu-id="c7c6b-118">`ActionCard` Presenta uno o varios tipos de entrada y acciones asociadas.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-118">`ActionCard` Presents one or more input types and associated actions</span></span>
- <span data-ttu-id="c7c6b-119">`HttpPOST` Envía una solicitud POST a una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-119">`HttpPOST` Sends a POST request to a URL</span></span>
- <span data-ttu-id="c7c6b-120">`OpenUri` Abre un identificador URI en un explorador o aplicación independiente. De manera opcional, marca como destino diferentes URI en función de los sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-120">`OpenUri` Opens a URI in a separate browser or app; optionally targets different URIs based on operating systems</span></span>

<span data-ttu-id="c7c6b-121">La acción `ActionCard` admite tres tipos de entrada:</span><span class="sxs-lookup"><span data-stu-id="c7c6b-121">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="c7c6b-122">`TextInput` Un campo de texto de una sola línea o multilínea con un límite de longitud opcional.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-122">`TextInput` A single-line or multiline text field with an optional length limit</span></span>
- <span data-ttu-id="c7c6b-123">`DateInput` Un selector de fecha con un selector de hora opcional.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-123">`DateInput` A date selector with an optional time selector</span></span>
- <span data-ttu-id="c7c6b-124">`MultichoiceInput` Una lista de opciones enumeradas que ofrece una sola selección o selecciones múltiples.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-124">`MultichoiceInput` A enumerated list of choices offering either a single selection or multiple selections</span></span>

<span data-ttu-id="c7c6b-125">`MultichoiceInput` admite una propiedad `style` que controla si inicialmente la lista se muestra totalmente expandida.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-125">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="c7c6b-126">El valor predeterminado de `style` depende del valor de `isMultiSelect`.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-126">The default value of `style` depends on the value of `isMultiSelect`.</span></span>

| `isMultiSelect` | <span data-ttu-id="c7c6b-127">`style` predeterminado</span><span class="sxs-lookup"><span data-stu-id="c7c6b-127">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="c7c6b-128">`false` o no especificado</span><span class="sxs-lookup"><span data-stu-id="c7c6b-128">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="c7c6b-129">Si quiere que se muestre inicialmente una lista de selección múltiple en el estilo compacto, debe especificar `"isMultiSelect": true` y `"style": true`.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-129">If you want a multiselect list initially displayed in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

> [!NOTE]
> <span data-ttu-id="c7c6b-130">Especificar `compact` para la propiedad `style` en Microsoft Teams es igual que especificar `normal` para la propiedad `style` en Microsoft Outlook.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-130">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>

<span data-ttu-id="c7c6b-131">Para obtener más información sobre las acciones de la tarjeta conector, consulte **[Acciones](/outlook/actionable-messages/card-reference#actions)** en la referencia de la tarjeta de mensaje accionable.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-131">For all other details about Connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="setting-up-a-custom-incoming-webhook"></a><span data-ttu-id="c7c6b-132">Configurar un webhook de entrada personalizado</span><span class="sxs-lookup"><span data-stu-id="c7c6b-132">Setting up a custom incoming webhook</span></span>

<span data-ttu-id="c7c6b-133">Siga estos pasos para ver cómo se envía una tarjeta simple a un conector.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-133">Follow these steps to see how to send a simple card to a Connector.</span></span>

1. <span data-ttu-id="c7c6b-134">En Microsoft Teams, elija **Más opciones** (**&#8943;**) junto al nombre del canal y elija **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-134">In Microsoft Teams, choose **More options** (**&#8943;**) next to the channel name and then choose **Connectors**.</span></span>
2. <span data-ttu-id="c7c6b-135">Desplácese por la lista de conectores hasta **Webhook entrante** y elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-135">Scroll through the list of Connectors to **Incoming Webhook**, and choose **Add**.</span></span>
3. <span data-ttu-id="c7c6b-136">Escriba un nombre para el webhook, cargue una imagen para asociarla a los datos del webhook y elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-136">Enter a name for the webhook, upload an image to associate with data from the webhook, and choose **Create**.</span></span>
4. <span data-ttu-id="c7c6b-137">Copie el webhook en el portapapeles y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-137">Copy the webhook to the clipboard and save it.</span></span> <span data-ttu-id="c7c6b-138">Necesitará la dirección URL del webhook para enviar información a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-138">You'll need the webhook URL for sending information to Microsoft Teams.</span></span>
5. <span data-ttu-id="c7c6b-139">Seleccione **Listo**.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-139">Choose **Done**.</span></span>

### <a name="post-a-message-to-the-webhook-using-curl"></a><span data-ttu-id="c7c6b-140">Publicar un mensaje en webhook con cURL</span><span class="sxs-lookup"><span data-stu-id="c7c6b-140">Post a message to the webhook using cURL</span></span>

<span data-ttu-id="c7c6b-141">Los siguientes pasos usan [cURL](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="c7c6b-141">The following steps use [cURL](https://curl.haxx.se/).</span></span> <span data-ttu-id="c7c6b-142">Damos por sentado que lo tiene instalado y está familiarizado con su uso básico.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-142">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="c7c6b-143">Desde la línea de comandos, escriba el siguiente comando cURL:</span><span class="sxs-lookup"><span data-stu-id="c7c6b-143">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="c7c6b-144">Si el envío se realiza correctamente, debería ver un resultado de salida **1** por `curl`.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-144">If the POST succeeds, you should see a simple **1** output by `curl`.</span></span>
3. <span data-ttu-id="c7c6b-145">Compruebe el cliente de Microsoft Team.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-145">Check the Microsoft Team client.</span></span> <span data-ttu-id="c7c6b-146">Debería ver la nueva tarjeta publicada en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-146">You should see the new card posted to the team.</span></span>

### <a name="post-a-message-to-the-webhook-using-powershell"></a><span data-ttu-id="c7c6b-147">Publicar un mensaje en webhook con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7c6b-147">Post a message to the webhook using PowerShell</span></span>

<span data-ttu-id="c7c6b-148">Los siguientes pasos usan PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-148">The following steps use PowerShell.</span></span> <span data-ttu-id="c7c6b-149">Damos por sentado que lo tiene instalado y está familiarizado con su uso básico.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-149">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="c7c6b-150">Desde el símbolo del sistema de PowerShell, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7c6b-150">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="c7c6b-151">Si el envío se realiza correctamente, debería ver un resultado de salida **1** por `Invoke-RestMethod`.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-151">If the POST succeeds, you should see a simple **1** output by `Invoke-RestMethod`.</span></span>
3. <span data-ttu-id="c7c6b-152">Compruebe el canal de Microsoft Teams asociado a la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-152">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="c7c6b-153">Debería ver la nueva tarjeta publicada en el canal.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-153">You should see the new card posted to the channel.</span></span>

- <span data-ttu-id="c7c6b-154">[Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="c7c6b-154">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="c7c6b-155">Modifique la parte `icons` del manifiesto para hacer referencia a los nombres de archivo de los iconos en lugar de a las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-155">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="c7c6b-156">El archivo manifest.json siguiente contiene los elementos básicos necesarios para probar y enviar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-156">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="c7c6b-157">Reemplace `id` y `connectorId` en el ejemplo siguiente con el GUID del conector.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-157">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="c7c6b-158">Ejemplo de manifest.json con conector</span><span class="sxs-lookup"><span data-stu-id="c7c6b-158">Example manifest.json with connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="c7c6b-159">Enviar tarjetas adaptables con un webhook entrante</span><span class="sxs-lookup"><span data-stu-id="c7c6b-159">Send adaptive cards using an incoming webhook</span></span>

> [!NOTE]
>
> <span data-ttu-id="c7c6b-160">✔ Todos los elementos de esquema de tarjetas adaptables nativas, excepto `Action.Submit`, son completamente compatibles.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-160">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="c7c6b-161">✔ Las acciones compatibles son [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), y [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span><span class="sxs-lookup"><span data-stu-id="c7c6b-161">✔ The supported Actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

### <a name="the-flow-for-sending-adaptive-cards-via-an-incoming-webhook-is-as-follows"></a><span data-ttu-id="c7c6b-162">El flujo para el envío de [tarjetas adaptables](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) mediante un webhook entrante es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7c6b-162">The flow for sending [adaptive cards](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) via an incoming webhook is as follows:</span></span>

<span data-ttu-id="c7c6b-163">**1.** [Configurar un webhook personalizado](#setting-up-a-custom-incoming-webhook) en Teams.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-163">**1.** [Setup a custom webhook](#setting-up-a-custom-incoming-webhook) in Teams.</span></span></br></br>
<span data-ttu-id="c7c6b-164">**2.** Crear el archivo JSON de la tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="c7c6b-164">**2.** Create your adaptive card JSON file:</span></span>

```json
{
   "type":"message",
   "attachments":[
      {
         "contentType":"application/vnd.microsoft.card.adaptive",
         "contentUrl":null,
         "content":{
            "$schema":"http://adaptivecards.io/schemas/adaptive-card.json",
            "type":"AdaptiveCard",
            "version":"1.2",
            "body":[
                {
                "type": "TextBlock",
                "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)",
                }
            ]
         }
      }
   ]
}
```

> [!div class="checklist"]
>
> - <span data-ttu-id="c7c6b-165">El campo `"type"` debe ser `"message"`.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-165">The `"type"` field must be `"message"`.</span></span>
> - <span data-ttu-id="c7c6b-166">La matriz `"attachments"` contiene un conjunto de objetos de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-166">The `"attachments"` array contains a set of card objects.</span></span>
> - <span data-ttu-id="c7c6b-167">El campo `"contentType"` debe establecerse en tipo de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-167">The `"contentType"` field must be set to adaptive card type.</span></span>
> - <span data-ttu-id="c7c6b-168">El objeto `"content"` es la tarjeta con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-168">The `"content"` object is the card formatted in JSON.</span></span>

<span data-ttu-id="c7c6b-169">**3.** Probar la tarjeta adaptable con Postman</span><span class="sxs-lookup"><span data-stu-id="c7c6b-169">**3.** Test your adaptive card with Postman</span></span>

<span data-ttu-id="c7c6b-170">Para probar la tarjeta adaptativa, puede usar [Postman](https://www.postman.com) para enviar una solicitud POST a la dirección URL que creó cuando configuró el webhook entrante.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-170">You can test your adaptive card using [Postman](https://www.postman.com) to send a POST request to the URL that you created when you setup your incoming webhook.</span></span> <span data-ttu-id="c7c6b-171">Pegue el archivo JSON en el cuerpo de la solicitud y vea el mensaje de la tarjeta adaptable en Teams.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-171">Paste your JSON file in the body of the request and view your adaptive card message in Teams.</span></span>

>[!TIP]
> <span data-ttu-id="c7c6b-172">Puede usar el código de tarjeta adaptable [Ejemplos y plantillas](https://adaptivecards.io/samples) para el cuerpo de la solicitud Post de prueba.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-172">You can use adaptive card code [Samples and Templates](https://adaptivecards.io/samples) for the body of your test Post request.</span></span>

## <a name="testing-your-connector"></a><span data-ttu-id="c7c6b-173">Probar el conector</span><span class="sxs-lookup"><span data-stu-id="c7c6b-173">Testing your connector</span></span>

<span data-ttu-id="c7c6b-174">Para probar el conector, cárguelo en un equipo igual que lo haría con cualquier otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-174">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="c7c6b-175">Puede crear un paquete .zip mediante el archivo de manifiesto desde el Panel del programador de conectores (modificado como se indica en la sección anterior) y los dos archivos de icono.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-175">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="c7c6b-176">Después de cargar la aplicación, abra la lista Conectores desde cualquier canal.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-176">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="c7c6b-177">Desplácese hasta la parte inferior para ver la aplicación en la sección **Cargada**.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-177">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![Captura de pantalla de la sección cargada en el cuadro de diálogo Conector](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="c7c6b-179">Ahora, puede iniciar la experiencia de configuración.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-179">You can now launch the configuration experience.</span></span> <span data-ttu-id="c7c6b-180">Tenga en cuenta que este flujo se produce completamente en Microsoft Teams a través de una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-180">Be aware that this flow occurs entirely within Microsoft Teams through a pop-up window.</span></span> <span data-ttu-id="c7c6b-181">Actualmente, este comportamiento es distinto de la experiencia de configuración en Conectores que hemos creado; estamos trabajando para unificar las experiencias.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-181">Currently, this behavior differs from the configuration experience in Connectors that we created; we are working on unifying the experiences.</span></span>

<span data-ttu-id="c7c6b-182">Para comprobar que una acción `HttpPOST` está funcionando correctamente, utilice el [webhook entrante personalizado](#setting-up-a-custom-incoming-webhook).</span><span class="sxs-lookup"><span data-stu-id="c7c6b-182">To verify that an `HttpPOST` action is working correctly, use your [custom incoming webhook](#setting-up-a-custom-incoming-webhook).</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="c7c6b-183">Limitación de velocidad para conectores</span><span class="sxs-lookup"><span data-stu-id="c7c6b-183">Rate limiting for connectors</span></span>

<span data-ttu-id="c7c6b-184">Los límites de velocidad de la aplicación controlan el tráfico que puede generar un conector o un webhook entrante en un canal.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-184">Application rate limits control the traffic that a connector or an incoming webhook is allowed to generate on a channel.</span></span> <span data-ttu-id="c7c6b-185">Teams realiza un seguimiento de las solicitudes a través de una ventana de velocidad fija y un contador incremental medido en segundos.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-185">Teams tracks requests via a fixed-rate window and incremental counter measured in seconds.</span></span>  <span data-ttu-id="c7c6b-186">Si se hacen demasiadas solicitudes, se limita la conexión de cliente hasta que se actualice la ventana, es decir, mientras dure la velocidad fija.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-186">If too many requests are made, the client connection will be throttled until the window refreshes, i.e., for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="c7c6b-187">**Umbrales de transacciones por segundo**</span><span class="sxs-lookup"><span data-stu-id="c7c6b-187">**Transactions per second thresholds**</span></span>

| <span data-ttu-id="c7c6b-188">Tiempo (segundos)</span><span class="sxs-lookup"><span data-stu-id="c7c6b-188">Time (seconds)</span></span>  | <span data-ttu-id="c7c6b-189">Número máximo de solicitudes permitidas</span><span class="sxs-lookup"><span data-stu-id="c7c6b-189">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="c7c6b-190">1</span><span class="sxs-lookup"><span data-stu-id="c7c6b-190">1</span></span>   | <span data-ttu-id="c7c6b-191">4</span><span class="sxs-lookup"><span data-stu-id="c7c6b-191">4</span></span>  |  
| <span data-ttu-id="c7c6b-192">30</span><span class="sxs-lookup"><span data-stu-id="c7c6b-192">30</span></span>   | <span data-ttu-id="c7c6b-193">60</span><span class="sxs-lookup"><span data-stu-id="c7c6b-193">60</span></span>  |  
| <span data-ttu-id="c7c6b-194">3600</span><span class="sxs-lookup"><span data-stu-id="c7c6b-194">3600</span></span>   | <span data-ttu-id="c7c6b-195">100</span><span class="sxs-lookup"><span data-stu-id="c7c6b-195">100</span></span>  |
| <span data-ttu-id="c7c6b-196">7200</span><span class="sxs-lookup"><span data-stu-id="c7c6b-196">7200</span></span> | <span data-ttu-id="c7c6b-197">150</span><span class="sxs-lookup"><span data-stu-id="c7c6b-197">150</span></span>  |
| <span data-ttu-id="c7c6b-198">86400</span><span class="sxs-lookup"><span data-stu-id="c7c6b-198">86400</span></span>  | <span data-ttu-id="c7c6b-199">1800</span><span class="sxs-lookup"><span data-stu-id="c7c6b-199">1800</span></span>  |

<span data-ttu-id="c7c6b-200">*Consulte también* [Conectores de Office 365: Microsoft Teams](https://docs.microsoft.com/connectors/teams/)</span><span class="sxs-lookup"><span data-stu-id="c7c6b-200">*See also* [Office 365 Connectors — Microsoft Teams](https://docs.microsoft.com/connectors/teams/)</span></span>

<span data-ttu-id="c7c6b-201">Una [lógica de reintento con interrupción exponencial](/azure/architecture/patterns/retry) como la que se muestra a continuación mitigaría la restricción de velocidad en casos en que las solicitudes superen los límites en un segundo.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-201">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) like below would mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="c7c6b-202">Siga los [procedimientos recomendados](../../bots/how-to/rate-limit.md#best-practices) para evitar alcanzar los límites de velocidad.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-202">Please follow [best practices](../../bots/how-to/rate-limit.md#best-practices) to avoid hitting the rate limits.</span></span>

```csharp
// Please note that response body needs to be extracted and read 
// as Connectors do not throw 429s
try
{
    // Perform Connector POST operation     
    var httpResponseMessage = await _client.PostAsync(IncomingWebhookUrl, new StringContent(content));
    // Read response content
    var responseContent = await httpResponseMessage.Content.ReadAsStringAsync();
    if (responseContent.Contains("Microsoft Teams endpoint returned HTTP error 429")) 
    {
        // initiate retry logic
    }
}
```
 
<span data-ttu-id="c7c6b-203">Estos límites tienen el propósito de reducir el correo no deseado en un canal con un conector y garantizan una experiencia óptima para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="c7c6b-203">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to your end users.</span></span>
