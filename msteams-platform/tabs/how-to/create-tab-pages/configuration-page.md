---
title: Creación de una página de configuración
author: surbhigupta
description: Obtenga información sobre cómo crear una página de configuración para configurar un canal o un chat de grupo para la configuración, como la obtención de datos de contexto, la inserción de marcadores de posición y la autenticación mediante ejemplos de código.
keywords: canal de grupo de pestañas de teams configurable
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: ec1a479421b7439db7a5492a059d470bd2d7024e
ms.sourcegitcommit: 6f1bd36b1071e256bdc14e6ccb31dfdda9ca6d6b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/13/2022
ms.locfileid: "66048979"
---
# <a name="create-a-configuration-page"></a>Creación de una página de configuración

Una página de configuración es un tipo especial de [página de contenido](content-page.md). Los usuarios configuran algunos aspectos de la aplicación de Microsoft Teams mediante la página de configuración y usan esa configuración como parte de lo siguiente:

* Una pestaña de chat de canal o grupo: recopila información de los usuarios y establece el `contentUrl` de la página de contenido que se va a mostrar.
* Una [extensión de mensaje](~/messaging-extensions/what-are-messaging-extensions.md)
* Un [Conector de Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

[!INCLUDE [sdk-include](~/includes/sdk-include.md)].

## <a name="configure-a-channel-or-group-chat-tab"></a>Configurar una pestaña de chat de canal o grupo

La aplicación debe hacer referencia al [SDK de cliente de JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) y llamar a `app.initialize()`. Las direcciones URL usadas deben ser puntos de conexión HTTPS protegidos y estar disponibles en la nube.

### <a name="example"></a>Ejemplo

En la imagen siguiente se muestra un ejemplo de una página de configuración:

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

El código siguiente es un ejemplo de código correspondiente para la página de configuración:

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<head>
    <script src='https://statics.teams.cdn.office.net/sdk/v2.0.0/js/MicrosoftTeams.min.js'></script>
</head>
<body>
    <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
    <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
    <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

    <script>
        app.initialize();
        let saveGray = () => {
            pages.config.registerOnSaveHandler((saveEvent) => {
                const configPromise = pages.config.setConfig({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/gray",
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                configPromise.
                    then((result) => {saveEvent.notifySuccess()}).
                    catch((error) => {saveEvent.notifyFailure("failure message")});
            });
        }

        let saveRed = () => {
            pages.config.registerOnSaveHandler((saveEvent) => {
                const configPromise = pages.config.setConfig({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/red",
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                configPromise.
                    then((result) => {saveEvent.notifySuccess();}).
                    catch((error) => {saveEvent.notifyFailure("failure message")});
            });
        }

        let gr = document.getElementById("gray").style;
        let rd = document.getElementById("red").style;

        const colorClickGray = () => {
            gr.display = "block";
            rd.display = "none";
            pages.config.setValidityState(true);
            saveGray()
        }

        const colorClickRed = () => {
            rd.display = "block";
            gr.display = "none";
            pages.config.setValidityState(true);
            saveRed();
        }
    </script>
    ...
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***
Elija los botones **Seleccionar gris** o **Seleccionar rojo** en la página de configuración para mostrar el contenido de la pestaña con un icono gris o rojo.

En la imagen siguiente se muestra el contenido de la pestaña con el icono **Gris** seleccionado:

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

En la imagen siguiente se muestra el contenido de la pestaña con el icono **Rojo** seleccionado:

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

Al elegir los desencadenadores `saveGray()` de botón adecuados o `saveRed()`, se invoca lo siguiente:

* Establezca `pages.config.setValidityState(true)` en true.
* Se desencadena el `pages.config.registerOnSaveHandler()` controlador de eventos.
* **Guardar** en la página de configuración de la aplicación, está habilitado.

El código de la página de configuración informa a Teams de que se cumplen los requisitos de configuración y que la instalación puede continuar. Cuando el usuario selecciona **Guardar**, se establecen los parámetros de `pages.config.setConfig()`, tal y como se define en la interfaz `Config`. Para obtener más información, consulte [la interfaz de configuración](/javascript/api/@microsoft/teams-js/pages.config?). `saveEvent.notifySuccess()` se llama para indicar que la dirección URL de contenido se ha resuelto correctamente.

>[!NOTE]
>
>* Tiene 30 segundos para completar la operación de guardado (la devolución de llamada para registerOnSaveHandler) antes del tiempo de espera. Después del tiempo de espera, aparece un mensaje de error genérico.
>* Si registra un controlador de guardado mediante `registerOnSaveHandler()`, la devolución de llamada debe invocar `saveEvent.notifySuccess()` o `saveEvent.notifyFailure()` para indicar el resultado de la configuración.
>* Si no registra un controlador de guardado, la llamada `saveEvent.notifySuccess()` se realiza automáticamente cuando el usuario selecciona **Guardar**.

### <a name="get-context-data-for-your-tab-settings"></a>Obtener datos de contexto para la configuración de la pestaña

La pestaña requiere información contextual para mostrar contenido relevante. La información contextual mejora aún más el atractivo de la pestaña al proporcionar una experiencia de usuario más personalizada.

Para obtener más información sobre las propiedades usadas para la configuración de pestañas, vea [interfaz de contexto](/javascript/api/@microsoft/teams-js/app.context?view=msteams-client-js-latest&preserve-view=true). Recopile los valores de las variables de datos de contexto de las dos maneras siguientes:

* Inserte marcadores de posición de cadena de consulta url en el `configurationURL` del manifiesto.

* Use el método [SDK de Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)`app.getContext()`.

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insertar marcadores de posición en el `configurationUrl`

Agregue marcadores de posición de interfaz de contexto a la base `configurationUrl`. Por ejemplo:

##### <a name="base-url"></a>Dirección URL base

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

Después de cargar la página, Teams actualiza los marcadores de posición de cadena de consulta con los valores pertinentes. Incluya lógica en la página de configuración para recuperar y usar esos valores. Para obtener más información sobre cómo trabajar con cadenas de consulta url, consulte [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) en MDN Web Docs. En el ejemplo de código siguiente se proporciona la manera de extraer un valor de la propiedad`configurationUrl`:

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<script>
   app.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Usar la función `getContext()` para recuperar el contexto

La `app.getContext()` función devuelve una promesa que se resuelve con el objeto de [interfaz de contexto](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest&preserve-view=true) .

El código siguiente proporciona un ejemplo de cómo agregar esta función a la página de configuración para recuperar valores de contexto:

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    const contextPromise = app.getContext();
    contextPromise.
        then((context) => {
            let userId = document.getElementById('user');
            userId.innerHTML = context.user.userPrincipalName;
        }).
        catch((error) => {/*Unsuccessful operation*/});
</script>
...
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***

## <a name="context-and-authentication"></a>Contexto y autenticación

Autentíquese antes de permitir que un usuario configure la aplicación. De lo contrario, el contenido podría incluir orígenes que tengan sus protocolos de autenticación. Para obtener más información, consulte [autenticación de un usuario en una pestaña de Microsoft Teams](~/tabs/how-to/authentication/auth-flow-tab.md). Use información de contexto para construir las direcciones URL de página de autorización y solicitudes de autenticación. Asegúrese de que todos los dominios usados en las páginas de pestañas aparecen en la matriz `manifest.json` y `validDomains`.

## <a name="modify-or-remove-a-tab"></a>Modificar o quitar una pestaña

Establezca la propiedad del `canUpdateConfiguration` manifiesto en `true`. Permite a los usuarios modificar, volver a configurar o cambiar el nombre de una pestaña de canal o grupo. Informe al usuario sobre el impacto en el contenido cuando se quita una pestaña. Para ello, incluya una página de opciones de eliminación en la aplicación y establezca un valor para la `removeUrl` propiedad en la `setConfig()` configuración (anteriormente `setSettings()`). El usuario puede desinstalar pestañas personales, pero no puede modificarlas. Para obtener más información, vea [crear una página de eliminación para la pestaña](~/tabs/how-to/create-tab-pages/removal-page.md).

`setConfig()` Microsoft Teams (anteriormente `setSettings()`) configuración para la página de eliminación:

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
const configPromise = pages.config.setConfig({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
configPromise.
    then((result) => {/*Successful operation*/).
    catch((error) => {/*Unsuccessful operation*/});
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

***

## <a name="mobile-clients"></a>Clientes móviles

Si decide que su pestaña de canal o grupo aparezca en los clientes móviles de Teams, la configuración de `setConfig()` debe tener un valor para `websiteUrl`. Para obtener más información, consulte las [instrucciones para pestañas en móviles](~/tabs/design/tabs-mobile.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una página de eliminación para la pestaña](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>Consulte también

* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de grupo o canal personalizado](~/tabs/how-to/create-channel-group-tab.md)
* [Creación de una página de contenido](~/tabs/how-to/create-tab-pages/content-page.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
