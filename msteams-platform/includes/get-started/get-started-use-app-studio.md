### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="660b0-101">Use App Studio para actualizar el paquete de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="660b0-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="660b0-102">App Studio es una aplicación Teams que puedes instalar desde la tienda Teams.</span><span class="sxs-lookup"><span data-stu-id="660b0-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="660b0-103">Simplifica la creación y registro de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="660b0-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="660b0-104">Complete los pasos siguientes para actualizar el paquete de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="660b0-104">Complete the following steps to update the app package:</span></span>

1. <span data-ttu-id="660b0-105">Para instalar App Studio en Teams, seleccione el icono **Aplicaciones** en la parte inferior de la barra izquierda y busque **App Studio:**</span><span class="sxs-lookup"><span data-stu-id="660b0-105">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**:</span></span>

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. <span data-ttu-id="660b0-106">Seleccione el icono **de App Studio** y elija **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="660b0-106">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="660b0-107">App Studio está instalado:</span><span class="sxs-lookup"><span data-stu-id="660b0-107">The App Studio is installed:</span></span>

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. <span data-ttu-id="660b0-108">Para crear el paquete de aplicación para la aplicación Teams, seleccione la pestaña **Editor de manifiestos** en **App Studio:**</span><span class="sxs-lookup"><span data-stu-id="660b0-108">To create the app package for your Teams app, select the **Manifest editor** tab in **App Studio**:</span></span>

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    <span data-ttu-id="660b0-109">El ejemplo viene con su propio manifiesto y está diseñado para crear un paquete de aplicación cuando se compila el proyecto.</span><span class="sxs-lookup"><span data-stu-id="660b0-109">The sample comes with its own manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="660b0-110">En .NET esto se hace en Visual Studio y en Node.js esto se hace escribiendo `gulp` en la línea de comandos en el directorio raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="660b0-110">On .NET this is done in Visual Studio and on Node.js this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

    <span data-ttu-id="660b0-111">El nombre del paquete de aplicación generado se **helloworldapp.zip**.</span><span class="sxs-lookup"><span data-stu-id="660b0-111">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="660b0-112">Puede buscar este archivo si la ubicación no está clara en la herramienta que está utilizando.</span><span class="sxs-lookup"><span data-stu-id="660b0-112">You can search for this file if the location is not clear in the tool you are using.</span></span>

1. <span data-ttu-id="660b0-113">Ahora para modificar este paquete de aplicación, seleccione **Importar una aplicación existente** en el editor de **manifiestos:**</span><span class="sxs-lookup"><span data-stu-id="660b0-113">Now to modify this app package, select **Import an existing app** in the **Manifest editor**:</span></span>

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. <span data-ttu-id="660b0-114">Seleccione el icono **Hello World** para su aplicación recién importada:</span><span class="sxs-lookup"><span data-stu-id="660b0-114">Select the **Hello World** tile for your newly imported app:</span></span>

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="660b0-115">La siguiente imagen muestra el paquete de aplicación importado en App Studio:</span><span class="sxs-lookup"><span data-stu-id="660b0-115">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="660b0-116">En el lado izquierdo del editor de manifiestos hay una lista de pasos.</span><span class="sxs-lookup"><span data-stu-id="660b0-116">On the left-hand side of the Manifest editor there is a list of steps.</span></span> <span data-ttu-id="660b0-117">En el lado derecho hay una lista de propiedades que deben rellenarse para cada paso.</span><span class="sxs-lookup"><span data-stu-id="660b0-117">On the right-hand side there is a list of properties that need to be filled in for each step.</span></span> <span data-ttu-id="660b0-118">Como comenzó con una aplicación de ejemplo, gran parte de la información ya se ha completado.</span><span class="sxs-lookup"><span data-stu-id="660b0-118">As you started with a sample app, much of the information is already completed.</span></span> <span data-ttu-id="660b0-119">Los pasos siguientes le permiten actualizar las propiedades de la aplicación Hello World.</span><span class="sxs-lookup"><span data-stu-id="660b0-119">The next steps enable you to update the properties of the Hello World app.</span></span>

#### <a name="app-details"></a><span data-ttu-id="660b0-120">Detalles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="660b0-120">App details</span></span>

<span data-ttu-id="660b0-121">Seleccione **Detalles de la aplicación** en **Detalles**.</span><span class="sxs-lookup"><span data-stu-id="660b0-121">Select **App details** under **Details**.</span></span> <span data-ttu-id="660b0-122">Seleccione el botón **Generar** para crear un nuevo ID de aplicación.</span><span class="sxs-lookup"><span data-stu-id="660b0-122">Select the **Generate** button to create a new App ID.</span></span>

<span data-ttu-id="660b0-123">El nuevo ID de aplicación es similar a `2322041b-72bf-459d-b107-f4f335bc35bd` .</span><span class="sxs-lookup"><span data-stu-id="660b0-123">Your new App ID is similar to `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="660b0-124">Revisa los detalles de la aplicación en el panel derecho, incluida la **información del desarrollador** y los detalles de personalización de **marca.**</span><span class="sxs-lookup"><span data-stu-id="660b0-124">Go through the app details in the right-hand pane including **Developer information** and **Branding** details.</span></span> <span data-ttu-id="660b0-125">Estos detalles son importantes si está escribiendo una nueva aplicación para su distribución.</span><span class="sxs-lookup"><span data-stu-id="660b0-125">These details are important if you are writing a new app for distribution.</span></span>

#### <a name="tabs"></a><span data-ttu-id="660b0-126">Pestañas</span><span class="sxs-lookup"><span data-stu-id="660b0-126">Tabs</span></span>

<span data-ttu-id="660b0-127">Es fácil agregar pestañas a una aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="660b0-127">It is simple to add tabs to a Teams app.</span></span> <span data-ttu-id="660b0-128">La aplicación de ejemplo ya admite varias pestañas y puede habilitarlas.</span><span class="sxs-lookup"><span data-stu-id="660b0-128">The sample app already supports several tabs, and you can enable them.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="660b0-129">Ficha Equipo</span><span class="sxs-lookup"><span data-stu-id="660b0-129">Team tab</span></span>

<span data-ttu-id="660b0-130">La aplicación solo puede tener una pestaña Equipo:</span><span class="sxs-lookup"><span data-stu-id="660b0-130">Your app can only have one Team tab:</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="660b0-131">En este ejemplo, la pestaña Equipo es donde se muestra la página de configuración.</span><span class="sxs-lookup"><span data-stu-id="660b0-131">In this sample, the Team tab is where your configuration page is displayed.</span></span> <span data-ttu-id="660b0-132">Seleccione el **símbolo ...** de la url de configuración de **tabulación** y elija **Editar** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="660b0-132">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="660b0-133">Cambie la dirección URL a `https://yourteamsapp.ngrok.io/configure` donde se debe reemplazar con la dirección URL que usó al `yourteamsapp.ngrok.io` [hospedar la aplicación.](#host-the-sample-app)</span><span class="sxs-lookup"><span data-stu-id="660b0-133">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` must be replaced with the URL that you used when [hosting your app](#host-the-sample-app).</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="660b0-134">Pestañas personales</span><span class="sxs-lookup"><span data-stu-id="660b0-134">Personal tabs</span></span>

<span data-ttu-id="660b0-135">La aplicación puede tener hasta 16 pestañas, incluida la pestaña Equipo.</span><span class="sxs-lookup"><span data-stu-id="660b0-135">Your app can have up to 16 tabs, including the Team tab.</span></span>

<span data-ttu-id="660b0-136">Las pestañas personales son diferentes de la pestaña **Equipo.** `com.contoso.helloworld.hellotab`</span><span class="sxs-lookup"><span data-stu-id="660b0-136">Personal tabs are different from the Team tab. **Hello Tab** is already listed in the personal tabs list with a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="660b0-137">Seleccione el **símbolo ...** de la url de configuración de **tabulación** y elija **Editar** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="660b0-137">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="660b0-138">Aparece el siguiente cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="660b0-138">The following dialog box appears:</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="660b0-139">Actualice los siguientes cuadros con la DIRECCIÓN URL de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="660b0-139">Update the following boxes with your app URL:</span></span>

- <span data-ttu-id="660b0-140">Cambie el cuadro **Url de contenido** a `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="660b0-140">Change the **Content URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="660b0-141">Cambie el cuadro URL del **sitio web** a `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="660b0-141">Change the **Website URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="660b0-142">Reemplace `yourteamsapp.ngrok.io` por la dirección URL que usó al hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="660b0-142">Replace `yourteamsapp.ngrok.io` by the URL that you used when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="660b0-143">Bots</span><span class="sxs-lookup"><span data-stu-id="660b0-143">Bots</span></span>

<span data-ttu-id="660b0-144">Es fácil agregar la funcionalidad de bots a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="660b0-144">It is easy to add the bots functionality to your app.</span></span> <span data-ttu-id="660b0-145">La aplicación de ejemplo **Hello World** ya tiene un bot como parte del ejemplo, pero debe registrarlo con Microsoft:</span><span class="sxs-lookup"><span data-stu-id="660b0-145">The **Hello World** sample app already has a bot as part of the sample, but you must register it with Microsoft:</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="660b0-146">El bot que se importó desde el ejemplo no tiene un identificador de aplicación asociado.</span><span class="sxs-lookup"><span data-stu-id="660b0-146">The bot that was imported from the sample does not have an associated App ID.</span></span> <span data-ttu-id="660b0-147">Debe crear un nuevo bot para que App Studio pueda crear un nuevo identificador de aplicación y registrarlo con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="660b0-147">You must create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span>

> [!NOTE]
> <span data-ttu-id="660b0-148">El identificador de aplicación creado por App Studio para el bot es diferente del identificador de aplicación creado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="660b0-148">The App ID created by App Studio for the bot is different from the App ID created for the app.</span></span> <span data-ttu-id="660b0-149">Cada bot de una aplicación requiere su propio IDENTIFICADOR de aplicación.</span><span class="sxs-lookup"><span data-stu-id="660b0-149">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="660b0-150">Complete los siguientes pasos para configurar el bot:</span><span class="sxs-lookup"><span data-stu-id="660b0-150">Complete the following steps to setup your bot:</span></span>

1. <span data-ttu-id="660b0-151">Seleccione **Eliminar** junto al bot importado en la lista de bots.</span><span class="sxs-lookup"><span data-stu-id="660b0-151">Select **Delete** next to the imported bot in the bot list.</span></span> <span data-ttu-id="660b0-152">Ahora no quedan bots por mostrar.</span><span class="sxs-lookup"><span data-stu-id="660b0-152">Now there are no bots left to show.</span></span> 
1. <span data-ttu-id="660b0-153">Seleccione **Configuración** para mostrar el cuadro de diálogo **Configurar un bot.**</span><span class="sxs-lookup"><span data-stu-id="660b0-153">Select **Setup** to display the **Set up a bot** dialog box.</span></span>

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. <span data-ttu-id="660b0-154">Agregue un **bot** name Contoso bot y seleccione las tres casillas de verificación en **Ámbito**.</span><span class="sxs-lookup"><span data-stu-id="660b0-154">Add a bot name **Contoso bot** and select all three check boxes under **Scope**.</span></span>
1. <span data-ttu-id="660b0-155">Elija **Guardar** para salir del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="660b0-155">Choose **Save** to exit the dialog box.</span></span> <span data-ttu-id="660b0-156">App Studio registra el bot con Microsoft y muestra el nuevo bot en la lista de bots.</span><span class="sxs-lookup"><span data-stu-id="660b0-156">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> 
1. <span data-ttu-id="660b0-157">Ahora abra un archivo de texto en el bloc de notas y copie y pegue su nuevo ID de bot en él.</span><span class="sxs-lookup"><span data-stu-id="660b0-157">Now open a text file in notepad and copy and paste your new bot ID into it.</span></span>
1. <span data-ttu-id="660b0-158">Haga clic en **Generar nueva contraseña** y anote la contraseña en el mismo archivo de texto que anotó el ID de aplicación del bot.</span><span class="sxs-lookup"><span data-stu-id="660b0-158">Click **Generate New Password**, and note the password in the same text file you noted your bot App ID.</span></span>
1. <span data-ttu-id="660b0-159">Actualice la **dirección de punto de conexión de Bot** a y `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` reemplacela por la dirección URL que usó al hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="660b0-159">Update the **Bot endpoint address** to `https://yourteamsapp.ngrok.io/api/messages`, and replace `yourteamsapp.ngrok.io` with the URL that you used when hosting your app.</span></span>
1. <span data-ttu-id="660b0-160">Ahora guarde el archivo de texto, ya que debe agregar la información del archivo a la aplicación hospedada para permitir una comunicación segura con el bot.</span><span class="sxs-lookup"><span data-stu-id="660b0-160">Now save your text file as you must add the information from the file to your hosted app to allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="660b0-161">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="660b0-161">Messaging extensions</span></span>

<span data-ttu-id="660b0-162">Las extensiones de mensajería permiten a los usuarios solicitar información de su servicio y publicar esa información.</span><span class="sxs-lookup"><span data-stu-id="660b0-162">Messaging extensions let users ask for information from your service and post that information.</span></span> <span data-ttu-id="660b0-163">La información se publica en forma de tarjetas en la conversación del canal.</span><span class="sxs-lookup"><span data-stu-id="660b0-163">The information is posted in the form of cards into the channel conversation.</span></span> <span data-ttu-id="660b0-164">Las extensiones de mensajería aparecen en la parte inferior del cuadro de composición.</span><span class="sxs-lookup"><span data-stu-id="660b0-164">Messaging extensions appear at the bottom of the compose box.</span></span>

<span data-ttu-id="660b0-165">Complete los siguientes pasos para configurar la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="660b0-165">Complete the following steps to setup your messaging extension:</span></span>

1. <span data-ttu-id="660b0-166">Seleccione **Extensiones de mensajería** en **Capacidades** en el panel izquierdo de App Studio para configurar la extensión de mensajería:</span><span class="sxs-lookup"><span data-stu-id="660b0-166">Select **Messaging extensions** under **Capabilities** in the left-hand pane of App Studio to configure the messaging extension:</span></span>

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    <span data-ttu-id="660b0-167">La extensión de mensajería de ejemplo aparece en el panel **Extensiones de mensajería.**</span><span class="sxs-lookup"><span data-stu-id="660b0-167">The sample messaging extension is listed in the **Messaging Extensions** pane.</span></span>

1. <span data-ttu-id="660b0-168">Seleccione **Eliminar** para quitar la extensión de mensajería, seleccione **Configurar** y siga los mismos pasos utilizados para [los bots.](#bots)</span><span class="sxs-lookup"><span data-stu-id="660b0-168">Select **Delete** to remove the messaging extension, select **Set up**, and follow the same steps used for [bots](#bots).</span></span> <span data-ttu-id="660b0-169">Se muestra el cuadro de diálogo **Extensión de mensajería.**</span><span class="sxs-lookup"><span data-stu-id="660b0-169">The **Messaging Extension** dialog box is displayed.</span></span>
1. <span data-ttu-id="660b0-170">Seleccione la pestaña **Usar bot existente** y Seleccione uno de mis **bots existentes.**</span><span class="sxs-lookup"><span data-stu-id="660b0-170">Select the **Use existing bot** tab and **Select from one of my existing bots**.</span></span>
1. <span data-ttu-id="660b0-171">Seleccione el bot que creó en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="660b0-171">Select the bot you created from the drop-down menu.</span></span> <span data-ttu-id="660b0-172">Agregue un **nombre de bot** y seleccione **Guardar** para cerrar el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="660b0-172">Add a **Bot name** and select **Save** to close the dialog box.</span></span>
1. <span data-ttu-id="660b0-173">En la sección **Comando,** seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="660b0-173">Under the **Command** section, select **Add**.</span></span> <span data-ttu-id="660b0-174">Para agregar un comando basado en búsqueda, seleccione la opción **Permitir que los usuarios consulten el servicio en busca de información e insértela en un mensaje.**</span><span class="sxs-lookup"><span data-stu-id="660b0-174">To add a search-based command, select the **Allow users to query your service for information and insert that into a message** option.</span></span>
1. <span data-ttu-id="660b0-175">En el cuadro de diálogo **Nuevo comando,** escriba los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="660b0-175">In the **New command** dialog box, enter the following values:</span></span>

    <span data-ttu-id="660b0-176">Bajo **nuevo comando**:</span><span class="sxs-lookup"><span data-stu-id="660b0-176">Under **New command**:</span></span>

    - <span data-ttu-id="660b0-177">**Id. de comando**: Introduzca texto aleatorio</span><span class="sxs-lookup"><span data-stu-id="660b0-177">**Command ID**: Enter random text</span></span>
    - <span data-ttu-id="660b0-178">**Título**: Introduzca el título aleatorio</span><span class="sxs-lookup"><span data-stu-id="660b0-178">**Title**: Enter random title</span></span>
    - <span data-ttu-id="660b0-179">**Descripción**: Introduzca la descripción aleatoria</span><span class="sxs-lookup"><span data-stu-id="660b0-179">**Description**: Enter random description</span></span>

    <span data-ttu-id="660b0-180">Bajo **parámetro**:</span><span class="sxs-lookup"><span data-stu-id="660b0-180">Under **Parameter**:</span></span>

    - <span data-ttu-id="660b0-181">**Nombre**: Escriba el nombre del parámetro</span><span class="sxs-lookup"><span data-stu-id="660b0-181">**Name**: Enter the parameter name</span></span>
    - <span data-ttu-id="660b0-182">**Título**: Introduzca el título de la tarjeta</span><span class="sxs-lookup"><span data-stu-id="660b0-182">**Title**: Enter the card title</span></span>
    - <span data-ttu-id="660b0-183">**Descripción**: Introduzca la descripción de la tarjeta</span><span class="sxs-lookup"><span data-stu-id="660b0-183">**Description**: Enter card description</span></span>

1. <span data-ttu-id="660b0-184">Después de introducir la información, seleccione **Guardar** para cerrar el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="660b0-184">After you enter the information, select **Save** to close the dialog box.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="660b0-185">Registra tu aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="660b0-185">Register your app in Teams</span></span>

<span data-ttu-id="660b0-186">Después de introducir los detalles de la aplicación, siga estos pasos para registrar la aplicación en Teams:</span><span class="sxs-lookup"><span data-stu-id="660b0-186">After entering the details of your app, complete the following steps to register your app in Teams:</span></span>

1. <span data-ttu-id="660b0-187">Usa **Probar y distribuir** App Studio para instalar la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="660b0-187">Use **Test and distribute** of App Studio to install your app in Teams.</span></span> 
1. <span data-ttu-id="660b0-188">Actualice la aplicación hospedada con el ID de aplicación y la contraseña del bot.</span><span class="sxs-lookup"><span data-stu-id="660b0-188">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="660b0-189">Para la aplicación de ejemplo, use el mismo IDENTIFICADOR de aplicación y contraseña para la extensión de bot y mensajería.</span><span class="sxs-lookup"><span data-stu-id="660b0-189">For the sample app, use the same App ID and password for both bot and messaging extension.</span></span> 
1. <span data-ttu-id="660b0-190">Seleccione **Probar y distribuir**  en **Finalizar** en el panel izquierdo de App Studio:</span><span class="sxs-lookup"><span data-stu-id="660b0-190">Select **Test and distribute**  under **Finish** in the left-hand pane of App Studio:</span></span>

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. <span data-ttu-id="660b0-191">Para cargar la aplicación en Teams, seleccione el botón **Instalar** en **Probar y distribuir:**</span><span class="sxs-lookup"><span data-stu-id="660b0-191">To upload your app to Teams, select the **Install** button under **Test and Distribute**:</span></span>

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

1. <span data-ttu-id="660b0-192">Seleccione el cuadro **Buscar** en la sección **Agregar a un equipo** y seleccione un equipo para agregar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="660b0-192">Select the **Search** box in the **Add to a team** section and select a team to add the sample app.</span></span> <span data-ttu-id="660b0-193">Puede configurar un equipo especial para las pruebas.</span><span class="sxs-lookup"><span data-stu-id="660b0-193">You can set up a special team for testing.</span></span>
1. <span data-ttu-id="660b0-194">Seleccione el botón **Instalar** en la parte inferior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="660b0-194">Select the **Install** button at the bottom of the dialog box.</span></span>

<span data-ttu-id="660b0-195">La aplicación ya está disponible en Teams.</span><span class="sxs-lookup"><span data-stu-id="660b0-195">Your app is now available in Teams.</span></span> <span data-ttu-id="660b0-196">Sin embargo, el bot y la extensión de mensajería no funcionarán hasta que actualice el entorno de aplicaciones hospedadas con los archivos DE YD y contraseñas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="660b0-196">However, the bot and the messaging extension will not work until you update the hosted applications environment with the App IDs and passwords.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
