---
title: Agregar acciones de tarjeta en un bot
description: Describe las acciones de tarjeta en Microsoft Teams y cómo usarlas en los bots
ms.topic: conceptual
keywords: acciones de tarjetas de bots de teams
ms.openlocfilehash: f02e195f619fdfa2ebbc4b2ef00669a1cb5b38f6
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696027"
---
# <a name="card-actions"></a>Acciones de tarjeta

Las tarjetas usadas por bots y extensiones de mensajería en Teams admiten los siguientes tipos de actividad ( [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) ) . Tenga en cuenta que estas acciones difieren de las tarjetas de Conector de `potentialActions` Office 365 cuando se usan de Connectors.

| Tipo | Acción |
| --- | --- |
| `openUrl` | Abre una dirección URL en el explorador predeterminado. |
| `messageBack` | Envía un mensaje y una carga al bot (del usuario que ha hecho clic en el botón o ha pulsado la tarjeta) y envía un mensaje independiente a la secuencia de chat. |
| `imBack`| Envía un mensaje al bot (del usuario que ha hecho clic en el botón o ha pulsado la tarjeta). Este mensaje (de usuario a bot) es visible para todos los participantes de la conversación. |
| `invoke` | Envía un mensaje y una carga al bot (del usuario que ha hecho clic en el botón o ha pulsado la tarjeta). Este mensaje no está visible. |
| `signin` | Inicia el flujo de OAuth, lo que permite a los bots conectarse con servicios seguros. |

> [!NOTE]
>* Teams no admite tipos `CardAction` que no aparecen en la tabla anterior.
>* Teams no admite la `potentialActions` propiedad.
>* Las acciones de tarjeta son diferentes de [las acciones sugeridas](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) en Bot Framework/Azure Bot Service. Las acciones sugeridas no se admiten en Microsoft Teams: si quieres que los botones aparezcan en un mensaje de bot de Teams, usa una tarjeta.
>* Si usa una acción de tarjeta como parte de una extensión de mensajería, las acciones no funcionarán hasta que la tarjeta se envía al canal (no funcionarán mientras la tarjeta esté en el cuadro de mensaje de redacción).

Teams también admite [acciones de tarjetas adaptables,](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)que solo las usan las tarjetas adaptables. Estas acciones se enumeran en su propia sección al final de esta referencia.

## <a name="openurl"></a>openUrl

Este tipo de acción especifica una dirección URL que se iniciará en el explorador predeterminado. Tenga en cuenta que el bot no recibe ningún aviso en el que se hizo clic en el botón.

El `value` campo debe contener una dirección URL completa y correctamente formada.

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>messageBack

Con `messageBack` , puede crear una acción totalmente personalizada con las siguientes propiedades:

| Propiedad | Descripción |
| --- | --- |
| `title` | Aparece como la etiqueta del botón. |
| `displayText` | Opcional. El usuario hizo eco en la secuencia de chat cuando se realiza la acción. Este texto no *se* envía al bot. |
| `value` | Se envía al bot cuando se realiza la acción. Puede codificar el contexto de la acción, como identificadores únicos o un objeto JSON. |
| `text` | Se envía al bot cuando se realiza la acción. Use esta propiedad para simplificar el desarrollo de bots: el código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot. |

La flexibilidad de significa que el código puede elegir no dejar un mensaje de usuario visible en el historial simplemente sin `messageBack` usar `displayText` .

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

La `value` propiedad puede ser una cadena JSON serializada o un objeto JSON.

### <a name="inbound-message-example"></a>Ejemplo de mensaje entrante

`replyToId` contiene el identificador del mensaje del que provenía la acción de la tarjeta. Úselo si desea actualizar el mensaje.

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

## <a name="imback"></a>imBack

Esta acción desencadena un mensaje devuelto al bot, como si el usuario lo hubiera especificado en un mensaje de chat normal. El usuario, y todos los demás usuarios si están en un canal, verán la respuesta del botón.

El campo debe contener la cadena de texto que se hace eco en el chat y, por lo `value` tanto, se envía de nuevo al bot. Este es el texto del mensaje que procesará en el bot para realizar la lógica deseada. Nota: este campo es una cadena sencilla: no hay compatibilidad con el formato ni los caracteres ocultos.

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>invoke

La `invoke` acción se usa para invocar módulos de [tareas](~/task-modules-and-cards/task-modules/task-modules-bots.md).

La `invoke` acción contiene tres propiedades: , y `type` `title` `value` . La `value` propiedad puede contener una cadena, un objeto JSON con cadena o un objeto JSON.

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

Cuando un usuario hace clic en el botón, el bot recibirá el `value` objeto con información adicional. Tenga en cuenta que el tipo de actividad será `invoke` en lugar de ( `message` `activity.Type == "invoke"` ).

### <a name="example-invoke-button-definition-net"></a>Ejemplo: Invocar definición de botón (.NET)

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>Ejemplo: Mensaje de invocación entrante

La propiedad de nivel superior contiene el identificador del mensaje del que provenía la `replyToId` acción de la tarjeta. Úselo si desea actualizar el mensaje.

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

## <a name="signin"></a>signin

Inicia un flujo de OAuth, lo que permite a los bots conectarse con servicios seguros, como se describe con más detalle aquí: Flujo de [autenticación en bots](~/bots/how-to/authentication/auth-flow-bot.md).

## <a name="adaptive-cards-actions"></a>Acciones de tarjetas adaptables

Las tarjetas adaptables admiten tres tipos de acción:

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)

Además de las acciones mencionadas anteriormente, puede modificar la carga de la tarjeta adaptable para admitir acciones existentes de Bot Framework mediante una propiedad `Action.Submit` en el objeto de `msteams` `data` `Action.Submit` . En las secciones siguientes se detalla cómo usar acciones existentes de Bot Framework con tarjetas adaptables.

> [!NOTE]
> Agregar `msteams` a datos, con una acción de Bot Framework, no funciona con un módulo de tareas de tarjeta adaptable.

### <a name="adaptive-cards-with-messageback-action"></a>Tarjetas adaptables con acción messageBack

Para incluir una `messageBack` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto. Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Establecer en `messageBack` |
| `displayText` | Opcional. El usuario hizo eco en la secuencia de chat cuando se realiza la acción. Este texto no *se* envía al bot. |
| `value` | Se envía al bot cuando se realiza la acción. Puede codificar el contexto de la acción, como identificadores únicos o un objeto JSON. |
| `text` | Se envía al bot cuando se realiza la acción. Use esta propiedad para simplificar el desarrollo de bots: el código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot. |

#### <a name="example"></a>Ejemplo

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

### <a name="adaptive-cards-with-imback-action"></a>Tarjetas adaptables con acción de imBack

Para incluir una `imBack` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto. Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Establecer en `imBack` |
| `value` | Cadena que debe tener eco en el chat |

#### <a name="example"></a>Ejemplo

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

### <a name="adaptive-cards-with-signin-action"></a>Tarjetas adaptables con acción de inicio de sesión

Para incluir una `signin` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto. Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Establecer en `signin` |
| `value` | Establecer en la dirección URL a la que desea redirigir  |

#### <a name="example"></a>Ejemplo

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

### <a name="adaptive-cards-with-invoke-action"></a>Tarjetas adaptables con acción invocar
 
Para incluir una `invoke` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto. Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Establecer en `task/fetch` |
| `data` | Establecer el valor  |

#### <a name="example"></a>Ejemplo

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

#### <a name="example-2-with-additional-payload-data"></a>Ejemplo 2 (con datos de carga adicionales)

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
