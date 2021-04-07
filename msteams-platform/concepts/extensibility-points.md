---
title: Puntos de entrada para aplicaciones de Teams
author: heath-hamilton
description: Describe dónde pueden los usuarios descubrir y usar su aplicación en Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 72ce2620160f854bbe458821db01e91d2d9f62cd
ms.sourcegitcommit: 098d38dd947e87e69d289b99e807bea2d95c42f9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2020
ms.locfileid: "49713630"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="c97ba-103">Puntos de entrada para aplicaciones de Teams</span><span class="sxs-lookup"><span data-stu-id="c97ba-103">Entry points for Teams apps</span></span>

<span data-ttu-id="c97ba-104">La plataforma de Teams ofrece un conjunto flexible de puntos de entrada en los que los usuarios pueden descubrir y usar su aplicación.</span><span class="sxs-lookup"><span data-stu-id="c97ba-104">The Teams platform provides a flexible set of entry points where people can discover and use your app.</span></span> <span data-ttu-id="c97ba-105">Su aplicación puede ser tan simple como incrustar contenido web existente en una pestaña o una aplicación con varias facetas con la que los usuarios interactúen en varios contextos.</span><span class="sxs-lookup"><span data-stu-id="c97ba-105">Your app can be as simple as embedding existing web content in a tab or a multi-faceted app that users interact with across several contexts.</span></span>

<span data-ttu-id="c97ba-106">Las aplicaciones de mayor éxito son las que parecen nativas de Teams, por lo que es importante planificar cuidadosamente los puntos de entrada de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="c97ba-106">The most successful apps feel native to Teams, so it's important to carefully plan your app's entry points.</span></span>

## <a name="teams-channels-and-chats"></a><span data-ttu-id="c97ba-107">Equipos, canales y chats</span><span class="sxs-lookup"><span data-stu-id="c97ba-107">Teams, channels, and chats</span></span>

<span data-ttu-id="c97ba-108">Los equipos, canales y chats son espacios de colaboración.</span><span class="sxs-lookup"><span data-stu-id="c97ba-108">Teams, channels, and chats are collaboration spaces.</span></span> <span data-ttu-id="c97ba-109">Las aplicaciones en estos contextos están disponibles para cualquier usuario en dicho espacio y se suelen centrar en flujos de trabajo adicionales o en establecer nuevas interacciones sociales.</span><span class="sxs-lookup"><span data-stu-id="c97ba-109">Apps in these contexts are available to everyone in that space and typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="c97ba-110">Aquí tiene una explicación sobre cómo se suelen usar las funciones de la aplicación de Teams en los contextos colaborativos:</span><span class="sxs-lookup"><span data-stu-id="c97ba-110">Here's how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="c97ba-111">Las [**pestañas**](~/tabs/what-are-tabs.md) ofrecen una experiencia web insertada en pantalla completa configurada para el equipo, canal o chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="c97ba-111">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="c97ba-112">Todos los miembros interactúan con el mismo contenido basado en la web, por lo que es habitual una experiencia de aplicación de una sola página sin estado.</span><span class="sxs-lookup"><span data-stu-id="c97ba-112">All members interact with the same web-based content, so a stateless single page app experience is typical.</span></span>

* <span data-ttu-id="c97ba-113">Las [**extensiones de mensajería**](~/messaging-extensions/what-are-messaging-extensions.md) son accesos directos para insertar contenido externo en una conversación o para tomar acciones en mensajes sin salir de Teams.</span><span class="sxs-lookup"><span data-stu-id="c97ba-113">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="c97ba-114">El despliegue de vínculos proporciona contenido enriquecido al compartir contenido desde una dirección URL común.</span><span class="sxs-lookup"><span data-stu-id="c97ba-114">Link unfurling provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="c97ba-115">Los [**bots**](~/bots/what-are-bots.md) interactúan con los miembros de la conversación a través del chat y responden a eventos (como agregar un nuevo miembro o cambiar el nombre de un canal).</span><span class="sxs-lookup"><span data-stu-id="c97ba-115">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events (like adding a new member or renaming a channel).</span></span> <span data-ttu-id="c97ba-116">Las conversaciones con un bot en estos contextos son visibles para todos los miembros del equipo, canal o grupo, por lo que las conversaciones con bots deberían ser relevantes para todos.</span><span class="sxs-lookup"><span data-stu-id="c97ba-116">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations should be relevant to everyone.</span></span>

* <span data-ttu-id="c97ba-117">Los [**webhooks y conectores**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permiten a un servicio externo publicar mensajes en una conversación y a los usuarios enviar mensajes a un servicio.</span><span class="sxs-lookup"><span data-stu-id="c97ba-117">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="c97ba-118">La [**API de REST de Microsoft Graph**](https://docs.microsoft.com/graph/teams-concept-overview) obtiene datos sobre equipos, canales y chats de grupo para ayudar a automatizar y a administrar procesos de Teams.</span><span class="sxs-lookup"><span data-stu-id="c97ba-118">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="c97ba-119">Aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="c97ba-119">Personal apps</span></span>

<span data-ttu-id="c97ba-120">Las [aplicaciones personales](~/concepts/design/personal-apps.md) se centran en las interacciones con un solo usuario.</span><span class="sxs-lookup"><span data-stu-id="c97ba-120">[Personal apps](~/concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="c97ba-121">La experiencia en este contexto es única para cada usuario.</span><span class="sxs-lookup"><span data-stu-id="c97ba-121">The experience in this context is unique to each user.</span></span>

<span data-ttu-id="c97ba-122">Aquí tiene una explicación sobre cómo se suelen usar las funciones de Teams en los contextos personales:</span><span class="sxs-lookup"><span data-stu-id="c97ba-122">Here's how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="c97ba-123">Los [**bots**](~/bots/what-are-bots.md) mantienen conversaciones individuales con un usuario.</span><span class="sxs-lookup"><span data-stu-id="c97ba-123">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="c97ba-124">Los bots que requieren conversaciones de varios turnos o que proporcionan notificaciones relevantes solo para un usuario específico son más adecuados en las aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="c97ba-124">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal apps.</span></span>

* <span data-ttu-id="c97ba-125">Las [**pestañas**](~/tabs/what-are-tabs.md) ofrecen una experiencia web insertada de pantalla completa que resulta significativa para el usuario que la ve.</span><span class="sxs-lookup"><span data-stu-id="c97ba-125">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that's meaningful to the user looking at it.</span></span>

## <a name="examples"></a><span data-ttu-id="c97ba-126">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c97ba-126">Examples</span></span>

<span data-ttu-id="c97ba-127">Las directrices de diseño de aplicaciones de Teams proporcionan elementos visuales detallados que muestran dónde pueden los usuarios encontrar y usar aplicaciones de Teams.</span><span class="sxs-lookup"><span data-stu-id="c97ba-127">The Teams app design guidelines provide detailed visuals showing you where people can find and use Teams apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c97ba-128">Ver las directrices de diseño de aplicaciones de Teams</span><span class="sxs-lookup"><span data-stu-id="c97ba-128">See the Teams app design guidelines</span></span>](../concepts/design/design-teams-app-overview.md)
