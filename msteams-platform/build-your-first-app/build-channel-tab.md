---
title: 'Introducción: crear una pestaña de canal y de grupo'
author: heath-hamilton
description: Cree rápidamente una ficha de canal y de grupo de Microsoft Teams mediante el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: bb87d34974469057287cf63725e7722125c57c34
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605248"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>Crear una pestaña de canal y de grupo para Microsoft Teams

En este tutorial, creará una ficha de *canal* básico (también conocida como una *pestaña de grupo*), que es una página en pantalla completa para un canal o un chat de equipo. A diferencia de una pestaña personal, los usuarios pueden configurar algunos aspectos de este tipo de pestaña (por ejemplo, cambiar el nombre de la ficha para que tenga sentido en su canal).

## <a name="your-assignment"></a>La asignación

No hace mucho tiempo, su organización ha creado una aplicación de Microsoft teams que usa una pestaña para mostrar información de contacto importante (soporte técnico, recursos humanos, etc.). Sin embargo, puesto que se trata de una pestaña personal, cada usuario debe instalar la pestaña para ver el resultado y la adopción es inferior a lo esperado. En otras palabras, hay demasiados trabajadores que todavía no saben cómo llegar al Departamento de soporte técnico.

Puede facilitar la búsqueda de esta información si crea una pestaña de canal, lo que eliminará la carga de requerir que todos los usuarios instalen una aplicación. En su lugar, un usuario puede Agregar la pestaña en un canal o chatear para beneficiar de todo el grupo.

## <a name="what-youll-learn"></a>Qué aprenderá

> [!div class="checklist"]
>
> * Crear un proyecto de aplicación con Microsoft Teams Toolkit para Visual Studio Code
> * Identificar algunas de las configuraciones de aplicación y scaffolding relevantes para las pestañas de canal y de grupo
> * Crear contenido de ficha
> * Crear contenido para la página de configuración de una pestaña
> * Proporcionar un nombre de pestaña sugerido
> * Compilar y ejecutar la aplicación localmente
> * Transferir localmente la aplicación en Teams para realizar pruebas

## <a name="before-you-begin"></a>Antes de empezar

Si aún no lo ha hecho, asegúrese [de que comprende e instala los requisitos previos de desarrollo de Microsoft Teams](build-first-app-overview.md#get-prerequisites).

## <a name="1-create-your-app-project"></a>1. crear un proyecto de aplicación

El kit de herramientas de Microsoft Teams ayuda a configurar la aplicación y a configurar la técnica scaffolding relevante para las pestañas de canal y grupo, incluida una página de configuración básica y una página de contenido que muestra un "Hello, World!" Mensaje.

> [!TIP]
> Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. Cuando se le solicite, inicie sesión con su cuenta de desarrollo de 365 de Microsoft.
1. En la pantalla **Agregar funciones** , seleccione la **pestaña** **siguiente**.
1. Escriba un nombre para la aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).
1. Compruebe la **pestaña personal** y las opciones de la **ficha canal de grupo o de Teams** . (Pronto aprenderá por qué necesita ambos tipos de pestañas).
1. Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.  

## <a name="2-identify-relevant-app-project-components"></a>2. identificar los componentes relevantes del proyecto de aplicación

Una gran parte de la configuración de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams. Echemos un vistazo a los componentes principales para crear una ficha de canal y de grupo.

### <a name="app-configurations"></a>Configuraciones de aplicaciones

Puede ver y actualizar las configuraciones de la aplicación mediante App Studio, que se incluye en el kit de herramientas.

Durante la configuración, el kit de herramientas configuró inicialmente dos componentes básicos de las fichas de canal y de Grupo:

* **Página de configuración**: modal para agregar una pestaña a un canal o un chat. (En App Studio, puede encontrar esta página yendo a **pestañas > ficha equipo**).
* **Página de contenido**: donde se muestra el contenido principal. (En App Studio, puede encontrar esta página yendo a las **pestañas > agregar una pestaña personal**).

### <a name="app-scaffolding"></a>Scaffolding de la aplicación

El scaffolding de la aplicación proporciona los componentes para representar la pestaña personal en Teams. Hay muchas cosas con las que puede trabajar, pero por ahora solo necesita centrarse en lo siguiente:

* Dos archivos ubicados en el `src/components` directorio del proyecto:
  * `Tab.js` para representar la página de contenido de la pestaña.
  * `TabConfig.js` para representar la página de configuración de la pestaña.
* SDK cliente de JavaScript de Microsoft Teams, que viene precargado en los componentes front-end del proyecto.

## <a name="3-customize-your-tab-content-page"></a>3. personalizar la página de contenido de la pestaña

Copie y actualice el siguiente fragmento de código con información relevante para su organización o, por el momento, use el código tal y como está.

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

Agregue la siguiente regla a `App.css` (también se encuentra en `src/components` ) para que los vínculos de correo electrónico sean más fáciles de leer independientemente del tema que se use.

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a>4. personalizar la página de configuración de pestañas

Cada pestaña en un canal o chat tiene una página de configuración, un modal con al menos una opción de configuración que se muestra cuando los usuarios agregan la aplicación. De forma predeterminada, la página de configuración pregunta a los usuarios si quieren notificar al canal o al chat cuando se instala la ficha.

Agregue contenido personalizado a la página de configuración. Vaya al directorio del proyecto `src/components` , Abra `TabConfig.js` y actualice el contenido del marcador de posición dentro de `return()` (como se muestra en el siguiente ejemplo).

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
> Como mínimo, proporcione información breve sobre la aplicación en esta página, ya que esto puede ser la primera vez que los usuarios aprenden sobre ella. También puede incluir opciones de configuración personalizadas o un [flujo de trabajo de autenticación](../tabs/how-to/authentication/auth-aad-sso.md), que es común en las páginas de configuración de pestañas.

## <a name="5-provide-a-suggested-tab-name"></a>5. proporcionar un nombre de pestaña sugerido

Cuando se agrega una pestaña de canal o de grupo, se muestra el nombre de la aplicación (por ejemplo, la **primera aplicación**) de forma predeterminada.

Esto puede ser adecuado, en función de lo que llame a su aplicación, pero puede que desee proporcionar un nombre que sea más lógico en el contexto de la colaboración en grupo (por ejemplo, los **contactos del equipo**).

En `TabConfig.js` , vaya a `microsoftTeams.settings.setSettings` . Agregue la `suggestedDisplayName` propiedad con el nombre de la pestaña que desee mostrar de forma predeterminada (como se muestra). Use el nombre proporcionado o cree el suyo propio. (De forma predeterminada, los usuarios pueden cambiar el nombre si lo desean).

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a>6. compilar y ejecutar la aplicación

En aras del tiempo, se creará y se ejecutará la aplicación de forma local.

(Esta información también está disponible en el kit de herramientas `README` ).

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecutar `npm start` .

Una vez completada la **compilación correctamente.** mensaje en el terminal. La aplicación se está ejecutando en `https://localhost:3000` .

## <a name="7-sideload-your-app-in-teams"></a>7. transferir localmente la aplicación en Microsoft Teams

La aplicación está lista para realizar pruebas en Microsoft Teams. Para ello, debe tener una cuenta que permita la transferencia local de aplicaciones. (Si no está seguro de ello, obtenga información sobre cómo obtener una cuenta de desarrollo de Microsoft [Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)).

1. En Visual Studio Code, presione la tecla **F5** para iniciar un cliente web de Teams.
1. Para mostrar el contenido de la aplicación en Teams, especifique que la aplicación en ejecución ( `localhost` ) sea de confianza:
   1. Abrir una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abre después de presionar **F5**.
   1. Vaya a `https://localhost:3000/tab` la página y continúe con ella.
1. Vuelva a teams. En el modal, seleccione **Agregar a un equipo** o **Agregar a un chat** y busque un canal o un chat que pueda usar para las pruebas.
1. Seleccione **configurar una pestaña**. La página de configuración se muestra en un modal.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Captura de pantalla de una página de configuración de ficha de canal.":::
1. Seleccione **Guardar** para configurar la pestaña. Se muestra la página de contenido.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Captura de pantalla de una pestaña de canal con vista de contenido estático.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene una aplicación de Microsoft Teams con una pestaña para mostrar contenido útil en canales y chats.

## <a name="learn-more"></a>Más información

* [Autenticar usuarios de pestaña con SSO](../tabs/how-to/authentication/auth-aad-sso.md): si solo quiere que los usuarios autorizados vean su pestaña, configure el inicio de sesión único (SSO) a través de Azure Active Directory (ad).
* [Insertar contenido de una aplicación web o página web existente](../tabs/how-to/add-tab.md#tab-requirements): le mostramos cómo crear nuevo contenido para una pestaña personal, pero también puede cargar contenido desde una dirección URL externa.
* [Crear una experiencia sin problemas para su pestaña](../tabs/design/tabs.md): Consulte las directrices recomendadas para diseñar pestañas de Microsoft Teams.
* [Crear pestañas para móviles](../tabs/design/tabs-mobile.md): comprenda cómo desarrollar pestañas para teléfonos y tabletas.
* [Uso de datos de Teams con la API de Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview)
* [Crear una ficha sin el kit de herramientas](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>Lección siguiente

Sabe cómo crear una pestaña para la colaboración. ¿Desea intentar compilar un tipo diferente de aplicación de Teams?

> [!div class="nextstepaction"]
> [Crear un bot](../build-your-first-app/build-bot.md)
