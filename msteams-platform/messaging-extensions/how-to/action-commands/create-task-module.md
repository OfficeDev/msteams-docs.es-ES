---
title: Crear y enviar el módulo de tareas
author: clearab
description: Cómo controlar la acción de invocación inicial y responder con un módulo de tarea desde un comando de extensión de mensajería de acción
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: fbe90b3a3af8dbb053fdbaf6b4cd9b96344eaf00
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075594"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="c15e2-103">Crear y enviar el módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="c15e2-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="c15e2-104">Puede crear el módulo de tareas mediante una tarjeta adaptable o una vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="c15e2-104">You can create the task module using an Adaptive Card or an embedded web view.</span></span> <span data-ttu-id="c15e2-105">Para crear un módulo de tareas, debe realizar el proceso denominado solicitud de invocación inicial.</span><span class="sxs-lookup"><span data-stu-id="c15e2-105">To create a task module, you must perform the process called the initial invoke request.</span></span> <span data-ttu-id="c15e2-106">Este documento trata la solicitud de invocación inicial, las propiedades de actividad de carga cuando se invoca un módulo de tareas desde el chat 1:1, el chat de grupo, el canal (nueva publicación), el canal (respuesta al subproceso) y el cuadro de comandos.</span><span class="sxs-lookup"><span data-stu-id="c15e2-106">This document covers the initial invoke request, payload activity properties when a task module is invoked from 1:1 chat, group chat, channel (new post), channel (reply to thread), and command box.</span></span> 
> [!NOTE]
> <span data-ttu-id="c15e2-107">Si no va a rellenar el módulo de tareas con parámetros definidos en el manifiesto de la aplicación, debe crear el módulo de tareas para los usuarios con una tarjeta adaptable o una vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="c15e2-107">If you are not populating the task module with parameters defined in the app manifest, you must create the task module for users with either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="c15e2-108">La solicitud de invocación inicial</span><span class="sxs-lookup"><span data-stu-id="c15e2-108">The initial invoke request</span></span>

<span data-ttu-id="c15e2-109">En el proceso de la solicitud de invocación inicial, el servicio recibe un objeto de tipo y debe responder con un objeto que contenga una tarjeta adaptable o una dirección URL a la vista `Activity` `composeExtension/fetchTask` web `task` incrustada.</span><span class="sxs-lookup"><span data-stu-id="c15e2-109">In the process of the initial invoke request, your service receives an `Activity` object of type `composeExtension/fetchTask`, and you must respond with a `task` object containing either an Adaptive Card or a URL to the embedded web view.</span></span> <span data-ttu-id="c15e2-110">Junto con las propiedades de actividad del bot estándar, la carga inicial de invocación contiene los siguientes metadatos de solicitud:</span><span class="sxs-lookup"><span data-stu-id="c15e2-110">Along with the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="c15e2-111">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="c15e2-111">Property name</span></span>|<span data-ttu-id="c15e2-112">Objetivo</span><span class="sxs-lookup"><span data-stu-id="c15e2-112">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="c15e2-113">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-113">Type of request.</span></span> <span data-ttu-id="c15e2-114">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-114">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="c15e2-115">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="c15e2-115">Type of command that is issued to your service.</span></span> <span data-ttu-id="c15e2-116">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-116">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="c15e2-117">Id. del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-117">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="c15e2-118">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-118">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="c15e2-119">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-119">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="c15e2-120">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c15e2-120">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="c15e2-121">Identificador de canal (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="c15e2-121">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="c15e2-122">Id. de equipo (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="c15e2-122">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="c15e2-123">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="c15e2-123">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="c15e2-124">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="c15e2-124">The context that triggered the event.</span></span> <span data-ttu-id="c15e2-125">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-125">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="c15e2-126">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="c15e2-126">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="c15e2-127">Debe ser `default` , `contrast` o `dark` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-127">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="c15e2-128">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-128">Example</span></span>

<span data-ttu-id="c15e2-129">El código de la solicitud de invocación inicial se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c15e2-129">The code for the initial invoke request is given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a><span data-ttu-id="c15e2-130">Propiedades de actividad de carga cuando se invoca un módulo de tareas desde el chat 1:1</span><span class="sxs-lookup"><span data-stu-id="c15e2-130">Payload activity properties when a task module is invoked from 1:1 chat</span></span> 

<span data-ttu-id="c15e2-131">Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde el chat 1:1 se enumeran de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c15e2-131">The payload activity properties when a task module is invoked from 1:1 chat are listed as follows:</span></span>

|<span data-ttu-id="c15e2-132">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="c15e2-132">Property name</span></span>|<span data-ttu-id="c15e2-133">Objetivo</span><span class="sxs-lookup"><span data-stu-id="c15e2-133">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="c15e2-134">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-134">Type of request.</span></span> <span data-ttu-id="c15e2-135">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-135">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="c15e2-136">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="c15e2-136">Type of command that is issued to your service.</span></span> <span data-ttu-id="c15e2-137">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-137">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="c15e2-138">Id. del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-138">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="c15e2-139">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-139">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="c15e2-140">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-140">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="c15e2-141">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c15e2-141">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="c15e2-142">Nombre de origen desde el que se invoca el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="c15e2-142">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="c15e2-143">Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta.</span><span class="sxs-lookup"><span data-stu-id="c15e2-143">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="c15e2-144">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="c15e2-144">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="c15e2-145">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="c15e2-145">The context that triggered the event.</span></span> <span data-ttu-id="c15e2-146">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-146">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="c15e2-147">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="c15e2-147">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="c15e2-148">Debe ser `default` , `contrast` o `dark` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-148">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="c15e2-149">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-149">Example</span></span>

<span data-ttu-id="c15e2-150">Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde el chat 1:1 se dan en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c15e2-150">The payload activity properties when a task module is invoked from 1:1 chat are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```
## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a><span data-ttu-id="c15e2-151">Propiedades de actividad de carga cuando se invoca un módulo de tarea desde un chat de grupo</span><span class="sxs-lookup"><span data-stu-id="c15e2-151">Payload activity properties when a task module is invoked from a group chat</span></span> 

<span data-ttu-id="c15e2-152">Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde un chat de grupo se enumeran de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c15e2-152">The payload activity properties when a task module is invoked from a group chat are listed as follows:</span></span>

|<span data-ttu-id="c15e2-153">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="c15e2-153">Property name</span></span>|<span data-ttu-id="c15e2-154">Objetivo</span><span class="sxs-lookup"><span data-stu-id="c15e2-154">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="c15e2-155">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-155">Type of request.</span></span> <span data-ttu-id="c15e2-156">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-156">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="c15e2-157">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="c15e2-157">Type of command that is issued to your service.</span></span> <span data-ttu-id="c15e2-158">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-158">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="c15e2-159">Id. del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-159">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="c15e2-160">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-160">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="c15e2-161">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-161">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="c15e2-162">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c15e2-162">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="c15e2-163">Nombre de origen desde el que se invoca el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="c15e2-163">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="c15e2-164">Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta.</span><span class="sxs-lookup"><span data-stu-id="c15e2-164">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="c15e2-165">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="c15e2-165">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="c15e2-166">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="c15e2-166">The context that triggered the event.</span></span> <span data-ttu-id="c15e2-167">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-167">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="c15e2-168">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="c15e2-168">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="c15e2-169">Debe ser `default` , `contrast` o `dark` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-169">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="c15e2-170">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-170">Example</span></span>

<span data-ttu-id="c15e2-171">Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde un chat de grupo se dan en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c15e2-171">The payload activity properties when a task module is invoked from a group chat are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bf72031f-a17e-f99c-48dc-5c0714950d87",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "groupChat",
    "id": "19:d77be72390a1416e9644261e9064fa00@thread.skype",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "213167a1e3b6428b93e186ea5407c759",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a><span data-ttu-id="c15e2-172">Propiedades de actividad de carga cuando se invoca un módulo de tarea desde un canal (nueva publicación)</span><span class="sxs-lookup"><span data-stu-id="c15e2-172">Payload activity properties when a task module is invoked from a channel (new post)</span></span> 

<span data-ttu-id="c15e2-173">Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde un canal (nueva publicación) se enumeran de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c15e2-173">The payload activity properties when a task module is invoked from a channel (new post) are listed as follows:</span></span>

|<span data-ttu-id="c15e2-174">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="c15e2-174">Property name</span></span>|<span data-ttu-id="c15e2-175">Objetivo</span><span class="sxs-lookup"><span data-stu-id="c15e2-175">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="c15e2-176">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-176">Type of request.</span></span> <span data-ttu-id="c15e2-177">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-177">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="c15e2-178">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="c15e2-178">Type of command that is issued to your service.</span></span> <span data-ttu-id="c15e2-179">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-179">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="c15e2-180">Id. del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-180">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="c15e2-181">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-181">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="c15e2-182">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-182">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="c15e2-183">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c15e2-183">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="c15e2-184">Identificador de canal (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="c15e2-184">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="c15e2-185">Id. de equipo (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="c15e2-185">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="c15e2-186">Nombre de origen desde el que se invoca el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="c15e2-186">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="c15e2-187">Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta.</span><span class="sxs-lookup"><span data-stu-id="c15e2-187">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="c15e2-188">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="c15e2-188">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="c15e2-189">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="c15e2-189">The context that triggered the event.</span></span> <span data-ttu-id="c15e2-190">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-190">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="c15e2-191">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="c15e2-191">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="c15e2-192">Debe ser `default` , `contrast` o `dark` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-192">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="c15e2-193">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-193">Example</span></span>

<span data-ttu-id="c15e2-194">Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde un canal (nueva publicación) se dan en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c15e2-194">The payload activity properties when a task module is invoked from a channel (new post) are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:a5fbb109-c989-c449-ee83-71ac99919d4b",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "5336640edc7748b28ce2df43f5b45963",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a><span data-ttu-id="c15e2-195">Propiedades de actividad de carga cuando se invoca un módulo de tareas desde un canal (responder al subproceso)</span><span class="sxs-lookup"><span data-stu-id="c15e2-195">Payload activity properties when a task module is invoked from a channel (reply to thread)</span></span> 

<span data-ttu-id="c15e2-196">Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde un canal (respuesta al subproceso) se enumeran de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c15e2-196">The payload activity properties when a task module is invoked from a channel (reply to thread) are listed as follows:</span></span>

|<span data-ttu-id="c15e2-197">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="c15e2-197">Property name</span></span>|<span data-ttu-id="c15e2-198">Objetivo</span><span class="sxs-lookup"><span data-stu-id="c15e2-198">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="c15e2-199">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-199">Type of request.</span></span> <span data-ttu-id="c15e2-200">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-200">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="c15e2-201">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="c15e2-201">Type of command that is issued to your service.</span></span> <span data-ttu-id="c15e2-202">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-202">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="c15e2-203">Id. del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-203">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="c15e2-204">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-204">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="c15e2-205">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-205">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="c15e2-206">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c15e2-206">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="c15e2-207">Identificador de canal (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="c15e2-207">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="c15e2-208">Id. de equipo (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="c15e2-208">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="c15e2-209">Nombre de origen desde el que se invoca el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="c15e2-209">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="c15e2-210">Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta.</span><span class="sxs-lookup"><span data-stu-id="c15e2-210">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="c15e2-211">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="c15e2-211">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="c15e2-212">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="c15e2-212">The context that triggered the event.</span></span> <span data-ttu-id="c15e2-213">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-213">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="c15e2-214">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="c15e2-214">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="c15e2-215">Debe ser `default` , `contrast` o `dark` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-215">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="c15e2-216">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-216">Example</span></span>

<span data-ttu-id="c15e2-217">Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde un canal (respuesta al subproceso) se dan en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c15e2-217">The payload activity properties when a task module is invoked from a channel (reply to thread) are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:19ccc884-c792-35ef-2f40-d0ff43dcca71",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype;messageid=1611060744833",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "message",
    "requestId": "7f7d22efe5414818becebcec649a7912",
    "messagePayload": {
      "linkToMessage": "https://teams.microsoft.com/l/message/19:6decf54d86d945e4b3924b63a9161a78@thread.skype/1611060744833",
      "id": "1611060744833",
      "replyToId": null,
      "createdDateTime": "2021-01-19T12:52:24.833Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "<div><div><at id=\"0\">Testing outgoing Webhook-Nikitha</at> - Hi</div>\n</div>"
      },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc",
          "displayName": "Olo Brockhouse"
        },
        "application": null
      },
      "reactions": [],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Testing outgoing Webhook-Nikitha",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": null,
            "application": {
              "applicationIdentityType": "webhook",
              "id": "b8c1c68c-e290-4bdd-81c3-266f310751dc",
              "displayName": "Testing outgoing Webhook-Nikitha"
            }
          }
        }
      ],
      "attachments": []
    },
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a><span data-ttu-id="c15e2-218">Propiedades de actividad de carga cuando se invoca un módulo de tareas desde un cuadro de comandos</span><span class="sxs-lookup"><span data-stu-id="c15e2-218">Payload activity properties when a task module is invoked from a command box</span></span> 

<span data-ttu-id="c15e2-219">Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde un cuadro de comandos se enumeran de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c15e2-219">The payload activity properties when a task module is invoked from a command box are listed as follows:</span></span>

|<span data-ttu-id="c15e2-220">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="c15e2-220">Property name</span></span>|<span data-ttu-id="c15e2-221">Objetivo</span><span class="sxs-lookup"><span data-stu-id="c15e2-221">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="c15e2-222">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-222">Type of request.</span></span> <span data-ttu-id="c15e2-223">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-223">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="c15e2-224">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="c15e2-224">Type of command that is issued to your service.</span></span> <span data-ttu-id="c15e2-225">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-225">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="c15e2-226">Id. del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-226">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="c15e2-227">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-227">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="c15e2-228">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c15e2-228">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="c15e2-229">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c15e2-229">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="c15e2-230">Nombre de origen desde el que se invoca el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="c15e2-230">The source name from where task module is invoked.</span></span> |
|`value.commandId` | <span data-ttu-id="c15e2-231">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="c15e2-231">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="c15e2-232">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="c15e2-232">The context that triggered the event.</span></span> <span data-ttu-id="c15e2-233">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-233">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="c15e2-234">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="c15e2-234">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="c15e2-235">Debe ser `default` , `contrast` o `dark` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-235">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="c15e2-236">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-236">Example</span></span>

<span data-ttu-id="c15e2-237">Las propiedades de actividad de carga cuando se invoca un módulo de tareas desde un cuadro de comandos se dan en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c15e2-237">The payload activity properties when a task module is invoked from a command box are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:172560f1-95f9-3189-edb2-b7612cd1a3cd",
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "compose",
    "requestId": "d2ce690cdc2b4920a538e75882610a30",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

### <a name="example"></a><span data-ttu-id="c15e2-238">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-238">Example</span></span> 

<span data-ttu-id="c15e2-239">La siguiente sección de código es un ejemplo de `fetchTask` solicitud:</span><span class="sxs-lookup"><span data-stu-id="c15e2-239">The following code section is an example of `fetchTask` request:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="c15e2-240">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c15e2-240">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="c15e2-241">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="c15e2-241">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[<span data-ttu-id="c15e2-242">JSON</span><span class="sxs-lookup"><span data-stu-id="c15e2-242">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="c15e2-243">Solicitud de invocación inicial de un mensaje</span><span class="sxs-lookup"><span data-stu-id="c15e2-243">Initial invoke request from a message</span></span>

<span data-ttu-id="c15e2-244">Cuando se invoca el bot desde un mensaje, el objeto de la solicitud de invocación inicial debe contener los detalles del mensaje desde el que se invoca la extensión `value` de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c15e2-244">When your bot is invoked from a message,  the `value` object in the initial invoke request must contain the details of the message that your messaging extension is invoked from.</span></span> <span data-ttu-id="c15e2-245">Las matrices y son opcionales y no están presentes si no hay ninguna reacción o `reactions` `mentions` menciones en el mensaje original.</span><span class="sxs-lookup"><span data-stu-id="c15e2-245">The `reactions` and `mentions` arrays are optional, and they are not present if there are no reactions or mentions in the original message.</span></span> <span data-ttu-id="c15e2-246">La siguiente sección es un ejemplo del `value` objeto:</span><span class="sxs-lookup"><span data-stu-id="c15e2-246">The following section is an example of the `value` object:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="c15e2-247">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c15e2-247">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="c15e2-248">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="c15e2-248">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[<span data-ttu-id="c15e2-249">JSON</span><span class="sxs-lookup"><span data-stu-id="c15e2-249">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="c15e2-250">Responder a fetchTask</span><span class="sxs-lookup"><span data-stu-id="c15e2-250">Respond to the fetchTask</span></span>

<span data-ttu-id="c15e2-251">Responda a la solicitud de invocación con un objeto que contenga un objeto con la tarjeta adaptable o la dirección URL web, o `task` un mensaje de cadena `taskInfo` simple.</span><span class="sxs-lookup"><span data-stu-id="c15e2-251">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the Adaptive Card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="c15e2-252">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="c15e2-252">Property name</span></span>|<span data-ttu-id="c15e2-253">Objetivo</span><span class="sxs-lookup"><span data-stu-id="c15e2-253">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="c15e2-254">Puede ser para `continue` presentar un formulario o para un elemento emergente `message` simple.</span><span class="sxs-lookup"><span data-stu-id="c15e2-254">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="c15e2-255">Un `taskInfo` objeto para un formulario o un `string` para un mensaje.</span><span class="sxs-lookup"><span data-stu-id="c15e2-255">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="c15e2-256">El esquema del objeto taskInfo es:</span><span class="sxs-lookup"><span data-stu-id="c15e2-256">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="c15e2-257">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="c15e2-257">Property name</span></span>|<span data-ttu-id="c15e2-258">Objetivo</span><span class="sxs-lookup"><span data-stu-id="c15e2-258">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="c15e2-259">El título del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="c15e2-259">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="c15e2-260">Debe ser un entero (en píxeles) o `small` , `medium` , `large` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-260">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="c15e2-261">Debe ser un entero (en píxeles) o `small` , `medium` , `large` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-261">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="c15e2-262">La tarjeta adaptable que define el formulario (si se usa uno).</span><span class="sxs-lookup"><span data-stu-id="c15e2-262">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="c15e2-263">Dirección URL que se abrirá dentro del módulo de tareas como una vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="c15e2-263">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="c15e2-264">Si un cliente no admite la característica del módulo de tareas, esta dirección URL se abre en una pestaña del explorador.</span><span class="sxs-lookup"><span data-stu-id="c15e2-264">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a><span data-ttu-id="c15e2-265">Responder a fetchTask con una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="c15e2-265">Respond to the fetchTask with an Adaptive Card</span></span>

<span data-ttu-id="c15e2-266">Al usar una tarjeta adaptable, debe responder con un `task` objeto con el objeto que contiene una tarjeta `value` adaptable.</span><span class="sxs-lookup"><span data-stu-id="c15e2-266">When using an adaptive card, you must respond with a `task` object with the `value` object containing an Adaptive Card.</span></span>

#### <a name="example"></a><span data-ttu-id="c15e2-267">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-267">Example</span></span>

<span data-ttu-id="c15e2-268">La siguiente sección de código es un ejemplo para `fetchTask` responder con una tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="c15e2-268">The following code section is an example to `fetchTask` response with an adaptive card:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="c15e2-269">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c15e2-269">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="c15e2-270">En este ejemplo se usa [el paquete AdaptiveCards NuGet](https://www.nuget.org/packages/AdaptiveCards) además del SDK de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c15e2-270">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="c15e2-271">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="c15e2-271">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[<span data-ttu-id="c15e2-272">JSON</span><span class="sxs-lookup"><span data-stu-id="c15e2-272">JSON</span></span>](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="create-a-task-module-with-an-embedded-web-view"></a><span data-ttu-id="c15e2-273">Crear un módulo de tareas con una vista web incrustada</span><span class="sxs-lookup"><span data-stu-id="c15e2-273">Create a task module with an embedded web view</span></span>

<span data-ttu-id="c15e2-274">Al usar una vista web incrustada, debe responder con un objeto con el objeto que contiene la dirección URL al formulario `task` `value` web que desea cargar.</span><span class="sxs-lookup"><span data-stu-id="c15e2-274">When using an embedded web view, you must respond with a `task` object with the `value` object containing the URL to the web form that you want to load.</span></span> <span data-ttu-id="c15e2-275">Los dominios de cualquier dirección URL que quieras cargar deben incluirse en la `validDomains` matriz en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c15e2-275">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="c15e2-276">Para obtener más información sobre cómo crear la vista web incrustada, vea la documentación [del módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md).</span><span class="sxs-lookup"><span data-stu-id="c15e2-276">For more information on building your embedded web view, see the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md).</span></span> 

# <a name="cnet"></a>[<span data-ttu-id="c15e2-277">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="c15e2-277">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="c15e2-278">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="c15e2-278">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[<span data-ttu-id="c15e2-279">JSON</span><span class="sxs-lookup"><span data-stu-id="c15e2-279">JSON</span></span>](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="c15e2-280">Solicitud para instalar el bot de conversación</span><span class="sxs-lookup"><span data-stu-id="c15e2-280">Request to install your conversational bot</span></span>

<span data-ttu-id="c15e2-281">Si la aplicación contiene un bot de conversación, instala el bot en la conversación y, a continuación, carga el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="c15e2-281">If the app contains a conversational bot, install the bot in the conversation and then load the task module.</span></span> <span data-ttu-id="c15e2-282">El bot es útil para obtener contexto adicional para el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="c15e2-282">The bot is useful to get additional context for the task module.</span></span> <span data-ttu-id="c15e2-283">Un ejemplo de este escenario es capturar la lista para rellenar un control de selector de personas o la lista de canales de un equipo.</span><span class="sxs-lookup"><span data-stu-id="c15e2-283">An example for this scenario is to fetch the roster to populate a people picker control or the list of channels in a team.</span></span>

<span data-ttu-id="c15e2-284">Cuando la extensión de mensajería recibe la invocación, compruebe si `composeExtension/fetchTask` el bot está instalado en el contexto actual para facilitar el flujo.</span><span class="sxs-lookup"><span data-stu-id="c15e2-284">When the messaging extension receives the `composeExtension/fetchTask` invoke, check if the bot is installed in the current context to facilitate the flow.</span></span> <span data-ttu-id="c15e2-285">Por ejemplo, compruebe el flujo con una llamada de lista get.</span><span class="sxs-lookup"><span data-stu-id="c15e2-285">For example, check the flow with a get roster call.</span></span> <span data-ttu-id="c15e2-286">Si el bot no está instalado, devuelve una tarjeta adaptable con una acción que solicita al usuario que instale el bot.</span><span class="sxs-lookup"><span data-stu-id="c15e2-286">If the bot is not installed, return an Adaptive Card with an action that requests the user to install the bot.</span></span> <span data-ttu-id="c15e2-287">El usuario debe tener permiso para instalar las aplicaciones en esa ubicación para su comprobación.</span><span class="sxs-lookup"><span data-stu-id="c15e2-287">The user must have the permission to install the apps in that location for checking.</span></span> <span data-ttu-id="c15e2-288">Si la instalación de la aplicación no se realiza correctamente, el usuario recibe un mensaje para ponerse en contacto con el administrador.</span><span class="sxs-lookup"><span data-stu-id="c15e2-288">If the app installation is unsuccessful, the user receives a message to contact the administrator.</span></span>

#### <a name="example"></a><span data-ttu-id="c15e2-289">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-289">Example</span></span> 

<span data-ttu-id="c15e2-290">La siguiente sección de código es un ejemplo de la respuesta:</span><span class="sxs-lookup"><span data-stu-id="c15e2-290">The following code section is an example of the response:</span></span>

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

<span data-ttu-id="c15e2-291">Después de la instalación del bot de conversación, recibe otro mensaje de invocación con `name = composeExtension/submitAction` , y `value.data.msteams.justInTimeInstall = true` .</span><span class="sxs-lookup"><span data-stu-id="c15e2-291">After the installation of conversational bot, it receives another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

#### <a name="example"></a><span data-ttu-id="c15e2-292">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-292">Example</span></span> 

<span data-ttu-id="c15e2-293">La siguiente sección de código es un ejemplo de la respuesta de tarea a la invocación:</span><span class="sxs-lookup"><span data-stu-id="c15e2-293">The following code section is an example of the task response to the invoke:</span></span>

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

<span data-ttu-id="c15e2-294">La respuesta de tarea a la invocación debe ser similar a la del bot instalado.</span><span class="sxs-lookup"><span data-stu-id="c15e2-294">The task response to the invoke must be similar to that of the installed bot.</span></span>

#### <a name="example"></a><span data-ttu-id="c15e2-295">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-295">Example</span></span> 

<span data-ttu-id="c15e2-296">La siguiente sección de código es un ejemplo de instalación a tiempo justo de la aplicación con tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="c15e2-296">The following code section is an example of just-in time installation of app with Adaptive card:</span></span> 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="code-sample"></a><span data-ttu-id="c15e2-297">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="c15e2-297">Code sample</span></span>

| <span data-ttu-id="c15e2-298">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c15e2-298">Sample Name</span></span>           | <span data-ttu-id="c15e2-299">Description</span><span class="sxs-lookup"><span data-stu-id="c15e2-299">Description</span></span> | <span data-ttu-id="c15e2-300">.NET</span><span class="sxs-lookup"><span data-stu-id="c15e2-300">.NET</span></span>    | <span data-ttu-id="c15e2-301">Node.js</span><span class="sxs-lookup"><span data-stu-id="c15e2-301">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="c15e2-302">Acción de extensión de mensajería de Teams</span><span class="sxs-lookup"><span data-stu-id="c15e2-302">Teams messaging extension action</span></span>| <span data-ttu-id="c15e2-303">Describe cómo definir comandos de acción, crear módulo de tareas y responder a la acción de envío del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="c15e2-303">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="c15e2-304">View</span><span class="sxs-lookup"><span data-stu-id="c15e2-304">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="c15e2-305">View</span><span class="sxs-lookup"><span data-stu-id="c15e2-305">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="c15e2-306">Búsqueda de extensión de mensajería de Teams</span><span class="sxs-lookup"><span data-stu-id="c15e2-306">Teams messaging extension search</span></span>   |  <span data-ttu-id="c15e2-307">Describe cómo definir comandos de búsqueda y responder a las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="c15e2-307">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="c15e2-308">View</span><span class="sxs-lookup"><span data-stu-id="c15e2-308">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="c15e2-309">View</span><span class="sxs-lookup"><span data-stu-id="c15e2-309">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a><span data-ttu-id="c15e2-310">Consulte también</span><span class="sxs-lookup"><span data-stu-id="c15e2-310">See also</span></span>

[<span data-ttu-id="c15e2-311">Definir comandos de acción</span><span class="sxs-lookup"><span data-stu-id="c15e2-311">Define action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)


## <a name="next-step"></a><span data-ttu-id="c15e2-312">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="c15e2-312">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="c15e2-313">Responder al comando action</span><span class="sxs-lookup"><span data-stu-id="c15e2-313">Respond to action command</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

