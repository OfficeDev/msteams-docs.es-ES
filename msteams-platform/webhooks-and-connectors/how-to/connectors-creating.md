---
title: Crear Conectores de Office 365
author: laujan
description: Describe cómo empezar a trabajar con conectores de Office 365 en Microsoft Teams
keywords: conector de Office365 de teams
ms.localizationpriority: high
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 9381fb9a55b6a48126e8c157040745d56708e9f8
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111615"
---
# <a name="create-office-365-connectors"></a>Crear Conectores de Office 365

Con las aplicaciones de Microsoft Teams, puede agregar su conector de Office 365 existente o crear uno nuevo en Teams. Para obtener más información, vea [compilación de su propio conector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).

## <a name="add-a-connector-to-teams-app"></a>Agregar un conector a la aplicación de Teams

Puede crear un [paquete](~/concepts/build-and-test/apps-package.md) y [publicar](~/concepts/deploy-and-publish/apps-publish.md) el conector como parte del envío de AppSource. Puede distribuir el conector registrado como parte del paquete de la aplicación de Teams. Para obtener información sobre los puntos de entrada de la aplicación de Teams, vea [capacidades](~/concepts/extensibility-points.md). También puede proporcionar el paquete a los usuarios directamente para cargarlo en Teams.

Para distribuir el conector, regístrelo en el [Conectores Panel de control para desarrolladores](https://aka.ms/connectorsdashboard).

Para que un conector funcione solo en Microsoft Teams, siga las instrucciones para enviar el conector en el artículo [publicar la aplicación en la tienda de Microsoft Teams](~/concepts/deploy-and-publish/appsource/publish.md). De lo contrario, un conector registrado funciona en todos los productos de Office 365 que admiten aplicaciones, incluidos Outlook y Teams.

> [!IMPORTANT]
> El conector se registra después de seleccionar **Guardar** en el Panel del desarrollador de conectores. Si desea publicar el conector en AppSource, siga las instrucciones de [publicar la aplicación de Microsoft Teams en AppSource](~/concepts/deploy-and-publish/apps-publish.md). Si no desea publicar la aplicación en AppSource, distribúyala directamente a la organización. Después de [publicar conectores para su organización](#publish-connectors-for-the-organization), no es necesario realizar ninguna otra acción en el panel del conector.

### <a name="integrate-the-configuration-experience"></a>Cree la base de datos de configuración:

Los usuarios pueden completar toda la experiencia de configuración del conector sin tener que salir del cliente de Teams. Para obtener la experiencia, Teams puede insertar la página de configuración directamente en un iframe. La secuencia de operaciones es la siguiente:

1. El usuario selecciona su conector para iniciar el proceso de configuración.
1. El usuario interactúa con la experiencia web para completar la configuración.
1. El usuario selecciona **Guardar**, que desencadena una devolución de llamada en el código.

    > [!NOTE]
    >
    > * El código puede procesar el evento de guardado recuperando la configuración del webhook. El código almacena el webhook para publicar eventos más adelante.
    > * La experiencia de configuración se carga en línea en Teams.

Puede reutilizar la experiencia de configuración web existente o crear una versión independiente para hospedarla específicamente en Teams. El código debe incluir el SDK de JavaScript de Microsoft Teams. Esto proporciona al código acceso a las API para realizar operaciones comunes, como obtener el contexto de usuario, canal o equipo actual e iniciar flujos de autenticación.

Para integrar la experiencia de la configuración:

1. Para inicializar el SDK, llame a `microsoftTeams.initialize()`.
1. Llame a `microsoftTeams.settings.setValidityState(true)` para habilitar **Guardar**.

    > [!NOTE]
    > Debe llamar a `microsoftTeams.settings.setValidityState(true)` como respuesta a la selección del usuario o a la actualización de campos.

1. Registre `microsoftTeams.settings.registerOnSaveHandler()` controlador de eventos, al que se llama cuando el usuario selecciona **Guardar**.
1. Llame a `microsoftTeams.settings.setSettings()` para guardar la configuración del conector. La configuración guardada también se muestra en el cuadro de diálogo de configuración si el usuario intenta actualizar una configuración existente para el conector.
1. Llame a `microsoftTeams.settings.getSettings()` para capturar las propiedades de webhook, incluida la dirección URL.

    > [!NOTE]
    > Debe llamar a `microsoftTeams.settings.getSettings()` cuando la página se cargue por primera vez en caso de reconfiguración.

1. Registre `microsoftTeams.settings.registerOnRemoveHandler()` controlador de eventos, al que se llama cuando el usuario quita el conector.

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

<script src="https://statics.teams.microsoft.com/sdk/v1.5.2/js/MicrosoftTeams.min.js" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="text/javascript">

        function onClick() {
            microsoftTeams.settings.setValidityState(true);
        }

        microsoftTeams.initialize();
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            microsoftTeams.settings.setSettings({
                 entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                 configName: eventType
                });

            microsoftTeams.settings.getSettings(function (settings) {
                // We get the Webhook URL in settings.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        microsoftTeams.settings.registerOnRemoveHandler(function (removeEvent) {
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

Para autenticar al usuario como parte de la carga de la página, consulte [flujo de autenticación para las pestañas](~/tabs/how-to/authentication/auth-flow-tab.md) para integrar el inicio de sesión cuando la página está incrustada.

> [!NOTE]
> Debido a razones de compatibilidad entre clientes, el código debe llamar a `microsoftTeams.authentication.registerAuthenticationHandlers()` con la dirección URL y los métodos de devolución de llamada correctos o erróneos antes de llamar a `authenticate()`.

#### <a name="getsettings-response-properties"></a>`GetSettings` Propiedades de la respuesta

>[!NOTE]
>Los parámetros devueltos por la llamada `getSettings` son diferentes cuando se invoca este método desde una pestaña y difieren de los documentados en [configuración de js](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).

En la tabla siguiente se proporcionan los parámetros y los detalles de las propiedades de respuesta `GetSetting`:

| Parámetros   | Detalles |
|-------------|---------|
| `entityId`       | El identificador de entidad, establecido por el código al llamar a `setSettings()`. |
| `configName`  | El nombre de configuración, según lo establecido por el código al llamar a `setSettings()`. |
| `contentUrl` | Dirección URL de la página de configuración, establecida por el código al llamar a `setSettings()`. |
| `webhookUrl` | Dirección URL del webhook creada para el conector. Use la dirección URL del webhook para PUBLICAR JSON estructurado para enviar tarjetas al canal. El `webhookUrl` solo se devuelve cuando la aplicación devuelve datos correctamente. |
| `appType` | Los valores devueltos pueden ser `mail`, `groups` o `teams`, que corresponden al Correo de Office 365, a Grupos de Office 365 o a Microsoft Teams respectivamente. |
| `userObjectId` | Identificador único correspondiente al usuario de Office 365 que inició la configuración del conector. Debe protegerse. Este valor se puede usar para asociar al usuario en Office 365, que ha configurado la configuración en el servicio. |

#### <a name="handle-edits"></a>Controlar ediciones

El código debe controlar los usuarios que vuelven para editar una configuración de conector existente. Para ello, llame a `microsoftTeams.settings.setSettings()` durante la configuración inicial con los parámetros siguientes:

* `entityId` es el identificador personalizado que representa lo que el usuario ha configurado y comprendido por el servicio.
* `configName` es un nombre que el código de configuración puede recuperar.
* `contentUrl` es una dirección URL personalizada que se carga cuando un usuario edita una configuración de conector existente.

Esta llamada se realiza como parte del controlador de eventos de guardado. A continuación, cuando se cargue el `contentUrl`, el código debe llamar a `getSettings()` para rellenar previamente cualquier configuración o formulario de la interfaz de usuario de configuración.

#### <a name="handle-removals"></a>Control de eliminaciones

Opcionalmente, puede ejecutar un controlador de eventos cuando el usuario quita una configuración de conector existente. Para registrar este controlador, llame a `microsoftTeams.settings.registerOnRemoveHandler()`. Este controlador se usa para realizar operaciones de limpieza, como quitar entradas de una base de datos.

### <a name="include-the-connector-in-your-manifest"></a>Incluir el conector en el manifiesto

Descargue el `Teams app manifest` generado automáticamente desde el portal. Realice los pasos siguientes antes de probar o publicar la aplicación:

1. [Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).
1. Modifique la parte `icons` del manifiesto para hacer referencia a los nombres de archivo de los iconos en lugar de a las direcciones URL.

El archivo manifest.json siguiente contiene los elementos básicos necesarios para probar y enviar la aplicación:

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

## <a name="enable-or-disable-connectors-in-teams"></a>Habilitar o deshabilitar conectores en Teams

El módulo Exchange Online PowerShell V2 usa la autenticación moderna y funciona con la autenticación multifactor, denominada MFA para conectarse a todos los entornos de PowerShell relacionados con Exchange en Microsoft 365. Los administradores pueden usar Exchange Online PowerShell para deshabilitar conectores para todo un inquilino o un buzón de grupo específico, lo que afecta a todos los usuarios de ese inquilino o buzón. No es posible deshabilitar para algunos y no para otros. Además, los conectores están deshabilitados de forma predeterminada para Government Community Cloud, denominados inquilinos de GCC.

La configuración de nivel de inquilino invalida la configuración de nivel de grupo. Por ejemplo, si un administrador habilita los conectores para el grupo y los deshabilita en el inquilino, los conectores del grupo se deshabilitan. Para habilitar un conector en Teams, [conectar a Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) mediante la autenticación moderna con o sin MFA.

### <a name="commands-to-enable-or-disable-connectors"></a>Comandos para habilitar o deshabilitar conectores

Ejecute los comandos siguientes en Exchange Online PowerShell:

* Para deshabilitar los conectores para el inquilino: `Set-OrganizationConfig -ConnectorsEnabled:$false`.
* Para deshabilitar los mensajes accionables para el inquilino: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false`.
* Para habilitar conectores para Teams, ejecute los siguientes comandos:
  * `Set-OrganizationConfig -ConnectorsEnabled:$true`
  * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
  * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

Para obtener más información sobre el intercambio de módulos de PowerShell, vea [Configuración de-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true). Para habilitar o deshabilitar los conectores de Outlook, [conectar aplicaciones a los grupos en Outlook](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab).

## <a name="test-your-connector"></a>Pruebe su conector

Para probar el conector, cárguelo en un equipo con cualquier otra aplicación. Puedes crear un paquete .zip utilizando el archivo de manifiesto de los dos archivos de iconos y conectores Developer Dashboard, modificado como se indica en [Incluir el conector en tu manifiesto](#include-the-connector-in-your-manifest).

Después de cargar la aplicación, abra la lista Conectores desde cualquier canal. Desplácese hasta la parte inferior para ver la aplicación en la sección **Cargada**:

![Captura de pantalla de la sección cargada en el cuadro de diálogo Conector](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> El flujo se produce completamente en Microsoft Teams como una experiencia hospedada.

Para comprobar que `HttpPOST` acción funciona correctamente, [envíe mensajes al conector](~/webhooks-and-connectors/how-to/connectors-using.md).

Siga la guía [paso a paso](../../sbs-teams-connectors.yml) para crear y probar los conectores en Microsoft Teams.

## <a name="publish-connectors-for-the-organization"></a>Publicar conectores para la organización

Si quiere que el conector esté disponible solo para los usuarios de su organización, puede cargar la aplicación del conector personalizado en el [ catálogo de aplicaciones de la organización](~/concepts/deploy-and-publish/apps-publish.md).

Después de cargar el paquete de la aplicación para configurar y usar el conector en un equipo, instale el conector desde el catálogo de aplicaciones de la organización.

Para configurar un conector:

1. Seleccione **Apps** en la barra de navegación izquierda.
1. En la sección **Apps**, selecciona **Connectors**.
1. Seleccione el conector que desea agregar. Aparece una ventana de cuadro de diálogo emergente.
1. En el menú desplegable, seleccione **Agregar a un equipo**.
1. En el cuadro de búsqueda, escriba un nombre de equipo o canal.
1. Seleccione **Configurar un conector** en el menú desplegable de la esquina inferior derecha de la ventana de diálogo.

> [!IMPORTANT]
> Actualmente, las pestañas personalizadas están disponibles en Government Community Cloud (GCC), GCC-High y Department of Defense (DOD).

El conector está disponible en la sección &#9679;&#9679;&#9679; > **Más opciones** > **Conectores** > **Todos** > **Conectores para el equipo** para ese equipo. Para navegar, desplácese a esta sección o busque la aplicación del conector. Para configurar o modificar el conector, seleccione **Configurar**.

## <a name="distribute-webhook-and-connector"></a>Distribución de webhook y conector

1. [Configurar un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md#create-an-incoming-webhook) directamente para su equipo.
1. Agregue una [configuración](~/webhooks-and-connectors/how-to/connectors-creating.md?#integrate-the-configuration-experience) y [Publicar tu Webhook próximo](~/webhooks-and-connectors/how-to/connectors-creating.md#publish-connectors-for-the-organization) en un conector de Office 365.
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
