---
title: 'Introducción: crear una pestaña personal'
author: heath-hamilton
description: Cree rápidamente una pestaña personal de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: 083d1425fe43a9b150732aa35bef34e2349c6ea6
ms.sourcegitcommit: b99ed616db734371e4af4594b7e895c5b05737c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2021
ms.locfileid: "50162904"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="8577e-103">Crear una pestaña personal para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8577e-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="8577e-104">Las pestañas son una forma sencilla de hacer que el contenido de la aplicación se inserte básicamente en Una página web en Teams.</span><span class="sxs-lookup"><span data-stu-id="8577e-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="8577e-105">Hay dos tipos de pestañas en Teams.</span><span class="sxs-lookup"><span data-stu-id="8577e-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="8577e-106">En este tutorial, compilará una pestaña *personal* básica, una página de contenido de pantalla completa para usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="8577e-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="8577e-107">(Las pestañas personales son lo más cercano a una experiencia de sitio web tradicional en Teams).</span><span class="sxs-lookup"><span data-stu-id="8577e-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8577e-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="8577e-108">Before you begin</span></span>

<span data-ttu-id="8577e-109">Necesita una pestaña personal básica en ejecución para empezar.</span><span class="sxs-lookup"><span data-stu-id="8577e-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="8577e-110">Si no tiene uno, vea [compilar y ejecutar la primera aplicación de Teams.](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="8577e-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="8577e-111">Su asignación</span><span class="sxs-lookup"><span data-stu-id="8577e-111">Your assignment</span></span>

<span data-ttu-id="8577e-112">Las personas de su organización tienen problemas para encontrar información de contacto básica para funciones importantes (servicio de soporte, recursos humanos, etc.).</span><span class="sxs-lookup"><span data-stu-id="8577e-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="8577e-113">Usted es el encargado de asegurarse de que puedan encontrar rápidamente esta información en un solo lugar.</span><span class="sxs-lookup"><span data-stu-id="8577e-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="8577e-114">¿Cómo lo haría?</span><span class="sxs-lookup"><span data-stu-id="8577e-114">How would you do that?</span></span> <span data-ttu-id="8577e-115">Una pestaña personal de Teams, por supuesto.</span><span class="sxs-lookup"><span data-stu-id="8577e-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="8577e-116">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="8577e-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="8577e-117">Identificar algunas de las configuraciones de aplicaciones y scaffolding relevantes para las pestañas personales</span><span class="sxs-lookup"><span data-stu-id="8577e-117">Identify some of the app configurations and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="8577e-118">Crear contenido de pestaña</span><span class="sxs-lookup"><span data-stu-id="8577e-118">Create tab content</span></span>
> * <span data-ttu-id="8577e-119">Actualizar el tema de color de una pestaña en función de las preferencias del usuario</span><span class="sxs-lookup"><span data-stu-id="8577e-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="8577e-120">1. Identificar componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="8577e-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="8577e-121">Gran parte de las configuraciones de aplicaciones y scaffolding se establecen automáticamente al crear el proyecto con Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="8577e-121">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="8577e-122">Veamos los componentes principales para crear una pestaña personal.</span><span class="sxs-lookup"><span data-stu-id="8577e-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="8577e-123">Configuraciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8577e-123">App configurations</span></span>

<span data-ttu-id="8577e-124">En el kit de herramientas, ve **a App Studio** para ver y actualizar las configuraciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8577e-124">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="8577e-125">Scaffolding de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8577e-125">App scaffolding</span></span>

<span data-ttu-id="8577e-126">El scaffolding de la aplicación proporciona los componentes para representar la pestaña personal en Teams.</span><span class="sxs-lookup"><span data-stu-id="8577e-126">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="8577e-127">Hay mucho con lo que puede trabajar, pero por ahora solo necesita centrarse en lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8577e-127">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="8577e-128">`Tab.js` en el `src/components` directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="8577e-128">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="8577e-129">Esto es para representar la página de contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="8577e-129">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="8577e-130">SDK de cliente de JavaScript de Microsoft Teams, que viene cargado previamente en los componentes front-end de su proyecto.</span><span class="sxs-lookup"><span data-stu-id="8577e-130">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="8577e-131">2. Personalizar la página de contenido de la pestaña</span><span class="sxs-lookup"><span data-stu-id="8577e-131">2. Customize your tab content page</span></span>

<span data-ttu-id="8577e-132">Compile una lista de contactos importantes de su organización.</span><span class="sxs-lookup"><span data-stu-id="8577e-132">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="8577e-133">Copie y actualice el siguiente fragmento de código con información que sea relevante para usted o, por razones de tiempo, use el código tal como está.</span><span class="sxs-lookup"><span data-stu-id="8577e-133">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="8577e-134">Vaya al directorio `src/components` y abra `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="8577e-134">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="8577e-135">Busque la `render()` función y pegue el contenido dentro `return()` (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="8577e-135">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="8577e-136">Agregue la siguiente regla para que los vínculos de correo electrónico sean más fáciles `App.css` de leer, independientemente del tema que se utilice.</span><span class="sxs-lookup"><span data-stu-id="8577e-136">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="8577e-137">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="8577e-137">Save your changes.</span></span> <span data-ttu-id="8577e-138">Vaya a la pestaña de la aplicación en Teams para ver el nuevo contenido.</span><span class="sxs-lookup"><span data-stu-id="8577e-138">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Captura de pantalla de una pestaña personal con contenido estático.":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="8577e-140">3. Actualizar el tema de la pestaña</span><span class="sxs-lookup"><span data-stu-id="8577e-140">3. Update the tab theme</span></span>

<span data-ttu-id="8577e-141">Las buenas aplicaciones se sienten nativas de Teams, por lo que es importante que la pestaña se combine con el tema de Teams que prefieran los usuarios: predeterminado (claro), oscuro o contraste alto.</span><span class="sxs-lookup"><span data-stu-id="8577e-141">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="8577e-142">Como puede que hayas observado en la última captura de pantalla, la pestaña aún tiene un fondo claro cuando el cliente usa el tema oscuro.</span><span class="sxs-lookup"><span data-stu-id="8577e-142">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="8577e-143">Esta no es una experiencia de usuario recomendada.</span><span class="sxs-lookup"><span data-stu-id="8577e-143">This is not a recommended user experience.</span></span>

<span data-ttu-id="8577e-144">El [SDK del cliente de JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) de Teams puede hacer que su aplicación conozca y reaccione a los cambios de tema en el cliente.</span><span class="sxs-lookup"><span data-stu-id="8577e-144">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="8577e-145">Veamos cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="8577e-145">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="8577e-146">Obtener contexto sobre el cliente de Teams</span><span class="sxs-lookup"><span data-stu-id="8577e-146">Get context about the Teams client</span></span>

<span data-ttu-id="8577e-147">En el archivo, hay una llamada que proporciona información sobre, entre otros detalles, el `Tab.js` tema de cliente `microsoftTeams.getContext()` [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) configurado.</span><span class="sxs-lookup"><span data-stu-id="8577e-147">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="8577e-148">Gracias al scaffolding de la aplicación, usa este código tal como está para acceder a la `context` interfaz y sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="8577e-148">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

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

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="8577e-149">Crear un controlador de cambios de tema</span><span class="sxs-lookup"><span data-stu-id="8577e-149">Create a theme change handler</span></span>

<span data-ttu-id="8577e-150">Con las propiedades en mano, la aplicación tiene una comprensión sólida de lo que sucede a su alrededor `context` en Teams.</span><span class="sxs-lookup"><span data-stu-id="8577e-150">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="8577e-151">Pero la aplicación aún no sabe que su apariencia debe reflejar el tema que elija el usuario.</span><span class="sxs-lookup"><span data-stu-id="8577e-151">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="8577e-152">Necesitas un controlador para que el estado de la aplicación cambie con el tema.</span><span class="sxs-lookup"><span data-stu-id="8577e-152">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="8577e-153">Inserte el siguiente controlador de cambios de tema inmediatamente después de la `microsoftTeams.getContext()` llamada.</span><span class="sxs-lookup"><span data-stu-id="8577e-153">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="8577e-154">Coincidencia de estilos de tema</span><span class="sxs-lookup"><span data-stu-id="8577e-154">Match theme styles</span></span>

<span data-ttu-id="8577e-155">El controlador de cambios de tema está en su lugar, pero necesitas código que responda a esos cambios y alinee los colores de la pestaña con el tema actual.</span><span class="sxs-lookup"><span data-stu-id="8577e-155">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="8577e-156">El siguiente ejemplo es solo una forma de aplicar estilos a la pestaña. Use el código tal como está, expándalo o escriba el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="8577e-156">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="8577e-157">En la `render()` función, almacene el estado proporcionado por el controlador de cambios de tema en `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="8577e-157">In the `render()` function, store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="8577e-158">Después de almacenar el estado proporcionado por el controlador de cambios de tema, proporciona lógica condicional para representar los estilos de la pestaña en función del tema actual.</span><span class="sxs-lookup"><span data-stu-id="8577e-158">After storing the state provided by the theme change handler, provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="8577e-159">En el siguiente ejemplo se muestra una forma básica de hacerlo:</span><span class="sxs-lookup"><span data-stu-id="8577e-159">The following example shows a basic way to do this:</span></span>
1. <span data-ttu-id="8577e-160">Compruebe el tema actual en `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="8577e-160">Check the current theme in `isTheme`.</span></span>
2. <span data-ttu-id="8577e-161">Cree un `newTheme` objeto con propiedades CSS relevantes para el tema actual.</span><span class="sxs-lookup"><span data-stu-id="8577e-161">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
3. <span data-ttu-id="8577e-162">Aplicar el CSS al elemento HTML raíz del contenido de la pestaña ( `<div style={newTheme}>` ).</span><span class="sxs-lookup"><span data-stu-id="8577e-162">Apply the CSS to your tab content's root HTML element (`<div style={newTheme}>`).</span></span>

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

<span data-ttu-id="8577e-163">Compruebe la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="8577e-163">Check your tab in Teams.</span></span> <span data-ttu-id="8577e-164">La apariencia debe coincidir estrechamente con el tema oscuro.</span><span class="sxs-lookup"><span data-stu-id="8577e-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Captura de pantalla de una pestaña personal con vista de contenido estático.":::

## <a name="well-done"></a><span data-ttu-id="8577e-166">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="8577e-166">Well done</span></span>

<span data-ttu-id="8577e-167">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="8577e-167">Congratulations!</span></span> <span data-ttu-id="8577e-168">Tiene una aplicación de Teams con una pestaña personal que facilita la búsqueda de contactos importantes en su organización.</span><span class="sxs-lookup"><span data-stu-id="8577e-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="8577e-169">Más información</span><span class="sxs-lookup"><span data-stu-id="8577e-169">Learn more</span></span>

* <span data-ttu-id="8577e-170">Sigue nuestras [directrices de diseño](../tabs/design/tabs.md) y compila con [plantillas de interfaz](../concepts/design/design-teams-app-ui-templates.md) de usuario listas para producción para crear una experiencia sin problemas.</span><span class="sxs-lookup"><span data-stu-id="8577e-170">Follow our [design guidelines](../tabs/design/tabs.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* <span data-ttu-id="8577e-171">Comprenda [las consideraciones móviles para](../tabs/design/tabs-mobile.md) las pestañas.</span><span class="sxs-lookup"><span data-stu-id="8577e-171">Understand [mobile considerations](../tabs/design/tabs-mobile.md) for tabs.</span></span>
* <span data-ttu-id="8577e-172">[Agregue la autenticación SSO a la pestaña.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="8577e-172">[Add SSO authentication to your tab](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>
* <span data-ttu-id="8577e-173">Use los datos de Teams [con Microsoft Graph.](https://docs.microsoft.com/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="8577e-173">Utilize Teams data with [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>
* <span data-ttu-id="8577e-174">[Crea una pestaña sin el kit de herramientas.](../tabs/quickstarts/create-personal-tab-node-yeoman.md)</span><span class="sxs-lookup"><span data-stu-id="8577e-174">[Create a tab without the toolkit](../tabs/quickstarts/create-personal-tab-node-yeoman.md).</span></span>

## <a name="next-lesson"></a><span data-ttu-id="8577e-175">Siguiente lección</span><span class="sxs-lookup"><span data-stu-id="8577e-175">Next lesson</span></span>

<span data-ttu-id="8577e-176">Sabe cómo crear una pestaña para uso personal.</span><span class="sxs-lookup"><span data-stu-id="8577e-176">You know how to build a tab for personal use.</span></span> <span data-ttu-id="8577e-177">Veamos lo que se necesita para crear una pestaña para canales de equipo y chats.</span><span class="sxs-lookup"><span data-stu-id="8577e-177">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8577e-178">Crear una pestaña de canal</span><span class="sxs-lookup"><span data-stu-id="8577e-178">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
