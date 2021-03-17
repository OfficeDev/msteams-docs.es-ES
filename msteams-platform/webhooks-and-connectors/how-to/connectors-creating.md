---
title: Conectores de Office 365
description: Describe cómo empezar a usar Office 365 Connectors en Microsoft Teams
keywords: teams o365 conector
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: d0fe380cd168b8dcbddc5af0de96160e0bc259a9
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827924"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a><span data-ttu-id="d1d5a-104">Creación de conectores de Office 365 para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d1d5a-104">Creating Office 365 Connectors for Microsoft Teams</span></span>

><span data-ttu-id="d1d5a-105">Con las aplicaciones de Microsoft Teams, puede agregar el conector de Office 365 existente o crear uno nuevo para incluirlo en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one to include in Microsoft Teams.</span></span> <span data-ttu-id="d1d5a-106">Consulte [Crear su propio conector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-106">See [Build your own Connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) for more information.</span></span>

## <a name="adding-a-connector-to-your-teams-app"></a><span data-ttu-id="d1d5a-107">Agregar un conector a la aplicación de Teams</span><span class="sxs-lookup"><span data-stu-id="d1d5a-107">Adding a Connector to your Teams App</span></span>

<span data-ttu-id="d1d5a-108">Puedes distribuir el conector registrado como parte del paquete de la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-108">You can distribute your registered Connector as part of your Teams app package.</span></span> <span data-ttu-id="d1d5a-109">Ya sea como una solución independiente o como una de [](~/concepts/build-and-test/apps-package.md) las [](~/concepts/deploy-and-publish/apps-publish.md) varias funcionalidades que su experiencia habilita en Teams, puede empaquetar y publicar el conector como parte del envío de AppSource, o puede proporcionarlo a los usuarios directamente para cargarlo en Teams. [](~/concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="d1d5a-109">Whether as a standalone solution, or one of several [capabilities](~/concepts/extensibility-points.md) that your experience enables in Teams, you can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your Connector as part of your AppSource submission, or you can provide it to users directly for uploading within Teams.</span></span>

<span data-ttu-id="d1d5a-110">Para distribuir el conector, debe registrarse mediante el Panel de desarrolladores de [conectores.](https://outlook.office.com/connectors/home/login/#/publish)</span><span class="sxs-lookup"><span data-stu-id="d1d5a-110">To distribute your Connector, you need to register by using the [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="d1d5a-111">De forma predeterminada, una vez registrado un conector, se supone que el conector funcionará en todos los productos de Office 365 compatibles con ellos, incluidos Outlook y Teams.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-111">By default, once a Connector is registered, it's assumed that your Connector will work in all Office 365 products that support them, including Outlook and Teams.</span></span> <span data-ttu-id="d1d5a-112">Si ese no _es el_ caso y necesita crear un conector que solo funcione en Microsoft Teams, póngase en contacto con nosotros directamente en Microsoft Teams [App Submissions](mailto:teamsubm@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d1d5a-112">If that is _not_ the case and you need to create a Connector that only works in Microsoft Teams, contact us directly at [Microsoft Teams App Submissions](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1d5a-113">Después de elegir **Guardar en** el Panel de desarrolladores de Conectores, se registra el conector.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-113">After you choose **Save** in the Connectors Developer Dashboard, your Connector is registered.</span></span> <span data-ttu-id="d1d5a-114">Si quieres publicar el conector en AppSource, sigue las instrucciones de Publicar la aplicación [de Microsoft Teams en AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span><span class="sxs-lookup"><span data-stu-id="d1d5a-114">If you want to publish your Connector in AppSource, follow the instructions in [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="d1d5a-115">Si no quieres publicar la aplicación en AppSource y, en su lugar, simplemente distribuirla directamente a tu organización solo, puedes hacerlo publicando en [tu organización](#publish-connectors-for-your-organization).</span><span class="sxs-lookup"><span data-stu-id="d1d5a-115">If you do not wish to publish your app in AppSource, and rather simply distribute it directly to your organization only, you can do so by [publishing to your organization](#publish-connectors-for-your-organization).</span></span> <span data-ttu-id="d1d5a-116">Si solo desea publicar en su organización, no es necesario realizar ninguna otra acción en el panel de Connector.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-116">If you only want to publish to your organization, no further action is necessary on the Connector dashboard.</span></span>

### <a name="integrating-the-configuration-experience"></a><span data-ttu-id="d1d5a-117">Integración de la experiencia de configuración</span><span class="sxs-lookup"><span data-stu-id="d1d5a-117">Integrating the configuration experience</span></span>

<span data-ttu-id="d1d5a-118">Los usuarios completarán toda la experiencia de configuración de Connector sin tener que salir del cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-118">Your users will complete the entire Connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="d1d5a-119">Para lograr esta experiencia, Teams insertará la página de configuración directamente dentro de un iframe.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-119">To achieve this experience, Teams will embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="d1d5a-120">La secuencia de operaciones es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="d1d5a-120">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="d1d5a-121">El usuario hace clic en el conector para iniciar el proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-121">The user clicks on your connector to begin the configuration process.</span></span>
2. <span data-ttu-id="d1d5a-122">Teams cargará la experiencia de configuración en línea.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-122">Teams will load your configuration experience in line.</span></span>
3. <span data-ttu-id="d1d5a-123">El usuario interactúa con la experiencia web para completar la configuración.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-123">The user interacts with your web experience to complete the configuration.</span></span>
4. <span data-ttu-id="d1d5a-124">El usuario presiona "Guardar", lo que desencadena una devolución de llamada en el código.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-124">The user presses "Save", which triggers a callback in your code.</span></span>
5. <span data-ttu-id="d1d5a-125">El código procesará el evento save recuperando la configuración de webhook (documentada a continuación).</span><span class="sxs-lookup"><span data-stu-id="d1d5a-125">Your code will process the save event by retrieving the webhook settings (documented below).</span></span> <span data-ttu-id="d1d5a-126">A continuación, el código debe almacenar el webhook para publicar eventos más adelante.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-126">Your code should then store the webhook to post events later.</span></span>

<span data-ttu-id="d1d5a-127">Puede reutilizar la experiencia de configuración web existente o crear una versión independiente para hospedarse específicamente en Teams.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-127">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="d1d5a-128">El código debe:</span><span class="sxs-lookup"><span data-stu-id="d1d5a-128">Your code should:</span></span>

1. <span data-ttu-id="d1d5a-129">Incluye el SDK de JavaScript de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-129">Include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="d1d5a-130">Esto proporciona acceso de código a las API para realizar operaciones comunes, como obtener el contexto actual de usuario,canal/equipo e iniciar flujos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-130">This gives your code access to APIs to perform common operations like getting the current user/channel/team context and initiating authentication flows.</span></span> <span data-ttu-id="d1d5a-131">Inicializar el SDK llamando a `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="d1d5a-131">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
2. <span data-ttu-id="d1d5a-132">Llama `microsoftTeams.settings.setValidityState(true)` cuando quieras habilitar el botón Guardar.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-132">Call `microsoftTeams.settings.setValidityState(true)` when you want to enable the Save button.</span></span> <span data-ttu-id="d1d5a-133">Debe hacerlo como una respuesta a la entrada válida del usuario, como una actualización de campo o selección.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-133">You should do this as a response to valid user input, such as a selection or field update.</span></span>
3. <span data-ttu-id="d1d5a-134">Registrar un `microsoftTeams.settings.registerOnSaveHandler()` controlador de eventos, al que se llama cuando el usuario hace clic en Guardar.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-134">Register a `microsoftTeams.settings.registerOnSaveHandler()` event handler, which gets called when the user clicks Save.</span></span>
4. <span data-ttu-id="d1d5a-135">Llama `microsoftTeams.settings.setSettings()` para guardar la configuración del conector.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-135">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="d1d5a-136">Lo que se guarda aquí también es lo que se mostrará en el cuadro de diálogo de configuración si el usuario intenta actualizar una configuración existente para el conector.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-136">What's saved here is also what will be shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
5. <span data-ttu-id="d1d5a-137">Llama `microsoftTeams.settings.getSettings()` para capturar propiedades de webhook, incluida la dirección URL en sí.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-137">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL itself.</span></span> <span data-ttu-id="d1d5a-138">Debe llamar a esto Además de durante el evento save, también debe llamar a esto cuando la página se cargue por primera vez en el caso de una nueva configuración.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-138">You should call this  In addition to during the save event, you should also call this when your page is first loaded in the case of a re-configuration.</span></span>
6. <span data-ttu-id="d1d5a-139">(Opcional) Registra un `microsoftTeams.settings.registerOnRemoveHandler()` controlador de eventos, al que se llama cuando el usuario quita el conector.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-139">(Optional) Register a `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which gets called when the user removes your connector.</span></span> <span data-ttu-id="d1d5a-140">Este evento ofrece al servicio la oportunidad de realizar cualquier acción de limpieza.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-140">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="d1d5a-141">Este es un HTML de ejemplo para crear una página de configuración de Connector sin css:</span><span class="sxs-lookup"><span data-stu-id="d1d5a-141">Here's a sample HTML to create a Connector configuration page without the CSS:</span></span>

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

#### <a name="getsettings-response-properties"></a><span data-ttu-id="d1d5a-142">`GetSettings()` propiedades de respuesta</span><span class="sxs-lookup"><span data-stu-id="d1d5a-142">`GetSettings()` response properties</span></span>

>[!Note]
><span data-ttu-id="d1d5a-143">Los parámetros devueltos por la llamada aquí son diferentes de si se invocara este método desde una pestaña y difieren de los `getSettings` documentados [aquí](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="d1d5a-143">The parameters returned by the `getSettings` call here are different than if you were to invoke this method from a tab, and differ from those documented [here](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

| <span data-ttu-id="d1d5a-144">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1d5a-144">Parameter</span></span>   | <span data-ttu-id="d1d5a-145">Detalles</span><span class="sxs-lookup"><span data-stu-id="d1d5a-145">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="d1d5a-146">El identificador de entidad, establecido por el código al llamar `setSettings()` a .</span><span class="sxs-lookup"><span data-stu-id="d1d5a-146">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="d1d5a-147">El nombre de configuración, establecido por el código al llamar `setSettings()` a .</span><span class="sxs-lookup"><span data-stu-id="d1d5a-147">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="d1d5a-148">La dirección URL de la página de configuración, establecida por el código al llamar `setSettings()`</span><span class="sxs-lookup"><span data-stu-id="d1d5a-148">The URL of the configuration page, as set by your code when calling `setSettings()`</span></span> |
| `webhookUrl` | <span data-ttu-id="d1d5a-149">La dirección URL de webhook creada para este conector.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-149">The webhook URL created for this connector.</span></span> <span data-ttu-id="d1d5a-150">Conserve la dirección URL del webhook y úsela para PUBLICAR JSON estructurado para enviar tarjetas al canal.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-150">Persist the webhook URL and use it to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="d1d5a-151">El elemento `webhookUrl` se devuelve únicamente si la aplicación vuelve correctamente.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-151">The `webhookUrl` is returned only when application returns successfully.</span></span> |
| `appType` | <span data-ttu-id="d1d5a-152">Los valores devueltos pueden ser `mail`, `groups` o `teams`, que corresponden al correo de Office 365, a Grupos de Office 365 o a Microsoft Teams respectivamente.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-152">The values returned can be `mail`, `groups` or `teams` corresponding to the Office 365 Mail, Office 365 Groups or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="d1d5a-153">Este es el identificador único correspondiente al usuario de Office 365 que inició la instalación del conector.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-153">This is the unique id corresponding to the Office 365 user who initiated setup of the connector.</span></span> <span data-ttu-id="d1d5a-154">Debe estar protegido.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-154">It should be secured.</span></span> <span data-ttu-id="d1d5a-155">Este valor puede servir para asociar el usuario de Office 365 que define la configuración con el usuario de su servicio.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-155">This value can be used to associate the user in Office 365 who set up the configuration to the user in your service.</span></span> |

<span data-ttu-id="d1d5a-156">Si necesita autenticar al usuario como parte de la carga de [](~/tabs/how-to/authentication/auth-flow-tab.md) la página en el paso 2 anterior, consulte este vínculo para obtener más información sobre cómo integrar el inicio de sesión cuando la página está incrustada.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-156">If you need to authenticate the user as part of loading your page in step 2 above, refer to [this link](~/tabs/how-to/authentication/auth-flow-tab.md) for details on how you can integrate login when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="d1d5a-157">Debido a motivos de compatibilidad entre clientes, el código tendrá que llamar con la dirección URL y los métodos de devolución de llamada correctos o `microsoftTeams.authentication.registerAuthenticationHandlers()` de error antes de llamar a `authenticate()` .</span><span class="sxs-lookup"><span data-stu-id="d1d5a-157">Due to cross-client compatibility reasons, your code will need to call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success/failure callback methods before calling `authenticate()`.</span></span>

#### <a name="handling-edits"></a><span data-ttu-id="d1d5a-158">Control de ediciones</span><span class="sxs-lookup"><span data-stu-id="d1d5a-158">Handling edits</span></span>

<span data-ttu-id="d1d5a-159">El código debe controlar los usuarios que vuelvan a editar una configuración de conector existente.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-159">Your code should handle users returning to edit an existing connector configuration.</span></span> <span data-ttu-id="d1d5a-160">Para ello, llame `microsoftTeams.settings.setSettings()` durante la configuración inicial con los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="d1d5a-160">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="d1d5a-161">`entityId` es el identificador personalizado que entiende el servicio y representa lo que el usuario ha configurado.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-161">`entityId` is the custom ID that is understood by your service and represents what the user has configured.</span></span>
- <span data-ttu-id="d1d5a-162">`configName` es un nombre descriptivo que el código de configuración puede recuperar</span><span class="sxs-lookup"><span data-stu-id="d1d5a-162">`configName` is a friendly name that your configuration code can retrieve</span></span>
- <span data-ttu-id="d1d5a-163">`contentUrl` es una dirección URL personalizada que se carga cuando un usuario edita una configuración de conector existente.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-163">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span> <span data-ttu-id="d1d5a-164">Puede usar esta dirección URL para facilitar que el código controle el caso de edición.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-164">You can use this URL to make it easier for your code to handle the edit case.</span></span>

<span data-ttu-id="d1d5a-165">Normalmente, esta llamada se realiza como parte del controlador de eventos de guardar.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-165">Typically, this call is made as part of your save event handler.</span></span> <span data-ttu-id="d1d5a-166">Después, cuando se carga lo anterior, el código debe llamar para rellenar previamente cualquier configuración o formulario en la interfaz `contentUrl` `getSettings()` de usuario de configuración.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-166">Then, when the `contentUrl` above is loaded, your code should call `getSettings()` to prepopulate any settings or forms in your configuration UI.</span></span>

#### <a name="handling-removals"></a><span data-ttu-id="d1d5a-167">Controlar las eliminaciones</span><span class="sxs-lookup"><span data-stu-id="d1d5a-167">Handling removals</span></span>

<span data-ttu-id="d1d5a-168">Opcionalmente, puede ejecutar un controlador de eventos cuando el usuario quita una configuración de conector existente.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-168">You can optionally execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="d1d5a-169">Para registrar este controlador, llame a `microsoftTeams.settings.registerOnRemoveHandler()` .</span><span class="sxs-lookup"><span data-stu-id="d1d5a-169">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="d1d5a-170">Este controlador se puede usar para realizar operaciones de limpieza, como la eliminación de entradas de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-170">This handler can be used to perform cleanup operations such as removing entries from a database.</span></span>

### <a name="including-the-connector-in-your-manifest"></a><span data-ttu-id="d1d5a-171">Incluir el conector en el manifiesto</span><span class="sxs-lookup"><span data-stu-id="d1d5a-171">Including the Connector in your Manifest</span></span>

<span data-ttu-id="d1d5a-172">Puedes descargar el manifiesto de la aplicación de Teams generado automáticamente desde el portal.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-172">You can download the auto-generated Teams app manifest from the portal.</span></span> <span data-ttu-id="d1d5a-173">Sin embargo, para poder usarla para probar o publicar la aplicación, debes hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d1d5a-173">Before you can use it to test or publish your app, though, you must do the following:</span></span>

- <span data-ttu-id="d1d5a-174">[Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="d1d5a-174">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="d1d5a-175">Modifique la parte `icons` del manifiesto para hacer referencia a los nombres de archivo de los iconos en lugar de a las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-175">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="d1d5a-176">El archivo manifest.json siguiente contiene los elementos básicos necesarios para probar y enviar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-176">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="d1d5a-177">Reemplace `id` y `connectorId` en el ejemplo siguiente con el GUID del conector.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-177">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="d1d5a-178">Ejemplo de manifest.json con conector</span><span class="sxs-lookup"><span data-stu-id="d1d5a-178">Example manifest.json with Connector</span></span>

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

## <a name="testing-your-connector"></a><span data-ttu-id="d1d5a-179">Probar el conector</span><span class="sxs-lookup"><span data-stu-id="d1d5a-179">Testing your Connector</span></span>

<span data-ttu-id="d1d5a-180">Para probar el conector, cárguelo en un equipo igual que lo haría con cualquier otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-180">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="d1d5a-181">Puede crear un paquete .zip mediante el archivo de manifiesto desde el Panel del programador de conectores (modificado como se indica en la sección anterior) y los dos archivos de icono.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-181">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="d1d5a-182">Después de cargar la aplicación, abra la lista Conectores desde cualquier canal.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-182">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="d1d5a-183">Desplácese hasta la parte inferior para ver la aplicación en la sección **Cargada**.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-183">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![Captura de pantalla de la sección cargada en el cuadro de diálogo Conector](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="d1d5a-185">Ahora, puede iniciar la experiencia de configuración.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-185">You can now launch the configuration experience.</span></span> <span data-ttu-id="d1d5a-186">Tenga en cuenta que este flujo se produce completamente en Microsoft Teams como una experiencia hospedada.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-186">Be aware that this flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="d1d5a-187">Para comprobar que una `HttpPOST` acción funciona correctamente, [envíe mensajes al conector](~/webhooks-and-connectors/how-to/connectors-using.md).</span><span class="sxs-lookup"><span data-stu-id="d1d5a-187">To verify that an `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-your-organization"></a><span data-ttu-id="d1d5a-188">Publicar conectores para su organización</span><span class="sxs-lookup"><span data-stu-id="d1d5a-188">Publish Connectors for your organization</span></span>

<span data-ttu-id="d1d5a-189">A veces, es posible que no quieras publicar la aplicación del conector en la AppSource/Store pública, pero te gustaría que solo esté disponible para los usuarios de tu organización.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-189">Sometimes, you may not want to publish your connector app to the public AppSource/Store but would like it to be available only to the users in your organization.</span></span> <span data-ttu-id="d1d5a-190">En tales casos, puedes cargar la aplicación de conector personalizada en el Catálogo de aplicaciones [de tu organización.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="d1d5a-190">In such cases, you can upload your custom connector app to your [organization's App Catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="d1d5a-191">De esta forma, la aplicación de conector estará disponible solo para esa organización y no tendrá que publicar el conector en la tienda pública.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-191">This way, your connector app will be available only to that organization, and you will not need to publish your connector to the public store.</span></span>

<span data-ttu-id="d1d5a-192">Una vez cargado el paquete de la aplicación, para configurar y usar el conector en un equipo, puede instalarlo desde el catálogo de aplicaciones de la organización siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d1d5a-192">Once you've uploaded your app package, to configure and use the connector in a Team it can be installed from the organization's app catalog by following these steps:</span></span>

1. <span data-ttu-id="d1d5a-193">Selecciona el icono de aplicaciones en la barra de navegación vertical de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-193">Select the apps icon from the far left vertical navigation bar.</span></span>
1. <span data-ttu-id="d1d5a-194">En la **ventana Aplicaciones,** seleccione **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-194">In the **Apps** window select **Connectors**.</span></span>
1. <span data-ttu-id="d1d5a-195">Seleccione el conector que desea agregar y se mostrará una ventana de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-195">Select the connector that you want to add and a pop-up dialog window will display.</span></span>
1. <span data-ttu-id="d1d5a-196">Seleccione la **barra Agregar a un** equipo.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-196">Select the **Add to a team** bar.</span></span>
1. <span data-ttu-id="d1d5a-197">En la siguiente ventana de diálogo, escriba un nombre de equipo o canal.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-197">In the next dialog window type a team or channel name.</span></span>
1. <span data-ttu-id="d1d5a-198">Seleccione la **barra Configurar un conector** en la esquina inferior derecha de la ventana de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-198">Select the **Set up a connector** bar from the bottom right corner of dialog window.</span></span>
1. <span data-ttu-id="d1d5a-199">El conector estará disponible en la sección &#9679;&#9679;&#9679; => *Más* opciones Conectores todos los conectores para su equipo  =>    =>    =>   para ese equipo.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-199">The connector will be available in the  section &#9679;&#9679;&#9679; => *More options* => *Connectors* => *All* => *Connectors for you team* for that team.</span></span> <span data-ttu-id="d1d5a-200">Puedes desplazarte a esta sección o buscar la aplicación del conector.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-200">You can navigate by scrolling to this section or search for the connector app.</span></span>
1. <span data-ttu-id="d1d5a-201">Para configurar o modificar el conector, seleccione la **barra Configurar.**</span><span class="sxs-lookup"><span data-stu-id="d1d5a-201">To configure or modify the connector select the **Configure** bar.</span></span>

## <a name="code-sample"></a><span data-ttu-id="d1d5a-202">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="d1d5a-202">Code sample</span></span>
|<span data-ttu-id="d1d5a-203">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="d1d5a-203">**Sample name**</span></span> | <span data-ttu-id="d1d5a-204">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="d1d5a-204">**Description**</span></span> | <span data-ttu-id="d1d5a-205">**.NET**</span><span class="sxs-lookup"><span data-stu-id="d1d5a-205">**.NET**</span></span> | <span data-ttu-id="d1d5a-206">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="d1d5a-206">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="d1d5a-207">Conectores</span><span class="sxs-lookup"><span data-stu-id="d1d5a-207">Connectors</span></span>    | <span data-ttu-id="d1d5a-208">Ejemplo de Office 365 Connector que genera notificaciones al canal de teams.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-208">Sample Office 365 Connector generating notifications to teams channel.</span></span>|   [<span data-ttu-id="d1d5a-209">View</span><span class="sxs-lookup"><span data-stu-id="d1d5a-209">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="d1d5a-210">View</span><span class="sxs-lookup"><span data-stu-id="d1d5a-210">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="d1d5a-211">Ejemplo de conectores genéricos</span><span class="sxs-lookup"><span data-stu-id="d1d5a-211">Generic connectors sample</span></span> |<span data-ttu-id="d1d5a-212">Código de ejemplo para un conector genérico que es fácil de personalizar para cualquier sistema que admita webhooks.</span><span class="sxs-lookup"><span data-stu-id="d1d5a-212">Sample code for a generic connector that's easy to customize for any system which supports webhooks.</span></span>|  | [<span data-ttu-id="d1d5a-213">View</span><span class="sxs-lookup"><span data-stu-id="d1d5a-213">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
