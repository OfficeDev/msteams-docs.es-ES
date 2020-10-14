### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="df455-101">Usar App Studio para actualizar el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="df455-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="df455-102">App Studio es una aplicación de Microsoft teams que se puede instalar desde la tienda Teams.</span><span class="sxs-lookup"><span data-stu-id="df455-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="df455-103">Simplifica la creación y el registro de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="df455-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="df455-104">Para instalar App Studio en Teams, haga clic en el icono App Store situado en la parte inferior de la barra izquierda y busque App Studio.</span><span class="sxs-lookup"><span data-stu-id="df455-104">To install App Studio in Teams, click on the app store icon at the bottom of the left hand bar, and search for App Studio.</span></span>

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

<span data-ttu-id="df455-105">Una vez que encuentre el icono de App Studio, haga clic en él y elija *instalar* en el cuadro de diálogo que aparece.</span><span class="sxs-lookup"><span data-stu-id="df455-105">Once you find the tile for App Studio, click on it and choose *install* in the dialog that pops up.</span></span>

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

<span data-ttu-id="df455-106">Una vez instalado App Studio, haga clic en la pestaña del editor de manifiestos para empezar a crear el paquete de la aplicación para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="df455-106">Once App Studio is installed click on the Manifest editor tab to begin creating the app package for your Teams app.</span></span>

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

<span data-ttu-id="df455-107">El ejemplo incluye su propio manifiesto predefinido y está diseñado para compilar un paquete de la aplicación cuando se crea el proyecto.</span><span class="sxs-lookup"><span data-stu-id="df455-107">The sample comes with its own pre-made manifest, and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="df455-108">En .NET esto se hace en Visual Studio y en el nodo JS esto se hace escribiendo `gulp` en la línea de comandos en el directorio raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="df455-108">On .NET this is done in Visual Studio, and on Node JS this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="df455-109">El nombre del paquete de la aplicación generado es *helloworldapp.zip*.</span><span class="sxs-lookup"><span data-stu-id="df455-109">The name of the generated app package is *helloworldapp.zip*.</span></span> <span data-ttu-id="df455-110">Puede buscar este archivo si la ubicación no está clara en la herramienta que está usando.</span><span class="sxs-lookup"><span data-stu-id="df455-110">You can search for this file if the location is not clear in the tool you are using.</span></span>

<span data-ttu-id="df455-111">En la siguiente parte de este tutorial, va a modificar este paquete de la aplicación seleccionando el icono *importar una aplicación existente* en el editor de manifiestos.</span><span class="sxs-lookup"><span data-stu-id="df455-111">In the next part of this walkthrough you are going to modify this app package by selecting the *Import an existing app* tile in the Manifest Editor.</span></span>

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

<span data-ttu-id="df455-112">Una vez que se ha importado el paquete de la aplicación, App Studio debería tener el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="df455-112">Once the app package has been imported App Studio should look like this:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="df455-113">Haga clic en el icono de la aplicación recién importada, *Hello World*.</span><span class="sxs-lookup"><span data-stu-id="df455-113">Click on the tile for your newly imported app, *Hello World*.</span></span>

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="df455-114">Hay una lista de pasos en el lado izquierdo del editor de manifiestos y, a la derecha, una lista de propiedades que deben rellenarse para cada uno de estos pasos.</span><span class="sxs-lookup"><span data-stu-id="df455-114">There is a list of steps in the left-hand side of the Manifest editor, and on the right a list of properties that need to be filled in for each of those steps.</span></span> <span data-ttu-id="df455-115">Desde que empezó con una aplicación de muestra, gran parte de la información ya se ha rellenado. Los pasos siguientes le guiarán por el cambio de las partes que todavía deben actualizarse.</span><span class="sxs-lookup"><span data-stu-id="df455-115">Since you started with a sample app, much of the information is already filled out. The next steps will walk you through changing the parts that still need to be updated.</span></span>

#### <a name="app-details"></a><span data-ttu-id="df455-116">Detalles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="df455-116">App details</span></span>

<span data-ttu-id="df455-117">Haga clic en la entrada detalles de la *aplicación* en *detalles*.</span><span class="sxs-lookup"><span data-stu-id="df455-117">Click on the *App details* entry under *Details*.</span></span> <span data-ttu-id="df455-118">Haga clic en el botón *generar* para crear un nuevo identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="df455-118">Click the *Generate* button to create a new app id.</span></span>

<span data-ttu-id="df455-119">El nuevo identificador de la aplicación debe tener un aspecto similar al siguiente: `2322041b-72bf-459d-b107-f4f335bc35bd` .</span><span class="sxs-lookup"><span data-stu-id="df455-119">Your new app id should look something like: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="df455-120">Mire el resto de los detalles de la aplicación en el panel de la derecha y familiarícese con algunas de las entradas, como *información de desarrolladores* y *Personalización de marca*.</span><span class="sxs-lookup"><span data-stu-id="df455-120">Look through the rest of the App details in the right hand pane, and familiarize yourself with some of the entries such as *Developer information* and *Branding*.</span></span> <span data-ttu-id="df455-121">Estas secciones son importantes si está escribiendo una nueva aplicación para la distribución.</span><span class="sxs-lookup"><span data-stu-id="df455-121">These sections are important if you are writing a new app for distribution.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="df455-122">Capacidades: pestañas</span><span class="sxs-lookup"><span data-stu-id="df455-122">Capabilities: Tabs</span></span>

<span data-ttu-id="df455-123">Las pestañas se encuentran entre los elementos más simples para agregar a una aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="df455-123">Tabs are among the simplest elements to add to a Teams app.</span></span> <span data-ttu-id="df455-124">La aplicación de ejemplo ya admite varias pestañas y puede habilitarlas de la siguiente manera.</span><span class="sxs-lookup"><span data-stu-id="df455-124">The sample app already supports several tabs, and you can enable them as follows.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="df455-125">Ficha equipo</span><span class="sxs-lookup"><span data-stu-id="df455-125">Team tab</span></span>

<span data-ttu-id="df455-126">La aplicación solo puede tener una pestaña de equipo.</span><span class="sxs-lookup"><span data-stu-id="df455-126">Your app can only have one Team tab.</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="df455-127">En este ejemplo, la ficha equipo es donde se encuentra la página de configuración.</span><span class="sxs-lookup"><span data-stu-id="df455-127">In this sample, the Team tab is where your configuration page goes.</span></span> <span data-ttu-id="df455-128">Haga clic en el símbolo *...* al final de la entrada y elija *Editar* en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="df455-128">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="df455-129">Cambie la dirección URL a `https://yourteamsapp.ngrok.io/configure` donde `yourteamsapp.ngrok.io` se debe reemplazar la dirección URL que usó al hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df455-129">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="df455-130">Pestañas personales</span><span class="sxs-lookup"><span data-stu-id="df455-130">Personal tabs</span></span>

<span data-ttu-id="df455-131">La aplicación puede tener hasta 16 pestañas, incluida la pestaña equipo.</span><span class="sxs-lookup"><span data-stu-id="df455-131">Your app can have up to 16 tabs, including the team tab.</span></span>

<span data-ttu-id="df455-132">Las pestañas personales se representan de forma diferente a la ficha equipo. Debe ver la *ficha Hello* que ya aparece en la lista de pestañas personales.</span><span class="sxs-lookup"><span data-stu-id="df455-132">Personal tabs are represented differently from the team tab. You should see *Hello Tab* already listed in the personal tabs list.</span></span> <span data-ttu-id="df455-133">En el momento tiene un valor de marcador de posición `com.contoso.helloworld.hellotab` .</span><span class="sxs-lookup"><span data-stu-id="df455-133">At the moment it has a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="df455-134">Haga clic en el símbolo *...* al final de la entrada y elija *Editar* en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="df455-134">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="df455-135">Aparecerá el siguiente cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df455-135">The following dialog will appear.</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="df455-136">Hay dos campos que debe actualizar con la dirección URL de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df455-136">There are two fields that you need to update with your app URL.</span></span>

- <span data-ttu-id="df455-137">Cambiar la dirección URL del contenido a `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="df455-137">Change Content URL to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="df455-138">Cambiar la dirección URL del sitio web a `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="df455-138">Change Website URL to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="df455-139">Donde `yourteamsapp.ngrok.io` se debe reemplazar por la dirección URL que ha usado anteriormente al hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df455-139">Where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="df455-140">Bots</span><span class="sxs-lookup"><span data-stu-id="df455-140">Bots</span></span>

<span data-ttu-id="df455-141">Los bots son la forma más común de agregar funcionalidad a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df455-141">Bots are the most common way to add functionality to your app.</span></span> <span data-ttu-id="df455-142">La muestra Hello World ya tiene un bot como parte de la muestra, pero todavía no se ha registrado con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="df455-142">The hello world sample already has a bot as part of the sample, but it has not been registered with Microsoft yet.</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="df455-143">El bot que se importó desde el ejemplo no tiene un identificador de aplicación asociado todavía.</span><span class="sxs-lookup"><span data-stu-id="df455-143">The bot that was imported from the sample does not have an App ID associated with it yet.</span></span> <span data-ttu-id="df455-144">Tendrá que crear un nuevo bot para que App Studio pueda crear un nuevo identificador de aplicación y registrarlo en Microsoft.</span><span class="sxs-lookup"><span data-stu-id="df455-144">You will have to create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span> <span data-ttu-id="df455-145">Tenga en cuenta que este es el identificador de la aplicación para bot, que es diferente del identificador de aplicación que se ha creado para la aplicación en un paso anterior.</span><span class="sxs-lookup"><span data-stu-id="df455-145">Note that this is the App ID for the bot, which is different from the App ID that we created for the app in a earlier step.</span></span> <span data-ttu-id="df455-146">Cada bot en una aplicación requiere su propio identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="df455-146">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="df455-147">Haga clic en el botón *eliminar* situado junto al *Bot importado* en la lista de robots.</span><span class="sxs-lookup"><span data-stu-id="df455-147">Click the *delete* button next to the *Imported bot* in the bot list.</span></span>

<span data-ttu-id="df455-148">Ahora no quedan bots para mostrar.</span><span class="sxs-lookup"><span data-stu-id="df455-148">Now there are no bots left to show.</span></span> <span data-ttu-id="df455-149">Haga clic en *configurar*.</span><span class="sxs-lookup"><span data-stu-id="df455-149">Click *Setup*.</span></span> <span data-ttu-id="df455-150">Se mostrará el cuadro de diálogo *configurar un bot* .</span><span class="sxs-lookup"><span data-stu-id="df455-150">This will display the *Set up a bot* dialog.</span></span>

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

<span data-ttu-id="df455-151">Agregue un nombre de bot, por ejemplo `Contoso bot` , y seleccione los tres botones bajo *ámbito*.</span><span class="sxs-lookup"><span data-stu-id="df455-151">Add a bot name such as `Contoso bot`, and select all three buttons under *scope*.</span></span>

<span data-ttu-id="df455-152">Elija *crear bot* para salir del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df455-152">Choose *Create bot* to exit the dialog.</span></span> <span data-ttu-id="df455-153">App Studio dedicará un momento a registrar el bot con Microsoft y, a continuación, deberá mostrar el nuevo bot en la lista de robots.</span><span class="sxs-lookup"><span data-stu-id="df455-153">App Studio will spend a moment registering your bot with Microsoft, and then should display your new bot in the bot list.</span></span> <span data-ttu-id="df455-154">Ahora sería un buen momento para abrir un archivo de texto en el Bloc de notas y copiar y pegar el nuevo identificador de bot en él.</span><span class="sxs-lookup"><span data-stu-id="df455-154">Now would be a good time to open a text file in notepad and copy and paste your new bot id into it.</span></span> <span data-ttu-id="df455-155">Necesitará este identificador más adelante.</span><span class="sxs-lookup"><span data-stu-id="df455-155">You will need this id later.</span></span>

<span data-ttu-id="df455-156">Haga clic en *generar nueva contraseña*y anote la contraseña en el mismo archivo de texto que anotó con el identificador de la aplicación de bot en.</span><span class="sxs-lookup"><span data-stu-id="df455-156">Click *Generate New Password*, and make a note of the password in the same text file you noted your Bot app ID in.</span></span> <span data-ttu-id="df455-157">Esta es la única vez que se mostrará su contraseña, por lo que debe asegurarse de hacerlo ahora.</span><span class="sxs-lookup"><span data-stu-id="df455-157">This is the only time your password will be shown, so be sure to do this now.</span></span>

<span data-ttu-id="df455-158">Actualice la *dirección del punto de conexión del bot* con `https://yourteamsapp.ngrok.io/api/messages` , donde `yourteamsapp.ngrok.io` debe reemplazarse por la dirección URL que usó al hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df455-158">Update the *Bot endpoint address* to `https://yourteamsapp.ngrok.io/api/messages`, where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

<span data-ttu-id="df455-159">Ahora sería un buen momento para guardar el archivo de texto si todavía no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="df455-159">Now would be a good time to save your text file if you have not done so already.</span></span> <span data-ttu-id="df455-160">Esta información se agregará a la aplicación hospedada más adelante en este tutorial, lo que permitirá la comunicación segura con el bot.</span><span class="sxs-lookup"><span data-stu-id="df455-160">You will add this information to your hosted app later in this walkthrough, which will allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="df455-161">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="df455-161">Messaging extensions</span></span>

<span data-ttu-id="df455-162">Las extensiones de mensajería permiten a los usuarios solicitar información de su servicio y publicarla, en forma de tarjetas, directamente en la conversación del canal.</span><span class="sxs-lookup"><span data-stu-id="df455-162">Messaging extensions let users ask for information from your service and post that information, in the form of cards, right into the channel conversation.</span></span> <span data-ttu-id="df455-163">Las extensiones de mensajería aparecen a lo largo de la parte inferior del cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="df455-163">Messaging extensions appear along the bottom of the compose box.</span></span>

<span data-ttu-id="df455-164">Haga clic en *extensiones de mensajería* en *funcionalidades* en la columna izquierda de App Studio para comenzar a configurar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="df455-164">Click on *Messaging extensions* under *Capabilities* in the left hand column of App Studio to begin configuring the messaging extension.</span></span>

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

<span data-ttu-id="df455-165">La extensión de mensajería de muestra aparece en el panel de la derecha, en *extensiones de mensajería*.</span><span class="sxs-lookup"><span data-stu-id="df455-165">The sample messaging extension is listed in the right hand pane under *Messaging Extensions*.</span></span> <span data-ttu-id="df455-166">Haga clic en *eliminar* de nuevo para quitar esta entrada y, a continuación, haga clic en el botón *configurar* siguiendo los mismos pasos que siguió para los bots.</span><span class="sxs-lookup"><span data-stu-id="df455-166">Click *Delete* again to remove this entry, and then click the *Set up* button following the same steps as you followed for bots.</span></span> <span data-ttu-id="df455-167">Se mostrará el cuadro de diálogo de la *extensión de mensajería* .</span><span class="sxs-lookup"><span data-stu-id="df455-167">This will display the *Messaging Extension* dialog.</span></span>

<span data-ttu-id="df455-168">Seleccione la pestaña *usar bot existente* y, a continuación, *Seleccione uno de los bots existentes*.</span><span class="sxs-lookup"><span data-stu-id="df455-168">Select the *Use existing bot* tab, then *Select from one of my existing bots*.</span></span> <span data-ttu-id="df455-169">En el menú desplegable, seleccione el bot que creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="df455-169">In the drop-down menu, select the bot you created in the section above.</span></span> <span data-ttu-id="df455-170">Agregue un *nombre de bot* y haga clic en *Guardar* para cerrar el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df455-170">Add a *Bot name* and click *Save* to close the dialog.</span></span>

<span data-ttu-id="df455-171">En la sección *comando* , haga clic en *Agregar*.</span><span class="sxs-lookup"><span data-stu-id="df455-171">Under the *Command* section, click *Add*.</span></span> <span data-ttu-id="df455-172">Estamos agregando un comando basado en la búsqueda, por lo que debe elegir la opción *permitir que los usuarios consulten su servicio...*</span><span class="sxs-lookup"><span data-stu-id="df455-172">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span></span>

<span data-ttu-id="df455-173">En el cuadro de diálogo *nuevo comando* , escriba los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="df455-173">In the *New command* dialog enter the following values.</span></span>

<span data-ttu-id="df455-174">En *nuevo comando*:</span><span class="sxs-lookup"><span data-stu-id="df455-174">Under *New command*:</span></span>

- <span data-ttu-id="df455-175">*Identificador de comando*  = getRandomText</span><span class="sxs-lookup"><span data-stu-id="df455-175">*Command ID*  = getRandomText</span></span>
- <span data-ttu-id="df455-176">*Title*       = obtener texto aleatorio para divertirse</span><span class="sxs-lookup"><span data-stu-id="df455-176">*Title*       = Get some random text for fun</span></span>
- <span data-ttu-id="df455-177">*Description* = obtiene texto e imágenes aleatorios</span><span class="sxs-lookup"><span data-stu-id="df455-177">*Description* = Gets some random text and images</span></span>

<span data-ttu-id="df455-178">En *parámetro*:</span><span class="sxs-lookup"><span data-stu-id="df455-178">Under *Parameter*:</span></span>

- <span data-ttu-id="df455-179">*Name*        = cardTitle</span><span class="sxs-lookup"><span data-stu-id="df455-179">*Name*        = cardTitle</span></span>
- <span data-ttu-id="df455-180">*Title*       = título de la tarjeta</span><span class="sxs-lookup"><span data-stu-id="df455-180">*Title*       = Card title</span></span>
- <span data-ttu-id="df455-181">*Description* = título de la tarjeta para usar</span><span class="sxs-lookup"><span data-stu-id="df455-181">*Description* = Card title to use</span></span>

<span data-ttu-id="df455-182">Una vez que haya introducido la información, haga clic en *Guardar* para cerrar el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df455-182">Once you're entered the information, click *Save* to close the dialog.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="df455-183">Registrar la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="df455-183">Register your app in Teams</span></span>

<span data-ttu-id="df455-184">Ya ha completado la especificación de los detalles de la aplicación, pero quedan dos pasos.</span><span class="sxs-lookup"><span data-stu-id="df455-184">You have now completed entering the details of your app, but two steps remain.</span></span> <span data-ttu-id="df455-185">En primer lugar, debe usar la sección probar y distribuir de App Studio para instalar la aplicación en Teams y, en segundo lugar, debe actualizar la aplicación hospedada con el identificador de aplicación y la contraseña de su bot.</span><span class="sxs-lookup"><span data-stu-id="df455-185">First you must use the Test and Distribute section of App Studio to install your app in Teams, and second you must update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="df455-186">Recuerde que el ejemplo espera usar el mismo identificador de aplicación y la misma contraseña para el bot y la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="df455-186">Remember that the sample expects to use the same App ID and password for both the bot and the messaging extension.</span></span>

<span data-ttu-id="df455-187">Haga clic en el elemento *probar y distribuir* en *Finalizar* en la columna izquierda de App Studio.</span><span class="sxs-lookup"><span data-stu-id="df455-187">Click on the *Test and distribute* item under *Finish* in the left hand column of App Studio.</span></span>

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

<span data-ttu-id="df455-188">Para cargar la aplicación en Teams, haga clic en el botón *instalar* en *probar y distribuir*.</span><span class="sxs-lookup"><span data-stu-id="df455-188">In order to upload your app to Teams, click the *Install* button under *Test and Distribute*.</span></span>

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

<span data-ttu-id="df455-189">Haga clic en el cuadro de *búsqueda* en la sección *Agregar a un equipo* y seleccione un equipo al que desee agregar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="df455-189">Click on the *Search* box in the *Add to a team* section and select a team to add the sample app to.</span></span> <span data-ttu-id="df455-190">Normalmente querrá configurar un equipo especial para realizar las pruebas.</span><span class="sxs-lookup"><span data-stu-id="df455-190">Usually you will want to set up a special team for testing.</span></span>

<span data-ttu-id="df455-191">Haga clic en el botón *instalar* situado en la parte inferior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df455-191">Click the *Install* button at the bottom of the dialog.</span></span>

<span data-ttu-id="df455-192">Esto finaliza la parte de App Studio de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="df455-192">This finishes the App Studio portion of this walkthrough.</span></span> <span data-ttu-id="df455-193">Ahora debería ver que la aplicación se está ejecutando en Teams, pero el bot y la extensión de mensajería no funcionarán hasta que actualice el entorno de aplicaciones hospedadas para conocer los identificadores de aplicación y las contraseñas.</span><span class="sxs-lookup"><span data-stu-id="df455-193">You should now see your app running in Teams, however the bot and the messaging extension will not work until you update the hosted applications environment to know what the App IDs and passwords are.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
