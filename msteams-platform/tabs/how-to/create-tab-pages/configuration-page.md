---
title: Creación de una página de configuración
author: laujan
description: cómo crear una página de configuración
keywords: Canal de grupo de pestañas de teams configurable
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2544454fd06348fa41269f3a8fd57cc71a07d140
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886740"
---
# <a name="create-a-configuration-page"></a>Creación de una página de configuración

Una página de configuración es un tipo especial de [página de contenido.](content-page.md) Los usuarios configuran algunos aspectos de la aplicación de Microsoft Teams mediante la página de configuración y usan esa configuración como parte de lo siguiente:

* Una pestaña de chat de grupo o canal: recopilar información de los usuarios y establecer la `contentUrl` página de contenido que se mostrará.
* Una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md)
* Un [conector de Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>Configurar una pestaña de chat en grupo o canal

La aplicación debe hacer referencia al [SDK del cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams y llamar `microsoft.initialize()` a . Además, las direcciones URL usadas deben ser puntos de conexión HTTPS seguros y disponibles desde la nube. El siguiente código es un ejemplo de una página de configuración:

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

Elija el **botón Seleccionar gris** o Seleccionar rojo en la página de configuración para mostrar el contenido de la pestaña con un icono gris o rojo.  Elegir el botón relativo se ejecuta `saveGray()` o `saveRed()` invoca lo siguiente:

1. Se `settings.setValidityState(true)` establece en true.
1. Se `microsoftTeams.settings.registerOnSaveHandler()` desencadena el controlador de eventos.
1. El **botón** Guardar de la página de configuración de la aplicación, cargado en Teams, está habilitado.

El código de la página de configuración informa a Teams de que se cumplen los requisitos de configuración y la instalación puede continuar. Cuando el usuario selecciona **Guardar**, se establecen los parámetros, según `settings.setSettings()` lo define la `Settings` interfaz. Para obtener más información, vea [La interfaz de configuración.](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true) En el último paso, se llama para indicar que la dirección URL de `saveEvent.notifySuccess()` contenido se ha resuelto correctamente.

>[!NOTE]
>
>* Si registra un controlador de guardado mediante , la devolución de llamada debe invocar o indicar `microsoftTeams.settings.registerOnSaveHandler()` el resultado de la `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` configuración.
>* Si no registra un controlador de guardado, la llamada se realiza `saveEvent.notifySuccess()` automáticamente cuando el usuario selecciona **Guardar**.

### <a name="get-context-data-for-your-tab-settings"></a>Obtener datos de contexto para la configuración de la pestaña

Es posible que la pestaña requiera información contextual para mostrar contenido relevante. La información contextual mejora aún más el atractivo de la pestaña al proporcionar una experiencia de usuario más personalizada.

Para obtener más información sobre las propiedades usadas para la configuración de pestañas, vea [la interfaz de contexto.](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) Recopile los valores de las variables de datos de contexto de las dos maneras siguientes:

1. Inserte marcadores de posición de cadena de consulta DE URL en el `configurationURL` manifiesto.

1. Use el método [del SDK de Teams.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insertar marcadores de posición en el `configurationUrl`

Agregue marcadores de posición de interfaz de contexto a la `configurationUrl` base. Por ejemplo:

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

Después de cargar la página, Teams actualiza los marcadores de posición de cadena de consulta con valores relevantes. Incluya lógica en la página de configuración para recuperar y usar esos valores. Para obtener más información sobre cómo trabajar con cadenas de consulta url, vea [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) en MDN Web Docs. En el siguiente ejemplo se describe la forma de extraer un valor de la `configurationUrl` propiedad:

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

La `microsoftTeams.getContext((context) => {})` función recupera la interfaz de contexto [cuando](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) se invoca. Agregue esta función a la página de configuración para recuperar valores de contexto:

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

 Autentica antes de permitir que un usuario configure la aplicación. De lo contrario, el contenido podría incluir orígenes que tengan sus protocolos de autenticación. Para obtener más información, vea [Autenticar a un usuario en una pestaña de Microsoft Teams.](~/tabs/how-to/authentication/auth-flow-tab.md) Use la información de contexto para crear las solicitudes de autenticación y las direcciones URL de la página de autorización.
Asegúrese de que todos los dominios usados en las páginas de pestañas se enumeran en la `manifest.json` `validDomains` matriz y.

## <a name="modify-or-remove-a-tab"></a>Modificar o quitar una pestaña

Las opciones de eliminación admitidas refinan aún más la experiencia del usuario. Establezca la propiedad del manifiesto en , que permite a los usuarios `canUpdateConfiguration` modificar, reconfigurar o cambiar el nombre de una `true` pestaña de grupo o canal. Además, indica lo que sucede con el contenido cuando se quita una pestaña, incluyendo una página de opciones de eliminación en la aplicación y estableciendo un valor para la propiedad `removeUrl` en la  `setSettings()` configuración. Para obtener más información, vea [Clientes móviles.](#mobile-clients) El usuario puede desinstalar las pestañas Personales, pero no modificarlas. Para obtener más información, vea [Crear una página de eliminación para la pestaña](~/tabs/how-to/create-tab-pages/removal-page.md).

## <a name="mobile-clients"></a>Clientes móviles

Si decide que la pestaña de canal o grupo aparezca en los clientes móviles de Teams, la configuración debe `setSettings()` tener un valor para la `websiteUrl` propiedad. Para obtener más información, [vea las instrucciones para pestañas en dispositivos móviles.](~/tabs/design/tabs-mobile.md)

Configuración de Microsoft Teams setSettings() para la página de eliminación o clientes móviles:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
