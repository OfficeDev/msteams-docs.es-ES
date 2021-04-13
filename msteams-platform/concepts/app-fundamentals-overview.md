---
title: Introducción a los conceptos básicos de desarrollo de aplicaciones
author: heath-hamilton
description: Describir los conceptos básicos del desarrollo de plataformas de Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4af23e06cbf7a3f630b77ee1693e0931c9c9c03e
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654275"
---
# <a name="microsoft-teams-app-development-fundamentals"></a><span data-ttu-id="03781-103">Conceptos básicos de desarrollo de aplicaciones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="03781-103">Microsoft Teams app development fundamentals</span></span>

<span data-ttu-id="03781-104">Los conceptos básicos de la aplicación de Microsoft Teams te dan la dirección que necesitas para crear la aplicación personalizada de Teams.</span><span class="sxs-lookup"><span data-stu-id="03781-104">Microsoft Teams app fundamentals give the direction you need to create your custom Teams app.</span></span> <span data-ttu-id="03781-105">Puedes reconocer el marco necesario para planear la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="03781-105">You can recognize the framework required to plan your Teams app.</span></span> <span data-ttu-id="03781-106">El documento te ayuda a comprender la comunicación usuario-aplicación y averiguar el tipo de superficies de aplicación que necesitas usar o las API que la aplicación puede necesitar en el proceso.</span><span class="sxs-lookup"><span data-stu-id="03781-106">The document helps you to understand the user-app communication and figure out the kind of app surfaces you need to use or the APIs your app might require in the process.</span></span> <span data-ttu-id="03781-107">Obtén algo de inspiración para adoptar la interactividad que puede profundizar la experiencia de la aplicación cuando te integres con Teams.</span><span class="sxs-lookup"><span data-stu-id="03781-107">Get some inspiration to embrace interactivity that can deepen the app experience when you integrate with Teams.</span></span>

## <a name="capabilities-and-entry-points"></a><span data-ttu-id="03781-108">Capacidades y puntos de entrada</span><span class="sxs-lookup"><span data-stu-id="03781-108">Capabilities and entry points</span></span>

<span data-ttu-id="03781-109">Puedes ampliar la aplicación de Teams de varias maneras.</span><span class="sxs-lookup"><span data-stu-id="03781-109">You can extend your Teams app in multiple ways.</span></span> <span data-ttu-id="03781-110">Para poder ampliar la aplicación, debes comprender todas las funcionalidades principales y los puntos de entrada que funcionan en un espacio de colaboración.</span><span class="sxs-lookup"><span data-stu-id="03781-110">To be able to extend your app you must understand all the core capabilities and the entry points that work in a collaborative space.</span></span> <span data-ttu-id="03781-111">Puedes experimentar con los puntos de extensión para crear tus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="03781-111">You can experiment with the extension points for building your apps.</span></span> <span data-ttu-id="03781-112">Los componentes importantes del proyecto de aplicación te ayudan a configurar correctamente la página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03781-112">Important app project components help you to correctly configure your app page.</span></span> <span data-ttu-id="03781-113">La aplicación de Teams puede tener [varias capacidades](../concepts/capabilities-overview.md) [y puntos de entrada.](../concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="03781-113">Teams app can have [multiple capabilities](../concepts/capabilities-overview.md) and [entry points](../concepts/extensibility-points.md).</span></span>

## <a name="understand-your-use-cases"></a><span data-ttu-id="03781-114">Entender los casos de uso</span><span class="sxs-lookup"><span data-stu-id="03781-114">Understand your use cases</span></span>

<span data-ttu-id="03781-115">Puede reconocer problemas de usuario e identificar las respuestas a algunos problemas comunes a los que se enfrentan los usuarios.</span><span class="sxs-lookup"><span data-stu-id="03781-115">You can recognize user issues and identify the answers to some common problems the users face.</span></span> <span data-ttu-id="03781-116">Puedes crear la aplicación de Teams buscando la combinación adecuada para satisfacer las necesidades del usuario.</span><span class="sxs-lookup"><span data-stu-id="03781-116">You can build your Teams app by finding the right combination to meet your user's needs.</span></span> <span data-ttu-id="03781-117">[Comprender los casos de](../concepts/design/understand-use-cases.md) uso para saber cómo interactúa un usuario final con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03781-117">[Understand use cases](../concepts/design/understand-use-cases.md) to know how an end-user interacts with your app.</span></span> <span data-ttu-id="03781-118">Aprendes a comprender el usuario y su problema.</span><span class="sxs-lookup"><span data-stu-id="03781-118">You learn to understand the user and their problem.</span></span> <span data-ttu-id="03781-119">Algunas preguntas comunes que se responden son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="03781-119">Some common questions answered are as follows:</span></span>

* <span data-ttu-id="03781-120">¿Necesita autenticación?</span><span class="sxs-lookup"><span data-stu-id="03781-120">Do you need authentication?</span></span>
* <span data-ttu-id="03781-121">¿Qué problema va a solucionar la aplicación?</span><span class="sxs-lookup"><span data-stu-id="03781-121">What problem is your app going to solve?</span></span>
* <span data-ttu-id="03781-122">¿Quiénes son los usuarios finales de la aplicación?</span><span class="sxs-lookup"><span data-stu-id="03781-122">Who are the end-users of the app?</span></span>
* <span data-ttu-id="03781-123">¿Cómo debe ser la experiencia de incorporación y qué más puede hacer la aplicación?</span><span class="sxs-lookup"><span data-stu-id="03781-123">How should the onboarding experience be and what else the app can do?</span></span>

## <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="03781-124">Asignar los casos de uso a las funcionalidades de la aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="03781-124">Map your use cases to Teams app capabilities</span></span>

<span data-ttu-id="03781-125">[Map your use cases](../concepts/design/map-use-cases.md) covers some common scenarios and how to choose your app's capabilities.</span><span class="sxs-lookup"><span data-stu-id="03781-125">[Map your use cases](../concepts/design/map-use-cases.md) covers some common scenarios and how to choose your app's capabilities.</span></span> <span data-ttu-id="03781-126">Se proporciona información para compartir la aplicación y colaborar en elementos de un sistema externo.</span><span class="sxs-lookup"><span data-stu-id="03781-126">Information to share your app and collaborate on items in an external system is provided.</span></span> <span data-ttu-id="03781-127">También puede aprender a iniciar flujos de trabajo y enviar notificaciones a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="03781-127">You can also learn how to initiate workflows and send notifications to users.</span></span> <span data-ttu-id="03781-128">Obtén sugerencias adicionales sobre dónde empezar, cómo crear redes sociales con los usuarios, bots de conversación y combinar varias características.</span><span class="sxs-lookup"><span data-stu-id="03781-128">Get additional tips on where to start, how to get social with users, conversational bots, and combining multiple features.</span></span>

## <a name="see-also"></a><span data-ttu-id="03781-129">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="03781-129">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="03781-130">Integrar aplicaciones web con Teams</span><span class="sxs-lookup"><span data-stu-id="03781-130">Integrate web apps with Teams</span></span>](../samples/integrating-web-apps.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="03781-131">Crear la primera aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="03781-131">Build your first Microsoft Teams app</span></span>](../build-your-first-app/build-first-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="03781-132">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="03781-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="03781-133">Comprender las capacidades de la aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="03781-133">Understand Teams app capabilities</span></span>](capabilities-overview.md)

