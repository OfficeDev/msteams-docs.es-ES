---
title: Enviar y recibir mensajes con un bot
description: Describe cómo enviar y recibir mensajes con bots en Microsoft Teams.
keywords: mensajes de los bots de Microsoft Teams
ms.date: 05/20/2019
ms.openlocfilehash: 864473c7f502d96987a48e5837840236c45f59c7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676199"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="109a7-104">Tener una conversación con un bot de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="109a7-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="109a7-105">Una conversación es una serie de mensajes enviados entre el bot y uno o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="109a7-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="109a7-106">Hay tres tipos de conversaciones (también denominadas ámbitos) en Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="109a7-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="109a7-107">`teams`También se denominan conversaciones de canal, visibles para todos los miembros del canal.</span><span class="sxs-lookup"><span data-stu-id="109a7-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="109a7-108">`personal`Conversaciones entre bots y un único usuario.</span><span class="sxs-lookup"><span data-stu-id="109a7-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="109a7-109">`groupChat`Chatear entre un bot y dos o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="109a7-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="109a7-110">Un bot tiene un comportamiento ligeramente diferente en función del tipo de conversación en el que esté involucrado:</span><span class="sxs-lookup"><span data-stu-id="109a7-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="109a7-111">Los [bots en conversaciones de chat en el grupo y en el canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) requieren al usuario que mencione el bot para invocarlo en un canal.</span><span class="sxs-lookup"><span data-stu-id="109a7-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="109a7-112">Los [bots en conversaciones de usuario único](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) no necesitan @ mencionar: el usuario simplemente puede escribir.</span><span class="sxs-lookup"><span data-stu-id="109a7-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @ mention -  the user can just type.</span></span>

<span data-ttu-id="109a7-113">Para que el bot funcione en un ámbito determinado, debe aparecer como compatible con ese ámbito en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="109a7-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="109a7-114">Los ámbitos se definen y explican con más detalle en la [Referencia del manifiesto](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="109a7-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="109a7-115">Mensajes proactivos</span><span class="sxs-lookup"><span data-stu-id="109a7-115">Proactive messages</span></span>

<span data-ttu-id="109a7-116">Los bots pueden participar en una conversación o iniciar una.</span><span class="sxs-lookup"><span data-stu-id="109a7-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="109a7-117">La mayor parte de la comunicación está en respuesta a otro mensaje.</span><span class="sxs-lookup"><span data-stu-id="109a7-117">Most communication is in response to another message.</span></span> <span data-ttu-id="109a7-118">Si un bot inicia una conversación, se denomina *mensaje proactivo*.</span><span class="sxs-lookup"><span data-stu-id="109a7-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="109a7-119">Algunos ejemplos son:</span><span class="sxs-lookup"><span data-stu-id="109a7-119">Examples include:</span></span>

* <span data-ttu-id="109a7-120">Mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="109a7-120">Welcome messages</span></span>
* <span data-ttu-id="109a7-121">Notificaciones de eventos</span><span class="sxs-lookup"><span data-stu-id="109a7-121">Event notifications</span></span>
* <span data-ttu-id="109a7-122">Mensajes de sondeo</span><span class="sxs-lookup"><span data-stu-id="109a7-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="109a7-123">Conceptos básicos de la conversación</span><span class="sxs-lookup"><span data-stu-id="109a7-123">Conversation basics</span></span>

<span data-ttu-id="109a7-124">Cada mensaje es un `Activity` objeto de tipo `messageType: message`.</span><span class="sxs-lookup"><span data-stu-id="109a7-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="109a7-125">Cuando un usuario envía un mensaje, Microsoft Teams expone el mensaje a su bot; en concreto, envía un objeto JSON al extremo de mensajería de bot.</span><span class="sxs-lookup"><span data-stu-id="109a7-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="109a7-126">El bot examina el mensaje para determinar su tipo y responde en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="109a7-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="109a7-127">Los bots también admiten mensajes de estilo de evento.</span><span class="sxs-lookup"><span data-stu-id="109a7-127">Bots also support event-style messages.</span></span> <span data-ttu-id="109a7-128">Consulte [administrar eventos de bot en Microsoft Teams](~/resources/bot-v3/bots-notifications.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="109a7-128">See [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md) for more details.</span></span> <span data-ttu-id="109a7-129">Actualmente no se admite la voz.</span><span class="sxs-lookup"><span data-stu-id="109a7-129">Speech is currently not supported.</span></span>

<span data-ttu-id="109a7-130">Los mensajes son, en su mayoría, iguales en todos los ámbitos, pero hay diferencias en el modo en que se tiene acceso a bot en la interfaz de usuario y las diferencias entre bastidores que necesitará conocer.</span><span class="sxs-lookup"><span data-stu-id="109a7-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="109a7-131">La conversación básica se controla a través del conector de bot Framework, una única API de REST para permitir que su bot se comunique con Microsoft Teams y otros canales.</span><span class="sxs-lookup"><span data-stu-id="109a7-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="109a7-132">El SDK de bot Builder proporciona acceso sencillo a esta API, funcionalidad adicional para administrar el flujo de conversaciones y el estado, y formas sencillas de incorporar servicios cognitivos como el procesamiento de lenguaje natural (NLP).</span><span class="sxs-lookup"><span data-stu-id="109a7-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="109a7-133">Contenido del mensaje</span><span class="sxs-lookup"><span data-stu-id="109a7-133">Message content</span></span>

<span data-ttu-id="109a7-134">El bot puede enviar texto enriquecido, imágenes y tarjetas.</span><span class="sxs-lookup"><span data-stu-id="109a7-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="109a7-135">Los usuarios pueden enviar texto enriquecido e imágenes a su bot.</span><span class="sxs-lookup"><span data-stu-id="109a7-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="109a7-136">Puede especificar el tipo de contenido que puede controlar el bot en la página de configuración de Microsoft Teams de su bot.</span><span class="sxs-lookup"><span data-stu-id="109a7-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="109a7-137">Formato</span><span class="sxs-lookup"><span data-stu-id="109a7-137">Format</span></span> | <span data-ttu-id="109a7-138">De un usuario a un bot</span><span class="sxs-lookup"><span data-stu-id="109a7-138">From user to bot</span></span>  | <span data-ttu-id="109a7-139">De bot a User</span><span class="sxs-lookup"><span data-stu-id="109a7-139">From bot to user</span></span> |  <span data-ttu-id="109a7-140">Notas</span><span class="sxs-lookup"><span data-stu-id="109a7-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="109a7-141">Texto enriquecido </span><span class="sxs-lookup"><span data-stu-id="109a7-141">Rich text</span></span> | <span data-ttu-id="109a7-142">✔</span><span class="sxs-lookup"><span data-stu-id="109a7-142">✔</span></span> | <span data-ttu-id="109a7-143">✔</span><span class="sxs-lookup"><span data-stu-id="109a7-143">✔</span></span> |  |
| <span data-ttu-id="109a7-144">Imágenes</span><span class="sxs-lookup"><span data-stu-id="109a7-144">Pictures</span></span> | <span data-ttu-id="109a7-145">✔</span><span class="sxs-lookup"><span data-stu-id="109a7-145">✔</span></span> | <span data-ttu-id="109a7-146">✔</span><span class="sxs-lookup"><span data-stu-id="109a7-146">✔</span></span> | <span data-ttu-id="109a7-147">Máximo de 1024 × 1024 y 1 MB en formato PNG, JPEG o GIF; no se admiten GIF animados</span><span class="sxs-lookup"><span data-stu-id="109a7-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span> |
| <span data-ttu-id="109a7-148">Tarjetas</span><span class="sxs-lookup"><span data-stu-id="109a7-148">Cards</span></span> | <span data-ttu-id="109a7-149">✖</span><span class="sxs-lookup"><span data-stu-id="109a7-149">✖</span></span> | <span data-ttu-id="109a7-150">✔</span><span class="sxs-lookup"><span data-stu-id="109a7-150">✔</span></span> | <span data-ttu-id="109a7-151">Ver la [referencia de la tarjeta Teams](~/task-modules-and-cards/cards/cards-reference.md) para tarjetas compatibles</span><span class="sxs-lookup"><span data-stu-id="109a7-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="109a7-152">Emojis</span><span class="sxs-lookup"><span data-stu-id="109a7-152">Emojis</span></span> | <span data-ttu-id="109a7-153">✖</span><span class="sxs-lookup"><span data-stu-id="109a7-153">✖</span></span> | <span data-ttu-id="109a7-154">✔</span><span class="sxs-lookup"><span data-stu-id="109a7-154">✔</span></span> | <span data-ttu-id="109a7-155">Actualmente, los equipos son compatibles con emojis mediante UTF-16 (como U + 1F600 para la cara Grinning).</span><span class="sxs-lookup"><span data-stu-id="109a7-155">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span> |
|

<span data-ttu-id="109a7-156">Para obtener más información acerca de los tipos de interacción de bot admitidos por el marco de robots (en el que se basan los bots en Teams), vea la documentación sobre el [flujo](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) de la conversación y los conceptos relacionados en la documentación del [SDK de bot Builder para .net](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) y [el SDK del generador de robots para node. js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="109a7-156">For more information on the types of bot interaction supported by the Bot Framework (which bots in teams are based on), see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="109a7-157">Formato de mensajes</span><span class="sxs-lookup"><span data-stu-id="109a7-157">Message formatting</span></span>

<span data-ttu-id="109a7-158">Puede establecer la propiedad Optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) de `message` a para controlar cómo se representa el contenido de texto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="109a7-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="109a7-159">Vea [Message Formatting](~/resources/bot-v3/bots-message-format.md) para obtener una descripción detallada del formato admitido en los mensajes de bot.</span><span class="sxs-lookup"><span data-stu-id="109a7-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="109a7-160">Puede establecer la propiedad opcional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) para controlar cómo se representa el contenido de texto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="109a7-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="109a7-161">Para obtener información detallada sobre cómo Teams admite el formato de texto en Teams, vea [Text Formatting Text messages in Bot messages](~/resources/bot-v3/bots-text-formats.md).</span><span class="sxs-lookup"><span data-stu-id="109a7-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="109a7-162">Para obtener información sobre cómo dar formato a las tarjetas de los mensajes, vea [formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md).</span><span class="sxs-lookup"><span data-stu-id="109a7-162">For information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="109a7-163">Mensajes de imagen</span><span class="sxs-lookup"><span data-stu-id="109a7-163">Picture messages</span></span>

<span data-ttu-id="109a7-164">Las imágenes se envían agregando datos adjuntos a un mensaje.</span><span class="sxs-lookup"><span data-stu-id="109a7-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="109a7-165">Puede encontrar más información sobre los datos adjuntos en la [documentación de bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="109a7-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span></span>

<span data-ttu-id="109a7-166">Las imágenes pueden tener como máximo 1024 x 1024 y 1 MB en formato PNG, JPEG o GIF; GIF animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="109a7-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="109a7-167">Le recomendamos que especifique el alto y el ancho de cada imagen utilizando XML.</span><span class="sxs-lookup"><span data-stu-id="109a7-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="109a7-168">Si usa Markdown, el tamaño de imagen predeterminado es de 256 × 256.</span><span class="sxs-lookup"><span data-stu-id="109a7-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="109a7-169">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="109a7-169">For example:</span></span>

* <span data-ttu-id="109a7-170">Utilizados`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="109a7-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="109a7-171">No use `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="109a7-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages"></a><span data-ttu-id="109a7-172">Recibir mensajes</span><span class="sxs-lookup"><span data-stu-id="109a7-172">Receiving messages</span></span>

<span data-ttu-id="109a7-173">Dependiendo de los ámbitos que se declaren, el bot puede recibir mensajes en los siguientes contextos:</span><span class="sxs-lookup"><span data-stu-id="109a7-173">Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id="109a7-174">**chat personal** Los usuarios pueden interactuar en una conversación privada con un bot seleccionando el bot agregado en el historial de chats o escribiendo su nombre o identificador de aplicación en el cuadro para: de un nuevo chat.</span><span class="sxs-lookup"><span data-stu-id="109a7-174">**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id="109a7-175">**Canales** Un bot puede mencionarse ("@_botname_") en un canal si se ha agregado al equipo.</span><span class="sxs-lookup"><span data-stu-id="109a7-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="109a7-176">Tenga en cuenta que las respuestas adicionales a un bot en un canal requieren la mención del bot.</span><span class="sxs-lookup"><span data-stu-id="109a7-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="109a7-177">No responderá a las respuestas en las que no se haya mencionado.</span><span class="sxs-lookup"><span data-stu-id="109a7-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="109a7-178">Para los mensajes entrantes, el bot [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) recibe un objeto `messageType: message`de tipo.</span><span class="sxs-lookup"><span data-stu-id="109a7-178">For incoming messages, your bot receives an [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) object of type `messageType: message`.</span></span> <span data-ttu-id="109a7-179">Aunque el `Activity` objeto puede contener otros tipos de información, como [las actualizaciones de canal](~/resources/bot-v3/bots-notifications.md#channel-updates) enviadas a su `message` bot, el tipo representa la comunicación entre el bot y el usuario.</span><span class="sxs-lookup"><span data-stu-id="109a7-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="109a7-180">El bot recibe una carga que contiene el mensaje `Text` de usuario, así como otra información sobre el usuario, el origen del mensaje y la información de los equipos.</span><span class="sxs-lookup"><span data-stu-id="109a7-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="109a7-181">De Nota:</span><span class="sxs-lookup"><span data-stu-id="109a7-181">Of note:</span></span>

* <span data-ttu-id="109a7-182">`timestamp`La fecha y la hora del mensaje en la hora universal coordinada (UTC)</span><span class="sxs-lookup"><span data-stu-id="109a7-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC)</span></span>
* <span data-ttu-id="109a7-183">`localTimestamp`La fecha y la hora del mensaje en la zona horaria del remitente</span><span class="sxs-lookup"><span data-stu-id="109a7-183">`localTimestamp` The date and time of the message in the time zone of the sender</span></span>
* <span data-ttu-id="109a7-184">`channelId`Siempre es "msteams".</span><span class="sxs-lookup"><span data-stu-id="109a7-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="109a7-185">Se refiere a un canal del marco de bot, no a un canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="109a7-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="109a7-186">`from.id`Un identificador único y cifrado para el usuario de su bot; adecuado como clave si la aplicación necesita almacenar datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="109a7-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="109a7-187">Es único para el bot y no se puede usar directamente fuera de la instancia de bot de ninguna forma significativa para identificar al usuario</span><span class="sxs-lookup"><span data-stu-id="109a7-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user</span></span>
* <span data-ttu-id="109a7-188">`channelData.tenant.id`El identificador de inquilino del usuario.</span><span class="sxs-lookup"><span data-stu-id="109a7-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="109a7-189">`from.id`es único para el bot y no se puede usar directamente fuera de la instancia de bot de ninguna forma significativa para identificar a ese usuario.</span><span class="sxs-lookup"><span data-stu-id="109a7-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="109a7-190">Combinación de interacciones de canal y privado con el bot</span><span class="sxs-lookup"><span data-stu-id="109a7-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="109a7-191">Al interactuar en un canal, el bot debe ser inteligente al poner en línea ciertas conversaciones con un usuario.</span><span class="sxs-lookup"><span data-stu-id="109a7-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="109a7-192">Por ejemplo, supongamos que un usuario intenta coordinar una tarea compleja, como la programación con un conjunto de miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="109a7-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="109a7-193">En lugar de tener la secuencia completa de interacciones visibles para el canal, considere la posibilidad de enviar un mensaje de chat personal al usuario.</span><span class="sxs-lookup"><span data-stu-id="109a7-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="109a7-194">El bot debe poder realizar una transición sencilla al usuario entre conversaciones personales y de canal sin perder el estado.</span><span class="sxs-lookup"><span data-stu-id="109a7-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="109a7-195">No olvide actualizar el canal cuando la interacción se haya completado para notificar a los demás miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="109a7-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="109a7-196">Ejemplo de esquema entrante completo</span><span class="sxs-lookup"><span data-stu-id="109a7-196">Full inbound schema example</span></span>

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
> <span data-ttu-id="109a7-197">El campo de texto de los mensajes entrantes a veces contiene menciones.</span><span class="sxs-lookup"><span data-stu-id="109a7-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="109a7-198">Asegúrese de comprobarlos y eliminarlos correctamente.</span><span class="sxs-lookup"><span data-stu-id="109a7-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="109a7-199">Para obtener más información, vea [menciones](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span><span class="sxs-lookup"><span data-stu-id="109a7-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="109a7-200">Datos del canal de Teams</span><span class="sxs-lookup"><span data-stu-id="109a7-200">Teams channel data</span></span>

<span data-ttu-id="109a7-201">El `channelData` objeto contiene información específica de Microsoft Teams y es la fuente definitiva de los identificadores de equipo y de canal.</span><span class="sxs-lookup"><span data-stu-id="109a7-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="109a7-202">Debe almacenar en caché y usar estos identificadores como claves para el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="109a7-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="109a7-203">El `channelData` objeto no está incluido en los mensajes de las conversaciones personales, ya que éstos tienen lugar fuera de cualquier canal.</span><span class="sxs-lookup"><span data-stu-id="109a7-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="109a7-204">Un objeto channelData típico de una actividad enviada a su bot contiene la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="109a7-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="109a7-205">`eventType`Tipo de evento de Teams; solo se pasa en casos de [eventos de modificación de canal](~/resources/bot-v3/bots-notifications.md#channel-updates)</span><span class="sxs-lookup"><span data-stu-id="109a7-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates)</span></span>
* <span data-ttu-id="109a7-206">`tenant.id`IDENTIFICADOR de inquilino de Azure Active Directory; se pasan en todos los contextos</span><span class="sxs-lookup"><span data-stu-id="109a7-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="109a7-207">`team`Solo se pasa en contextos de canal, no en chat personal.</span><span class="sxs-lookup"><span data-stu-id="109a7-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="109a7-208">`id`GUID para el canal</span><span class="sxs-lookup"><span data-stu-id="109a7-208">`id` GUID for the channel</span></span>
  * <span data-ttu-id="109a7-209">`name`Nombre del equipo; solo se pasa en casos de [eventos de cambio de nombre de equipo](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span><span class="sxs-lookup"><span data-stu-id="109a7-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span></span>
* <span data-ttu-id="109a7-210">`channel`Solo se pasa en contextos de canal cuando se menciona el bot o para eventos en los canales en equipos en los que se ha agregado el bot</span><span class="sxs-lookup"><span data-stu-id="109a7-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="109a7-211">`id`GUID para el canal</span><span class="sxs-lookup"><span data-stu-id="109a7-211">`id` GUID for the channel</span></span>
  * <span data-ttu-id="109a7-212">`name`Nombre del canal; se pasa solo en casos de [eventos de modificación de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).</span><span class="sxs-lookup"><span data-stu-id="109a7-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="109a7-213">`channelData.teamsTeamId`En desuso.</span><span class="sxs-lookup"><span data-stu-id="109a7-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="109a7-214">Esta propiedad se incluye únicamente para la compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="109a7-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="109a7-215">`channelData.teamsChannelId`En desuso.</span><span class="sxs-lookup"><span data-stu-id="109a7-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="109a7-216">Esta propiedad se incluye únicamente para la compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="109a7-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="109a7-217">Ejemplo de objeto channelData (evento channelCreated)</span><span class="sxs-lookup"><span data-stu-id="109a7-217">Example channelData object (channelCreated event)</span></span>

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

### <a name="net-example"></a><span data-ttu-id="109a7-218">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="109a7-218">.NET example</span></span>

<span data-ttu-id="109a7-219">El paquete NuGet [Microsoft. bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) proporciona un `TeamsChannelData` objeto especializado, que expone propiedades para obtener acceso a información específica de Teams.</span><span class="sxs-lookup"><span data-stu-id="109a7-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="109a7-220">Enviar respuestas a mensajes</span><span class="sxs-lookup"><span data-stu-id="109a7-220">Sending replies to messages</span></span>

<span data-ttu-id="109a7-221">Para responder a un mensaje existente, llame [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) a .net o [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) a node. js.</span><span class="sxs-lookup"><span data-stu-id="109a7-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) in Node.js.</span></span> <span data-ttu-id="109a7-222">El SDK de bot Builder controla todos los detalles.</span><span class="sxs-lookup"><span data-stu-id="109a7-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="109a7-223">Si decide usar la API de REST, también puede llamar al punto de [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) conexión.</span><span class="sxs-lookup"><span data-stu-id="109a7-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) endpoint.</span></span>

<span data-ttu-id="109a7-224">El contenido del mensaje puede contener texto simple o algunas de las [tarjetas y las acciones](~/task-modules-and-cards/cards/cards-actions.md)de la tarjeta suministradas con bot Framework.</span><span class="sxs-lookup"><span data-stu-id="109a7-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="109a7-225">Tenga en cuenta que en el esquema saliente siempre debe usar el mismo `serviceUrl` que el que recibió.</span><span class="sxs-lookup"><span data-stu-id="109a7-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="109a7-226">Tenga en cuenta que el valor `serviceUrl` de tiende a ser estable, pero puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="109a7-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="109a7-227">Cuando llega un nuevo mensaje, el bot debe comprobar su valor almacenado de `serviceUrl`.</span><span class="sxs-lookup"><span data-stu-id="109a7-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="109a7-228">Actualizar mensajes</span><span class="sxs-lookup"><span data-stu-id="109a7-228">Updating messages</span></span>

<span data-ttu-id="109a7-229">En lugar de que los mensajes sean instantáneas estáticas de los datos, el bot puede actualizar de forma dinámica los mensajes en línea después de enviarlos.</span><span class="sxs-lookup"><span data-stu-id="109a7-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="109a7-230">Puede usar actualizaciones de mensajes dinámicas para escenarios como sondeos de actualizaciones, modificación de acciones disponibles después de presionar un botón o cualquier otro cambio de estado asincrónico.</span><span class="sxs-lookup"><span data-stu-id="109a7-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="109a7-231">El nuevo mensaje no tiene que coincidir con el original en el tipo.</span><span class="sxs-lookup"><span data-stu-id="109a7-231">The new message need not match the original in type.</span></span> <span data-ttu-id="109a7-232">Por ejemplo, si el mensaje original contenía datos adjuntos, el nuevo mensaje puede ser un mensaje de texto simple.</span><span class="sxs-lookup"><span data-stu-id="109a7-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="109a7-233">Solo puede actualizar contenido enviado en diseños de carrusel y mensajes de datos adjuntos únicos.</span><span class="sxs-lookup"><span data-stu-id="109a7-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="109a7-234">No se admite el envío de actualizaciones a mensajes con varios datos adjuntos en el diseño de lista.</span><span class="sxs-lookup"><span data-stu-id="109a7-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="109a7-235">API REST</span><span class="sxs-lookup"><span data-stu-id="109a7-235">REST API</span></span>

<span data-ttu-id="109a7-236">Para emitir una actualización de mensaje, simplemente realice una solicitud PUT contra `/v3/conversations/<conversationId>/activities/<activityId>/` el extremo con un identificador de actividad determinado.</span><span class="sxs-lookup"><span data-stu-id="109a7-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="109a7-237">Para completar este escenario, debe almacenar en caché el identificador de actividad devuelto por la llamada de publicación original.</span><span class="sxs-lookup"><span data-stu-id="109a7-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="109a7-238">Ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="109a7-238">.NET example</span></span>

<span data-ttu-id="109a7-239">Puede usar el `UpdateActivityAsync` método en el SDK del generador de robots para actualizar un mensaje existente.</span><span class="sxs-lookup"><span data-stu-id="109a7-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

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

### <a name="nodejs-example"></a><span data-ttu-id="109a7-240">Ejemplo de node. js</span><span class="sxs-lookup"><span data-stu-id="109a7-240">Node.js example</span></span>

<span data-ttu-id="109a7-241">Puede usar el `session.connector.update` método en el SDK del generador de robots para actualizar un mensaje existente.</span><span class="sxs-lookup"><span data-stu-id="109a7-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

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

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="109a7-242">Iniciar una conversación (mensajería proactiva)</span><span class="sxs-lookup"><span data-stu-id="109a7-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="109a7-243">Puede crear una conversación personal con un usuario o iniciar una nueva cadena de respuesta en un canal para su bot de equipo.</span><span class="sxs-lookup"><span data-stu-id="109a7-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="109a7-244">Esto le permite enviar un mensaje a su usuario o usuarios sin que ellos inicien primero contacto con su bot.</span><span class="sxs-lookup"><span data-stu-id="109a7-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="109a7-245">Para obtener más información, vea los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="109a7-245">For more information, see the following topics:</span></span>

<span data-ttu-id="109a7-246">Consulte [Mensajería proactiva de bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) para obtener más información general sobre las conversaciones iniciadas por bots.</span><span class="sxs-lookup"><span data-stu-id="109a7-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="109a7-247">Eliminación de mensajes</span><span class="sxs-lookup"><span data-stu-id="109a7-247">Deleting messages</span></span>

<span data-ttu-id="109a7-248">Los mensajes se pueden eliminar con el [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) método Connectors en el [SDK de BotBuilder](/bot-framework/bot-builder-overview-getstarted).</span><span class="sxs-lookup"><span data-stu-id="109a7-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

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
