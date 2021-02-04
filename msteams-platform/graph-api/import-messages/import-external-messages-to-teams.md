---
title: Usar Microsoft Graph para importar mensajes de plataforma externa a Teams
description: Describe cómo usar Microsoft Graph para importar mensajes de una plataforma externa a Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 97f24c34ebb825aad0fd104c9a814e46f9b5fa0d
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093263"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Importar mensajes de plataformas de terceros a Teams con Microsoft Graph

>[!IMPORTANT]
> Las vistas previas públicas de Microsoft Graph y Microsoft Teams están disponibles para el acceso anticipado y los comentarios. Aunque esta versión se ha sometido a pruebas exhaustivas, no está pensada para su uso en producción.

Con Microsoft Graph, puede migrar el historial de mensajes y los datos existentes de los usuarios desde un sistema externo a un canal de Teams. Al habilitar la recreación de una jerarquía de mensajería de plataforma de terceros dentro de Teams, los usuarios pueden continuar sus comunicaciones sin problemas y continuar sin interrupciones.

## <a name="import-overview"></a>Introducción a la importación

En un nivel alto, el proceso de importación consta de lo siguiente:

1. [Crear un equipo con una marca de tiempo back-in-time](#step-one-create-a-team)
1. [Crear un canal con una marca de tiempo back-in-time](#step-two-create-a-channel)  
1. [Importar mensajes externos con fecha de espera](#step-three-import-messages)
1. [Completar el proceso de migración de equipos y canales](#step-four-complete-migration-mode)
1. [Agregar miembros del equipo](#step-five-add-team-members)

## <a name="necessary-requirements"></a>Requisitos necesarios

### <a name="analyze-and-prepare-message-data"></a>Analizar y preparar los datos del mensaje

✔ revisar los datos de terceros para decidir qué se migrará.  
✔ extraer los datos seleccionados del sistema de chat de terceros.  
✔ asignar la estructura de chat de terceros a la estructura de Teams.  
✔ convertir los datos de importación en el formato necesario para la migración.  

### <a name="set-up-your-office-365-tenant"></a>Configurar el espacio empresarial de Office 365

✔ asegúrese de que existe un inquilino de Office 365 para los datos de importación. Para obtener más información sobre cómo configurar un inquilino de Office 365 para *Teams,* vea , Preparar el espacio empresarial [de Office 365.](../../concepts/build-and-test/prepare-your-o365-tenant.md)  
✔ asegúrese de que los miembros del equipo están en Azure Active Directory (AAD).  Para obtener más *información, vea* [Agregar un nuevo usuario a](/azure/active-directory/fundamentals/add-users-azure-active-directory) Azure Active Directory.

## <a name="step-one-create-a-team"></a>Paso uno: Crear un equipo

Dado que los datos existentes se migran, el mantenimiento de las marcas de tiempo del mensaje original y la prevención de la actividad de mensajería durante el proceso de migración son clave para volver a crear el flujo de mensajes existente del usuario en Teams. Esto se logra de la siguiente manera:

> [Cree un nuevo equipo con](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) una marca de tiempo back-in-time con la propiedad de recurso de  `createdDateTime`  equipo. Coloque el nuevo equipo en un estado especial que resalte a los usuarios de la mayoría de las actividades dentro del equipo hasta que se `migration mode` complete el proceso de migración. Incluya el atributo de instancia con el valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado `teamCreationMode` `migration` para la migración.  

> **NOTA:** El campo solo se rellenará para las instancias de un equipo o canal que `createdDateTime` se hayan migrado.

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>Permisos

|ScopeName|DisplayName|Descripción|Tipo|¿Consentimiento del administrador?|Entidades/API cubiertas|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Administrar la migración a Microsoft Teams|Creación y administración de recursos para la migración a Microsoft Teams|**Solo aplicación**|**Sí**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Solicitud (crear un equipo en estado de migración)

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a>Mensajes de error

```http
400 Bad Request
```

* `createdDateTime`  se establece para el futuro.
* `createdDateTime`  especificado correctamente, pero falta `teamCreationMode`  el atributo de instancia o se establece en un valor no válido.

## <a name="step-two-create-a-channel"></a>Paso dos: Crear un canal

Crear un canal para los mensajes importados es similar al escenario de creación de equipo:

> [Crea un nuevo canal con](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) una marca de tiempo back-in-time mediante la propiedad de recurso de `createdDateTime` canal. Coloque el nuevo canal en un estado especial que resalte a los usuarios de la mayoría de las actividades de chat dentro del canal hasta que se complete `migration mode` el proceso de migración.  Incluya el atributo de instancia con el valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado `channelCreationMode` `migration` para la migración.  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>Permisos

|ScopeName|DisplayName|Descripción|Tipo|¿Consentimiento del administrador?|Entidades/API cubiertas|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Administrar la migración a Microsoft Teams|Creación y administración de recursos para la migración a Microsoft Teams|**Solo aplicación**|**Sí**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>Solicitud (crear un canal en estado de migración)

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.047Z"
}
```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 202 Accepted

{
   "@odata.context":"https://canary.graph.microsoft.com/testprodbetateamsgraphsvcncus/$metadata#teams('9cc6d6ab-07d8-4d14-bc2b-7db8995d6d23')/channels/$entity",
   "id":"19:e90f6814ce674072a4126206e7de485e@thread.tacv2",
   "createdDateTime":null,
   "displayName":"Architecture Discussion",
   "description":"This channel is where we debate all future architecture plans",
   "isFavoriteByDefault":null,
   "email":null,
   "webUrl":null,
   "membershipType":null,
   "moderationSettings":null
}
```

#### <a name="error-message"></a>Mensaje de error

```http
400 Bad Request
```

* `createdDateTime`  se establece para el futuro.
* `createdDateTime`  especificado correctamente, pero `channelCreationMode`  falta el atributo de instancia o se establece en un valor no válido.

## <a name="step-three-import-messages"></a>Paso tres: Importar mensajes

Una vez creados el equipo y el canal, puede empezar a enviar mensajes back-in-time con las claves y el cuerpo `createdDateTime` `from`  de la solicitud. **NOTA:** no se admiten los mensajes importados con versiones anteriores al `createdDateTime` hilo de `createdDateTime` mensaje.

> [!NOTE]
> * `createdDateTime` debe ser único en todos los mensajes del mismo subproceso.
> * `createdDateTime` admite marcas de tiempo con precisión de milisegundos. Por ejemplo, si el mensaje de solicitud entrante tiene el valor establecido como `createdDateTime` *2020-09-16T05:50:31.0025302Z*, se convertiría a *2020-09-16T05:50:31.002Z* cuando se ingera el mensaje.

#### <a name="request-post-message-that-is-text-only"></a>Solicitud (mensaje POST que es de solo texto)

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
   "createdDateTime":"2019-02-04T19:58:15.511Z",
   "from":{
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   }
}
```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 200 OK

{
   "@odata.context":"https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
   "id":"id-value",
   "replyToId":null,
   "etag":"id-value",
   "messageType":"message",
   "createdDateTime":"2019-02-04T19:58:15.58Z",
   "lastModifiedDateTime":null,
   "deleted":false,
   "subject":null,
   "summary":null,
   "importance":"normal",
   "locale":"en-us",
   "policyViolation":null,
   "from":{
      "application":null,
      "device":null,
      "conversation":null,
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   },
   "attachments":[
   ],
   "mentions":[
   ],
   "reactions":[
   ]
}
```

#### <a name="error-messages"></a>Mensajes de error

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>Solicitud (POST a message with inline image)

> **Nota:** no hay ámbitos de permisos especiales en este escenario, ya que la solicitud forma parte de chatMessage; los ámbitos de chatMessage también se aplican aquí.

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
  "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"../hostedContents/1/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "hostedContents":[
        {
            "@microsoft.graph.temporaryId": "1",
            "contentBytes": "iVBORw0KGgoAAAANSUhEUgAAANcAAAExCAYAAADvFzeeAAAXjklEQVR4Ae2d/XNU1RnH+9e0FFrA0RCIyaS8hRA0HV5KbS1gHRgVpjMClY4GHJ3yYm1HCmXaWttaaZUZtIIFKYi8lFAkvOQ9u5vN225IARVBbX9/Os9NbrLZbMjmhCfJPX5+2Lmb3T25y3O+n/M599x7w9f+++UXwoMakIF7n4GvUdR7X1RqSk01A8CFuZm5GGUAuIwKi72wF3ABF+YyygBwGRUWc2Eu4AIuzGWUAeAyKizmwlzABVyYyygDwGVUWMyFuYALuDCXUQaAy6iwmAtzARdwfWXMdeuzT+TGxz3Sfb1LunrapL07IW3pePDQ5/qavqef0c+OdYAELuAac4jGGkLL9rdvfyo9N9ODQAqBGmmrwGlb/R0u3xG4gMspOC5hG882CoRaaCSA8n1ff9doIQMu4PIOrus3u+8ZVNnw6e/Od5AALuDKOyz5hmqiPnfnzi1J9bSbgRWCpvvQfY307wQu4BoxJCOFaDK8rwsQmQsUIQhWW93XSIsewAVckYdLQ24F0Ui/926AARdwRRounZ6Np7GyYdN9DzdFBC7gijRc43GMlQ1U9s/6HXJNjYELuHI<<-----Removed----->>>>",
            "contentType": "image/png"
        }
    ]
}
```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 200 OK

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
    "id": "id-value",
    "replyToId": null,
    "etag": "id-value",
    "messageType": "message",
    "createdDateTime": "2019-02-04T19:58:15.511Z",
    "lastModifiedDateTime": null,
    "deleted": false,
    "subject": null,
    "summary": null,
    "importance": "normal",
    "locale": "en-us",
    "policyViolation": null,
    "from": {
        "application": null,
        "device": null,
        "conversation": null,
        "user": {
            "id": "id-value",
            "displayName": "Joh Doe",
            "userIdentityType": "aadUser"
        }
    },
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-four-complete-migration-mode"></a>Paso cuatro: Completar el modo de migración

Una vez completado el proceso de migración de mensajes, el equipo y el canal se sacarán del modo de migración mediante el  `completeMigration`  método. Este paso abre los recursos de equipo y canal para que los usen los miembros del equipo en general. La acción está enlazada a la `team` instancia.

#### <a name="request-end-team-migration-mode"></a>Solicitud (modo de migración de equipo final)

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>Solicitud (modo de migración de canal final)

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a>Respuesta de error

```http
400 Bad Request
```

* Acción llamada en un `team` o que no está en `channel` `migrationMode` .

## <a name="step-five-add-team-members"></a>Paso cinco: Agregar miembros del equipo

Puede agregar un miembro a un equipo mediante la INTERFAZ de usuario [de Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) o la API de miembro de Complemento [de](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) Microsoft Graph:

#### <a name="request-add-member"></a>Solicitud (agregar miembro)

```http
POST https://graph.microsoft.com/beta/teams/{id}/members
Content-type: application/json
Content-length: 30
{
"@odata.type": "#microsoft.graph.aadUserConversationMember",
"roles": [],
"user@odata.bind": "https://graph.microsoft.com/beta/users/{user-id}"
}
```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a>Sugerencias e información adicional

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* Puede importar mensajes de usuarios que no están en Teams. **NOTA:** Los mensajes importados para los usuarios que no están presentes en el inquilino no se podrán buscar en los portales de cumplimiento o cliente de Teams durante la versión preliminar pública.

* Una vez `completeMigration` realizada la solicitud, no podrá importar más mensajes en el equipo.

* Los miembros del equipo solo se pueden agregar al nuevo equipo después de `completeMigration` que la solicitud haya devuelto una respuesta correcta.

* Limitación: los mensajes se importan a 5 RPS por canal.

* Si necesita realizar una corrección en los resultados de la migración, debe eliminar el equipo y repetir los pasos para crear el equipo y el canal y volver a migrar los mensajes.

> [!NOTE]
> Actualmente, las imágenes en línea son el único tipo de medio admitido por el esquema de API de mensaje de importación.

##### <a name="import-content-scope"></a>Importar ámbito de contenido

|Dentro del ámbito | Actualmente fuera del ámbito|
|----------|--------------------------|
|Mensajes de equipo y canal|1:1 y mensajes de chat en grupo|
|Hora de creación del mensaje original|Canales privados|
|Imágenes en línea como parte del mensaje|Menciones|
|Vínculos a archivos existentes en SPO/OneDrive|Reacción|
|Mensajes con texto enriquecido|Vídeos|
|Cadena de respuesta de mensajes|Anuncios|
|Procesamiento de alto rendimiento|Fragmentos de código|
||Tarjetas adaptables|
||Adhesivos|
||Emojis|
||Comillas|
||Publicaciones cruzadas entre canales|

> [!div class="nextstepaction"]
>[Más información sobre la integración de Microsoft Graph y Teams](/graph/teams-concept-overview)
