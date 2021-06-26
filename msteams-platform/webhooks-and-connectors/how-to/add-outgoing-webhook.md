---
title: Crear un webhook saliente
author: laujan
description: describe cómo crear un webhook saliente
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
keywords: teams tabs outgoing webhook actionable message verify webhook
ms.openlocfilehash: c02ff5388e47ba40056afcc1fcf5e8d7ad4437e8
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140340"
---
# <a name="create-outgoing-webhook"></a><span data-ttu-id="0e507-104">Crear webhook saliente</span><span class="sxs-lookup"><span data-stu-id="0e507-104">Create Outgoing Webhook</span></span>

<span data-ttu-id="0e507-105">El webhook saliente actúa como bot y busca mensajes en canales mediante **@mention**.</span><span class="sxs-lookup"><span data-stu-id="0e507-105">The Outgoing Webhook acts as a bot and search for messages in channels using **@mention**.</span></span> <span data-ttu-id="0e507-106">Envía notificaciones a servicios web externos y responde con mensajes enriquecidos, que incluyen tarjetas e imágenes.</span><span class="sxs-lookup"><span data-stu-id="0e507-106">It sends notifications to external web services and responds with rich messages, which include cards and images.</span></span> <span data-ttu-id="0e507-107">Ayuda a omitir el proceso de creación de bots a través [del Microsoft Bot Framework](https://dev.botframework.com/).</span><span class="sxs-lookup"><span data-stu-id="0e507-107">It helps to skip the process of creating bots through the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span>

## <a name="key-features-of-outgoing-webhook"></a><span data-ttu-id="0e507-108">Características clave del webhook saliente</span><span class="sxs-lookup"><span data-stu-id="0e507-108">Key features of Outgoing Webhook</span></span>

<span data-ttu-id="0e507-109">En la tabla siguiente se proporcionan las características y la descripción de los webhooks salientes:</span><span class="sxs-lookup"><span data-stu-id="0e507-109">The following table provides the features and description of Outgoing Webhooks:</span></span>

| <span data-ttu-id="0e507-110">Características</span><span class="sxs-lookup"><span data-stu-id="0e507-110">Features</span></span> | <span data-ttu-id="0e507-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="0e507-111">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="0e507-112">Configuración con ámbito</span><span class="sxs-lookup"><span data-stu-id="0e507-112">Scoped configuration</span></span>| <span data-ttu-id="0e507-113">Los webhooks están en el ámbito del nivel de equipo.</span><span class="sxs-lookup"><span data-stu-id="0e507-113">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="0e507-114">El proceso de configuración obligatorio para cada uno agrega un webhook saliente.</span><span class="sxs-lookup"><span data-stu-id="0e507-114">Mandatory set up process for each adds an Outgoing Webhook.</span></span> |
| <span data-ttu-id="0e507-115">Mensajería reactiva</span><span class="sxs-lookup"><span data-stu-id="0e507-115">Reactive messaging</span></span>| <span data-ttu-id="0e507-116">Los usuarios deben usar @mention para que el webhook reciba mensajes.</span><span class="sxs-lookup"><span data-stu-id="0e507-116">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="0e507-117">Actualmente, los usuarios solo pueden enviar mensajes a un webhook saliente en canales públicos y no dentro del ámbito personal o privado.</span><span class="sxs-lookup"><span data-stu-id="0e507-117">Currently, users can only message an Outgoing Webhook in public channels and not within the personal or private scope.</span></span> |
|<span data-ttu-id="0e507-118">Intercambio de mensajes HTTP estándar</span><span class="sxs-lookup"><span data-stu-id="0e507-118">Standard HTTP message exchange</span></span>|<span data-ttu-id="0e507-119">Las respuestas aparecen en la misma cadena que el mensaje de solicitud original y pueden incluir cualquier contenido de mensaje de Bot Framework, por ejemplo, texto enriquecido, imágenes, tarjetas y emojis.</span><span class="sxs-lookup"><span data-stu-id="0e507-119">Responses appear in the same chain as the original request message and can include any Bot Framework message content, for example, rich text, images, cards, and emojis.</span></span> <span data-ttu-id="0e507-120">Aunque los webhooks salientes pueden usar tarjetas, no pueden usar ninguna acción de tarjeta excepto `openURL` para .</span><span class="sxs-lookup"><span data-stu-id="0e507-120">Although Outgoing Webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="0e507-121">Teams Compatibilidad con métodos api</span><span class="sxs-lookup"><span data-stu-id="0e507-121">Teams API method support</span></span>|<span data-ttu-id="0e507-122">Los webhooks salientes envían un HTTP POST a un servicio web y obtienen una respuesta.</span><span class="sxs-lookup"><span data-stu-id="0e507-122">Outgoing Webhooks sends an HTTP POST to a web service and gets a response.</span></span> <span data-ttu-id="0e507-123">No pueden tener acceso a otras API, como recuperar la lista o la lista de canales de un equipo.</span><span class="sxs-lookup"><span data-stu-id="0e507-123">They cannot access any other APIs, such as retrieve the roster or list of channels in a team.</span></span>|

## <a name="create-outgoing-webhooks"></a><span data-ttu-id="0e507-124">Crear webhooks salientes</span><span class="sxs-lookup"><span data-stu-id="0e507-124">Create Outgoing Webhooks</span></span>

<span data-ttu-id="0e507-125">Cree webhooks salientes y agregue bots personalizados a Teams.</span><span class="sxs-lookup"><span data-stu-id="0e507-125">Create Outgoing Webhooks and add custom bots to Teams.</span></span>

<span data-ttu-id="0e507-126">**Para crear un webhook saliente**</span><span class="sxs-lookup"><span data-stu-id="0e507-126">**To create an Outgoing Webhook**</span></span>

1. <span data-ttu-id="0e507-127">Seleccione **Teams** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="0e507-127">Select **Teams** from the left pane.</span></span> <span data-ttu-id="0e507-128">La **Teams** aparece:</span><span class="sxs-lookup"><span data-stu-id="0e507-128">The **Teams** page appears:</span></span>

    ![Canal de Teams](~/assets/images/teamschannel.png)

1. <span data-ttu-id="0e507-130">En la **Teams,** seleccione el equipo necesario para crear un webhook saliente y seleccione el &#8226;&#8226;&#8226;.</span><span class="sxs-lookup"><span data-stu-id="0e507-130">In the **Teams** page, select the required team to create an Outgoing Webhook and select the &#8226;&#8226;&#8226;.</span></span> <span data-ttu-id="0e507-131">En el menú desplegable, seleccione **Administrar equipo**:</span><span class="sxs-lookup"><span data-stu-id="0e507-131">In the dropdown menu, select **Manage team**:</span></span>

    ![Crear webhook saliente](~/assets/images/outgoingwebhook1.png)

1. <span data-ttu-id="0e507-133">Seleccione la **pestaña** Aplicaciones en la página del canal:</span><span class="sxs-lookup"><span data-stu-id="0e507-133">Select the **Apps** tab on the channel page:</span></span>

    ![Crear un webhook saliente](~/assets/images/outgoingwebhook2.png)

1. <span data-ttu-id="0e507-135">Seleccione **Crear un webhook saliente**:</span><span class="sxs-lookup"><span data-stu-id="0e507-135">Select **Create an Outgoing Webhook**:</span></span>

    ![Crear webhooks salientes](~/assets/images/outgoingwebhook3.png)

1. <span data-ttu-id="0e507-137">Escriba los siguientes detalles en la **página Crear un webhook** saliente:</span><span class="sxs-lookup"><span data-stu-id="0e507-137">Type the following details in the **Create an Outgoing Webhook** page:</span></span>

    * <span data-ttu-id="0e507-138">**Nombre:** el título del webhook y @mention pestaña.</span><span class="sxs-lookup"><span data-stu-id="0e507-138">**Name**: The webhook title and @mention tab.</span></span>
    * <span data-ttu-id="0e507-139">**Dirección URL de devolución** de llamada: el extremo HTTPS que acepta cargas JSON y recibe solicitudes POST de Teams.</span><span class="sxs-lookup"><span data-stu-id="0e507-139">**Callback URL**: The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams.</span></span>
    * <span data-ttu-id="0e507-140">**Descripción:** una cadena detallada que aparece en la tarjeta de perfil y en el panel de aplicaciones de nivel de equipo.</span><span class="sxs-lookup"><span data-stu-id="0e507-140">**Description**: A detailed string that appears in the profile card and the team-level App dashboard.</span></span>
    * <span data-ttu-id="0e507-141">**Imagen de** perfil: icono de aplicación para el webhook, que es opcional.</span><span class="sxs-lookup"><span data-stu-id="0e507-141">**Profile Picture**: An app icon for your webhook, which is optional.</span></span>

1. <span data-ttu-id="0e507-142">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0e507-142">Select **Create**.</span></span> <span data-ttu-id="0e507-143">El webhook saliente se agrega al canal del equipo actual:</span><span class="sxs-lookup"><span data-stu-id="0e507-143">The Outgoing Webhook is added to the current team's channel:</span></span>

    ![crear webhook saliente](~/assets/images/outgoingwebhook.png)

<span data-ttu-id="0e507-145">Aparece un cuadro de diálogo Código de autenticación de mensajes [(HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) basado en hash.</span><span class="sxs-lookup"><span data-stu-id="0e507-145">A [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) dialogue box appears.</span></span> <span data-ttu-id="0e507-146">Es un token de seguridad que se usa para autenticar llamadas entre Teams y el servicio externo designado.</span><span class="sxs-lookup"><span data-stu-id="0e507-146">It is a security token used to authenticate calls between Teams and the designated outside service.</span></span>

>[!NOTE]
> <span data-ttu-id="0e507-147">El webhook saliente está disponible para los usuarios del equipo, solo si la dirección URL es válida y los tokens de autenticación de servidor y cliente son iguales.</span><span class="sxs-lookup"><span data-stu-id="0e507-147">The Outgoing Webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal.</span></span> <span data-ttu-id="0e507-148">Por ejemplo, un protocolo de enlace HMAC.</span><span class="sxs-lookup"><span data-stu-id="0e507-148">For example, an HMAC handshake.</span></span>

<span data-ttu-id="0e507-149">En el siguiente escenario se proporcionan los detalles para agregar un webhook saliente:</span><span class="sxs-lookup"><span data-stu-id="0e507-149">The following scenario provides the details to add an Outgoing Webhook:</span></span>

* <span data-ttu-id="0e507-150">Escenario: insertar notificaciones de estado de cambio en un servidor Teams base de datos de canales a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e507-150">Scenario: Push change status notifications on a Teams channel database server to your app.</span></span>
* <span data-ttu-id="0e507-151">Ejemplo: tienes una línea de aplicación empresarial que realiza un seguimiento de todas las operaciones CRUD, como crear, leer, actualizar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="0e507-151">Example: You have a line of business app that tracks all CRUD operations, such as create, read, update, and delete.</span></span> <span data-ttu-id="0e507-152">Estas operaciones se realizan en los registros de los empleados Teams canal de recursos humanos en un Office 365 arrendamiento.</span><span class="sxs-lookup"><span data-stu-id="0e507-152">These operations are made to the employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

# <a name="url-json-payload"></a>[<span data-ttu-id="0e507-153">Carga JSON de dirección URL</span><span class="sxs-lookup"><span data-stu-id="0e507-153">URL JSON payload</span></span>](#tab/urljsonpayload)
<span data-ttu-id="0e507-154">**Crear una dirección URL en el servidor de la aplicación para aceptar y procesar una solicitud POST con una carga JSON**</span><span class="sxs-lookup"><span data-stu-id="0e507-154">**Create a URL on your app's server to accept and process a POST request with a JSON payload**</span></span>

<span data-ttu-id="0e507-155">El servicio recibe mensajes en un esquema de mensajería de servicio de bots de Azure estándar.</span><span class="sxs-lookup"><span data-stu-id="0e507-155">Your service receives messages in a standard Azure bot service messaging schema.</span></span> <span data-ttu-id="0e507-156">El conector de Bot Framework es un servicio RESTful que permite procesar el intercambio de mensajes con formato JSON a través de protocolos HTTPS, tal como se documenta en la API de servicio de [bots de Azure.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)</span><span class="sxs-lookup"><span data-stu-id="0e507-156">The Bot Framework connector is a RESTful service that empowers to process the interchange of JSON formatted messages through HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="0e507-157">Como alternativa, puede seguir el SDK de Microsoft Bot Framework para procesar y analizar mensajes.</span><span class="sxs-lookup"><span data-stu-id="0e507-157">Alternatively, you can follow the Microsoft Bot Framework SDK to process and parse messages.</span></span> <span data-ttu-id="0e507-158">Para obtener más información, vea [Overview of Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span><span class="sxs-lookup"><span data-stu-id="0e507-158">For more information, see [overview of Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span></span>

<span data-ttu-id="0e507-159">Los webhooks salientes están en el ámbito `team` del nivel y son visibles para todos los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="0e507-159">Outgoing Webhooks are scoped to the `team` level and are visible to all the team members.</span></span> <span data-ttu-id="0e507-160">Los usuarios deben **\@ mencionar** el nombre del webhook saliente para invocarlo en el canal.</span><span class="sxs-lookup"><span data-stu-id="0e507-160">Users need to **\@mention** the name of the Outgoing Webhook to invoke it in the channel.</span></span>

# <a name="verify-hmac-token"></a>[<span data-ttu-id="0e507-161">Comprobar token HMAC</span><span class="sxs-lookup"><span data-stu-id="0e507-161">Verify HMAC token</span></span>](#tab/verifyhmactoken)
<span data-ttu-id="0e507-162">**Crear un método para comprobar el token HMAC de webhook saliente**</span><span class="sxs-lookup"><span data-stu-id="0e507-162">**Create a method to verify the Outgoing Webhook HMAC token**</span></span>

<span data-ttu-id="0e507-163">Usando un ejemplo de mensaje entrante e identificador: "contoso" de SigningKeyDictionary de {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span><span class="sxs-lookup"><span data-stu-id="0e507-163">Using example of inbound message and ID: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="0e507-164">Use el valor "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" en la autorización del encabezado de solicitud.</span><span class="sxs-lookup"><span data-stu-id="0e507-164">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="0e507-165">Para asegurarse de que el servicio recibe llamadas solo de clientes Teams reales, Teams proporciona un código HMAC en el encabezado de autorización `hmac` HTTP.</span><span class="sxs-lookup"><span data-stu-id="0e507-165">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` authorization header.</span></span> <span data-ttu-id="0e507-166">Incluya siempre el código en el protocolo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="0e507-166">Always include the code in your authentication protocol.</span></span>

<span data-ttu-id="0e507-167">El código siempre debe validar la firma HMAC incluida en la solicitud de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="0e507-167">Your code must always validate the HMAC signature included in the request as follows:</span></span>

* <span data-ttu-id="0e507-168">Genere el token HMAC desde el cuerpo de la solicitud del mensaje.</span><span class="sxs-lookup"><span data-stu-id="0e507-168">Generate the HMAC token from the request body of the message.</span></span> <span data-ttu-id="0e507-169">Hay bibliotecas estándar para hacerlo en la mayoría de la plataforma, como [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) para Node.js y Teams [ejemplo de webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) para C \# ).</span><span class="sxs-lookup"><span data-stu-id="0e507-169">There are standard libraries to do this on most platform, such as [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js and [Teams webhook sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="0e507-170">Microsoft Teams usa criptografía HMAC estándar SHA256.</span><span class="sxs-lookup"><span data-stu-id="0e507-170">Microsoft Teams uses standard SHA256 HMAC cryptography.</span></span> <span data-ttu-id="0e507-171">Debe convertir el cuerpo en una matriz de bytes en UTF8.</span><span class="sxs-lookup"><span data-stu-id="0e507-171">You must convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="0e507-172">Calcule el hash de la matriz de bytes del token de seguridad proporcionado por Teams cuando registró el webhook saliente en el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="0e507-172">Compute the hash from the byte array of the security token provided by Teams when you registered the Outgoing Webhook in the Teams client.</span></span> <span data-ttu-id="0e507-173">Vea [crear un webhook saliente](#create-outgoing-webhook).</span><span class="sxs-lookup"><span data-stu-id="0e507-173">See [create an Outgoing Webhook](#create-outgoing-webhook).</span></span>
* <span data-ttu-id="0e507-174">Convertir el hash en una cadena mediante codificación UTF-8.</span><span class="sxs-lookup"><span data-stu-id="0e507-174">Convert the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="0e507-175">Compare el valor de cadena del hash generado con el valor proporcionado en la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="0e507-175">Compare the string value of the generated hash with the value provided in the HTTP request.</span></span>

# <a name="method-to-respond"></a>[<span data-ttu-id="0e507-176">Método para responder</span><span class="sxs-lookup"><span data-stu-id="0e507-176">Method to respond</span></span>](#tab/methodtorespond)
<span data-ttu-id="0e507-177">**Crear un método para enviar una respuesta correcta o de error**</span><span class="sxs-lookup"><span data-stu-id="0e507-177">**Create a method to send a success or failure response**</span></span>

<span data-ttu-id="0e507-178">Las respuestas de los webhooks salientes aparecen en la misma cadena de respuesta que el mensaje original.</span><span class="sxs-lookup"><span data-stu-id="0e507-178">Responses from your Outgoing Webhooks appear in the same reply chain as the original message.</span></span> <span data-ttu-id="0e507-179">Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica al servicio y el código obtiene cinco segundos para responder al mensaje antes de que la conexión finalice.</span><span class="sxs-lookup"><span data-stu-id="0e507-179">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="0e507-180">Ejemplo de respuesta</span><span class="sxs-lookup"><span data-stu-id="0e507-180">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```
---

> [!NOTE]
> * <span data-ttu-id="0e507-181">Puede enviar mensajes de texto, tarjetas de héroe y tarjeta adaptables como datos adjuntos con el webhook saliente.</span><span class="sxs-lookup"><span data-stu-id="0e507-181">You can send Adaptive Card, Hero card, and text messages as attachment with Outgoing Webhook.</span></span>
> * <span data-ttu-id="0e507-182">Las tarjetas admiten el formato.</span><span class="sxs-lookup"><span data-stu-id="0e507-182">Cards support formatting.</span></span> <span data-ttu-id="0e507-183">Para obtener más información, vea [format cards with markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).</span><span class="sxs-lookup"><span data-stu-id="0e507-183">For more information, see [format cards with markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).</span></span>

<span data-ttu-id="0e507-184">Los siguientes códigos son ejemplos de una respuesta de tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="0e507-184">Following codes are examples of an Adaptive Card response:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="0e507-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0e507-185">C#/.NET</span></span>](#tab/dotnet)

```csharp
string content = await this.Request.Content.ReadAsStringAsync();
Activity incomingActivity = JsonConvert.DeserializeObject<Activity>(content);

var Card = new AdaptiveCard(new AdaptiveSchemaVersion("1.4"))
{
    Body = new List<AdaptiveElement>()
    {
        new AdaptiveTextBlock(){Text= $"Request sent by: {incomingActivity.From.Name}"},
        new AdaptiveImage(){Url=new Uri("https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6")},
        new AdaptiveTextBlock(){Text="Sample image for Adaptive Card.."}
    }
};

var attachment = new Attachment()
{
    ContentType = AdaptiveCard.ContentType,
    Content = Card
};

var sampleResponseActivity = new Activity
{
    Attachments = new [] { attachment }
};

return sampleResponseActivity;
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="0e507-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="0e507-186">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
var receivedMsg = JSON.parse(payload);
var responseMsg = JSON.stringify({
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "contentUrl": null,
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: " + receivedMsg.from.name
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card."
                    }
                ]
            },
            "name": null,
            "thumbnailUrl": null
        }
    ]
});
```

# <a name="json"></a>[<span data-ttu-id="0e507-187">JSON</span><span class="sxs-lookup"><span data-stu-id="0e507-187">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: Megan"
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card.."
                    }
                ]
            }
        }
    ]
}
```

* * *

## <a name="code-sample"></a><span data-ttu-id="0e507-188">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="0e507-188">Code sample</span></span>

|<span data-ttu-id="0e507-189">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="0e507-189">**Sample name**</span></span> | <span data-ttu-id="0e507-190">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="0e507-190">**Description**</span></span> | <span data-ttu-id="0e507-191">**.NET**</span><span class="sxs-lookup"><span data-stu-id="0e507-191">**.NET**</span></span> | <span data-ttu-id="0e507-192">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="0e507-192">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="0e507-193">Webhooks salientes</span><span class="sxs-lookup"><span data-stu-id="0e507-193">Outgoing Webhooks</span></span> | <span data-ttu-id="0e507-194">Ejemplos para crear bots personalizados que se usarán en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0e507-194">Samples to create custom bots to be used in Microsoft Teams.</span></span>| [<span data-ttu-id="0e507-195">View</span><span class="sxs-lookup"><span data-stu-id="0e507-195">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [<span data-ttu-id="0e507-196">View</span><span class="sxs-lookup"><span data-stu-id="0e507-196">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="see-also"></a><span data-ttu-id="0e507-197">Vea también</span><span class="sxs-lookup"><span data-stu-id="0e507-197">See also</span></span>
* [<span data-ttu-id="0e507-198">Crear un webhook entrante</span><span class="sxs-lookup"><span data-stu-id="0e507-198">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="0e507-199">Crear un Conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="0e507-199">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="0e507-200">Crear y enviar mensajes</span><span class="sxs-lookup"><span data-stu-id="0e507-200">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
