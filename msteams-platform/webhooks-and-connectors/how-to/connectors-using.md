---
title: Crear y enviar mensajes
author: laujan
description: Describe cómo usar los Conectores de Office 365 en Microsoft Teams
ms.topic: how-to
ms.localizationpriority: medium
keywords: teams o365 conector
ms.openlocfilehash: 49f14862870fae216de1a6d810eacd4b23c81540
ms.sourcegitcommit: 85d0584877db21e2d3e49d3ee940d22675617582
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/29/2021
ms.locfileid: "61216198"
---
# <a name="create-and-send-messages"></a>Crear y enviar mensajes

Puede crear mensajes que puedan realizar acciones y enviarlos a través de Webhook entrante o Office 365 Connector.

## <a name="create-actionable-messages"></a>Crear mensajes que pueden actuar

Los mensajes que pueden actuar incluyen seis botones visibles en la tarjeta. Cada botón se define en la propiedad del mensaje mediante acciones, cada una con un tipo de entrada, un campo de texto, un selector de fechas o una lista de `potentialAction` `ActionCard` opciones múltiples. Cada `ActionCard` uno tiene una acción asociada, por ejemplo `HttpPOST` .

Las tarjetas de conector admiten las siguientes acciones:

- `ActionCard`: presenta uno o varios tipos de entrada y acciones asociadas.
- `HttpPOST`: envía la solicitud POST a una dirección URL.
- `OpenUri`: abre uri en un explorador o aplicación independiente, opcionalmente tiene como destino diferentes URI basados en sistemas operativos.

La acción `ActionCard` admite tres tipos de entrada:

- `TextInput`: un campo de texto de línea única o de varias líneas con un límite de longitud opcional.
- `DateInput`: selector de fecha con un selector de hora opcional.
- `MultichoiceInput`: Una lista enumerada de opciones que ofrecen una sola selección o varias selecciones.

`MultichoiceInput` admite una propiedad `style` que controla si inicialmente la lista se muestra totalmente expandida. El valor predeterminado de `style` depende del valor de la siguiente `isMultiSelect` manera:

| `isMultiSelect` | `style` predeterminado |
| --- | --- |
| `false` o no especificado | `compact` |
| `true` | `expanded` |

Para mostrar la lista de selección múltiple en el estilo compacto, debe especificar ambos `"isMultiSelect": true` y `"style": true` .

Para obtener más información sobre las acciones de tarjeta de conector, vea [Actions](/outlook/actionable-messages/card-reference#actions).

> [!NOTE]
> * Especificar `compact` para la propiedad `style` en Microsoft Teams es igual que especificar `normal` para la propiedad `style` en Microsoft Outlook.
> * Para la acción HttpPOST, el token de usuario se incluye con las solicitudes. Este token incluye la identidad de Azure AD del usuario de Office 365 que realizó la acción.

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a>Enviar un mensaje a través de Webhook entrante o Office 365 Connector

Para enviar un mensaje a través del Webhook entrante o Office 365 Connector, publique una carga JSON en la dirección URL del webhook. Esta carga debe tener la forma de una [Office 365 de conector .](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)

También puede usar este JSON para crear tarjetas que contengan entradas enriqueciendo, como entrada de texto, selección múltiple o selección de fecha y hora. El código que genera la tarjeta y la publica en la dirección URL de webhook puede ejecutarse en cualquier servicio hospedado. Estas tarjetas se definen como parte de los [](~/task-modules-and-cards/what-are-cards.md)mensajes que se pueden usar y también se admiten en tarjetas, que se usan Teams bots y extensiones de mensajería.

### <a name="example-of-connector-message"></a>Ejemplo de mensaje de conector

Un ejemplo de mensaje de conector es el siguiente:

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "Larry Bryant created a new task",
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
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
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
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "OpenUri",
        "name": "Learn More",
        "targets": [{
            "os": "default",
            "uri": "https://docs.microsoft.com/outlook/actionable-messages"
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
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }]
}
```

Este mensaje proporciona la siguiente tarjeta en el canal:

![Captura de pantalla de una tarjeta de conector](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a>Enviar mensajes con cURL y PowerShell

# <a name="curl"></a>[cURL](#tab/cURL)

**Para publicar un mensaje en el webhook con cURL**

1. Instale cURL con: https://curl.haxx.se/ .

1. Desde la línea de comandos, escriba el siguiente comando cURL:

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > Si post se realiza correctamente, debe ver una salida simple **1** por `curl` .

1. Compruebe en Microsoft Teams cliente la nueva tarjeta publicada.

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

 Requisito previo: instalación de PowerShell y familiarización con su uso básico.

**Para publicar un mensaje en el webhook con PowerShell**

1. Desde el símbolo del sistema de PowerShell, escriba el comando siguiente:

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > Si post se realiza correctamente, debe ver una salida simple **1** por `Invoke-RestMethod` .

1. Compruebe el canal de Microsoft Teams asociado a la dirección URL del webhook. Puede ver la nueva tarjeta publicada en el canal. Antes de usar el conector para probar o publicar la aplicación, debe hacer lo siguiente:

    - [Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).
    - Modifique la `icons` parte del manifiesto a los nombres de archivo de los iconos en lugar de las direcciones URL.

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>Enviar tarjetas adaptables mediante un webhook entrante

> [!NOTE]
> * Todos los elementos nativos del esquema de tarjeta adaptable, excepto `Action.Submit` , son totalmente compatibles.
> * Las acciones admitidas [**son Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)y [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).

**Para enviar tarjetas adaptables a través de un webhook entrante**

1. [Configure un webhook personalizado](~/webhooks-and-connectors/how-to/add-incoming-webhook.md) en Teams.
1. Cree un archivo JSON de tarjeta adaptable con el código siguiente:

    ```json
    {
       "type":"message",
       "attachments":[
          {
             "contentType":"application/vnd.microsoft.card.adaptive",
             "contentUrl":null,
             "content":{
                "$schema":"http://adaptivecards.io/schemas/adaptive-card.json",
                "type":"AdaptiveCard",
                "version":"1.2",
                "body":[
                    {
                    "type": "TextBlock",
                    "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)"
                    }
                ]
             }
          }
       ]
    }
    ```

    Las propiedades del archivo JSON de tarjeta adaptable son las siguientes:

    * El campo `"type"` debe ser `"message"`.
    * La matriz `"attachments"` contiene un conjunto de objetos de tarjeta.
    * El `"contentType"` campo debe establecerse en Tipo de tarjeta adaptable.
    * El objeto `"content"` es la tarjeta con formato JSON.

1. Pruebe la tarjeta adaptable con Postman:

    * Pruebe la tarjeta adaptable con [Postman](https://www.postman.com) para enviar una solicitud POST a la dirección URL, creada para configurar el webhook entrante.
    * Pegue el archivo JSON en el cuerpo de la solicitud y vea el mensaje de tarjeta adaptable en Teams.

> [!TIP]
> Use plantillas y [ejemplos de código de tarjeta](https://adaptivecards.io/samples) adaptable para probar el cuerpo de la solicitud POST.

## <a name="rate-limiting-for-connectors"></a>Limitación de velocidad para conectores

Los límites de velocidad de aplicación controlan el tráfico que puede generar un conector o un webhook entrante en un canal. Teams realizar un seguimiento de las solicitudes mediante una ventana de tasa fija y un contador incremental medidos en segundos. Si se realizan más de cuatro solicitudes en un segundo, la conexión de cliente se limita hasta que la ventana se actualiza durante la duración de la tasa fija.

### <a name="transactions-per-second-thresholds"></a>Umbrales de transacciones por segundo

En la tabla siguiente se proporcionan los detalles de transacciones basadas en tiempo:

| Tiempo en segundos  | Número máximo de solicitudes permitidas  |
|---|---|
| 1   | 4  |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

Una [lógica de reintentos con retroceso](/azure/architecture/patterns/retry) exponencial puede mitigar la limitación de velocidad en casos en los que las solicitudes superan los límites en un segundo. Siga [los procedimientos recomendados](../../bots/how-to/rate-limit.md) para evitar alcanzar los límites de velocidad.

> [!NOTE]
> Una [lógica de reintentos con retroceso](/azure/architecture/patterns/retry) exponencial puede mitigar la limitación de velocidad en casos en los que las solicitudes superan los límites en un segundo. Consulte las [respuestas HTTP 429](../../bots/how-to/rate-limit.md#handle-http-429-responses) para evitar superar los límites de velocidad.

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

Estos límites se aplican para reducir el correo no deseado de un canal por un conector y garantiza una experiencia óptima para los usuarios.

## <a name="see-also"></a>Consulte también

* [Office 365 conectores para Microsoft Teams](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Crear un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Crear un webhook saliente](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Limitación de velocidad para Teams bots](~/bots/how-to/rate-limit.md)
* [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Dar formato a tarjetas en Microsoft Teams](~/task-modules-and-cards/cards/cards-format.md)
