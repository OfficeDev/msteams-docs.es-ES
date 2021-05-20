---
title: Agregar acciones de tarjeta en un bot
description: Describe las acciones de la tarjeta en Microsoft Teams y cómo usarlas en los bots
localization_priority: Normal
ms.topic: conceptual
keywords: equipos bots tarjetas acciones
ms.openlocfilehash: b9276c7197070df43ba447707e6fa4d3d4098591
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566855"
---
# <a name="card-actions"></a>Acciones con tarjeta

Las tarjetas utilizadas por bots y extensiones de mensajería en Teams admiten los siguientes tipos de actividad ( [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) ). Tenga en cuenta que estas acciones difieren de `potentialActions` las tarjetas de conector de Office 365 cuando se usan desde conectores.

| Tipo | Action |
| --- | --- |
| `openUrl` | Abre una dirección URL en el explorador predeterminado. |
| `messageBack` | Envía un mensaje y carga al bot del usuario que ha hecho clic en el botón o ha tocado la tarjeta y envía un mensaje independiente a la secuencia de chat. |
| `imBack`| Envía un mensaje al bot del usuario que ha haciendo clic en el botón o ha tocado la tarjeta. Este mensaje (de usuario a bot) es visible para todos los participantes de la conversación. |
| `invoke` | Envía un mensaje y carga al bot del usuario que ha haciendo clic en el botón o ha tocado la tarjeta. Este mensaje no está visible. |
| `signin` | Inicia el flujo OAuth, lo que permite a los bots conectarse con servicios seguros. |

> [!NOTE]
>* Teams no admite `CardAction` tipos que no aparecen en la tabla anterior.
>* Teams no admite este `potentialActions` alojamiento.
>* Las acciones de tarjeta son diferentes de las [acciones sugeridas](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) en Bot Framework/Azure Bot Service. Las acciones sugeridas no se admiten en Microsoft Teams: si desea que los botones aparezcan en un mensaje de bot Teams, utilice una tarjeta.
>* Si utiliza una acción de tarjeta como parte de una extensión de mensajería, las acciones no funcionan hasta que la tarjeta se envía al canal. No funcionan mientras la tarjeta está en el cuadro de mensaje de composición.

Teams también admite [acciones de tarjetas adaptables,](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)que solo son utilizadas por las tarjetas adaptables. Estas acciones se enumeran en su propia sección al final de esta referencia.

## <a name="openurl"></a>openUrl

Este tipo de acción especifica una dirección URL que se iniciará en el explorador predeterminado. Tenga en cuenta que el bot no recibe ningún aviso en el que se haya hecho clic en el botón.

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
| `displayText` | Opcional. Se hace eco del usuario en la secuencia de chat cuando se realiza la acción. Este texto *no* se envía al bot. |
| `value` | Se envía al bot cuando se realiza la acción. Puede codificar el contexto de la acción, como identificadores únicos o un objeto JSON. |
| `text` | Se envía al bot cuando se realiza la acción. Utilice esta propiedad para simplificar el desarrollo de bots: el código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot. |

La flexibilidad de `messageBack` los medios para que el código pueda optar por no dejar un mensaje de usuario visible en el historial simplemente no mediante el uso `displayText` de .

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

`replyToId` contiene el IDENTIFICADOR del mensaje del que procede la acción de la tarjeta. Úsalo si quieres actualizar el mensaje.

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

Esta acción desencadena un mensaje de retorno al bot, como si el usuario lo escribió en un mensaje de chat normal. El usuario, y todos los demás usuarios si están en un canal, verán esa respuesta de botón.

El `value` campo debe contener la cadena de texto de la que se hace eco en el chat y, por lo tanto, se envía de vuelta al bot. Este es el texto del mensaje que procesará en el bot para realizar la lógica deseada. Nota: este campo es una cadena simple - no hay soporte para el formato o caracteres ocultos.

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>invocar

La `invoke` acción se utiliza para invocar módulos de [tareas.](~/task-modules-and-cards/task-modules/task-modules-bots.md)

La `invoke` acción contiene tres propiedades: , y `type` `title` `value` . La `value` propiedad puede contener una cadena, un objeto JSON encadenado o un objeto JSON.

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

La propiedad de nivel superior `replyToId` contiene el identificador del mensaje del que procede la acción de tarjeta. Úsalo si quieres actualizar el mensaje.

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

Inicia un flujo OAuth, lo que permite a los bots conectarse con servicios seguros, como se describe con más detalle aquí: [Flujo de autenticación en bots](~/bots/how-to/authentication/auth-flow-bot.md).

## <a name="adaptive-cards-actions"></a>Acciones de tarjetas adaptables

Las tarjetas adaptables admiten cuatro tipos de acción:

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Exelindo](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

Además de las acciones mencionadas anteriormente, puede modificar la carga útil de la tarjeta adaptable para admitir acciones existentes de `Action.Submit` Bot Framework mediante una propiedad en el objeto de `msteams` `data` `Action.Submit` . En las secciones siguientes se detalla cómo utilizar las acciones existentes de Bot Framework con tarjetas adaptables.

> [!NOTE]
> Agregar `msteams` a datos, con una acción de Bot Framework, no funciona con un módulo de tareas de tarjeta adaptable.

### <a name="adaptive-cards-with-messageback-action"></a>Tarjetas adaptables con acción messageBack

Para incluir una `messageBack` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto. Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Establecer en `messageBack` |
| `displayText` | Opcional. Se hace eco del usuario en la secuencia de chat cuando se realiza la acción. Este texto *no* se envía al bot. |
| `value` | Se envía al bot cuando se realiza la acción. Puede codificar el contexto de la acción, como identificadores únicos o un objeto JSON. |
| `text` | Se envía al bot cuando se realiza la acción. Utilice esta propiedad para simplificar el desarrollo de bots: el código puede comprobar una sola propiedad de nivel superior para distribuir la lógica del bot. |

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

### <a name="adaptive-cards-with-imback-action"></a>Tarjetas adaptables con acción imBack

Para incluir una `imBack` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto. Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Establecer en `imBack` |
| `value` | Cadena de la que hay que volver a hacerse eco en el chat |

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

### <a name="adaptive-cards-with-signin-action"></a>Tarjetas adaptables con acción de firma

Para incluir una `signin` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto. Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Estad en `signin` . |
| `value` | Establezca en la dirección URL a la que desea redirigir.  |

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

### <a name="adaptive-cards-with-invoke-action"></a>Tarjetas adaptables con acción de invocación
 
Para incluir una `invoke` acción con una tarjeta adaptable, incluya los siguientes detalles en el `msteams` objeto. Tenga en cuenta que puede incluir propiedades ocultas adicionales en el `data` objeto si es necesario.

| Propiedad | Descripción |
| --- | --- |
| `type` | Establecer en `task/fetch` |
| `data` | Establezca el valor  |

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

#### <a name="example-2-with-additional-payload-data"></a>Ejemplo 2 (con datos de carga útil adicionales)

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
