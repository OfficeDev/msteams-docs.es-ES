---
title: Creación de una página de contenido
author: surbhigupta
description: cómo crear una página de contenido
keywords: Canal de grupo de pestañas de teams configurable estático
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1276fdac2d3a30836b574b8e51b99fcbd7a415d2
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179737"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="6bba1-104">Crear una página de contenido para la pestaña</span><span class="sxs-lookup"><span data-stu-id="6bba1-104">Create a content page for your tab</span></span>

<span data-ttu-id="6bba1-105">Una página de contenido es una página web que se representa en el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="6bba1-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="6bba1-106">Estos son parte de:</span><span class="sxs-lookup"><span data-stu-id="6bba1-106">These are part of:</span></span>

* <span data-ttu-id="6bba1-107">Pestaña personalizada de ámbito personal: en este caso, la página de contenido es la primera página que encuentra el usuario.</span><span class="sxs-lookup"><span data-stu-id="6bba1-107">A personal-scoped custom tab: In this case, the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="6bba1-108">Pestaña personalizada de canal o grupo: la página de contenido se muestra después de que el usuario anclar y configure la pestaña en el contexto adecuado.</span><span class="sxs-lookup"><span data-stu-id="6bba1-108">A channel or group custom tab: The content page is displayed after the user pins and configures the tab in the appropriate context.</span></span>
* <span data-ttu-id="6bba1-109">Un [módulo de](~/task-modules-and-cards/what-are-task-modules.md)tareas: puede crear una página de contenido e insertarla como vista web dentro de un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="6bba1-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md): You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="6bba1-110">La página se representa dentro de la ventana emergente modal.</span><span class="sxs-lookup"><span data-stu-id="6bba1-110">The page is rendered inside the modal pop-up.</span></span>

<span data-ttu-id="6bba1-111">Este artículo es específico para usar páginas de contenido como pestañas; sin embargo, la mayoría de las instrucciones aquí se aplican independientemente de cómo se presente la página de contenido al usuario.</span><span class="sxs-lookup"><span data-stu-id="6bba1-111">This article is specific to using content pages as tabs; however the majority of the guidance here applies regardless of how the content page is presented to the user.</span></span>

## <a name="tab-content-and-design-guidelines"></a><span data-ttu-id="6bba1-112">Directrices de diseño y contenido de tabulación</span><span class="sxs-lookup"><span data-stu-id="6bba1-112">Tab content and design guidelines</span></span>

<span data-ttu-id="6bba1-113">El objetivo general de la pestaña es proporcionar acceso al contenido significativo y atractivo que tiene un valor práctico y un propósito evidente.</span><span class="sxs-lookup"><span data-stu-id="6bba1-113">Your tab's overall objective is to provide access to meaningful and engaging content that has practical value and an evident purpose.</span></span> <span data-ttu-id="6bba1-114">Debes centrarte en hacer que el diseño de la pestaña sea limpio, la navegación intuitiva y el contenido envolvente.</span><span class="sxs-lookup"><span data-stu-id="6bba1-114">You must focus on making your tab design clean, navigation intuitive, and content immersive.</span></span>

<span data-ttu-id="6bba1-115">Para obtener más información, vea [directrices de diseño de](~/tabs/design/tabs.md) [pestañas y Microsoft Teams directrices de validación del almacén.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)</span><span class="sxs-lookup"><span data-stu-id="6bba1-115">For more information, see [tab design guidelines](~/tabs/design/tabs.md) and [Microsoft Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="6bba1-116">Integre el código con Teams</span><span class="sxs-lookup"><span data-stu-id="6bba1-116">Integrate your code with Teams</span></span>

<span data-ttu-id="6bba1-117">Para que la página se muestre en Teams, debe incluir el SDK de cliente Microsoft Teams [JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) e incluir una llamada después de `microsoftTeams.initialize()` que se cargue la página.</span><span class="sxs-lookup"><span data-stu-id="6bba1-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> 

<span data-ttu-id="6bba1-118">El siguiente código proporciona un ejemplo de cómo se comunican la página y Teams cliente:</span><span class="sxs-lookup"><span data-stu-id="6bba1-118">The following code provides an example of how your page and the Teams client communicate:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    microsoftTeams.initialize();
    </script>
...
</body>
```

## <a name="access-additional-content"></a><span data-ttu-id="6bba1-119">Acceso a contenido adicional</span><span class="sxs-lookup"><span data-stu-id="6bba1-119">Access additional content</span></span>

<span data-ttu-id="6bba1-120">Puede obtener acceso a contenido adicional mediante el SDK para interactuar con Teams, crear vínculos profundos, usar módulos de tareas y comprobar si los dominios de dirección URL se incluyen en la `validDomains` matriz.</span><span class="sxs-lookup"><span data-stu-id="6bba1-120">You can access additional content by using the SDK to interact with Teams, creating deep links, using task modules, and verifying if URL domains are included in the `validDomains` array.</span></span>

### <a name="use-the-sdk-to-interact-with-teams"></a><span data-ttu-id="6bba1-121">Use el SDK para interactuar con Teams</span><span class="sxs-lookup"><span data-stu-id="6bba1-121">Use the SDK to interact with Teams</span></span>

<span data-ttu-id="6bba1-122">El [SDK Teams cliente de JavaScript](~/tabs/how-to/using-teams-client-sdk.md) proporciona muchas funciones adicionales que puede encontrar útiles al desarrollar la página de contenido.</span><span class="sxs-lookup"><span data-stu-id="6bba1-122">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions that you can find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="6bba1-123">Vínculos profundos</span><span class="sxs-lookup"><span data-stu-id="6bba1-123">Deep links</span></span>

<span data-ttu-id="6bba1-124">Puede crear vínculos profundos a entidades en Teams.</span><span class="sxs-lookup"><span data-stu-id="6bba1-124">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="6bba1-125">Se usan para crear vínculos que naveguen al contenido y a la información de la pestaña. Para obtener más información, vea [crear vínculos profundos al contenido y las características en Teams](~/concepts/build-and-test/deep-links.md).</span><span class="sxs-lookup"><span data-stu-id="6bba1-125">These are used to create links that navigate to content and information within your tab. For more information, see [create deep links to content and features in Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="6bba1-126">Módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="6bba1-126">Task modules</span></span>

<span data-ttu-id="6bba1-127">Un módulo de tareas es una experiencia emergente modal que puede desencadenar desde la pestaña. En una página de contenido, puede usar módulos de tareas para presentar formularios para recopilar información adicional, mostrar los detalles de un elemento en una lista o presentar al usuario información adicional.</span><span class="sxs-lookup"><span data-stu-id="6bba1-127">A task module is a modal pop-up experience that you can trigger from your tab. In a content page, you can use task modules to present forms for gathering additional information, displaying the details of an item in a list, or presenting the user with additional information.</span></span> <span data-ttu-id="6bba1-128">Los módulos de tareas pueden ser páginas de contenido adicionales o crearse completamente con tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="6bba1-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="6bba1-129">Para obtener más información, vea [using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="6bba1-129">For more information, see [using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

### <a name="valid-domains"></a><span data-ttu-id="6bba1-130">Dominios válidos</span><span class="sxs-lookup"><span data-stu-id="6bba1-130">Valid domains</span></span>

<span data-ttu-id="6bba1-131">Asegúrese de que todos los dominios url usados en las pestañas se incluyan en la `validDomains` matriz del [manifiesto](~/concepts/build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="6bba1-131">Ensure that all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="6bba1-132">Para obtener más información, [vea validDomains](~/resources/schema/manifest-schema.md#validdomains) en la referencia del esquema de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="6bba1-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span>

> [!NOTE]
> <span data-ttu-id="6bba1-133">La funcionalidad principal de la pestaña existe en Teams y no fuera de Teams.</span><span class="sxs-lookup"><span data-stu-id="6bba1-133">The core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="6bba1-134">Mostrar un indicador de carga nativo</span><span class="sxs-lookup"><span data-stu-id="6bba1-134">Show a native loading indicator</span></span>

<span data-ttu-id="6bba1-135">A partir [del esquema de manifiesto v1.7,](../../../resources/schema/manifest-schema.md)puede proporcionar un indicador de carga [nativo](../../../resources/schema/manifest-schema.md#showloadingindicator).</span><span class="sxs-lookup"><span data-stu-id="6bba1-135">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator).</span></span> <span data-ttu-id="6bba1-136">Por ejemplo, [página de contenido de tabulación,](#integrate-your-code-with-teams)página de [configuración,](configuration-page.md) [página de](removal-page.md)eliminación y [módulos de tareas en pestañas](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="6bba1-136">For example, [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md), and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="6bba1-137">El comportamiento de los clientes móviles no se puede configurar a través de la propiedad del indicador de carga nativo.</span><span class="sxs-lookup"><span data-stu-id="6bba1-137">The behavior on mobile clients is not configurable through the native loading indicator property.</span></span> <span data-ttu-id="6bba1-138">Los clientes móviles muestran este indicador de forma predeterminada en las páginas de contenido y los módulos de tareas basados en iframe.</span><span class="sxs-lookup"><span data-stu-id="6bba1-138">Mobile clients show this indicator by default across content pages and iframe-based task modules.</span></span> <span data-ttu-id="6bba1-139">Este indicador en el móvil se muestra cuando se realiza una solicitud para capturar contenido y se descarta en cuanto se completa la solicitud.</span><span class="sxs-lookup"><span data-stu-id="6bba1-139">This indicator on mobile is shown when a request is made to fetch content and gets dismissed as soon as the request gets completed.</span></span>

<span data-ttu-id="6bba1-140">Si indicas en el manifiesto de la aplicación, todas las páginas de configuración, contenido y eliminación de pestañas y todos los módulos de tareas basados en iframe deben `showLoadingIndicator : true`  seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6bba1-140">If you indicate `showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow these steps:</span></span>

<span data-ttu-id="6bba1-141">**Para mostrar el indicador de carga**</span><span class="sxs-lookup"><span data-stu-id="6bba1-141">**To show the loading indicator**</span></span>

1. <span data-ttu-id="6bba1-142">Agregue `"showLoadingIndicator": true` al manifiesto.</span><span class="sxs-lookup"><span data-stu-id="6bba1-142">Add `"showLoadingIndicator": true` to your manifest.</span></span>
1. <span data-ttu-id="6bba1-143">Llamar a `microsoftTeams.initialize();`.</span><span class="sxs-lookup"><span data-stu-id="6bba1-143">Call `microsoftTeams.initialize();`.</span></span>
1. <span data-ttu-id="6bba1-144">Como paso **obligatorio,** llama para `microsoftTeams.appInitialization.notifySuccess()` notificar a Teams que la aplicación se ha cargado correctamente.</span><span class="sxs-lookup"><span data-stu-id="6bba1-144">As a **mandatory** step, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="6bba1-145">Teams oculta el indicador de carga, si procede.</span><span class="sxs-lookup"><span data-stu-id="6bba1-145">Teams then hides the loading indicator, if applicable.</span></span> <span data-ttu-id="6bba1-146">Si `notifySuccess`  no se llama en 30 segundos, se supone que la aplicación ha pasado el tiempo de espera y aparece una pantalla de error con una opción de reintento.</span><span class="sxs-lookup"><span data-stu-id="6bba1-146">If `notifySuccess`  is not called within 30 seconds, it is assumed that your app timed out and an error screen with a retry option appears.</span></span>
1. <span data-ttu-id="6bba1-147">**Opcionalmente,** si está listo para imprimir en la pantalla y desea cargar de forma diferida el resto del contenido de la aplicación, puede ocultar manualmente el indicador de carga llamando a `microsoftTeams.appInitialization.notifyAppLoaded();` .</span><span class="sxs-lookup"><span data-stu-id="6bba1-147">**Optionally**, if you are ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`.</span></span>
1. <span data-ttu-id="6bba1-148">Si la aplicación no se carga, puede llamar para Teams `microsoftTeams.appInitialization.notifyFailure(reason);` que se produjo un error.</span><span class="sxs-lookup"><span data-stu-id="6bba1-148">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="6bba1-149">Se muestra una pantalla de error al usuario.</span><span class="sxs-lookup"><span data-stu-id="6bba1-149">An error screen is shown to the user.</span></span> <span data-ttu-id="6bba1-150">El código siguiente proporciona un ejemplo de motivos de error de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="6bba1-150">The following code provides an example of application failure reasons:</span></span>

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="see-also"></a><span data-ttu-id="6bba1-151">Vea también</span><span class="sxs-lookup"><span data-stu-id="6bba1-151">See also</span></span>

* [<span data-ttu-id="6bba1-152">Teams pestañas</span><span class="sxs-lookup"><span data-stu-id="6bba1-152">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="6bba1-153">Crear una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="6bba1-153">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="6bba1-154">Crear una pestaña de canal o grupo</span><span class="sxs-lookup"><span data-stu-id="6bba1-154">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="6bba1-155">Creación de una página de contenido</span><span class="sxs-lookup"><span data-stu-id="6bba1-155">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="next-step"></a><span data-ttu-id="6bba1-156">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="6bba1-156">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6bba1-157">Creación de una página de configuración</span><span class="sxs-lookup"><span data-stu-id="6bba1-157">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
