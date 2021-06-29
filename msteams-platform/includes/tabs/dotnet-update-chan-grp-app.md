### <a name="_layoutcshtml"></a><span data-ttu-id="0bc1b-101">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="0bc1b-101">_Layout.cshtml</span></span>

<span data-ttu-id="0bc1b-102">Para que la pestaña se muestre en Teams, debe incluir el SDK de cliente Microsoft Teams **JavaScript** e incluir una llamada después de `microsoftTeams.initialize()` que se cargue la página.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="0bc1b-103">Así se comunican la pestaña y Teams cliente:</span><span class="sxs-lookup"><span data-stu-id="0bc1b-103">This is how your tab and the Teams client communicate:</span></span>

<span data-ttu-id="0bc1b-104">Vaya a la **carpeta Shared,** abra **_Layout.cshtml** y agregue lo siguiente a la `<head>` etiqueta:</span><span class="sxs-lookup"><span data-stu-id="0bc1b-104">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
> <span data-ttu-id="0bc1b-105">No copie ni pegue las direcciones URL de esta página, ya que es posible que `<script src="...">` no representen la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-105">Do not copy and paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="0bc1b-106">Para obtener la versión más reciente del SDK, vaya siempre [a Microsoft Teams API de JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).</span><span class="sxs-lookup"><span data-stu-id="0bc1b-106">To get the latest version of the SDK, always go to [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="0bc1b-107">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="0bc1b-107">Tab.cshtml</span></span>

<span data-ttu-id="0bc1b-108">**Para actualizar el script incrustado**</span><span class="sxs-lookup"><span data-stu-id="0bc1b-108">**To update the embedded script**</span></span>

1. <span data-ttu-id="0bc1b-109">En Visual Studio, abra **Tab.cshtml** para actualizar el `<script>` .</span><span class="sxs-lookup"><span data-stu-id="0bc1b-109">In Visual Studio, open **Tab.cshtml** to update the embedded `<script>`.</span></span>

1. <span data-ttu-id="0bc1b-110">En la parte superior del script, llame `microsoftTeams.initialize()` a .</span><span class="sxs-lookup"><span data-stu-id="0bc1b-110">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

1. <span data-ttu-id="0bc1b-111">Actualice los `websiteUrl` valores y de cada función con la dirección URL de https `contentUrl` ngrok a la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-111">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

    <span data-ttu-id="0bc1b-112">El código ahora debería tener el siguiente aspecto con **y8rCgT2b** reemplazado por la dirección URL de ngrok:</span><span class="sxs-lookup"><span data-stu-id="0bc1b-112">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

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

1. <span data-ttu-id="0bc1b-113">Asegúrese de guardar el **tab.cshtml actualizado.**</span><span class="sxs-lookup"><span data-stu-id="0bc1b-113">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="0bc1b-114">Compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="0bc1b-114">Build and run your application</span></span>

<span data-ttu-id="0bc1b-115">En Visual Studio, presione **F5** o **elija Iniciar depuración** en el **menú** Depurar.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-115">In Visual Studio, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="0bc1b-116">Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-116">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="0bc1b-117">Debe tener la aplicación en ejecución Visual Studio y ngrok.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-117">You need to have both your application in Visual Studio and ngrok running.</span></span> <span data-ttu-id="0bc1b-118">Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en **ella, mantenga ngrok en ejecución**.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-118">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="0bc1b-119">Seguirá escuchando y reanudará el enrutamiento de la solicitud de la aplicación cuando se reinicie en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-119">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="0bc1b-120">Si tiene que reiniciar el servicio ngrok, devolverá una nueva dirección URL y tendrá que actualizar la aplicación con la nueva dirección URL.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-120">If you have to restart the ngrok service, it will return a new URL and you will have to update your application with the new URL.</span></span>

## <a name="upload-your-tab"></a><span data-ttu-id="0bc1b-121">Upload la pestaña</span><span class="sxs-lookup"><span data-stu-id="0bc1b-121">Upload your tab</span></span>

>[!Note]
> <span data-ttu-id="0bc1b-122">App Studio se puede usar para editar el **archivomanifest.jsarchivo** y cargar el paquete completado en Teams.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-122">App Studio can be used to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="0bc1b-123">También puede editar manualmente el **archivomanifest.jsen** si lo prefiere.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-123">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="0bc1b-124">Si lo hace, asegúrese de compilar la solución de nuevo para crear el **archivotab.zip** que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-124">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

<span data-ttu-id="0bc1b-125">**Para cargar la pestaña**</span><span class="sxs-lookup"><span data-stu-id="0bc1b-125">**To upload your tab**</span></span>

1. <span data-ttu-id="0bc1b-126">Vaya a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-126">Go to Microsoft Teams.</span></span> <span data-ttu-id="0bc1b-127">Si usa la versión [basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end con las herramientas de desarrollo [del explorador.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="0bc1b-127">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="0bc1b-128">Ve a **App Studio** y selecciona la pestaña Editor **de manifiestos.**</span><span class="sxs-lookup"><span data-stu-id="0bc1b-128">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="0bc1b-129">Selecciona **Importar una aplicación existente en** el editor de manifiestos para empezar a actualizar el paquete de la aplicación para la pestaña. El código fuente viene con su propio manifiesto parcialmente completo.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-129">Select **Import an existing app** in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="0bc1b-130">El nombre del paquete de la **aplicación estab.zip**.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-130">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="0bc1b-131">Está disponible aquí:</span><span class="sxs-lookup"><span data-stu-id="0bc1b-131">It is available here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="0bc1b-132">Upload **tab.zip** a App Studio.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-132">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="0bc1b-133">Actualizar el paquete de la aplicación con el editor de manifiestos</span><span class="sxs-lookup"><span data-stu-id="0bc1b-133">Update your app package with Manifest editor</span></span>

<span data-ttu-id="0bc1b-134">Después de cargar el paquete de la aplicación en App Studio, debes terminar de configurarlo.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-134">After you have uploaded your app package into App Studio, you must finish configuring it.</span></span>

<span data-ttu-id="0bc1b-135">Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-135">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="0bc1b-136">Hay una lista de pasos en el lado izquierdo del editor de manifiesto y, a la derecha, una lista de propiedades que deben tener valores para cada uno de esos pasos.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-136">There is a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="0bc1b-137">El usuario ha proporcionado gran parte de la **informaciónmanifest.js,** pero hay algunos campos que debe actualizar:</span><span class="sxs-lookup"><span data-stu-id="0bc1b-137">Much of the information has been provided by your **manifest.json** but there are a few fields that you must update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="0bc1b-138">Detalles: Detalles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="0bc1b-138">Details: App details</span></span>

<span data-ttu-id="0bc1b-139">En la **sección Detalles de la** aplicación:</span><span class="sxs-lookup"><span data-stu-id="0bc1b-139">In the **App details** section:</span></span>

1. <span data-ttu-id="0bc1b-140">En **Identificación**, seleccione **Generar** para reemplazar el identificador de marcador de posición con el GUID necesario para la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-140">Under **Identification**, select **Generate** to replace the placeholder ID with the required GUID for your tab.</span></span>

1. <span data-ttu-id="0bc1b-141">En **Información para desarrolladores,** actualice **el** sitio web con la dirección URL HTTPS de **ngrok.**</span><span class="sxs-lookup"><span data-stu-id="0bc1b-141">Under **Developer information**, update **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="0bc1b-142">En **Direcciones URL de la** aplicación, actualice la declaración **privacidad** y `https://<yourngrokurl>/privacy` los **Términos** de uso `https://<yourngrokurl>/tou` para>.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-142">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="0bc1b-143">Capacidades: pestañas</span><span class="sxs-lookup"><span data-stu-id="0bc1b-143">Capabilities: Tabs</span></span>

<span data-ttu-id="0bc1b-144">En la **sección Pestañas:**</span><span class="sxs-lookup"><span data-stu-id="0bc1b-144">In the **Tabs** section:</span></span>

1. <span data-ttu-id="0bc1b-145">En **la pestaña Equipo,** **seleccione Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-145">Under **Team tab**, select **Add**.</span></span>

1. <span data-ttu-id="0bc1b-146">En la **ventana emergente de la pestaña** Equipo, actualice la dirección URL de **configuración** a `https://<yourngrokurl>/tab` .</span><span class="sxs-lookup"><span data-stu-id="0bc1b-146">In the **Team tab** pop-up window, update the **Configuration URL** to `https://<yourngrokurl>/tab`.</span></span>

1. <span data-ttu-id="0bc1b-147">Asegúrese de **que las casillas ¿Puede** actualizar la configuración? , **Equipo** y **Chat** de grupo están seleccionadas y **seleccione Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-147">Ensure the **Can update configuration?**, **Team**, and **Group chat** checkboxes are selected and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="0bc1b-148">Finalizar: dominios y permisos</span><span class="sxs-lookup"><span data-stu-id="0bc1b-148">Finish: Domains and permissions</span></span>

<span data-ttu-id="0bc1b-149">En la **sección Dominios y permisos,** los dominios de las **pestañas** deben contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="0bc1b-149">In the **Domains and permissions** section, **Domains from your tabs** must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="0bc1b-150">Finalizar: probar y distribuir</span><span class="sxs-lookup"><span data-stu-id="0bc1b-150">Finish: Test and distribute</span></span>

>[!IMPORTANT]
> <span data-ttu-id="0bc1b-151">A la derecha, en **Descripción,** verá la siguiente advertencia:</span><span class="sxs-lookup"><span data-stu-id="0bc1b-151">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="0bc1b-152">&#9888; "**La matriz 'validDomains' no puede contener un sitio de túnel...**"</span><span class="sxs-lookup"><span data-stu-id="0bc1b-152">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
> <span data-ttu-id="0bc1b-153">Esta advertencia puede omitirse mientras se prueba la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-153">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="0bc1b-154">En la **sección Probar y distribuir,** seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-154">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="0bc1b-155">En el cuadro de diálogo emergente, seleccione **Agregar a un** equipo o en la lista desplegable, seleccione Agregar a un **chat.**</span><span class="sxs-lookup"><span data-stu-id="0bc1b-155">In the pop-up dialog box, select **Add to a team** or from the drop-down, select **Add to a chat**.</span></span>

1. <span data-ttu-id="0bc1b-156">Elija el equipo o el chat donde desea que se muestre la pestaña y seleccione **Configurar una pestaña**.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-156">Choose the team or chat where you want the tab to be displayed and select **Set up a tab**.</span></span>

1. <span data-ttu-id="0bc1b-157">En el siguiente cuadro de diálogo emergente, elija **Seleccionar gris** o **Seleccionar** rojo y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-157">In the next pop-up dialog box, choose either **Select Gray** or **Select Red**, and select **Save**.</span></span>

1. <span data-ttu-id="0bc1b-158">Para ver la pestaña, vaya al equipo donde instaló la pestaña y selecciónelo en la barra de pestañas.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-158">To view your tab, go to the team where you installed the tab, and select it from the tab bar.</span></span> <span data-ttu-id="0bc1b-159">Se muestra la página que eligió durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="0bc1b-159">The page that you chose during configuration is displayed.</span></span>

    ![Pestaña canal ASPNETMVC cargada](../../assets/images/tab-images/channeltabaspnetmvcuploaded.png)

