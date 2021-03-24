---
title: Cambios en la API de bot para los miembros del equipo o chat
author: ojasvichoudhary
description: Describe los próximos cambios en curso de las API de bot usadas para recuperar miembros de equipos y chats
keywords: Lista de miembros del equipo de apis de bot framework
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: d55cbcdfea5e374c151c3eec82c52ac7f434c153
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034694"
---
# <a name="changes-to-teams-bot-apis-for-fetching-team-and-chat-members"></a>Cambios en las API de bots de Teams para capturar miembros de equipo y chat

>[!NOTE]
> Hemos empezado con el proceso de desuso para `TeamsInfo.getMembers` las API y las `TeamsInfo.GetMembersAsync` API. Inicialmente, se limitarán en gran medida a 5 solicitudes por minuto y devolverán un máximo de 10.000 miembros por equipo. Esto hará que no se devuelva la lista completa a medida que aumente el tamaño del equipo. 
> 
> **Debe actualizar a la versión 4.10** o posterior del SDK de Bot Framework y cambiar a los extremos de api paginados o a la `TeamsInfo.GetMemberAsync` API de usuario único. Esto también se aplica al bot incluso si no estás usando directamente estas API, ya que los SDK antiguos llaman a estas API durante [los eventos membersAdded.](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) Para ver la lista de próximos cambios, vea [Cambios de la API](team-chat-member-api-changes.md#api-changes). 

Actualmente, los desarrolladores de bots que desean recuperar información para uno o varios miembros de un chat o equipo usan las API de bots de Microsoft Teams `TeamsInfo.GetMembersAsync` (para C#) o `TeamsInfo.getMembers` (para TypeScript/Node.js) [(documentadas aquí).](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile) Estas API tienen varios defectos en la actualidad:

* **Para equipos grandes, el rendimiento es bajo y los tiempos de espera son más probables.** El tamaño máximo del equipo ha aumentado considerablemente desde que Microsoft Teams se lanzó a principios de 2017. Dado que devuelve toda la lista de miembros, la llamada a la API tarda mucho tiempo en volver para equipos grandes, y no es raro que la llamada se desalome y tenga que intentarlo de `GetMembersAsync` / `getMembers` nuevo.
* **Obtener detalles de perfil para un solo usuario es engorroso.** Para obtener la información de perfil de un solo usuario, debe recuperar toda la lista de miembros y, a continuación, buscar el que desee. True, hay una función auxiliar en el SDK de Bot Framework para que sea más sencilla, pero bajo las cubiertas no es eficaz.

Por separado, con la introducción de equipos de toda la organización, nos dimos cuenta de que era el momento de alinear mejor estas API con los controles de privacidad de Office 365: los bots usados en equipos grandes pueden recuperar información básica de perfil, que es similar al permiso de `User.ReadBasic.All` Microsoft Graph. Los administradores de inquilinos tienen un gran control sobre qué aplicaciones y bots se pueden usar en su inquilino, pero esta configuración es diferente de las que rigen Microsoft Graph.

Esta es una representación JSON de ejemplo de lo que devuelven estas API hoy en día. Me referiré a algunos de los campos siguientes.

```json
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
    "userRole": "anonymous"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
    "userRole": "user"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
    "userRole": "user"
}]
```

## <a name="api-changes"></a>Cambios en la API
Estos son los próximos cambios en la API:

* Hemos creado una nueva API para recuperar información [`TeamsInfo.GetPagedMembersAsync`](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile) de perfil para los miembros de un chat o equipo. Esta API ya está disponible con el SDK de Bot Framework 4.10. Para el desarrollo en todas las demás versiones, use el [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) método. 
  > [!NOTE]
  > En v3 o v4, la mejor acción es actualizar a la versión de punto más reciente. 
* Hemos creado una nueva API para [`TeamsInfo.GetMemberAsync`](../bots/how-to/get-teams-context.md#get-single-member-details) recuperar la información de perfil de un solo usuario. Toma el identificador del equipo/chat y un [UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) ( , vea más arriba ), El identificador de objeto de Azure Active Directory ( , vea más arriba ) o el id. de usuario de Teams ( , vea más arriba ) como parámetros y devuelve la información de perfil para ese `userPrincipalName`  `objectId`  `id` usuario.  
  > [!NOTE]
  > Estamos cambiando a para que coincida con lo que se `objectId` llama en el objeto de un mensaje de Bot `aadObjectId` `Activity` Framework. La nueva API está disponible con la versión 4.10 del SDK de Bot Framework. Pronto estará disponible en la extensión del SDK de Teams Bot Framework 3.x también; mientras tanto, puede usar el extremo [REST.](../bots/how-to/get-teams-context.md?get-single-member-details)
* `TeamsInfo.GetMembersAsync` (C#) y (TypeScript/Node.js) están formalmente en desuso y dejarán de funcionar a finales de `TeamsInfo.getMembers` 2021. Actualice los bots para usar las API paginadas. (Esto también se aplica a la [API de REST subyacente que usan estas API](../bots/how-to/get-teams-context.md)).)
* A finales de 2021, los bots no podrán recuperar proactivamente las propiedades or de los miembros de un chat o equipo y tendrán que usar Microsoft Graph para `userPrincipalName` `email` recuperarlas. En concreto, las propiedades no se devolverán desde la nueva API a `userPrincipalName` partir de `email` `GetConversationPagedMembers` finales de 2021. Los bots tendrán que usar Microsoft Graph con un token de acceso para recuperar esta información. Obviamente, este es un cambio importante: debemos facilitar que los bots obtengan un token de acceso y debemos simplificar y simplificar el proceso de consentimiento del usuario final.

## <a name="feedback-and-more-information"></a>Comentarios y más información
Usaremos esta página para proporcionar información actualizada sobre estos cambios. Si tiene preguntas, use la sección "Enviar comentarios > en esta página" en la **sección Comentarios** que aparece a continuación. 
