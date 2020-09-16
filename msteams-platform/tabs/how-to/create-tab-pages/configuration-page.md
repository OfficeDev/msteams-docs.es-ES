---
title: Creación de una página de configuración
author: laujan
description: Cómo crear una página de configuración
keywords: canal de grupo de pestañas de Teams configurable
ms.topic: conceptualF
ms.author: lajanuar
ms.openlocfilehash: 6288fc8c296ebf0aa85ffe8e08234e5faf22a1ef
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819028"
---
# <a name="create-a-configuration-page"></a>Creación de una página de configuración

Una página de configuración es un tipo especial de [Página de contenido](content-page.md) que permite a los usuarios configurar algún aspecto de la aplicación de Teams. Normalmente se usan como parte de:

* Una pestaña de canal o de chat de Grupo: la página de configuración permite recopilar información de los usuarios y establecer la `contentUrl` de la página de contenido que se va a mostrar.
* Una [extensión de mensajería](~/messaging-extensions/what-are-messaging-extensions.md)
* Un [conector de Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>Configuración de una pestaña de chat de grupo o de canal

Una página de configuración informa A la página de contenido sobre cómo debe representarse. La aplicación debe hacer referencia al [SDK del cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) y llamar a `microsoft.initialize()` . Además, las direcciones URL deben ser extremos HTTPS seguros y disponibles en la nube. A continuación se muestra un ejemplo de página de configuración.

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

Aquí, al usuario se le presentan dos botones de opción, **Seleccione gris** o **Seleccione rojo** para mostrar el contenido de la pestaña con un icono rojo o gris. Elegir el botón relativo se activa `saveGray()` o `saveRed()` llama a lo siguiente:

1. El `settings.setValidityState(true)` está establecido en true.
1. `microsoftTeams.settings.registerOnSaveHandler()`Se desencadena el controlador de eventos.
1. El botón **Guardar** de la página Configuración de la aplicación, cargado en Microsoft Teams, está habilitado.

Este código permite que los equipos sepan que se han cumplido los requisitos de configuración y que la instalación puede continuar. Al **Guardar**, `settings.setSettings()` se configuran los parámetros de, tal y como se define en la `Settings` interfaz, para la instancia actual (consulte la [interfaz de configuración](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ). Por último, `saveEvent.notifySuccess()` se llama a para indicar que la dirección URL del contenido se ha resuelto correctamente.

>[!NOTE]
>
>* Si se registró un controlador de guardado con `microsoftTeams.settings.registerOnSaveHandler()` , la devolución de llamada debe invocar `saveEvent.notifySuccess()` o `saveEvent.notifyFailure()` para indicar el resultado de la configuración.
>* Si no se registró ningún controlador de guardado, la `saveEvent.notifySuccess()` llamada se realiza automáticamente inmediatamente después de que el usuario seleccione el botón **Guardar** .

### <a name="get-context-data-for-your-tab-settings"></a>Obtener datos de contexto para la configuración de pestañas

Es posible que la pestaña requiera información contextual para mostrar contenido relevante. La información contextual puede mejorar aún más el atractivo de su pestaña proporcionando una experiencia de usuario más personalizada.

La [interfaz de contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) de Microsoft Teams define las propiedades que se pueden usar para la configuración de pestañas. Puede recopilar los valores de las variables de datos de contexto de dos maneras:

1. Insertar marcadores de posición de cadena de consulta de URL en el manifiesto `configurationURL` .

1. Usar el método de [Team SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` .

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insertar marcadores de posición en el `configurationURL`

Los marcadores de posición de la interfaz de contexto se pueden agregar a la base `configurationUrl` . Por ejemplo:

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

Una vez que se haya cargado la página, los marcadores de posición de la cadena de consulta se actualizarán en Microsoft Teams con los valores relevantes. Puede incluir lógica en la página de configuración para recuperar y usar esos valores. Para obtener más información sobre cómo trabajar con cadenas de consulta de dirección URL, vea [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) en los documentos web de MDN. A continuación, se muestra un ejemplo de cómo extraer un valor de la `configurationURL` propiedad anterior:

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Usar la `getContext()` función para recuperar el contexto

Cuando se invoca, la `microsoftTeams.getContext((context) => {})` función recupera la [interfaz de contexto](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest). Puede Agregar esta función a la página de configuración para recuperar los valores de contexto:

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

Es posible que necesite autenticación antes de permitir que un usuario configure la aplicación o que el contenido pueda incluir orígenes que tengan sus propios protocolos de autenticación. Consulte [autenticar a un usuario en una pestaña de Microsoft teams la información de](~/tabs/how-to/authentication/auth-flow-tab.md) contexto se puede usar para ayudar a construir solicitudes de autenticación y direcciones URL de la página de autorización.
Asegúrese de que todos los dominios usados en las páginas de pestañas se enumeran en la `manifest.json` `validDomains` matriz.

## <a name="modify-or-remove-a-tab"></a>Modificación o eliminación de una pestaña

Las opciones de eliminación admitidas pueden restringir aún más la experiencia del usuario. Puede habilitar a los usuarios para modificar, reconfigurar o cambiar el nombre de una pestaña de grupo o canal al establecer la propiedad del manifiesto `canUpdateConfiguration` en `true` .  Además, puede designar lo que ocurre con el contenido cuando se quita una pestaña incluyendo una página Opciones de eliminación en la aplicación y estableciendo un valor para la `removeUrl` propiedad en la  `setSettings()` configuración (vea a continuación). Las pestañas personales no se pueden modificar, pero el usuario puede desinstalarlas. Para obtener más información, vea [crear una página de eliminación para la ficha](~/tabs/how-to/create-tab-pages/removal-page.md).

## <a name="mobile-clients"></a>Clientes móviles

Si elige que la ficha canal/grupo aparezca en los clientes móviles de Teams, la `setSettings()` configuración debe tener un valor para la `websiteUrl` propiedad (vea a continuación). Pronto se ofrecerá compatibilidad completa para las pestañas en los clientes móviles. Para preparar la actualización, debe seguir las [instrucciones para las pestañas de dispositivos móviles](~/tabs/design/tabs-mobile.md) al crear las pestañas.

Configuración de Microsoft Teams setSettings () para la página de eliminación o los clientes móviles:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
