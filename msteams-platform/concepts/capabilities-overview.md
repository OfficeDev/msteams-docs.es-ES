---
title: Comprender las funcionalidades de la aplicación
author: heath-hamilton
description: Características de la aplicación de Teams explicadas
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 6d08d06c55aed4b531fba4bb533c896c13073cfc
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654436"
---
# <a name="understand-microsoft-teams-app-capabilities"></a><span data-ttu-id="b21a0-103">Comprender las capacidades de la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b21a0-103">Understand Microsoft Teams app capabilities</span></span>

<span data-ttu-id="b21a0-104">La extensibilidad o los puntos de entrada son diferentes formas en las que una aplicación puede manifestarse a un usuario.</span><span class="sxs-lookup"><span data-stu-id="b21a0-104">Extensibility or entry points are different ways in which an app can manifest itself to a user.</span></span> <span data-ttu-id="b21a0-105">Por ejemplo, un usuario puede interactuar con una aplicación en una pestaña de lienzo para realizar una actividad o puede optar por hacer lo mismo con un bot de conversación.</span><span class="sxs-lookup"><span data-stu-id="b21a0-105">For example, a user can interact with an app on a canvas tab to do an activity or might choose to do the same using a conversational bot.</span></span> <span data-ttu-id="b21a0-106">Las distintas funcionalidades usadas para crear la aplicación de Teams te permiten aumentar su ámbito de uso.</span><span class="sxs-lookup"><span data-stu-id="b21a0-106">The various capabilities used to build your Teams app allow you to increase its usage scope.</span></span>

<span data-ttu-id="b21a0-107">Hay varias formas de extender Teams, por lo que cada aplicación es única.</span><span class="sxs-lookup"><span data-stu-id="b21a0-107">There are multiple ways to extend Teams, so every app is unique.</span></span> <span data-ttu-id="b21a0-108">Algunos solo tienen una funcionalidad, como un webhook, mientras que otros tienen más de una característica para ofrecer a los usuarios varias opciones.</span><span class="sxs-lookup"><span data-stu-id="b21a0-108">Some only have one capability, such as a webhook, while others have more than one feature to give users various options.</span></span> <span data-ttu-id="b21a0-109">Por ejemplo, la aplicación puede mostrar datos en  una ubicación central, es decir, la pestaña y presentar esa misma información a través de una interfaz conversacional, es decir, el **bot**.</span><span class="sxs-lookup"><span data-stu-id="b21a0-109">For example, your app can display data in a central location, that is, the **tab** and present that same information through a conversational interface, that is, the **bot**.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="b21a0-110">Capacidades de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b21a0-110">App capabilities</span></span>

<span data-ttu-id="b21a0-111">La aplicación de Teams tiene una o todas las siguientes funcionalidades principales:</span><span class="sxs-lookup"><span data-stu-id="b21a0-111">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="b21a0-112">Pestañas</span><span class="sxs-lookup"><span data-stu-id="b21a0-112">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="b21a0-113">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="b21a0-113">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="b21a0-114">Bots</span><span class="sxs-lookup"><span data-stu-id="b21a0-114">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="b21a0-115">Webhooks y conectores</span><span class="sxs-lookup"><span data-stu-id="b21a0-115">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="b21a0-116">La aplicación también puede aprovechar las capacidades avanzadas, como la API de [Microsoft Graph para Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span><span class="sxs-lookup"><span data-stu-id="b21a0-116">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="b21a0-117">La siguiente ilustración te ofrece una idea de qué funcionalidades proporcionarán las características que quieras en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b21a0-117">The following illustration gives you an idea of which capabilities will provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Mapa de la mente que ilustra las funcionalidades de la aplicación de Teams.":::

## <a name="always-consider-your-user"></a><span data-ttu-id="b21a0-119">Tenga en cuenta siempre al usuario</span><span class="sxs-lookup"><span data-stu-id="b21a0-119">Always consider your user</span></span>

<span data-ttu-id="b21a0-120">A medida que te familiarices con el desarrollo de aplicaciones de Teams, comprendes sus fundamentos básicos.</span><span class="sxs-lookup"><span data-stu-id="b21a0-120">As you familiarize yourself with Teams app development, you understand its core fundamentals.</span></span> <span data-ttu-id="b21a0-121">Comprende que hay más de una forma de crear determinadas características.</span><span class="sxs-lookup"><span data-stu-id="b21a0-121">You understand that there is more than one way to build certain features.</span></span> <span data-ttu-id="b21a0-122">En estos escenarios, considere cómo puede proporcionar una experiencia más nativa al usuario.</span><span class="sxs-lookup"><span data-stu-id="b21a0-122">In such scenarios, consider how you can provide a more native experience to your user.</span></span>
<span data-ttu-id="b21a0-123">Por ejemplo, puedes recopilar la entrada del usuario en un formulario creado como una pestaña en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b21a0-123">For example, you can collect user input in a form built as a tab in the app.</span></span> <span data-ttu-id="b21a0-124">También puede hacerlo con un módulo de tareas sin cambiar las vistas y interrumpir el flujo de trabajo del usuario.</span><span class="sxs-lookup"><span data-stu-id="b21a0-124">You can also do this using a task module without switching views and disrupting user's flow of work.</span></span> <span data-ttu-id="b21a0-125">Es importante elegir puntos de extensión que proporcionen una desviación mínima del flujo de trabajo normal de un usuario.</span><span class="sxs-lookup"><span data-stu-id="b21a0-125">It is important to choose extension points that provide least deviation from a user's regular flow of work.</span></span>

## <a name="see-also"></a><span data-ttu-id="b21a0-126">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b21a0-126">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b21a0-127">Crear aplicaciones para Teams</span><span class="sxs-lookup"><span data-stu-id="b21a0-127">Build apps for Teams</span></span>](../overview.md)
## <a name="next-step"></a><span data-ttu-id="b21a0-128">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="b21a0-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b21a0-129">Puntos de entrada de la aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="b21a0-129">Teams app entry points</span></span>](../concepts/extensibility-points.md)
