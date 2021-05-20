---
title: Cambios en la API de bot para los miembros del equipo o chat
author: ojasvichoudhary
description: Describe los cambios próximos y en curso en las API de Bot utilizadas para recuperar miembros de equipos y chats
keywords: lista de miembros del equipo de apis de bot framework
localization_priority: Normal
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 333a29664f0d60e89039f906fce77e71054d486f
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555440"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Teams cambios en la API de bots para obtener miembros del equipo o del chat

>[!NOTE]
> Se ha iniciado el proceso de desuso `TeamsInfo.getMembers` y `TeamsInfo.GetMembersAsync` las API. Inicialmente, están fuertemente limitados a cinco solicitudes por minuto y devuelven un máximo de 10K miembros por equipo. Esto hace que la lista completa no se devuelva a medida que aumenta el tamaño del equipo.
> Debe actualizar a la versión 4.10 o superior del SDK de Bot Framework y cambiar a los puntos de conexión de API paginados o a la API de `TeamsInfo.GetMemberAsync` usuario único. Esto también se aplica al bot incluso si no está utilizando directamente estas API, ya que los SDK anteriores llaman a estas API durante los eventos [membersAdded.](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) Para ver la lista de los próximos cambios, consulte [Cambios en la API.](team-chat-member-api-changes.md#api-changes) 

Actualmente, los desarrolladores de bots que desean recuperar información para uno o varios miembros de un chat o equipo usan las API de bot de Microsoft Teams `TeamsInfo.GetMembersAsync` para C# o `TeamsInfo.getMembers` para TypeScript o Node.js API. Para obtener más información, consulte [fetch roster o user profile](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile). Estas API tienen varias deficiencias.

Actualmente, si desea recuperar información para uno o varios miembros de un chat o equipo, puede usar las [API de bot de Microsoft Teams](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) para `TeamsInfo.GetMembersAsync` C# o para Las API de `TeamsInfo.getMembers` TypeScript o Node.js. Estas API tienen las siguientes deficiencias:

* Para los equipos grandes, el rendimiento es pobre y los tiempos de espera son más probables: el tamaño máximo del equipo ha crecido considerablemente desde que Teams fue lanzado a principios de 2017. Como `GetMembersAsync` o devuelve toda la lista de `getMembers` miembros, la llamada a la API tarda mucho tiempo en devolverse para equipos grandes, y es común que la llamada agote el tiempo de espera y tenga que intentarlo de nuevo.
* Obtener detalles de perfil para un solo usuario es difícil: para obtener la información de perfil de un solo usuario, debe recuperar toda la lista de miembros y, a continuación, buscar la que desee. Hay una función auxiliar en el SDK de Bot Framework para que sea más sencilla, pero no es eficaz.

Con la introducción de equipos de toda la organización, es necesario alinear mejor estas API con Office 365 controles de privacidad. Los bots utilizados en equipos grandes pueden recuperar información básica del perfil similar al `User.ReadBasic.All` permiso de Microsoft Graph. Los administradores de inquilinos tienen un gran control sobre qué aplicaciones y bots se pueden usar en su inquilino, pero esta configuración es diferente de Microsoft Graph.

El código siguiente proporciona una representación JSON de ejemplo de lo que devuelven las API de bot de Teams:

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

A continuación se presentan los próximos cambios en la API:

* Se crea una nueva API [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) para recuperar información de perfil para los miembros de un chat o equipo. Esta API ya está disponible con bot framework versión 4.8 o posterior SDK. Para el desarrollo en todas las demás versiones, utilice el [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) método.

    > [!NOTE]
    > En v3 o v4, la mejor acción es actualizar a la última versión de puntos que es 3.30.2 o 4.8 o posterior respectivamente.

* Se crea una nueva API [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) para recuperar la información de perfil de un solo usuario. Toma el ID del equipo o chat y un [UPN](/windows/win32/ad/naming-properties#userprincipalname) que `userPrincipalName` es, Azure Active Directory Id. de objeto, o el ID de `objectId` usuario Teams como parámetros y devuelve la información de perfil de ese `id` usuario.

    > [!NOTE]
    > `objectId` se cambia `aadObjectId` para que coincida con lo que se llama en el objeto de un mensaje de Bot `Activity` Framework. La nueva API está disponible con la versión 4.8 o posterior del SDK de Bot Framework. También está disponible en la extensión Teams SDK Bot Framework 3.x. Mientras tanto, puede usar el punto de conexión [REST.](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details)

* `TeamsInfo.GetMembersAsync` en C# y `TeamsInfo.getMembers` en TypeScript o Node.js está formalmente en desuso. Una vez que la nueva API esté disponible, debe actualizar los bots para usarlo. Esto también se aplica a la [API de REST subyacente que usan estas API.](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)
* A finales de 2021, los bots no pueden recuperar proactivamente las `userPrincipalName` propiedades o propiedades de los miembros de un chat o `email` equipo. Los bots deben usar Graph para recuperarlos. La `userPrincipalName` `email` nueva API no se devuelve desde la nueva API a partir de finales de `GetConversationPagedMembers` 2021. Los bots tienen que usar Graph con un token de acceso para recuperar información. Debe facilitarse a los bots obtener un token de acceso y optimizar y simplificar el proceso de consentimiento del usuario final.
