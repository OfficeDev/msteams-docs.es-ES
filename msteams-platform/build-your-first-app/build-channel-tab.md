---
title: 'Introducción: crear una pestaña de canal y grupo'
author: girliemac
description: Cree rápidamente una pestaña Microsoft Teams canal y grupo mediante el Microsoft Teams Toolkit.
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: ff9cfbfb7d099db52966f119add4ce8729929aa1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566071"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a>Cree la primera pestaña de canal y grupo para Microsoft Teams

Este tutorial le enseña a  crear una pestaña de canal básica también conocida como pestaña de grupo *,* que es una página a pantalla completa para un canal de grupo o chat. También puede configurar algunos aspectos de este tipo de pestaña, por ejemplo, cambiar el nombre de la pestaña para que sea significativa para su canal, lo que no puede hacer en una pestaña personal.

## <a name="what-youll-learn"></a>Lo que aprenderás

* Crea un proyecto de aplicación con el Microsoft Teams Toolkit para Visual Studio Code.
* Comprenda las configuraciones de la aplicación y los scaffolding relevantes para las pestañas de canal.
* Crear contenido de pestaña y configuración de pestañas.
* Crea y ejecuta la aplicación en teams para pruebas.

## <a name="prerequisites"></a>Requisitos previos

Asegúrate de comprender cómo configurar y crear una aplicación Teams sencilla. Para obtener más información, consulta [crear la primera aplicación Microsoft Teams "Hello, World!"](../build-your-first-app/build-and-run.md).

## <a name="1-create-your-app-project"></a>1. Crear el proyecto de aplicación

El Microsoft Teams Toolkit te ayuda a configurar la aplicación y configurar el scaffolding relevante para las pestañas de canal y grupo. También contiene una página de configuración básica y una página de contenido que muestra un "Hello, World!" Mensaje.

**Para crear el proyecto de aplicación**

1. Vaya a Visual Studio Code y seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividades izquierda.
1. Inicie sesión con su Microsoft 365 de desarrollo cuando se le pida que lo haga.
1. En la **pantalla Seleccionar proyecto,** seleccione **JS** (JavaScript) en Canal y aplicación **de grupo.**
1. Escribe un nombre para la Teams aplicación. 

    > [!NOTE]
    > Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local.

1. Seleccione **Grupo o Teams de canal**.
1. Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto y guardar el proyecto en el equipo local.  

## <a name="2-understand-your-app-project-components"></a>2. Comprender los componentes del proyecto de la aplicación

Gran parte de las configuraciones de la aplicación y los scaffolding se establecen automáticamente al crear el proyecto con el kit de herramientas. Veamos los componentes principales para crear una pestaña de canal.

* **Configuraciones de aplicaciones:** abre **App Studio** en el kit de herramientas para ver y actualizar las configuraciones de la aplicación.
* **Scaffolding de aplicaciones:** el scaffolding de la aplicación proporciona los componentes necesarios para representar la pestaña de canal en Teams. Sin embargo, hay mucho con lo que puede trabajar, por ahora vamos a centrarnos en lo siguiente:
  * Los archivos ubicados en el `src/components` directorio del proyecto:
    * `Tab.js` para representar la página de contenido de la pestaña.
    * `TabConfig.js` para representar la página de configuración de la pestaña.
  * Microsoft Teams SDK de cliente de JavaScript, que viene precargado en los componentes front-end del proyecto.

## <a name="3-customize-your-tab-content-page"></a>3. Personalizar la página de contenido de la pestaña

1. Copie y modifique el siguiente ejemplo de código con información relevante para su organización. También puede usar el fragmento de código tal como es:
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
    
1. Vaya al `src/components` directorio y abra el `Tab.js` archivo. Busque la `render()` función y pegue el código dentro como se muestra en el siguiente `return()` ejemplo:
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
    
1. Vaya al directorio y actualice el archivo con el siguiente código para que los vínculos de correo electrónico sean más fáciles de `src/components` leer en cualquier tema que se `App.css` utilice:
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a>4. Personalizar la página de configuración de pestañas

Cada pestaña de un canal o chat tiene una página de configuración, un modal con al menos una opción de configuración que se muestra cuando los usuarios agregan la aplicación. De forma predeterminada, la página de configuración pregunta a los usuarios si quieren notificar al canal o al chat cuando se instala la pestaña. Puede personalizar la página de configuración agregando contenido personalizado.

Para agregar contenido personalizado, abra el archivo desde el directorio y actualice el contenido de marcador de posición dentro como `TabConfig.js` se muestra en el ejemplo `src/components` `return()` siguiente:

  ```JavaScript
  return (
      <div>
        <h1>Add My Contoso Contacts</h1>
        <div>
          Select <b>Save</b> to add our organization's important contacts to this workspace.
        </div>
      </div>
  );
  ```
 
> [!TIP]
> Proporciona una breve información sobre la aplicación en esta página, ya que esta sería la primera vez que los usuarios leen sobre ella. También puede incluir opciones de configuración personalizadas o un flujo [de trabajo de autenticación,](../tabs/how-to/authentication/auth-aad-sso.md)que es común en las páginas de configuración de pestañas.

## <a name="5-customize-your-tab-name"></a>5. Personalizar el nombre de la pestaña

Al agregar una pestaña de canal, el nombre de la aplicación se muestra de forma predeterminada, por ejemplo, **first-app**. También puede proporcionar un nombre que tenga más sentido en el contexto de la colaboración en grupo, por ejemplo, **Contactos de grupo:**

1. Vaya al `src/components` directorio y abra el `TabConfig.js` archivo.
1. Agregue la propiedad con el nombre de pestaña que desea mostrar de forma predeterminada `suggestedDisplayName` `microsoftTeams.settings.setSettings` en, como se muestra en el ejemplo siguiente:

    ```JavaScript
        microsoftTeams.settings.setSettings({
        "contentUrl": "https://localhost:3000/tab",
        "suggestedDisplayName": "Team Contacts"
      });
      ```

## <a name="6-build-and-run-your-app"></a>6. Crear y ejecutar la aplicación

Este tutorial te enseña a crear y ejecutar la aplicación localmente. 

1. Vaya al directorio raíz del proyecto de la aplicación en Terminal.
1. Ejecute `npm install`.
1. Ejecute `npm start`.

Esta información también está presente en la `README` sección del kit de herramientas.
La aplicación se está ejecutando `https://localhost:3000` después de **la compilación correctamente.** mensaje aparece en el terminal. 

## <a name="7-sideload-your-app-in-teams"></a>7. Instalación local de la aplicación en Teams

La aplicación está lista para probarse en Teams. Para ello, debes tener una cuenta que permita la instalación local de la aplicación. 

1. Abra un Teams web en Visual Studio Code con la **clave F5.**
1. Agregue ( ) como confiable siguiendo estos pasos para permitir que el contenido de la aplicación `localhost` se muestre en Teams:

   1. Abra una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abrió con la **tecla F5.**
   1. Abra `https://localhost:3000/tab` y continúe con la página.

1. Selecciona **Agregar a un equipo** o Agregar a un **chat** y busca un canal o chat que puedas usar para realizar pruebas desde el modal en Teams.
1. Seleccione **Configurar una pestaña**. La página de configuración se muestra en un modal.

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Captura de pantalla de una página de configuración de pestaña de canal.":::

1. Seleccione **Guardar** para configurar la pestaña. Aparece la siguiente página de contenido:

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Captura de pantalla de una pestaña de canal con vista de contenido estático.":::

## <a name="see-also"></a>Consulte también

* [Compilar y ejecutar la primera Microsoft Teams aplicación](../build-your-first-app/build-and-run.md) 
* [SDK para cliente de JavaScript en Teams](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Diseño de la pestaña para Microsoft Teams escritorio y web](../tabs/design/tabs.md) 
* [Diseñar la aplicación Microsoft Teams con plantillas de interfaz de usuario](../concepts/design/design-teams-app-ui-templates.md) 
* [Pestañas en dispositivos móviles](../tabs/design/tabs-mobile.md)
* [Compatibilidad con inicio de sesión único (SSO) para pestañas](../tabs/how-to/authentication/auth-aad-sso.md)
* [Introducción a la API de Microsoft Teams](/graph/teams-concept-overview)
* [Crear una pestaña personal personalizada con Node.js y el generador de Yeoman para Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear un bot](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [Crear una extensión de mensajería](../build-your-first-app/build-messaging-extension.md)
