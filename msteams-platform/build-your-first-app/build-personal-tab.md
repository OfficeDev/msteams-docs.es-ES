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
# <a name="build-a-basic-personal-tab-for-microsoft-teams"></a>Crear una pestaña personal básica para Microsoft Teams

Este tutorial le enseña a crear una pestaña personal básica en Microsoft Teams. Las pestañas son una forma sencilla de presentar información en la aplicación hospedando contenido web en Teams. Las pestañas son una característica común de las aplicaciones personales que proporcionan un área de trabajo privada para usuarios individuales. Las pestañas personales son lo más cercano a una experiencia web tradicional en Teams. 

## <a name="what-youll-learn"></a>Lo que aprenderás

* Comprenda las configuraciones de la aplicación y los scaffolding relevantes para las pestañas personales.
* Cree un contenido de pestaña con una lista de contactos de su organización.
* Actualice el tema de color de una pestaña en función de las preferencias del usuario.

## <a name="prerequisites"></a>Requisitos previos

Asegúrate de comprender cómo configurar y crear una aplicación sencilla de Teams. Para obtener más información, consulta crear la primera aplicación de [Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)

## <a name="1-understand-your-app-project-components"></a>1. Comprender los componentes del proyecto de la aplicación

Después de crear una pestaña personal básica, el scaffolding de la aplicación generada proporciona los componentes para representar la pestaña personal en Teams. Hay mucho con lo que puede trabajar, pero por ahora vamos a centrarnos en lo siguiente: 

* `Tab.js` en el `src/components` directorio del proyecto. Esto es para representar la página de contenido de la pestaña.
* SDK de cliente de JavaScript de Microsoft Teams, que se carga previamente en los componentes front-end del proyecto.

Como puede observar en la sección de la parte superior del archivo, el código de ejemplo usa React , una biblioteca de JavaScript de código abierto para crear `import` `Tabs.js` la interfaz de usuario. [](https://reactjs.org/) 

> [!NOTE]
> Aunque el uso de React _no es_ necesario para el desarrollo de Teams, este tutorial te enseña con React.

## <a name="2-customize-your-tab-content-page"></a>2. Personalizar la página de contenido de la pestaña

Puede personalizar la página de contenido de la pestaña para representar una lista de contactos importantes de su organización. 

**Para personalizar la página de contenido de la pestaña**

1. Copie y modifique el siguiente ejemplo de código con información que sea relevante para usted. También puede usar el código tal como está: 
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
1. Llegó al `src/components` directorio y abra el `Tab.js` archivo. 
1. Vaya a `render()` y reemplace el código de plantilla por el código modificado `return()` dentro, como se muestra en el ejemplo siguiente:
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
1. Vaya al directorio y modifique el archivo con el siguiente código para que los vínculos de correo electrónico sean más fáciles de leer `src/components` con cualquier tema que se `App.css` utilice:
    ```CSS
    a {
      color: inherit;
    }
    ```
1. Guarde los cambios. 

   Puedes ver el nuevo contenido en la pestaña de la aplicación en Teams.

   :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-content.png" alt-text="Captura de pantalla de una pestaña personal con contenido estático.":::

## <a name="3-update-your-tab-theme"></a>3. Actualizar el tema de pestaña

Es importante que la pestaña tenga un tema que se sienta nativo de Teams. Debe combinar la pestaña con el tema Teams. Por lo general, los usuarios prefieren los temas predeterminados (claros), oscuros o de contraste alto. Como podrías haber notado en la última captura de pantalla, la pestaña todavía tiene un fondo claro cuando el usuario usa el tema oscuro. Esta no es una experiencia de usuario recomendada.

El SDK de cliente de JavaScript de Teams puede hacer que la aplicación conozca y reaccione a los cambios de tema en el cliente. Para ello, siga estos pasos:

1. **Obtener contexto sobre el tema de cliente de Teams configurado** La `microsoftTeams.getContext()` llamada en el `Tab.js` archivo, proporciona algún contexto sobre el tema de cliente configurado (como el tema oscuro). El siguiente código tiene acceso a la `context` interfaz y sus propiedades:

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
1. **Crear un controlador de cambios de tema** Con las propiedades en la mano, la aplicación tiene una comprensión sólida de lo que está sucediendo a su alrededor `context` en Teams. Sin embargo, la aplicación aún no tiene una apariencia que refleje el tema cuando un usuario lo actualiza.

   Necesitas un controlador para actualizar el estado de la aplicación con el tema. Para crear un controlador, inserte el siguiente controlador de cambios de tema inmediatamente después de la `microsoftTeams.getContext()` llamada:

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
1. **Coincidir con los estilos de tema** Sin embargo, el controlador de cambios de tema está en su lugar, pero aún tiene que responder a los cambios y alinear los colores de la pestaña con el tema actual.

   En la `render()` función, almacene el estado proporcionado por el controlador de cambios de tema en `isTheme` :

    ```JavaScript
      const isTheme = this.state.context.theme
    ```
    
    > [!NOTE]
    > Este ejemplo es solo una forma de aplicar estilos a la pestaña. Use el código tal como está, expándalo o escriba el suyo propio.

    Después de almacenar el estado proporcionado por el controlador de cambios de tema, proporcione la lógica condicional para representar los estilos de la pestaña en función del tema actual. En el ejemplo siguiente se muestra una forma básica de hacerlo:

    1. Vaya a `render()` y compruebe el tema actual en `isTheme` .
    1. Cree un `newTheme` objeto con propiedades CSS relevantes para el tema actual.
    1. Aplique el siguiente CSS al elemento HTML raíz del contenido de la pestaña ( `<div style={newTheme}>` ):

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

       Compruebe la pestaña en Teams. La apariencia ahora coincide estrechamente con el tema oscuro.

       :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-updated-theme.png" alt-text="Captura de pantalla de una pestaña personal con vista de contenido estático.":::

## <a name="see-also"></a>Consulte también

* [SDK para cliente de JavaScript en Teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Diseño de la pestaña para escritorio y web de Microsoft Teams](../tabs/design/tabs.md) 
* [Interfaz de contexto](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)
* [Diseño de la aplicación de Microsoft Teams con plantillas de interfaz de usuario](../concepts/design/design-teams-app-ui-templates.md) 
* [Pestañas en dispositivos móviles](../tabs/design/tabs-mobile.md)
* [Compatibilidad con inicio de sesión único (SSO) para pestañas](../tabs/how-to/authentication/auth-aad-sso.md)
* [Introducción a la API de Microsoft Teams](https://docs.microsoft.com/graph/teams-concept-overview)
* [Crear una pestaña personal personalizada con Node.js y el generador de Yeoman para Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una pestaña de canal](../build-your-first-app/build-channel-tab.md)