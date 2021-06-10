---
title: Introducción a los conceptos básicos de desarrollo de aplicaciones
author: heath-hamilton
description: Describir los conceptos fundamentales del Teams de plataformas.
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 1ecae34c38950f16e49fc123f73bdc746c4b28cc
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630162"
---
# <a name="microsoft-teams-app-development-fundamentals"></a><span data-ttu-id="a67e2-103">Microsoft Teams de desarrollo de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a67e2-103">Microsoft Teams app development fundamentals</span></span>

<span data-ttu-id="a67e2-104">Microsoft Teams conceptos básicos de la aplicación dan la dirección que necesitas para crear la aplicación Teams personalizada.</span><span class="sxs-lookup"><span data-stu-id="a67e2-104">Microsoft Teams app fundamentals give the direction you need to create your custom Teams app.</span></span> <span data-ttu-id="a67e2-105">Puedes reconocer el marco necesario para planear tu Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="a67e2-105">You can recognize the framework required to plan your Teams app.</span></span> <span data-ttu-id="a67e2-106">El documento te ayuda a comprender la comunicación usuario-aplicación y averiguar el tipo de superficies de aplicación que necesitas usar o las API que la aplicación puede necesitar en el proceso.</span><span class="sxs-lookup"><span data-stu-id="a67e2-106">The document helps you to understand the user-app communication and figure out the kind of app surfaces you need to use or the APIs your app might require in the process.</span></span> <span data-ttu-id="a67e2-107">Obtén algo de inspiración para adoptar la interactividad que puede profundizar la experiencia de la aplicación cuando te integres con Teams.</span><span class="sxs-lookup"><span data-stu-id="a67e2-107">Get some inspiration to embrace interactivity that can deepen the app experience when you integrate with Teams.</span></span>

## <a name="capabilities-and-entry-points"></a><span data-ttu-id="a67e2-108">Capacidades y puntos de entrada</span><span class="sxs-lookup"><span data-stu-id="a67e2-108">Capabilities and entry points</span></span>

<span data-ttu-id="a67e2-109">Puedes extender la aplicación Teams de varias maneras.</span><span class="sxs-lookup"><span data-stu-id="a67e2-109">You can extend your Teams app in multiple ways.</span></span> <span data-ttu-id="a67e2-110">Para poder ampliar la aplicación, debes comprender todas las funcionalidades principales y los puntos de entrada que funcionan en un espacio de colaboración.</span><span class="sxs-lookup"><span data-stu-id="a67e2-110">To be able to extend your app you must understand all the core capabilities and the entry points that work in a collaborative space.</span></span> <span data-ttu-id="a67e2-111">Puedes experimentar con los puntos de extensión para crear tus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a67e2-111">You can experiment with the extension points for building your apps.</span></span> <span data-ttu-id="a67e2-112">Los componentes importantes del proyecto de aplicación te ayudan a configurar correctamente la página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a67e2-112">Important app project components help you to correctly configure your app page.</span></span> <span data-ttu-id="a67e2-113">Teams aplicación puede tener [varias capacidades y](../concepts/capabilities-overview.md) puntos de [entrada.](../concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="a67e2-113">Teams app can have [multiple capabilities](../concepts/capabilities-overview.md) and [entry points](../concepts/extensibility-points.md).</span></span>

## <a name="understand-your-use-cases"></a><span data-ttu-id="a67e2-114">Entender los casos de uso</span><span class="sxs-lookup"><span data-stu-id="a67e2-114">Understand your use cases</span></span>

<span data-ttu-id="a67e2-115">Puede reconocer problemas de usuario e identificar las respuestas a algunos problemas comunes a los que se enfrentan los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a67e2-115">You can recognize user issues and identify the answers to some common problems the users face.</span></span> <span data-ttu-id="a67e2-116">Puedes crear tu aplicación Teams buscando la combinación adecuada para satisfacer las necesidades del usuario.</span><span class="sxs-lookup"><span data-stu-id="a67e2-116">You can build your Teams app by finding the right combination to meet your user's needs.</span></span> <span data-ttu-id="a67e2-117">[Comprender los casos de](../concepts/design/understand-use-cases.md) uso para saber cómo interactúa un usuario final con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a67e2-117">[Understand use cases](../concepts/design/understand-use-cases.md) to know how an end-user interacts with your app.</span></span> <span data-ttu-id="a67e2-118">Aprendes a comprender el usuario y su problema.</span><span class="sxs-lookup"><span data-stu-id="a67e2-118">You learn to understand the user and their problem.</span></span> <span data-ttu-id="a67e2-119">Algunas preguntas comunes que se responden son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="a67e2-119">Some common questions answered are as follows:</span></span>

* <span data-ttu-id="a67e2-120">¿Necesita autenticación?</span><span class="sxs-lookup"><span data-stu-id="a67e2-120">Do you need authentication?</span></span>
* <span data-ttu-id="a67e2-121">¿Qué problema va a solucionar la aplicación?</span><span class="sxs-lookup"><span data-stu-id="a67e2-121">What problem is your app going to solve?</span></span>
* <span data-ttu-id="a67e2-122">Quién Son los usuarios finales de la aplicación?</span><span class="sxs-lookup"><span data-stu-id="a67e2-122">Who are the end-users of the app?</span></span>
* <span data-ttu-id="a67e2-123">¿Cómo debe ser la experiencia de incorporación y qué más puede hacer la aplicación?</span><span class="sxs-lookup"><span data-stu-id="a67e2-123">How should the onboarding experience be and what else the app can do?</span></span>

## <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="a67e2-124">Asignar los casos de uso a Teams funcionalidades de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a67e2-124">Map your use cases to Teams app capabilities</span></span>

<span data-ttu-id="a67e2-125">[Map your use cases](../concepts/design/map-use-cases.md) covers some common scenarios and how to choose your app's capabilities.</span><span class="sxs-lookup"><span data-stu-id="a67e2-125">[Map your use cases](../concepts/design/map-use-cases.md) covers some common scenarios and how to choose your app's capabilities.</span></span> <span data-ttu-id="a67e2-126">Se proporciona información para compartir la aplicación y colaborar en elementos de un sistema externo.</span><span class="sxs-lookup"><span data-stu-id="a67e2-126">Information to share your app and collaborate on items in an external system is provided.</span></span> <span data-ttu-id="a67e2-127">También puede aprender a iniciar flujos de trabajo y enviar notificaciones a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a67e2-127">You can also learn how to initiate workflows and send notifications to users.</span></span> <span data-ttu-id="a67e2-128">Obtén sugerencias adicionales sobre dónde empezar, cómo crear redes sociales con los usuarios, bots de conversación y combinar varias características.</span><span class="sxs-lookup"><span data-stu-id="a67e2-128">Get additional tips on where to start, how to get social with users, conversational bots, and combining multiple features.</span></span>

## <a name="see-also"></a><span data-ttu-id="a67e2-129">Consulte también</span><span class="sxs-lookup"><span data-stu-id="a67e2-129">See also</span></span>

* [<span data-ttu-id="a67e2-130">Integrar aplicaciones web con Teams</span><span class="sxs-lookup"><span data-stu-id="a67e2-130">Integrate web apps with Teams</span></span>](../samples/integrating-web-apps.md)
* [<span data-ttu-id="a67e2-131">Crear la primera Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="a67e2-131">Build your first Microsoft Teams app</span></span>](../build-your-first-app/build-first-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="a67e2-132">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="a67e2-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a67e2-133">Comprender Teams funcionalidades de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a67e2-133">Understand Teams app capabilities</span></span>](capabilities-overview.md)

