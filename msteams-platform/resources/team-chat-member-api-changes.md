---
title: Cambios en la API de bot para los miembros del equipo o chat
author: ojasvichoudhary
description: Describe los próximos cambios en curso en las API de bot que se usan para recuperar miembros de equipos y chats
keywords: lista de miembros del equipo de api de bot framework
ms.localizationpriority: medium
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: f41e70352400814ede0d1cf683608b33e7c2ad72
ms.sourcegitcommit: 73e6767127cb27462f819acd71a1e480580bcf83
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2022
ms.locfileid: "65906235"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Cambios en la API del bot de Teams para capturar miembros del equipo o chat

>[!NOTE]
> Se inició el proceso de desuso de las API `TeamsInfo.getMembers` y `TeamsInfo.GetMembersAsync`. Inicialmente, están muy limitadas a cinco solicitudes por minuto y devuelven un máximo de 10 000 miembros por equipo. Como resultado, no se devuelve la lista completa a medida que aumenta el tamaño del equipo.
> Debe actualizar a la versión 4.10 o posterior del SDK de Bot Framework y cambiar a los puntos de conexión de API paginada o a la API de usuario único `TeamsInfo.GetMemberAsync`. Esto también se aplica al bot incluso si no usa directamente estas API, ya que los SDK más antiguos llaman a estas API durante los eventos de [miembros agregados](../bots/how-to/conversations/subscribe-to-conversation-events.md#members-added). Para ver la lista de los próximos cambios, consulte [Cambios de API](team-chat-member-api-changes.md#api-changes).

Actualmente, si desea recuperar información de uno o varios miembros de un chat o equipo, puede usar las [API de bot de Microsoft Teams](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)`TeamsInfo.GetMembersAsync` para C# o `TeamsInfo.getMembers` para las API de TypeScript o Node.js. Para obtener más información, vea [obtener la lista o el perfil de usuario](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile).

Estas API tienen las siguientes deficiencias:

* Para equipos grandes, el rendimiento es deficiente y los tiempos de espera son más probables: el tamaño máximo del equipo ha aumentado considerablemente desde que Teams se lanzó a principios de 2017. Como `GetMembersAsync` o `getMembers` devuelve toda la lista de miembros, la llamada API tarda mucho tiempo en devolverse para equipos grandes y es habitual que la llamada agote el tiempo de espera y tenga que intentarlo de nuevo.
* Obtener los detalles del perfil de un solo usuario es difícil: para obtener la información de perfil de un solo usuario, tiene que recuperar toda la lista de miembros y, a continuación, buscar la que desee. Hay una función auxiliar en el SDK de Bot Framework para simplificarla, pero no es eficaz.

Con la introducción de equipos de toda la organización, hay un requisito para alinear mejor estas API con los controles de privacidad de Office 365. Los bots usados en equipos grandes pueden recuperar información de perfil básica similar al permiso `User.ReadBasic.All` de Microsoft Graph. Los administradores de cuentas empresariales tienen un gran control sobre qué aplicaciones y bots se pueden usar en su cuenta empresarial, pero esta configuración es diferente de Microsoft Graph.

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

Estos son los próximos cambios en la API:

* Se crea una nueva API [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) para recuperar la información de perfil de los miembros de un chat o equipo. Esta API ya está disponible con el SDK de Bot Framework versión 4.8 o posterior. Para el desarrollo en todas las demás versiones, use el método [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true).

    > [!NOTE]
    > En v3 o v4, la mejor acción es actualizar a la versión más reciente que es 3.30.2, 4.8 o posterior, respectivamente.

* Se crea una nueva API [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) para recuperar la información de perfil de un solo usuario. Toma el identificador del equipo o chat y un [UPN](/windows/win32/ad/naming-properties#userprincipalname) que es el `userPrincipalName`, id. de objeto de Microsoft Azure Active Directory (Azure AD) `objectId` o el identificador de usuario de Teams `id` como parámetros y devuelve la información de perfil de ese usuario.

    > [!NOTE]
    > `objectId` se cambia a `aadObjectId` para que coincida con lo que se llama en el objeto `Activity` de un mensaje Bot Framework. La nueva API está disponible con la versión 4.8 o posterior del SDK de Bot Framework. También está disponible en la extensión del SDK de Bot Framework 3.x de Teams. Mientras tanto, puede usar el punto de conexión de [REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details).

* `TeamsInfo.GetMembersAsync` en C# y `TeamsInfo.getMembers` en TypeScript o Node.js están en desuso formalmente. Una vez que la nueva API está disponible, debe actualizar los bots para usarla. Esto también se aplica a la [API REST subyacente que estas API usan](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json).
* A finales de 2022, los bots no podrán recuperar proactivamente las propiedades `userPrincipalName` o `email` para los miembros de un chat o equipo. Los bots deben usar las API de Graph para recuperar la información necesaria. La nueva API `GetConversationPagedMembers` no podrá devolver las propiedades `userPrincipalName` y `email` a finales de 2022. Los bots deben usar la API de Graph con un token de acceso para recuperar información. 
