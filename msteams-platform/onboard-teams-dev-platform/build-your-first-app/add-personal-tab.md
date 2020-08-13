---
title: Crear una pestaña personal para Teams
author: heath-hamilton
description: Obtenga información sobre cómo crear una pestaña personal en su primera aplicación de Microsoft Teams.
ms.topic: tutorial
ms.openlocfilehash: 1c782adce2201550d30d658907d507dc6a1337f3
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652229"
---
# <a name="create-a-personal-tab-for-teams"></a><span data-ttu-id="407f4-103">Crear una pestaña personal para Teams</span><span class="sxs-lookup"><span data-stu-id="407f4-103">Create a personal tab for Teams</span></span>

<span data-ttu-id="407f4-104">Las pestañas son una forma sencilla de exponer contenido en la aplicación básicamente mediante la inserción de una página web en Teams.</span><span class="sxs-lookup"><span data-stu-id="407f4-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="407f4-105">Hay dos tipos de pestañas en Teams.</span><span class="sxs-lookup"><span data-stu-id="407f4-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="407f4-106">En este tutorial, creará una *pestaña personal*básica, una página de contenido a pantalla completa para usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="407f4-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="407f4-107">(Las pestañas personales son lo más cercano a una experiencia de sitio web tradicional en Microsoft Teams).</span><span class="sxs-lookup"><span data-stu-id="407f4-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="407f4-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="407f4-108">Before you begin</span></span>

<span data-ttu-id="407f4-109">Necesita una aplicación básica que se ejecute para empezar.</span><span class="sxs-lookup"><span data-stu-id="407f4-109">You need a basic running app to get started.</span></span> <span data-ttu-id="407f4-110">Si no tiene uno, vea [crear y ejecutar su aplicación primera aplicación Teams](build-and-run-with-toolkit.md).</span><span class="sxs-lookup"><span data-stu-id="407f4-110">If you don't have one, see [build and run your first Teams app](build-and-run-with-toolkit.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="407f4-111">La asignación</span><span class="sxs-lookup"><span data-stu-id="407f4-111">Your assignment</span></span>

<span data-ttu-id="407f4-112">Las personas de su organización tienen problemas para encontrar información de contacto básica para funciones importantes (Departamento de soporte, recursos humanos, etc.).</span><span class="sxs-lookup"><span data-stu-id="407f4-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="407f4-113">Está a cargo de asegurarse de que puede encontrar rápidamente esta información en un solo punto.</span><span class="sxs-lookup"><span data-stu-id="407f4-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="407f4-114">¿Cómo lo haría?</span><span class="sxs-lookup"><span data-stu-id="407f4-114">How would you do that?</span></span> <span data-ttu-id="407f4-115">Por supuesto, una ficha personal de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="407f4-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="407f4-116">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="407f4-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="407f4-117">Identificar las propiedades del manifiesto de la aplicación y los scaffolding relevantes para las pestañas personales</span><span class="sxs-lookup"><span data-stu-id="407f4-117">Identify the app manifest properties and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="407f4-118">Crear contenido para la pestaña</span><span class="sxs-lookup"><span data-stu-id="407f4-118">Create content for your tab</span></span>
> * <span data-ttu-id="407f4-119">Actualizar el tema de color de la pestaña según las preferencias del usuario</span><span class="sxs-lookup"><span data-stu-id="407f4-119">Update your tab's color theme based on user preference</span></span>

## <a name="identify-relevant-app-manifest-and-scaffolding-components"></a><span data-ttu-id="407f4-120">Identificar los componentes relevantes del manifiesto de la aplicación y los componentes de scaffolding</span><span class="sxs-lookup"><span data-stu-id="407f4-120">Identify relevant app manifest and scaffolding components</span></span>

<span data-ttu-id="407f4-121">Gran parte del manifiesto y el uso de scaffolding de la aplicación de pestaña personal se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="407f4-121">Much of the personal tab app scaffolding and manifest is set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="407f4-122">Echemos un vistazo a los componentes principales para crear una pestaña personal.</span><span class="sxs-lookup"><span data-stu-id="407f4-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="407f4-123">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="407f4-123">App manifest</span></span>

<span data-ttu-id="407f4-124">El siguiente fragmento de código del manifiesto de la aplicación (el `manifest.json` archivo del `.publish` directorio del proyecto) muestra [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs) , que incluye las propiedades y los valores predeterminados relacionados con las pestañas personales.</span><span class="sxs-lookup"><span data-stu-id="407f4-124">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs), which includes properties and default values relevant to personal tabs.</span></span>

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

* <span data-ttu-id="407f4-125">`entityId`: Un identificador único para la página que se muestra en la pestaña.</span><span class="sxs-lookup"><span data-stu-id="407f4-125">`entityId`: A unique identifier for the page displayed by the tab.</span></span>
* <span data-ttu-id="407f4-126">`name`: El nombre para mostrar de la ficha (por ejemplo, "mis contactos").</span><span class="sxs-lookup"><span data-stu-id="407f4-126">`name`: The tab's display name (for example, "My Contacts").</span></span>
* <span data-ttu-id="407f4-127">`contentUrl`: La dirección URL del host la página de contenido de la ficha (debe ser HTTPS).</span><span class="sxs-lookup"><span data-stu-id="407f4-127">`contentUrl`: The host URL the tab content page (must be HTTPS).</span></span>
* <span data-ttu-id="407f4-128">`scopes`: Especifica que la pestaña es solo para uso personal.</span><span class="sxs-lookup"><span data-stu-id="407f4-128">`scopes`: Specifies the tab is for personal use only.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="407f4-129">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="407f4-129">App scaffolding</span></span>

<span data-ttu-id="407f4-130">El scaffolding de la aplicación proporciona los componentes para representar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="407f4-130">The app scaffolding provides the components for rendering your tab in Teams.</span></span> <span data-ttu-id="407f4-131">Hay muchas cosas con las que puede trabajar, pero por ahora solo necesita centrarse en lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="407f4-131">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="407f4-132">`Tab.js` archivo en el `src/components` directorio del proyecto</span><span class="sxs-lookup"><span data-stu-id="407f4-132">`Tab.js` file in the `src/components` directory of your project</span></span>
* <span data-ttu-id="407f4-133">SDK para cliente de JavaScript de Microsoft Teams, que viene previamente cargado en los componentes front-end del proyecto</span><span class="sxs-lookup"><span data-stu-id="407f4-133">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components</span></span>

## <a name="create-your-tab-content"></a><span data-ttu-id="407f4-134">Crear el contenido de la pestaña</span><span class="sxs-lookup"><span data-stu-id="407f4-134">Create your tab content</span></span>

<span data-ttu-id="407f4-135">Compile una lista de contactos importantes en la organización.</span><span class="sxs-lookup"><span data-stu-id="407f4-135">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="407f4-136">Copie y actualice el siguiente fragmento de código con información que sea relevante para usted o, por el momento, use el código tal y como está.</span><span class="sxs-lookup"><span data-stu-id="407f4-136">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="407f4-137">Vaya al `src/components` Directorio y Abra `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="407f4-137">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="407f4-138">Busque la `render()` función y pegue el contenido dentro de `return()` (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="407f4-138">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="407f4-139">Agregue la regla siguiente a para que `App.css` los vínculos de correo electrónico sean más fáciles de leer independientemente del tema que se use.</span><span class="sxs-lookup"><span data-stu-id="407f4-139">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
  a {
    color: inherit;
  }
```

<span data-ttu-id="407f4-140">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="407f4-140">Save your changes.</span></span> <span data-ttu-id="407f4-141">Vaya a la pestaña de la aplicación en Microsoft Teams para ver el nuevo contenido.</span><span class="sxs-lookup"><span data-stu-id="407f4-141">Go to your app's tab in Teams to view the new content.</span></span>

![Captura de pantalla de ejemplo de una pestaña personal con contenido estático](../doc-links/images/personal-tab-tutorial-content.png)

## <a name="update-the-tab-theme"></a><span data-ttu-id="407f4-143">Actualizar el tema de pestaña</span><span class="sxs-lookup"><span data-stu-id="407f4-143">Update the tab theme</span></span>

<span data-ttu-id="407f4-144">Las aplicaciones buenas se sienten nativas para Teams, por lo que es importante la pestaña se combina con el tema de teams que prefieren los usuarios: predeterminado (claro), oscuro o contraste alto.</span><span class="sxs-lookup"><span data-stu-id="407f4-144">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="407f4-145">Como puede haber notado en la última captura de pantalla, la pestaña todavía tiene un fondo claro cuando el cliente usa el tema oscuro.</span><span class="sxs-lookup"><span data-stu-id="407f4-145">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="407f4-146">Esta no es una experiencia de usuario recomendada.</span><span class="sxs-lookup"><span data-stu-id="407f4-146">This is not a recommended user experience.</span></span>

<span data-ttu-id="407f4-147">El [SDK del cliente de JavaScript para Teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest) puede hacer que su aplicación conozca y reaccione a los cambios de tema en el cliente.</span><span class="sxs-lookup"><span data-stu-id="407f4-147">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="407f4-148">Vamos a examinar cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="407f4-148">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="407f4-149">Obtener contexto sobre el cliente de Teams</span><span class="sxs-lookup"><span data-stu-id="407f4-149">Get context about the Teams client</span></span>

<span data-ttu-id="407f4-150">En el `Tab.js` archivo, hay una `microsoftTeams.getContext()` llamada que proporciona [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) información acerca del tema del cliente configurado, entre otros detalles.</span><span class="sxs-lookup"><span data-stu-id="407f4-150">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) about, among other details, the configured client theme.</span></span> <span data-ttu-id="407f4-151">Gracias a la técnica scaffolding de la aplicación, use este código tal y como está para obtener acceso a la `context` interfaz y sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="407f4-151">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

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

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="407f4-152">Crear un controlador de cambios de tema</span><span class="sxs-lookup"><span data-stu-id="407f4-152">Create a theme change handler</span></span>

<span data-ttu-id="407f4-153">Con las propiedades que hay a `context` mano, la aplicación tiene una sólida comprensión de lo que sucede alrededor de ella en Teams.</span><span class="sxs-lookup"><span data-stu-id="407f4-153">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="407f4-154">Pero la aplicación sigue sin saber que su apariencia debería reflejar cualquier tema que elija el usuario.</span><span class="sxs-lookup"><span data-stu-id="407f4-154">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="407f4-155">Necesita un controlador para que el estado de la aplicación cambie con el tema.</span><span class="sxs-lookup"><span data-stu-id="407f4-155">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="407f4-156">Inserte el siguiente controlador de cambio de tema inmediatamente después de la `microsoftTeams.getContext()` llamada.</span><span class="sxs-lookup"><span data-stu-id="407f4-156">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="407f4-157">Coincidencia de estilos de tema</span><span class="sxs-lookup"><span data-stu-id="407f4-157">Match theme styles</span></span>

<span data-ttu-id="407f4-158">El controlador de cambios de tema está en su ubicación, pero necesitará algún código que responda a los cambios y alinear los colores de la pestaña con el tema actual.</span><span class="sxs-lookup"><span data-stu-id="407f4-158">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="407f4-159">El siguiente ejemplo es sólo una forma de aplicar estilos a la ficha. Use el código tal y como está, expándalo o escriba el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="407f4-159">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="407f4-160">Almacene el estado proporcionado por el controlador de cambios de tema en `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="407f4-160">Store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="407f4-161">Proporcionar una lógica condicional para representar los estilos de la ficha basándose en el tema actual.</span><span class="sxs-lookup"><span data-stu-id="407f4-161">Provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="407f4-162">En el siguiente ejemplo se muestra una forma básica de hacerlo en 1) comprobando el tema actual en `isTheme` , 2) crear un `newTheme` objeto con propiedades CSS relevantes para el tema actual y 3 aplicar la CSS al elemento HTML raíz del contenido de la pestaña ( `<div>` ).</span><span class="sxs-lookup"><span data-stu-id="407f4-162">The following example shows a basic way to do this by 1) checking the current theme in `isTheme`, 2) creating a `newTheme` object with CSS properties relevant to the current theme, and 3) applying the CSS to your tab content's root HTML element (`<div>`).</span></span>

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

<span data-ttu-id="407f4-163">Compruebe la pestaña en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="407f4-163">Check your tab in Teams.</span></span> <span data-ttu-id="407f4-164">La apariencia debe coincidir exactamente con el tema oscuro.</span><span class="sxs-lookup"><span data-stu-id="407f4-164">The appearance should closely match the dark theme.</span></span>

![Captura de pantalla de ejemplo de una pestaña personal con contenido estático](../doc-links/images/personal-tab-tutorial-updated-theme.png)

## <a name="well-done"></a><span data-ttu-id="407f4-166">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="407f4-166">Well done</span></span>

<span data-ttu-id="407f4-167">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="407f4-167">Congratulations!</span></span> <span data-ttu-id="407f4-168">Tiene una aplicación de Microsoft Teams con una pestaña personal que facilita la búsqueda de contactos importantes en la organización.</span><span class="sxs-lookup"><span data-stu-id="407f4-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="next-step"></a><span data-ttu-id="407f4-169">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="407f4-169">Next step</span></span>

<span data-ttu-id="407f4-170">Sabe cómo crear una pestaña para uso personal.</span><span class="sxs-lookup"><span data-stu-id="407f4-170">You know how to build a tab for personal use.</span></span> <span data-ttu-id="407f4-171">Echemos un vistazo a lo que se necesita para crear una pestaña para los canales y chats del equipo.</span><span class="sxs-lookup"><span data-stu-id="407f4-171">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="407f4-172">Crear una ficha de canal</span><span class="sxs-lookup"><span data-stu-id="407f4-172">Build a channel tab</span></span>](add-channel-tab.md)

## <a name="learn-more"></a><span data-ttu-id="407f4-173">Más información</span><span class="sxs-lookup"><span data-stu-id="407f4-173">Learn more</span></span>

* <span data-ttu-id="407f4-174">[Autenticar usuarios de pestaña con SSO](../../tabs/how-to/authentication/auth-aad-sso.md): si solo quiere que los usuarios autorizados vean su pestaña, configure el inicio de sesión único (SSO) a través de Azure Active Directory (ad).</span><span class="sxs-lookup"><span data-stu-id="407f4-174">[Authenticate tab users with SSO](../../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="407f4-175">[Insertar contenido de una aplicación web o página web existente](../../tabs/how-to/add-tab.md#tab-requirements): le mostramos cómo crear nuevo contenido para una pestaña personal, pero también puede cargar contenido desde una dirección URL externa.</span><span class="sxs-lookup"><span data-stu-id="407f4-175">[Embed content from an existing web app or webpage](../../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="407f4-176">[Crear una experiencia sin problemas para su pestaña](../../tabs/design/tabs.md): Consulte las directrices recomendadas para diseñar pestañas de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="407f4-176">[Create a seamless experience for your tab](../../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="407f4-177">[Crear pestañas para dispositivos móviles](../../tabs/design/tabs-mobile.md): comprenda cómo desarrollar pestañas para smartphones y tabletas.</span><span class="sxs-lookup"><span data-stu-id="407f4-177">[Build tabs for mobile](../../tabs/design/tabs-mobile.md): Understand how to develop tabs for smartphones and tablets.</span></span>

