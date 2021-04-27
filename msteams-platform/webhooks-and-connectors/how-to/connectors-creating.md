---
title: Conectores de Office 365
description: Describe cómo empezar a usar Office 365 Connectors en Microsoft Teams
keywords: teams o365 conector
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 8091f71e22fcbdc297e2f7b54665b47e597e670e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018400"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Creación de conectores de Office 365 para Microsoft Teams

>Con las aplicaciones de Microsoft Teams, puede agregar el conector de Office 365 existente o crear uno nuevo para incluirlo en Microsoft Teams. Consulte [Crear su propio conector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) para obtener más información.

## <a name="adding-a-connector-to-your-teams-app"></a>Agregar un conector a la aplicación de Teams

Puede distribuir el conector registrado como parte del paquete de la aplicación de Teams. Ya sea como una solución independiente o como una de [](~/concepts/build-and-test/apps-package.md) las [](~/concepts/deploy-and-publish/apps-publish.md) varias funcionalidades que su experiencia habilita en Teams, puede empaquetar y publicar el conector como parte del envío de AppSource, o puede proporcionarlo a los usuarios directamente para cargarlo en Teams. [](~/concepts/extensibility-points.md)

Para distribuir el conector, debe registrarse mediante el Panel de desarrolladores de [conectores.](https://outlook.office.com/connectors/home/login/#/publish) De forma predeterminada, una vez registrado un conector, se supone que el conector funcionará en todos los productos de Office 365 compatibles con ellos, incluidos Outlook y Teams. Si ese no _es el_ caso y necesita crear un conector que solo funcione en Microsoft Teams, póngase en contacto con nosotros directamente en Microsoft Teams [App Submissions](mailto:teamsubm@microsoft.com).

> [!IMPORTANT]
> Después de elegir **Guardar en** el Panel de desarrolladores de Conectores, se registra el conector. Si quieres publicar el conector en AppSource, sigue las instrucciones de Publicar la aplicación [de Microsoft Teams en AppSource](~/concepts/deploy-and-publish/apps-publish.md). Si no quieres publicar la aplicación en AppSource y, en su lugar, simplemente distribuirla directamente a tu organización solo, puedes hacerlo publicando en [tu organización](#publish-connectors-for-your-organization). Si solo desea publicar en su organización, no es necesario realizar ninguna otra acción en el panel de Connector.

### <a name="integrating-the-configuration-experience"></a>Integración de la experiencia de configuración

Los usuarios completarán toda la experiencia de configuración de Connector sin tener que salir del cliente de Teams. Para lograr esta experiencia, Teams insertará la página de configuración directamente dentro de un iframe. La secuencia de operaciones es la siguiente:

1. El usuario hace clic en el conector para iniciar el proceso de configuración.
2. Teams cargará la experiencia de configuración en línea.
3. El usuario interactúa con la experiencia web para completar la configuración.
4. El usuario presiona "Guardar", lo que desencadena una devolución de llamada en el código.
5. El código procesará el evento save recuperando la configuración de webhook (documentada a continuación). A continuación, el código debe almacenar el webhook para publicar eventos más adelante.

Puede reutilizar la experiencia de configuración web existente o crear una versión independiente para hospedarse específicamente en Teams. El código debe:

1. Incluye el SDK de JavaScript de Microsoft Teams. Esto proporciona acceso de código a las API para realizar operaciones comunes, como obtener el contexto actual de usuario,canal/equipo e iniciar flujos de autenticación. Para inicializar el SDK, llame a `microsoftTeams.initialize()`.
2. Llama `microsoftTeams.settings.setValidityState(true)` cuando quieras habilitar el botón Guardar. Debe hacerlo como una respuesta a la entrada válida del usuario, como una actualización de campo o selección.
3. Registrar un `microsoftTeams.settings.registerOnSaveHandler()` controlador de eventos, al que se llama cuando el usuario hace clic en Guardar.
4. Llama `microsoftTeams.settings.setSettings()` para guardar la configuración del conector. Lo que se guarda aquí también es lo que se mostrará en el cuadro de diálogo de configuración si el usuario intenta actualizar una configuración existente para el conector.
5. Llama `microsoftTeams.settings.getSettings()` para capturar propiedades de webhook, incluida la dirección URL en sí. Debe llamar a esto Además de durante el evento save, también debe llamar a esto cuando la página se cargue por primera vez en el caso de una nueva configuración.
6. (Opcional) Registra un `microsoftTeams.settings.registerOnRemoveHandler()` controlador de eventos, al que se llama cuando el usuario quita el conector. Este evento ofrece al servicio la oportunidad de realizar cualquier acción de limpieza.

Este es un HTML de ejemplo para crear una página de configuración de Connector sin css:

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

#### <a name="getsettings-response-properties"></a>`GetSettings()` propiedades de respuesta

>[!Note]
>Los parámetros devueltos por la llamada aquí son diferentes de si se invocara este método desde una pestaña y difieren de los `getSettings` documentados [aquí](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).

| Parámetro   | Detalles |
|-------------|---------|
| `entityId`       | El identificador de entidad, establecido por el código al llamar `setSettings()` a . |
| `configName`  | El nombre de configuración, establecido por el código al llamar `setSettings()` a . |
| `contentUrl` | La dirección URL de la página de configuración, establecida por el código al llamar `setSettings()` |
| `webhookUrl` | La dirección URL de webhook creada para este conector. Conserve la dirección URL del webhook y úsela para PUBLICAR JSON estructurado para enviar tarjetas al canal. El elemento `webhookUrl` se devuelve únicamente si la aplicación vuelve correctamente. |
| `appType` | Los valores devueltos pueden ser `mail`, `groups` o `teams`, que corresponden al correo de Office 365, a Grupos de Office 365 o a Microsoft Teams respectivamente. |
| `userObjectId` | Este es el identificador único correspondiente al usuario de Office 365 que inició la instalación del conector. Debe estar protegido. Este valor puede servir para asociar el usuario de Office 365 que define la configuración con el usuario de su servicio. |

Si necesita autenticar al usuario como parte de la carga de [](~/tabs/how-to/authentication/auth-flow-tab.md) la página en el paso 2 anterior, consulte este vínculo para obtener más información sobre cómo integrar el inicio de sesión cuando la página está incrustada.

> [!NOTE]
> Debido a motivos de compatibilidad entre clientes, el código tendrá que llamar con la dirección URL y los métodos de devolución de llamada correctos o `microsoftTeams.authentication.registerAuthenticationHandlers()` de error antes de llamar a `authenticate()` .

#### <a name="handling-edits"></a>Control de ediciones

El código debe controlar los usuarios que vuelven a editar una configuración de conector existente. Para ello, llame `microsoftTeams.settings.setSettings()` durante la configuración inicial con los siguientes parámetros:

- `entityId` es el identificador personalizado que entiende el servicio y representa lo que el usuario ha configurado.
- `configName` es un nombre descriptivo que el código de configuración puede recuperar
- `contentUrl` es una dirección URL personalizada que se carga cuando un usuario edita una configuración de conector existente. Puede usar esta dirección URL para facilitar que el código controle el caso de edición.

Normalmente, esta llamada se realiza como parte del controlador de eventos de guardar. Después, cuando se carga lo anterior, el código debe llamar para rellenar previamente cualquier configuración o formulario en la interfaz `contentUrl` `getSettings()` de usuario de configuración.

#### <a name="handling-removals"></a>Controlar las eliminaciones

Opcionalmente, puede ejecutar un controlador de eventos cuando el usuario quita una configuración de conector existente. Para registrar este controlador, llame a `microsoftTeams.settings.registerOnRemoveHandler()` . Este controlador se puede usar para realizar operaciones de limpieza, como la eliminación de entradas de una base de datos.

### <a name="including-the-connector-in-your-manifest"></a>Incluir el conector en el manifiesto

Puedes descargar el manifiesto de la aplicación de Teams generado automáticamente desde el portal. Sin embargo, para poder usarla para probar o publicar la aplicación, debes hacer lo siguiente:

- [Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).
- Modifique la parte `icons` del manifiesto para hacer referencia a los nombres de archivo de los iconos en lugar de a las direcciones URL.

El archivo manifest.json siguiente contiene los elementos básicos necesarios para probar y enviar la aplicación.

> [!NOTE]
> Reemplace `id` y `connectorId` en el ejemplo siguiente con el GUID del conector.

#### <a name="example-manifestjson-with-connector"></a>Ejemplo de manifest.json con conector

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
    "full": "This is a sample manifest for an app with a connector with an inline configuration experience.",
    "short": "This is a sample manifest for an app with a connector."
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "configurationUrl": "https://teamstodoappconnectorwithinlineconfig.azurewebsites.net/Connector/Setup",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App Long Name"
  },
  "accentColor": "#FFFFFF"
}
```

## <a name="testing-your-connector"></a>Probar el conector

Para probar el conector, cárguelo en un equipo igual que lo haría con cualquier otra aplicación. Puede crear un paquete .zip mediante el archivo de manifiesto desde el Panel del programador de conectores (modificado como se indica en la sección anterior) y los dos archivos de icono.

Después de cargar la aplicación, abra la lista Conectores desde cualquier canal. Desplácese hasta la parte inferior para ver la aplicación en la sección **Cargada**.

![Captura de pantalla de la sección cargada en el cuadro de diálogo Conector](~/assets/images/connectors/connector_dialog_uploaded.png)

Ahora, puede iniciar la experiencia de configuración. Tenga en cuenta que este flujo se produce completamente en Microsoft Teams como una experiencia hospedada.

Para comprobar que una `HttpPOST` acción funciona correctamente, [envíe mensajes al conector](~/webhooks-and-connectors/how-to/connectors-using.md).

## <a name="publish-connectors-for-your-organization"></a>Publicar conectores para su organización

A veces, es posible que no quieras publicar la aplicación del conector en la AppSource/Store pública, pero te gustaría que solo esté disponible para los usuarios de tu organización. En tales casos, puedes cargar la aplicación de conector personalizada en el Catálogo de aplicaciones [de tu organización.](~/concepts/deploy-and-publish/apps-publish.md) De esta forma, la aplicación de conector estará disponible solo para esa organización y no tendrá que publicar el conector en la tienda pública.

Una vez cargado el paquete de la aplicación, para configurar y usar el conector en un equipo, puede instalarlo desde el catálogo de aplicaciones de la organización siguiendo estos pasos:

1. Selecciona el icono de aplicaciones en la barra de navegación vertical de la izquierda.
1. En la **ventana Aplicaciones,** seleccione **Conectores**.
1. Seleccione el conector que desea agregar y se mostrará una ventana de diálogo emergente.
1. Seleccione la **barra Agregar a un** equipo.
1. En la siguiente ventana de diálogo, escriba un nombre de equipo o canal.
1. Seleccione la **barra Configurar un conector** en la esquina inferior derecha de la ventana de diálogo.
1. El conector estará disponible en la sección &#9679;&#9679;&#9679; => *Más* opciones Conectores todos los conectores para su equipo  =>    =>    =>   para ese equipo. Puedes desplazarte a esta sección o buscar la aplicación del conector.
1. Para configurar o modificar el conector, seleccione la **barra Configurar.**

## <a name="code-sample"></a>Ejemplo de código
|**Nombre de ejemplo** | **Description** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Conectores    | Ejemplo de Office 365 Connector que genera notificaciones al canal de teams.|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Ejemplo de conectores genéricos |Código de ejemplo para un conector genérico que es fácil de personalizar para cualquier sistema que admita webhooks.|  | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
