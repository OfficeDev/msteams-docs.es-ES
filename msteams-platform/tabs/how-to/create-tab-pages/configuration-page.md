---
title: Creación de una página de configuración
author: surbhigupta
description: cómo crear una página de configuración
keywords: Canal de grupo de pestañas de teams configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 041ef78fcc6e3f5203842e808949e86e8dd3aae4
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069213"
---
# <a name="create-a-configuration-page"></a>Creación de una página de configuración

Una página de configuración es un tipo especial de [página de contenido](content-page.md). Los usuarios configuran algunos aspectos de la aplicación Microsoft Teams con la página de configuración y la usan como parte de lo siguiente:

* Una pestaña de chat de canal o grupo: recopilar información de los usuarios y establecer la `contentUrl` página de contenido que se mostrará.
* Una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md).
* Un [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="configuring-a-channel-or-group-chat-tab"></a>Configuración de una pestaña de chat de grupo o canal

La aplicación debe hacer referencia al [sdk Microsoft Teams cliente de JavaScript y](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) llamar a `microsoft.initialize()` . Además, las direcciones URL usadas deben estar protegidas con puntos de conexión HTTPS y disponibles desde la nube. 

### <a name="example"></a>Ejemplo

En la siguiente imagen se muestra un ejemplo de una página de configuración: 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

El código correspondiente para la página de configuración se muestra en la siguiente sección:

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
    </body>
...
```

Elija seleccionar **el botón Gris** o **Seleccionar** rojo en la página de configuración para mostrar el contenido de la pestaña con un icono gris o rojo. 

La siguiente imagen muestra el contenido de la pestaña con el icono gris:

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

La siguiente imagen muestra el contenido de la pestaña con el icono rojo:

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

Elegir el botón relativo desencadena `saveGray()` o , e invoca lo `saveRed()` siguiente:

1. Se `settings.setValidityState(true)` establece en true.
1. Se `microsoftTeams.settings.registerOnSaveHandler()` desencadena el controlador de eventos.
1. El **botón** Guardar de la página de configuración de la aplicación, cargado en Teams, está habilitado.

El código de página de configuración informa a Teams que los requisitos de configuración se cumplen y la instalación puede continuar. Cuando el usuario selecciona **Guardar**, los parámetros de `settings.setSettings()` se establecen, según lo define la `Settings` interfaz. Para obtener más información, [vea Configuración interfaz](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true). En el último paso, se llama para indicar que la dirección URL de `saveEvent.notifySuccess()` contenido se ha resuelto correctamente.

>[!NOTE]
>
>* Si registra un controlador de guardado mediante , la devolución de llamada debe invocar o indicar `microsoftTeams.settings.registerOnSaveHandler()` el resultado de la `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` configuración.
>* Si no registra un controlador de guardado, la llamada se realiza `saveEvent.notifySuccess()` automáticamente cuando el usuario selecciona **Guardar**.

### <a name="get-context-data-for-your-tab-settings"></a>Obtener datos de contexto para la configuración de la pestaña

Puede que su pestaña necesite información contextual para mostrar contenido relevante. La información contextual mejora aún más el atractivo de la pestaña al proporcionar una experiencia de usuario más personalizada.

Para obtener más información sobre las propiedades usadas para la configuración de pestañas, vea [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true). Recopile los valores de las variables de datos de contexto de las dos maneras siguientes:

1. Inserte marcadores de posición de cadena de consulta url en el `configurationURL` manifiesto .

1. Use el [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insertar marcadores de posición en el `configurationUrl`

Agregue marcadores de posición de interfaz de contexto a la base `configurationUrl` . Por ejemplo:

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

Después de cargar la página, el Teams actualiza los marcadores de posición de cadena de consulta con valores relevantes. Incluya lógica en la página de configuración para recuperar y usar esos valores. Para obtener más información sobre cómo trabajar con cadenas de consulta de dirección URL, vea [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. En el siguiente ejemplo se describe la forma de extraer un valor de la `configurationUrl` propiedad:

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Usar la `getContext()` función para recuperar contexto

La `microsoftTeams.getContext((context) => {})` función recupera la interfaz context [cuando](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) se invoca. Agregue esta función a la página de configuración para recuperar valores de contexto:

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

 Autentica antes de permitir que un usuario configure la aplicación. De lo contrario, el contenido podría incluir orígenes que tienen sus protocolos de autenticación. Para obtener más información, vea [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use información de contexto para crear las direcciones URL de la página de autorización y las solicitudes de autenticación.
Asegúrese de que todos los dominios usados en las páginas de pestañas se enumeran en la `manifest.json` matriz `validDomains` and.

## <a name="modify-or-remove-a-tab"></a>Modificar o quitar una pestaña

Las opciones de eliminación admitidas refinan aún más la experiencia del usuario. Establezca la propiedad del manifiesto en , que permite a los usuarios `canUpdateConfiguration` modificar, reconfigurar o cambiar el nombre de una pestaña de grupo `true` o canal. Además, indica lo que sucede con el contenido cuando se quita una pestaña, incluyendo una página de opciones de eliminación en la aplicación y estableciendo un valor para la propiedad `removeUrl` en la  `setSettings()` configuración. El usuario puede desinstalar las pestañas Personales, pero no puede modificarlas. Para obtener más información, vea [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).

Microsoft Teams setSettings() para la página de eliminación:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a>Clientes móviles

Si decide que la pestaña canal o grupo aparezca en el Teams móviles, la configuración `setSettings()` debe tener un valor para `websiteUrl` . Para obtener más información, consulte [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).
