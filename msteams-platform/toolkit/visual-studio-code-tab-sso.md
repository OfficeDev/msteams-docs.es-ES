---
title: Autenticación de inicio de sesión único con Teams Toolkit y Visual Studio Code para pestañas
description: Cree una pestaña que admita llamadas de inicio de sesión único y Microsoft Graph directamente dentro de Visual Studio Code con la Microsoft Teams Toolkit
keywords: equipos visual studio toolkit pestañas sso graph authentication Plataforma de identidad de Azure
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 11e642ce335dae4344f1c730b73763e9172fd76c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566834"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="a33c5-104">Autenticación de inicio de sesión único con Teams Toolkit y Visual Studio Code para pestañas</span><span class="sxs-lookup"><span data-stu-id="a33c5-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="a33c5-105">El Microsoft Teams Toolkit le permite crear autenticación de inicio de sesión único (SSO) para aplicaciones de pestañas directamente dentro de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a33c5-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="a33c5-106">El kit de herramientas le guía a través del proceso y proporciona todo lo que necesita, incluido el aprovisionamiento del registro de Plataforma de identidad de Microsoft en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a33c5-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="a33c5-107">Empezar: cree un proyecto</span><span class="sxs-lookup"><span data-stu-id="a33c5-107">Get started — create a project</span></span>

1. <span data-ttu-id="a33c5-108">Cree un nuevo proyecto en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="a33c5-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="a33c5-109">Seleccione la pestaña como el tipo de extensión que desea crear.</span><span class="sxs-lookup"><span data-stu-id="a33c5-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="a33c5-110">Seleccione la opción para admitir SSO.</span><span class="sxs-lookup"><span data-stu-id="a33c5-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="a33c5-111">Después de la instalación, debería ver la Teams Toolkit en la barra de actividades Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a33c5-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="a33c5-112">Si no es así, haga clic con el botón derecho en la barra de actividades y seleccione **Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="a33c5-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="a33c5-113">Configure el proyecto</span><span class="sxs-lookup"><span data-stu-id="a33c5-113">Configure your project</span></span>

1. <span data-ttu-id="a33c5-114">Para habilitar SSO dentro de Teams, la aplicación debe tener un recurso de registro de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="a33c5-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="a33c5-115">El Teams Toolkit aprovisionará el registro de la aplicación en su nombre.</span><span class="sxs-lookup"><span data-stu-id="a33c5-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="a33c5-116">Escriba la dirección URL donde se hospedará la aplicación y seleccione **la siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a33c5-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="a33c5-117">El registro de la aplicación se configurará con la dirección URL proporcionada.</span><span class="sxs-lookup"><span data-stu-id="a33c5-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="a33c5-118">Los detalles de configuración del registro de la aplicación se almacenarán en los `.env` archivos del código fuente del proyecto.</span><span class="sxs-lookup"><span data-stu-id="a33c5-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="a33c5-119">Si desea obtener más información sobre cómo se aprovisionará el registro de la aplicación de Azure, _consulte_ nuestra [compatibilidad con el inicio de sesión único (SSO) para obtener documentación sobre pestañas.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="a33c5-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="a33c5-120">Deberá ir a **Azure App Registrations** y actualizar el *URI* de la API y *redirigir las direcciones URL* cada vez que cambie esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="a33c5-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="a33c5-121">Ejecute su proyecto</span><span class="sxs-lookup"><span data-stu-id="a33c5-121">Run your project</span></span>

1. <span data-ttu-id="a33c5-122">Seleccione **npm install** en la `api-server` carpeta.</span><span class="sxs-lookup"><span data-stu-id="a33c5-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="a33c5-123">A **continuación, npm iniciar**.</span><span class="sxs-lookup"><span data-stu-id="a33c5-123">Then **npm start**.</span></span>
1. <span data-ttu-id="a33c5-124">Seleccione **npm install** en la `.src` carpeta.</span><span class="sxs-lookup"><span data-stu-id="a33c5-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="a33c5-125">A **continuación, npm iniciar**.</span><span class="sxs-lookup"><span data-stu-id="a33c5-125">Then **npm start**.</span></span>
1. <span data-ttu-id="a33c5-126">Si está utilizando un servicio de tunelización como [ngrok,](https://ngrok.com/)ejecute y asegúrese de que la dirección URL coincide con lo que ha especificado en el asistente de creación de proyectos.</span><span class="sxs-lookup"><span data-stu-id="a33c5-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="a33c5-127">Si no es así, deberá actualizar el _URI_ de la API y _redirigir_ la dirección URL en el registro de la aplicación que se creó en Azure.</span><span class="sxs-lookup"><span data-stu-id="a33c5-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="a33c5-128">Vaya a la barra de actividades en el lado izquierdo de la ventana de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a33c5-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="a33c5-129">Seleccione el icono **Ejecutar** para mostrar la vista **Ejecutar y depurar.**</span><span class="sxs-lookup"><span data-stu-id="a33c5-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="a33c5-130">También puede utilizar el método abreviado de teclado **Ctrl+Mayús+D**.</span><span class="sxs-lookup"><span data-stu-id="a33c5-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="a33c5-131">Es posible que no vea el diálogo de instalación de la aplicación en el explorador si las ventanas emergentes están deshabilitadas para su navegador.</span><span class="sxs-lookup"><span data-stu-id="a33c5-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="a33c5-132">Si esto sucede, habilite las ventanas emergentes y actualice la página.</span><span class="sxs-lookup"><span data-stu-id="a33c5-132">If this happens, enable pop-up windows and refresh the page.</span></span>

## <a name="see-also"></a><span data-ttu-id="a33c5-133">Vea también</span><span class="sxs-lookup"><span data-stu-id="a33c5-133">See also</span></span>

- [<span data-ttu-id="a33c5-134">Cree aplicaciones con el Microsoft Teams Toolkit y el Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a33c5-134">Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
