---
title: Crear Conectores de Office 365
author: laujan
description: En este módulo, aprenderá a empezar a trabajar con conectores de Office 365 y a agregar conector a la aplicación Teams en Microsoft Teams.
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: bb4bd02553ebb49752fa6450cd0f94f41dcc7ac8
ms.sourcegitcommit: 217025a61ed9c3b76b507fe95563142abc6d0318
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2022
ms.locfileid: "67363487"
---
# <a name="create-office-365-connectors"></a>Crear Conectores de Office 365

Con las aplicaciones de Microsoft Teams, puede agregar su conector de Office 365 existente o compilar uno nuevo en Teams. Para obtener más información, vea [cómo compilar su propio conector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).

Consulte el siguiente vídeo para obtener información sobre cómo crear un conector de Office 365:
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OIzv]
<br>

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="add-a-connector-to-teams-app"></a>Agregar un conector a la aplicación de Teams

Puede crear un [paquete](~/concepts/build-and-test/apps-package.md) y [publicar](~/concepts/deploy-and-publish/apps-publish.md) el conector como parte del envío de AppSource. Puede distribuir el conector registrado como parte del paquete de la aplicación de Teams. Para obtener información sobre los puntos de entrada de la aplicación de Teams, vea [capacidades](~/concepts/extensibility-points.md). También puede proporcionar el paquete a los usuarios directamente para cargarlo en Teams.

Para distribuir el conector, regístrelo en el [Conectores Panel de control para desarrolladores](https://aka.ms/connectorsdashboard).

Para que un conector funcione solo en Teams, siga las instrucciones para enviar el conector en [el artículo publicar la aplicación en la Tienda Microsoft Teams](~/concepts/deploy-and-publish/appsource/publish.md) . De lo contrario, un conector registrado funciona en todos los productos de Office 365 que admiten aplicaciones, incluidos Outlook y Teams.

> [!IMPORTANT]
> El conector se registra después de seleccionar **Guardar** en el Panel del desarrollador de conectores. Si desea publicar el conector en AppSource, siga las instrucciones de [publicar la aplicación de Microsoft Teams en AppSource](~/concepts/deploy-and-publish/apps-publish.md). Si no desea publicar la aplicación en AppSource, distribúyala directamente a la organización. Después de publicar conectores para su organización, no es necesario realizar ninguna otra acción en el panel del conector.

### <a name="integrate-the-configuration-experience"></a>Cree la base de datos de configuración:

Los usuarios pueden completar toda la experiencia de configuración del conector sin tener que salir del cliente de Teams. Para obtener la experiencia, Teams puede insertar la página de configuración directamente en un iframe. La secuencia de operaciones es la siguiente:

1. El usuario selecciona su conector para iniciar el proceso de configuración.
1. El usuario interactúa con la experiencia web para completar la configuración.
1. El usuario selecciona **Guardar**, que desencadena una devolución de llamada en el código.

    > [!NOTE]
    >
    > * El código puede procesar el evento de guardado recuperando la configuración del webhook. El código almacena el webhook para publicar eventos más adelante.
    > * La experiencia de configuración se carga en línea en Teams.

Puede reutilizar la experiencia de configuración web existente o crear una versión independiente para hospedarla específicamente en Teams. El código debe incluir el SDK de JavaScript de Teams. Esto proporciona a su código acceso a las API para realizar operaciones comunes, como obtener el contexto de usuario, canal o equipo actual, e iniciar flujos de autenticación.

Para integrar la experiencia de la configuración:

> [!NOTE]
> A partir del SDK de cliente de JavaScript (TeamsJS) v.2.0.0 de Teams, las API del espacio de nombres *de configuración* han quedado en desuso en favor de API equivalentes en el espacio de nombres *pages* , incluidas `pages.getConfig()` y otras API del `pages.config` subespacial. Para obtener más información, consulte [Novedades de TeamsJS versión 2.0](../../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20)

1. Para inicializar el SDK, llame a `app.initialize()`.
1. Llame a `pages.config.setValidityState(true)` para habilitar **Guardar**.

    > [!NOTE]
    > Debe llamar a `microsoftTeams.pages.config.setValidityState(true)` como respuesta a la selección del usuario o a la actualización de campos.

1. Registre `microsoftTeams.pages.config.registerOnSaveHandler()` controlador de eventos, al que se llama cuando el usuario selecciona **Guardar**.
1. Llame a `microsoftTeams.pages.config.setConfig()` para guardar la configuración del conector. La configuración guardada también se muestra en el cuadro de diálogo de configuración si el usuario intenta actualizar una configuración existente para el conector.
1. Llame a `microsoftTeams.pages.getConfig()` para capturar las propiedades de webhook, incluida la dirección URL.

    > [!NOTE]
    > Debe llamar a `microsoftTeams.pages.getConfig()` cuando la página se cargue por primera vez en caso de reconfiguración.

1. Registre `microsoftTeams.pages.config.registerOnRemoveHandler()` controlador de eventos, al que se llama cuando el usuario quita el conector.

Este evento ofrece al servicio la oportunidad de realizar cualquier acción de limpieza.

El código siguiente proporciona un código HTML de ejemplo para crear una página de configuración del conector sin el servicio de atención al cliente y el soporte técnico:

```html
<h2>Send notifications when tasks are:</h2>
<div class="col-md-8">
    <section id="configSection">
        <form id="configForm">
            <input type="radio" name="notificationType" value="Create" onclick="onClick()"> Created
            <br>
            <br>
            <input type="radio" name="notificationType" value="Update" onclick="onClick()"> Updated
        </form>
    </section>
</div>

<script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js" integrity="sha384-Q2Z9S56exI6Oz/ThvYaV0SUn8j4HwS8BveGPmuwLXe4CvCUEGlL80qSzHMnvGqee" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="module">
        import {app, pages} from 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js';
        
        function onClick() {
            pages.config.setValidityState(true);
        }

        await app.initialize();
        pages.config.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            await pages.config.setConfig({
                entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                configName: eventType
                });

            pages.getConfig().then(async (config) {
                // We get the Webhook URL from config.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        pages.config.registerOnRemoveHandler(function (removeEvent) {
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

Para autenticar al usuario como parte de la carga de la página, consulte [flujo de autenticación para las pestañas](~/tabs/how-to/authentication/auth-flow-tab.md) para integrar el inicio de sesión cuando la página está incrustada.

> [!NOTE]
> Antes de TeamsJS v.2.0.0, el código debe llamar a `microsoftTeams.authentication.registerAuthenticationHandlers()` con la dirección URL y los métodos de devolución de llamada correctos o incorrectos antes de llamar `authenticate()` a debido a motivos de compatibilidad entre clientes. A partir de TeamsJS v.2.0.0, *registerAuthenticationHandlers* ha quedado en desuso a favor de llamar directamente a [authenticate()](/javascript/api/@microsoft/teams-js/authentication#@microsoft-teams-js-authentication-authenticate) con los parámetros de autenticación necesarios.

#### <a name="getconfig-response-properties"></a>`getConfig` Propiedades de la respuesta

>[!NOTE]
>Los parámetros devueltos por la `getConfig` llamada son diferentes cuando se invoca este método desde una pestaña y difieren de los documentados en la [referencia](/javascript/api/@microsoft/teams-js/pages#@microsoft-teams-js-pages-getconfig).

En la tabla siguiente se proporcionan los parámetros y los detalles de las propiedades de respuesta `getConfig`:

| Parámetros   | Detalles |
|-------------|---------|
| `entityId`       | El identificador de entidad, establecido por el código al llamar a `setConfig()`. |
| `configName`  | El nombre de configuración, según lo establecido por el código al llamar a `setConfig()`. |
| `contentUrl` | Dirección URL de la página de configuración, establecida por el código al llamar a `setConfig()`. |
| `webhookUrl` | Dirección URL del webhook creada para el conector. Use la dirección URL del webhook para PUBLICAR JSON estructurado para enviar tarjetas al canal. El `webhookUrl` solo se devuelve cuando la aplicación devuelve datos correctamente. |
| `appType` | Los valores devueltos pueden ser `mail`, `groups`o `teams` correspondientes a la Office 365 Mail, Office 365 Groups o Teams, respectivamente. |
| `userObjectId` | Identificador único correspondiente al usuario de Office 365 que inició la configuración del conector. Debe protegerse. Este valor se puede usar para asociar al usuario en Office 365, que ha configurado la configuración en el servicio. |

#### <a name="handle-edits"></a>Controlar ediciones

El código debe controlar los usuarios que vuelven para editar una configuración de conector existente. Para ello, llame a `microsoftTeams.pages.config.setConfig()` durante la configuración inicial con los parámetros siguientes:

* `entityId` es el identificador personalizado que representa lo que el usuario ha configurado y comprendido por el servicio.
* `configName` es un nombre que el código de configuración puede recuperar.
* `contentUrl` es una dirección URL personalizada que se carga cuando un usuario edita una configuración de conector existente.

Esta llamada se realiza como parte del controlador de eventos de guardado. A continuación, cuando se cargue el `contentUrl`, el código debe llamar a `getConfig()` para rellenar previamente cualquier configuración o formulario de la interfaz de usuario de configuración.

#### <a name="handle-removals"></a>Control de eliminaciones

Opcionalmente, puede ejecutar un controlador de eventos cuando el usuario quita una configuración de conector existente. Para registrar este controlador, llame a `microsoftTeams.pages.config.registerOnRemoveHandler()`. Este controlador se usa para realizar operaciones de limpieza, como quitar entradas de una base de datos.

### <a name="include-the-connector-in-your-manifest"></a>Incluir el conector en el manifiesto

Descargue el manifiesto de aplicación de *Teams* generado automáticamente desde el Portal para desarrolladores (<https://dev.teams.microsoft.com>). Realice los pasos siguientes antes de probar o publicar la aplicación:

1. [Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).
1. Modifique la parte `icons` del manifiesto para hacer referencia a los nombres de archivo de los iconos en lugar de a las direcciones URL.

El siguiente archivo *manifest.json* contiene los elementos necesarios para probar y enviar la aplicación:

> [!NOTE]
> Reemplace `id` y `connectorId` en el ejemplo siguiente con el GUID del conector.

#### <a name="example-of-manifestjson-with-connector"></a>Ejemplo de manifest.json con conector

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="test-your-connector"></a>Pruebe su conector

Para probar el conector, cárguelo a un equipo con cualquier otra aplicación. Puede crear un paquete .zip mediante el archivo de manifiesto de los dos archivos de icono y del Panel de desarrollador de conectores, modificados como se indica en [Incluir el conector en el manifiesto](#include-the-connector-in-your-manifest).

Después de cargar la aplicación, abra la lista Conectores desde cualquier canal. Desplácese hasta la parte inferior para ver la aplicación en la sección **Cargada**:

![Captura de pantalla de la sección cargada en el cuadro de diálogo Conector](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> El flujo se produce completamente dentro de Teams como una experiencia hospedada.

Para comprobar que `HttpPOST` acción funciona correctamente, [envíe mensajes al conector](~/webhooks-and-connectors/how-to/connectors-using.md).

Siga la [guía paso a paso](../../sbs-teams-connectors.yml) para crear y probar los conectores en Teams.

## <a name="distribute-webhook-and-connector"></a>Distribución de webhook y conector

1. [Configurar un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md#create-an-incoming-webhook) directamente para su equipo.

1. Agregue una [página de configuración](~/webhooks-and-connectors/how-to/connectors-creating.md?#integrate-the-configuration-experience) y publique el webhook entrante en un conector de Office 365.

1. Empaqueta y publica el conector como parte del envío de [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md).

## <a name="code-sample"></a>Ejemplo de código

En la tabla siguiente se proporciona el nombre de ejemplo y su descripción:

|**Ejemplo de nombre** | **Descripción** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Conectores | Conector de Office 365 de ejemplo que genera notificaciones para el canal de Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Ejemplo de conectores genéricos |Código de ejemplo para un conector genérico que es fácil de personalizar para cualquier sistema que admita webhooks.| | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../../sbs-teams-connectors.yml) para crear y probar el conector en Teams.

## <a name="see-also"></a>Vea también

* [Crear y enviar mensajes](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Creación de un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Crear un Conector de Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Cómo pueden los administradores habilitar o deshabilitar conectores](/MicrosoftTeams/office-365-custom-connectors#enable-or-disable-connectors-in-teams)
* [Cómo pueden los administradores publicar conectores personalizados en su organización](/MicrosoftTeams/office-365-custom-connectors)
* [Crear un bot de notificaciones con JavaScript](../../sbs-gs-notificationbot.yml)
* [Cree su primera aplicación de bot con JavaScript](../../sbs-gs-bot.yml)
