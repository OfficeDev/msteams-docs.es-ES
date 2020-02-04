---
title: Enviar y recibir archivos desde un bot
description: Describe cómo enviar y recibir archivos desde un bot
keywords: archivos bots de Microsoft Teams enviar recibir
ms.date: 05/20/2019
ms.openlocfilehash: ee26b4031c6022ab30ec5b2b58b42105c2dc6b0f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676193"
---
# <a name="send-and-receive-files-through-your-bot"></a><span data-ttu-id="db7a4-104">Enviar y recibir archivos a través de su bot</span><span class="sxs-lookup"><span data-stu-id="db7a4-104">Send and receive files through your bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="db7a4-105">Hay dos formas de enviar archivos a y desde un bot:</span><span class="sxs-lookup"><span data-stu-id="db7a4-105">There are two ways to send files to and from a bot:</span></span>

* <span data-ttu-id="db7a4-106">Uso de las API de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="db7a4-106">Using the Microsoft Graph APIs.</span></span> <span data-ttu-id="db7a4-107">Este método funciona con bots en todos los ámbitos de Teams:</span><span class="sxs-lookup"><span data-stu-id="db7a4-107">This method works for bots in all scopes in Teams:</span></span>
  * `personal`
  * `channel`
  * `groupchat`
* <span data-ttu-id="db7a4-108">Uso de las API de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="db7a4-108">Using the Teams APIs.</span></span> <span data-ttu-id="db7a4-109">Estos solo admiten archivos en un contexto:</span><span class="sxs-lookup"><span data-stu-id="db7a4-109">These only support files in one context:</span></span>
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a><span data-ttu-id="db7a4-110">Uso de las API de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="db7a4-110">Using the Microsoft Graph APIs</span></span>

<span data-ttu-id="db7a4-111">Puede publicar mensajes con datos adjuntos de tarjeta que hacen referencia a archivos existentes de SharePoint mediante las API de Microsoft Graph para [OneDrive y SharePoint](/onedrive/developer/rest-api/).</span><span class="sxs-lookup"><span data-stu-id="db7a4-111">You can post messages with card attachments referencing existing SharePoint files using the Microsoft Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="db7a4-112">El uso de las API de Graph requiere obtener acceso a la carpeta de OneDrive `personal` ( `groupchat` archivos y archivos) de un usuario o los archivos en los `channel` canales de un equipo (para archivos) a través del flujo de autorización OAuth 2,0 estándar.</span><span class="sxs-lookup"><span data-stu-id="db7a4-112">Using the Graph APIs requires obtaining access to a user's OneDrive folder (for `personal` and `groupchat` files) or the files in a team's channels (for `channel` files) through the standard OAuth 2.0 authorization flow.</span></span> <span data-ttu-id="db7a4-113">Este método funciona en todos los ámbitos de Teams.</span><span class="sxs-lookup"><span data-stu-id="db7a4-113">This method works in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="db7a4-114">Uso de las API de bot de Teams</span><span class="sxs-lookup"><span data-stu-id="db7a4-114">Using the Teams Bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="db7a4-115">Este método sólo funciona en el `personal` contexto.</span><span class="sxs-lookup"><span data-stu-id="db7a4-115">This method works only in the `personal` context.</span></span> <span data-ttu-id="db7a4-116">No funciona en el `channel` contexto o. `groupchat`</span><span class="sxs-lookup"><span data-stu-id="db7a4-116">It does not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="db7a4-117">El bot puede enviar y recibir archivos directamente con usuarios en el `personal` contexto, también conocido como chats personales, mediante las API de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="db7a4-117">Your bot can directly send and receive files with users in the `personal` context, also known as personal chats, using Teams APIs.</span></span> <span data-ttu-id="db7a4-118">Esto le permite implementar informes de gastos, reconocimiento de imágenes, archivado de archivos, firmas electrónicas y otros escenarios que impliquen la manipulación directa del contenido de los archivos.</span><span class="sxs-lookup"><span data-stu-id="db7a4-118">This lets you implement expense reporting, image recognition, file archival, e-signatures, and other scenarios involving direct manipulation of file content.</span></span> <span data-ttu-id="db7a4-119">Los archivos compartidos en Microsoft Teams normalmente aparecen como tarjetas y permiten la visualización en una aplicación enriquecida.</span><span class="sxs-lookup"><span data-stu-id="db7a4-119">Files shared in Teams typically appear as cards, and allow rich in-app viewing.</span></span>

<span data-ttu-id="db7a4-120">En las secciones siguientes se describe cómo hacerlo para enviar contenido de archivo como resultado de la interacción directa del usuario, como el envío de un mensaje.</span><span class="sxs-lookup"><span data-stu-id="db7a4-120">The following sections describe how to do this to send file content as a result of direct user interaction, like sending a message.</span></span> <span data-ttu-id="db7a4-121">Esta API se proporciona como parte de la plataforma de robots de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="db7a4-121">This API is provided as part of the Microsoft Teams Bot Platform.</span></span>

### <a name="configure-your-bot-to-support-files"></a><span data-ttu-id="db7a4-122">Configurar el bot para que admita archivos</span><span class="sxs-lookup"><span data-stu-id="db7a4-122">Configure your bot to support files</span></span>

<span data-ttu-id="db7a4-123">Para poder enviar y recibir archivos en el bot, debe establecer la `supportsFiles` propiedad del manifiesto en. `true`</span><span class="sxs-lookup"><span data-stu-id="db7a4-123">In order to send and receive files in your bot, you have to set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="db7a4-124">Esta propiedad se describe en la sección [bots](~/resources/schema/manifest-schema.md#bots) de la referencia del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="db7a4-124">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="db7a4-125">La definición tendrá un aspecto similar a `"supportsFiles": true`este:.</span><span class="sxs-lookup"><span data-stu-id="db7a4-125">The definition will look like this: `"supportsFiles": true`.</span></span> <span data-ttu-id="db7a4-126">Si el bot no está habilitado `supportsFiles`, las siguientes características no funcionarán.</span><span class="sxs-lookup"><span data-stu-id="db7a4-126">If your bot does not enable `supportsFiles`, the following features will not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="db7a4-127">Recibir archivos en chat personal</span><span class="sxs-lookup"><span data-stu-id="db7a4-127">Receiving files in personal chat</span></span>

<span data-ttu-id="db7a4-128">Cuando un usuario envía un archivo a su bot, el archivo se carga primero en el almacenamiento de OneDrive para la empresa del usuario.</span><span class="sxs-lookup"><span data-stu-id="db7a4-128">When a user sends a file to your bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="db7a4-129">A continuación, el bot recibirá una actividad de mensaje en la que se notifica que la carga del usuario.</span><span class="sxs-lookup"><span data-stu-id="db7a4-129">Your bot will then receive a message activity notifying you of the user upload.</span></span> <span data-ttu-id="db7a4-130">La actividad contendrá metadatos de archivo, como su nombre y la dirección URL de contenido.</span><span class="sxs-lookup"><span data-stu-id="db7a4-130">The activity will contain file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="db7a4-131">Puede leer directamente desde esta dirección URL para obtener su contenido binario.</span><span class="sxs-lookup"><span data-stu-id="db7a4-131">You can directly read from this URL to fetch its binary content.</span></span>

### <a name="send-and-receive-files-through-bot-on-teams-mobile-app"></a><span data-ttu-id="db7a4-132">Enviar y recibir archivos a través de bot en la aplicación móvil de Teams</span><span class="sxs-lookup"><span data-stu-id="db7a4-132">Send and receive files through bot on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="db7a4-133">No se admite el envío y la recepción de archivos en bots en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="db7a4-133">Sending and receiving files to bots on mobile devices is not supported.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="db7a4-134">Ejemplo de actividad de mensajes con datos adjuntos de archivo</span><span class="sxs-lookup"><span data-stu-id="db7a4-134">Message activity with file attachment example</span></span>

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

<span data-ttu-id="db7a4-135">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="db7a4-135">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="db7a4-136">Propiedad</span><span class="sxs-lookup"><span data-stu-id="db7a4-136">Property</span></span> | <span data-ttu-id="db7a4-137">Objetivo</span><span class="sxs-lookup"><span data-stu-id="db7a4-137">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="db7a4-138">Dirección URL de OneDrive para recuperar el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="db7a4-138">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="db7a4-139">Puede emitir `HTTP GET` directamente desde esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="db7a4-139">You can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="db7a4-140">IDENTIFICADOR de archivo único.</span><span class="sxs-lookup"><span data-stu-id="db7a4-140">Unique file ID.</span></span> <span data-ttu-id="db7a4-141">Este será el identificador de elemento de la unidad de OneDrive, en el caso de que el usuario envíe un archivo a su bot.</span><span class="sxs-lookup"><span data-stu-id="db7a4-141">This will be the OneDrive drive item ID, in the case of the user sending a file to your bot.</span></span> |
| `fileType` | <span data-ttu-id="db7a4-142">Tipo de extensión de archivo, como PDF o DOCX.</span><span class="sxs-lookup"><span data-stu-id="db7a4-142">File extension type, such as pdf or docx.</span></span> |

<span data-ttu-id="db7a4-143">Como práctica recomendada, debe confirmar la carga del archivo mediante el envío de un mensaje al usuario.</span><span class="sxs-lookup"><span data-stu-id="db7a4-143">As a best practice, you should acknowledge the file upload by sending back a message to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="db7a4-144">Cargar archivos en un chat personal</span><span class="sxs-lookup"><span data-stu-id="db7a4-144">Uploading files to personal chat</span></span>

<span data-ttu-id="db7a4-145">La carga de un archivo a un usuario implica los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="db7a4-145">Uploading a file to a user involves the following steps:</span></span>

1. <span data-ttu-id="db7a4-146">Envíe un mensaje al usuario que solicita permiso para escribir el archivo.</span><span class="sxs-lookup"><span data-stu-id="db7a4-146">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="db7a4-147">Este mensaje debe contener `FileConsentCard` datos adjuntos con el nombre del archivo que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="db7a4-147">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="db7a4-148">Si el usuario acepta la descarga del archivo, el bot recibirá una actividad de *invocación* con una dirección URL de la ubicación.</span><span class="sxs-lookup"><span data-stu-id="db7a4-148">If the user accepts the file download, your bot will receive an *Invoke* activity with a location URL.</span></span>
3. <span data-ttu-id="db7a4-149">Para transferir el archivo, el bot realiza una `HTTP POST` directamente en la dirección URL de ubicación proporcionada.</span><span class="sxs-lookup"><span data-stu-id="db7a4-149">To transfer the file, your bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="db7a4-150">Opcionalmente, puede quitar la tarjeta de consentimiento original si no desea permitir que el usuario acepte más cargas del mismo archivo.</span><span class="sxs-lookup"><span data-stu-id="db7a4-150">Optionally, you can remove the original consent card if you do not want to allow the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="db7a4-151">Mensaje que solicita permiso para cargar</span><span class="sxs-lookup"><span data-stu-id="db7a4-151">Message requesting permission to upload</span></span>

<span data-ttu-id="db7a4-152">Este mensaje contiene un objeto Attachment simple que solicita permiso de usuario para cargar el archivo.</span><span class="sxs-lookup"><span data-stu-id="db7a4-152">This message contains a simple attachment object requesting user permission to upload the file.</span></span>

![Captura de pantalla de la tarjeta de consentimiento que solicita permiso de usuario para cargar archivo](~/assets/images/bots/bot-file-consent-card.png)

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

<span data-ttu-id="db7a4-154">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="db7a4-154">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="db7a4-155">Propiedad</span><span class="sxs-lookup"><span data-stu-id="db7a4-155">Property</span></span> | <span data-ttu-id="db7a4-156">Objetivo</span><span class="sxs-lookup"><span data-stu-id="db7a4-156">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="db7a4-157">Descripción del archivo.</span><span class="sxs-lookup"><span data-stu-id="db7a4-157">Description of the file.</span></span> <span data-ttu-id="db7a4-158">Se puede mostrar al usuario para describir su finalidad o resumir su contenido.</span><span class="sxs-lookup"><span data-stu-id="db7a4-158">May be shown to the user to describe its purpose or to summarize its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="db7a4-159">Proporciona al usuario una estimación del tamaño del archivo y la cantidad de espacio que tendrá en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="db7a4-159">Provides the user an estimate of the file size and the amount of space it will take in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="db7a4-160">Contexto adicional que se transmitirá silenciosamente a su bot cuando el usuario acepte el archivo.</span><span class="sxs-lookup"><span data-stu-id="db7a4-160">Additional context that will be silently transmitted to your bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="db7a4-161">Contexto adicional que se transmitirá silenciosamente a su bot cuando el usuario rechace el archivo.</span><span class="sxs-lookup"><span data-stu-id="db7a4-161">Additional context that will be silently transmitted to your bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="db7a4-162">Invocar la actividad cuando el usuario acepta el archivo</span><span class="sxs-lookup"><span data-stu-id="db7a4-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="db7a4-163">Se envía una actividad de invocación a su bot cuando el usuario acepta el archivo.</span><span class="sxs-lookup"><span data-stu-id="db7a4-163">An invoke activity is sent to your bot if and when the user accepts the file.</span></span> <span data-ttu-id="db7a4-164">Contiene la dirección URL del marcador de posición de OneDrive para la empresa que el `PUT` bot puede enviar a en para transferir el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="db7a4-164">It contains the OneDrive for Business placeholder URL that your bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="db7a4-165">para obtener información sobre cómo cargar en la dirección URL de OneDrive, lea este artículo: [cargar bytes a la sesión de carga](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span><span class="sxs-lookup"><span data-stu-id="db7a4-165">for information on uploading to the OneDrive URL read this article: [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="db7a4-166">En el ejemplo siguiente se muestra una versión abreviada de la actividad Invoke que recibirá el bot:</span><span class="sxs-lookup"><span data-stu-id="db7a4-166">The following example shows an abridged version of the invoke activity that your bot will receive:</span></span>

```json
{
  ...

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

<span data-ttu-id="db7a4-167">De forma similar, si el usuario rechaza el archivo, el bot recibirá el evento siguiente, con el mismo nombre de actividad general:</span><span class="sxs-lookup"><span data-stu-id="db7a4-167">Similarly, if the user declines the file, your bot will receive the following event, with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="db7a4-168">Notificar al usuario sobre un archivo cargado</span><span class="sxs-lookup"><span data-stu-id="db7a4-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="db7a4-169">Después de cargar un archivo en el OneDrive del usuario, independientemente de si usa el mecanismo descrito anteriormente o las API delegadas del usuario de OneDrive, debe enviar un mensaje de confirmación al usuario.</span><span class="sxs-lookup"><span data-stu-id="db7a4-169">After uploading a file to the user's OneDrive, whether you use the mechanism described above or OneDrive user delegated APIs, you should send a confirmation message to the user.</span></span> <span data-ttu-id="db7a4-170">Este mensaje debe contener `FileCard` datos adjuntos en los que el usuario puede hacer clic, ya sea para obtener una vista previa, abrirlo en OneDrive o descargarse de forma local.</span><span class="sxs-lookup"><span data-stu-id="db7a4-170">This message should contain  a `FileCard` attachment that the user can click on, either to preview it, open it in OneDrive, or download locally.</span></span>

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

<span data-ttu-id="db7a4-171">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="db7a4-171">The following table describes the content properties of the attachment:</span></span> 

| <span data-ttu-id="db7a4-172">Propiedad</span><span class="sxs-lookup"><span data-stu-id="db7a4-172">Property</span></span> | <span data-ttu-id="db7a4-173">Objetivo</span><span class="sxs-lookup"><span data-stu-id="db7a4-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="db7a4-174">IDENTIFICADOR de elemento de unidad de OneDrive/SharePoint.</span><span class="sxs-lookup"><span data-stu-id="db7a4-174">OneDrive/SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="db7a4-175">Tipo de archivo, como PDF o DOCX.</span><span class="sxs-lookup"><span data-stu-id="db7a4-175">File type, such as pdf or docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="db7a4-176">Ejemplo básico en C #</span><span class="sxs-lookup"><span data-stu-id="db7a4-176">Basic example in C#</span></span>

<span data-ttu-id="db7a4-177">El siguiente ejemplo muestra cómo puede controlar cargas de archivos y enviar solicitudes de consentimiento de archivo en el cuadro de diálogo de su bot.</span><span class="sxs-lookup"><span data-stu-id="db7a4-177">The following sample shows how you can handle file uploads and send file consent requests in your bot's dialog.</span></span>

```csharp

// This sample dialog shows two simple flows:
// 1) A silly example of receiving a file from the user, processing the key elements,
//    and then constructing the attachment and sending it back.
// 2) Creating a new file consent card requesting user permission to upload a file.
private async Task MessageReceivedAsync(IDialogContext context, IAwaitable<object> result)
{
    var replyMessage = context.MakeMessage();
    Attachment returnCard;

    var message = await result as Activity;

    // Check to see if the user is sending the bot a file.
    if (message.Attachments != null && message.Attachments.Any())
    {
        var attachment = message.Attachments.First();

        if (attachment.ContentType == FileDownloadInfo.ContentType)
        {
            FileDownloadInfo downloadInfo = (attachment.Content as JObject).ToObject<FileDownloadInfo>();
            if (downloadInfo != null)
            {
                returnCard = CreateFileInfoAttachment(downloadInfo, attachment.Name, attachment.ContentUrl);
                replyMessage.Attachments.Add(returnCard);
            }
        }
    }
    else
    {
        // Illustrates creating a file consent card.
        returnCard = CreateFileConsentAttachment();
        replyMessage.Attachments.Add(returnCard);
    }
    await context.PostAsync(replyMessage);
}


private static Attachment CreateFileInfoAttachment(FileDownloadInfo downloadInfo, string name, string contentUrl)
{
    FileInfoCard card = new FileInfoCard()
    {
        FileType = downloadInfo.FileType,
        UniqueId = downloadInfo.UniqueId
    };

    Attachment att = card.ToAttachment();
    att.ContentUrl = contentUrl;
    att.Name = name;

    return att;
}

private static Attachment CreateFileConsentAttachment()
{
    JObject acceptContext = new JObject();
    // Fill in any additional context to be sent back when the user accepts the file.

    JObject declineContext = new JObject();
    // Fill in any additional context to be sent back when the user declines the file.

    FileConsentCard card = new FileConsentCard()
    {
        AcceptContext = acceptContext,
        DeclineContext = declineContext,
        SizeInBytes = 102635,
        Description = "File description"
    };

    Attachment att = card.ToAttachment();
    att.Name = "Example file";

    return att;
}
```
