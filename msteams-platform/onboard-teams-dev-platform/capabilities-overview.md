---
title: Descripción de las funcionalidades de la aplicación Teams
author: heath-hamilton
description: Información general sobre las capacidades de la plataforma de Microsoft Teams, que son los puntos de extensión para crear aplicaciones de Teams.
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 9bb94d2cfd5c30b2245c5ccf580d374972315e72
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964567"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="c759f-103">Descripción de las funcionalidades de la aplicación Teams</span><span class="sxs-lookup"><span data-stu-id="c759f-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="c759f-104">Las *funcionalidades* son los puntos de extensión para crear aplicaciones en la plataforma de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c759f-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="c759f-105">Hay varias formas de ampliar el cliente de Microsoft Teams, de modo que cada aplicación sea única: algunas solo tienen una capacidad (como un webhook), mientras que otras tienen algunas para conceder opciones a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c759f-105">There are multiple ways to extend the Teams client, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="c759f-106">Por ejemplo, la aplicación puede mostrar datos en una ubicación central (pestaña) y presentar la misma información a través de una interfaz de conversación (bot).</span><span class="sxs-lookup"><span data-stu-id="c759f-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="c759f-107">La aplicación de Microsoft Teams puede tener una de las siguientes capacidades principales, o todas ellas:</span><span class="sxs-lookup"><span data-stu-id="c759f-107">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="c759f-108">Pestañas</span><span class="sxs-lookup"><span data-stu-id="c759f-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="c759f-109">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="c759f-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="c759f-110">Webhooks y conectores</span><span class="sxs-lookup"><span data-stu-id="c759f-110">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [<span data-ttu-id="c759f-111">Bots</span><span class="sxs-lookup"><span data-stu-id="c759f-111">Bots</span></span>](../bots/what-are-bots.md)

<span data-ttu-id="c759f-112">La aplicación también puede aprovechar las funcionalidades avanzadas, como la [API de REST de Microsoft Graph](../graph-api/rsc/resource-specific-consent.md).</span><span class="sxs-lookup"><span data-stu-id="c759f-112">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph REST API](../graph-api/rsc/resource-specific-consent.md).</span></span>

<span data-ttu-id="c759f-113">Vea la siguiente ilustración para obtener una idea de las funcionalidades que proporcionarán las características que desea en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c759f-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

![Diagrama de ideas ilustrativo de las funcionalidades de la aplicación Teams](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="c759f-115">¿Qué es lo mejor para los usuarios?</span><span class="sxs-lookup"><span data-stu-id="c759f-115">Doing what's best for your users</span></span>

<span data-ttu-id="c759f-116">A medida que se familiarice con el desarrollo de aplicaciones de Microsoft Teams, empezará a comprender sus matices.</span><span class="sxs-lookup"><span data-stu-id="c759f-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="c759f-117">Hay más de una forma de crear determinadas características (como la recopilación de entradas de usuario).</span><span class="sxs-lookup"><span data-stu-id="c759f-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="c759f-118">Por ejemplo, puede insertar un formulario basado en Web en una pestaña usando un `<iframe>` .</span><span class="sxs-lookup"><span data-stu-id="c759f-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="c759f-119">También puede hacerlo en una pestaña usando un módulo de tareas, una Convención de interfaz de usuario de Microsoft Teams, para una experiencia más nativa que los usuarios prefieren.</span><span class="sxs-lookup"><span data-stu-id="c759f-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="c759f-120">La elección de la combinación correcta de capacidades y convenciones, controles y elementos de la interfaz de usuario se refiere a [comprender los casos de uso de la audiencia](../concepts/design/understand-use-cases.md).</span><span class="sxs-lookup"><span data-stu-id="c759f-120">Choosing the right combination of capabilities and UI conventions, controls, and elements comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>

## <a name="learn-more"></a><span data-ttu-id="c759f-121">Obtén más información</span><span class="sxs-lookup"><span data-stu-id="c759f-121">Learn more</span></span>

* [<span data-ttu-id="c759f-122">Empezar a planear la aplicación</span><span class="sxs-lookup"><span data-stu-id="c759f-122">Start planning your app</span></span>](../concepts/extensibility-points.md)
