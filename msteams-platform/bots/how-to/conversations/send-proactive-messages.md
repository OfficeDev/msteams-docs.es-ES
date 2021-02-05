---
title: enviar mensajes proactivos
description: describe cómo enviar mensajes proactivos con el bot de Microsoft Teams.
ms.topic: overview
ms.author: anclear
Keywords: enviar un mensaje para obtener el id. de usuario id. de la conversación de conversación de id. de canal
ms.openlocfilehash: 2d7ff10469a181bb06fda5029c8f6b2725b0402d
ms.sourcegitcommit: 7db6eabe3ef128ac7f14b32d07e9e86c995d187f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/04/2021
ms.locfileid: "50103608"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="cb634-104">Enviar mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="cb634-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="cb634-105">Un mensaje proactivo es cualquier mensaje enviado por un bot que no está en respuesta directa a una solicitud de un usuario.</span><span class="sxs-lookup"><span data-stu-id="cb634-105">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="cb634-106">Esto puede incluir mensajes como:</span><span class="sxs-lookup"><span data-stu-id="cb634-106">This can include messages like:</span></span>

* <span data-ttu-id="cb634-107">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="cb634-107">Welcome messages</span></span>
* <span data-ttu-id="cb634-108">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="cb634-108">Notifications</span></span>
* <span data-ttu-id="cb634-109">Mensajes programados</span><span class="sxs-lookup"><span data-stu-id="cb634-109">Scheduled messages</span></span>

<span data-ttu-id="cb634-110">Para que el bot envíe un mensaje proactivo, debe tener acceso al usuario, al chat en grupo o al equipo al que desea enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="cb634-110">For your bot to send a proactive message, it must have access to the user, group chat, or team that you want to send the message to.</span></span> <span data-ttu-id="cb634-111">Para un chat de grupo o equipo, esto significa que la aplicación que contiene el bot debe instalarse primero en esa ubicación.</span><span class="sxs-lookup"><span data-stu-id="cb634-111">For a group chat or team, this means the app that contains your bot must be installed to that location first.</span></span> <span data-ttu-id="cb634-112">Puede instalar [la aplicación de](#proactively-install-your-app-using-graph) forma proactiva con Graph [](/microsoftteams/teams-custom-app-policies-and-settings) en un equipo, si es necesario o usar una directiva de aplicación para enviar aplicaciones a equipos y usuarios de su espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="cb634-112">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team, if required or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="cb634-113">Para los usuarios, la aplicación debe estar instalada para el usuario o el usuario debe formar parte de un equipo donde esté instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb634-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="cb634-114">El envío de un mensaje proactivo es diferente al envío de un mensaje normal.</span><span class="sxs-lookup"><span data-stu-id="cb634-114">Sending a proactive message is different than sending a regular message.</span></span> <span data-ttu-id="cb634-115">En ese caso, no hay ningún activo `turnContext` para usar para una respuesta.</span><span class="sxs-lookup"><span data-stu-id="cb634-115">In that, there is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="cb634-116">Es posible que también necesite crear la conversación antes de enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="cb634-116">You may also need to create the conversation before sending the message.</span></span> <span data-ttu-id="cb634-117">Por ejemplo, un nuevo chat uno a uno o un nuevo hilo de conversación en un canal.</span><span class="sxs-lookup"><span data-stu-id="cb634-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="cb634-118">No puede crear un nuevo chat de grupo o un nuevo canal en un equipo con mensajería proactiva.</span><span class="sxs-lookup"><span data-stu-id="cb634-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="cb634-119">En un nivel alto, los pasos que deberá completar para enviar un mensaje proactivo son:</span><span class="sxs-lookup"><span data-stu-id="cb634-119">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="cb634-120">[Obtenga el identificador de usuario o el identificador de equipo o canal](#get-the-user-id-or-teamchannel-id) (si es necesario).</span><span class="sxs-lookup"><span data-stu-id="cb634-120">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="cb634-121">[Cree el hilo de conversación o conversación](#create-the-conversation) (si es necesario).</span><span class="sxs-lookup"><span data-stu-id="cb634-121">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="cb634-122">[Obtener el id. de conversación.](#get-the-conversation-id)</span><span class="sxs-lookup"><span data-stu-id="cb634-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="cb634-123">[Envíe el mensaje.](#send-the-message)</span><span class="sxs-lookup"><span data-stu-id="cb634-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="cb634-124">Los fragmentos de código de la [sección de](#examples) ejemplos son para crear una conversación uno a uno.</span><span class="sxs-lookup"><span data-stu-id="cb634-124">The code snippets in the [examples](#examples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="cb634-125">Para obtener vínculos a ejemplos de trabajo completos para conversaciones de uno a uno y grupos o canales, vea [ejemplos de código.](#code-samples)</span><span class="sxs-lookup"><span data-stu-id="cb634-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code samples](#code-samples).</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="cb634-126">Obtener el identificador de usuario o el identificador de equipo o canal</span><span class="sxs-lookup"><span data-stu-id="cb634-126">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="cb634-127">Para crear una conversación o conversación nueva en un canal, necesita el identificador correcto.</span><span class="sxs-lookup"><span data-stu-id="cb634-127">To create a new conversation or conversation thread in a channel, you need the correct ID.</span></span> <span data-ttu-id="cb634-128">Puede recibir o recuperar este identificador de varias maneras:</span><span class="sxs-lookup"><span data-stu-id="cb634-128">You can receive or retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="cb634-129">Cuando la aplicación esté instalada en cualquier contexto en particular, recibirás una [ `onMembersAdded` actividad.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="cb634-129">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="cb634-130">Cuando se agrega un nuevo usuario a un contexto donde está instalada la aplicación, recibirás una [ `onMembersAdded` actividad.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="cb634-130">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="cb634-131">Puedes recuperar la [lista de canales](~/bots/how-to/get-teams-context.md) de un equipo en el que está instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb634-131">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="cb634-132">Puedes recuperar la [lista de miembros](~/bots/how-to/get-teams-context.md) de un equipo que tiene instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb634-132">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="cb634-133">Cada actividad que reciba el bot debe contener la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="cb634-133">Every Activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="cb634-134">Independientemente de cómo obtenga la información, tendrá que almacenar la conversación o `tenantId` `userId` `channelId` crearla.</span><span class="sxs-lookup"><span data-stu-id="cb634-134">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="cb634-135">También puede usar la opción para crear un nuevo hilo de conversación en el canal general o `teamId` predeterminado de un equipo.</span><span class="sxs-lookup"><span data-stu-id="cb634-135">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="cb634-136">El identificador de bot y un usuario determinado son únicos, no se `userId` pueden volver a usar entre bots.</span><span class="sxs-lookup"><span data-stu-id="cb634-136">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="cb634-137">Sin embargo, el bot es global y debe instalarse en el equipo para poder enviar un mensaje `channelId` proactivo a un canal.</span><span class="sxs-lookup"><span data-stu-id="cb634-137">The `channelId` is global, however, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="cb634-138">Crear la conversación</span><span class="sxs-lookup"><span data-stu-id="cb634-138">Create the conversation</span></span>

<span data-ttu-id="cb634-139">Una vez que tenga la información del usuario o del canal, debe crear la conversación si aún no existe o si no conoce el `conversationId` archivo .</span><span class="sxs-lookup"><span data-stu-id="cb634-139">After you have the user or channel information, you need to create the conversation if it doesn't already exist or you don't know the `conversationId`.</span></span> <span data-ttu-id="cb634-140">Solo debe crear la conversación una vez y asegurarse de almacenar el `conversationId` valor u objeto que se va a usar en el `conversationReference` futuro.</span><span class="sxs-lookup"><span data-stu-id="cb634-140">You must only create the conversation once and make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="cb634-141">Obtener el identificador de conversación</span><span class="sxs-lookup"><span data-stu-id="cb634-141">Get the conversation ID</span></span>

<span data-ttu-id="cb634-142">Después de crear la conversación, use el `conversationReference` objeto o envíe el `conversationId` `tenantId` mensaje.</span><span class="sxs-lookup"><span data-stu-id="cb634-142">After the conversation is created, use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="cb634-143">Para obtener este identificador, puede crear la conversación o almacenarla desde cualquier actividad que se le envíe desde ese contexto.</span><span class="sxs-lookup"><span data-stu-id="cb634-143">You can get this ID by either creating the conversation or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="cb634-144">Asegúrese de almacenar este identificador.</span><span class="sxs-lookup"><span data-stu-id="cb634-144">Make certain that you store this ID.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="cb634-145">Enviar el mensaje</span><span class="sxs-lookup"><span data-stu-id="cb634-145">Send the message</span></span>

<span data-ttu-id="cb634-146">Ahora que tiene la información de dirección correcta, puede enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="cb634-146">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="cb634-147">Si usa el SDK, lo hará con el método y con `continueConversation` la llamada a la API `conversationId` `tenantId` directa.</span><span class="sxs-lookup"><span data-stu-id="cb634-147">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="cb634-148">Debe establecer la configuración `conversationParameters` correcta para enviar correctamente el mensaje.</span><span class="sxs-lookup"><span data-stu-id="cb634-148">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="cb634-149">Vea la [sección de](#examples) ejemplos o use uno de los ejemplos enumerados en la sección de [ejemplos de](#code-samples) código.</span><span class="sxs-lookup"><span data-stu-id="cb634-149">See the [examples](#examples) section or use one of the samples listed in the [code samples](#code-samples) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="cb634-150">Procedimientos recomendados para mensajería proactiva</span><span class="sxs-lookup"><span data-stu-id="cb634-150">Best practices for proactive messaging</span></span>

<span data-ttu-id="cb634-151">Enviar mensajes proactivos a los usuarios es una forma muy eficaz de comunicarse con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="cb634-151">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="cb634-152">Sin embargo, desde su punto de vista, este mensaje puede aparecer completamente desprotegido y, en el caso de los mensajes de bienvenida, es la primera vez que interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb634-152">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="cb634-153">Por lo tanto, es muy importante usar esta funcionalidad con moderación, no enviar correo no deseado a los usuarios y proporcionar información suficiente para que los usuarios comprendan por qué se les envía un mensaje.</span><span class="sxs-lookup"><span data-stu-id="cb634-153">Therefore, it is very important to use this functionality sparingly, don't spam your users, and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="cb634-154">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="cb634-154">Welcome messages</span></span>

<span data-ttu-id="cb634-155">Al usar la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que, para la mayoría de las personas que reciben el mensaje, no hay contexto para por qué lo está recibiendo.</span><span class="sxs-lookup"><span data-stu-id="cb634-155">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there is no context for why they are receiving it.</span></span> <span data-ttu-id="cb634-156">También es la primera vez que interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb634-156">This is also the first time they have interacted with your app.</span></span> <span data-ttu-id="cb634-157">Es su oportunidad de crear una buena primera impresión.</span><span class="sxs-lookup"><span data-stu-id="cb634-157">It is your opportunity to create a good first impression.</span></span> <span data-ttu-id="cb634-158">Los mensajes de bienvenida más importantes deben incluir:</span><span class="sxs-lookup"><span data-stu-id="cb634-158">The best welcome messages must include:</span></span>

* <span data-ttu-id="cb634-159">**Por qué un usuario recibe el mensaje.**</span><span class="sxs-lookup"><span data-stu-id="cb634-159">**Why a user is receiving the message.**</span></span> <span data-ttu-id="cb634-160">Debe ser muy claro para el usuario por qué está recibiendo el mensaje.</span><span class="sxs-lookup"><span data-stu-id="cb634-160">It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="cb634-161">Si el bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, indálles en qué canal se instaló y quién lo instaló.</span><span class="sxs-lookup"><span data-stu-id="cb634-161">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="cb634-162">**¿Qué ofrece?**</span><span class="sxs-lookup"><span data-stu-id="cb634-162">**What do you offer.**</span></span> <span data-ttu-id="cb634-163">¿Qué pueden hacer con la aplicación?</span><span class="sxs-lookup"><span data-stu-id="cb634-163">What can they do with your app?</span></span> <span data-ttu-id="cb634-164">¿Qué valor puede aportarles?</span><span class="sxs-lookup"><span data-stu-id="cb634-164">What value can you bring to them?</span></span>
* <span data-ttu-id="cb634-165">**Qué deben hacer a continuación.**</span><span class="sxs-lookup"><span data-stu-id="cb634-165">**What should they do next.**</span></span> <span data-ttu-id="cb634-166">Invítelos a probar un comando o interactuar con la aplicación de alguna manera.</span><span class="sxs-lookup"><span data-stu-id="cb634-166">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="cb634-167">Recuerde que los mensajes de bienvenida deficientes pueden provocar que los usuarios bloqueen el bot.</span><span class="sxs-lookup"><span data-stu-id="cb634-167">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="cb634-168">Dedica mucho tiempo a elaborar los mensajes de bienvenida y repite en ellos si no tienen el efecto deseado.</span><span class="sxs-lookup"><span data-stu-id="cb634-168">Spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="cb634-169">Mensajes de notificación</span><span class="sxs-lookup"><span data-stu-id="cb634-169">Notification messages</span></span>

<span data-ttu-id="cb634-170">Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta clara para realizar acciones comunes basadas en la notificación y una comprensión clara de por qué se produjo la notificación.</span><span class="sxs-lookup"><span data-stu-id="cb634-170">When using proactive messaging to send notifications you must ensure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="cb634-171">Por lo general, los mensajes de notificación de buena calidad incluyen:</span><span class="sxs-lookup"><span data-stu-id="cb634-171">Good notification messages generally include:</span></span>

* <span data-ttu-id="cb634-172">**Qué ha pasado.**</span><span class="sxs-lookup"><span data-stu-id="cb634-172">**What happened.**</span></span> <span data-ttu-id="cb634-173">Una indicación clara de lo que ocurrió para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="cb634-173">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="cb634-174">**Cuál fue el resultado.**</span><span class="sxs-lookup"><span data-stu-id="cb634-174">**What was the result.**</span></span> <span data-ttu-id="cb634-175">Debe estar claro qué elemento o cosa se actualizó para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="cb634-175">It must be clear what item or thing was updated to cause the notification.</span></span>
* <span data-ttu-id="cb634-176">**Quién/qué lo desencadenó.**</span><span class="sxs-lookup"><span data-stu-id="cb634-176">**Who/what triggered it.**</span></span> <span data-ttu-id="cb634-177">Quién o qué acción realizó que se enviara la notificación.</span><span class="sxs-lookup"><span data-stu-id="cb634-177">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="cb634-178">**Qué pueden hacer los usuarios en respuesta.**</span><span class="sxs-lookup"><span data-stu-id="cb634-178">**What can users do in response.**</span></span> <span data-ttu-id="cb634-179">Facilita a los usuarios la realización de acciones en función de las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="cb634-179">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="cb634-180">**Cómo pueden optar por no participar los usuarios.** Debes proporcionar una ruta de acceso para que los usuarios puedan optar por no recibir notificaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="cb634-180">**How can users opt out.** You must provide a path for users to opt out of additional notifications.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="cb634-181">Instalar de forma proactiva la aplicación con Graph</span><span class="sxs-lookup"><span data-stu-id="cb634-181">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="cb634-182">La instalación proactiva de aplicaciones con Microsoft Graph se encuentra actualmente en versión beta.</span><span class="sxs-lookup"><span data-stu-id="cb634-182">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="cb634-183">En ocasiones, puede que sea necesario enviar mensajes de forma proactiva a los usuarios que no han instalado o interactuado con la aplicación anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cb634-183">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="cb634-184">Por ejemplo, desea usar el comunicador de la empresa [para](~/samples/app-templates.md#company-communicator) enviar mensajes a toda la organización.</span><span class="sxs-lookup"><span data-stu-id="cb634-184">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="cb634-185">Para este escenario, puede usar la API de Graph para instalar de forma proactiva la aplicación para los usuarios y, a continuación, almacenar en caché los valores necesarios del evento que la aplicación recibe `conversationUpdate` tras la instalación.</span><span class="sxs-lookup"><span data-stu-id="cb634-185">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="cb634-186">Solo puede instalar aplicaciones que se encuentran en el catálogo de aplicaciones de su organización o en la tienda de aplicaciones de Teams.</span><span class="sxs-lookup"><span data-stu-id="cb634-186">You can only install apps that are in your organizational app catalog or the Teams app store.</span></span>

<span data-ttu-id="cb634-187">Consulte [Instalar aplicaciones para usuarios en la](/graph/api/userteamwork-post-installedapps) documentación de Graph e instalación proactiva de bots y mensajes en Teams con Microsoft [Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="cb634-187">See [Install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="cb634-188">También hay un ejemplo [de Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) en la plataforma GitHub.</span><span class="sxs-lookup"><span data-stu-id="cb634-188">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="cb634-189">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="cb634-189">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="cb634-190">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cb634-190">C#/.NET</span></span>](#tab/dotnet)

```csharp
[Route("api/notify")]
[ApiController]
public class NotifyController : ControllerBase
{
    private readonly IBotFrameworkHttpAdapter _adapter;
    private readonly string _appId;
    private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

    public NotifyController(IBotFrameworkHttpAdapter adapter, IConfiguration configuration, ConcurrentDictionary<string, ConversationReference> conversationReferences)
    {
        _adapter = adapter;
        _conversationReferences = conversationReferences;
        _appId = configuration["MicrosoftAppId"] ?? string.Empty;
    }

    public async Task<IActionResult> Get()
    {
        foreach (var conversationReference in _conversationReferences.Values)
        {
            await ((BotAdapter)_adapter).ContinueConversationAsync(_appId, conversationReference, BotCallback, default(CancellationToken));
        }
        
        // Let the caller know proactive messages have been sent
        return new ContentResult()
        {
            Content = "<html><body><h1>Proactive messages have been sent.</h1></body></html>",
            ContentType = "text/html",
            StatusCode = (int)HttpStatusCode.OK,
        };
    }

    private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
    {
        // If you encounter permission-related errors when sending this message, see
        // https://aka.ms/BotTrustServiceUrl
        await turnContext.SendActivityAsync("proactive hello");
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="cb634-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="cb634-191">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="cb634-192">Python</span><span class="sxs-lookup"><span data-stu-id="cb634-192">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="cb634-193">JSON</span><span class="sxs-lookup"><span data-stu-id="cb634-193">JSON</span></span>](#tab/json)

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

<span data-ttu-id="cb634-194">Debe proporcionar el identificador de usuario y el id. de inquilino.</span><span class="sxs-lookup"><span data-stu-id="cb634-194">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="cb634-195">Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta.</span><span class="sxs-lookup"><span data-stu-id="cb634-195">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a><span data-ttu-id="cb634-196">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="cb634-196">Code samples</span></span>

<span data-ttu-id="cb634-197">Los ejemplos oficiales de mensajería proactiva son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="cb634-197">The official proactive messaging samples are as follows:</span></span>

| <span data-ttu-id="cb634-198">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="cb634-198">Sample Name</span></span>           | <span data-ttu-id="cb634-199">Descripción</span><span class="sxs-lookup"><span data-stu-id="cb634-199">Description</span></span>                                                                      | <span data-ttu-id="cb634-200">.NET</span><span class="sxs-lookup"><span data-stu-id="cb634-200">.NET</span></span>    | <span data-ttu-id="cb634-201">JavaScript</span><span class="sxs-lookup"><span data-stu-id="cb634-201">JavaScript</span></span>   | <span data-ttu-id="cb634-202">Python</span><span class="sxs-lookup"><span data-stu-id="cb634-202">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="cb634-203">Conceptos básicos de la conversación de Teams</span><span class="sxs-lookup"><span data-stu-id="cb634-203">Teams Conversation Basics</span></span>  | <span data-ttu-id="cb634-204">Muestra los conceptos básicos de las conversaciones en Teams, incluido el envío de mensajes proactivos de uno a uno.</span><span class="sxs-lookup"><span data-stu-id="cb634-204">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="cb634-205">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="cb634-205">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="cb634-206">JavaScript</span><span class="sxs-lookup"><span data-stu-id="cb634-206">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="cb634-207">Python</span><span class="sxs-lookup"><span data-stu-id="cb634-207">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="cb634-208">Iniciar nuevo subproceso en un canal</span><span class="sxs-lookup"><span data-stu-id="cb634-208">Start new thread in a channel</span></span>     | <span data-ttu-id="cb634-209">Muestra cómo crear un nuevo subproceso en un canal.</span><span class="sxs-lookup"><span data-stu-id="cb634-209">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="cb634-210">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="cb634-210">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="cb634-211">JavaScript</span><span class="sxs-lookup"><span data-stu-id="cb634-211">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="cb634-212">Python</span><span class="sxs-lookup"><span data-stu-id="cb634-212">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a><span data-ttu-id="cb634-213">Ver ejemplos de código adicionales</span><span class="sxs-lookup"><span data-stu-id="cb634-213">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="cb634-214">**Ejemplos de código de mensajería proactiva de Teams**</span><span class="sxs-lookup"><span data-stu-id="cb634-214">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
