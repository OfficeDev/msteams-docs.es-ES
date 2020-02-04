---
title: Uso de la biblioteca de controles
description: Cómo usar la biblioteca de controles proporcionada por Microsoft Teams App Studio
keywords: Biblioteca de control de App Studio de Teams
ms.openlocfilehash: d817f55bd75216f77375b7848c5c32cbd29304c2
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675831"
---
# <a name="using-the-control-library-in-app-studio"></a><span data-ttu-id="29e47-104">Usar la biblioteca de controles en App Studio</span><span class="sxs-lookup"><span data-stu-id="29e47-104">Using the control library in App Studio</span></span>

<span data-ttu-id="29e47-105">[Microsoft Teams App Studio](~/get-started/get-started-app-studio.md) le proporciona un conjunto de controles que puede usar en sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="29e47-105">[Microsoft Teams App Studio](~/get-started/get-started-app-studio.md) provides you with a set of controls that you can use in your own apps.</span></span> <span data-ttu-id="29e47-106">Estos controles se proporcionan en la pestaña *biblioteca de controles* de App Studio.</span><span class="sxs-lookup"><span data-stu-id="29e47-106">These controls are provided in the *Control Library* tab of App Studio.</span></span>

<span data-ttu-id="29e47-107">Estos controles fueron creados por los diseñadores de Microsoft Teams para simplificar sus propios flujos de trabajo, estandarizar el comportamiento de los controles y dar soporte a los temas predeterminados del equipo.</span><span class="sxs-lookup"><span data-stu-id="29e47-107">These controls were created by the Microsoft Teams designers to streamline their own workflows, standardize control behavior and support Team's default themes.</span></span> <span data-ttu-id="29e47-108">Puede usar esta biblioteca en sus propias aplicaciones para lograr un aspecto unificado.</span><span class="sxs-lookup"><span data-stu-id="29e47-108">You can use this library in your own apps to achieve a unified look and feel.</span></span>

<span data-ttu-id="29e47-109">Entre los controles se incluyen:</span><span class="sxs-lookup"><span data-stu-id="29e47-109">Controls include:</span></span>

* <span data-ttu-id="29e47-110">Botones</span><span class="sxs-lookup"><span data-stu-id="29e47-110">Buttons</span></span>
* <span data-ttu-id="29e47-111">Desplegables</span><span class="sxs-lookup"><span data-stu-id="29e47-111">Dropdowns</span></span>
* <span data-ttu-id="29e47-112">Casillas</span><span class="sxs-lookup"><span data-stu-id="29e47-112">Checkboxes</span></span>
* <span data-ttu-id="29e47-113">Botones de opción</span><span class="sxs-lookup"><span data-stu-id="29e47-113">Radio Buttons</span></span>
* <span data-ttu-id="29e47-114">Alterna</span><span class="sxs-lookup"><span data-stu-id="29e47-114">Toggles</span></span>
* <span data-ttu-id="29e47-115">Áreas de prueba</span><span class="sxs-lookup"><span data-stu-id="29e47-115">Test Areas</span></span>
* <span data-ttu-id="29e47-116">Vínculos</span><span class="sxs-lookup"><span data-stu-id="29e47-116">Links</span></span>
* <span data-ttu-id="29e47-117">Pestañas</span><span class="sxs-lookup"><span data-stu-id="29e47-117">Tabs</span></span>
* <span data-ttu-id="29e47-118">Tablas</span><span class="sxs-lookup"><span data-stu-id="29e47-118">Tables</span></span>
* <span data-ttu-id="29e47-119">Iconos</span><span class="sxs-lookup"><span data-stu-id="29e47-119">Icons</span></span>

## <a name="optionally-use-react-controls"></a><span data-ttu-id="29e47-120">Opcionalmente, usar controles de reAct</span><span class="sxs-lookup"><span data-stu-id="29e47-120">Optionally use React controls</span></span>

<span data-ttu-id="29e47-121">La biblioteca de control completa de Microsoft Teams usa el marco de trabajo de la [interfaz de usuario de reaccionar JavaScript](https://reactjs.org/) , aunque se ha creado para que no esté ligado a un marco de interfaz de usuario específico</span><span class="sxs-lookup"><span data-stu-id="29e47-121">The full Teams control library uses the [React JavaScript UI framework](https://reactjs.org/) however it is built so that it is not tied to a specific UI framework.</span></span> <span data-ttu-id="29e47-122">Hay cuatro paquetes NPM distintos:</span><span class="sxs-lookup"><span data-stu-id="29e47-122">There are four different npm packages:</span></span>

* <span data-ttu-id="29e47-123">**msteams-UI-Styles-Core** Los estilos CSS principales de los componentes de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="29e47-123">**msteams-ui-styles-core** The core CSS styles of UI components.</span></span> <span data-ttu-id="29e47-124">Es independiente de cualquier marco de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="29e47-124">It’s independent of any UI framework.</span></span>
* <span data-ttu-id="29e47-125">**msteams-UI-Icons-Core** El conjunto principal de iconos de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="29e47-125">**msteams-ui-icons-core** The core set of Teams icons.</span></span>
* <span data-ttu-id="29e47-126">**msteams-UI-Components-reAct** La biblioteca de enlaces de reAct.</span><span class="sxs-lookup"><span data-stu-id="29e47-126">**msteams-ui-components-react** The React binding library.</span></span> <span data-ttu-id="29e47-127">Depende de msteams-UI-Styles-Core.</span><span class="sxs-lookup"><span data-stu-id="29e47-127">It depends on msteams-ui-styles-core.</span></span>
* <span data-ttu-id="29e47-128">**msteams-UI-Icons-reAct** La biblioteca de enlaces de reAct para el conjunto de iconos de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="29e47-128">**msteams-ui-icons-react** The React binding library for the set of Teams icons.</span></span> <span data-ttu-id="29e47-129">Depende de msteams-UI-Icons-Core.</span><span class="sxs-lookup"><span data-stu-id="29e47-129">It depends on msteams-ui-icons-core.</span></span>

<span data-ttu-id="29e47-130">Estas bibliotecas son todas de origen abierto y puede usar msteams-UI-Styles-Core y msteams-UI-Icons-Core sin reAct.</span><span class="sxs-lookup"><span data-stu-id="29e47-130">These libraries are all open source, and you can use msteams-ui-styles-core and msteams-ui-icons-core without React.</span></span>

## <a name="adding-the-control-library"></a><span data-ttu-id="29e47-131">Adición de la biblioteca de controles</span><span class="sxs-lookup"><span data-stu-id="29e47-131">Adding the control library</span></span>

<span data-ttu-id="29e47-132">Instale la biblioteca de controles y su dependencia `typestyle`del mismo nivel:</span><span class="sxs-lookup"><span data-stu-id="29e47-132">Install the control library and its peer dependency `typestyle`:</span></span>

```terminal
npm install --save typestyle && npm install --save msteams-ui-components-react
```

<span data-ttu-id="29e47-133">*Opcional:* Instale los iconos de Teams.</span><span class="sxs-lookup"><span data-stu-id="29e47-133">*Optional:* Install the Teams icons.</span></span>

```terminal
npm install --save msteams-ui-icons-react
```

<span data-ttu-id="29e47-134">Busque y Abra `src/App.js` y reemplace su contenido por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="29e47-134">Find and open `src/App.js` and replace its content with following code:</span></span>

```javascript
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, PrimaryButton } from ‘msteams-ui-components-react’

class App extends Component {
   render() {
      // Sets up the top-level context for the library. It accepts global
      // configurations such as font size and theme. fontSize is your page’s
      // default font size. We made it a parameter so that you could use this
      // library with CSS frameworks such as Bootstrap. Some CSS frameworks
      // set the default font size for the page; retrieve it and use it
      // instead of {16} in the block.
      // This library uses the power of CSS to do most of the work for you.
      // Instead of passing themes as a parameter to every UI component,
      // we set it on a parent HTML element. All HTML elements nested within
      // that parent will inherit these properties.

      return (
        <TeamsComponentContext
            fontSize={16}
            theme={ThemeStyle.Light}
        />
      );
   }
}
export default App;
```

<span data-ttu-id="29e47-135">Ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="29e47-135">Run the app</span></span>

```terminal
npm run start
```

<span data-ttu-id="29e47-136">Cuando navegue a http://localhost:3000, debería ver la pantalla siguiente:</span><span class="sxs-lookup"><span data-stu-id="29e47-136">When you navigate to http://localhost:3000, you should see the following screen:</span></span>

<img width="530px" src="~/assets/images/get-started/control-library-button.png" title="Botón biblioteca de controles"/>

## <a name="dynamically-handling-theme-changes"></a><span data-ttu-id="29e47-138">Controlar dinámicamente los cambios de tema</span><span class="sxs-lookup"><span data-stu-id="29e47-138">Dynamically handling theme changes</span></span>

<span data-ttu-id="29e47-139">La aplicación debe controlar los temas cuando:</span><span class="sxs-lookup"><span data-stu-id="29e47-139">Your app needs to handle themes when:</span></span>

* <span data-ttu-id="29e47-140">La pestaña se carga inicialmente</span><span class="sxs-lookup"><span data-stu-id="29e47-140">The tab is initially loaded</span></span>
* <span data-ttu-id="29e47-141">Un usuario cambia el tema después de que la pestaña ya esté cargada</span><span class="sxs-lookup"><span data-stu-id="29e47-141">A user changes the theme after the tab is already loaded</span></span>

<span data-ttu-id="29e47-142">El tema se incluye en el [contexto](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest)de una pestaña, que se puede recuperar antes de que se cargue la pestaña a través de valores de marcador de posición de dirección URL o en cualquier momento mediante el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/%40microsoft/teams-js/context).</span><span class="sxs-lookup"><span data-stu-id="29e47-142">The theme is included in a tab’s [Context](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest), which can be retrieved before the tab is loaded via URL placeholder values, or at any time by using the [Microsoft Teams JavaScript client SDK](/javascript/api/%40microsoft/teams-js/context).</span></span>

<span data-ttu-id="29e47-143">Aquí se describe cómo se recupera el tema actual y cómo responder a los cambios en el tema: [obtener contexto para la pestaña de Microsoft Teams](~/concepts/tabs/tabs-context.md).</span><span class="sxs-lookup"><span data-stu-id="29e47-143">How the current theme is retrieved and how to respond to theme changes is discussed here: [Get context for your Microsoft Teams tab](~/concepts/tabs/tabs-context.md).</span></span>

<span data-ttu-id="29e47-144">En este código de ejemplo se muestra cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="29e47-144">This sample code shows how this is done.</span></span>

```js
componentWillMount() {
    // If you are deploying your site as a MS Teams static or configurable tab,
    // you should add “?theme={theme}” to your tabs URL in the manifest.
    // That way you will get the current theme before it’s loaded; getContext()
    // is called only after the tab is loaded, which will cause the tab to flash
    // if the current theme is different than the default.
    this.updateTheme(this.getQueryVariable('theme'));
    this.setState({
        fontSize: this.pageFontSize(),
    });

    // If you are not using the MS Teams Javascript SDK, you can remove this entire
    // if block, but if you want theme changes in the MS Teams client to propagate
    // to the tab, leave it here.
    microsoftTeams.initialize();
    microsoftTeams.registerOnThemeChangeHandler(this.updateTheme);
}
```

## <a name="connect-your-own-component-to-the-teamscomponentcontext"></a><span data-ttu-id="29e47-145">Conectar su propio componente al TeamsComponentContext</span><span class="sxs-lookup"><span data-stu-id="29e47-145">Connect your own component to the TeamsComponentContext</span></span>

<span data-ttu-id="29e47-146">Si desea usar su propio código CSS, puede seguir respondiendo a los cambios de tema y usar colores definidos por Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="29e47-146">If you want to use your own CSS code you can still respond to theme changes and use colors defined by teams.</span></span> <span data-ttu-id="29e47-147">TeamsComponentContext permite hacer esto.</span><span class="sxs-lookup"><span data-stu-id="29e47-147">TeamsComponentContext allows you to do this.</span></span>

<span data-ttu-id="29e47-148">Una vez más, edite el archivo y reemplace el contenido por el `src/App.js` siguiente código:</span><span class="sxs-lookup"><span data-stu-id="29e47-148">Once again, edit your `src/App.js` file and replace its content with following code:</span></span>

```javascript
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, ConnectedComponent } from ‘msteams-ui-components-react’

class App extends Component {
    render() {
        return (
            <TeamsComponentContext
                fontSize={16}
                theme={ThemeStyle.HighContrast}>
                <MyComponent />
            </TeamsComponentContext>
        );
    }
}

class MyComponent extends Component {
    render() {
        return (
            <ConnectedComponent render={(props) => {
                const context = props.context;

                switch (context.style) {
                case ThemeStyle.Dark:
                    return <div style={{ color: context.colors.dark.brand00 }}>Dark theme!</div>;
                case ThemeStyle.HighContrast:
                    return <div style={{ color: context.colors.highContrast.black }}>High Contrast theme!</div>;
                case ThemeStyle.Light:
                    return <div style={{ color: context.colors.light.brand00 }}>Light theme!</div>;
                }
            }} />
        );
    }
}

export default App;
```

<span data-ttu-id="29e47-149">En este código, se define un nuevo componente denominado componente.</span><span class="sxs-lookup"><span data-stu-id="29e47-149">In this code, a new component is defined called MyComponent.</span></span> <span data-ttu-id="29e47-150">A continuación, se agrega un componente especial de la biblioteca de controles denominado ConnectedComponent.</span><span class="sxs-lookup"><span data-stu-id="29e47-150">Then a special component from the control library called ConnectedComponent is added.</span></span> <span data-ttu-id="29e47-151">ConnectedComponent tiene una propiedad llamada `render` que toma una función como parámetro.</span><span class="sxs-lookup"><span data-stu-id="29e47-151">ConnectedComponent has a property called `render` which takes a function as a parameter.</span></span> <span data-ttu-id="29e47-152">En tiempo de representación, se llamará a esta función con el contexto adecuado para la pestaña. El contexto incluye el tema en el que se está representando la página, así como el objeto de color global que se puede usar para aplicar colores de Microsoft Teams a la ficha. Como puede ver en la `switch` instrucción, se elige el `<div>` adecuado en función del tema.</span><span class="sxs-lookup"><span data-stu-id="29e47-152">At render time this function will be called with the appropriate context for your tab. The context includes the theme that the page is being rendered in as well as the global color object that you can use to apply Teams colors to your tab. As you can see in the `switch` statement, the appropriate `<div>` is chosen based on the theme.</span></span>

<span data-ttu-id="29e47-153">Para cambiar los temas, debemos pasar el TeamsComponentContext en el nivel de raíz a un tema diferente.</span><span class="sxs-lookup"><span data-stu-id="29e47-153">To change themes, we need to pass the root-level TeamsComponentContext a different theme.</span></span> <span data-ttu-id="29e47-154">Cuando cambia un tema, se volverán a representar todos los elementos secundarios ajustados en ConnectedComponent.</span><span class="sxs-lookup"><span data-stu-id="29e47-154">When a theme changes, all the child elements wrapped in ConnectedComponent will be re-rendered.</span></span> <span data-ttu-id="29e47-155">Vea la sección anterior "controlar dinámicamente los cambios de tema".</span><span class="sxs-lookup"><span data-stu-id="29e47-155">See previous section “Dynamically Handle Theme Changes.”</span></span>

<span data-ttu-id="29e47-156">Hay otras formas de conectar el componente a TeamsComponentContext.</span><span class="sxs-lookup"><span data-stu-id="29e47-156">There are other ways to connect your component to TeamsComponentContext.</span></span> <span data-ttu-id="29e47-157">Si está familiarizado con [Redux](https://redux.js.org/basics/usage-with-react), es posible que prefiera el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="29e47-157">If you’re familiar with [Redux](https://redux.js.org/basics/usage-with-react), you may prefer the following pattern:</span></span>

```js
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, connectTeamsComponent } from ‘msteams-ui-components-react’

class App extends Component {
    render() {
        return (
            <TeamsComponentContext
                fontSize={16}
                theme={ThemeStyle.HighContrast}>
                <MyComponent />
            </TeamsComponentContext>
        );
    }
}

class MyComponentInner extends Component {
    render() {
        const context = this.props.context;
        switch (context.style) {
            case ThemeStyle.Dark:
                return <div style={{ color: context.colors.dark.brand00 }}>Dark theme!</div>;
            case ThemeStyle.HighContrast:
                return <div style={{ color: context.colors.highContrast.black }}>High Contrast theme!</div>;
            case ThemeStyle.Light:
                return <div style={{ color: context.colors.light.brand00 }}>Light theme!</div>;
        }
    }
}

const MyComponent = connectTeamsComponent(MyComponentInner);

export default App;
```

<span data-ttu-id="29e47-158">En este método, en lugar de usar ConnectedComponent, se usa la función connectTeamsComponent.</span><span class="sxs-lookup"><span data-stu-id="29e47-158">In this method, instead of using ConnectedComponent, you use the connectTeamsComponent function.</span></span> <span data-ttu-id="29e47-159">La función connectTeamsComponent toma el componente actual y devuelve un nuevo componente con el objeto contextual insertado.</span><span class="sxs-lookup"><span data-stu-id="29e47-159">The connectTeamsComponent function takes your current component and returns a new component with the context object injected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29e47-160">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="29e47-160">Next steps</span></span>

<span data-ttu-id="29e47-161">Vaya a teams App Studio y consulte todos los controles que ofrecemos y el código de ejemplo de cómo usarlos.</span><span class="sxs-lookup"><span data-stu-id="29e47-161">Head to Teams App Studio and check out all the controls we offer and sample code of how to use them.</span></span> <span data-ttu-id="29e47-162">No olvide explorarlos en temas diferentes.</span><span class="sxs-lookup"><span data-stu-id="29e47-162">Don’t forget to explore them in different themes.</span></span>