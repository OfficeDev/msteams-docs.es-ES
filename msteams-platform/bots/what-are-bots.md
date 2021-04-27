---
title: Bots en Microsoft Teams
author: clearab
description: Una introducción a los bots en Microsoft Teams.
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 70240b7396fc5e7a77749dc4e7326bfb30ea4415
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020894"
---
# <a name="bots-in-microsoft-teams"></a><span data-ttu-id="6d352-103">Bots en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6d352-103">Bots in Microsoft Teams</span></span>

<span data-ttu-id="6d352-104">Un bot también conocido como bot de chat o bot de conversación es una aplicación que ejecuta tareas automatizadas simples y repetitivas realizadas por los usuarios, como el servicio de atención al cliente o el personal de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="6d352-104">A bot also referred to as a chatbot or conversational bot is an app that runs simple and repetitive automated tasks performed by the users, such as customer service or support staff.</span></span> <span data-ttu-id="6d352-105">Algunos ejemplos de bots de uso diario incluyen bots que proporcionan información sobre el tiempo, reservan la cena o proporcionan información de viaje.</span><span class="sxs-lookup"><span data-stu-id="6d352-105">Examples of bots in everyday use include, bots that provide information about the weather, make dinner reservations, or provide travel information.</span></span> <span data-ttu-id="6d352-106">Una interacción de bot puede ser una pregunta y una respuesta rápidas, o puede ser una conversación compleja que proporciona acceso a los servicios.</span><span class="sxs-lookup"><span data-stu-id="6d352-106">A bot interaction can be a quick question and answer, or it can be a complex conversation that provides access to services.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/zSIysk0yL0Q]

<span data-ttu-id="6d352-107">Los robots de conversación permiten que los usuarios interactúen con el servicio web mediante texto, tarjetas interactivas y módulos de tareas.</span><span class="sxs-lookup"><span data-stu-id="6d352-107">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span>

![Invocar bot con texto](~/assets/images/invokebotwithtext.png)

![Invocar bot con tarjeta](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

<span data-ttu-id="6d352-110">Los bots conversacionales son increíblemente flexibles y se pueden tener en cuenta para controlar algunos comandos simples o tareas complejas, basadas en inteligencia artificial y procesamiento de lenguaje natural.</span><span class="sxs-lookup"><span data-stu-id="6d352-110">Conversational bots are incredibly flexible and can be scoped to handle a few simple commands, or complex, artificial-intelligence-powered, and natural-language-processing tasks.</span></span> <span data-ttu-id="6d352-111">Pueden ser un aspecto de una aplicación más grande o ser completamente independientes.</span><span class="sxs-lookup"><span data-stu-id="6d352-111">They can be one aspect of a larger application, or be completely stand-alone.</span></span>

<span data-ttu-id="6d352-112">Encontrar la combinación adecuada de tarjetas, texto y módulos de tareas es clave para crear un bot útil.</span><span class="sxs-lookup"><span data-stu-id="6d352-112">Finding the right mix of cards, text, and task modules are key to create a useful bot.</span></span> <span data-ttu-id="6d352-113">En la siguiente imagen se muestra a un usuario conversando con un bot en un chat uno a uno con tarjetas interactivas y de texto:</span><span class="sxs-lookup"><span data-stu-id="6d352-113">The following image shows a user conversing with a bot in a one-to-one chat using both, text and interactive cards:</span></span>

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="Bot de preguntas frecuentes de ejemplo" border="true":::

<span data-ttu-id="6d352-115">Cada interacción entre el usuario y el bot se representa como una actividad.</span><span class="sxs-lookup"><span data-stu-id="6d352-115">Every interaction between the user and the bot is represented as an activity.</span></span> <span data-ttu-id="6d352-116">Cuando un bot recibe una actividad, la pasa a sus controladores de actividad.</span><span class="sxs-lookup"><span data-stu-id="6d352-116">When a bot receives an activity, it passes it on to its activity handlers.</span></span> <span data-ttu-id="6d352-117">Para obtener más información, vea [controladores de actividad de bot .](~/bots/bot-basics.md)</span><span class="sxs-lookup"><span data-stu-id="6d352-117">For more information, see [bot activity handlers](~/bots/bot-basics.md).</span></span> 

<span data-ttu-id="6d352-118">Además, los bots son aplicaciones que tienen una interfaz de conversación.</span><span class="sxs-lookup"><span data-stu-id="6d352-118">In addition, bots are apps that have a conversational interface.</span></span> <span data-ttu-id="6d352-119">Puedes interactuar con un bot con texto, tarjetas interactivas y voz.</span><span class="sxs-lookup"><span data-stu-id="6d352-119">You can interact with a bot using text, interactive cards, and speech.</span></span> <span data-ttu-id="6d352-120">Un bot se comporta de forma diferente en función de si la conversación es un canal o una conversación de chat de grupo, o si es una conversación uno a uno.</span><span class="sxs-lookup"><span data-stu-id="6d352-120">A bot behaves differently depending on whether the conversation is a channel or group chat conversation, or it is a one-to-one conversation.</span></span> <span data-ttu-id="6d352-121">Las conversaciones se controlan a través del conector de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="6d352-121">Conversations are handled through the Bot Framework connector.</span></span> <span data-ttu-id="6d352-122">Para obtener más información, vea [conceptos básicos de la conversación](~/bots/how-to/conversations/conversation-basics.md).</span><span class="sxs-lookup"><span data-stu-id="6d352-122">For more information, see [conversation basics](~/bots/how-to/conversations/conversation-basics.md).</span></span>

<span data-ttu-id="6d352-123">El bot requiere información contextual, como los detalles del perfil de usuario para tener acceso al contenido relevante y mejorar la experiencia del bot.</span><span class="sxs-lookup"><span data-stu-id="6d352-123">Your bot requires contextual information, such as user profile details to access relevant content and enhance the bot experience.</span></span> <span data-ttu-id="6d352-124">Para obtener más información, vea [obtener el contexto de Teams](~/bots/how-to/get-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="6d352-124">For more information, see [get Teams context](~/bots/how-to/get-teams-context.md).</span></span> 

<span data-ttu-id="6d352-125">También puedes enviar y recibir archivos a través del bot mediante API de Graph o API de bots de Teams.</span><span class="sxs-lookup"><span data-stu-id="6d352-125">You can also send and receive files through the bot using Graph APIs or Teams bot APIs.</span></span> <span data-ttu-id="6d352-126">Para obtener más información, [vea Enviar y recibir archivos a través del bot](~/bots/how-to/bots-filesv4.md).</span><span class="sxs-lookup"><span data-stu-id="6d352-126">For more information, see [send and receive files through the bot](~/bots/how-to/bots-filesv4.md).</span></span>

<span data-ttu-id="6d352-127">Además, la limitación de velocidad se usa para optimizar los bots usados para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="6d352-127">In addition, rate limiting is used to optimize bots used for your Teams application.</span></span> <span data-ttu-id="6d352-128">Para proteger Microsoft Teams y sus usuarios, las API de bot proporcionan un límite de velocidad para las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="6d352-128">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="6d352-129">Para obtener más información, consulta [optimizar el bot con limitación de velocidad en Teams](~/bots/how-to/rate-limit.md).</span><span class="sxs-lookup"><span data-stu-id="6d352-129">For more information, see [optimize your bot with rate limiting in Teams](~/bots/how-to/rate-limit.md).</span></span>

<span data-ttu-id="6d352-130">Con las API de Microsoft Graph para llamadas y reuniones en línea, las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios mediante voz y vídeo.</span><span class="sxs-lookup"><span data-stu-id="6d352-130">With Microsoft Graph APIs for calls and online meetings, Microsoft Teams apps can now interact with users using voice and video.</span></span> <span data-ttu-id="6d352-131">Para obtener más información, vea [bots de llamadas y reuniones](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d352-131">For more information, see [calls and meetings bots](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span> 

<span data-ttu-id="6d352-132">Puedes usar las API de bots de Teams para obtener información para uno o varios miembros de un chat o equipo.</span><span class="sxs-lookup"><span data-stu-id="6d352-132">You can use the Teams bot APIs to get information for one or more members of a chat or team.</span></span> <span data-ttu-id="6d352-133">Para obtener más información, vea cambios en las API de bots de [Teams para obtener miembros de equipo o chat.](~/resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="6d352-133">For more information, see [changes to Teams bot APIs for fetching team or chat members](~/resources/team-chat-member-api-changes.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="6d352-134">Consulte también</span><span class="sxs-lookup"><span data-stu-id="6d352-134">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6d352-135">Creación de un bot para Teams</span><span class="sxs-lookup"><span data-stu-id="6d352-135">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="next-step"></a><span data-ttu-id="6d352-136">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="6d352-136">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6d352-137">Bots y SDK</span><span class="sxs-lookup"><span data-stu-id="6d352-137">Bots and SDKs</span></span>](~/bots/bot-features.md)
