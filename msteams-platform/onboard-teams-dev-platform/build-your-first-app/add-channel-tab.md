---
title: Crear una pestaña de canal para Teams
author: heath-hamilton
description: Obtenga información sobre cómo crear una pestaña de canal en su primera aplicación de Microsoft Teams.
ms.topic: tutorial
ms.openlocfilehash: f0c59328219b5611efc02c9eb04db6fdc517ca08
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652230"
---
# <a name="create-a-channel-tab-for-teams"></a>Crear una pestaña de canal para Teams

En este tutorial, creará una ficha básica de *canal*, una página de contenido a pantalla completa para un canal de equipo o un chat. A diferencia de una pestaña personal, los usuarios pueden configurar algunos aspectos de una ficha de canal (por ejemplo, cambiar el nombre de la ficha para que tenga sentido en su canal).

## <a name="before-you-begin"></a>Antes de empezar

Necesita una aplicación básica que se ejecute para empezar. Si no tiene uno, siga las instrucciones de la [compilación y ejecute la primera aplicación de Teams](build-and-run-with-toolkit.md). Al crear el proyecto de la aplicación, elija solo la opción de la **ficha canal de grupo o de Teams** .

## <a name="your-assignment"></a>La asignación

No hace mucho tiempo, su organización ha creado una ficha de Microsoft Teams con información sobre cómo ponerse en contacto con las funciones importantes (Departamento de soporte técnico, recursos humanos, etc.). Sin embargo, como el ámbito de la pestaña solo es para uso personal, cada usuario debe instalar la ficha para verla y la adopción es inferior a la esperada. En otras palabras, hay demasiados trabajadores que todavía no saben cómo llegar al Departamento de soporte técnico.

Puede facilitar la búsqueda de esta información si crea una pestaña de canal, lo que eliminará la carga de requerir que todos los usuarios instalen una aplicación. En su lugar, un usuario puede instalar la pestaña en un canal o chatear para obtener el beneficio de todo el grupo.

## <a name="what-youll-learn"></a>Qué aprenderá

> [!div class="checklist"]
>
> * Identificar el manifiesto de la aplicación y los componentes de scaffolding relevantes para las pestañas de canal
> * Crear contenido para la pestaña
> * Crear contenido para la página de configuración de una pestaña
> * Permitir la configuración y la instalación de la ficha
> * Proporcionar un nombre de pestaña sugerido

## <a name="identify-relevant-app-manifest-and-scaffolding-components"></a>Identificar los componentes relevantes del manifiesto de la aplicación y los componentes de scaffolding

Gran parte del manifiesto y el manifiesto de la aplicación de pestañas de canal se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams. Echemos un vistazo a los componentes principales para crear una pestaña de canal.

### <a name="app-manifest"></a>Manifiesto de la aplicación

El siguiente fragmento de código del manifiesto de la aplicación muestra [`configurableTabs`](../../resources/schema/manifest-schema.md#configurabletabs) , que incluye las propiedades y los valores predeterminados que son relevantes para las pestañas de canal.

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

## <a name="create-your-tab-content"></a>Crear el contenido de la pestaña

Abra el manifiesto de la aplicación ( `manifest.json` ) y establezca las siguientes propiedades en [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs) , que define la página de contenido de la pestaña.

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

## <a name="create-your-tab-configuration-page"></a>Crear la página de configuración de pestañas

Cada ficha de canal tiene una página de configuración, un modal con al menos una opción de configuración que se muestra al instalar la aplicación. De forma predeterminada, la página de configuración pregunta a los usuarios si quieren notificar al canal o al chat cuando se instala la ficha.

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
> Como mínimo, proporcione información breve sobre la aplicación en esta página, ya que esto puede ser la primera vez que los usuarios aprenden sobre ella. También puede incluir opciones de configuración personalizadas o un [flujo de trabajo de autenticación](../../tabs/how-to/authentication/auth-aad-sso.md), que es común en las páginas de configuración de pestañas.

## <a name="allow-the-tab-to-be-configured-and-installed"></a>Permitir la configuración y la instalación de la ficha

Para que los usuarios puedan configurar e instalar correctamente la ficha canal, debe agregar la dirección URL de host que configuró al [crear y ejecutar su primera aplicación](build-and-run-with-toolkit.md) en el componente de página de configuración.

Vaya a `TabConfig.js` y busque `microsoftTeams.settings.setSettings` . Para `"contentUrl"` , reemplace la `localhost:3000` parte de la dirección URL con el dominio en el que hospeda el contenido de la pestaña (como se muestra).

```JavaScript
    microsoftTeams.settings.setSettings({
      "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
    });
```

Además, asegúrese de que `microsoftTeams.settings.setValidityState(true);` . De forma predeterminada, pero si se establece en `false` , el botón **Guardar** se deshabilita en la página Configuración.

## <a name="provide-a-suggested-tab-name"></a>Proporcionar un nombre de pestaña sugerido

Al instalar una pestaña para uso personal, el nombre para mostrar es la `name` propiedad en la `staticTabs` parte del manifiesto de la aplicación (por ejemplo, **mis contactos**). Al instalar una pestaña de canal, se muestra el nombre de la aplicación (por ejemplo, **primera aplicación**) de forma predeterminada.

Esto puede ser adecuado, en función de lo que llame a su aplicación, pero puede que desee proporcionar un nombre que sea más lógico en el contexto de la colaboración en grupo (por ejemplo, los **contactos del equipo**).

En `TabConfig.js` , vuelva a `microsoftTeams.settings.setSettings` . Agregue la `suggestedDisplayName` propiedad con el nombre de la pestaña que desee mostrar de forma predeterminada (como se muestra). Use el nombre proporcionado o cree el suyo propio. Recuerde que en el manifiesto está permitiendo a los usuarios cambiar el nombre si lo desean.

```JavaScript
    microsoftTeams.settings.setSettings({
      "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
      "suggestedDisplayName": "Team Contacts"
    });
```

## <a name="view-the-channel-tab"></a>Ver la ficha canal

Para ver las páginas de contenido y configuración de la pestaña de canal, debe instalarla en un canal o chat.

1. En el cliente de Microsoft Teams, seleccione **aplicaciones**.
1. Seleccione **cargar una aplicación personalizada** y elija la aplicación `Development.zip` .
1. Elija **Agregar a un equipo** o **Agregar a un chat** y busque un canal o un chat que pueda usar para las pruebas.
1. Seleccione **configurar una pestaña**. Aparece la página Configuración.

:::image type="content" source="../doc-links/images/channel-tab-tutorial-content.png" alt-text="Captura de pantalla de ejemplo de una página de configuración de ficha de canal":::

Una vez que seleccione **Guardar** para configurar la ficha, se mostrará el contenido.

![Captura de pantalla de ejemplo de una pestaña de canal con contenido estático](../doc-links/images/channel-tab-tutorial-content-installed.png)

## <a name="well-done"></a>Bien hecho

¡Enhorabuena! Tiene una aplicación de Microsoft Teams con una pestaña de canal para mostrar contenido útil en canales y chats.

## <a name="learn-more"></a>Más información

* [Autenticar usuarios de pestaña con SSO](../../tabs/how-to/authentication/auth-aad-sso.md): si solo quiere que los usuarios autorizados vean su pestaña, configure el inicio de sesión único (SSO) a través de Azure Active Directory (ad).
* [Insertar contenido de una aplicación web o página web existente](../../tabs/how-to/add-tab.md#tab-requirements): le mostramos cómo crear nuevo contenido para una pestaña personal, pero también puede cargar contenido desde una dirección URL externa.
* [Crear una experiencia sin problemas para su pestaña](../../tabs/design/tabs.md): Consulte las directrices recomendadas para diseñar pestañas de Microsoft Teams.
* [Crear pestañas para dispositivos móviles](../../tabs/design/tabs-mobile.md): comprenda cómo desarrollar pestañas para smartphones y tabletas.
