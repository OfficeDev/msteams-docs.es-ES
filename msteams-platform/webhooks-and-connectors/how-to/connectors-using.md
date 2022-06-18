---
title: Crear y enviar mensajes
author: laujan
description: En este módulo, aprenderá a usar conectores de Office 365 y a crear y enviar mensajes accionables en Microsoft Teams
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 86fe2237b5cf92c4fbc345f171cc8365baa0f348
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143266"
---
# <a name="create-and-send-messages"></a>Crear y enviar mensajes

Puede crear mensajes que requieren acción y enviarlos a través de un webhook entrante o el conector de Office 365.

## <a name="create-actionable-messages"></a>Crear mensajes que requieren acción

Los mensajes que requieren acción incluyen seis botones visibles en la tarjeta. Cada botón se define en la propiedad `potentialAction` del mensaje mediante acciones `ActionCard`, cada una de las cuales con un tipo de entrada, un campo de texto, un selector de fecha o una lista de opciones múltiples. Cada `ActionCard` tiene asociada una acción, por ejemplo `HttpPOST`.

Las tarjetas de conector admiten las siguientes acciones:

* `ActionCard`: presenta uno o varios tipos de entrada y acciones asociadas.
* `HttpPOST`: envía la solicitud POST a una dirección URL.
* `OpenUri`: abre un identificador URI en un explorador o aplicación independiente. De manera opcional, marca como destino diferentes URI en función de los sistemas operativos.

La acción `ActionCard` admite tres tipos de entrada:

* `TextInput`: campo de texto de una o varias líneas con un límite de longitud opcional.
* `DateInput`: selector de fecha con un selector de hora opcional.
* `MultichoiceInput`: una lista enumerada de opciones que ofrecen una sola selección o varias selecciones.

`MultichoiceInput` admite una propiedad `style` que controla si inicialmente la lista se muestra totalmente expandida. El valor predeterminado de `style` depende del valor de `isMultiSelect`, como se indica a continuación:

| `isMultiSelect` | `style` predeterminado |
| --- | --- |
| `false` o no especificado | `compact` |
| `true` | `expanded` |

Para mostrar la lista de selección múltiple en el estilo compacto, debe especificar `"isMultiSelect": true` y `"style": true`.

Para más información sobre las acciones de tarjeta de conector, vea [Acciones](/outlook/actionable-messages/card-reference#actions).

> [!NOTE]
>
> * Especificar `compact` para la propiedad `style` en Microsoft Teams es igual que especificar `normal` para la propiedad `style` en Microsoft Outlook.
> * Para la acción HttpPOST, el token de usuario se incluye con las solicitudes. Este token incluye la identidad de Microsoft Azure Active Directory (Azure AD) del usuario de Office 365 que realizó la acción.

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a>Enviar un mensaje a través del webhook entrante o del conector de Office 365

Para enviar un mensaje a través del conector de Office 365 o el webhook entrante, debe publicar una carga JSON en la dirección URL del webhook. Esta carga debe tener el formato de una [tarjeta de conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

También puede usar este JSON para crear tarjetas que contengan entradas enriquecidas, como entrada de texto, selección múltiple o selección de una fecha y hora. El código que genera la tarjeta y publica en la dirección URL de webhook se puede ejecutar en cualquier servicio hospedado. Estas tarjetas se definen como parte de mensajes que requieren acción y también se admiten en las[tarjetas](~/task-modules-and-cards/what-are-cards.md) que se usan en los bots de Teams y las extensiones de mensajería.

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

## <a name="send-messages-using-curl-and-powershell"></a>Envío de mensajes mediante cURL y PowerShell

# <a name="curl"></a>[cURL](#tab/cURL)

Para publicar un mensaje en el webhook con cURL, siga estos pasos:

1. Instale cURL desde el [sitio web de cURL](https://curl.haxx.se/).

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
    > Si el envío se realiza correctamente, debería ver un resultado de salida **1** por `curl`.

1. Compruebe la nueva tarjeta publicada en el cliente de Microsoft Teams.

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

 Requisito previo: instalación de PowerShell y familiarización con su uso básico.

Para publicar un mensaje en el webhook con PowerShell, siga estos pasos:

1. Desde el símbolo del sistema de PowerShell, escriba el comando siguiente:

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > Si el envío se realiza correctamente, debería ver un resultado de salida **1** por `Invoke-RestMethod`.

1. Compruebe el canal de Microsoft Teams asociado a la dirección URL del webhook. Puede ver la nueva tarjeta publicada en el canal. Antes de usar el conector para probar o publicar la aplicación, debe hacer lo siguiente:

    * [Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).
    * Modifique la parte `icons` del manifiesto para hacer referencia a los nombres de archivo de los iconos en lugar de a las direcciones URL.

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>Enviar tarjetas adaptables con un webhook entrante

> [!NOTE]
>
> * Todos los elementos de esquema de tarjetas adaptables nativas, excepto `Action.Submit`, son completamente compatibles.
> * Las acciones compatibles son [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html) y [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).

Para enviar tarjetas adaptables a través de un webhook entrante, siga estos pasos:

1. [Configurar un webhook personalizado](~/webhooks-and-connectors/how-to/add-incoming-webhook.md) en Teams.
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
    * El campo `"contentType"` debe establecerse en tipo de tarjeta adaptable.
    * El objeto `"content"` es la tarjeta con formato JSON.

1. Pruebe la tarjeta adaptable con Postman:

    * Pruebe la tarjeta adaptable con [Postman](https://www.postman.com) para enviar una solicitud POST a la dirección URL, creada para configurar el webhook entrante.
    * Pegue el archivo JSON en el cuerpo de la solicitud y vea el mensaje de la tarjeta adaptable en Teams.

> [!TIP]
> Use [plantillas y ejemplos de código](https://adaptivecards.io/samples) de tarjeta adaptable para probar el cuerpo de la solicitud POST.

## <a name="rate-limiting-for-connectors"></a>Limitación de velocidad para conectores

Los límites de velocidad de la aplicación controlan el tráfico que puede generar un conector o un webhook entrante en un canal. Teams realiza un seguimiento de las solicitudes a través de una ventana de velocidad fija y un contador incremental medido en segundos. Si se realizan más de cuatro solicitudes en un segundo, la conexión de cliente se limita hasta que la ventana se actualiza mientras dure la tasa fija.

### <a name="transactions-per-second-thresholds"></a>Umbrales de transacciones por segundo

En la tabla siguiente se proporcionan los detalles de la transacción basada en el tiempo:

| Tiempo en segundos  | Número máximo de solicitudes permitidas  |
|---|---|
| 1   | 4   |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

Una [lógica de reintento con interrupción exponencial](/azure/architecture/patterns/retry) puede mitigar la restricción de velocidad en casos en que las solicitudes superen los límites en un segundo. Siga los [procedimientos recomendados](../../bots/how-to/rate-limit.md) para evitar alcanzar los límites de velocidad.

> [!NOTE]
> Una [lógica de reintento con retroceso exponencial](/azure/architecture/patterns/retry) puede mitigar la limitación de velocidad en los casos en los que las solicitudes superan los límites en un segundo. Consulte [respuestas HTTP 429](../../bots/how-to/rate-limit.md#handle-http-429-responses) para evitar alcanzar los límites de velocidad.

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

Estos límites tienen el propósito de reducir el correo no deseado en un canal con un conector y garantizan una experiencia óptima para los usuarios.

## <a name="see-also"></a>Vea también

* [Conectores de Office 365 para Microsoft Teams](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Creación de un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Creación de un webhook saliente](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Limitación de velocidad para los mensajes de bots de Teams](~/bots/how-to/rate-limit.md)
* [Compilar pestañas con tarjetas adaptables](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Dar formato a tarjetas en Microsoft Teams](~/task-modules-and-cards/cards/cards-format.md)
