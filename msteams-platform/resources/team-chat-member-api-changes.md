---
title: Cambios en la API de bot para los miembros del equipo o chat
author: ojasvichoudhary
description: Describe los próximos cambios en curso de las API de bot usadas para recuperar miembros de equipos y chats
keywords: Lista de miembros del equipo de apis de bot framework
ms.localizationpriority: medium
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 464283c145bf8b6cff6ac65db74c9e7b97c2d04b
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157262"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Teams api de bots para capturar miembros de equipo o chat

>[!NOTE]
> Se ha iniciado el proceso de desuso `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` y las API. Inicialmente, están muy limitadas a cinco solicitudes por minuto y devuelven un máximo de 10.000 miembros por equipo. Esto hace que no se devuelva la lista completa a medida que aumenta el tamaño del equipo.
> Debe actualizar a la versión 4.10 o posterior del SDK de Bot Framework y cambiar a los extremos de api paginados o a la `TeamsInfo.GetMemberAsync` API de usuario único. Esto también se aplica al bot incluso si no estás usando directamente estas API, ya que los SDK antiguos llaman a estas API durante [los eventos membersAdded.](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) Para ver la lista de próximos cambios, vea [Cambios de la API](team-chat-member-api-changes.md#api-changes).

Actualmente, si desea recuperar información para uno o varios miembros de un chat o equipo, puede usar las API de [bots](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) de Microsoft Teams para C# o para Las API de `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` TypeScript o Node.js. Para obtener más información, vea [fetch roster or user profile](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile).

Estas API tienen los siguientes defectos:

* Para equipos grandes, el rendimiento es bajo y los tiempos de espera son más probables: el tamaño máximo del equipo ha aumentado considerablemente desde Teams se publicó a principios de 2017. Como o devuelve toda la lista de miembros, la llamada a la API tarda mucho tiempo en volver para equipos grandes, y es común que la llamada se desalome y tenga que intentarlo de `GetMembersAsync` `getMembers` nuevo.
* Obtener detalles de perfil para un solo usuario es difícil: para obtener la información de perfil de un solo usuario, debe recuperar toda la lista de miembros y, a continuación, buscar la que desee. Hay una función auxiliar en el SDK de Bot Framework para que sea más sencilla, pero no es eficaz.

Con la introducción de equipos de toda la organización, hay un requisito para alinear mejor estas API con los Office 365 privacidad. Los bots usados en equipos grandes pueden recuperar información de perfil básica similar al permiso de Graph `User.ReadBasic.All` Microsoft. Los administradores de inquilinos tienen un gran control sobre qué aplicaciones y bots se pueden usar en su inquilino, pero esta configuración es diferente de microsoft Graph.

El siguiente código proporciona una representación JSON de ejemplo de lo que devuelven las API Teams bot:

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

Estos son los próximos cambios de api:

* Se crea una nueva API [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) para recuperar información de perfil para los miembros de un chat o equipo. Esta API ya está disponible con el SDK de Bot Framework versión 4.8 o posterior. Para el desarrollo en todas las demás versiones, use el [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) método.

    > [!NOTE]
    > En v3 o v4, la mejor acción es actualizar a la última versión de punto que es 3.30.2 o 4.8 o posterior respectivamente.

* Se crea una nueva API [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) para recuperar la información de perfil de un solo usuario. Toma el identificador del equipo o chat y un [UPN](/windows/win32/ad/naming-properties#userprincipalname) que es , Azure Active Directory Identificador de objeto o el identificador de usuario de Teams como parámetros y devuelve la información de perfil para `userPrincipalName` ese `objectId` `id` usuario.

    > [!NOTE]
    > `objectId` se cambia a `aadObjectId` para que coincida con lo que se llama en el objeto de un mensaje de Bot `Activity` Framework. La nueva API está disponible con la versión 4.8 o posterior del SDK de Bot Framework. También está disponible en la extensión Teams SDK bot Framework 3.x. Mientras tanto, puede usar el extremo [REST.](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details)

* `TeamsInfo.GetMembersAsync` en C# y `TeamsInfo.getMembers` en TypeScript o Node.js está formalmente en desuso. Una vez que la nueva API esté disponible, debes actualizar los bots para usarlos. Esto también se aplica a la [API de REST subyacente que usan estas API](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json).
* A finales de 2022, los bots no pueden recuperar proactivamente las propiedades or de los miembros `userPrincipalName` de un chat o `email` equipo. Los bots deben Graph para recuperarlos. Las `userPrincipalName` propiedades y no se `email` devuelven desde la nueva API a partir de `GetConversationPagedMembers` finales de 2022. Los bots deben usar Graph con un token de acceso para recuperar información. Se debe facilitar que los bots obtengan un token de acceso y simplifiquen y simplifiquen el proceso de consentimiento del usuario final.
