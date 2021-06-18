### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="7059a-101">Usar App Studio para actualizar el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="7059a-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="7059a-102">App Studio es una Teams que puedes instalar desde la Teams tienda.</span><span class="sxs-lookup"><span data-stu-id="7059a-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="7059a-103">Simplifica la creación y el registro de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="7059a-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="7059a-104">Siga estos pasos para actualizar el paquete de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="7059a-104">Complete the following steps to update the app package:</span></span>

1. <span data-ttu-id="7059a-105">Para instalar App Studio en Teams,  selecciona el icono Aplicaciones en la parte inferior de la barra izquierda y busca **App Studio**:</span><span class="sxs-lookup"><span data-stu-id="7059a-105">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**:</span></span>

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. <span data-ttu-id="7059a-106">Selecciona el **icono de App Studio** y elige **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="7059a-106">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="7059a-107">App Studio está instalado:</span><span class="sxs-lookup"><span data-stu-id="7059a-107">The App Studio is installed:</span></span>

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. <span data-ttu-id="7059a-108">Para crear el paquete de la aplicación para Teams aplicación, selecciona la pestaña Editor de **manifiestos** en **App Studio**:</span><span class="sxs-lookup"><span data-stu-id="7059a-108">To create the app package for your Teams app, select the **Manifest editor** tab in **App Studio**:</span></span>

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    <span data-ttu-id="7059a-109">El ejemplo viene con su propio manifiesto y está diseñado para crear un paquete de aplicación cuando se crea el proyecto.</span><span class="sxs-lookup"><span data-stu-id="7059a-109">The sample comes with its own manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="7059a-110">Puedes crear el paquete de la aplicación en .NET con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7059a-110">You can build the app package on .NET with Visual Studio.</span></span> <span data-ttu-id="7059a-111">En Visual Studio, el manifest.jsel archivo on se encuentra en **en Manifiesto** en `Microsoft.Teams.Samples.HelloWorld.Web` .</span><span class="sxs-lookup"><span data-stu-id="7059a-111">In Visual Studio, the manifest.json file is located in under **Manifest** in `Microsoft.Teams.Samples.HelloWorld.Web`.</span></span> <span data-ttu-id="7059a-112">Este paso se describe en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="7059a-112">This step is described by the following image:</span></span>  
    
    <img  width="450px" alt="Build the app package on .NET with Visual Studio" src="~/assets/images/get-started/app-package-on-.NET-with-Visual-Studio.png"/>
    
    <span data-ttu-id="7059a-113">Puedes crear el paquete de la aplicación en Node.js escribiendo en la línea `gulp` de comandos en el directorio raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7059a-113">You can build the app package on Node.js by typing `gulp` at the command line in the root directory of the project.</span></span>

    ```bash
    $ gulp
    [13:39:27] Using gulpfile ~\documents\github\msteams-samples-hello-world-nodejs\gulpfile.js
    [13:39:27] Starting 'clean'...
    [13:39:27] Starting 'generate-manifest'...
    [13:39:27] Finished 'generate-manifest' after 11 ms
    [13:39:27] Finished 'clean' after 21 ms
    [13:39:27] Starting 'default'...
    Build completed. Output in manifest folder
    [13:39:27] Finished 'default' after 62 μs
    ```

    <span data-ttu-id="7059a-114">El nombre del paquete de aplicación generado es **helloworldapp.zip**.</span><span class="sxs-lookup"><span data-stu-id="7059a-114">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="7059a-115">Puede buscar este archivo si la ubicación no está clara en la herramienta que está usando.</span><span class="sxs-lookup"><span data-stu-id="7059a-115">You can search for this file if the location is not clear in the tool you are using.</span></span>

1. <span data-ttu-id="7059a-116">Ahora, para modificar este paquete de aplicación, selecciona **Importar una aplicación existente** en el editor de **manifiestos:**</span><span class="sxs-lookup"><span data-stu-id="7059a-116">Now to modify this app package, select **Import an existing app** in the **Manifest editor**:</span></span>

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. <span data-ttu-id="7059a-117">Selecciona el **icono Hello World** para la aplicación recién importada:</span><span class="sxs-lookup"><span data-stu-id="7059a-117">Select the **Hello World** tile for your newly imported app:</span></span>

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="7059a-118">La siguiente imagen muestra el paquete de aplicación importado en App Studio:</span><span class="sxs-lookup"><span data-stu-id="7059a-118">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="7059a-119">En el lado izquierdo del editor de manifiesto hay una lista de pasos.</span><span class="sxs-lookup"><span data-stu-id="7059a-119">On the left-hand side of the Manifest editor there is a list of steps.</span></span> <span data-ttu-id="7059a-120">En el lado derecho hay una lista de propiedades que deben rellenarse para cada paso.</span><span class="sxs-lookup"><span data-stu-id="7059a-120">On the right-hand side there is a list of properties that need to be filled in for each step.</span></span> <span data-ttu-id="7059a-121">Al empezar con una aplicación de ejemplo, gran parte de la información ya se ha completado.</span><span class="sxs-lookup"><span data-stu-id="7059a-121">As you started with a sample app, much of the information is already completed.</span></span> <span data-ttu-id="7059a-122">Los siguientes pasos te permiten actualizar las propiedades de la aplicación Hello World.</span><span class="sxs-lookup"><span data-stu-id="7059a-122">The next steps enable you to update the properties of the Hello World app.</span></span>

#### <a name="app-details"></a><span data-ttu-id="7059a-123">Detalles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="7059a-123">App details</span></span>

<span data-ttu-id="7059a-124">Seleccione **Detalles de la aplicación** en **Detalles**.</span><span class="sxs-lookup"><span data-stu-id="7059a-124">Select **App details** under **Details**.</span></span> <span data-ttu-id="7059a-125">Selecciona el **botón** Generar para crear un nuevo identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7059a-125">Select the **Generate** button to create a new App ID.</span></span>

<span data-ttu-id="7059a-126">El nuevo identificador de aplicación es similar a `2322041b-72bf-459d-b107-f4f335bc35bd` .</span><span class="sxs-lookup"><span data-stu-id="7059a-126">Your new App ID is similar to `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="7059a-127">Consulta los detalles de la aplicación en el panel derecho, incluida la información del **desarrollador** y los **detalles de personal** de marca.</span><span class="sxs-lookup"><span data-stu-id="7059a-127">Go through the app details in the right-hand pane including **Developer information** and **Branding** details.</span></span> <span data-ttu-id="7059a-128">Estos detalles son importantes si vas a escribir una nueva aplicación para su distribución.</span><span class="sxs-lookup"><span data-stu-id="7059a-128">These details are important if you are writing a new app for distribution.</span></span>

#### <a name="tabs"></a><span data-ttu-id="7059a-129">Pestañas</span><span class="sxs-lookup"><span data-stu-id="7059a-129">Tabs</span></span>

<span data-ttu-id="7059a-130">Es sencillo agregar pestañas a una Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="7059a-130">It is simple to add tabs to a Teams app.</span></span> <span data-ttu-id="7059a-131">La aplicación de ejemplo ya admite varias pestañas y puedes habilitarlas.</span><span class="sxs-lookup"><span data-stu-id="7059a-131">The sample app already supports several tabs, and you can enable them.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="7059a-132">Ficha Equipo</span><span class="sxs-lookup"><span data-stu-id="7059a-132">Team tab</span></span>

<span data-ttu-id="7059a-133">La aplicación solo puede tener una pestaña Equipo:</span><span class="sxs-lookup"><span data-stu-id="7059a-133">Your app can only have one Team tab:</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="7059a-134">En este ejemplo, la pestaña Equipo es donde se muestra la página de configuración.</span><span class="sxs-lookup"><span data-stu-id="7059a-134">In this sample, the Team tab is where your configuration page is displayed.</span></span> <span data-ttu-id="7059a-135">Seleccione el **símbolo ...** de la dirección URL de **configuración tab** y elija **Editar** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="7059a-135">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="7059a-136">Cambie la dirección URL a `https://yourteamsapp.ngrok.io/configure` donde `yourteamsapp.ngrok.io` debe reemplazarse por la dirección URL que usó al [hospedar la aplicación](#host-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="7059a-136">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` must be replaced with the URL that you used when [hosting your app](#host-the-sample-app).</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="7059a-137">Pestañas personales</span><span class="sxs-lookup"><span data-stu-id="7059a-137">Personal tabs</span></span>

<span data-ttu-id="7059a-138">La aplicación puede tener hasta 16 pestañas, incluida la pestaña Equipo.</span><span class="sxs-lookup"><span data-stu-id="7059a-138">Your app can have up to 16 tabs, including the Team tab.</span></span>

<span data-ttu-id="7059a-139">Las pestañas personales son diferentes de la pestaña Equipo. **Hello Tab** ya aparece en la lista de pestañas personales con un valor de marcador de posición `com.contoso.helloworld.hellotab` .</span><span class="sxs-lookup"><span data-stu-id="7059a-139">Personal tabs are different from the Team tab. **Hello Tab** is already listed in the personal tabs list with a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="7059a-140">Seleccione el **símbolo ...** de la dirección URL de **configuración tab** y elija **Editar** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="7059a-140">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="7059a-141">Aparece el siguiente cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="7059a-141">The following dialog box appears:</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="7059a-142">Actualice los siguientes cuadros con la dirección URL de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="7059a-142">Update the following boxes with your app URL:</span></span>

- <span data-ttu-id="7059a-143">Cambiar el **cuadro Dirección URL de** contenido a `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="7059a-143">Change the **Content URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="7059a-144">Cambiar el **cuadro Dirección URL del** sitio web a `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="7059a-144">Change the **Website URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="7059a-145">Reemplace `yourteamsapp.ngrok.io` por la dirección URL que usó al hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7059a-145">Replace `yourteamsapp.ngrok.io` by the URL that you used when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="7059a-146">Bots</span><span class="sxs-lookup"><span data-stu-id="7059a-146">Bots</span></span>

<span data-ttu-id="7059a-147">Es fácil agregar la funcionalidad de bots a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7059a-147">It is easy to add the bots functionality to your app.</span></span> <span data-ttu-id="7059a-148">La aplicación de ejemplo **Hello World** ya tiene un bot como parte de la muestra, pero debes registrarlo con Microsoft:</span><span class="sxs-lookup"><span data-stu-id="7059a-148">The **Hello World** sample app already has a bot as part of the sample, but you must register it with Microsoft:</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="7059a-149">El bot que se importó desde el ejemplo no tiene un identificador de aplicación asociado.</span><span class="sxs-lookup"><span data-stu-id="7059a-149">The bot that was imported from the sample does not have an associated App ID.</span></span> <span data-ttu-id="7059a-150">Debes crear un bot nuevo para que App Studio pueda crear un nuevo id. de aplicación y registrarlo con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7059a-150">You must create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span>

> [!NOTE]
> <span data-ttu-id="7059a-151">El id. de aplicación creado por App Studio para el bot es diferente del id. de aplicación creado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7059a-151">The App ID created by App Studio for the bot is different from the App ID created for the app.</span></span> <span data-ttu-id="7059a-152">Cada bot de una aplicación requiere su propio identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7059a-152">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="7059a-153">Siga estos pasos para configurar el bot:</span><span class="sxs-lookup"><span data-stu-id="7059a-153">Complete the following steps to setup your bot:</span></span>

1. <span data-ttu-id="7059a-154">Seleccione **Eliminar** junto al bot importado en la lista de bots.</span><span class="sxs-lookup"><span data-stu-id="7059a-154">Select **Delete** next to the imported bot in the bot list.</span></span> <span data-ttu-id="7059a-155">Ahora no quedan bots que mostrar.</span><span class="sxs-lookup"><span data-stu-id="7059a-155">Now there are no bots left to show.</span></span> 
1. <span data-ttu-id="7059a-156">Seleccione **Configurar** para mostrar el cuadro de diálogo Configurar **un bot.**</span><span class="sxs-lookup"><span data-stu-id="7059a-156">Select **Setup** to display the **Set up a bot** dialog box.</span></span>

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. <span data-ttu-id="7059a-157">Agregue un bot name **Contoso bot** y active las tres casillas en **Scope**.</span><span class="sxs-lookup"><span data-stu-id="7059a-157">Add a bot name **Contoso bot** and select all three check boxes under **Scope**.</span></span>
1. <span data-ttu-id="7059a-158">Elija **Guardar** para salir del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7059a-158">Choose **Save** to exit the dialog box.</span></span> <span data-ttu-id="7059a-159">App Studio registra el bot con Microsoft y muestra el nuevo bot en la lista de bots.</span><span class="sxs-lookup"><span data-stu-id="7059a-159">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> 
1. <span data-ttu-id="7059a-160">Ahora abra un archivo de texto en el bloc de notas y copie y pegue el nuevo identificador de bot en él.</span><span class="sxs-lookup"><span data-stu-id="7059a-160">Now open a text file in notepad and copy and paste your new bot ID into it.</span></span>
1. <span data-ttu-id="7059a-161">Haga **clic en Generar nueva contraseña** y anote la contraseña en el mismo archivo de texto que anotó el id. de la aplicación del bot.</span><span class="sxs-lookup"><span data-stu-id="7059a-161">Click **Generate New Password**, and note the password in the same text file you noted your bot App ID.</span></span>
1. <span data-ttu-id="7059a-162">Actualice la **dirección del extremo bot** a y reemplace por la dirección URL que `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` usó al hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7059a-162">Update the **Bot endpoint address** to `https://yourteamsapp.ngrok.io/api/messages`, and replace `yourteamsapp.ngrok.io` with the URL that you used when hosting your app.</span></span>
1. <span data-ttu-id="7059a-163">Ahora guarda el archivo de texto, ya que debes agregar la información del archivo a la aplicación hospedada para permitir una comunicación segura con el bot.</span><span class="sxs-lookup"><span data-stu-id="7059a-163">Now save your text file as you must add the information from the file to your hosted app to allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="7059a-164">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="7059a-164">Messaging extensions</span></span>

<span data-ttu-id="7059a-165">Las extensiones de mensajería permiten a los usuarios solicitar información del servicio y publicar esa información.</span><span class="sxs-lookup"><span data-stu-id="7059a-165">Messaging extensions let users ask for information from your service and post that information.</span></span> <span data-ttu-id="7059a-166">La información se publica en forma de tarjetas en la conversación del canal.</span><span class="sxs-lookup"><span data-stu-id="7059a-166">The information is posted in the form of cards into the channel conversation.</span></span> <span data-ttu-id="7059a-167">Las extensiones de mensajería aparecen en la parte inferior del cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="7059a-167">Messaging extensions appear at the bottom of the compose box.</span></span>

<span data-ttu-id="7059a-168">Siga estos pasos para configurar la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="7059a-168">Complete the following steps to setup your messaging extension:</span></span>

1. <span data-ttu-id="7059a-169">Seleccione **Extensiones de mensajería en** **Funcionalidades** en el panel izquierdo de App Studio para configurar la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="7059a-169">Select **Messaging extensions** under **Capabilities** in the left-hand pane of App Studio to configure the messaging extension:</span></span>

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    <span data-ttu-id="7059a-170">La extensión de mensajería de ejemplo se muestra en el panel **Extensiones de** mensajería.</span><span class="sxs-lookup"><span data-stu-id="7059a-170">The sample messaging extension is listed in the **Messaging Extensions** pane.</span></span>

1. <span data-ttu-id="7059a-171">Seleccione **Eliminar** para quitar la extensión de mensajería, **seleccione Configurar** y siga los mismos pasos usados para [bots](#bots).</span><span class="sxs-lookup"><span data-stu-id="7059a-171">Select **Delete** to remove the messaging extension, select **Set up**, and follow the same steps used for [bots](#bots).</span></span> <span data-ttu-id="7059a-172">Se **muestra el cuadro de diálogo** Extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="7059a-172">The **Messaging Extension** dialog box is displayed.</span></span>
1. <span data-ttu-id="7059a-173">Seleccione la **pestaña Usar bot existente** y Seleccionar de uno de mis **bots existentes**.</span><span class="sxs-lookup"><span data-stu-id="7059a-173">Select the **Use existing bot** tab and **Select from one of my existing bots**.</span></span>
1. <span data-ttu-id="7059a-174">Selecciona el bot que creaste en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="7059a-174">Select the bot you created from the drop-down menu.</span></span> <span data-ttu-id="7059a-175">Agregue un **nombre bot y** seleccione **Guardar** para cerrar el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7059a-175">Add a **Bot name** and select **Save** to close the dialog box.</span></span>
1. <span data-ttu-id="7059a-176">En la **sección Comando,** seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7059a-176">Under the **Command** section, select **Add**.</span></span> <span data-ttu-id="7059a-177">Para agregar un comando basado en búsqueda, seleccione la opción Permitir a los usuarios consultar su servicio para obtener información e **insertarla en un mensaje.**</span><span class="sxs-lookup"><span data-stu-id="7059a-177">To add a search-based command, select the **Allow users to query your service for information and insert that into a message** option.</span></span>
1. <span data-ttu-id="7059a-178">En el **cuadro de diálogo Nuevo** comando, escriba los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="7059a-178">In the **New command** dialog box, enter the following values:</span></span>

    <span data-ttu-id="7059a-179">En **Nuevo comando**:</span><span class="sxs-lookup"><span data-stu-id="7059a-179">Under **New command**:</span></span>

    - <span data-ttu-id="7059a-180">**Identificador de comando:** escriba texto aleatorio</span><span class="sxs-lookup"><span data-stu-id="7059a-180">**Command ID**: Enter random text</span></span>
    - <span data-ttu-id="7059a-181">**Title**: Enter random title</span><span class="sxs-lookup"><span data-stu-id="7059a-181">**Title**: Enter random title</span></span>
    - <span data-ttu-id="7059a-182">**Descripción:** escriba una descripción aleatoria</span><span class="sxs-lookup"><span data-stu-id="7059a-182">**Description**: Enter random description</span></span>

    <span data-ttu-id="7059a-183">En **Parámetro**:</span><span class="sxs-lookup"><span data-stu-id="7059a-183">Under **Parameter**:</span></span>

    - <span data-ttu-id="7059a-184">**Nombre:** escriba el nombre del parámetro</span><span class="sxs-lookup"><span data-stu-id="7059a-184">**Name**: Enter the parameter name</span></span>
    - <span data-ttu-id="7059a-185">**Título:** escriba el título de la tarjeta</span><span class="sxs-lookup"><span data-stu-id="7059a-185">**Title**: Enter the card title</span></span>
    - <span data-ttu-id="7059a-186">**Descripción:** escriba la descripción de la tarjeta</span><span class="sxs-lookup"><span data-stu-id="7059a-186">**Description**: Enter card description</span></span>

1. <span data-ttu-id="7059a-187">Después de escribir la información, seleccione **Guardar** para cerrar el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7059a-187">After you enter the information, select **Save** to close the dialog box.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="7059a-188">Registrar la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="7059a-188">Register your app in Teams</span></span>

<span data-ttu-id="7059a-189">Después de especificar los detalles de la aplicación, siga estos pasos para registrar la aplicación en Teams:</span><span class="sxs-lookup"><span data-stu-id="7059a-189">After entering the details of your app, complete the following steps to register your app in Teams:</span></span>

1. <span data-ttu-id="7059a-190">Usa **Probar y distribuir** App Studio para instalar la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="7059a-190">Use **Test and distribute** of App Studio to install your app in Teams.</span></span> 
1. <span data-ttu-id="7059a-191">Actualice la aplicación hospedada con el identificador de aplicación y la contraseña del bot.</span><span class="sxs-lookup"><span data-stu-id="7059a-191">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="7059a-192">Para la aplicación de ejemplo, usa el mismo id. de la aplicación y la misma contraseña para bot y extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="7059a-192">For the sample app, use the same App ID and password for both bot and messaging extension.</span></span> 
1. <span data-ttu-id="7059a-193">Seleccione **Probar y distribuir en** **Finalizar** en el panel izquierdo de App Studio:</span><span class="sxs-lookup"><span data-stu-id="7059a-193">Select **Test and distribute**  under **Finish** in the left-hand pane of App Studio:</span></span>

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. <span data-ttu-id="7059a-194">Para cargar la aplicación en Teams, selecciona el botón **Instalar** en **Probar y distribuir**:</span><span class="sxs-lookup"><span data-stu-id="7059a-194">To upload your app to Teams, select the **Install** button under **Test and Distribute**:</span></span>

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

1. <span data-ttu-id="7059a-195">Selecciona el **cuadro** Buscar en la **sección Agregar a un** equipo y selecciona un equipo para agregar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7059a-195">Select the **Search** box in the **Add to a team** section and select a team to add the sample app.</span></span> <span data-ttu-id="7059a-196">Puede configurar un equipo especial para las pruebas.</span><span class="sxs-lookup"><span data-stu-id="7059a-196">You can set up a special team for testing.</span></span>
1. <span data-ttu-id="7059a-197">Seleccione el **botón** Instalar en la parte inferior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7059a-197">Select the **Install** button at the bottom of the dialog box.</span></span>

<span data-ttu-id="7059a-198">La aplicación ya está disponible en Teams.</span><span class="sxs-lookup"><span data-stu-id="7059a-198">Your app is now available in Teams.</span></span> <span data-ttu-id="7059a-199">Sin embargo, el bot y la extensión de mensajería no funcionarán hasta que actualice el entorno de aplicaciones hospedadas con los IDs y contraseñas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7059a-199">However, the bot and the messaging extension will not work until you update the hosted applications environment with the App IDs and passwords.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
