## <a name="prerequisites"></a><span data-ttu-id="a33af-101">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a33af-101">Prerequisites</span></span>

- <span data-ttu-id="a33af-102">Para completar esta iniciación rápida necesitará un inquilino Office 365 y un equipo configurado con *Permitir cargar aplicaciones personalizadas* habilitadas.</span><span class="sxs-lookup"><span data-stu-id="a33af-102">To complete this quickstart you will need an Office 365 tenant and a team configured with *Allow uploading custom apps* enabled.</span></span> <span data-ttu-id="a33af-103">Para obtener más información, consulte [Preparar el inquilino de Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="a33af-103">To learn more, see [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

  - <span data-ttu-id="a33af-104">Si actualmente no tiene una cuenta de Office 365, puede registrarse para obtener una suscripción gratuita a través del Programa de desarrollador Office 365.</span><span class="sxs-lookup"><span data-stu-id="a33af-104">If you don't currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="a33af-105">La suscripción permanecerá activa mientras la use para el desarrollo continuo.</span><span class="sxs-lookup"><span data-stu-id="a33af-105">The subscription will remain active as long as you're using it for ongoing development.</span></span> <span data-ttu-id="a33af-106">Consulte [Bienvenido al Programa para desarrolladores de Office 365](/office/developer-program/microsoft-365-developer-program).</span><span class="sxs-lookup"><span data-stu-id="a33af-106">See [Welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="a33af-107">Además, este proyecto requiere que tenga instalado lo siguiente en el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="a33af-107">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="a33af-108">Cualquier editor de texto o IDE.</span><span class="sxs-lookup"><span data-stu-id="a33af-108">Any text editor or IDE.</span></span> <span data-ttu-id="a33af-109">Puede instalar y utilizar [Visual Studio Code](https://code.visualstudio.com/download) de forma gratuita.</span><span class="sxs-lookup"><span data-stu-id="a33af-109">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="a33af-110">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="a33af-110">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="a33af-111">Debe utilizar la versión lts más reciente.</span><span class="sxs-lookup"><span data-stu-id="a33af-111">You should use the latest LTS version.</span></span> <span data-ttu-id="a33af-112">El nodo Administrador de paquetes (npm) se instalará en el sistema con la instalación de Node.js.</span><span class="sxs-lookup"><span data-stu-id="a33af-112">The Node Package Manager (npm) will install into your system with the installation of Node.js.</span></span>

- <span data-ttu-id="a33af-113">Después de instalar correctamente Node.js, instale los paquetes [Yeoman](https://yeoman.io/) y [gulp-cli](https://www.npmjs.com/package/gulp-cli) escribiendo lo siguiente en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="a33af-113">After you've successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by typing the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="a33af-114">Instale el generador de aplicaciones de Microsoft Teams escribiendo lo siguiente en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="a33af-114">Install the Microsoft Teams Apps generator by typing the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

## <a name="generate-your-project"></a><span data-ttu-id="a33af-115">Generar su proyecto</span><span class="sxs-lookup"><span data-stu-id="a33af-115">Generate your project</span></span>

- <span data-ttu-id="a33af-116">Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestaña.</span><span class="sxs-lookup"><span data-stu-id="a33af-116">Open a command prompt and create a new directory for your tab project.</span></span>

- <span data-ttu-id="a33af-117">Para iniciar el generador, vaya al nuevo directorio y escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a33af-117">To start the generator, navigate to your new directory and type the following command:</span></span>

    ```bash
    yo teams
    ```

- <span data-ttu-id="a33af-118">A continuación, proporcionará una serie de valores que se usarán en **lamanifest.js** de archivo de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="a33af-118">Next, you'll provide a series of values that will be used in your application's **manifest.json** file:</span></span>

    ![captura de pantalla de apertura del generador](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="a33af-120">**¿Cómo se llama su solución?**</span><span class="sxs-lookup"><span data-stu-id="a33af-120">**What is your solution name?**</span></span>

    <span data-ttu-id="a33af-121">Este es el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="a33af-121">This is your project name.</span></span> <span data-ttu-id="a33af-122">Puede aceptar el nombre sugerido pulsando Intro.</span><span class="sxs-lookup"><span data-stu-id="a33af-122">You can accept the suggested name by pressing enter.</span></span>

    <span data-ttu-id="a33af-123">**¿Dónde desea ubicar los archivos?**</span><span class="sxs-lookup"><span data-stu-id="a33af-123">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="a33af-124">Actualmente se encuentra en el directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="a33af-124">You're currently in your project directory.</span></span> <span data-ttu-id="a33af-125">Pulse Intro.</span><span class="sxs-lookup"><span data-stu-id="a33af-125">Press enter.</span></span>

    <span data-ttu-id="a33af-126">**¿El título del proyecto de la aplicación Microsoft Teams?**</span><span class="sxs-lookup"><span data-stu-id="a33af-126">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="a33af-127">Este es el nombre del paquete de la aplicación y se usará en el manifiesto y la descripción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a33af-127">This is your app package name and will be used in the app manifest and description.</span></span>

    <span data-ttu-id="a33af-128">**¿Su nombre (de la compañía)? (máximo 32 caracteres)**</span><span class="sxs-lookup"><span data-stu-id="a33af-128">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="a33af-129">El nombre de su empresa se usará en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a33af-129">Your company name will be used in the app manifest.</span></span>

    <span data-ttu-id="a33af-130">**¿Qué versión de manifiesto le gustaría usar?**</span><span class="sxs-lookup"><span data-stu-id="a33af-130">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="a33af-131">Seleccione el esquema predeterminado.</span><span class="sxs-lookup"><span data-stu-id="a33af-131">Select the default schema.</span></span>

    <span data-ttu-id="a33af-132">**¿Andamios rápidos? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="a33af-132">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="a33af-133">El valor predeterminado es sí; **escriba n** para introducir el Identificador de socio de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a33af-133">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="a33af-134">**Escriba su Id de socio de Microsoft, si tiene uno? (Deje en blanco para omitir)**</span><span class="sxs-lookup"><span data-stu-id="a33af-134">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="a33af-135">Este campo no es obligatorio y solo se debe usar si ya forma parte de [Microsoft Partner Network.](https://partner.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="a33af-135">This field isn't required and should only be used if you're already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="a33af-136">**¿Qué desea agregar a su proyecto?**</span><span class="sxs-lookup"><span data-stu-id="a33af-136">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="a33af-137">Seleccione ( &ast; ) Una pestaña.</span><span class="sxs-lookup"><span data-stu-id="a33af-137">Select ( &ast; ) A Tab.</span></span>

    <span data-ttu-id="a33af-138">**¿La dirección URL donde hospedará esta solución?**</span><span class="sxs-lookup"><span data-stu-id="a33af-138">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="a33af-139">De forma predeterminada, el generador sugiere una dirección URL de sitios Web de Azure.</span><span class="sxs-lookup"><span data-stu-id="a33af-139">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="a33af-140">Solo probará la aplicación localmente, por lo tanto, no es necesaria una dirección URL válida para completar esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="a33af-140">You'll only be testing your app locally, therefore, a valid URL is not necessary to complete this quickstart.</span></span>

    <span data-ttu-id="a33af-141">**¿Desea incluir el marco de trabajo de prueba y las pruebas iniciales? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="a33af-141">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="a33af-142">Elija **no** incluir un marco de trabajo de prueba para este proyecto.</span><span class="sxs-lookup"><span data-stu-id="a33af-142">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="a33af-143">El valor predeterminado es sí; entrar **n**.</span><span class="sxs-lookup"><span data-stu-id="a33af-143">The default is yes; enter **n**.</span></span>

    <span data-ttu-id="a33af-144">**¿Desea usar Azure Applications Insights para telemetría? (y/N)**</span><span class="sxs-lookup"><span data-stu-id="a33af-144">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="a33af-145">Elija **no** incluir [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a33af-145">Choose **not** to include [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md).</span></span> <span data-ttu-id="a33af-146">El valor predeterminado es no; entrar **n**.</span><span class="sxs-lookup"><span data-stu-id="a33af-146">The default is no; enter **n**.</span></span>

    <span data-ttu-id="a33af-147">**¿Nombre de tabulación predeterminado (máx. 16 caracteres)?**</span><span class="sxs-lookup"><span data-stu-id="a33af-147">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="a33af-148">Nombra tu pestaña. Este nombre de pestaña se utilizará en todo el proyecto como un componente de ruta de acceso de archivo/URL.</span><span class="sxs-lookup"><span data-stu-id="a33af-148">Name your tab. This tab name will be used throughout your project as a file/URL path component.</span></span>
