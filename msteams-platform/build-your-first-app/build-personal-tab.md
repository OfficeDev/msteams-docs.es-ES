---
title: 'Introducción: crear una pestaña personal'
author: heath-hamilton
description: Cree rápidamente una pestaña personal de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: 86be39503ec4e4fde5fafe63f83b3a4fb6d956bf
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797809"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a>Crear una pestaña personal para Microsoft Teams

Las pestañas son una forma sencilla de ver el contenido de la aplicación insertando básicamente una página web en Teams.

Hay dos tipos de pestañas en Teams. En este tutorial, compilará una pestaña *personal* básica, una página de contenido de pantalla completa para usuarios individuales. (Las pestañas personales son lo más cercano a una experiencia de sitio web tradicional en Teams).

## <a name="before-you-begin"></a>Antes de empezar

Necesita una pestaña personal básica en ejecución para empezar. Si no tiene uno, consulte [compilar y ejecutar la primera aplicación de Teams.](../build-your-first-app/build-and-run.md)

## <a name="your-assignment"></a>Su asignación

Las personas de su organización tienen problemas para encontrar información de contacto básica para funciones importantes (servicio de soporte, recursos humanos, etc.). Usted es el encargado de asegurarse de que puedan encontrar rápidamente esta información en un solo lugar. ¿Cómo lo haría? Una pestaña personal de Teams, por supuesto.

## <a name="what-youll-learn"></a>Lo que aprenderás

> [!div class="checklist"]
>
> * Identificar algunas de las configuraciones de aplicaciones y scaffolding relevantes para las pestañas personales
> * Crear contenido de pestaña
> * Actualizar el tema de color de una pestaña en función de las preferencias del usuario

## <a name="1-identify-relevant-app-project-components"></a>1. Identificar componentes relevantes del proyecto de aplicación

Gran parte de las configuraciones de aplicaciones y scaffolding se establecen automáticamente al crear el proyecto con Teams Toolkit. Veamos los componentes principales para crear una pestaña personal.

### <a name="app-configurations"></a>Configuraciones de aplicaciones

En el kit de herramientas, ve **a App Studio** para ver y actualizar las configuraciones de la aplicación.

### <a name="app-scaffolding"></a>Scaffolding de aplicaciones

El scaffolding de la aplicación proporciona los componentes para representar la pestaña personal en Teams. Hay mucho con lo que puede trabajar, pero por ahora solo necesita centrarse en lo siguiente:

* `Tab.js` en el `src/components` directorio del proyecto. Esto es para representar la página de contenido de la pestaña.
* SDK de cliente de JavaScript de Microsoft Teams, que viene cargado previamente en los componentes front-end de su proyecto.

## <a name="2-customize-your-tab-content-page"></a>2. Personalizar la página de contenido de la pestaña

Compile una lista de contactos importantes de su organización. Copie y actualice el siguiente fragmento de código con información que sea relevante para usted o, por razones de tiempo, use el código tal como está.

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

Vaya al directorio `src/components` y abra `Tab.js` . Busque la `render()` función y pegue el contenido dentro `return()` (como se muestra).

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

Agregue la siguiente regla para `App.css` que los vínculos de correo electrónico sean más fáciles de leer, independientemente del tema que se utilice.

```CSS
a {
  color: inherit;
}
```

Guarde los cambios. Vaya a la pestaña de la aplicación en Teams para ver el nuevo contenido.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Captura de pantalla de una pestaña personal con contenido estático.":::

## <a name="3-update-the-tab-theme"></a>3. Actualizar el tema de la pestaña

Las aplicaciones buenas se sienten nativas de Teams, por lo que es importante que la pestaña se combine con el tema de Teams que prefieran los usuarios: predeterminado (claro), oscuro o contraste alto. Como puede que hayas observado en la última captura de pantalla, la pestaña aún tiene un fondo claro cuando el cliente usa el tema oscuro. Esta no es una experiencia de usuario recomendada.

El [SDK del cliente de JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) de Teams puede hacer que su aplicación conozca y reaccione a los cambios de tema en el cliente. Veamos cómo hacerlo.

### <a name="get-context-about-the-teams-client"></a>Obtener contexto sobre el cliente de Teams

En el archivo, hay una llamada que proporciona información sobre, entre otros detalles, el `Tab.js` tema de cliente `microsoftTeams.getContext()` [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) configurado. Gracias al scaffolding de la aplicación, usa este código tal como está para acceder a la `context` interfaz y sus propiedades.

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

Con las propiedades en mano, la aplicación tiene una comprensión sólida de lo que sucede a su alrededor `context` en Teams. Pero la aplicación aún no sabe que su apariencia debe reflejar el tema que elija el usuario.

Necesitas un controlador para que el estado de la aplicación cambie con el tema. Inserte el siguiente controlador de cambios de tema inmediatamente después de la `microsoftTeams.getContext()` llamada.

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>Estilos de temas de coincidencia

El controlador de cambios de tema está en su lugar, pero necesitas código que responda a esos cambios y alinee los colores de la pestaña con el tema actual.

> [!NOTE]
> El siguiente ejemplo es solo una forma de aplicar estilos a la pestaña. Use el código tal como está, expándalo o escriba el suyo propio.

En la `render()` función, almacene el estado proporcionado por el controlador de cambios de tema en `isTheme` .

```JavaScript
  const isTheme = this.state.theme
```

Después de almacenar el estado proporcionado por el controlador de cambios de tema, proporciona lógica condicional para representar los estilos de la pestaña en función del tema actual. En el siguiente ejemplo se muestra una forma básica de hacerlo:
1. Compruebe el tema actual en `isTheme` .
2. Cree un `newTheme` objeto con propiedades CSS relevantes para el tema actual.
3. Aplicar el CSS al elemento HTML raíz del contenido de la pestaña ( `<div>` ).

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

Compruebe la pestaña en Teams. La apariencia debe coincidir estrechamente con el tema oscuro.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Captura de pantalla de una pestaña personal con vista de contenido estático.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene una aplicación de Teams con una pestaña personal que facilita la búsqueda de contactos importantes en su organización.

## <a name="learn-more"></a>Más información

* [Autenticar usuarios de](../tabs/how-to/authentication/auth-aad-sso.md)pestaña con SSO: si solo quiere que los usuarios autorizados visualice la pestaña, configure el inicio de sesión único (SSO) a través de Azure Active Directory (AD).
* [Insertar contenido de una aplicación web](../tabs/how-to/tab-requirements.md)o página web existente: le mostramos cómo crear contenido nuevo para una pestaña personal, pero también puede cargar contenido desde una dirección URL externa.
* [Cree una experiencia perfecta para su pestaña:](../tabs/design/tabs.md)vea las directrices recomendadas para diseñar pestañas de Teams.
* [Crear pestañas para móviles:](../tabs/design/tabs-mobile.md)comprenda cómo desarrollar pestañas para teléfonos y tabletas.
* [Usar datos de Teams con Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview)
* [Crear una pestaña sin el kit de herramientas](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a>Siguiente lección

Sabe cómo crear una pestaña para uso personal. Veamos lo que se necesita para crear una pestaña para canales de equipo y chats.

> [!div class="nextstepaction"]
> [Crear una pestaña de canal](../build-your-first-app/build-channel-tab.md)
