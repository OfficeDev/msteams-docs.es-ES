## <a name="prerequisites"></a><span data-ttu-id="19207-101">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="19207-101">Prerequisites</span></span>

- <span data-ttu-id="19207-102">Para completar esta guía de inicio rápido, necesitará un inquilino Office 365 y un equipo configurado con *Permitir cargar aplicaciones personalizadas* habilitadas.</span><span class="sxs-lookup"><span data-stu-id="19207-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="19207-103">Para obtener más información, vea [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="19207-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="19207-104">Si actualmente no tiene una cuenta Office 365, puede registrarse para obtener una suscripción gratuita a través del programa Office 365 desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="19207-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="19207-105">La suscripción permanecerá activa mientras la estés usando para el desarrollo continuo.</span><span class="sxs-lookup"><span data-stu-id="19207-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="19207-106">Vea [Welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span><span class="sxs-lookup"><span data-stu-id="19207-106">See [Welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="19207-107">Además, este proyecto requiere que tenga lo siguiente instalado en el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="19207-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="19207-108">Cualquier editor de texto o IDE.</span><span class="sxs-lookup"><span data-stu-id="19207-108">Any text editor or IDE.</span></span> <span data-ttu-id="19207-109">Puede instalar y [usar](https://code.visualstudio.com/download) Visual Studio Code de forma gratuita.</span><span class="sxs-lookup"><span data-stu-id="19207-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="19207-110">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="19207-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="19207-111">Debe usar la versión lts más reciente.</span><span class="sxs-lookup"><span data-stu-id="19207-111">You should use the latest LTS version.</span></span> <span data-ttu-id="19207-112">El nodo Administrador de paquetes (npm) se instalará en el sistema con la instalación de Node.js.</span><span class="sxs-lookup"><span data-stu-id="19207-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="19207-113">Después de instalar correctamente Node.js, instale los paquetes [Yeoman](https://yeoman.io/) y [gulp-cli](https://www.npmjs.com/package/gulp-cli) escribiendo lo siguiente en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="19207-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="19207-114">Instale el generador Microsoft Teams aplicaciones escribiendo lo siguiente en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="19207-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

## <a name="generate-your-project"></a><span data-ttu-id="19207-115">Generar el proyecto</span><span class="sxs-lookup"><span data-stu-id="19207-115">Generate your project</span></span>

- <span data-ttu-id="19207-116">Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestaña.</span><span class="sxs-lookup"><span data-stu-id="19207-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="19207-117">Para iniciar el generador, vaya al nuevo directorio y escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="19207-117">To start the generator, navigate to your new directory and type the following command:</span></span>

    ```bash
    yo teams
    ```

- <span data-ttu-id="19207-118">A continuación, proporcionará una serie de valores que se usarán en el archivo demanifest.js **aplicación:**</span><span class="sxs-lookup"><span data-stu-id="19207-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

    ![captura de pantalla de apertura del generador](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="19207-120">**¿Cuál es el nombre de la solución?**</span><span class="sxs-lookup"><span data-stu-id="19207-120">**What is your solution name?**</span></span>

    <span data-ttu-id="19207-121">Este es el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="19207-121">This is your project name.</span></span> <span data-ttu-id="19207-122">Puede aceptar el nombre sugerido presionando entrar.</span><span class="sxs-lookup"><span data-stu-id="19207-122">You can accept the suggested name by pressing enter.</span></span>

    <span data-ttu-id="19207-123">**¿Dónde desea ubicar los archivos?**</span><span class="sxs-lookup"><span data-stu-id="19207-123">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="19207-124">Actualmente está en el directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="19207-124">You're currently in your project directory.</span></span> <span data-ttu-id="19207-125">Presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="19207-125">Press enter.</span></span>

    <span data-ttu-id="19207-126">**¿Título de tu Microsoft Teams de aplicación?**</span><span class="sxs-lookup"><span data-stu-id="19207-126">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="19207-127">Este es el nombre del paquete de la aplicación y se usará en el manifiesto y la descripción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="19207-127">This is your app package name and will be used in the app manifest and description.</span></span>

    <span data-ttu-id="19207-128">**¿Su nombre (empresa)? (máximo 32 caracteres)**</span><span class="sxs-lookup"><span data-stu-id="19207-128">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="19207-129">El nombre de la empresa se usará en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="19207-129">Your company name will be used in the app manifest.</span></span>

    <span data-ttu-id="19207-130">**¿Qué versión de manifiesto le gustaría usar?**</span><span class="sxs-lookup"><span data-stu-id="19207-130">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="19207-131">Seleccione el esquema predeterminado.</span><span class="sxs-lookup"><span data-stu-id="19207-131">Select the default schema.</span></span>

    <span data-ttu-id="19207-132">**¿Scaffolding rápido? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="19207-132">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="19207-133">El valor predeterminado es sí; escriba **n** para escribir su Id. de partner de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19207-133">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="19207-134">**Escriba su id. de partner de Microsoft, si tiene uno. (Dejar en blanco para omitir)**</span><span class="sxs-lookup"><span data-stu-id="19207-134">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="19207-135">Este campo no es obligatorio y solo debe usarse si ya forma parte de [la red de partners de Microsoft](https://partner.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="19207-135">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="19207-136">**¿Qué desea agregar al proyecto?**</span><span class="sxs-lookup"><span data-stu-id="19207-136">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="19207-137">Seleccione ( &ast; ) Una pestaña.</span><span class="sxs-lookup"><span data-stu-id="19207-137">Select ( &ast; ) A Tab.</span></span>

    <span data-ttu-id="19207-138">**¿La dirección URL donde hospedará esta solución?**</span><span class="sxs-lookup"><span data-stu-id="19207-138">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="19207-139">De forma predeterminada, el generador sugiere una dirección URL de Sitios web de Azure.</span><span class="sxs-lookup"><span data-stu-id="19207-139">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="19207-140">Solo probarás tu aplicación localmente, por lo tanto, no es necesaria una dirección URL válida para completar esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="19207-140">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

    <span data-ttu-id="19207-141">**¿Desea incluir el marco de pruebas y las pruebas iniciales? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="19207-141">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="19207-142">Elija **no incluir** un marco de prueba para este proyecto.</span><span class="sxs-lookup"><span data-stu-id="19207-142">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="19207-143">El valor predeterminado es sí; escriba **n**.</span><span class="sxs-lookup"><span data-stu-id="19207-143">The default is yes; enter **n**.</span></span>

    <span data-ttu-id="19207-144">**¿Desea usar Azure Applications Insights para telemetría? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="19207-144">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="19207-145">Elija **no incluir** Azure Application [Insights](/azure/azure-monitor/app/app-insights-overview).</span><span class="sxs-lookup"><span data-stu-id="19207-145">Choose **not** to include [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview).</span></span> <span data-ttu-id="19207-146">El valor predeterminado es no; escriba **n**.</span><span class="sxs-lookup"><span data-stu-id="19207-146">The default is no; enter **n**.</span></span>

    <span data-ttu-id="19207-147">**Nombre de tabulación predeterminado (máximo 16 caracteres)?**</span><span class="sxs-lookup"><span data-stu-id="19207-147">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="19207-148">Asigne un nombre a la pestaña. Este nombre de pestaña se usará en todo el proyecto como un componente de ruta de acceso de archivo/dirección URL.</span><span class="sxs-lookup"><span data-stu-id="19207-148">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
