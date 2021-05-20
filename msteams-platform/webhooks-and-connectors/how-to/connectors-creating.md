---
title: Conectores de Office 365
description: Describe cómo empezar a usar conectores de Office 365 en Microsoft Teams
keywords: teams o365 conector
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 9eaaedf88d907dd7a7422068ab5d20450345f0e7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566813"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Creación de conectores de Office 365 para Microsoft Teams

>Con Microsoft Teams aplicaciones, puede agregar el conector de Office 365 existente o crear uno nuevo para incluirlo en Microsoft Teams. Consulte [Crear su propio conector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) para obtener más información.

## <a name="adding-a-connector-to-your-teams-app"></a>Agregar un conector a la aplicación Teams

Puede distribuir el conector registrado como parte del paquete de la aplicación de Teams. Ya sea como una solución independiente o como una de las varias [capacidades](~/concepts/extensibility-points.md) que la experiencia habilita en Teams, puede [empaquetar](~/concepts/build-and-test/apps-package.md) y [publicar](~/concepts/deploy-and-publish/apps-publish.md) el conector como parte del envío de AppSource o puede proporcionarlo a los usuarios directamente para cargarlo dentro de Teams.

Para distribuir el conector, debe registrarse mediante el [Panel para desarrolladores de conectores.](https://outlook.office.com/connectors/home/login/#/publish) De forma predeterminada, una vez registrado un conector, se supone que el conector funcionará en todos los Office 365 productos que los admitan, incluidos Outlook y Teams. Si ese _no_ es el caso y necesita crear un conector que solo funcione en Microsoft Teams, póngase en contacto con nosotros directamente en [Microsoft Teams envíos de aplicaciones.](mailto:teamsubm@microsoft.com)

> [!IMPORTANT]
> Después de elegir **Guardar** en el panel para desarrolladores de conectores, se registra el conector. Si desea publicar el conector en AppSource, siga las instrucciones de Publicar la [aplicación Microsoft Teams en AppSource](~/concepts/deploy-and-publish/apps-publish.md). Si no desea publicar la aplicación en AppSource y, en lugar de simplemente, distribuirla directamente solo a su organización, puede hacerlo [publicando en su organización.](#publish-connectors-for-your-organization) Si solo desea publicar en su organización, no es necesaria ninguna otra acción en el panel Conector.

### <a name="integrating-the-configuration-experience"></a>Integración de la experiencia de configuración

Los usuarios completarán toda la experiencia de configuración del conector sin tener que abandonar el cliente Teams. Para lograr esta experiencia, Teams incrustará la página de configuración directamente dentro de un iframe. La secuencia de operaciones es la siguiente:

1. El usuario hace clic en el conector para iniciar el proceso de configuración.
2. Teams cargará su experiencia de configuración en línea.
3. El usuario interactúa con su experiencia web para completar la configuración.
4. El usuario presiona "Guardar", que activa una devolución de llamada en el código.
5. El código procesará el evento save recuperando la configuración del webhook (documentada a continuación). A continuación, el código debe almacenar el webhook para publicar eventos más adelante.

Puede reutilizar la experiencia de configuración web existente o crear una versión independiente que se hospeda específicamente en Teams. El código debe:

1. Incluya el SDK de JavaScript Microsoft Teams. Esto proporciona al código acceso a las API para realizar operaciones comunes, como obtener el contexto actual de usuario/canal/equipo e iniciar flujos de autenticación. Para inicializar el SDK, llame a `microsoftTeams.initialize()`.
2. Llame `microsoftTeams.settings.setValidityState(true)` cuando desee habilitar el botón Guardar. Debe hacerlo como respuesta a una entrada de usuario válida, como una selección o una actualización de campo.
3. Registre un `microsoftTeams.settings.registerOnSaveHandler()` controlador de eventos, al que se llama cuando el usuario hace clic en Guardar.
4. Llame `microsoftTeams.settings.setSettings()` para guardar la configuración del conector. Lo que se guarda aquí también es lo que se mostrará en el cuadro de diálogo de configuración si el usuario intenta actualizar una configuración existente para el conector.
5. Llame `microsoftTeams.settings.getSettings()` para capturar propiedades de webhook, incluida la propia dirección URL. Debe llamar a esto Además durante el evento save, también debe llamar a esto cuando la página se cargue por primera vez en el caso de una re-configuración.
6. (Opcional) Registre un `microsoftTeams.settings.registerOnRemoveHandler()` controlador de eventos, al que se llama cuando el usuario quita el conector. Este evento ofrece al servicio la oportunidad de realizar cualquier acción de limpieza.

Aquí hay un HTML de ejemplo para crear una página de configuración del conector sin el CSS:

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
>Los parámetros devueltos por la `getSettings` llamada aquí son diferentes de si usted fuera a invocar este método de una pestaña, y difieren de los documentados [aquí.](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)

| Parámetro   | Detalles |
|-------------|---------|
| `entityId`       | El identificador de entidad, establecido por el código al llamar a `setSettings()` . |
| `configName`  | El nombre de configuración, establecido por el código al llamar a `setSettings()` . |
| `contentUrl` | La dirección URL de la página de configuración, establecida por el código al llamar a `setSettings()` . |
| `webhookUrl` | La dirección URL de webhook creada para este conector. Conserve la dirección URL del webhook y utilícela para publicar JSON estructurado para enviar tarjetas al canal. El elemento `webhookUrl` se devuelve únicamente si la aplicación vuelve correctamente. |
| `appType` | Los valores devueltos pueden ser `mail`, `groups` o `teams`, que corresponden al correo de Office 365, a Grupos de Office 365 o a Microsoft Teams respectivamente. |
| `userObjectId` | Este es el identificador único correspondiente al usuario Office 365 que inició la configuración del conector. Debe estar protegido. Este valor puede servir para asociar el usuario de Office 365 que define la configuración con el usuario de su servicio. |

Si necesita autenticar al usuario como parte de la carga de su página en el paso 2 anterior, consulte [este enlace](~/tabs/how-to/authentication/auth-flow-tab.md) para obtener más información sobre cómo puede integrar el inicio de sesión cuando la página está incrustada.

> [!NOTE]
> Debido a razones de compatibilidad entre clientes, el código tendrá que llamar `microsoftTeams.authentication.registerAuthenticationHandlers()` con los métodos de devolución de llamada de error y dirección URL antes de llamar a `authenticate()` .

#### <a name="handling-edits"></a>Manejo de ediciones

El código debe controlar los usuarios que vuelven a editar una configuración de conector existente. Para ello, llame `microsoftTeams.settings.setSettings()` durante la configuración inicial con los siguientes parámetros:

- `entityId` es el identificador personalizado que entiende el servicio y representa lo que el usuario ha configurado.
- `configName` es un nombre descriptivo que el código de configuración puede recuperar
- `contentUrl` es una dirección URL personalizada que se carga cuando un usuario edita una configuración de conector existente. Puede usar esta dirección URL para facilitar que el código controle el caso de edición.

Normalmente, esta llamada se realiza como parte del controlador de eventos save. A continuación, cuando `contentUrl` se carga lo anterior, el código debe llamar `getSettings()` para prepoblar cualquier configuración o formulario en la interfaz de usuario de configuración.

#### <a name="handling-removals"></a>Manipulación de eliminaciones

Opcionalmente, puede ejecutar un controlador de eventos cuando el usuario quita una configuración de conector existente. Registre este controlador llamando a `microsoftTeams.settings.registerOnRemoveHandler()` . Este controlador se puede usar para realizar operaciones de limpieza, como quitar entradas de una base de datos.

### <a name="including-the-connector-in-your-manifest"></a>Incluido el conector en el manifiesto

Puede descargar el manifiesto de aplicación de Teams generado automáticamente desde el portal. Sin embargo, para poder usarlo para probar o publicar la aplicación, debe hacer lo siguiente:

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

Ahora, puede iniciar la experiencia de configuración. Tenga en cuenta que este flujo se produce completamente dentro de Microsoft Teams como una experiencia hospedada.

Para comprobar que una `HttpPOST` acción funciona correctamente, [envíe mensajes al conector.](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="publish-connectors-for-your-organization"></a>Publicar conectores para su organización

A veces, es posible que no desee publicar la aplicación de conector en la AppSource/Store pública, pero desea que solo esté disponible para los usuarios de su organización. En estos casos, puede cargar la aplicación de conector personalizada en el catálogo de aplicaciones de su [organización.](~/concepts/deploy-and-publish/apps-publish.md) De esta manera, la aplicación de conector solo estará disponible para esa organización y no tendrá que publicar el conector en la tienda pública.

Una vez que haya cargado el paquete de la aplicación, para configurar y usar el conector en un equipo se puede instalar desde el catálogo de aplicaciones de la organización siguiendo estos pasos:

1. Seleccione el icono de aplicaciones en la barra de navegación vertical de extrema izquierda.
1. En la ventana **Aplicaciones,** seleccione **Conectores**.
1. Seleccione el conector que desea agregar y se mostrará una ventana de diálogo emergente.
1. Seleccione la barra **Agregar a un equipo.**
1. En la siguiente ventana de diálogo escriba un nombre de equipo o canal.
1. Seleccione la **barra Configurar un conector** en la esquina inferior derecha de la ventana de diálogo.
1. El conector estará disponible en la sección &#9679;&#9679;&#9679; => *Más opciones*  =>  *Conectores*  =>  *todos los*  =>  *conectores para su equipo* para ese equipo. Puede navegar desplazándose a esta sección o buscar la aplicación del conector.
1. Para configurar o modificar el conector, seleccione la **barra Configurar.**

## <a name="code-sample"></a>Ejemplo de código
|**Nombre de la muestra** | **Descripción** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Conectores    | Ejemplo Office 365 conector que genera notificaciones al canal de equipos.|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Muestra de conectores genéricos |Código de ejemplo para un conector genérico que es fácil de personalizar para cualquier sistema que admita webhooks.|  | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
