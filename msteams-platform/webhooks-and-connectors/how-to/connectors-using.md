---
title: Envío de mensajes a conectores y webhooks
description: Describe cómo usar los Conectores de Office 365 en Microsoft Teams
localization_priority: Priority
keywords: teams o365 conector
ms.openlocfilehash: b22159002713ccec6441f2128190e9944945aff6
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783916"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a><span data-ttu-id="b03bd-104">Envío de mensajes a conectores y webhooks</span><span class="sxs-lookup"><span data-stu-id="b03bd-104">Sending messages to Connectors and Webhooks</span></span>

<span data-ttu-id="b03bd-105">Para enviar un mensaje a través del conector de Office 365 o el webhook de entrada, debe publicar una carga JSON en la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="b03bd-105">To send a message through your Office 365 Connector or incoming webhook, you post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="b03bd-106">Por lo general, esta carga será una [tarjeta de conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="b03bd-106">Typically this payload will be in the form of an [Office 365 Connector Card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="b03bd-107">También puede usar este JSON para crear tarjetas que contengan entradas enriquecidas, como entrada de texto, selección múltiple o selección de una fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="b03bd-107">You can also use this JSON to create cards containing rich inputs, such as text entry, multi-select, or picking a date and time.</span></span> <span data-ttu-id="b03bd-108">El código que genera la tarjeta y publica en la dirección URL de webhook se puede ejecutar en cualquier servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="b03bd-108">The code that generates the card and posts to the webhook URL can be running on any hosted service.</span></span> <span data-ttu-id="b03bd-109">Estas tarjetas se definen como parte de mensajes accionables, y también se admiten en las [tarjetas](~/task-modules-and-cards/what-are-cards.md) que se usan en los bots de Teams y las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b03bd-109">These cards are defined as part of actionable messages, and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md) used in Teams bots and Messaging extensions.</span></span>

### <a name="example-connector-message"></a><span data-ttu-id="b03bd-110">Ejemplo de mensaje de conector</span><span class="sxs-lookup"><span data-stu-id="b03bd-110">Example Connector message</span></span>

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "![TestImage](https://47a92947.ngrok.io/Content/Images/default.png)Larry Bryant created a new task",
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
            "target": "http://..."
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
            "target": "http://..."
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
            "target": "http://..."
        }]
    }]
}
```

<span data-ttu-id="b03bd-111">Este mensaje produce la siguiente tarjeta en el canal.</span><span class="sxs-lookup"><span data-stu-id="b03bd-111">This message produces the following card in the channel.</span></span>

![Captura de pantalla de una tarjeta de conector](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a><span data-ttu-id="b03bd-113">Creación de mensajes que requieren acción</span><span class="sxs-lookup"><span data-stu-id="b03bd-113">Creating actionable messages</span></span>

<span data-ttu-id="b03bd-114">En el ejemplo de la sección anterior se incluyen tres botones visibles en la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b03bd-114">The example in the preceding section includes three visible buttons on the card.</span></span> <span data-ttu-id="b03bd-115">Cada botón se define en la propiedad `potentialAction` del mensaje mediante acciones `ActionCard`, cada una de las cuales contiene un tipo de entrada: un campo de texto, un selector de fecha o una lista de opciones múltiples.</span><span class="sxs-lookup"><span data-stu-id="b03bd-115">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each containing an input type: a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="b03bd-116">Cada acción `ActionCard` tiene asociada una acción, por ejemplo `HttpPOST`.</span><span class="sxs-lookup"><span data-stu-id="b03bd-116">Each `ActionCard` action has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="b03bd-117">Las tarjetas de conector admiten tres tipos de acciones:</span><span class="sxs-lookup"><span data-stu-id="b03bd-117">Connector cards support three types of actions:</span></span>

- <span data-ttu-id="b03bd-118">`ActionCard` Presenta uno o varios tipos de entrada y acciones asociadas.</span><span class="sxs-lookup"><span data-stu-id="b03bd-118">`ActionCard` Presents one or more input types and associated actions</span></span>
- <span data-ttu-id="b03bd-119">`HttpPOST` Envía una solicitud POST a una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="b03bd-119">`HttpPOST` Sends a POST request to a URL</span></span>
- <span data-ttu-id="b03bd-120">`OpenUri` Abre un identificador URI en un explorador o aplicación independiente. De manera opcional, marca como destino diferentes URI en función de los sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="b03bd-120">`OpenUri` Opens a URI in a separate browser or app; optionally targets different URIs based on operating systems</span></span>

<span data-ttu-id="b03bd-121">(Una cuarta acción, `ViewAction`, aún es compatible pero ya no es necesaria; use `OpenUri` en su lugar).</span><span class="sxs-lookup"><span data-stu-id="b03bd-121">(A fourth action, `ViewAction`, is still supported but no longer needed; use `OpenUri` instead.)</span></span>

<span data-ttu-id="b03bd-122">La acción `ActionCard` admite tres tipos de entrada:</span><span class="sxs-lookup"><span data-stu-id="b03bd-122">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="b03bd-123">`TextInput` Un campo de texto de una sola línea o multilínea con un límite de longitud opcional.</span><span class="sxs-lookup"><span data-stu-id="b03bd-123">`TextInput` A single-line or multiline text field with an optional length limit</span></span>
- <span data-ttu-id="b03bd-124">`DateInput` Un selector de fecha con un selector de hora opcional.</span><span class="sxs-lookup"><span data-stu-id="b03bd-124">`DateInput` A date selector with an optional time selector</span></span>
- <span data-ttu-id="b03bd-125">`MultichoiceInput` Una lista de opciones enumeradas que ofrece una sola selección o selecciones múltiples.</span><span class="sxs-lookup"><span data-stu-id="b03bd-125">`MultichoiceInput` A enumerated list of choices offering either a single selection or multiple selections</span></span>

<span data-ttu-id="b03bd-126">`MultichoiceInput` admite una propiedad `style` que controla si inicialmente la lista se muestra totalmente expandida.</span><span class="sxs-lookup"><span data-stu-id="b03bd-126">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="b03bd-127">El valor predeterminado de `style` depende del valor de `isMultiSelect`.</span><span class="sxs-lookup"><span data-stu-id="b03bd-127">The default value of `style` depends on the value of `isMultiSelect`.</span></span>

| `isMultiSelect` | <span data-ttu-id="b03bd-128">`style` predeterminado</span><span class="sxs-lookup"><span data-stu-id="b03bd-128">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="b03bd-129">`false` o no especificado</span><span class="sxs-lookup"><span data-stu-id="b03bd-129">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="b03bd-130">Si quiere que se muestre inicialmente una lista de selección múltiple en el estilo compacto, debe especificar `"isMultiSelect": true` y `"style": true`.</span><span class="sxs-lookup"><span data-stu-id="b03bd-130">If you want a multiselect list initially displayed in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

> [!NOTE]
> <span data-ttu-id="b03bd-131">Especificar `compact` para la propiedad `style` en Microsoft Teams es igual que especificar `normal` para la propiedad `style` en Microsoft Outlook.</span><span class="sxs-lookup"><span data-stu-id="b03bd-131">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>

<span data-ttu-id="b03bd-132">Para obtener más información sobre las acciones de la tarjeta conector, consulte **[Acciones](/outlook/actionable-messages/card-reference#actions)** en la referencia de la tarjeta de mensaje accionable.</span><span class="sxs-lookup"><span data-stu-id="b03bd-132">For all other details about Connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="setting-up-a-custom-incoming-webhook"></a><span data-ttu-id="b03bd-133">Configurar un webhook de entrada personalizado</span><span class="sxs-lookup"><span data-stu-id="b03bd-133">Setting up a custom incoming webhook</span></span>

<span data-ttu-id="b03bd-134">Siga estos pasos para ver cómo se envía una tarjeta simple a un conector.</span><span class="sxs-lookup"><span data-stu-id="b03bd-134">Follow these steps to see how to send a simple card to a Connector.</span></span>

1. <span data-ttu-id="b03bd-135">En Microsoft Teams, elija **Más opciones** (**&#8943;**) junto al nombre del canal y elija **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="b03bd-135">In Microsoft Teams, choose **More options** (**&#8943;**) next to the channel name and then choose **Connectors**.</span></span>
2. <span data-ttu-id="b03bd-136">Desplácese por la lista de conectores hasta **Webhook entrante** y elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b03bd-136">Scroll through the list of Connectors to **Incoming Webhook**, and choose **Add**.</span></span>
3. <span data-ttu-id="b03bd-137">Escriba un nombre para el webhook, cargue una imagen para asociarla a los datos del webhook y elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b03bd-137">Enter a name for the webhook, upload an image to associate with data from the webhook, and choose **Create**.</span></span>
4. <span data-ttu-id="b03bd-138">Copie el webhook en el portapapeles y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="b03bd-138">Copy the webhook to the clipboard and save it.</span></span> <span data-ttu-id="b03bd-139">Necesitará la dirección URL del webhook para enviar información a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b03bd-139">You'll need the webhook URL for sending information to Microsoft Teams.</span></span>
5. <span data-ttu-id="b03bd-140">Seleccione **Listo**.</span><span class="sxs-lookup"><span data-stu-id="b03bd-140">Choose **Done**.</span></span>

### <a name="post-a-message-to-the-webhook-using-curl"></a><span data-ttu-id="b03bd-141">Publicar un mensaje en webhook con cURL</span><span class="sxs-lookup"><span data-stu-id="b03bd-141">Post a message to the webhook using cURL</span></span>

<span data-ttu-id="b03bd-142">Los siguientes pasos usan [cURL](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="b03bd-142">The following steps use [cURL](https://curl.haxx.se/).</span></span> <span data-ttu-id="b03bd-143">Damos por sentado que lo tiene instalado y está familiarizado con su uso básico.</span><span class="sxs-lookup"><span data-stu-id="b03bd-143">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="b03bd-144">Desde la línea de comandos, escriba el siguiente comando cURL:</span><span class="sxs-lookup"><span data-stu-id="b03bd-144">From the command line, enter the following cURL command:</span></span>

   ```bash
   curl -H "Content-Type: application/json" -d "{\"text\": \"Hello World\"}" <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="b03bd-145">Si el envío se realiza correctamente, debería ver un resultado de salida **1** por `curl`.</span><span class="sxs-lookup"><span data-stu-id="b03bd-145">If the POST succeeds, you should see a simple **1** output by `curl`.</span></span>
3. <span data-ttu-id="b03bd-146">Compruebe el cliente de Microsoft Team.</span><span class="sxs-lookup"><span data-stu-id="b03bd-146">Check the Microsoft Team client.</span></span> <span data-ttu-id="b03bd-147">Debería ver la nueva tarjeta publicada en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b03bd-147">You should see the new card posted to the team.</span></span>

### <a name="post-a-message-to-the-webhook-using-powershell"></a><span data-ttu-id="b03bd-148">Publicar un mensaje en webhook con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b03bd-148">Post a message to the webhook using PowerShell</span></span>

<span data-ttu-id="b03bd-149">Los siguientes pasos usan PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b03bd-149">The following steps use PowerShell.</span></span> <span data-ttu-id="b03bd-150">Damos por sentado que lo tiene instalado y está familiarizado con su uso básico.</span><span class="sxs-lookup"><span data-stu-id="b03bd-150">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="b03bd-151">Desde el símbolo del sistema de PowerShell, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b03bd-151">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="b03bd-152">Si el envío se realiza correctamente, debería ver un resultado de salida **1** por `Invoke-RestMethod`.</span><span class="sxs-lookup"><span data-stu-id="b03bd-152">If the POST succeeds, you should see a simple **1** output by `Invoke-RestMethod`.</span></span>
3. <span data-ttu-id="b03bd-153">Compruebe el canal de Microsoft Teams asociado a la dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="b03bd-153">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="b03bd-154">Debería ver la nueva tarjeta publicada en el canal.</span><span class="sxs-lookup"><span data-stu-id="b03bd-154">You should see the new card posted to the channel.</span></span>

- <span data-ttu-id="b03bd-155">Incluya dos iconos, siguiendo las instrucciones de [Iconos](~/concepts/build-and-test/apps-package.md#icons).</span><span class="sxs-lookup"><span data-stu-id="b03bd-155">Include two icons, following the instructions in [Icons](~/concepts/build-and-test/apps-package.md#icons).</span></span>
- <span data-ttu-id="b03bd-156">Modifique la parte `icons` del manifiesto para hacer referencia a los nombres de archivo de los iconos en lugar de a las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="b03bd-156">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="b03bd-157">El archivo manifest.json siguiente contiene los elementos básicos necesarios para probar y enviar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b03bd-157">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="b03bd-158">Reemplace `id` y `connectorId` en el ejemplo siguiente con el GUID del conector.</span><span class="sxs-lookup"><span data-stu-id="b03bd-158">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="b03bd-159">Ejemplo de manifest.json con conector</span><span class="sxs-lookup"><span data-stu-id="b03bd-159">Example manifest.json with Connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

## <a name="testing-your-connector"></a><span data-ttu-id="b03bd-160">Probar el conector</span><span class="sxs-lookup"><span data-stu-id="b03bd-160">Testing your Connector</span></span>

<span data-ttu-id="b03bd-161">Para probar el conector, cárguelo en un equipo igual que lo haría con cualquier otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="b03bd-161">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="b03bd-162">Puede crear un paquete .zip mediante el archivo de manifiesto desde el Panel del programador de conectores (modificado como se indica en la sección anterior) y los dos archivos de icono.</span><span class="sxs-lookup"><span data-stu-id="b03bd-162">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="b03bd-163">Después de cargar la aplicación, abra la lista Conectores desde cualquier canal.</span><span class="sxs-lookup"><span data-stu-id="b03bd-163">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="b03bd-164">Desplácese hasta la parte inferior para ver la aplicación en la sección **Cargada**.</span><span class="sxs-lookup"><span data-stu-id="b03bd-164">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![Captura de pantalla de la sección cargada en el cuadro de diálogo Conector](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="b03bd-166">Ahora, puede iniciar la experiencia de configuración.</span><span class="sxs-lookup"><span data-stu-id="b03bd-166">You can now launch the configuration experience.</span></span> <span data-ttu-id="b03bd-167">Tenga en cuenta que este flujo se produce completamente en Microsoft Teams a través de una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="b03bd-167">Be aware that this flow occurs entirely within Microsoft Teams through a pop-up window.</span></span> <span data-ttu-id="b03bd-168">Actualmente, este comportamiento es distinto de la experiencia de configuración en Conectores que hemos creado; estamos trabajando para unificar las experiencias.</span><span class="sxs-lookup"><span data-stu-id="b03bd-168">Currently, this behavior differs from the configuration experience in Connectors that we created; we are working on unifying the experiences.</span></span>

<span data-ttu-id="b03bd-169">Para comprobar que una acción `HttpPOST` está funcionando correctamente, utilice el [webhook entrante personalizado](#setting-up-a-custom-incoming-webhook).</span><span class="sxs-lookup"><span data-stu-id="b03bd-169">To verify that an `HttpPOST` action is working correctly, use your [custom incoming webhook](#setting-up-a-custom-incoming-webhook).</span></span>


## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="b03bd-170">Limitación de velocidad para Conectores</span><span class="sxs-lookup"><span data-stu-id="b03bd-170">Rate limiting for Connectors</span></span>

<span data-ttu-id="b03bd-171">Este límite controla el tráfico que puede generar un conector o un webhook entrante en un canal.</span><span class="sxs-lookup"><span data-stu-id="b03bd-171">This limit controls the traffic that a connector or an incoming webhook is allowed to generate on a channel.</span></span> <span data-ttu-id="b03bd-172">Las solicitudes que realiza su webhook o conector se limitarán cuando se supere el umbral del límite de velocidad.</span><span class="sxs-lookup"><span data-stu-id="b03bd-172">Requests made by your webhook or connector will be throttled when the rate limit threshhold is exceeded.</span></span> <span data-ttu-id="b03bd-173">La cantidad de tiempo para el comportamiento de limitación se relaciona directamente con los parámetros de velocidad de solicitudes superada.</span><span class="sxs-lookup"><span data-stu-id="b03bd-173">The length of time for the throttling behavior is directly correlated to the exceeded request rate parameters.</span></span> <span data-ttu-id="b03bd-174">Por ejemplo, si un conector o webhook supera 100 solicitudes de mensajes en 3600 segundos, el conector se limitará durante los próximos 3600 segundos:</span><span class="sxs-lookup"><span data-stu-id="b03bd-174">For example, if a connector or webhook exceeds 100 message requests in 3600 seconds, the connector will be throttled for the next 3600 seconds:</span></span>

| <span data-ttu-id="b03bd-175">Período de tiempo: (seg.)</span><span class="sxs-lookup"><span data-stu-id="b03bd-175">Time-period (sec)</span></span>  | <span data-ttu-id="b03bd-176">Máximo de solicitudes de mensaje permitidas</span><span class="sxs-lookup"><span data-stu-id="b03bd-176">Max allowed message requests</span></span>  |
|---|---|
| <span data-ttu-id="b03bd-177">1</span><span class="sxs-lookup"><span data-stu-id="b03bd-177">1</span></span>   | <span data-ttu-id="b03bd-178">4</span><span class="sxs-lookup"><span data-stu-id="b03bd-178">4</span></span>  |  
| <span data-ttu-id="b03bd-179">30</span><span class="sxs-lookup"><span data-stu-id="b03bd-179">30</span></span>   | <span data-ttu-id="b03bd-180">60</span><span class="sxs-lookup"><span data-stu-id="b03bd-180">60</span></span>  |  
| <span data-ttu-id="b03bd-181">3600 (1 hora)</span><span class="sxs-lookup"><span data-stu-id="b03bd-181">3600 (1 hour)</span></span>  | <span data-ttu-id="b03bd-182">100</span><span class="sxs-lookup"><span data-stu-id="b03bd-182">100</span></span>  | 
| <span data-ttu-id="b03bd-183">7200</span><span class="sxs-lookup"><span data-stu-id="b03bd-183">7200</span></span> | <span data-ttu-id="b03bd-184">150</span><span class="sxs-lookup"><span data-stu-id="b03bd-184">150</span></span>  | 
| <span data-ttu-id="b03bd-185">86 400 (1 día)</span><span class="sxs-lookup"><span data-stu-id="b03bd-185">86400 (1 day)</span></span> | <span data-ttu-id="b03bd-186">1800</span><span class="sxs-lookup"><span data-stu-id="b03bd-186">1800</span></span>  | 

<span data-ttu-id="b03bd-187">Una [lógica de reintento con interrupción exponencial](/azure/architecture/patterns/retry) como la que se muestra a continuación mitigaría la restricción de velocidad en casos en que las solicitudes superen los límites en un segundo.</span><span class="sxs-lookup"><span data-stu-id="b03bd-187">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) like below would mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="b03bd-188">Siga los [procedimientos recomendados](../../bots/how-to/rate-limit.md#best-practices) para evitar alcanzar los límites de velocidad.</span><span class="sxs-lookup"><span data-stu-id="b03bd-188">Please follow [best practices](../../bots/how-to/rate-limit.md#best-practices) to avoid hitting the rate limits.</span></span>

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
 
<span data-ttu-id="b03bd-189">Estos límites tienen el propósito de reducir el correo no deseado en un canal con un conector y garantizan una experiencia óptima para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="b03bd-189">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to your end users.</span></span>
