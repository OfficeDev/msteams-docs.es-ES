---
title: Compilación de aplicaciones para usuarios anónimos
author: v-sdhakshina
description: Obtenga información sobre cómo crear aplicaciones para usuarios anónimos y probar la experiencia entregada a los usuarios anónimos en aplicaciones de reunión con toda la configuración de administrador.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: ff897c5135740557e12898e7e5d231557b2e2823
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615506"
---
# <a name="build-apps-for-anonymous-users"></a>Compilación de aplicaciones para usuarios anónimos

Puede crear bots, extensiones de mensajería, tarjetas y módulos de tareas en la aplicación para interactuar con participantes anónimos de la reunión.

Para probar la experiencia de la aplicación para usuarios anónimos, seleccione la dirección URL de la invitación a la reunión y únase a ella desde una ventana del explorador privado.

## <a name="admin-setting-for-anonymous-user-app-interaction"></a>Administración configuración para la interacción anónima de la aplicación de usuario

Los administradores de Teams pueden usar el portal de administración para habilitar o deshabilitar la interacción anónima de aplicaciones de usuario para todo el inquilino. Esta opción está habilitada de manera predeterminada. Para obtener más información, consulte [Permitir que los usuarios anónimos interactúen con aplicaciones en reuniones](/microsoftteams/meeting-settings-in-teams).

## <a name="in-meeting-getcontext-from-teams-client-sdk"></a>In-Meeting getContext del SDK de cliente de Teams

Las aplicaciones reciben la siguiente información para un usuario anónimo cuando llaman a la `getContext` API desde la fase de aplicación compartida. Para reconocer usuarios anónimos, compruebe si hay un `userLicenseType` **valor desconocido.**

```csharp
"userObjectId": "8:anon:<GUID1>",
"userLicenseType": "Unknown",
"loginHint": "8:teamsvisitor:<ID>",
"userPrincipalName": "8:teamsvisitor:<ID>",
"tid": "<meeting organizer tenant ID>"
```

| **Nombre de propiedad** | **Descripción** |
| --- | --- |
| `userObjectId` | Valor único generado para el usuario anónimo. Este valor no se puede usar en las llamadas a las API de Graph. |
| `userLicenseType` | `Unknown`, representa al usuario anónimo. |
| `loginHint` | Valor generado único. Este valor no se puede usar como sugerencia en los flujos de inicio de sesión. |
| `userPrincipalName` | Valor generado único. Este valor no se puede usar en las llamadas a las API de Graph. |
| `tid` | Identificador de inquilino del organizador de la reunión. |

> [!NOTE]
> Cuando un usuario anónimo se une a una reunión, se genera un nuevo identificador de usuario. Cada vez que el usuario anónimo vuelve a unirse a una reunión, se genera un identificador de usuario diferente.

## <a name="bot-activities-and-apis"></a>Api y actividades de bot

Con algunas diferencias, las actividades enviadas al bot y las respuestas que recibe de las API del bot son coherentes entre los participantes de reuniones anónimos y no anónimos. En general:

* El identificador de usuario es un valor generado que es diferente cada vez que el usuario anónimo se une a la reunión.
* Se `aadObjectId` omite la propiedad .
* La `userRole` propiedad se establece en **anónima**.
* El identificador de inquilino proporcionado se establece en el identificador de inquilino del organizador de la reunión.

### <a name="get-members-and-get-single-member-apis"></a>Obtener miembros y obtener API de miembro único

Los [miembros get](/microsoftteams/platform/bots/how-to/get-teams-context#fetch-the-roster-or-user-profile) y [get single member](/microsoftteams/platform/bots/how-to/get-teams-context#get-single-member-details) API devuelven información limitada para los usuarios anónimos:

```json
{ 
  "id": "<GUID1>", 
  "name": "<AnonTest (Guest)>",  
  "tenantId": "<GUID2>", 
  "userRole": "anonymous" 
} 
```

| **Nombre de propiedad** | **Descripción** |
| --- | --- |
| `id` | Valor único generado para el usuario anónimo. |
| `name` | Nombre proporcionado por el usuario anónimo al unirse a la reunión. |
| `tenantId` | Identificador de inquilino del organizador de la reunión. |
| `userRole` | `anonymous`, representa al usuario anónimo. |

> [!NOTE]
> El identificador recibido de las API del bot y la API del SDK de cliente de Teams no son los mismos.

### <a name="conversationupdate-activity-membersadded-and-membersremoved"></a>Miembros de la actividad ConversationUpdateAgregar y MiembrosRemoved

```csharp
{ 
  "membersAdded": [ 
    { 
      "id": "<GUID1>" 
    } 
  ], 
  "type": "conversationUpdate", 
  "timestamp": "<timestamp>", 
  "id": "<event unique identifier>", 
  "channelId": "msteams", 
  "serviceUrl": "<serviceURL>", 
  "from": { 
    "id": "<GUID2>" 
  }, 
  "conversation": { 
    "isGroup": true, 
    "tenantId": "<tenant id>", 
    "id": "<conversation id>" 
  }, 
  "recipient": { 
    "id": "<bot id>", 
    "name": "<bot name>" 
  }, 
  "channelData": { 
    "tenant": { 
      "id": "<tenant id>" 
    }, 
    "source": null, 
    "meeting": { 
      "id": "<meeting id>" 
    } 
  } 
} 
```

| **Nombre de propiedad** | **Descripción** |
| --- | --- |
| `membersAdded.id` | Identificador de usuario anónimo. |
| `from.id` | Identificador del organizador de la reunión. |
| `conversation.tenantId` | Identificador de inquilino del organizador de la reunión. |
| `conversation.id` | Identificador de conversación del chat de reunión. |
| `tenant.id` | Identificador de inquilino del organizador de la reunión. |

Los cambios similares se aplican a la carga de actividad `membersRemoved` .

> [!NOTE]
>
> Cuando un usuario anónimo se une a una reunión o sale de ella, el `from` objeto de la carga siempre tiene el identificador del organizador de la reunión, incluso si otra persona ha realizado la acción.

### <a name="create-conversation-api"></a>Creación de Conversation API

Los bots no pueden iniciar una conversación uno a uno con un usuario anónimo. Si un bot llama a Create Conversation API con el identificador de usuario de un usuario anónimo, recibirá un `400` código de estado de solicitud incorrecta y la siguiente respuesta de error:

```csharp
{ 
  "error": {
    "code": "BadArgument",
    "message": "Bot cannot create a conversation with an anonymous user"
  }
} 
```

### <a name="adaptive-cards"></a>Tarjetas adaptables

Los usuarios anónimos pueden ver e interactuar con tarjetas adaptables en el chat de reunión. Las acciones de tarjeta adaptable se comportan de la misma manera para los usuarios anónimos y no anónimos. Para obtener más información, vea [Acciones de tarjeta](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json).

## <a name="known-issues-and-limitations"></a>Problemas y limitaciones conocidos

* Las pestañas del panel lateral y las burbujas de contenido no están disponibles para los usuarios anónimos. Los usuarios anónimos todavía pueden ver el contenido de la aplicación compartido en la fase de reunión.

* Para un usuario anónimo, el identificador de usuario de y el identificador de `getContext` usuario recibido por el bot son diferentes. No es posible correlacionar los dos directamente. Si necesita realizar un seguimiento de la identidad del usuario entre la pestaña y el bot, debe pedir al usuario que se autentique con un proveedor de identidades externo.

* Los usuarios anónimos verán un icono de aplicación genérico en los mensajes y tarjetas del bot, en lugar del icono real de la aplicación. Por ejemplo:

    :::image type="content" source="../assets/images/apps-in-meetings/app-icon.png" alt-text="En esta captura de pantalla se muestra cómo se muestra el icono de aplicación para el usuario anónimo.":::

## <a name="see-also"></a>Vea también

* [Compilación de aplicaciones para la fase de reunión de Teams](build-apps-for-teams-meeting-stage.md)
* [API de aplicaciones de reunión](meeting-apps-apis.md)
* [Cómo funcionan los bots de Microsoft Teams](/azure/bot-service/bot-builder-basics-teams)
