## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="41bdc-101">Cargar la pestaña en Teams con App Studio</span><span class="sxs-lookup"><span data-stu-id="41bdc-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="41bdc-102">Usamos App Studio para editar el archivo **manifest. JSON** y cargar el paquete completado en Teams.</span><span class="sxs-lookup"><span data-stu-id="41bdc-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="41bdc-103">También puede editar **manifest. JSON** manualmente si lo prefiere.</span><span class="sxs-lookup"><span data-stu-id="41bdc-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="41bdc-104">Si lo hace, asegúrese de volver a crear la solución para crear el archivo **. zip de pestañas** que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="41bdc-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="41bdc-105">Abra el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="41bdc-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="41bdc-106">Si usa la [versión basada en Web](https://teams.microsoft.com) , puede inspeccionar el código Front-end con las [herramientas de desarrollo](~/tabs/how-to/developer-tools.md)de su explorador.</span><span class="sxs-lookup"><span data-stu-id="41bdc-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="41bdc-107">Abra App Studio y seleccione la pestaña **Editor de manifiestos** .</span><span class="sxs-lookup"><span data-stu-id="41bdc-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="41bdc-108">Seleccione el icono **importar una aplicación existente** en el editor de manifiestos para empezar a actualizar el paquete de la aplicación de la pestaña. El código fuente incluye su propio manifiesto parcialmente completado.</span><span class="sxs-lookup"><span data-stu-id="41bdc-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="41bdc-109">El nombre del paquete de la aplicación es **Tab. zip**.</span><span class="sxs-lookup"><span data-stu-id="41bdc-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="41bdc-110">Se debe encontrar aquí:</span><span class="sxs-lookup"><span data-stu-id="41bdc-110">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/Tab.zip
```

- <span data-ttu-id="41bdc-111">Cargue la **ficha. zip** en App Studio.</span><span class="sxs-lookup"><span data-stu-id="41bdc-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="41bdc-112">Actualizar el paquete de la aplicación con el editor de manifiestos</span><span class="sxs-lookup"><span data-stu-id="41bdc-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="41bdc-113">Una vez que haya cargado el paquete de la aplicación en App Studio, tendrá que finalizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="41bdc-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="41bdc-114">Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiestos.</span><span class="sxs-lookup"><span data-stu-id="41bdc-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="41bdc-115">Hay una lista de pasos en la parte izquierda del editor de manifiestos y, a la derecha, una lista de propiedades que deben tener valores para cada uno de estos pasos.</span><span class="sxs-lookup"><span data-stu-id="41bdc-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="41bdc-116">La gran parte de la información se ha proporcionado en *manifest. JSON* , pero hay algunos campos que debe actualizar:</span><span class="sxs-lookup"><span data-stu-id="41bdc-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="41bdc-117">Detalles: detalles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="41bdc-117">Details: App details</span></span>

<span data-ttu-id="41bdc-118">En la sección detalles de la *aplicación* :</span><span class="sxs-lookup"><span data-stu-id="41bdc-118">In the *App details* section:</span></span>

- <span data-ttu-id="41bdc-119">En *identificación* , seleccione **generar** para generar un nuevo identificador de aplicación para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="41bdc-119">Under *Identification* select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="41bdc-120">En *información para desarrolladores* , actualice la **dirección URL del sitio web** con la dirección URL https de *ngrok* .</span><span class="sxs-lookup"><span data-stu-id="41bdc-120">Under *Developer information* update the **Website URL** with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="41bdc-121">En *direcciones URL* de aplicaciones \*\*\*\* `https://<yourngrokurl>/privacy` , actualice la declaración de privacidad y las `https://<yourngrokurl>/tou` **condiciones de uso** para>.</span><span class="sxs-lookup"><span data-stu-id="41bdc-121">Under *App URLs* update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="41bdc-122">Capacidades: pestañas</span><span class="sxs-lookup"><span data-stu-id="41bdc-122">Capabilities: Tabs</span></span>

<span data-ttu-id="41bdc-123">En la sección de *tabulaciones* :</span><span class="sxs-lookup"><span data-stu-id="41bdc-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="41bdc-124">En *Agregar una pestaña personal* , seleccione ***Agregar***.</span><span class="sxs-lookup"><span data-stu-id="41bdc-124">Under *Add a personal tab* select ***Add***.</span></span> <span data-ttu-id="41bdc-125">Aparecerá una ventana emergente de cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="41bdc-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="41bdc-126">Complete el campo *nombre* .</span><span class="sxs-lookup"><span data-stu-id="41bdc-126">Complete the *Name* field.</span></span>

- <span data-ttu-id="41bdc-127">Complete el campo *identificador de entidad* .</span><span class="sxs-lookup"><span data-stu-id="41bdc-127">Complete the *Entity Id* field.</span></span>

- <span data-ttu-id="41bdc-128">Actualice el campo *dirección URL* de contenido `https://<yourngrokurl>/personalTab`con el.</span><span class="sxs-lookup"><span data-stu-id="41bdc-128">Update the *Content URL* field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="41bdc-129">Deje en blanco el campo *dirección URL del sitio web* .</span><span class="sxs-lookup"><span data-stu-id="41bdc-129">Leave the *Website URL* field blank.</span></span>

- <span data-ttu-id="41bdc-130">Haga clic en ***Guardar***.</span><span class="sxs-lookup"><span data-stu-id="41bdc-130">Select ***Save***.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="41bdc-131">Finalizar: dominios y permisos</span><span class="sxs-lookup"><span data-stu-id="41bdc-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="41bdc-132">En la sección *dominios y permisos* , los *dominios del campo de pestañas* deben contener la dirección URL de ngrok sin el `<yourngrokurl>.ngrok.io/`prefijo https.</span><span class="sxs-lookup"><span data-stu-id="41bdc-132">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="41bdc-133">Finalizar: probar y distribuir</span><span class="sxs-lookup"><span data-stu-id="41bdc-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="41bdc-134">En el campo **Descripción** de la derecha, verá la siguiente ADVERTENCIA:</span><span class="sxs-lookup"><span data-stu-id="41bdc-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="41bdc-135">&#9888; "**la matriz ' validDomains ' no puede contener un sitio de túnel...**"</span><span class="sxs-lookup"><span data-stu-id="41bdc-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="41bdc-136">Esta advertencia puede omitirse mientras se prueba la pestaña.</span><span class="sxs-lookup"><span data-stu-id="41bdc-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="41bdc-137">En la sección *probar y distribuir* :</span><span class="sxs-lookup"><span data-stu-id="41bdc-137">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="41bdc-138">Haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="41bdc-138">Select **Install**.</span></span>

- <span data-ttu-id="41bdc-139">En la ventana emergente, asegúrese de que *Agregar para usted* está establecido en *sí* y *Agregar a un equipo o chat* está establecido en *no*.</span><span class="sxs-lookup"><span data-stu-id="41bdc-139">In the pop-up window make sure that *Add for you* is set to *Yes* and *Add to a team or chat* is set to *No*.</span></span>

- <span data-ttu-id="41bdc-140">Haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="41bdc-140">Select **Install**.</span></span>

- <span data-ttu-id="41bdc-141">En la siguiente ventana emergente, seleccione **abrir** y se mostrará la pestaña.</span><span class="sxs-lookup"><span data-stu-id="41bdc-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="41bdc-142">Ver su pestaña personal</span><span class="sxs-lookup"><span data-stu-id="41bdc-142">View your personal tab</span></span>

- <span data-ttu-id="41bdc-143">En la barra de navegación ubicada en la parte más a la izquierda de la aplicación Teams, seleccione el `...` menú.</span><span class="sxs-lookup"><span data-stu-id="41bdc-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="41bdc-144">Se le mostrará una lista de aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="41bdc-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="41bdc-145">Seleccione la pestaña de la lista para ver.</span><span class="sxs-lookup"><span data-stu-id="41bdc-145">Select your tab from the list to view.</span></span>
