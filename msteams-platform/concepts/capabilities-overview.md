---
title: Descripción de las capacidades de la aplicación de Teams
author: heath-hamilton
description: Características de la aplicación de Teams explicadas
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 5336b36b52cf81be414f18ccaaf9e235c079e626
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034708"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="8f715-103">Descripción de las capacidades de la aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="8f715-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="8f715-104">*Las funcionalidades* son los puntos de extensión para crear aplicaciones en la plataforma de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8f715-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="8f715-105">Hay varias formas de extender Teams, por lo que cada aplicación es única: algunas solo tienen una funcionalidad (como un webhook), mientras que otras tienen algunas para dar opciones a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8f715-105">There are multiple ways to extend Teams, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="8f715-106">Por ejemplo, la aplicación podría mostrar datos en una ubicación central (pestaña) y presentar esa misma información a través de una interfaz conversacional (bot).</span><span class="sxs-lookup"><span data-stu-id="8f715-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="8f715-107">La aplicación de Teams tiene una o todas las siguientes funcionalidades principales:</span><span class="sxs-lookup"><span data-stu-id="8f715-107">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="8f715-108">Pestañas</span><span class="sxs-lookup"><span data-stu-id="8f715-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="8f715-109">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="8f715-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="8f715-110">Bots</span><span class="sxs-lookup"><span data-stu-id="8f715-110">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="8f715-111">Webhooks y conectores</span><span class="sxs-lookup"><span data-stu-id="8f715-111">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="8f715-112">La aplicación también puede aprovechar las capacidades avanzadas, como la API de [Microsoft Graph para Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span><span class="sxs-lookup"><span data-stu-id="8f715-112">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="8f715-113">Consulta la siguiente ilustración para obtener una idea de qué capacidades proporcionarían las características que quieres en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8f715-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Mapa de la mente que ilustra las funcionalidades de la aplicación de Teams.":::

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="8f715-115">Hacer lo mejor para los usuarios</span><span class="sxs-lookup"><span data-stu-id="8f715-115">Doing what's best for your users</span></span>

<span data-ttu-id="8f715-116">A medida que te familiarices con el desarrollo de aplicaciones de Teams, empezarás a comprender sus sutilezas.</span><span class="sxs-lookup"><span data-stu-id="8f715-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="8f715-117">Hay más de una forma de crear determinadas características (como recopilar la entrada del usuario).</span><span class="sxs-lookup"><span data-stu-id="8f715-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="8f715-118">Por ejemplo, puede insertar un formulario basado en web en una pestaña mediante un `<iframe>` .</span><span class="sxs-lookup"><span data-stu-id="8f715-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="8f715-119">También puedes hacerlo en una pestaña con un módulo de tareas, una convención de la interfaz de usuario de Teams, para una experiencia más nativa que los usuarios prefieran.</span><span class="sxs-lookup"><span data-stu-id="8f715-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="8f715-120">Elegir las capacidades y el diseño adecuados se debe a comprender primero [los casos de uso de la audiencia.](../concepts/design/understand-use-cases.md)</span><span class="sxs-lookup"><span data-stu-id="8f715-120">Choosing the right capabilities and design comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>
