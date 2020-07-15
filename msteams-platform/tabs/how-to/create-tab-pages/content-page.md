---
title: Creación de una página de contenido
author: laujan
description: ''
keywords: canal de grupo de pestañas de Teams configurable estático
ms.topic: conceptual
ms.author: v-laujan
ms.openlocfilehash: a9f1fa407c6377daa8bce6a6a6c63b47d50d8100
ms.sourcegitcommit: d0ca6a4856ffd03d197d47338e633126723fa78a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2020
ms.locfileid: "45137639"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="f2c72-103">Crear una página de contenido para la pestaña</span><span class="sxs-lookup"><span data-stu-id="f2c72-103">Create a content page for your tab</span></span>

<span data-ttu-id="f2c72-104">Una página de contenido es una página web que se representa dentro del cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="f2c72-104">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="f2c72-105">Normalmente son parte de:</span><span class="sxs-lookup"><span data-stu-id="f2c72-105">Typically these are part of:</span></span>

* <span data-ttu-id="f2c72-106">Una ficha personalizada con ámbito personal en esta instancia la página de contenido es la primera página que encuentra el usuario.</span><span class="sxs-lookup"><span data-stu-id="f2c72-106">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="f2c72-107">Una pestaña personalizada de canal o Grupo: después de que el usuario PIN y configure la pestaña en el contexto adecuado, se muestra la página de contenido.</span><span class="sxs-lookup"><span data-stu-id="f2c72-107">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="f2c72-108">Un [módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md) : puede crear una página de contenido e incrustarla como WebView dentro de un módulo de tareas.</span><span class="sxs-lookup"><span data-stu-id="f2c72-108">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="f2c72-109">La página se representará dentro del elemento emergente modal.</span><span class="sxs-lookup"><span data-stu-id="f2c72-109">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="f2c72-110">Este artículo es específico para usar páginas de contenido como fichas; sin embargo, la mayoría de las instrucciones aquí aplicadas se aplican independientemente de cómo se presente la página de contenido al usuario final.</span><span class="sxs-lookup"><span data-stu-id="f2c72-110">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="f2c72-111">Contenido de la pestaña y directrices de estilo</span><span class="sxs-lookup"><span data-stu-id="f2c72-111">Tab content and style guidelines</span></span>

<span data-ttu-id="f2c72-112">El objetivo general de su pestaña debe ser proporcionar acceso a contenido significativo y atractivo que tenga un valor práctico y un propósito claro.</span><span class="sxs-lookup"><span data-stu-id="f2c72-112">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="f2c72-113">Esto no significa que deba prepararse con un estilo agradable, pero debe centrarse en minimizar la confusión haciendo que el diseño de pestaña sea limpio, navegación intuitiva y contenido envolvente.</span><span class="sxs-lookup"><span data-stu-id="f2c72-113">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="f2c72-114">Ver [contenido y conversaciones, todos a la vez mediante pestañas](~/tabs/design/tabs.md) y [Guía del proceso de aprobación de aplicaciones de Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span><span class="sxs-lookup"><span data-stu-id="f2c72-114">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="f2c72-115">Integrar el código con Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f2c72-115">Integrate your code with Teams</span></span>

<span data-ttu-id="f2c72-116">Para que la página se muestre en Microsoft Teams, debe incluir el [SDK del cliente de JavaScript para Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) e incluir una llamada a `microsoftTeams.initialize()` después de que se cargue la página.</span><span class="sxs-lookup"><span data-stu-id="f2c72-116">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="f2c72-117">Así es como se comunican la página y el cliente de Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="f2c72-117">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="f2c72-118">Obtener acceso a contenido adicional</span><span class="sxs-lookup"><span data-stu-id="f2c72-118">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="f2c72-119">Uso del SDK para interactuar con Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f2c72-119">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="f2c72-120">El [SDK de JavaScript del cliente de Microsoft Teams](~/tabs/how-to/using-teams-client-sdk.md) proporciona muchas funciones adicionales que puede que le resulten útiles mientras se programa la página de contenido.</span><span class="sxs-lookup"><span data-stu-id="f2c72-120">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developer your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="f2c72-121">Vínculos profundos</span><span class="sxs-lookup"><span data-stu-id="f2c72-121">Deep links</span></span>

<span data-ttu-id="f2c72-122">Puede crear vínculos profundos a entidades en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f2c72-122">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="f2c72-123">Normalmente, estos se usan para crear vínculos que naveguen a contenido e información dentro de la pestaña. Consulte [crear vínculos detallados para el contenido y las características de Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span><span class="sxs-lookup"><span data-stu-id="f2c72-123">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="f2c72-124">Módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="f2c72-124">Task Modules</span></span>

<span data-ttu-id="f2c72-125">Un módulo de tareas es una experiencia modal de tipo popup que puede desencadenar desde su pestaña. normalmente, en una página de contenido no desea explorar al usuario a través de varias páginas.</span><span class="sxs-lookup"><span data-stu-id="f2c72-125">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="f2c72-126">En su lugar, usará módulos de tareas para presentar formularios para recopilar información adicional, mostrar los detalles de un elemento en una lista o cualquier otro momento en que necesite presentar al usuario información adicional.</span><span class="sxs-lookup"><span data-stu-id="f2c72-126">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="f2c72-127">Los propios módulos de tareas pueden ser páginas de contenido adicionales o crearse completamente mediante tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="f2c72-127">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="f2c72-128">Consulte [uso de módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md) para obtener información completa.</span><span class="sxs-lookup"><span data-stu-id="f2c72-128">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="f2c72-129">Dominios válidos</span><span class="sxs-lookup"><span data-stu-id="f2c72-129">Valid Domains</span></span>

<span data-ttu-id="f2c72-130">Asegúrese de que todos los dominios de dirección URL usados en las pestañas se incluyen en la `validDomains` matriz del [manifiesto](~/concepts/build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="f2c72-130">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="f2c72-131">Para obtener más información, vea [validDomains](~/resources/schema/manifest-schema.md#validdomains) en la referencia del esquema del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="f2c72-131">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="f2c72-132">Sin embargo, tenga en cuenta que la funcionalidad principal de su pestaña existe en Microsoft Teams y no fuera de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f2c72-132">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="showing-a-native-loading-indicator"></a><span data-ttu-id="f2c72-133">Mostrar un indicador de carga nativo</span><span class="sxs-lookup"><span data-stu-id="f2c72-133">Showing a native loading indicator</span></span>

<span data-ttu-id="f2c72-134">Comenzando con [el esquema de manifiesto v 1.7](../../../resources/schema/manifest-schema.md), puede proporcionar un [indicador de carga nativo](../../../resources/schema/manifest-schema.md#showloadingindicator) siempre que el contenido web se cargue en Microsoft Teams, por ejemplo, [Página de contenido](#integrate-your-code-with-teams)de la ficha, página de [configuración](configuration-page.md), [Página de eliminación](removal-page.md) y [módulos de tareas en las pestañas](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="f2c72-134">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams, e.g., [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md) and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f2c72-135">Si indica `"showLoadingIndicator : true` en el manifiesto de la aplicación, todas las páginas de configuración, contenido y eliminación de la ficha y todos los módulos de tareas basados en iframe deben seguir el protocolo obligatorio, a continuación:</span><span class="sxs-lookup"><span data-stu-id="f2c72-135">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>

1. <span data-ttu-id="f2c72-136">Para mostrar el indicador de carga, agregue `"showLoadingIndicator": true` al manifiesto.</span><span class="sxs-lookup"><span data-stu-id="f2c72-136">To show the loading indicator, add `"showLoadingIndicator": true` to your manifest.</span></span> 
2. <span data-ttu-id="f2c72-137">Recuerde que debe llamar a `microsoftTeams.initialize();` .</span><span class="sxs-lookup"><span data-stu-id="f2c72-137">Remember to call `microsoftTeams.initialize();`.</span></span>
3. <span data-ttu-id="f2c72-138">**Opcional**.</span><span class="sxs-lookup"><span data-stu-id="f2c72-138">**Optional**.</span></span> <span data-ttu-id="f2c72-139">Si está listo para imprimir en la pantalla y desea cargar perezosos el resto del contenido de la aplicación, puede ocultar manualmente el indicador de carga mediante una llamada a`microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="f2c72-139">If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
4. <span data-ttu-id="f2c72-140">**Obligatorio**.</span><span class="sxs-lookup"><span data-stu-id="f2c72-140">**Mandatory**.</span></span> <span data-ttu-id="f2c72-141">Por último, llame `microsoftTeams.appInitialization.notifySuccess()` a para notificar a los equipos que la aplicación se ha cargado correctamente.</span><span class="sxs-lookup"><span data-stu-id="f2c72-141">Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="f2c72-142">Teams ocultará el indicador de carga si procede.</span><span class="sxs-lookup"><span data-stu-id="f2c72-142">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="f2c72-143">Si `notifySuccess` no se llama a en el plazo de 30 segundos, se asumirá que la aplicación ha agotado el tiempo de espera y aparecerá una pantalla de error con una opción de reintento.</span><span class="sxs-lookup"><span data-stu-id="f2c72-143">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
5. <span data-ttu-id="f2c72-144">Si la aplicación no se puede cargar, puede llamar `microsoftTeams.appInitialization.notifyFailure(reason);` para informar a Microsoft Teams de que se ha producido un error.</span><span class="sxs-lookup"><span data-stu-id="f2c72-144">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="f2c72-145">A continuación, se mostrará una pantalla de error al usuario:</span><span class="sxs-lookup"><span data-stu-id="f2c72-145">An error screen will then be shown to the user:</span></span>

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