---
title: Envío y recepción de archivos desde un bot
description: Aprenda a enviar y recibir archivos a través del bot mediante Graph API para ámbitos personales, de canal y de chat grupal. Use las API de bot de Teams mediante ejemplos de código basados en el SDK de Bot Framework v3.
keywords: equipos bots archivos enviar recibir
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 1bc04d2dfde200917c9faeb9fcb1c91b145463de
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558292"
---
# <a name="send-and-receive-files-using-bots"></a>Envío y recepción de archivos mediante bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Hay dos maneras de enviar archivos a y desde un bot:

* Uso de las API de Microsoft Graph. Este método funciona para bots en todos los ámbitos de Teams:
  * `personal`
  * `channel`
  * `groupchat`
* Usar las API de Teams. Estos solo admiten archivos en un contexto:
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>Uso de las API de Microsoft Graph

Puede publicar mensajes con datos adjuntos de tarjeta que hagan referencia a archivos de SharePoint ya existentes mediante las API de Microsoft Graph para [OneDrive y SharePoint](/onedrive/developer/rest-api/). El uso de graph API requiere obtener acceso a la carpeta de OneDrive de un usuario (para archivos de `personal` y `groupchat`) o a los archivos de los canales de un equipo (para archivos de `channel`) a través del flujo de autorización estándar de OAuth 2.0. Este método funciona en todos los ámbitos de Teams.

## <a name="using-the-teams-bot-apis"></a>Uso de las API de bot de Teams

> [!NOTE]
> Este método solo funciona en el contexto de `personal`. No funciona en el contexto de `channel` o `groupchat`.

El bot puede enviar y recibir archivos directamente con los usuarios en el contexto de `personal`, también conocido como chats personales, mediante las API de Teams. Esto le permite implementar informes de gastos, reconocimiento de imágenes, archivado de archivos, firmas electrónicas y otros escenarios que implican la manipulación directa del contenido del archivo. Los archivos compartidos en Teams suelen aparecer como tarjetas y permiten una visualización enriquecida desde la aplicación.

En las secciones siguientes se describe cómo hacerlo para enviar contenido de archivo como resultado de la interacción directa del usuario, como el envío de un mensaje. Esta API se proporciona como parte de la plataforma de bots de Microsoft Teams.

### <a name="configure-your-bot-to-support-files"></a>Configuración del bot para admitir archivos

Para enviar y recibir archivos en el bot, debe establecer la propiedad `supportsFiles` del manifiesto en `true`. Esta propiedad se describe en la sección [bots](~/resources/schema/manifest-schema.md#bots) de la referencia de manifiesto.

La definición tendrá el siguiente aspecto: `"supportsFiles": true`. Si el bot no habilita `supportsFiles`, las siguientes características no funcionarán.

### <a name="receiving-files-in-personal-chat"></a>Recepción de archivos en un chat personal

Cuando un usuario envía un archivo al bot, el archivo se carga primero en el almacenamiento OneDrive para la Empresa del usuario. A continuación, el bot recibirá una actividad de mensaje en la que se le notificará la carga del usuario. La actividad contendrá metadatos de archivo, como es su nombre y la dirección URL de contenido. Puede leer directamente desde esta dirección URL para capturar su contenido binario.

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
| `downloadUrl` | Dirección URL de OneDrive para capturar el contenido del archivo. Puede emitir un `HTTP GET` directamente desde esta dirección URL. |
| `uniqueId` | Identificador de archivo único. Este será el identificador del elemento de unidad de OneDrive, en el caso de que el usuario envíe un archivo al bot. |
| `fileType` | Tipo de extensión de archivo, como es pdf o docx. |

Como procedimiento recomendado, debe confirmar la carga de archivos devolviendo un mensaje al usuario.

### <a name="uploading-files-to-personal-chat"></a>Cargando archivos en un chat personal

La carga de un archivo en un usuario implica los pasos siguientes:

1. Envíe un mensaje al usuario que solicita permiso para escribir el archivo. Este mensaje debe contener `FileConsentCard` datos adjuntos con el nombre del archivo que se va a cargar.
2. Si el usuario acepta la descarga del archivo, el bot recibirá una actividad *Invocar* con una dirección URL de ubicación.
3. Para transferir el archivo, el bot realiza una `HTTP POST` directamente en la dirección URL de ubicación proporcionada.
4. Opcionalmente, puede quitar la tarjeta de consentimiento original si no desea permitir que el usuario acepte cargas adicionales del mismo archivo.

#### <a name="message-requesting-permission-to-upload"></a>Mensaje que solicita permiso para cargar

Este mensaje de escritorio contiene un objeto de datos adjuntos sencillo que solicita permiso de usuario para cargar el archivo:

:::image type="content" source="../../assets/images/bots/bot-file-consent-card.png" alt-text="Captura de pantalla de la tarjeta de consentimiento que solicita permiso de usuario para cargar el archivo":::

Este mensaje móvil contiene un objeto de datos adjuntos que solicita permiso de usuario para cargar el archivo:

![Captura de pantalla de la tarjeta de consentimiento que solicita permiso de usuario para cargar el archivo en dispositivos móviles](../../assets/images/bots/mobile-bot-file-consent-card.png)

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
| `description` | Descripción del archivo. Se puede mostrar al usuario para describir su propósito o para resumir su contenido. |
| `sizeInBytes` | Proporciona al usuario una estimación del tamaño del archivo y la cantidad de espacio que tardará en OneDrive. |
| `acceptContext` | Contexto adicional que se transmitirá silenciosamente al bot cuando el usuario acepte el archivo. |
| `declineContext` | Contexto adicional que se transmitirá silenciosamente al bot cuando el usuario rechace el archivo. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Invocación de la actividad cuando el usuario acepta el archivo

Se envía una actividad de invocación al bot cuando el usuario acepta el archivo. Contiene la dirección URL del marcador de posición OneDrive para la Empresa a la que el bot puede emitir un `PUT` para transferir el contenido del archivo. Para obtener información sobre cómo cargar en la dirección URL de OneDrive, lea este artículo: [Cargar bytes en la sesión de carga](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).

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

### <a name="notifying-the-user-about-an-uploaded-file"></a>Notificar al usuario sobre un archivo cargado

Después de cargar un archivo en el OneDrive del usuario, tanto si usa el mecanismo descrito anteriormente como las API delegadas por el usuario de OneDrive, debe enviar un mensaje de confirmación al usuario. Este mensaje debe contener un `FileCard` archivo adjunto en el que el usuario puede seleccionar, ya sea para obtener una vista previa, abrirlo en OneDrive o descargarlo localmente.

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
| `uniqueId` | Id. de elemento de unidad de OneDrive/SharePoint. |
| `fileType` | Tipo de archivo, como es pdf o docx. |

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

## <a name="see-also"></a>Vea también

[Trabajar con archivos en Microsoft Graph](/graph/api/resources/onedrive)
