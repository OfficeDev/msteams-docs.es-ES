---
title: Use Microsoft Graph para importar mensajes de plataforma externa a Teams
description: Describe cómo usar Microsoft Graph importar mensajes desde una plataforma externa a Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 5ea06e8b490bae0595abb31086848d0b050bded0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566162"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Importar mensajes de plataformas de terceros a Teams con Microsoft Graph

Con Microsoft Graph, puede migrar el historial de mensajes y los datos existentes de los usuarios desde un sistema externo a un canal Teams usuario. Al habilitar la recreación de una jerarquía de mensajería de plataforma de terceros dentro de Teams, los usuarios pueden continuar sus comunicaciones sin problemas y continuar sin interrupciones.

> [!NOTE] 
> En el futuro, Microsoft puede solicitarle a usted o a sus clientes que paguen tarifas adicionales en función de la cantidad de datos que se importen.

## <a name="import-overview"></a>Introducción a la importación

En un nivel alto, el proceso de importación consta de lo siguiente:

1. [Crear un equipo con una marca de tiempo back-in-time](#step-one-create-a-team)
1. [Crear un canal con una marca de tiempo back-in-time](#step-two-create-a-channel) 
1. [Importar mensajes con fecha de back-in-time externos](#step-three-import-messages)
1. [Completar el proceso de migración de equipos y canales](#step-four-complete-migration-mode)
1. [Agregar miembros del equipo](#step-five-add-team-members)

## <a name="necessary-requirements"></a>Requisitos necesarios

### <a name="analyze-and-prepare-message-data"></a>Analizar y preparar datos de mensajes

✔ revisar los datos de terceros para decidir qué se migrará.  
✔ extraer los datos seleccionados del sistema de chat de terceros.  
✔ asignar la estructura de chat de terceros a la Teams de chat.  
✔ Convertir datos de importación en formato necesario para la migración.  

### <a name="set-up-your-office-365-tenant"></a>Configurar el espacio empresarial de Office 365

✔ asegúrese de que existe Office 365 inquilino para los datos de importación. Para obtener más información sobre cómo configurar un arrendamiento Office 365 para Teams, vea [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).  
✔ Asegúrese de que los miembros del equipo están en Azure Active Directory (AAD).  Para obtener más información, [vea Agregar un nuevo usuario a](/azure/active-directory/fundamentals/add-users-azure-active-directory) Azure Active Directory.

## <a name="step-one-create-a-team"></a>Paso uno: Crear un equipo

Dado que los datos existentes se migran, el mantenimiento de las marcas de tiempo de mensajes originales y la prevención de la actividad de mensajería durante el proceso de migración son fundamentales para volver a crear el flujo de mensajes existente del usuario en Teams. Esto se consigue de la siguiente manera:

> [Cree un nuevo equipo con](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) una marca de tiempo back-in-time con la propiedad de recurso de  `createdDateTime`  grupo. Coloque el nuevo equipo en , un estado especial que reja a los usuarios de la mayoría de las actividades dentro del equipo hasta que se complete `migration mode` el proceso de migración. Incluya el atributo de instancia con el valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado `teamCreationMode` `migration` para la migración.  

> [!Note]
> El `createdDateTime` campo solo se rellenará para las instancias de un equipo o canal que se hayan migrado.

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>Permisos

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

#### <a name="error-messages"></a>Mensajes de error

```http
400 Bad Request
```

* `createdDateTime`  para el futuro.
* `createdDateTime`  especificado correctamente, pero falta `teamCreationMode`  el atributo de instancia o se establece en valor no válido.

## <a name="step-two-create-a-channel"></a>Paso dos: Crear un canal

La creación de un canal para los mensajes importados es similar al escenario de creación de equipo:

> [Cree un nuevo canal con](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) una marca de tiempo back-in-time con la propiedad de recurso `createdDateTime` channel. Coloque el nuevo canal en , un estado especial que reja a los usuarios de la mayoría de las actividades de chat dentro del canal hasta que se complete `migration mode` el proceso de migración.  Incluya el atributo de instancia con el valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado `channelCreationMode` `migration` para la migración.  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>Permisos

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

* `createdDateTime`  para el futuro.
* `createdDateTime`  especificado correctamente, pero `channelCreationMode`  falta el atributo de instancia o se establece en valor no válido.

## <a name="step-three-import-messages"></a>Paso tres: Importar mensajes

Después de crear el equipo y el canal, puede empezar a enviar mensajes back-in-time con las claves `createdDateTime`  y del cuerpo de la `from`  solicitud. **NOTA:** no se admiten los mensajes importados con versiones anteriores al `createdDateTime` `createdDateTime` subproceso de mensaje.

> [!NOTE]
> * `createdDateTime` debe ser único entre los mensajes del mismo subproceso.
> * `createdDateTime` admite marcas de tiempo con precisión de milisegundos. Por ejemplo, si el mensaje de solicitud entrante tiene el valor de establecido como `createdDateTime` *2020-09-16T05:50:31.0025302Z*, se convertiría a *2020-09-16T05:50:31.002Z* cuando se ingiere el mensaje.

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

#### <a name="error-messages"></a>Mensajes de error

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>Solicitud (POST un mensaje con imagen en línea)

> [!Note]
> No hay ámbitos de permisos especiales en este escenario, ya que la solicitud forma parte de chatMessage; los ámbitos de chatMessage también se aplican aquí.

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

## <a name="step-four-complete-migration-mode"></a>Paso cuatro: Completar el modo de migración

Una vez completado el proceso de migración de mensajes, tanto el equipo como el canal se sacarán del modo de migración mediante el  `completeMigration`  método. En este paso se abren los recursos de equipo y canal para su uso general por parte de los miembros del equipo. La acción está enlazada a la `team` instancia. Todos los canales deben completarse fuera del modo de migración para poder completar el equipo.

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

* Acción llamada en un `team` o que no está en `channel` `migrationMode` .

## <a name="step-five-add-team-members"></a>Paso cinco: Agregar miembros del equipo

Puedes agregar un miembro a un equipo mediante la interfaz de usuario Teams [o](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) la API Graph [agregar miembro](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) de Microsoft:

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

* Una vez `completeMigration` realizada la solicitud, no puede importar más mensajes en el equipo.

* Los miembros del equipo solo se pueden agregar al nuevo equipo después de `completeMigration` que la solicitud haya devuelto una respuesta correcta.

* Limitación: los mensajes se importan a 5 RPS por canal.

* Si necesita realizar una corrección en los resultados de la migración, debe eliminar el equipo y repetir los pasos para crear el equipo y canalizar y volver a migrar los mensajes.

> [!NOTE]
> Actualmente, las imágenes en línea son el único tipo de medios admitidos por el esquema de api de mensajes de importación.

##### <a name="import-content-scope"></a>Importar ámbito de contenido

|En el ámbito | Actualmente fuera del ámbito|
|----------|--------------------------|
|Mensajes de equipo y canal|1:1 y mensajes de chat en grupo|
|Hora de creación del mensaje original|Canales privados|
|Imágenes en línea como parte del mensaje|En menciones|
|Vínculos a archivos existentes en SPO/OneDrive|Reacciones|
|Mensajes con texto enriquecido|Vídeos|
|Cadena de respuesta de mensajes|Anuncios|
|Procesamiento de alto rendimiento|Fragmentos de código|
||Adhesivos|
||Emojis|
||Ofertas|
||Publicaciones cruzadas entre canales|


## <a name="see-also"></a>Consulte también

[Obtenga más información sobre microsoft Graph y Teams integración](/graph/teams-concept-overview)
