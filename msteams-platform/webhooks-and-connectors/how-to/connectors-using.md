---
title: Envío de mensajes a conectores y webhooks
description: Describe cómo usar los Conectores de Office 365 en Microsoft Teams
ms.topic: how-to
localization_priority: Normal
keywords: teams o365 conector
ms.openlocfilehash: f9546b3550b3c53452c5856cfb87fdc6d71f2ad0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566526"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a><span data-ttu-id="ede95-104">Envío de mensajes a conectores y webhooks</span><span class="sxs-lookup"><span data-stu-id="ede95-104">Sending messages to connectors and webhooks</span></span>

<span data-ttu-id="ede95-105">Para enviar un mensaje a través del conector de Office 365 o el webhook de entrada, debe publicar una carga JSON en la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="ede95-105">To send a message through your Office 365 Connector or incoming webhook, you post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="ede95-106">Por lo general, esta carga será una [tarjeta de conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="ede95-106">Typically this payload will be in the form of an [Office 365 Connector Card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="ede95-107">También puede usar este JSON para crear tarjetas que contengan entradas enriquecidas, como entrada de texto, selección múltiple o selección de una fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="ede95-107">You can also use this JSON to create cards containing rich inputs, such as text entry, multi-select, or picking a date and time.</span></span> <span data-ttu-id="ede95-108">El código que genera la tarjeta y publica en la dirección URL de webhook se puede ejecutar en cualquier servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="ede95-108">The code that generates the card and posts to the webhook URL can be running on any hosted service.</span></span> <span data-ttu-id="ede95-109">Estas tarjetas se definen como parte de mensajes accionables, y también se admiten en las [tarjetas](~/task-modules-and-cards/what-are-cards.md) que se usan en los bots de Teams y las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="ede95-109">These cards are defined as part of actionable messages, and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md) used in Teams bots and Messaging extensions.</span></span>

### <a name="example-connector-message"></a><span data-ttu-id="ede95-110">Ejemplo de mensaje de conector</span><span class="sxs-lookup"><span data-stu-id="ede95-110">Example connector message</span></span>

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

<span data-ttu-id="ede95-111">Este mensaje produce la siguiente tarjeta en el canal:</span><span class="sxs-lookup"><span data-stu-id="ede95-111">This message produces the following card in the channel:</span></span>

![Captura de pantalla de una tarjeta de conector](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a><span data-ttu-id="ede95-113">Creación de mensajes que requieren acción</span><span class="sxs-lookup"><span data-stu-id="ede95-113">Creating actionable messages</span></span>

<span data-ttu-id="ede95-114">En el ejemplo de la sección anterior se incluyen tres botones visibles en la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ede95-114">The example in the preceding section includes three visible buttons on the card.</span></span> <span data-ttu-id="ede95-115">Cada botón se define en la propiedad `potentialAction` del mensaje mediante acciones `ActionCard`, cada una de las cuales contiene un tipo de entrada: un campo de texto, un selector de fecha o una lista de opciones múltiples.</span><span class="sxs-lookup"><span data-stu-id="ede95-115">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each containing an input type: a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="ede95-116">Cada acción `ActionCard` tiene asociada una acción, por ejemplo `HttpPOST`.</span><span class="sxs-lookup"><span data-stu-id="ede95-116">Each `ActionCard` action has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="ede95-117">Las tarjetas de conector admiten tres tipos de acciones:</span><span class="sxs-lookup"><span data-stu-id="ede95-117">Connector cards support three types of actions:</span></span>

- <span data-ttu-id="ede95-118">`ActionCard` Presenta uno o varios tipos de entrada y acciones asociadas.</span><span class="sxs-lookup"><span data-stu-id="ede95-118">`ActionCard` Presents one or more input types and associated actions</span></span>
- <span data-ttu-id="ede95-119">`HttpPOST` Envía una solicitud POST a una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="ede95-119">`HttpPOST` Sends a POST request to a URL</span></span>
- <span data-ttu-id="ede95-120">`OpenUri` Abre un identificador URI en un explorador o aplicación independiente. De manera opcional, marca como destino diferentes URI en función de los sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="ede95-120">`OpenUri` Opens a URI in a separate browser or app; optionally targets different URIs based on operating systems</span></span>

<span data-ttu-id="ede95-121">La acción `ActionCard` admite tres tipos de entrada:</span><span class="sxs-lookup"><span data-stu-id="ede95-121">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="ede95-122">`TextInput` Un campo de texto de una sola línea o multilínea con un límite de longitud opcional.</span><span class="sxs-lookup"><span data-stu-id="ede95-122">`TextInput` A single-line or multiline text field with an optional length limit</span></span>
- <span data-ttu-id="ede95-123">`DateInput` Un selector de fecha con un selector de hora opcional.</span><span class="sxs-lookup"><span data-stu-id="ede95-123">`DateInput` A date selector with an optional time selector</span></span>
- <span data-ttu-id="ede95-124">`MultichoiceInput` Una lista de opciones enumeradas que ofrece una sola selección o selecciones múltiples.</span><span class="sxs-lookup"><span data-stu-id="ede95-124">`MultichoiceInput` A enumerated list of choices offering either a single selection or multiple selections</span></span>

<span data-ttu-id="ede95-125">`MultichoiceInput` admite una propiedad `style` que controla si inicialmente la lista se muestra totalmente expandida.</span><span class="sxs-lookup"><span data-stu-id="ede95-125">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="ede95-126">El valor predeterminado de `style` depende del valor de `isMultiSelect`.</span><span class="sxs-lookup"><span data-stu-id="ede95-126">The default value of `style` depends on the value of `isMultiSelect`.</span></span>

| `isMultiSelect` | <span data-ttu-id="ede95-127">`style` predeterminado</span><span class="sxs-lookup"><span data-stu-id="ede95-127">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="ede95-128">`false` o no especificado</span><span class="sxs-lookup"><span data-stu-id="ede95-128">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="ede95-129">Si quiere que se muestre inicialmente una lista de selección múltiple en el estilo compacto, debe especificar `"isMultiSelect": true` y `"style": true`.</span><span class="sxs-lookup"><span data-stu-id="ede95-129">If you want a multiselect list initially displayed in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

<span data-ttu-id="ede95-130">Para obtener más información sobre las acciones de tarjetas de conector, consulte **[Acciones]**(/outlook/actionable-messages/card-reference#actions) en la referencia de tarjeta de mensajes accionables.</span><span class="sxs-lookup"><span data-stu-id="ede95-130">For more information on Connector card actions, see **[Actions]**(/outlook/actionable-messages/card-reference#actions) in the actionable message card reference.</span></span>

> [!NOTE]
> <span data-ttu-id="ede95-131">Especificar `compact` para la propiedad `style` en Microsoft Teams es igual que especificar `normal` para la propiedad `style` en Microsoft Outlook.</span><span class="sxs-lookup"><span data-stu-id="ede95-131">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>
> 
> <span data-ttu-id="ede95-132">Para la acción HttpPOST, el token de usuario se incluye con las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="ede95-132">For the HttpPOST action, the bearer token is included with the requests.</span></span> <span data-ttu-id="ede95-133">Este token incluye la identidad de Azure AD del usuario de Office 365 que realizó la acción.</span><span class="sxs-lookup"><span data-stu-id="ede95-133">This token includes the Azure AD identity of the Office 365 user who took the action.</span></span>

## <a name="setting-up-a-custom-incoming-webhook"></a><span data-ttu-id="ede95-134">Configurar un webhook de entrada personalizado</span><span class="sxs-lookup"><span data-stu-id="ede95-134">Setting up a custom incoming webhook</span></span>

<span data-ttu-id="ede95-135">Siga estos pasos para ver cómo enviar una tarjeta simple a un conector:</span><span class="sxs-lookup"><span data-stu-id="ede95-135">Follow these steps to see how to send a simple card to a Connector:</span></span>

1. <span data-ttu-id="ede95-136">En Microsoft Teams, elija **Más opciones** (**&#8943;**) junto al nombre del canal y elija **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="ede95-136">In Microsoft Teams, choose **More options** (**&#8943;**) next to the channel name and then choose **Connectors**.</span></span>
1. <span data-ttu-id="ede95-137">Desplácese por la lista de conectores hasta **Webhook entrante** y elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ede95-137">Scroll through the list of Connectors to **Incoming Webhook**, and choose **Add**.</span></span>
1. <span data-ttu-id="ede95-138">Escriba un nombre para el webhook, cargue una imagen para asociarla a los datos del webhook y elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ede95-138">Enter a name for the webhook, upload an image to associate with data from the webhook, and choose **Create**.</span></span>
1. <span data-ttu-id="ede95-139">Copie el webhook en el portapapeles y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="ede95-139">Copy the webhook to the clipboard and save it.</span></span> <span data-ttu-id="ede95-140">Necesitará la dirección URL del webhook para enviar información a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ede95-140">You'll need the webhook URL for sending information to Microsoft Teams.</span></span>
1. <span data-ttu-id="ede95-141">Seleccione **Listo**.</span><span class="sxs-lookup"><span data-stu-id="ede95-141">Choose **Done**.</span></span>

### <a name="post-a-message-to-the-webhook-using-curl"></a><span data-ttu-id="ede95-142">Publicar un mensaje en webhook con cURL</span><span class="sxs-lookup"><span data-stu-id="ede95-142">Post a message to the webhook using cURL</span></span>

<span data-ttu-id="ede95-143">Los siguientes pasos usan [cURL](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="ede95-143">The following steps use [cURL](https://curl.haxx.se/).</span></span> <span data-ttu-id="ede95-144">Damos por sentado que lo tiene instalado y está familiarizado con su uso básico.</span><span class="sxs-lookup"><span data-stu-id="ede95-144">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="ede95-145">Desde la línea de comandos, escriba el siguiente comando cURL:</span><span class="sxs-lookup"><span data-stu-id="ede95-145">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

1. <span data-ttu-id="ede95-146">Si el envío se realiza correctamente, debería ver un resultado de salida **1** por `curl`.</span><span class="sxs-lookup"><span data-stu-id="ede95-146">If the POST succeeds, you should see a simple **1** output by `curl`.</span></span>
1. <span data-ttu-id="ede95-147">Compruebe el cliente de Microsoft Team.</span><span class="sxs-lookup"><span data-stu-id="ede95-147">Check the Microsoft Team client.</span></span> <span data-ttu-id="ede95-148">Debería ver la nueva tarjeta publicada en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ede95-148">You should see the new card posted to the team.</span></span>

### <a name="post-a-message-to-the-webhook-using-powershell"></a><span data-ttu-id="ede95-149">Publicar un mensaje en webhook con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ede95-149">Post a message to the webhook using PowerShell</span></span>

<span data-ttu-id="ede95-150">Los siguientes pasos usan PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ede95-150">The following steps use PowerShell.</span></span> <span data-ttu-id="ede95-151">Damos por sentado que lo tiene instalado y está familiarizado con su uso básico.</span><span class="sxs-lookup"><span data-stu-id="ede95-151">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="ede95-152">Desde el símbolo del sistema de PowerShell, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="ede95-152">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

1. <span data-ttu-id="ede95-153">Si el envío se realiza correctamente, debería ver un resultado de salida **1** por `Invoke-RestMethod`.</span><span class="sxs-lookup"><span data-stu-id="ede95-153">If the POST succeeds, you should see a simple **1** output by `Invoke-RestMethod`.</span></span>
1. <span data-ttu-id="ede95-154">Compruebe el canal de Microsoft Teams asociado a la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="ede95-154">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="ede95-155">Debería ver la nueva tarjeta publicada en el canal.</span><span class="sxs-lookup"><span data-stu-id="ede95-155">You should see the new card posted to the channel.</span></span>

- <span data-ttu-id="ede95-156">[Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="ede95-156">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="ede95-157">Modifique la parte `icons` del manifiesto para hacer referencia a los nombres de archivo de los iconos en lugar de a las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="ede95-157">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="ede95-158">La siguiente manifest.jsen el archivo contiene los elementos básicos necesarios para probar y enviar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="ede95-158">The following manifest.json file contains the basic elements needed to test and submit your app:</span></span>

> [!NOTE]
> <span data-ttu-id="ede95-159">Reemplace `id` y `connectorId` en el ejemplo siguiente con el GUID del conector.</span><span class="sxs-lookup"><span data-stu-id="ede95-159">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="ede95-160">Ejemplo de manifest.json con conector</span><span class="sxs-lookup"><span data-stu-id="ede95-160">Example manifest.json with connector</span></span>

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

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="ede95-161">Enviar tarjetas adaptables con un webhook entrante</span><span class="sxs-lookup"><span data-stu-id="ede95-161">Send adaptive cards using an incoming webhook</span></span>

> [!NOTE]
>
> <span data-ttu-id="ede95-162">✔ Todos los elementos de esquema de tarjetas adaptables nativas, excepto `Action.Submit`, son completamente compatibles.</span><span class="sxs-lookup"><span data-stu-id="ede95-162">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="ede95-163">✔ Las acciones compatibles son [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), y [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span><span class="sxs-lookup"><span data-stu-id="ede95-163">✔ The supported Actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

### <a name="the-flow-for-sending-adaptive-cards-via-an-incoming-webhook-is-as-follows"></a><span data-ttu-id="ede95-164">El flujo para el envío de [tarjetas adaptables](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) mediante un webhook entrante es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="ede95-164">The flow for sending [adaptive cards](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) via an incoming webhook is as follows:</span></span>

1. <span data-ttu-id="ede95-165">[Configure un webhook personalizado](#setting-up-a-custom-incoming-webhook) en Teams.</span><span class="sxs-lookup"><span data-stu-id="ede95-165">[Setup a custom webhook](#setting-up-a-custom-incoming-webhook) in Teams.</span></span></br></br>
1. <span data-ttu-id="ede95-166">Cree el archivo JSON de la tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="ede95-166">Create your adaptive card JSON file:</span></span>

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
                    "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)"
                    }
                ]
             }
          }
       ]
    }
    ```

    > [!div class="checklist"]
    >
    > - <span data-ttu-id="ede95-167">El campo `"type"` debe ser `"message"`.</span><span class="sxs-lookup"><span data-stu-id="ede95-167">The `"type"` field must be `"message"`.</span></span>
    > - <span data-ttu-id="ede95-168">La matriz `"attachments"` contiene un conjunto de objetos de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ede95-168">The `"attachments"` array contains a set of card objects.</span></span>
    > - <span data-ttu-id="ede95-169">El campo `"contentType"` debe establecerse en tipo de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="ede95-169">The `"contentType"` field must be set to adaptive card type.</span></span>
    > - <span data-ttu-id="ede95-170">El objeto `"content"` es la tarjeta con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ede95-170">The `"content"` object is the card formatted in JSON.</span></span>

1. <span data-ttu-id="ede95-171">Prueba tu tarjeta adaptable con Cartero.</span><span class="sxs-lookup"><span data-stu-id="ede95-171">Test your adaptive card with Postman.</span></span>

<span data-ttu-id="ede95-172">Para probar la tarjeta adaptativa, puede usar [Postman](https://www.postman.com) para enviar una solicitud POST a la dirección URL que creó cuando configuró el webhook entrante.</span><span class="sxs-lookup"><span data-stu-id="ede95-172">You can test your adaptive card using [Postman](https://www.postman.com) to send a POST request to the URL that you created when you setup your incoming webhook.</span></span> <span data-ttu-id="ede95-173">Pegue el archivo JSON en el cuerpo de la solicitud y vea el mensaje de la tarjeta adaptable en Teams.</span><span class="sxs-lookup"><span data-stu-id="ede95-173">Paste your JSON file in the body of the request and view your adaptive card message in Teams.</span></span>

>[!TIP]
> <span data-ttu-id="ede95-174">Puede usar el código de tarjeta adaptable [Ejemplos y plantillas](https://adaptivecards.io/samples) para el cuerpo de la solicitud Post de prueba.</span><span class="sxs-lookup"><span data-stu-id="ede95-174">You can use adaptive card code [Samples and Templates](https://adaptivecards.io/samples) for the body of your test Post request.</span></span>

## <a name="testing-your-connector"></a><span data-ttu-id="ede95-175">Probar el conector</span><span class="sxs-lookup"><span data-stu-id="ede95-175">Testing your connector</span></span>

<span data-ttu-id="ede95-176">Para probar el conector, cárguelo en un equipo igual que lo haría con cualquier otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="ede95-176">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="ede95-177">Puede crear un paquete de .zip mediante el archivo de manifiesto desde el Panel para desarrolladores de conectores que se modificó como se indicó en la sección anterior y los dos archivos de icono.</span><span class="sxs-lookup"><span data-stu-id="ede95-177">You can create a .zip package using the manifest file from the Connectors Developer Dashboard which was modified as directed in the preceding section and the two icon files.</span></span>

<span data-ttu-id="ede95-178">Después de cargar la aplicación, abra la lista Conectores desde cualquier canal.</span><span class="sxs-lookup"><span data-stu-id="ede95-178">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="ede95-179">Desplázate hasta la parte inferior para ver tu aplicación en la sección **Cargado:**</span><span class="sxs-lookup"><span data-stu-id="ede95-179">Scroll to the bottom to see your app in the **Uploaded** section:</span></span>

![Captura de pantalla de la sección cargada en el cuadro de diálogo Conector](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="ede95-181">Ahora, puede iniciar la experiencia de configuración.</span><span class="sxs-lookup"><span data-stu-id="ede95-181">You can now launch the configuration experience.</span></span> <span data-ttu-id="ede95-182">Tenga en cuenta que este flujo se produce completamente en Microsoft Teams a través de una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="ede95-182">Be aware that this flow occurs entirely within Microsoft Teams through a pop-up window.</span></span> <span data-ttu-id="ede95-183">Actualmente, este comportamiento es distinto de la experiencia de configuración en Conectores que hemos creado; estamos trabajando para unificar las experiencias.</span><span class="sxs-lookup"><span data-stu-id="ede95-183">Currently, this behavior differs from the configuration experience in Connectors that we created; we are working on unifying the experiences.</span></span>

<span data-ttu-id="ede95-184">Para comprobar que una acción `HttpPOST` está funcionando correctamente, utilice el [webhook entrante personalizado](#setting-up-a-custom-incoming-webhook).</span><span class="sxs-lookup"><span data-stu-id="ede95-184">To verify that an `HttpPOST` action is working correctly, use your [custom incoming webhook](#setting-up-a-custom-incoming-webhook).</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="ede95-185">Limitación de velocidad para conectores</span><span class="sxs-lookup"><span data-stu-id="ede95-185">Rate limiting for connectors</span></span>

<span data-ttu-id="ede95-186">Los límites de velocidad de la aplicación controlan el tráfico que puede generar un conector o un webhook entrante en un canal.</span><span class="sxs-lookup"><span data-stu-id="ede95-186">Application rate limits control the traffic that a connector or an incoming webhook is allowed to generate on a channel.</span></span> <span data-ttu-id="ede95-187">Teams realiza un seguimiento de las solicitudes a través de una ventana de velocidad fija y un contador incremental medido en segundos.</span><span class="sxs-lookup"><span data-stu-id="ede95-187">Teams tracks requests via a fixed-rate window and incremental counter measured in seconds.</span></span>  <span data-ttu-id="ede95-188">Si se hacen demasiadas solicitudes, se limita la conexión de cliente hasta que se actualice la ventana, es decir, mientras dure la velocidad fija.</span><span class="sxs-lookup"><span data-stu-id="ede95-188">If too many requests are made, the client connection will be throttled until the window refreshes, i.e., for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="ede95-189">**Umbrales de transacciones por segundo**</span><span class="sxs-lookup"><span data-stu-id="ede95-189">**Transactions per second thresholds**</span></span>

| <span data-ttu-id="ede95-190">Tiempo (segundos)</span><span class="sxs-lookup"><span data-stu-id="ede95-190">Time (seconds)</span></span>  | <span data-ttu-id="ede95-191">Número máximo de solicitudes permitidas</span><span class="sxs-lookup"><span data-stu-id="ede95-191">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="ede95-192">1</span><span class="sxs-lookup"><span data-stu-id="ede95-192">1</span></span>   | <span data-ttu-id="ede95-193">4 </span><span class="sxs-lookup"><span data-stu-id="ede95-193">4</span></span>  |  
| <span data-ttu-id="ede95-194">30</span><span class="sxs-lookup"><span data-stu-id="ede95-194">30</span></span>   | <span data-ttu-id="ede95-195">60</span><span class="sxs-lookup"><span data-stu-id="ede95-195">60</span></span>  |  
| <span data-ttu-id="ede95-196">3600</span><span class="sxs-lookup"><span data-stu-id="ede95-196">3600</span></span>   | <span data-ttu-id="ede95-197">100</span><span class="sxs-lookup"><span data-stu-id="ede95-197">100</span></span>  |
| <span data-ttu-id="ede95-198">7200</span><span class="sxs-lookup"><span data-stu-id="ede95-198">7200</span></span> | <span data-ttu-id="ede95-199">150</span><span class="sxs-lookup"><span data-stu-id="ede95-199">150</span></span>  |
| <span data-ttu-id="ede95-200">86400</span><span class="sxs-lookup"><span data-stu-id="ede95-200">86400</span></span>  | <span data-ttu-id="ede95-201">1800</span><span class="sxs-lookup"><span data-stu-id="ede95-201">1800</span></span>  |

<span data-ttu-id="ede95-202">Una [lógica de reintento con interrupción exponencial](/azure/architecture/patterns/retry) como la que se muestra a continuación mitigaría la restricción de velocidad en casos en que las solicitudes superen los límites en un segundo.</span><span class="sxs-lookup"><span data-stu-id="ede95-202">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) like below would mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="ede95-203">Consulte las [respuestas HTTP 429](../../bots/how-to/rate-limit.md#handle-http-429-responses) para evitar superar los límites de velocidad.</span><span class="sxs-lookup"><span data-stu-id="ede95-203">Refer [HTTP 429 responses](../../bots/how-to/rate-limit.md#handle-http-429-responses) to avoid hitting the rate limits.</span></span>

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
 
<span data-ttu-id="ede95-204">Estos límites tienen el propósito de reducir el correo no deseado en un canal con un conector y garantizan una experiencia óptima para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="ede95-204">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to your end users.</span></span>

## <a name="see-also"></a><span data-ttu-id="ede95-205">Vea también</span><span class="sxs-lookup"><span data-stu-id="ede95-205">See also</span></span>

[<span data-ttu-id="ede95-206">Office 365 Conectores — Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ede95-206">Office 365 Connectors — Microsoft Teams</span></span>](/connectors/teams/)