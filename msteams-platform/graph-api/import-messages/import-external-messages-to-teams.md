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
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="a2788-104">Importar mensajes de una plataforma de terceros a Microsoft Teams con Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="a2788-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="a2788-105">Las vistas previas públicas de Microsoft Graph y Microsoft Teams están disponibles para el acceso anticipado y los comentarios.</span><span class="sxs-lookup"><span data-stu-id="a2788-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="a2788-106">Aunque esta versión se ha sometido a pruebas exhaustivas, no está pensada para su uso en producción.</span><span class="sxs-lookup"><span data-stu-id="a2788-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="a2788-107">Con Microsoft Graph, puede migrar los datos y el historial de mensajes existentes de los usuarios de un sistema externo a un canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="a2788-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="a2788-108">Al habilitar la recreación de una jerarquía de mensajería de una plataforma de terceros en Microsoft Teams, los usuarios pueden continuar sus comunicaciones de manera transparente y continuar sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="a2788-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="a2788-109">Información general sobre la importación</span><span class="sxs-lookup"><span data-stu-id="a2788-109">Import overview</span></span>

<span data-ttu-id="a2788-110">En un nivel alto, el proceso de importación consta de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a2788-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="a2788-111">Crear un equipo con una marca de tiempo de fondo</span><span class="sxs-lookup"><span data-stu-id="a2788-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="a2788-112">Crear un canal con una marca de tiempo de fondo</span><span class="sxs-lookup"><span data-stu-id="a2788-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="a2788-113">Importar mensajes externos de fecha y hora de atrás</span><span class="sxs-lookup"><span data-stu-id="a2788-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="a2788-114">Completar el proceso de migración de equipos y canales</span><span class="sxs-lookup"><span data-stu-id="a2788-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="a2788-115">Agregar miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="a2788-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="a2788-116">Requisitos necesarios</span><span class="sxs-lookup"><span data-stu-id="a2788-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="a2788-117">Analizar y preparar los datos de los mensajes</span><span class="sxs-lookup"><span data-stu-id="a2788-117">Analyze and prepare message data</span></span>

<span data-ttu-id="a2788-118">✔ Revise los datos de terceros para decidir qué se va a migrar.</span><span class="sxs-lookup"><span data-stu-id="a2788-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="a2788-119">✔ Extraer los datos seleccionados del sistema de chat de terceros.</span><span class="sxs-lookup"><span data-stu-id="a2788-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="a2788-120">✔ Convertir los datos de importación en el formato necesario para la migración.</span><span class="sxs-lookup"><span data-stu-id="a2788-120">✔ Convert import data into format needed for migration.</span></span>  
<span data-ttu-id="a2788-121">✔ Asignar la estructura de charla de terceros a la estructura de Teams.</span><span class="sxs-lookup"><span data-stu-id="a2788-121">✔ Map the third-party chat structure to the Teams structure.</span></span>

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="a2788-122">Configurar el espacio empresarial de Office 365</span><span class="sxs-lookup"><span data-stu-id="a2788-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="a2788-123">✔ Asegúrese de que existe un inquilino de Office 365 para los datos de importación.</span><span class="sxs-lookup"><span data-stu-id="a2788-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="a2788-124">Para obtener más información sobre cómo configurar un arrendamiento de Office 365 para Teams, *vea* [preparar el inquilino de Office 365](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="a2788-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="a2788-125">✔ Asegúrese de que los integrantes del grupo estén en Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="a2788-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="a2788-126">Para obtener más información, *consulte* [Agregar un nuevo usuario](/azure/active-directory/fundamentals/add-users-azure-active-directory) a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a2788-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="a2788-127">Paso uno: crear un equipo</span><span class="sxs-lookup"><span data-stu-id="a2788-127">Step One: Create a team</span></span>

<span data-ttu-id="a2788-128">Como los datos existentes se migran, el mantenimiento de las marcas de tiempo del mensaje original y la prevención de la actividad de mensajería durante el proceso de migración son clave para volver a crear el flujo de mensajes existente del usuario en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a2788-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="a2788-129">Esto se logra de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="a2788-129">This is achieved as follows:</span></span>

1. <span data-ttu-id="a2788-130">[Cree un nuevo equipo](/graph/api/team-post?view=graph-rest-beta&tabs=http) con una marca de tiempo de fondo con la propiedad de recurso de equipo  `createdDateTime`  .</span><span class="sxs-lookup"><span data-stu-id="a2788-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span>  

1. <span data-ttu-id="a2788-131">Ponga el nuevo equipo en `migration mode` , un estado especial que reubique a los usuarios de la mayoría de las actividades del equipo hasta que se complete el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="a2788-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="a2788-132">Incluya el `teamCreationMode` atributo de instancia con el `migration` valor en la solicitud post para identificar explícitamente el nuevo equipo como creado para la migración.</span><span class="sxs-lookup"><span data-stu-id="a2788-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="a2788-133">Permisos</span><span class="sxs-lookup"><span data-stu-id="a2788-133">Permissions</span></span>

|<span data-ttu-id="a2788-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="a2788-134">ScopeName</span></span>|<span data-ttu-id="a2788-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="a2788-135">DisplayName</span></span>|<span data-ttu-id="a2788-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="a2788-136">Description</span></span>|<span data-ttu-id="a2788-137">Tipo</span><span class="sxs-lookup"><span data-stu-id="a2788-137">Type</span></span>|<span data-ttu-id="a2788-138">¿El consentimiento del administrador?</span><span class="sxs-lookup"><span data-stu-id="a2788-138">Admin Consent?</span></span>|<span data-ttu-id="a2788-139">Entidades o API cubiertas</span><span class="sxs-lookup"><span data-stu-id="a2788-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="a2788-140">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a2788-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="a2788-141">Creación, administración de recursos para la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a2788-141">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="a2788-142">**Solo de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="a2788-142">**Application-only**</span></span>|<span data-ttu-id="a2788-143">**Sí**</span><span class="sxs-lookup"><span data-stu-id="a2788-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="a2788-144">Solicitud (crear un equipo en el estado de migración)</span><span class="sxs-lookup"><span data-stu-id="a2788-144">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="a2788-145">Respuesta</span><span class="sxs-lookup"><span data-stu-id="a2788-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="a2788-146">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="a2788-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="a2788-147">`createdDateTime`  establecer para el futuro.</span><span class="sxs-lookup"><span data-stu-id="a2788-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="a2788-148">`createdDateTime`  se especificó correctamente, pero `teamCreationMode`  falta el atributo de instancia o está establecido en un valor no válido.</span><span class="sxs-lookup"><span data-stu-id="a2788-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="a2788-149">Paso 2: crear un canal</span><span class="sxs-lookup"><span data-stu-id="a2788-149">Step Two: Create a channel</span></span>

<span data-ttu-id="a2788-150">La creación de un canal para los mensajes importados es similar al escenario crear equipo:</span><span class="sxs-lookup"><span data-stu-id="a2788-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span> 

1. <span data-ttu-id="a2788-151">[Cree un canal nuevo](/graph/api/channel-post?view=graph-rest-beta&tabs=http) con una marca de tiempo de fondo con la propiedad de recurso Channel `createdDateTime` .</span><span class="sxs-lookup"><span data-stu-id="a2788-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span>

1. <span data-ttu-id="a2788-152">Inserte el nuevo canal en `migration mode` , un estado especial que reubique a los usuarios de la mayoría de las actividades de chat en el canal hasta que se complete el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="a2788-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="a2788-153">Incluya el `channelCreationMode` atributo de instancia con el `migration` valor en la solicitud post para identificar explícitamente el nuevo equipo como creado para la migración.</span><span class="sxs-lookup"><span data-stu-id="a2788-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="a2788-154">Permisos</span><span class="sxs-lookup"><span data-stu-id="a2788-154">Permissions</span></span>

|<span data-ttu-id="a2788-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="a2788-155">ScopeName</span></span>|<span data-ttu-id="a2788-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="a2788-156">DisplayName</span></span>|<span data-ttu-id="a2788-157">Descripción</span><span class="sxs-lookup"><span data-stu-id="a2788-157">Description</span></span>|<span data-ttu-id="a2788-158">Tipo</span><span class="sxs-lookup"><span data-stu-id="a2788-158">Type</span></span>|<span data-ttu-id="a2788-159">¿El consentimiento del administrador?</span><span class="sxs-lookup"><span data-stu-id="a2788-159">Admin Consent?</span></span>|<span data-ttu-id="a2788-160">Entidades o API cubiertas</span><span class="sxs-lookup"><span data-stu-id="a2788-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="a2788-161">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a2788-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="a2788-162">Creación, administración de recursos para la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a2788-162">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="a2788-163">**Solo de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="a2788-163">**Application-only**</span></span>|<span data-ttu-id="a2788-164">**Sí**</span><span class="sxs-lookup"><span data-stu-id="a2788-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="a2788-165">Solicitud (crear un canal en el estado de migración)</span><span class="sxs-lookup"><span data-stu-id="a2788-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="a2788-166">Respuesta</span><span class="sxs-lookup"><span data-stu-id="a2788-166">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a><span data-ttu-id="a2788-167">Mensaje de error</span><span class="sxs-lookup"><span data-stu-id="a2788-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="a2788-168">`createdDateTime`  establecer para el futuro.</span><span class="sxs-lookup"><span data-stu-id="a2788-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="a2788-169">`createdDateTime`  especificado correctamente pero el `channelCreationMode`  atributo de instancia falta o está establecido en un valor no válido.</span><span class="sxs-lookup"><span data-stu-id="a2788-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="a2788-170">Paso tres: importar mensajes</span><span class="sxs-lookup"><span data-stu-id="a2788-170">Step Three: Import messages</span></span>

<span data-ttu-id="a2788-171">Una vez que se han creado el equipo y el canal, puede empezar a enviar mensajes en tiempo de inactividad con las `createdDateTime` `from`  claves y en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="a2788-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="a2788-172">Request (mensaje POST que es de solo texto)</span><span class="sxs-lookup"><span data-stu-id="a2788-172">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="a2788-173">Respuesta</span><span class="sxs-lookup"><span data-stu-id="a2788-173">Response</span></span>

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

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="a2788-174">Solicitud (publicar un mensaje con una imagen en línea)</span><span class="sxs-lookup"><span data-stu-id="a2788-174">Request (POST a message with inline \`image)</span></span>

> <span data-ttu-id="a2788-175">**Nota**: no hay ámbitos de permisos especiales en este escenario, ya que la solicitud es parte de chatMessage; los ámbitos para chatMessage también se aplican aquí.</span><span class="sxs-lookup"><span data-stu-id="a2788-175">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="a2788-176">Respuesta</span><span class="sxs-lookup"><span data-stu-id="a2788-176">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="a2788-177">Paso cuatro: completar el modo de migración</span><span class="sxs-lookup"><span data-stu-id="a2788-177">Step Four: Complete migration mode</span></span>

<span data-ttu-id="a2788-178">Una vez que se ha completado el proceso de migración de mensajes, el equipo y el canal se sacan del modo de migración mediante el  `completeMigration`  método.</span><span class="sxs-lookup"><span data-stu-id="a2788-178">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="a2788-179">Este paso abre los recursos de equipo y canal para uso general por parte de los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="a2788-179">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="a2788-180">La acción está enlazada a la `team` instancia.</span><span class="sxs-lookup"><span data-stu-id="a2788-180">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="a2788-181">Solicitud (finalizar modo de migración de equipo)</span><span class="sxs-lookup"><span data-stu-id="a2788-181">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="a2788-182">Respuesta</span><span class="sxs-lookup"><span data-stu-id="a2788-182">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="a2788-183">Solicitud (modo de migración de canal de fin)</span><span class="sxs-lookup"><span data-stu-id="a2788-183">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="a2788-184">Respuesta</span><span class="sxs-lookup"><span data-stu-id="a2788-184">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="a2788-185">Respuesta de error</span><span class="sxs-lookup"><span data-stu-id="a2788-185">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="a2788-186">Acción llamada en `team` o `channel` que no está en `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="a2788-186">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="a2788-187">Paso cinco: agregar miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="a2788-187">Step Five: Add team members</span></span>

<span data-ttu-id="a2788-188">Puede Agregar un miembro a un equipo [mediante la interfaz de usuario de Microsoft Teams o la](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) API de [miembro para agregar](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) de Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="a2788-188">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="a2788-189">Solicitud (agregar miembro)</span><span class="sxs-lookup"><span data-stu-id="a2788-189">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a><span data-ttu-id="a2788-190">Respuesta</span><span class="sxs-lookup"><span data-stu-id="a2788-190">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="a2788-191">Sugerencias e información adicional</span><span class="sxs-lookup"><span data-stu-id="a2788-191">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="a2788-192">Puede importar mensajes de usuarios que no están en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a2788-192">You can import messages from users who are not in Teams.</span></span>

* <span data-ttu-id="a2788-193">Una vez que `completeMigration` se haya realizado la solicitud, no podrá importar más mensajes al equipo.</span><span class="sxs-lookup"><span data-stu-id="a2788-193">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="a2788-194">Los integrantes del grupo solo se pueden agregar al nuevo equipo después de que la `completeMigration` solicitud haya devuelto una respuesta correcta.</span><span class="sxs-lookup"><span data-stu-id="a2788-194">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="a2788-195">Limitación de peticiones: mensajes que se importan a 5 RPS por canal.</span><span class="sxs-lookup"><span data-stu-id="a2788-195">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="a2788-196">Si necesita realizar una corrección de los resultados de la migración, debe eliminar el equipo y repetir los pasos para crear el equipo y el canal y volver a migrar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="a2788-196">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="a2788-197">Actualmente, las imágenes insertadas son el único tipo de medios admitidos por el esquema de la API de importación de mensajes.</span><span class="sxs-lookup"><span data-stu-id="a2788-197">Currently, Inline images is the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="a2788-198">Ámbito de importación de contenido</span><span class="sxs-lookup"><span data-stu-id="a2788-198">Import content scope</span></span>

|<span data-ttu-id="a2788-199">En el ámbito</span><span class="sxs-lookup"><span data-stu-id="a2788-199">In-scope</span></span> | <span data-ttu-id="a2788-200">Actualmente fuera de ámbito</span><span class="sxs-lookup"><span data-stu-id="a2788-200">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="a2788-201">Mensajes de equipo y de canal</span><span class="sxs-lookup"><span data-stu-id="a2788-201">Team and channel messages</span></span>|<span data-ttu-id="a2788-202">1:1 y mensajes de chat en grupo</span><span class="sxs-lookup"><span data-stu-id="a2788-202">1:1 and group chat messages</span></span>|
|<span data-ttu-id="a2788-203">Hora de creación del mensaje original</span><span class="sxs-lookup"><span data-stu-id="a2788-203">Created time of the original message</span></span>|<span data-ttu-id="a2788-204">Canales privados</span><span class="sxs-lookup"><span data-stu-id="a2788-204">Private channels</span></span>|
|<span data-ttu-id="a2788-205">Imágenes en línea como parte del mensaje</span><span class="sxs-lookup"><span data-stu-id="a2788-205">Inline images as part of the message</span></span>|<span data-ttu-id="a2788-206">A las menciones</span><span class="sxs-lookup"><span data-stu-id="a2788-206">At mentions</span></span>|
|<span data-ttu-id="a2788-207">Vínculos a archivos existentes en SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="a2788-207">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="a2788-208">Comunicar</span><span class="sxs-lookup"><span data-stu-id="a2788-208">Reactions</span></span>|
|<span data-ttu-id="a2788-209">Mensajes con texto enriquecido</span><span class="sxs-lookup"><span data-stu-id="a2788-209">Messages with rich text</span></span>|<span data-ttu-id="a2788-210">Vídeos</span><span class="sxs-lookup"><span data-stu-id="a2788-210">Videos</span></span>|
|<span data-ttu-id="a2788-211">Cadena de respuesta de mensaje</span><span class="sxs-lookup"><span data-stu-id="a2788-211">Message reply chain</span></span>|<span data-ttu-id="a2788-212">Anuncios</span><span class="sxs-lookup"><span data-stu-id="a2788-212">Announcements</span></span>|
|<span data-ttu-id="a2788-213">Procesamiento de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="a2788-213">High throughput processing</span></span>|<span data-ttu-id="a2788-214">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="a2788-214">Code snippets</span></span>|
||<span data-ttu-id="a2788-215">Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a2788-215">Adaptive cards</span></span>|
||<span data-ttu-id="a2788-216">Adhesivos</span><span class="sxs-lookup"><span data-stu-id="a2788-216">Stickers</span></span>|
||<span data-ttu-id="a2788-217">Emojis</span><span class="sxs-lookup"><span data-stu-id="a2788-217">Emojis</span></span>|
||<span data-ttu-id="a2788-218">Las</span><span class="sxs-lookup"><span data-stu-id="a2788-218">Quotes</span></span>|
||<span data-ttu-id="a2788-219">Envíos cruzados entre canales</span><span class="sxs-lookup"><span data-stu-id="a2788-219">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="a2788-220">Más información sobre la integración de Microsoft Graph y Teams</span><span class="sxs-lookup"><span data-stu-id="a2788-220">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
