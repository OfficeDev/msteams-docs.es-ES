## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="4cc86-101">Upload la pestaña para Teams con App Studio</span><span class="sxs-lookup"><span data-stu-id="4cc86-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="4cc86-102">Usamos App Studio para editar su **manifest.jsen el** archivo y cargar el paquete completado en Teams.</span><span class="sxs-lookup"><span data-stu-id="4cc86-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="4cc86-103">También puede editar manualmente **manifest.jsen** si lo prefiere.</span><span class="sxs-lookup"><span data-stu-id="4cc86-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="4cc86-104">Si lo hace, asegúrese de volver a compilar la solución para crear el archivo **Tab.zip** que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="4cc86-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="4cc86-105">Abra el cliente Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="4cc86-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="4cc86-106">Si utiliza la [versión basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end utilizando las herramientas para [desarrolladores](~/tabs/how-to/developer-tools.md)de su navegador.</span><span class="sxs-lookup"><span data-stu-id="4cc86-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="4cc86-107">Abra App Studio y seleccione la pestaña **Editor de manifiestos.**</span><span class="sxs-lookup"><span data-stu-id="4cc86-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="4cc86-108">Seleccione el icono **Importar una aplicación existente** en el editor de manifiestos para comenzar a actualizar el paquete de aplicación de la pestaña. El código fuente viene con su propio manifiesto parcialmente completo.</span><span class="sxs-lookup"><span data-stu-id="4cc86-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="4cc86-109">El nombre del paquete de la aplicación es **tab.zip**.</span><span class="sxs-lookup"><span data-stu-id="4cc86-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="4cc86-110">Debe encontrarse aquí:</span><span class="sxs-lookup"><span data-stu-id="4cc86-110">It should be found here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/Tab.zip
    ```

- <span data-ttu-id="4cc86-111">Upload **Tab.zip** a App Studio.</span><span class="sxs-lookup"><span data-stu-id="4cc86-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="4cc86-112">Actualiza tu paquete de aplicaciones con el editor de manifiestos</span><span class="sxs-lookup"><span data-stu-id="4cc86-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="4cc86-113">Una vez que haya cargado el paquete de la aplicación en App Studio, deberá terminar de configurarlo.</span><span class="sxs-lookup"><span data-stu-id="4cc86-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="4cc86-114">Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiestos.</span><span class="sxs-lookup"><span data-stu-id="4cc86-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="4cc86-115">Hay una lista de pasos en el lado izquierdo del editor de manifiestos y, a la derecha, una lista de propiedades que necesitan tener valores para cada uno de esos pasos.</span><span class="sxs-lookup"><span data-stu-id="4cc86-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="4cc86-116">Gran parte de la información ha sido proporcionada por su *manifest.js,* pero hay algunos campos que tendrá que actualizar:</span><span class="sxs-lookup"><span data-stu-id="4cc86-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="4cc86-117">Detalles: Detalles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4cc86-117">Details: App details</span></span>

<span data-ttu-id="4cc86-118">En la sección Detalles de la **aplicación:**</span><span class="sxs-lookup"><span data-stu-id="4cc86-118">In the **App details** section:</span></span>

- <span data-ttu-id="4cc86-119">En **Identificación,** seleccione **Generar** para generar un nuevo identificador de aplicación para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4cc86-119">Under **Identification** select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="4cc86-120">En **Información del desarrollador,** actualice la **URL del sitio web** con su URL HTTPS **de ngrok.**</span><span class="sxs-lookup"><span data-stu-id="4cc86-120">Under **Developer information** update the **Website URL** with your **ngrok** HTTPS URL.</span></span>

- <span data-ttu-id="4cc86-121">En **URL de aplicación,** actualice la **declaración de privacidad** y los Términos `https://<yourngrokurl>/privacy` de **uso** a `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="4cc86-121">Under **App URLs** update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="4cc86-122">Capacidades: Pestañas</span><span class="sxs-lookup"><span data-stu-id="4cc86-122">Capabilities: Tabs</span></span>

<span data-ttu-id="4cc86-123">En la sección *Pestañas:*</span><span class="sxs-lookup"><span data-stu-id="4cc86-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="4cc86-124">En **Agregar una pestaña personal,** seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4cc86-124">Under **Add a personal tab** select **Add**.</span></span> <span data-ttu-id="4cc86-125">Se le presentará una ventana de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="4cc86-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="4cc86-126">Complete el campo **Nombre.**</span><span class="sxs-lookup"><span data-stu-id="4cc86-126">Complete the **Name** field.</span></span>

- <span data-ttu-id="4cc86-127">Complete el campo **Entity Id.**</span><span class="sxs-lookup"><span data-stu-id="4cc86-127">Complete the **Entity Id** field.</span></span>

- <span data-ttu-id="4cc86-128">Actualice el campo **Dirección URL de contenido** con to `https://<yourngrokurl>/personalTab` .</span><span class="sxs-lookup"><span data-stu-id="4cc86-128">Update the **Content URL** field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="4cc86-129">Deje el campo URL del **sitio web** en blanco.</span><span class="sxs-lookup"><span data-stu-id="4cc86-129">Leave the **Website URL** field blank.</span></span>

- <span data-ttu-id="4cc86-130">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4cc86-130">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="4cc86-131">Finalizar: Dominios y permisos</span><span class="sxs-lookup"><span data-stu-id="4cc86-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="4cc86-132">En la sección **Dominios y permisos,** el campo **Dominios de las pestañas** debe contener la dirección URL de ngrok sin el prefijo HTTPS - `<yourngrokurl>.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="4cc86-132">In the **Domains and permissions** section, the **Domains from your tabs** field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="4cc86-133">Finalizar: Probar y distribuir</span><span class="sxs-lookup"><span data-stu-id="4cc86-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="4cc86-134">En el campo **Descripción** de la derecha verá la siguiente advertencia:</span><span class="sxs-lookup"><span data-stu-id="4cc86-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="4cc86-135">&#9888; "**La matriz 'validDomains' no puede contener un sitio de tunelización...**"</span><span class="sxs-lookup"><span data-stu-id="4cc86-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="4cc86-136">Esta advertencia se puede omitir al probar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="4cc86-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="4cc86-137">En la sección **Prueba y distribución:**</span><span class="sxs-lookup"><span data-stu-id="4cc86-137">In the **Test and distribute** section:</span></span>

- <span data-ttu-id="4cc86-138">Seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="4cc86-138">Select **Install**.</span></span>

- <span data-ttu-id="4cc86-139">En la ventana emergente asegúrese de que **Agregar para usted** está establecido en **Sí** y **Agregar a un equipo o chat** está establecido en **No**.</span><span class="sxs-lookup"><span data-stu-id="4cc86-139">In the pop-up window make sure that **Add for you** is set to **Yes** and **Add to a team or chat** is set to **No**.</span></span>

- <span data-ttu-id="4cc86-140">Seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="4cc86-140">Select **Install**.</span></span>

- <span data-ttu-id="4cc86-141">En la siguiente ventana emergente, seleccione **Abrir** y se mostrará la pestaña.</span><span class="sxs-lookup"><span data-stu-id="4cc86-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="4cc86-142">Ver su pestaña personal</span><span class="sxs-lookup"><span data-stu-id="4cc86-142">View your personal tab</span></span>

- <span data-ttu-id="4cc86-143">En la barra de navegación situada a la izquierda de la aplicación Teams, seleccione el `...` menú.</span><span class="sxs-lookup"><span data-stu-id="4cc86-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="4cc86-144">Se te presentará una lista de aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="4cc86-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="4cc86-145">Seleccione la pestaña de la lista que desea ver.</span><span class="sxs-lookup"><span data-stu-id="4cc86-145">Select your tab from the list to view.</span></span>
