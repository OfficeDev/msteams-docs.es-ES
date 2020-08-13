---
title: ¿Qué son los webhooks y los conectores?
author: clearab
description: Comprenda cómo los conectores y webhooks pueden conectar sus servicios web con el cliente de Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 740806e43af94d5a5da876affec2070a5a461b11
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652181"
---
# <a name="what-are-webhooks-and-connectors"></a><span data-ttu-id="67ec2-103">¿Qué son los webhooks y los conectores?</span><span class="sxs-lookup"><span data-stu-id="67ec2-103">What are webhooks and connectors?</span></span>

<span data-ttu-id="67ec2-104">Los webhooks y los conectores son formas sencillas de conectar sistemas y servicios externos con canales y chats de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="67ec2-104">Webhooks and connectors are straightforward ways to connect external systems and services with Microsoft Teams channels and chats.</span></span>

<span data-ttu-id="67ec2-105">Por ejemplo, los usuarios pueden suscribirse a las notificaciones de otra aplicación (normalmente en forma de tarjetas).</span><span class="sxs-lookup"><span data-stu-id="67ec2-105">Users can, for example, subscribe to notifications from another app (typically in the form of cards).</span></span>

## <a name="incoming-webhooks"></a><span data-ttu-id="67ec2-106">Webhooks entrantes</span><span class="sxs-lookup"><span data-stu-id="67ec2-106">Incoming webhooks</span></span>

<span data-ttu-id="67ec2-107">Los webhooks entrantes son el tipo más sencillo de conector y una forma rápida y sencilla de conectar el canal de un equipo a un servicio externo.</span><span class="sxs-lookup"><span data-stu-id="67ec2-107">Incoming webhooks are the simplest type of connector and a quick and easy way to connect a team's channel to an external service.</span></span> <span data-ttu-id="67ec2-108">Para cualquier canal (si está habilitado para ese equipo), puede exponer un extremo HTTPS que acepte el JSON con el formato correcto e inserte mensajes en el canal.</span><span class="sxs-lookup"><span data-stu-id="67ec2-108">For any channel (if enabled for that team), you can expose an HTTPS endpoint that accepts correctly formatted JSON and insert messages into the channel.</span></span>

<span data-ttu-id="67ec2-109">Consulte [crear un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="67ec2-109">See [Create an incoming webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="67ec2-110">Escenarios de usuario</span><span class="sxs-lookup"><span data-stu-id="67ec2-110">User scenarios</span></span>

<span data-ttu-id="67ec2-111">Los webhooks entrantes son los más idóneos para escenarios exclusivos de un equipo en particular.</span><span class="sxs-lookup"><span data-stu-id="67ec2-111">Incoming webhooks are best for scenarios unique to a particular team.</span></span> <span data-ttu-id="67ec2-112">Por ejemplo, puede crear un webhook entrante en el canal de DevOps y configurar los servicios de compilación, implementación y supervisión para enviar alertas.</span><span class="sxs-lookup"><span data-stu-id="67ec2-112">For example, you could create an incoming webhook in your DevOps channel and configure your build, deployment, and monitoring services to send alerts.</span></span>

## <a name="office-365-connectors"></a><span data-ttu-id="67ec2-113">Conectores de Office 365</span><span class="sxs-lookup"><span data-stu-id="67ec2-113">Office 365 Connectors</span></span>

<span data-ttu-id="67ec2-114">Un conector de Office 365 permite crear una página de configuración personalizada para el webhook entrante y empaquetarla como parte de una aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="67ec2-114">An Office 365 Connector allows you to create a custom configuration page for your incoming webhook and package it as part of a Teams app.</span></span> <span data-ttu-id="67ec2-115">A continuación, puede distribuir esa aplicación de forma más amplia o incluso en nuestra tienda de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="67ec2-115">You can then distribute that app more broadly or even to our app store.</span></span> <span data-ttu-id="67ec2-116">Los mensajes se envían principalmente mediante tarjetas de conector de Office 365 que también pueden tener un conjunto limitado de acciones de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="67ec2-116">You send messages primarily using Office 365 Connector cards that can also have a limited set of card actions.</span></span> <span data-ttu-id="67ec2-117">Se configuran en el nivel de canal, pero se instalan en el nivel de equipo.</span><span class="sxs-lookup"><span data-stu-id="67ec2-117">They are configured on the channel level but installed at the team level.</span></span>

<span data-ttu-id="67ec2-118">Consulte [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span><span class="sxs-lookup"><span data-stu-id="67ec2-118">See [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="67ec2-119">Escenarios de usuario</span><span class="sxs-lookup"><span data-stu-id="67ec2-119">User scenarios</span></span>

<span data-ttu-id="67ec2-120">Un conector meteorológico que permite elegir una ubicación y una hora del día para recibir actualizaciones sobre la previsión del futuro.</span><span class="sxs-lookup"><span data-stu-id="67ec2-120">A weather connector that lets you choose a location and time of day to receive updates about tomorrow's forecast.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="67ec2-121">Webhooks salientes</span><span class="sxs-lookup"><span data-stu-id="67ec2-121">Outgoing webhooks</span></span>

<span data-ttu-id="67ec2-122">Los webhooks salientes permiten a los usuarios enviar mensajes de texto desde un canal a los servicios Web.</span><span class="sxs-lookup"><span data-stu-id="67ec2-122">Outgoing webhooks allow your users to send text messages from a channel to your web services.</span></span> <span data-ttu-id="67ec2-123">Una vez configurados, los usuarios pueden @mention la aplicación y enviar un mensaje al servicio externo.</span><span class="sxs-lookup"><span data-stu-id="67ec2-123">Once configured, users can @mention your app and send a message to your external service.</span></span> <span data-ttu-id="67ec2-124">El servicio tiene cinco segundos para enviar una respuesta al mensaje, posiblemente con texto o con una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="67ec2-124">Your service has five seconds to send a response to the message, potentially containing text or a card.</span></span>

<span data-ttu-id="67ec2-125">Los webhooks salientes se configuran por equipo y no pueden incluirse como parte de una aplicación normal de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="67ec2-125">Outgoing webhooks are configured on a per-team basis and can't be included as part of a normal Teams app.</span></span>

<span data-ttu-id="67ec2-126">Consulte [crear un webhook saliente](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="67ec2-126">See [Create an outgoing webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="67ec2-127">Escenarios de usuario</span><span class="sxs-lookup"><span data-stu-id="67ec2-127">User scenarios</span></span>

<span data-ttu-id="67ec2-128">Los webhooks salientes son idóneos para completar flujos de trabajo específicos del equipo que no requieran la recopilación o el intercambio de grandes cantidades de información.</span><span class="sxs-lookup"><span data-stu-id="67ec2-128">Outgoing webhooks are best suited for completing team-specific workflows that don't require collecting or exchanging large amounts of information.</span></span>

## <a name="learn-more"></a><span data-ttu-id="67ec2-129">Más información</span><span class="sxs-lookup"><span data-stu-id="67ec2-129">Learn more</span></span>

* [<span data-ttu-id="67ec2-130">Planeación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="67ec2-130">Planning your app</span></span>](../../concepts/extensibility-points.md)
* [<span data-ttu-id="67ec2-131">Compilar la aplicación</span><span class="sxs-lookup"><span data-stu-id="67ec2-131">Building your app</span></span>](../../concepts/building-an-app.md)
* [<span data-ttu-id="67ec2-132">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="67ec2-132">Publishing your app</span></span>](../../concepts/deploy-and-publish/overview.md)
