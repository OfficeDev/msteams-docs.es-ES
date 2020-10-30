---
title: Usar Microsoft Graph para importar mensajes de la plataforma externa a teams
description: Describe cómo usar Microsoft Graph para importar mensajes de una plataforma externa a teams.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: mensajes de importación de Teams gráfico de API de Microsoft migrar publicación de migración
ms.openlocfilehash: 934e00541773140c90c270a616d6bc50aacac6e1
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796298"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="c90c1-104">Importar mensajes de plataformas de terceros a Teams con Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="c90c1-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="c90c1-105">Las vistas previas públicas de Microsoft Graph y Microsoft Teams están disponibles para el acceso anticipado y los comentarios.</span><span class="sxs-lookup"><span data-stu-id="c90c1-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="c90c1-106">Aunque esta versión se ha sometido a pruebas exhaustivas, no está pensada para su uso en producción.</span><span class="sxs-lookup"><span data-stu-id="c90c1-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="c90c1-107">Con Microsoft Graph, puede migrar los datos y el historial de mensajes existentes de los usuarios de un sistema externo a un canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="c90c1-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="c90c1-108">Al habilitar la recreación de una jerarquía de mensajería de una plataforma de terceros en Microsoft Teams, los usuarios pueden continuar sus comunicaciones de manera transparente y continuar sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="c90c1-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="c90c1-109">Información general sobre la importación</span><span class="sxs-lookup"><span data-stu-id="c90c1-109">Import overview</span></span>

<span data-ttu-id="c90c1-110">En un nivel alto, el proceso de importación consta de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c90c1-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="c90c1-111">Crear un equipo con una marca de tiempo de fondo</span><span class="sxs-lookup"><span data-stu-id="c90c1-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="c90c1-112">Crear un canal con una marca de tiempo de fondo</span><span class="sxs-lookup"><span data-stu-id="c90c1-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="c90c1-113">Importar mensajes externos de fecha y hora de atrás</span><span class="sxs-lookup"><span data-stu-id="c90c1-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="c90c1-114">Completar el proceso de migración de equipos y canales</span><span class="sxs-lookup"><span data-stu-id="c90c1-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="c90c1-115">Agregar miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="c90c1-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="c90c1-116">Requisitos necesarios</span><span class="sxs-lookup"><span data-stu-id="c90c1-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="c90c1-117">Analizar y preparar los datos de los mensajes</span><span class="sxs-lookup"><span data-stu-id="c90c1-117">Analyze and prepare message data</span></span>

<span data-ttu-id="c90c1-118">✔ Revise los datos de terceros para decidir qué se va a migrar.</span><span class="sxs-lookup"><span data-stu-id="c90c1-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="c90c1-119">✔ Extraer los datos seleccionados del sistema de chat de terceros.</span><span class="sxs-lookup"><span data-stu-id="c90c1-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="c90c1-120">✔ Asignar la estructura de charla de terceros a la estructura de Teams.</span><span class="sxs-lookup"><span data-stu-id="c90c1-120">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="c90c1-121">✔ Convertir los datos de importación en el formato necesario para la migración.</span><span class="sxs-lookup"><span data-stu-id="c90c1-121">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="c90c1-122">Configurar el espacio empresarial de Office 365</span><span class="sxs-lookup"><span data-stu-id="c90c1-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="c90c1-123">✔ Asegúrese de que existe un inquilino de Office 365 para los datos de importación.</span><span class="sxs-lookup"><span data-stu-id="c90c1-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="c90c1-124">Para obtener más información sobre cómo configurar un arrendamiento de Office 365 para Teams, *vea* [preparar el inquilino de Office 365](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="c90c1-124">For more information on setting up an Office 365 tenancy for Teams, *see* , [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="c90c1-125">✔ Asegúrese de que los integrantes del grupo estén en Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="c90c1-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="c90c1-126">Para obtener más información, *consulte* [Agregar un nuevo usuario](/azure/active-directory/fundamentals/add-users-azure-active-directory) a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c90c1-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="c90c1-127">Paso uno: crear un equipo</span><span class="sxs-lookup"><span data-stu-id="c90c1-127">Step One: Create a team</span></span>

<span data-ttu-id="c90c1-128">Como los datos existentes se migran, el mantenimiento de las marcas de tiempo del mensaje original y la prevención de la actividad de mensajería durante el proceso de migración son clave para volver a crear el flujo de mensajes existente del usuario en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c90c1-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="c90c1-129">Esto se logra de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c90c1-129">This is achieved as follows:</span></span>

> <span data-ttu-id="c90c1-130">[Cree un nuevo equipo](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) con una marca de tiempo de fondo con la propiedad de recurso de equipo  `createdDateTime`  .</span><span class="sxs-lookup"><span data-stu-id="c90c1-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="c90c1-131">Ponga el nuevo equipo en `migration mode` , un estado especial que reubique a los usuarios de la mayoría de las actividades del equipo hasta que se complete el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="c90c1-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="c90c1-132">Incluya el `teamCreationMode` atributo de instancia con el `migration` valor en la solicitud post para identificar explícitamente el nuevo equipo como creado para la migración.</span><span class="sxs-lookup"><span data-stu-id="c90c1-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="c90c1-133">**Nota** : el `createdDateTime` campo solo se rellenará para las instancias de un equipo o canal que se hayan migrado.</span><span class="sxs-lookup"><span data-stu-id="c90c1-133">**NOTE** :  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="c90c1-134">Permissions</span><span class="sxs-lookup"><span data-stu-id="c90c1-134">Permissions</span></span>

|<span data-ttu-id="c90c1-135">ScopeName</span><span class="sxs-lookup"><span data-stu-id="c90c1-135">ScopeName</span></span>|<span data-ttu-id="c90c1-136">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c90c1-136">DisplayName</span></span>|<span data-ttu-id="c90c1-137">Descripción</span><span class="sxs-lookup"><span data-stu-id="c90c1-137">Description</span></span>|<span data-ttu-id="c90c1-138">Tipo</span><span class="sxs-lookup"><span data-stu-id="c90c1-138">Type</span></span>|<span data-ttu-id="c90c1-139">¿El consentimiento del administrador?</span><span class="sxs-lookup"><span data-stu-id="c90c1-139">Admin Consent?</span></span>|<span data-ttu-id="c90c1-140">Entidades o API cubiertas</span><span class="sxs-lookup"><span data-stu-id="c90c1-140">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="c90c1-141">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c90c1-141">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="c90c1-142">Creación, administración de recursos para la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c90c1-142">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="c90c1-143">**Solo de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="c90c1-143">**Application-only**</span></span>|<span data-ttu-id="c90c1-144">**Sí**</span><span class="sxs-lookup"><span data-stu-id="c90c1-144">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="c90c1-145">Solicitud (crear un equipo en el estado de migración)</span><span class="sxs-lookup"><span data-stu-id="c90c1-145">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="c90c1-146">Respuesta</span><span class="sxs-lookup"><span data-stu-id="c90c1-146">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="c90c1-147">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="c90c1-147">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="c90c1-148">`createdDateTime`  establecer para el futuro.</span><span class="sxs-lookup"><span data-stu-id="c90c1-148">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="c90c1-149">`createdDateTime`  se especificó correctamente, pero `teamCreationMode`  falta el atributo de instancia o está establecido en un valor no válido.</span><span class="sxs-lookup"><span data-stu-id="c90c1-149">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="c90c1-150">Paso 2: crear un canal</span><span class="sxs-lookup"><span data-stu-id="c90c1-150">Step Two: Create a channel</span></span>

<span data-ttu-id="c90c1-151">La creación de un canal para los mensajes importados es similar al escenario crear equipo:</span><span class="sxs-lookup"><span data-stu-id="c90c1-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="c90c1-152">[Cree un canal nuevo](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) con una marca de tiempo de fondo con la propiedad de recurso Channel `createdDateTime` .</span><span class="sxs-lookup"><span data-stu-id="c90c1-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="c90c1-153">Inserte el nuevo canal en `migration mode` , un estado especial que reubique a los usuarios de la mayoría de las actividades de chat en el canal hasta que se complete el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="c90c1-153">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="c90c1-154">Incluya el `channelCreationMode` atributo de instancia con el `migration` valor en la solicitud post para identificar explícitamente el nuevo equipo como creado para la migración.</span><span class="sxs-lookup"><span data-stu-id="c90c1-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="c90c1-155">Permissions</span><span class="sxs-lookup"><span data-stu-id="c90c1-155">Permissions</span></span>

|<span data-ttu-id="c90c1-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="c90c1-156">ScopeName</span></span>|<span data-ttu-id="c90c1-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c90c1-157">DisplayName</span></span>|<span data-ttu-id="c90c1-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="c90c1-158">Description</span></span>|<span data-ttu-id="c90c1-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="c90c1-159">Type</span></span>|<span data-ttu-id="c90c1-160">¿El consentimiento del administrador?</span><span class="sxs-lookup"><span data-stu-id="c90c1-160">Admin Consent?</span></span>|<span data-ttu-id="c90c1-161">Entidades o API cubiertas</span><span class="sxs-lookup"><span data-stu-id="c90c1-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="c90c1-162">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c90c1-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="c90c1-163">Creación, administración de recursos para la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c90c1-163">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="c90c1-164">**Solo de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="c90c1-164">**Application-only**</span></span>|<span data-ttu-id="c90c1-165">**Sí**</span><span class="sxs-lookup"><span data-stu-id="c90c1-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="c90c1-166">Solicitud (crear un canal en el estado de migración)</span><span class="sxs-lookup"><span data-stu-id="c90c1-166">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="c90c1-167">Respuesta</span><span class="sxs-lookup"><span data-stu-id="c90c1-167">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="c90c1-168">Mensaje de error</span><span class="sxs-lookup"><span data-stu-id="c90c1-168">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="c90c1-169">`createdDateTime`  establecer para el futuro.</span><span class="sxs-lookup"><span data-stu-id="c90c1-169">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="c90c1-170">`createdDateTime`  especificado correctamente pero el `channelCreationMode`  atributo de instancia falta o está establecido en un valor no válido.</span><span class="sxs-lookup"><span data-stu-id="c90c1-170">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="c90c1-171">Paso tres: importar mensajes</span><span class="sxs-lookup"><span data-stu-id="c90c1-171">Step Three: Import messages</span></span>

<span data-ttu-id="c90c1-172">Una vez que se han creado el equipo y el canal, puede empezar a enviar mensajes en tiempo de inactividad con las `createdDateTime` `from`  claves y en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c90c1-172">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="c90c1-173">**Nota** : `createdDateTime` `createdDateTime` no se admiten los mensajes importados con anterioridad que el hilo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="c90c1-173">**NOTE** : messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> <span data-ttu-id="c90c1-174">createdDateTime debe ser único entre los mensajes del mismo subproceso.</span><span class="sxs-lookup"><span data-stu-id="c90c1-174">createdDateTime must be unique across messages in the same thread.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="c90c1-175">Request (mensaje POST que es de solo texto)</span><span class="sxs-lookup"><span data-stu-id="c90c1-175">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="c90c1-176">Respuesta</span><span class="sxs-lookup"><span data-stu-id="c90c1-176">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="c90c1-177">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="c90c1-177">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="c90c1-178">Solicitud (publicar un mensaje con una imagen en línea)</span><span class="sxs-lookup"><span data-stu-id="c90c1-178">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="c90c1-179">**Nota** : no hay ámbitos de permisos especiales en este escenario, ya que la solicitud es parte de chatMessage; los ámbitos para chatMessage también se aplican aquí.</span><span class="sxs-lookup"><span data-stu-id="c90c1-179">**Note** : There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="c90c1-180">Respuesta</span><span class="sxs-lookup"><span data-stu-id="c90c1-180">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="c90c1-181">Paso cuatro: completar el modo de migración</span><span class="sxs-lookup"><span data-stu-id="c90c1-181">Step Four: Complete migration mode</span></span>

<span data-ttu-id="c90c1-182">Una vez que se ha completado el proceso de migración de mensajes, el equipo y el canal se sacan del modo de migración mediante el  `completeMigration`  método.</span><span class="sxs-lookup"><span data-stu-id="c90c1-182">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="c90c1-183">Este paso abre los recursos de equipo y canal para uso general por parte de los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="c90c1-183">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="c90c1-184">La acción está enlazada a la `team` instancia.</span><span class="sxs-lookup"><span data-stu-id="c90c1-184">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="c90c1-185">Solicitud (finalizar modo de migración de equipo)</span><span class="sxs-lookup"><span data-stu-id="c90c1-185">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="c90c1-186">Respuesta</span><span class="sxs-lookup"><span data-stu-id="c90c1-186">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="c90c1-187">Solicitud (modo de migración de canal de fin)</span><span class="sxs-lookup"><span data-stu-id="c90c1-187">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="c90c1-188">Respuesta</span><span class="sxs-lookup"><span data-stu-id="c90c1-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="c90c1-189">Respuesta de error</span><span class="sxs-lookup"><span data-stu-id="c90c1-189">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="c90c1-190">Acción llamada en `team` o `channel` que no está en `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="c90c1-190">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="c90c1-191">Paso cinco: agregar miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="c90c1-191">Step Five: Add team members</span></span>

<span data-ttu-id="c90c1-192">Puede Agregar un miembro a un equipo [mediante la interfaz de usuario de Microsoft Teams o la](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) API de [miembro para agregar](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) de Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="c90c1-192">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="c90c1-193">Solicitud (agregar miembro)</span><span class="sxs-lookup"><span data-stu-id="c90c1-193">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="c90c1-194">Respuesta</span><span class="sxs-lookup"><span data-stu-id="c90c1-194">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="c90c1-195">Sugerencias e información adicional</span><span class="sxs-lookup"><span data-stu-id="c90c1-195">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="c90c1-196">Puede importar mensajes de usuarios que no están en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c90c1-196">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="c90c1-197">**Nota** : los mensajes importados para los usuarios que no están presentes en el inquilino no se podrán buscar en el cliente de Microsoft Teams ni en los portales de cumplimiento durante la versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="c90c1-197">**NOTE** : Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="c90c1-198">Una vez que `completeMigration` se haya realizado la solicitud, no podrá importar más mensajes al equipo.</span><span class="sxs-lookup"><span data-stu-id="c90c1-198">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="c90c1-199">Los integrantes del grupo solo se pueden agregar al nuevo equipo después de que la `completeMigration` solicitud haya devuelto una respuesta correcta.</span><span class="sxs-lookup"><span data-stu-id="c90c1-199">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="c90c1-200">Limitación de peticiones: mensajes que se importan a 5 RPS por canal.</span><span class="sxs-lookup"><span data-stu-id="c90c1-200">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="c90c1-201">Si necesita realizar una corrección de los resultados de la migración, debe eliminar el equipo y repetir los pasos para crear el equipo y el canal y volver a migrar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="c90c1-201">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="c90c1-202">Actualmente, las imágenes insertadas son el único tipo de medios admitidos por el esquema de la API de importación de mensajes.</span><span class="sxs-lookup"><span data-stu-id="c90c1-202">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="c90c1-203">Ámbito de importación de contenido</span><span class="sxs-lookup"><span data-stu-id="c90c1-203">Import content scope</span></span>

|<span data-ttu-id="c90c1-204">En el ámbito</span><span class="sxs-lookup"><span data-stu-id="c90c1-204">In-scope</span></span> | <span data-ttu-id="c90c1-205">Actualmente fuera de ámbito</span><span class="sxs-lookup"><span data-stu-id="c90c1-205">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="c90c1-206">Mensajes de equipo y de canal</span><span class="sxs-lookup"><span data-stu-id="c90c1-206">Team and channel messages</span></span>|<span data-ttu-id="c90c1-207">1:1 y mensajes de chat en grupo</span><span class="sxs-lookup"><span data-stu-id="c90c1-207">1:1 and group chat messages</span></span>|
|<span data-ttu-id="c90c1-208">Hora de creación del mensaje original</span><span class="sxs-lookup"><span data-stu-id="c90c1-208">Created time of the original message</span></span>|<span data-ttu-id="c90c1-209">Canales privados</span><span class="sxs-lookup"><span data-stu-id="c90c1-209">Private channels</span></span>|
|<span data-ttu-id="c90c1-210">Imágenes en línea como parte del mensaje</span><span class="sxs-lookup"><span data-stu-id="c90c1-210">Inline images as part of the message</span></span>|<span data-ttu-id="c90c1-211">A las menciones</span><span class="sxs-lookup"><span data-stu-id="c90c1-211">At mentions</span></span>|
|<span data-ttu-id="c90c1-212">Vínculos a archivos existentes en SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="c90c1-212">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="c90c1-213">Comunicar</span><span class="sxs-lookup"><span data-stu-id="c90c1-213">Reactions</span></span>|
|<span data-ttu-id="c90c1-214">Mensajes con texto enriquecido</span><span class="sxs-lookup"><span data-stu-id="c90c1-214">Messages with rich text</span></span>|<span data-ttu-id="c90c1-215">Vídeos</span><span class="sxs-lookup"><span data-stu-id="c90c1-215">Videos</span></span>|
|<span data-ttu-id="c90c1-216">Cadena de respuesta de mensaje</span><span class="sxs-lookup"><span data-stu-id="c90c1-216">Message reply chain</span></span>|<span data-ttu-id="c90c1-217">Anuncios</span><span class="sxs-lookup"><span data-stu-id="c90c1-217">Announcements</span></span>|
|<span data-ttu-id="c90c1-218">Procesamiento de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="c90c1-218">High throughput processing</span></span>|<span data-ttu-id="c90c1-219">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="c90c1-219">Code snippets</span></span>|
||<span data-ttu-id="c90c1-220">Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="c90c1-220">Adaptive cards</span></span>|
||<span data-ttu-id="c90c1-221">Adhesivos</span><span class="sxs-lookup"><span data-stu-id="c90c1-221">Stickers</span></span>|
||<span data-ttu-id="c90c1-222">Emojis</span><span class="sxs-lookup"><span data-stu-id="c90c1-222">Emojis</span></span>|
||<span data-ttu-id="c90c1-223">Las</span><span class="sxs-lookup"><span data-stu-id="c90c1-223">Quotes</span></span>|
||<span data-ttu-id="c90c1-224">Envíos cruzados entre canales</span><span class="sxs-lookup"><span data-stu-id="c90c1-224">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="c90c1-225">Más información sobre la integración de Microsoft Graph y Teams</span><span class="sxs-lookup"><span data-stu-id="c90c1-225">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
