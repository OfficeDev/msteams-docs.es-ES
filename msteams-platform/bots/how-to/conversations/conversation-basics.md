---
title: Conceptos básicos de la conversación
description: Introducción a las conversaciones
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: conversations basics messages
ms.openlocfilehash: c06f8765ae17f28f3abb1dff67d77aad4e76958c
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020038"
---
# <a name="conversation-basics"></a><span data-ttu-id="5be88-103">Conceptos básicos de la conversación</span><span class="sxs-lookup"><span data-stu-id="5be88-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="5be88-104">Una conversación es una serie de mensajes enviados entre el bot de Microsoft Teams y uno o varios usuarios.</span><span class="sxs-lookup"><span data-stu-id="5be88-104">A conversation is a series of messages sent between your Microsoft Teams bot and one or more users.</span></span> <span data-ttu-id="5be88-105">En la tabla siguiente se proporcionan los tres tipos de conversaciones, también denominadas ámbitos en Teams:</span><span class="sxs-lookup"><span data-stu-id="5be88-105">The following table provides the three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="5be88-106">Tipo de conversación</span><span class="sxs-lookup"><span data-stu-id="5be88-106">Conversation type</span></span> | <span data-ttu-id="5be88-107">Descripción</span><span class="sxs-lookup"><span data-stu-id="5be88-107">Description</span></span> |
| ------- | ----------- |
| `channel` | <span data-ttu-id="5be88-108">Este tipo de conversación es visible para todos los miembros del canal.</span><span class="sxs-lookup"><span data-stu-id="5be88-108">This conversation type is visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="5be88-109">Este tipo de conversación incluye conversaciones entre bots y un solo usuario.</span><span class="sxs-lookup"><span data-stu-id="5be88-109">This conversation type includes conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="5be88-110">Este tipo de conversación incluye chat entre un bot y dos o más usuarios.</span><span class="sxs-lookup"><span data-stu-id="5be88-110">This conversation type includes chat between a bot and two or more users.</span></span> <span data-ttu-id="5be88-111">También habilita el bot en chats de reunión.</span><span class="sxs-lookup"><span data-stu-id="5be88-111">It also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="5be88-112">Un bot se comporta de forma diferente en función de la conversación en la que esté implicado:</span><span class="sxs-lookup"><span data-stu-id="5be88-112">A bot behaves differently depending on the conversation it is involved in:</span></span>

* <span data-ttu-id="5be88-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span><span class="sxs-lookup"><span data-stu-id="5be88-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="5be88-114">Los bots de una conversación uno a uno no requieren una mención @.</span><span class="sxs-lookup"><span data-stu-id="5be88-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="5be88-115">Todos los mensajes enviados por el usuario se enrutan al bot.</span><span class="sxs-lookup"><span data-stu-id="5be88-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="5be88-116">Para que el bot funcione en una conversación o ámbito en particular, agregue compatibilidad a ese ámbito en el manifiesto [de la aplicación](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5be88-116">For the bot to work in a particular conversation or scope, add support to that scope in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

<span data-ttu-id="5be88-117">Cada mensaje de una conversación de bot es `Activity` un objeto de tipo `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="5be88-117">Each message in a bot conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="5be88-118">Cuando un usuario envía un mensaje, Teams publica el mensaje en el bot y el bot controla el mensaje.</span><span class="sxs-lookup"><span data-stu-id="5be88-118">When a user sends a message, Teams posts the message to your bot and the bot handles the message.</span></span> <span data-ttu-id="5be88-119">Además, para definir los comandos principales a los que responde el bot, puede agregar un menú de comandos con una lista desplegable de comandos para el bot.</span><span class="sxs-lookup"><span data-stu-id="5be88-119">In addition, to define core commands that your bot responds to, you can add a command menu with a drop-down list of commands for your bot.</span></span> <span data-ttu-id="5be88-120">Los bots de un grupo o canal solo reciben mensajes cuando se mencionan @botname.</span><span class="sxs-lookup"><span data-stu-id="5be88-120">Bots in a group or channel only receive messages when they are mentioned @botname.</span></span> <span data-ttu-id="5be88-121">Teams envía notificaciones al bot para eventos de conversación que se suceden en ámbitos donde el bot está activo.</span><span class="sxs-lookup"><span data-stu-id="5be88-121">Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="5be88-122">Puede capturar estos eventos en el código y realizar acciones en ellos.</span><span class="sxs-lookup"><span data-stu-id="5be88-122">You can capture these events in your code and take action on them.</span></span> 

<span data-ttu-id="5be88-123">Un bot también puede enviar mensajes proactivos a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="5be88-123">A bot can also send proactive messages to users.</span></span> <span data-ttu-id="5be88-124">Un mensaje proactivo es cualquier mensaje enviado por un bot que no responde a una solicitud de un usuario.</span><span class="sxs-lookup"><span data-stu-id="5be88-124">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="5be88-125">Puedes dar formato a los mensajes del bot para que incluyan tarjetas enriquecciones que incluyan elementos interactivos, como botones, texto, imágenes, audio, vídeo, entre otros.</span><span class="sxs-lookup"><span data-stu-id="5be88-125">You can format your bot messages to include rich cards that include interactive elements, such as buttons, text, images, audio, video, and so on.</span></span> <span data-ttu-id="5be88-126">Bot puede actualizar dinámicamente los mensajes después de enviarlos, en lugar de tener los mensajes como instantáneas estáticas de datos.</span><span class="sxs-lookup"><span data-stu-id="5be88-126">Bot can dynamically update messages after sending them, instead of having your messages as static snapshots of data.</span></span> <span data-ttu-id="5be88-127">Los mensajes también se pueden eliminar mediante el método de Bot `DeleteActivity` Framework.</span><span class="sxs-lookup"><span data-stu-id="5be88-127">Messages can also be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

## <a name="next-step"></a><span data-ttu-id="5be88-128">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="5be88-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5be88-129">Mensajes en conversaciones de bot</span><span class="sxs-lookup"><span data-stu-id="5be88-129">Messages in bot conversations</span></span>](~/bots/how-to/conversations/conversation-messages.md)
