---
title: Crear un webhook saliente
author: laujan
description: En este módulo, aprenderá a crear un webhook saliente en Microsoft Teams junto con sus características clave y ejemplos de código
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: a290d7197c842c3920bd536fa71774fd82e47d84
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189894"
---
# <a name="create-outgoing-webhook"></a>Crear webhook saliente

El webhook saliente actúa como bot y busca mensajes en canales mediante **@mención**. Envía notificaciones a servicios web externos y responde con mensajes enriquecidos, que incluyen tarjetas e imágenes. Ayuda a omitir el proceso de creación de bots a través de [Microsoft Bot Framework](https://dev.botframework.com/).

<!--- TBD: Edit this article.
* Admonitions/alerts may be overused in this article. Check once.
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* Some screenshots like teamschannel.png may be redundant. Check once.
* Some headings use title case. We use sentence case for titles.
* Check for markdownlint errors. 
* Try using &nbsp; to add spaces in codeblocks for indentation and remove the hard tabs.
* Table with just a row is not really needed. Provide the content without tabulating it.
--->

Vea el siguiente vídeo para aprender a crear webhooks salientes:
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OIzu]
<br>

## <a name="key-features-of-outgoing-webhook"></a>Características clave del webhook saliente

En la tabla siguiente se proporcionan las características y la descripción de los webhooks salientes:

| Características | Descripción |
| ------- | ----------- |
| Configuración con ámbito| Los webhooks tienen como ámbito el nivel de equipo. El proceso de configuración obligatorio para cada uno agrega un webhook saliente. |
| Mensajería reactiva| Los usuarios deben usar @mención para que el webhook reciba mensajes. Actualmente, los usuarios solo pueden enviar mensajes a un webhook saliente en canales públicos y no dentro del ámbito personal o privado. |
|Intercambio de mensajes HTTP estándar|Las respuestas aparecen en la misma cadena que el mensaje de solicitud original y pueden incluir cualquier Bot Framework contenido del mensaje. Por ejemplo, texto enriquecido, imágenes, tarjetas y emojis. Aunque los webhooks salientes pueden usar tarjetas, no pueden usar ninguna acción de tarjeta excepto `openURL`.|
| Compatibilidad con el método de API de Teams|Los webhooks salientes envían una solicitud HTTP POST a un servicio web y obtienen una respuesta. No pueden acceder a ninguna otra API, como recuperar la lista de participantes o la lista de canales de un equipo.|

## <a name="create-outgoing-webhooks"></a>Crear webhooks salientes

Crear webhooks salientes y agregar bots personalizados a Teams.

Para crear un webhook saliente, siga estos pasos:

1. Seleccione **Teams** en el panel izquierdo. La página de **Teams** aparece:

    ![Canal de Teams](~/assets/images/teamschannel.png)

1. En la página de **Teams,** seleccione el equipo necesario para crear un webhook saliente y seleccione &#8226;&#8226;&#8226;. En el menú desplegable, seleccione **Administrar equipo**:

    ![Crear webhook saliente](~/assets/images/outgoingwebhook1.png)

1. Seleccione la pestaña **Aplicaciones** en la página del canal:

    ![Crear un webhook saliente](~/assets/images/outgoingwebhook2.png)

1. Seleccione **Crear un webhook saliente**:

    ![Crear webhooks salientes](~/assets/images/outgoingwebhook3.png)

1. Escriba los detalles siguientes en la página **Crear un webhook saliente**:

    * **Nombre:** el título del webhook y la pestaña @mención.
    * **Dirección URL de devolución de llamada**: el punto de conexión HTTPS que acepta cargas JSON y recibe solicitudes POST de Teams.
    * **Descripción**: una cadena detallada que aparece en la tarjeta de perfil y en el panel de la aplicación de nivel de equipo.
    * **Imagen de perfil**: un icono de aplicación para el webhook, que es opcional.

1. Seleccione **Crear**. El webhook saliente se agrega al canal del equipo actual:

    ![crear webhook saliente](~/assets/images/outgoingwebhook.png)

Aparece un cuadro de diálogo[Código de autenticación de mensajes basado en hash (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301). Es un token de seguridad que se usa para autenticar las llamadas entre Teams y el servicio externo designado. El token de seguridad HMAC no expira y es único para cada configuración.

>[!NOTE]
> El webhook saliente está disponible para los usuarios del equipo, solo si la dirección URL es válida y los tokens de autenticación de servidor y cliente son iguales. Por ejemplo, un protocolo de enlace HMAC.

En el escenario siguiente se proporcionan los detalles para agregar un webhook saliente:

* Escenario: enviar notificaciones de estado de cambios de inserción en un servidor de base de datos de canal de Teams a la aplicación.
* Ejemplo: tiene una aplicación de línea de negocio que realiza un seguimiento de todas las operaciones CRUD (crear, leer, actualizar y eliminar). Estas operaciones se realizan en los registros de empleados por parte de los usuarios de recursos humanos del canal de Teams en un inquilino de Office 365.

# <a name="url-json-payload"></a>[Carga JSON de dirección URL](#tab/urljsonpayload)

**Crear una dirección URL en el servidor de la aplicación para aceptar y procesar una solicitud POST con una carga JSON**

El servicio recibe mensajes en un esquema de mensajería estándar de Azure Bot Service. El conector de Bot Framework es un servicio RESTful que permite procesar el intercambio de mensajes con formato JSON a través de protocolos HTTPS, tal como se documenta en la [API de Azure Bot Service](/bot-framework/rest-api/bot-framework-rest-connector-api-reference). Como alternativa, puede seguir el SDK de Microsoft Bot Framework para procesar y analizar mensajes. Para obtener más información, consulte [Información general de Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).

Los webhooks salientes se limitan al nivel de `team` y son visibles para todos los miembros del equipo. Los usuarios deben **\@ mencionar** el nombre del webhook saliente para invocarlo en el canal.

# <a name="verify-hmac-token"></a>[Comprobar token HMAC](#tab/verifyhmactoken)

**Crear un método para comprobar el token HMAC de webhook saliente**

Usando el ejemplo de mensaje entrante e identificador: "contoso" de SigningKeyDictionary de {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hK Bytes/N2bOmlM31zaA=" }.

Use el valor "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" en la autorización del encabezado de solicitud.

Para asegurarse de que el servicio recibe llamadas solo de clientes reales de Teams, Teams proporciona un código HMAC en el encabezado de autorización HTTP `hmac`. Incluya siempre el código en su protocolo de autenticación.

El código siempre debe validar la firma HMAC incluida en la solicitud de la siguiente manera:

* Genere el token HMAC a partir del cuerpo de la solicitud del mensaje. Hay bibliotecas estándar para hacerlo en la mayoría de la plataforma, como [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) para Node.js y [Ejemplo de webhook de Teams](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) para C\#. Microsoft Teams usa criptografía SHA256 HMAC estándar. Debe convertir el cuerpo en una matriz de bytes en UTF8.
* Calcule el hash de la matriz de bytes del token de seguridad proporcionado por Teams cuando registró el webhook saliente en el cliente de Teams. Consulte [crear un Webhook de salida](#create-outgoing-webhook).
* Convierta el hash en una cadena mediante codificación UTF-8.
* Compare el valor de cadena del hash generado con el valor proporcionado en la solicitud HTTP.

# <a name="method-to-respond"></a>[Método para responder](#tab/methodtorespond)

**Crear un método para enviar una respuesta correcta o errónea**

Las respuestas de los webhooks salientes aparecen en la misma cadena de respuestas que el mensaje original. Cuando el usuario realiza una consulta, Teams emite una solicitud HTTP sincrónica al servicio y el código tiene cinco segundos para responder al mensaje antes de que se agote el tiempo de espera de la conexión y finalice.

### <a name="example-response"></a>Ejemplo de respuesta

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

---

> [!NOTE]
>
> * Puede enviar mensajes de texto, tarjetas prominentes y tarjetas adaptables como datos adjuntos con un webhook saliente.
> * Las tarjetas admiten el formato. Para más información, consulte [formatear tarjetas con Markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).
> * La tarjeta adaptable en webhooks salientes solo admite las acciones de la tarjeta `openURL`.

Los siguientes códigos son ejemplos de una respuesta de tarjeta adaptable:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

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

---

## <a name="code-sample"></a>Ejemplo de código

|**Ejemplo de nombre** | **Descripción** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Webhooks salientes | Ejemplos para crear bots personalizados para su uso en Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../../sbs-outgoing-webhooks.yml) para crear webhooks salientes en Teams.

## <a name="see-also"></a>Vea también

* [Creación de un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Crear un Conector de Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Crear y enviar mensajes](~/webhooks-and-connectors/how-to/connectors-using.md)
