---
title: Upload la aplicación personalizada
description: Obtén información sobre cómo descargar tu aplicación de forma lateral en Microsoft Teams. La carga lateral es común al probar y depurar una aplicación durante el desarrollo.
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 39e94317ceb615ecd7d5481276ffafed5afe5cde
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565196"
---
# <a name="upload-your-app-in-microsoft-teams"></a><span data-ttu-id="939f6-104">Upload la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="939f6-104">Upload your app in Microsoft Teams</span></span>

<span data-ttu-id="939f6-105">Puede descargar Microsoft Teams aplicaciones sin tener que publicar en su organización o en la tienda de Teams.</span><span class="sxs-lookup"><span data-stu-id="939f6-105">You can sideload Microsoft Teams apps without having to publish to your organization or the Teams store.</span></span> <span data-ttu-id="939f6-106">Esto tiene sentido en los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="939f6-106">This makes sense in the following scenarios:</span></span>

* <span data-ttu-id="939f6-107">Desea probar y depurar una aplicación localmente usted mismo o con otros desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="939f6-107">You want to test and debug an app locally yourself or with other developers.</span></span>
* <span data-ttu-id="939f6-108">Usted construyó una aplicación sólo para usted.</span><span class="sxs-lookup"><span data-stu-id="939f6-108">You built an app just for yourself.</span></span> <span data-ttu-id="939f6-109">Por ejemplo, para automatizar un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="939f6-109">For example, to automate a workflow.</span></span>
* <span data-ttu-id="939f6-110">Ha creado una aplicación para un pequeño conjunto de usuarios, como el grupo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="939f6-110">You built an app for a small set of users, such as, your work group.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="939f6-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="939f6-111">Prerequisites</span></span>

* <span data-ttu-id="939f6-112">Cree el [paquete de la aplicación](~/concepts/build-and-test/apps-package.md) y valide para [errores.](https://dev.teams.microsoft.com/appvalidation.html)</span><span class="sxs-lookup"><span data-stu-id="939f6-112">Create your [app package](~/concepts/build-and-test/apps-package.md) and [validate it](https://dev.teams.microsoft.com/appvalidation.html) for errors.</span></span>
* <span data-ttu-id="939f6-113">[Habilite la carga de aplicaciones personalizadas](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) en Teams.</span><span class="sxs-lookup"><span data-stu-id="939f6-113">[Enable custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) in Teams.</span></span>
* <span data-ttu-id="939f6-114">Asegúrese de que la aplicación se está ejecutando y accesible a través de HTTPs.</span><span class="sxs-lookup"><span data-stu-id="939f6-114">Make sure that your app is running and accessible via HTTPs.</span></span>

## <a name="upload-your-app"></a><span data-ttu-id="939f6-115">Cargar la aplicación</span><span class="sxs-lookup"><span data-stu-id="939f6-115">Upload your app</span></span>

<span data-ttu-id="939f6-116">Puedes descargar tu aplicación en un equipo, chatear, reunión o para uso personal en función de cómo hayas configurado el ámbito de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="939f6-116">You can sideload your app to a team, chat, meeting, or for personal use depending on how you configured your app's scope.</span></span>

1. <span data-ttu-id="939f6-117">Inicie sesión en el cliente Teams con su [cuenta de desarrollo de Microsoft 365.](~/build-your-first-app/build-and-run.md#prerequisites)</span><span class="sxs-lookup"><span data-stu-id="939f6-117">Log in to the Teams client with your [Microsoft 365 development account](~/build-your-first-app/build-and-run.md#prerequisites).</span></span>
1. <span data-ttu-id="939f6-118">Seleccione **Aplicaciones** y elija **Upload una aplicación personalizada.**</span><span class="sxs-lookup"><span data-stu-id="939f6-118">Select **Apps** and choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="939f6-119">Seleccione el paquete de la aplicación .zip archivo.</span><span class="sxs-lookup"><span data-stu-id="939f6-119">Select your app package .zip file.</span></span> <span data-ttu-id="939f6-120">Aparece un cuadro de diálogo de instalación.</span><span class="sxs-lookup"><span data-stu-id="939f6-120">An install dialog displays.</span></span>
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Captura de pantalla que muestra un ejemplo de un cuadro de diálogo de instalación de Teams aplicación.":::
1. <span data-ttu-id="939f6-122">Agrega tu aplicación a Teams.</span><span class="sxs-lookup"><span data-stu-id="939f6-122">Add your app to Teams.</span></span>

## <a name="troubleshoot-upload-issues"></a><span data-ttu-id="939f6-123">Solucionar problemas de carga</span><span class="sxs-lookup"><span data-stu-id="939f6-123">Troubleshoot upload issues</span></span>

<span data-ttu-id="939f6-124">Si la aplicación no se puede descargar de lado, haga lo siguiente hasta que se resuelva el problema:</span><span class="sxs-lookup"><span data-stu-id="939f6-124">If your app fails to sideload, do the following until the issue resolves:</span></span>

1. <span data-ttu-id="939f6-125">Vuelve a consultar las instrucciones para [crear el paquete de la aplicación.](../../concepts/build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="939f6-125">Go back through the instructions for [creating your app package](../../concepts/build-and-test/apps-package.md).</span></span>
1. <span data-ttu-id="939f6-126">[Valide el paquete de la aplicación](https://dev.teams.microsoft.com/appvalidation.html) de nuevo.</span><span class="sxs-lookup"><span data-stu-id="939f6-126">[Validate your app package](https://dev.teams.microsoft.com/appvalidation.html) again.</span></span>
1. <span data-ttu-id="939f6-127">Asegúrese de que el manifiesto de la aplicación coincida con el [esquema](../../resources/schema/manifest-schema.md)más reciente.</span><span class="sxs-lookup"><span data-stu-id="939f6-127">Make sure your app manifest matches the latest [schema](../../resources/schema/manifest-schema.md).</span></span>

## <a name="access-your-app"></a><span data-ttu-id="939f6-128">Accede a tu aplicación</span><span class="sxs-lookup"><span data-stu-id="939f6-128">Access your app</span></span>

<span data-ttu-id="939f6-129">Teams proporciona varias maneras de abrir aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="939f6-129">Teams provides several ways to open apps.</span></span> <span data-ttu-id="939f6-130">Para obtener más información, consulta [acceder a tus aplicaciones en Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span><span class="sxs-lookup"><span data-stu-id="939f6-130">For more information, see [access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span></span>

## <a name="update-your-app"></a><span data-ttu-id="939f6-131">Actualiza tu aplicación</span><span class="sxs-lookup"><span data-stu-id="939f6-131">Update your app</span></span>

<span data-ttu-id="939f6-132">No es que volver a cargar la aplicación si realiza cambios de código (estos se reflejan en Teams en tiempo real).</span><span class="sxs-lookup"><span data-stu-id="939f6-132">You don't have to sideload your app again if you make code changes (these are reflected in Teams in real-time).</span></span> <span data-ttu-id="939f6-133">Sin embargo, debe reinstalar si cambia las configuraciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="939f6-133">However, you must reinstall if you change any app configurations.</span></span>

## <a name="remove-your-app"></a><span data-ttu-id="939f6-134">Elimina tu aplicación</span><span class="sxs-lookup"><span data-stu-id="939f6-134">Remove your app</span></span>

<span data-ttu-id="939f6-135">Para quitar la aplicación, haga clic con el botón derecho en el icono de la aplicación en Teams y seleccione **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="939f6-135">To remove your app, right click the app icon in Teams and select **Uninstall**.</span></span>

> [!NOTE]
> <span data-ttu-id="939f6-136">No puede eliminar por completo la actividad personal del bot.</span><span class="sxs-lookup"><span data-stu-id="939f6-136">You can't remove personal bot activity entirely.</span></span> <span data-ttu-id="939f6-137">Si quitas la aplicación y la vuelves a agregar, la nueva comunicación con el bot se anexa a la conversación anterior con ella.</span><span class="sxs-lookup"><span data-stu-id="939f6-137">If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.</span></span>

## <a name="next-step"></a><span data-ttu-id="939f6-138">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="939f6-138">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="939f6-139">Usa tu aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="939f6-139">Use your Teams app</span></span>](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
