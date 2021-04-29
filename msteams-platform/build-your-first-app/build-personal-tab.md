---
title: 'Introducción: crear una pestaña personal'
author: girliemac
description: Cree rápidamente una pestaña personal de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: timura
ms.date: 03/16/2020
ms.topic: tutorial
ms.openlocfilehash: 05ef9913e338a54c7e6ebc301825b27d4bec9705
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068588"
---
# <a name="build-a-basic-personal-tab-for-microsoft-teams"></a><span data-ttu-id="840bc-103">Crear una pestaña personal básica para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="840bc-103">Build a basic personal tab for Microsoft Teams</span></span>

<span data-ttu-id="840bc-104">Este tutorial le enseña a crear una pestaña personal básica en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="840bc-104">This tutorial teaches you to build a basic personal tab in Microsoft Teams.</span></span> <span data-ttu-id="840bc-105">Las pestañas son una forma sencilla de presentar información en la aplicación hospedando contenido web en Teams.</span><span class="sxs-lookup"><span data-stu-id="840bc-105">Tabs are a simple way to surface information in your app by hosting web content in Teams.</span></span> <span data-ttu-id="840bc-106">Las pestañas son una característica común de las aplicaciones personales que proporcionan un área de trabajo privada para usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="840bc-106">Tabs are a common feature of personal apps that provide a private workspace for individual users.</span></span> <span data-ttu-id="840bc-107">Las pestañas personales son lo más cercano a una experiencia web tradicional en Teams.</span><span class="sxs-lookup"><span data-stu-id="840bc-107">Personal tabs are the closest thing to a traditional web experience in Teams.</span></span> 

## <a name="what-youll-learn"></a><span data-ttu-id="840bc-108">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="840bc-108">What you'll learn</span></span>

* <span data-ttu-id="840bc-109">Comprenda las configuraciones de la aplicación y los scaffolding relevantes para las pestañas personales.</span><span class="sxs-lookup"><span data-stu-id="840bc-109">Understand the app configurations and scaffolding relevant to personal tabs.</span></span>
* <span data-ttu-id="840bc-110">Cree un contenido de pestaña con una lista de contactos de su organización.</span><span class="sxs-lookup"><span data-stu-id="840bc-110">Create a tab content with a contact list of your organization.</span></span>
* <span data-ttu-id="840bc-111">Actualice el tema de color de una pestaña en función de las preferencias del usuario.</span><span class="sxs-lookup"><span data-stu-id="840bc-111">Update a tab's color theme based on user preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="840bc-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="840bc-112">Prerequisites</span></span>

<span data-ttu-id="840bc-113">Asegúrate de comprender cómo configurar y crear una aplicación sencilla de Teams.</span><span class="sxs-lookup"><span data-stu-id="840bc-113">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="840bc-114">Para obtener más información, consulta crear la primera aplicación de [Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="840bc-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-understand-your-app-project-components"></a><span data-ttu-id="840bc-115">1. Comprender los componentes del proyecto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="840bc-115">1. Understand your app project components</span></span>

<span data-ttu-id="840bc-116">Después de crear una pestaña personal básica, el scaffolding de la aplicación generada proporciona los componentes para representar la pestaña personal en Teams.</span><span class="sxs-lookup"><span data-stu-id="840bc-116">After you have created a basic personal tab, the generated app scaffold provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="840bc-117">Hay mucho con lo que puede trabajar, pero por ahora vamos a centrarnos en lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="840bc-117">There's a lot you can work with, but for now let us focus on the following:</span></span> 

* <span data-ttu-id="840bc-118">`Tab.js` en el `src/components` directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="840bc-118">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="840bc-119">Esto es para representar la página de contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="840bc-119">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="840bc-120">SDK de cliente de JavaScript de Microsoft Teams, que se carga previamente en los componentes front-end del proyecto.</span><span class="sxs-lookup"><span data-stu-id="840bc-120">Microsoft Teams JavaScript client SDK, which is pre-loaded in your project's front-end components.</span></span>

<span data-ttu-id="840bc-121">Como puede observar en la sección de la parte superior del archivo, el código de ejemplo usa React , una biblioteca de JavaScript de código abierto para crear `import` `Tabs.js` la interfaz de usuario. [](https://reactjs.org/)</span><span class="sxs-lookup"><span data-stu-id="840bc-121">As you may notice from the `import` section at the top of `Tabs.js` file, the sample code uses [React](https://reactjs.org/), an open-source JavaScript library for building user-interface.</span></span> 

> [!NOTE]
> <span data-ttu-id="840bc-122">Aunque el uso de React _no es_ necesario para el desarrollo de Teams, este tutorial te enseña con React.</span><span class="sxs-lookup"><span data-stu-id="840bc-122">Although using React is _not_ required for Teams development, this tutorial teaches you with React.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="840bc-123">2. Personalizar la página de contenido de la pestaña</span><span class="sxs-lookup"><span data-stu-id="840bc-123">2. Customize your tab content page</span></span>

<span data-ttu-id="840bc-124">Puede personalizar la página de contenido de la pestaña para representar una lista de contactos importantes de su organización.</span><span class="sxs-lookup"><span data-stu-id="840bc-124">You can customize your tab content page to render a list of important contacts in your organization.</span></span> 

<span data-ttu-id="840bc-125">**Para personalizar la página de contenido de la pestaña**</span><span class="sxs-lookup"><span data-stu-id="840bc-125">**To customize your tab content page**</span></span>

1. <span data-ttu-id="840bc-126">Copie y modifique el siguiente ejemplo de código con información que sea relevante para usted.</span><span class="sxs-lookup"><span data-stu-id="840bc-126">Copy and modify the following code sample with information that's relevant to you.</span></span> <span data-ttu-id="840bc-127">También puede usar el código tal como está:</span><span class="sxs-lookup"><span data-stu-id="840bc-127">You can also use the code as is:</span></span> 
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
1. <span data-ttu-id="840bc-128">Llegó al `src/components` directorio y abra el `Tab.js` archivo.</span><span class="sxs-lookup"><span data-stu-id="840bc-128">Got to the `src/components` directory and open the `Tab.js` file.</span></span> 
1. <span data-ttu-id="840bc-129">Vaya a `render()` y reemplace el código de plantilla por el código modificado `return()` dentro, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="840bc-129">Go to `render()` and replace the template code with the modified code inside `return()` as shown in the following example:</span></span>
    ```JavaScript
    render() {
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
1. <span data-ttu-id="840bc-130">Vaya al directorio y modifique el archivo con el siguiente código para que los vínculos de correo electrónico sean más fáciles de leer `src/components` con cualquier tema que se `App.css` utilice:</span><span class="sxs-lookup"><span data-stu-id="840bc-130">Go to the `src/components` directory and modify the `App.css` file with the following code to make the email links easier to read with any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```
1. <span data-ttu-id="840bc-131">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="840bc-131">Save your changes.</span></span> 

   <span data-ttu-id="840bc-132">Puedes ver el nuevo contenido en la pestaña de la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="840bc-132">You can view the new content in your app's tab in Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-content.png" alt-text="Captura de pantalla de una pestaña personal con contenido estático.":::

## <a name="3-update-your-tab-theme"></a><span data-ttu-id="840bc-134">3. Actualizar el tema de pestaña</span><span class="sxs-lookup"><span data-stu-id="840bc-134">3. Update your tab theme</span></span>

<span data-ttu-id="840bc-135">Es importante que la pestaña tenga un tema que se sienta nativo de Teams.</span><span class="sxs-lookup"><span data-stu-id="840bc-135">It is important for your tab to have a theme that feels native to Teams.</span></span> <span data-ttu-id="840bc-136">Debe combinar la pestaña con el tema Teams.</span><span class="sxs-lookup"><span data-stu-id="840bc-136">You must blend your tab with the Teams theme.</span></span> <span data-ttu-id="840bc-137">Por lo general, los usuarios prefieren los temas predeterminados (claros), oscuros o de contraste alto.</span><span class="sxs-lookup"><span data-stu-id="840bc-137">Your users generally prefer default (light), dark, or high contrast themes.</span></span> <span data-ttu-id="840bc-138">Como podrías haber notado en la última captura de pantalla, la pestaña todavía tiene un fondo claro cuando el usuario usa el tema oscuro.</span><span class="sxs-lookup"><span data-stu-id="840bc-138">As you might have noticed in the last screenshot, your tab still has a light background when your user is using the dark theme.</span></span> <span data-ttu-id="840bc-139">Esta no es una experiencia de usuario recomendada.</span><span class="sxs-lookup"><span data-stu-id="840bc-139">This is not a recommended user experience.</span></span>

<span data-ttu-id="840bc-140">El SDK de cliente de JavaScript de Teams puede hacer que la aplicación conozca y reaccione a los cambios de tema en el cliente.</span><span class="sxs-lookup"><span data-stu-id="840bc-140">The Teams JavaScript client SDK can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="840bc-141">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="840bc-141">To do this, follow these steps:</span></span>

1. <span data-ttu-id="840bc-142">**Obtener contexto sobre el tema de cliente de Teams configurado** La `microsoftTeams.getContext()` llamada en el `Tab.js` archivo, proporciona algún contexto sobre el tema de cliente configurado (como el tema oscuro).</span><span class="sxs-lookup"><span data-stu-id="840bc-142">**Get context about the configured Teams client theme** The `microsoftTeams.getContext()` call in your `Tab.js` file, provides some context about the configured client theme (such as dark theme).</span></span> <span data-ttu-id="840bc-143">El siguiente código tiene acceso a la `context` interfaz y sus propiedades:</span><span class="sxs-lookup"><span data-stu-id="840bc-143">The following code accesses the `context` interface and its properties:</span></span>

    ```JavaScript
    componentDidMount(){
      // Get the user context from Teams and set it in the state
      microsoftTeams.getContext((context, error) => {
        this.setState({
          context: context,
          theme: context.theme
        });
      });
    }
    ```
1. <span data-ttu-id="840bc-144">**Crear un controlador de cambios de tema** Con las propiedades en la mano, la aplicación tiene una comprensión sólida de lo que está sucediendo a su alrededor `context` en Teams.</span><span class="sxs-lookup"><span data-stu-id="840bc-144">**Create a theme change handler** With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="840bc-145">Sin embargo, la aplicación aún no tiene una apariencia que refleje el tema cuando un usuario lo actualiza.</span><span class="sxs-lookup"><span data-stu-id="840bc-145">However, the app still doesn't have an appearance reflecting the theme when a user updates it.</span></span>

   <span data-ttu-id="840bc-146">Necesitas un controlador para actualizar el estado de la aplicación con el tema.</span><span class="sxs-lookup"><span data-stu-id="840bc-146">You need a handler to update your app's state with the theme.</span></span> <span data-ttu-id="840bc-147">Para crear un controlador, inserte el siguiente controlador de cambios de tema inmediatamente después de la `microsoftTeams.getContext()` llamada:</span><span class="sxs-lookup"><span data-stu-id="840bc-147">To create a handler, insert the following theme change handler immediately after the `microsoftTeams.getContext()` call:</span></span>

    ```JavaScript
    microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.context.theme) {
    this.setState({
      context: {
      ...this.state.context,
      theme
      }
      })   
      }
    });
      ```
1. <span data-ttu-id="840bc-148">**Coincidir con los estilos de tema** Sin embargo, el controlador de cambios de tema está en su lugar, pero aún tiene que responder a los cambios y alinear los colores de la pestaña con el tema actual.</span><span class="sxs-lookup"><span data-stu-id="840bc-148">**Match the theme styles** Your theme change handler is in place, however, you still have to respond to changes and align your tab's colors with the current theme.</span></span>

   <span data-ttu-id="840bc-149">En la `render()` función, almacene el estado proporcionado por el controlador de cambios de tema en `isTheme` :</span><span class="sxs-lookup"><span data-stu-id="840bc-149">In the `render()` function, store the state provided by the theme change handler in `isTheme`:</span></span>

    ```JavaScript
      const isTheme = this.state.context.theme
    ```
    
    > [!NOTE]
    > <span data-ttu-id="840bc-150">Este ejemplo es solo una forma de aplicar estilos a la pestaña. Use el código tal como está, expándalo o escriba el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="840bc-150">This example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

    <span data-ttu-id="840bc-151">Después de almacenar el estado proporcionado por el controlador de cambios de tema, proporcione la lógica condicional para representar los estilos de la pestaña en función del tema actual.</span><span class="sxs-lookup"><span data-stu-id="840bc-151">After storing the state provided by the theme change handler, provide the conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="840bc-152">En el ejemplo siguiente se muestra una forma básica de hacerlo:</span><span class="sxs-lookup"><span data-stu-id="840bc-152">The following example shows a basic way to do this:</span></span>

    1. <span data-ttu-id="840bc-153">Vaya a `render()` y compruebe el tema actual en `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="840bc-153">Go to `render()` and check the current theme in `isTheme`.</span></span>
    1. <span data-ttu-id="840bc-154">Cree un `newTheme` objeto con propiedades CSS relevantes para el tema actual.</span><span class="sxs-lookup"><span data-stu-id="840bc-154">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
    1. <span data-ttu-id="840bc-155">Aplique el siguiente CSS al elemento HTML raíz del contenido de la pestaña ( `<div style={newTheme}>` ):</span><span class="sxs-lookup"><span data-stu-id="840bc-155">Apply the following CSS to your tab content's root HTML element (`<div style={newTheme}>`):</span></span>

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

       <span data-ttu-id="840bc-156">Compruebe la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="840bc-156">Check your tab in Teams.</span></span> <span data-ttu-id="840bc-157">La apariencia ahora coincide estrechamente con el tema oscuro.</span><span class="sxs-lookup"><span data-stu-id="840bc-157">The appearance now closely matches the dark theme.</span></span>

       :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-updated-theme.png" alt-text="Captura de pantalla de una pestaña personal con vista de contenido estático.":::

## <a name="see-also"></a><span data-ttu-id="840bc-159">Consulte también</span><span class="sxs-lookup"><span data-stu-id="840bc-159">See also</span></span>

* [<span data-ttu-id="840bc-160">SDK para cliente de JavaScript en Teams</span><span class="sxs-lookup"><span data-stu-id="840bc-160">Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="840bc-161">Diseño de la pestaña para escritorio y web de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="840bc-161">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="840bc-162">Interfaz de contexto</span><span class="sxs-lookup"><span data-stu-id="840bc-162">Context interface</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="840bc-163">Diseño de la aplicación de Microsoft Teams con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="840bc-163">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="840bc-164">Pestañas en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="840bc-164">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="840bc-165">Compatibilidad con inicio de sesión único (SSO) para pestañas</span><span class="sxs-lookup"><span data-stu-id="840bc-165">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="840bc-166">Introducción a la API de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="840bc-166">Microsoft Teams API overview</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="840bc-167">Crear una pestaña personal personalizada con Node.js y el generador de Yeoman para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="840bc-167">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="840bc-168">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="840bc-168">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="840bc-169">Crear una pestaña de canal</span><span class="sxs-lookup"><span data-stu-id="840bc-169">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)