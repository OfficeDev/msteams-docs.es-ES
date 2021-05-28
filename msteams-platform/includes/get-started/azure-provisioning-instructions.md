## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="dbba1-101">Implementar la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="dbba1-101">Deploy your app to Azure</span></span>

<span data-ttu-id="dbba1-102">La implementación consta de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="dbba1-102">Deployment consists of two steps.</span></span>  <span data-ttu-id="dbba1-103">En primer lugar, se crean los recursos en la nube necesarios (también conocidos como aprovisionamiento) y, a continuación, el código que forma la aplicación se copia en los recursos de nube creados.</span><span class="sxs-lookup"><span data-stu-id="dbba1-103">First, necessary cloud resources are created (also known as provisioning), then the code that makes up your app is copied into the created cloud resources.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="dbba1-104">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="dbba1-104">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="dbba1-105">Abra Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dbba1-105">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="dbba1-106">Seleccione el Teams Toolkit de la barra lateral seleccionando el Teams.</span><span class="sxs-lookup"><span data-stu-id="dbba1-106">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="dbba1-107">Seleccione **Aprovisionar en la nube**.</span><span class="sxs-lookup"><span data-stu-id="dbba1-107">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Captura de pantalla que muestra los comandos de aprovisionamiento":::

1. <span data-ttu-id="dbba1-109">Si es necesario, seleccione una suscripción para usar para los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbba1-109">If required, select a subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dbba1-110">Siempre hay algunos recursos de Azure usados para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dbba1-110">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="dbba1-111">Un cuadro de diálogo le advierte de que pueden producirse costos al ejecutar recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="dbba1-111">A dialog warns you that costs may be incurred when running resources in Azure.</span></span>  <span data-ttu-id="dbba1-112">Presione **Aprovisionar**.</span><span class="sxs-lookup"><span data-stu-id="dbba1-112">Press **Provision**.</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-warning.png" alt-text="Captura de pantalla del cuadro de diálogo de aprovisionamiento.":::

   <span data-ttu-id="dbba1-114">El proceso de aprovisionamiento creará recursos en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbba1-114">The provisioning process will create resources in the Azure cloud.</span></span>  <span data-ttu-id="dbba1-115">Esto llevará algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="dbba1-115">This will take some time.</span></span>  <span data-ttu-id="dbba1-116">Puede supervisar el progreso viendo los cuadros de diálogo en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="dbba1-116">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="dbba1-117">Después de unos minutos, verá el siguiente aviso:</span><span class="sxs-lookup"><span data-stu-id="dbba1-117">After a few minutes, you will see the following notice:</span></span>

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Captura de pantalla que muestra el cuadro de diálogo completado de aprovisionamiento.":::

1. <span data-ttu-id="dbba1-119">Una vez completado el aprovisionamiento, seleccione **Implementar en la nube.**</span><span class="sxs-lookup"><span data-stu-id="dbba1-119">Once provisioning is complete, select **Deploy to the Cloud**.</span></span>  <span data-ttu-id="dbba1-120">Al igual que con el aprovisionamiento, este proceso tarda algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="dbba1-120">As with provisioning, this process takes some time.</span></span>  <span data-ttu-id="dbba1-121">Puede supervisar el proceso viendo los cuadros de diálogo en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="dbba1-121">You can monitor the process by watching the dialogs in the bottom right corner.</span></span> <span data-ttu-id="dbba1-122">Después de unos minutos, verá un aviso de finalización.</span><span class="sxs-lookup"><span data-stu-id="dbba1-122">After a few minutes, you will see a completion notice.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="dbba1-123">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="dbba1-123">Command Line</span></span>](#tab/cli)

<span data-ttu-id="dbba1-124">En la ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="dbba1-124">In your terminal window:</span></span>

1. <span data-ttu-id="dbba1-125">Ejecute `teamsfx provision`.</span><span class="sxs-lookup"><span data-stu-id="dbba1-125">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="dbba1-126">Es posible que se le pida que inicie sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbba1-126">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="dbba1-127">Si es necesario, se le pedirá que seleccione una suscripción de Azure que se usará para los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbba1-127">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dbba1-128">Siempre hay algunos recursos de Azure usados para hospedar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dbba1-128">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="dbba1-129">Ejecute `teamsfx deploy`.</span><span class="sxs-lookup"><span data-stu-id="dbba1-129">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> <span data-ttu-id="dbba1-130">**¿Cuál es la diferencia entre Aprovisionar e Implementar?**</span><span class="sxs-lookup"><span data-stu-id="dbba1-130">**What's the difference between Provision and Deploy?**</span></span>
>
> <span data-ttu-id="dbba1-131">El **paso Aprovisionar** creará recursos en Azure y M365 para la aplicación, pero no se copia ningún código (HTML, CSS, JavaScript, etc.) en los recursos.</span><span class="sxs-lookup"><span data-stu-id="dbba1-131">The **Provision** step will create resources in Azure and M365 for your app, but no code (HTML, CSS, JavaScript, etc.) is copied to the resources.</span></span>  <span data-ttu-id="dbba1-132">El **paso** Implementar copiará el código de la aplicación en los recursos que creaste durante el paso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="dbba1-132">The **Deploy** step will copy the code for your app to the resources you created during the provision step.</span></span>  <span data-ttu-id="dbba1-133">Es común implementar varias veces sin aprovisionar nuevos recursos.</span><span class="sxs-lookup"><span data-stu-id="dbba1-133">It is common to deploy multiple times without provisioning new resources.</span></span> <span data-ttu-id="dbba1-134">Dado que el paso de aprovisionamiento puede tardar algún tiempo en completarse, es independiente del paso de implementación.</span><span class="sxs-lookup"><span data-stu-id="dbba1-134">Since the provision step can take some time to complete, it is separate from the deployment step.</span></span>

<span data-ttu-id="dbba1-135">Una vez finalizados los pasos de aprovisionamiento e implementación:</span><span class="sxs-lookup"><span data-stu-id="dbba1-135">Once the provisioning and deployment steps are finished:</span></span>

1. <span data-ttu-id="dbba1-136">Desde Visual Studio Code, abra el panel de depuración (**Ctrl+Mayús+D**  /  **.⇧-D** o **Ver > Ejecutar**)</span><span class="sxs-lookup"><span data-stu-id="dbba1-136">From Visual Studio Code, open the debug panel (**Ctrl+Shift+D** / **⌘⇧-D** or **View > Run**)</span></span>
1. <span data-ttu-id="dbba1-137">Seleccione **Iniciar remoto (perimetral)** en la lista desplegable configuración de inicio.</span><span class="sxs-lookup"><span data-stu-id="dbba1-137">Select **Launch Remote (Edge)** from the launch configuration drop-down.</span></span>
1. <span data-ttu-id="dbba1-138">Presione el botón Reproducir para iniciar la aplicación: ahora se ejecuta de forma remota desde Azure.</span><span class="sxs-lookup"><span data-stu-id="dbba1-138">Press the Play button to launch your app - now running remotely from Azure!</span></span>
