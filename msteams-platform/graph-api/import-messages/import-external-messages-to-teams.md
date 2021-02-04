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
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="887e6-104">Importar mensajes de plataformas de terceros a Teams con Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="887e6-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="887e6-105">Las vistas previas públicas de Microsoft Graph y Microsoft Teams están disponibles para el acceso anticipado y los comentarios.</span><span class="sxs-lookup"><span data-stu-id="887e6-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="887e6-106">Aunque esta versión se ha sometido a pruebas exhaustivas, no está pensada para su uso en producción.</span><span class="sxs-lookup"><span data-stu-id="887e6-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="887e6-107">Con Microsoft Graph, puede migrar el historial de mensajes y los datos existentes de los usuarios desde un sistema externo a un canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="887e6-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="887e6-108">Al habilitar la recreación de una jerarquía de mensajería de plataforma de terceros dentro de Teams, los usuarios pueden continuar sus comunicaciones sin problemas y continuar sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="887e6-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="887e6-109">Introducción a la importación</span><span class="sxs-lookup"><span data-stu-id="887e6-109">Import overview</span></span>

<span data-ttu-id="887e6-110">En un nivel alto, el proceso de importación consta de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="887e6-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="887e6-111">Crear un equipo con una marca de tiempo back-in-time</span><span class="sxs-lookup"><span data-stu-id="887e6-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="887e6-112">Crear un canal con una marca de tiempo back-in-time</span><span class="sxs-lookup"><span data-stu-id="887e6-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="887e6-113">Importar mensajes externos con fecha de espera</span><span class="sxs-lookup"><span data-stu-id="887e6-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="887e6-114">Completar el proceso de migración de equipos y canales</span><span class="sxs-lookup"><span data-stu-id="887e6-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="887e6-115">Agregar miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="887e6-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="887e6-116">Requisitos necesarios</span><span class="sxs-lookup"><span data-stu-id="887e6-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="887e6-117">Analizar y preparar los datos del mensaje</span><span class="sxs-lookup"><span data-stu-id="887e6-117">Analyze and prepare message data</span></span>

<span data-ttu-id="887e6-118">✔ revisar los datos de terceros para decidir qué se migrará.</span><span class="sxs-lookup"><span data-stu-id="887e6-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="887e6-119">✔ extraer los datos seleccionados del sistema de chat de terceros.</span><span class="sxs-lookup"><span data-stu-id="887e6-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="887e6-120">✔ asignar la estructura de chat de terceros a la estructura de Teams.</span><span class="sxs-lookup"><span data-stu-id="887e6-120">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="887e6-121">✔ convertir los datos de importación en el formato necesario para la migración.</span><span class="sxs-lookup"><span data-stu-id="887e6-121">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="887e6-122">Configurar el espacio empresarial de Office 365</span><span class="sxs-lookup"><span data-stu-id="887e6-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="887e6-123">✔ asegúrese de que existe un inquilino de Office 365 para los datos de importación.</span><span class="sxs-lookup"><span data-stu-id="887e6-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="887e6-124">Para obtener más información sobre cómo configurar un inquilino de Office 365 para *Teams,* vea , Preparar el espacio empresarial [de Office 365.](../../concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="887e6-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="887e6-125">✔ asegúrese de que los miembros del equipo están en Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="887e6-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="887e6-126">Para obtener más *información, vea* [Agregar un nuevo usuario a](/azure/active-directory/fundamentals/add-users-azure-active-directory) Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="887e6-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="887e6-127">Paso uno: Crear un equipo</span><span class="sxs-lookup"><span data-stu-id="887e6-127">Step One: Create a team</span></span>

<span data-ttu-id="887e6-128">Dado que los datos existentes se migran, el mantenimiento de las marcas de tiempo del mensaje original y la prevención de la actividad de mensajería durante el proceso de migración son clave para volver a crear el flujo de mensajes existente del usuario en Teams.</span><span class="sxs-lookup"><span data-stu-id="887e6-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="887e6-129">Esto se logra de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="887e6-129">This is achieved as follows:</span></span>

> <span data-ttu-id="887e6-130">[Cree un nuevo equipo con](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) una marca de tiempo back-in-time con la propiedad de recurso de  `createdDateTime`  equipo.</span><span class="sxs-lookup"><span data-stu-id="887e6-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="887e6-131">Coloque el nuevo equipo en un estado especial que resalte a los usuarios de la mayoría de las actividades dentro del equipo hasta que se `migration mode` complete el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="887e6-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="887e6-132">Incluya el atributo de instancia con el valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado `teamCreationMode` `migration` para la migración.</span><span class="sxs-lookup"><span data-stu-id="887e6-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="887e6-133">**NOTA:** El campo solo se rellenará para las instancias de un equipo o canal que `createdDateTime` se hayan migrado.</span><span class="sxs-lookup"><span data-stu-id="887e6-133">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="887e6-134">Permisos</span><span class="sxs-lookup"><span data-stu-id="887e6-134">Permissions</span></span>

|<span data-ttu-id="887e6-135">ScopeName</span><span class="sxs-lookup"><span data-stu-id="887e6-135">ScopeName</span></span>|<span data-ttu-id="887e6-136">DisplayName</span><span class="sxs-lookup"><span data-stu-id="887e6-136">DisplayName</span></span>|<span data-ttu-id="887e6-137">Descripción</span><span class="sxs-lookup"><span data-stu-id="887e6-137">Description</span></span>|<span data-ttu-id="887e6-138">Tipo</span><span class="sxs-lookup"><span data-stu-id="887e6-138">Type</span></span>|<span data-ttu-id="887e6-139">¿Consentimiento del administrador?</span><span class="sxs-lookup"><span data-stu-id="887e6-139">Admin Consent?</span></span>|<span data-ttu-id="887e6-140">Entidades/API cubiertas</span><span class="sxs-lookup"><span data-stu-id="887e6-140">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="887e6-141">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="887e6-141">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="887e6-142">Creación y administración de recursos para la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="887e6-142">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="887e6-143">**Solo aplicación**</span><span class="sxs-lookup"><span data-stu-id="887e6-143">**Application-only**</span></span>|<span data-ttu-id="887e6-144">**Sí**</span><span class="sxs-lookup"><span data-stu-id="887e6-144">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="887e6-145">Solicitud (crear un equipo en estado de migración)</span><span class="sxs-lookup"><span data-stu-id="887e6-145">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="887e6-146">Respuesta</span><span class="sxs-lookup"><span data-stu-id="887e6-146">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="887e6-147">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="887e6-147">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="887e6-148">`createdDateTime`  se establece para el futuro.</span><span class="sxs-lookup"><span data-stu-id="887e6-148">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="887e6-149">`createdDateTime`  especificado correctamente, pero falta `teamCreationMode`  el atributo de instancia o se establece en un valor no válido.</span><span class="sxs-lookup"><span data-stu-id="887e6-149">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="887e6-150">Paso dos: Crear un canal</span><span class="sxs-lookup"><span data-stu-id="887e6-150">Step Two: Create a channel</span></span>

<span data-ttu-id="887e6-151">Crear un canal para los mensajes importados es similar al escenario de creación de equipo:</span><span class="sxs-lookup"><span data-stu-id="887e6-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="887e6-152">[Crea un nuevo canal con](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) una marca de tiempo back-in-time mediante la propiedad de recurso de `createdDateTime` canal.</span><span class="sxs-lookup"><span data-stu-id="887e6-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="887e6-153">Coloque el nuevo canal en un estado especial que resalte a los usuarios de la mayoría de las actividades de chat dentro del canal hasta que se complete `migration mode` el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="887e6-153">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="887e6-154">Incluya el atributo de instancia con el valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado `channelCreationMode` `migration` para la migración.</span><span class="sxs-lookup"><span data-stu-id="887e6-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="887e6-155">Permisos</span><span class="sxs-lookup"><span data-stu-id="887e6-155">Permissions</span></span>

|<span data-ttu-id="887e6-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="887e6-156">ScopeName</span></span>|<span data-ttu-id="887e6-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="887e6-157">DisplayName</span></span>|<span data-ttu-id="887e6-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="887e6-158">Description</span></span>|<span data-ttu-id="887e6-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="887e6-159">Type</span></span>|<span data-ttu-id="887e6-160">¿Consentimiento del administrador?</span><span class="sxs-lookup"><span data-stu-id="887e6-160">Admin Consent?</span></span>|<span data-ttu-id="887e6-161">Entidades/API cubiertas</span><span class="sxs-lookup"><span data-stu-id="887e6-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="887e6-162">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="887e6-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="887e6-163">Creación y administración de recursos para la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="887e6-163">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="887e6-164">**Solo aplicación**</span><span class="sxs-lookup"><span data-stu-id="887e6-164">**Application-only**</span></span>|<span data-ttu-id="887e6-165">**Sí**</span><span class="sxs-lookup"><span data-stu-id="887e6-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="887e6-166">Solicitud (crear un canal en estado de migración)</span><span class="sxs-lookup"><span data-stu-id="887e6-166">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="887e6-167">Respuesta</span><span class="sxs-lookup"><span data-stu-id="887e6-167">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="887e6-168">Mensaje de error</span><span class="sxs-lookup"><span data-stu-id="887e6-168">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="887e6-169">`createdDateTime`  se establece para el futuro.</span><span class="sxs-lookup"><span data-stu-id="887e6-169">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="887e6-170">`createdDateTime`  especificado correctamente, pero `channelCreationMode`  falta el atributo de instancia o se establece en un valor no válido.</span><span class="sxs-lookup"><span data-stu-id="887e6-170">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="887e6-171">Paso tres: Importar mensajes</span><span class="sxs-lookup"><span data-stu-id="887e6-171">Step Three: Import messages</span></span>

<span data-ttu-id="887e6-172">Una vez creados el equipo y el canal, puede empezar a enviar mensajes back-in-time con las claves y el cuerpo `createdDateTime` `from`  de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="887e6-172">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="887e6-173">**NOTA:** no se admiten los mensajes importados con versiones anteriores al `createdDateTime` hilo de `createdDateTime` mensaje.</span><span class="sxs-lookup"><span data-stu-id="887e6-173">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="887e6-174">`createdDateTime` debe ser único en todos los mensajes del mismo subproceso.</span><span class="sxs-lookup"><span data-stu-id="887e6-174">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="887e6-175">`createdDateTime` admite marcas de tiempo con precisión de milisegundos.</span><span class="sxs-lookup"><span data-stu-id="887e6-175">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="887e6-176">Por ejemplo, si el mensaje de solicitud entrante tiene el valor establecido como `createdDateTime` *2020-09-16T05:50:31.0025302Z*, se convertiría a *2020-09-16T05:50:31.002Z* cuando se ingera el mensaje.</span><span class="sxs-lookup"><span data-stu-id="887e6-176">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="887e6-177">Solicitud (mensaje POST que es de solo texto)</span><span class="sxs-lookup"><span data-stu-id="887e6-177">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="887e6-178">Respuesta</span><span class="sxs-lookup"><span data-stu-id="887e6-178">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="887e6-179">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="887e6-179">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="887e6-180">Solicitud (POST a message with inline image)</span><span class="sxs-lookup"><span data-stu-id="887e6-180">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="887e6-181">**Nota:** no hay ámbitos de permisos especiales en este escenario, ya que la solicitud forma parte de chatMessage; los ámbitos de chatMessage también se aplican aquí.</span><span class="sxs-lookup"><span data-stu-id="887e6-181">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="887e6-182">Respuesta</span><span class="sxs-lookup"><span data-stu-id="887e6-182">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="887e6-183">Paso cuatro: Completar el modo de migración</span><span class="sxs-lookup"><span data-stu-id="887e6-183">Step Four: Complete migration mode</span></span>

<span data-ttu-id="887e6-184">Una vez completado el proceso de migración de mensajes, el equipo y el canal se sacarán del modo de migración mediante el  `completeMigration`  método.</span><span class="sxs-lookup"><span data-stu-id="887e6-184">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="887e6-185">Este paso abre los recursos de equipo y canal para que los usen los miembros del equipo en general.</span><span class="sxs-lookup"><span data-stu-id="887e6-185">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="887e6-186">La acción está enlazada a la `team` instancia.</span><span class="sxs-lookup"><span data-stu-id="887e6-186">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="887e6-187">Solicitud (modo de migración de equipo final)</span><span class="sxs-lookup"><span data-stu-id="887e6-187">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="887e6-188">Respuesta</span><span class="sxs-lookup"><span data-stu-id="887e6-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="887e6-189">Solicitud (modo de migración de canal final)</span><span class="sxs-lookup"><span data-stu-id="887e6-189">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="887e6-190">Respuesta</span><span class="sxs-lookup"><span data-stu-id="887e6-190">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="887e6-191">Respuesta de error</span><span class="sxs-lookup"><span data-stu-id="887e6-191">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="887e6-192">Acción llamada en un `team` o que no está en `channel` `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="887e6-192">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="887e6-193">Paso cinco: Agregar miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="887e6-193">Step Five: Add team members</span></span>

<span data-ttu-id="887e6-194">Puede agregar un miembro a un equipo mediante la INTERFAZ de usuario [de Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) o la API de miembro de Complemento [de](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="887e6-194">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="887e6-195">Solicitud (agregar miembro)</span><span class="sxs-lookup"><span data-stu-id="887e6-195">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="887e6-196">Respuesta</span><span class="sxs-lookup"><span data-stu-id="887e6-196">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="887e6-197">Sugerencias e información adicional</span><span class="sxs-lookup"><span data-stu-id="887e6-197">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="887e6-198">Puede importar mensajes de usuarios que no están en Teams.</span><span class="sxs-lookup"><span data-stu-id="887e6-198">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="887e6-199">**NOTA:** Los mensajes importados para los usuarios que no están presentes en el inquilino no se podrán buscar en los portales de cumplimiento o cliente de Teams durante la versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="887e6-199">**NOTE**: Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="887e6-200">Una vez `completeMigration` realizada la solicitud, no podrá importar más mensajes en el equipo.</span><span class="sxs-lookup"><span data-stu-id="887e6-200">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="887e6-201">Los miembros del equipo solo se pueden agregar al nuevo equipo después de `completeMigration` que la solicitud haya devuelto una respuesta correcta.</span><span class="sxs-lookup"><span data-stu-id="887e6-201">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="887e6-202">Limitación: los mensajes se importan a 5 RPS por canal.</span><span class="sxs-lookup"><span data-stu-id="887e6-202">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="887e6-203">Si necesita realizar una corrección en los resultados de la migración, debe eliminar el equipo y repetir los pasos para crear el equipo y el canal y volver a migrar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="887e6-203">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="887e6-204">Actualmente, las imágenes en línea son el único tipo de medio admitido por el esquema de API de mensaje de importación.</span><span class="sxs-lookup"><span data-stu-id="887e6-204">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="887e6-205">Importar ámbito de contenido</span><span class="sxs-lookup"><span data-stu-id="887e6-205">Import content scope</span></span>

|<span data-ttu-id="887e6-206">Dentro del ámbito</span><span class="sxs-lookup"><span data-stu-id="887e6-206">In-scope</span></span> | <span data-ttu-id="887e6-207">Actualmente fuera del ámbito</span><span class="sxs-lookup"><span data-stu-id="887e6-207">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="887e6-208">Mensajes de equipo y canal</span><span class="sxs-lookup"><span data-stu-id="887e6-208">Team and channel messages</span></span>|<span data-ttu-id="887e6-209">1:1 y mensajes de chat en grupo</span><span class="sxs-lookup"><span data-stu-id="887e6-209">1:1 and group chat messages</span></span>|
|<span data-ttu-id="887e6-210">Hora de creación del mensaje original</span><span class="sxs-lookup"><span data-stu-id="887e6-210">Created time of the original message</span></span>|<span data-ttu-id="887e6-211">Canales privados</span><span class="sxs-lookup"><span data-stu-id="887e6-211">Private channels</span></span>|
|<span data-ttu-id="887e6-212">Imágenes en línea como parte del mensaje</span><span class="sxs-lookup"><span data-stu-id="887e6-212">Inline images as part of the message</span></span>|<span data-ttu-id="887e6-213">Menciones</span><span class="sxs-lookup"><span data-stu-id="887e6-213">At mentions</span></span>|
|<span data-ttu-id="887e6-214">Vínculos a archivos existentes en SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="887e6-214">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="887e6-215">Reacción</span><span class="sxs-lookup"><span data-stu-id="887e6-215">Reactions</span></span>|
|<span data-ttu-id="887e6-216">Mensajes con texto enriquecido</span><span class="sxs-lookup"><span data-stu-id="887e6-216">Messages with rich text</span></span>|<span data-ttu-id="887e6-217">Vídeos</span><span class="sxs-lookup"><span data-stu-id="887e6-217">Videos</span></span>|
|<span data-ttu-id="887e6-218">Cadena de respuesta de mensajes</span><span class="sxs-lookup"><span data-stu-id="887e6-218">Message reply chain</span></span>|<span data-ttu-id="887e6-219">Anuncios</span><span class="sxs-lookup"><span data-stu-id="887e6-219">Announcements</span></span>|
|<span data-ttu-id="887e6-220">Procesamiento de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="887e6-220">High throughput processing</span></span>|<span data-ttu-id="887e6-221">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="887e6-221">Code snippets</span></span>|
||<span data-ttu-id="887e6-222">Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="887e6-222">Adaptive cards</span></span>|
||<span data-ttu-id="887e6-223">Adhesivos</span><span class="sxs-lookup"><span data-stu-id="887e6-223">Stickers</span></span>|
||<span data-ttu-id="887e6-224">Emojis</span><span class="sxs-lookup"><span data-stu-id="887e6-224">Emojis</span></span>|
||<span data-ttu-id="887e6-225">Comillas</span><span class="sxs-lookup"><span data-stu-id="887e6-225">Quotes</span></span>|
||<span data-ttu-id="887e6-226">Publicaciones cruzadas entre canales</span><span class="sxs-lookup"><span data-stu-id="887e6-226">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="887e6-227">Más información sobre la integración de Microsoft Graph y Teams</span><span class="sxs-lookup"><span data-stu-id="887e6-227">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
