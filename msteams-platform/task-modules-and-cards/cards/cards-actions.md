---
title: Agregar acciones de tarjeta en un bot
description: Describe las acciones de tarjeta en Microsoft Teams y cómo usarlas en sus bots.
ms.localizationpriority: medium
ms.topic: conceptual
keywords: acciones de tarjetas de bots de equipos
ms.openlocfilehash: 12100ca05d8e4ff4f68c934bc82e1f078dd0210e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103912"
---
# <a name="card-actions"></a>Acciones de tarjeta

Las tarjetas usadas por los bots y las extensiones de mensaje en Teams admiten los siguientes tipos de actividad[`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards):

> [!NOTE]
> Las acciones de `CardAction` difieren de `potentialActions` para las tarjetas del conector de Office 365 cuando se usan desde conectores.

| Tipo | Acción |
| --- | --- |
| `openUrl` | Abre una dirección URL en el explorador predeterminado. |
| `messageBack` | Envía un mensaje y una carga al bot desde el usuario que seleccionó el botón o tocó la tarjeta. Envía un mensaje independiente a la secuencia de chat. |
| `imBack`| Envía un mensaje al bot desde el usuario que seleccionó el botón o tocó la tarjeta. Este mensaje del usuario al bot es visible para todos los participantes de la conversación. |
| `invoke` | Envía un mensaje y una carga al bot desde el usuario que seleccionó el botón o tocó la tarjeta. Este mensaje no está visible. |
| `signin` | Inicia el flujo de OAuth, lo que permite a los bots conectarse con servicios seguros. |

> [!NOTE]
>
>* Teams no admite `CardAction` tipos no enumerados en la tabla anterior.
>* Teams no admite la `potentialActions` propiedad.
>* Las acciones de tarjeta son diferentes a [las acciones sugeridas](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) en Bot Framework o Azure Bot Service. Las acciones sugeridas no se admiten en Microsoft Teams. Si desea que los botones aparezcan en un mensaje de bot de Teams, use una tarjeta.
>* Si usa una acción de tarjeta como parte de una extensión de mensaje, las acciones no funcionarán hasta que la tarjeta se envíe al canal. Las acciones no funcionan mientras la tarjeta está en el cuadro de redacción del mensaje.

## <a name="action-type-openurl"></a>Tipo de acción, openURL

`openUrl` El tipo de acción especifica una dirección URL para iniciar en el explorador predeterminado.

> [!NOTE]
> El bot no recibe ningún aviso sobre qué botón fue seleccionado.

Con `openUrl`, puede crear una acción con las siguientes propiedades:

| Propiedad | Descripción |
| --- | --- |
| `title` | Aparece como la etiqueta del botón. |
| `value` | Este campo debe contener una dirección URL completa y con el formato correcto. |

# <a name="json"></a>[JSON](#tab/json)

El siguiente código muestra un ejemplo de `openUrl`un tipo de acción en JSON:

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[C#](#tab/csharp)

El siguiente código muestra un ejemplo de `openUrl`un tipo de acción en C#:

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

El siguiente código muestra un ejemplo de `openUrl`un tipo de acción en JavaScript:

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a>Tipo de acción messageBack

Con `messageBack`, puede crear una acción totalmente personalizada con las siguientes propiedades:

| Propiedad | Descripción |
| --- | --- |
| `title` | Aparece como la etiqueta del botón. |
| `displayText` | Opcional. Lo usa el usuario en la secuencia de chat cuando se realiza la acción. Este texto no se envía al bot. |
| `value` | Se envía al bot cuando se realiza la acción. Puede codificar el contexto para la acción, tales como identificadores únicos o un objeto JSON. |
| `text` | Se envía al bot cuando se realiza la acción. Use esta propiedad para simplificar el desarrollo de los bots. Su código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot. |

La flexibilidad de `messageBack` significa que su código no puede dejar un mensaje de usuario visible en el historial simplemente sin usar `displayText`.

# <a name="json"></a>[JSON](#tab/json)

El siguiente código muestra un ejemplo de `messageBack`un tipo de acción en JSON:

```json
{
  "buttons": [
    {
    "type": "messageBack",
    "title": "My MessageBack button",
    "displayText": "I clicked this button",
    "text": "User just clicked the MessageBack button",
    "value": "{\"property\": \"propertyValue\" }"
    }
  ]
}
```

La propiedad `value` puede ser una cadena JSON serializada o un objeto JSON.

# <a name="c"></a>[C#](#tab/csharp)

El siguiente código muestra un ejemplo de `messageBack`un tipo de acción en C#:

```csharp
var button = new CardAction()
{
    Type = ActionTypes.MessageBack,
    Title = "My MessageBack button",
    DisplayText = "I clicked this button",
    Text = "User just clicked the MessageBack button",
    Value = "{\"property\": \"propertyValue\" }"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

El siguiente código muestra un ejemplo de `messageBack`un tipo de acción en JavaScript:

```javascript
CardFactory.actions([
{
    type: 'messageBack',
    title: "My MessageBack button",
    displayText: "I clicked this button",
    text: "User just clicked the MessageBack button",
    value: {property: "propertyValue" }
}])
```

---

### <a name="inbound-message-example"></a>Ejemplo de un mensaje entrante

`replyToId` contiene el id. del mensaje del que proviene la acción de la tarjeta. Úselo si desea actualizar el mensaje.

El siguiente código muestra un ejemplo de un mensaje entrante:

```json
{
   "text":"User just clicked the MessageBack button",
   "value":{
      "property":"propertyValue"
   },
   "type":"message",
   "timestamp":"2017-06-22T22:38:47.407Z",
   "id":"f:5261769396935243054",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:102jd210jd010icsoaeclaejcoa9ue09u",
      "name":"John Smith"
   },
   "conversation":{
      "id":"19:malejcou081i20ojmlcau0@thread.skype;messageid=1498171086622"
   },
   "recipient":{
      "id":"28:76096e45-119f-4736-859c-6dfff54395f7",
      "name":"MyBot"
   },
   "entities":[
      {
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo" 
      }
   ],
   "channelData":{
      "channel":{
         "id":"19:malejcou081i20ojmlcau0@thread.skype"
      },
      "team":{
         "id":"19:12d021jdoijsaeoaue0u@thread.skype"
      },
      "tenant":{
         "id":"bec8e231-67ad-484e-87f4-3e5438390a77"
      }
   },
        "replyToId": "1575667808184",
}
```

## <a name="action-type-imback"></a>Tipo de acción imBack

La acción `imBack` desencadena un mensaje de devolución su bot, como si el usuario lo hubiera escrito en un mensaje de chat normal. Sul usuario y todos los demás usuarios de un canal pueden ver el botón de respuesta.

Con `imBack`, puede crear una acción con las siguientes propiedades:

| Propiedad | Descripción |
| --- | --- |
| `title` | Aparece como la etiqueta del botón. |
| `value` | Este campo debe contener la cadena de texto que se usa en el chat y, por tanto, se envía al bot. Este es el texto del mensaje que se procesa en su bot para realizar la lógica deseada. |

> [!NOTE]
> El campo `value` es una cadena simple. No se admite el formato ni los caracteres ocultos.

# <a name="json"></a>[JSON](#tab/json)

El siguiente código muestra un ejemplo de `imBack`un tipo de acción en JSON:

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[C#](#tab/csharp)

El siguiente código muestra un ejemplo de `imBack`un tipo de acción en C#:

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

El siguiente código muestra un ejemplo de `imBack`un tipo de acción en JavaScript:

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a>Tipo de acción invoke

La acción `invoke` se usa para invocar [módulos de tareas](~/task-modules-and-cards/task-modules/task-modules-bots.md).

La acción `invoke` contiene tres propiedades, `type`, `title`y `value`.

Con `invoke`, puede crear una acción con las siguientes propiedades:

| Propiedad | Descripción |
| --- | --- |
| `title` | Aparece como la etiqueta del botón. |
| `value` | Esta propiedad puede contener una cadena, un objeto JSON con cadenas o un objeto JSON. |

# <a name="json"></a>[JSON](#tab/json)

El siguiente código muestra un ejemplo de `invoke`un tipo de acción en JSON:

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

Cuando un usuario selecciona el botón, su bot recibe el objeto `value` con información adicional.

> [!NOTE]
> El tipo de actividad es `invoke` en lugar de `message` que es `activity.Type == "invoke"`.

# <a name="c"></a>[C#](#tab/csharp)

El siguiente código muestra un ejemplo de `invoke`un tipo de acción en C#:

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

El siguiente código muestra un ejemplo de `invoke`un tipo de acción Node.js:

```javascript
CardFactory.actions([
{
    type: "invoke",
    title: "Option 1",
    value: {
        option: "opt1"
    }
}])
```

---

### <a name="example-of-incoming-invoke-message"></a>Ejemplo de mensaje de invocación entrante

La propiedad del nível superiror`replyToId` contiene el id. del mensaje del cual proviene la acción de la tarjeta. Úselo si desea actualizar el mensaje.

El siguiente código muestra un ejemplo de un mensaje de invocación entrante:

```json
{
    "type": "invoke",
    "value": {
        "option": "opt1"
    },
    "timestamp": "2017-02-10T04:11:19.614Z",
    "localTimestamp": "2017-02-09T21:11:19.614-07:00",
    "id": "f:6894910862892785420",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1Eniglq0-uVL83xNB9GU6w_G5a4SZF0gcJLprZzhtEbel21G_5h-
    NgoprRw45mP0AXUIZVeqrsIHSYV4ntgfVJQ",
        "name": "John Doe"
    },
    "conversation": {
        "id": "19:97b1ec61-45bf-453c-9059-6e8984e0cef4_8d88f59b-ae61-4300-bec0-caace7d28446@unq.gbl.spaces"
    },
    "recipient": {
        "id": "28:8d88f59b-ae61-4300-bec0-caace7d28446",
        "name": "MyBot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Web",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "channel": {
            "id": "19:dc5ba12695be4eb7bf457cad6b4709eb@thread.skype"
        },
        "team": {
            "id": "19:712c61d0ef384e5fa681ba90ca943398@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

## <a name="action-type-signin"></a>Tipo de acción signin

`signin` El tipo de acción inicia un flujo de OAuth que permite a los bots conectarse con servicios seguros. Para más información, consulte [flujos de autenticación en bots](~/bots/how-to/authentication/auth-flow-bot.md).

Teams también admite[acciones de tarjetas adaptables](#adaptive-cards-actions) que solo usan las tarjetas adaptables.

# <a name="json"></a>[JSON](#tab/json)

El siguiente código muestra un ejemplo de `signin`un tipo de acción en JSON:

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[C#](#tab/csharp)

El siguiente código muestra un ejemplo de `signin`un tipo de acción en C#:

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

El siguiente código muestra un ejemplo de `signin`un tipo de acción en JavaScript:

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a>Acciones de tarjetas adaptables

Las arjetas adaptables admiten cuatro tipos de acción:

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

También puede modificar la carga `Action.Submit` de la tarjeta adaptable para admitir acciones de Bot Framework existentes mediante una`msteams`propiedad en el`data` objeto de `Action.Submit`. En la siguiente sección se proporcionan detalles sobre cómo usar las acciones de Bot Framework existentes con tarjetas adaptables.

> [!NOTE]
> Agregar `msteams` a los datos con una acción Bot Framework no funciona con un módulo de tareas de una tarjeta adaptable.

### <a name="adaptive-cards-with-messageback-action"></a>Tarjetas adaptables con la acción messageBack

Para incluir una acción `messageBack` con una tarjeta adaptable, incluya los detalles siguientes en el`msteams`objeto :

> [!NOTE]
> Puede incluir propiedades ocultas adicionales en el objeto `data`, si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Establecer a`messageBack`. |
| `displayText` | Opcional. Lo usa el usuario en la secuencia de chat cuando se realiza la acción. Este texto no se envía al bot. |
| `value` | Se envía al bot cuando se realiza la acción. Puede codificar el contexto para la acción, tales como identificadores únicos o un objeto JSON. |
| `text` | Se envía al bot cuando se realiza la acción. Use esta propiedad para simplificar el desarrollo de los bots. Su código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot. |

El siguiente código muestra un ejemplo de tarjetas adaptables `messageBack`con la acción:

```json
{
  "type": "Action.Submit",
  "title": "Click me for messageBack",
  "data": {
    "msteams": {
        "type": "messageBack",
        "displayText": "I clicked this button",
        "text": "text to bots",
        "value": "{\"bfKey\": \"bfVal\", \"conflictKey\": \"from value\"}"
    }
  }
}
```

### <a name="adaptive-cards-with-imback-action"></a>Tarjetas adaptables con la acción imBack

Para incluir una acción `imBack` con una tarjeta adaptable, incluya los detalles siguientes en el`msteams`objeto :

> [!NOTE]
> Puede incluir propiedades ocultas adicionales en el objeto `data`, si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Establecer a`imBack`. |
| `value` | Cadena que debe repetirse en el chat. |

El siguiente código muestra un ejemplo de tarjetas adaptables `imBack`con la acción:

```json
{
  "type": "Action.Submit",
  "title": "Click me for imBack",
  "data": {
    "msteams": {
        "type": "imBack",
        "value": "Text to reply in chat"
    }
  }
}
```

### <a name="adaptive-cards-with-signin-action"></a>Tarjetas adaptables con la acción signin

Para incluir una acción `signin` con una tarjeta adaptable, incluya los detalles siguientes en el`msteams`objeto :

> [!NOTE]
> Puede incluir propiedades ocultas adicionales en el objeto `data`, si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Establecer a`signin`. |
| `value` | Establézcala en la dirección URL a la que desea redirigir.  |

El siguiente código muestra un ejemplo de tarjetas adaptables `signin`con la acción:

```json
{
  "type": "Action.Submit",
  "title": "Click me for signin",
  "data": {
    "msteams": {
        "type": "signin",
        "value": "https://signin.com"
    }
  }
}
```

### <a name="adaptive-cards-with-invoke-action"></a>Tarjetas adaptables con la acción invoke

Para incluir una acción `invoke` con una tarjeta adaptable, incluya los detalles siguientes en el`msteams`objeto :

> [!NOTE]
> Puede incluir propiedades ocultas adicionales en el objeto `data`, si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Establecer a`task/fetch`. |
| `data` | Establezca el valor.  |

El siguiente código muestra un ejemplo de tarjetas adaptables `invoke`con la acción:

```json
{
  "type": "Action.Submit",
  "title": "submit",
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

El siguiente código muestra un ejemplo de tarjetas adaptables `invoke`con la acción con datos de carga adicionales:

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    },
    "Value1": "some value"
  }
}
```

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Acciones universales para tarjetas adaptables](../cards/Universal-actions-for-adaptive-cards/Overview.md)

## <a name="see-also"></a>Consulte también

* [Referencia de tarjetas](./cards-reference.md)
* [Uso de módulos de tareas desde los bots](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [Tarjetas adaptables en bots](../../bots/how-to/conversations/conversation-messages.md#adaptive-cards)
* [Acciones universales para tarjetas adaptables](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md)
* [Comentarios de finalización de formularios](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
