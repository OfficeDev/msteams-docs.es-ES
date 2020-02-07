---
title: Envío de mensajes a conectores y webhooks
description: Describe cómo usar los Conectores de Office 365 en Microsoft Teams
localization_priority: Priority
keywords: teams o365 conector
ms.openlocfilehash: b22159002713ccec6441f2128190e9944945aff6
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783916"
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
        "activityTitle": "![TestImage](https://47a92947.ngrok.io/Content/Images/default.png)Larry Bryant created a new task",
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
            "target": "http://..."
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
            "target": "http://..."
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
            "target": "http://..."
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

(Una cuarta acción, `ViewAction`, aún es compatible pero ya no es necesaria; use `OpenUri` en su lugar).

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

> [!NOTE]
> Especificar `compact` para la propiedad `style` en Microsoft Teams es igual que especificar `normal` para la propiedad `style` en Microsoft Outlook.

Para obtener más información sobre las acciones de la tarjeta conector, consulte **[Acciones](/outlook/actionable-messages/card-reference#actions)** en la referencia de la tarjeta de mensaje accionable.

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
   curl -H "Content-Type: application/json" -d "{\"text\": \"Hello World\"}" <YOUR WEBHOOK URL>
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

- Incluya dos iconos, siguiendo las instrucciones de [Iconos](~/concepts/build-and-test/apps-package.md#icons).
- Modifique la parte `icons` del manifiesto para hacer referencia a los nombres de archivo de los iconos en lugar de a las direcciones URL.

El archivo manifest.json siguiente contiene los elementos básicos necesarios para probar y enviar la aplicación.

> [!NOTE]
> Reemplace `id` y `connectorId` en el ejemplo siguiente con el GUID del conector.

#### <a name="example-manifestjson-with-connector"></a>Ejemplo de manifest.json con conector

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

## <a name="testing-your-connector"></a>Probar el conector

Para probar el conector, cárguelo en un equipo igual que lo haría con cualquier otra aplicación. Puede crear un paquete .zip mediante el archivo de manifiesto desde el Panel del programador de conectores (modificado como se indica en la sección anterior) y los dos archivos de icono.

Después de cargar la aplicación, abra la lista Conectores desde cualquier canal. Desplácese hasta la parte inferior para ver la aplicación en la sección **Cargada**.

![Captura de pantalla de la sección cargada en el cuadro de diálogo Conector](~/assets/images/connectors/connector_dialog_uploaded.png)

Ahora, puede iniciar la experiencia de configuración. Tenga en cuenta que este flujo se produce completamente en Microsoft Teams a través de una ventana emergente. Actualmente, este comportamiento es distinto de la experiencia de configuración en Conectores que hemos creado; estamos trabajando para unificar las experiencias.

Para comprobar que una acción `HttpPOST` está funcionando correctamente, utilice el [webhook entrante personalizado](#setting-up-a-custom-incoming-webhook).


## <a name="rate-limiting-for-connectors"></a>Limitación de velocidad para Conectores

Este límite controla el tráfico que puede generar un conector o un webhook entrante en un canal. Las solicitudes que realiza su webhook o conector se limitarán cuando se supere el umbral del límite de velocidad. La cantidad de tiempo para el comportamiento de limitación se relaciona directamente con los parámetros de velocidad de solicitudes superada. Por ejemplo, si un conector o webhook supera 100 solicitudes de mensajes en 3600 segundos, el conector se limitará durante los próximos 3600 segundos:

| Período de tiempo: (seg.)  | Máximo de solicitudes de mensaje permitidas  |
|---|---|
| 1   | 4  |  
| 30   | 60  |  
| 3600 (1 hora)  | 100  | 
| 7200 | 150  | 
| 86 400 (1 día) | 1800  | 

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
