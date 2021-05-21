---
title: Creación de una página de contenido
author: laujan
description: cómo crear una página de contenido
keywords: Canal de grupo de pestañas de teams configurable estático
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 136160cb9154d62be40d8e29075ac1fc86135a6b
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566680"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="6c699-104">Crear una página de contenido para la pestaña</span><span class="sxs-lookup"><span data-stu-id="6c699-104">Create a content page for your tab</span></span>

<span data-ttu-id="6c699-105">Una página de contenido es una página web que se representa en el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="6c699-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="6c699-106">Por lo general, estos son parte de:</span><span class="sxs-lookup"><span data-stu-id="6c699-106">Typically these are part of:</span></span>

* <span data-ttu-id="6c699-107">Pestaña personalizada de ámbito personal: en este caso, la página de contenido es la primera página que encuentra el usuario.</span><span class="sxs-lookup"><span data-stu-id="6c699-107">A personal-scoped custom tab: In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="6c699-108">Una pestaña personalizada de canal o grupo: después de que el usuario anclar y configure la pestaña en el contexto adecuado, se muestra la página de contenido.</span><span class="sxs-lookup"><span data-stu-id="6c699-108">A channel/group custom tab: After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="6c699-109">Un [módulo de](~/task-modules-and-cards/what-are-task-modules.md)tareas: puede crear una página de contenido e insertarla como vista web dentro de un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="6c699-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md): You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="6c699-110">La página se representará dentro del elemento emergente modal.</span><span class="sxs-lookup"><span data-stu-id="6c699-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="6c699-111">Este artículo es específico para usar páginas de contenido como pestañas; sin embargo, la mayoría de las instrucciones aquí se aplicarían independientemente de cómo se presente la página de contenido al usuario final.</span><span class="sxs-lookup"><span data-stu-id="6c699-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-design-guidelines"></a><span data-ttu-id="6c699-112">Directrices de diseño y contenido de tabulación</span><span class="sxs-lookup"><span data-stu-id="6c699-112">Tab content and design guidelines</span></span>

<span data-ttu-id="6c699-113">El objetivo general de la pestaña debe ser proporcionar acceso a contenido significativo y atractivo que tenga un valor práctico y un propósito evidente.</span><span class="sxs-lookup"><span data-stu-id="6c699-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="6c699-114">Eso no significa que debas renunciar a un estilo agradable, pero debes centrarte en minimizar el desorden haciendo que el diseño de pestaña sea limpio, intuitivo de navegación y que el contenido sea envolvente.</span><span class="sxs-lookup"><span data-stu-id="6c699-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span>

<span data-ttu-id="6c699-115">Para obtener más información, consulte las [directrices de diseño de pestañas](~/tabs/design/tabs.md) [y Microsoft Teams de validación del almacén](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)</span><span class="sxs-lookup"><span data-stu-id="6c699-115">For more information, see the [tab design guidelines](~/tabs/design/tabs.md) and [Microsoft Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="6c699-116">Integre el código con Teams</span><span class="sxs-lookup"><span data-stu-id="6c699-116">Integrate your code with Teams</span></span>

<span data-ttu-id="6c699-117">Para que la página se muestre en Teams, debe incluir el SDK de cliente Microsoft Teams [JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) e incluir una llamada después de `microsoftTeams.initialize()` que se cargue la página.</span><span class="sxs-lookup"><span data-stu-id="6c699-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="6c699-118">Así se comunican su página y Teams cliente:</span><span class="sxs-lookup"><span data-stu-id="6c699-118">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="6c699-119">Acceso a contenido adicional</span><span class="sxs-lookup"><span data-stu-id="6c699-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="6c699-120">Uso del SDK para interactuar con Teams</span><span class="sxs-lookup"><span data-stu-id="6c699-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="6c699-121">El [SDK Teams cliente de JavaScript](~/tabs/how-to/using-teams-client-sdk.md) proporciona muchas funciones adicionales que puede resultar útiles al desarrollar la página de contenido.</span><span class="sxs-lookup"><span data-stu-id="6c699-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="6c699-122">Vínculos profundos</span><span class="sxs-lookup"><span data-stu-id="6c699-122">Deep links</span></span>

<span data-ttu-id="6c699-123">Puede crear vínculos profundos a entidades en Teams.</span><span class="sxs-lookup"><span data-stu-id="6c699-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="6c699-124">Normalmente, se usan para crear vínculos que naveguen al contenido y a la información de la pestaña. Para obtener más información, vea [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span><span class="sxs-lookup"><span data-stu-id="6c699-124">Typically, these are used to create links that navigate to content and information within your tab. For more information, see [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="6c699-125">Módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="6c699-125">Task Modules</span></span>

<span data-ttu-id="6c699-126">Un módulo de tareas es una experiencia emergente modal que se puede desencadenar desde la pestaña. Normalmente, en una página de contenido no desea navegar por el usuario a través de varias páginas.</span><span class="sxs-lookup"><span data-stu-id="6c699-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="6c699-127">En su lugar, usará módulos de tareas para presentar formularios para recopilar información adicional, mostrar los detalles de un elemento en una lista o en cualquier otro momento que necesite presentar al usuario información adicional.</span><span class="sxs-lookup"><span data-stu-id="6c699-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="6c699-128">Los módulos de tareas pueden ser páginas de contenido adicionales o crearse completamente con tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="6c699-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="6c699-129">Consulte [Uso de módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md) para obtener información completa.</span><span class="sxs-lookup"><span data-stu-id="6c699-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="6c699-130">Dominios válidos</span><span class="sxs-lookup"><span data-stu-id="6c699-130">Valid Domains</span></span>

<span data-ttu-id="6c699-131">Asegúrese de que todos los dominios url usados en las pestañas se incluyen en la `validDomains` matriz del [manifiesto](~/concepts/build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="6c699-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="6c699-132">Para obtener más información, [vea validDomains](~/resources/schema/manifest-schema.md#validdomains) en la referencia del esquema de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="6c699-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="6c699-133">Sin embargo, tenga en cuenta que la funcionalidad principal de la pestaña existe en Teams y no fuera de Teams.</span><span class="sxs-lookup"><span data-stu-id="6c699-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="reorder-static-personal-tabs"></a><span data-ttu-id="6c699-134">Reordenar pestañas personales estáticas</span><span class="sxs-lookup"><span data-stu-id="6c699-134">Reorder static personal tabs</span></span>

<span data-ttu-id="6c699-135">A partir de la versión 1.7 del manifiesto, los desarrolladores pueden reorganizar todas las pestañas de su aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="6c699-135">Starting with manifest version 1.7, developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="6c699-136">En concreto, un desarrollador puede mover la pestaña de chat del *bot,* que siempre se sitúa de forma predeterminada en la primera posición, en cualquier lugar del encabezado de pestaña de la aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="6c699-136">In particular, a developer can move the *bot chat* tab, which always defaults to the first position, anywhere in the personal app tab header.</span></span> <span data-ttu-id="6c699-137">Hemos declarado dos palabras clave entityId de pestaña reservadas, *conversaciones* y *acerca de*.</span><span class="sxs-lookup"><span data-stu-id="6c699-137">We’ve declared two reserved tab entityId keywords, *conversations* and *about*.</span></span>

<span data-ttu-id="6c699-138">Si creas un bot con un *ámbito personal,* aparecerá en la primera posición de pestaña de una aplicación personal de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6c699-138">If you create a bot with a *personal* scope, it will show up in the first tab position in a personal app by default.</span></span> <span data-ttu-id="6c699-139">Si desea moverlo a otra posición, debe agregar un objeto tab estático al manifiesto con la palabra clave reservada, *conversaciones*.</span><span class="sxs-lookup"><span data-stu-id="6c699-139">If you wish to move it to another position, you must add a static tab object to your manifest with the reserved keyword, *conversations*.</span></span> <span data-ttu-id="6c699-140">La *pestaña de* conversación aparece en la web o en el escritorio en función de dónde agregue la pestaña *de* conversación en la `staticTabs` matriz.</span><span class="sxs-lookup"><span data-stu-id="6c699-140">The *conversation* tab appears on web or desktop based on where you add the *conversation* tab in the `staticTabs` array.</span></span> 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="6c699-141">Mostrar un indicador de carga nativo</span><span class="sxs-lookup"><span data-stu-id="6c699-141">Show a native loading indicator</span></span>

<span data-ttu-id="6c699-142">A partir [del esquema de manifiesto v1.7,](../../../resources/schema/manifest-schema.md)puede proporcionar un indicador de carga nativo donde se cargue el contenido web en Teams. [](../../../resources/schema/manifest-schema.md#showloadingindicator)</span><span class="sxs-lookup"><span data-stu-id="6c699-142">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams.</span></span> <span data-ttu-id="6c699-143">Por ejemplo, [página de contenido de tabulación,](#integrate-your-code-with-teams)página de [configuración,](configuration-page.md) [página de](removal-page.md)eliminación y [módulos de tareas en pestañas](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="6c699-143">For example, [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md), and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="6c699-144">El comportamiento de los clientes móviles no se puede configurar a través de esta propiedad de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="6c699-144">The behavior on mobile clients is not configurable through this manifest property.</span></span> <span data-ttu-id="6c699-145">Los clientes móviles muestran un indicador de carga nativo de forma predeterminada en las páginas de contenido y los módulos de tareas basados en iframe.</span><span class="sxs-lookup"><span data-stu-id="6c699-145">Mobile clients show a native loading indicator by default across content pages and iframe-based task modules.</span></span> <span data-ttu-id="6c699-146">Este indicador en el móvil se muestra cuando se realiza una solicitud para capturar contenido y se descarta en cuanto se completa la solicitud.</span><span class="sxs-lookup"><span data-stu-id="6c699-146">This indicator on mobile is shown when a request is made to fetch content and gets dismissed as soon as the request gets completed.</span></span>
> * <span data-ttu-id="6c699-147">Si indicas en el manifiesto de la aplicación, todas las páginas de configuración, contenido y eliminación de pestañas y todos los módulos de tareas basados en iframe deben seguir el protocolo obligatorio, a  `"showLoadingIndicator : true`  continuación:</span><span class="sxs-lookup"><span data-stu-id="6c699-147">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>

<span data-ttu-id="6c699-148">**Para mostrar el indicador de carga**</span><span class="sxs-lookup"><span data-stu-id="6c699-148">**To show the loading indicator**</span></span>

* <span data-ttu-id="6c699-149">Agregue `"showLoadingIndicator": true` al manifiesto.</span><span class="sxs-lookup"><span data-stu-id="6c699-149">Add `"showLoadingIndicator": true` to your manifest.</span></span> 
* <span data-ttu-id="6c699-150">Recuerde llamar `microsoftTeams.initialize();` a .</span><span class="sxs-lookup"><span data-stu-id="6c699-150">Remember to call `microsoftTeams.initialize();`.</span></span>
* <span data-ttu-id="6c699-151">**Opcional:** si está listo para imprimir en la pantalla y desea cargar de forma diferida el resto del contenido de la aplicación, puede ocultar manualmente el indicador de carga llamando a `microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="6c699-151">**Optional**: If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
* <span data-ttu-id="6c699-152">**Obligatorio:** por último, llama para `microsoftTeams.appInitialization.notifySuccess()` notificar Teams que la aplicación se ha cargado correctamente.</span><span class="sxs-lookup"><span data-stu-id="6c699-152">**Mandatory**: Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="6c699-153">Teams ocultará el indicador de carga si procede.</span><span class="sxs-lookup"><span data-stu-id="6c699-153">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="6c699-154">Si  `notifySuccess`  no se llama en 30 segundos, se supone que la aplicación ha pasado el tiempo de espera y aparecerá una pantalla de error con una opción de reintento.</span><span class="sxs-lookup"><span data-stu-id="6c699-154">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
* <span data-ttu-id="6c699-155">Si la aplicación no se carga, puede llamar para Teams `microsoftTeams.appInitialization.notifyFailure(reason);` que se produjo un error.</span><span class="sxs-lookup"><span data-stu-id="6c699-155">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="6c699-156">A continuación, se mostrará al usuario una pantalla de error:</span><span class="sxs-lookup"><span data-stu-id="6c699-156">An error screen will then be shown to the user:</span></span>

    ```typescript
    ``
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```
    >
