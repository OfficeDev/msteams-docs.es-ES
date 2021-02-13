### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="31185-101">Usar App Studio para actualizar el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="31185-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="31185-102">App Studio es una aplicación de Teams que puede instalar desde la tienda de Teams.</span><span class="sxs-lookup"><span data-stu-id="31185-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="31185-103">Simplifica la creación y el registro de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="31185-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="31185-104">Para instalar App Studio en  Teams, seleccione el icono Aplicaciones en la parte inferior de la barra izquierda y busque **App Studio.**</span><span class="sxs-lookup"><span data-stu-id="31185-104">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**.</span></span>

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

<span data-ttu-id="31185-105">Seleccione el **icono de App Studio** y elija **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="31185-105">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="31185-106">App Studio está instalado.</span><span class="sxs-lookup"><span data-stu-id="31185-106">The App Studio is installed.</span></span>

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

<span data-ttu-id="31185-107">Seleccione la **pestaña Editor de manifiestos** para crear el paquete de la aplicación para su aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="31185-107">Select the **Manifest editor** tab to create the app package for your Teams app.</span></span>

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

<span data-ttu-id="31185-108">El ejemplo viene con su propio manifiesto predefinido y está diseñado para crear un paquete de la aplicación cuando se crea el proyecto.</span><span class="sxs-lookup"><span data-stu-id="31185-108">The sample comes with its own pre-made manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="31185-109">En .NET, esto se realiza en Visual Studio y, en Node JS, esto se realiza escribiendo en la línea de comandos del directorio `gulp` raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="31185-109">On .NET this is done in Visual Studio, and on Node JS this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="31185-110">El nombre del paquete de la aplicación generado **eshelloworldapp.zip**.</span><span class="sxs-lookup"><span data-stu-id="31185-110">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="31185-111">Puedes buscar este archivo si la ubicación no está clara en la herramienta que estás usando.</span><span class="sxs-lookup"><span data-stu-id="31185-111">You can search for this file if the location is not clear in the tool you are using.</span></span>

<span data-ttu-id="31185-112">Ahora, para modificar este paquete de la aplicación, seleccione el icono Importar **una aplicación** existente en el editor **de manifiestos.**</span><span class="sxs-lookup"><span data-stu-id="31185-112">Now to modify this app package, select the **Import an existing app** tile in the **Manifest editor**.</span></span>

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

<span data-ttu-id="31185-113">Haz clic **en el icono Hola** a todos para la aplicación recién importada.</span><span class="sxs-lookup"><span data-stu-id="31185-113">Click the **Hello World** tile for your newly imported app.</span></span>

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="31185-114">La siguiente imagen muestra el paquete de la aplicación importado en App Studio:</span><span class="sxs-lookup"><span data-stu-id="31185-114">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="31185-115">Hay una lista de pasos en el lado izquierdo del editor de manifiestos y, en el lado derecho, una lista de propiedades que deben rellenarse para cada uno de esos pasos.</span><span class="sxs-lookup"><span data-stu-id="31185-115">There is a list of steps on the left-hand side of the Manifest editor and on the right-hand side, a list of properties that need to be filled in for each of those steps.</span></span> <span data-ttu-id="31185-116">Desde que empezaste con una aplicación de ejemplo, gran parte de la información ya está rellenada. Los pasos siguientes le ayudarán a cambiar los elementos que aún deben actualizarse.</span><span class="sxs-lookup"><span data-stu-id="31185-116">Since you started with a sample app, much of the information is already filled out. The next steps will walk you through changing the parts that still need to be updated.</span></span>

#### <a name="app-details"></a><span data-ttu-id="31185-117">Detalles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="31185-117">App details</span></span>

<span data-ttu-id="31185-118">Haga clic en la *entrada detalles de la* aplicación en *Detalles.*</span><span class="sxs-lookup"><span data-stu-id="31185-118">Click on the *App details* entry under *Details*.</span></span> <span data-ttu-id="31185-119">Haz clic *en el botón* Generar para crear un nuevo identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="31185-119">Click the *Generate* button to create a new app id.</span></span>

<span data-ttu-id="31185-120">El nuevo id. de aplicación debe tener un aspecto parecido a: `2322041b-72bf-459d-b107-f4f335bc35bd` .</span><span class="sxs-lookup"><span data-stu-id="31185-120">Your new app id should look something like: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="31185-121">Consulte el resto de los detalles de la aplicación en el panel derecho y  familiarícese con algunas de las entradas, como información de desarrollador y *personalización de marca.*</span><span class="sxs-lookup"><span data-stu-id="31185-121">Look through the rest of the App details in the right-hand pane, and familiarize yourself with some of the entries such as *Developer information* and *Branding*.</span></span> <span data-ttu-id="31185-122">Estas secciones son importantes si estás escribiendo una nueva aplicación para su distribución.</span><span class="sxs-lookup"><span data-stu-id="31185-122">These sections are important if you are writing a new app for distribution.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="31185-123">Funcionalidades: pestañas</span><span class="sxs-lookup"><span data-stu-id="31185-123">Capabilities: Tabs</span></span>

<span data-ttu-id="31185-124">Las pestañas son uno de los elementos más sencillos para agregar a una aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="31185-124">Tabs are among the simplest elements to add to a Teams app.</span></span> <span data-ttu-id="31185-125">La aplicación de ejemplo ya admite varias pestañas y puedes habilitarlas de la siguiente manera.</span><span class="sxs-lookup"><span data-stu-id="31185-125">The sample app already supports several tabs, and you can enable them as follows.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="31185-126">Pestaña Equipo</span><span class="sxs-lookup"><span data-stu-id="31185-126">Team tab</span></span>

<span data-ttu-id="31185-127">La aplicación solo puede tener una pestaña equipo.</span><span class="sxs-lookup"><span data-stu-id="31185-127">Your app can only have one Team tab.</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="31185-128">En este ejemplo, la pestaña Equipo es donde va la página de configuración.</span><span class="sxs-lookup"><span data-stu-id="31185-128">In this sample, the Team tab is where your configuration page goes.</span></span> <span data-ttu-id="31185-129">Haga clic en *el símbolo ...* al final de la entrada y elija *Editar* en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="31185-129">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="31185-130">Cambie la dirección URL a la dirección URL en la que debe reemplazarse por la dirección URL que `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` usó anteriormente al hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31185-130">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="31185-131">Pestañas personales</span><span class="sxs-lookup"><span data-stu-id="31185-131">Personal tabs</span></span>

<span data-ttu-id="31185-132">La aplicación puede tener hasta 16 pestañas, incluida la pestaña de equipo.</span><span class="sxs-lookup"><span data-stu-id="31185-132">Your app can have up to 16 tabs, including the team tab.</span></span>

<span data-ttu-id="31185-133">Las pestañas personales se representan de forma diferente a la pestaña de equipo. Debería ver la *pestaña Hello* ya en la lista de pestañas personales.</span><span class="sxs-lookup"><span data-stu-id="31185-133">Personal tabs are represented differently from the team tab. You should see *Hello Tab* already listed in the personal tabs list.</span></span> <span data-ttu-id="31185-134">En este momento tiene un valor de marcador de `com.contoso.helloworld.hellotab` posición.</span><span class="sxs-lookup"><span data-stu-id="31185-134">At the moment it has a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="31185-135">Haga clic en *el símbolo ...* al final de la entrada y elija *Editar* en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="31185-135">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="31185-136">Aparecerá el siguiente cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31185-136">The following dialog will appear.</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="31185-137">Hay dos campos que debes actualizar con la dirección URL de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31185-137">There are two fields that you need to update with your app URL.</span></span>

- <span data-ttu-id="31185-138">Cambiar la dirección URL de contenido a `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="31185-138">Change Content URL to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="31185-139">Cambiar la dirección URL del sitio web a `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="31185-139">Change Website URL to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="31185-140">Dónde `yourteamsapp.ngrok.io` debe reemplazarse por la dirección URL que usó anteriormente al hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31185-140">Where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="31185-141">Bots</span><span class="sxs-lookup"><span data-stu-id="31185-141">Bots</span></span>

<span data-ttu-id="31185-142">Los bots son la forma más común de agregar funcionalidad a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31185-142">Bots are the most common way to add functionality to your app.</span></span> <span data-ttu-id="31185-143">La muestra hello world ya tiene un bot como parte de la muestra, pero aún no se ha registrado con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="31185-143">The hello world sample already has a bot as part of the sample, but it has not been registered with Microsoft yet.</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="31185-144">El bot que se importó de la muestra aún no tiene asociado un id. de aplicación.</span><span class="sxs-lookup"><span data-stu-id="31185-144">The bot that was imported from the sample does not have an App ID associated with it yet.</span></span> <span data-ttu-id="31185-145">Tendrá que crear un nuevo bot para que App Studio pueda crear un nuevo id. de aplicación y registrarlo con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="31185-145">You will have to create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span> <span data-ttu-id="31185-146">Ten en cuenta que este es el id. de aplicación del bot, que es diferente del id. de aplicación creado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31185-146">Note that this is the App ID for the bot, which is different from the App ID created for the app.</span></span> <span data-ttu-id="31185-147">Cada bot de una aplicación requiere su propio identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="31185-147">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="31185-148">Haga clic *en el botón* Eliminar situado junto al bot *importado* en la lista de bots.</span><span class="sxs-lookup"><span data-stu-id="31185-148">Click the *delete* button next to the *Imported bot* in the bot list.</span></span>

<span data-ttu-id="31185-149">Ahora no quedan bots para mostrar.</span><span class="sxs-lookup"><span data-stu-id="31185-149">Now there are no bots left to show.</span></span> <span data-ttu-id="31185-150">Haga clic *en Instalación.*</span><span class="sxs-lookup"><span data-stu-id="31185-150">Click *Setup*.</span></span> <span data-ttu-id="31185-151">Se mostrará el cuadro *de diálogo Configurar un bot.*</span><span class="sxs-lookup"><span data-stu-id="31185-151">This will display the *Set up a bot* dialog.</span></span>

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

<span data-ttu-id="31185-152">Agregue un nombre de bot como `Contoso bot` , y seleccione los tres botones en **Ámbito**.</span><span class="sxs-lookup"><span data-stu-id="31185-152">Add a bot name such as `Contoso bot`, and select all three buttons under **Scope**.</span></span>

<span data-ttu-id="31185-153">Elija *Crear bot para* salir del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31185-153">Choose *Create bot* to exit the dialog.</span></span> <span data-ttu-id="31185-154">App Studio registra el bot con Microsoft y muestra el nuevo bot en la lista de bots.</span><span class="sxs-lookup"><span data-stu-id="31185-154">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> <span data-ttu-id="31185-155">Ahora sería un buen momento para abrir un archivo de texto en el bloc de notas y copiar y pegar el nuevo identificador de bot en él.</span><span class="sxs-lookup"><span data-stu-id="31185-155">Now would be a good time to open a text file in notepad and copy and paste your new bot id into it.</span></span> <span data-ttu-id="31185-156">Necesitará este identificador más adelante.</span><span class="sxs-lookup"><span data-stu-id="31185-156">You will need this id later.</span></span>

<span data-ttu-id="31185-157">Haga *clic en Generar nueva* contraseña y anote la contraseña en el mismo archivo de texto en el que anotó el id. de la aplicación bot.</span><span class="sxs-lookup"><span data-stu-id="31185-157">Click *Generate New Password*, and make a note of the password in the same text file you noted your Bot app ID in.</span></span> <span data-ttu-id="31185-158">Esta es la única vez que se mostrará la contraseña, así que asegúrate de hacerlo ahora.</span><span class="sxs-lookup"><span data-stu-id="31185-158">This is the only time your password will be shown, so be sure to do this now.</span></span>

<span data-ttu-id="31185-159">Actualice la *dirección del punto de conexión del bot* a , donde debe reemplazarse por la dirección URL que usó anteriormente al hospedar la `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` aplicación.</span><span class="sxs-lookup"><span data-stu-id="31185-159">Update the *Bot endpoint address* to `https://yourteamsapp.ngrok.io/api/messages`, where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

<span data-ttu-id="31185-160">Ahora sería un buen momento para guardar el archivo de texto si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="31185-160">Now would be a good time to save your text file if you have not done so already.</span></span> <span data-ttu-id="31185-161">Agregará esta información a la aplicación hospedada más adelante en este tutorial, lo que permitirá una comunicación segura con el bot.</span><span class="sxs-lookup"><span data-stu-id="31185-161">You will add this information to your hosted app later in this walkthrough, which will allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="31185-162">Extensiones de mensajería</span><span class="sxs-lookup"><span data-stu-id="31185-162">Messaging extensions</span></span>

<span data-ttu-id="31185-163">Las extensiones de mensajería permiten a los usuarios solicitar información de su servicio y publicar esa información, en forma de tarjetas, directamente en la conversación del canal.</span><span class="sxs-lookup"><span data-stu-id="31185-163">Messaging extensions let users ask for information from your service and post that information, in the form of cards, right into the channel conversation.</span></span> <span data-ttu-id="31185-164">Las extensiones de mensajería aparecen en la parte inferior del cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="31185-164">Messaging extensions appear along the bottom of the compose box.</span></span>

<span data-ttu-id="31185-165">Seleccione **Extensiones de mensajería en** **Funcionalidades** de la columna izquierda de App Studio para configurar la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="31185-165">Select **Messaging extensions** under **Capabilities** in the left-hand column of App Studio to configure the messaging extension.</span></span>

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

<span data-ttu-id="31185-166">La extensión de mensajería de ejemplo aparece en el panel derecho en **Extensiones de mensajería.**</span><span class="sxs-lookup"><span data-stu-id="31185-166">The sample messaging extension is listed in the right-hand pane under **Messaging Extensions**.</span></span> <span data-ttu-id="31185-167">Seleccione **Eliminar** de nuevo para quitar  esta entrada y, a continuación, haga clic en el botón Configurar siguiendo los mismos pasos que siguió para los bots.</span><span class="sxs-lookup"><span data-stu-id="31185-167">Select **Delete** again to remove this entry, and then click the *Set up* button following the same steps as you followed for bots.</span></span> <span data-ttu-id="31185-168">Se mostrará el cuadro *de diálogo Extensión de* mensajería.</span><span class="sxs-lookup"><span data-stu-id="31185-168">This will display the *Messaging Extension* dialog.</span></span>

<span data-ttu-id="31185-169">Seleccione la *pestaña Usar bot existente* y, a continuación, seleccione uno de mis *bots existentes.*</span><span class="sxs-lookup"><span data-stu-id="31185-169">Select the *Use existing bot* tab, then *Select from one of my existing bots*.</span></span> <span data-ttu-id="31185-170">En el menú desplegable, seleccione el bot que creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="31185-170">In the drop-down menu, select the bot you created in the section above.</span></span> <span data-ttu-id="31185-171">Agregue un *nombre de bot y* haga clic en *Guardar* para cerrar el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31185-171">Add a *Bot name* and click *Save* to close the dialog.</span></span>

<span data-ttu-id="31185-172">En la *sección Comando,* haga clic *en Agregar*.</span><span class="sxs-lookup"><span data-stu-id="31185-172">Under the *Command* section, click *Add*.</span></span> <span data-ttu-id="31185-173">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span><span class="sxs-lookup"><span data-stu-id="31185-173">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span></span>

<span data-ttu-id="31185-174">En el **cuadro de diálogo Nuevo** comando, escriba los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="31185-174">In the **New command** dialog, enter the following values.</span></span>

<span data-ttu-id="31185-175">En *Nuevo comando:*</span><span class="sxs-lookup"><span data-stu-id="31185-175">Under *New command*:</span></span>

- <span data-ttu-id="31185-176">*Identificador de comando*  = getRandomText</span><span class="sxs-lookup"><span data-stu-id="31185-176">*Command ID*  = getRandomText</span></span>
- <span data-ttu-id="31185-177">*Title*       = Obtener texto aleatorio para la diversión</span><span class="sxs-lookup"><span data-stu-id="31185-177">*Title*       = Get some random text for fun</span></span>
- <span data-ttu-id="31185-178">*Description* = Obtiene texto e imágenes aleatorios</span><span class="sxs-lookup"><span data-stu-id="31185-178">*Description* = Gets some random text and images</span></span>

<span data-ttu-id="31185-179">En *Parámetro*:</span><span class="sxs-lookup"><span data-stu-id="31185-179">Under *Parameter*:</span></span>

- <span data-ttu-id="31185-180">*Name*        = cardTitle</span><span class="sxs-lookup"><span data-stu-id="31185-180">*Name*        = cardTitle</span></span>
- <span data-ttu-id="31185-181">*Título*       = Título de la tarjeta</span><span class="sxs-lookup"><span data-stu-id="31185-181">*Title*       = Card title</span></span>
- <span data-ttu-id="31185-182">*Descripción* = título de la tarjeta que se usará</span><span class="sxs-lookup"><span data-stu-id="31185-182">*Description* = Card title to use</span></span>

<span data-ttu-id="31185-183">Una vez que haya escrito la información, haga clic *en Guardar* para cerrar el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31185-183">Once you're entered the information, click *Save* to close the dialog.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="31185-184">Registrar la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="31185-184">Register your app in Teams</span></span>

<span data-ttu-id="31185-185">Ya has completado la especificación de los detalles de la aplicación, pero quedan los dos pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="31185-185">You have now completed entering the details of your app, but the following two steps remain:</span></span>
1. <span data-ttu-id="31185-186">Use la sección Probar y distribuir de App Studio para instalar la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="31185-186">Use the Test and Distribute section of App Studio to install your app in Teams.</span></span>
1. <span data-ttu-id="31185-187">Actualice la aplicación hospedada con el identificador de aplicación y la contraseña del bot.</span><span class="sxs-lookup"><span data-stu-id="31185-187">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="31185-188">Recuerde que el ejemplo espera usar el mismo id. de aplicación y contraseña tanto para el bot como para la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="31185-188">Remember that the sample expects to use the same App ID and password for both the bot and the messaging extension.</span></span>

<span data-ttu-id="31185-189">Selecciona el **elemento Probar y distribuir en** **Finalizar** en la columna izquierda de App Studio.</span><span class="sxs-lookup"><span data-stu-id="31185-189">Select the **Test and distribute** item under **Finish** in the left-hand column of App Studio.</span></span>

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

<span data-ttu-id="31185-190">Para cargar la aplicación en Teams, haga clic en el botón Instalar en *Probar y distribuir.* </span><span class="sxs-lookup"><span data-stu-id="31185-190">In order to upload your app to Teams, click the *Install* button under *Test and Distribute*.</span></span>

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

<span data-ttu-id="31185-191">Seleccione el **cuadro** de búsqueda en la sección Agregar **a un** equipo y seleccione un equipo al que agregar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="31185-191">Select the **Search** box in the **Add to a team** section and select a team to add the sample app to.</span></span> <span data-ttu-id="31185-192">Por lo general, puede configurar un equipo especial para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="31185-192">Usually, you can set up a special team for testing.</span></span>

<span data-ttu-id="31185-193">Seleccione el **botón** Instalar en la parte inferior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31185-193">Select the **Install** button at the bottom of the dialog.</span></span>

<span data-ttu-id="31185-194">Esto finaliza la parte de App Studio de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="31185-194">This finishes the App Studio portion of this walkthrough.</span></span> <span data-ttu-id="31185-195">Ahora debería ver que la aplicación se ejecuta en Teams, pero el bot y la extensión de mensajería no funcionarán hasta que actualice el entorno de aplicaciones hospedadas para saber cuáles son los IDs y las contraseñas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31185-195">You should now see your app running in Teams, however, the bot and the messaging extension will not work until you update the hosted applications environment to know what the App IDs and passwords are.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
