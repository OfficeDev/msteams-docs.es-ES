---
title: Conectores de Office 365
description: Describe cómo empezar a trabajar con conectores de Office 365 en Microsoft Teams
keywords: teams o365 conector
ms.date: 04/19/2019
ms.openlocfilehash: 9c18a4c0dfda449c1507b26e78889cfab56ffd5f
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2020
ms.locfileid: "44590854"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Creación de conectores de Office 365 para Microsoft Teams

>Con las aplicaciones de Microsoft Teams, puede agregar su conector de Office 365 existente o crear uno nuevo para incluirlo en Microsoft Teams. Consulte [crear su propio conector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) para obtener más información.

## <a name="adding-a-connector-to-your-teams-app"></a>Adición de un conector a la aplicación Microsoft Teams

Puede distribuir su conector registrado como parte del paquete de la aplicación Teams. Ya sea una solución independiente o una de varias [funcionalidades](~/concepts/extensibility-points.md) que su experiencia permite en Microsoft Teams, puede [empaquetar](~/concepts/build-and-test/apps-package.md) y [publicar](~/concepts/deploy-and-publish/apps-publish.md) su conector como parte del envío de AppSource o puede proporcionarlo a los usuarios directamente para cargarlos en Teams.

Para distribuir el conector, debe registrarse mediante el [panel del programador de conectores](https://outlook.office.com/connectors/home/login/#/publish). De forma predeterminada, una vez que se registra un conector, se supone que el conector funcionará en todos los productos de Office 365 que los admiten, incluidos Outlook y Teams. Si este _no_ es el caso y necesita crear un conector que solo funcione en Microsoft Teams, póngase en contacto con nosotros directamente en [Teams Submissions support para la tienda](mailto:TeamsSubSupport@microsoft.com).

> [!IMPORTANT]
> Después de elegir **Guardar** en el panel del programador conectores, se registra el conector. Si desea publicar el conector en AppSource, siga las instrucciones que se indican en [publicar su aplicación de Microsoft Teams en AppSource](~/concepts/deploy-and-publish/apps-publish.md). Si no quiere publicar la aplicación en AppSource y, en su lugar, simplemente distribuirla directamente a su organización, puede hacerlo [publicando en su organización](#publish-connectors-for-your-organization). Si solo quiere publicar en su organización, no es necesario realizar ninguna acción adicional en el panel del conector.

### <a name="integrating-the-configuration-experience"></a>Integración de la experiencia de configuración

Los usuarios rellenarán toda la experiencia de configuración del conector sin tener que abandonar el cliente de Microsoft Teams. Para conseguir esta experiencia, Microsoft Teams insertará la página de configuración directamente en un iframe. La secuencia de operaciones es la siguiente:

1. El usuario hace clic en el conector para comenzar el proceso de configuración.
2. Teams cargará la experiencia de configuración en línea.
3. El usuario interactúa con su experiencia web para completar la configuración.
4. El usuario presiona "guardar", lo que desencadena una devolución de llamada en el código.
5. El código procesará el evento Save recuperando la configuración de webhook (documentada más adelante). El código debe almacenar el webhook para publicar los eventos más adelante.

Puede volver a usar su experiencia de configuración web existente o crear una versión independiente para hospedar específicamente en Microsoft Teams. El código debe:

1. Incluir el SDK de JavaScript de Microsoft Teams. Esto proporciona al código acceso a las API para realizar operaciones comunes, como obtener el contexto de usuario/canal/equipo actual e iniciar flujos de autenticación. Inicialice el SDK mediante una llamada a `microsoftTeams.initialize()` .
2. Llame `microsoftTeams.settings.setValidityState(true)` cuando quiera habilitar el botón Guardar. Debe hacerlo como respuesta a una entrada de usuario válida, como una selección o actualización de campo.
3. Registrar un `microsoftTeams.settings.registerOnSaveHandler()` controlador de eventos, al que se llama cuando el usuario hace clic en guardar.
4. Llamada `microsoftTeams.settings.setSettings()` para guardar la configuración del conector. Lo que se guarda aquí también es lo que se mostrará en el cuadro de diálogo de configuración si el usuario intenta actualizar una configuración existente para el conector.
5. Llamar `microsoftTeams.settings.getSettings()` a las propiedades de webhook de Fetch, incluida la propia dirección URL. Debe llamar a este método además de durante el evento Save, también debe llamar a este método cuando la página se cargue por primera vez en el caso de una nueva configuración.
6. Opcional Registrar un `microsoftTeams.settings.registerOnRemoveHandler()` controlador de eventos, al que se llama cuando el usuario quita el conector. Este evento le da al servicio la oportunidad de realizar cualquier acción de limpieza.

#### <a name="getsettings-response-properties"></a>`GetSettings()`propiedades de respuesta

>[!Note]
>Los parámetros devueltos por la `getSettings` llamada aquí son diferentes de si se va a invocar este método desde una pestaña y son distintos de los que se documentan [aquí](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest).

| Parámetro   | Detalles |
|-------------|---------|
| `entityId`       | IDENTIFICADOR de entidad, tal y como lo ha establecido el código cuando se llama `setSettings()` . |
| `configName`  | El nombre de la configuración, tal como lo ha establecido el código cuando se llama `setSettings()` . |
| `contentUrl` | La dirección URL de la página de configuración, tal y como lo establece el código al llamar a`setSettings()` |
| `webhookUrl` | La URL de webhook creada para este conector. Conserve la dirección URL del webhook y Úsela para exponer el JSON estructurado para enviar tarjetas al canal. El elemento `webhookUrl` se devuelve únicamente si la aplicación vuelve correctamente. |
| `appType` | Los valores devueltos pueden ser `mail`, `groups` o `teams`, que corresponden al correo de Office 365, a Grupos de Office 365 o a Microsoft Teams respectivamente. |
| `userObjectId` | Se trata del identificador único correspondiente al usuario de Office 365 que ha iniciado la instalación del conector. Debe estar protegido. Este valor puede servir para asociar el usuario de Office 365 que define la configuración con el usuario de su servicio. |

Si necesita autenticar al usuario como parte de la carga de la página en el paso 2 anterior, consulte [este vínculo](~/tabs/how-to/authentication/auth-flow-tab.md) para obtener detalles sobre cómo puede integrar el inicio de sesión cuando la página está incrustada.

> [!NOTE]
> Debido a los motivos de compatibilidad entre clientes, el código tendrá que llamar `microsoftTeams.authentication.registerAuthenticationHandlers()` con los métodos de devolución de llamada de éxito o error de la dirección URL antes de llamar `authenticate()` .

#### <a name="handling-edits"></a>Administración de ediciones

El código debe controlar a los usuarios que vuelvan a editar una configuración de conector existente. Para ello, realice una llamada `microsoftTeams.settings.setSettings()` durante la configuración inicial con los siguientes parámetros:

- `entityId`es el identificador personalizado que el servicio entiende y que representa lo que ha configurado el usuario.
- `configName`es un nombre descriptivo que el código de configuración puede recuperar
- `contentUrl`es una dirección URL personalizada que se carga cuando un usuario edita una configuración de conector existente. Puede usar esta dirección URL para facilitar que el código controle el caso de edición.

Normalmente, esta llamada se realiza como parte del controlador del evento Save. A continuación, cuando `contentUrl` se carga el código anterior, el código debe llamar `getSettings()` para rellenar previamente cualquier configuración o formulario en la interfaz de usuario de configuración.

#### <a name="handling-removals"></a>Control de eliminaciones

Opcionalmente, puede ejecutar un controlador de eventos cuando el usuario quita una configuración de conector existente. Para registrar este controlador, llame a `microsoftTeams.settings.registerOnRemoveHandler()` . Este controlador se puede usar para realizar operaciones de limpieza, como quitar entradas de una base de datos.

### <a name="including-the-connector-in-your-manifest"></a>Incluir el conector en el manifiesto

Puede descargar el manifiesto de la aplicación de Microsoft Teams generado automáticamente desde el portal. Sin embargo, para poder usarlo para probar o publicar la aplicación, debe hacer lo siguiente:

- Incluya dos iconos, siguiendo las instrucciones de [Iconos](~/concepts/build-and-test/apps-package.md#icons).
- Modifique la parte `icons` del manifiesto para hacer referencia a los nombres de archivo de los iconos en lugar de a las direcciones URL.

El archivo manifest.json siguiente contiene los elementos básicos necesarios para probar y enviar la aplicación.

> [!NOTE]
> Reemplace `id` y `connectorId` en el ejemplo siguiente con el GUID del conector.

#### <a name="example-manifestjson-with-connector"></a>Ejemplo de manifest.json con conector

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

## <a name="publish-connectors-for-your-organization"></a>Publicar conectores para la organización

A veces, es posible que no desee publicar la aplicación del conector en el almacén o la AppSource pública, pero desea que solo esté disponible para los usuarios de la organización. En estos casos, puede cargar la aplicación de conector personalizada en el [Catálogo de aplicaciones de su organización](~/concepts/deploy-and-publish/apps-publish.md). De esta forma, la aplicación de conector solo estará disponible para esa organización y no será necesario que publique el conector en el almacén público.

Una vez que haya cargado el paquete de la aplicación, para configurar y usar el conector en un equipo, se puede instalar desde el catálogo de aplicaciones de la organización siguiendo estos pasos:

1. Seleccione el icono aplicaciones de la barra de navegación vertical izquierda.
1. En la ventana de la **aplicación** , seleccione **conectores**.
1. Seleccione el conector que desea agregar y se mostrará una ventana emergente de cuadro de diálogo.
1. Seleccione **Agregar a una** barra de equipo.
1. En la siguiente ventana de diálogo, escriba un nombre de equipo o de canal.
1. Seleccione la barra **configurar un conector** desde la esquina inferior derecha de la ventana del cuadro de diálogo.
1. El conector estará disponible en la sección &#9679;&#9679;&#9679; => *More Options*  =>  *Connectors*  =>  *todos los*  =>  *conectores para el equipo* del equipo. Puede desplazarse a esta sección o buscar la aplicación conectora.
1. Para configurar o modificar el conector, seleccione la barra **configurar** .
