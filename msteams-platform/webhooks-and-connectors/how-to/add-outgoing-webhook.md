---
title: Crear un webhook saliente
author: laujan
description: describe cómo crear un webhook saliente
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
keywords: teams tabs outgoing webhook actionable message verify webhook
ms.openlocfilehash: 8dabf78cd27f0f59bd8ce617eb83ded24ecc3dc92478e7233bf8f8bb6a2a4e19
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57704318"
---
# <a name="create-outgoing-webhook"></a>Crear webhook saliente

El webhook saliente actúa como bot y busca mensajes en canales mediante **@mention**. Envía notificaciones a servicios web externos y responde con mensajes enriquecidos, que incluyen tarjetas e imágenes. Ayuda a omitir el proceso de creación de bots a través [del Microsoft Bot Framework](https://dev.botframework.com/).

## <a name="key-features-of-outgoing-webhook"></a>Características clave del webhook saliente

En la tabla siguiente se proporcionan las características y la descripción de los webhooks salientes:

| Características | Descripción |
| ------- | ----------- |
| Configuración con ámbito| Los webhooks están en el ámbito del nivel de equipo. El proceso de configuración obligatorio para cada uno agrega un webhook saliente. |
| Mensajería reactiva| Los usuarios deben usar @mention para que el webhook reciba mensajes. Actualmente, los usuarios solo pueden enviar mensajes a un webhook saliente en canales públicos y no dentro del ámbito personal o privado. |
|Intercambio de mensajes HTTP estándar|Las respuestas aparecen en la misma cadena que el mensaje de solicitud original y pueden incluir cualquier contenido de mensaje de Bot Framework, por ejemplo, texto enriquecido, imágenes, tarjetas y emojis. Aunque los webhooks salientes pueden usar tarjetas, no pueden usar ninguna acción de tarjeta excepto `openURL` para .|
| Teams Compatibilidad con métodos api|Los webhooks salientes envían un HTTP POST a un servicio web y obtienen una respuesta. No pueden tener acceso a otras API, como recuperar la lista o la lista de canales de un equipo.|

## <a name="create-outgoing-webhooks"></a>Crear webhooks salientes

Cree webhooks salientes y agregue bots personalizados a Teams.

**Para crear un webhook saliente**

1. Seleccione **Teams** en el panel izquierdo. La **Teams** aparece:

    ![Canal de Teams](~/assets/images/teamschannel.png)

1. En la **Teams,** seleccione el equipo necesario para crear un webhook saliente y seleccione el &#8226;&#8226;&#8226;. En el menú desplegable, seleccione **Administrar equipo**:

    ![Crear webhook saliente](~/assets/images/outgoingwebhook1.png)

1. Seleccione la **pestaña** Aplicaciones en la página del canal:

    ![Crear un webhook saliente](~/assets/images/outgoingwebhook2.png)

1. Seleccione **Crear un webhook saliente**:

    ![Crear webhooks salientes](~/assets/images/outgoingwebhook3.png)

1. Escriba los siguientes detalles en la **página Crear un webhook** saliente:

    * **Nombre:** el título del webhook y @mention pestaña.
    * **Dirección URL de devolución** de llamada: el extremo HTTPS que acepta cargas JSON y recibe solicitudes POST de Teams.
    * **Descripción:** una cadena detallada que aparece en la tarjeta de perfil y en el panel de aplicaciones de nivel de equipo.
    * **Imagen de** perfil: icono de aplicación para el webhook, que es opcional.

1. Seleccione **Crear**. El webhook saliente se agrega al canal del equipo actual:

    ![crear webhook saliente](~/assets/images/outgoingwebhook.png)

Aparece un cuadro de diálogo Código de autenticación de mensajes [(HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) basado en hash. Es un token de seguridad que se usa para autenticar llamadas entre Teams y el servicio externo designado.

>[!NOTE]
> El webhook saliente está disponible para los usuarios del equipo, solo si la dirección URL es válida y los tokens de autenticación de servidor y cliente son iguales. Por ejemplo, un protocolo de enlace HMAC.

En el siguiente escenario se proporcionan los detalles para agregar un webhook saliente:

* Escenario: insertar notificaciones de estado de cambio en un servidor Teams base de datos de canales a la aplicación.
* Ejemplo: tienes una línea de aplicación empresarial que realiza un seguimiento de todas las operaciones CRUD, como crear, leer, actualizar y eliminar. Estas operaciones se realizan en los registros de los empleados Teams canal de recursos humanos en un Office 365 arrendamiento.

# <a name="url-json-payload"></a>[Carga JSON de dirección URL](#tab/urljsonpayload)
**Crear una dirección URL en el servidor de la aplicación para aceptar y procesar una solicitud POST con una carga JSON**

El servicio recibe mensajes en un esquema de mensajería de servicio de bots de Azure estándar. El conector de Bot Framework es un servicio RESTful que permite procesar el intercambio de mensajes con formato JSON a través de protocolos HTTPS, tal como se documenta en la API de servicio de [bots de Azure.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference) Como alternativa, puede seguir el SDK de Microsoft Bot Framework para procesar y analizar mensajes. Para obtener más información, vea [Overview of Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).

Los webhooks salientes están en el ámbito `team` del nivel y son visibles para todos los miembros del equipo. Los usuarios deben **\@ mencionar** el nombre del webhook saliente para invocarlo en el canal.

# <a name="verify-hmac-token"></a>[Comprobar token HMAC](#tab/verifyhmactoken)
**Crear un método para comprobar el token HMAC de webhook saliente**

Usando un ejemplo de mensaje entrante e identificador: "contoso" de SigningKeyDictionary de {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.

Use el valor "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" en la autorización del encabezado de solicitud.

Para asegurarse de que el servicio recibe llamadas solo de clientes Teams reales, Teams proporciona un código HMAC en el encabezado de autorización `hmac` HTTP. Incluya siempre el código en el protocolo de autenticación.

El código siempre debe validar la firma HMAC incluida en la solicitud de la siguiente manera:

* Genere el token HMAC desde el cuerpo de la solicitud del mensaje. Hay bibliotecas estándar para hacerlo en la mayoría de la plataforma, como [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) para Node.js y Teams [ejemplo de webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) para C \# ). Microsoft Teams usa criptografía HMAC estándar SHA256. Debe convertir el cuerpo en una matriz de bytes en UTF8.
* Calcule el hash de la matriz de bytes del token de seguridad proporcionado por Teams cuando registró el webhook saliente en el Teams cliente. Vea [crear un webhook saliente](#create-outgoing-webhook).
* Convertir el hash en una cadena mediante codificación UTF-8.
* Compare el valor de cadena del hash generado con el valor proporcionado en la solicitud HTTP.

# <a name="method-to-respond"></a>[Método para responder](#tab/methodtorespond)
**Crear un método para enviar una respuesta correcta o de error**

Las respuestas de los webhooks salientes aparecen en la misma cadena de respuesta que el mensaje original. Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica al servicio y el código obtiene cinco segundos para responder al mensaje antes de que la conexión finalice.

### <a name="example-response"></a>Ejemplo de respuesta

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```
---

> [!NOTE]
> * Puede enviar mensajes de texto, tarjetas de héroe y tarjeta adaptables como datos adjuntos con el webhook saliente.
> * Las tarjetas admiten el formato. Para obtener más información, vea [format cards with markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).

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

* * *

## <a name="code-sample"></a>Ejemplo de código

|**Ejemplo de nombre** | **Descripción** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Webhooks salientes | Ejemplos para crear bots personalizados que se usarán en Microsoft Teams.| [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="see-also"></a>Consulte también
* [Crear un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Crear un Conector de Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Crear y enviar mensajes](~/webhooks-and-connectors/how-to/connectors-using.md)
