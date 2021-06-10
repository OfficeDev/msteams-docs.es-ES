---
title: Enviar y recibir archivos desde un bot
description: Describe cómo enviar y recibir archivos de un bot
keywords: bots teams bots files send receive
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: f69a6ca9cfcdf3b1e559fbe8cf569accf3166f69
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566484"
---
# <a name="send-and-receive-files-through-your-bot"></a><span data-ttu-id="04d64-104">Enviar y recibir archivos a través del bot</span><span class="sxs-lookup"><span data-stu-id="04d64-104">Send and receive files through your bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="04d64-105">Hay dos maneras de enviar archivos a y desde un bot:</span><span class="sxs-lookup"><span data-stu-id="04d64-105">There are two ways to send files to and from a bot:</span></span>

* <span data-ttu-id="04d64-106">Uso de las API Graph Microsoft.</span><span class="sxs-lookup"><span data-stu-id="04d64-106">Using the Microsoft Graph APIs.</span></span> <span data-ttu-id="04d64-107">Este método funciona para bots en todos los ámbitos de Teams:</span><span class="sxs-lookup"><span data-stu-id="04d64-107">This method works for bots in all scopes in Teams:</span></span>
  * `personal`
  * `channel`
  * `groupchat`
* <span data-ttu-id="04d64-108">Uso de Teams API.</span><span class="sxs-lookup"><span data-stu-id="04d64-108">Using the Teams APIs.</span></span> <span data-ttu-id="04d64-109">Estos solo admiten archivos en un contexto:</span><span class="sxs-lookup"><span data-stu-id="04d64-109">These only support files in one context:</span></span>
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a><span data-ttu-id="04d64-110">Uso de las API Graph Microsoft</span><span class="sxs-lookup"><span data-stu-id="04d64-110">Using the Microsoft Graph APIs</span></span>

<span data-ttu-id="04d64-111">Puede publicar mensajes con datos adjuntos de tarjeta que hagan referencia a archivos SharePoint existentes mediante las API de Microsoft Graph para OneDrive [y SharePoint](/onedrive/developer/rest-api/).</span><span class="sxs-lookup"><span data-stu-id="04d64-111">You can post messages with card attachments referencing existing SharePoint files using the Microsoft Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="04d64-112">El uso de las API de Graph requiere obtener acceso a la carpeta OneDrive de un usuario (para y archivos) o a los archivos de los canales de un equipo (para archivos) mediante el flujo de autorización estándar de `personal` `groupchat` `channel` OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="04d64-112">Using the Graph APIs requires obtaining access to a user's OneDrive folder (for `personal` and `groupchat` files) or the files in a team's channels (for `channel` files) through the standard OAuth 2.0 authorization flow.</span></span> <span data-ttu-id="04d64-113">Este método funciona en todos Teams ámbitos.</span><span class="sxs-lookup"><span data-stu-id="04d64-113">This method works in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="04d64-114">Uso de las API Teams Bot</span><span class="sxs-lookup"><span data-stu-id="04d64-114">Using the Teams Bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="04d64-115">Este método solo funciona en el `personal` contexto.</span><span class="sxs-lookup"><span data-stu-id="04d64-115">This method works only in the `personal` context.</span></span> <span data-ttu-id="04d64-116">No funciona en el `channel` contexto `groupchat` o.</span><span class="sxs-lookup"><span data-stu-id="04d64-116">It does not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="04d64-117">El bot puede enviar y recibir directamente archivos con usuarios en el contexto, también conocido como chats personales, mediante Teams `personal` API.</span><span class="sxs-lookup"><span data-stu-id="04d64-117">Your bot can directly send and receive files with users in the `personal` context, also known as personal chats, using Teams APIs.</span></span> <span data-ttu-id="04d64-118">Esto le permite implementar informes de gastos, reconocimiento de imágenes, archivo de archivo, firmas electrónicas y otros escenarios que implican la manipulación directa del contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="04d64-118">This lets you implement expense reporting, image recognition, file archival, e-signatures, and other scenarios involving direct manipulation of file content.</span></span> <span data-ttu-id="04d64-119">Los archivos compartidos Teams suelen aparecer como tarjetas y permiten la visualización enriquecte desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="04d64-119">Files shared in Teams typically appear as cards, and allow rich in-app viewing.</span></span>

<span data-ttu-id="04d64-120">En las secciones siguientes se describe cómo hacerlo para enviar contenido de archivo como resultado de la interacción directa del usuario, como enviar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="04d64-120">The following sections describe how to do this to send file content as a result of direct user interaction, like sending a message.</span></span> <span data-ttu-id="04d64-121">Esta API se proporciona como parte de la plataforma Microsoft Teams bot.</span><span class="sxs-lookup"><span data-stu-id="04d64-121">This API is provided as part of the Microsoft Teams Bot Platform.</span></span>

### <a name="configure-your-bot-to-support-files"></a><span data-ttu-id="04d64-122">Configurar el bot para admitir archivos</span><span class="sxs-lookup"><span data-stu-id="04d64-122">Configure your bot to support files</span></span>

<span data-ttu-id="04d64-123">Para enviar y recibir archivos en el bot, debe establecer la propiedad `supportsFiles` en el manifiesto en `true` .</span><span class="sxs-lookup"><span data-stu-id="04d64-123">In order to send and receive files in your bot, you have to set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="04d64-124">Esta propiedad se describe en la [sección bots](~/resources/schema/manifest-schema.md#bots) de la referencia manifest.</span><span class="sxs-lookup"><span data-stu-id="04d64-124">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="04d64-125">La definición tendrá este aspecto: `"supportsFiles": true` .</span><span class="sxs-lookup"><span data-stu-id="04d64-125">The definition will look like this: `"supportsFiles": true`.</span></span> <span data-ttu-id="04d64-126">Si el bot no lo `supportsFiles` habilita, las siguientes características no funcionarán.</span><span class="sxs-lookup"><span data-stu-id="04d64-126">If your bot does not enable `supportsFiles`, the following features will not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="04d64-127">Recepción de archivos en chat personal</span><span class="sxs-lookup"><span data-stu-id="04d64-127">Receiving files in personal chat</span></span>

<span data-ttu-id="04d64-128">Cuando un usuario envía un archivo al bot, el archivo se carga por primera vez en el almacenamiento de OneDrive para la Empresa usuario.</span><span class="sxs-lookup"><span data-stu-id="04d64-128">When a user sends a file to your bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="04d64-129">A continuación, el bot recibirá una actividad de mensaje que le notificará sobre la carga del usuario.</span><span class="sxs-lookup"><span data-stu-id="04d64-129">Your bot will then receive a message activity notifying you of the user upload.</span></span> <span data-ttu-id="04d64-130">La actividad contendrá metadatos de archivo, como su nombre y la dirección URL de contenido.</span><span class="sxs-lookup"><span data-stu-id="04d64-130">The activity will contain file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="04d64-131">Puede leer directamente desde esta dirección URL para capturar su contenido binario.</span><span class="sxs-lookup"><span data-stu-id="04d64-131">You can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="04d64-132">Ejemplo de actividad de mensaje con datos adjuntos de archivo</span><span class="sxs-lookup"><span data-stu-id="04d64-132">Message activity with file attachment example</span></span>

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

<span data-ttu-id="04d64-133">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="04d64-133">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="04d64-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="04d64-134">Property</span></span> | <span data-ttu-id="04d64-135">Objetivo</span><span class="sxs-lookup"><span data-stu-id="04d64-135">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="04d64-136">OneDrive Dirección URL para capturar el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="04d64-136">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="04d64-137">Puede emitir una `HTTP GET` directamente desde esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="04d64-137">You can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="04d64-138">Identificador de archivo único.</span><span class="sxs-lookup"><span data-stu-id="04d64-138">Unique file ID.</span></span> <span data-ttu-id="04d64-139">Este será el identificador OneDrive elemento de unidad, en el caso de que el usuario envíe un archivo al bot.</span><span class="sxs-lookup"><span data-stu-id="04d64-139">This will be the OneDrive drive item ID, in the case of the user sending a file to your bot.</span></span> |
| `fileType` | <span data-ttu-id="04d64-140">Tipo de extensión de archivo, como pdf o docx.</span><span class="sxs-lookup"><span data-stu-id="04d64-140">File extension type, such as pdf or docx.</span></span> |

<span data-ttu-id="04d64-141">Como práctica recomendada, debes confirmar la carga del archivo enviando un mensaje al usuario.</span><span class="sxs-lookup"><span data-stu-id="04d64-141">As a best practice, you should acknowledge the file upload by sending back a message to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="04d64-142">Cargar archivos en chat personal</span><span class="sxs-lookup"><span data-stu-id="04d64-142">Uploading files to personal chat</span></span>

<span data-ttu-id="04d64-143">Cargar un archivo a un usuario implica los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="04d64-143">Uploading a file to a user involves the following steps:</span></span>

1. <span data-ttu-id="04d64-144">Enviar un mensaje al usuario que solicita permiso para escribir el archivo.</span><span class="sxs-lookup"><span data-stu-id="04d64-144">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="04d64-145">Este mensaje debe contener `FileConsentCard` datos adjuntos con el nombre del archivo que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="04d64-145">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="04d64-146">Si el usuario acepta la descarga de archivos, el bot recibirá una *actividad Invoke* con una dirección URL de ubicación.</span><span class="sxs-lookup"><span data-stu-id="04d64-146">If the user accepts the file download, your bot will receive an *Invoke* activity with a location URL.</span></span>
3. <span data-ttu-id="04d64-147">Para transferir el archivo, el bot realiza una `HTTP POST` operación directamente en la dirección URL de ubicación proporcionada.</span><span class="sxs-lookup"><span data-stu-id="04d64-147">To transfer the file, your bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="04d64-148">Opcionalmente, puedes quitar la tarjeta de consentimiento original si no quieres permitir que el usuario acepte más cargas del mismo archivo.</span><span class="sxs-lookup"><span data-stu-id="04d64-148">Optionally, you can remove the original consent card if you do not want to allow the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="04d64-149">Mensaje que solicita permiso para cargar</span><span class="sxs-lookup"><span data-stu-id="04d64-149">Message requesting permission to upload</span></span>

<span data-ttu-id="04d64-150">Este mensaje de escritorio contiene un objeto de datos adjuntos sencillo que solicita permiso al usuario para cargar el archivo:</span><span class="sxs-lookup"><span data-stu-id="04d64-150">This desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![Captura de pantalla de la tarjeta de consentimiento que solicita permiso de usuario para cargar el archivo](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="04d64-152">Este mensaje móvil contiene un objeto attachment que solicita permiso al usuario para cargar el archivo:</span><span class="sxs-lookup"><span data-stu-id="04d64-152">This mobile message contains an attachment object requesting user permission to upload the file:</span></span>

![Captura de pantalla de la tarjeta de consentimiento que solicita permiso al usuario para cargar el archivo en el móvil](../../assets/images/bots/mobile-bot-file-consent-card.png)

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

<span data-ttu-id="04d64-154">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="04d64-154">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="04d64-155">Propiedad</span><span class="sxs-lookup"><span data-stu-id="04d64-155">Property</span></span> | <span data-ttu-id="04d64-156">Objetivo</span><span class="sxs-lookup"><span data-stu-id="04d64-156">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="04d64-157">Descripción del archivo.</span><span class="sxs-lookup"><span data-stu-id="04d64-157">Description of the file.</span></span> <span data-ttu-id="04d64-158">Puede mostrarse al usuario para describir su propósito o para resumir su contenido.</span><span class="sxs-lookup"><span data-stu-id="04d64-158">May be shown to the user to describe its purpose or to summarize its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="04d64-159">Proporciona al usuario una estimación del tamaño del archivo y la cantidad de espacio que ocupará en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="04d64-159">Provides the user an estimate of the file size and the amount of space it will take in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="04d64-160">Contexto adicional que se transmitirá silenciosamente al bot cuando el usuario acepte el archivo.</span><span class="sxs-lookup"><span data-stu-id="04d64-160">Additional context that will be silently transmitted to your bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="04d64-161">Contexto adicional que se transmitirá silenciosamente al bot cuando el usuario rechace el archivo.</span><span class="sxs-lookup"><span data-stu-id="04d64-161">Additional context that will be silently transmitted to your bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="04d64-162">Invocar actividad cuando el usuario acepta el archivo</span><span class="sxs-lookup"><span data-stu-id="04d64-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="04d64-163">Se envía una actividad de invocación al bot si el usuario acepta el archivo y cuándo.</span><span class="sxs-lookup"><span data-stu-id="04d64-163">An invoke activity is sent to your bot if and when the user accepts the file.</span></span> <span data-ttu-id="04d64-164">Contiene la dirección URL OneDrive para la Empresa marcador de posición que el bot puede emitir para `PUT` transferir el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="04d64-164">It contains the OneDrive for Business placeholder URL that your bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="04d64-165">para obtener información sobre la carga en la dirección URL OneDrive este artículo: Upload [bytes a la sesión de carga](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span><span class="sxs-lookup"><span data-stu-id="04d64-165">for information on uploading to the OneDrive URL read this article: [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="04d64-166">En el ejemplo siguiente se muestra una versión abreviada de la actividad de invocación que recibirá el bot:</span><span class="sxs-lookup"><span data-stu-id="04d64-166">The following example shows an abridged version of the invoke activity that your bot will receive:</span></span>

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

<span data-ttu-id="04d64-167">Del mismo modo, si el usuario rechaza el archivo, el bot recibirá el siguiente evento, con el mismo nombre de actividad general:</span><span class="sxs-lookup"><span data-stu-id="04d64-167">Similarly, if the user declines the file, your bot will receive the following event, with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="04d64-168">Notificar al usuario acerca de un archivo cargado</span><span class="sxs-lookup"><span data-stu-id="04d64-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="04d64-169">Después de cargar un archivo en el OneDrive del usuario, tanto si usa el mecanismo descrito anteriormente como si OneDrive API delegadas por el usuario, debe enviar un mensaje de confirmación al usuario.</span><span class="sxs-lookup"><span data-stu-id="04d64-169">After uploading a file to the user's OneDrive, whether you use the mechanism described above or OneDrive user delegated APIs, you should send a confirmation message to the user.</span></span> <span data-ttu-id="04d64-170">Este mensaje debe contener datos adjuntos en los que el usuario pueda hacer clic, ya sea para obtener una vista previa, abrirlo en `FileCard` OneDrive o descargar localmente.</span><span class="sxs-lookup"><span data-stu-id="04d64-170">This message should contain  a `FileCard` attachment that the user can click on, either to preview it, open it in OneDrive, or download locally.</span></span>

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

<span data-ttu-id="04d64-171">En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:</span><span class="sxs-lookup"><span data-stu-id="04d64-171">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="04d64-172">Propiedad</span><span class="sxs-lookup"><span data-stu-id="04d64-172">Property</span></span> | <span data-ttu-id="04d64-173">Objetivo</span><span class="sxs-lookup"><span data-stu-id="04d64-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="04d64-174">OneDrive/SharePoint de elemento de unidad.</span><span class="sxs-lookup"><span data-stu-id="04d64-174">OneDrive/SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="04d64-175">Tipo de archivo, como pdf o docx.</span><span class="sxs-lookup"><span data-stu-id="04d64-175">File type, such as pdf or docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="04d64-176">Ejemplo básico en C #</span><span class="sxs-lookup"><span data-stu-id="04d64-176">Basic example in C#</span></span>

<span data-ttu-id="04d64-177">En el ejemplo siguiente se muestra cómo controlar las cargas de archivos y enviar solicitudes de consentimiento de archivos en el cuadro de diálogo del bot:</span><span class="sxs-lookup"><span data-stu-id="04d64-177">The following sample shows how you can handle file uploads and send file consent requests in your bot's dialog:</span></span>

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
