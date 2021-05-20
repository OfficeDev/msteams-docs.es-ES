---
title: Comprender las capacidades de la aplicación
author: heath-hamilton
description: Teams capacidades de la aplicación explicadas
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 209d187681b1370440931fcd40744965395b13e8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565154"
---
# <a name="understand-microsoft-teams-app-capabilities"></a><span data-ttu-id="803af-103">Comprender Microsoft Teams capacidades de la aplicación</span><span class="sxs-lookup"><span data-stu-id="803af-103">Understand Microsoft Teams app capabilities</span></span>

<span data-ttu-id="803af-104">La extensibilidad o los puntos de entrada son formas diferentes en las que una aplicación puede manifestarse ante un usuario.</span><span class="sxs-lookup"><span data-stu-id="803af-104">Extensibility or entry points are different ways in which an app can manifest itself to a user.</span></span> <span data-ttu-id="803af-105">Por ejemplo, un usuario puede interactuar con una aplicación en una pestaña de lienzo para realizar una actividad o puede elegir hacer lo mismo mediante un bot conversacional.</span><span class="sxs-lookup"><span data-stu-id="803af-105">For example, a user can interact with an app on a canvas tab to do an activity or might choose to do the same using a conversational bot.</span></span> <span data-ttu-id="803af-106">Las distintas capacidades utilizadas para crear la aplicación Teams le permiten aumentar su ámbito de uso.</span><span class="sxs-lookup"><span data-stu-id="803af-106">The various capabilities used to build your Teams app allow you to increase its usage scope.</span></span>

<span data-ttu-id="803af-107">Hay varias maneras de extender Teams, por lo que cada aplicación es única.</span><span class="sxs-lookup"><span data-stu-id="803af-107">There are multiple ways to extend Teams, so every app is unique.</span></span> <span data-ttu-id="803af-108">Algunos solo tienen una capacidad, como un webhook, mientras que otros tienen más de una característica para dar a los usuarios varias opciones.</span><span class="sxs-lookup"><span data-stu-id="803af-108">Some only have one capability, such as a webhook, while others have more than one feature to give users various options.</span></span> <span data-ttu-id="803af-109">Por ejemplo, la aplicación puede mostrar datos en una ubicación central, es decir, la **pestaña** y presentar esa misma información a través de una interfaz conversacional, es decir, el **bot.**</span><span class="sxs-lookup"><span data-stu-id="803af-109">For example, your app can display data in a central location, that is, the **tab** and present that same information through a conversational interface, that is, the **bot**.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="803af-110">Capacidades de la aplicación</span><span class="sxs-lookup"><span data-stu-id="803af-110">App capabilities</span></span>

<span data-ttu-id="803af-111">La aplicación Teams tiene una o todas las siguientes capacidades principales:</span><span class="sxs-lookup"><span data-stu-id="803af-111">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="803af-112">Pestañas</span><span class="sxs-lookup"><span data-stu-id="803af-112">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="803af-113">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="803af-113">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="803af-114">Bots</span><span class="sxs-lookup"><span data-stu-id="803af-114">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="803af-115">Webhooks y conectores</span><span class="sxs-lookup"><span data-stu-id="803af-115">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="803af-116">La aplicación también puede aprovechar las capacidades avanzadas, como la [API de Microsoft Graph para Teams.](/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="803af-116">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="803af-117">La siguiente ilustración le da una idea de qué capacidades proporcionará las características que desea en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="803af-117">The following illustration gives you an idea of which capabilities will provide the features you want in your app:</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Mapa mental que ilustra cuáles son Teams capacidades de la aplicación.":::

## <a name="always-consider-your-user"></a><span data-ttu-id="803af-119">Siempre considere a su usuario</span><span class="sxs-lookup"><span data-stu-id="803af-119">Always consider your user</span></span>

<span data-ttu-id="803af-120">A medida que te familiarizas con Teams desarrollo de aplicaciones, entiendes sus fundamentos fundamentales.</span><span class="sxs-lookup"><span data-stu-id="803af-120">As you familiarize yourself with Teams app development, you understand its core fundamentals.</span></span> <span data-ttu-id="803af-121">Usted entiende que hay más de una manera de construir ciertas características.</span><span class="sxs-lookup"><span data-stu-id="803af-121">You understand that there is more than one way to build certain features.</span></span> <span data-ttu-id="803af-122">En estos escenarios, considere cómo puede proporcionar una experiencia más nativa al usuario.</span><span class="sxs-lookup"><span data-stu-id="803af-122">In such scenarios, consider how you can provide a more native experience to your user.</span></span>
<span data-ttu-id="803af-123">Por ejemplo, puede recopilar la entrada del usuario en un formulario creado como una pestaña en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="803af-123">For example, you can collect user input in a form built as a tab in the app.</span></span> <span data-ttu-id="803af-124">También puede hacerlo mediante un módulo de tareas sin cambiar de vista e interrumpir el flujo de trabajo del usuario.</span><span class="sxs-lookup"><span data-stu-id="803af-124">You can also do this using a task module without switching views and disrupting user's flow of work.</span></span> <span data-ttu-id="803af-125">Es importante elegir puntos de extensión que proporcionen menos desviación del flujo de trabajo regular de un usuario.</span><span class="sxs-lookup"><span data-stu-id="803af-125">It is important to choose extension points that provide least deviation from a user's regular flow of work.</span></span>

## <a name="see-also"></a><span data-ttu-id="803af-126">Vea también</span><span class="sxs-lookup"><span data-stu-id="803af-126">See also</span></span>

[<span data-ttu-id="803af-127">Crear aplicaciones para Teams</span><span class="sxs-lookup"><span data-stu-id="803af-127">Build apps for Teams</span></span>](../overview.md)

## <a name="next-step"></a><span data-ttu-id="803af-128">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="803af-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="803af-129">Puntos de entrada de la aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="803af-129">Teams app entry points</span></span>](../concepts/extensibility-points.md)
