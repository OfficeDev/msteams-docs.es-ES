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
# <a name="using-the-control-library-in-app-studio"></a>Usar la biblioteca de controles en App Studio

[Microsoft Teams App Studio](~/get-started/get-started-app-studio.md) le proporciona un conjunto de controles que puede usar en sus propias aplicaciones. Estos controles se proporcionan en la pestaña *biblioteca de controles* de App Studio.

Estos controles fueron creados por los diseñadores de Microsoft Teams para simplificar sus propios flujos de trabajo, estandarizar el comportamiento de los controles y dar soporte a los temas predeterminados del equipo. Puede usar esta biblioteca en sus propias aplicaciones para lograr un aspecto unificado.

Entre los controles se incluyen:

* Botones
* Desplegables
* Casillas
* Botones de opción
* Alterna
* Áreas de prueba
* Vínculos
* Pestañas
* Tablas
* Iconos

## <a name="optionally-use-react-controls"></a>Opcionalmente, usar controles de reAct

La biblioteca de control completa de Microsoft Teams usa el marco de trabajo de la [interfaz de usuario de reaccionar JavaScript](https://reactjs.org/) , aunque se ha creado para que no esté ligado a un marco de interfaz de usuario específico Hay cuatro paquetes NPM distintos:

* **msteams-UI-Styles-Core** Los estilos CSS principales de los componentes de la interfaz de usuario. Es independiente de cualquier marco de interfaz de usuario.
* **msteams-UI-Icons-Core** El conjunto principal de iconos de Microsoft Teams.
* **msteams-UI-Components-reAct** La biblioteca de enlaces de reAct. Depende de msteams-UI-Styles-Core.
* **msteams-UI-Icons-reAct** La biblioteca de enlaces de reAct para el conjunto de iconos de Microsoft Teams. Depende de msteams-UI-Icons-Core.

Estas bibliotecas son todas de origen abierto y puede usar msteams-UI-Styles-Core y msteams-UI-Icons-Core sin reAct.

## <a name="adding-the-control-library"></a>Adición de la biblioteca de controles

Instale la biblioteca de controles y su dependencia `typestyle`del mismo nivel:

```terminal
npm install --save typestyle && npm install --save msteams-ui-components-react
```

*Opcional:* Instale los iconos de Teams.

```terminal
npm install --save msteams-ui-icons-react
```

Busque y Abra `src/App.js` y reemplace su contenido por el código siguiente:

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

Ejecutar la aplicación

```terminal
npm run start
```

Cuando navegue a http://localhost:3000, debería ver la pantalla siguiente:

<img width="530px" src="~/assets/images/get-started/control-library-button.png" title="Botón biblioteca de controles"/>

## <a name="dynamically-handling-theme-changes"></a>Controlar dinámicamente los cambios de tema

La aplicación debe controlar los temas cuando:

* La pestaña se carga inicialmente
* Un usuario cambia el tema después de que la pestaña ya esté cargada

El tema se incluye en el [contexto](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest)de una pestaña, que se puede recuperar antes de que se cargue la pestaña a través de valores de marcador de posición de dirección URL o en cualquier momento mediante el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/%40microsoft/teams-js/context).

Aquí se describe cómo se recupera el tema actual y cómo responder a los cambios en el tema: [obtener contexto para la pestaña de Microsoft Teams](~/concepts/tabs/tabs-context.md).

En este código de ejemplo se muestra cómo hacerlo.

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

## <a name="connect-your-own-component-to-the-teamscomponentcontext"></a>Conectar su propio componente al TeamsComponentContext

Si desea usar su propio código CSS, puede seguir respondiendo a los cambios de tema y usar colores definidos por Microsoft Teams. TeamsComponentContext permite hacer esto.

Una vez más, edite el archivo y reemplace el contenido por el `src/App.js` siguiente código:

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

En este código, se define un nuevo componente denominado componente. A continuación, se agrega un componente especial de la biblioteca de controles denominado ConnectedComponent. ConnectedComponent tiene una propiedad llamada `render` que toma una función como parámetro. En tiempo de representación, se llamará a esta función con el contexto adecuado para la pestaña. El contexto incluye el tema en el que se está representando la página, así como el objeto de color global que se puede usar para aplicar colores de Microsoft Teams a la ficha. Como puede ver en la `switch` instrucción, se elige el `<div>` adecuado en función del tema.

Para cambiar los temas, debemos pasar el TeamsComponentContext en el nivel de raíz a un tema diferente. Cuando cambia un tema, se volverán a representar todos los elementos secundarios ajustados en ConnectedComponent. Vea la sección anterior "controlar dinámicamente los cambios de tema".

Hay otras formas de conectar el componente a TeamsComponentContext. Si está familiarizado con [Redux](https://redux.js.org/basics/usage-with-react), es posible que prefiera el siguiente patrón:

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

En este método, en lugar de usar ConnectedComponent, se usa la función connectTeamsComponent. La función connectTeamsComponent toma el componente actual y devuelve un nuevo componente con el objeto contextual insertado.

## <a name="next-steps"></a>Siguientes pasos

Vaya a teams App Studio y consulte todos los controles que ofrecemos y el código de ejemplo de cómo usarlos. No olvide explorarlos en temas diferentes.