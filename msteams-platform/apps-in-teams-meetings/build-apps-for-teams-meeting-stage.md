---
title: Compilación de aplicaciones para la fase de reunión de Teams
author: v-sdhakshina
description: Obtenga información sobre cómo crear aplicaciones para la fase de reunión de Teams, compartirlas en las API de fase y generar un vínculo profundo para compartir contenido para la fase de las reuniones.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: ea5d7b57b9ee6344d34fcc6ed560936ac6109304
ms.sourcegitcommit: 4e355e22ddcd10ba9a8f37965c4f5c8fa04f5776
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2022
ms.locfileid: "68701037"
---
# <a name="build-apps-for-teams-meeting-stage"></a>Compilación de aplicaciones para la fase de reunión de Teams

Compartir en fase permite a los usuarios compartir una aplicación en la fase de reunión desde el panel lateral de la reunión en una reunión en curso. Este uso compartido es interactivo y colaborativo en comparación con el uso compartido de pantalla pasivo.

Para invocar el recurso compartido a la fase, los usuarios pueden seleccionar el icono **Compartir en fase** en la parte superior derecha del panel lateral de la reunión. **El icono Compartir en fase** es nativo del cliente de Teams y al seleccionarlo se comparte toda la aplicación en la fase de reunión.

## <a name="app-manifest-settings-for-apps-in-meeting-stage"></a>Configuración del manifiesto de aplicación para aplicaciones en la fase de reunión

Para compartir una aplicación en la fase de reunión, actualice la `context` propiedad en el manifiesto de la aplicación de la siguiente manera:

```json
"context":[ 
    "meetingSidePanel", 
    "meetingStage" 
     ] 
```

## <a name="advanced-share-to-stage-apis"></a>Uso compartido avanzado para las API de fase

Hay muchos escenarios en los que compartir toda la aplicación en la fase de reunión no es tan útil como compartir partes específicas de la aplicación:  

1. En el caso de una aplicación de lluvia de ideas o pizarra, es posible que un usuario quiera compartir un panel específico en una reunión frente a toda la aplicación con todos los paneles.  

1. Para una aplicación médica, es posible que un médico quiera compartir solo los rayos X en la pantalla con el paciente en lugar de compartir toda la aplicación con todos los registros o resultados de los pacientes, etc.

1. Es posible que un usuario quiera compartir contenido de un único proveedor de contenido a la vez (por ejemplo, YouTube) en lugar de compartir un catálogo de vídeos completo en el escenario.

Para ayudar a los usuarios en estos escenarios, hemos publicado las API dentro del SDK de cliente de Teams que le permite invocar mediante programación el recurso compartido para realizar la fase de partes específicas de la aplicación desde un botón en el panel lateral de la reunión.

:::image type="content" source="../assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="En la captura de pantalla se muestra el recurso compartido en la vista de la fase de reunión.":::

Use las siguientes API para compartir una parte específica de la aplicación:

|Método| Descripción| Origen|
|---|---|----|
|[**Compartir contenido de la aplicación en la fase**](#share-app-content-to-stage-api)| Comparta partes específicas de la aplicación en la fase de reunión desde el panel lateral de la reunión en una reunión. | [SDK de biblioteca de JavaScript de Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting) |
|[**Obtener el estado de uso compartido del contenido de la aplicación**](#get-app-content-stage-sharing-state-api)| Obtenga información sobre el estado de uso compartido de la aplicación en la fase de reunión. | [SDK de biblioteca de JavaScript de Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingstate) |
|[**Obtener funcionalidades de uso compartido de la fase de contenido de la aplicación**](#get-app-content-stage-sharing-capabilities-api)| Capture las capacidades de la aplicación para compartir en la fase de reunión. | [SDK de biblioteca de JavaScript de Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingcapabilities) |

## <a name="share-app-content-to-stage-api"></a>Compartir contenido de la aplicación para API de fase

La `shareAppContentToStage` API le permite compartir partes específicas de la aplicación en la fase de reunión. La API está disponible a través del SDK de cliente de Teams.

### <a name="prerequisite"></a>Requisito previo

* Para usar la `shareAppContentToStage` API, debe obtener los permisos de RSC. En el manifiesto de la aplicación, configure la propiedad `authorization` y la `name` y `type` en el campo`resourceSpecific`. Por ejemplo:

    ```json
    "authorization": {
        "permissions": { 
        "resourceSpecific": [
        { 
         "name": "MeetingStage.Write.Chat",
         "type": "Delegated"
        }
        ]
    }
    }
    ```

* `appContentUrl` la matriz debe permitirse `validDomains` dentro de manifest.json; de lo contrario, la API devuelve un error 501.

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluyen los parámetros de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**callback**| Cadena | Sí | La devolución de llamada contiene dos parámetros, error y resultado. El *error* puede contener un error de tipo *SdkError* o NULL cuando el recurso compartido se realiza correctamente. El *resultado* puede contener un valor true, si hay un recurso compartido correcto, o null cuando se produce un error en el recurso compartido. |
|**appContentURL**| Cadena | Sí | Dirección URL que se compartirá en la fase. |

### <a name="example"></a>Ejemplo

```javascript
const appContentUrl = "https://www.bing.com/";

microsoftTeams.meeting.shareAppContentToStage((err, result) => {
    if (result) {
        // handle success
    }
    if (err) {
        // handle error
    }
}, appContentUrl);
```

### <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **500** | Error interno. |
| **501** | La API no se admite en el contexto actual.|
| **1 000** | La aplicación no tiene los permisos adecuados para permitir que el recurso compartido se almacene en fase.|

## <a name="get-app-content-stage-sharing-state-api"></a>Obtención de la API de estado de uso compartido de la fase de contenido de la aplicación

La `getAppContentStageSharingState` API le permite capturar información sobre el uso compartido de aplicaciones en la fase de reunión.

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluye el parámetro de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**callback**| Cadena | Sí | La devolución de llamada contiene dos parámetros, error y resultado. El *error* puede contener un error de tipo *SdkError*, en caso de error, o NULL cuando el recurso compartido se realiza correctamente. El *resultado* puede contener un `IAppContentStageSharingState` objeto, cuando el recurso compartido se realiza correctamente, o null, en caso de error.|

### <a name="example"></a>Ejemplo

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates if app is sharing content on the meeting stage.
    }
});
```

El cuerpo de la respuesta JSON para la API de `getAppContentStageSharingState` es:

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **500** | Error interno. |
| **501** | La API no se admite en el contexto actual.|
| **1 000** | La aplicación no tiene los permisos adecuados para permitir que el recurso compartido se almacene en fase.|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>API de obtención de funcionalidades de uso compartido de la fase de contenido de la aplicación

La `getAppContentStageSharingCapabilities` API le permite capturar las funcionalidades de la aplicación para compartir en la fase de reunión.

### <a name="query-parameter"></a>Parámetro de consulta

En la tabla siguiente se incluye el parámetro de consulta:

|Valor|Tipo|Obligatorio|Descripción|
|---|---|----|---|
|**callback**| Cadena | Sí | La devolución de llamada contiene dos parámetros, error y resultado. El *error* puede contener un error de tipo *SdkError* o NULL cuando el recurso compartido se realiza correctamente. El resultado puede contener un `IAppContentStageSharingCapabilities` objeto, cuando el recurso compartido se realiza correctamente, o null, en caso de error.|

### <a name="example"></a>Ejemplo

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

El cuerpo de respuesta JSON para `getAppContentStageSharingCapabilities` API es:

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>Códigos de respuesta

En la tabla siguiente se proporcionan los códigos de respuesta:

|Código de respuesta|Descripción|
|---|---|
| **500** | Error interno. |
| **501** | La API no se admite en el contexto actual.|
| **1 000** | La aplicación no tiene permisos para permitir que el recurso compartido se almacene provisionalmente.|

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>Generación de un vínculo profundo para compartir contenido para realizar una fase en las reuniones

También puede generar un vínculo profundo para compartir la aplicación para realizar la fase e iniciar o unirse a una reunión.

> [!NOTE]
>
> * Actualmente, el vínculo profundo para compartir contenido para la fase de las reuniones está experimentando mejoras en la experiencia de usuario y solo está disponible en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).
> * El vínculo profundo para compartir contenido para la fase de reunión solo se admite en el cliente de escritorio de Teams.

Cuando un usuario que forma parte de una reunión en curso selecciona un vínculo profundo en una aplicación, la aplicación se comparte en la fase y aparece una ventana emergente de permisos. Los usuarios pueden conceder acceso a los participantes para colaborar con una aplicación.

:::image type="content" source="../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="La captura de pantalla es un ejemplo que muestra una ventana emergente de permisos.":::

Cuando un usuario no está en una reunión, el usuario se redirige al calendario de Teams, donde puede unirse a una reunión o iniciar una reunión instantánea (Reunirse ahora).

:::image type="content" source="../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="La captura de pantalla es un ejemplo que muestra una ventana emergente cuando no hay ninguna reunión en curso.":::

Una vez que el usuario inicia una reunión instantánea (Reunirse ahora), puede agregar participantes e interactuar con la aplicación.

:::image type="content" source="../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="La captura de pantalla es un ejemplo que muestra una opción para agregar participantes y cómo interactuar con la aplicación.":::

Para agregar un vínculo profundo para compartir contenido en el escenario, debe tener un contexto de aplicación. El contexto de la aplicación permite al cliente de Teams capturar el manifiesto de la aplicación y comprobar si es posible el uso compartido en el escenario. A continuación se muestra un ejemplo de contexto de aplicación.

`{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

Los parámetros de consulta para el contexto de la aplicación son:

* `appID`: es el identificador que se puede obtener del manifiesto de la aplicación.
* `appSharingUrl`: la dirección URL que debe compartirse en el escenario debe ser un dominio válido definido en el manifiesto de la aplicación. Si la dirección URL no es un dominio válido, aparecerá un cuadro de diálogo de error para proporcionar al usuario una descripción del error.
* `useMeetNow`: incluye un parámetro booleano que puede ser true o false.
  * **True**: cuando el `UseMeetNow` valor es true y no hay ninguna reunión en curso, se iniciará una nueva reunión meet now. Cuando haya una reunión en curso, se omitirá este valor.

  * **False**: el valor predeterminado de `UseMeetNow` es false, lo que significa que cuando se comparte un vínculo profundo en la fase y no hay ninguna reunión en curso, aparecerá un elemento emergente de calendario. Sin embargo, puede compartir directamente durante una reunión.

Asegúrese de que todos los parámetros de consulta estén correctamente codificados mediante URI y que el contexto de la aplicación tenga que codificarse dos veces en la dirección URL final. A continuación, se muestra un ejemplo.

```json
var appContext= JSON.stringify({ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9cc80a93-1d41-4bcb-8170-4b9ec9e29fbb", "useMeetNow":false })
var encodedContext = encodeURIComponent(appcontext).replace(/'/g,"%27").replace(/"/g,"%22")
var encodedAppContext = encodeURIComponent(encodedContext).replace(/'/g,"%27").replace(/"/g,"%22")
```

Se puede iniciar un vínculo profundo desde la web de Teams o desde el cliente de escritorio de Teams.

* **Web de Teams**: use el siguiente formato para iniciar un vínculo profundo desde la web de Teams para compartir contenido en el escenario.

    `https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`

    Ejemplo: `https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Vínculo profundo|Formato|Ejemplo|
    |---------|---------|---------|
    |Para compartir la aplicación y abrir el calendario de Teams, cuando UseMeeetNow es false, es **el** valor predeterminado.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Para compartir la aplicación e iniciar una reunión instantánea, cuando UseMeeetNow es **true**.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **Cliente de escritorio de equipo**: use el siguiente formato para iniciar un vínculo profundo desde el cliente de escritorio de Teams para compartir contenido en el escenario.

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    Ejemplo: `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Vínculo profundo|Formato|Ejemplo|
    |---------|---------|---------|
    |Para compartir la aplicación y abrir el calendario de Teams, cuando UseMeeetNow es false, es **el** valor predeterminado.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Para compartir la aplicación e iniciar una reunión instantánea, cuando UseMeeetNow es **true**.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

Los parámetros de consulta son:

* `deepLinkId`: cualquier identificador usado para la correlación de telemetría.
* `fqdn`: `fqdn` es un parámetro opcional, que se puede usar para cambiar a un entorno adecuado de una reunión para compartir una aplicación en el escenario. Admite escenarios en los que se produce un recurso compartido de aplicaciones específico en un entorno determinado. El valor predeterminado de es dirección URL de `fqdn` empresa y los valores posibles son `Teams.live.com` para Teams for Life, `teams.microsoft.com`o `teams.microsoft.us`.

Para compartir toda la aplicación para la fase, en el manifiesto de la aplicación, debe configurar `meetingStage` y `meetingSidePanel` , como contextos de marco, consulte [manifiesto de la aplicación](../resources/schema/manifest-schema.md). De lo contrario, es posible que los asistentes a la reunión no puedan ver el contenido en el escenario.

> [!NOTE]
> Para que la aplicación pase la validación, cuando cree un vínculo profundo desde el sitio web, la aplicación web o la tarjeta adaptable, use **Compartir en la reunión** como cadena o copia.

## <a name="build-an-in-meeting-document-signing-app"></a>Creación de una aplicación de firma de documentos en la reunión

Puede crear una aplicación en la reunión para permitir que los participantes de la reunión firmen documentos en tiempo real. Facilita la revisión y firma de documentos en una sola sesión. Los participantes pueden firmar los documentos con su identidad de inquilino actual.

Puede usar una aplicación de firma en reunión para:

- Adición de documentos que se revisarán durante una reunión
- Uso compartido de documentos que se van a revisar en la fase principal
- Firmar documentos con la identidad del firmante

Los participantes pueden revisar y firmar documentos, como contratos de compra y pedidos de compra.

:::image type="content" source="../assets/images/sbs-inmeeting-doc-signing/final-output.png" alt-text="Aplicación de firma de documentos en la reunión":::

Los siguientes roles de participante pueden estar implicados durante la reunión:

- **Creador de** documentos: este rol puede agregar sus propios documentos para revisarlos y firmarlos.
- **Firmante**: este rol puede firmar documentos revisados.
- **Lector**: este rol puede ver los documentos agregados a la reunión.

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | C# | Node.js |
|----------------|-----------------|--------------|----------------|
|Ejemplo de fase de reunión | Aplicación de ejemplo para mostrar una pestaña en la fase de reunión para la colaboración | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| Notificación en la reunión | Muestra cómo implementar la notificación en la reunión mediante el bot. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| Firma de documentos en la reunión | Muestra cómo implementar una aplicación de Teams de firma de documentos. Incluye el uso compartido de contenido específico de la aplicación para la fase, el inicio de sesión único de Teams y la vista de fase específica del usuario. | [Ver](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | ND |

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../sbs-inmeeting-document-signing.yml) para crear una aplicación de firma de documentos en la reunión.

## <a name="see-also"></a>Consulte también

* [Flujo de autenticación de Teams para pestañas](../tabs/how-to/authentication/auth-flow-tab.md)
* [Aplicaciones para reuniones de Teams](teams-apps-in-meetings.md)
* [Pestañas de compilación para la reunión](build-tabs-for-meeting.md)
* [Creación de una conversación extensible para el chat de reuniones](build-extensible-conversation-for-meeting-chat.md)
* [Compilación de aplicaciones para usuarios anónimos](build-apps-for-anonymous-user.md)
* [API avanzadas de reunión](meeting-apps-apis.md)
* [Escenas personalizadas del Modo conferencia](~/apps-in-teams-meetings/teams-together-mode.md)
* [SDK de Live Share](teams-live-share-overview.md)
