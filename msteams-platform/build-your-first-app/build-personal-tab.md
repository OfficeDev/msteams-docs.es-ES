---
title: Crear una ficha personal de Teams
author: heath-hamilton
description: Obtenga información sobre cómo crear una pestaña personal para su primera aplicación de Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: a86c9e1e46b97c6b265bfa9ad2f618655c524ee4
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237807"
---
# <a name="build-a-teams-personal-tab"></a><span data-ttu-id="8477d-103">Crear una ficha personal de Teams</span><span class="sxs-lookup"><span data-stu-id="8477d-103">Build a Teams personal tab</span></span>

<span data-ttu-id="8477d-104">Las pestañas son una forma sencilla de exponer contenido en la aplicación básicamente mediante la inserción de una página web en Teams.</span><span class="sxs-lookup"><span data-stu-id="8477d-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="8477d-105">Hay dos tipos de pestañas en Teams.</span><span class="sxs-lookup"><span data-stu-id="8477d-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="8477d-106">En este tutorial, creará una *pestaña personal*básica, una página de contenido a pantalla completa para usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="8477d-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="8477d-107">(Las pestañas personales son lo más cercano a una experiencia de sitio web tradicional en Microsoft Teams).</span><span class="sxs-lookup"><span data-stu-id="8477d-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8477d-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="8477d-108">Before you begin</span></span>

<span data-ttu-id="8477d-109">Necesita una pestaña personal de ejecución básica para empezar.</span><span class="sxs-lookup"><span data-stu-id="8477d-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="8477d-110">Si no tiene uno, vea [crear y ejecutar su aplicación primera aplicación Teams](../build-your-first-app/build-and-run.md).</span><span class="sxs-lookup"><span data-stu-id="8477d-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="8477d-111">La asignación</span><span class="sxs-lookup"><span data-stu-id="8477d-111">Your assignment</span></span>

<span data-ttu-id="8477d-112">Las personas de su organización tienen problemas para encontrar información de contacto básica para funciones importantes (Departamento de soporte, recursos humanos, etc.).</span><span class="sxs-lookup"><span data-stu-id="8477d-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="8477d-113">Está a cargo de asegurarse de que puede encontrar rápidamente esta información en un solo punto.</span><span class="sxs-lookup"><span data-stu-id="8477d-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="8477d-114">¿Cómo lo haría?</span><span class="sxs-lookup"><span data-stu-id="8477d-114">How would you do that?</span></span> <span data-ttu-id="8477d-115">Por supuesto, una ficha personal de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8477d-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="8477d-116">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="8477d-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="8477d-117">Identificar algunas de las propiedades del manifiesto de la aplicación y scaffolding relevantes para las pestañas personales</span><span class="sxs-lookup"><span data-stu-id="8477d-117">Identify some of the app manifest properties and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="8477d-118">Crear contenido de ficha</span><span class="sxs-lookup"><span data-stu-id="8477d-118">Create tab content</span></span>
> * <span data-ttu-id="8477d-119">Actualizar el tema de color de una pestaña según las preferencias del usuario</span><span class="sxs-lookup"><span data-stu-id="8477d-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="8477d-120">1. identificar los componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="8477d-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="8477d-121">La gran parte del manifiesto de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="8477d-121">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="8477d-122">Echemos un vistazo a los componentes principales para crear una pestaña personal.</span><span class="sxs-lookup"><span data-stu-id="8477d-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="8477d-123">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8477d-123">App manifest</span></span>

<span data-ttu-id="8477d-124">El siguiente fragmento de código del manifiesto de la aplicación (el `manifest.json` archivo del `.publish` directorio del proyecto) muestra [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , que incluye las propiedades y los valores predeterminados relacionados con las pestañas personales.</span><span class="sxs-lookup"><span data-stu-id="8477d-124">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which includes properties and default values relevant to personal tabs.</span></span>

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "Personal Tab",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

* <span data-ttu-id="8477d-125">`entityId`: Un identificador único para la página que se muestra en la pestaña.</span><span class="sxs-lookup"><span data-stu-id="8477d-125">`entityId`: A unique identifier for the page displayed by the tab.</span></span>
* <span data-ttu-id="8477d-126">`name`: El nombre para mostrar de la ficha (por ejemplo, "mis contactos").</span><span class="sxs-lookup"><span data-stu-id="8477d-126">`name`: The tab's display name (for example, "My Contacts").</span></span>
* <span data-ttu-id="8477d-127">`contentUrl`: La dirección URL del host la página de contenido de la ficha (debe ser HTTPS).</span><span class="sxs-lookup"><span data-stu-id="8477d-127">`contentUrl`: The host URL the tab content page (must be HTTPS).</span></span>
* <span data-ttu-id="8477d-128">`scopes`: Especifica que la pestaña es solo para uso personal.</span><span class="sxs-lookup"><span data-stu-id="8477d-128">`scopes`: Specifies the tab is for personal use only.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="8477d-129">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8477d-129">App scaffolding</span></span>

<span data-ttu-id="8477d-130">El scaffolding de la aplicación proporciona los componentes para representar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="8477d-130">The app scaffolding provides the components for rendering your tab in Teams.</span></span> <span data-ttu-id="8477d-131">Hay muchas cosas con las que puede trabajar, pero por ahora solo necesita centrarse en lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8477d-131">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="8477d-132">`Tab.js` archivo en el `src/components` directorio del proyecto</span><span class="sxs-lookup"><span data-stu-id="8477d-132">`Tab.js` file in the `src/components` directory of your project</span></span>
* <span data-ttu-id="8477d-133">SDK para cliente de JavaScript de Microsoft Teams, que viene previamente cargado en los componentes front-end del proyecto</span><span class="sxs-lookup"><span data-stu-id="8477d-133">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="8477d-134">2. personalizar la página de contenido de la pestaña</span><span class="sxs-lookup"><span data-stu-id="8477d-134">2. Customize your tab content page</span></span>

<span data-ttu-id="8477d-135">Compile una lista de contactos importantes en la organización.</span><span class="sxs-lookup"><span data-stu-id="8477d-135">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="8477d-136">Copie y actualice el siguiente fragmento de código con información que sea relevante para usted o, por el momento, use el código tal y como está.</span><span class="sxs-lookup"><span data-stu-id="8477d-136">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

```JSX
<div>
  <h1>Important Contacts</h1>
    <ul>
      <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
      <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
      <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
    </ul>
</div>
```

<span data-ttu-id="8477d-137">Vaya al `src/components` Directorio y Abra `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="8477d-137">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="8477d-138">Busque la `render()` función y pegue el contenido dentro de `return()` (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="8477d-138">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

```JavaScript
render() {

    let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

    return (
    <div>
      <h1>Important Contacts</h1>
        <ul>
          <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
          <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
          <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
        </ul>
    </div>
    );
}
```

<span data-ttu-id="8477d-139">Agregue la regla siguiente a para que `App.css` los vínculos de correo electrónico sean más fáciles de leer independientemente del tema que se use.</span><span class="sxs-lookup"><span data-stu-id="8477d-139">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="8477d-140">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="8477d-140">Save your changes.</span></span> <span data-ttu-id="8477d-141">Vaya a la pestaña de la aplicación en Microsoft Teams para ver el nuevo contenido.</span><span class="sxs-lookup"><span data-stu-id="8477d-141">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Captura de pantalla de una pestaña personal con contenido estático.":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="8477d-143">3. actualizar el tema de ficha</span><span class="sxs-lookup"><span data-stu-id="8477d-143">3. Update the tab theme</span></span>

<span data-ttu-id="8477d-144">Las aplicaciones buenas se sienten nativas para Teams, por lo que es importante la pestaña se combina con el tema de teams que prefieren los usuarios: predeterminado (claro), oscuro o contraste alto.</span><span class="sxs-lookup"><span data-stu-id="8477d-144">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="8477d-145">Como puede haber notado en la última captura de pantalla, la pestaña todavía tiene un fondo claro cuando el cliente usa el tema oscuro.</span><span class="sxs-lookup"><span data-stu-id="8477d-145">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="8477d-146">Esta no es una experiencia de usuario recomendada.</span><span class="sxs-lookup"><span data-stu-id="8477d-146">This is not a recommended user experience.</span></span>

<span data-ttu-id="8477d-147">El [SDK del cliente de JavaScript para Teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) puede hacer que su aplicación conozca y reaccione a los cambios de tema en el cliente.</span><span class="sxs-lookup"><span data-stu-id="8477d-147">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="8477d-148">Vamos a examinar cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="8477d-148">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="8477d-149">Obtener contexto sobre el cliente de Teams</span><span class="sxs-lookup"><span data-stu-id="8477d-149">Get context about the Teams client</span></span>

<span data-ttu-id="8477d-150">En el `Tab.js` archivo, hay una `microsoftTeams.getContext()` llamada que proporciona [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) información acerca del tema del cliente configurado, entre otros detalles.</span><span class="sxs-lookup"><span data-stu-id="8477d-150">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="8477d-151">Gracias a la técnica scaffolding de la aplicación, use este código tal y como está para obtener acceso a la `context` interfaz y sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="8477d-151">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

```JavaScript
componentDidMount(){
  // Get the user context from Teams and set it in the state
  microsoftTeams.getContext((context, error) => {
    this.setState({
      context: context
    });
  });
  // Next steps: Error handling using the error object
}
```

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="8477d-152">Crear un controlador de cambios de tema</span><span class="sxs-lookup"><span data-stu-id="8477d-152">Create a theme change handler</span></span>

<span data-ttu-id="8477d-153">Con las propiedades que hay a `context` mano, la aplicación tiene una sólida comprensión de lo que sucede alrededor de ella en Teams.</span><span class="sxs-lookup"><span data-stu-id="8477d-153">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="8477d-154">Pero la aplicación sigue sin saber que su apariencia debería reflejar cualquier tema que elija el usuario.</span><span class="sxs-lookup"><span data-stu-id="8477d-154">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="8477d-155">Necesita un controlador para que el estado de la aplicación cambie con el tema.</span><span class="sxs-lookup"><span data-stu-id="8477d-155">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="8477d-156">Inserte el siguiente controlador de cambio de tema inmediatamente después de la `microsoftTeams.getContext()` llamada.</span><span class="sxs-lookup"><span data-stu-id="8477d-156">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="8477d-157">Coincidencia de estilos de tema</span><span class="sxs-lookup"><span data-stu-id="8477d-157">Match theme styles</span></span>

<span data-ttu-id="8477d-158">El controlador de cambios de tema está en su ubicación, pero necesitará algún código que responda a los cambios y alinear los colores de la pestaña con el tema actual.</span><span class="sxs-lookup"><span data-stu-id="8477d-158">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="8477d-159">El siguiente ejemplo es sólo una forma de aplicar estilos a la ficha. Use el código tal y como está, expándalo o escriba el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="8477d-159">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="8477d-160">Almacene el estado proporcionado por el controlador de cambios de tema en `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="8477d-160">Store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="8477d-161">Proporcionar una lógica condicional para representar los estilos de la ficha basándose en el tema actual.</span><span class="sxs-lookup"><span data-stu-id="8477d-161">Provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="8477d-162">En el siguiente ejemplo se muestra una forma básica de hacerlo en 1) comprobando el tema actual en `isTheme` , 2) crear un `newTheme` objeto con propiedades CSS relevantes para el tema actual y 3 aplicar la CSS al elemento HTML raíz del contenido de la pestaña ( `<div>` ).</span><span class="sxs-lookup"><span data-stu-id="8477d-162">The following example shows a basic way to do this by 1) checking the current theme in `isTheme`, 2) creating a `newTheme` object with CSS properties relevant to the current theme, and 3) applying the CSS to your tab content's root HTML element (`<div>`).</span></span>

```JavaScript
let newTheme

if (isTheme === "default") {
  newTheme = {
    backgroundColor: "#EEF1F5",
    color: "#16233A"
  };
} else {
  newTheme = {
    backgroundColor: "#2B2B30",
    color: "#FFFFFF"
  };
}
```

<span data-ttu-id="8477d-163">Compruebe la pestaña en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8477d-163">Check your tab in Teams.</span></span> <span data-ttu-id="8477d-164">La apariencia debe coincidir exactamente con el tema oscuro.</span><span class="sxs-lookup"><span data-stu-id="8477d-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Captura de pantalla de una pestaña personal con vista de contenido estático.":::

## <a name="well-done"></a><span data-ttu-id="8477d-166">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="8477d-166">Well done</span></span>

<span data-ttu-id="8477d-167">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="8477d-167">Congratulations!</span></span> <span data-ttu-id="8477d-168">Tiene una aplicación de Microsoft Teams con una pestaña personal que facilita la búsqueda de contactos importantes en la organización.</span><span class="sxs-lookup"><span data-stu-id="8477d-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="8477d-169">Más información</span><span class="sxs-lookup"><span data-stu-id="8477d-169">Learn more</span></span>

* <span data-ttu-id="8477d-170">[Autenticar usuarios de pestaña con SSO](../tabs/how-to/authentication/auth-aad-sso.md): si solo quiere que los usuarios autorizados vean su pestaña, configure el inicio de sesión único (SSO) a través de Azure Active Directory (ad).</span><span class="sxs-lookup"><span data-stu-id="8477d-170">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="8477d-171">[Insertar contenido de una aplicación web o página web existente](../tabs/how-to/add-tab.md#tab-requirements): le mostramos cómo crear nuevo contenido para una pestaña personal, pero también puede cargar contenido desde una dirección URL externa.</span><span class="sxs-lookup"><span data-stu-id="8477d-171">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="8477d-172">[Crear una experiencia sin problemas para su pestaña](../tabs/design/tabs.md): Consulte las directrices recomendadas para diseñar pestañas de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8477d-172">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="8477d-173">[Crear pestañas para móviles](../tabs/design/tabs-mobile.md): comprenda cómo desarrollar pestañas para teléfonos y tabletas.</span><span class="sxs-lookup"><span data-stu-id="8477d-173">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="8477d-174">Integración con la API de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="8477d-174">Integrate with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="8477d-175">Crear una ficha sin el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="8477d-175">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="8477d-176">Lección siguiente</span><span class="sxs-lookup"><span data-stu-id="8477d-176">Next lesson</span></span>

<span data-ttu-id="8477d-177">Sabe cómo crear una pestaña para uso personal.</span><span class="sxs-lookup"><span data-stu-id="8477d-177">You know how to build a tab for personal use.</span></span> <span data-ttu-id="8477d-178">Echemos un vistazo a lo que se necesita para crear una pestaña para los canales y chats del equipo.</span><span class="sxs-lookup"><span data-stu-id="8477d-178">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8477d-179">Crear una ficha de canal</span><span class="sxs-lookup"><span data-stu-id="8477d-179">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
