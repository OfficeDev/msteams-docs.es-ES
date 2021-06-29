---
title: Expansión del vínculo de la pestaña y vista de fases
author: Rajeshwari-v
description: Cómo deshacer un vínculo, abrir la vista fase y anclar una pestaña con Microsoft Teams aplicación.
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: b54eb5942d19749b39bb9bb504dd8645f5655ef3
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179947"
---
# <a name="tabs-link-unfurling-and-stage-view"></a><span data-ttu-id="1f3e6-103">Expansión del vínculo de la pestaña y vista de fases</span><span class="sxs-lookup"><span data-stu-id="1f3e6-103">Tabs link unfurling and Stage View</span></span>

> [!NOTE]
> <span data-ttu-id="1f3e6-104">Esta característica solo está disponible en [la versión preliminar del](../resources/dev-preview/developer-preview-intro.md) desarrollador público.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-104">This feature is available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="1f3e6-105">Stage View es un nuevo componente de interfaz de usuario (UI), que te permite representar el contenido que se abre en pantalla completa en Teams y anclado como una pestaña.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-105">Stage View is a new user interface (UI) component, which allows you to render the content that is opened in full screen in Teams and pinned as a tab.</span></span>
 
> [!NOTE]
> <span data-ttu-id="1f3e6-106">Actualmente, Teams los clientes móviles no admiten el desafusado y la vista fase.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-106">Currently, Teams mobile clients do no support tabs link unfurling and Stage View.</span></span> <span data-ttu-id="1f3e6-107">Los clientes móviles usan el atributo proporcionado por el desarrollador para abrir la página en el `websiteUrl` explorador web del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-107">Mobile clients use the `websiteUrl` attribute provided by the developer to open the page in the device's web browser.</span></span>

## <a name="stage-view"></a><span data-ttu-id="1f3e6-108">Vista fase</span><span class="sxs-lookup"><span data-stu-id="1f3e6-108">Stage View</span></span>

<span data-ttu-id="1f3e6-109">Stage View es un componente de interfaz de usuario de pantalla completa que puedes invocar para mostrar el contenido web.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-109">Stage View is a full screen UI component that you can invoke to surface your web content.</span></span> <span data-ttu-id="1f3e6-110">El servicio de desamuestración de vínculos existente se actualiza para que se use para convertir direcciones URL en una pestaña mediante una tarjeta adaptable y servicios de chat.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-110">The existing link unfurling service is updated so that it is used to turn URLs into a tab using an Adaptive Card and Chat Services.</span></span> <span data-ttu-id="1f3e6-111">Cuando un usuario envía una dirección URL en un chat o canal, la dirección URL se despliega en una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-111">When a user sends a URL in a chat or channel, the URL is unfurled to an Adaptive Card.</span></span> <span data-ttu-id="1f3e6-112">El usuario puede seleccionar **Ver en** la tarjeta y anclar el contenido como una pestaña directamente desde vista fase.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-112">The user can select **View** in the card, and pin the content as a tab directly from Stage View.</span></span>

## <a name="advantage-of-stage-view"></a><span data-ttu-id="1f3e6-113">Ventaja de la vista fase</span><span class="sxs-lookup"><span data-stu-id="1f3e6-113">Advantage of Stage View</span></span>

<span data-ttu-id="1f3e6-114">Stage View ayuda a proporcionar una experiencia más fluida de visualización de contenido en Teams.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-114">Stage View helps provide a more seamless experience of viewing content in Teams.</span></span> <span data-ttu-id="1f3e6-115">Los usuarios pueden abrir y ver el contenido proporcionado por la aplicación sin salir del contexto y pueden anclar el contenido al chat o canal para un acceso rápido futuro.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-115">Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access.</span></span> <span data-ttu-id="1f3e6-116">Esto lleva a una mayor interacción del usuario con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-116">This leads to a higher user engagement with your app.</span></span>

## <a name="stage-view-vs-task-module"></a><span data-ttu-id="1f3e6-117">Módulo vista fase frente a tarea</span><span class="sxs-lookup"><span data-stu-id="1f3e6-117">Stage View vs. Task module</span></span>

|<span data-ttu-id="1f3e6-118">Vista fase</span><span class="sxs-lookup"><span data-stu-id="1f3e6-118">Stage View</span></span>|<span data-ttu-id="1f3e6-119">Módulo de tareas</span><span class="sxs-lookup"><span data-stu-id="1f3e6-119">Task module</span></span>|
|:-----------|:-----------|
|<span data-ttu-id="1f3e6-120">La vista fase es útil cuando tiene contenido enriquecido para mostrar a los usuarios, como una página, un panel, un archivo, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-120">Stage View is useful when you have rich content to display to the users, such as a page, a dashboard, a file, and so on.</span></span> <span data-ttu-id="1f3e6-121">Proporciona características enriquecciones que ayudan a representar el contenido en el lienzo de pantalla completa.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-121">It provides  rich features that helps to render your content in the full-screen canvas.</span></span>|<span data-ttu-id="1f3e6-122">[El módulo de](../task-modules-and-cards/task-modules/task-modules-tabs.md) tareas es especialmente útil para mostrar mensajes que requieren atención del usuario o recopilar información necesaria para pasar al paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-122">[Task module](../task-modules-and-cards/task-modules/task-modules-tabs.md) is especially useful to display messages that require user attention, or collect information required to move to the next step.</span></span>|
  
## <a name="invoke-stage-view"></a><span data-ttu-id="1f3e6-123">Invocar vista fase</span><span class="sxs-lookup"><span data-stu-id="1f3e6-123">Invoke Stage View</span></span>

<span data-ttu-id="1f3e6-124">Puede invocar la vista fase de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="1f3e6-124">You can invoke Stage View in the following  ways:</span></span>

* [<span data-ttu-id="1f3e6-125">Invocar la vista fase desde la tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="1f3e6-125">Invoke Stage View from Adaptive Card</span></span>](#invoke-stage-view-from-adaptive-card)
* [<span data-ttu-id="1f3e6-126">Invocar vista de fase a través de un vínculo profundo</span><span class="sxs-lookup"><span data-stu-id="1f3e6-126">Invoke Stage View through deep link</span></span>](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a><span data-ttu-id="1f3e6-127">Invocar la vista fase desde la tarjeta adaptable</span><span class="sxs-lookup"><span data-stu-id="1f3e6-127">Invoke Stage View from Adaptive Card</span></span>

<span data-ttu-id="1f3e6-128">Cuando el usuario escribe una dirección URL en el cliente de escritorio [](../task-modules-and-cards/cards/cards-actions.md) Teams, el bot se invoca y devuelve una tarjeta adaptable con la opción de abrir la dirección URL en una fase.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-128">When the user enters a URL on the Teams desktop client, the bot is invoked and returns an [Adaptive Card](../task-modules-and-cards/cards/cards-actions.md) with the option to open the URL in a stage.</span></span> <span data-ttu-id="1f3e6-129">Después de iniciar una fase y de proporcionarla, puede agregar la capacidad de anclar `tabInfo` la fase como una pestaña.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-129">After a stage is launched and the `tabInfo` is provided, you can add the ability to pin the stage as a tab.</span></span>  

<span data-ttu-id="1f3e6-130">Las siguientes imágenes muestran una fase abierta desde una tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="1f3e6-130">The following images display a stage opened from an Adaptive Card:</span></span>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt="Open a stage from Adaptive Card" width="700"/>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt="Open a stage" width="700"/>

### <a name="example"></a><span data-ttu-id="1f3e6-131">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1f3e6-131">Example</span></span>

<span data-ttu-id="1f3e6-132">A continuación se muestra el código para abrir una fase desde una tarjeta adaptable:</span><span class="sxs-lookup"><span data-stu-id="1f3e6-132">Following is the code to open a stage from an Adaptive Card:</span></span>

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

<span data-ttu-id="1f3e6-133">El `invoke` tipo de solicitud debe ser `composeExtension/queryLink` .</span><span class="sxs-lookup"><span data-stu-id="1f3e6-133">The `invoke` request type must be `composeExtension/queryLink`.</span></span>

> [!NOTE]
> * <span data-ttu-id="1f3e6-134">`invoke` flujo de trabajo es similar al flujo de trabajo `appLinking` actual.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-134">`invoke` workflow is similar to the current `appLinking` workflow.</span></span> 
> * <span data-ttu-id="1f3e6-135">Para mantener la coherencia, se recomienda nombrar `Action.Submit` como `View` .</span><span class="sxs-lookup"><span data-stu-id="1f3e6-135">To maintain consistency, it is recommended to name `Action.Submit` as `View`.</span></span>
> * <span data-ttu-id="1f3e6-136">`websiteUrl` es una propiedad necesaria que se debe pasar en el `TabInfo` objeto.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-136">`websiteUrl` is a required property to be passed in the `TabInfo` object.</span></span>

<span data-ttu-id="1f3e6-137">A continuación se muestra el proceso para invocar la vista fase:</span><span class="sxs-lookup"><span data-stu-id="1f3e6-137">Following is the process to invoke Stage View:</span></span>

* <span data-ttu-id="1f3e6-138">Cuando el usuario selecciona **Ver,** el bot recibe una `invoke` solicitud.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-138">When the user selects **View**, the bot receives an `invoke` request.</span></span> <span data-ttu-id="1f3e6-139">El tipo de solicitud es `composeExtension/queryLink` .</span><span class="sxs-lookup"><span data-stu-id="1f3e6-139">The request type is `composeExtension/queryLink`.</span></span>
* <span data-ttu-id="1f3e6-140">`invoke` respuesta del bot contiene una tarjeta adaptable con tipo `tab/tabInfoAction` en él.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-140">`invoke` response from bot contains an Adaptive Card with type `tab/tabInfoAction` in it.</span></span>
* <span data-ttu-id="1f3e6-141">El bot responde con un `200` código.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-141">The bot responds with a `200` code.</span></span>

> [!NOTE]
> <span data-ttu-id="1f3e6-142">Actualmente, Teams los clientes móviles no admiten la funcionalidad Vista de fase.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-142">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="1f3e6-143">Cuando un usuario selecciona **Ver** en un cliente móvil, el usuario se toma en el explorador del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-143">When a user selects **View** on a mobile client, the user is taken to the device's browser.</span></span> <span data-ttu-id="1f3e6-144">El explorador abre la dirección URL especificada en el `websiteUrl` parámetro del `TabInfo` objeto.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-144">The browser opens the URL specified in the `websiteUrl` parameter of the `TabInfo` object.</span></span>

## <a name="invoke-stage-view-through-deep-link"></a><span data-ttu-id="1f3e6-145">Invocar vista de fase a través de un vínculo profundo</span><span class="sxs-lookup"><span data-stu-id="1f3e6-145">Invoke Stage View through deep link</span></span>

<span data-ttu-id="1f3e6-146">Para invocar la vista de fase a través del vínculo profundo desde la pestaña, debe ajustar la dirección URL del vínculo profundo en la `microsoftTeams.executeDeeplink(url)` API.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-146">To invoke the Stage View through deep link from your tab, you must wrap the deep link URL in the `microsoftTeams.executeDeeplink(url)` API.</span></span> <span data-ttu-id="1f3e6-147">El vínculo profundo también se puede pasar a través de una `OpenURL` acción en la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-147">The deep link can also be passed through an `OpenURL` action in the card.</span></span>

<span data-ttu-id="1f3e6-148">La siguiente imagen muestra una vista de fase invocada a través de un vínculo profundo:</span><span class="sxs-lookup"><span data-stu-id="1f3e6-148">The following image displays a Stage View invoked through a deep link:</span></span>

<img src="~/assets/images/tab-images/invoke-stage-view-through-deep-link.png" alt="Invoke a Stage View through a deep link" width="400"/>

### <a name="syntax"></a><span data-ttu-id="1f3e6-149">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="1f3e6-149">Syntax</span></span>

<span data-ttu-id="1f3e6-150">A continuación se muestra la sintaxis de vínculo profundo:</span><span class="sxs-lookup"><span data-stu-id="1f3e6-150">Following is the deeplink syntax:</span></span>  
 
<span data-ttu-id="1f3e6-151"> https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":"[contentUrl]","websiteUrl":"[websiteUrl]","name":"[name]"}</span><span class="sxs-lookup"><span data-stu-id="1f3e6-151">https://teams.microsoft.com/l/stage/{appId}/0?context={“contentUrl”:”[contentUrl]”,“websiteUrl”:”[websiteUrl]”,“name”:”[name]”}</span></span>

### <a name="examples"></a><span data-ttu-id="1f3e6-152">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="1f3e6-152">Examples</span></span>

<span data-ttu-id="1f3e6-153">Cuando un usuario escribe una dirección URL, se despliega en una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-153">When a user enters a URL, it is unfurled into an Adaptive card.</span></span>

<span data-ttu-id="1f3e6-154">A continuación se muestran los ejemplos de vínculos profundos para invocar la vista fase:</span><span class="sxs-lookup"><span data-stu-id="1f3e6-154">Following are the deep link examples to invoke Stage View:</span></span>

<span data-ttu-id="1f3e6-155">**Ejemplo 1**</span><span class="sxs-lookup"><span data-stu-id="1f3e6-155">**Example 1**</span></span>

<span data-ttu-id="1f3e6-156"> https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","websiteUrl https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="1f3e6-156">https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

<span data-ttu-id="1f3e6-157">**Ejemplo 2**</span><span class="sxs-lookup"><span data-stu-id="1f3e6-157">**Example 2**</span></span>

<span data-ttu-id="1f3e6-158"> https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","websiteUrl https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name"Contoso"}</span><span class="sxs-lookup"><span data-stu-id="1f3e6-158">https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={“contentUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“websiteUrl”:”https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx”,“name”:”Contoso”}</span></span>

> [!NOTE]
> * <span data-ttu-id="1f3e6-159">El `name` vínculo es opcional en profundidad.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-159">The `name` is optional in deep link.</span></span> <span data-ttu-id="1f3e6-160">Si no se incluye, el nombre de la aplicación lo reemplaza.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-160">If not included, the app name replaces it.</span></span>
> * <span data-ttu-id="1f3e6-161">El vínculo profundo también se puede pasar a través de una `OpenURL` acción.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-161">The deep link can also be passed through an `OpenURL` action.</span></span>
> * <span data-ttu-id="1f3e6-162">Actualmente, Teams los clientes móviles no admiten la funcionalidad Vista de fase.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-162">Currently, Teams mobile clients do not support the Stage View capability.</span></span> <span data-ttu-id="1f3e6-163">Cuando los usuarios seleccionan un vínculo profundo a una vista de fase, se les traslada al explorador web de su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-163">When users select a deep link to a Stage View, they are taken to their device's web browser.</span></span> <span data-ttu-id="1f3e6-164">El explorador web abre la dirección URL especificada en el `websiteUrl` parámetro del vínculo profundo.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-164">The web browser opens the URL specified in the `websiteUrl` parameter of the deep link.</span></span>
> * <span data-ttu-id="1f3e6-165">Cuando inicies una fase desde un contexto determinado, asegúrate de que la aplicación funciona en ese contexto.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-165">When you launch a Stage from a certain context, ensure that your app works in that context.</span></span> <span data-ttu-id="1f3e6-166">Por ejemplo, si la vista fase se inicia desde una aplicación personal, debes asegurarte de que la aplicación tenga un ámbito personal.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-166">For example, if your Stage View is launched from a personal app, you must ensure your app has a personal scope.</span></span>

## <a name="tab-information-property"></a><span data-ttu-id="1f3e6-167">Propiedad tab information</span><span class="sxs-lookup"><span data-stu-id="1f3e6-167">Tab information property</span></span>

| <span data-ttu-id="1f3e6-168">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="1f3e6-168">Property name</span></span> | <span data-ttu-id="1f3e6-169">Tipo</span><span class="sxs-lookup"><span data-stu-id="1f3e6-169">Type</span></span> | <span data-ttu-id="1f3e6-170">Número de caracteres</span><span class="sxs-lookup"><span data-stu-id="1f3e6-170">Number of characters</span></span> | <span data-ttu-id="1f3e6-171">Descripción</span><span class="sxs-lookup"><span data-stu-id="1f3e6-171">Description</span></span> |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | <span data-ttu-id="1f3e6-172">Cadena</span><span class="sxs-lookup"><span data-stu-id="1f3e6-172">String</span></span> | <span data-ttu-id="1f3e6-173">64</span><span class="sxs-lookup"><span data-stu-id="1f3e6-173">64</span></span> | <span data-ttu-id="1f3e6-174">Esta propiedad es un identificador único para la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-174">This property is a  unique identifier for the entity that the tab displays.</span></span> <span data-ttu-id="1f3e6-175">Este campo es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-175">This is a required field.</span></span>|
| `name` | <span data-ttu-id="1f3e6-176">Cadena</span><span class="sxs-lookup"><span data-stu-id="1f3e6-176">String</span></span> | <span data-ttu-id="1f3e6-177">128</span><span class="sxs-lookup"><span data-stu-id="1f3e6-177">128</span></span> | <span data-ttu-id="1f3e6-178">Esta propiedad es el nombre para mostrar de la pestaña en la interfaz de canal.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-178">This property is the display name of the tab in the channel interface.</span></span> <span data-ttu-id="1f3e6-179">Este campo es opcional.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-179">This is an optional field.</span></span>|
| `contentUrl` | <span data-ttu-id="1f3e6-180">Cadena</span><span class="sxs-lookup"><span data-stu-id="1f3e6-180">String</span></span> | <span data-ttu-id="1f3e6-181">2048</span><span class="sxs-lookup"><span data-stu-id="1f3e6-181">2048</span></span> | <span data-ttu-id="1f3e6-182">Esta propiedad es la dirección URL https:// que apunta a la interfaz de usuario de la entidad que se va a mostrar en el Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-182">This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span> <span data-ttu-id="1f3e6-183">Este campo es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-183">This is a required field.</span></span>|
| `websiteUrl?` | <span data-ttu-id="1f3e6-184">Cadena</span><span class="sxs-lookup"><span data-stu-id="1f3e6-184">String</span></span> | <span data-ttu-id="1f3e6-185">2048</span><span class="sxs-lookup"><span data-stu-id="1f3e6-185">2048</span></span> | <span data-ttu-id="1f3e6-186">Esta propiedad es la https:// url a la que apuntar, si un usuario selecciona ver en un explorador.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-186">This property is the https:// URL to point at, if a user selects to view in a browser.</span></span> <span data-ttu-id="1f3e6-187">Este campo es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-187">This is a required field.</span></span>|
| `removeUrl?` | <span data-ttu-id="1f3e6-188">Cadena</span><span class="sxs-lookup"><span data-stu-id="1f3e6-188">String</span></span> | <span data-ttu-id="1f3e6-189">2048</span><span class="sxs-lookup"><span data-stu-id="1f3e6-189">2048</span></span> | <span data-ttu-id="1f3e6-190">Esta propiedad es la dirección URL https:// que apunta a la interfaz de usuario que se va a mostrar cuando el usuario elimina la pestaña. Este es un campo opcional.</span><span class="sxs-lookup"><span data-stu-id="1f3e6-190">This property is the https:// URL that points to the UI to be displayed when the user deletes the tab. This is an optional field.</span></span>|

## <a name="see-also"></a><span data-ttu-id="1f3e6-191">Vea también</span><span class="sxs-lookup"><span data-stu-id="1f3e6-191">See also</span></span>

* [<span data-ttu-id="1f3e6-192">Desafutización de vínculos de extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="1f3e6-192">Messaging extensions link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="1f3e6-193">Teams pestañas</span><span class="sxs-lookup"><span data-stu-id="1f3e6-193">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="1f3e6-194">Crear una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="1f3e6-194">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="1f3e6-195">Crear una pestaña de canal o grupo</span><span class="sxs-lookup"><span data-stu-id="1f3e6-195">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a><span data-ttu-id="1f3e6-196">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="1f3e6-196">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1f3e6-197">Crear pestañas de conversación</span><span class="sxs-lookup"><span data-stu-id="1f3e6-197">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)