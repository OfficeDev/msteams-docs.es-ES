---
title: Autenticación de inicio de sesión único con Team Toolkit y Visual Studio Code para pestañas
description: Crear una pestaña que admita el inicio de sesión único y las llamadas de Microsoft Graph directamente en Visual Studio Code con el kit de herramientas de Microsoft Teams
keywords: Teams Visual Studio Code Toolkit pestañas autenticación de gráfico de SSO plataforma de identidad de Azure
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: fe734143975688cd35c510cd68cd0779a2200a18
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2020
ms.locfileid: "49477739"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="a0185-104">Autenticación de inicio de sesión único con Team Toolkit y Visual Studio Code para pestañas</span><span class="sxs-lookup"><span data-stu-id="a0185-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="a0185-105">El kit de herramientas de Microsoft Teams le permite crear una autenticación de inicio de sesión único (SSO) para las aplicaciones de pestaña directamente en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a0185-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="a0185-106">El kit de herramientas le guiará a través del proceso y le proporcionará todo lo que necesita, incluido el aprovisionamiento del registro de la plataforma de identidad de Microsoft en Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a0185-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="a0185-107">Introducción: crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="a0185-107">Get started — create a project</span></span>

1. <span data-ttu-id="a0185-108">Cree un proyecto nuevo en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="a0185-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="a0185-109">Seleccione Tab como el tipo de extensión que quiera crear.</span><span class="sxs-lookup"><span data-stu-id="a0185-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="a0185-110">Seleccione la opción para admitir SSO.</span><span class="sxs-lookup"><span data-stu-id="a0185-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="a0185-111">Después de la instalación, debería ver Team Toolkit en la barra de actividad del código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0185-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="a0185-112">Si no es así, haga clic con el botón derecho en la barra de actividad y seleccione **Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="a0185-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="a0185-113">Configurar el proyecto</span><span class="sxs-lookup"><span data-stu-id="a0185-113">Configure your project</span></span>

1. <span data-ttu-id="a0185-114">Para habilitar el SSO dentro de Teams, la aplicación debe tener un recurso de registro de la aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="a0185-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="a0185-115">El kit de herramientas de Teams aprovisionará el registro de la aplicación en su nombre.</span><span class="sxs-lookup"><span data-stu-id="a0185-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="a0185-116">Escriba la dirección URL donde se hospedará la aplicación y seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a0185-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="a0185-117">El registro de la aplicación se configurará con la dirección URL proporcionada.</span><span class="sxs-lookup"><span data-stu-id="a0185-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="a0185-118">Los detalles de configuración del registro de la aplicación se almacenarán en los `.env` archivos del código fuente del proyecto.</span><span class="sxs-lookup"><span data-stu-id="a0185-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="a0185-119">Si desea obtener más información sobre cómo se aprovisionará el registro de la aplicación de Azure, _consulte_  nuestra documentación [de pestañas de inicio de sesión único (SSO)](../tabs/how-to/authentication/auth-aad-sso.md) .</span><span class="sxs-lookup"><span data-stu-id="a0185-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="a0185-120">Tendrá que ir a los registros de la **aplicación de Azure** y actualizar el URI de la *API* y *redirigir las direcciones URL* siempre que cambie esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="a0185-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="a0185-121">Ejecutar el proyecto</span><span class="sxs-lookup"><span data-stu-id="a0185-121">Run your project</span></span>

1. <span data-ttu-id="a0185-122">Seleccione **NPM install** desde la `api-server` carpeta.</span><span class="sxs-lookup"><span data-stu-id="a0185-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="a0185-123">A continuación, **NPM Start**.</span><span class="sxs-lookup"><span data-stu-id="a0185-123">Then **npm start**.</span></span>
1. <span data-ttu-id="a0185-124">Seleccione **NPM install** desde la `.src` carpeta.</span><span class="sxs-lookup"><span data-stu-id="a0185-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="a0185-125">A continuación, **NPM Start**.</span><span class="sxs-lookup"><span data-stu-id="a0185-125">Then **npm start**.</span></span>
1. <span data-ttu-id="a0185-126">Si usa un servicio de túnel como [ngrok](https://ngrok.com/), ejecútelo y asegúrese de que la dirección URL coincida con lo que escribió en el Asistente para creación de proyectos.</span><span class="sxs-lookup"><span data-stu-id="a0185-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="a0185-127">Si no es así, tendrá que actualizar el URI de la _API_ y la _dirección URL de redireccionamiento_ en el registro de la aplicación que se creó en Azure.</span><span class="sxs-lookup"><span data-stu-id="a0185-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="a0185-128">Navegue a la barra de actividades en el lado izquierdo de la ventana de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a0185-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="a0185-129">Seleccione el icono **Ejecutar** para mostrar la vista **Ejecutar y depurar** .</span><span class="sxs-lookup"><span data-stu-id="a0185-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="a0185-130">También puede usar el método abreviado de teclado **Ctrl + Mayús + D**.</span><span class="sxs-lookup"><span data-stu-id="a0185-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="a0185-131">Es posible que no vea el cuadro de diálogo de instalación de la aplicación en el explorador si las ventanas emergentes están deshabilitadas para el explorador.</span><span class="sxs-lookup"><span data-stu-id="a0185-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="a0185-132">Si esto ocurre, habilite las ventanas emergentes y actualice la página.</span><span class="sxs-lookup"><span data-stu-id="a0185-132">If this happens, enable pop-up windows and refresh the page.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a0185-133">Más información: crear aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a0185-133">Learn more: Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
