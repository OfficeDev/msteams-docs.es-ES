## <a name="upload-your-tab-with-app-studio"></a><span data-ttu-id="76b83-101">Upload pestaña con App Studio</span><span class="sxs-lookup"><span data-stu-id="76b83-101">Upload your tab with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="76b83-102">Usamos **App Studio** para editar el archivomanifest.js **y** cargar el paquete completado en Teams.</span><span class="sxs-lookup"><span data-stu-id="76b83-102">We use **App Studio** to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="76b83-103">También puede editar manualmentemanifest.js **en**.</span><span class="sxs-lookup"><span data-stu-id="76b83-103">You can also manually edit **manifest.json**.</span></span> <span data-ttu-id="76b83-104">Si lo hace, asegúrese de volver a crear la solución para crear el **archivoTab.zip** cargar.</span><span class="sxs-lookup"><span data-stu-id="76b83-104">If you do, ensure that you build the solution again to create the **Tab.zip** file to upload.</span></span>

<span data-ttu-id="76b83-105">**Para cargar la pestaña con App Studio**</span><span class="sxs-lookup"><span data-stu-id="76b83-105">**To upload your tab with App Studio**</span></span>

1. <span data-ttu-id="76b83-106">Vaya a Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="76b83-106">Go to Microsoft Teams.</span></span> <span data-ttu-id="76b83-107">Si usa la versión [basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end con las herramientas de desarrollo [del explorador.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="76b83-107">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="76b83-108">Ve a **App Studio** y selecciona la pestaña Editor **de manifiestos.**</span><span class="sxs-lookup"><span data-stu-id="76b83-108">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="76b83-109">Selecciona **Importar una aplicación existente en** el editor de **manifiestos** para empezar a actualizar el paquete de la aplicación para la pestaña. El código fuente viene con su propio manifiesto parcialmente completo.</span><span class="sxs-lookup"><span data-stu-id="76b83-109">Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="76b83-110">El nombre del paquete de la **aplicación estab.zip**.</span><span class="sxs-lookup"><span data-stu-id="76b83-110">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="76b83-111">Está disponible en la siguiente ruta de acceso:</span><span class="sxs-lookup"><span data-stu-id="76b83-111">It is available from the following path:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="76b83-112">Upload **tab.zip** a App **Studio**.</span><span class="sxs-lookup"><span data-stu-id="76b83-112">Upload **tab.zip** to **App Studio**.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="76b83-113">Actualizar el paquete de la aplicación con el editor de manifiestos</span><span class="sxs-lookup"><span data-stu-id="76b83-113">Update your app package with Manifest editor</span></span>

<span data-ttu-id="76b83-114">Después de cargar el paquete de la aplicación en App Studio, debes configurarlo.</span><span class="sxs-lookup"><span data-stu-id="76b83-114">After you have uploaded your app package into App Studio, you must configure it.</span></span>

<span data-ttu-id="76b83-115">Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="76b83-115">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="76b83-116">Hay una lista de pasos en el lado izquierdo del editor de manifiesto y, a la derecha, una lista de propiedades que deben tener valores para cada uno de esos pasos.</span><span class="sxs-lookup"><span data-stu-id="76b83-116">There is a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="76b83-117">El usuario ha proporcionado gran parte de la **informaciónmanifest.js,** pero hay campos que debe actualizar.</span><span class="sxs-lookup"><span data-stu-id="76b83-117">Much of the information has been provided by your **manifest.json** but there are fields that you must update.</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="76b83-118">Detalles: Detalles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="76b83-118">Details: App details</span></span>

<span data-ttu-id="76b83-119">En la **sección Detalles de la** aplicación:</span><span class="sxs-lookup"><span data-stu-id="76b83-119">In the **App details** section:</span></span>

1. <span data-ttu-id="76b83-120">En **Identificación,** selecciona **Generar** para generar un nuevo identificador de aplicación para tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="76b83-120">Under **Identification**, select **Generate** to generate a new App Id for your app.</span></span>

1. <span data-ttu-id="76b83-121">En **Información del desarrollador,** actualice el **sitio web** con la dirección URL HTTPS de **ngrok.**</span><span class="sxs-lookup"><span data-stu-id="76b83-121">Under **Developer information**, update the **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="76b83-122">En **Direcciones URL de la** aplicación, actualice la declaración **privacidad** y `https://<yourngrokurl>/privacy` los **Términos** de uso `https://<yourngrokurl>/tou` para>.</span><span class="sxs-lookup"><span data-stu-id="76b83-122">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="76b83-123">Capacidades: pestañas</span><span class="sxs-lookup"><span data-stu-id="76b83-123">Capabilities: Tabs</span></span>

<span data-ttu-id="76b83-124">En la **sección Pestañas:**</span><span class="sxs-lookup"><span data-stu-id="76b83-124">In the **Tabs** section:</span></span>

1. <span data-ttu-id="76b83-125">En **Agregar una pestaña personal,** seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="76b83-125">Under **Add a personal tab**, select **Add**.</span></span> <span data-ttu-id="76b83-126">Aparece un cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="76b83-126">A pop-up dialog box appears.</span></span>

1. <span data-ttu-id="76b83-127">Escriba un nombre para la ficha personal en **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="76b83-127">Enter a name for the personal tab in **Name**.</span></span>

1. <span data-ttu-id="76b83-128">Escriba el **id. de entidad**.</span><span class="sxs-lookup"><span data-stu-id="76b83-128">Enter the **Entity ID**.</span></span>

1. <span data-ttu-id="76b83-129">Actualizar **dirección URL de contenido** con `https://<yourngrokurl>/personalTab` .</span><span class="sxs-lookup"><span data-stu-id="76b83-129">Update **Content URL** with `https://<yourngrokurl>/personalTab`.</span></span>

    <span data-ttu-id="76b83-130">Deje el **campo Dirección URL** del sitio web en blanco.</span><span class="sxs-lookup"><span data-stu-id="76b83-130">Leave the **Website URL** field blank.</span></span>

1. <span data-ttu-id="76b83-131">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="76b83-131">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="76b83-132">Finalizar: dominios y permisos</span><span class="sxs-lookup"><span data-stu-id="76b83-132">Finish: Domains and permissions</span></span>

<span data-ttu-id="76b83-133">En la **sección Dominios y permisos,** el campo Dominios de las **pestañas** debe contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="76b83-133">In the **Domains and permissions** section, the **Domains from your tabs** field must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="76b83-134">Finalizar: probar y distribuir</span><span class="sxs-lookup"><span data-stu-id="76b83-134">Finish: Test and distribute</span></span>

>[!IMPORTANT]
> <span data-ttu-id="76b83-135">A la derecha, en **Descripción,** verá la siguiente advertencia:</span><span class="sxs-lookup"><span data-stu-id="76b83-135">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="76b83-136">&#9888; La **matriz 'validDomains' no puede contener un sitio de túnel...**</span><span class="sxs-lookup"><span data-stu-id="76b83-136">&#9888; **The 'validDomains' array cannot contain a tunneling site...**</span></span>
>
><span data-ttu-id="76b83-137">Esta advertencia puede omitirse mientras se prueba la pestaña.</span><span class="sxs-lookup"><span data-stu-id="76b83-137">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="76b83-138">En la **sección Probar y distribuir,** seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="76b83-138">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="76b83-139">En el cuadro de diálogo emergente, seleccione **Agregar** y la pestaña se muestra con dos opciones.</span><span class="sxs-lookup"><span data-stu-id="76b83-139">In the pop-up dialog box, select **Add** and your tab is displayed with two options.</span></span>

1. <span data-ttu-id="76b83-140">En las opciones de la pestaña, elija **Seleccionar gris** o **Seleccionar rojo**.</span><span class="sxs-lookup"><span data-stu-id="76b83-140">From the options in the tab, choose either **Select Gray** or **Select Red**.</span></span> <span data-ttu-id="76b83-141">La pestaña se muestra según el color seleccionado.</span><span class="sxs-lookup"><span data-stu-id="76b83-141">The tab is displayed according to the color you selected.</span></span>
 
    ![Pestaña personal ASPNETMVC cargada](../../assets/images/tab-images/personaltabaspnetmvcuploaded.png)

## <a name="view-your-personal-tab"></a><span data-ttu-id="76b83-143">Ver la pestaña personal</span><span class="sxs-lookup"><span data-stu-id="76b83-143">View your personal tab</span></span>

1. <span data-ttu-id="76b83-144">En la barra de navegación situada en el extremo izquierdo de la Teams, selecciona los puntos suspensivos &#x25CF;&#x25CF;&#x25CF;.</span><span class="sxs-lookup"><span data-stu-id="76b83-144">In the navigation bar located at the far left of the Teams app, select the ellipses &#x25CF;&#x25CF;&#x25CF;.</span></span> <span data-ttu-id="76b83-145">Se muestra una lista de aplicaciones personales.</span><span class="sxs-lookup"><span data-stu-id="76b83-145">A list of personal apps is shown.</span></span>

1. <span data-ttu-id="76b83-146">Seleccione la pestaña de la lista para verlo.</span><span class="sxs-lookup"><span data-stu-id="76b83-146">Select your tab from the list to view it.</span></span>
