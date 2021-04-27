---
title: Enviar y recibir mensajes con un bot
description: Describe cómo enviar y recibir mensajes con bots en Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: mensajes de bots de teams
ms.date: 05/20/2019
ms.openlocfilehash: 67dae46d0d34ff842d3fe6717f51e00ad4b8c80a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020670"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="7d934-104">Tener una conversación con un bot de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7d934-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="7d934-105">Una conversación es una serie de mensajes enviados entre el bot y uno o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="7d934-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="7d934-106">Hay tres tipos de conversaciones (también denominadas ámbitos) en Teams:</span><span class="sxs-lookup"><span data-stu-id="7d934-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="7d934-107">`teams` También se denomina conversaciones de canal, visibles para todos los miembros del canal.</span><span class="sxs-lookup"><span data-stu-id="7d934-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="7d934-108">`personal` Conversaciones entre bots y un solo usuario.</span><span class="sxs-lookup"><span data-stu-id="7d934-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="7d934-109">`groupChat` Chatear entre un bot y dos o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="7d934-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="7d934-110">Un bot se comporta de forma ligeramente diferente en función del tipo de conversación en la que esté implicado:</span><span class="sxs-lookup"><span data-stu-id="7d934-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="7d934-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @ mention the bot to invoke it in a channel.</span><span class="sxs-lookup"><span data-stu-id="7d934-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="7d934-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @ mention - the user can just type.</span><span class="sxs-lookup"><span data-stu-id="7d934-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @ mention -  the user can just type.</span></span>

<span data-ttu-id="7d934-113">Para que el bot funcione en un ámbito determinado, debe aparecer como compatible con ese ámbito en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="7d934-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="7d934-114">Los ámbitos se definen y se analizan más adelante en la [referencia de manifiesto](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7d934-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="7d934-115">Mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="7d934-115">Proactive messages</span></span>

<span data-ttu-id="7d934-116">Los bots pueden participar en una conversación o iniciar una.</span><span class="sxs-lookup"><span data-stu-id="7d934-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="7d934-117">La mayoría de la comunicación es en respuesta a otro mensaje.</span><span class="sxs-lookup"><span data-stu-id="7d934-117">Most communication is in response to another message.</span></span> <span data-ttu-id="7d934-118">Si un bot inicia una conversación, se denomina mensaje *proactivo*.</span><span class="sxs-lookup"><span data-stu-id="7d934-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="7d934-119">Algunos ejemplos son:</span><span class="sxs-lookup"><span data-stu-id="7d934-119">Examples include:</span></span>

* <span data-ttu-id="7d934-120">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="7d934-120">Welcome messages</span></span>
* <span data-ttu-id="7d934-121">Notificaciones de eventos</span><span class="sxs-lookup"><span data-stu-id="7d934-121">Event notifications</span></span>
* <span data-ttu-id="7d934-122">Mensajes de sondeo</span><span class="sxs-lookup"><span data-stu-id="7d934-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="7d934-123">Conceptos básicos de la conversación</span><span class="sxs-lookup"><span data-stu-id="7d934-123">Conversation basics</span></span>

<span data-ttu-id="7d934-124">Cada mensaje es un objeto `Activity` de tipo `messageType: message`.</span><span class="sxs-lookup"><span data-stu-id="7d934-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="7d934-125">Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot; en concreto, envía un objeto JSON al punto de conexión de mensajería del bot.</span><span class="sxs-lookup"><span data-stu-id="7d934-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="7d934-126">El bot examina el mensaje para determinar su tipo y responde en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="7d934-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="7d934-127">Los bots también admiten mensajes de estilo de evento.</span><span class="sxs-lookup"><span data-stu-id="7d934-127">Bots also support event-style messages.</span></span> <span data-ttu-id="7d934-128">Consulta [Controlar eventos de bot en Microsoft Teams](~/resources/bot-v3/bots-notifications.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="7d934-128">See [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md) for more details.</span></span> <span data-ttu-id="7d934-129">Actualmente, no se admite voz.</span><span class="sxs-lookup"><span data-stu-id="7d934-129">Speech is currently not supported.</span></span>

<span data-ttu-id="7d934-130">En la mayoría de los casos, los mensajes son iguales en todos los ámbitos, pero hay diferencias en la forma en que se accede al bot en la interfaz de usuario y diferencias entre bastidores que necesitarás conocer.</span><span class="sxs-lookup"><span data-stu-id="7d934-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="7d934-131">La conversación básica se controla a través de Bot Framework Connector, una única API de REST para permitir que el bot se comunique con Teams y otros canales.</span><span class="sxs-lookup"><span data-stu-id="7d934-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="7d934-132">El SDK de Bot Builder proporciona acceso fácil a esta API, funcionalidad adicional para administrar el estado y el flujo de conversación, y formas sencillas de incorporar servicios cognitivos como el procesamiento de lenguaje natural (NLP).</span><span class="sxs-lookup"><span data-stu-id="7d934-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="7d934-133">Contenido del mensaje</span><span class="sxs-lookup"><span data-stu-id="7d934-133">Message content</span></span>

<span data-ttu-id="7d934-134">El bot puede enviar texto enriquecido, imágenes y tarjetas.</span><span class="sxs-lookup"><span data-stu-id="7d934-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="7d934-135">Los usuarios pueden enviar texto enriquecido e imágenes al bot.</span><span class="sxs-lookup"><span data-stu-id="7d934-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="7d934-136">Puede especificar el tipo de contenido que el bot puede controlar en la página de configuración de Microsoft Teams para el bot.</span><span class="sxs-lookup"><span data-stu-id="7d934-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="7d934-137">Formato</span><span class="sxs-lookup"><span data-stu-id="7d934-137">Format</span></span> | <span data-ttu-id="7d934-138">De usuario a bot</span><span class="sxs-lookup"><span data-stu-id="7d934-138">From user to bot</span></span>  | <span data-ttu-id="7d934-139">De bot a usuario</span><span class="sxs-lookup"><span data-stu-id="7d934-139">From bot to user</span></span> |  <span data-ttu-id="7d934-140">Notas</span><span class="sxs-lookup"><span data-stu-id="7d934-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="7d934-141">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="7d934-141">Rich text</span></span> | <span data-ttu-id="7d934-142">✔</span><span class="sxs-lookup"><span data-stu-id="7d934-142">✔</span></span> | <span data-ttu-id="7d934-143">✔</span><span class="sxs-lookup"><span data-stu-id="7d934-143">✔</span></span> |  |
| <span data-ttu-id="7d934-144">Imágenes</span><span class="sxs-lookup"><span data-stu-id="7d934-144">Pictures</span></span> | <span data-ttu-id="7d934-145">✔</span><span class="sxs-lookup"><span data-stu-id="7d934-145">✔</span></span> | <span data-ttu-id="7d934-146">✔</span><span class="sxs-lookup"><span data-stu-id="7d934-146">✔</span></span> | <span data-ttu-id="7d934-147">Máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no se admite</span><span class="sxs-lookup"><span data-stu-id="7d934-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span> |
| <span data-ttu-id="7d934-148">Tarjetas</span><span class="sxs-lookup"><span data-stu-id="7d934-148">Cards</span></span> | <span data-ttu-id="7d934-149">✖</span><span class="sxs-lookup"><span data-stu-id="7d934-149">✖</span></span> | <span data-ttu-id="7d934-150">✔</span><span class="sxs-lookup"><span data-stu-id="7d934-150">✔</span></span> | <span data-ttu-id="7d934-151">Consulta referencia [de tarjetas de Teams](~/task-modules-and-cards/cards/cards-reference.md) para obtener tarjetas compatibles</span><span class="sxs-lookup"><span data-stu-id="7d934-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="7d934-152">Emojis</span><span class="sxs-lookup"><span data-stu-id="7d934-152">Emojis</span></span> | <span data-ttu-id="7d934-153">✖</span><span class="sxs-lookup"><span data-stu-id="7d934-153">✖</span></span> | <span data-ttu-id="7d934-154">✔</span><span class="sxs-lookup"><span data-stu-id="7d934-154">✔</span></span> | <span data-ttu-id="7d934-155">Teams actualmente admite emojis a través de UTF-16 (como U+1F600 para la cara sonriente)</span><span class="sxs-lookup"><span data-stu-id="7d934-155">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span> |
|

<span data-ttu-id="7d934-156">Para obtener más información sobre los tipos de interacción de bot compatibles con Bot Framework [](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) (en los que se basan los bots de teams), consulte la documentación de Bot Framework sobre el flujo de conversación y los conceptos relacionados en la documentación del SDK del generador de bots para [.NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) y el SDK de [Bot Builder ](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true)para Node.js.</span><span class="sxs-lookup"><span data-stu-id="7d934-156">For more information on the types of bot interaction supported by the Bot Framework (which bots in teams are based on), see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="7d934-157">Formato de mensajes</span><span class="sxs-lookup"><span data-stu-id="7d934-157">Message formatting</span></span>

<span data-ttu-id="7d934-158">Puede establecer la propiedad opcional de a para controlar cómo se representa el contenido de texto [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) `message` del mensaje.</span><span class="sxs-lookup"><span data-stu-id="7d934-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="7d934-159">Consulte [Formato de mensaje para](~/resources/bot-v3/bots-message-format.md) obtener una descripción detallada del formato admitido en los mensajes de bot.</span><span class="sxs-lookup"><span data-stu-id="7d934-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="7d934-160">Puede establecer la propiedad opcional para controlar cómo se representa el contenido de texto [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) del mensaje.</span><span class="sxs-lookup"><span data-stu-id="7d934-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="7d934-161">Para obtener información detallada sobre cómo Teams admite el formato de texto en equipos, vea [Formato de texto en mensajes de bot.](~/resources/bot-v3/bots-text-formats.md)</span><span class="sxs-lookup"><span data-stu-id="7d934-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="7d934-162">Para obtener información sobre el formato de tarjetas en mensajes, vea [Formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="7d934-162">For information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="7d934-163">Mensajes de imagen</span><span class="sxs-lookup"><span data-stu-id="7d934-163">Picture messages</span></span>

<span data-ttu-id="7d934-164">Las imágenes se envían agregando datos adjuntos a un mensaje.</span><span class="sxs-lookup"><span data-stu-id="7d934-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="7d934-165">Encontrará más información sobre los datos adjuntos en la [documentación de Bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="7d934-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span></span>

<span data-ttu-id="7d934-166">Las imágenes pueden tener como máximo 1024×1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="7d934-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="7d934-167">Se recomienda especificar el alto y el ancho de cada imagen mediante XML.</span><span class="sxs-lookup"><span data-stu-id="7d934-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="7d934-168">Si usa Markdown, el tamaño de la imagen tiene el valor predeterminado 256×256.</span><span class="sxs-lookup"><span data-stu-id="7d934-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="7d934-169">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7d934-169">For example:</span></span>

* <span data-ttu-id="7d934-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="7d934-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="7d934-171">No usar `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="7d934-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages&quot;></a><span data-ttu-id=&quot;7d934-172&quot;>Recepción de mensajes</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;7d934-172&quot;>Receiving messages</span></span>

<span data-ttu-id=&quot;7d934-173&quot;>Según los ámbitos declarados, el bot puede recibir mensajes en los siguientes contextos:</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;7d934-173&quot;>Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id=&quot;7d934-174&quot;>**chat personal** Los usuarios pueden interactuar en una conversación privada con un bot simplemente seleccionando el bot agregado en el historial de chat o escribiendo su nombre o identificador de aplicación en el cuadro Para: en un nuevo chat.</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;7d934-174&quot;>**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id=&quot;7d934-175&quot;>**Canales** Se puede mencionar un bot (&quot;@_botname")_ en un canal si se ha agregado al equipo.</span><span class="sxs-lookup"><span data-stu-id="7d934-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="7d934-176">Tenga en cuenta que las respuestas adicionales a un bot en un canal requieren mencionar el bot.</span><span class="sxs-lookup"><span data-stu-id="7d934-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="7d934-177">No responderá a las respuestas en las que no se menciona.</span><span class="sxs-lookup"><span data-stu-id="7d934-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="7d934-178">Para los mensajes entrantes, el bot recibe un [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) objeto de tipo `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="7d934-178">For incoming messages, your bot receives an [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) object of type `messageType: message`.</span></span> <span data-ttu-id="7d934-179">Aunque el objeto puede contener otros tipos de información, como las actualizaciones de canal enviadas al bot, el tipo representa la comunicación `Activity` entre bot y [](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` usuario.</span><span class="sxs-lookup"><span data-stu-id="7d934-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="7d934-180">El bot recibe una carga que contiene el mensaje de usuario, así como otra información sobre el usuario, el origen del mensaje `Text` y la información de Teams.</span><span class="sxs-lookup"><span data-stu-id="7d934-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="7d934-181">Nota:</span><span class="sxs-lookup"><span data-stu-id="7d934-181">Of note:</span></span>

* <span data-ttu-id="7d934-182">`timestamp` La fecha y hora del mensaje en la hora universal coordinada (UTC)</span><span class="sxs-lookup"><span data-stu-id="7d934-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC)</span></span>
* <span data-ttu-id="7d934-183">`localTimestamp` La fecha y hora del mensaje en la zona horaria del remitente</span><span class="sxs-lookup"><span data-stu-id="7d934-183">`localTimestamp` The date and time of the message in the time zone of the sender</span></span>
* <span data-ttu-id="7d934-184">`channelId` Siempre "msteams".</span><span class="sxs-lookup"><span data-stu-id="7d934-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="7d934-185">Esto hace referencia a un canal de marco de bot, no a un canal de teams.</span><span class="sxs-lookup"><span data-stu-id="7d934-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="7d934-186">`from.id` Un identificador único y cifrado para ese usuario para el bot; adecuado como clave si la aplicación necesita almacenar datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="7d934-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="7d934-187">Es único para el bot y no se puede usar directamente fuera de la instancia del bot de ninguna manera significativa para identificar a ese usuario</span><span class="sxs-lookup"><span data-stu-id="7d934-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user</span></span>
* <span data-ttu-id="7d934-188">`channelData.tenant.id` El identificador de inquilino del usuario.</span><span class="sxs-lookup"><span data-stu-id="7d934-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="7d934-189">`from.id` es único para el bot y no se puede usar directamente fuera de la instancia del bot de ninguna manera significativa para identificar a ese usuario.</span><span class="sxs-lookup"><span data-stu-id="7d934-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="7d934-190">Combinar interacciones privadas y de canal con el bot</span><span class="sxs-lookup"><span data-stu-id="7d934-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="7d934-191">Al interactuar en un canal, el bot debe ser inteligente para desconectar determinadas conversaciones con un usuario.</span><span class="sxs-lookup"><span data-stu-id="7d934-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="7d934-192">Por ejemplo, supongamos que un usuario está intentando coordinar una tarea compleja, como la programación con un conjunto de miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="7d934-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="7d934-193">En lugar de tener toda la secuencia de interacciones visible para el canal, considere la posibilidad de enviar un mensaje de chat personal al usuario.</span><span class="sxs-lookup"><span data-stu-id="7d934-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="7d934-194">El bot debe poder realizar una transición fácil al usuario entre conversaciones personales y de canal sin perder el estado.</span><span class="sxs-lookup"><span data-stu-id="7d934-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="7d934-195">No olvide actualizar el canal cuando se complete la interacción para notificar a los demás miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="7d934-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="7d934-196">Ejemplo de esquema entrante completo</span><span class="sxs-lookup"><span data-stu-id="7d934-196">Full inbound schema example</span></span>

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

> [!NOTE]
> <span data-ttu-id="7d934-197">El campo de texto de los mensajes entrantes a veces contiene menciones.</span><span class="sxs-lookup"><span data-stu-id="7d934-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="7d934-198">Asegúrese de comprobar y quitar los archivos correctamente.</span><span class="sxs-lookup"><span data-stu-id="7d934-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="7d934-199">Para obtener más información, vea [Menciones](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span><span class="sxs-lookup"><span data-stu-id="7d934-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="7d934-200">Datos del canal de Teams</span><span class="sxs-lookup"><span data-stu-id="7d934-200">Teams channel data</span></span>

<span data-ttu-id="7d934-201">El objeto contiene información específica de Teams y es el origen definitivo de `channelData` los IDs de equipo y canal.</span><span class="sxs-lookup"><span data-stu-id="7d934-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="7d934-202">Debe almacenar en caché y usar estos identificadores como claves para el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="7d934-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="7d934-203">El objeto no se incluye en los mensajes de las conversaciones personales, ya que se llevan a `channelData` cabo fuera de cualquier canal.</span><span class="sxs-lookup"><span data-stu-id="7d934-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="7d934-204">Un objeto channelData típico de una actividad enviada al bot contiene la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="7d934-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="7d934-205">`eventType` Tipo de evento teams; se pasa solo en casos de [eventos de modificación de canal](~/resources/bot-v3/bots-notifications.md#channel-updates)</span><span class="sxs-lookup"><span data-stu-id="7d934-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates)</span></span>
* <span data-ttu-id="7d934-206">`tenant.id` Identificador de inquilino de Azure Active Directory; pasado en todos los contextos</span><span class="sxs-lookup"><span data-stu-id="7d934-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="7d934-207">`team` Se pasa solo en contextos de canal, no en chat personal.</span><span class="sxs-lookup"><span data-stu-id="7d934-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="7d934-208">`id` GUID para el canal</span><span class="sxs-lookup"><span data-stu-id="7d934-208">`id` GUID for the channel</span></span>
  * <span data-ttu-id="7d934-209">`name` Nombre del equipo; se pasa solo en casos de [eventos de cambio de nombre de equipo](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span><span class="sxs-lookup"><span data-stu-id="7d934-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span></span>
* <span data-ttu-id="7d934-210">`channel` Se pasa solo en contextos de canal cuando se menciona el bot o para eventos en canales de equipos donde se ha agregado el bot</span><span class="sxs-lookup"><span data-stu-id="7d934-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="7d934-211">`id` GUID para el canal</span><span class="sxs-lookup"><span data-stu-id="7d934-211">`id` GUID for the channel</span></span>
  * <span data-ttu-id="7d934-212">`name` Nombre del canal; se pasa solo en casos de [eventos de modificación de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).</span><span class="sxs-lookup"><span data-stu-id="7d934-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="7d934-213">`channelData.teamsTeamId` En desuso.</span><span class="sxs-lookup"><span data-stu-id="7d934-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="7d934-214">Esta propiedad se incluye solo por compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="7d934-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="7d934-215">`channelData.teamsChannelId` En desuso.</span><span class="sxs-lookup"><span data-stu-id="7d934-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="7d934-216">Esta propiedad se incluye solo por compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="7d934-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="7d934-217">Objeto channelData de ejemplo (evento channelCreated)</span><span class="sxs-lookup"><span data-stu-id="7d934-217">Example channelData object (channelCreated event)</span></span>

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

### <a name="net-example"></a><span data-ttu-id="7d934-218">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="7d934-218">.NET example</span></span>

<span data-ttu-id="7d934-219">El [paquete NuGet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) proporciona un objeto especializado, que expone las propiedades para obtener acceso a `TeamsChannelData` información específica de Teams.</span><span class="sxs-lookup"><span data-stu-id="7d934-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="7d934-220">Enviar respuestas a mensajes</span><span class="sxs-lookup"><span data-stu-id="7d934-220">Sending replies to messages</span></span>

<span data-ttu-id="7d934-221">Para responder a un mensaje existente, llame [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) en .NET o [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) en Node.js.</span><span class="sxs-lookup"><span data-stu-id="7d934-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) in Node.js.</span></span> <span data-ttu-id="7d934-222">El SDK de Bot Builder controla todos los detalles.</span><span class="sxs-lookup"><span data-stu-id="7d934-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="7d934-223">Si elige usar la API de REST, también puede llamar al punto de [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) conexión.</span><span class="sxs-lookup"><span data-stu-id="7d934-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) endpoint.</span></span>

<span data-ttu-id="7d934-224">El contenido del mensaje en sí puede contener texto simple o algunas de las tarjetas y acciones de [tarjeta proporcionadas](~/task-modules-and-cards/cards/cards-actions.md)por Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="7d934-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="7d934-225">Tenga en cuenta que en el esquema saliente siempre debe usar lo mismo `serviceUrl` que el que recibió.</span><span class="sxs-lookup"><span data-stu-id="7d934-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="7d934-226">Tenga en cuenta que el valor `serviceUrl` de tiende a ser estable pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="7d934-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="7d934-227">Cuando llega un mensaje nuevo, el bot debe comprobar su valor almacenado de `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="7d934-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="7d934-228">Actualizar mensajes</span><span class="sxs-lookup"><span data-stu-id="7d934-228">Updating messages</span></span>

<span data-ttu-id="7d934-229">En lugar de hacer que los mensajes sean instantáneas estáticas de datos, el bot puede actualizar dinámicamente los mensajes en línea después de enviarlos.</span><span class="sxs-lookup"><span data-stu-id="7d934-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="7d934-230">Puede usar actualizaciones dinámicas de mensajes para escenarios como las actualizaciones de sondeo, la modificación de acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.</span><span class="sxs-lookup"><span data-stu-id="7d934-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="7d934-231">El nuevo mensaje no necesita coincidir con el tipo original.</span><span class="sxs-lookup"><span data-stu-id="7d934-231">The new message need not match the original in type.</span></span> <span data-ttu-id="7d934-232">Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.</span><span class="sxs-lookup"><span data-stu-id="7d934-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="7d934-233">Solo puede actualizar el contenido enviado en mensajes de datos adjuntos únicos y diseños de carrusel.</span><span class="sxs-lookup"><span data-stu-id="7d934-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="7d934-234">No se admite la publicación de actualizaciones en mensajes con varios datos adjuntos en el diseño de lista.</span><span class="sxs-lookup"><span data-stu-id="7d934-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="7d934-235">API REST</span><span class="sxs-lookup"><span data-stu-id="7d934-235">REST API</span></span>

<span data-ttu-id="7d934-236">Para emitir una actualización de mensaje, solo tiene que realizar una solicitud PUT en el `/v3/conversations/<conversationId>/activities/<activityId>/` extremo mediante un identificador de actividad determinado.</span><span class="sxs-lookup"><span data-stu-id="7d934-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="7d934-237">Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada POST original.</span><span class="sxs-lookup"><span data-stu-id="7d934-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="7d934-238">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="7d934-238">.NET example</span></span>

<span data-ttu-id="7d934-239">Puede usar el método `UpdateActivityAsync` en el SDK de Bot Builder para actualizar un mensaje existente.</span><span class="sxs-lookup"><span data-stu-id="7d934-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
  if (activity.Type == ActivityTypes.Message)
  {
    ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
    Activity reply = activity.CreateReply($"You sent {activity.Text} which was {activity.Text.Length} characters");
    var msgToUpdate = await connector.Conversations.ReplyToActivityAsync(reply);
    Activity updatedReply = activity.CreateReply($"This is an updated message");
    await connector.Conversations.UpdateActivityAsync(reply.Conversation.Id, msgToUpdate.Id, updatedReply);
  }
}
```

### <a name="nodejs-example"></a><span data-ttu-id="7d934-240">Node.js ejemplo</span><span class="sxs-lookup"><span data-stu-id="7d934-240">Node.js example</span></span>

<span data-ttu-id="7d934-241">Puede usar el método `session.connector.update` en el SDK de Bot Builder para actualizar un mensaje existente.</span><span class="sxs-lookup"><span data-stu-id="7d934-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

```javascript
function sendCardUpdate(bot, session, originalMessage, address) {

  var origAttachment = originalMessage.data.attachments[0];
  origAttachment.content.subtitle = 'Assigned to Larry Jin';

  var updatedMsg = new builder.Message()
    .address(address)
    .textFormat(builder.TextFormat.markdown)
    .addAttachment(origAttachment)
    .toMessage();

  session.connector.update(updatedMsg, function(err, addresses) {
    if (err) {
      console.log(`Could not update the message`);
    }
  });
}
```

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="7d934-242">Iniciar una conversación (mensajería proactiva)</span><span class="sxs-lookup"><span data-stu-id="7d934-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="7d934-243">Puedes crear una conversación personal con un usuario o iniciar una nueva cadena de respuesta en un canal para el bot de equipo.</span><span class="sxs-lookup"><span data-stu-id="7d934-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="7d934-244">Esto le permite enviar un mensaje a su usuario o usuarios sin que inicien el primer contacto con el bot.</span><span class="sxs-lookup"><span data-stu-id="7d934-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="7d934-245">Para obtener más información, consulte los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="7d934-245">For more information, see the following topics:</span></span>

<span data-ttu-id="7d934-246">Consulta [Mensajería proactiva para bots para](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) obtener más información general sobre las conversaciones iniciadas por bots.</span><span class="sxs-lookup"><span data-stu-id="7d934-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="7d934-247">Eliminación de mensajes</span><span class="sxs-lookup"><span data-stu-id="7d934-247">Deleting messages</span></span>

<span data-ttu-id="7d934-248">Los mensajes se pueden eliminar mediante el método connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) en el SDK de [BotBuilder](/bot-framework/bot-builder-overview-getstarted).</span><span class="sxs-lookup"><span data-stu-id="7d934-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

```typescript
bot.dialog('BotDeleteMessage', function (session: builder.Session) {
  var msg = new teams.TeamsMessage(session).text("Bot will delete this message in 5 sec.")
  bot.send(msg, function (err, response) {
    if (err) {
      console.log(err);
      session.endDialog();
    }

    console.log('Proactive message response:');
    console.log(response);
    console.log('---------------------------------------------------')
    setTimeout(function () {
      var activityId: string = null;
      var messageAddress: builder.IChatConnectorAddress = null;
      if (response[0]){
        messageAddress = response[0];
        activityId = messageAddress.id;
      }

      if (activityId == null)
      {
        console.log('Message failed to send.');
        session.endDialog();
        return;
      }

      // Bot delete message
      let address: builder.IChatConnectorAddress  = {
        channelId: 'msteams',
        user: messageAddress.user,
        bot: messageAddress.bot,
        id : activityId,
        serviceUrl : (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
        conversation: {
          id: session.message.address.conversation.id
        }
      };

      connector.delete(address, function (err) {
        if (err)
        {
          console.log(err);
        }
        else
        {
          console.log("Message: " + activityId + " deleted successfully.");
        }

        // Try editing deleted message would fail
        var newMsg = new builder.Message().address(address).text("To edit message.");
        connector.update(newMsg.toMessage(), function (err, address) {
          if (err)
          {
            console.log(err);
            console.log('Deleted message can not be edited.');
          }
          else
          {
            console.log("There is something wrong. Message: " + activityId + " edited successfully.");
            console.log(address);
          }

          session.endDialog();
        });
      });
    }, 5000);
  });
})
```
