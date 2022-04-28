---
title: Creación de una página de configuración
author: surbhigupta
description: Obtenga información sobre cómo crear una página de configuración para configurar un canal o un chat de grupo para la configuración, como obtener datos de contexto, insertar marcadores de posición y autenticación mediante ejemplos de código.
keywords: Canal de grupo de pestañas de teams configurable
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: dc1c5c7c8852d13ab490ae0782be0a01eef3fbea
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103421"
---
# <a name="create-a-configuration-page"></a>Creación de una página de configuración

Una página de configuración es un tipo especial de [página de contenido](content-page.md). Los usuarios configuran algunos aspectos de la aplicación Microsoft Teams mediante la página de configuración y usan esa configuración como parte de lo siguiente:

* Una pestaña de chat de canal o grupo: recopile información de los usuarios y establezca la `contentUrl` de la página de contenido que se va a mostrar.
* Extensión [de mensaje](~/messaging-extensions/what-are-messaging-extensions.md).
* Un [conector de Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="configure-a-channel-or-group-chat-tab"></a>Configuración de una pestaña de chat de canal o grupo

La aplicación debe hacer referencia al [SDK de cliente de JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) y llamar a `microsoft.initialize()`. Las direcciones URL usadas deben ser puntos de conexión HTTPS protegidos y estar disponibles en la nube.

### <a name="example"></a>Ejemplo

En la siguiente imagen se muestra un ejemplo de una página de configuración:

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

El código siguiente es un ejemplo de código correspondiente para la página de configuración:

```html
<head>
    <script src='https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
</head>
<body>
    <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
    <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
    <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

    <script>
        microsoftTeams.initialize();
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.settings.setSettings({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/gray",
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.settings.setSettings({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/red",
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let gr = document.getElementById("gray").style;
        let rd = document.getElementById("red").style;

        const colorClickGray = () => {
            gr.display = "block";
            rd.display = "none";
            microsoftTeams.settings.setValidityState(true);
            saveGray()
        }

        const colorClickRed = () => {
            rd.display = "block";
            gr.display = "none";
            microsoftTeams.settings.setValidityState(true);
            saveRed();
        }
    </script>
    ...
</body>
```

Elija los botones **Seleccionar gris** o **Seleccionar rojo** en la página de configuración para mostrar el contenido de la pestaña con un icono gris o rojo.

En la imagen siguiente se muestra el contenido de la pestaña con el icono **Gris** seleccionado:

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

En la imagen siguiente se muestra el contenido de la pestaña con el icono **Rojo** seleccionado:

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

Al elegir los desencadenadores `saveGray()` de botón adecuados o `saveRed()`, se invoca lo siguiente:

* Establézcalo en `settings.setValidityState(true)` true.
* Se desencadena el `microsoftTeams.settings.registerOnSaveHandler()` controlador de eventos.
* **Guardar** en la página de configuración de la aplicación, está habilitado.

El código de la página de configuración informa Teams que se cumplen los requisitos de configuración y que la instalación puede continuar. Cuando el usuario selecciona **Guardar**, se establecen los parámetros de `settings.setSettings()` , tal y como se define en la `Settings` interfaz. Para obtener más información, consulte [la interfaz de configuración](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true). `saveEvent.notifySuccess()` se llama a para indicar que la dirección URL de contenido se ha resuelto correctamente.

>[!NOTE]
>
>* Tiene 30 segundos para completar la operación de guardado (la devolución de llamada a registerOnSaveHandler) antes del tiempo de espera. Después del tiempo de espera, aparece un mensaje de error genérico.
>* Si registra un controlador de guardado mediante `microsoftTeams.settings.registerOnSaveHandler()`, la devolución de llamada debe invocar `saveEvent.notifySuccess()` o `saveEvent.notifyFailure()` indicar el resultado de la configuración.
>* Si no registra un controlador de guardado, la `saveEvent.notifySuccess()` llamada se realiza automáticamente cuando el usuario selecciona **Guardar**.

### <a name="get-context-data-for-your-tab-settings"></a>Obtención de datos de contexto para la configuración de la pestaña

La pestaña requiere información contextual para mostrar el contenido pertinente. La información contextual mejora aún más el atractivo de la pestaña al proporcionar una experiencia de usuario más personalizada.

Para obtener más información sobre las propiedades usadas para la configuración de tabulación, consulte [interfaz de contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true). Recopile los valores de las variables de datos de contexto de las dos maneras siguientes:

* Inserte marcadores de posición de cadena de consulta url en el manifiesto `configurationURL`.

* Use el método [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)`microsoftTeams.getContext((context) =>{})`.

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insertar marcadores de posición en `configurationUrl`

Agregue marcadores de posición de interfaz de contexto a la base `configurationUrl`. Por ejemplo:

##### <a name="base-url"></a>Base URL

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>Dirección URL base con cadenas de consulta

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

Después de cargar la página, Teams actualiza los marcadores de posición de cadena de consulta con los valores pertinentes. Incluya lógica en la página de configuración para recuperar y usar esos valores. Para obtener más información sobre cómo trabajar con cadenas de consulta url, consulte [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) en MDN Web Docs. En el ejemplo de código siguiente se proporciona la manera de extraer un valor de la `configurationUrl` propiedad :

```html
<script>
   microsoftTeams.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Uso de la `getContext()` función para recuperar el contexto

La `microsoftTeams.getContext((context) => {})` función recupera la [interfaz de contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) cuando se invoca.

El código siguiente proporciona un ejemplo de cómo agregar esta función a la página de configuración para recuperar valores de contexto:

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    microsoftTeams.getContext((context) =>{
        let userId = document.getElementById('user');
        userId.innerHTML = context.userPrincipalName;
    });
</script>
...
```

## <a name="context-and-authentication"></a>Contexto y autenticación

Autentíquese antes de permitir que un usuario configure la aplicación. De lo contrario, el contenido podría incluir orígenes que tengan sus protocolos de autenticación. Para obtener más información, consulte [autenticación de un usuario en una pestaña de Microsoft Teams](~/tabs/how-to/authentication/auth-flow-tab.md). Use información de contexto para construir las direcciones URL de página de autorización y solicitudes de autenticación. Asegúrese de que todos los dominios usados en las páginas de pestaña aparecen en la `manifest.json` matriz y `validDomains` .

## <a name="modify-or-remove-a-tab"></a>Modificar o quitar una pestaña

Establezca la propiedad `true`del `canUpdateConfiguration` manifiesto en , que permite a los usuarios modificar, volver a configurar o cambiar el nombre de una pestaña de canal o grupo. Además, indique lo que sucede con el contenido cuando se quita una pestaña, incluyendo una página de opciones de eliminación en la aplicación y estableciendo un valor para la `removeUrl` propiedad en la `setSettings()` configuración. El usuario puede desinstalar pestañas personales, pero no puede modificarlas. Para obtener más información, vea [Crear una página de eliminación para la pestaña](~/tabs/how-to/create-tab-pages/removal-page.md).

`setSettings()` Microsoft Teams configuración para la página de eliminación:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a>Clientes móviles

Si decide que la pestaña de canal o grupo aparezca en el Teams clientes móviles, la `setSettings()` configuración debe tener un valor para `websiteUrl`. Para obtener más información, consulte [guía para pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una página de eliminación para la pestaña](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>Vea también

* [pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
* [Creación de una página de contenido](~/tabs/how-to/create-tab-pages/content-page.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
