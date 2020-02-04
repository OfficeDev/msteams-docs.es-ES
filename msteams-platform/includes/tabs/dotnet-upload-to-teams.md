## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="a1b9c-101">Cargar la pestaña en Teams con App Studio</span><span class="sxs-lookup"><span data-stu-id="a1b9c-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="a1b9c-102">Usamos App Studio para editar el archivo **manifest. JSON** y cargar el paquete completado en Teams.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="a1b9c-103">También puede editar manualmente el archivo **manifest. JSON** si lo prefiere.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-103">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="a1b9c-104">Si lo hace, asegúrese de volver a crear la solución para crear el archivo **. zip de pestañas** que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-104">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="a1b9c-105">Abra el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="a1b9c-106">Si usa la [versión basada en Web](https://teams.microsoft.com) , puede inspeccionar el código Front-end con las [herramientas de desarrollo](~/tabs/how-to/developer-tools.md)de su explorador.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="a1b9c-107">Abra la aplicación de App Studio y seleccione la pestaña **Editor de manifiestos** .</span><span class="sxs-lookup"><span data-stu-id="a1b9c-107">Open the App Studio app and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="a1b9c-108">Seleccione el icono **importar una aplicación existente** en el editor de manifiestos para empezar a actualizar el paquete de la aplicación de la pestaña. El código fuente incluye su propio manifiesto parcialmente completado.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="a1b9c-109">El nombre del paquete de la aplicación es **Tab. zip**.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="a1b9c-110">Se debe encontrar aquí:</span><span class="sxs-lookup"><span data-stu-id="a1b9c-110">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- <span data-ttu-id="a1b9c-111">Cargue la **ficha. zip** en App Studio.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-111">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="a1b9c-112">Actualizar el paquete de la aplicación con el editor de manifiestos</span><span class="sxs-lookup"><span data-stu-id="a1b9c-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="a1b9c-113">Una vez que haya cargado el paquete de la aplicación en App Studio, tendrá que finalizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="a1b9c-114">Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiestos.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="a1b9c-115">Hay una lista de pasos en la parte izquierda del editor de manifiestos y, a la derecha, una lista de propiedades que deben tener valores para cada uno de estos pasos.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="a1b9c-116">La gran parte de la información se ha proporcionado en *manifest. JSON* , pero hay algunos campos que debe actualizar:</span><span class="sxs-lookup"><span data-stu-id="a1b9c-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="a1b9c-117">Detalles: detalles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a1b9c-117">Details: App details</span></span>

- <span data-ttu-id="a1b9c-118">En *identificación* , seleccione **generar** para generar un nuevo identificador de aplicación para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-118">Under *Identification* select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="a1b9c-119">En *información para desarrolladores* , actualice el campo **dirección URL del sitio web** con la dirección URL https de *ngrok* .</span><span class="sxs-lookup"><span data-stu-id="a1b9c-119">Under *Developer information* update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="a1b9c-120">En *direcciones URL* de aplicaciones \*\*\*\* `https://<yourngrokurl>/privacy` , actualice la declaración de privacidad y las `https://<yourngrokurl>/tou` **condiciones de uso** para>.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-120">Under *App URLs* update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="a1b9c-121">Capacidades: pestañas</span><span class="sxs-lookup"><span data-stu-id="a1b9c-121">Capabilities: Tabs</span></span>

<span data-ttu-id="a1b9c-122">En la sección de *tabulaciones* :</span><span class="sxs-lookup"><span data-stu-id="a1b9c-122">In the *Tabs* section:</span></span>

- <span data-ttu-id="a1b9c-123">En la *pestaña equipo* , seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-123">Under *Team Tab* select **Add**.</span></span>

- <span data-ttu-id="a1b9c-124">En la ventana emergente de la pestaña equipo, actualice la *dirección URL de configuración* a `https://<yourngrokurl>/tab`.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-124">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="a1b9c-125">Por último, asegúrese de que la configuración de se \*puede actualizar. \*Los cuadros equipo y *grupo de chat* están seleccionados y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-125">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="a1b9c-126">Finalizar: dominios y permisos</span><span class="sxs-lookup"><span data-stu-id="a1b9c-126">Finish: Domains and permissions</span></span>

<span data-ttu-id="a1b9c-127">En la sección *dominios y permisos* , los *dominios del campo de pestañas* deben contener la dirección URL de ngrok sin el `<yourngrokurl>.ngrok.io/`prefijo https.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-127">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="a1b9c-128">Finalizar: probar y distribuir</span><span class="sxs-lookup"><span data-stu-id="a1b9c-128">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="a1b9c-129">En el campo **Descripción** de la derecha, verá la siguiente ADVERTENCIA:</span><span class="sxs-lookup"><span data-stu-id="a1b9c-129">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="a1b9c-130">&#9888; "**la matriz ' validDomains ' no puede contener un sitio de túnel...**"</span><span class="sxs-lookup"><span data-stu-id="a1b9c-130">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="a1b9c-131">Esta advertencia puede omitirse mientras se prueba la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-131">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="a1b9c-132">En la sección *probar y distribuir* :</span><span class="sxs-lookup"><span data-stu-id="a1b9c-132">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="a1b9c-133">Haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-133">Select **Install**.</span></span>

- <span data-ttu-id="a1b9c-134">En el campo *Agregar a un equipo o chat* de la ventana emergente, especifique el equipo y seleccione **instalar**.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-134">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="a1b9c-135">En la siguiente ventana emergente, elija el canal de equipo en el que desea que se muestre la pestaña y seleccione **configurar**.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-135">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="a1b9c-136">En la última ventana emergente, seleccione un valor para la página de ficha (bien un icono rojo o gris) y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-136">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="a1b9c-137">Para ver la pestaña, navegue hasta el equipo en el que se instaló y selecciónela en la barra de pestañas.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-137">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="a1b9c-138">Debe mostrarse la página elegida durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="a1b9c-138">The page that you chose during configuration should be displayed.</span></span>
