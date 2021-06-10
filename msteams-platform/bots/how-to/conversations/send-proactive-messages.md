---
title: Enviar mensajes proactivos
description: Describe cómo enviar mensajes proactivos con el Microsoft Teams bot.
ms.topic: conceptual
ms.author: anclear
localization_priority: Normal
Keywords: enviar un mensaje obtener id. de usuario Id. id. de conversación de conversación
ms.openlocfilehash: ae651ac94b1b092374f6fae284b67070036b561f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020922"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="787cb-104">Enviar mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="787cb-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="787cb-105">Un mensaje proactivo es cualquier mensaje enviado por un bot que no responde a una solicitud de un usuario.</span><span class="sxs-lookup"><span data-stu-id="787cb-105">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="787cb-106">Esto puede incluir mensajes, como:</span><span class="sxs-lookup"><span data-stu-id="787cb-106">This can include messages, such as:</span></span>

* <span data-ttu-id="787cb-107">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="787cb-107">Welcome messages</span></span>
* <span data-ttu-id="787cb-108">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="787cb-108">Notifications</span></span>
* <span data-ttu-id="787cb-109">Mensajes programados</span><span class="sxs-lookup"><span data-stu-id="787cb-109">Scheduled messages</span></span>

<span data-ttu-id="787cb-110">Para que el bot envíe un mensaje proactivo a un usuario, chat de grupo o equipo, debe tener acceso para enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-110">For your bot to send a proactive message to a user, group chat, or team, it must have access to send the message.</span></span> <span data-ttu-id="787cb-111">Para un chat de grupo o un equipo, la aplicación que contiene el bot debe instalarse primero en esa ubicación.</span><span class="sxs-lookup"><span data-stu-id="787cb-111">For a group chat or team, the app that contains your bot must be first installed in that location.</span></span> <span data-ttu-id="787cb-112">Puedes instalar [proactivamente](#proactively-install-your-app-using-graph) la aplicación con Microsoft Graph en un equipo, [](/microsoftteams/teams-custom-app-policies-and-settings) si es necesario, o usar una directiva de aplicación para enviar aplicaciones a equipos y usuarios de tu inquilino.</span><span class="sxs-lookup"><span data-stu-id="787cb-112">You can [proactively install your app using Microsoft Graph](#proactively-install-your-app-using-graph) in a team, if required, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="787cb-113">Para los usuarios, la aplicación debe estar instalada para el usuario o el usuario debe formar parte de un equipo donde esté instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="787cb-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="787cb-114">Enviar un mensaje proactivo es diferente del envío de un mensaje normal.</span><span class="sxs-lookup"><span data-stu-id="787cb-114">Sending a proactive message is different from sending a regular message.</span></span> <span data-ttu-id="787cb-115">No hay ningún activo `turnContext` que usar para una respuesta.</span><span class="sxs-lookup"><span data-stu-id="787cb-115">There is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="787cb-116">Debe crear la conversación antes de enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-116">You must create the conversation before sending the message.</span></span> <span data-ttu-id="787cb-117">Por ejemplo, un nuevo chat uno a uno o un nuevo hilo de conversación en un canal.</span><span class="sxs-lookup"><span data-stu-id="787cb-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="787cb-118">No puede crear un nuevo chat de grupo o un nuevo canal en un equipo con mensajería proactiva.</span><span class="sxs-lookup"><span data-stu-id="787cb-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="787cb-119">**Para enviar un mensaje proactivo**</span><span class="sxs-lookup"><span data-stu-id="787cb-119">**To send a proactive message**</span></span>

1. <span data-ttu-id="787cb-120">[Obtiene el id. de usuario, id. de equipo o id. de canal,](#get-the-user-id-team-id-or-channel-id)si es necesario.</span><span class="sxs-lookup"><span data-stu-id="787cb-120">[Get the user ID, team ID, or channel ID](#get-the-user-id-team-id-or-channel-id), if required.</span></span>
1. <span data-ttu-id="787cb-121">[Cree la conversación](#create-the-conversation), si es necesario.</span><span class="sxs-lookup"><span data-stu-id="787cb-121">[Create the conversation](#create-the-conversation), if required.</span></span>
1. <span data-ttu-id="787cb-122">[Obtener el identificador de conversación](#get-the-conversation-id).</span><span class="sxs-lookup"><span data-stu-id="787cb-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="787cb-123">[Enviar el mensaje](#send-the-message).</span><span class="sxs-lookup"><span data-stu-id="787cb-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="787cb-124">Los fragmentos de código de la [sección samples](#samples) son para crear una conversación uno a uno.</span><span class="sxs-lookup"><span data-stu-id="787cb-124">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="787cb-125">Para ver los vínculos a ejemplos de trabajo completos para conversaciones uno a uno y grupos o canales, vea [el ejemplo de código](#code-sample).</span><span class="sxs-lookup"><span data-stu-id="787cb-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code sample](#code-sample).</span></span>

<span data-ttu-id="787cb-126">Para usar mensajes proactivos de forma eficaz, vea [procedimientos recomendados para la mensajería proactiva.](#best-practices-for-proactive-messaging)</span><span class="sxs-lookup"><span data-stu-id="787cb-126">For using proactive messages effectively, see [best practices for proactive messaging](#best-practices-for-proactive-messaging).</span></span> <span data-ttu-id="787cb-127">Para determinados escenarios, debes [instalar proactivamente la aplicación con Graph](#proactively-install-your-app-using-graph).</span><span class="sxs-lookup"><span data-stu-id="787cb-127">For certain scenarios, you must [proactively install your app using Graph](#proactively-install-your-app-using-graph).</span></span> <span data-ttu-id="787cb-128">Los fragmentos de código de la [sección samples](#samples) son para crear una conversación uno a uno.</span><span class="sxs-lookup"><span data-stu-id="787cb-128">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="787cb-129">Para obtener ejemplos de trabajo completos para conversaciones uno a uno y grupos o canales, vea [el ejemplo de código](#code-sample).</span><span class="sxs-lookup"><span data-stu-id="787cb-129">For complete working samples for both one-to-one conversations and groups or channels, see [code sample](#code-sample).</span></span>

## <a name="get-the-user-id-team-id-or-channel-id"></a><span data-ttu-id="787cb-130">Obtener el id. de usuario, id. de equipo o id. de canal</span><span class="sxs-lookup"><span data-stu-id="787cb-130">Get the user ID, team ID or channel ID</span></span>

<span data-ttu-id="787cb-131">Para crear un nuevo hilo de conversación o conversación en un canal, debe tener el identificador correcto.</span><span class="sxs-lookup"><span data-stu-id="787cb-131">To create a new conversation or conversation thread in a channel, you must have the correct ID.</span></span> <span data-ttu-id="787cb-132">Puede recibir o recuperar este identificador con cualquiera de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="787cb-132">You can receive or retrieve this ID using any of the following:</span></span>

* <span data-ttu-id="787cb-133">Cuando la aplicación está instalada en un contexto determinado, recibes una [ `onMembersAdded` actividad](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="787cb-133">When your app is installed in any particular context, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="787cb-134">Cuando se agrega un nuevo usuario a un contexto donde está instalada la aplicación, recibes una [ `onMembersAdded` actividad](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="787cb-134">When a new user is added to a context where your app is installed, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="787cb-135">Puedes recuperar la [lista de canales](~/bots/how-to/get-teams-context.md) de un equipo donde está instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="787cb-135">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team where your app is installed.</span></span>
* <span data-ttu-id="787cb-136">Puedes recuperar la [lista de miembros](~/bots/how-to/get-teams-context.md) de un equipo donde está instalada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="787cb-136">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team where your app is installed.</span></span>
* <span data-ttu-id="787cb-137">Cada actividad que recibe el bot debe contener la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="787cb-137">Every activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="787cb-138">Independientemente de cómo obtenga la información, debe almacenar el o para `tenantId` `userId` crear una nueva `channelId` conversación.</span><span class="sxs-lookup"><span data-stu-id="787cb-138">Regardless of how you get the information, you must store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="787cb-139">También puede usar el para crear un nuevo subproceso de conversación en el canal `teamId` general o predeterminado de un equipo.</span><span class="sxs-lookup"><span data-stu-id="787cb-139">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="787cb-140">El `userId` es único para el identificador del bot y un usuario en particular.</span><span class="sxs-lookup"><span data-stu-id="787cb-140">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="787cb-141">No puede volver a usar `userId` los bots entre.</span><span class="sxs-lookup"><span data-stu-id="787cb-141">You cannot reuse the `userId` between bots.</span></span> <span data-ttu-id="787cb-142">El `channelId` es global.</span><span class="sxs-lookup"><span data-stu-id="787cb-142">The `channelId` is global.</span></span> <span data-ttu-id="787cb-143">Sin embargo, el bot debe instalarse en el equipo para poder enviar un mensaje proactivo a un canal.</span><span class="sxs-lookup"><span data-stu-id="787cb-143">However, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

<span data-ttu-id="787cb-144">Después de tener la información del usuario o del canal, debe crear la conversación.</span><span class="sxs-lookup"><span data-stu-id="787cb-144">After you have the user or channel information, you must create the conversation.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="787cb-145">Crear la conversación</span><span class="sxs-lookup"><span data-stu-id="787cb-145">Create the conversation</span></span>

<span data-ttu-id="787cb-146">Debe crear la conversación si no existe o si no conoce el `conversationId` archivo .</span><span class="sxs-lookup"><span data-stu-id="787cb-146">You must create the conversation if it does not exist or you do not know the `conversationId`.</span></span> <span data-ttu-id="787cb-147">Solo debe crear la conversación una vez y almacenar el `conversationId` valor u `conversationReference` objeto.</span><span class="sxs-lookup"><span data-stu-id="787cb-147">You must only create the conversation once and store the `conversationId` value or `conversationReference` object.</span></span>

<span data-ttu-id="787cb-148">Después de crear la conversación, debe obtener el identificador de conversación.</span><span class="sxs-lookup"><span data-stu-id="787cb-148">After the conversation is created, you must get the conversation ID.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="787cb-149">Obtener el identificador de conversación</span><span class="sxs-lookup"><span data-stu-id="787cb-149">Get the conversation ID</span></span>

<span data-ttu-id="787cb-150">Use el `conversationReference` objeto o y envíe el `conversationId` `tenantId` mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-150">Use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="787cb-151">Para obtener este identificador, puede crear la conversación o almacenarla desde cualquier actividad que se le envíe desde ese contexto.</span><span class="sxs-lookup"><span data-stu-id="787cb-151">You can get this ID by either creating the conversation or storing it from any activity sent to you from that context.</span></span> <span data-ttu-id="787cb-152">Almacene este identificador como referencia.</span><span class="sxs-lookup"><span data-stu-id="787cb-152">Store this ID for reference.</span></span>

<span data-ttu-id="787cb-153">Después de obtener la información de dirección adecuada, puede enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-153">After you get the appropriate address information, you can send your message.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="787cb-154">Enviar el mensaje</span><span class="sxs-lookup"><span data-stu-id="787cb-154">Send the message</span></span>

<span data-ttu-id="787cb-155">Ahora que tiene la información de dirección correcta, puede enviar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-155">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="787cb-156">Si usas el SDK, lo harás con el método y con y para realizar `continueConversation` una llamada directa a la `conversationId` `tenantId` API.</span><span class="sxs-lookup"><span data-stu-id="787cb-156">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="787cb-157">Debe establecer `conversationParameters` correctamente para enviar correctamente el mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-157">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="787cb-158">Vea la [sección de](#samples) ejemplos o use uno de los ejemplos enumerados en la sección de [ejemplo de](#code-sample) código.</span><span class="sxs-lookup"><span data-stu-id="787cb-158">See the [samples](#samples) section or use one of the samples listed in the [code sample](#code-sample) section.</span></span>

<span data-ttu-id="787cb-159">Si usa el SDK, debe usar el método y la llamada a la API directa `continueConversation` `conversationId` para enviar el `tenantId` mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-159">If you are using the SDK, you must use the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call to send the message.</span></span> <span data-ttu-id="787cb-160">Debe establecer `conversationParameters` correctamente para enviar correctamente el mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-160">You must set the `conversationParameters` correctly to successfully send your message.</span></span>

<span data-ttu-id="787cb-161">Ahora que ha enviado el mensaje proactivo, debe seguir estos procedimientos recomendados mientras envía mensajes proactivos para un mejor intercambio de información entre los usuarios y el bot.</span><span class="sxs-lookup"><span data-stu-id="787cb-161">Now that you have sent the proactive message, you must follow these best practices while sending proactive messages for better information exchange between users and the bot.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="787cb-162">Procedimientos recomendados para mensajería proactiva</span><span class="sxs-lookup"><span data-stu-id="787cb-162">Best practices for proactive messaging</span></span>

<span data-ttu-id="787cb-163">Enviar mensajes proactivos a los usuarios es una forma muy eficaz de comunicarse con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="787cb-163">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="787cb-164">Sin embargo, desde su punto de vista, este mensaje puede aparecer completamente sin respuesta y, en el caso de los mensajes de bienvenida, es la primera vez que interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="787cb-164">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="787cb-165">Por lo tanto, es muy importante usar la mensajería proactiva con moderación, no enviar correo no deseado a los usuarios y proporcionar suficiente información para que los usuarios comprendan por qué están recibiendo los mensajes.</span><span class="sxs-lookup"><span data-stu-id="787cb-165">Therefore, it is very important to use proactive messaging sparingly, not spam your users, and provide enough information to let users understand why they are receiving the messages.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="787cb-166">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="787cb-166">Welcome messages</span></span>

<span data-ttu-id="787cb-167">Cuando se usa la mensajería proactiva para enviar un mensaje de bienvenida a un usuario, no hay contexto para la razón por la que los usuarios reciben el mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-167">When proactive messaging is used to send a welcome message to a user, there is no context for why the users receive the message.</span></span> <span data-ttu-id="787cb-168">También es la primera vez que los usuarios interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="787cb-168">This is also the first time users interact with your app.</span></span> <span data-ttu-id="787cb-169">Es una oportunidad para crear una buena primera impresión.</span><span class="sxs-lookup"><span data-stu-id="787cb-169">It is an opportunity to create a good first impression.</span></span> <span data-ttu-id="787cb-170">Los mejores mensajes de bienvenida deben incluir:</span><span class="sxs-lookup"><span data-stu-id="787cb-170">The best welcome messages must include:</span></span>

* <span data-ttu-id="787cb-171">Por qué un usuario recibe el mensaje: debe ser muy claro para el usuario por qué está recibiendo el mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-171">Why a user is receiving the message: It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="787cb-172">Si el bot se instaló en un canal y envió un mensaje de bienvenida a todos los usuarios, háles saber en qué canal se instaló y quién lo instaló.</span><span class="sxs-lookup"><span data-stu-id="787cb-172">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and who installed it.</span></span>
* <span data-ttu-id="787cb-173">Qué ofrece: los usuarios deben ser capaces de identificar lo que pueden hacer con la aplicación y qué valor puede aportarles.</span><span class="sxs-lookup"><span data-stu-id="787cb-173">What do you offer: Users must be able to identify what they can do with your app and what value can you bring to them.</span></span>
* <span data-ttu-id="787cb-174">Qué deben hacer a continuación: Invitar a los usuarios a probar un comando o interactuar con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="787cb-174">What should they do next: Invite users to try out a command, or interact with your app.</span></span>

<span data-ttu-id="787cb-175">Los mensajes de bienvenida deficientes pueden provocar que los usuarios bloqueen el bot.</span><span class="sxs-lookup"><span data-stu-id="787cb-175">Poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="787cb-176">Escribe en el punto y borra los mensajes de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="787cb-176">Write to the point and clear welcome messages.</span></span> <span data-ttu-id="787cb-177">Itera en los mensajes de bienvenida si no tienen el efecto deseado.</span><span class="sxs-lookup"><span data-stu-id="787cb-177">Iterate on the welcome messages if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="787cb-178">Mensajes de notificación</span><span class="sxs-lookup"><span data-stu-id="787cb-178">Notification messages</span></span>

<span data-ttu-id="787cb-179">Para enviar notificaciones mediante mensajería proactiva, asegúrese de que los usuarios tienen una ruta de acceso clara para realizar acciones comunes en función de la notificación.</span><span class="sxs-lookup"><span data-stu-id="787cb-179">To send notifications using proactive messaging, ensure your users have a clear path to take common actions based on your notification.</span></span> <span data-ttu-id="787cb-180">Asegúrese de que los usuarios comprendan claramente por qué han recibido una notificación.</span><span class="sxs-lookup"><span data-stu-id="787cb-180">Ensure users have a clear understanding of why they have received a notification.</span></span> <span data-ttu-id="787cb-181">Por lo general, los mensajes de notificación de buena calidad incluyen lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="787cb-181">Good notification messages generally include the following:</span></span>

* <span data-ttu-id="787cb-182">Qué ocurrió: una indicación clara de lo que ocurrió para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="787cb-182">What happened: A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="787cb-183">Cuál fue el resultado: debe estar claro qué elemento se actualizó para provocar la notificación.</span><span class="sxs-lookup"><span data-stu-id="787cb-183">What was the result: It must be clear what item was updated to cause the notification.</span></span>
* <span data-ttu-id="787cb-184">Quién o lo que lo desencadenó: Quién o qué acción llevó a que se enviara la notificación.</span><span class="sxs-lookup"><span data-stu-id="787cb-184">Who or what triggered it: Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="787cb-185">Qué pueden hacer los usuarios en respuesta: facilita que los usuarios realicen acciones en función de las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="787cb-185">What can users do in response: Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="787cb-186">Cómo pueden optar por no participar los usuarios: debe proporcionar una ruta de acceso para que los usuarios no puedan participar en notificaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="787cb-186">How can users opt-out: You must provide a path for users to opt-out of additional notifications.</span></span>

<span data-ttu-id="787cb-187">Para enviar mensajes a un gran grupo de usuarios, por ejemplo, a su organización, instale proactivamente la aplicación mediante Graph.</span><span class="sxs-lookup"><span data-stu-id="787cb-187">To send messages to a large group of users, for example to your organization, proactively install your app using Graph.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="787cb-188">Mensajes programados</span><span class="sxs-lookup"><span data-stu-id="787cb-188">Scheduled messages</span></span>

<span data-ttu-id="787cb-189">Al usar la mensajería proactiva para enviar mensajes programados a los usuarios, compruebe que la zona horaria se actualiza a su zona horaria.</span><span class="sxs-lookup"><span data-stu-id="787cb-189">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="787cb-190">Esto garantiza que los mensajes se entreguen a los usuarios en el momento correspondiente.</span><span class="sxs-lookup"><span data-stu-id="787cb-190">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="787cb-191">Por lo general, los mensajes de programación incluyen:</span><span class="sxs-lookup"><span data-stu-id="787cb-191">Schedule messages generally include:</span></span>

* <span data-ttu-id="787cb-192">¿Por qué recibe el usuario el mensaje?: Haga que sea fácil para los usuarios comprender el motivo por el que están recibiendo el mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-192">Why is the user receiving the message: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="787cb-193">Qué puede hacer el usuario a continuación: los usuarios pueden realizar la acción necesaria en función del contenido del mensaje.</span><span class="sxs-lookup"><span data-stu-id="787cb-193">What can user do next: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="787cb-194">Instale proactivamente la aplicación con Graph</span><span class="sxs-lookup"><span data-stu-id="787cb-194">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="787cb-195">La instalación proactiva de aplicaciones Graph está actualmente en versión beta.</span><span class="sxs-lookup"><span data-stu-id="787cb-195">Proactively installing apps using Graph is currently in beta.</span></span>

<span data-ttu-id="787cb-196">Envía un mensaje de forma proactiva a los usuarios que no han instalado o interactuado anteriormente con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="787cb-196">Proactively message users that have previously not installed or interacted with your app.</span></span> <span data-ttu-id="787cb-197">Por ejemplo, desea usar el comunicador de la compañía [para](~/samples/app-templates.md#company-communicator) enviar mensajes a toda la organización.</span><span class="sxs-lookup"><span data-stu-id="787cb-197">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="787cb-198">En este caso, puedes usar la API Graph para instalar proactivamente la aplicación para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="787cb-198">In this case, you can use the Graph API to proactively install your app for your users.</span></span> <span data-ttu-id="787cb-199">Almacena en caché los valores necesarios del `conversationUpdate` evento que la aplicación recibe al instalarlo.</span><span class="sxs-lookup"><span data-stu-id="787cb-199">Cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="787cb-200">Solo puedes instalar aplicaciones que estén en el catálogo de aplicaciones de la organización o en Teams App Store.</span><span class="sxs-lookup"><span data-stu-id="787cb-200">You can only install apps that are in your organizational app catalog or the Teams App Store.</span></span>

<span data-ttu-id="787cb-201">Consulta [instalar aplicaciones para usuarios en](/graph/api/userteamwork-post-installedapps) la documentación Graph y la instalación proactiva de [bots](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)y la mensajería en Teams con Graph .</span><span class="sxs-lookup"><span data-stu-id="787cb-201">See [install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [proactive bot installation and messaging in Teams with Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="787cb-202">También hay un ejemplo [de Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) en la plataforma GitHub.</span><span class="sxs-lookup"><span data-stu-id="787cb-202">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="samples"></a><span data-ttu-id="787cb-203">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="787cb-203">Samples</span></span>

<span data-ttu-id="787cb-204">El siguiente código muestra un ejemplo de código simple que instala proactivamente la aplicación mediante Graph:</span><span class="sxs-lookup"><span data-stu-id="787cb-204">The following code shows a simple code sample that proactively installs your app using Graph:</span></span>

# <a name="c"></a>[<span data-ttu-id="787cb-205">C#</span><span class="sxs-lookup"><span data-stu-id="787cb-205">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="787cb-206">TypeScript</span><span class="sxs-lookup"><span data-stu-id="787cb-206">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="787cb-207">Python</span><span class="sxs-lookup"><span data-stu-id="787cb-207">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="787cb-208">JSON</span><span class="sxs-lookup"><span data-stu-id="787cb-208">JSON</span></span>](#tab/json)

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

<span data-ttu-id="787cb-209">Debe proporcionar el identificador de usuario y el identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="787cb-209">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="787cb-210">Si la llamada se realiza correctamente, la API devuelve el siguiente objeto de respuesta:</span><span class="sxs-lookup"><span data-stu-id="787cb-210">If the call succeeds, the API returns the following response object:</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a><span data-ttu-id="787cb-211">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="787cb-211">Code sample</span></span>

<span data-ttu-id="787cb-212">En la tabla siguiente se proporciona un ejemplo de código simple que incorpora el flujo de conversación básico en una aplicación de Teams y cómo crear un nuevo subproceso de conversación en un canal en Teams:</span><span class="sxs-lookup"><span data-stu-id="787cb-212">The following table provides a simple code sample that incorporate basic conversation flow into a Teams application and how to create a new conversation thread in a channel in Teams:</span></span>

| <span data-ttu-id="787cb-213">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="787cb-213">**Sample Name**</span></span> | <span data-ttu-id="787cb-214">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="787cb-214">**Description**</span></span> | <span data-ttu-id="787cb-215">**.NET**</span><span class="sxs-lookup"><span data-stu-id="787cb-215">**.NET**</span></span> | <span data-ttu-id="787cb-216">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="787cb-216">**Node.js**</span></span> | <span data-ttu-id="787cb-217">**Python**</span><span class="sxs-lookup"><span data-stu-id="787cb-217">**Python**</span></span> |
|---------------|--------------|--------|-------------|--------|
| <span data-ttu-id="787cb-218">Teams Conceptos básicos de conversación</span><span class="sxs-lookup"><span data-stu-id="787cb-218">Teams Conversation Basics</span></span>  | <span data-ttu-id="787cb-219">Muestra los conceptos básicos de las conversaciones Teams, incluido el envío de mensajes proactivos de uno a uno.</span><span class="sxs-lookup"><span data-stu-id="787cb-219">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>| [<span data-ttu-id="787cb-220">View</span><span class="sxs-lookup"><span data-stu-id="787cb-220">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [<span data-ttu-id="787cb-221">View</span><span class="sxs-lookup"><span data-stu-id="787cb-221">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="787cb-222">View</span><span class="sxs-lookup"><span data-stu-id="787cb-222">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| <span data-ttu-id="787cb-223">Iniciar nuevo subproceso en un canal</span><span class="sxs-lookup"><span data-stu-id="787cb-223">Start new thread in a channel</span></span> | <span data-ttu-id="787cb-224">Muestra la creación de un nuevo subproceso en un canal.</span><span class="sxs-lookup"><span data-stu-id="787cb-224">Demonstrates creating a new thread in a channel.</span></span> | [<span data-ttu-id="787cb-225">View</span><span class="sxs-lookup"><span data-stu-id="787cb-225">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [<span data-ttu-id="787cb-226">View</span><span class="sxs-lookup"><span data-stu-id="787cb-226">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [<span data-ttu-id="787cb-227">View</span><span class="sxs-lookup"><span data-stu-id="787cb-227">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a><span data-ttu-id="787cb-228">Ejemplo de código adicional</span><span class="sxs-lookup"><span data-stu-id="787cb-228">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="787cb-229">Teams de código de mensajería proactiva</span><span class="sxs-lookup"><span data-stu-id="787cb-229">Teams proactive messaging code samples</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a><span data-ttu-id="787cb-230">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="787cb-230">Next step</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="787cb-231">[**Teams de código de mensajería proactiva**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp) 
>  [Dar formato a los mensajes del bot](~/bots/how-to/format-your-bot-messages.md)</span><span class="sxs-lookup"><span data-stu-id="787cb-231">[**Teams proactive messaging code samples**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
[Format your bot messages](~/bots/how-to/format-your-bot-messages.md)</span></span>
