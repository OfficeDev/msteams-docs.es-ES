---
title: Puntos de entrada para aplicaciones de Teams
author: heath-hamilton
description: Describe dónde pueden los usuarios descubrir y usar su aplicación en Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f61e5b5c05855c0a3a766920095cf46f699f08a6
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654359"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="1cdec-103">Puntos de entrada para aplicaciones de Teams</span><span class="sxs-lookup"><span data-stu-id="1cdec-103">Entry points for Teams apps</span></span>

<span data-ttu-id="1cdec-104">La plataforma de Teams proporciona un conjunto flexible de puntos de entrada, como equipo, canal y chat donde las personas pueden descubrir y usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1cdec-104">The Teams platform provides a flexible set of entry points, such as team, channel, and chat where people can discover and use your app.</span></span> <span data-ttu-id="1cdec-105">Su aplicación puede ser tan simple como incrustar contenido web existente en una pestaña o una aplicación con varias facetas con la que los usuarios interactúen en varios contextos.</span><span class="sxs-lookup"><span data-stu-id="1cdec-105">Your app can be as simple as embedding existing web content in a tab or a multi-faceted app that users interact with across several contexts.</span></span>
<span data-ttu-id="1cdec-106">Las aplicaciones más exitosas son nativas de Teams, por lo que elige cuidadosamente los puntos de entrada de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1cdec-106">The most successful apps are native to Teams, so choose your app's entry points carefully.</span></span>

## <a name="shared-app-experiences"></a><span data-ttu-id="1cdec-107">Experiencias de aplicaciones compartidas</span><span class="sxs-lookup"><span data-stu-id="1cdec-107">Shared app experiences</span></span>

<span data-ttu-id="1cdec-108">El equipo, el canal y el chat son espacios de colaboración.</span><span class="sxs-lookup"><span data-stu-id="1cdec-108">Team, channel, and chat are collaboration spaces.</span></span> <span data-ttu-id="1cdec-109">Las aplicaciones en estos contextos están disponibles para todos los usuarios de ese espacio.</span><span class="sxs-lookup"><span data-stu-id="1cdec-109">Apps in these contexts are available to everyone in that space.</span></span> <span data-ttu-id="1cdec-110">Los espacios de colaboración suelen centrarse en flujos de trabajo adicionales o en desbloquear nuevas interacciones sociales.</span><span class="sxs-lookup"><span data-stu-id="1cdec-110">Collaboration spaces typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="1cdec-111">En la siguiente lista se muestra cómo se usan habitualmente las funcionalidades de la aplicación de Teams en contextos de colaboración:</span><span class="sxs-lookup"><span data-stu-id="1cdec-111">The following list shows how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="1cdec-112">Las [**pestañas**](~/tabs/what-are-tabs.md) ofrecen una experiencia web insertada en pantalla completa configurada para el equipo, canal o chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="1cdec-112">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="1cdec-113">Todos los miembros interactúan con el mismo contenido basado en web, por lo que es habitual una experiencia de aplicación sin estado de una sola página.</span><span class="sxs-lookup"><span data-stu-id="1cdec-113">All members interact with the same web-based content, so a stateless single-page app experience is typical.</span></span>

* <span data-ttu-id="1cdec-114">Las [**extensiones de mensajería**](~/messaging-extensions/what-are-messaging-extensions.md) son accesos directos para insertar contenido externo en una conversación o para tomar acciones en mensajes sin salir de Teams.</span><span class="sxs-lookup"><span data-stu-id="1cdec-114">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="1cdec-115">[La eliminación de vínculos](~/messaging-extensions/how-to/link-unfurling.md) proporciona contenido enriquecido al compartir contenido desde una dirección URL común.</span><span class="sxs-lookup"><span data-stu-id="1cdec-115">[Link unfurling](~/messaging-extensions/how-to/link-unfurling.md) provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="1cdec-116">[**Los bots**](~/bots/what-are-bots.md) interactúan con los miembros de la conversación a través del chat y responden a eventos, como agregar un nuevo miembro o cambiar el nombre de un canal.</span><span class="sxs-lookup"><span data-stu-id="1cdec-116">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events, such as adding a new member or renaming a channel.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="1cdec-117">Las conversaciones con un bot en estos contextos son visibles para todos los miembros del equipo, canal o grupo, por lo que las conversaciones de bot deben ser relevantes para todos.</span><span class="sxs-lookup"><span data-stu-id="1cdec-117">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations must be relevant to everyone.</span></span>

* <span data-ttu-id="1cdec-118">Los [**webhooks y conectores**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) permiten a un servicio externo publicar mensajes en una conversación y a los usuarios enviar mensajes a un servicio.</span><span class="sxs-lookup"><span data-stu-id="1cdec-118">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="1cdec-119">La [**API de REST de Microsoft Graph**](https://docs.microsoft.com/graph/teams-concept-overview) obtiene datos sobre equipos, canales y chats de grupo para ayudar a automatizar y a administrar procesos de Teams.</span><span class="sxs-lookup"><span data-stu-id="1cdec-119">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-app-experiences"></a><span data-ttu-id="1cdec-120">Experiencias de aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="1cdec-120">Personal app experiences</span></span>

<span data-ttu-id="1cdec-121">Las [aplicaciones personales](../concepts/design/personal-apps.md) se centran en las interacciones con un solo usuario.</span><span class="sxs-lookup"><span data-stu-id="1cdec-121">[Personal apps](../concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="1cdec-122">La experiencia en este contexto es única para cada usuario.</span><span class="sxs-lookup"><span data-stu-id="1cdec-122">The experience in this context is unique to each user.</span></span>

<span data-ttu-id="1cdec-123">En la siguiente lista se muestra cómo se usan normalmente las capacidades de Teams en contextos personales:</span><span class="sxs-lookup"><span data-stu-id="1cdec-123">The following list shows how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="1cdec-124">Los [**bots**](~/bots/what-are-bots.md) mantienen conversaciones individuales con un usuario.</span><span class="sxs-lookup"><span data-stu-id="1cdec-124">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="1cdec-125">Los bots que requieren conversaciones de varios turnos o que proporcionan notificaciones relevantes solo para un usuario específico son más adecuados en las aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="1cdec-125">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal apps.</span></span>

* <span data-ttu-id="1cdec-126">[**Las pestañas**](~/tabs/what-are-tabs.md) proporcionan una experiencia web incrustada a pantalla completa que es significativa para el usuario que la está viendo.</span><span class="sxs-lookup"><span data-stu-id="1cdec-126">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that is meaningful to the user looking at it.</span></span>

## <a name="see-also"></a><span data-ttu-id="1cdec-127">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1cdec-127">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1cdec-128">Directrices de diseño de aplicaciones de Teams</span><span class="sxs-lookup"><span data-stu-id="1cdec-128">Teams app design guidelines</span></span>](../concepts/design/design-teams-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="1cdec-129">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="1cdec-129">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1cdec-130">Comprender casos de uso</span><span class="sxs-lookup"><span data-stu-id="1cdec-130">Understand use cases</span></span>](../concepts/design/understand-use-cases.md)
