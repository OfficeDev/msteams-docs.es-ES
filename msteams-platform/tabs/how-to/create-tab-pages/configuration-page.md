---
title: Creación de una página de configuración
author: laujan
description: cómo crear una página de configuración
keywords: equipos pestañas canal de grupo configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: aeab1cf96d1e875db79d9143fefd0e46348f585a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566687"
---
# <a name="create-a-configuration-page"></a>Creación de una página de configuración

Una página de configuración es un tipo especial de página de [contenido.](content-page.md) Los usuarios configuran algunos aspectos de la aplicación Microsoft Teams mediante la página de configuración y usan esa configuración como parte de lo siguiente:

* Una pestaña de chat de canal o grupo: recopile información de los usuarios y establezca la `contentUrl` página de contenido que se va a mostrar.
* Una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md).
* Un [conector de Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="configuring-a-channel-or-group-chat-tab"></a>Configuración de un canal o pestaña de chat de grupo

La aplicación debe hacer referencia al [SDK de cliente de JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) y llamar a `microsoft.initialize()` . Además, las direcciones URL utilizadas deben estar protegidas y estar disponibles en la nube. 

### <a name="example"></a>Ejemplo

Un ejemplo de una página de configuración se muestra en la siguiente imagen: 

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

Elija **el** botón Seleccionar gris o **Seleccionar rojo** en la página de configuración para mostrar el contenido de la pestaña con un icono gris o rojo. 

La siguiente imagen muestra el contenido de la pestaña con el icono gris:

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

La siguiente imagen muestra el contenido de la pestaña con el icono rojo:

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

La elección del botón relativo desencadena `saveGray()` uno o varios e invoca lo `saveRed()` siguiente:

1. El `settings.setValidityState(true)` está establecido en true.
1. `microsoftTeams.settings.registerOnSaveHandler()`Se desencadena el controlador de eventos.
1. El botón **Guardar** de la página de configuración de la aplicación, cargado en Teams, está habilitado.

El código de página de configuración informa a la Teams que se cumplen los requisitos de configuración y la instalación puede continuar. Cuando el usuario selecciona **Guardar,** se establecen los parámetros de `settings.setSettings()` la interfaz, tal como se `Settings` define. Para obtener más información, consulte [Configuración interfaz](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true). En el último paso, `saveEvent.notifySuccess()` se llama para indicar que la dirección URL del contenido se ha resuelto correctamente.

>[!NOTE]
>
>* Si registra un controlador de guardado mediante `microsoftTeams.settings.registerOnSaveHandler()` , la devolución de llamada debe invocar o indicar el resultado de la `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` configuración.
>* Si no registra un controlador de guardado, la `saveEvent.notifySuccess()` llamada se realiza automáticamente cuando el usuario selecciona **Guardar**.

### <a name="get-context-data-for-your-tab-settings"></a>Obtenga datos de contexto para la configuración de la pestaña

Puede que su pestaña necesite información contextual para mostrar contenido relevante. La información contextual mejora aún más el atractivo de su pestaña al proporcionar una experiencia de usuario más personalizada.

Para obtener más información sobre las propiedades utilizadas para la configuración de pestañas, consulte [Interfaz de contexto](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true). Recopile los valores de las variables de datos de contexto de las dos maneras siguientes:

1. Inserte marcadores de posición de cadena de consulta de DIRECCIÓN URL en el `configurationURL` manifiesto.

1. Utilice el método [SDK de Teams.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insertar marcadores de posición en el `configurationUrl`

Agregue marcadores de posición de interfaz de contexto a la `configurationUrl` base. Por ejemplo:

##### <a name="base-url"></a>Base URL

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>URL base con cadenas de consulta

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

Después de cargar la página, el Teams actualiza los marcadores de posición de cadena de consulta con valores relevantes. Incluya lógica en la página de configuración para recuperar y usar esos valores. Para obtener más información sobre cómo trabajar con cadenas de consulta de DIRECCIÓN URL, vea [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) en MDN Web Docs. En el ejemplo siguiente se describe la forma de extraer un valor de la `configurationUrl` propiedad:

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Utilice la `getContext()` función para recuperar el contexto

La `microsoftTeams.getContext((context) => {})` función recupera la interfaz [Context](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) cuando se invoca. Agregue esta función a la página de configuración para recuperar valores de contexto:

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

 Autentique antes de permitir que un usuario configure la aplicación. De lo contrario, el contenido podría incluir orígenes que tienen sus protocolos de autenticación. Para obtener más información, consulte [Autenticar a un usuario en una pestaña Microsoft Teams](~/tabs/how-to/authentication/auth-flow-tab.md). Use información de contexto para construir las solicitudes de autenticación y las direcciones URL de página de autorización.
Asegúrese de que todos los dominios utilizados en las páginas de pestañas se enumeran en la `manifest.json` matriz y `validDomains` la matriz.

## <a name="modify-or-remove-a-tab"></a>Modificar o eliminar una pestaña

Las opciones de eliminación compatibles refinan aún más la experiencia del usuario. Establezca la propiedad del manifiesto `canUpdateConfiguration` en , que permite a los usuarios `true` modificar, reconfigurar o cambiar el nombre de un grupo o canal pestaña. Además, indique lo que sucede con el contenido cuando se quita una pestaña, incluyendo una página de opciones de eliminación en la aplicación y estableciendo un valor para la `removeUrl` propiedad en la  `setSettings()` configuración. El usuario puede desinstalar las pestañas Personal, pero no puede modificarlas. Para obtener más información, consulte [Crear una página de eliminación para la pestaña](~/tabs/how-to/create-tab-pages/removal-page.md).

Microsoft Teams configuración setSettings() para la página de eliminación:

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

Si decide que la pestaña de canal o grupo aparezca en la Teams clientes móviles, la `setSettings()` configuración debe tener un valor para la `websiteUrl` propiedad. Para obtener más información, consulte [instrucciones para pestañas en dispositivos móviles.](~/tabs/design/tabs-mobile.md)
