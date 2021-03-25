---
title: Usar Microsoft Graph para importar mensajes de plataforma externa a Teams
description: Describe cómo usar Microsoft Graph para importar mensajes de una plataforma externa a Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 8cf4f964aba7ce9375b1b259ae88a7fbcb620631
ms.sourcegitcommit: f6e4a303828224a702138753a8e5e27c8a094c82
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/24/2021
ms.locfileid: "51176959"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="8c7ca-104">Importar mensajes de plataformas de terceros a Teams con Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="8c7ca-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="8c7ca-105">Las vistas previas públicas de Microsoft Graph y Microsoft Teams están disponibles para el acceso anticipado y los comentarios.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="8c7ca-106">Aunque esta versión se ha sometido a pruebas exhaustivas, no está diseñada para su uso en producción.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="8c7ca-107">Con Microsoft Graph, puede migrar el historial de mensajes y los datos existentes de los usuarios desde un sistema externo a un canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="8c7ca-108">Al habilitar la recreación de una jerarquía de mensajería de plataforma de terceros dentro de Teams, los usuarios pueden continuar sus comunicaciones sin problemas y continuar sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE] 
> <span data-ttu-id="8c7ca-109">En el futuro, Microsoft puede solicitarle a usted o a sus clientes que paguen tarifas adicionales en función de la cantidad de datos que se importen.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-109">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="8c7ca-110">Introducción a la importación</span><span class="sxs-lookup"><span data-stu-id="8c7ca-110">Import overview</span></span>

<span data-ttu-id="8c7ca-111">En un nivel alto, el proceso de importación consta de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8c7ca-111">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="8c7ca-112">Crear un equipo con una marca de tiempo back-in-time</span><span class="sxs-lookup"><span data-stu-id="8c7ca-112">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="8c7ca-113">Crear un canal con una marca de tiempo back-in-time</span><span class="sxs-lookup"><span data-stu-id="8c7ca-113">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="8c7ca-114">Importar mensajes con fecha de back-in-time externos</span><span class="sxs-lookup"><span data-stu-id="8c7ca-114">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="8c7ca-115">Completar el proceso de migración de equipos y canales</span><span class="sxs-lookup"><span data-stu-id="8c7ca-115">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="8c7ca-116">Agregar miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="8c7ca-116">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="8c7ca-117">Requisitos necesarios</span><span class="sxs-lookup"><span data-stu-id="8c7ca-117">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="8c7ca-118">Analizar y preparar datos de mensajes</span><span class="sxs-lookup"><span data-stu-id="8c7ca-118">Analyze and prepare message data</span></span>

<span data-ttu-id="8c7ca-119">✔ revisar los datos de terceros para decidir qué se migrará.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-119">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="8c7ca-120">✔ extraer los datos seleccionados del sistema de chat de terceros.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-120">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="8c7ca-121">✔ asignar la estructura de chat de terceros a la estructura de Teams.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-121">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="8c7ca-122">✔ Convertir datos de importación en formato necesario para la migración.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-122">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="8c7ca-123">Configurar el espacio empresarial de Office 365</span><span class="sxs-lookup"><span data-stu-id="8c7ca-123">Set up your Office 365 tenant</span></span>

<span data-ttu-id="8c7ca-124">✔ asegúrese de que existe un inquilino de Office 365 para los datos de importación.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-124">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="8c7ca-125">Para obtener más información sobre cómo configurar un arrendamiento de Office 365 para *Teams,* vea , [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="8c7ca-125">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="8c7ca-126">✔ asegúrese de que los miembros del equipo están en Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="8c7ca-126">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="8c7ca-127">Para obtener más *información, vea* [Agregar un nuevo usuario a](/azure/active-directory/fundamentals/add-users-azure-active-directory) Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-127">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="8c7ca-128">Paso uno: Crear un equipo</span><span class="sxs-lookup"><span data-stu-id="8c7ca-128">Step One: Create a team</span></span>

<span data-ttu-id="8c7ca-129">Dado que los datos existentes se migran, el mantenimiento de las marcas de tiempo de mensajes originales y la prevención de la actividad de mensajería durante el proceso de migración son fundamentales para recrear el flujo de mensajes existente del usuario en Teams.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-129">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="8c7ca-130">Esto se consigue de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="8c7ca-130">This is achieved as follows:</span></span>

> <span data-ttu-id="8c7ca-131">[Cree un nuevo equipo con](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) una marca de tiempo back-in-time con la propiedad de recurso de  `createdDateTime`  grupo.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-131">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="8c7ca-132">Coloque el nuevo equipo en , un estado especial que reja a los usuarios de la mayoría de las actividades dentro del equipo hasta que se complete `migration mode` el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-132">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="8c7ca-133">Incluya el atributo de instancia con el valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado `teamCreationMode` `migration` para la migración.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-133">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="8c7ca-134">**NOTA:** El `createdDateTime` campo solo se rellenará para las instancias de un equipo o canal que se hayan migrado.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-134">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="8c7ca-135">Permisos</span><span class="sxs-lookup"><span data-stu-id="8c7ca-135">Permissions</span></span>

|<span data-ttu-id="8c7ca-136">ScopeName</span><span class="sxs-lookup"><span data-stu-id="8c7ca-136">ScopeName</span></span>|<span data-ttu-id="8c7ca-137">DisplayName</span><span class="sxs-lookup"><span data-stu-id="8c7ca-137">DisplayName</span></span>|<span data-ttu-id="8c7ca-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="8c7ca-138">Description</span></span>|<span data-ttu-id="8c7ca-139">Tipo</span><span class="sxs-lookup"><span data-stu-id="8c7ca-139">Type</span></span>|<span data-ttu-id="8c7ca-140">¿Consentimiento de administrador?</span><span class="sxs-lookup"><span data-stu-id="8c7ca-140">Admin Consent?</span></span>|<span data-ttu-id="8c7ca-141">Entidades/API cubiertas</span><span class="sxs-lookup"><span data-stu-id="8c7ca-141">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="8c7ca-142">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8c7ca-142">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="8c7ca-143">Creación y administración de recursos para la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8c7ca-143">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="8c7ca-144">**Solo aplicación**</span><span class="sxs-lookup"><span data-stu-id="8c7ca-144">**Application-only**</span></span>|<span data-ttu-id="8c7ca-145">**Sí**</span><span class="sxs-lookup"><span data-stu-id="8c7ca-145">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="8c7ca-146">Solicitud (crear un equipo en estado de migración)</span><span class="sxs-lookup"><span data-stu-id="8c7ca-146">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="8c7ca-147">Respuesta</span><span class="sxs-lookup"><span data-stu-id="8c7ca-147">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="8c7ca-148">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="8c7ca-148">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="8c7ca-149">`createdDateTime`  para el futuro.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-149">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="8c7ca-150">`createdDateTime`  especificado correctamente, pero falta `teamCreationMode`  el atributo de instancia o se establece en valor no válido.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-150">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="8c7ca-151">Paso dos: Crear un canal</span><span class="sxs-lookup"><span data-stu-id="8c7ca-151">Step Two: Create a channel</span></span>

<span data-ttu-id="8c7ca-152">La creación de un canal para los mensajes importados es similar al escenario de creación de equipo:</span><span class="sxs-lookup"><span data-stu-id="8c7ca-152">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="8c7ca-153">[Cree un nuevo canal con](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) una marca de tiempo back-in-time con la propiedad de recurso `createdDateTime` channel.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-153">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="8c7ca-154">Coloque el nuevo canal en , un estado especial que reja a los usuarios de la mayoría de las actividades de chat dentro del canal hasta que se complete `migration mode` el proceso de migración.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-154">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="8c7ca-155">Incluya el atributo de instancia con el valor en la solicitud POST para identificar explícitamente al nuevo equipo como creado `channelCreationMode` `migration` para la migración.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-155">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="8c7ca-156">Permisos</span><span class="sxs-lookup"><span data-stu-id="8c7ca-156">Permissions</span></span>

|<span data-ttu-id="8c7ca-157">ScopeName</span><span class="sxs-lookup"><span data-stu-id="8c7ca-157">ScopeName</span></span>|<span data-ttu-id="8c7ca-158">DisplayName</span><span class="sxs-lookup"><span data-stu-id="8c7ca-158">DisplayName</span></span>|<span data-ttu-id="8c7ca-159">Descripción</span><span class="sxs-lookup"><span data-stu-id="8c7ca-159">Description</span></span>|<span data-ttu-id="8c7ca-160">Tipo</span><span class="sxs-lookup"><span data-stu-id="8c7ca-160">Type</span></span>|<span data-ttu-id="8c7ca-161">¿Consentimiento de administrador?</span><span class="sxs-lookup"><span data-stu-id="8c7ca-161">Admin Consent?</span></span>|<span data-ttu-id="8c7ca-162">Entidades/API cubiertas</span><span class="sxs-lookup"><span data-stu-id="8c7ca-162">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="8c7ca-163">Administrar la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8c7ca-163">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="8c7ca-164">Creación y administración de recursos para la migración a Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8c7ca-164">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="8c7ca-165">**Solo aplicación**</span><span class="sxs-lookup"><span data-stu-id="8c7ca-165">**Application-only**</span></span>|<span data-ttu-id="8c7ca-166">**Sí**</span><span class="sxs-lookup"><span data-stu-id="8c7ca-166">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="8c7ca-167">Solicitud (crear un canal en estado de migración)</span><span class="sxs-lookup"><span data-stu-id="8c7ca-167">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="8c7ca-168">Respuesta</span><span class="sxs-lookup"><span data-stu-id="8c7ca-168">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="8c7ca-169">Mensaje de error</span><span class="sxs-lookup"><span data-stu-id="8c7ca-169">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="8c7ca-170">`createdDateTime`  para el futuro.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-170">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="8c7ca-171">`createdDateTime`  especificado correctamente, pero `channelCreationMode`  falta el atributo de instancia o se establece en valor no válido.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-171">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="8c7ca-172">Paso tres: Importar mensajes</span><span class="sxs-lookup"><span data-stu-id="8c7ca-172">Step Three: Import messages</span></span>

<span data-ttu-id="8c7ca-173">Después de crear el equipo y el canal, puede empezar a enviar mensajes back-in-time con las claves `createdDateTime`  y del cuerpo de la `from`  solicitud.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-173">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="8c7ca-174">**NOTA:** no se admiten los mensajes importados con versiones anteriores al `createdDateTime` `createdDateTime` subproceso de mensaje.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-174">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="8c7ca-175">`createdDateTime` debe ser único entre los mensajes del mismo subproceso.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-175">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="8c7ca-176">`createdDateTime` admite marcas de tiempo con precisión de milisegundos.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-176">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="8c7ca-177">Por ejemplo, si el mensaje de solicitud entrante tiene el valor de establecido como `createdDateTime` *2020-09-16T05:50:31.0025302Z*, se convertiría a *2020-09-16T05:50:31.002Z* cuando se ingiere el mensaje.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-177">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="8c7ca-178">Solicitud (mensaje POST que es de solo texto)</span><span class="sxs-lookup"><span data-stu-id="8c7ca-178">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="8c7ca-179">Respuesta</span><span class="sxs-lookup"><span data-stu-id="8c7ca-179">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="8c7ca-180">Mensajes de error</span><span class="sxs-lookup"><span data-stu-id="8c7ca-180">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="8c7ca-181">Solicitud (POST un mensaje con imagen en línea)</span><span class="sxs-lookup"><span data-stu-id="8c7ca-181">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="8c7ca-182">**Nota:** No hay ámbitos de permisos especiales en este escenario, ya que la solicitud forma parte de chatMessage; los ámbitos de chatMessage también se aplican aquí.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-182">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="8c7ca-183">Respuesta</span><span class="sxs-lookup"><span data-stu-id="8c7ca-183">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="8c7ca-184">Paso cuatro: Completar el modo de migración</span><span class="sxs-lookup"><span data-stu-id="8c7ca-184">Step Four: Complete migration mode</span></span>

<span data-ttu-id="8c7ca-185">Una vez completado el proceso de migración de mensajes, tanto el equipo como el canal se sacarán del modo de migración mediante el  `completeMigration`  método.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-185">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="8c7ca-186">En este paso se abren los recursos de equipo y canal para su uso general por parte de los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-186">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="8c7ca-187">La acción está enlazada a la `team` instancia.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-187">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="8c7ca-188">Solicitud (modo de migración de equipo final)</span><span class="sxs-lookup"><span data-stu-id="8c7ca-188">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="8c7ca-189">Respuesta</span><span class="sxs-lookup"><span data-stu-id="8c7ca-189">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="8c7ca-190">Solicitud (modo de migración de canal final)</span><span class="sxs-lookup"><span data-stu-id="8c7ca-190">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="8c7ca-191">Respuesta</span><span class="sxs-lookup"><span data-stu-id="8c7ca-191">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="8c7ca-192">Respuesta de error</span><span class="sxs-lookup"><span data-stu-id="8c7ca-192">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="8c7ca-193">Acción llamada en un `team` o que no está en `channel` `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="8c7ca-193">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="8c7ca-194">Paso cinco: Agregar miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="8c7ca-194">Step Five: Add team members</span></span>

<span data-ttu-id="8c7ca-195">Puedes agregar un miembro a un equipo [mediante la](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) INTERFAZ de usuario de Teams o la API de miembros de Microsoft Graph [Add:](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8c7ca-195">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="8c7ca-196">Solicitud (agregar miembro)</span><span class="sxs-lookup"><span data-stu-id="8c7ca-196">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="8c7ca-197">Respuesta</span><span class="sxs-lookup"><span data-stu-id="8c7ca-197">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="8c7ca-198">Sugerencias e información adicional</span><span class="sxs-lookup"><span data-stu-id="8c7ca-198">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="8c7ca-199">Puede importar mensajes de usuarios que no están en Teams.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-199">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="8c7ca-200">**NOTA:** Los mensajes importados para usuarios que no están presentes en el espacio empresarial no se podrán buscar en los portales de cumplimiento o cliente de Teams durante la versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-200">**NOTE**: Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="8c7ca-201">Una vez `completeMigration` realizada la solicitud, no puede importar más mensajes en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-201">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="8c7ca-202">Los miembros del equipo solo se pueden agregar al nuevo equipo después de `completeMigration` que la solicitud haya devuelto una respuesta correcta.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-202">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="8c7ca-203">Limitación: los mensajes se importan a 5 RPS por canal.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-203">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="8c7ca-204">Si necesita realizar una corrección en los resultados de la migración, debe eliminar el equipo y repetir los pasos para crear el equipo y canalizar y volver a migrar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-204">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="8c7ca-205">Actualmente, las imágenes en línea son el único tipo de medios admitidos por el esquema de api de mensajes de importación.</span><span class="sxs-lookup"><span data-stu-id="8c7ca-205">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="8c7ca-206">Importar ámbito de contenido</span><span class="sxs-lookup"><span data-stu-id="8c7ca-206">Import content scope</span></span>

|<span data-ttu-id="8c7ca-207">En el ámbito</span><span class="sxs-lookup"><span data-stu-id="8c7ca-207">In-scope</span></span> | <span data-ttu-id="8c7ca-208">Actualmente fuera del ámbito</span><span class="sxs-lookup"><span data-stu-id="8c7ca-208">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="8c7ca-209">Mensajes de equipo y canal</span><span class="sxs-lookup"><span data-stu-id="8c7ca-209">Team and channel messages</span></span>|<span data-ttu-id="8c7ca-210">1:1 y mensajes de chat en grupo</span><span class="sxs-lookup"><span data-stu-id="8c7ca-210">1:1 and group chat messages</span></span>|
|<span data-ttu-id="8c7ca-211">Hora de creación del mensaje original</span><span class="sxs-lookup"><span data-stu-id="8c7ca-211">Created time of the original message</span></span>|<span data-ttu-id="8c7ca-212">Canales privados</span><span class="sxs-lookup"><span data-stu-id="8c7ca-212">Private channels</span></span>|
|<span data-ttu-id="8c7ca-213">Imágenes en línea como parte del mensaje</span><span class="sxs-lookup"><span data-stu-id="8c7ca-213">Inline images as part of the message</span></span>|<span data-ttu-id="8c7ca-214">En menciones</span><span class="sxs-lookup"><span data-stu-id="8c7ca-214">At mentions</span></span>|
|<span data-ttu-id="8c7ca-215">Vínculos a archivos existentes en SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="8c7ca-215">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="8c7ca-216">Reacciones</span><span class="sxs-lookup"><span data-stu-id="8c7ca-216">Reactions</span></span>|
|<span data-ttu-id="8c7ca-217">Mensajes con texto enriquecido</span><span class="sxs-lookup"><span data-stu-id="8c7ca-217">Messages with rich text</span></span>|<span data-ttu-id="8c7ca-218">Vídeos</span><span class="sxs-lookup"><span data-stu-id="8c7ca-218">Videos</span></span>|
|<span data-ttu-id="8c7ca-219">Cadena de respuesta de mensajes</span><span class="sxs-lookup"><span data-stu-id="8c7ca-219">Message reply chain</span></span>|<span data-ttu-id="8c7ca-220">Anuncios</span><span class="sxs-lookup"><span data-stu-id="8c7ca-220">Announcements</span></span>|
|<span data-ttu-id="8c7ca-221">Procesamiento de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="8c7ca-221">High throughput processing</span></span>|<span data-ttu-id="8c7ca-222">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="8c7ca-222">Code snippets</span></span>|
||<span data-ttu-id="8c7ca-223">Tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="8c7ca-223">Adaptive cards</span></span>|
||<span data-ttu-id="8c7ca-224">Adhesivos</span><span class="sxs-lookup"><span data-stu-id="8c7ca-224">Stickers</span></span>|
||<span data-ttu-id="8c7ca-225">Emojis</span><span class="sxs-lookup"><span data-stu-id="8c7ca-225">Emojis</span></span>|
||<span data-ttu-id="8c7ca-226">Comillas</span><span class="sxs-lookup"><span data-stu-id="8c7ca-226">Quotes</span></span>|
||<span data-ttu-id="8c7ca-227">Publicaciones cruzadas entre canales</span><span class="sxs-lookup"><span data-stu-id="8c7ca-227">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="8c7ca-228">Consulte también</span><span class="sxs-lookup"><span data-stu-id="8c7ca-228">See also</span></span>
> [!div class="nextstepaction"]
>[<span data-ttu-id="8c7ca-229">Más información sobre la integración de Microsoft Graph y Teams</span><span class="sxs-lookup"><span data-stu-id="8c7ca-229">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
