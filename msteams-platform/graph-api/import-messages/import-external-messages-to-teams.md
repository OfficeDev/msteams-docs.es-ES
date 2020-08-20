---
title: Usar Microsoft Graph para importar mensajes de la plataforma externa a teams
description: Describe cómo usar Microsoft Graph para importar mensajes de una plataforma externa a teams.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: margen de demora de los equipos mensajes de importación gráfico de API Microsoft migrar publicación de migración
ms.openlocfilehash: 8e8b21c9a38570d7ede745e27b9316b7aba29956
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "46820374"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Importar mensajes de una plataforma de terceros a Microsoft Teams con Microsoft Graph

>[!IMPORTANT]
> Las vistas previas públicas de Microsoft Graph y Microsoft Teams están disponibles para el acceso anticipado y los comentarios. Aunque esta versión se ha sometido a pruebas exhaustivas, no está pensada para su uso en producción.

Con Microsoft Graph, puede migrar los datos y el historial de mensajes existentes de los usuarios de un sistema externo a un canal de Teams. Al habilitar la recreación de una jerarquía de mensajería de una plataforma de terceros en Microsoft Teams, los usuarios pueden continuar sus comunicaciones de manera transparente y continuar sin interrupciones.

## <a name="import-overview"></a>Información general sobre la importación

En un nivel alto, el proceso de importación consta de lo siguiente:

1. [Crear un equipo con una marca de tiempo de fondo](#step-one-create-a-team)
1. [Crear un canal con una marca de tiempo de fondo](#step-two-create-a-channel)  
1. [Importar mensajes externos de fecha y hora de atrás](#step-three-import-messages)
1. [Completar el proceso de migración de equipos y canales](#step-four-complete-migration-mode)
1. [Agregar miembros del equipo](#step-five-add-team-members)

## <a name="necessary-requirements"></a>Requisitos necesarios

### <a name="analyze-and-prepare-message-data"></a>Analizar y preparar los datos de los mensajes

✔ Revise los datos de terceros para decidir qué se va a migrar.  
✔ Extraer los datos seleccionados del sistema de chat de terceros.  
✔ Convertir los datos de importación en el formato necesario para la migración.  
✔ Asignar la estructura de charla de terceros a la estructura de Teams.

### <a name="set-up-your-office-365-tenant"></a>Configurar el espacio empresarial de Office 365

✔ Asegúrese de que existe un inquilino de Office 365 para los datos de importación. Para obtener más información sobre cómo configurar un arrendamiento de Office 365 para Teams, *vea* [preparar el inquilino de Office 365](../../concepts/build-and-test/prepare-your-o365-tenant.md).  
✔ Asegúrese de que los integrantes del grupo estén en Azure Active Directory (AAD).  Para obtener más información, *consulte* [Agregar un nuevo usuario](/azure/active-directory/fundamentals/add-users-azure-active-directory) a Azure Active Directory.

## <a name="step-one-create-a-team"></a>Paso uno: crear un equipo

Como los datos existentes se migran, el mantenimiento de las marcas de tiempo del mensaje original y la prevención de la actividad de mensajería durante el proceso de migración son clave para volver a crear el flujo de mensajes existente del usuario en Microsoft Teams. Esto se logra de la siguiente manera:

1. [Cree un nuevo equipo](/graph/api/team-post?view=graph-rest-beta&tabs=http) con una marca de tiempo de fondo con la propiedad de recurso de equipo  `createdDateTime`  .  

1. Ponga el nuevo equipo en `migration mode` , un estado especial que reubique a los usuarios de la mayoría de las actividades del equipo hasta que se complete el proceso de migración. Incluya el `teamCreationMode` atributo de instancia con el `migration` valor en la solicitud post para identificar explícitamente el nuevo equipo como creado para la migración.  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>Permisos

|ScopeName|DisplayName|Descripción|Tipo|¿El consentimiento del administrador?|Entidades o API cubiertas|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Administrar la migración a Microsoft Teams|Creación, administración de recursos para la migración a Microsoft Teams|**Solo de la aplicación**|**Sí**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Solicitud (crear un equipo en el estado de migración)

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description"
  "createdDateTime": "2020-03-14T11:22:17.067Z"
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

* `createdDateTime`  establecer para el futuro.
* `createdDateTime`  se especificó correctamente, pero `teamCreationMode`  falta el atributo de instancia o está establecido en un valor no válido.

## <a name="step-two-create-a-channel"></a>Paso 2: crear un canal

La creación de un canal para los mensajes importados es similar al escenario crear equipo: 

1. [Cree un canal nuevo](/graph/api/channel-post?view=graph-rest-beta&tabs=http) con una marca de tiempo de fondo con la propiedad de recurso Channel `createdDateTime` .

1. Inserte el nuevo canal en `migration mode` , un estado especial que reubique a los usuarios de la mayoría de las actividades de chat en el canal hasta que se complete el proceso de migración.  Incluya el `channelCreationMode` atributo de instancia con el `migration` valor en la solicitud post para identificar explícitamente el nuevo equipo como creado para la migración.  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>Permisos

|ScopeName|DisplayName|Descripción|Tipo|¿El consentimiento del administrador?|Entidades o API cubiertas|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Administrar la migración a Microsoft Teams|Creación, administración de recursos para la migración a Microsoft Teams|**Solo de la aplicación**|**Sí**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>Solicitud (crear un canal en el estado de migración)

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a>Mensaje de error

```http
400 Bad Request
```

* `createdDateTime`  establecer para el futuro.
* `createdDateTime`  especificado correctamente pero el `channelCreationMode`  atributo de instancia falta o está establecido en un valor no válido.

## <a name="step-three-import-messages"></a>Paso tres: importar mensajes

Una vez que se han creado el equipo y el canal, puede empezar a enviar mensajes en tiempo de inactividad con las `createdDateTime` `from`  claves y en el cuerpo de la solicitud.

#### <a name="request-post-message-that-is-text-only"></a>Request (mensaje POST que es de solo texto)

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
    "replyToId": null,
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

#### <a name="request-post-a-message-with-inline-image"></a>Solicitud (publicar un mensaje con una imagen en línea)

> **Nota**: no hay ámbitos de permisos especiales en este escenario, ya que la solicitud es parte de chatMessage; los ámbitos para chatMessage también se aplican aquí.

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
    {
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-four-complete-migration-mode"></a>Paso cuatro: completar el modo de migración

Una vez que se ha completado el proceso de migración de mensajes, el equipo y el canal se sacan del modo de migración mediante el  `completeMigration`  método. Este paso abre los recursos de equipo y canal para uso general por parte de los miembros del equipo. La acción está enlazada a la `team` instancia.

#### <a name="request-end-team-migration-mode"></a>Solicitud (finalizar modo de migración de equipo)

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>Solicitud (modo de migración de canal de fin)

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

* Acción llamada en `team` o `channel` que no está en `migrationMode` .

## <a name="step-five-add-team-members"></a>Paso cinco: agregar miembros del equipo

Puede Agregar un miembro a un equipo [mediante la interfaz de usuario de Microsoft Teams o la](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) API de [miembro para agregar](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) de Microsoft Graph:

#### <a name="request-add-member"></a>Solicitud (agregar miembro)

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a>Sugerencias e información adicional

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* Puede importar mensajes de usuarios que no están en Microsoft Teams.

* Una vez que `completeMigration` se haya realizado la solicitud, no podrá importar más mensajes al equipo.

* Los integrantes del grupo solo se pueden agregar al nuevo equipo después de que la `completeMigration` solicitud haya devuelto una respuesta correcta.

* Limitación de peticiones: mensajes que se importan a 5 RPS por canal.

* Si necesita realizar una corrección de los resultados de la migración, debe eliminar el equipo y repetir los pasos para crear el equipo y el canal y volver a migrar los mensajes.

> [!NOTE]
> Actualmente, las imágenes insertadas son el único tipo de medios admitidos por el esquema de la API de importación de mensajes.

##### <a name="import-content-scope"></a>Ámbito de importación de contenido

|En el ámbito | Actualmente fuera de ámbito|
|----------|--------------------------|
|Mensajes de equipo y de canal|1:1 y mensajes de chat en grupo|
|Hora de creación del mensaje original|Canales privados|
|Imágenes en línea como parte del mensaje|A las menciones|
|Vínculos a archivos existentes en SPO/OneDrive|Comunicar|
|Mensajes con texto enriquecido|Vídeos|
|Cadena de respuesta de mensaje|Anuncios|
|Procesamiento de alto rendimiento|Fragmentos de código|
||Tarjetas adaptables|
||Adhesivos|
||Emojis|
||Las|
||Envíos cruzados entre canales|

> [!div class="nextstepaction"]
>[Más información sobre la integración de Microsoft Graph y Teams](/graph/teams-concept-overview)
