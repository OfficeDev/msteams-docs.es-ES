## <a name="prerequisites"></a><span data-ttu-id="98a47-101">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="98a47-101">Prerequisites</span></span>

- <span data-ttu-id="98a47-102">Para completar este tutorial, necesitará un inquilino de Office 365 y un equipo configurado con la *opción permitir la carga de aplicaciones personalizadas* habilitada.</span><span class="sxs-lookup"><span data-stu-id="98a47-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="98a47-103">Para obtener más información, vea [preparar el inquilino de Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="98a47-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="98a47-104">Si actualmente no tiene una cuenta de Office 365, puede registrarse para obtener una suscripción gratuita a través del programa de desarrolladores de Office 365.</span><span class="sxs-lookup"><span data-stu-id="98a47-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="98a47-105">La suscripción permanecerá activa siempre que la use para el desarrollo continuado.</span><span class="sxs-lookup"><span data-stu-id="98a47-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="98a47-106">Vea [Bienvenido al programa de desarrolladores de Office 365](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md).</span><span class="sxs-lookup"><span data-stu-id="98a47-106">See [Welcome to the Office 365 Developer Program](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md).</span></span>

<span data-ttu-id="98a47-107">Además, este proyecto requiere que tenga instalado lo siguiente en el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="98a47-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="98a47-108">Cualquier editor de texto o IDE.</span><span class="sxs-lookup"><span data-stu-id="98a47-108">Any text editor or IDE.</span></span> <span data-ttu-id="98a47-109">Puede instalar y usar [Visual Studio Code](https://code.visualstudio.com/download) de forma gratuita.</span><span class="sxs-lookup"><span data-stu-id="98a47-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="98a47-110">[Node. js/NPM](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="98a47-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="98a47-111">Debe usar la última versión de LTS.</span><span class="sxs-lookup"><span data-stu-id="98a47-111">You should use the latest LTS version.</span></span> <span data-ttu-id="98a47-112">El administrador de paquetes de nodos (NPM) se instalará en el sistema con la instalación de node. js.</span><span class="sxs-lookup"><span data-stu-id="98a47-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="98a47-113">Después de instalar correctamente node. js, instale los paquetes [Yeoman](https://yeoman.io/) y [Gulp-CLI](https://www.npmjs.com/package/gulp-cli) escribiendo lo siguiente en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="98a47-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

```bash
npm install yo gulp-cli --global
```

- <span data-ttu-id="98a47-114">Para instalar el generador de aplicaciones de Microsoft Teams, escriba lo siguiente en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="98a47-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a><span data-ttu-id="98a47-115">Generar el proyecto</span><span class="sxs-lookup"><span data-stu-id="98a47-115">Generate your project</span></span>

- <span data-ttu-id="98a47-116">Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestañas.</span><span class="sxs-lookup"><span data-stu-id="98a47-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="98a47-117">Para iniciar el generador, navegue hasta el nuevo directorio y escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="98a47-117">To start the generator, navigate to your new directory and type the following command:</span></span>

```bash
yo teams
```

- <span data-ttu-id="98a47-118">A continuación, deberá proporcionar una serie de valores que se usarán en el archivo **manifest. JSON** de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="98a47-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

![captura de pantalla de apertura del generador](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

<span data-ttu-id="98a47-120">**¿Cuál es el nombre de la solución?**</span><span class="sxs-lookup"><span data-stu-id="98a47-120">**What is your solution name?**</span></span>

<span data-ttu-id="98a47-121">Este es el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="98a47-121">This is your project name.</span></span> <span data-ttu-id="98a47-122">Puede aceptar el nombre sugerido; para ello, presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="98a47-122">You can accept the suggested name by pressing enter.</span></span>

<span data-ttu-id="98a47-123">**¿Dónde desea ubicar los archivos?**</span><span class="sxs-lookup"><span data-stu-id="98a47-123">**Where do you want to place the files?**</span></span>

<span data-ttu-id="98a47-124">Actualmente está en el directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="98a47-124">You're currently in your project directory.</span></span> <span data-ttu-id="98a47-125">Presione entrar.</span><span class="sxs-lookup"><span data-stu-id="98a47-125">Press enter.</span></span>

<span data-ttu-id="98a47-126">**¿El título del proyecto de la aplicación de Microsoft Teams?**</span><span class="sxs-lookup"><span data-stu-id="98a47-126">**Title of your Microsoft Teams app project?**</span></span>

<span data-ttu-id="98a47-127">Este es el nombre del paquete de la aplicación y se usará en el manifiesto de la aplicación y la descripción.</span><span class="sxs-lookup"><span data-stu-id="98a47-127">This is your app package name and will be used in the app manifest and description.</span></span>

<span data-ttu-id="98a47-128">**El nombre de la (empresa)? (máximo 32 caracteres)**</span><span class="sxs-lookup"><span data-stu-id="98a47-128">**Your (company) name? (max 32 characters)**</span></span>

<span data-ttu-id="98a47-129">El nombre de la compañía se usará en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="98a47-129">Your company name will be used in the app manifest.</span></span>

<br><span data-ttu-id="98a47-130">**¿Qué versión de manifiesto desearía usar?**</span><span class="sxs-lookup"><span data-stu-id="98a47-130">**Which manifest version would you like to use?**</span></span>

<span data-ttu-id="98a47-131">Seleccione el esquema predeterminado.</span><span class="sxs-lookup"><span data-stu-id="98a47-131">Select the default schema.</span></span>

<span data-ttu-id="98a47-132">**Escriba su identificador de socio de Microsoft, si tiene uno? (Déjelo en blanco para omitir)**</span><span class="sxs-lookup"><span data-stu-id="98a47-132">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

<span data-ttu-id="98a47-133">Este campo no es necesario y solo debe usarse si ya forma parte de la [red de asociados de Microsoft](https://partner.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="98a47-133">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

<span data-ttu-id="98a47-134">**¿Qué desea agregar al proyecto?**</span><span class="sxs-lookup"><span data-stu-id="98a47-134">**What do you want to add to your project?**</span></span>

<span data-ttu-id="98a47-135">Seleccione ( &ast; ) una tabulación.</span><span class="sxs-lookup"><span data-stu-id="98a47-135">Select ( &ast; ) A Tab.</span></span>

<span data-ttu-id="98a47-136">**La dirección URL en la que va a hospedar esta solución?**</span><span class="sxs-lookup"><span data-stu-id="98a47-136">**The URL where you will host this solution?**</span></span>

<span data-ttu-id="98a47-137">De forma predeterminada, el generador sugiere una dirección URL de sitios web de Azure.</span><span class="sxs-lookup"><span data-stu-id="98a47-137">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="98a47-138">Solo va a probar la aplicación de forma local, por lo tanto, no es necesaria una dirección URL válida para completar este inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="98a47-138">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

<span data-ttu-id="98a47-139">**¿Le gustaría incluir el marco de pruebas y las pruebas iniciales? (s/N)**</span><span class="sxs-lookup"><span data-stu-id="98a47-139">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

<span data-ttu-id="98a47-140">Elija **no** incluir un marco de pruebas para este proyecto.</span><span class="sxs-lookup"><span data-stu-id="98a47-140">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="98a47-141">El valor predeterminado es sí; Escriba **n**.</span><span class="sxs-lookup"><span data-stu-id="98a47-141">The default is yes; enter **n**.</span></span>

<span data-ttu-id="98a47-142">**¿Desea usar las aplicaciones de Azure Insights para telemetría? (s/N)**</span><span class="sxs-lookup"><span data-stu-id="98a47-142">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

<span data-ttu-id="98a47-143">Elija **no** incluir [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98a47-143">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="98a47-144">El valor predeterminado es no; Escriba **n**.</span><span class="sxs-lookup"><span data-stu-id="98a47-144">The default is no; enter **n**.</span></span>

<span data-ttu-id="98a47-145">**Nombre de pestaña predeterminado (16 caracteres como máximo)?**</span><span class="sxs-lookup"><span data-stu-id="98a47-145">**Default Tab Name (max 16 characters)?**</span></span>

<span data-ttu-id="98a47-146">Asigne un nombre a la pestaña. Este nombre de la pestaña se usará en el proyecto como un componente de ruta de acceso de archivo o dirección URL.</span><span class="sxs-lookup"><span data-stu-id="98a47-146">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
