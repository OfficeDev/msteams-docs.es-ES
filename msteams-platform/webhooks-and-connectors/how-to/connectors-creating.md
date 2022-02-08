---
title: Crear Conectores de Office 365
author: laujan
description: Describe cómo empezar a usar Office 365 Connectors en Microsoft Teams
keywords: conector de Office365 de teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 719d73394c3ab072c61f08b826b42e35c3475ca1
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435149"
---
# <a name="create-office-365-connectors"></a>Crear Conectores de Office 365

Con Microsoft Teams aplicaciones, puedes agregar el conector de Office 365 existente o crear uno nuevo dentro de Teams. Para obtener más información, [consulte build your own connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).

## <a name="add-a-connector-to-teams-app"></a>Agregar un conector a Teams aplicación

Puede crear un paquete [y](~/concepts/build-and-test/apps-package.md) [publicar el](~/concepts/deploy-and-publish/apps-publish.md) conector como parte del envío de AppSource. Puedes distribuir el conector registrado como parte del paquete Teams aplicación. Para obtener información sobre los puntos de entrada Teams aplicación, consulta [funcionalidades](~/concepts/extensibility-points.md). También puede proporcionar el paquete a los usuarios directamente para cargarlo en Teams.

Para distribuir el conector, debe registrarse a través del [Panel de desarrolladores de conectores](https://aka.ms/connectorsdashboard). Cuando se registra un conector, se supone que funciona en todos los Office 365 compatibles con aplicaciones, incluidos Outlook y Teams. Si ese no es el caso y debe crear un conector que solo funcione en Microsoft Teams, póngase en contacto con: [Microsoft Teams correo electrónico de envíos de aplicaciones](mailto:teamsubm@microsoft.com).

> [!IMPORTANT]
> El conector se registra después de seleccionar **Guardar** en el Panel de desarrolladores de conectores. Si quieres publicar el conector en AppSource, sigue las instrucciones de publicar la [aplicación Microsoft Teams app en AppSource](~/concepts/deploy-and-publish/apps-publish.md). Si no quieres publicar la aplicación en AppSource, distribuyela directamente a la organización. Después [de publicar conectores para la organización](#publish-connectors-for-the-organization), no se requiere ninguna acción adicional en el Panel de conectores.

### <a name="integrate-the-configuration-experience"></a>Integrar la experiencia de configuración

Los usuarios pueden completar toda la experiencia de configuración del conector sin tener que salir del Teams cliente. Para obtener la experiencia, Teams puede insertar la página de configuración directamente dentro de un iframe. La secuencia de operaciones es la siguiente:

1. El usuario selecciona el conector para iniciar el proceso de configuración.
1. El usuario interactúa con la experiencia web para completar la configuración.
1. El usuario selecciona **Guardar**, que desencadena una devolución de llamada en el código.

    > [!NOTE]
    > * El código puede procesar el evento save recuperando la configuración del webhook. El código almacena el webhook para publicar eventos más adelante.
    > * La experiencia de configuración se carga en línea en Teams.

Puede reutilizar la experiencia de configuración web existente o crear una versión independiente que se hospedará específicamente en Teams. El código debe incluir el Microsoft Teams SDK de JavaScript. Esto proporciona al código acceso a las API para realizar operaciones comunes, como obtener el contexto de usuario, canal o equipo actual e iniciar flujos de autenticación.

**Para integrar la experiencia de configuración**

1. Para inicializar el SDK, llame a `microsoftTeams.initialize()`.
1. Llama `microsoftTeams.settings.setValidityState(true)` para habilitar **Guardar**.

    > [!NOTE]
    > Debe llamar como respuesta `microsoftTeams.settings.setValidityState(true)` a la selección del usuario o a la actualización de campos.

1. Registrar  `microsoftTeams.settings.registerOnSaveHandler()` el controlador de eventos, al que se llama cuando el usuario selecciona **Guardar**.
1. Llama `microsoftTeams.settings.setSettings()` para guardar la configuración del conector. La configuración guardada también se muestra en el cuadro de diálogo de configuración si el usuario intenta actualizar una configuración existente para el conector.
1. Llamada `microsoftTeams.settings.getSettings()` para capturar propiedades de webhook, incluida la dirección URL.

    > [!NOTE]
    > Debe llamar cuando `microsoftTeams.settings.getSettings()` se cargue la página por primera vez en caso de reconfiguración.

1. Registrar `microsoftTeams.settings.registerOnRemoveHandler()` el controlador de eventos, al que se llama cuando el usuario quita el conector.

Este evento ofrece al servicio la oportunidad de realizar cualquier acción de limpieza.

El siguiente código proporciona un CÓDIGO HTML de ejemplo para crear una página de configuración de conector sin el servicio de atención al cliente y la compatibilidad:

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

Para autenticar al usuario como parte de la carga de la página, vea flujo de autenticación para que las [pestañas](~/tabs/how-to/authentication/auth-flow-tab.md) integren el inicio de sesión cuando la página está incrustada.

> [!NOTE]
> Debido a motivos de compatibilidad entre clientes, el código debe llamar `microsoftTeams.authentication.registerAuthenticationHandlers()` con la dirección URL y los métodos de devolución de llamada correctos o de error antes de llamar a `authenticate()`.

#### <a name="getsettings-response-properties"></a>`GetSettings` propiedades de respuesta

>[!NOTE]
>Los parámetros devueltos por la `getSettings` llamada son diferentes al invocar este método desde una pestaña y difieren de los documentados en la [configuración de js](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).

En la tabla siguiente se proporcionan los parámetros y los detalles de las propiedades de `GetSetting` respuesta:

| Parámetros   | Detalles |
|-------------|---------|
| `entityId`       | El identificador de entidad, establecido por el código al llamar a `setSettings()`. |
| `configName`  | El nombre de configuración, establecido por el código al llamar a `setSettings()`. |
| `contentUrl` | La dirección URL de la página de configuración, establecida por el código al llamar a `setSettings()`. |
| `webhookUrl` | La dirección URL de webhook creada para el conector. Use la dirección URL de webhook para POST JSON estructurado para enviar tarjetas al canal. Se `webhookUrl` devuelve solo cuando la aplicación devuelve datos correctamente. |
| `appType` | Los valores devueltos pueden ser `mail`, `groups`o `teams` correspondientes a los Office 365 Mail, Office 365 Groups o Microsoft Teams respectivamente. |
| `userObjectId` | Identificador único que corresponde al Office 365 usuario que inició la configuración del conector. Debe estar protegido. Este valor se puede usar para asociar al usuario en Office 365, que ha configurado la configuración en el servicio. |

#### <a name="handle-edits"></a>Controlar ediciones

El código debe controlar los usuarios que vuelvan a editar una configuración de conector existente. Para ello, llame durante `microsoftTeams.settings.setSettings()` la configuración inicial con los siguientes parámetros:

- `entityId` es el identificador personalizado que representa lo que el usuario ha configurado y comprendido por el servicio.
- `configName` es un nombre que el código de configuración puede recuperar.
- `contentUrl` es una dirección URL personalizada que se carga cuando un usuario edita una configuración de conector existente.

Esta llamada se realiza como parte del controlador de eventos guardar. Después, cuando se carga `contentUrl` , el código debe `getSettings()` llamar para rellenar previamente cualquier configuración o formulario en la interfaz de usuario de configuración.

#### <a name="handle-removals"></a>Controlar eliminaciones

Puede ejecutar un controlador de eventos cuando el usuario quita una configuración de conector existente. Para registrar este controlador, llame a `microsoftTeams.settings.registerOnRemoveHandler()`. Este controlador se usa para realizar operaciones de limpieza, como quitar entradas de una base de datos.

### <a name="include-the-connector-in-your-manifest"></a>Incluir el conector en el manifiesto

Descargue el auto generado `Teams app manifest` desde el portal. Realice los siguientes pasos antes de probar o publicar la aplicación:

1. [Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).
1. Modifique la `icons` parte del manifiesto para incluir los nombres de archivo de los iconos en lugar de las direcciones URL.

El siguiente archivo manifest.json contiene los elementos necesarios para probar y enviar la aplicación:

> [!NOTE]
> Reemplace `id` y `connectorId` en el siguiente ejemplo por el GUID del conector.

#### <a name="example-of-manifestjson-with-connector"></a>Ejemplo de manifest.json con connector

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

El módulo Exchange Online PowerShell V2 usa la autenticación moderna y funciona con la autenticación multifactor, denominada MFA para conectarse Exchange todos los entornos de PowerShell relacionados en Microsoft 365. Los administradores pueden usar Exchange Online PowerShell para deshabilitar conectores para un inquilino completo o un buzón de grupo específico, lo que afecta a todos los usuarios de ese espacio empresarial o buzón. No es posible deshabilitar para algunos y no para otros. Además, los conectores están deshabilitados de forma predeterminada para Government Community Cloud, denominados GCC inquilinos.

La configuración de nivel de espacio empresarial invalida la configuración de nivel de grupo. Por ejemplo, si un administrador habilita conectores para el grupo y los deshabilita en el inquilino, se deshabilitan los conectores para el grupo. Para habilitar un conector en Teams, conéctese a [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) mediante la autenticación moderna con o sin MFA.

### <a name="commands-to-enable-or-disable-connectors"></a>Comandos para habilitar o deshabilitar conectores

Ejecute los comandos siguientes en Exchange Online PowerShell:

* Para deshabilitar conectores para el inquilino: `Set-OrganizationConfig -ConnectorsEnabled:$false`.
* Para deshabilitar los mensajes que se pueden usar para el inquilino: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false`.
* Para habilitar conectores para Teams, ejecute los siguientes comandos:
  * `Set-OrganizationConfig -ConnectorsEnabled:$true `
  * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
  * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

Para obtener más información sobre el intercambio de módulos de PowerShell, [vea Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true). Para habilitar o deshabilitar los Outlook, [conecta aplicaciones a tus grupos en Outlook](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us).

## <a name="test-your-connector"></a>Probar el conector

Para probar el conector, cárbalo en un equipo con cualquier otra aplicación. Puede crear un paquete .zip mediante el archivo de manifiesto de los dos archivos de icono y conectores Panel de desarrolladores, modificado según se indica en Incluir el conector [en el manifiesto](#include-the-connector-in-your-manifest).

Después de cargar la aplicación, abre la lista de conectores desde cualquier canal. Desplácese a la parte inferior para ver la aplicación en la **sección Cargado** :

![Captura de pantalla de una sección cargada en el cuadro de diálogo conector](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> El flujo se produce por completo en Microsoft Teams como una experiencia hospedada.

Para comprobar que la `HttpPOST` acción funciona correctamente, [envíe mensajes al conector](~/webhooks-and-connectors/how-to/connectors-using.md).

## <a name="publish-connectors-for-the-organization"></a>Publicar conectores para la organización

Si quieres que el conector solo esté disponible para los usuarios de tu organización, puedes cargar la aplicación de conector personalizada en el catálogo de aplicaciones [de la organización](~/concepts/deploy-and-publish/apps-publish.md).

Después de cargar el paquete de la aplicación para configurar y usar el conector en un equipo, instale el conector desde el catálogo de aplicaciones de la organización.

**Para configurar un conector**

1. Selecciona **Aplicaciones en** la barra de navegación izquierda.
1. En la **sección Aplicaciones** , seleccione **Conectores**.
1. Seleccione el conector que desea agregar. Aparece una ventana de diálogo emergente.
1. En el menú desplegable, selecciona **Agregar a un equipo**.
1. En el cuadro de búsqueda, escriba un nombre de equipo o canal.
1. Seleccione **Configurar un conector en** el menú desplegable de la esquina inferior derecha de la ventana de diálogo.

> [!IMPORTANT]
> Actualmente, los conectores personalizados no están disponibles en Government Community Cloud (GCC), GCC-High y Department of Defense (DOD).

El conector está disponible en la sección &#9679;&#9679;&#9679; > **Más** **opcionesConnectorsAllConnectors** >  >  >  **para su equipo** para ese equipo. Puedes desplazarte a esta sección o buscar la aplicación del conector. Para configurar o modificar el conector, seleccione **Configurar**.

## <a name="distribute-webhook-and-connector"></a>Distribuir webhook y conector

1. [Configure un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) directamente para su equipo.
1. Agregue una [página de configuración](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) [y publique el webhook](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) entrante en un Office 365 Connector.
1. Empaquetar y publicar el conector como parte del envío [de AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) .

## <a name="code-sample"></a>Ejemplo de código

En la tabla siguiente se proporciona el nombre de ejemplo y su descripción:

|**Ejemplo de nombre** | **Descripción** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Conectores    | Sample Office 365 Connector que genera notificaciones en Teams canal.|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Ejemplo de conectores genéricos |Código de ejemplo para un conector genérico que es fácil de personalizar para cualquier sistema que admita webhooks.|  | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="see-also"></a>Consulte también

* [Crear y enviar mensajes](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Crear un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Crear un Conector de Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
