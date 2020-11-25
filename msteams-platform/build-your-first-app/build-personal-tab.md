---
title: 'Introducción: creación de una pestaña personal'
author: heath-hamilton
description: Cree rápidamente una pestaña personal de Microsoft Teams mediante el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: 89d9a2109a863402dd7641d0882c530a0c2e6f66
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409074"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="dface-103">Crear una pestaña personal para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dface-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="dface-104">Las pestañas son una forma sencilla de exponer contenido en la aplicación básicamente mediante la inserción de una página web en Teams.</span><span class="sxs-lookup"><span data-stu-id="dface-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="dface-105">Hay dos tipos de pestañas en Teams.</span><span class="sxs-lookup"><span data-stu-id="dface-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="dface-106">En este tutorial, creará una *pestaña personal* básica, una página de contenido a pantalla completa para usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="dface-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="dface-107">(Las pestañas personales son lo más cercano a una experiencia de sitio web tradicional en Microsoft Teams).</span><span class="sxs-lookup"><span data-stu-id="dface-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dface-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="dface-108">Before you begin</span></span>

<span data-ttu-id="dface-109">Necesita una pestaña personal de ejecución básica para empezar.</span><span class="sxs-lookup"><span data-stu-id="dface-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="dface-110">Si no tiene uno, vea [crear y ejecutar su aplicación primera aplicación Teams](../build-your-first-app/build-and-run.md).</span><span class="sxs-lookup"><span data-stu-id="dface-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="dface-111">La asignación</span><span class="sxs-lookup"><span data-stu-id="dface-111">Your assignment</span></span>

<span data-ttu-id="dface-112">Las personas de su organización tienen problemas para encontrar información de contacto básica para funciones importantes (Departamento de soporte, recursos humanos, etc.).</span><span class="sxs-lookup"><span data-stu-id="dface-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="dface-113">Está a cargo de asegurarse de que puede encontrar rápidamente esta información en un solo punto.</span><span class="sxs-lookup"><span data-stu-id="dface-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="dface-114">¿Cómo lo haría?</span><span class="sxs-lookup"><span data-stu-id="dface-114">How would you do that?</span></span> <span data-ttu-id="dface-115">Por supuesto, una ficha personal de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="dface-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="dface-116">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="dface-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="dface-117">Identificar algunas de las configuraciones de la aplicación y scaffolding relevantes para las pestañas personales</span><span class="sxs-lookup"><span data-stu-id="dface-117">Identify some of the app configurations and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="dface-118">Crear contenido de ficha</span><span class="sxs-lookup"><span data-stu-id="dface-118">Create tab content</span></span>
> * <span data-ttu-id="dface-119">Actualizar el tema de color de una pestaña según las preferencias del usuario</span><span class="sxs-lookup"><span data-stu-id="dface-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="dface-120">1. identificar los componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="dface-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="dface-121">Una gran parte de la configuración de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="dface-121">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="dface-122">Echemos un vistazo a los componentes principales para crear una pestaña personal.</span><span class="sxs-lookup"><span data-stu-id="dface-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="dface-123">Configuraciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="dface-123">App configurations</span></span>

<span data-ttu-id="dface-124">Puede ver y actualizar las configuraciones de la aplicación mediante App Studio, que se incluye en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="dface-124">You can view and update your app configurations using App Studio, which is included in the toolkit.</span></span>

<span data-ttu-id="dface-125">Durante la configuración, el kit de herramientas configuró inicialmente la página de contenido de la pestaña, que es donde se muestra el contenido principal.</span><span class="sxs-lookup"><span data-stu-id="dface-125">During setup, the toolkit initially configured your tab content page, which is where you display your primary content.</span></span> <span data-ttu-id="dface-126">En el kit de herramientas, vaya a **App Studio** y seleccione **pestañas** para ver la configuración.</span><span class="sxs-lookup"><span data-stu-id="dface-126">In the toolkit, go to **App Studio** and select **Tabs** to see the configuration.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="dface-127">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="dface-127">App scaffolding</span></span>

<span data-ttu-id="dface-128">El scaffolding de la aplicación proporciona los componentes para representar la pestaña personal en Teams.</span><span class="sxs-lookup"><span data-stu-id="dface-128">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="dface-129">Hay muchas cosas con las que puede trabajar, pero por ahora solo necesita centrarse en lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="dface-129">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="dface-130">`Tab.js` archivo en el `src/components` directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="dface-130">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="dface-131">Esto es para representar la página de contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="dface-131">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="dface-132">SDK cliente de JavaScript de Microsoft Teams, que viene precargado en los componentes front-end del proyecto.</span><span class="sxs-lookup"><span data-stu-id="dface-132">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="dface-133">2. personalizar la página de contenido de la pestaña</span><span class="sxs-lookup"><span data-stu-id="dface-133">2. Customize your tab content page</span></span>

<span data-ttu-id="dface-134">Compile una lista de contactos importantes en la organización.</span><span class="sxs-lookup"><span data-stu-id="dface-134">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="dface-135">Copie y actualice el siguiente fragmento de código con información que sea relevante para usted o, por el momento, use el código tal y como está.</span><span class="sxs-lookup"><span data-stu-id="dface-135">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="dface-136">Vaya al `src/components` Directorio y Abra `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="dface-136">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="dface-137">Busque la `render()` función y pegue el contenido dentro de `return()` (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="dface-137">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="dface-138">Agregue la regla siguiente a para que `App.css` los vínculos de correo electrónico sean más fáciles de leer independientemente del tema que se use.</span><span class="sxs-lookup"><span data-stu-id="dface-138">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="dface-139">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="dface-139">Save your changes.</span></span> <span data-ttu-id="dface-140">Vaya a la pestaña de la aplicación en Microsoft Teams para ver el nuevo contenido.</span><span class="sxs-lookup"><span data-stu-id="dface-140">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Captura de pantalla de una pestaña personal con contenido estático.":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="dface-142">3. actualizar el tema de ficha</span><span class="sxs-lookup"><span data-stu-id="dface-142">3. Update the tab theme</span></span>

<span data-ttu-id="dface-143">Las aplicaciones buenas se sienten nativas para Teams, por lo que es importante la pestaña se combina con el tema de teams que prefieren los usuarios: predeterminado (claro), oscuro o contraste alto.</span><span class="sxs-lookup"><span data-stu-id="dface-143">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="dface-144">Como puede haber notado en la última captura de pantalla, la pestaña todavía tiene un fondo claro cuando el cliente usa el tema oscuro.</span><span class="sxs-lookup"><span data-stu-id="dface-144">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="dface-145">Esta no es una experiencia de usuario recomendada.</span><span class="sxs-lookup"><span data-stu-id="dface-145">This is not a recommended user experience.</span></span>

<span data-ttu-id="dface-146">El [SDK del cliente de JavaScript para Teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) puede hacer que su aplicación conozca y reaccione a los cambios de tema en el cliente.</span><span class="sxs-lookup"><span data-stu-id="dface-146">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="dface-147">Vamos a examinar cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="dface-147">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="dface-148">Obtener contexto sobre el cliente de Teams</span><span class="sxs-lookup"><span data-stu-id="dface-148">Get context about the Teams client</span></span>

<span data-ttu-id="dface-149">En el `Tab.js` archivo, hay una `microsoftTeams.getContext()` llamada que proporciona [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) información acerca del tema del cliente configurado, entre otros detalles.</span><span class="sxs-lookup"><span data-stu-id="dface-149">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="dface-150">Gracias a la técnica scaffolding de la aplicación, use este código tal y como está para obtener acceso a la `context` interfaz y sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="dface-150">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

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

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="dface-151">Crear un controlador de cambios de tema</span><span class="sxs-lookup"><span data-stu-id="dface-151">Create a theme change handler</span></span>

<span data-ttu-id="dface-152">Con las propiedades que hay a `context` mano, la aplicación tiene una sólida comprensión de lo que sucede alrededor de ella en Teams.</span><span class="sxs-lookup"><span data-stu-id="dface-152">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="dface-153">Pero la aplicación sigue sin saber que su apariencia debería reflejar cualquier tema que elija el usuario.</span><span class="sxs-lookup"><span data-stu-id="dface-153">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="dface-154">Necesita un controlador para que el estado de la aplicación cambie con el tema.</span><span class="sxs-lookup"><span data-stu-id="dface-154">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="dface-155">Inserte el siguiente controlador de cambio de tema inmediatamente después de la `microsoftTeams.getContext()` llamada.</span><span class="sxs-lookup"><span data-stu-id="dface-155">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="dface-156">Coincidencia de estilos de tema</span><span class="sxs-lookup"><span data-stu-id="dface-156">Match theme styles</span></span>

<span data-ttu-id="dface-157">El controlador de cambios de tema está en su ubicación, pero necesitará algún código que responda a los cambios y alinear los colores de la pestaña con el tema actual.</span><span class="sxs-lookup"><span data-stu-id="dface-157">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="dface-158">El siguiente ejemplo es sólo una forma de aplicar estilos a la ficha. Use el código tal y como está, expándalo o escriba el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="dface-158">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="dface-159">Almacene el estado proporcionado por el controlador de cambios de tema en `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="dface-159">Store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="dface-160">Proporcionar una lógica condicional para representar los estilos de la ficha basándose en el tema actual.</span><span class="sxs-lookup"><span data-stu-id="dface-160">Provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="dface-161">En el siguiente ejemplo se muestra una forma básica de hacerlo en 1) comprobando el tema actual en `isTheme` , 2) crear un `newTheme` objeto con propiedades CSS relevantes para el tema actual y 3 aplicar la CSS al elemento HTML raíz del contenido de la pestaña ( `<div>` ).</span><span class="sxs-lookup"><span data-stu-id="dface-161">The following example shows a basic way to do this by 1) checking the current theme in `isTheme`, 2) creating a `newTheme` object with CSS properties relevant to the current theme, and 3) applying the CSS to your tab content's root HTML element (`<div>`).</span></span>

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

<span data-ttu-id="dface-162">Compruebe la pestaña en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="dface-162">Check your tab in Teams.</span></span> <span data-ttu-id="dface-163">La apariencia debe coincidir exactamente con el tema oscuro.</span><span class="sxs-lookup"><span data-stu-id="dface-163">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Captura de pantalla de una pestaña personal con vista de contenido estático.":::

## <a name="well-done"></a><span data-ttu-id="dface-165">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="dface-165">Well done</span></span>

<span data-ttu-id="dface-166">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="dface-166">Congratulations!</span></span> <span data-ttu-id="dface-167">Tiene una aplicación de Microsoft Teams con una pestaña personal que facilita la búsqueda de contactos importantes en la organización.</span><span class="sxs-lookup"><span data-stu-id="dface-167">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="dface-168">Más información</span><span class="sxs-lookup"><span data-stu-id="dface-168">Learn more</span></span>

* <span data-ttu-id="dface-169">[Autenticar usuarios de pestaña con SSO](../tabs/how-to/authentication/auth-aad-sso.md): si solo quiere que los usuarios autorizados vean su pestaña, configure el inicio de sesión único (SSO) a través de Azure Active Directory (ad).</span><span class="sxs-lookup"><span data-stu-id="dface-169">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="dface-170">[Insertar contenido de una aplicación web o página web existente](../tabs/how-to/add-tab.md#tab-requirements): le mostramos cómo crear nuevo contenido para una pestaña personal, pero también puede cargar contenido desde una dirección URL externa.</span><span class="sxs-lookup"><span data-stu-id="dface-170">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="dface-171">[Crear una experiencia sin problemas para su pestaña](../tabs/design/tabs.md): Consulte las directrices recomendadas para diseñar pestañas de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="dface-171">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="dface-172">[Crear pestañas para móviles](../tabs/design/tabs-mobile.md): comprenda cómo desarrollar pestañas para teléfonos y tabletas.</span><span class="sxs-lookup"><span data-stu-id="dface-172">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="dface-173">Uso de datos de Teams con la API de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="dface-173">Utilize Teams data with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="dface-174">Crear una ficha sin el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="dface-174">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="dface-175">Lección siguiente</span><span class="sxs-lookup"><span data-stu-id="dface-175">Next lesson</span></span>

<span data-ttu-id="dface-176">Sabe cómo crear una pestaña para uso personal.</span><span class="sxs-lookup"><span data-stu-id="dface-176">You know how to build a tab for personal use.</span></span> <span data-ttu-id="dface-177">Echemos un vistazo a lo que se necesita para crear una pestaña para los canales y chats del equipo.</span><span class="sxs-lookup"><span data-stu-id="dface-177">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dface-178">Crear una pestaña de canal</span><span class="sxs-lookup"><span data-stu-id="dface-178">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
