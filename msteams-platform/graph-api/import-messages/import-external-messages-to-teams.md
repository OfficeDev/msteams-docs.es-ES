---
title: Use Microsoft Graph para importar mensajes de plataforma externos a Teams
description: Describe cómo usar Microsoft Graph para importar mensajes desde una plataforma externa a Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: los equipos importan mensajes api gráfico microsoft migrate migration post
ms.openlocfilehash: 5ea06e8b490bae0595abb31086848d0b050bded0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566162"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="16b19-104">Importar mensajes de plataformas de terceros a Teams con Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="16b19-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

<span data-ttu-id="16b19-105">Con Microsoft Graph, puede migrar el historial de mensajes y los datos existentes de los usuarios desde un sistema externo a un canal Teams.</span><span class="sxs-lookup"><span data-stu-id="16b19-105">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="16b19-106">Al permitir la recreación de una jerarquía de mensajería de plataforma de terceros dentro de Teams, los usuarios pueden continuar sus comunicaciones de una manera perfecta y proceder sin interrupción.</span><span class="sxs-lookup"><span data-stu-id="16b19-106">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE] 
> <span data-ttu-id="16b19-107">En el futuro, Microsoft puede solicitarle a usted o a sus clientes que paguen tarifas adicionales en función de la cantidad de datos que se importen.</span><span class="sxs-lookup"><span data-stu-id="16b19-107">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="16b19-108">Descripción general de las importaciones</span><span class="sxs-lookup"><span data-stu-id="16b19-108">Import overview</span></span>

<span data-ttu-id="16b19-109">En un nivel alto, el proceso de importación consta de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="16b19-109">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="16b19-110">Crea un equipo con una marca de tiempo de vuelta en el tiempo</span><span class="sxs-lookup"><span data-stu-id="16b19-110">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="16b19-111">Cree un canal con una marca de tiempo de nuevo en el tiempo</span><span class="sxs-lookup"><span data-stu-id="16b19-111">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel) 
1. [<span data-ttu-id="16b19-112">Importar mensajes externos de fecha de nuevo en el tiempo</span><span class="sxs-lookup"><span data-stu-id="16b19-112">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="16b19-113">Completar el equipo y el proceso de migración de canales</span><span class="sxs-lookup"><span data-stu-id="16b19-113">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="16b19-114">Añadir miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="16b19-114">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="16b19-115">Requisitos necesarios</span><span class="sxs-lookup"><span data-stu-id="16b19-115">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="16b19-116">Analizar y preparar datos de mensajes</span><span class="sxs-lookup"><span data-stu-id="16b19-116">Analyze and prepare message data</span></span>

<span data-ttu-id="16b19-117">✔ Revise los datos de terceros para decidir qué se migrarán.</span><span class="sxs-lookup"><span data-stu-id="16b19-117">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="16b19-118">✔ Extraer los datos seleccionados del sistema de chat de terceros.</span><span class="sxs-lookup"><span data-stu-id="16b19-118">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="16b19-119">✔ Asignar la estructura de chat de terceros a la estructura Teams.</span><span class="sxs-lookup"><span data-stu-id="16b19-119">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="16b19-120">✔ Convertir datos de importación en el formato necesario para la migración.</span><span class="sxs-lookup"><span data-stu-id="16b19-120">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="16b19-121">Configurar el espacio empresarial de Office 365</span><span class="sxs-lookup"><span data-stu-id="16b19-121">Set up your Office 365 tenant</span></span>

<span data-ttu-id="16b19-122">✔ Asegúrese de que existe un inquilino Office 365 para los datos de importación.</span><span class="sxs-lookup"><span data-stu-id="16b19-122">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="16b19-123">Para obtener más información sobre cómo configurar una tenencia Office 365 para Teams, consulte [Preparar el inquilino de Office 365](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="16b19-123">For more information on setting up an Office 365 tenancy for Teams, see [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="16b19-124">✔ Asegúrese de que los miembros del equipo estén en Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="16b19-124">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="16b19-125">Para obtener más información, consulte [Agregar un nuevo usuario](/azure/active-directory/fundamentals/add-users-azure-active-directory) a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16b19-125">For more information, see [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="16b19-126">Paso Uno: Crear un equipo</span><span class="sxs-lookup"><span data-stu-id="16b19-126">Step One: Create a team</span></span>

<span data-ttu-id="16b19-127">Dado que se migran los datos existentes, mantener las marcas de tiempo del mensaje original y evitar la actividad de mensajería durante el proceso de migración son clave para volver a crear el flujo de mensajes existente del usuario en Teams.</span><span class="sxs-lookup"><span data-stu-id="16b19-127">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="16b19-128">Esto se logra de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="16b19-128">This is achieved as follows:</span></span>

> <span data-ttu-id="16b19-129">[Cree un nuevo equipo](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) con una marca de tiempo consecutiva mediante la propiedad de recursos del  `createdDateTime`  equipo.</span><span class="sxs-lookup"><span data-stu-id="16b19-129">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="16b19-130">Coloque el nuevo equipo en `migration mode` , un estado especial que prohíbe a los usuarios de la mayoría de las actividades dentro del equipo hasta que se complete el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="16b19-130">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="16b19-131">Incluya el `teamCreationMode` atributo instance con el valor de la solicitud POST para identificar `migration` explícitamente el nuevo equipo como creado para la migración.</span><span class="sxs-lookup"><span data-stu-id="16b19-131">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> [!Note]
> <span data-ttu-id="16b19-132">El `createdDateTime` campo solo se rellenará para las instancias de un equipo o canal que se hayan migrado.</span><span class="sxs-lookup"><span data-stu-id="16b19-132">The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="16b19-133">Permisos</span><span class="sxs-lookup"><span data-stu-id="16b19-133">Permissions</span></span>

|<span data-ttu-id="16b19-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="16b19-134">ScopeName</span></span>|<span data-ttu-id="16b19-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="16b19-135">DisplayName</span></span>|<span data-ttu-id="16b19-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="16b19-136">Description</span></span>|<span data-ttu-id="16b19-137">Tipo</span><span class="sxs-lookup"><span data-stu-id="16b19-137">Type</span></span>|<span data-ttu-id="16b19-138">¿Consentimiento de administrador?</span><span class="sxs-lookup"><span data-stu-id="16b19-138">Admin Consent?</span></span>|<span data-ttu-id="16b19-139">Entidades/API cubiertas</span><span class="sxs-lookup"><span data-stu-id="16b19-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="16b19-140">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="16b19-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="16b19-141">Crear y administrar recursos para la migración a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="16b19-141">Creating, managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="16b19-142">**Solo aplicación**</span><span class="sxs-lookup"><span data-stu-id="16b19-142">**Application-only**</span></span>|<span data-ttu-id="16b19-143">**Sí**</span><span class="sxs-lookup"><span data-stu-id="16b19-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="16b19-144">Solicitud (cree un equipo en estado de migración)</span><span class="sxs-lookup"><span data-stu-id="16b19-144">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="16b19-145">Respuesta</span><span class="sxs-lookup"><span data-stu-id="16b19-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-messages"></a><span data-ttu-id="16b19-146">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="16b19-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="16b19-147">`createdDateTime`  listo para el futuro.</span><span class="sxs-lookup"><span data-stu-id="16b19-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="16b19-148">`createdDateTime`  especificado correctamente, pero `teamCreationMode`  falta el atributo instance o se establece en valor no válido.</span><span class="sxs-lookup"><span data-stu-id="16b19-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="16b19-149">Paso Dos: Crear un canal</span><span class="sxs-lookup"><span data-stu-id="16b19-149">Step Two: Create a channel</span></span>

<span data-ttu-id="16b19-150">Crear un canal para los mensajes importados es similar al escenario de crear equipo:</span><span class="sxs-lookup"><span data-stu-id="16b19-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="16b19-151">[Cree un nuevo canal](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) con una marca de tiempo de nuevo en el tiempo mediante la propiedad de recurso de `createdDateTime` canal.</span><span class="sxs-lookup"><span data-stu-id="16b19-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="16b19-152">Coloque el nuevo canal en `migration mode` , un estado especial que prohíbe a los usuarios de la mayoría de las actividades de chat dentro del canal hasta que se complete el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="16b19-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="16b19-153">Incluya el `channelCreationMode` atributo instance con el valor de la solicitud POST para identificar `migration` explícitamente el nuevo equipo como creado para la migración.</span><span class="sxs-lookup"><span data-stu-id="16b19-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="16b19-154">Permisos</span><span class="sxs-lookup"><span data-stu-id="16b19-154">Permissions</span></span>

|<span data-ttu-id="16b19-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="16b19-155">ScopeName</span></span>|<span data-ttu-id="16b19-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="16b19-156">DisplayName</span></span>|<span data-ttu-id="16b19-157">Descripción</span><span class="sxs-lookup"><span data-stu-id="16b19-157">Description</span></span>|<span data-ttu-id="16b19-158">Tipo</span><span class="sxs-lookup"><span data-stu-id="16b19-158">Type</span></span>|<span data-ttu-id="16b19-159">¿Consentimiento de administrador?</span><span class="sxs-lookup"><span data-stu-id="16b19-159">Admin Consent?</span></span>|<span data-ttu-id="16b19-160">Entidades/API cubiertas</span><span class="sxs-lookup"><span data-stu-id="16b19-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="16b19-161">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="16b19-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="16b19-162">Crear y administrar recursos para la migración a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="16b19-162">Creating, managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="16b19-163">**Solo aplicación**</span><span class="sxs-lookup"><span data-stu-id="16b19-163">**Application-only**</span></span>|<span data-ttu-id="16b19-164">**Sí**</span><span class="sxs-lookup"><span data-stu-id="16b19-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="16b19-165">Solicitud (cree un canal en estado de migración)</span><span class="sxs-lookup"><span data-stu-id="16b19-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="16b19-166">Respuesta</span><span class="sxs-lookup"><span data-stu-id="16b19-166">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="16b19-167">Mensaje de error</span><span class="sxs-lookup"><span data-stu-id="16b19-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="16b19-168">`createdDateTime`  listo para el futuro.</span><span class="sxs-lookup"><span data-stu-id="16b19-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="16b19-169">`createdDateTime`  especificado correctamente, pero `channelCreationMode`  falta el atributo instance o se establece en valor no válido.</span><span class="sxs-lookup"><span data-stu-id="16b19-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="16b19-170">Paso tres: Importar mensajes</span><span class="sxs-lookup"><span data-stu-id="16b19-170">Step Three: Import messages</span></span>

<span data-ttu-id="16b19-171">Una vez creado el equipo y el canal, puede comenzar a enviar mensajes a tiempo mediante las `createdDateTime`  teclas y `from`  las claves del cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="16b19-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="16b19-172">**NOTA:** no se admiten los mensajes importados con `createdDateTime` anterioridad al subproceso de `createdDateTime` mensaje.</span><span class="sxs-lookup"><span data-stu-id="16b19-172">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="16b19-173">`createdDateTime` debe ser único entre los mensajes del mismo subproceso.</span><span class="sxs-lookup"><span data-stu-id="16b19-173">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="16b19-174">`createdDateTime` soporta marcas de tiempo con precisión de milisegundos.</span><span class="sxs-lookup"><span data-stu-id="16b19-174">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="16b19-175">Por ejemplo, si el mensaje de solicitud entrante tiene el valor de `createdDateTime` set como *2020-09-16T05:50:31.0025302Z*, se convertiría en *2020-09-16T05:50:31.002Z* cuando se ingiere el mensaje.</span><span class="sxs-lookup"><span data-stu-id="16b19-175">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="16b19-176">Solicitud (mensaje POST que es de solo texto)</span><span class="sxs-lookup"><span data-stu-id="16b19-176">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="16b19-177">Respuesta</span><span class="sxs-lookup"><span data-stu-id="16b19-177">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="16b19-178">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="16b19-178">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="16b19-179">Solicitud (PUBLIQUE un mensaje con imagen en línea)</span><span class="sxs-lookup"><span data-stu-id="16b19-179">Request (POST a message with inline image)</span></span>

> [!Note]
> <span data-ttu-id="16b19-180">No hay ámbitos de permisos especiales en este escenario, ya que la solicitud forma parte de chatMessage; también se aplican alcances para chatMessage aquí.</span><span class="sxs-lookup"><span data-stu-id="16b19-180">There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="16b19-181">Respuesta</span><span class="sxs-lookup"><span data-stu-id="16b19-181">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="16b19-182">Paso cuatro: Modo de migración completo</span><span class="sxs-lookup"><span data-stu-id="16b19-182">Step Four: Complete migration mode</span></span>

<span data-ttu-id="16b19-183">Una vez completado el proceso de migración de mensajes, tanto el equipo como el canal se sacan del modo de migración mediante el  `completeMigration`  método.</span><span class="sxs-lookup"><span data-stu-id="16b19-183">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="16b19-184">Este paso abre los recursos de equipo y canal para uso general de los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="16b19-184">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="16b19-185">La acción está enlazada a la `team` instancia.</span><span class="sxs-lookup"><span data-stu-id="16b19-185">The action is bound to the `team` instance.</span></span> <span data-ttu-id="16b19-186">Todos los canales deben completarse fuera del modo de migración antes de que el equipo pueda completarse.</span><span class="sxs-lookup"><span data-stu-id="16b19-186">All channels must be completed out of migration mode before the team can be completed.</span></span>

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="16b19-187">Solicitud (modo de migración de canal final)</span><span class="sxs-lookup"><span data-stu-id="16b19-187">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a><span data-ttu-id="16b19-188">Respuesta</span><span class="sxs-lookup"><span data-stu-id="16b19-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="16b19-189">Solicitud (modo de migración de equipo final)</span><span class="sxs-lookup"><span data-stu-id="16b19-189">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a><span data-ttu-id="16b19-190">Respuesta</span><span class="sxs-lookup"><span data-stu-id="16b19-190">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

* <span data-ttu-id="16b19-191">Acción llamada a un `team` o que no está en `channel` `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="16b19-191">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="16b19-192">Paso Cinco: Añadir miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="16b19-192">Step Five: Add team members</span></span>

<span data-ttu-id="16b19-193">Puede agregar un miembro a un equipo [mediante la interfaz de usuario de Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) o Microsoft Graph Agregar API [miembro:](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="16b19-193">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="16b19-194">Solicitud (agregar miembro)</span><span class="sxs-lookup"><span data-stu-id="16b19-194">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="16b19-195">Respuesta</span><span class="sxs-lookup"><span data-stu-id="16b19-195">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="16b19-196">Sugerencias e información adicional</span><span class="sxs-lookup"><span data-stu-id="16b19-196">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="16b19-197">Una vez realizada la `completeMigration` solicitud, no puede importar más mensajes al equipo.</span><span class="sxs-lookup"><span data-stu-id="16b19-197">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="16b19-198">Los miembros del equipo solo se pueden agregar al nuevo equipo después de que la `completeMigration` solicitud haya devuelto una respuesta correcta.</span><span class="sxs-lookup"><span data-stu-id="16b19-198">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="16b19-199">Limitación: los mensajes importan a 5 RPS por canal.</span><span class="sxs-lookup"><span data-stu-id="16b19-199">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="16b19-200">Si necesita realizar una corrección de los resultados de la migración, debe eliminar el equipo y repetir los pasos para crear el equipo y el canal y volver a migrar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="16b19-200">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="16b19-201">Actualmente, las imágenes en línea son el único tipo de medio admitido por el esquema de API de mensajes de importación.</span><span class="sxs-lookup"><span data-stu-id="16b19-201">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="16b19-202">Importar contenido</span><span class="sxs-lookup"><span data-stu-id="16b19-202">Import content scope</span></span>

|<span data-ttu-id="16b19-203">En el ámbito</span><span class="sxs-lookup"><span data-stu-id="16b19-203">In-scope</span></span> | <span data-ttu-id="16b19-204">Actualmente fuera de alcance</span><span class="sxs-lookup"><span data-stu-id="16b19-204">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="16b19-205">Mensajes de equipo y canal</span><span class="sxs-lookup"><span data-stu-id="16b19-205">Team and channel messages</span></span>|<span data-ttu-id="16b19-206">1:1 y mensajes de chat de grupo</span><span class="sxs-lookup"><span data-stu-id="16b19-206">1:1 and group chat messages</span></span>|
|<span data-ttu-id="16b19-207">Tiempo creado del mensaje original</span><span class="sxs-lookup"><span data-stu-id="16b19-207">Created time of the original message</span></span>|<span data-ttu-id="16b19-208">Canales privados</span><span class="sxs-lookup"><span data-stu-id="16b19-208">Private channels</span></span>|
|<span data-ttu-id="16b19-209">Imágenes en línea como parte del mensaje</span><span class="sxs-lookup"><span data-stu-id="16b19-209">Inline images as part of the message</span></span>|<span data-ttu-id="16b19-210">En las menciones</span><span class="sxs-lookup"><span data-stu-id="16b19-210">At mentions</span></span>|
|<span data-ttu-id="16b19-211">Vínculos a archivos existentes en SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="16b19-211">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="16b19-212">Reacciones</span><span class="sxs-lookup"><span data-stu-id="16b19-212">Reactions</span></span>|
|<span data-ttu-id="16b19-213">Mensajes con texto enriquecido</span><span class="sxs-lookup"><span data-stu-id="16b19-213">Messages with rich text</span></span>|<span data-ttu-id="16b19-214">Vídeos</span><span class="sxs-lookup"><span data-stu-id="16b19-214">Videos</span></span>|
|<span data-ttu-id="16b19-215">Cadena de respuesta de mensajes</span><span class="sxs-lookup"><span data-stu-id="16b19-215">Message reply chain</span></span>|<span data-ttu-id="16b19-216">Anuncios</span><span class="sxs-lookup"><span data-stu-id="16b19-216">Announcements</span></span>|
|<span data-ttu-id="16b19-217">Procesamiento de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="16b19-217">High throughput processing</span></span>|<span data-ttu-id="16b19-218">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="16b19-218">Code snippets</span></span>|
||<span data-ttu-id="16b19-219">Pegatinas</span><span class="sxs-lookup"><span data-stu-id="16b19-219">Stickers</span></span>|
||<span data-ttu-id="16b19-220">Emojis</span><span class="sxs-lookup"><span data-stu-id="16b19-220">Emojis</span></span>|
||<span data-ttu-id="16b19-221">Ofertas</span><span class="sxs-lookup"><span data-stu-id="16b19-221">Quotes</span></span>|
||<span data-ttu-id="16b19-222">Cruce de publicaciones entre canales</span><span class="sxs-lookup"><span data-stu-id="16b19-222">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="16b19-223">Vea también</span><span class="sxs-lookup"><span data-stu-id="16b19-223">See also</span></span>

[<span data-ttu-id="16b19-224">Obtenga más información sobre la integración de Microsoft Graph y Teams</span><span class="sxs-lookup"><span data-stu-id="16b19-224">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
