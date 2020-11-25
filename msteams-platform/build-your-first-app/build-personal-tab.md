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
# <a name="build-a-personal-tab-for-microsoft-teams"></a>Crear una pestaña personal para Microsoft Teams

Las pestañas son una forma sencilla de exponer contenido en la aplicación básicamente mediante la inserción de una página web en Teams.

Hay dos tipos de pestañas en Teams. En este tutorial, creará una *pestaña personal* básica, una página de contenido a pantalla completa para usuarios individuales. (Las pestañas personales son lo más cercano a una experiencia de sitio web tradicional en Microsoft Teams).

## <a name="before-you-begin"></a>Antes de empezar

Necesita una pestaña personal de ejecución básica para empezar. Si no tiene uno, vea [crear y ejecutar su aplicación primera aplicación Teams](../build-your-first-app/build-and-run.md).

## <a name="your-assignment"></a>La asignación

Las personas de su organización tienen problemas para encontrar información de contacto básica para funciones importantes (Departamento de soporte, recursos humanos, etc.). Está a cargo de asegurarse de que puede encontrar rápidamente esta información en un solo punto. ¿Cómo lo haría? Por supuesto, una ficha personal de Microsoft Teams.

## <a name="what-youll-learn"></a>Qué aprenderá

> [!div class="checklist"]
>
> * Identificar algunas de las configuraciones de la aplicación y scaffolding relevantes para las pestañas personales
> * Crear contenido de ficha
> * Actualizar el tema de color de una pestaña según las preferencias del usuario

## <a name="1-identify-relevant-app-project-components"></a>1. identificar los componentes relevantes del proyecto de aplicación

Una gran parte de la configuración de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams. Echemos un vistazo a los componentes principales para crear una pestaña personal.

### <a name="app-configurations"></a>Configuraciones de aplicaciones

Puede ver y actualizar las configuraciones de la aplicación mediante App Studio, que se incluye en el kit de herramientas.

Durante la configuración, el kit de herramientas configuró inicialmente la página de contenido de la pestaña, que es donde se muestra el contenido principal. En el kit de herramientas, vaya a **App Studio** y seleccione **pestañas** para ver la configuración.

### <a name="app-scaffolding"></a>Scaffolding de la aplicación

El scaffolding de la aplicación proporciona los componentes para representar la pestaña personal en Teams. Hay muchas cosas con las que puede trabajar, pero por ahora solo necesita centrarse en lo siguiente:

* `Tab.js` archivo en el `src/components` directorio del proyecto. Esto es para representar la página de contenido de la pestaña.
* SDK cliente de JavaScript de Microsoft Teams, que viene precargado en los componentes front-end del proyecto.

## <a name="2-customize-your-tab-content-page"></a>2. personalizar la página de contenido de la pestaña

Compile una lista de contactos importantes en la organización. Copie y actualice el siguiente fragmento de código con información que sea relevante para usted o, por el momento, use el código tal y como está.

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

Vaya al `src/components` Directorio y Abra `Tab.js` . Busque la `render()` función y pegue el contenido dentro de `return()` (como se muestra).

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

Agregue la regla siguiente a para que `App.css` los vínculos de correo electrónico sean más fáciles de leer independientemente del tema que se use.

```CSS
a {
  color: inherit;
}
```

Guarde los cambios. Vaya a la pestaña de la aplicación en Microsoft Teams para ver el nuevo contenido.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Captura de pantalla de una pestaña personal con contenido estático.":::

## <a name="3-update-the-tab-theme"></a>3. actualizar el tema de ficha

Las aplicaciones buenas se sienten nativas para Teams, por lo que es importante la pestaña se combina con el tema de teams que prefieren los usuarios: predeterminado (claro), oscuro o contraste alto. Como puede haber notado en la última captura de pantalla, la pestaña todavía tiene un fondo claro cuando el cliente usa el tema oscuro. Esta no es una experiencia de usuario recomendada.

El [SDK del cliente de JavaScript para Teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) puede hacer que su aplicación conozca y reaccione a los cambios de tema en el cliente. Vamos a examinar cómo hacerlo.

### <a name="get-context-about-the-teams-client"></a>Obtener contexto sobre el cliente de Teams

En el `Tab.js` archivo, hay una `microsoftTeams.getContext()` llamada que proporciona [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) información acerca del tema del cliente configurado, entre otros detalles. Gracias a la técnica scaffolding de la aplicación, use este código tal y como está para obtener acceso a la `context` interfaz y sus propiedades.

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

### <a name="create-a-theme-change-handler"></a>Crear un controlador de cambios de tema

Con las propiedades que hay a `context` mano, la aplicación tiene una sólida comprensión de lo que sucede alrededor de ella en Teams. Pero la aplicación sigue sin saber que su apariencia debería reflejar cualquier tema que elija el usuario.

Necesita un controlador para que el estado de la aplicación cambie con el tema. Inserte el siguiente controlador de cambio de tema inmediatamente después de la `microsoftTeams.getContext()` llamada.

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>Coincidencia de estilos de tema

El controlador de cambios de tema está en su ubicación, pero necesitará algún código que responda a los cambios y alinear los colores de la pestaña con el tema actual.

> [!NOTE]
> El siguiente ejemplo es sólo una forma de aplicar estilos a la ficha. Use el código tal y como está, expándalo o escriba el suyo propio.

Almacene el estado proporcionado por el controlador de cambios de tema en `isTheme` .

```JavaScript
  const isTheme = this.state.theme
```

Proporcionar una lógica condicional para representar los estilos de la ficha basándose en el tema actual. En el siguiente ejemplo se muestra una forma básica de hacerlo en 1) comprobando el tema actual en `isTheme` , 2) crear un `newTheme` objeto con propiedades CSS relevantes para el tema actual y 3 aplicar la CSS al elemento HTML raíz del contenido de la pestaña ( `<div>` ).

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

Compruebe la pestaña en Microsoft Teams. La apariencia debe coincidir exactamente con el tema oscuro.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Captura de pantalla de una pestaña personal con vista de contenido estático.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene una aplicación de Microsoft Teams con una pestaña personal que facilita la búsqueda de contactos importantes en la organización.

## <a name="learn-more"></a>Más información

* [Autenticar usuarios de pestaña con SSO](../tabs/how-to/authentication/auth-aad-sso.md): si solo quiere que los usuarios autorizados vean su pestaña, configure el inicio de sesión único (SSO) a través de Azure Active Directory (ad).
* [Insertar contenido de una aplicación web o página web existente](../tabs/how-to/add-tab.md#tab-requirements): le mostramos cómo crear nuevo contenido para una pestaña personal, pero también puede cargar contenido desde una dirección URL externa.
* [Crear una experiencia sin problemas para su pestaña](../tabs/design/tabs.md): Consulte las directrices recomendadas para diseñar pestañas de Microsoft Teams.
* [Crear pestañas para móviles](../tabs/design/tabs-mobile.md): comprenda cómo desarrollar pestañas para teléfonos y tabletas.
* [Uso de datos de Teams con la API de Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview)
* [Crear una ficha sin el kit de herramientas](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>Lección siguiente

Sabe cómo crear una pestaña para uso personal. Echemos un vistazo a lo que se necesita para crear una pestaña para los canales y chats del equipo.

> [!div class="nextstepaction"]
> [Crear una pestaña de canal](../build-your-first-app/build-channel-tab.md)
