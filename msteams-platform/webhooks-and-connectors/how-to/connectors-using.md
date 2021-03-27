---
title: Envío de mensajes a conectores y webhooks
description: Describe cómo usar los Conectores de Office 365 en Microsoft Teams
ms.topic: how-to
localization_priority: Priority
keywords: teams o365 conector
ms.openlocfilehash: 6554a9cc1db0ffdae65f1cb875ca7a4c47c21259
ms.sourcegitcommit: 3727fc58e84b6f1752612884c2e0b25e207fb56e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/26/2021
ms.locfileid: "51382334"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a>Envío de mensajes a conectores y webhooks

Para enviar un mensaje a través del conector de Office 365 o el webhook de entrada, debe publicar una carga JSON en la dirección URL del webhook. Por lo general, esta carga será una [tarjeta de conector de Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

También puede usar este JSON para crear tarjetas que contengan entradas enriquecidas, como entrada de texto, selección múltiple o selección de una fecha y hora. El código que genera la tarjeta y publica en la dirección URL de webhook se puede ejecutar en cualquier servicio hospedado. Estas tarjetas se definen como parte de mensajes accionables, y también se admiten en las [tarjetas](~/task-modules-and-cards/what-are-cards.md) que se usan en los bots de Teams y las extensiones de mensajería.

### <a name="example-connector-message"></a>Ejemplo de mensaje de conector

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

Este mensaje produce la siguiente tarjeta en el canal.

![Captura de pantalla de una tarjeta de conector](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a>Creación de mensajes que requieren acción

En el ejemplo de la sección anterior se incluyen tres botones visibles en la tarjeta. Cada botón se define en la propiedad `potentialAction` del mensaje mediante acciones `ActionCard`, cada una de las cuales contiene un tipo de entrada: un campo de texto, un selector de fecha o una lista de opciones múltiples. Cada acción `ActionCard` tiene asociada una acción, por ejemplo `HttpPOST`.

Las tarjetas de conector admiten tres tipos de acciones:

- `ActionCard` Presenta uno o varios tipos de entrada y acciones asociadas.
- `HttpPOST` Envía una solicitud POST a una dirección URL.
- `OpenUri` Abre un identificador URI en un explorador o aplicación independiente. De manera opcional, marca como destino diferentes URI en función de los sistemas operativos.

La acción `ActionCard` admite tres tipos de entrada:

- `TextInput` Un campo de texto de una sola línea o multilínea con un límite de longitud opcional.
- `DateInput` Un selector de fecha con un selector de hora opcional.
- `MultichoiceInput` Una lista de opciones enumeradas que ofrece una sola selección o selecciones múltiples.

`MultichoiceInput` admite una propiedad `style` que controla si inicialmente la lista se muestra totalmente expandida. El valor predeterminado de `style` depende del valor de `isMultiSelect`.

| `isMultiSelect` | `style` predeterminado |
| --- | --- |
| `false` o no especificado | `compact` |
| `true` | `expanded` |

Si quiere que se muestre inicialmente una lista de selección múltiple en el estilo compacto, debe especificar `"isMultiSelect": true` y `"style": true`.

Para obtener más información sobre las acciones de tarjetas de conector, consulte **[Acciones]**(/outlook/actionable-messages/card-reference#actions) en la referencia de tarjeta de mensajes accionables.

> [!NOTE]
> Especificar `compact` para la propiedad `style` en Microsoft Teams es igual que especificar `normal` para la propiedad `style` en Microsoft Outlook.
> 
> Para la acción HttpPOST, el token de usuario se incluye con las solicitudes. Este token incluye la identidad de Azure AD del usuario de Office 365 que realizó la acción.

## <a name="setting-up-a-custom-incoming-webhook"></a>Configurar un webhook de entrada personalizado

Siga estos pasos para ver cómo se envía una tarjeta simple a un conector.

1. En Microsoft Teams, elija **Más opciones** (**&#8943;**) junto al nombre del canal y elija **Conectores**.
2. Desplácese por la lista de conectores hasta **Webhook entrante** y elija **Agregar**.
3. Escriba un nombre para el webhook, cargue una imagen para asociarla a los datos del webhook y elija **Crear**.
4. Copie el webhook en el portapapeles y guárdelo. Necesitará la dirección URL del webhook para enviar información a Microsoft Teams.
5. Seleccione **Listo**.

### <a name="post-a-message-to-the-webhook-using-curl"></a>Publicar un mensaje en webhook con cURL

Los siguientes pasos usan [cURL](https://curl.haxx.se/). Damos por sentado que lo tiene instalado y está familiarizado con su uso básico.

1. Desde la línea de comandos, escriba el siguiente comando cURL:

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

2. Si el envío se realiza correctamente, debería ver un resultado de salida **1** por `curl`.
3. Compruebe el cliente de Microsoft Team. Debería ver la nueva tarjeta publicada en el equipo.

### <a name="post-a-message-to-the-webhook-using-powershell"></a>Publicar un mensaje en webhook con PowerShell

Los siguientes pasos usan PowerShell. Damos por sentado que lo tiene instalado y está familiarizado con su uso básico.

1. Desde el símbolo del sistema de PowerShell, escriba el comando siguiente:

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. Si el envío se realiza correctamente, debería ver un resultado de salida **1** por `Invoke-RestMethod`.
3. Compruebe el canal de Microsoft Teams asociado a la dirección URL del webhook. Debería ver la nueva tarjeta publicada en el canal.

- [Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).
- Modifique la parte `icons` del manifiesto para hacer referencia a los nombres de archivo de los iconos en lugar de a las direcciones URL.

El archivo manifest.json siguiente contiene los elementos básicos necesarios para probar y enviar la aplicación.

> [!NOTE]
> Reemplace `id` y `connectorId` en el ejemplo siguiente con el GUID del conector.

#### <a name="example-manifestjson-with-connector"></a>Ejemplo de manifest.json con conector

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>Enviar tarjetas adaptables con un webhook entrante

> [!NOTE]
>
> ✔ Todos los elementos de esquema de tarjetas adaptables nativas, excepto `Action.Submit`, son completamente compatibles.
>
> ✔ Las acciones compatibles son [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), y [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).

### <a name="the-flow-for-sending-adaptive-cards-via-an-incoming-webhook-is-as-follows"></a>El flujo para el envío de [tarjetas adaptables](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) mediante un webhook entrante es el siguiente:

**1.** [Configurar un webhook personalizado](#setting-up-a-custom-incoming-webhook) en Teams.</br></br>
**2.** Crear el archivo JSON de la tarjeta adaptable:

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

> [!div class="checklist"]
>
> - El campo `"type"` debe ser `"message"`.
> - La matriz `"attachments"` contiene un conjunto de objetos de tarjeta.
> - El campo `"contentType"` debe establecerse en tipo de tarjeta adaptable.
> - El objeto `"content"` es la tarjeta con formato JSON.

**3.** Probar la tarjeta adaptable con Postman

Para probar la tarjeta adaptativa, puede usar [Postman](https://www.postman.com) para enviar una solicitud POST a la dirección URL que creó cuando configuró el webhook entrante. Pegue el archivo JSON en el cuerpo de la solicitud y vea el mensaje de la tarjeta adaptable en Teams.

>[!TIP]
> Puede usar el código de tarjeta adaptable [Ejemplos y plantillas](https://adaptivecards.io/samples) para el cuerpo de la solicitud Post de prueba.

## <a name="testing-your-connector"></a>Probar el conector

Para probar el conector, cárguelo en un equipo igual que lo haría con cualquier otra aplicación. Puede crear un paquete .zip mediante el archivo de manifiesto desde el Panel del programador de conectores (modificado como se indica en la sección anterior) y los dos archivos de icono.

Después de cargar la aplicación, abra la lista Conectores desde cualquier canal. Desplácese hasta la parte inferior para ver la aplicación en la sección **Cargada**.

![Captura de pantalla de la sección cargada en el cuadro de diálogo Conector](~/assets/images/connectors/connector_dialog_uploaded.png)

Ahora, puede iniciar la experiencia de configuración. Tenga en cuenta que este flujo se produce completamente en Microsoft Teams a través de una ventana emergente. Actualmente, este comportamiento es distinto de la experiencia de configuración en Conectores que hemos creado; estamos trabajando para unificar las experiencias.

Para comprobar que una acción `HttpPOST` está funcionando correctamente, utilice el [webhook entrante personalizado](#setting-up-a-custom-incoming-webhook).

## <a name="rate-limiting-for-connectors"></a>Limitación de velocidad para conectores

Los límites de velocidad de la aplicación controlan el tráfico que puede generar un conector o un webhook entrante en un canal. Teams realiza un seguimiento de las solicitudes a través de una ventana de velocidad fija y un contador incremental medido en segundos.  Si se hacen demasiadas solicitudes, se limita la conexión de cliente hasta que se actualice la ventana, es decir, mientras dure la velocidad fija.

### <a name="transactions-per-second-thresholds"></a>**Umbrales de transacciones por segundo**

| Tiempo (segundos)  | Número máximo de solicitudes permitidas  |
|---|---|
| 1   | 4  |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

*Consulte también* [Conectores de Office 365: Microsoft Teams](https://docs.microsoft.com/connectors/teams/)

Una [lógica de reintento con interrupción exponencial](/azure/architecture/patterns/retry) como la que se muestra a continuación mitigaría la restricción de velocidad en casos en que las solicitudes superen los límites en un segundo. Siga los [procedimientos recomendados](../../bots/how-to/rate-limit.md#best-practices) para evitar alcanzar los límites de velocidad.

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
 
Estos límites tienen el propósito de reducir el correo no deseado en un canal con un conector y garantizan una experiencia óptima para los usuarios finales.
