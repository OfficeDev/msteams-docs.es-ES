---
title: Crear y enviar el módulo de tareas
author: clearab
description: Cómo controlar la acción de invocación inicial y responder con un módulo de tarea desde un comando de extensión de mensajería de acciones
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 58fb7e1ff5690b33c2e23f68529f05869afa9016
ms.sourcegitcommit: ce74f821660b1258c72b3c3f71c1cf177e7e92ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2021
ms.locfileid: "50072878"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="69481-103">Crear y enviar el módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="69481-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="69481-104">Si no va a rellenar el módulo de tareas con parámetros definidos en el manifiesto de la aplicación, debe crear el módulo de tareas para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="69481-104">If you are not populating the task module with parameters defined in the app manifest, you must create the task module for users.</span></span> <span data-ttu-id="69481-105">Usa una tarjeta adaptable o una vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="69481-105">Use either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="69481-106">La solicitud de invocación inicial</span><span class="sxs-lookup"><span data-stu-id="69481-106">The initial invoke request</span></span>

<span data-ttu-id="69481-107">Con este método, el servicio recibirá un objeto de tipo y debe responder con un objeto que contenga la tarjeta adaptable o una dirección URL a la `Activity` `composeExtension/fetchTask` vista web `task` incrustada.</span><span class="sxs-lookup"><span data-stu-id="69481-107">Using this method your service will receive an `Activity` object of type `composeExtension/fetchTask`, and you must respond with a `task` object containing either the adaptive card or a URL to the embedded web view.</span></span> <span data-ttu-id="69481-108">Junto con las propiedades de actividad de bot estándar, la carga inicial de invocación contiene los siguientes metadatos de solicitud:</span><span class="sxs-lookup"><span data-stu-id="69481-108">Along with the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="69481-109">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="69481-109">Property name</span></span>|<span data-ttu-id="69481-110">Finalidad</span><span class="sxs-lookup"><span data-stu-id="69481-110">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="69481-111">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-111">Type of request.</span></span> <span data-ttu-id="69481-112">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="69481-112">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="69481-113">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="69481-113">Type of command that is issued to your service.</span></span> <span data-ttu-id="69481-114">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="69481-114">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="69481-115">Identificador del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-115">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="69481-116">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-116">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="69481-117">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-117">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="69481-118">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69481-118">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="69481-119">Id. de canal (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="69481-119">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="69481-120">Identificador de equipo (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="69481-120">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="69481-121">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="69481-121">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="69481-122">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="69481-122">The context that triggered the event.</span></span> <span data-ttu-id="69481-123">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="69481-123">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="69481-124">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="69481-124">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="69481-125">Debe ser `default` o `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="69481-125">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-11-chat-are-listed-in-the-following-section"></a><span data-ttu-id="69481-126">Las propiedades de actividad de carga cuando se invoca un módulo de tarea desde el chat 1:1 se enumeran en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="69481-126">Payload activity properties when invoked a task module from 1:1 chat are listed in the following section:</span></span>

|<span data-ttu-id="69481-127">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="69481-127">Property name</span></span>|<span data-ttu-id="69481-128">Finalidad</span><span class="sxs-lookup"><span data-stu-id="69481-128">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="69481-129">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-129">Type of request.</span></span> <span data-ttu-id="69481-130">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="69481-130">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="69481-131">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="69481-131">Type of command that is issued to your service.</span></span> <span data-ttu-id="69481-132">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="69481-132">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="69481-133">Identificador del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-133">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="69481-134">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-134">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="69481-135">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-135">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="69481-136">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69481-136">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="69481-137">Nombre de origen desde el que se invoca el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="69481-137">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="69481-138">Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta.</span><span class="sxs-lookup"><span data-stu-id="69481-138">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="69481-139">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="69481-139">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="69481-140">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="69481-140">The context that triggered the event.</span></span> <span data-ttu-id="69481-141">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="69481-141">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="69481-142">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="69481-142">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="69481-143">Debe ser `default` o `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="69481-143">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-group-chat-are-listed-in-the-following-section"></a><span data-ttu-id="69481-144">Las propiedades de actividad de carga cuando se invoca un módulo de tarea desde un chat de grupo se enumeran en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="69481-144">Payload activity properties when invoked a task module from a group chat are listed in the following section:</span></span>

|<span data-ttu-id="69481-145">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="69481-145">Property name</span></span>|<span data-ttu-id="69481-146">Finalidad</span><span class="sxs-lookup"><span data-stu-id="69481-146">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="69481-147">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-147">Type of request.</span></span> <span data-ttu-id="69481-148">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="69481-148">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="69481-149">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="69481-149">Type of command that is issued to your service.</span></span> <span data-ttu-id="69481-150">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="69481-150">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="69481-151">Identificador del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-151">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="69481-152">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-152">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="69481-153">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-153">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="69481-154">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69481-154">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="69481-155">Nombre de origen desde el que se invoca el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="69481-155">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="69481-156">Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta.</span><span class="sxs-lookup"><span data-stu-id="69481-156">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="69481-157">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="69481-157">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="69481-158">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="69481-158">The context that triggered the event.</span></span> <span data-ttu-id="69481-159">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="69481-159">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="69481-160">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="69481-160">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="69481-161">Debe ser `default` o `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="69481-161">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-new-post-are-listed-in-the-following-section"></a><span data-ttu-id="69481-162">Las propiedades de actividad de carga cuando se invoca un módulo de tarea desde un canal (nueva publicación) se enumeran en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="69481-162">Payload activity properties when invoked a task module from a channel (new post) are listed in the following section:</span></span>

|<span data-ttu-id="69481-163">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="69481-163">Property name</span></span>|<span data-ttu-id="69481-164">Finalidad</span><span class="sxs-lookup"><span data-stu-id="69481-164">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="69481-165">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-165">Type of request.</span></span> <span data-ttu-id="69481-166">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="69481-166">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="69481-167">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="69481-167">Type of command that is issued to your service.</span></span> <span data-ttu-id="69481-168">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="69481-168">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="69481-169">Identificador del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-169">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="69481-170">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-170">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="69481-171">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-171">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="69481-172">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69481-172">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="69481-173">Id. de canal (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="69481-173">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="69481-174">Identificador de equipo (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="69481-174">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="69481-175">Nombre de origen desde el que se invoca el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="69481-175">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="69481-176">Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta.</span><span class="sxs-lookup"><span data-stu-id="69481-176">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="69481-177">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="69481-177">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="69481-178">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="69481-178">The context that triggered the event.</span></span> <span data-ttu-id="69481-179">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="69481-179">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="69481-180">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="69481-180">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="69481-181">Debe ser `default` o `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="69481-181">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-reply-to-thread-are-listed-in-the-following-section"></a><span data-ttu-id="69481-182">Las propiedades de actividad de carga cuando se invoca un módulo de tarea desde un canal (responder a subproceso) se enumeran en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="69481-182">Payload activity properties when invoked a task module from a channel (reply to thread) are listed in the following section:</span></span>

|<span data-ttu-id="69481-183">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="69481-183">Property name</span></span>|<span data-ttu-id="69481-184">Finalidad</span><span class="sxs-lookup"><span data-stu-id="69481-184">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="69481-185">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-185">Type of request.</span></span> <span data-ttu-id="69481-186">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="69481-186">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="69481-187">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="69481-187">Type of command that is issued to your service.</span></span> <span data-ttu-id="69481-188">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="69481-188">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="69481-189">Identificador del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-189">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="69481-190">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-190">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="69481-191">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-191">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="69481-192">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69481-192">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="69481-193">Id. de canal (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="69481-193">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="69481-194">Identificador de equipo (si la solicitud se realizó en un canal).</span><span class="sxs-lookup"><span data-stu-id="69481-194">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="69481-195">Nombre de origen desde el que se invoca el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="69481-195">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="69481-196">Obtiene o establece el identificador del mensaje al que este mensaje es una respuesta.</span><span class="sxs-lookup"><span data-stu-id="69481-196">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="69481-197">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="69481-197">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="69481-198">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="69481-198">The context that triggered the event.</span></span> <span data-ttu-id="69481-199">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="69481-199">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="69481-200">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="69481-200">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="69481-201">Debe ser `default` o `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="69481-201">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-command-box-are-listed-in-the-following-section"></a><span data-ttu-id="69481-202">Las propiedades de actividad de carga cuando se invoca un módulo de tarea desde un cuadro de comando se enumeran en la siguiente sección:</span><span class="sxs-lookup"><span data-stu-id="69481-202">Payload activity properties when invoked a task module from a command box are listed in the following section:</span></span>

|<span data-ttu-id="69481-203">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="69481-203">Property name</span></span>|<span data-ttu-id="69481-204">Finalidad</span><span class="sxs-lookup"><span data-stu-id="69481-204">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="69481-205">Tipo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-205">Type of request.</span></span> <span data-ttu-id="69481-206">Debe ser `invoke` .</span><span class="sxs-lookup"><span data-stu-id="69481-206">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="69481-207">Tipo de comando que se emite al servicio.</span><span class="sxs-lookup"><span data-stu-id="69481-207">Type of command that is issued to your service.</span></span> <span data-ttu-id="69481-208">Debe ser `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="69481-208">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="69481-209">Identificador del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-209">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="69481-210">Nombre del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-210">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="69481-211">Identificador de objeto de Azure Active Directory del usuario que envió la solicitud.</span><span class="sxs-lookup"><span data-stu-id="69481-211">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="69481-212">Identificador del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69481-212">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="69481-213">Nombre de origen desde el que se invoca el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="69481-213">The source name from where task module is invoked.</span></span> |
|`value.commandId` | <span data-ttu-id="69481-214">Contiene el identificador del comando que se invocó.</span><span class="sxs-lookup"><span data-stu-id="69481-214">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="69481-215">Contexto que desencadenó el evento.</span><span class="sxs-lookup"><span data-stu-id="69481-215">The context that triggered the event.</span></span> <span data-ttu-id="69481-216">Debe ser `compose` .</span><span class="sxs-lookup"><span data-stu-id="69481-216">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="69481-217">El tema de cliente del usuario, útil para el formato de vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="69481-217">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="69481-218">Debe ser `default` o `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="69481-218">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example-fetchtask-request"></a><span data-ttu-id="69481-219">Ejemplo de solicitud fetchTask</span><span class="sxs-lookup"><span data-stu-id="69481-219">Example fetchTask request</span></span>

# <a name="cnet"></a>[<span data-ttu-id="69481-220">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="69481-220">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="69481-221">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="69481-221">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[<span data-ttu-id="69481-222">JSON</span><span class="sxs-lookup"><span data-stu-id="69481-222">JSON</span></span>](#tab/json)

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

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="69481-223">Solicitud de invocación inicial de un mensaje</span><span class="sxs-lookup"><span data-stu-id="69481-223">Initial invoke request from a message</span></span>

<span data-ttu-id="69481-224">Cuando se invoca el bot desde un mensaje en lugar del área de redacción o la barra de comandos, el objeto de la solicitud inicial debe contener los detalles del mensaje desde el que se invoca la extensión `value` de mensajería.</span><span class="sxs-lookup"><span data-stu-id="69481-224">When your bot is invoked from a message rather than the compose area or the command bar, the `value` object in the initial request must contain the details of the message your messaging extension is invoked from.</span></span> <span data-ttu-id="69481-225">Vea la sección siguiente para ver el ejemplo de este objeto.</span><span class="sxs-lookup"><span data-stu-id="69481-225">See the following section  for the example of this object .</span></span> <span data-ttu-id="69481-226">Las matrices y son opcionales y no están presentes si no hay ninguna reacción o `reactions` `mentions` mención en el mensaje original.</span><span class="sxs-lookup"><span data-stu-id="69481-226">The `reactions` and `mentions` arrays are optional, and they are not present if there are no reactions or mentions in the original message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="69481-227">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="69481-227">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="69481-228">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="69481-228">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[<span data-ttu-id="69481-229">JSON</span><span class="sxs-lookup"><span data-stu-id="69481-229">JSON</span></span>](#tab/json)

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

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="69481-230">Responder a fetchTask</span><span class="sxs-lookup"><span data-stu-id="69481-230">Respond to the fetchTask</span></span>

<span data-ttu-id="69481-231">Responda a la solicitud de invocación con un objeto que contenga un objeto con la tarjeta adaptable o la dirección URL web, o `task` un mensaje de cadena `taskInfo` simple.</span><span class="sxs-lookup"><span data-stu-id="69481-231">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the adaptive card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="69481-232">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="69481-232">Property name</span></span>|<span data-ttu-id="69481-233">Finalidad</span><span class="sxs-lookup"><span data-stu-id="69481-233">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="69481-234">Puede ser `continue` para presentar un formulario o para un elemento emergente `message` simple.</span><span class="sxs-lookup"><span data-stu-id="69481-234">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="69481-235">Un objeto `taskInfo` de un formulario o un `string` mensaje.</span><span class="sxs-lookup"><span data-stu-id="69481-235">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="69481-236">El esquema del objeto taskInfo es:</span><span class="sxs-lookup"><span data-stu-id="69481-236">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="69481-237">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="69481-237">Property name</span></span>|<span data-ttu-id="69481-238">Finalidad</span><span class="sxs-lookup"><span data-stu-id="69481-238">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="69481-239">Título del módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="69481-239">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="69481-240">Debe ser un entero (en píxeles) o `small` `medium` , `large` .</span><span class="sxs-lookup"><span data-stu-id="69481-240">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="69481-241">Debe ser un entero (en píxeles) o `small` `medium` , `large` .</span><span class="sxs-lookup"><span data-stu-id="69481-241">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="69481-242">La tarjeta adaptable que define el formulario (si se usa uno).</span><span class="sxs-lookup"><span data-stu-id="69481-242">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="69481-243">Dirección URL que se abrirá dentro del módulo de tareas como una vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="69481-243">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="69481-244">Si un cliente no admite la característica del módulo de tareas, esta dirección URL se abre en una pestaña del explorador.</span><span class="sxs-lookup"><span data-stu-id="69481-244">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="with-an-adaptive-card"></a><span data-ttu-id="69481-245">Con una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="69481-245">With an adaptive card</span></span>

<span data-ttu-id="69481-246">Al usar una tarjeta adaptable, debes responder con un `task` objeto con el objeto que contiene una tarjeta `value` adaptable.</span><span class="sxs-lookup"><span data-stu-id="69481-246">When using an adaptive card, you must respond with a `task` object with the `value` object containing an adaptive card.</span></span>

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a><span data-ttu-id="69481-247">Ejemplo de respuesta fetchTask con una tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="69481-247">Example fetchTask response with an adaptive card</span></span>

# <a name="cnet"></a>[<span data-ttu-id="69481-248">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="69481-248">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="69481-249">En este ejemplo se usa [el paquete NuGet AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards) además del SDK de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="69481-249">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="69481-250">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="69481-250">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="69481-251">JSON</span><span class="sxs-lookup"><span data-stu-id="69481-251">JSON</span></span>](#tab/json)

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

### <a name="with-an-embedded-web-view"></a><span data-ttu-id="69481-252">Con una vista web incrustada</span><span class="sxs-lookup"><span data-stu-id="69481-252">With an embedded web view</span></span>

<span data-ttu-id="69481-253">Al usar una vista web incrustada, debe responder con un objeto con el objeto que contiene la dirección URL del formulario web que `task` `value` desea cargar.</span><span class="sxs-lookup"><span data-stu-id="69481-253">When using an embedded web view, you must respond with a `task` object with the `value` object containing the URL to the web form you'd like to load.</span></span> <span data-ttu-id="69481-254">Los dominios de cualquier dirección URL que quiera cargar deben incluirse en la `validDomains` matriz en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69481-254">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="69481-255">Consulte la documentación [del módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md) para obtener información completa sobre cómo crear la vista web incrustada.</span><span class="sxs-lookup"><span data-stu-id="69481-255">See the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md) for complete information on building your embedded web view.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="69481-256">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="69481-256">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="69481-257">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="69481-257">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="69481-258">JSON</span><span class="sxs-lookup"><span data-stu-id="69481-258">JSON</span></span>](#tab/json)

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="69481-259">Solicitud para instalar el bot de conversación</span><span class="sxs-lookup"><span data-stu-id="69481-259">Request to install your conversational bot</span></span>

<span data-ttu-id="69481-260">Si la aplicación contiene un bot de conversación, instale el bot en la conversación antes de cargar el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="69481-260">If the app contains a conversational bot, install the bot in the conversation before loading the task module.</span></span> <span data-ttu-id="69481-261">Es útil obtener contexto adicional para el módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="69481-261">It is useful to get additional context for the task module.</span></span> <span data-ttu-id="69481-262">Un ejemplo típico de este escenario es capturar la lista para rellenar un control de selector de personas o la lista de canales de un equipo.</span><span class="sxs-lookup"><span data-stu-id="69481-262">Typical example for this scenario is to fetch the roster to populate a people picker control or the list of channels in a team.</span></span>

<span data-ttu-id="69481-263">Cuando la extensión de mensajería reciba la invocación, compruebe si el bot está instalado `composeExtension/fetchTask` en el contexto actual para facilitar el flujo.</span><span class="sxs-lookup"><span data-stu-id="69481-263">When the messaging extension receives the `composeExtension/fetchTask` invoke, check if the bot is installed in the current context to facilitate the flow.</span></span> <span data-ttu-id="69481-264">Por ejemplo, compruebe el flujo con una llamada de lista de obtener.</span><span class="sxs-lookup"><span data-stu-id="69481-264">For example, check the flow with a get roster call.</span></span> <span data-ttu-id="69481-265">Si el bot no está instalado, devuelve una tarjeta adaptable con una acción que solicita al usuario que instale el bot.</span><span class="sxs-lookup"><span data-stu-id="69481-265">If the bot is not installed, return an Adaptive Card with an action that requests the user to install the bot.</span></span> <span data-ttu-id="69481-266">Vea la acción en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="69481-266">See the action in the following example.</span></span> <span data-ttu-id="69481-267">El usuario debe tener permiso para instalar las aplicaciones en esa ubicación para su comprobación.</span><span class="sxs-lookup"><span data-stu-id="69481-267">The user must have permission to install the apps in that location for checking.</span></span> <span data-ttu-id="69481-268">Si la instalación de la aplicación no se realiza correctamente, el usuario recibe un mensaje para ponerse en contacto con el administrador.</span><span class="sxs-lookup"><span data-stu-id="69481-268">If the app installation is unsuccessful, the user receives a message to contact the administrator.</span></span>

#### <a name="example-of-the-response"></a><span data-ttu-id="69481-269">Ejemplo de la respuesta:</span><span class="sxs-lookup"><span data-stu-id="69481-269">Example of the response:</span></span>

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

<span data-ttu-id="69481-270">Después de la instalación, el bot recibe otro mensaje de invocación con `name = composeExtension/submitAction` y `value.data.msteams.justInTimeInstall = true` .</span><span class="sxs-lookup"><span data-stu-id="69481-270">After the installation, the bot receives another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

#### <a name="example-of-the-invoke"></a><span data-ttu-id="69481-271">Ejemplo de la invocación:</span><span class="sxs-lookup"><span data-stu-id="69481-271">Example of the invoke:</span></span>

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

<span data-ttu-id="69481-272">La respuesta de tarea a la invocación debe ser similar a la del bot instalado.</span><span class="sxs-lookup"><span data-stu-id="69481-272">The task response to the invoke must be similar to that of the installed bot.</span></span>

#### <a name="example-of-just-in-time-installation-of-app-with-adaptive-card"></a><span data-ttu-id="69481-273">Ejemplo de instalación just-in-time de la aplicación con tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="69481-273">Example of just-in time installation of app with Adaptive card:</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="69481-274">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69481-274">Next steps</span></span>

<span data-ttu-id="69481-275">Si permite que los usuarios envíen una respuesta desde el módulo de tareas, debe controlar la acción de envío.</span><span class="sxs-lookup"><span data-stu-id="69481-275">If you allow your users to send a response back from the task module, you must handle the submit action.</span></span>

* [<span data-ttu-id="69481-276">Crear y responder con un módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="69481-276">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
