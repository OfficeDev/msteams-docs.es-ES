---
title: Enviar y recibir archivos a través del bot
description: Describe cómo enviar y recibir archivos a través del bot
keywords: bots teams bots files send receive
ms.date: 05/20/2019
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 7d5ea3434b10d60e20574ca6d1935943c687f4d7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020943"
---
# <a name="send-and-receive-files-through-the-bot"></a><span data-ttu-id="6df7f-104">Enviar y recibir archivos a través del bot</span><span class="sxs-lookup"><span data-stu-id="6df7f-104">Send and receive files through the bot</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6df7f-105">Los artículos de este documento se basan en el SDK de Bot Framework de v4.</span><span class="sxs-lookup"><span data-stu-id="6df7f-105">The articles in this document are based on the v4 Bot Framework SDK.</span></span>

<span data-ttu-id="6df7f-106">Hay dos maneras de enviar y recibir archivos desde un bot:</span><span class="sxs-lookup"><span data-stu-id="6df7f-106">There are two ways to send files to and receive files from a bot:</span></span>

* <span data-ttu-id="6df7f-107">[**Use las API Graph Microsoft:**](#use-the-graph-apis) Este método funciona para bots en todos Microsoft Teams ámbitos:</span><span class="sxs-lookup"><span data-stu-id="6df7f-107">[**Use the Microsoft Graph APIs:**](#use-the-graph-apis) This method works for bots in all Microsoft Teams scopes:</span></span>
  * `personal`
  * `channel`
  * `groupchat`

* <span data-ttu-id="6df7f-108">[**Use las API Teams bot de Teams:**](#use-the-teams-bot-apis) Estos solo admiten archivos en `personal` contexto.</span><span class="sxs-lookup"><span data-stu-id="6df7f-108">[**Use the Teams bot APIs:**](#use-the-teams-bot-apis) These only support files in `personal` context.</span></span>

## <a name="use-the-graph-apis"></a><span data-ttu-id="6df7f-109">Usar las API Graph de datos</span><span class="sxs-lookup"><span data-stu-id="6df7f-109">Use the Graph APIs</span></span>

<span data-ttu-id="6df7f-110">Publique mensajes con datos adjuntos de tarjeta que hacen referencia a archivos SharePoint existentes, mediante las API de Graph para OneDrive [y SharePoint](/onedrive/developer/rest-api/).</span><span class="sxs-lookup"><span data-stu-id="6df7f-110">Post messages with card attachments that refer to existing SharePoint files, using the Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="6df7f-111">Para usar las API Graph, obtenga acceso a cualquiera de las siguientes opciones a través del flujo de autorización estándar de OAuth 2.0:</span><span class="sxs-lookup"><span data-stu-id="6df7f-111">To use the Graph APIs, obtain access to either of the following through the standard OAuth 2.0 authorization flow:</span></span>

* <span data-ttu-id="6df7f-112">Carpeta de OneDrive y archivos `personal` de `groupchat` un usuario.</span><span class="sxs-lookup"><span data-stu-id="6df7f-112">A user's OneDrive folder for `personal` and `groupchat` files.</span></span>
* <span data-ttu-id="6df7f-113">Los archivos del canal de un equipo para `channel` los archivos.</span><span class="sxs-lookup"><span data-stu-id="6df7f-113">The files in a team's channel for `channel` files.</span></span>

<span data-ttu-id="6df7f-114">Graph Las API funcionan en todos Teams ámbitos.</span><span class="sxs-lookup"><span data-stu-id="6df7f-114">Graph APIs work in all Teams scopes.</span></span> <span data-ttu-id="6df7f-115">Para obtener más información, vea [Enviar datos adjuntos de archivos de mensajes de chat.](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="6df7f-115">For more information, see [send chat message file attachments](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true).</span></span>

<span data-ttu-id="6df7f-116">Como alternativa, puede enviar archivos a y recibir archivos de un bot mediante las API Teams bot.</span><span class="sxs-lookup"><span data-stu-id="6df7f-116">Alternately, you can send files to and receive files from a bot using the Teams bot APIs.</span></span>

## <a name="use-the-teams-bot-apis"></a><span data-ttu-id="6df7f-117">Usar las API Teams bot</span><span class="sxs-lookup"><span data-stu-id="6df7f-117">Use the Teams bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="6df7f-118">Teams API de bot solo funcionan en el `personal` contexto.</span><span class="sxs-lookup"><span data-stu-id="6df7f-118">Teams bot APIs work only in the `personal` context.</span></span> <span data-ttu-id="6df7f-119">No funcionan en el `channel` contexto `groupchat` o.</span><span class="sxs-lookup"><span data-stu-id="6df7f-119">They do not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="6df7f-120">Con Teams API, el bot puede enviar y recibir directamente archivos con usuarios en el contexto, también conocido `personal` como chats personales.</span><span class="sxs-lookup"><span data-stu-id="6df7f-120">Using Teams APIs, the bot can directly send and receive files with users in the `personal` context, also known as personal chats.</span></span> <span data-ttu-id="6df7f-121">Implemente características, como informes de gastos, reconocimiento de imágenes, archivo de archivo y firmas electrónicas que impliquen la edición del contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="6df7f-121">Implement features, such as expense reporting, image recognition, file archival, and e-signatures involving the editing of file content.</span></span> <span data-ttu-id="6df7f-122">Los archivos compartidos Teams suelen aparecer como tarjetas y permiten la visualización enriquecte desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6df7f-122">Files shared in Teams typically appear as cards and allow rich in-app viewing.</span></span>

<span data-ttu-id="6df7f-123">En las secciones siguientes se describe cómo enviar contenido de archivo como interacción directa del usuario, como enviar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="6df7f-123">The next sections describe how to send file content as direct user interaction, like sending a message.</span></span> <span data-ttu-id="6df7f-124">Esta API se proporciona como parte de la plataforma Teams bot.</span><span class="sxs-lookup"><span data-stu-id="6df7f-124">This API is provided as part of the Teams bot platform.</span></span>

### <a name="configure-the-bot-to-support-files"></a><span data-ttu-id="6df7f-125">Configurar el bot para admitir archivos</span><span class="sxs-lookup"><span data-stu-id="6df7f-125">Configure the bot to support files</span></span>

<span data-ttu-id="6df7f-126">Para enviar y recibir archivos en el bot, establezca la `supportsFiles` propiedad del manifiesto en `true` .</span><span class="sxs-lookup"><span data-stu-id="6df7f-126">To send and receive files in the bot, set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="6df7f-127">Esta propiedad se describe en la [sección bots](~/resources/schema/manifest-schema.md#bots) de la referencia manifest.</span><span class="sxs-lookup"><span data-stu-id="6df7f-127">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="6df7f-128">La definición tiene este aspecto, `"supportsFiles": true` .</span><span class="sxs-lookup"><span data-stu-id="6df7f-128">The definition looks like this, `"supportsFiles": true`.</span></span> <span data-ttu-id="6df7f-129">Si el bot no habilita `supportsFiles` , las características enumeradas en esta sección no funcionan.</span><span class="sxs-lookup"><span data-stu-id="6df7f-129">If the bot does not enable `supportsFiles`, the features listed in this section do not work.</span></span>

### <a name="receive-files-in-personal-chat"></a><span data-ttu-id="6df7f-130">Recibir archivos en chat personal</span><span class="sxs-lookup"><span data-stu-id="6df7f-130">Receive files in personal chat</span></span>

<span data-ttu-id="6df7f-131">Cuando un usuario envía un archivo al bot, el archivo se carga por primera vez en el OneDrive de almacenamiento empresarial del usuario.</span><span class="sxs-lookup"><span data-stu-id="6df7f-131">When a user sends a file to the bot, the file is first uploaded to the user's OneDrive for business storage.</span></span> <span data-ttu-id="6df7f-132">A continuación, el bot recibe una actividad de mensaje que notifica al usuario sobre la carga del usuario.</span><span class="sxs-lookup"><span data-stu-id="6df7f-132">The bot then receives a message activity notifying the user about the user upload.</span></span> <span data-ttu-id="6df7f-133">La actividad contiene metadatos de archivo, como su nombre y la dirección URL de contenido.</span><span class="sxs-lookup"><span data-stu-id="6df7f-133">The activity contains file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="6df7f-134">El usuario puede leer directamente desde esta dirección URL para capturar su contenido binario.</span><span class="sxs-lookup"><span data-stu-id="6df7f-134">The user can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="6df7f-135">Ejemplo de actividad de mensaje con datos adjuntos de archivo</span><span class="sxs-lookup"><span data-stu-id="6df7f-135">Message activity with file attachment example</span></span>

<span data-ttu-id="6df7f-136">El siguiente código muestra un ejemplo de actividad de mensaje con datos adjuntos de archivo:</span><span class="sxs-lookup"><span data-stu-id="6df7f-136">The following code shows an example of message activity with file attachment:</span></span>

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.file.download.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "downloadUrl" : "https://download.link",
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C9D",
      "fileType": "txt",
      "etag": "123"
    }
  }]
}
```

<span data-ttu-id="6df7f-137">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="6df7f-137">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="6df7f-138">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6df7f-138">Property</span></span> | <span data-ttu-id="6df7f-139">Objetivo</span><span class="sxs-lookup"><span data-stu-id="6df7f-139">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="6df7f-140">OneDrive Dirección URL para capturar el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="6df7f-140">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="6df7f-141">El usuario puede emitir una `HTTP GET` directamente desde esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="6df7f-141">The user can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="6df7f-142">Identificador de archivo único.</span><span class="sxs-lookup"><span data-stu-id="6df7f-142">Unique file ID.</span></span> <span data-ttu-id="6df7f-143">Este es el identificador OneDrive elemento de unidad de disco, en caso de que el usuario envíe un archivo al bot.</span><span class="sxs-lookup"><span data-stu-id="6df7f-143">This is the OneDrive drive item ID, in case the user sends a file to the bot.</span></span> |
| `fileType` | <span data-ttu-id="6df7f-144">Tipo de archivo, como .pdf o .docx.</span><span class="sxs-lookup"><span data-stu-id="6df7f-144">Type of file, such as .pdf or .docx.</span></span> |

<span data-ttu-id="6df7f-145">Como práctica recomendada, confirme la carga del archivo enviando un mensaje de vuelta al usuario.</span><span class="sxs-lookup"><span data-stu-id="6df7f-145">As a best practice, acknowledge the file upload by sending a message back to the user.</span></span>

### <a name="upload-files-to-personal-chat"></a><span data-ttu-id="6df7f-146">Upload archivos al chat personal</span><span class="sxs-lookup"><span data-stu-id="6df7f-146">Upload files to personal chat</span></span>

<span data-ttu-id="6df7f-147">**Para cargar un archivo a un usuario**</span><span class="sxs-lookup"><span data-stu-id="6df7f-147">**To upload a file to a user**</span></span>

1. <span data-ttu-id="6df7f-148">Enviar un mensaje al usuario que solicita permiso para escribir el archivo.</span><span class="sxs-lookup"><span data-stu-id="6df7f-148">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="6df7f-149">Este mensaje debe contener `FileConsentCard` datos adjuntos con el nombre del archivo que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="6df7f-149">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="6df7f-150">Si el usuario acepta la descarga de archivos, el bot recibe una actividad de invocación con una dirección URL de ubicación.</span><span class="sxs-lookup"><span data-stu-id="6df7f-150">If the user accepts the file download, the bot receives an invoke activity with a location URL.</span></span>
3. <span data-ttu-id="6df7f-151">Para transferir el archivo, el bot realiza una `HTTP POST` operación directamente en la dirección URL de ubicación proporcionada.</span><span class="sxs-lookup"><span data-stu-id="6df7f-151">To transfer the file, the bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="6df7f-152">Opcionalmente, quite la tarjeta de consentimiento original si no desea que el usuario acepte más cargas del mismo archivo.</span><span class="sxs-lookup"><span data-stu-id="6df7f-152">Optionally, remove the original consent card if you do not want the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="6df7f-153">Mensaje que solicita permiso para cargar</span><span class="sxs-lookup"><span data-stu-id="6df7f-153">Message requesting permission to upload</span></span>

<span data-ttu-id="6df7f-154">El siguiente mensaje de escritorio contiene un objeto de datos adjuntos sencillo que solicita permiso al usuario para cargar el archivo:</span><span class="sxs-lookup"><span data-stu-id="6df7f-154">The following desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![Tarjeta de consentimiento que solicita permiso de usuario para cargar archivo](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="6df7f-156">El siguiente mensaje móvil contiene un objeto attachment que solicita permiso al usuario para cargar el archivo:</span><span class="sxs-lookup"><span data-stu-id="6df7f-156">The following mobile message contains an attachment object requesting user permission to upload the file:</span></span>

<img src="../../assets/images/bots/mobile-bot-file-consent-card.png" alt="Consent card requesting user permission to upload file on mobile" width="350"/>

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.consent",
    "name": "file_example.txt",
    "content": {
      "description": "<Purpose of the file, such as: this is your monthly expense report>",
      "sizeInBytes": 1029393,
      "acceptContext": {
      },
      "declineContext": {
      }
    }
  }]
}
```

<span data-ttu-id="6df7f-157">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="6df7f-157">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="6df7f-158">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6df7f-158">Property</span></span> | <span data-ttu-id="6df7f-159">Objetivo</span><span class="sxs-lookup"><span data-stu-id="6df7f-159">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="6df7f-160">Describe el propósito del archivo o resume su contenido.</span><span class="sxs-lookup"><span data-stu-id="6df7f-160">Describes the purpose of the file or summarizes its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="6df7f-161">Proporciona al usuario una estimación del tamaño del archivo y la cantidad de espacio que ocupa OneDrive.</span><span class="sxs-lookup"><span data-stu-id="6df7f-161">Provides the user an estimate of the file size and the amount of space it takes in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="6df7f-162">Contexto adicional que se transmite silenciosamente al bot cuando el usuario acepta el archivo.</span><span class="sxs-lookup"><span data-stu-id="6df7f-162">Additional context that is silently transmitted to the bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="6df7f-163">Contexto adicional que se transmite silenciosamente al bot cuando el usuario rechaza el archivo.</span><span class="sxs-lookup"><span data-stu-id="6df7f-163">Additional context that is silently transmitted to the bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="6df7f-164">Invocar actividad cuando el usuario acepta el archivo</span><span class="sxs-lookup"><span data-stu-id="6df7f-164">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="6df7f-165">Se envía una actividad de invocación al bot si el usuario acepta el archivo y cuándo lo acepta.</span><span class="sxs-lookup"><span data-stu-id="6df7f-165">An invoke activity is sent to the bot if and when the user accepts the file.</span></span> <span data-ttu-id="6df7f-166">Contiene la dirección URL OneDrive para la Empresa marcador de posición que el bot puede emitir para `PUT` transferir el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="6df7f-166">It contains the OneDrive for Business placeholder URL that the bot can then issue a `PUT` to transfer the file contents.</span></span> <span data-ttu-id="6df7f-167">Para obtener información sobre la carga en la dirección URL OneDrive, vea [upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span><span class="sxs-lookup"><span data-stu-id="6df7f-167">For information on uploading to the OneDrive URL, see [upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="6df7f-168">El código siguiente muestra un ejemplo de una versión concisa de la actividad de invocación que recibe el bot:</span><span class="sxs-lookup"><span data-stu-id="6df7f-168">The following code shows an example of a concise version of the invoke activity that the bot receives:</span></span>

```json
{
  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "accept",
    "context": {
    },
    "uploadInfo": {
      "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
      "name": "file_example.txt",
      "uploadUrl": "https://upload.link",
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C8C",
      "fileType": "txt",
      "etag": "123"
    }
  }
}
```

<span data-ttu-id="6df7f-169">Del mismo modo, si el usuario rechaza el archivo, el bot recibe el siguiente evento con el mismo nombre de actividad general:</span><span class="sxs-lookup"><span data-stu-id="6df7f-169">Similarly, if the user declines the file, the bot receives the following event with the same overall activity name:</span></span>

```json
{
  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "decline",
    "context": {
    }
  }
}
```

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="6df7f-170">Notificar al usuario acerca de un archivo cargado</span><span class="sxs-lookup"><span data-stu-id="6df7f-170">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="6df7f-171">Después de cargar un archivo en el OneDrive usuario, envíe un mensaje de confirmación al usuario.</span><span class="sxs-lookup"><span data-stu-id="6df7f-171">After uploading a file to the user's OneDrive, send a confirmation message to the user.</span></span> <span data-ttu-id="6df7f-172">El mensaje debe contener los siguientes datos adjuntos que el usuario puede seleccionar, ya sea para obtener una vista previa o abrirla en `FileCard` OneDrive o descargar localmente:</span><span class="sxs-lookup"><span data-stu-id="6df7f-172">The message must contain the following `FileCard` attachment that the user can select, either to preview or open it in OneDrive, or download locally:</span></span>

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C8C",
      "fileType": "txt",
    }
  }]
}
```

<span data-ttu-id="6df7f-173">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="6df7f-173">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="6df7f-174">Propiedad</span><span class="sxs-lookup"><span data-stu-id="6df7f-174">Property</span></span> | <span data-ttu-id="6df7f-175">Objetivo</span><span class="sxs-lookup"><span data-stu-id="6df7f-175">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="6df7f-176">OneDrive o SharePoint de elemento de unidad.</span><span class="sxs-lookup"><span data-stu-id="6df7f-176">OneDrive or SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="6df7f-177">Tipo de archivo, como .pdf o .docx.</span><span class="sxs-lookup"><span data-stu-id="6df7f-177">Type of file, such as .pdf or .docx.</span></span> |

### <a name="fetch-inline-images-from-message"></a><span data-ttu-id="6df7f-178">Capturar imágenes en línea del mensaje</span><span class="sxs-lookup"><span data-stu-id="6df7f-178">Fetch inline images from message</span></span>

<span data-ttu-id="6df7f-179">Capturar imágenes en línea que forman parte del mensaje mediante el token de acceso del bot.</span><span class="sxs-lookup"><span data-stu-id="6df7f-179">Fetch inline images that are part of the message using the Bot's access token.</span></span>

![Imagen en línea](../../assets/images/bots/inline-image.png)

<span data-ttu-id="6df7f-181">El siguiente código muestra un ejemplo de captura de imágenes en línea desde el mensaje:</span><span class="sxs-lookup"><span data-stu-id="6df7f-181">The following code shows an example of fetching inline images from message:</span></span>

```csharp
private async Task ProcessInlineImage(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var attachment = turnContext.Activity.Attachments[0];
    var client = _clientFactory.CreateClient();
    // Get Bot's access token to fetch inline image. 
    var token = await new MicrosoftAppCredentials(microsoftAppId, microsoftAppPassword).GetTokenAsync();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    var responseMessage = await client.GetAsync(attachment.ContentUrl);
    // Save the inline image to Files directory.
    var filePath = Path.Combine("Files", "ImageFromUser.png");
    using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
    {
        await responseMessage.Content.CopyToAsync(fileStream);
    }
    // Create reply with image.
    var reply = MessageFactory.Text($"Attachment of {attachment.ContentType} type and size of {responseMessage.Content.Headers.ContentLength} bytes received.");
    reply.Attachments = new List<Attachment>() { 
        GetInlineAttachment() 
    };
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
private static Attachment GetInlineAttachment()
{
    var imagePath = Path.Combine("Files", "ImageFromUser.png");
    var imageData = Convert.ToBase64String(File.ReadAllBytes(imagePath));
    return new Attachment
    {
        Name = @"ImageFromUser.png",
        ContentType = "image/png",
        ContentUrl = $"data:image/png;base64,{imageData}",
    };
}
```

### <a name="basic-example-in-c"></a><span data-ttu-id="6df7f-182">Ejemplo básico en C #</span><span class="sxs-lookup"><span data-stu-id="6df7f-182">Basic example in C#</span></span>

<span data-ttu-id="6df7f-183">El siguiente código muestra un ejemplo de cómo controlar las cargas de archivos y enviar solicitudes de consentimiento de archivos en el cuadro de diálogo del bot:</span><span class="sxs-lookup"><span data-stu-id="6df7f-183">The following code shows an example of how to handle file uploads and send file consent requests in the bot's dialog:</span></span>

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    if (turnContext.Activity.Attachments?[0].ContentType.Contains("image/*") == true)
    {
        // Inline image.
        await ProcessInlineImage(turnContext, cancellationToken);
    }
    else
    {
        string filename = "teams-logo.png";
        string filePath = Path.Combine("Files", filename);
        long fileSize = new FileInfo(filePath).Length;
        await SendFileCardAsync(turnContext, filename, fileSize, cancellationToken);
    }
}
private async Task ProcessInlineImage(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var attachment = turnContext.Activity.Attachments[0];
    var client = _clientFactory.CreateClient();
    // Get Bot's access token to fetch inline image. 
    var token = await new MicrosoftAppCredentials(microsoftAppId, microsoftAppPassword).GetTokenAsync();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    var responseMessage = await client.GetAsync(attachment.ContentUrl);
    // Save the inline image to Files directory.
    var filePath = Path.Combine("Files", "ImageFromUser.png");
    using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
    {
        await responseMessage.Content.CopyToAsync(fileStream);
    }
    // Create reply with image.
    var reply = MessageFactory.Text($"Attachment of {attachment.ContentType} type and size of {responseMessage.Content.Headers.ContentLength} bytes received.");
    reply.Attachments = new List<Attachment>() { GetInlineAttachment() };
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
private static Attachment GetInlineAttachment()
{
    var imagePath = Path.Combine("Files", "ImageFromUser.png");
    var imageData = Convert.ToBase64String(File.ReadAllBytes(imagePath));
    return new Attachment
    {
        Name = @"ImageFromUser.png",
        ContentType = "image/png",
        ContentUrl = $"data:image/png;base64,{imageData}",
    };
}
private async Task SendFileCardAsync(ITurnContext turnContext, string filename, long filesize, CancellationToken cancellationToken)
{
    var consentContext = new Dictionary<string, string>
    {
        { 
            "filename", filename 
        },
    };
    var fileCard = new FileConsentCard
    {
        Description = "This is the file I want to send you",
        SizeInBytes = filesize,
        AcceptContext = consentContext,
        DeclineContext = consentContext,
    };
    var asAttachment = new Attachment
    {
        Content = fileCard,
        ContentType = FileConsentCard.ContentType,
        Name = filename,
    };
    var replyActivity = turnContext.Activity.CreateReply();
    replyActivity.Attachments = new List<Attachment>() { asAttachment };
    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

## <a name="code-sample"></a><span data-ttu-id="6df7f-184">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="6df7f-184">Code sample</span></span>

<span data-ttu-id="6df7f-185">En el ejemplo de código siguiente se muestra cómo obtener el consentimiento del archivo y cargar archivos Teams desde un bot:</span><span class="sxs-lookup"><span data-stu-id="6df7f-185">The following code sample demonstrates how to obtain file consent and upload files to Teams from a bot:</span></span>

|<span data-ttu-id="6df7f-186">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="6df7f-186">**Sample name**</span></span> | <span data-ttu-id="6df7f-187">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="6df7f-187">**Description**</span></span> | <span data-ttu-id="6df7f-188">**.NET**</span><span class="sxs-lookup"><span data-stu-id="6df7f-188">**.NET**</span></span> | <span data-ttu-id="6df7f-189">**Javascript**</span><span class="sxs-lookup"><span data-stu-id="6df7f-189">**Javascript**</span></span> | <span data-ttu-id="6df7f-190">**Python**</span><span class="sxs-lookup"><span data-stu-id="6df7f-190">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="6df7f-191">File upload</span><span class="sxs-lookup"><span data-stu-id="6df7f-191">File upload</span></span> | <span data-ttu-id="6df7f-192">Muestra cómo obtener el consentimiento de archivos y cargar archivos a Teams desde un bot.</span><span class="sxs-lookup"><span data-stu-id="6df7f-192">Demonstrates how to obtain file consent and upload files to Teams from a bot.</span></span> <span data-ttu-id="6df7f-193">Además, cómo recibir un archivo enviado a un bot.</span><span class="sxs-lookup"><span data-stu-id="6df7f-193">Also, how to receive a file sent to a bot.</span></span> | [<span data-ttu-id="6df7f-194">View</span><span class="sxs-lookup"><span data-stu-id="6df7f-194">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [<span data-ttu-id="6df7f-195">View</span><span class="sxs-lookup"><span data-stu-id="6df7f-195">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [<span data-ttu-id="6df7f-196">View</span><span class="sxs-lookup"><span data-stu-id="6df7f-196">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |

## <a name="next-step"></a><span data-ttu-id="6df7f-197">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="6df7f-197">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6df7f-198">Optimizar un bot con la limitación de volumen en Teams</span><span class="sxs-lookup"><span data-stu-id="6df7f-198">Optimize your bot with rate limiting in Teams</span></span>](~/bots/how-to/rate-limit.md)
