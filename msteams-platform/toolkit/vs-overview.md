---
title: Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente en Visual Studio con el kit de herramientas de Microsoft Teams
keywords: Teams Visual Studio Toolkit
ms.date: 06/30/2020
ms.openlocfilehash: e5715cf23cfd221b65afe0e6258ce06ff98770aa
ms.sourcegitcommit: 694babb79d379360a20cf928a9d2b88dd6d3bdd0
ms.translationtype: Auto
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2020
ms.locfileid: "45051734"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a><span data-ttu-id="162e7-104">Compilar aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio</span><span class="sxs-lookup"><span data-stu-id="162e7-104">Build apps with the Microsoft Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="162e7-105">El kit de herramientas de Microsoft Teams permite crear aplicaciones de Team personalizadas directamente en el entorno de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="162e7-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio environment.</span></span> <span data-ttu-id="162e7-106">El kit de herramientas le guiará por el proceso y le proporciona todo lo que necesita para crear, depurar e iniciar la aplicación de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="162e7-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="162e7-107">Instalación de Team Toolkit</span><span class="sxs-lookup"><span data-stu-id="162e7-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="162e7-108">El kit de herramientas de Microsoft Teams para Visual Studio está disponible para su descarga desde [Visual Studio Marketplace](https://aka.ms/teams-toolkit) o directamente como una extensión en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="162e7-108">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="162e7-109">Uso del kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="162e7-109">Using the toolkit</span></span>

- [<span data-ttu-id="162e7-110">Configurar un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="162e7-110">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="162e7-111">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="162e7-111">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="162e7-112">Empaquetar la aplicación</span><span class="sxs-lookup"><span data-stu-id="162e7-112">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="162e7-113">Ejecutar la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="162e7-113">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="162e7-114">Validar la aplicación</span><span class="sxs-lookup"><span data-stu-id="162e7-114">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="162e7-115">Publicar la aplicación</span><span class="sxs-lookup"><span data-stu-id="162e7-115">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="162e7-116">Configurar un nuevo proyecto de Teams</span><span class="sxs-lookup"><span data-stu-id="162e7-116">Set up a new Teams project</span></span>

1. <span data-ttu-id="162e7-117">Cree un nuevo proyecto y seleccione la plantilla Microsoft Terams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="162e7-117">Create a new project and select the Microsoft Terams Toolkit template.</span></span>
1. <span data-ttu-id="162e7-118">Llegará a la pantalla **Agregar funcionalidad** para configurar las propiedades de la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="162e7-118">You will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="162e7-119">Seleccione el botón **Finalizar** para completar el proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="162e7-119">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="162e7-120">Configurar la aplicación</span><span class="sxs-lookup"><span data-stu-id="162e7-120">Configure your app</span></span>

<span data-ttu-id="162e7-121">En esencia, la aplicación de Microsoft Teams adopta tres componentes:</span><span class="sxs-lookup"><span data-stu-id="162e7-121">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="162e7-122">El cliente de Microsoft Teams (Web, escritorio o móvil) donde los usuarios interactúan con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="162e7-122">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="162e7-123">Un servidor que responde a las solicitudes de contenido que se mostrarán en Microsoft Teams, por ejemplo, contenido de la ficha HTML o una tarjeta adaptable de bot.</span><span class="sxs-lookup"><span data-stu-id="162e7-123">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="162e7-124">Un paquete de la [aplicación](/concepts/build-and-test/apps-package.md) teams que consta de tres archivos:</span><span class="sxs-lookup"><span data-stu-id="162e7-124">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="162e7-125">La manifest.jsen</span><span class="sxs-lookup"><span data-stu-id="162e7-125">The manifest.json</span></span> 
  > - <span data-ttu-id="162e7-126">Un [icono de color](../resources/schema/manifest-schema.md#icons) de la aplicación para que se muestre en el catálogo de aplicaciones públicas o de la organización</span><span class="sxs-lookup"><span data-stu-id="162e7-126">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="162e7-127">Un [icono de esquema](../resources/schema/manifest-schema.md#icons) para mostrar en la barra de actividad de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="162e7-127">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="162e7-128">Cuando se instala una aplicación, el cliente de Microsoft Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL en la que se encuentran los servicios.</span><span class="sxs-lookup"><span data-stu-id="162e7-128">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="162e7-129">Para configurar la aplicación, navegue a la ventana de extensiones de **Microsoft Team Toolkit** .</span><span class="sxs-lookup"><span data-stu-id="162e7-129">To configure your app, navigate to the **Microsoft Teams Toolkit** extension window.</span></span>
1. <span data-ttu-id="162e7-130">Seleccione **Editar paquete** de la aplicación para ver la página de detalles de la **aplicación** .</span><span class="sxs-lookup"><span data-stu-id="162e7-130">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="162e7-131">Al editar los campos en la página de detalles de la aplicación, se actualiza el contenido del manifest.jsen el archivo que se entregará como parte del paquete de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="162e7-131">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="162e7-132">Más información</span><span class="sxs-lookup"><span data-stu-id="162e7-132">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="162e7-133">Empaquetar la aplicación</span><span class="sxs-lookup"><span data-stu-id="162e7-133">Package your app</span></span>

<span data-ttu-id="162e7-134">La modificación es la página de detalles de la **aplicación** o la actualización del **manifiesto**, o los archivos **. env** en la carpeta **. Publish** de la aplicación generarán automáticamente el archivo de **Development.zip** .</span><span class="sxs-lookup"><span data-stu-id="162e7-134">Modifying your the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="162e7-135">Deberá incluir [dos iconos](../concepts/build-and-test/apps-package.md#icons) en la misma carpeta.</span><span class="sxs-lookup"><span data-stu-id="162e7-135">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="162e7-136">Instalar y ejecutar la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="162e7-136">Install and run your app locally</span></span>

<span data-ttu-id="162e7-137">En el menú desplegable de *configuraciones de soluciones* , seleccione *implementar*.</span><span class="sxs-lookup"><span data-stu-id="162e7-137">From the *Solutions Configurations* dropdown menu, select *Deploy*.</span></span> <span data-ttu-id="162e7-138">Pulse el botón *ISS Express + Teams* .</span><span class="sxs-lookup"><span data-stu-id="162e7-138">Press the *ISS Express + Teams* button.</span></span> <span data-ttu-id="162e7-139">Se iniciará Microsoft Teams y el cuadro de diálogo de instalación de la aplicación debería aparecer en el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="162e7-139">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="162e7-140">Validar la aplicación</span><span class="sxs-lookup"><span data-stu-id="162e7-140">Validate your app</span></span>

<span data-ttu-id="162e7-141">La página **validar** permite comprobar el paquete de la aplicación antes de enviar la aplicación a AppSource.</span><span class="sxs-lookup"><span data-stu-id="162e7-141">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="162e7-142">Simplemente cargue el paquete del manifiesto y la herramienta de validación comprobará la aplicación en todos los casos de prueba relacionados con el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="162e7-142">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="162e7-143">Para cada prueba con errores, la descripción proporciona un vínculo de documentación para ayudarle a corregir el error.</span><span class="sxs-lookup"><span data-stu-id="162e7-143">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="162e7-144">Para las pruebas que son difíciles de automatizar, los detalles de la **lista de comprobación preliminar** 7 de los casos de prueba con errores más comunes, así como un vínculo a una lista de comprobación de envío completa.</span><span class="sxs-lookup"><span data-stu-id="162e7-144">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="162e7-145">Publicar la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="162e7-145">Publish your app to Teams</span></span>

<span data-ttu-id="162e7-146">En la Página principal de su proyecto, puede cargar su aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizada de la empresa para los usuarios de su organización o bien enviar la aplicación al origen de la aplicación para todos los usuarios de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="162e7-146">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="162e7-147">El administrador de ti consultará estos envíos.</span><span class="sxs-lookup"><span data-stu-id="162e7-147">Your IT admin will review these submissions.</span></span> <span data-ttu-id="162e7-148">Puede volver a la página *publicar* para comprobar el estado del envío y saber si su administrador de ti aprobó o rechazó la aplicación. Aquí también puede ir a enviar actualizaciones a la aplicación o cancelar los envíos actualmente activos.</span><span class="sxs-lookup"><span data-stu-id="162e7-148">You can return to the *Publish* page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="162e7-149">Siguiente paso: mantenimiento y soporte de la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="162e7-149">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
