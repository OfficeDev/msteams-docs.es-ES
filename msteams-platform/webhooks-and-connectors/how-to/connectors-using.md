---
title: Crear y enviar mensajes
author: laujan
description: Describe cómo usar los Conectores de Office 365 en Microsoft Teams
ms.topic: how-to
localization_priority: Normal
keywords: teams o365 conector
ms.openlocfilehash: 8835e43ed74a8da5ad3b3b4358b259d63068b469
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179898"
---
# <a name="create-and-send-messages"></a><span data-ttu-id="49179-104">Crear y enviar mensajes</span><span class="sxs-lookup"><span data-stu-id="49179-104">Create and send messages</span></span>

<span data-ttu-id="49179-105">Puede crear mensajes que puedan realizar acciones y enviarlos a través de Webhook entrante o Office 365 Connector.</span><span class="sxs-lookup"><span data-stu-id="49179-105">You can create actionable messages and send it through Incoming Webhook or Office 365 Connector.</span></span>

## <a name="create-actionable-messages"></a><span data-ttu-id="49179-106">Crear mensajes que pueden actuar</span><span class="sxs-lookup"><span data-stu-id="49179-106">Create actionable messages</span></span>

<span data-ttu-id="49179-107">Los mensajes que pueden actuar incluyen tres botones visibles en la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="49179-107">The actionable messages include three visible buttons on the card.</span></span> <span data-ttu-id="49179-108">Cada botón se define en la propiedad del mensaje mediante acciones, cada una con un tipo de entrada, un campo de texto, un selector de fechas o una lista de `potentialAction` `ActionCard` opciones múltiples.</span><span class="sxs-lookup"><span data-stu-id="49179-108">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each with an input type, a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="49179-109">Cada `ActionCard` uno tiene una acción asociada, por ejemplo `HttpPOST` .</span><span class="sxs-lookup"><span data-stu-id="49179-109">Each `ActionCard` has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="49179-110">Las tarjetas de conector admiten las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="49179-110">The connector cards support the following actions:</span></span>

- <span data-ttu-id="49179-111">`ActionCard`: presenta uno o varios tipos de entrada y acciones asociadas.</span><span class="sxs-lookup"><span data-stu-id="49179-111">`ActionCard`: Presents one or more input types and associated actions.</span></span>
- <span data-ttu-id="49179-112">`HttpPOST`: envía la solicitud POST a una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="49179-112">`HttpPOST`: Sends POST request to a URL.</span></span>
- <span data-ttu-id="49179-113">`OpenUri`: abre uri en un explorador o aplicación independiente, opcionalmente tiene como destino diferentes URI basados en sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="49179-113">`OpenUri`: Opens URI in a separate browser or app, optionally targets different URIs based on operating systems.</span></span>

<span data-ttu-id="49179-114">La acción `ActionCard` admite tres tipos de entrada:</span><span class="sxs-lookup"><span data-stu-id="49179-114">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="49179-115">`TextInput`: un campo de texto de línea única o de varias líneas con un límite de longitud opcional.</span><span class="sxs-lookup"><span data-stu-id="49179-115">`TextInput`: A single line or multiline text field with an optional length limit.</span></span>
- <span data-ttu-id="49179-116">`DateInput`: selector de fecha con un selector de hora opcional.</span><span class="sxs-lookup"><span data-stu-id="49179-116">`DateInput`: A date selector with an optional time selector.</span></span>
- <span data-ttu-id="49179-117">`MultichoiceInput`: Una lista enumerada de opciones que ofrecen una sola selección o varias selecciones.</span><span class="sxs-lookup"><span data-stu-id="49179-117">`MultichoiceInput`: An enumerated list of choices offering either a single selection or multiple selections.</span></span>

<span data-ttu-id="49179-118">`MultichoiceInput` admite una propiedad `style` que controla si inicialmente la lista se muestra totalmente expandida.</span><span class="sxs-lookup"><span data-stu-id="49179-118">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="49179-119">El valor predeterminado de `style` depende del valor de la siguiente `isMultiSelect` manera:</span><span class="sxs-lookup"><span data-stu-id="49179-119">The default value of `style` depends on the value of `isMultiSelect` as follows:</span></span>

| `isMultiSelect` | <span data-ttu-id="49179-120">`style` predeterminado</span><span class="sxs-lookup"><span data-stu-id="49179-120">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="49179-121">`false` o no especificado</span><span class="sxs-lookup"><span data-stu-id="49179-121">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="49179-122">Para mostrar la lista de selección múltiple en el estilo compacto, debe especificar ambos `"isMultiSelect": true` y `"style": true` .</span><span class="sxs-lookup"><span data-stu-id="49179-122">To display the multiselect list in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

<span data-ttu-id="49179-123">Para obtener más información sobre las acciones de tarjeta de conector, vea [Actions](/outlook/actionable-messages/card-reference#actions).</span><span class="sxs-lookup"><span data-stu-id="49179-123">For more information on connector card actions, see [Actions](/outlook/actionable-messages/card-reference#actions).</span></span>

> [!NOTE]
> * <span data-ttu-id="49179-124">Especificar `compact` para la propiedad `style` en Microsoft Teams es igual que especificar `normal` para la propiedad `style` en Microsoft Outlook.</span><span class="sxs-lookup"><span data-stu-id="49179-124">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>
> * <span data-ttu-id="49179-125">Para la acción HttpPOST, el token de usuario se incluye con las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="49179-125">For the HttpPOST action, the bearer token is included with the requests.</span></span> <span data-ttu-id="49179-126">Este token incluye la identidad de Azure AD del usuario de Office 365 que realizó la acción.</span><span class="sxs-lookup"><span data-stu-id="49179-126">This token includes the Azure AD identity of the Office 365 user who took the action.</span></span>

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a><span data-ttu-id="49179-127">Enviar un mensaje a través de Webhook entrante o Office 365 Connector</span><span class="sxs-lookup"><span data-stu-id="49179-127">Send a message through Incoming Webhook or Office 365 Connector</span></span>

<span data-ttu-id="49179-128">Para enviar un mensaje a través del Webhook entrante o Office 365 Connector, publique una carga JSON en la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="49179-128">To send a message through your Incoming Webhook or Office 365 Connector, post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="49179-129">Esta carga debe tener la forma de una [Office 365 de conector .](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="49179-129">This payload must be in the form of an [Office 365 connector card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="49179-130">También puede usar este JSON para crear tarjetas que contengan entradas enriqueciendo, como entrada de texto, selección múltiple o selección de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="49179-130">You can also use this JSON to create cards containing rich inputs, such as text entry, multiselect, or selecting date and time.</span></span> <span data-ttu-id="49179-131">El código que genera la tarjeta y la publica en la dirección URL de webhook puede ejecutarse en cualquier servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="49179-131">The code that generates the card and posts it to the webhook URL can run on any hosted service.</span></span> <span data-ttu-id="49179-132">Estas tarjetas se definen como parte de los [](~/task-modules-and-cards/what-are-cards.md)mensajes que se pueden usar y también se admiten en tarjetas, que se usan Teams bots y extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="49179-132">These cards are defined as part of actionable messages and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md), used in Teams bots and messaging extensions.</span></span>

### <a name="example-of-connector-message"></a><span data-ttu-id="49179-133">Ejemplo de mensaje de conector</span><span class="sxs-lookup"><span data-stu-id="49179-133">Example of connector message</span></span>

<span data-ttu-id="49179-134">Un ejemplo de mensaje de conector es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="49179-134">An example of connector message is as follows:</span></span>

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

<span data-ttu-id="49179-135">Este mensaje proporciona la siguiente tarjeta en el canal:</span><span class="sxs-lookup"><span data-stu-id="49179-135">This message provides the following card in the channel:</span></span>

![Captura de pantalla de una tarjeta de conector](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a><span data-ttu-id="49179-137">Enviar mensajes con cURL y PowerShell</span><span class="sxs-lookup"><span data-stu-id="49179-137">Send messages using cURL and PowerShell</span></span>

# <a name="curl"></a>[<span data-ttu-id="49179-138">cURL</span><span class="sxs-lookup"><span data-stu-id="49179-138">cURL</span></span>](#tab/cURL)

<span data-ttu-id="49179-139">**Para publicar un mensaje en el webhook con cURL**</span><span class="sxs-lookup"><span data-stu-id="49179-139">**To post a message in the webhook with cURL**</span></span>

1. <span data-ttu-id="49179-140">Instale cURL con: https://curl.haxx.se/ .</span><span class="sxs-lookup"><span data-stu-id="49179-140">Install cURL using: https://curl.haxx.se/.</span></span>

1. <span data-ttu-id="49179-141">Desde la línea de comandos, escriba el siguiente comando cURL:</span><span class="sxs-lookup"><span data-stu-id="49179-141">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > <span data-ttu-id="49179-142">Si post se realiza correctamente, debe ver una salida simple **1** por `curl` .</span><span class="sxs-lookup"><span data-stu-id="49179-142">If the POST succeeds, you must see a simple **1** output by `curl`.</span></span>

1. <span data-ttu-id="49179-143">Compruebe en Microsoft Teams cliente la nueva tarjeta publicada.</span><span class="sxs-lookup"><span data-stu-id="49179-143">Check the Microsoft Teams client for the new card posted.</span></span>

# <a name="powershell"></a>[<span data-ttu-id="49179-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="49179-144">PowerShell</span></span>](#tab/PowerShell)

 <span data-ttu-id="49179-145">Requisito previo: instalación de PowerShell y familiarización con su uso básico.</span><span class="sxs-lookup"><span data-stu-id="49179-145">Prerequisite: Installation of PowerShell and familiarization with its basic usage.</span></span>

<span data-ttu-id="49179-146">**Para publicar un mensaje en el webhook con PowerShell**</span><span class="sxs-lookup"><span data-stu-id="49179-146">**To post a message to the webhook with PowerShell**</span></span>

1. <span data-ttu-id="49179-147">Desde el símbolo del sistema de PowerShell, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="49179-147">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > <span data-ttu-id="49179-148">Si post se realiza correctamente, debe ver una salida simple **1** por `Invoke-RestMethod` .</span><span class="sxs-lookup"><span data-stu-id="49179-148">If the POST succeeds, you must see a simple **1** output by `Invoke-RestMethod`.</span></span>

1. <span data-ttu-id="49179-149">Compruebe el canal de Microsoft Teams asociado a la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="49179-149">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="49179-150">Puede ver la nueva tarjeta publicada en el canal.</span><span class="sxs-lookup"><span data-stu-id="49179-150">You can see the new card posted to the channel.</span></span> <span data-ttu-id="49179-151">Antes de usar el conector para probar o publicar la aplicación, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="49179-151">Before you use the connector to test or publish your app, you must do the following:</span></span>

    - <span data-ttu-id="49179-152">[Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="49179-152">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
    - <span data-ttu-id="49179-153">Modifique la `icons` parte del manifiesto a los nombres de archivo de los iconos en lugar de las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="49179-153">Modify the `icons` portion of the manifest to the file names of the icons instead of URLs.</span></span>

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="49179-154">Enviar tarjetas adaptables mediante un webhook entrante</span><span class="sxs-lookup"><span data-stu-id="49179-154">Send Adaptive Cards using an Incoming Webhook</span></span>

> [!NOTE]
> * <span data-ttu-id="49179-155">Todos los elementos nativos del esquema de tarjeta adaptable, excepto `Action.Submit` , son totalmente compatibles.</span><span class="sxs-lookup"><span data-stu-id="49179-155">All native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span>
> * <span data-ttu-id="49179-156">Las acciones admitidas [**son Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)y [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span><span class="sxs-lookup"><span data-stu-id="49179-156">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

<span data-ttu-id="49179-157">**Para enviar tarjetas adaptables a través de un webhook entrante**</span><span class="sxs-lookup"><span data-stu-id="49179-157">**To send Adaptive Cards through an Incoming Webhook**</span></span>

1. <span data-ttu-id="49179-158">[Configure un webhook personalizado](~/webhooks-and-connectors/how-to/add-incoming-webhook.md) en Teams.</span><span class="sxs-lookup"><span data-stu-id="49179-158">[Setup a custom webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md) in Teams.</span></span>
1. <span data-ttu-id="49179-159">Cree un archivo JSON de tarjeta adaptable con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="49179-159">Create Adaptive Card JSON file using the following code:</span></span>

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

    <span data-ttu-id="49179-160">Las propiedades del archivo JSON de tarjeta adaptable son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="49179-160">The properties for Adaptive Card JSON file are as follows:</span></span>

    * <span data-ttu-id="49179-161">El campo `"type"` debe ser `"message"`.</span><span class="sxs-lookup"><span data-stu-id="49179-161">The `"type"` field must be `"message"`.</span></span>
    * <span data-ttu-id="49179-162">La matriz `"attachments"` contiene un conjunto de objetos de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="49179-162">The `"attachments"` array contains a set of card objects.</span></span>
    * <span data-ttu-id="49179-163">El `"contentType"` campo debe establecerse en Tipo de tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="49179-163">The `"contentType"` field must be set to Adaptive Card type.</span></span>
    * <span data-ttu-id="49179-164">El objeto `"content"` es la tarjeta con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="49179-164">The `"content"` object is the card formatted in JSON.</span></span>

1. <span data-ttu-id="49179-165">Pruebe la tarjeta adaptable con Postman:</span><span class="sxs-lookup"><span data-stu-id="49179-165">Test your Adaptive Card with Postman:</span></span>

    * <span data-ttu-id="49179-166">Pruebe la tarjeta adaptable con [Postman](https://www.postman.com) para enviar una solicitud POST a la dirección URL, creada para configurar el webhook entrante.</span><span class="sxs-lookup"><span data-stu-id="49179-166">Test the Adaptive Card using [Postman](https://www.postman.com) to send a POST request to the URL, created to set up Incoming Webhook.</span></span>
    * <span data-ttu-id="49179-167">Pegue el archivo JSON en el cuerpo de la solicitud y vea el mensaje de tarjeta adaptable en Teams.</span><span class="sxs-lookup"><span data-stu-id="49179-167">Paste the JSON file in the body of the request and view the Adaptive Card message in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="49179-168">Use plantillas y [ejemplos de código de tarjeta](https://adaptivecards.io/samples) adaptable para probar el cuerpo de la solicitud POST.</span><span class="sxs-lookup"><span data-stu-id="49179-168">Use Adaptive Card [code samples and templates](https://adaptivecards.io/samples) to test the body of POST request.</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="49179-169">Limitación de velocidad para conectores</span><span class="sxs-lookup"><span data-stu-id="49179-169">Rate limiting for connectors</span></span>

<span data-ttu-id="49179-170">Los límites de velocidad de aplicación controlan el tráfico que puede generar un conector o un webhook entrante en un canal.</span><span class="sxs-lookup"><span data-stu-id="49179-170">Application rate limits control the traffic that a connector or an Incoming Webhook is permitted to generate on a channel.</span></span> <span data-ttu-id="49179-171">Teams realizar un seguimiento de las solicitudes mediante una ventana de tasa fija y un contador incremental medidos en segundos.</span><span class="sxs-lookup"><span data-stu-id="49179-171">Teams track requests using a fixed rate window and incremental counter measured in seconds.</span></span> <span data-ttu-id="49179-172">Si se realizan más de cuatro solicitudes en un segundo, la conexión de cliente se limita hasta que la ventana se actualiza durante la duración de la tasa fija.</span><span class="sxs-lookup"><span data-stu-id="49179-172">If more than four requests are made in a second, the client connection is throttled until the window refreshes for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="49179-173">Umbrales de transacciones por segundo</span><span class="sxs-lookup"><span data-stu-id="49179-173">Transactions per second thresholds</span></span>

<span data-ttu-id="49179-174">En la tabla siguiente se proporcionan los detalles de transacciones basadas en tiempo:</span><span class="sxs-lookup"><span data-stu-id="49179-174">The following table provides the time based transaction details:</span></span>

| <span data-ttu-id="49179-175">Tiempo en segundos</span><span class="sxs-lookup"><span data-stu-id="49179-175">Time in seconds</span></span>  | <span data-ttu-id="49179-176">Número máximo de solicitudes permitidas</span><span class="sxs-lookup"><span data-stu-id="49179-176">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="49179-177">1 </span><span class="sxs-lookup"><span data-stu-id="49179-177">1</span></span>   | <span data-ttu-id="49179-178">4 </span><span class="sxs-lookup"><span data-stu-id="49179-178">4</span></span>  |  
| <span data-ttu-id="49179-179">30</span><span class="sxs-lookup"><span data-stu-id="49179-179">30</span></span>   | <span data-ttu-id="49179-180">60</span><span class="sxs-lookup"><span data-stu-id="49179-180">60</span></span>  |  
| <span data-ttu-id="49179-181">3600</span><span class="sxs-lookup"><span data-stu-id="49179-181">3600</span></span>   | <span data-ttu-id="49179-182">100</span><span class="sxs-lookup"><span data-stu-id="49179-182">100</span></span>  |
| <span data-ttu-id="49179-183">7200</span><span class="sxs-lookup"><span data-stu-id="49179-183">7200</span></span> | <span data-ttu-id="49179-184">150</span><span class="sxs-lookup"><span data-stu-id="49179-184">150</span></span>  |
| <span data-ttu-id="49179-185">86400</span><span class="sxs-lookup"><span data-stu-id="49179-185">86400</span></span>  | <span data-ttu-id="49179-186">1800</span><span class="sxs-lookup"><span data-stu-id="49179-186">1800</span></span>  |

<span data-ttu-id="49179-187">Una [lógica de reintentos con retroceso](/azure/architecture/patterns/retry) exponencial puede mitigar la limitación de velocidad en casos en los que las solicitudes superan los límites en un segundo.</span><span class="sxs-lookup"><span data-stu-id="49179-187">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) can mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="49179-188">Siga [los procedimientos recomendados](../../bots/how-to/rate-limit.md) para evitar alcanzar los límites de velocidad.</span><span class="sxs-lookup"><span data-stu-id="49179-188">Follow [best practices](../../bots/how-to/rate-limit.md) to avoid hitting the rate limits.</span></span>

> [!NOTE]
> <span data-ttu-id="49179-189">Una [lógica de reintentos con retroceso](/azure/architecture/patterns/retry) exponencial puede mitigar la limitación de velocidad en casos en los que las solicitudes superan los límites en un segundo.</span><span class="sxs-lookup"><span data-stu-id="49179-189">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) can mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="49179-190">Consulte las [respuestas HTTP 429](../../bots/how-to/rate-limit.md#handle-http-429-responses) para evitar superar los límites de velocidad.</span><span class="sxs-lookup"><span data-stu-id="49179-190">Refer [HTTP 429 responses](../../bots/how-to/rate-limit.md#handle-http-429-responses) to avoid hitting the rate limits.</span></span>

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

<span data-ttu-id="49179-191">Estos límites se aplican para reducir el correo no deseado de un canal por un conector y garantiza una experiencia óptima para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="49179-191">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to users.</span></span>

## <a name="see-also"></a><span data-ttu-id="49179-192">Vea también</span><span class="sxs-lookup"><span data-stu-id="49179-192">See also</span></span>

* [<span data-ttu-id="49179-193">Office 365 Conectores para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="49179-193">Office 365 Connectors for Microsoft Teams</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="49179-194">Crear un webhook entrante</span><span class="sxs-lookup"><span data-stu-id="49179-194">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="49179-195">Crear un webhook saliente</span><span class="sxs-lookup"><span data-stu-id="49179-195">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
