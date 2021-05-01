---
title: Upload aplicación personalizada
description: Aprende a descargar localmente la aplicación en Microsoft Teams. La instalación local es común al probar y depurar una aplicación durante el desarrollo.
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: a82f7d6498db4cceb69f1b7f5ff53b1646371ce8
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101572"
---
# <a name="upload-your-app-in-microsoft-teams"></a><span data-ttu-id="74a7a-104">Upload la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="74a7a-104">Upload your app in Microsoft Teams</span></span>

<span data-ttu-id="74a7a-105">Puedes descargar localmente Microsoft Teams aplicaciones sin tener que publicar en tu organización o en la Teams local.</span><span class="sxs-lookup"><span data-stu-id="74a7a-105">You can sideload Microsoft Teams apps without having to publish to your organization or the Teams store.</span></span> <span data-ttu-id="74a7a-106">Esto tiene sentido en los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="74a7a-106">This makes sense in the following scenarios:</span></span>

* <span data-ttu-id="74a7a-107">Quieres probar y depurar una aplicación localmente tú mismo o con otros desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="74a7a-107">You want to test and debug an app locally yourself or with other developers.</span></span>
* <span data-ttu-id="74a7a-108">Has creado una aplicación solo para ti (por ejemplo, para automatizar un flujo de trabajo).</span><span class="sxs-lookup"><span data-stu-id="74a7a-108">You built an app just for yourself (for example, to automate a workflow).</span></span>
* <span data-ttu-id="74a7a-109">Has creado una aplicación para un pequeño conjunto de usuarios (como el grupo de trabajo).</span><span class="sxs-lookup"><span data-stu-id="74a7a-109">You built an app for a small set of users (such as your work group).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74a7a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="74a7a-110">Prerequisites</span></span>

* <span data-ttu-id="74a7a-111">Crea el [paquete de la aplicación](~/concepts/build-and-test/apps-package.md) y [valida los](https://dev.teams.microsoft.com/appvalidation.html) errores.</span><span class="sxs-lookup"><span data-stu-id="74a7a-111">Create your [app package](~/concepts/build-and-test/apps-package.md) and [validate it](https://dev.teams.microsoft.com/appvalidation.html) for errors.</span></span>
* <span data-ttu-id="74a7a-112">[Habilitar la carga de aplicaciones personalizadas](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) en Teams.</span><span class="sxs-lookup"><span data-stu-id="74a7a-112">[Enable custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) in Teams.</span></span>
* <span data-ttu-id="74a7a-113">Asegúrate de que la aplicación se ejecuta y se puede acceder a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="74a7a-113">Make sure that your app is running and accessible via HTTPs.</span></span>

## <a name="upload-your-app"></a><span data-ttu-id="74a7a-114">Upload aplicación</span><span class="sxs-lookup"><span data-stu-id="74a7a-114">Upload your app</span></span>

<span data-ttu-id="74a7a-115">Puedes descargar localmente la aplicación en un equipo, chat, reunión o para uso personal en función de cómo configuraste el ámbito de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="74a7a-115">You can sideload your app to a team, chat, meeting, or for personal use depending on how you configured your app's scope.</span></span>

1. <span data-ttu-id="74a7a-116">Inicie sesión en el Teams con su [Microsoft 365 de desarrollo](~/build-your-first-app/build-and-run.md#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="74a7a-116">Log in to the Teams client with your [Microsoft 365 development account](~/build-your-first-app/build-and-run.md#prerequisites).</span></span>
1. <span data-ttu-id="74a7a-117">Selecciona **Aplicaciones** y elige **Upload una aplicación personalizada.**</span><span class="sxs-lookup"><span data-stu-id="74a7a-117">Select **Apps** and choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="74a7a-118">Selecciona el paquete de la aplicación .zip archivo.</span><span class="sxs-lookup"><span data-stu-id="74a7a-118">Select your app package .zip file.</span></span> <span data-ttu-id="74a7a-119">Se muestra un cuadro de diálogo de instalación.</span><span class="sxs-lookup"><span data-stu-id="74a7a-119">An install dialog displays.</span></span>
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Captura de pantalla que muestra un ejemplo de un Teams de instalación de la aplicación.":::
1. <span data-ttu-id="74a7a-121">Agrega la aplicación a Teams.</span><span class="sxs-lookup"><span data-stu-id="74a7a-121">Add your app to Teams.</span></span>

## <a name="troubleshoot-upload-issues"></a><span data-ttu-id="74a7a-122">Solucionar problemas de carga</span><span class="sxs-lookup"><span data-stu-id="74a7a-122">Troubleshoot upload issues</span></span>

<span data-ttu-id="74a7a-123">Si la aplicación no puede realizar la instalación local, haga lo siguiente hasta que se resuelva el problema:</span><span class="sxs-lookup"><span data-stu-id="74a7a-123">If your app fails to sideload, do the following until the issue resolves:</span></span>

1. <span data-ttu-id="74a7a-124">Vuelva a las instrucciones para [crear el paquete de la aplicación](../../concepts/build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="74a7a-124">Go back through the instructions for [creating your app package](../../concepts/build-and-test/apps-package.md).</span></span>
1. <span data-ttu-id="74a7a-125">[Valide de nuevo el paquete de](https://dev.teams.microsoft.com/appvalidation.html) la aplicación.</span><span class="sxs-lookup"><span data-stu-id="74a7a-125">[Validate your app package](https://dev.teams.microsoft.com/appvalidation.html) again.</span></span>
1. <span data-ttu-id="74a7a-126">Asegúrate de que el manifiesto de la aplicación coincida con el esquema [más reciente.](../../resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="74a7a-126">Make sure your app manifest matches the latest [schema](../../resources/schema/manifest-schema.md).</span></span>

## <a name="access-your-app"></a><span data-ttu-id="74a7a-127">Acceder a la aplicación</span><span class="sxs-lookup"><span data-stu-id="74a7a-127">Access your app</span></span>

<span data-ttu-id="74a7a-128">Teams varias formas de abrir aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="74a7a-128">Teams provides several ways to open apps.</span></span> <span data-ttu-id="74a7a-129">Para obtener más información, [vea access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span><span class="sxs-lookup"><span data-stu-id="74a7a-129">For more information, see [access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span></span>

## <a name="update-your-app"></a><span data-ttu-id="74a7a-130">Actualizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="74a7a-130">Update your app</span></span>

<span data-ttu-id="74a7a-131">No tienes que volver a cargar localmente la aplicación si realizas cambios de código (estos se reflejan en Teams en tiempo real).</span><span class="sxs-lookup"><span data-stu-id="74a7a-131">You don't have to sideload your app again if you make code changes (these are reflected in Teams in real-time).</span></span> <span data-ttu-id="74a7a-132">Sin embargo, debes reinstalar si cambias las configuraciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="74a7a-132">However, you must reinstall if you change any app configurations.</span></span>

## <a name="remove-your-app"></a><span data-ttu-id="74a7a-133">Quitar la aplicación</span><span class="sxs-lookup"><span data-stu-id="74a7a-133">Remove your app</span></span>

<span data-ttu-id="74a7a-134">Para quitar la aplicación, haz clic con el botón secundario en el icono de la Teams y selecciona **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="74a7a-134">To remove your app, right click the app icon in Teams and select **Uninstall**.</span></span>

> [!NOTE]
> <span data-ttu-id="74a7a-135">No puedes quitar completamente la actividad del bot personal.</span><span class="sxs-lookup"><span data-stu-id="74a7a-135">You can't remove personal bot activity entirely.</span></span> <span data-ttu-id="74a7a-136">Si quitas la aplicación y la vuelves a agregar, la nueva comunicación con el bot se anexa a la conversación anterior con ella.</span><span class="sxs-lookup"><span data-stu-id="74a7a-136">If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.</span></span>

## <a name="next-step"></a><span data-ttu-id="74a7a-137">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="74a7a-137">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="74a7a-138">Usar la Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="74a7a-138">Use your Teams app</span></span>](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
