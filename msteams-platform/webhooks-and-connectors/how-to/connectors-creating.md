---
title: Crear Conectores de Office 365
author: laujan
description: Describe cómo empezar a usar Office 365 Connectors en Microsoft Teams
keywords: teams o365 conector
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 28a2b35e868baf34e35a11a00e10b30b0f09c236
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179758"
---
# <a name="create-office-365-connectors"></a><span data-ttu-id="0c26e-104">Crear Conectores de Office 365</span><span class="sxs-lookup"><span data-stu-id="0c26e-104">Create Office 365 Connectors</span></span>

<span data-ttu-id="0c26e-105">Con Microsoft Teams aplicaciones, puedes agregar el conector de Office 365 existente o crear uno nuevo dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="0c26e-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one within Teams.</span></span> <span data-ttu-id="0c26e-106">Para obtener más información, [vea build your own connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).</span><span class="sxs-lookup"><span data-stu-id="0c26e-106">For more information, see [build your own connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).</span></span>

## <a name="add-a-connector-to-teams-app"></a><span data-ttu-id="0c26e-107">Agregar un conector a Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="0c26e-107">Add a connector to Teams app</span></span>

<span data-ttu-id="0c26e-108">Puede [empaquetar y](~/concepts/build-and-test/apps-package.md) [publicar el](~/concepts/deploy-and-publish/apps-publish.md) conector como parte del envío de AppSource.</span><span class="sxs-lookup"><span data-stu-id="0c26e-108">You can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your connector as part of your AppSource submission.</span></span> <span data-ttu-id="0c26e-109">Puedes distribuir el conector registrado como parte del paquete Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="0c26e-109">You can distribute your registered connector as part of your Teams app package.</span></span> <span data-ttu-id="0c26e-110">Para obtener información sobre los puntos de entrada Teams aplicación, consulta [funcionalidades](~/concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="0c26e-110">For information on entry points for Teams app, see [capabilities](~/concepts/extensibility-points.md).</span></span> <span data-ttu-id="0c26e-111">También puede proporcionar el paquete a los usuarios directamente para cargarlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="0c26e-111">You can also provide the package to users directly for uploading within Teams.</span></span>

<span data-ttu-id="0c26e-112">Para distribuir el conector, debe registrarse a través [del Panel de desarrolladores de Conectores.](https://outlook.office.com/connectors/home/login/#/publish)</span><span class="sxs-lookup"><span data-stu-id="0c26e-112">To distribute your connector, you must register through [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="0c26e-113">Cuando se registra un conector, se supone que funciona en todos los Office 365 compatibles con aplicaciones, incluidos Outlook y Teams.</span><span class="sxs-lookup"><span data-stu-id="0c26e-113">When a connector is registered, it is assumed that it works in all Office 365 products that support applications, including Outlook and Teams.</span></span> <span data-ttu-id="0c26e-114">Si ese no es el caso y debe crear un conector que solo funcione en Microsoft Teams, póngase en contacto con: Microsoft Teams correo electrónico [de envíos de aplicaciones](mailto:teamsubm@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0c26e-114">If that is not the case and you must create a connector that only works in Microsoft Teams, contact: [Microsoft Teams App Submissions email](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c26e-115">El conector se registra después de seleccionar **Guardar** en el Panel de desarrolladores de conectores.</span><span class="sxs-lookup"><span data-stu-id="0c26e-115">Your connector is registered after you select **Save** in the Connectors Developer Dashboard.</span></span> <span data-ttu-id="0c26e-116">Si quieres publicar el conector en AppSource, sigue las instrucciones de publicar la aplicación Microsoft Teams [en AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span><span class="sxs-lookup"><span data-stu-id="0c26e-116">If you want to publish your connector in AppSource, follow the instructions in [publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="0c26e-117">Si no quieres publicar la aplicación en AppSource, distribuyela directamente a la organización.</span><span class="sxs-lookup"><span data-stu-id="0c26e-117">If you do not want to publish your app in AppSource, distribute it directly to the organization.</span></span> <span data-ttu-id="0c26e-118">Después [de publicar conectores para la organización,](#publish-connectors-for-the-organization)no se requiere ninguna acción adicional en el Panel del conector.</span><span class="sxs-lookup"><span data-stu-id="0c26e-118">After [publishing connectors for your organization](#publish-connectors-for-the-organization), no further action is required on the Connector Dashboard.</span></span>

### <a name="integrate-the-configuration-experience"></a><span data-ttu-id="0c26e-119">Integrar la experiencia de configuración</span><span class="sxs-lookup"><span data-stu-id="0c26e-119">Integrate the configuration experience</span></span>

<span data-ttu-id="0c26e-120">Los usuarios pueden completar toda la experiencia de configuración del conector sin tener que salir del Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="0c26e-120">Users can complete the entire connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="0c26e-121">Para obtener la experiencia, Teams puede insertar la página de configuración directamente dentro de un iframe.</span><span class="sxs-lookup"><span data-stu-id="0c26e-121">To get the experience, Teams can embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="0c26e-122">La secuencia de operaciones es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="0c26e-122">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="0c26e-123">El usuario selecciona el conector para iniciar el proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="0c26e-123">The user selects the connector to begin the configuration process.</span></span>
1. <span data-ttu-id="0c26e-124">El usuario interactúa con la experiencia web para completar la configuración.</span><span class="sxs-lookup"><span data-stu-id="0c26e-124">The user interacts with the web experience to complete the configuration.</span></span>
1. <span data-ttu-id="0c26e-125">El usuario selecciona **Guardar**, que desencadena una devolución de llamada en el código.</span><span class="sxs-lookup"><span data-stu-id="0c26e-125">The user selects **Save**, which triggers a callback in code.</span></span>

    > [!NOTE]
    > * <span data-ttu-id="0c26e-126">El código puede procesar el evento save recuperando la configuración del webhook.</span><span class="sxs-lookup"><span data-stu-id="0c26e-126">The code can process the save event by retrieving the webhook settings.</span></span> <span data-ttu-id="0c26e-127">El código almacena el webhook para publicar eventos más adelante.</span><span class="sxs-lookup"><span data-stu-id="0c26e-127">Your code stores the webhook to post events later.</span></span>
    > * <span data-ttu-id="0c26e-128">La experiencia de configuración se carga en línea en Teams.</span><span class="sxs-lookup"><span data-stu-id="0c26e-128">The configuration experience is loaded inline within Teams.</span></span>

<span data-ttu-id="0c26e-129">Puede reutilizar la experiencia de configuración web existente o crear una versión independiente que se hospedará específicamente en Teams.</span><span class="sxs-lookup"><span data-stu-id="0c26e-129">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="0c26e-130">El código debe incluir el Microsoft Teams SDK de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0c26e-130">Your code must include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="0c26e-131">Esto proporciona al código acceso a las API para realizar operaciones comunes, como obtener el contexto de usuario, canal o equipo actual e iniciar flujos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="0c26e-131">This gives your code access to APIs to perform common operations, such as getting the current user, channel, or team context and initiate authentication flows.</span></span>

<span data-ttu-id="0c26e-132">**Para integrar la experiencia de configuración**</span><span class="sxs-lookup"><span data-stu-id="0c26e-132">**To integrate the configuration experience**</span></span>

1. <span data-ttu-id="0c26e-133">Para inicializar el SDK, llame a `microsoftTeams.initialize()`.</span><span class="sxs-lookup"><span data-stu-id="0c26e-133">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
1. <span data-ttu-id="0c26e-134">Llamada `microsoftTeams.settings.setValidityState(true)` para habilitar **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0c26e-134">Call `microsoftTeams.settings.setValidityState(true)` to enable **Save**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0c26e-135">Debe llamar como respuesta a la selección del usuario `microsoftTeams.settings.setValidityState(true)` o a la actualización de campos.</span><span class="sxs-lookup"><span data-stu-id="0c26e-135">You must call `microsoftTeams.settings.setValidityState(true)` as a response to user selection or field update.</span></span>

1. <span data-ttu-id="0c26e-136">Registrar  `microsoftTeams.settings.registerOnSaveHandler()` controlador de eventos, al que se llama cuando el usuario selecciona **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0c26e-136">Register  `microsoftTeams.settings.registerOnSaveHandler()` event handler, which is called when the user selects **Save**.</span></span>
1. <span data-ttu-id="0c26e-137">Llama `microsoftTeams.settings.setSettings()` para guardar la configuración del conector.</span><span class="sxs-lookup"><span data-stu-id="0c26e-137">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="0c26e-138">La configuración guardada también se muestra en el cuadro de diálogo de configuración si el usuario intenta actualizar una configuración existente para el conector.</span><span class="sxs-lookup"><span data-stu-id="0c26e-138">The saved settings are also shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
1. <span data-ttu-id="0c26e-139">Llamada `microsoftTeams.settings.getSettings()` para capturar propiedades de webhook, incluida la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="0c26e-139">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0c26e-140">Debe llamar cuando `microsoftTeams.settings.getSettings()` se cargue la página por primera vez en caso de reconfiguración.</span><span class="sxs-lookup"><span data-stu-id="0c26e-140">You must call `microsoftTeams.settings.getSettings()` when your page is first loaded in case of reconfiguration.</span></span>

1. <span data-ttu-id="0c26e-141">Registrar `microsoftTeams.settings.registerOnRemoveHandler()` el controlador de eventos, al que se llama cuando el usuario quita el conector.</span><span class="sxs-lookup"><span data-stu-id="0c26e-141">Register `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which is called when the user removes connector.</span></span>

<span data-ttu-id="0c26e-142">Este evento ofrece al servicio la oportunidad de realizar cualquier acción de limpieza.</span><span class="sxs-lookup"><span data-stu-id="0c26e-142">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="0c26e-143">El siguiente código proporciona un CÓDIGO HTML de ejemplo para crear una página de configuración de conector sin el servicio de atención al cliente y la compatibilidad:</span><span class="sxs-lookup"><span data-stu-id="0c26e-143">The following code provides a sample HTML to create a connector configuration page without the customer service and support:</span></span>

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

<span data-ttu-id="0c26e-144">Para autenticar al usuario como parte de la carga de la página, vea flujo de autenticación para que las [pestañas](~/tabs/how-to/authentication/auth-flow-tab.md) integren el inicio de sesión cuando la página está incrustada.</span><span class="sxs-lookup"><span data-stu-id="0c26e-144">To authenticate the user as part of loading your page, see [authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md) to integrate sign in when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="0c26e-145">Debido a motivos de compatibilidad entre clientes, el código debe llamar con la dirección URL y los métodos de devolución de llamada correctos o `microsoftTeams.authentication.registerAuthenticationHandlers()` de error antes de llamar a `authenticate()` .</span><span class="sxs-lookup"><span data-stu-id="0c26e-145">Due to cross client compatibility reasons, your code must call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success or failure callback methods before calling `authenticate()`.</span></span>

#### <a name="getsettings-response-properties"></a><span data-ttu-id="0c26e-146">`GetSettings` propiedades de respuesta</span><span class="sxs-lookup"><span data-stu-id="0c26e-146">`GetSettings` response properties</span></span>

>[!NOTE]
><span data-ttu-id="0c26e-147">Los parámetros devueltos por la llamada son diferentes al invocar este método desde una pestaña y difieren de los `getSettings` documentados en la [configuración de js](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="0c26e-147">The parameters returned by the `getSettings` call are different when you invoke this method from a tab and differ from those documented in [js settings](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

<span data-ttu-id="0c26e-148">En la tabla siguiente se proporcionan los parámetros y los detalles de las propiedades `GetSetting` de respuesta:</span><span class="sxs-lookup"><span data-stu-id="0c26e-148">The following table provides the parameters and the details of `GetSetting` response properties:</span></span>

| <span data-ttu-id="0c26e-149">Parámetros</span><span class="sxs-lookup"><span data-stu-id="0c26e-149">Parameters</span></span>   | <span data-ttu-id="0c26e-150">Detalles</span><span class="sxs-lookup"><span data-stu-id="0c26e-150">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="0c26e-151">El identificador de entidad, establecido por el código al llamar `setSettings()` a .</span><span class="sxs-lookup"><span data-stu-id="0c26e-151">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="0c26e-152">El nombre de configuración, establecido por el código al llamar `setSettings()` a .</span><span class="sxs-lookup"><span data-stu-id="0c26e-152">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="0c26e-153">La dirección URL de la página de configuración, establecida por el código al llamar `setSettings()` a .</span><span class="sxs-lookup"><span data-stu-id="0c26e-153">The URL of the configuration page, as set by your code when calling `setSettings()`.</span></span> |
| `webhookUrl` | <span data-ttu-id="0c26e-154">La dirección URL de webhook creada para el conector.</span><span class="sxs-lookup"><span data-stu-id="0c26e-154">The webhook URL created for the connector.</span></span> <span data-ttu-id="0c26e-155">Use la dirección URL de webhook para POST JSON estructurado para enviar tarjetas al canal.</span><span class="sxs-lookup"><span data-stu-id="0c26e-155">Use the webhook URL to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="0c26e-156">Se `webhookUrl` devuelve solo cuando la aplicación devuelve datos correctamente.</span><span class="sxs-lookup"><span data-stu-id="0c26e-156">The `webhookUrl` is returned only when the application returns data successfully.</span></span> |
| `appType` | <span data-ttu-id="0c26e-157">Los valores devueltos pueden ser , o corresponde a los Office 365 `mail` `groups` `teams` Mail, Office 365 Groups o Microsoft Teams respectivamente.</span><span class="sxs-lookup"><span data-stu-id="0c26e-157">The values returned can be `mail`, `groups`, or `teams` corresponding to the Office 365 Mail, Office 365 Groups, or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="0c26e-158">Identificador único que corresponde al Office 365 usuario que inició la configuración del conector.</span><span class="sxs-lookup"><span data-stu-id="0c26e-158">The unique ID corresponding to the Office 365 user who initiated the set up of the connector.</span></span> <span data-ttu-id="0c26e-159">Debe estar protegido.</span><span class="sxs-lookup"><span data-stu-id="0c26e-159">It must be secured.</span></span> <span data-ttu-id="0c26e-160">Este valor se puede usar para asociar al usuario en Office 365, que ha configurado la configuración en el servicio.</span><span class="sxs-lookup"><span data-stu-id="0c26e-160">This value can be used to associate the user in Office 365, who has set up the configuration in your service.</span></span> |

#### <a name="handle-edits"></a><span data-ttu-id="0c26e-161">Controlar ediciones</span><span class="sxs-lookup"><span data-stu-id="0c26e-161">Handle edits</span></span>

<span data-ttu-id="0c26e-162">El código debe controlar los usuarios que vuelvan a editar una configuración de conector existente.</span><span class="sxs-lookup"><span data-stu-id="0c26e-162">Your code must handle users who return to edit an existing connector configuration.</span></span> <span data-ttu-id="0c26e-163">Para ello, llame `microsoftTeams.settings.setSettings()` durante la configuración inicial con los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="0c26e-163">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="0c26e-164">`entityId` es el identificador personalizado que representa lo que el usuario ha configurado y comprendido por el servicio.</span><span class="sxs-lookup"><span data-stu-id="0c26e-164">`entityId` is the custom ID that represents what the user has configured and understood by your service.</span></span>
- <span data-ttu-id="0c26e-165">`configName` es un nombre que el código de configuración puede recuperar.</span><span class="sxs-lookup"><span data-stu-id="0c26e-165">`configName` is a name that configuration code can retrieve.</span></span>
- <span data-ttu-id="0c26e-166">`contentUrl` es una dirección URL personalizada que se carga cuando un usuario edita una configuración de conector existente.</span><span class="sxs-lookup"><span data-stu-id="0c26e-166">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span>

<span data-ttu-id="0c26e-167">Esta llamada se realiza como parte del controlador de eventos guardar.</span><span class="sxs-lookup"><span data-stu-id="0c26e-167">This call is made as part of your save event handler.</span></span> <span data-ttu-id="0c26e-168">Después, cuando se carga, el código debe llamar para rellenar previamente cualquier `contentUrl` configuración o formulario en la interfaz de usuario de `getSettings()` configuración.</span><span class="sxs-lookup"><span data-stu-id="0c26e-168">Then, when the `contentUrl` is loaded, your code must call `getSettings()` to pre populate any settings or forms in your configuration user interface.</span></span>

#### <a name="handle-removals"></a><span data-ttu-id="0c26e-169">Controlar eliminaciones</span><span class="sxs-lookup"><span data-stu-id="0c26e-169">Handle removals</span></span>

<span data-ttu-id="0c26e-170">Puede ejecutar un controlador de eventos cuando el usuario quita una configuración de conector existente.</span><span class="sxs-lookup"><span data-stu-id="0c26e-170">You can execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="0c26e-171">Para registrar este controlador, llame a `microsoftTeams.settings.registerOnRemoveHandler()` .</span><span class="sxs-lookup"><span data-stu-id="0c26e-171">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="0c26e-172">Este controlador se usa para realizar operaciones de limpieza, como quitar entradas de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="0c26e-172">This handler is used to perform cleanup operations, such as removing entries from a database.</span></span>

### <a name="include-the-connector-in-your-manifest"></a><span data-ttu-id="0c26e-173">Incluir el conector en el manifiesto</span><span class="sxs-lookup"><span data-stu-id="0c26e-173">Include the connector in your Manifest</span></span>

<span data-ttu-id="0c26e-174">Descargue el auto generado `Teams app manifest` desde el portal.</span><span class="sxs-lookup"><span data-stu-id="0c26e-174">Download the auto generated `Teams app manifest` from the portal.</span></span> <span data-ttu-id="0c26e-175">Realice los siguientes pasos antes de probar o publicar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="0c26e-175">Perform the following steps, before testing or publishing the app:</span></span>

1. <span data-ttu-id="0c26e-176">[Incluya dos iconos](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="0c26e-176">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
1. <span data-ttu-id="0c26e-177">Modifique la `icons` parte del manifiesto para incluir los nombres de archivo de los iconos en lugar de las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="0c26e-177">Modify the `icons` portion of the manifest to include the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="0c26e-178">La siguiente manifest.jsen el archivo contiene los elementos necesarios para probar y enviar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="0c26e-178">The following manifest.json file contains the elements needed to test and submit the app:</span></span>

> [!NOTE]
> <span data-ttu-id="0c26e-179">Reemplace `id` y en el siguiente ejemplo por el GUID del `connectorId` conector.</span><span class="sxs-lookup"><span data-stu-id="0c26e-179">Replace `id` and `connectorId` in the following example with the GUID of the connector.</span></span>

#### <a name="example-of-manifestjson-with-connector"></a><span data-ttu-id="0c26e-180">Ejemplo de manifest.jscon conector</span><span class="sxs-lookup"><span data-stu-id="0c26e-180">Example of manifest.json with connector</span></span>

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

## <a name="enable-or-disable-connectors-in-teams"></a><span data-ttu-id="0c26e-181">Habilitar o deshabilitar conectores en Teams</span><span class="sxs-lookup"><span data-stu-id="0c26e-181">Enable or disable connectors in Teams</span></span>

<span data-ttu-id="0c26e-182">El módulo Exchange Online PowerShell V2 usa la autenticación moderna y funciona con la autenticación multifactor, denominada MFA para conectarse Exchange todos los entornos de PowerShell relacionados en Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="0c26e-182">The Exchange Online PowerShell V2 module uses modern authentication and works with multi factor authentication, called MFA for connecting to all Exchange related PowerShell environments in Microsoft 365.</span></span> <span data-ttu-id="0c26e-183">Los administradores pueden usar Exchange Online PowerShell para deshabilitar conectores para un inquilino completo o un buzón de grupo específico, lo que afecta a todos los usuarios de ese espacio empresarial o buzón.</span><span class="sxs-lookup"><span data-stu-id="0c26e-183">Admins can use Exchange Online PowerShell to disable connectors for an entire tenant or a specific group mailbox, affecting all users in that tenant or mailbox.</span></span> <span data-ttu-id="0c26e-184">No es posible deshabilitar para algunos y no para otros.</span><span class="sxs-lookup"><span data-stu-id="0c26e-184">It is not possible to disable for some and not others.</span></span> <span data-ttu-id="0c26e-185">Además, los conectores están deshabilitados de forma predeterminada para Government Community Cloud, denominados GCC inquilinos.</span><span class="sxs-lookup"><span data-stu-id="0c26e-185">Also, connectors are disabled by default for Government Community Cloud, called GCC tenants.</span></span>

<span data-ttu-id="0c26e-186">La configuración de nivel de espacio empresarial invalida la configuración de nivel de grupo.</span><span class="sxs-lookup"><span data-stu-id="0c26e-186">The tenant level setting overrides the group level setting.</span></span> <span data-ttu-id="0c26e-187">Por ejemplo, si un administrador habilita conectores para el grupo y los deshabilita en el inquilino, se deshabilitan los conectores para el grupo.</span><span class="sxs-lookup"><span data-stu-id="0c26e-187">For example, if an admin enables connectors for the group and disables them on the tenant, connectors for the group is disabled.</span></span> <span data-ttu-id="0c26e-188">Para habilitar un conector en Teams, conéctese a [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) mediante la autenticación moderna con o sin MFA.</span><span class="sxs-lookup"><span data-stu-id="0c26e-188">To enable a connector in Teams, [connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) using modern authentication with or without MFA.</span></span>

### <a name="commands-to-enable-or-disable-connectors"></a><span data-ttu-id="0c26e-189">Comandos para habilitar o deshabilitar conectores</span><span class="sxs-lookup"><span data-stu-id="0c26e-189">Commands to enable or disable connectors</span></span>

<span data-ttu-id="0c26e-190">Ejecute los comandos siguientes en Exchange Online PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0c26e-190">Run the following commands in Exchange Online PowerShell:</span></span>

* <span data-ttu-id="0c26e-191">Para deshabilitar conectores para el inquilino: `Set-OrganizationConfig -ConnectorsEnabled:$false` .</span><span class="sxs-lookup"><span data-stu-id="0c26e-191">To disable connectors for the tenant: `Set-OrganizationConfig -ConnectorsEnabled:$false`.</span></span>
* <span data-ttu-id="0c26e-192">Para deshabilitar los mensajes que se pueden usar para el inquilino: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` .</span><span class="sxs-lookup"><span data-stu-id="0c26e-192">To disable actionable messages for the tenant: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false`.</span></span>
* <span data-ttu-id="0c26e-193">Para habilitar conectores para Teams, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="0c26e-193">To enable connectors for Teams, run the following commands:</span></span>
  * `Set-OrganizationConfig -ConnectorsEnabled:$true `
  * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
  * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

<span data-ttu-id="0c26e-194">Para obtener más información sobre el intercambio de módulos de PowerShell, [vea Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="0c26e-194">For more information on PowerShell module exchange, see [Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true).</span></span> <span data-ttu-id="0c26e-195">Para habilitar o deshabilitar los Outlook, [conecta aplicaciones a tus grupos en Outlook](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us).</span><span class="sxs-lookup"><span data-stu-id="0c26e-195">To enable or disable Outlook connectors, [connect apps to your groups in Outlook](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us).</span></span>

## <a name="test-your-connector"></a><span data-ttu-id="0c26e-196">Probar el conector</span><span class="sxs-lookup"><span data-stu-id="0c26e-196">Test your connector</span></span>

<span data-ttu-id="0c26e-197">Para probar el conector, cárbalo en un equipo con cualquier otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="0c26e-197">To test your connector, upload it to a team with any other app.</span></span> <span data-ttu-id="0c26e-198">Puede crear un paquete .zip mediante el archivo de manifiesto de los dos archivos de icono y conectores Panel de desarrolladores, modificado según se indica en Incluir el conector [en el manifiesto](#include-the-connector-in-your-manifest).</span><span class="sxs-lookup"><span data-stu-id="0c26e-198">You can create a .zip package using the manifest file from the two icon files and connectors Developer Dashboard, modified as directed in [Include the connector in your Manifest](#include-the-connector-in-your-manifest).</span></span>

<span data-ttu-id="0c26e-199">Después de cargar la aplicación, abre la lista de conectores desde cualquier canal.</span><span class="sxs-lookup"><span data-stu-id="0c26e-199">After you upload the app, open the connectors list from any channel.</span></span> <span data-ttu-id="0c26e-200">Desplácese a la parte inferior para ver la aplicación en la **sección Cargado:**</span><span class="sxs-lookup"><span data-stu-id="0c26e-200">Scroll to the bottom to see your app in the **Uploaded** section:</span></span>

![Captura de pantalla de una sección cargada en el cuadro de diálogo conector](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> <span data-ttu-id="0c26e-202">El flujo se produce por completo en Microsoft Teams como una experiencia hospedada.</span><span class="sxs-lookup"><span data-stu-id="0c26e-202">The flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="0c26e-203">Para comprobar que `HttpPOST` la acción funciona correctamente, [envíe mensajes al conector](~/webhooks-and-connectors/how-to/connectors-using.md).</span><span class="sxs-lookup"><span data-stu-id="0c26e-203">To verify that `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-the-organization"></a><span data-ttu-id="0c26e-204">Publicar conectores para la organización</span><span class="sxs-lookup"><span data-stu-id="0c26e-204">Publish connectors for the organization</span></span>

<span data-ttu-id="0c26e-205">Si quieres que el conector solo esté disponible para los usuarios de la organización, puedes cargar la aplicación de conector personalizada en el catálogo de aplicaciones [de la organización.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="0c26e-205">If you want the connector to be available only to the users in your organization, you can upload your custom connector app to your [organization's app catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span>

<span data-ttu-id="0c26e-206">Después de cargar el paquete de la aplicación para configurar y usar el conector en un equipo, instale el conector desde el catálogo de aplicaciones de la organización.</span><span class="sxs-lookup"><span data-stu-id="0c26e-206">After uploading the app package to configure and use the connector in a team, install the connector from the organization's app catalog.</span></span>

<span data-ttu-id="0c26e-207">**Para configurar un conector**</span><span class="sxs-lookup"><span data-stu-id="0c26e-207">**To set up a connector**</span></span>

1. <span data-ttu-id="0c26e-208">Selecciona **Aplicaciones en** la barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="0c26e-208">Select **Apps** from the left navigation bar.</span></span>
1. <span data-ttu-id="0c26e-209">En la **sección Aplicaciones,** seleccione **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="0c26e-209">In the **Apps** section, select **Connectors**.</span></span>
1. <span data-ttu-id="0c26e-210">Seleccione el conector que desea agregar.</span><span class="sxs-lookup"><span data-stu-id="0c26e-210">Select the connector that you want to add.</span></span> <span data-ttu-id="0c26e-211">Aparece una ventana de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="0c26e-211">A pop up dialog window appears.</span></span>
1. <span data-ttu-id="0c26e-212">En el menú desplegable, seleccione **Agregar a un equipo**.</span><span class="sxs-lookup"><span data-stu-id="0c26e-212">From the dropdown menu, select **Add to a team**.</span></span>
1. <span data-ttu-id="0c26e-213">En el cuadro de búsqueda, escriba un nombre de equipo o canal.</span><span class="sxs-lookup"><span data-stu-id="0c26e-213">In the search box, type a team or channel name.</span></span>
1. <span data-ttu-id="0c26e-214">Seleccione **Configurar un conector en** el menú desplegable de la esquina inferior derecha de la ventana de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0c26e-214">Select **Set up a Connector** from the dropdown menu in the bottom right corner of the dialog window.</span></span>

<span data-ttu-id="0c26e-215">El conector está disponible en la sección &#9679;&#9679;&#9679; > **Más opciones** Conectores todos los conectores para  >    >    >  **su equipo** para ese equipo.</span><span class="sxs-lookup"><span data-stu-id="0c26e-215">The connector is available in the section &#9679;&#9679;&#9679; > **More options** > **Connectors** > **All** > **Connectors for your team** for that team.</span></span> <span data-ttu-id="0c26e-216">Puedes desplazarte a esta sección o buscar la aplicación del conector.</span><span class="sxs-lookup"><span data-stu-id="0c26e-216">You can navigate by scrolling to this section or search for the connector app.</span></span> <span data-ttu-id="0c26e-217">Para configurar o modificar el conector, seleccione **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="0c26e-217">To configure or modify the connector, select **Configure**.</span></span>

## <a name="distribute-webhook-and-connector"></a><span data-ttu-id="0c26e-218">Distribuir webhook y conector</span><span class="sxs-lookup"><span data-stu-id="0c26e-218">Distribute webhook and connector</span></span>

1. <span data-ttu-id="0c26e-219">[Configure un webhook entrante](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) directamente para su equipo.</span><span class="sxs-lookup"><span data-stu-id="0c26e-219">[Set up an Incoming Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) directly for your team.</span></span>
1. <span data-ttu-id="0c26e-220">Agregue una [página de configuración](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) y publique el [webhook entrante](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) en un conector de O365.</span><span class="sxs-lookup"><span data-stu-id="0c26e-220">Add a [configuration page](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) and [publish your Incoming Webhook](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) in a O365 Connector.</span></span>
1. <span data-ttu-id="0c26e-221">Empaquetar y publicar el conector como parte del envío [de AppSource.](~/concepts/deploy-and-publish/office-store-guidance.md)</span><span class="sxs-lookup"><span data-stu-id="0c26e-221">Package and publish your connector as part of your [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) submission.</span></span>

## <a name="code-sample"></a><span data-ttu-id="0c26e-222">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="0c26e-222">Code sample</span></span>

<span data-ttu-id="0c26e-223">En la tabla siguiente se proporciona el nombre de ejemplo y su descripción:</span><span class="sxs-lookup"><span data-stu-id="0c26e-223">The following table provides the sample name and its description:</span></span>

|<span data-ttu-id="0c26e-224">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="0c26e-224">**Sample name**</span></span> | <span data-ttu-id="0c26e-225">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="0c26e-225">**Description**</span></span> | <span data-ttu-id="0c26e-226">**.NET**</span><span class="sxs-lookup"><span data-stu-id="0c26e-226">**.NET**</span></span> | <span data-ttu-id="0c26e-227">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="0c26e-227">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="0c26e-228">Conectores</span><span class="sxs-lookup"><span data-stu-id="0c26e-228">Connectors</span></span>    | <span data-ttu-id="0c26e-229">Sample Office 365 Connector que genera notificaciones en Teams canal.</span><span class="sxs-lookup"><span data-stu-id="0c26e-229">Sample Office 365 Connector generating notifications to Teams channel.</span></span>|   [<span data-ttu-id="0c26e-230">View</span><span class="sxs-lookup"><span data-stu-id="0c26e-230">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="0c26e-231">View</span><span class="sxs-lookup"><span data-stu-id="0c26e-231">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="0c26e-232">Ejemplo de conectores genéricos</span><span class="sxs-lookup"><span data-stu-id="0c26e-232">Generic connectors sample</span></span> |<span data-ttu-id="0c26e-233">Código de ejemplo para un conector genérico que es fácil de personalizar para cualquier sistema que admita webhooks.</span><span class="sxs-lookup"><span data-stu-id="0c26e-233">Sample code for a generic connector that is easy to customize for any system that supports webhooks.</span></span>|  | [<span data-ttu-id="0c26e-234">View</span><span class="sxs-lookup"><span data-stu-id="0c26e-234">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="see-also"></a><span data-ttu-id="0c26e-235">Vea también</span><span class="sxs-lookup"><span data-stu-id="0c26e-235">See also</span></span>

* [<span data-ttu-id="0c26e-236">Crear y enviar mensajes</span><span class="sxs-lookup"><span data-stu-id="0c26e-236">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
* [<span data-ttu-id="0c26e-237">Crear un webhook entrante</span><span class="sxs-lookup"><span data-stu-id="0c26e-237">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="0c26e-238">Crear un Conector de Office 365</span><span class="sxs-lookup"><span data-stu-id="0c26e-238">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
