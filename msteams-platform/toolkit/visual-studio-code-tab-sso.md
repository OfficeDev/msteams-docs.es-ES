---
title: Autenticación de inicio de sesión único con Teams Toolkit y Visual Studio Code para pestañas
description: Cree una pestaña que admita el inicio de sesión único y microsoft Graph llamadas directamente dentro de Visual Studio Code con el Microsoft Teams Toolkit
keywords: Teams visual studio code toolkit tabs sso graph authentication Azure identity platform
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 2ef409a45b92240cced09d2d77793af33945589e
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721818"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="27e2a-104">Autenticación de inicio de sesión único con Teams Toolkit y Visual Studio Code para pestañas</span><span class="sxs-lookup"><span data-stu-id="27e2a-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27e2a-105">**Este documento hace referencia a una versión antigua de Teams Toolkit**</span><span class="sxs-lookup"><span data-stu-id="27e2a-105">**This document refers to an old version of Teams Toolkit**</span></span>
>
> <span data-ttu-id="27e2a-106">Para obtener información actual, lea los [requisitos previos](../get-started/prerequisites.md) y siga uno de los tutoriales más recientes.</span><span class="sxs-lookup"><span data-stu-id="27e2a-106">For current information, read the [prerequisites](../get-started/prerequisites.md) and follow  one of the newer tutorials.</span></span>

<span data-ttu-id="27e2a-107">La Microsoft Teams Toolkit permite crear la autenticación de inicio de sesión único (SSO) para aplicaciones de pestañas directamente en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="27e2a-107">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="27e2a-108">El kit de herramientas lo guía a través del proceso y proporciona todo lo que necesita, incluido el aprovisionamiento Plataforma de identidad de Microsoft registro en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="27e2a-108">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="27e2a-109">Introducción: crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="27e2a-109">Get started — create a project</span></span>

1. <span data-ttu-id="27e2a-110">Cree un nuevo proyecto en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="27e2a-110">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="27e2a-111">Seleccione la pestaña como el tipo de extensión que desea crear.</span><span class="sxs-lookup"><span data-stu-id="27e2a-111">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="27e2a-112">Seleccione la opción para admitir SSO.</span><span class="sxs-lookup"><span data-stu-id="27e2a-112">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="27e2a-113">Después de la instalación, debería ver el Teams Toolkit en la barra Visual Studio Code actividad.</span><span class="sxs-lookup"><span data-stu-id="27e2a-113">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="27e2a-114">Si no es así, haga clic con el botón secundario en la barra de actividades **y seleccione Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="27e2a-114">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="27e2a-115">Configurar el proyecto</span><span class="sxs-lookup"><span data-stu-id="27e2a-115">Configure your project</span></span>

1. <span data-ttu-id="27e2a-116">Para habilitar SSO en Teams, la aplicación debe tener un recurso de registro de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="27e2a-116">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="27e2a-117">El Teams Toolkit aprovisionará el registro de la aplicación en su nombre.</span><span class="sxs-lookup"><span data-stu-id="27e2a-117">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="27e2a-118">Escribe la dirección URL donde se hospedará la aplicación y selecciona **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="27e2a-118">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="27e2a-119">El registro de la aplicación se configurará con la dirección URL proporcionada.</span><span class="sxs-lookup"><span data-stu-id="27e2a-119">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="27e2a-120">Los detalles de configuración del registro de la aplicación se almacenarán en `.env` los archivos del código fuente del proyecto.</span><span class="sxs-lookup"><span data-stu-id="27e2a-120">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="27e2a-121">Si desea obtener más información sobre cómo se aprovisionará  el registro de la aplicación de Azure, consulte nuestra documentación sobre el inicio de sesión único [(SSO) para las pestañas.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="27e2a-121">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="27e2a-122">Tendrá que ir a Registros de aplicaciones de **Azure** y actualizar el URI de *la API* y redirigir las direcciones *URL* siempre que cambie esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="27e2a-122">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="27e2a-123">Ejecutar el proyecto</span><span class="sxs-lookup"><span data-stu-id="27e2a-123">Run your project</span></span>

1. <span data-ttu-id="27e2a-124">Seleccione **npm install** en la `api-server` carpeta.</span><span class="sxs-lookup"><span data-stu-id="27e2a-124">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="27e2a-125">A **continuación, npm start**.</span><span class="sxs-lookup"><span data-stu-id="27e2a-125">Then **npm start**.</span></span>
1. <span data-ttu-id="27e2a-126">Seleccione **npm install** en la `.src` carpeta.</span><span class="sxs-lookup"><span data-stu-id="27e2a-126">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="27e2a-127">A **continuación, npm start**.</span><span class="sxs-lookup"><span data-stu-id="27e2a-127">Then **npm start**.</span></span>
1. <span data-ttu-id="27e2a-128">Si usa un servicio de túnel como [ngrok,](https://ngrok.com/)ejecutelo y asegúrese de que la dirección URL coincida con lo que ha escrito en el asistente para la creación del proyecto.</span><span class="sxs-lookup"><span data-stu-id="27e2a-128">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="27e2a-129">Si no lo hace, deberá actualizar el URI de _la API_ y redirigir la _dirección URL_ en el registro de la aplicación que se creó en Azure.</span><span class="sxs-lookup"><span data-stu-id="27e2a-129">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="27e2a-130">Vaya a la barra de actividades de la parte izquierda de la ventana Visual Studio Code actividad.</span><span class="sxs-lookup"><span data-stu-id="27e2a-130">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="27e2a-131">Seleccione el **icono Ejecutar** para mostrar la vista **Ejecutar y** depurar.</span><span class="sxs-lookup"><span data-stu-id="27e2a-131">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="27e2a-132">También puede usar el método abreviado de **teclado Ctrl+Mayús+D**.</span><span class="sxs-lookup"><span data-stu-id="27e2a-132">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="27e2a-133">Es posible que no veas el diálogo de instalación de la aplicación en el explorador si las ventanas emergentes están deshabilitadas para el explorador.</span><span class="sxs-lookup"><span data-stu-id="27e2a-133">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="27e2a-134">Si esto sucede, habilita las ventanas emergentes y actualiza la página.</span><span class="sxs-lookup"><span data-stu-id="27e2a-134">If this happens, enable pop-up windows and refresh the page.</span></span>

## <a name="see-also"></a><span data-ttu-id="27e2a-135">Ver también</span><span class="sxs-lookup"><span data-stu-id="27e2a-135">See also</span></span>

[<span data-ttu-id="27e2a-136">Crear aplicaciones con el Microsoft Teams Toolkit y Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="27e2a-136">Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
