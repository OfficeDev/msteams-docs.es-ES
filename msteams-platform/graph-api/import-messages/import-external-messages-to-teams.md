---
title: Use Microsoft Graph para importar mensajes de plataforma externa a Teams
description: Describe cómo usar Microsoft Graph importar mensajes desde una plataforma externa a Teams
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: Teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 95cbf6bf2deac4ea71e60fe0fece06c1dd3ad24c
ms.sourcegitcommit: 656a1de9e23e0ad90dddcb93a2bbfcc63848a856
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53130097"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="1930a-104">Importar mensajes de plataformas de terceros a Teams con Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="1930a-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

<span data-ttu-id="1930a-105">Con Microsoft Graph, puede migrar el historial de mensajes y los datos existentes de los usuarios desde un sistema externo a un canal Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="1930a-105">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="1930a-106">Al habilitar la recreación de una jerarquía de mensajería de plataforma de terceros dentro de Teams, los usuarios pueden continuar sus comunicaciones sin problemas y continuar sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="1930a-106">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE]
> <span data-ttu-id="1930a-107">En el futuro, Microsoft puede solicitarle a usted o a sus clientes que paguen tarifas adicionales en función de la cantidad de datos que se importen.</span><span class="sxs-lookup"><span data-stu-id="1930a-107">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="1930a-108">Introducción a la importación</span><span class="sxs-lookup"><span data-stu-id="1930a-108">Import overview</span></span>

<span data-ttu-id="1930a-109">En un nivel alto, el proceso de importación consta de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1930a-109">At a high level, the import process consists of the following:</span></span>

1. <span data-ttu-id="1930a-110">[Crear un equipo con una marca de tiempo back-in-time](#step-1-create-a-team).</span><span class="sxs-lookup"><span data-stu-id="1930a-110">[Create a team with a back-in-time timestamp](#step-1-create-a-team).</span></span>
1. <span data-ttu-id="1930a-111">[Crear un canal con una marca de tiempo back-in-time](#step-2-create-a-channel).</span><span class="sxs-lookup"><span data-stu-id="1930a-111">[Create a channel with a back-in-time timestamp](#step-2-create-a-channel).</span></span>
1. <span data-ttu-id="1930a-112">[Importar mensajes externos con fecha de back-in-time](#step-3-import-messages).</span><span class="sxs-lookup"><span data-stu-id="1930a-112">[Import external back-in-time dated messages](#step-3-import-messages).</span></span>
1. <span data-ttu-id="1930a-113">[Complete el proceso de migración de equipo y canal](#step-4-complete-migration-mode).</span><span class="sxs-lookup"><span data-stu-id="1930a-113">[Complete the team and channel migration process](#step-4-complete-migration-mode).</span></span>
1. <span data-ttu-id="1930a-114">[Agregar miembros del equipo](#step-five-add-team-members).</span><span class="sxs-lookup"><span data-stu-id="1930a-114">[Add team members](#step-five-add-team-members).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1930a-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1930a-115">Prerequisites</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="1930a-116">Analizar y preparar datos de mensajes</span><span class="sxs-lookup"><span data-stu-id="1930a-116">Analyze and prepare message data</span></span>

* <span data-ttu-id="1930a-117">Revise los datos de terceros para decidir qué se migrará.</span><span class="sxs-lookup"><span data-stu-id="1930a-117">Review the third-party data to decide what will be migrated.</span></span>  
* <span data-ttu-id="1930a-118">Extrae los datos seleccionados del sistema de chat de terceros.</span><span class="sxs-lookup"><span data-stu-id="1930a-118">Extract the selected data from the third-party chat system.</span></span>  
* <span data-ttu-id="1930a-119">Asigne la estructura de chat de terceros a la Teams de chat.</span><span class="sxs-lookup"><span data-stu-id="1930a-119">Map the third-party chat structure to the Teams structure.</span></span>  
* <span data-ttu-id="1930a-120">Convertir datos de importación en formato necesario para la migración.</span><span class="sxs-lookup"><span data-stu-id="1930a-120">Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="1930a-121">Configurar el espacio empresarial de Office 365</span><span class="sxs-lookup"><span data-stu-id="1930a-121">Set up your Office 365 tenant</span></span>

* <span data-ttu-id="1930a-122">Asegúrese de que existe Office 365 inquilino para los datos de importación.</span><span class="sxs-lookup"><span data-stu-id="1930a-122">Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="1930a-123">Para obtener más información sobre cómo configurar un arrendamiento Office 365 para Teams, vea [prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="1930a-123">For more information on setting up an Office 365 tenancy for Teams, see [prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
* <span data-ttu-id="1930a-124">Asegúrese de que los miembros del equipo están en Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="1930a-124">Make sure that team members are in Azure Active Directory (AAD).</span></span> <span data-ttu-id="1930a-125">Para obtener más información, [vea Agregar un nuevo usuario a](/azure/active-directory/fundamentals/add-users-azure-active-directory) AAD.</span><span class="sxs-lookup"><span data-stu-id="1930a-125">For more information, see [add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to AAD.</span></span>

## <a name="step-1-create-a-team"></a><span data-ttu-id="1930a-126">Paso 1: Crear un equipo</span><span class="sxs-lookup"><span data-stu-id="1930a-126">Step 1: Create a team</span></span>

<span data-ttu-id="1930a-127">Dado que está migrando datos existentes, el mantenimiento de las marcas de tiempo de mensajes originales y la prevención de la actividad de mensajería durante el proceso de migración son fundamentales para volver a crear el flujo de mensajes existente del usuario en Teams.</span><span class="sxs-lookup"><span data-stu-id="1930a-127">Since you are migrating existing data, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="1930a-128">Esto se consigue de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="1930a-128">This is achieved as follows:</span></span>

> <span data-ttu-id="1930a-129">[Cree un nuevo equipo con](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) una marca de tiempo back-in-time con la propiedad de recurso de `createdDateTime` grupo.</span><span class="sxs-lookup"><span data-stu-id="1930a-129">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource `createdDateTime` property.</span></span> <span data-ttu-id="1930a-130">Coloque el nuevo equipo en , un estado especial que restringe a los usuarios de la mayoría de las actividades dentro del equipo hasta que se complete `migration mode` el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="1930a-130">Place the new team in `migration mode`, a special state that restricts users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="1930a-131">Incluya el atributo de instancia con el valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado `teamCreationMode` `migration` para la migración.</span><span class="sxs-lookup"><span data-stu-id="1930a-131">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> [!NOTE]
> <span data-ttu-id="1930a-132">El `createdDateTime` campo solo se rellenará para las instancias de un equipo o canal que se hayan migrado.</span><span class="sxs-lookup"><span data-stu-id="1930a-132">The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permission"></a><span data-ttu-id="1930a-133">Permiso</span><span class="sxs-lookup"><span data-stu-id="1930a-133">Permission</span></span>

|<span data-ttu-id="1930a-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="1930a-134">ScopeName</span></span>|<span data-ttu-id="1930a-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="1930a-135">DisplayName</span></span>|<span data-ttu-id="1930a-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="1930a-136">Description</span></span>|<span data-ttu-id="1930a-137">Tipo</span><span class="sxs-lookup"><span data-stu-id="1930a-137">Type</span></span>|<span data-ttu-id="1930a-138">¿Consentimiento de administrador?</span><span class="sxs-lookup"><span data-stu-id="1930a-138">Admin Consent?</span></span>|<span data-ttu-id="1930a-139">Entidades/API cubiertas</span><span class="sxs-lookup"><span data-stu-id="1930a-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="1930a-140">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1930a-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="1930a-141">Crear y administrar recursos para la migración a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1930a-141">Creating and managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="1930a-142">**Solo aplicación**</span><span class="sxs-lookup"><span data-stu-id="1930a-142">**Application-only**</span></span>|<span data-ttu-id="1930a-143">**Sí**</span><span class="sxs-lookup"><span data-stu-id="1930a-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="1930a-144">Solicitud (crear un equipo en estado de migración)</span><span class="sxs-lookup"><span data-stu-id="1930a-144">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="1930a-145">Respuesta</span><span class="sxs-lookup"><span data-stu-id="1930a-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-message"></a><span data-ttu-id="1930a-146">Mensaje de error</span><span class="sxs-lookup"><span data-stu-id="1930a-146">Error message</span></span>

```http
400 Bad Request
```

<span data-ttu-id="1930a-147">Puede recibir el mensaje de error en los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="1930a-147">You can receive the error message in the following scenarios:</span></span>

* <span data-ttu-id="1930a-148">Si `createdDateTime` está establecido para el futuro.</span><span class="sxs-lookup"><span data-stu-id="1930a-148">If `createdDateTime` is set for future.</span></span>
* <span data-ttu-id="1930a-149">Si se especifica correctamente, pero falta el atributo `createdDateTime` de instancia o se establece en valor no `teamCreationMode` válido.</span><span class="sxs-lookup"><span data-stu-id="1930a-149">If `createdDateTime` is correctly specified, but `teamCreationMode` instance attribute is missing or set to invalid value.</span></span>

## <a name="step-2-create-a-channel"></a><span data-ttu-id="1930a-150">Paso 2: Crear un canal</span><span class="sxs-lookup"><span data-stu-id="1930a-150">Step 2: Create a channel</span></span>

<span data-ttu-id="1930a-151">La creación de un canal para los mensajes importados es similar al escenario de creación de equipo:</span><span class="sxs-lookup"><span data-stu-id="1930a-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="1930a-152">[Cree un nuevo canal con](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) una marca de tiempo back-in-time con la propiedad de recurso `createdDateTime` channel.</span><span class="sxs-lookup"><span data-stu-id="1930a-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="1930a-153">Coloque el nuevo canal en , un estado especial que restringe a los usuarios de la mayoría de las actividades de chat dentro del canal hasta que se complete `migration mode` el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="1930a-153">Place the new channel in `migration mode`, a special state that restricts users from most chat activities within the channel until the migration process is complete.</span></span> <span data-ttu-id="1930a-154">Incluya el atributo de instancia con el valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado `channelCreationMode` `migration` para la migración.</span><span class="sxs-lookup"><span data-stu-id="1930a-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permission"></a><span data-ttu-id="1930a-155">Permiso</span><span class="sxs-lookup"><span data-stu-id="1930a-155">Permission</span></span>

|<span data-ttu-id="1930a-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="1930a-156">ScopeName</span></span>|<span data-ttu-id="1930a-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="1930a-157">DisplayName</span></span>|<span data-ttu-id="1930a-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="1930a-158">Description</span></span>|<span data-ttu-id="1930a-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="1930a-159">Type</span></span>|<span data-ttu-id="1930a-160">¿Consentimiento de administrador?</span><span class="sxs-lookup"><span data-stu-id="1930a-160">Admin Consent?</span></span>|<span data-ttu-id="1930a-161">Entidades/API cubiertas</span><span class="sxs-lookup"><span data-stu-id="1930a-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="1930a-162">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1930a-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="1930a-163">Crear y administrar recursos para la migración a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1930a-163">Creating and managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="1930a-164">**Solo aplicación**</span><span class="sxs-lookup"><span data-stu-id="1930a-164">**Application-only**</span></span>|<span data-ttu-id="1930a-165">**Sí**</span><span class="sxs-lookup"><span data-stu-id="1930a-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="1930a-166">Solicitud (crear un canal en estado de migración)</span><span class="sxs-lookup"><span data-stu-id="1930a-166">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="1930a-167">Respuesta</span><span class="sxs-lookup"><span data-stu-id="1930a-167">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="1930a-168">Mensaje de error</span><span class="sxs-lookup"><span data-stu-id="1930a-168">Error message</span></span>

```http
400 Bad Request
```
<span data-ttu-id="1930a-169">Puede recibir el mensaje de error en los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="1930a-169">You can receive the error message in the following scenarios:</span></span>

* <span data-ttu-id="1930a-170">Si `createdDateTime` está establecido para el futuro.</span><span class="sxs-lookup"><span data-stu-id="1930a-170">If `createdDateTime` is set for future.</span></span>
* <span data-ttu-id="1930a-171">Si `createdDateTime` se especifica correctamente, pero falta el atributo de instancia o se establece en valor no `channelCreationMode` válido.</span><span class="sxs-lookup"><span data-stu-id="1930a-171">If `createdDateTime` is correctly specified but `channelCreationMode` instance attribute is missing or set to invalid value.</span></span>

## <a name="step-3-import-messages"></a><span data-ttu-id="1930a-172">Paso 3: Importar mensajes</span><span class="sxs-lookup"><span data-stu-id="1930a-172">Step 3: Import messages</span></span>

<span data-ttu-id="1930a-173">Después de crear el equipo y el canal, puede empezar a enviar mensajes back-in-time con las claves `createdDateTime`  y del cuerpo de la `from` solicitud.</span><span class="sxs-lookup"><span data-stu-id="1930a-173">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from` keys in the request body.</span></span>

> [!NOTE]
> * <span data-ttu-id="1930a-174">No se admiten los mensajes importados con versiones `createdDateTime` anteriores al subproceso de `createdDateTime` mensaje.</span><span class="sxs-lookup"><span data-stu-id="1930a-174">Messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>
> * <span data-ttu-id="1930a-175">`createdDateTime` debe ser único entre los mensajes del mismo subproceso.</span><span class="sxs-lookup"><span data-stu-id="1930a-175">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="1930a-176">`createdDateTime` admite marcas de tiempo con precisión de milisegundos.</span><span class="sxs-lookup"><span data-stu-id="1930a-176">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="1930a-177">Por ejemplo, si el mensaje de solicitud entrante tiene el valor de establecido como `createdDateTime` *2020-09-16T05:50:31.0025302Z*, se convertiría a *2020-09-16T05:50:31.002Z* cuando se ingiere el mensaje.</span><span class="sxs-lookup"><span data-stu-id="1930a-177">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="1930a-178">Solicitud (mensaje POST que es de solo texto)</span><span class="sxs-lookup"><span data-stu-id="1930a-178">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="1930a-179">Respuesta</span><span class="sxs-lookup"><span data-stu-id="1930a-179">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="1930a-180">Mensaje de error</span><span class="sxs-lookup"><span data-stu-id="1930a-180">Error message</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="1930a-181">Solicitud (POST un mensaje con imagen en línea)</span><span class="sxs-lookup"><span data-stu-id="1930a-181">Request (POST a message with inline image)</span></span>

> [!NOTE]
> * <span data-ttu-id="1930a-182">No hay ámbitos de permisos especiales en este escenario, ya que la solicitud forma parte de `chatMessage` .</span><span class="sxs-lookup"><span data-stu-id="1930a-182">There are no special permission scopes in this scenario since the request is part of `chatMessage`.</span></span>
> * <span data-ttu-id="1930a-183">Los ámbitos para `chatMessage` aplicar aquí.</span><span class="sxs-lookup"><span data-stu-id="1930a-183">The scopes for `chatMessage` apply here.</span></span>

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

#### <a name="response"></a><span data-ttu-id="1930a-184">Respuesta</span><span class="sxs-lookup"><span data-stu-id="1930a-184">Response</span></span>

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

## <a name="step-4-complete-migration-mode"></a><span data-ttu-id="1930a-185">Paso 4: Completar el modo de migración</span><span class="sxs-lookup"><span data-stu-id="1930a-185">Step 4: Complete migration mode</span></span>

<span data-ttu-id="1930a-186">Una vez completado el proceso de migración de mensajes, tanto el equipo como el canal se sacarán del modo de migración mediante el  `completeMigration` método.</span><span class="sxs-lookup"><span data-stu-id="1930a-186">After the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration` method.</span></span> <span data-ttu-id="1930a-187">En este paso se abren los recursos de equipo y canal para su uso general por parte de los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="1930a-187">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="1930a-188">La acción está enlazada a la `team` instancia.</span><span class="sxs-lookup"><span data-stu-id="1930a-188">The action is bound to the `team` instance.</span></span> <span data-ttu-id="1930a-189">Antes de que el equipo se complete, todos los canales deben completarse fuera del modo de migración.</span><span class="sxs-lookup"><span data-stu-id="1930a-189">Before the team completes, all channels must be completed out of migration mode.</span></span>

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="1930a-190">Solicitud (modo de migración de canal final)</span><span class="sxs-lookup"><span data-stu-id="1930a-190">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a><span data-ttu-id="1930a-191">Respuesta</span><span class="sxs-lookup"><span data-stu-id="1930a-191">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="1930a-192">Solicitud (modo de migración de equipo final)</span><span class="sxs-lookup"><span data-stu-id="1930a-192">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a><span data-ttu-id="1930a-193">Respuesta</span><span class="sxs-lookup"><span data-stu-id="1930a-193">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

<span data-ttu-id="1930a-194">Acción llamada en un `team` o que no está en `channel` `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="1930a-194">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="1930a-195">Paso cinco: Agregar miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="1930a-195">Step five: Add team members</span></span>

<span data-ttu-id="1930a-196">Puedes agregar un miembro a un equipo mediante la interfaz de usuario Teams [o](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) la API Graph [miembro de](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) Microsoft:</span><span class="sxs-lookup"><span data-stu-id="1930a-196">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="1930a-197">Solicitud (agregar miembro)</span><span class="sxs-lookup"><span data-stu-id="1930a-197">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="1930a-198">Respuesta</span><span class="sxs-lookup"><span data-stu-id="1930a-198">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="1930a-199">Sugerencias información adicional</span><span class="sxs-lookup"><span data-stu-id="1930a-199">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="1930a-200">Después de `completeMigration` realizar la solicitud, no puede importar más mensajes en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1930a-200">After the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="1930a-201">Solo puede agregar miembros del equipo al nuevo equipo después de que `completeMigration` la solicitud haya devuelto una respuesta correcta.</span><span class="sxs-lookup"><span data-stu-id="1930a-201">You can only add team members to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="1930a-202">Limitación: los mensajes se importan a cinco RPS por canal.</span><span class="sxs-lookup"><span data-stu-id="1930a-202">Throttling: Messages import at five RPS per channel.</span></span>

* <span data-ttu-id="1930a-203">Si necesita realizar una corrección en los resultados de la migración, debe eliminar el equipo y repetir los pasos para crear el equipo y canalizar y volver a migrar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="1930a-203">If you need to make a correction to the migration results, you must delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="1930a-204">Actualmente, las imágenes en línea son el único tipo de medios admitidos por el esquema de api de mensajes de importación.</span><span class="sxs-lookup"><span data-stu-id="1930a-204">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="1930a-205">Importar ámbito de contenido</span><span class="sxs-lookup"><span data-stu-id="1930a-205">Import content scope</span></span>

<span data-ttu-id="1930a-206">En la tabla siguiente se proporciona el ámbito de contenido:</span><span class="sxs-lookup"><span data-stu-id="1930a-206">The following table provides the content scope:</span></span>

|<span data-ttu-id="1930a-207">En el ámbito</span><span class="sxs-lookup"><span data-stu-id="1930a-207">In-scope</span></span> | <span data-ttu-id="1930a-208">Actualmente fuera del ámbito</span><span class="sxs-lookup"><span data-stu-id="1930a-208">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="1930a-209">Mensajes de equipo y canal</span><span class="sxs-lookup"><span data-stu-id="1930a-209">Team and channel messages</span></span>|<span data-ttu-id="1930a-210">1:1 y mensajes de chat en grupo</span><span class="sxs-lookup"><span data-stu-id="1930a-210">1:1 and group chat messages</span></span>|
|<span data-ttu-id="1930a-211">Hora de creación del mensaje original</span><span class="sxs-lookup"><span data-stu-id="1930a-211">Created time of the original message</span></span>|<span data-ttu-id="1930a-212">Canales privados</span><span class="sxs-lookup"><span data-stu-id="1930a-212">Private channels</span></span>|
|<span data-ttu-id="1930a-213">Imágenes en línea como parte del mensaje</span><span class="sxs-lookup"><span data-stu-id="1930a-213">Inline images as part of the message</span></span>|<span data-ttu-id="1930a-214">En menciones</span><span class="sxs-lookup"><span data-stu-id="1930a-214">At mentions</span></span>|
|<span data-ttu-id="1930a-215">Vínculos a archivos existentes en SPO o OneDrive</span><span class="sxs-lookup"><span data-stu-id="1930a-215">Links to existing files in SPO or OneDrive</span></span>|<span data-ttu-id="1930a-216">Reacciones</span><span class="sxs-lookup"><span data-stu-id="1930a-216">Reactions</span></span>|
|<span data-ttu-id="1930a-217">Mensajes con texto enriquecido</span><span class="sxs-lookup"><span data-stu-id="1930a-217">Messages with rich text</span></span>|<span data-ttu-id="1930a-218">Vídeos</span><span class="sxs-lookup"><span data-stu-id="1930a-218">Videos</span></span>|
|<span data-ttu-id="1930a-219">Cadena de respuesta de mensajes</span><span class="sxs-lookup"><span data-stu-id="1930a-219">Message reply chain</span></span>|<span data-ttu-id="1930a-220">Anuncios</span><span class="sxs-lookup"><span data-stu-id="1930a-220">Announcements</span></span>|
|<span data-ttu-id="1930a-221">Procesamiento de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="1930a-221">High throughput processing</span></span>|<span data-ttu-id="1930a-222">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="1930a-222">Code snippets</span></span>|
||<span data-ttu-id="1930a-223">Adhesivos</span><span class="sxs-lookup"><span data-stu-id="1930a-223">Stickers</span></span>|
||<span data-ttu-id="1930a-224">Emojis</span><span class="sxs-lookup"><span data-stu-id="1930a-224">Emojis</span></span>|
||<span data-ttu-id="1930a-225">Ofertas</span><span class="sxs-lookup"><span data-stu-id="1930a-225">Quotes</span></span>|
||<span data-ttu-id="1930a-226">Publicaciones cruzadas entre canales</span><span class="sxs-lookup"><span data-stu-id="1930a-226">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="1930a-227">Vea también</span><span class="sxs-lookup"><span data-stu-id="1930a-227">See also</span></span>

[<span data-ttu-id="1930a-228">Integración Graph y Teams Microsoft</span><span class="sxs-lookup"><span data-stu-id="1930a-228">Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
