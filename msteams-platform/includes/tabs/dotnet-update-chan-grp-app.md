### <a name="_layoutcshtml"></a><span data-ttu-id="1967e-101">_Layout. cshtml</span><span class="sxs-lookup"><span data-stu-id="1967e-101">_Layout.cshtml</span></span>

<span data-ttu-id="1967e-102">Para que la pestaña aparezca en Microsoft Teams, debe incluir el **SDK del cliente de JavaScript para Microsoft Teams** e incluir una llamada a `microsoftTeams.initialize()` después de que se cargue la página.</span><span class="sxs-lookup"><span data-stu-id="1967e-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="1967e-103">Así es cómo se comunican la pestaña y el cliente de Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="1967e-103">This is how your tab and the Teams client communicate:</span></span>

- <span data-ttu-id="1967e-104">Navegue hasta la carpeta **compartida** , Abra **_Layout. cshtml**y agregue lo siguiente a la `<head>` etiqueta:</span><span class="sxs-lookup"><span data-stu-id="1967e-104">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
><span data-ttu-id="1967e-105">No copie ni pegue las `<script src="...">` direcciones URL de esta página, ya que es posible que no representen la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="1967e-105">Don't copy/paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="1967e-106">Para obtener la versión más reciente del SDK, vaya siempre a: [API de JavaScript de Microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js.com).</span><span class="sxs-lookup"><span data-stu-id="1967e-106">To get the latest version of the SDK, always go to: [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js.com).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="1967e-107">TAB. cshtml</span><span class="sxs-lookup"><span data-stu-id="1967e-107">Tab.cshtml</span></span>

<span data-ttu-id="1967e-108">Abra el **. cshtml** y actualice el insertado `<script>` de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="1967e-108">Open **Tab.cshtml** and update the embedded `<script>` as follows:</span></span>

- <span data-ttu-id="1967e-109">En la parte superior del script, llame `microsoftTeams.initialize()`a.</span><span class="sxs-lookup"><span data-stu-id="1967e-109">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

- <span data-ttu-id="1967e-110">Actualice los `websiteUrl` valores `contentUrl` y en cada función con la dirección URL https ngrok a su ficha.</span><span class="sxs-lookup"><span data-stu-id="1967e-110">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

<span data-ttu-id="1967e-111">El código ahora debería ser similar al siguiente con **y8rCgT2b** reemplazado por su dirección URL de ngrok:</span><span class="sxs-lookup"><span data-stu-id="1967e-111">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

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

<span data-ttu-id="1967e-112">Asegúrese de guardar la **pestaña. cshtml**actualizada.</span><span class="sxs-lookup"><span data-stu-id="1967e-112">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="1967e-113">Compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="1967e-113">Build and run your application</span></span>

- <span data-ttu-id="1967e-114">En Visual Studio, presione **F5**o elija **iniciar depuración** en el menú **depurar** .</span><span class="sxs-lookup"><span data-stu-id="1967e-114">In Visual Studio press **F5**, or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="1967e-115">Compruebe que **ngrok** se está ejecutando y que funciona correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL https ngrok que se proporcionó en la ventana del símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="1967e-115">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="1967e-116">Debe tener la aplicación en Visual Studio y ngrok en ejecución para completar este inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="1967e-116">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="1967e-117">Si necesita detener la ejecución de la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución**.</span><span class="sxs-lookup"><span data-stu-id="1967e-117">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="1967e-118">Seguirá escuchando y reanudará el enrutamiento de la solicitud de la aplicación cuando se reinicie en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1967e-118">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="1967e-119">Si tiene que reiniciar el servicio ngrok, devolverá una nueva dirección URL y tendrá que actualizar la aplicación con la nueva dirección URL.</span><span class="sxs-lookup"><span data-stu-id="1967e-119">If you have to restart the ngrok service it will return a new URL and you'll have to update your application with the new URL.</span></span>

## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="1967e-120">Cargar la pestaña en Teams con App Studio</span><span class="sxs-lookup"><span data-stu-id="1967e-120">Upload your tab to Teams with App Studio</span></span>

>[!Note]
> <span data-ttu-id="1967e-121">Usamos App Studio para editar el archivo **manifest. JSON** y cargar el paquete completado en Teams.</span><span class="sxs-lookup"><span data-stu-id="1967e-121">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="1967e-122">También puede editar manualmente el archivo **manifest. JSON** si lo prefiere.</span><span class="sxs-lookup"><span data-stu-id="1967e-122">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="1967e-123">Si lo hace, asegúrese de volver a crear la solución para crear el archivo **. zip de pestañas** que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="1967e-123">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="1967e-124">Abra el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1967e-124">Open the Microsoft Teams client.</span></span> <span data-ttu-id="1967e-125">Si usa la [versión basada en Web](https://teams.microsoft.com) , puede inspeccionar el código Front-end con las [herramientas de desarrollo](~/tabs/how-to/developer-tools.md)de su explorador.</span><span class="sxs-lookup"><span data-stu-id="1967e-125">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="1967e-126">Abra App Studio y seleccione la pestaña **Editor de manifiestos** .</span><span class="sxs-lookup"><span data-stu-id="1967e-126">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="1967e-127">Seleccione el icono **importar una aplicación existente** en el editor de manifiestos para empezar a actualizar el paquete de la aplicación de la pestaña. El código fuente incluye su propio manifiesto parcialmente completado.</span><span class="sxs-lookup"><span data-stu-id="1967e-127">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="1967e-128">El nombre del paquete de la aplicación es **Tab. zip**.</span><span class="sxs-lookup"><span data-stu-id="1967e-128">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="1967e-129">Se debe encontrar aquí:</span><span class="sxs-lookup"><span data-stu-id="1967e-129">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- <span data-ttu-id="1967e-130">Cargue la **ficha. zip** en App Studio.</span><span class="sxs-lookup"><span data-stu-id="1967e-130">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="1967e-131">Actualizar el paquete de la aplicación con el editor de manifiestos</span><span class="sxs-lookup"><span data-stu-id="1967e-131">Update your app package with Manifest editor</span></span>

<span data-ttu-id="1967e-132">Una vez que haya cargado el paquete de la aplicación en App Studio, tendrá que finalizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="1967e-132">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="1967e-133">Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiestos.</span><span class="sxs-lookup"><span data-stu-id="1967e-133">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="1967e-134">Hay una lista de pasos en la parte izquierda del editor de manifiestos y, a la derecha, una lista de propiedades que deben tener valores para cada uno de estos pasos.</span><span class="sxs-lookup"><span data-stu-id="1967e-134">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="1967e-135">La gran parte de la información se ha proporcionado en *manifest. JSON* , pero hay algunos campos que debe actualizar:</span><span class="sxs-lookup"><span data-stu-id="1967e-135">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="1967e-136">Detalles: detalles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1967e-136">Details: App details</span></span>

- <span data-ttu-id="1967e-137">En *identificación* , seleccione ***generar*** para reemplazar el identificador del marcador de posición por el GUID necesario para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="1967e-137">Under *Identification* select ***Generate*** to replace the placeholder id with the required GUID for your tab.</span></span>

- <span data-ttu-id="1967e-138">En *información para desarrolladores* , actualice el campo **dirección URL del sitio web** con la dirección URL https de *ngrok* .</span><span class="sxs-lookup"><span data-stu-id="1967e-138">Under *Developer information* update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="1967e-139">En *direcciones URL de aplicaciones* , actualice los campos **declaración de privacidad** y **condiciones de uso** URL con la dirección URL https de *ngrok* .</span><span class="sxs-lookup"><span data-stu-id="1967e-139">Under *App URLs* update the **Privacy statement** and **Terms of use** URL fields with your *ngrok* HTTPS URL.</span></span> <span data-ttu-id="1967e-140">Recuerde que debe incluir las rutas de */privacy* y */tou* al final de las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="1967e-140">Remember to include the */privacy* and */tou* paths at the end of the URLs.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="1967e-141">Capacidades: pestañas</span><span class="sxs-lookup"><span data-stu-id="1967e-141">Capabilities: Tabs</span></span>

<span data-ttu-id="1967e-142">En la sección de *tabulaciones* :</span><span class="sxs-lookup"><span data-stu-id="1967e-142">In the *Tabs* section:</span></span>

- <span data-ttu-id="1967e-143">En la *pestaña equipo* , seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1967e-143">Under *Team Tab* select **Add**.</span></span>

- <span data-ttu-id="1967e-144">En la ventana emergente de la pestaña equipo, actualice la *dirección URL de configuración* a `https://<yourngrokurl>/tab`.</span><span class="sxs-lookup"><span data-stu-id="1967e-144">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="1967e-145">Por último, asegúrese de que la configuración de se \*puede actualizar. \*Los cuadros equipo y *grupo de chat* están seleccionados y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1967e-145">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="1967e-146">Finalizar: dominios y permisos</span><span class="sxs-lookup"><span data-stu-id="1967e-146">Finish: Domains and permissions</span></span>

<span data-ttu-id="1967e-147">En la sección *dominios y permisos* , los *dominios del campo de pestañas* deben contener la dirección URL de ngrok sin el `<yourngrokurl>.ngrok.io/`prefijo https.</span><span class="sxs-lookup"><span data-stu-id="1967e-147">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="test-and-distribute-test-and-distribute"></a><span data-ttu-id="1967e-148">Pruebas y distribución: probar y distribuir</span><span class="sxs-lookup"><span data-stu-id="1967e-148">Test and distribute: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="1967e-149">En el campo **Descripción** de la derecha, verá la siguiente ADVERTENCIA:</span><span class="sxs-lookup"><span data-stu-id="1967e-149">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="1967e-150">&#9888; "**la matriz ' validDomains ' no puede contener un sitio de túnel...**"</span><span class="sxs-lookup"><span data-stu-id="1967e-150">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="1967e-151">Esta advertencia puede omitirse mientras se prueba la pestaña.</span><span class="sxs-lookup"><span data-stu-id="1967e-151">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="1967e-152">En la sección *probar y distribuir* :</span><span class="sxs-lookup"><span data-stu-id="1967e-152">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="1967e-153">Haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="1967e-153">Select **Install**.</span></span>

- <span data-ttu-id="1967e-154">En el campo *Agregar a un equipo o chat* de la ventana emergente, especifique el equipo y seleccione **instalar**.</span><span class="sxs-lookup"><span data-stu-id="1967e-154">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="1967e-155">En la siguiente ventana emergente, elija el canal de equipo en el que desea que se muestre la pestaña y seleccione **configurar**.</span><span class="sxs-lookup"><span data-stu-id="1967e-155">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="1967e-156">En la última ventana emergente, seleccione un valor para la página de ficha (bien un icono rojo o gris) y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1967e-156">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="1967e-157">Para ver la pestaña, navegue hasta el equipo en el que se instaló y selecciónela en la barra de pestañas.</span><span class="sxs-lookup"><span data-stu-id="1967e-157">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="1967e-158">Debe mostrarse la página elegida durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="1967e-158">The page that you chose during configuration should be displayed.</span></span>
