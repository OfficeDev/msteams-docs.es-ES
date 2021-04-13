---
title: enviar mensajes proactivos
description: describe cómo enviar mensajes proactivos con el bot de Microsoft Teams.
ms.topic: overview
ms.author: anclear
Keywords: enviar un mensaje obtener id. de usuario Id. id. de conversación de conversación
ms.openlocfilehash: 7da470eaba6ae9ecb82c9a7ba04d69b2f196a9d7
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654296"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="5e70d-104">Enviar mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="5e70d-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="5e70d-105">Un mensaje proactivo es cualquier mensaje enviado por un bot que no está en respuesta directa a una solicitud de un usuario.</span><span class="sxs-lookup"><span data-stu-id="5e70d-105">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="5e70d-106">Esto puede incluir mensajes como:</span><span class="sxs-lookup"><span data-stu-id="5e70d-106">This can include messages like:</span></span>

* <span data-ttu-id="5e70d-107">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="5e70d-107">Welcome messages</span></span>
* <span data-ttu-id="5e70d-108">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="5e70d-108">Notifications</span></span>
* <span data-ttu-id="5e70d-109">Mensajes programados</span><span class="sxs-lookup"><span data-stu-id="5e70d-109">Scheduled messages</span></span>

<span data-ttu-id="5e70d-110">Para que el bot envíe un mensaje proactivo, debe tener acceso al usuario, al chat de grupo o al equipo al que desea enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="5e70d-110">For your bot to send a proactive message, it must have access to the user, group chat, or team that you want to send the message to.</span></span> <span data-ttu-id="5e70d-111">Para un chat de grupo o un equipo, esto significa que la aplicación que contiene el bot debe instalarse en esa ubicación primero.</span><span class="sxs-lookup"><span data-stu-id="5e70d-111">For a group chat or team, this means the app that contains your bot must be installed to that location first.</span></span> <span data-ttu-id="5e70d-112">Puedes instalar [la aplicación de](#proactively-install-your-app-using-graph) forma proactiva con Graph [](/microsoftteams/teams-custom-app-policies-and-settings) en un equipo, si es necesario o usar una directiva de aplicación para enviar aplicaciones a equipos y usuarios de tu inquilino.</span><span class="sxs-lookup"><span data-stu-id="5e70d-112">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team, if required or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="5e70d-113">Para los usuarios, la aplicación debe estar instalada para el usuario o el usuario debe formar parte de un equipo donde esté instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e70d-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="5e70d-114">Enviar un mensaje proactivo es diferente al envío de un mensaje normal.</span><span class="sxs-lookup"><span data-stu-id="5e70d-114">Sending a proactive message is different than sending a regular message.</span></span> <span data-ttu-id="5e70d-115">En ese caso, no hay ningún activo `turnContext` que usar para una respuesta.</span><span class="sxs-lookup"><span data-stu-id="5e70d-115">In that, there is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="5e70d-116">Es posible que también necesite crear la conversación antes de enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="5e70d-116">You may also need to create the conversation before sending the message.</span></span> <span data-ttu-id="5e70d-117">Por ejemplo, un nuevo chat uno a uno o un nuevo hilo de conversación en un canal.</span><span class="sxs-lookup"><span data-stu-id="5e70d-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="5e70d-118">No puede crear un nuevo chat de grupo o un nuevo canal en un equipo con mensajería proactiva.</span><span class="sxs-lookup"><span data-stu-id="5e70d-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="5e70d-119">En un nivel alto, los pasos que deberá completar para enviar un mensaje proactivo son:</span><span class="sxs-lookup"><span data-stu-id="5e70d-119">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="5e70d-120">[Obtener el id. de usuario o el id. de equipo/canal](#get-the-user-id-or-teamchannel-id) (si es necesario).</span><span class="sxs-lookup"><span data-stu-id="5e70d-120">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="5e70d-121">[Cree el hilo de conversación o conversación](#create-the-conversation) (si es necesario).</span><span class="sxs-lookup"><span data-stu-id="5e70d-121">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="5e70d-122">[Obtener el identificador de conversación](#get-the-conversation-id).</span><span class="sxs-lookup"><span data-stu-id="5e70d-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="5e70d-123">[Enviar el mensaje](#send-the-message).</span><span class="sxs-lookup"><span data-stu-id="5e70d-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="5e70d-124">Los fragmentos de código de la [sección ejemplos](#examples) son para crear una conversación uno a uno.</span><span class="sxs-lookup"><span data-stu-id="5e70d-124">The code snippets in the [examples](#examples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="5e70d-125">Para obtener vínculos a ejemplos de trabajo completos para conversaciones de uno a uno y grupos o canales, vea [ejemplos de código](#code-samples).</span><span class="sxs-lookup"><span data-stu-id="5e70d-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code samples](#code-samples).</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="5e70d-126">Obtener el id. de usuario o el id. de equipo o canal</span><span class="sxs-lookup"><span data-stu-id="5e70d-126">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="5e70d-127">Para crear un nuevo hilo de conversación o conversación en un canal, necesita el identificador correcto.</span><span class="sxs-lookup"><span data-stu-id="5e70d-127">To create a new conversation or conversation thread in a channel, you need the correct ID.</span></span> <span data-ttu-id="5e70d-128">Puede recibir o recuperar este identificador de varias maneras:</span><span class="sxs-lookup"><span data-stu-id="5e70d-128">You can receive or retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="5e70d-129">Cuando la aplicación esté instalada en un contexto determinado, recibirás un [ `onMembersAdded` objeto Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="5e70d-129">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="5e70d-130">Cuando se agrega un nuevo usuario a un contexto donde está instalada la aplicación, recibirás un [ `onMembersAdded` objeto Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="5e70d-130">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="5e70d-131">Puedes recuperar la lista [de canales](~/bots/how-to/get-teams-context.md) de un equipo en el que está instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e70d-131">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="5e70d-132">Puedes recuperar la [lista de miembros](~/bots/how-to/get-teams-context.md) de un equipo que tiene instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e70d-132">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="5e70d-133">Cada actividad que reciba el bot debe contener la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="5e70d-133">Every Activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="5e70d-134">Independientemente de cómo obtenga la información, tendrá que almacenar la conversación o `tenantId` `userId` `channelId` crearla.</span><span class="sxs-lookup"><span data-stu-id="5e70d-134">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="5e70d-135">También puede usar el para crear un nuevo subproceso de conversación en el canal `teamId` general o predeterminado de un equipo.</span><span class="sxs-lookup"><span data-stu-id="5e70d-135">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="5e70d-136">El `userId` es único para el identificador de bot y un usuario determinado, no puede volver a usarlos entre bots.</span><span class="sxs-lookup"><span data-stu-id="5e70d-136">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="5e70d-137">Sin embargo, el bot es global y debe instalarse en el equipo para poder enviar un mensaje `channelId` proactivo a un canal.</span><span class="sxs-lookup"><span data-stu-id="5e70d-137">The `channelId` is global, however, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="5e70d-138">Crear la conversación</span><span class="sxs-lookup"><span data-stu-id="5e70d-138">Create the conversation</span></span>

<span data-ttu-id="5e70d-139">Después de tener la información del usuario o del canal, debe crear la conversación si aún no existe o si no conoce el `conversationId` archivo .</span><span class="sxs-lookup"><span data-stu-id="5e70d-139">After you have the user or channel information, you need to create the conversation if it doesn't already exist or you don't know the `conversationId`.</span></span> <span data-ttu-id="5e70d-140">Solo debe crear la conversación una vez y asegurarse de almacenar el valor u objeto que se va a `conversationId` `conversationReference` usar en el futuro.</span><span class="sxs-lookup"><span data-stu-id="5e70d-140">You must only create the conversation once and make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="5e70d-141">Obtener el identificador de conversación</span><span class="sxs-lookup"><span data-stu-id="5e70d-141">Get the conversation ID</span></span>

<span data-ttu-id="5e70d-142">Después de crear la conversación, use el `conversationReference` objeto o y envíe el `conversationId` `tenantId` mensaje.</span><span class="sxs-lookup"><span data-stu-id="5e70d-142">After the conversation is created, use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="5e70d-143">Puede obtener este identificador creando la conversación o almacenéndola desde cualquier actividad que se le envíe desde ese contexto.</span><span class="sxs-lookup"><span data-stu-id="5e70d-143">You can get this ID by either creating the conversation or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="5e70d-144">Asegúrese de almacenar este identificador.</span><span class="sxs-lookup"><span data-stu-id="5e70d-144">Make certain that you store this ID.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="5e70d-145">Enviar el mensaje</span><span class="sxs-lookup"><span data-stu-id="5e70d-145">Send the message</span></span>

<span data-ttu-id="5e70d-146">Ahora que tiene la información de dirección correcta, puede enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="5e70d-146">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="5e70d-147">Si usas el SDK, lo harás con el método y con y para realizar `continueConversation` una llamada directa a la `conversationId` `tenantId` API.</span><span class="sxs-lookup"><span data-stu-id="5e70d-147">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="5e70d-148">Debe establecer `conversationParameters` correctamente para enviar correctamente el mensaje.</span><span class="sxs-lookup"><span data-stu-id="5e70d-148">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="5e70d-149">Vea la [sección de](#examples) ejemplos o use uno de los ejemplos enumerados en la sección de [ejemplos de](#code-samples) código.</span><span class="sxs-lookup"><span data-stu-id="5e70d-149">See the [examples](#examples) section or use one of the samples listed in the [code samples](#code-samples) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="5e70d-150">Procedimientos recomendados para mensajería proactiva</span><span class="sxs-lookup"><span data-stu-id="5e70d-150">Best practices for proactive messaging</span></span>

<span data-ttu-id="5e70d-151">Enviar mensajes proactivos a los usuarios es una forma muy eficaz de comunicarse con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="5e70d-151">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="5e70d-152">Sin embargo, desde su punto de vista, este mensaje puede aparecer completamente sin respuesta y, en el caso de los mensajes de bienvenida, es la primera vez que interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e70d-152">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="5e70d-153">Por lo tanto, es muy importante usar esta funcionalidad con moderación, no enviar correo no deseado a los usuarios y proporcionar suficiente información para que los usuarios comprendan por qué se envían mensajes.</span><span class="sxs-lookup"><span data-stu-id="5e70d-153">Therefore, it is very important to use this functionality sparingly, don't spam your users, and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="5e70d-154">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="5e70d-154">Welcome messages</span></span>

<span data-ttu-id="5e70d-155">Al usar mensajes proactivos para enviar un mensaje de bienvenida a un usuario, debe tener en cuenta que, para la mayoría de las personas que reciben el mensaje, no hay contexto para el motivo de su recepción.</span><span class="sxs-lookup"><span data-stu-id="5e70d-155">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there is no context for why they are receiving it.</span></span> <span data-ttu-id="5e70d-156">También es la primera vez que interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e70d-156">This is also the first time they have interacted with your app.</span></span> <span data-ttu-id="5e70d-157">Es su oportunidad de crear una buena primera impresión.</span><span class="sxs-lookup"><span data-stu-id="5e70d-157">It is your opportunity to create a good first impression.</span></span> <span data-ttu-id="5e70d-158">Los mejores mensajes de bienvenida deben incluir:</span><span class="sxs-lookup"><span data-stu-id="5e70d-158">The best welcome messages must include:</span></span>

* <span data-ttu-id="5e70d-159">**Por qué un usuario recibe el mensaje.**</span><span class="sxs-lookup"><span data-stu-id="5e70d-159">**Why a user is receiving the message.**</span></span> <span data-ttu-id="5e70d-160">Debe ser muy claro para el usuario por qué está recibiendo el mensaje.</span><span class="sxs-lookup"><span data-stu-id="5e70d-160">It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="5e70d-161">Si el bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, hágles saber en qué canal se instaló y quién lo instaló.</span><span class="sxs-lookup"><span data-stu-id="5e70d-161">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="5e70d-162">**¿Qué ofrece?**</span><span class="sxs-lookup"><span data-stu-id="5e70d-162">**What do you offer.**</span></span> <span data-ttu-id="5e70d-163">¿Qué pueden hacer con la aplicación?</span><span class="sxs-lookup"><span data-stu-id="5e70d-163">What can they do with your app?</span></span> <span data-ttu-id="5e70d-164">¿Qué valor puede aportarles?</span><span class="sxs-lookup"><span data-stu-id="5e70d-164">What value can you bring to them?</span></span>
* <span data-ttu-id="5e70d-165">**Qué deben hacer a continuación.**</span><span class="sxs-lookup"><span data-stu-id="5e70d-165">**What should they do next.**</span></span> <span data-ttu-id="5e70d-166">Invítelos a probar un comando o interactuar con la aplicación de alguna manera.</span><span class="sxs-lookup"><span data-stu-id="5e70d-166">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="5e70d-167">Recuerde que los mensajes de bienvenida deficientes pueden provocar que los usuarios bloqueen el bot.</span><span class="sxs-lookup"><span data-stu-id="5e70d-167">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="5e70d-168">Dedica mucho tiempo a crear tus mensajes de bienvenida y recorre en iteración si no tienen el efecto deseado.</span><span class="sxs-lookup"><span data-stu-id="5e70d-168">Spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="5e70d-169">Mensajes de notificación</span><span class="sxs-lookup"><span data-stu-id="5e70d-169">Notification messages</span></span>

<span data-ttu-id="5e70d-170">Al usar la mensajería proactiva para enviar notificaciones, debe asegurarse de que los usuarios tienen una ruta de acceso clara para realizar acciones comunes en función de la notificación y una comprensión clara de por qué se produjo la notificación.</span><span class="sxs-lookup"><span data-stu-id="5e70d-170">When using proactive messaging to send notifications you must ensure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="5e70d-171">Por lo general, los mensajes de notificación de buena calidad incluyen:</span><span class="sxs-lookup"><span data-stu-id="5e70d-171">Good notification messages generally include:</span></span>

* <span data-ttu-id="5e70d-172">**Qué ha pasado.**</span><span class="sxs-lookup"><span data-stu-id="5e70d-172">**What happened.**</span></span> <span data-ttu-id="5e70d-173">Una indicación clara de lo que ocurrió para causar la notificación.</span><span class="sxs-lookup"><span data-stu-id="5e70d-173">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="5e70d-174">**Cuál fue el resultado.**</span><span class="sxs-lookup"><span data-stu-id="5e70d-174">**What was the result.**</span></span> <span data-ttu-id="5e70d-175">Debe estar claro qué elemento o cosa se actualizó para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="5e70d-175">It must be clear what item or thing was updated to cause the notification.</span></span>
* <span data-ttu-id="5e70d-176">**Quién o qué lo desencadenó.**</span><span class="sxs-lookup"><span data-stu-id="5e70d-176">**Who/what triggered it.**</span></span> <span data-ttu-id="5e70d-177">Quién o qué acción hizo que se enviara la notificación.</span><span class="sxs-lookup"><span data-stu-id="5e70d-177">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="5e70d-178">**Qué pueden hacer los usuarios en respuesta.**</span><span class="sxs-lookup"><span data-stu-id="5e70d-178">**What can users do in response.**</span></span> <span data-ttu-id="5e70d-179">Facilita a los usuarios realizar acciones en función de las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5e70d-179">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="5e70d-180">**Cómo pueden los usuarios optar por no participar.** Debe proporcionar una ruta de acceso para que los usuarios no puedan participar en notificaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="5e70d-180">**How can users opt out.** You must provide a path for users to opt out of additional notifications.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="5e70d-181">Mensajes programados</span><span class="sxs-lookup"><span data-stu-id="5e70d-181">Scheduled messages</span></span>

<span data-ttu-id="5e70d-182">Al usar la mensajería proactiva para enviar mensajes programados a los usuarios, compruebe que la zona horaria se actualiza a su zona horaria.</span><span class="sxs-lookup"><span data-stu-id="5e70d-182">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="5e70d-183">Esto garantiza que los mensajes se entreguen a los usuarios en el momento correspondiente.</span><span class="sxs-lookup"><span data-stu-id="5e70d-183">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="5e70d-184">Por lo general, los mensajes de programación incluyen:</span><span class="sxs-lookup"><span data-stu-id="5e70d-184">Schedule messages generally include:</span></span>

* <span data-ttu-id="5e70d-185">**Por qué el usuario recibe el mensaje:** Facilita que los usuarios comprendan el motivo por el que están recibiendo el mensaje.</span><span class="sxs-lookup"><span data-stu-id="5e70d-185">**Why is the user receiving the message**: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="5e70d-186">**Qué puede hacer el usuario a continuación:** los usuarios pueden realizar la acción necesaria en función del contenido del mensaje.</span><span class="sxs-lookup"><span data-stu-id="5e70d-186">**What can user do next**: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="5e70d-187">Instalar proactivamente la aplicación con Graph</span><span class="sxs-lookup"><span data-stu-id="5e70d-187">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="5e70d-188">Actualmente, la instalación proactiva de aplicaciones con Microsoft Graph está en versión beta.</span><span class="sxs-lookup"><span data-stu-id="5e70d-188">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="5e70d-189">En ocasiones, es posible que sea necesario enviar mensajes de forma proactiva a los usuarios que no han instalado o interactuado con la aplicación anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5e70d-189">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="5e70d-190">Por ejemplo, desea usar el comunicador de la compañía [para](~/samples/app-templates.md#company-communicator) enviar mensajes a toda la organización.</span><span class="sxs-lookup"><span data-stu-id="5e70d-190">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="5e70d-191">Para este escenario, puedes usar la API de Graph para instalar proactivamente la aplicación para los usuarios y, a continuación, almacenar en caché los valores necesarios del evento que la `conversationUpdate` aplicación recibe al instalarla.</span><span class="sxs-lookup"><span data-stu-id="5e70d-191">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="5e70d-192">Solo puedes instalar aplicaciones que estén en el catálogo de aplicaciones de la organización o en la tienda de aplicaciones de Teams.</span><span class="sxs-lookup"><span data-stu-id="5e70d-192">You can only install apps that are in your organizational app catalog or the Teams app store.</span></span>

<span data-ttu-id="5e70d-193">Consulta [Instalar aplicaciones para usuarios en](/graph/api/userteamwork-post-installedapps) la documentación de Graph y La instalación y mensajería proactiva de [bots en Teams con Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="5e70d-193">See [Install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="5e70d-194">También hay un ejemplo [de Microsoft .NET framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) en la plataforma GitHub.</span><span class="sxs-lookup"><span data-stu-id="5e70d-194">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="5e70d-195">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5e70d-195">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="5e70d-196">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="5e70d-196">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="5e70d-197">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="5e70d-197">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="5e70d-198">Python</span><span class="sxs-lookup"><span data-stu-id="5e70d-198">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="5e70d-199">JSON</span><span class="sxs-lookup"><span data-stu-id="5e70d-199">JSON</span></span>](#tab/json)

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

<span data-ttu-id="5e70d-200">Debe proporcionar el identificador de usuario y el identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="5e70d-200">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="5e70d-201">Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta.</span><span class="sxs-lookup"><span data-stu-id="5e70d-201">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a><span data-ttu-id="5e70d-202">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="5e70d-202">Code samples</span></span>

<span data-ttu-id="5e70d-203">Los ejemplos de mensajería proactiva oficiales son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="5e70d-203">The official proactive messaging samples are as follows:</span></span>

| <span data-ttu-id="5e70d-204">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5e70d-204">Sample Name</span></span>           | <span data-ttu-id="5e70d-205">Descripción</span><span class="sxs-lookup"><span data-stu-id="5e70d-205">Description</span></span>                                                                      | <span data-ttu-id="5e70d-206">.NET</span><span class="sxs-lookup"><span data-stu-id="5e70d-206">.NET</span></span>    | <span data-ttu-id="5e70d-207">JavaScript</span><span class="sxs-lookup"><span data-stu-id="5e70d-207">JavaScript</span></span>   | <span data-ttu-id="5e70d-208">Python</span><span class="sxs-lookup"><span data-stu-id="5e70d-208">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="5e70d-209">Conceptos básicos de la conversación de Teams</span><span class="sxs-lookup"><span data-stu-id="5e70d-209">Teams Conversation Basics</span></span>  | <span data-ttu-id="5e70d-210">Muestra los conceptos básicos de las conversaciones en Teams, incluido el envío de mensajes proactivos de uno a uno.</span><span class="sxs-lookup"><span data-stu-id="5e70d-210">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="5e70d-211">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="5e70d-211">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="5e70d-212">JavaScript</span><span class="sxs-lookup"><span data-stu-id="5e70d-212">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="5e70d-213">Python</span><span class="sxs-lookup"><span data-stu-id="5e70d-213">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="5e70d-214">Iniciar nuevo subproceso en un canal</span><span class="sxs-lookup"><span data-stu-id="5e70d-214">Start new thread in a channel</span></span>     | <span data-ttu-id="5e70d-215">Muestra la creación de un nuevo subproceso en un canal.</span><span class="sxs-lookup"><span data-stu-id="5e70d-215">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="5e70d-216">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="5e70d-216">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="5e70d-217">JavaScript</span><span class="sxs-lookup"><span data-stu-id="5e70d-217">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="5e70d-218">Python</span><span class="sxs-lookup"><span data-stu-id="5e70d-218">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a><span data-ttu-id="5e70d-219">Ver ejemplos de código adicionales</span><span class="sxs-lookup"><span data-stu-id="5e70d-219">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5e70d-220">**Ejemplos de código de mensajería proactiva de Teams**</span><span class="sxs-lookup"><span data-stu-id="5e70d-220">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
