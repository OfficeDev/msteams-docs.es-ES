### <a name="_layoutcshtml"></a><span data-ttu-id="363b7-101">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="363b7-101">_Layout.cshtml</span></span>

<span data-ttu-id="363b7-102">Para que la pestaña se muestre en Teams, debe incluir el SDK de cliente Microsoft Teams **JavaScript** e incluir una llamada después de `microsoftTeams.initialize()` que se cargue la página.</span><span class="sxs-lookup"><span data-stu-id="363b7-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="363b7-103">Así se comunican la pestaña y Teams cliente:</span><span class="sxs-lookup"><span data-stu-id="363b7-103">This is how your tab and the Teams client communicate:</span></span>

- <span data-ttu-id="363b7-104">Navegue a la **carpeta Shared,** **abra _Layout.cshtml** y agregue lo siguiente a la `<head>` etiqueta:</span><span class="sxs-lookup"><span data-stu-id="363b7-104">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

>[!IMPORTANT]
><span data-ttu-id="363b7-105">No copie ni pegue las direcciones URL de esta página, ya que es posible que `<script src="...">` no representen la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="363b7-105">Don't copy/paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="363b7-106">Para obtener la versión más reciente del SDK, vaya siempre a: Microsoft Teams [API de JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).</span><span class="sxs-lookup"><span data-stu-id="363b7-106">To get the latest version of the SDK, always go to: [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="363b7-107">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="363b7-107">Tab.cshtml</span></span>

<span data-ttu-id="363b7-108">Abra **Tab.cshtml** y actualice el incrustado `<script>` de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="363b7-108">Open **Tab.cshtml** and update the embedded `<script>` as follows:</span></span>

- <span data-ttu-id="363b7-109">En la parte superior del script, llame `microsoftTeams.initialize()` a .</span><span class="sxs-lookup"><span data-stu-id="363b7-109">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

- <span data-ttu-id="363b7-110">Actualice los `websiteUrl` valores y de cada función con la dirección URL de https `contentUrl` ngrok a la pestaña.</span><span class="sxs-lookup"><span data-stu-id="363b7-110">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

<span data-ttu-id="363b7-111">El código ahora debería tener el siguiente aspecto con **y8rCgT2b** reemplazado por la dirección URL de ngrok:</span><span class="sxs-lookup"><span data-stu-id="363b7-111">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

```javascript
    microsoftTeams.initialize();

    let saveGray = () => {
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            microsoftTeams.settings.setSettings({
                websiteUrl: `https://y8rCgT2b.ngrok.io`,
                contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                entityId: "grayIconTab",
                suggestedDisplayName: "MyNewTab"
            });
            saveEvent.notifySuccess();
        });
    }

    let saveRed = () => {
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            microsoftTeams.settings.setSettings({
                websiteUrl: `https://y8rCgT2b.ngrok.io`,
                contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                entityId: "redIconTab",
                suggestedDisplayName: "MyNewTab"
            });
            saveEvent.notifySuccess();
        });
    }
```

<span data-ttu-id="363b7-112">Asegúrese de guardar el **tab.cshtml actualizado.**</span><span class="sxs-lookup"><span data-stu-id="363b7-112">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="363b7-113">Compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="363b7-113">Build and run your application</span></span>

- <span data-ttu-id="363b7-114">En Visual Studio presione **F5** o **elija Iniciar depuración** en el **menú** Depurar.</span><span class="sxs-lookup"><span data-stu-id="363b7-114">In Visual Studio press **F5**, or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="363b7-115">Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="363b7-115">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="363b7-116">Debe tener la aplicación en ejecución Visual Studio y ngrok para completar esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="363b7-116">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="363b7-117">Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en **ella, mantenga ngrok en ejecución**.</span><span class="sxs-lookup"><span data-stu-id="363b7-117">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="363b7-118">Seguirá escuchando y reanudará el enrutamiento de la solicitud de la aplicación cuando se reinicie en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="363b7-118">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="363b7-119">Si tiene que reiniciar el servicio ngrok, devolverá una nueva dirección URL y tendrá que actualizar la aplicación con la nueva dirección URL.</span><span class="sxs-lookup"><span data-stu-id="363b7-119">If you have to restart the ngrok service it will return a new URL and you'll have to update your application with the new URL.</span></span>

## <a name="upload-your-tab-to-teams"></a><span data-ttu-id="363b7-120">Upload la pestaña a Teams</span><span class="sxs-lookup"><span data-stu-id="363b7-120">Upload your tab to Teams</span></span>

>[!Note]
> <span data-ttu-id="363b7-121">Usamos App Studio para editar el **archivomanifest.jsy** cargar el paquete completado en Teams.</span><span class="sxs-lookup"><span data-stu-id="363b7-121">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="363b7-122">También puede editar manualmente el **archivomanifest.jsen** si lo prefiere.</span><span class="sxs-lookup"><span data-stu-id="363b7-122">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="363b7-123">Si lo hace, asegúrese de compilar la solución de nuevo para crear el **archivotab.zip** que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="363b7-123">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="363b7-124">Abra el Microsoft Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="363b7-124">Open the Microsoft Teams client.</span></span> <span data-ttu-id="363b7-125">Si usa la versión [basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end con las herramientas de desarrollo [del explorador.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="363b7-125">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="363b7-126">Abre App studio y selecciona la **pestaña Editor de manifiestos.**</span><span class="sxs-lookup"><span data-stu-id="363b7-126">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="363b7-127">Selecciona el **icono Importar una aplicación existente** en el editor de manifiestos para empezar a actualizar el paquete de la aplicación para la pestaña. El código fuente viene con su propio manifiesto parcialmente completo.</span><span class="sxs-lookup"><span data-stu-id="363b7-127">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="363b7-128">El nombre del paquete de la **aplicación estab.zip**.</span><span class="sxs-lookup"><span data-stu-id="363b7-128">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="363b7-129">Debe encontrarse aquí:</span><span class="sxs-lookup"><span data-stu-id="363b7-129">It should be found here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

- <span data-ttu-id="363b7-130">Upload **tab.zip** a App Studio.</span><span class="sxs-lookup"><span data-stu-id="363b7-130">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="363b7-131">Actualizar el paquete de la aplicación con el editor de manifiestos</span><span class="sxs-lookup"><span data-stu-id="363b7-131">Update your app package with Manifest editor</span></span>

<span data-ttu-id="363b7-132">Una vez que hayas cargado el paquete de la aplicación en App Studio, tendrás que terminar de configurarlo.</span><span class="sxs-lookup"><span data-stu-id="363b7-132">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="363b7-133">Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="363b7-133">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="363b7-134">Hay una lista de pasos en el lado izquierdo del editor de manifiesto y, a la derecha, una lista de propiedades que necesitan tener valores para cada uno de esos pasos.</span><span class="sxs-lookup"><span data-stu-id="363b7-134">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="363b7-135">Gran parte de la información ha sido proporcionada por su *manifest.js,* pero hay algunos campos que necesitará actualizar:</span><span class="sxs-lookup"><span data-stu-id="363b7-135">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="363b7-136">Detalles: Detalles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="363b7-136">Details: App details</span></span>

<span data-ttu-id="363b7-137">En la *sección Detalles de la* aplicación:</span><span class="sxs-lookup"><span data-stu-id="363b7-137">In the *App details* section:</span></span>

- <span data-ttu-id="363b7-138">*Identificación:* seleccione **Generar para** reemplazar el identificador de marcador de posición con el GUID necesario para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="363b7-138">*Identification*: select **Generate** to replace the placeholder id with the required GUID for your tab.</span></span>

- <span data-ttu-id="363b7-139">*Información del desarrollador:* actualice el campo **Dirección URL** del sitio web con la dirección URL HTTPS de *ngrok.*</span><span class="sxs-lookup"><span data-stu-id="363b7-139">*Developer information*: update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="363b7-140">*Direcciones URL de la* aplicación: actualice la **declaración de privacidad a** y `https://<yourngrokurl>/privacy` los **Términos de uso** para `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="363b7-140">*App URLs*: update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="363b7-141">Capacidades: pestañas</span><span class="sxs-lookup"><span data-stu-id="363b7-141">Capabilities: Tabs</span></span>

<span data-ttu-id="363b7-142">En la *sección Pestañas:*</span><span class="sxs-lookup"><span data-stu-id="363b7-142">In the *Tabs* section:</span></span>

- <span data-ttu-id="363b7-143">*Ficha Equipo:* seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="363b7-143">*Team Tab*: select **Add**.</span></span>

- <span data-ttu-id="363b7-144">En la ventana emergente de la pestaña Equipo, actualice la *dirección URL de configuración* a `https://<yourngrokurl>/tab` .</span><span class="sxs-lookup"><span data-stu-id="363b7-144">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="363b7-145">Por último, asegúrese de que *puede actualizar la configuración. Los cuadros* de *chat* equipo y grupo están activados y selecciona **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="363b7-145">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="363b7-146">Finalizar: dominios y permisos</span><span class="sxs-lookup"><span data-stu-id="363b7-146">Finish: Domains and permissions</span></span>

<span data-ttu-id="363b7-147">En la *sección Dominios y permisos:*</span><span class="sxs-lookup"><span data-stu-id="363b7-147">In the *Domains and permissions* section:</span></span>

- <span data-ttu-id="363b7-148">El *campo Dominios de las pestañas* debe contener la dirección URL de ngrok sin el prefijo HTTPS - `<yourngrokurl>.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="363b7-148">The *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="363b7-149">Finalizar: probar y distribuir</span><span class="sxs-lookup"><span data-stu-id="363b7-149">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="363b7-150">En el **campo** Descripción de la derecha verá la siguiente advertencia:</span><span class="sxs-lookup"><span data-stu-id="363b7-150">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="363b7-151">&#9888; "**La matriz 'validDomains' no puede contener un sitio de túnel...**"</span><span class="sxs-lookup"><span data-stu-id="363b7-151">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="363b7-152">Esta advertencia puede omitirse mientras se prueba la pestaña.</span><span class="sxs-lookup"><span data-stu-id="363b7-152">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="363b7-153">En la *sección Probar y* distribuir:</span><span class="sxs-lookup"><span data-stu-id="363b7-153">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="363b7-154">Seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="363b7-154">Select **Install**.</span></span>

- <span data-ttu-id="363b7-155">En el campo Agregar *a* un equipo o chat de la ventana emergente, escriba el equipo y seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="363b7-155">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="363b7-156">En la siguiente ventana emergente, elija el canal de grupo en el que desea que se muestre la pestaña y **seleccione Configurar**.</span><span class="sxs-lookup"><span data-stu-id="363b7-156">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="363b7-157">En la ventana emergente final, seleccione un valor para la página de pestaña (ya sea un icono rojo o gris) y **seleccione Guardar**.</span><span class="sxs-lookup"><span data-stu-id="363b7-157">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="363b7-158">Para ver la pestaña, vaya al equipo en el que la instaló y selecciónelo en la barra de pestañas.</span><span class="sxs-lookup"><span data-stu-id="363b7-158">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="363b7-159">Se debe mostrar la página que eligió durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="363b7-159">The page that you chose during configuration should be displayed.</span></span>
