---
title: Enviar y recibir archivos a través del bot
description: Describe cómo enviar y recibir archivos a través del bot
keywords: recibir los archivos de bots de teams
ms.date: 05/20/2019
ms.topic: how-to
ms.openlocfilehash: 1699b9339bd6a49194240130d16795e8febcb76e
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037059"
---
# <a name="send-and-receive-files-through-the-bot"></a><span data-ttu-id="95c67-104">Enviar y recibir archivos a través del bot</span><span class="sxs-lookup"><span data-stu-id="95c67-104">Send and receive files through the bot</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95c67-105">Los artículos de este documento se basan en el SDK de Bot Framework v4.</span><span class="sxs-lookup"><span data-stu-id="95c67-105">The articles in this document are based on the v4 Bot Framework SDK.</span></span>

<span data-ttu-id="95c67-106">Hay dos formas de enviar y recibir archivos desde un bot:</span><span class="sxs-lookup"><span data-stu-id="95c67-106">There are two ways to send files to and receive files from a bot:</span></span>

* <span data-ttu-id="95c67-107">**Uso de las API de Microsoft Graph:** Este método funciona para bots en todos los ámbitos de Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="95c67-107">**Using the Microsoft Graph APIs:** This method works for bots in all Microsoft Teams scopes:</span></span>
  * `personal`
  * `channel`
  * `groupchat`

* <span data-ttu-id="95c67-108">**Uso de las API de bot de Teams:** Estos solo admiten archivos en `personal` contexto.</span><span class="sxs-lookup"><span data-stu-id="95c67-108">**Using the Teams bot APIs:** These only support files in `personal` context.</span></span>

## <a name="using-the-graph-apis"></a><span data-ttu-id="95c67-109">Uso de las API de Graph</span><span class="sxs-lookup"><span data-stu-id="95c67-109">Using the Graph APIs</span></span>

<span data-ttu-id="95c67-110">Publique mensajes con datos adjuntos de tarjeta que hacen referencia a archivos de SharePoint existentes, con las API de Graph para [OneDrive y SharePoint.](/onedrive/developer/rest-api/)</span><span class="sxs-lookup"><span data-stu-id="95c67-110">Post messages with card attachments that refer to existing SharePoint files, using the Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="95c67-111">Para usar las API de Graph, obtenga acceso a cualquiera de las siguientes opciones a través del flujo de autorización estándar de OAuth 2.0:</span><span class="sxs-lookup"><span data-stu-id="95c67-111">To use the Graph APIs, obtain access to either of the following through the standard OAuth 2.0 authorization flow:</span></span>
* <span data-ttu-id="95c67-112">Carpeta de OneDrive de un usuario y `personal` `groupchat` archivos.</span><span class="sxs-lookup"><span data-stu-id="95c67-112">A user's OneDrive folder for `personal` and `groupchat` files.</span></span>
* <span data-ttu-id="95c67-113">Los archivos del canal de un equipo para `channel` los archivos.</span><span class="sxs-lookup"><span data-stu-id="95c67-113">The files in a team's channel for `channel` files.</span></span>

<span data-ttu-id="95c67-114">Las API de Graph funcionan en todos los ámbitos de Teams.</span><span class="sxs-lookup"><span data-stu-id="95c67-114">Graph APIs work in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="95c67-115">Uso de las API de bot de Teams</span><span class="sxs-lookup"><span data-stu-id="95c67-115">Using the Teams bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="95c67-116">Las API de bot de Teams solo funcionan en el `personal` contexto.</span><span class="sxs-lookup"><span data-stu-id="95c67-116">Teams bot APIs work only in the `personal` context.</span></span> <span data-ttu-id="95c67-117">No funcionan en el `channel` contexto o en el `groupchat` contexto.</span><span class="sxs-lookup"><span data-stu-id="95c67-117">They do not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="95c67-118">Con las API de Teams, el bot puede enviar y recibir directamente archivos con usuarios en el contexto, también conocido `personal` como chats personales.</span><span class="sxs-lookup"><span data-stu-id="95c67-118">Using Teams APIs, the bot can directly send and receive files with users in the `personal` context, also known as personal chats.</span></span> <span data-ttu-id="95c67-119">Implementar características, como informes de gastos, reconocimiento de imágenes, archivado de archivos y firmas electrónicas que impliquen la edición del contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="95c67-119">Implement features, such as expense reporting, image recognition, file archival, and e-signatures involving the editing of file content.</span></span> <span data-ttu-id="95c67-120">Los archivos compartidos en Teams suelen aparecer como tarjetas y permiten la visualización enriquezca en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95c67-120">Files shared in Teams typically appear as cards and allow rich in-app viewing.</span></span>

<span data-ttu-id="95c67-121">En las secciones siguientes se describe cómo enviar contenido de archivos como una interacción directa del usuario, como enviar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="95c67-121">The following sections describe how to send file content as a direct user interaction, like sending a message.</span></span> <span data-ttu-id="95c67-122">Esta API se proporciona como parte de la plataforma de bots de Teams.</span><span class="sxs-lookup"><span data-stu-id="95c67-122">This API is provided as part of the Teams bot platform.</span></span>

### <a name="configuring-the-bot-to-support-files"></a><span data-ttu-id="95c67-123">Configuración del bot para admitir archivos</span><span class="sxs-lookup"><span data-stu-id="95c67-123">Configuring the bot to support files</span></span>

<span data-ttu-id="95c67-124">Para enviar y recibir archivos en el bot, establezca la `supportsFiles` propiedad en el manifiesto en `true` .</span><span class="sxs-lookup"><span data-stu-id="95c67-124">To send and receive files in the bot, set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="95c67-125">Esta propiedad se describe en la [sección bots](~/resources/schema/manifest-schema.md#bots) de la referencia de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="95c67-125">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="95c67-126">La definición tiene este `"supportsFiles": true` aspecto.</span><span class="sxs-lookup"><span data-stu-id="95c67-126">The definition looks like this, `"supportsFiles": true`.</span></span> <span data-ttu-id="95c67-127">Si el bot no lo habilita, las características que se `supportsFiles` enumeran en esta sección no funcionan.</span><span class="sxs-lookup"><span data-stu-id="95c67-127">If the bot does not enable `supportsFiles`, the features listed in this section do not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="95c67-128">Recepción de archivos en chat personal</span><span class="sxs-lookup"><span data-stu-id="95c67-128">Receiving files in personal chat</span></span>

<span data-ttu-id="95c67-129">Cuando un usuario envía un archivo al bot, el archivo se carga primero en el almacenamiento de OneDrive para la Empresa del usuario.</span><span class="sxs-lookup"><span data-stu-id="95c67-129">When a user sends a file to the bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="95c67-130">A continuación, el bot recibe una actividad de mensaje que notifica al usuario sobre la carga del usuario.</span><span class="sxs-lookup"><span data-stu-id="95c67-130">The bot then receives a message activity notifying the user about the user upload.</span></span> <span data-ttu-id="95c67-131">La actividad contiene metadatos de archivo, como su nombre y la dirección URL de contenido.</span><span class="sxs-lookup"><span data-stu-id="95c67-131">The activity contains file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="95c67-132">El usuario puede leer directamente desde esta dirección URL para capturar su contenido binario.</span><span class="sxs-lookup"><span data-stu-id="95c67-132">The user can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="95c67-133">Ejemplo de actividad de mensajes con datos adjuntos de archivo</span><span class="sxs-lookup"><span data-stu-id="95c67-133">Message activity with file attachment example</span></span>

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

<span data-ttu-id="95c67-134">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="95c67-134">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="95c67-135">Propiedad</span><span class="sxs-lookup"><span data-stu-id="95c67-135">Property</span></span> | <span data-ttu-id="95c67-136">Finalidad</span><span class="sxs-lookup"><span data-stu-id="95c67-136">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="95c67-137">Dirección URL de OneDrive para capturar el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="95c67-137">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="95c67-138">El usuario puede emitir una `HTTP GET` directamente desde esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="95c67-138">The user can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="95c67-139">Identificador de archivo único.</span><span class="sxs-lookup"><span data-stu-id="95c67-139">Unique file ID.</span></span> <span data-ttu-id="95c67-140">Este es el identificador de elemento de unidad de OneDrive, en caso de que el usuario envíe un archivo al bot.</span><span class="sxs-lookup"><span data-stu-id="95c67-140">This is the OneDrive drive item ID, in case the user sends a file to the bot.</span></span> |
| `fileType` | <span data-ttu-id="95c67-141">Tipo de archivo, como .pdf o .docx.</span><span class="sxs-lookup"><span data-stu-id="95c67-141">Type of file, such as .pdf or .docx.</span></span> |

<span data-ttu-id="95c67-142">Como procedimiento recomendado, confirme la carga de archivos enviando un mensaje al usuario.</span><span class="sxs-lookup"><span data-stu-id="95c67-142">As a best practice, acknowledge the file upload by sending a message back to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="95c67-143">Cargar archivos en un chat personal</span><span class="sxs-lookup"><span data-stu-id="95c67-143">Uploading files to personal chat</span></span>

<span data-ttu-id="95c67-144">Se requieren los siguientes pasos para cargar un archivo a un usuario:</span><span class="sxs-lookup"><span data-stu-id="95c67-144">The following steps are required to upload a file to a user:</span></span>

1. <span data-ttu-id="95c67-145">Envíe un mensaje al usuario que solicita permiso para escribir el archivo.</span><span class="sxs-lookup"><span data-stu-id="95c67-145">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="95c67-146">Este mensaje debe contener datos `FileConsentCard` adjuntos con el nombre del archivo que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="95c67-146">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="95c67-147">Si el usuario acepta la descarga de archivos, el bot recibe una actividad de invocación con una dirección URL de ubicación.</span><span class="sxs-lookup"><span data-stu-id="95c67-147">If the user accepts the file download, the bot receives an invoke activity with a location URL.</span></span>
3. <span data-ttu-id="95c67-148">Para transferir el archivo, el bot realiza una operación `HTTP POST` directamente en la dirección URL de ubicación proporcionada.</span><span class="sxs-lookup"><span data-stu-id="95c67-148">To transfer the file, the bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="95c67-149">Opcionalmente, quite la tarjeta de consentimiento original si no desea que el usuario acepte más cargas del mismo archivo.</span><span class="sxs-lookup"><span data-stu-id="95c67-149">Optionally, remove the original consent card if you do not want the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="95c67-150">Mensaje que solicita permiso para cargar</span><span class="sxs-lookup"><span data-stu-id="95c67-150">Message requesting permission to upload</span></span>

<span data-ttu-id="95c67-151">El siguiente mensaje de escritorio contiene un objeto de datos adjuntos sencillo que solicita permiso de usuario para cargar el archivo:</span><span class="sxs-lookup"><span data-stu-id="95c67-151">The following desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![Tarjeta de consentimiento que solicita permiso de usuario para cargar archivo](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="95c67-153">El siguiente mensaje móvil contiene un objeto de datos adjuntos que solicita permiso de usuario para cargar el archivo:</span><span class="sxs-lookup"><span data-stu-id="95c67-153">The following mobile message contains an attachment object requesting user permission to upload the file:</span></span>

![Tarjeta de consentimiento que solicita permiso de usuario para cargar un archivo en un dispositivo móvil](../../assets/images/bots/mobile-bot-file-consent-card.png)

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

<span data-ttu-id="95c67-155">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="95c67-155">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="95c67-156">Propiedad</span><span class="sxs-lookup"><span data-stu-id="95c67-156">Property</span></span> | <span data-ttu-id="95c67-157">Finalidad</span><span class="sxs-lookup"><span data-stu-id="95c67-157">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="95c67-158">Describe el propósito del archivo o resume su contenido.</span><span class="sxs-lookup"><span data-stu-id="95c67-158">Describes the purpose of the file or summarizes its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="95c67-159">Proporciona al usuario una estimación del tamaño del archivo y la cantidad de espacio que ocupa en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="95c67-159">Provides the user an estimate of the file size and the amount of space it takes in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="95c67-160">Contexto adicional que se transmite silenciosamente al bot cuando el usuario acepta el archivo.</span><span class="sxs-lookup"><span data-stu-id="95c67-160">Additional context that is silently transmitted to the bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="95c67-161">Contexto adicional que se transmite silenciosamente al bot cuando el usuario rechaza el archivo.</span><span class="sxs-lookup"><span data-stu-id="95c67-161">Additional context that is silently transmitted to the bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="95c67-162">Invocar actividad cuando el usuario acepta el archivo</span><span class="sxs-lookup"><span data-stu-id="95c67-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="95c67-163">Se envía una actividad de invocación al bot si el usuario acepta el archivo y cuándo lo acepta.</span><span class="sxs-lookup"><span data-stu-id="95c67-163">An invoke activity is sent to the bot if and when the user accepts the file.</span></span> <span data-ttu-id="95c67-164">Contiene la dirección URL de marcador de posición de OneDrive para la Empresa en la que el bot puede emitir una entrada `PUT` para transferir el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="95c67-164">It contains the OneDrive for Business placeholder URL that the bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="95c67-165">Para obtener información sobre cómo cargar en la dirección URL de OneDrive, vea [Cargar bytes en la sesión de carga.](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)</span><span class="sxs-lookup"><span data-stu-id="95c67-165">For information on uploading to the OneDrive URL, see [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="95c67-166">En el siguiente ejemplo se muestra una versión concisa de la actividad de invocación que recibe el bot:</span><span class="sxs-lookup"><span data-stu-id="95c67-166">The following example shows a concise version of the invoke activity that the bot receives:</span></span>

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

<span data-ttu-id="95c67-167">De forma similar, si el usuario rechaza el archivo, el bot recibe el siguiente evento con el mismo nombre de actividad general:</span><span class="sxs-lookup"><span data-stu-id="95c67-167">Similarly, if the user declines the file, the bot receives the following event with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="95c67-168">Notificar al usuario sobre un archivo cargado</span><span class="sxs-lookup"><span data-stu-id="95c67-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="95c67-169">Después de cargar un archivo en el OneDrive del usuario, envíe un mensaje de confirmación al usuario.</span><span class="sxs-lookup"><span data-stu-id="95c67-169">After uploading a file to the user's OneDrive, send a confirmation message to the user.</span></span> <span data-ttu-id="95c67-170">El mensaje debe contener los siguientes datos adjuntos que el usuario puede seleccionar, ya sea para obtener una vista previa o abrirlo en `FileCard` OneDrive, o descargar localmente:</span><span class="sxs-lookup"><span data-stu-id="95c67-170">The message must contain the following `FileCard` attachment that the user can select, either to preview or open it in OneDrive, or download locally:</span></span>

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

<span data-ttu-id="95c67-171">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="95c67-171">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="95c67-172">Propiedad</span><span class="sxs-lookup"><span data-stu-id="95c67-172">Property</span></span> | <span data-ttu-id="95c67-173">Finalidad</span><span class="sxs-lookup"><span data-stu-id="95c67-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="95c67-174">Id. de elemento de unidad de OneDrive o SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95c67-174">OneDrive or SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="95c67-175">Tipo de archivo, como .pdf o .docx.</span><span class="sxs-lookup"><span data-stu-id="95c67-175">Type of file, such as .pdf or .docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="95c67-176">Ejemplo básico en C #</span><span class="sxs-lookup"><span data-stu-id="95c67-176">Basic example in C#</span></span>

<span data-ttu-id="95c67-177">En el ejemplo siguiente se muestra cómo controlar las cargas de archivos y enviar solicitudes de consentimiento de archivos en el cuadro de diálogo del bot:</span><span class="sxs-lookup"><span data-stu-id="95c67-177">The following sample shows how to handle file uploads and send file consent requests in the bot's dialog:</span></span>

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    string filename = "teams-logo.png";
    string filePath = Path.Combine("Files", filename);
    long fileSize = new FileInfo(filePath).Length;
    await SendFileCardAsync(turnContext, filename, fileSize, cancellationToken);
}

private async Task SendFileCardAsync(ITurnContext turnContext, string filename, long filesize, CancellationToken cancellationToken)
{
    var consentContext = new Dictionary<string, string>
    {
        { "filename", filename 
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
    replyActivity.Attachments = new List<Attachment>() { asAttachment 
    };
    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}

protected override async Task OnTeamsFileConsentAcceptAsync(ITurnContext<IInvokeActivity> turnContext, FileConsentCardResponse fileConsentCardResponse, CancellationToken cancellationToken)
{
    try
    {
        JToken context = JObject.FromObject(fileConsentCardResponse.Context);

        string filePath = Path.Combine("Files", context["filename"].ToString());
        long fileSize = new FileInfo(filePath).Length;
        var client = _clientFactory.CreateClient();
        using (var fileStream = File.OpenRead(filePath))
        {
            var fileContent = new StreamContent(fileStream);
            fileContent.Headers.ContentLength = fileSize;
            fileContent.Headers.ContentRange = new ContentRangeHeaderValue(0, fileSize - 1, fileSize);
            await client.PutAsync(fileConsentCardResponse.UploadInfo.UploadUrl, fileContent, cancellationToken);
        }

        await FileUploadCompletedAsync(turnContext, fileConsentCardResponse, cancellationToken);
    }
    catch (Exception e)
    {
        await FileUploadFailedAsync(turnContext, e.ToString(), cancellationToken);
    }
}

protected override async Task OnTeamsFileConsentDeclineAsync(ITurnContext<IInvokeActivity> turnContext, FileConsentCardResponse fileConsentCardResponse, CancellationToken cancellationToken)
{
    JToken context = JObject.FromObject(fileConsentCardResponse.Context);

    var reply = MessageFactory.Text($"Declined. We won't upload file <b>{context["filename"]}</b>.");
    reply.TextFormat = "xml";
    await turnContext.SendActivityAsync(reply, cancellationToken);
}

private async Task FileUploadCompletedAsync(ITurnContext turnContext, FileConsentCardResponse fileConsentCardResponse, CancellationToken cancellationToken)
{
    var downloadCard = new FileInfoCard
    {
        UniqueId = fileConsentCardResponse.UploadInfo.UniqueId,
        FileType = fileConsentCardResponse.UploadInfo.FileType,
    };

    var asAttachment = new Attachment
    {
        Content = downloadCard,
        ContentType = FileInfoCard.ContentType,
        Name = fileConsentCardResponse.UploadInfo.Name,
        ContentUrl = fileConsentCardResponse.UploadInfo.ContentUrl,
    };

    var reply = MessageFactory.Text($"<b>File uploaded.</b> Your file <b>{fileConsentCardResponse.UploadInfo.Name}</b> is ready to download");
    reply.TextFormat = "xml";
    reply.Attachments = new List<Attachment> { asAttachment 
    };

    await turnContext.SendActivityAsync(reply, cancellationToken);
}

private async Task FileUploadFailedAsync(ITurnContext turnContext, string error, CancellationToken cancellationToken)
{
    var reply = MessageFactory.Text($"<b>File upload failed.</b> Error: <pre>{error}</pre>");
    reply.TextFormat = "xml";
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
```
