---
title: Cambios en la API de bot para miembros de equipo o chat (actualización de 2020)
author: ojasvichoudhary
description: Describe los cambios futuros y en curso de las API de bot que se usan para recuperar miembros de equipos y chats
keywords: API de bots Framework lista de miembros del equipo
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 243969796d9d1dc427ab7736cf5e0f0d320731c7
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796146"
---
# <a name="changes-to-teams-bot-apis-for-fetching-teamchat-members"></a>Cambios en las API de bot de Teams para obtener miembros de equipo o chat

Actualmente, los desarrolladores de bot que quieren recuperar información de uno o varios miembros de un chat o equipo usan las API de bot de Microsoft Teams `TeamsInfo.GetMembersAsync` (para C#) o `TeamsInfo.getMembers` (para TypeScript/Node.js) API (se [documenta aquí)](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetching-the-roster-or-user-profile). Estas API presentan varias deficiencias en la actualidad:

* **Para los equipos grandes, el rendimiento es deficiente y los tiempos de espera son más probables.** El tamaño máximo del equipo ha crecido considerablemente desde la publicación de Microsoft Teams a principios del 2017. Dado que `GetMembersAsync` / `getMembers` devuelve la lista completa de miembros, la llamada a la API tarda mucho tiempo en devolverse a los equipos grandes, por lo que no es raro que se agote el tiempo de espera y tiene que intentarlo de nuevo.
* **La obtención de detalles de perfil para un solo usuario es engorroso.** Para obtener la información de Perfil de un único usuario, tiene que recuperar la lista completa de miembros y, a continuación, buscar la que desee. True, hay una función auxiliar en el SDK de bot Framework para que sea más sencilla, pero en el caso de que no sea eficiente.

Por separado, con la introducción de los equipos de toda la organización, nos dimos cuenta de que se trataba de tiempo para alinear mejor estas API con los controles de privacidad de Office 365: los bots que se usan en los equipos grandes pueden recuperar información básica del perfil, que es similar al `User.ReadBasic.All` permiso de Microsoft Graph. Los administradores de espacios empresariales tienen una gran cantidad de control sobre qué aplicaciones y bots se pueden usar en su inquilino, pero estas opciones son diferentes de las que se rigen en Microsoft Graph.

Aquí tiene una representación JSON de ejemplo de lo que estas API devuelven actualmente. Haré referencia a algunos de los campos siguientes.

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

* Hemos creado una nueva API [`TeamsInfo.GetPagedMembersAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetching-the-roster-or-user-profile) para recuperar la información de Perfil de los miembros de un equipo o chat. Esta API ahora está disponible con bot Framework 4,8 SDK. Para el desarrollo en todas las demás versiones, use el [`GetConversationPagedMembers`](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable) método. **Nota** : en V3 o V4, la mejor acción es actualizar a la versión más reciente del punto (3.30.2 o 4,8 respectivamente). 
* Hemos creado una nueva API [`TeamsInfo.GetMemberAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) para recuperar la información de Perfil de un solo usuario. Toma el identificador del equipo/chat y un [UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) ( `userPrincipalName` , *vea más arriba* ), el identificador de objeto de Azure Active Directory ( `objectId` , *vea más arriba* ) o el identificador de usuario de Teams ( `id` , *vea lo anterior* ) como parámetros y devuelve la información de Perfil de ese usuario. **Nota** : estamos cambiando `objectId` a `aadObjectId` para que concuerda con lo que se llama en el `Activity` objeto de un mensaje de marco de bot. La nueva API está disponible con la versión 4,8 del SDK de bot Framework. Pronto estará disponible en el marco de bot extensiones de Team SDK, versión 3. x, y mientras tanto, puede usar el punto de conexión de [Rest](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) .
* `TeamsInfo.GetMembersAsync` (C#) y `TeamsInfo.getMembers` (TypeScript/Node.js) se ha dejado de usar formalmente y dejará de funcionar a finales de 2021. Anunciaremos un calendario específico en mayo de 2020, en función de los comentarios de los desarrolladores. Una vez que la nueva API paginada esté disponible, los desarrolladores deben actualizar sus bots para usarla. (Esto también se aplica a la [API de REST subyacente que usan estas API](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)).
* Con posterioridad a 2021, los bots no podrán recuperar de forma proactiva `userPrincipalName` las `email` propiedades o de los miembros de un chat o equipo, y deberán usar Microsoft Graph para recuperarlas. En concreto `userPrincipalName` , `email` no se devolverán las propiedades de la nueva `GetConversationPagedMembers` API a partir del 2021 posterior. Los bots tendrán que usar Microsoft Graph con un token de acceso para recuperar esta información. Obviamente esto es un cambio importante: debemos facilitar a los bots la tarea de obtener un token de acceso, y debemos racionalizar y simplificar el proceso de consentimiento del usuario final.

## <a name="feedback-and-more-information"></a>Comentarios y más información
Usaremos esta página para ofrecer información actualizada sobre estos cambios. Si tiene alguna pregunta, use "enviar comentarios > en esta p? gina" en la sección **comentarios** a continuación. 
