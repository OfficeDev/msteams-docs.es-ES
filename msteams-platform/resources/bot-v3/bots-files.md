---
title: Enviar y recibir archivos desde un bot
description: Obtenga información sobre cómo enviar y recibir archivos a través del bot Graph API para ámbitos personales, de canal y de chat de grupo. Use Teams API de bot con ejemplos de código basados en el SDK de Bot Framework de v3.
keywords: bots teams bots files send receive
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: c95ddbc4bfe0d491f48101b12d8658f7714c0075
ms.sourcegitcommit: 52af681132e496a57b18f468c5b73265a49a5f44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/31/2022
ms.locfileid: "64590755"
---
# <a name="send-and-receive-files-through-your-bot"></a>Enviar y recibir archivos a través del bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Hay dos maneras de enviar archivos a y desde un bot:

* Uso de las API Graph Microsoft. Este método funciona para bots en todos los ámbitos de Teams:
  * `personal`
  * `channel`
  * `groupchat`
* Uso de Teams API. Estos solo admiten archivos en un contexto:
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>Uso de las API Graph Microsoft

Puede publicar mensajes con datos adjuntos de tarjeta que hagan referencia a archivos SharePoint existentes mediante las API de Microsoft Graph para OneDrive [y SharePoint](/onedrive/developer/rest-api/). El uso de las API de Graph requiere obtener acceso a la carpeta OneDrive de un usuario (`personal` `groupchat` para y archivos) o a los archivos de los canales de un equipo (`channel`para archivos) mediante el flujo de autorización estándar de OAuth 2.0. Este método funciona en todos Teams ámbitos.

## <a name="using-the-teams-bot-apis"></a>Uso de las API Teams Bot

> [!NOTE]
> Este método solo funciona en el `personal` contexto. No funciona en el contexto `channel` o `groupchat` .

El bot puede enviar y recibir `personal` directamente archivos con usuarios en el contexto, también conocido como chats personales, mediante Teams API. Esto le permite implementar informes de gastos, reconocimiento de imágenes, archivo de archivo, firmas electrónicas y otros escenarios que implican la manipulación directa del contenido del archivo. Los archivos compartidos Teams suelen aparecer como tarjetas y permiten la visualización enriquecte desde la aplicación.

En las secciones siguientes se describe cómo hacerlo para enviar contenido de archivo como resultado de la interacción directa del usuario, como enviar un mensaje. Esta API se proporciona como parte de la plataforma Microsoft Teams bot.

### <a name="configure-your-bot-to-support-files"></a>Configurar el bot para admitir archivos

Para enviar y recibir archivos en el bot, debe establecer la `supportsFiles` propiedad en el manifiesto en `true`. Esta propiedad se describe en la [sección bots](~/resources/schema/manifest-schema.md#bots) de la referencia manifest.

La definición tendrá este aspecto: `"supportsFiles": true`. Si el bot no lo habilita `supportsFiles`, las siguientes características no funcionarán.

### <a name="receiving-files-in-personal-chat"></a>Recepción de archivos en chat personal

Cuando un usuario envía un archivo al bot, el archivo se carga por primera vez en el almacenamiento de OneDrive para la Empresa usuario. A continuación, el bot recibirá una actividad de mensaje que le notificará sobre la carga del usuario. La actividad contendrá metadatos de archivo, como su nombre y la dirección URL de contenido. Puede leer directamente desde esta dirección URL para capturar su contenido binario.

#### <a name="message-activity-with-file-attachment-example"></a>Ejemplo de actividad de mensaje con datos adjuntos de archivo

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

En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:

| Propiedad | Objetivo |
| --- | --- |
| `downloadUrl` | OneDrive url para capturar el contenido del archivo. Puede emitir una directamente `HTTP GET` desde esta dirección URL. |
| `uniqueId` | Identificador de archivo único. Este será el identificador OneDrive elemento de unidad, en el caso de que el usuario envíe un archivo al bot. |
| `fileType` | Tipo de extensión de archivo, como pdf o docx. |

Como práctica recomendada, debes confirmar la carga del archivo enviando un mensaje al usuario.

### <a name="uploading-files-to-personal-chat"></a>Cargar archivos en chat personal

Cargar un archivo a un usuario implica los siguientes pasos:

1. Enviar un mensaje al usuario que solicita permiso para escribir el archivo. Este mensaje debe contener datos `FileConsentCard` adjuntos con el nombre del archivo que se va a cargar.
2. Si el usuario acepta la descarga de archivos, el bot recibirá una *actividad Invoke* con una dirección URL de ubicación.
3. Para transferir el archivo, el bot realiza una `HTTP POST` operación directamente en la dirección URL de ubicación proporcionada.
4. Opcionalmente, puedes quitar la tarjeta de consentimiento original si no quieres permitir que el usuario acepte más cargas del mismo archivo.

#### <a name="message-requesting-permission-to-upload"></a>Mensaje que solicita permiso para cargar

Este mensaje de escritorio contiene un objeto de datos adjuntos sencillo que solicita permiso al usuario para cargar el archivo:

![Captura de pantalla de la tarjeta de consentimiento que solicita permiso de usuario para cargar el archivo](../../assets/images/bots/bot-file-consent-card.png)

Este mensaje móvil contiene un objeto attachment que solicita permiso al usuario para cargar el archivo:

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

En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:

| Propiedad | Objetivo |
| --- | --- |
| `description` | Descripción del archivo. Puede mostrarse al usuario para describir su propósito o para resumir su contenido. |
| `sizeInBytes` | Proporciona al usuario una estimación del tamaño del archivo y la cantidad de espacio que ocupará OneDrive. |
| `acceptContext` | Contexto adicional que se transmitirá silenciosamente al bot cuando el usuario acepte el archivo. |
| `declineContext` | Contexto adicional que se transmitirá silenciosamente al bot cuando el usuario rechace el archivo. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Invocar actividad cuando el usuario acepta el archivo

Se envía una actividad de invocación al bot si el usuario acepta el archivo y cuándo. Contiene la dirección URL OneDrive para la Empresa marcador de posición que el bot puede emitir para `PUT` transferir el contenido del archivo. para obtener información sobre la carga en la dirección URL OneDrive este artículo: [Upload bytes a la sesión de carga](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).

En el ejemplo siguiente se muestra una versión abreviada de la actividad de invocación que recibirá el bot:

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

Del mismo modo, si el usuario rechaza el archivo, el bot recibirá el siguiente evento, con el mismo nombre de actividad general:

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

### <a name="notifying-the-user-about-an-uploaded-file"></a>Notificar al usuario acerca de un archivo cargado

Después de cargar un archivo en el OneDrive del usuario, tanto si usa el mecanismo descrito anteriormente como si OneDrive API delegadas por el usuario, debe enviar un mensaje de confirmación al usuario. Este mensaje debe contener datos `FileCard` adjuntos en los que el usuario pueda hacer clic, ya sea para obtener una vista previa, abrirlo en OneDrive o descargar localmente.

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

En la tabla siguiente se describen las propiedades de contenido de los datos adjuntos:

| Propiedad | Objetivo |
| --- | --- |
| `uniqueId` | OneDrive/SharePoint id. de elemento de unidad. |
| `fileType` | Tipo de archivo, como pdf o docx. |

### <a name="basic-example-in-c"></a>Ejemplo básico en C #

En el ejemplo siguiente se muestra cómo controlar las cargas de archivos y enviar solicitudes de consentimiento de archivos en el cuadro de diálogo del bot:

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
