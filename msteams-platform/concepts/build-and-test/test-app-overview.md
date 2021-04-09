---
title: Introducción a la prueba de la aplicación
description: Describe el proceso para probar la aplicación personalizada de Teams en Microsoft 365
ms.topic: how-to
keywords: Configurar microsoft 365 inquilino Teams cargar aplicación de prueba
ms.openlocfilehash: b199ca4be31b546364091b754cdb890c8c0dd7d0
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634782"
---
# <a name="test-your-app"></a><span data-ttu-id="966ea-104">Probar la aplicación</span><span class="sxs-lookup"><span data-stu-id="966ea-104">Test your app</span></span>

<span data-ttu-id="966ea-105">Después de integrar la aplicación con Microsoft Teams, debes probar la aplicación antes de publicarla.</span><span class="sxs-lookup"><span data-stu-id="966ea-105">After integrating your app with Microsoft Teams, you must test your app before publishing it.</span></span> <span data-ttu-id="966ea-106">El objetivo final es obtener tantos usuarios para tu aplicación, por lo tanto, asegúrate de probar la aplicación en varios dispositivos que los usuarios podrían usar.</span><span class="sxs-lookup"><span data-stu-id="966ea-106">The ultimate goal is to get as many users for your app, therefore, ensure to test the app on multiple devices that users could use.</span></span> <span data-ttu-id="966ea-107">Para probar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="966ea-107">For testing your app:</span></span>

* <span data-ttu-id="966ea-108">Preparar el espacio empresarial de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="966ea-108">Prepare your Microsoft 365 tenant</span></span>
* <span data-ttu-id="966ea-109">Elegir un área de trabajo para probar y depurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="966ea-109">Choose a workspace to test and debug your app</span></span>
* <span data-ttu-id="966ea-110">Agregar datos de prueba al inquilino de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="966ea-110">Add test data to your Microsoft 365 tenant</span></span>

## <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="966ea-111">Preparar el espacio empresarial de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="966ea-111">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="966ea-112">Antes de empezar a probar la aplicación, prepare el inquilino de prueba de Microsoft 365 y habilite la aplicación personalizada de Teams que le permita cargar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="966ea-112">Before you start testing your app, prepare your Microsoft 365 test tenant and enable custom Teams app allow you to upload your app.</span></span> <span data-ttu-id="966ea-113">Debe registrarse en el programa para desarrolladores de Microsoft 365 y administrar la configuración de Teams para su organización.</span><span class="sxs-lookup"><span data-stu-id="966ea-113">You must sign-up for Microsoft 365 developer program and manage the Teams settings for your organization.</span></span> <span data-ttu-id="966ea-114">Configure la suscripción de desarrollador y configúrela a través [de preparar el inquilino de Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="966ea-114">Set up your developer subscription and configure it through [prepare your Microsoft 365 Tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

## <a name="test-and-debug"></a><span data-ttu-id="966ea-115">Probar y depurar</span><span class="sxs-lookup"><span data-stu-id="966ea-115">Test and debug</span></span>

<span data-ttu-id="966ea-116">Para probar y depurar la aplicación, debes crear al menos un área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="966ea-116">To test and debug your app, you must create at least one workspace.</span></span> <span data-ttu-id="966ea-117">Puedes seleccionar una configuración de prueba, como host local o host basado en la nube para probar y depurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="966ea-117">You can select a test setup, such as local host or cloud-based host to test and debug the app.</span></span> <span data-ttu-id="966ea-118">Se proporcionan instrucciones para depurar la aplicación de Teams para cargar y ejecutar la experiencia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="966ea-118">Guidance to debug your Teams app is provided to load and run your app experience.</span></span> <span data-ttu-id="966ea-119">Para obtener más información, [consulta elegir una configuración y ejecutar la aplicación de Microsoft Teams](~/concepts/build-and-test/debug.md).</span><span class="sxs-lookup"><span data-stu-id="966ea-119">For more information, see [choose a set up and run your Microsoft Teams app](~/concepts/build-and-test/debug.md).</span></span>

<span data-ttu-id="966ea-120">Pruebe el bot localmente.</span><span class="sxs-lookup"><span data-stu-id="966ea-120">Test your bot locally.</span></span> <span data-ttu-id="966ea-121">Para obtener más información, [vea depurar el bot localmente con un IDE](~/bots/how-to/debug/locally-with-an-ide.md).</span><span class="sxs-lookup"><span data-stu-id="966ea-121">For more information, see [debug your bot locally with an IDE](~/bots/how-to/debug/locally-with-an-ide.md).</span></span> <span data-ttu-id="966ea-122">También puede depurar el bot con software intermedio [de inspección](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) y [herramientas adaptables.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="966ea-122">You can also debug your bot with [inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) and [adaptive tools](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).</span></span> 

<span data-ttu-id="966ea-123">Para ver los registros de la consola, ver o modificar las solicitudes html, css y de red durante el tiempo de ejecución, agregue puntos de interrupción al código JavaScript y realice la depuración interactiva para obtener acceso a DevTools.</span><span class="sxs-lookup"><span data-stu-id="966ea-123">To view the console logs, view or modify html, css, and network requests during runtime, add breakpoints to your JavaScript code, and perform interactive debugging access the DevTools.</span></span> <span data-ttu-id="966ea-124">Para obtener más información, [vea Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md).</span><span class="sxs-lookup"><span data-stu-id="966ea-124">For more information, see [Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md).</span></span> 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a><span data-ttu-id="966ea-125">Agregar datos de prueba al inquilino de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="966ea-125">Add test data to your Microsoft 365 tenant</span></span>

<span data-ttu-id="966ea-126">Agregue los datos de prueba al inquilino de prueba de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="966ea-126">Add the test data to Microsoft 365 test tenant.</span></span> <span data-ttu-id="966ea-127">Para obtener más información, vea Agregar datos de prueba al inquilino de prueba de [Office 365](~/concepts/build-and-test/test-data.md)y completar todos los requisitos previos antes de empezar a cargar los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="966ea-127">For more information, see [add test data to your Office 365 test tenant](~/concepts/build-and-test/test-data.md), and complete all the prerequisites before you start uploading your test data.</span></span>

## <a name="see-also"></a><span data-ttu-id="966ea-128">Vea también</span><span class="sxs-lookup"><span data-stu-id="966ea-128">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="966ea-129">Depurar la pestaña</span><span class="sxs-lookup"><span data-stu-id="966ea-129">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="966ea-130">Depurar los bots</span><span class="sxs-lookup"><span data-stu-id="966ea-130">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="966ea-131">Probar permisos de RSC</span><span class="sxs-lookup"><span data-stu-id="966ea-131">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a><span data-ttu-id="966ea-132">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="966ea-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="966ea-133">Preparar el espacio empresarial de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="966ea-133">Prepare your Microsoft 365 tenant</span></span>](~/concepts/build-and-test/prepare-your-o365-tenant.md)
