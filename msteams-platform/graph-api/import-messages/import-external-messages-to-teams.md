---
title: Use Microsoft Graph para importar mensajes de plataforma externa a Teams
description: Describe cómo usar Microsoft Graph importar mensajes desde una plataforma externa a Teams
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: Teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 559dcc1c6ab19032854ca5a431268bed0ea2540f
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398641"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Importar mensajes de plataformas de terceros a Teams con Microsoft Graph

Con Microsoft Graph, puede migrar el historial de mensajes y los datos existentes de los usuarios desde un sistema externo a un canal Teams usuario. Al habilitar la recreación de una jerarquía de mensajería de plataforma de terceros dentro de Teams, los usuarios pueden continuar sus comunicaciones sin problemas y continuar sin interrupciones.

> [!NOTE]
> En el futuro, Microsoft puede solicitarle a usted o a sus clientes que paguen tarifas adicionales en función de la cantidad de datos que se importen.

## <a name="import-overview"></a>Introducción a la importación

En un nivel alto, el proceso de importación consta de lo siguiente:

1. [Cree un equipo con una marca de tiempo back-in-time](#step-1-create-a-team).
1. [Cree un canal con una marca de tiempo back-in-time](#step-2-create-a-channel).
1. [Importar mensajes con fecha de back-in-time externos](#step-3-import-messages).
1. [Complete el proceso de migración de equipos y canales](#step-4-complete-migration-mode).
1. [Agregar miembros del equipo](#step-five-add-team-members).

## <a name="prerequisites"></a>Requisitos previos

### <a name="analyze-and-prepare-message-data"></a>Analizar y preparar datos de mensajes

* Revise los datos de terceros para decidir qué se migrará.  
* Extrae los datos seleccionados del sistema de chat de terceros.  
* Asigne la estructura de chat de terceros a la Teams de chat.  
* Convertir datos de importación en formato necesario para la migración.  

### <a name="set-up-your-office-365-tenant"></a>Configurar el espacio empresarial de Office 365

* Asegúrese de que existe Office 365 inquilino para los datos de importación. Para obtener más información sobre cómo configurar un arrendamiento Office 365 para Teams, vea [prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).
* Asegúrese de que los miembros del equipo están en Azure Active Directory. Para obtener más información, [vea Agregar un nuevo usuario a](/azure/active-directory/fundamentals/add-users-azure-active-directory) Azure AD.

## <a name="step-1-create-a-team"></a>Paso 1: Crear un equipo

Dado que está migrando datos existentes, el mantenimiento de las marcas de tiempo de mensajes originales y la prevención de la actividad de mensajería durante el proceso de migración son fundamentales para volver a crear el flujo de mensajes existente del usuario en Teams. Esto se consigue de la siguiente manera:

> [Cree un nuevo equipo con](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) una marca de tiempo back-in-time con la propiedad de recurso de `createdDateTime` grupo. Coloque el nuevo equipo en `migration mode`, un estado especial que restringe a los usuarios de la mayoría de las actividades dentro del equipo hasta que se complete el proceso de migración. Incluya el `teamCreationMode` atributo de instancia con el `migration` valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado para la migración.  

> [!NOTE]
> El `createdDateTime` campo solo se rellenará para las instancias de un equipo o canal que se hayan migrado.

<!-- markdownlint-disable MD001 -->

#### <a name="permission"></a>Permiso

|ScopeName|DisplayName|Descripción|Tipo|¿Consentimiento de administrador?|Entidades/API cubiertas|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Administrar la migración a Microsoft Teams|Crear y administrar recursos para la migración a Microsoft Teams.|**Solo aplicación**|**Sí**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Solicitud (crear un equipo en estado de migración)

```http
POST https://graph.microsoft.com/v1.0/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/v1.0/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-message"></a>Mensaje de error

```http
400 Bad Request
```

Puede recibir el mensaje de error en los siguientes escenarios:

* Si `createdDateTime` está establecido para el futuro.
* Si `createdDateTime` se especifica correctamente, pero falta `teamCreationMode` el atributo de instancia o se establece en valor no válido.

## <a name="step-2-create-a-channel"></a>Paso 2: Crear un canal

La creación de un canal para los mensajes importados es similar al escenario de creación de equipo:

> [Cree un nuevo canal con](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) una marca de tiempo back-in-time con la propiedad de recurso channel `createdDateTime` . Coloque el nuevo canal en `migration mode`, un estado especial que restringe a los usuarios de la mayoría de las actividades de chat dentro del canal hasta que se complete el proceso de migración. Incluya el `channelCreationMode` atributo de instancia con el `migration` valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado para la migración.  
<!-- markdownlint-disable MD024 -->
#### <a name="permission"></a>Permiso

|ScopeName|DisplayName|Descripción|Tipo|¿Consentimiento de administrador?|Entidades/API cubiertas|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Administrar la migración a Microsoft Teams|Crear y administrar recursos para la migración a Microsoft Teams.|**Solo aplicación**|**Sí**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>Solicitud (crear un canal en estado de migración)

```http
POST https://graph.microsoft.com/v1.0/teams/{team-id}/channels

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
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels/$entity",
   "id":"id-value",
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

Puede recibir el mensaje de error en los siguientes escenarios:

* Si `createdDateTime` está establecido para el futuro.
* Si `createdDateTime` se especifica correctamente, pero falta `channelCreationMode` el atributo de instancia o se establece en valor no válido.

## <a name="step-3-import-messages"></a>Paso 3: Importar mensajes

Después de crear el equipo y el canal, puede empezar a enviar mensajes back-in-time con `createdDateTime`  las claves y `from` del cuerpo de la solicitud.

> [!NOTE]
>
> * No se admiten los `createdDateTime` mensajes importados con versiones anteriores al `createdDateTime` subproceso de mensaje.
> * `createdDateTime` debe ser único entre los mensajes del mismo subproceso.
> * `createdDateTime` admite marcas de tiempo con precisión de milisegundos. Por ejemplo, `createdDateTime` si el mensaje de solicitud entrante tiene el valor de establecido como *2020-09-16T05:50:31.0025302Z*, se convertiría a *2020-09-16T05:50:31.002Z* cuando se ingiere el mensaje.

#### <a name="request-post-message-that-is-text-only"></a>Solicitud (mensaje POST que es de solo texto)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

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
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
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

#### <a name="error-message"></a>Mensaje de error

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>Solicitud (POST un mensaje con imagen en línea)

> [!NOTE]
>
> * No hay ámbitos de permisos especiales en este escenario, ya que la solicitud forma parte de `chatMessage`.
> * Los ámbitos para aplicar `chatMessage` aquí.

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

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
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
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

## <a name="step-4-complete-migration-mode"></a>Paso 4: Completar el modo de migración

Una vez completado el proceso de migración de mensajes, tanto el equipo como el canal se sacarán del modo de migración mediante el método  `completeMigration` . En este paso se abren los recursos de equipo y canal para su uso general por parte de los miembros del equipo. La acción está enlazada a la `team` instancia. Antes de que el equipo se complete, todos los canales deben completarse fuera del modo de migración.

#### <a name="request-end-channel-migration-mode"></a>Solicitud (modo de migración de canal final)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a>Solicitud (modo de migración de equipo final)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a>Respuesta

```http
HTTP/1.1 204 NoContent
```

Acción llamada en un `team` o `channel` que no está en `migrationMode`.

## <a name="step-five-add-team-members"></a>Paso cinco: Agregar miembros del equipo

Puedes agregar un miembro a un equipo mediante la interfaz de usuario Teams [o](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) la API Graph [miembro de](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) Microsoft:

#### <a name="request-add-member"></a>Solicitud (agregar miembro)

```http
POST https://graph.microsoft.com/beta/teams/{team-id}/members
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

## <a name="tips-and-additional-information"></a>Sugerencias información adicional

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* Después de `completeMigration` realizar la solicitud, no puede importar más mensajes en el equipo.

* Solo puede agregar miembros del equipo al nuevo equipo después de que `completeMigration` la solicitud haya devuelto una respuesta correcta.

* Limitación: los mensajes se importan a cinco RPS por canal.

* Si necesita realizar una corrección en los resultados de la migración, debe eliminar el equipo y repetir los pasos para crear el equipo y canalizar y volver a migrar los mensajes.

> [!NOTE]
> Actualmente, las imágenes en línea son el único tipo de medios admitidos por el esquema de api de mensajes de importación.

##### <a name="import-content-scope"></a>Importar ámbito de contenido

En la tabla siguiente se proporciona el ámbito de contenido:

|En el ámbito | Actualmente fuera del ámbito|
|----------|--------------------------|
|Mensajes de equipo y canal|1:1 y mensajes de chat en grupo|
|Hora de creación del mensaje original|Canales privados|
|Imágenes en línea como parte del mensaje|En menciones|
|Vínculos a archivos existentes en SPO o OneDrive|Reacciones|
|Mensajes con texto enriquecido|Vídeos|
|Cadena de respuesta de mensajes|Anuncios|
|Procesamiento de alto rendimiento|Fragmentos de código|
||Adhesivos|
||Emojis|
||Ofertas|
||Publicaciones cruzadas entre canales|

## <a name="see-also"></a>Vea también

[Integración Graph y Teams Microsoft](/graph/teams-concept-overview)
