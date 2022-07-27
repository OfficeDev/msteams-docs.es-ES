---
title: Crear y enviar el módulo de tareas
author: surbhigupta
description: En este módulo, aprenderá a controlar la acción de invocación inicial y a responder con un módulo de tareas desde un comando de extensión de mensajería de acción.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 58b5d246c113262fa478a36246a224a52d160154
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035187"
---
# <a name="create-and-send-task-module"></a>Crear y enviar el módulo de tareas

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Puede crear el módulo de tareas mediante una tarjeta adaptable o una vista web insertada. Para crear un módulo de tareas, debe realizar el proceso denominado solicitud de invocación inicial. En este documento se trata la solicitud de invocación inicial, las propiedades de actividad de carga cuando se invoca un módulo de tareas desde el chat 1:1, el chat de grupo, el canal (nueva publicación), el canal (responder al subproceso) y el cuadro de comandos.
> [!NOTE]
> Si no va a rellenar el módulo de tareas con parámetros definidos en el manifiesto de la aplicación, debe crear el módulo de tareas para los usuarios con una tarjeta adaptable o una vista web insertada.

## <a name="the-initial-invoke-request"></a>La solicitud de invocación inicial

En el proceso de la solicitud de invocación inicial, el servicio recibe un objeto `Activity` de tipo `composeExtension/fetchTask` y debe responder con un objeto `task` que contenga una tarjeta adaptable o una dirección URL a la vista web incrustada. Junto con las propiedades de actividad del bot estándar, la carga de invocación inicial contiene los siguientes metadatos de solicitud:

|Nombre de propiedad|Objetivo|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke`. |
|`name`| Tipo de comando que se emite para el servicio. Debe ser `composeExtension/fetchTask`. |
|`from.id`| Id. del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Id de objeto Azure Active Directory identificador del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.channel.id`| Id. de canal (si la solicitud se realizó en un canal). |
|`channelData.team.id`| Id. de equipo (si la solicitud se realizó en un canal). |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose`. |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default`, `contrast` o `dark`. |

### <a name="example"></a>Ejemplo

El código para la solicitud de invocación inicial se proporciona en el ejemplo siguiente:

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a>Propiedades de actividad de carga cuando se invoca un módulo de tareas desde el chat 1:1

Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde el chat 1:1 se muestran de la siguiente manera:

|Nombre de propiedad|Objetivo|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke`. |
|`name`| Tipo de comando que se emite para el servicio. Debe ser `composeExtension/fetchTask`. |
|`from.id`| Id. del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Id de objeto Azure Active Directory identificador del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.source.name`| Nombre de origen desde el que se invoca el módulo de tareas. |
|`ChannelData.legacy. replyToId`| Obtiene o establece el identificador del mensaje para el que este mensaje es una respuesta. |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose`. |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default`, `contrast` o `dark`. |

### <a name="example"></a>Ejemplo

Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde el chat 1:1 se proporcionan en el ejemplo siguiente:

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a>Propiedades de actividad de carga cuando se invoca un módulo de tareas desde un chat de grupo

Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde un chat grupal se enumeran de la siguiente manera:

|Nombre de propiedad|Objetivo|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke`. |
|`name`| Tipo de comando que se emite para el servicio. Debe ser `composeExtension/fetchTask`. |
|`from.id`| Id. del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Id de objeto Azure Active Directory identificador del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.source.name`| Nombre de origen desde el que se invoca el módulo de tareas. |
|`ChannelData.legacy. replyToId`| Obtiene o establece el identificador del mensaje para el que este mensaje es una respuesta. |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose`. |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default`, `contrast` o `dark`. |

### <a name="example"></a>Ejemplo

Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde un chat grupal se proporcionan en el ejemplo siguiente:

```json
{
  "type": "invoke",
  "id": "f:bf72031f-a17e-f99c-48dc-5c0714950d87",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "groupChat",
    "id": "19:d77be72390a1416e9644261e9064fa00@thread.skype",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "213167a1e3b6428b93e186ea5407c759",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-meeting-chat"></a>Propiedades de actividad de carga cuando se invoca un módulo de tareas desde un chat de reunión

Las propiedades de la actividad de carga cuando se invoca un módulo de tareas desde un chat de reunión se proporcionan en el ejemplo siguiente:

```json
{
   "type": "invoke",
   "id": "f:4d271f11-4eed-622f-e820-6d82bf91692f",
   "channelId": "msteams",
   "from": {
      "id": "29:1yLsdbTM1UjxqqD8cjduNUCI1jm8xZaH3lx9u5JQ04t2bknuTCkP45TXdfROTOWk1LzN1AqTgFZUEqHIVGn_qUA",
      "name": "MOD Administrator",
      "aadObjectId": "ef16aa89-5b26-4a2c-aebb-761b551577c0"
   },
   "conversation": {
      "tenantId": "c9f9aafd-64ac-4f38-8e05-12feba3fb090",
      "id": "19:meeting_NTk4ZDY4ZmYtOWEzZS00OTRkLThhY2EtZmUzZmUzMDQyM2M0@thread.v2",
      "name": "Test meeting"
   },   
   "channelData": {
      "tenant": {
         "id": "c9f9aafd-64ac-4f38-8e05-12feba3fb090"
      },
      "source": {
         "name": "compose"
      },
      "meeting": {
         "id": "MCMxOTptZWV0aW5nX05UazRaRFk0Wm1ZdE9XRXpaUzAwT1RSa0xUaGhZMkV0Wm1VelptVXpNRFF5TTJNMEB0aHJlYWQudjIjMA=="
      }
   },
   "value": {
      "commandId": "Test",
      "commandContext": "compose",
      "requestId": "c46a6b53573f42b5bc801716e5ccc960",
      "context": {
         "theme": "default"
      }
   },
   "name": "composeExtension/fetchTask",
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a>Propiedades de actividad de carga cuando se invoca un módulo de tareas desde un canal (nueva publicación)

Las propiedades de la actividad de carga cuando se invoca un módulo de tareas desde un canal (nueva publicación) se enumeran de la siguiente manera:

|Nombre de propiedad|Objetivo|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke`. |
|`name`| Tipo de comando que se emite para el servicio. Debe ser `composeExtension/fetchTask`. |
|`from.id`| Id. del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Id de objeto Azure Active Directory identificador del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.channel.id`| Id. de canal (si la solicitud se realizó en un canal). |
|`channelData.team.id`| Id. de equipo (si la solicitud se realizó en un canal). |
|`channelData.source.name`| Nombre de origen desde el que se invoca el módulo de tareas. |
|`ChannelData.legacy. replyToId`| Obtiene o establece el identificador del mensaje para el que este mensaje es una respuesta. |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose`. |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default`, `contrast` o `dark`. |

### <a name="example"></a>Ejemplo

Las propiedades de la actividad de carga cuando se invoca un módulo de tareas desde un canal (nueva publicación) se proporcionan en el ejemplo siguiente:

```json
{
  "type": "invoke",
  "id": "f:a5fbb109-c989-c449-ee83-71ac99919d4b",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "5336640edc7748b28ce2df43f5b45963",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a>Propiedades de actividad de carga cuando se invoca un módulo de tareas desde un canal (respuesta al subproceso)

Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde un canal (respuesta al subproceso) se enumeran de la siguiente manera:

|Nombre de propiedad|Objetivo|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke`. |
|`name`| Tipo de comando que se emite para el servicio. Debe ser `composeExtension/fetchTask`. |
|`from.id`| Id. del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Id de objeto Azure Active Directory identificador del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.channel.id`| Id. de canal (si la solicitud se realizó en un canal). |
|`channelData.team.id`| Id. de equipo (si la solicitud se realizó en un canal). |
|`channelData.source.name`| Nombre de origen desde el que se invoca el módulo de tareas. |
|`ChannelData.legacy. replyToId`| Obtiene o establece el identificador del mensaje para el que este mensaje es una respuesta. |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose`. |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default`, `contrast` o `dark`. |

### <a name="example"></a>Ejemplo

Las propiedades de la actividad de carga cuando se invoca un módulo de tareas desde un canal (respuesta al subproceso) se proporcionan en el ejemplo siguiente:

```json
{
  "type": "invoke",
  "id": "f:19ccc884-c792-35ef-2f40-d0ff43dcca71",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype;messageid=1611060744833",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "message",
    "requestId": "7f7d22efe5414818becebcec649a7912",
    "messagePayload": {
      "linkToMessage": "https://teams.microsoft.com/l/message/19:6decf54d86d945e4b3924b63a9161a78@thread.skype/1611060744833",
      "id": "1611060744833",
      "replyToId": null,
      "createdDateTime": "2021-01-19T12:52:24.833Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "<div><div><at id=\"0\">Testing outgoing Webhook-Nikitha</at> - Hi</div>\n</div>"
      },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc",
          "displayName": "Olo Brockhouse"
        },
        "application": null
      },
      "reactions": [],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Testing outgoing Webhook-Nikitha",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": null,
            "application": {
              "applicationIdentityType": "webhook",
              "id": "b8c1c68c-e290-4bdd-81c3-266f310751dc",
              "displayName": "Testing outgoing Webhook-Nikitha"
            }
          }
        }
      ],
      "attachments": []
    },
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a>Propiedades de actividad de carga cuando se invoca un módulo de tareas desde un cuadro de comandos

Las propiedades de la actividad de carga cuando se invoca un módulo de tareas desde un cuadro de comando se enumeran de la siguiente manera:

|Nombre de propiedad|Objetivo|
|---|---|
|`type`| Tipo de solicitud. Debe ser `invoke`. |
|`name`| Tipo de comando que se emite para el servicio. Debe ser `composeExtension/fetchTask`. |
|`from.id`| Id. del usuario que envió la solicitud. |
|`from.name`| Nombre del usuario que envió la solicitud. |
|`from.aadObjectId`| Id de objeto Azure Active Directory identificador del usuario que envió la solicitud. |
|`channelData.tenant.id`| Identificador del inquilino de Azure Active Directory |
|`channelData.source.name`| Nombre de origen desde el que se invoca el módulo de tareas. |
|`value.commandId` | Contiene el identificador del comando que se invocó. |
|`value.commandContext` | Contexto que desencadenó el evento. Debe ser `compose`. |
|`value.context.theme` | El tema de cliente del usuario, útil para el formato de vista web incrustada. Debe ser `default`, `contrast` o `dark`. |

### <a name="example"></a>Ejemplo

Las propiedades de la actividad de carga cuando se invoca un módulo de tareas desde un cuadro de comando se proporcionan en el ejemplo siguiente:

```json
{
  "type": "invoke",
  "id": "f:172560f1-95f9-3189-edb2-b7612cd1a3cd",
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "compose",
    "requestId": "d2ce690cdc2b4920a538e75882610a30",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

### <a name="example"></a>Ejemplo

La siguiente sección de código es un ejemplo de solicitud `fetchTask`:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a>Solicitud de invocación inicial de un mensaje

Cuando se invoca el bot desde un mensaje, el objeto `value` en la solicitud de invocación inicial debe contener los detalles del mensaje desde el que se invoca la extensión de mensaje. Las matrices `reactions` y `mentions` son opcionales y no están presentes si no hay reacciones ni menciones en el mensaje original.
La sección siguiente es un ejemplo del objeto `value`:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a>Responder a fetchTask

Responda a la solicitud de invocación con un objeto `task` que contenga un objeto `taskInfo` con la tarjeta adaptable o la dirección URL web, o un mensaje de cadena simple.

|Nombre de propiedad|Objetivo|
|---|---|
|`type`| Puede ser `continue` para presentar un formulario o `message` para un elemento emergente simple. |
|`value`| Un objeto `taskInfo` para un formulario o un `string` para un mensaje. |

El esquema del objeto taskInfo es:

|Nombre de propiedad|Objetivo|
|---|---|
|`title`| Título del módulo de tareas.|
|`height`| Debe ser un entero (en píxeles) o `small`, `medium`, `large`.|
|`width`| Debe ser un entero (en píxeles) o `small`, `medium`, `large`.|
|`card`| Tarjeta adaptable que define el formulario (si se usa uno).
|`url`| Dirección URL que se va a abrir dentro del módulo de tareas como una vista web incrustada.|
|`fallbackUrl`| Si un cliente no admite la función del módulo de tareas, esta dirección URL se abre en una pestaña del explorador. |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a>Responder a fetchTask con una tarjeta adaptable

Al usar una tarjeta adaptable, debe responder con un objeto `task` con el objeto `value` que contiene una tarjeta adaptable.

#### <a name="example"></a>Ejemplo

La siguiente sección de código es un ejemplo para respuesta `fetchTask` con una tarjeta adaptable:

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

En este ejemplo se usa el paquete NuGet [AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards) además del SDK de Bot Framework.

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="create-a-task-module-with-an-embedded-web-view"></a>Creación de un módulo de tareas con una vista web insertada

Al usar una vista web incrustada, debe responder con un objeto `task` con el objeto `value` que contiene la dirección URL del formulario web que desea cargar. Los dominios de cualquier dirección URL que quiera cargar deben incluirse en la matriz `validDomains` del manifiesto de la aplicación. Para obtener más información sobre cómo compilar la vista web insertada, consulte la [documentación del módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md).

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a>Solicitud para instalar el bot conversacional

Si la aplicación contiene un bot conversacional, instale el bot en la conversación y, a continuación, cargue el módulo de tareas. El bot es útil para obtener contexto adicional para el módulo de tareas. Un ejemplo de este escenario es capturar la lista para rellenar un control selector de personas o la lista de canales de un equipo.

Cuando la extensión de mensaje recibe la invocación de `composeExtension/fetchTask`, compruebe si el bot está instalado en el contexto actual para facilitar el flujo. Por ejemplo, compruebe el flujo con una llamada de obtención de lista de participantes. Si el bot no está instalado, devuelva una tarjeta adaptable con una acción que solicite al usuario que instale el bot. El usuario debe tener permiso para instalar las aplicaciones en esa ubicación para la comprobación. Si la instalación de la aplicación no se realiza correctamente, el usuario recibe un mensaje para ponerse en contacto con el administrador.

#### <a name="example"></a>Ejemplo

La siguiente sección de código es un ejemplo de la respuesta:

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

Después de la instalación del bot conversacional, recibe otro mensaje de invocación con `name = composeExtension/submitAction`, y `value.data.msteams.justInTimeInstall = true`.

#### <a name="example"></a>Ejemplo

La siguiente sección de código es un ejemplo de la respuesta de la tarea a la invocación:

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

La respuesta de la tarea a la invocación debe ser similar a la del bot instalado.

#### <a name="example"></a>Ejemplo

La siguiente sección de código es un ejemplo de instalación cuando es necesario de la aplicación con tarjeta adaptable:

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre           | Descripción | .NET    | Node.js   | Python |
|:---------------------|:--------------|:---------|:--------|
|Acción de extensión de mensaje de Teams| Describe cómo definir comandos de acción, crear un módulo de tareas y responder a la acción de envío del módulo de tareas. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
|Búsqueda de extensión de mensaje de Teams   |  Describe cómo definir comandos de búsqueda y responder a búsquedas.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Responder al comando de acción](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

## <a name="see-also"></a>Consulte también

[Definir comandos de acción](~/messaging-extensions/how-to/action-commands/define-action-command.md)
