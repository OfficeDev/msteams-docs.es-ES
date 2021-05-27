---
title: Administrar las aplicaciones con el Portal de desarrolladores
description: Aprende a administrar tus aplicaciones mediante el Portal de desarrolladores para Microsoft Teams.
keywords: introducción a los equipos del portal de desarrolladores
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 950ca7e09f5b87647cb62b66a545a0b1cec33a7d
ms.sourcegitcommit: 25c02757fe207cdff916ba63aa215f88e24e1d6f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/26/2021
ms.locfileid: "52667449"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a><span data-ttu-id="d6416-104">Administrar tus aplicaciones con el Portal de desarrolladores para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d6416-104">Manage your apps with the Developer Portal for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="d6416-105">El Portal de desarrolladores para Teams está actualmente en [la versión preliminar del desarrollador público.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="d6416-105">The Developer Portal for Teams is currently in [public developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

<span data-ttu-id="d6416-106">Portal <a href="https://dev.teams.microsoft.com" target="_blank">para desarrolladores para Teams</a> es la herramienta principal para configurar, distribuir y administrar las aplicaciones Microsoft Teams aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d6416-106">The <a href="https://dev.teams.microsoft.com" target="_blank">Developer Portal for Teams</a> is the primary tool for configuring, distributing, and managing your Microsoft Teams apps.</span></span> <span data-ttu-id="d6416-107">Con el Portal de desarrolladores, puedes colaborar con compañeros de la aplicación, configurar entornos en tiempo de ejecución y mucho más.</span><span class="sxs-lookup"><span data-stu-id="d6416-107">With the Developer Portal, you can collaborate with colleagues on your app, set up runtime environments, and much more.</span></span>

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="Captura de pantalla que muestra la página principal del Portal de desarrolladores para Teams.":::

## <a name="register-an-app"></a><span data-ttu-id="d6416-109">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="d6416-109">Register an app</span></span>

<span data-ttu-id="d6416-110">El Portal de desarrolladores proporciona un par de formas de registrar una Teams aplicación:</span><span class="sxs-lookup"><span data-stu-id="d6416-110">The Developer Portal provides a couple ways to register a Teams app:</span></span>

* <span data-ttu-id="d6416-111">Registrar una aplicación nueva</span><span class="sxs-lookup"><span data-stu-id="d6416-111">Register a brand new app</span></span>
* <span data-ttu-id="d6416-112">Importar un paquete de aplicación existente</span><span class="sxs-lookup"><span data-stu-id="d6416-112">Import an existing app package</span></span>

> [!NOTE]
> <span data-ttu-id="d6416-113">Si creas una aplicación con el [Microsoft Teams Toolkit para Visual Studio Code,](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)puedes administrarla en el Portal de desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="d6416-113">If you create an app using the [Microsoft Teams Toolkit for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension), you can manage that app in the Developer Portal.</span></span>

## <a name="set-up-an-environment"></a><span data-ttu-id="d6416-114">Configurar un entorno</span><span class="sxs-lookup"><span data-stu-id="d6416-114">Set up an environment</span></span>

<span data-ttu-id="d6416-115">Puedes configurar entornos y variables globales para ayudar a la transición de la aplicación de tu tiempo de ejecución local a la producción.</span><span class="sxs-lookup"><span data-stu-id="d6416-115">You can configure environments and global variables to help transition your app from your local runtime to production.</span></span> <span data-ttu-id="d6416-116">Las variables globales se usan en todos los entornos.</span><span class="sxs-lookup"><span data-stu-id="d6416-116">Global variables are used across all environments.</span></span>

<span data-ttu-id="d6416-117">**Para configurar un entorno**</span><span class="sxs-lookup"><span data-stu-id="d6416-117">**To set up an environment**</span></span>

1. <span data-ttu-id="d6416-118">En el Portal de desarrolladores, selecciona la aplicación en la que estás trabajando.</span><span class="sxs-lookup"><span data-stu-id="d6416-118">In the Developer Portal, select the app you're working on.</span></span>
2. <span data-ttu-id="d6416-119">Vaya a la **página Entornos** y seleccione **+ Agregar un entorno**.</span><span class="sxs-lookup"><span data-stu-id="d6416-119">Go to the **Environments** page and select **+ Add an environment**.</span></span>
3. <span data-ttu-id="d6416-120">Seleccione **+ Agregar una variable** para crear variables de configuración para su entorno.</span><span class="sxs-lookup"><span data-stu-id="d6416-120">Select **+ Add a variable** to create configuration variables for your environment.</span></span>

<span data-ttu-id="d6416-121">**Para usar variables**</span><span class="sxs-lookup"><span data-stu-id="d6416-121">**To use variables**</span></span>

<span data-ttu-id="d6416-122">Usa los nombres de las variables en lugar de los valores codificados de forma automática para establecer las configuraciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6416-122">Use the variable names instead of hard-coded values to set your app configurations.</span></span>

1. <span data-ttu-id="d6416-123">Escriba `{{` en cualquier campo del Portal de desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="d6416-123">Enter `{{` in any field in the Developer Portal.</span></span> <span data-ttu-id="d6416-124">Aparece un desplegable con todas las variables creadas para el entorno elegido junto con las variables globales.</span><span class="sxs-lookup"><span data-stu-id="d6416-124">A dropdown with all the variables you've created for the chosen environment along with the global variables appears.</span></span>  
1. <span data-ttu-id="d6416-125">Antes de descargar el paquete de la aplicación (por ejemplo, al prepararse para publicar en la tienda Teams), selecciona el entorno que quieras usar.</span><span class="sxs-lookup"><span data-stu-id="d6416-125">Before downloading your app package (for example, when getting ready to publish to the Teams store), select the environment you want to use.</span></span> <span data-ttu-id="d6416-126">Las configuraciones de la aplicación se actualizan automáticamente en función del entorno.</span><span class="sxs-lookup"><span data-stu-id="d6416-126">Your app configurations update automatically based on the environment.</span></span> 

## <a name="identify-app-owners"></a><span data-ttu-id="d6416-127">Identificar propietarios de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d6416-127">Identify app owners</span></span>

<span data-ttu-id="d6416-128">Cada aplicación incluye una **página Propietarios,** donde puedes compartir el registro de la aplicación con compañeros de la organización. El **rol Colaborador** tiene los mismos permisos que el rol **Propietario,** excepto la capacidad de eliminar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6416-128">Each app includes an **Owners** page, where you can share your app registration with colleagues in your org. The **Contributor** role has the same permissions as the **Owner** role except the ability to delete an app.</span></span>

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a><span data-ttu-id="d6416-129">Configurar las capacidades de la aplicación y otros metadatos importantes</span><span class="sxs-lookup"><span data-stu-id="d6416-129">Configure your app's capabilities and other important metadata</span></span>

<span data-ttu-id="d6416-130">Una Teams es una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d6416-130">A Teams app is a web app.</span></span> <span data-ttu-id="d6416-131">Al igual que todas las aplicaciones web, su código fuente normalmente se desarrolla en un IDE o editor de código y se hospeda en algún lugar de la nube (como Azure).</span><span class="sxs-lookup"><span data-stu-id="d6416-131">Like all web apps, its source code is typically developed in an IDE or code editor and hosted somewhere in the cloud (like Azure).</span></span>

<span data-ttu-id="d6416-132">Para instalar y representar la aplicación en Teams, debes incluir un conjunto de configuraciones que Teams reconoce.</span><span class="sxs-lookup"><span data-stu-id="d6416-132">To install and render your app in Teams, you must include a set of configurations that Teams recognizes.</span></span> <span data-ttu-id="d6416-133">Esto se ha hecho tradicionalmente mediante la creación de un manifiesto de aplicación, un archivo JSON que contiene todos los metadatos Teams debe mostrar el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6416-133">This has traditionally been done by crafting an app manifest, a JSON file that contains all the metadata Teams needs to display your app content.</span></span> <span data-ttu-id="d6416-134">El Portal de desarrolladores abstrae este proceso e incluye nuevas características y herramientas para ayudarle a tener más éxito.</span><span class="sxs-lookup"><span data-stu-id="d6416-134">The Developer Portal abstracts this process and includes new features and tooling to help you be more successful.</span></span>

## <a name="test-your-app-directly-in-teams"></a><span data-ttu-id="d6416-135">Prueba la aplicación directamente en Teams</span><span class="sxs-lookup"><span data-stu-id="d6416-135">Test your app directly in Teams</span></span>

<span data-ttu-id="d6416-136">El Portal de desarrolladores proporciona opciones para probar y depurar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="d6416-136">The Developer Portal provides options for testing and debugging your app:</span></span>

* <span data-ttu-id="d6416-137">En la **página Información** general, puedes ver una instantánea de si las configuraciones de la aplicación se validan Teams casos de prueba de la tienda.</span><span class="sxs-lookup"><span data-stu-id="d6416-137">On the **Overview** page, you can see a snapshot of whether your app's configurations validate against Teams store test cases.</span></span>
* <span data-ttu-id="d6416-138">El **botón Vista previa Teams** permite iniciar la aplicación rápidamente en el Teams de depuración.</span><span class="sxs-lookup"><span data-stu-id="d6416-138">The **Preview in Teams** button lets you launch your app quickly in the Teams client for debugging.</span></span>

## <a name="distribute-your-app"></a><span data-ttu-id="d6416-139">Distribuir la aplicación</span><span class="sxs-lookup"><span data-stu-id="d6416-139">Distribute your app</span></span>

<span data-ttu-id="d6416-140">En el Portal de  desarrolladores, usa el botón Distribuir para descargar un paquete de aplicación, publicar en tu organización o publicar en la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6416-140">From the Developer Portal, use the **Distribute** button to download an app package, publish to your org, or publish to the Teams store.</span></span>

<span data-ttu-id="d6416-141">Para obtener más información, [consulta distribuir la Teams aplicación](~/concepts/deploy-and-publish/apps-publish-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6416-141">For more information, see [distribute your Teams app](~/concepts/deploy-and-publish/apps-publish-overview.md).</span></span>

## <a name="analyze-your-apps-usage"></a><span data-ttu-id="d6416-142">Analizar el uso de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d6416-142">Analyze your app's usage</span></span>

<span data-ttu-id="d6416-143">En la **página Información** general, puedes ver el número total de usuarios activos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6416-143">On the **Overview** page, you can see the total number of active users for your app.</span></span> <span data-ttu-id="d6416-144">Estas métricas están disponibles para las aplicaciones publicadas en la tienda Teams o en el catálogo de aplicaciones de una organización a través del Portal de desarrolladores y están en el ámbito del identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6416-144">These metrics are available for apps published to the Teams store or an org's app catalog through Developer Portal and scoped to the app ID.</span></span>

| <span data-ttu-id="d6416-145">Métrica</span><span class="sxs-lookup"><span data-stu-id="d6416-145">Metric</span></span> | <span data-ttu-id="d6416-146">Definición</span><span class="sxs-lookup"><span data-stu-id="d6416-146">Definition</span></span> |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d6416-147">*R30 mensual*</span><span class="sxs-lookup"><span data-stu-id="d6416-147">*Monthly R30*</span></span> | <span data-ttu-id="d6416-148">Métrica de uso predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d6416-148">The default usage metric.</span></span> <span data-ttu-id="d6416-149">Muestra el recuento de usuarios activos únicos que usaron la aplicación dentro de esa ventana móvil de 30 días en UTC.</span><span class="sxs-lookup"><span data-stu-id="d6416-149">It shows you the count of unique active users that used your app within that rolling 30-day window in UTC.</span></span> |
| <span data-ttu-id="d6416-150">*Diario*</span><span class="sxs-lookup"><span data-stu-id="d6416-150">*Daily*</span></span> | <span data-ttu-id="d6416-151">Muestra el recuento de usuarios activos únicos que usaron la aplicación en un día determinado en UTC.</span><span class="sxs-lookup"><span data-stu-id="d6416-151">Shows you the count of unique active users that used your app in a given day in UTC.</span></span> |

<span data-ttu-id="d6416-152">El uso mensual y diario se muestra durante los últimos siete, 30 días y 60 días.</span><span class="sxs-lookup"><span data-stu-id="d6416-152">Monthly and daily usage is shown for the past seven, 30 days, and 60 days.</span></span> <span data-ttu-id="d6416-153">Debería ver el uso reflejado durante un día determinado en un plazo de 24-48 horas.</span><span class="sxs-lookup"><span data-stu-id="d6416-153">You should see usage reflected for a given day within 24-48 hours.</span></span> <span data-ttu-id="d6416-154">El uso de nuevas aplicaciones puede tardar entre 3 y 5 días en mostrarse.</span><span class="sxs-lookup"><span data-stu-id="d6416-154">Usage for new apps can take up to 3-5 days to display.</span></span>

## <a name="use-tools-to-create-app-features"></a><span data-ttu-id="d6416-155">Usar herramientas para crear características de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d6416-155">Use tools to create app features</span></span>

<span data-ttu-id="d6416-156">El Portal de desarrolladores también incluye herramientas que le ayudarán a crear algunas características clave de Teams aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d6416-156">The Developer Portal also includes tools to help you build some key features of Teams apps.</span></span> <span data-ttu-id="d6416-157">Algunas de estas herramientas incluyen:</span><span class="sxs-lookup"><span data-stu-id="d6416-157">Some of these tools include:</span></span>

* <span data-ttu-id="d6416-158">**Scene studio:** diseñe escenas personalizadas del modo Together para Teams reuniones.</span><span class="sxs-lookup"><span data-stu-id="d6416-158">**Scene studio**: Design custom Together mode scenes for Teams meetings.</span></span>
* <span data-ttu-id="d6416-159">**Editor de tarjetas adaptables:** crea y previsualiza tarjetas adaptables para incluir con tus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d6416-159">**Adaptive Cards editor**: Create and preview Adaptive Cards to include with your apps.</span></span>
* <span data-ttu-id="d6416-160">**Plataforma de identidad de Microsoft:** registre sus aplicaciones con Azure Active Directory (Azure AD) para ayudar a los usuarios a iniciar sesión y proporcionar acceso a las API.</span><span class="sxs-lookup"><span data-stu-id="d6416-160">**Microsoft identity platform management**: Register your apps with Azure Active Directory (Azure AD) to help users sign in and provide access to APIs.</span></span>
