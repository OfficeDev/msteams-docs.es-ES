---
title: 'Introducción: crear una pestaña de canal y grupo'
author: heath-hamilton
description: Cree rápidamente un canal y una pestaña de grupo de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 0692d28653063c2f886db9a03e7136379edde9c3
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911880"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>Crear una pestaña de canal y grupo para Microsoft Teams

En este tutorial, compilará una pestaña de canal básica *(también* conocida como pestaña de *grupo),* que es una página de pantalla completa para un chat o canal de equipo. A diferencia de una pestaña personal, los usuarios pueden configurar algunos aspectos de este tipo de pestaña (por ejemplo, cambiar el nombre de la pestaña para que sea significativa para su canal).

## <a name="your-assignment"></a>Su asignación

No hace mucho, su organización creó una aplicación de Teams que usa una pestaña para mostrar información de contacto importante (servicio de soporte, recursos humanos, etc.). Sin embargo, dado que es una pestaña personal, cada usuario debe instalar la pestaña para verla y la adopción es menor de lo esperado. En otras palabras, demasiados trabajadores siguen sin saber cómo llegar al servicio de ayuda.

Puedes hacer que esta información sea más fácil de encontrar mediante la creación de una pestaña de canal, lo que quitará la carga de requerir que todos los usuarios instalen una aplicación. En su lugar, un usuario puede agregar la pestaña en un canal o chat para beneficio de todo un grupo.

## <a name="what-youll-learn"></a>Lo que aprenderás

> [!div class="checklist"]
>
> * Crear un proyecto de aplicación con Microsoft Teams Toolkit for Visual Studio Code
> * Identificar algunas de las configuraciones de aplicaciones y scaffolding relevantes para las pestañas de canal
> * Crear contenido de pestaña
> * Crear contenido para la página de configuración de una pestaña
> * Proporcionar un nombre de pestaña sugerido
> * Compilar y ejecutar la aplicación localmente
> * Instalación de prueba de la aplicación en Teams

## <a name="before-you-begin"></a>Antes de empezar

Si aún no lo ha hecho, asegúrese de comprender [e instalar los requisitos previos de desarrollo de Teams.](build-first-app-overview.md#get-prerequisites)

## <a name="1-create-your-app-project"></a>1. Crear el proyecto de aplicación

Microsoft Teams Toolkit ayuda a configurar la aplicación y a configurar scaffolding relevante para las pestañas de canal y grupo, incluida una página de configuración básica y una página de contenido que muestra un mensaje "Hola a todos". Mensaje.

> [!TIP]
> Si no ha creado un proyecto de aplicación de Teams [](../build-your-first-app/build-and-run.md) antes, es posible que le sea útil seguir estas instrucciones que explican los proyectos con más detalle.

1. En Visual Studio, seleccione **Microsoft Teams** en la barra de actividades de la izquierda y elija Crear una nueva aplicación :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: de **Teams.**
1. Cuando se le solicite, inicie sesión con su cuenta de desarrollo de Microsoft 365.
1. En la **pantalla Agregar funcionalidades,** seleccione **Pestaña** y, a **continuación, Siguiente.**
1. Escriba un nombre para su aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local). Seleccione **la pestaña De grupo o canal de Teams.**
1. Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.  

## <a name="2-identify-relevant-app-project-components"></a>2. Identificar componentes relevantes del proyecto de aplicación

Gran parte de las configuraciones de la aplicación y el scaffolding se establecen automáticamente al crear el proyecto con el kit de herramientas. Veamos los componentes principales para crear una pestaña de canal.

### <a name="app-configurations"></a>Configuraciones de aplicaciones

En el kit de herramientas, ve **a App Studio** para ver y actualizar las configuraciones de la aplicación.

### <a name="app-scaffolding"></a>Scaffolding de aplicaciones

El scaffolding de la aplicación proporciona los componentes para representar la pestaña de canal en Teams. Hay mucho con lo que puede trabajar, pero por ahora solo necesita centrarse en lo siguiente:

* Dos archivos ubicados en `src/components` el directorio del proyecto:
  * `Tab.js` para representar la página de contenido de la pestaña.
  * `TabConfig.js` para representar la página de configuración de la pestaña.
* SDK de cliente de JavaScript de Microsoft Teams, que viene cargado previamente en los componentes front-end de su proyecto.

## <a name="3-customize-your-tab-content-page"></a>3. Personalizar la página de contenido de la pestaña

Copie y actualice el siguiente fragmento de código con información relevante para su organización o, por razones de tiempo, use el código tal como está.

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

Agregue la siguiente regla (también ubicada en) para que los vínculos de correo electrónico sean más fáciles de `App.css` `src/components` leer, independientemente del tema que se utilice.

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a>4. Personalizar la página de configuración de la pestaña

Cada pestaña de un canal o chat tiene una página de configuración, un modal con al menos una opción de configuración que se muestra cuando los usuarios agregan la aplicación. De forma predeterminada, la página de configuración pregunta a los usuarios si desean notificar al canal o chat cuando se instala la pestaña.

Agregue contenido personalizado a la página de configuración. Vaya al directorio del proyecto, abra y actualice el contenido del marcador de posición `src/components` `TabConfig.js` dentro `return()` (como se muestra en el ejemplo siguiente).

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
> Como mínimo, proporciona información breve sobre la aplicación en esta página, ya que esta puede ser la primera vez que los usuarios estén informando sobre ella. También puede incluir opciones de configuración personalizadas o un flujo [de trabajo de](../tabs/how-to/authentication/auth-aad-sso.md)autenticación, que es común en las páginas de configuración de pestañas.

## <a name="5-provide-a-suggested-tab-name"></a>5. Proporcionar un nombre de pestaña sugerido

Cuando agregas una pestaña de canal, de forma predeterminada se muestra el nombre de la aplicación (por ejemplo, **primera aplicación).**

Esto puede estar bien en función de lo que llames a tu aplicación, pero es posible que quieras proporcionar un nombre que tenga más sentido en el contexto de la colaboración en grupo (por ejemplo, Contactos **de equipo).**

1. En `TabConfig.js` , vaya a `microsoftTeams.settings.setSettings` .
2. Agregue la `suggestedDisplayName` propiedad con el nombre de pestaña que desea mostrar de forma predeterminada. 
3. Use el nombre proporcionado en el ejemplo siguiente o escriba su nombre. (De forma predeterminada, los usuarios pueden cambiar el nombre).

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a>6. Compilar y ejecutar la aplicación

En interés del tiempo, compilarás y ejecutarás la aplicación localmente.

(Esta información también está disponible en el kit de `README` herramientas).

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecute `npm start` .

Una vez completado, se compila **correctamente.** en el terminal. La aplicación se está ejecutando en `https://localhost:3000` .

## <a name="7-sideload-your-app-in-teams"></a>7. Instalación local de la aplicación en Teams

La aplicación está lista para probarse en Teams. Para ello, debes tener una cuenta que permita la instalación de prueba de la aplicación. (Si no está seguro de que lo tiene, obtenga información sobre cómo obtener una cuenta [de desarrollo de Teams).](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)

1. En Visual Studio, presione la tecla **F5** para iniciar un cliente web de Teams.
1. Para mostrar el contenido de la aplicación en Teams, especifique que el lugar donde se ejecuta la aplicación ( `localhost` ) es de confianza:
   1. Abra una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abrió después de presionar **F5**.
   1. Vaya a `https://localhost:3000/tab` la página y continúe.
1. Vuelva a Teams. En el modal, seleccione **Agregar a un** equipo o Agregar a un **chat** y busque un canal o chat que pueda usar para las pruebas.
1. Seleccione **Configurar una pestaña.** La página de configuración se muestra en un modal.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Captura de pantalla de una página de configuración de pestaña de canal.":::
1. Seleccione **Guardar** para configurar la pestaña. Se muestra la página de contenido.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Captura de pantalla de una pestaña de canal con vista de contenido estático.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene una aplicación de Teams con una pestaña para mostrar contenido útil en canales y chats.

## <a name="learn-more"></a>Más información

* Sigue nuestras [directrices de diseño](../tabs/design/tabs.md) y compila con [plantillas de interfaz](../concepts/design/design-teams-app-ui-templates.md) de usuario listas para producción para crear una experiencia sin problemas.
* Comprenda [las consideraciones móviles para](../tabs/design/tabs-mobile.md) las pestañas.
* [Agregue la autenticación SSO a la pestaña.](../tabs/how-to/authentication/auth-aad-sso.md)
* Usar datos de Teams con [Microsoft Graph.](https://docs.microsoft.com/graph/teams-concept-overview)
* [Crear una pestaña sin el kit de herramientas](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a>Siguiente lección

Sabe cómo crear una pestaña para la colaboración. ¿Desea probar a crear un tipo diferente de aplicación de Teams?

> [!div class="nextstepaction"]
> [Crear un bot](../build-your-first-app/build-bot.md)
