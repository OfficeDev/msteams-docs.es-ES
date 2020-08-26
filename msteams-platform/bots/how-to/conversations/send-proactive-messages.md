---
title: Envío de mensajes proactivos
author: clearab
description: Cómo enviar mensajes proactivos con su bot de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2dfb8e18243079ca38d505f4b80deb7abf2de32f
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874852"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="101b1-103">Envío de mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="101b1-103">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="101b1-104">Un mensaje proactivo es cualquier mensaje enviado por un bot que no responde directamente a una solicitud de un usuario.</span><span class="sxs-lookup"><span data-stu-id="101b1-104">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="101b1-105">Esto puede incluir mensajes como:</span><span class="sxs-lookup"><span data-stu-id="101b1-105">This can include messages like:</span></span>

* <span data-ttu-id="101b1-106">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="101b1-106">Welcome messages</span></span>
* <span data-ttu-id="101b1-107">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="101b1-107">Notifications</span></span>
* <span data-ttu-id="101b1-108">Mensajes programados</span><span class="sxs-lookup"><span data-stu-id="101b1-108">Scheduled messages</span></span>

<span data-ttu-id="101b1-109">Para que el bot envíe un mensaje proactivo, debe tener acceso al usuario, al chat de grupo o al equipo al que desea enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="101b1-109">In order for your bot to send a proactive message, it must have access to the user, group chat, or team that you wish to send the message to.</span></span> <span data-ttu-id="101b1-110">Para un equipo o chat de grupo, esto significa que la aplicación que contiene el bot debe instalarse primero en esa ubicación.</span><span class="sxs-lookup"><span data-stu-id="101b1-110">For a group chat or team, this means the app that contains your bot must first be installed to that location.</span></span> <span data-ttu-id="101b1-111">Puede [instalar de forma proactiva su aplicación con Graph](#proactively-install-your-app-using-graph) en un equipo si es necesario o usar una [Directiva de aplicación](/microsoftteams/teams-custom-app-policies-and-settings) para insertar aplicaciones en Microsoft Teams y los usuarios de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="101b1-111">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team if necessary, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="101b1-112">Para los usuarios, su aplicación debe estar instalada para ese usuario o bien el usuario debe formar parte de un equipo en el que se instale la aplicación.</span><span class="sxs-lookup"><span data-stu-id="101b1-112">For users, your app either needs to be installed for that user, or your user needs to be part of a team where your app is installed.</span></span>

<span data-ttu-id="101b1-113">El envío de un mensaje proactivo es diferente al envío de un mensaje normal, ya que no tendrá un activo `turnContext` que usar para responder.</span><span class="sxs-lookup"><span data-stu-id="101b1-113">Sending a proactive message is different than sending a regular message in that you won't have an active `turnContext` to use for a reply.</span></span> <span data-ttu-id="101b1-114">Es posible que también necesite crear la conversación (por ejemplo, un nuevo chat uno a uno o un nuevo hilo de conversación en un canal) antes de enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="101b1-114">You may also need to create the conversation (for example a new one-to-one chat, or a new conversation thread in a channel) before sending the message.</span></span> <span data-ttu-id="101b1-115">No puede crear un nuevo chat de grupo o un nuevo canal en un equipo con mensajería proactiva.</span><span class="sxs-lookup"><span data-stu-id="101b1-115">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="101b1-116">En un nivel alto, los pasos que tendrá que completar para enviar un mensaje proactivo son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="101b1-116">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="101b1-117">[Obtenga el identificador de usuario o de equipo o de canal](#get-the-user-id-or-teamchannel-id) (si es necesario).</span><span class="sxs-lookup"><span data-stu-id="101b1-117">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="101b1-118">[Cree la conversación o hilo de conversación](#create-the-conversation) (si es necesario).</span><span class="sxs-lookup"><span data-stu-id="101b1-118">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="101b1-119">[Obtener el identificador de la conversación](#get-the-conversation-id).</span><span class="sxs-lookup"><span data-stu-id="101b1-119">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="101b1-120">[Enviar el mensaje](#send-the-message).</span><span class="sxs-lookup"><span data-stu-id="101b1-120">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="101b1-121">Los fragmentos de código de la sección de [ejemplos](#examples) que se muestran a continuación son para crear una conversación de uno a uno, consulte la sección [referencias](#references) para obtener vínculos para completar ejemplos de trabajo para conversaciones de uno a una y grupo/canales.</span><span class="sxs-lookup"><span data-stu-id="101b1-121">The code snippets in the [examples](#examples) section below are for creating a one-to-one conversation, see the [references](#references) section for links to complete working samples for both one-to-once conversations and group/channels.</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="101b1-122">Obtener el identificador de usuario o de equipo o de canal</span><span class="sxs-lookup"><span data-stu-id="101b1-122">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="101b1-123">Si necesita crear una conversación o un hilo de conversación nuevos en un canal, primero necesitará el identificador correcto para crear la conversación.</span><span class="sxs-lookup"><span data-stu-id="101b1-123">If you need to create a new conversation or conversation thread in a channel you'll first need the right ID to create the conversation.</span></span> <span data-ttu-id="101b1-124">Puede recibir o recuperar este identificador de varias formas:</span><span class="sxs-lookup"><span data-stu-id="101b1-124">You can receive/retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="101b1-125">Cuando la aplicación está instalada en un contexto determinado, recibirá una [ `onMembersAdded` actividad](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="101b1-125">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="101b1-126">Cuando se agrega un nuevo usuario a un contexto donde la aplicación está instalada, recibirá una [ `onMembersAdded` actividad](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="101b1-126">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="101b1-127">Puede recuperar la [lista de canales](~/bots/how-to/get-teams-context.md) en un equipo en el que está instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="101b1-127">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="101b1-128">Puede recuperar la [lista de miembros](~/bots/how-to/get-teams-context.md) de un equipo en el que está instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="101b1-128">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="101b1-129">Cada actividad que recibe el bot contendrá la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="101b1-129">Every Activity your bot receives will contain the necessary information.</span></span>

<span data-ttu-id="101b1-130">Independientemente de cómo obtenga la información, tendrá que almacenar el `tenantId` y el `userId` o `channelId` para crear una nueva conversación.</span><span class="sxs-lookup"><span data-stu-id="101b1-130">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` in order to create a new conversation.</span></span> <span data-ttu-id="101b1-131">También puede usar el `teamId` para crear una nueva secuencia de conversación en el canal general/predeterminado de un equipo.</span><span class="sxs-lookup"><span data-stu-id="101b1-131">You can also use the `teamId` to create a new conversation thread in the general/default channel of a team.</span></span>

<span data-ttu-id="101b1-132">El `userId` es único para el identificador de Bot y un usuario en particular, no puede volver a usarlos entre bots.</span><span class="sxs-lookup"><span data-stu-id="101b1-132">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="101b1-133">El `channelId` es global, sin embargo, el bot _debe_ estar instalado en el equipo para poder enviar un mensaje proactivo a un canal.</span><span class="sxs-lookup"><span data-stu-id="101b1-133">The `channelId` is global, however your bot _must_ be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="101b1-134">Crear la conversación</span><span class="sxs-lookup"><span data-stu-id="101b1-134">Create the conversation</span></span>

<span data-ttu-id="101b1-135">Una vez que tenga la información de usuario/canal, tendrá que crear la conversación si todavía no existe (o no sabe la `conversationId` ).</span><span class="sxs-lookup"><span data-stu-id="101b1-135">Once you have the user/channel information, you'll need to create the conversation if it doesn't already exist (or you don't know the `conversationId`).</span></span> <span data-ttu-id="101b1-136">Solo debe crear la conversación una vez; Asegúrese de almacenar el `conversationId` valor o el `conversationReference` objeto que se va a usar en el futuro.</span><span class="sxs-lookup"><span data-stu-id="101b1-136">You should only create the conversation once; make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="101b1-137">Obtener el identificador de conversación</span><span class="sxs-lookup"><span data-stu-id="101b1-137">Get the conversation ID</span></span>

<span data-ttu-id="101b1-138">Una vez que se haya creado la conversación, deberá usar el `conversationReference` objeto o el `conversationId` y el `tenantId` para enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="101b1-138">Once the conversation has been created, you will use either the `conversationReference` object or the `conversationId` and the `tenantId` to send the message.</span></span> <span data-ttu-id="101b1-139">Puede obtener este identificador si crea la conversación o la almacena desde cualquier actividad que se le envíe desde ese contexto.</span><span class="sxs-lookup"><span data-stu-id="101b1-139">You can get this Id by either creating the conversation, or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="101b1-140">Asegúrese de almacenar este identificador.</span><span class="sxs-lookup"><span data-stu-id="101b1-140">Make certain that you store this Id.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="101b1-141">Enviar el mensaje</span><span class="sxs-lookup"><span data-stu-id="101b1-141">Send the message</span></span>

<span data-ttu-id="101b1-142">Ahora que tiene la información de dirección correcta, puede enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="101b1-142">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="101b1-143">Si estás usando el SDK, tendrás que hacerlo usando el `continueConversation` método y el `conversationId` y `tenantId` para realizar una llamada directa a la API.</span><span class="sxs-lookup"><span data-stu-id="101b1-143">If you're using the SDK, you'll do so using the `continueConversation` method,and the `conversationId` and `tenantId` to make a direct API call.</span></span>  <span data-ttu-id="101b1-144">Necesitará configurar `conversationParameters` correctamente para que el mensaje se envíe correctamente; vea los [ejemplos](#examples) siguientes o use uno de los ejemplos que se enumeran en la sección [referencias](#references) .</span><span class="sxs-lookup"><span data-stu-id="101b1-144">You'll need to set the `conversationParameters` correctly to successfully send your message - see the [examples](#examples) below or use one of the samples listed in the [references](#references) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="101b1-145">Procedimientos recomendados para la mensajería proactiva</span><span class="sxs-lookup"><span data-stu-id="101b1-145">Best practices for proactive messaging</span></span>

<span data-ttu-id="101b1-146">El envío de mensajes proactivos a los usuarios puede ser una forma muy eficaz de comunicarse con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="101b1-146">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="101b1-147">Sin embargo, desde su perspectiva, este mensaje puede aparecer completamente sin intervención del usuario y, en el caso de los mensajes de bienvenida, será la primera vez que interactuen con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="101b1-147">However, from their perspective this message can appear completely unprompted and, in the case of welcome messages, it will be the first time they've interacted with your app.</span></span> <span data-ttu-id="101b1-148">Por lo tanto, es muy importante usar esta funcionalidad con moderación (no enviar correo no deseado a los usuarios) y proporcionar suficiente información para que los usuarios sepan por qué se les está enviando un mensaje.</span><span class="sxs-lookup"><span data-stu-id="101b1-148">As such, it is very important to use this functionality sparingly (don't spam your users) and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="101b1-149">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="101b1-149">Welcome messages</span></span>

<span data-ttu-id="101b1-150">Al usar la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que, en la mayoría de las personas que reciben el mensaje, no habrá ningún contexto para la razón por la cual lo reciben.</span><span class="sxs-lookup"><span data-stu-id="101b1-150">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there will be no context for why they are receiving it.</span></span> <span data-ttu-id="101b1-151">También es la primera vez que interactuarán con la aplicación; es su oportunidad para crear una buena primera impresión.</span><span class="sxs-lookup"><span data-stu-id="101b1-151">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="101b1-152">Los mejores mensajes de bienvenida incluirán:</span><span class="sxs-lookup"><span data-stu-id="101b1-152">The best welcome messages will include:</span></span>

* <span data-ttu-id="101b1-153">**Por qué un usuario recibe el mensaje.**</span><span class="sxs-lookup"><span data-stu-id="101b1-153">**Why a user is receiving the message.**</span></span> <span data-ttu-id="101b1-154">El usuario debe ser muy claro por qué reciben el mensaje.</span><span class="sxs-lookup"><span data-stu-id="101b1-154">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="101b1-155">Si el bot se ha instalado en un canal y se ha enviado un mensaje de bienvenida a todos los usuarios, hágales saber en qué canal se ha instalado y que podrían instalarlo.</span><span class="sxs-lookup"><span data-stu-id="101b1-155">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="101b1-156">**Qué ofrece.**</span><span class="sxs-lookup"><span data-stu-id="101b1-156">**What do you offer.**</span></span> <span data-ttu-id="101b1-157">¿Qué puede hacer con la aplicación?</span><span class="sxs-lookup"><span data-stu-id="101b1-157">What can they do with your app?</span></span> <span data-ttu-id="101b1-158">¿Qué valor puede aportar a ellos?</span><span class="sxs-lookup"><span data-stu-id="101b1-158">What value can you bring to them?</span></span>
* <span data-ttu-id="101b1-159">**Qué debería hacer a continuación.**</span><span class="sxs-lookup"><span data-stu-id="101b1-159">**What should they do next.**</span></span> <span data-ttu-id="101b1-160">Invitar a probar un comando o interactuar con la aplicación de alguna manera.</span><span class="sxs-lookup"><span data-stu-id="101b1-160">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="101b1-161">Recuerde que los mensajes de bienvenida deficientes pueden dar lugar a que los usuarios bloqueen su bot.</span><span class="sxs-lookup"><span data-stu-id="101b1-161">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="101b1-162">Debe dedicar mucho tiempo a elaborar los mensajes de bienvenida y realizar iteraciones en ellos si no tienen el efecto deseado.</span><span class="sxs-lookup"><span data-stu-id="101b1-162">You should spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="101b1-163">Mensajes de notificación</span><span class="sxs-lookup"><span data-stu-id="101b1-163">Notification messages</span></span>

<span data-ttu-id="101b1-164">Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta de acceso clara para emprender acciones comunes en función de la notificación y un conocimiento claro de la razón por la que se produjo la notificación.</span><span class="sxs-lookup"><span data-stu-id="101b1-164">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="101b1-165">Por lo general, los mensajes de notificación son correctos:</span><span class="sxs-lookup"><span data-stu-id="101b1-165">Good notification messages will generally include:</span></span>

* <span data-ttu-id="101b1-166">**Qué ha pasado.**</span><span class="sxs-lookup"><span data-stu-id="101b1-166">**What happened.**</span></span> <span data-ttu-id="101b1-167">Una indicación clara de lo que ha sucedido para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="101b1-167">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="101b1-168">**Cuál era el resultado.**</span><span class="sxs-lookup"><span data-stu-id="101b1-168">**What was the result.**</span></span> <span data-ttu-id="101b1-169">Debe estar claro qué elemento/Thing se actualizó para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="101b1-169">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="101b1-170">**Quién/lo ha desencadenado.**</span><span class="sxs-lookup"><span data-stu-id="101b1-170">**Who/what triggered it.**</span></span> <span data-ttu-id="101b1-171">Quién o qué emprendió acciones que hacían que se enviara la notificación.</span><span class="sxs-lookup"><span data-stu-id="101b1-171">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="101b1-172">**Qué pueden hacer los usuarios en respuesta.**</span><span class="sxs-lookup"><span data-stu-id="101b1-172">**What can users do in response.**</span></span> <span data-ttu-id="101b1-173">Facilite a los usuarios que realicen acciones basadas en las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="101b1-173">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="101b1-174">**Cómo pueden deselegir los usuarios.** Debe proporcionar una ruta de acceso para que los usuarios puedan optar por las notificaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="101b1-174">**How can users opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="101b1-175">Instalar de forma proactiva la aplicación con Graph</span><span class="sxs-lookup"><span data-stu-id="101b1-175">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="101b1-176">La instalación de aplicaciones con Microsoft Graph de forma proactiva se encuentra actualmente en versión beta.</span><span class="sxs-lookup"><span data-stu-id="101b1-176">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="101b1-177">En ocasiones, es posible que sea necesario enviar un mensaje de forma proactiva a los usuarios que no hayan instalado ni interactúen con la aplicación anteriormente.</span><span class="sxs-lookup"><span data-stu-id="101b1-177">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="101b1-178">Por ejemplo, desea usar el Communicator de la [compañía](~/samples/app-templates.md#company-communicator) para enviar mensajes a toda la organización.</span><span class="sxs-lookup"><span data-stu-id="101b1-178">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="101b1-179">Para este escenario, puede usar la API de Graph para instalar proactivamente la aplicación para sus usuarios y, a continuación, almacenar en caché los valores necesarios del `conversationUpdate` evento que la aplicación recibirá en el momento de la instalación.</span><span class="sxs-lookup"><span data-stu-id="101b1-179">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="101b1-180">Solo puede instalar aplicaciones que estén en el catálogo de aplicaciones de la organización o en la tienda de aplicaciones de Teams.</span><span class="sxs-lookup"><span data-stu-id="101b1-180">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="101b1-181">Consulte [instalar aplicaciones para usuarios](/graph/teams-proactive-messaging) en la documentación de Graph y la [instalación y mensajería de robots proactivas en Teams con Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="101b1-181">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="101b1-182">También hay un [ejemplo de Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  en la plataforma de github.</span><span class="sxs-lookup"><span data-stu-id="101b1-182">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="101b1-183">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="101b1-183">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="101b1-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="101b1-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
private async Task MessageAllMembersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var teamsChannelId = turnContext.Activity.TeamsGetChannelId();
    var serviceUrl = turnContext.Activity.ServiceUrl;
    var credentials = new MicrosoftAppCredentials(_appId, _appPassword);
    ConversationReference conversationReference = null;

    //Get the set of member IDs to send the message to
    var members = await GetPagedMembers(turnContext, cancellationToken);

    foreach (var teamMember in members)
    {
        var proactiveMessage = MessageFactory.Text($"Hello {teamMember.GivenName} {teamMember.Surname}. I'm a Teams conversation bot.");

        var conversationParameters = new ConversationParameters
        {
            IsGroup = false,
            Bot = turnContext.Activity.Recipient,
            Members = new ChannelAccount[] { teamMember },
            TenantId = turnContext.Activity.Conversation.TenantId,
        };
        //create the new one-to-one conversations
        await ((BotFrameworkAdapter)turnContext.Adapter).CreateConversationAsync(
            teamsChannelId,
            serviceUrl,
            credentials,
            conversationParameters,
            async (t1, c1) =>
            {
                //Get the conversationReference
                conversationReference = t1.Activity.GetConversationReference();
                //Send the proactive message
                await ((BotFrameworkAdapter)turnContext.Adapter).ContinueConversationAsync(
                    _appId,
                    conversationReference,
                    async (t2, c2) =>
                    {
                        await t2.SendActivityAsync(proactiveMessage, c2);
                    },
                    cancellationToken);
            },
            cancellationToken);
    }

    await turnContext.SendActivityAsync(MessageFactory.Text("All messages have been sent."), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="101b1-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="101b1-185">TypeScript/Node.js</span></span>](#tab/typescript)

```javascript

async messageAllMembersAsync(context) {
    const members = await this.getPagedMembers(context);

    members.forEach(async (teamMember) => {
        const message = MessageFactory.text('Hello ${ teamMember.givenName } ${ teamMember.surname }. I\'m a Teams conversation bot.');

        var ref = TurnContext.getConversationReference(context.activity);
        ref.user = teamMember;

        await context.adapter.createConversation(ref,
            async (t1) => {
                const ref2 = TurnContext.getConversationReference(t1.activity);
                await t1.adapter.continueConversation(ref2, async (t2) => {
                    await t2.sendActivity(message);
                });
            });
    });

    await context.sendActivity(MessageFactory.text('All messages have been sent.'));
}
```

# <a name="python"></a>[<span data-ttu-id="101b1-186">Python</span><span class="sxs-lookup"><span data-stu-id="101b1-186">Python</span></span>](#tab/python)

```python
async def _message_all_members(self, turn_context: TurnContext):
    team_members = await self._get_paged_members(turn_context)

    for member in team_members:
        conversation_reference = TurnContext.get_conversation_reference(
            turn_context.activity
        )

        conversation_parameters = ConversationParameters(
            is_group=False,
            bot=turn_context.activity.recipient,
            members=[member],
            tenant_id=turn_context.activity.conversation.tenant_id,
        )

        async def get_ref(tc1):
            conversation_reference_inner = TurnContext.get_conversation_reference(
                tc1.activity
            )
            return await tc1.adapter.continue_conversation(
                conversation_reference_inner, send_message, self._app_id
            )

        async def send_message(tc2: TurnContext):
            return await tc2.send_activity(
                f"Hello {member.name}. I'm a Teams conversation bot."
            )

        await turn_context.adapter.create_conversation(
            conversation_reference, get_ref, conversation_parameters
        )

    await turn_context.send_activity(
        MessageFactory.text("All messages have been sent")
    )

```

# <a name="json"></a>[<span data-ttu-id="101b1-187">JSON</span><span class="sxs-lookup"><span data-stu-id="101b1-187">JSON</span></span>](#tab/json)

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

<span data-ttu-id="101b1-188">Debe proporcionar el identificador de usuario y el identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="101b1-188">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="101b1-189">Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta.</span><span class="sxs-lookup"><span data-stu-id="101b1-189">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="references"></a><span data-ttu-id="101b1-190">Referencias</span><span class="sxs-lookup"><span data-stu-id="101b1-190">References</span></span>

<span data-ttu-id="101b1-191">A continuación se enumeran los ejemplos de mensajería proactiva oficial.</span><span class="sxs-lookup"><span data-stu-id="101b1-191">The official proactive messaging samples are listed below.</span></span>

|  <span data-ttu-id="101b1-192">No.</span><span class="sxs-lookup"><span data-stu-id="101b1-192">No.</span></span>  | <span data-ttu-id="101b1-193">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="101b1-193">Sample Name</span></span>           | <span data-ttu-id="101b1-194">Description</span><span class="sxs-lookup"><span data-stu-id="101b1-194">Description</span></span>                                                                      | <span data-ttu-id="101b1-195">.NET</span><span class="sxs-lookup"><span data-stu-id="101b1-195">.NET</span></span>    | <span data-ttu-id="101b1-196">JavaScript</span><span class="sxs-lookup"><span data-stu-id="101b1-196">JavaScript</span></span>   | <span data-ttu-id="101b1-197">Python</span><span class="sxs-lookup"><span data-stu-id="101b1-197">Python</span></span>  |
|:--:|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="101b1-198">57</span><span class="sxs-lookup"><span data-stu-id="101b1-198">57</span></span>|<span data-ttu-id="101b1-199">Conceptos básicos de la conversación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="101b1-199">Teams Conversation Basics</span></span>  | <span data-ttu-id="101b1-200">Muestra los conceptos básicos de las conversaciones en Microsoft Teams, incluido el envío de mensajes proactivos de uno a uno.</span><span class="sxs-lookup"><span data-stu-id="101b1-200">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="101b1-201">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="101b1-201">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="101b1-202">JavaScript</span><span class="sxs-lookup"><span data-stu-id="101b1-202">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="101b1-203">Python</span><span class="sxs-lookup"><span data-stu-id="101b1-203">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="101b1-204">58</span><span class="sxs-lookup"><span data-stu-id="101b1-204">58</span></span>|<span data-ttu-id="101b1-205">Iniciar un nuevo hilo en un canal</span><span class="sxs-lookup"><span data-stu-id="101b1-205">Start new thread in a channel</span></span>     | <span data-ttu-id="101b1-206">Muestra cómo crear un nuevo hilo en un canal.</span><span class="sxs-lookup"><span data-stu-id="101b1-206">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="101b1-207">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="101b1-207">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="101b1-208">JavaScript</span><span class="sxs-lookup"><span data-stu-id="101b1-208">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="101b1-209">Python</span><span class="sxs-lookup"><span data-stu-id="101b1-209">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

<span data-ttu-id="101b1-210">En el siguiente ejemplo se muestra la cantidad mínima de información necesaria para enviar un mensaje proactivo (sin usar un `conversationReference` objeto).</span><span class="sxs-lookup"><span data-stu-id="101b1-210">The sample below demonstrates the minimal amount of information needed to send a proactive message (without using a `conversationReference` object).</span></span> <span data-ttu-id="101b1-211">Este ejemplo puede resultar útil si está usando llamadas API de REST directamente o si no ha almacenado `conversationReference` objetos completos.</span><span class="sxs-lookup"><span data-stu-id="101b1-211">This sample can be useful if you're using REST API calls directly, or haven't been storing full `conversationReference` objects.</span></span>

* [<span data-ttu-id="101b1-212">Mensajería proactiva de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="101b1-212">Teams Proactive Messaging</span></span>](https://github.com/clearab/teamsProactiveMessaging)

## <a name="view-additional-code"></a><span data-ttu-id="101b1-213">Ver código adicional</span><span class="sxs-lookup"><span data-stu-id="101b1-213">View additional code</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="101b1-214">**Ejemplos de código de mensajería proactiva de Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="101b1-214">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>