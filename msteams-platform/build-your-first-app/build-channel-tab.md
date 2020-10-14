---
title: 'Introducción: crear una pestaña de canal y de grupo'
author: heath-hamilton
description: Cree rápidamente una ficha de canal y de grupo de Microsoft Teams mediante el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: f890754cdf4ca43f39c25e3ba24fcf47b08c5a9f
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452858"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>Crear una pestaña de canal y de grupo para Microsoft Teams

En este tutorial, creará una ficha de *canal* básico (también conocida como una *pestaña de grupo*), que es una página en pantalla completa para un canal o un chat de equipo. A diferencia de una pestaña personal, los usuarios pueden configurar algunos aspectos de este tipo de pestaña (por ejemplo, cambiar el nombre de la ficha para que tenga sentido en su canal).

## <a name="your-assignment"></a>La asignación

No hace mucho tiempo, su organización ha creado una ficha de Microsoft Teams con información sobre cómo ponerse en contacto con las funciones importantes (Departamento de soporte técnico, recursos humanos, etc.). Sin embargo, como el ámbito de la pestaña solo es para uso personal, cada usuario debe instalar la ficha para verla y la adopción es inferior a la esperada. En otras palabras, hay demasiados trabajadores que todavía no saben cómo llegar al Departamento de soporte técnico.

Puede facilitar la búsqueda de esta información si crea una pestaña de canal, lo que eliminará la carga de requerir que todos los usuarios instalen una aplicación. En su lugar, un usuario puede instalar la pestaña en un canal o chatear para obtener el beneficio de todo el grupo.

## <a name="what-youll-learn"></a>Qué aprenderá

> [!div class="checklist"]
>
> * Crear un proyecto de aplicación con Microsoft Teams Toolkit para Visual Studio Code
> * Identificar algunas de las propiedades del manifiesto de la aplicación y scaffolding relevantes para las pestañas de canal y de grupo
> * Hospedar una aplicación localmente
> * Crear contenido de ficha
> * Crear contenido para la página de configuración de una pestaña
> * Permitir la configuración y la instalación de una pestaña
> * Proporcionar un nombre de pestaña sugerido

## <a name="1-create-your-app-project"></a>1. crear un proyecto de aplicación

El kit de herramientas de Microsoft Teams le ayudará a configurar el manifiesto de la aplicación y los scaffolding relevantes para las pestañas de canal y grupo, incluida una página de configuración básica y una página de contenido que muestra un "Hello, World!" Mensaje.

> [!TIP]
> Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. Escriba un nombre para la aplicación de Teams. (Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).
1. En la pantalla **Agregar funciones** **, seleccione la pestaña luego** **grupo o grupo canal de Teams**.
1. Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.  

## <a name="2-identify-relevant-app-project-components"></a>2. identificar los componentes relevantes del proyecto de aplicación

La gran parte del manifiesto de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams. Echemos un vistazo a los componentes principales para crear una ficha de canal y de grupo.

### <a name="app-manifest"></a>Manifiesto de la aplicación

El siguiente fragmento de código del manifiesto de la aplicación muestra [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) , que incluye las propiedades y los valores predeterminados pertinentes para las pestañas de canal y grupo.

```JSON
"configurableTabs": [
    {
        "configurationUrl": "{baseUrl0}/config",
        "canUpdateConfiguration": true,
        "scopes": [
            "team",
            "groupchat"
        ]
    }
],
```

* `configurationUrl`: La dirección URL del host de la página de configuración de pestañas (debe ser HTTPS).
* `canUpdateConfiguration`: Si se establece en `true` , los usuarios pueden cambiar la configuración de las pestañas, cambiar el nombre de la pestaña o quitarla de un canal o un chat.
* `scopes`: Especifica si los usuarios pueden instalar la aplicación en los canales ( `team` ) y los chats ( `groupchat` ). Se requiere al menos un valor.

### <a name="app-scaffolding"></a>Scaffolding de la aplicación

El scaffolding de la aplicación proporciona un `TabConfig.js` archivo, que se encuentra en el `src/components` directorio del proyecto, para representar la página de configuración de la pestaña (próximamente, esto es más).

## <a name="3-run-your-app"></a>3. ejecutar la aplicación

En aras del tiempo, se creará y se ejecutará la aplicación de forma local.

1. En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .
1. Ejecutar `npm start` .

Una vez completada la **compilación correctamente.** mensaje en el terminal.

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a>4. configurar un túnel seguro a la aplicación

Para fines de prueba, vamos a hospedar su pestaña en un servidor Web local (puerto 3000).

1. En un terminal, ejecute `ngrok http 3000` .
1. Copie la dirección URL HTTPS que haya proporcionado.
1. En el `.publish` directorio, Abra `Development.env` .
1. Reemplace el `baseUrl0` valor por la dirección URL copiada. (Por ejemplo, cambie `baseUrl0=http://localhost:3000` a `baseUrl0=https://85528b2b3ca5.ngrok.io` ).

El manifiesto de la aplicación apunta al lugar donde hospeda la pestaña.

## <a name="5-customize-your-tab-content-page"></a>5. personalizar la página de contenido de la pestaña

Abra el manifiesto de la aplicación ( `manifest.json` ) en el `.publish` Directorio y establezca las siguientes propiedades en [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , que define la página de contenido de la pestaña.

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "My Contacts",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

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

Agregue la regla siguiente a para que `App.css` los vínculos de correo electrónico sean más fáciles de leer independientemente del tema que se use.

```CSS
a {
  color: inherit;
}
```

## <a name="6-create-your-tab-configuration-page"></a>6. crear la página de configuración de pestañas

Cada pestaña en un canal o chat tiene una página de configuración, un modal con al menos una opción de configuración que se muestra cuando los usuarios instalan la aplicación. De forma predeterminada, la página de configuración pregunta a los usuarios si quieren notificar al canal o al chat cuando se instala la ficha.

Agregue contenido a la página de configuración. Vaya al directorio del proyecto `src/components` , Abra `TabConfig.js` e inserte contenido dentro de `return()` (como se muestra).

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

## <a name="7-allow-the-tab-to-be-configured-and-installed"></a>7. permitir la configuración y la instalación de la pestaña

Para que los usuarios puedan configurar e instalar correctamente la ficha, debe agregar la [dirección URL de host seguro que configuró](#4-set-up-a-secure-tunnel-to-your-app) en el componente de página de configuración.

Vaya a `TabConfig.js` y busque `microsoftTeams.settings.setSettings` . Para `"contentUrl"` , reemplace la `localhost:3000` parte de la dirección URL con el dominio en el que hospeda el contenido de la pestaña (como se muestra).

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

Además, asegúrese de que `microsoftTeams.settings.setValidityState(true);` . De forma predeterminada, pero si se establece en `false` , el botón **Guardar** se deshabilita en la página Configuración.

## <a name="8-provide-a-suggested-tab-name"></a>8. proporcionar un nombre de pestaña sugerido

Al instalar una pestaña para uso personal, el nombre para mostrar es la `name` propiedad en la `staticTabs` parte del manifiesto de la aplicación (por ejemplo, **mis contactos**). Al instalar una pestaña de canal, se muestra el nombre de la aplicación (por ejemplo, **primera aplicación**) de forma predeterminada.

Esto puede ser adecuado, en función de lo que llame a su aplicación, pero puede que desee proporcionar un nombre que sea más lógico en el contexto de la colaboración en grupo (por ejemplo, los **contactos del equipo**).

En `TabConfig.js` , vuelva a `microsoftTeams.settings.setSettings` . Agregue la `suggestedDisplayName` propiedad con el nombre de la pestaña que desee mostrar de forma predeterminada (como se muestra). Use el nombre proporcionado o cree el suyo propio. Recuerde que en el manifiesto está permitiendo a los usuarios cambiar el nombre si lo desean.

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="9-view-the-tab"></a>9. ver la pestaña

Para ver las páginas de contenido y configuración de la pestaña, debe instalarla en un canal o chat.

1. En el cliente de Microsoft Teams, seleccione **aplicaciones**.
1. Seleccione **cargar una aplicación personalizada** y elija la aplicación `Development.zip` .
1. Elija **Agregar a un equipo** o **Agregar a un chat** y busque un canal o un chat que pueda usar para las pruebas.
1. Seleccione **configurar una pestaña**. Aparece la página Configuración.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Captura de pantalla de una página de configuración de ficha de canal.":::
1. Seleccione **Guardar** para configurar la pestaña. Se muestra el contenido.<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Captura de pantalla de una página de configuración de ficha de canal.":::

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene una aplicación de Microsoft Teams con una pestaña para mostrar contenido útil en canales y chats.

## <a name="learn-more"></a>Más información

* [Autenticar usuarios de pestaña con SSO](../tabs/how-to/authentication/auth-aad-sso.md): si solo quiere que los usuarios autorizados vean su pestaña, configure el inicio de sesión único (SSO) a través de Azure Active Directory (ad).
* [Insertar contenido de una aplicación web o página web existente](../tabs/how-to/add-tab.md#tab-requirements): le mostramos cómo crear nuevo contenido para una pestaña personal, pero también puede cargar contenido desde una dirección URL externa.
* [Crear una experiencia sin problemas para su pestaña](../tabs/design/tabs.md): Consulte las directrices recomendadas para diseñar pestañas de Microsoft Teams.
* [Crear pestañas para móviles](../tabs/design/tabs-mobile.md): comprenda cómo desarrollar pestañas para teléfonos y tabletas.
* [Crear una ficha sin el kit de herramientas](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>Lección siguiente

Sabe cómo crear una pestaña para la colaboración. ¿Desea intentar compilar un tipo diferente de aplicación de Teams?

> [!div class="nextstepaction"]
> [Crear un bot](../build-your-first-app/build-bot.md)
