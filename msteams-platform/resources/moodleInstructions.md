---
title: Instalar Moodle LMS
description: Cómo instalar y configurar la aplicación de integración de Moodle para Microsoft Teams
keywords: Teams Complementos de integración de aplicaciones de Moodle
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 54f4fec4e240f866c686ed715bd5093a319a2a48
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069172"
---
# <a name="install-moodle-lms"></a><span data-ttu-id="919b0-104">Instalar Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="919b0-104">Install Moodle LMS</span></span>

<span data-ttu-id="919b0-105">En este artículo aprenderá a instalar el LMS de Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-105">In this article you'll learn how to install the Moodle LMS.</span></span>

> [!NOTE]
> <span data-ttu-id="919b0-106">Para ayudar a los administradores de TI a configurar fácilmente La integración de Moodle y Teams, los complementos de código Microsoft 365 de Moodle se actualizan para lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="919b0-106">To help IT admins to easily set-up Moodle and Teams integration, open-source Microsoft 365 Moodle Plugins is updated for the following:</span></span>
>
> * <span data-ttu-id="919b0-107">Registro automático del servidor de Moodle [con Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="919b0-107">Auto-registration of your Moodle server with [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).</span></span>
>
> * <span data-ttu-id="919b0-108">Implementación con un solo clic del bot asistente de Moodle en Azure.</span><span class="sxs-lookup"><span data-stu-id="919b0-108">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
>
> * <span data-ttu-id="919b0-109">Aprovisionamiento automático de equipos y sincronización automática de las inscripciones de equipo para todos o seleccionar cursos de Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-109">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
>
> * <span data-ttu-id="919b0-110">Instalación automática de la pestaña Moodle y el bot asistente de Moodle en cada equipo sincronizado.</span><span class="sxs-lookup"><span data-stu-id="919b0-110">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>
>
> <span data-ttu-id="919b0-111">Para obtener más información sobre la funcionalidad que proporciona esta integración, vea [Microsoft Teams y Moodle](https://education.microsoft.com/resource/3dffb3a8).</span><span class="sxs-lookup"><span data-stu-id="919b0-111">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="919b0-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="919b0-112">Prerequisites</span></span>

<span data-ttu-id="919b0-113">Estos son los requisitos previos para instalar Moodle:</span><span class="sxs-lookup"><span data-stu-id="919b0-113">Following are the prerequisites to install Moodle:</span></span>

* <span data-ttu-id="919b0-114">Credenciales de administrador de Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-114">Moodle administrator credentials.</span></span>

* <span data-ttu-id="919b0-115">Credenciales de administrador de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919b0-115">Azure AD administrator credentials.</span></span>

* <span data-ttu-id="919b0-116">Una suscripción de Azure en la que puede crear nuevos recursos.</span><span class="sxs-lookup"><span data-stu-id="919b0-116">An Azure subscription where you can create new resources.</span></span>

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="919b0-117">1. Instalar el Microsoft 365 Complementos de Moodle</span><span class="sxs-lookup"><span data-stu-id="919b0-117">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="919b0-118">La integración de Moodle en Microsoft Teams funciona con la tecnología de código Microsoft 365 conjunto de [complementos de Moodle](https://github.com/Microsoft/o365-moodle).</span><span class="sxs-lookup"><span data-stu-id="919b0-118">Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugins set](https://github.com/Microsoft/o365-moodle).</span></span>

### <a name="requisite-applications-and-plugins"></a><span data-ttu-id="919b0-119">Aplicaciones y complementos necesarios</span><span class="sxs-lookup"><span data-stu-id="919b0-119">Requisite applications and plugins</span></span>

<span data-ttu-id="919b0-120">Asegúrese de instalar y descargar lo siguiente antes de continuar con la instalación Microsoft 365 complementos de Moodle:</span><span class="sxs-lookup"><span data-stu-id="919b0-120">Ensure to install and download the following before proceeding with the Microsoft 365 Moodle plugins installation:</span></span>

1. <span data-ttu-id="919b0-121">Asegúrese de instalar una [versión estable actual de Moodle](https://download.moodle.org/releases/latest/).</span><span class="sxs-lookup"><span data-stu-id="919b0-121">Ensure to install a [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="919b0-122">Descargue y guarde los complementos de [integración de Conectar](https://moodle.org/plugins/auth_oidc) y Microsoft 365 [de Integración](https://moodle.org/plugins/local_o365) de Moodle en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="919b0-122">Download and save the Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins to your local computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="919b0-123">La instalación de los Conectar OpenID y Microsoft 365 integration son necesarias para la Teams integración.</span><span class="sxs-lookup"><span data-stu-id="919b0-123">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span>
    >
    > <span data-ttu-id="919b0-124">Además, los complementos [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) son muy recomendables.</span><span class="sxs-lookup"><span data-stu-id="919b0-124">In addition, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugins is highly recommended.</span></span>

### <a name="microsoft-365-moodle-plugins"></a><span data-ttu-id="919b0-125">Microsoft 365 Complementos de Moodle</span><span class="sxs-lookup"><span data-stu-id="919b0-125">Microsoft 365 Moodle plugins</span></span>

1. <span data-ttu-id="919b0-126">Inicie sesión en el servidor de  Moodle como administrador y seleccione Administración del sitio en el bloque [Configuración](https://docs.moodle.org/22/en/Settings_block) ubicado en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="919b0-126">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="919b0-127">Selecciona la **pestaña Complementos** y, a continuación, selecciona **Instalar complementos.**</span><span class="sxs-lookup"><span data-stu-id="919b0-127">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="919b0-128">En la **sección Instalar complementos desde archivo ZIP,** seleccione Elegir un **archivo**.</span><span class="sxs-lookup"><span data-stu-id="919b0-128">From the **Install plugins from ZIP file** section, select **Choose a file**.</span></span>

1. <span data-ttu-id="919b0-129">Seleccione **Upload una opción de** archivo en el panel de navegación izquierdo, busque el archivo que descargó y seleccione Upload este **archivo**.</span><span class="sxs-lookup"><span data-stu-id="919b0-129">Select **Upload a file** option from the left navigation panel, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="919b0-130">Seleccione **Administración del sitio** en el panel de navegación izquierdo para volver al panel de administración.</span><span class="sxs-lookup"><span data-stu-id="919b0-130">Select **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="919b0-131">Desplácese hacia abajo hasta **los complementos locales** y seleccione el vínculo Microsoft 365 **integración.**</span><span class="sxs-lookup"><span data-stu-id="919b0-131">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span>

    > [!IMPORTANT]
    >
    > * <span data-ttu-id="919b0-132">Mantenga la Microsoft 365 de configuración de Los complementos de Moodle abierta en una pestaña del explorador independiente mientras necesita volver a este conjunto de páginas a lo largo del proceso.</span><span class="sxs-lookup"><span data-stu-id="919b0-132">Keep your Microsoft 365 Moodle Plugins configuration page open in a separate browser tab as you need to return to this set of pages throughout the process.</span></span>  
    >
    > * <span data-ttu-id="919b0-133">Si no tiene un sitio de Moodle existente, vaya al repositorio [de Moodle en Azure](https://github.com/azure/moodle) e implemente rápidamente una instancia de Moodle y personalízala según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="919b0-133">If you do not have an existing Moodle site, go to the [Moodle on Azure](https://github.com/azure/moodle) repo, and quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a><span data-ttu-id="919b0-134">2. Configurar la conexión entre los complementos Microsoft 365 y Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="919b0-134">2. Configure the connection between the Microsoft 365 plugins and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="919b0-135">Debe configurar la conexión entre los complementos Microsoft 365 y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919b0-135">You must configure the connection between the Microsoft 365 plugins and Azure AD.</span></span>

### <a name="requisites"></a><span data-ttu-id="919b0-136">Requisitos</span><span class="sxs-lookup"><span data-stu-id="919b0-136">Requisites</span></span>

<span data-ttu-id="919b0-137">Registre Moodle como una aplicación en Azure AD con el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="919b0-137">Register Moodle as an application in your Azure AD, using the PowerShell script.</span></span> <span data-ttu-id="919b0-138">El script de Powershell aprovisiona lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="919b0-138">The Powershell script provisions the following:</span></span>

* <span data-ttu-id="919b0-139">Una nueva aplicación de Azure AD para su Microsoft 365 inquilino, que usa el Microsoft 365 Complementos de Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-139">A new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugins.</span></span>
* <span data-ttu-id="919b0-140">La aplicación de tu Microsoft 365 inquilino, configura las direcciones URL de respuesta y los permisos necesarios para la aplicación aprovisionada y devuelve `AppID` el y `Key` .</span><span class="sxs-lookup"><span data-stu-id="919b0-140">The app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and returns the `AppID` and `Key`.</span></span>

<span data-ttu-id="919b0-141">Use la página de configuración generada y Microsoft 365 complementos de Moodle para configurar el sitio de servidor `AppID` `Key` de Moodle con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919b0-141">Use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugins setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="919b0-142">El script de PowerShell no se actualiza con los elementos de configuración más recientes, por lo tanto, debe completar la configuración manualmente siguiendo los pasos descritos en las páginas de lanzamiento de Moodle [3.8.0.4 y 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) y [3.8.0.5 y 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release)</span><span class="sxs-lookup"><span data-stu-id="919b0-142">The PowerShell script is not updated with the latest configuration items, therefore, you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span>
>
> * <span data-ttu-id="919b0-143">Para obtener más información sobre cómo registrar la instancia de Moodle manualmente, vea [Registrar la instancia de Moodle como una aplicación](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span><span class="sxs-lookup"><span data-stu-id="919b0-143">For more information on registering your Moodle instance manually, see [Register your Moodle instance as an application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="919b0-144">La pestaña Moodle para Microsoft Teams flujo de información</span><span class="sxs-lookup"><span data-stu-id="919b0-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="919b0-145">En la Microsoft 365 complementos de integración, seleccione la **pestaña Configurar.**</span><span class="sxs-lookup"><span data-stu-id="919b0-145">From the Microsoft 365 Integration plugins page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="919b0-146">Seleccione el **botón Descargar script de PowerShell** y guárdelo como una carpeta ZIP en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="919b0-146">Select the **Download PowerShell Script** button and save it as a ZIP folder to your local computer.</span></span>

1. <span data-ttu-id="919b0-147">Prepare el script de PowerShell desde el archivo ZIP de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="919b0-147">Prepare the PowerShell script from the ZIP file as follows:</span></span> 

    1. <span data-ttu-id="919b0-148">Descargue y extraiga el `Moodle-AzureAD-Powershell.zip` archivo.</span><span class="sxs-lookup"><span data-stu-id="919b0-148">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="919b0-149">Abra la carpeta extraída.</span><span class="sxs-lookup"><span data-stu-id="919b0-149">Open the extracted folder.</span></span>
    1. <span data-ttu-id="919b0-150">Haga clic con el botón secundario en `Moodle-AzureAD-Script.ps1` el archivo y seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="919b0-150">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="919b0-151">En la **pestaña General** de la ventana Propiedades, active la casilla situada junto al atributo `Unblock` **Seguridad** situado en la parte inferior de la ventana.</span><span class="sxs-lookup"><span data-stu-id="919b0-151">Under the **General** tab of the Properties window, select the `Unblock` checkbox next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="919b0-152">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="919b0-152">Select **OK**.</span></span>
    1. <span data-ttu-id="919b0-153">Copie la ruta de acceso del directorio en la carpeta extraída.</span><span class="sxs-lookup"><span data-stu-id="919b0-153">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="919b0-154">Ejecute PowerShell como administrador:</span><span class="sxs-lookup"><span data-stu-id="919b0-154">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="919b0-155">Seleccione Inicio.</span><span class="sxs-lookup"><span data-stu-id="919b0-155">Select Start.</span></span>
    1. <span data-ttu-id="919b0-156">Escriba PowerShell.</span><span class="sxs-lookup"><span data-stu-id="919b0-156">Type PowerShell.</span></span>
    1. <span data-ttu-id="919b0-157">Haga clic con el botón secundario **en Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="919b0-157">Right-click on **Windows PowerShell**.</span></span>
    1. <span data-ttu-id="919b0-158">Seleccione **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="919b0-158">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="919b0-159">Navegue al directorio descomprimido escribiendo `cd .../.../Moodle-AzureAD-Powershell` dónde está la ruta de acceso al `.../...` directorio.</span><span class="sxs-lookup"><span data-stu-id="919b0-159">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="919b0-160">Ejecute el script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="919b0-160">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="919b0-161">Escriba `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .</span><span class="sxs-lookup"><span data-stu-id="919b0-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="919b0-162">Escriba `./Moodle-AzureAD-Script.ps1` .</span><span class="sxs-lookup"><span data-stu-id="919b0-162">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="919b0-163">Inicie sesión en su cuenta Microsoft 365 administrador en la ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="919b0-163">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="919b0-164">Escriba el nombre de la aplicación de Azure AD, por ejemplo, complementos de Moodle o Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-164">Enter the name of the Azure AD Application, for example, Moodle or Moodle plugins.</span></span>
    1. <span data-ttu-id="919b0-165">Escriba la dirección URL del servidor de Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-165">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="919b0-166">Copie el **identificador de aplicación ( ) `AppID` y** **la clave de aplicación( `Key` )** generados por el script y guárdelos.</span><span class="sxs-lookup"><span data-stu-id="919b0-166">Copy the **Application ID (`AppID`)** and **Application Key(`Key`)** generated by the script and save them.</span></span>

1. <span data-ttu-id="919b0-167">A continuación, debe agregar `AppID` y al Microsoft 365 Complementos de `Key` Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-167">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugins.</span></span> <span data-ttu-id="919b0-168">Vuelva a la página de administración de complementos, Administración del sitio > complementos > Microsoft 365 integración.</span><span class="sxs-lookup"><span data-stu-id="919b0-168">Return to the plugins administration page, Site administration > Plugins > Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="919b0-169">En la **ficha Configuración,** agregue el y `AppID` copió anteriormente y, a continuación, seleccione Guardar `Key` **cambios**.</span><span class="sxs-lookup"><span data-stu-id="919b0-169">On the **Setup** tab add the `AppID` and `Key` you copied previously, and then select **Save changes**.</span></span> <span data-ttu-id="919b0-170">Después de actualizar la página, puede ver una nueva sección **Elegir método de conexión**.</span><span class="sxs-lookup"><span data-stu-id="919b0-170">After the page refreshes, you can see a new section **Choose connection method**.</span></span>

1. <span data-ttu-id="919b0-171">En el **método Choose connection**, seleccione la casilla de verificación predeterminada y, a continuación, seleccione Guardar cambios **de** nuevo. </span><span class="sxs-lookup"><span data-stu-id="919b0-171">In the **Choose connection method**, select the checkbox labeled **Default**, and then select **Save changes** again.</span></span>

1. <span data-ttu-id="919b0-172">Después de actualizar la página, puede ver otra nueva sección Consentimiento **de administrador & información adicional**.</span><span class="sxs-lookup"><span data-stu-id="919b0-172">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="919b0-173">Seleccione **El vínculo Proporcionar consentimiento de** administrador, escriba su Microsoft 365 de administrador global y, a continuación, acepte para conceder los permisos. </span><span class="sxs-lookup"><span data-stu-id="919b0-173">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="919b0-174">Junto al campo **Inquilino de Azure AD,** seleccione el **botón** Detectar.</span><span class="sxs-lookup"><span data-stu-id="919b0-174">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="919b0-175">Junto a la **dirección URL OneDrive para la Empresa**, seleccione el **botón** Detectar.</span><span class="sxs-lookup"><span data-stu-id="919b0-175">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="919b0-176">Después de rellenar los campos, vuelva a seleccionar **el** botón Guardar cambios.</span><span class="sxs-lookup"><span data-stu-id="919b0-176">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="919b0-177">Seleccione el **botón** Actualizar para comprobar la instalación y, a continuación, **seleccione Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="919b0-177">Select the **Update** button to verify the installation, and then select **Save changes**.</span></span>

1. <span data-ttu-id="919b0-178">Sincronizar usuarios entre el servidor de Moodle y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919b0-178">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="919b0-179">Para empezar:</span><span class="sxs-lookup"><span data-stu-id="919b0-179">To get started:</span></span>

    > [!NOTE]
    > <span data-ttu-id="919b0-180">Dependiendo del entorno, puede seleccionar diferentes opciones durante esta fase.</span><span class="sxs-lookup"><span data-stu-id="919b0-180">Depending on your environment, you can select different options during this stage.</span></span>

1. <span data-ttu-id="919b0-181">Sincronizar usuarios entre el servidor de Moodle y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919b0-181">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="919b0-182">Dependiendo del entorno, puede seleccionar diferentes opciones durante esta fase.</span><span class="sxs-lookup"><span data-stu-id="919b0-182">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="919b0-183">Para empezar:</span><span class="sxs-lookup"><span data-stu-id="919b0-183">To get started:</span></span>
    1. <span data-ttu-id="919b0-184">Cambie a la **pestaña Sincronizar Configuración**.</span><span class="sxs-lookup"><span data-stu-id="919b0-184">Switch to the **Sync Settings tab**.</span></span>

    1. <span data-ttu-id="919b0-185">En la **sección Sincronizar usuarios con Azure AD,** selecciona las casillas que se aplican a tu entorno.</span><span class="sxs-lookup"><span data-stu-id="919b0-185">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="919b0-186">Debe seleccionar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="919b0-186">You must select the following:</span></span>  

        <span data-ttu-id="919b0-187">✔ crear cuentas en Moodle para usuarios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919b0-187">✔ Create accounts in Moodle for users in Azure AD.</span></span>

        <span data-ttu-id="919b0-188">✔ todas las cuentas de Moodle para usuarios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919b0-188">✔ Update all accounts in Moodle for users in Azure AD.</span></span>

    1. <span data-ttu-id="919b0-189">En la **sección Restricción de** creación de usuarios, puede configurar un filtro para limitar los usuarios de Azure AD que están sincronizados con Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-189">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="919b0-190">La **sección Asignación de campos de** usuario permite personalizar la asignación de campos de Azure AD a Perfil de usuario de Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-190">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="919b0-191">En la **Teams sincronización,** puede seleccionar crear automáticamente grupos, como equipos para algunos o todos los cursos de Moodle existentes.</span><span class="sxs-lookup"><span data-stu-id="919b0-191">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

13. <span data-ttu-id="919b0-192">Para validar [los trabajos cron](https://docs.moodle.org/310/en/Cron) y ejecutarlos manualmente para la primera ejecución, seleccione el vínculo **página** Administración de tareas programadas en la sección Sincronizar usuarios con **Azure AD.**</span><span class="sxs-lookup"><span data-stu-id="919b0-192">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="919b0-193">Esto le llevará a la **página Tareas programadas.**</span><span class="sxs-lookup"><span data-stu-id="919b0-193">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="919b0-194">Desplácese hacia abajo y busque el trabajo **Sincronizar usuarios con Azure AD** y seleccione Ejecutar **ahora**.</span><span class="sxs-lookup"><span data-stu-id="919b0-194">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="919b0-195">Si selecciona crear grupos basados en cursos existentes, también puede ejecutar el trabajo Crear grupos de usuarios **Microsoft 365** usuario.</span><span class="sxs-lookup"><span data-stu-id="919b0-195">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="919b0-196">El Cron de [Moodle](https://docs.moodle.org/310/en/Cron) se ejecuta de acuerdo con la programación de tareas.</span><span class="sxs-lookup"><span data-stu-id="919b0-196">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="919b0-197">La programación predeterminada es una vez al día.</span><span class="sxs-lookup"><span data-stu-id="919b0-197">The default schedule is once a day.</span></span> <span data-ttu-id="919b0-198">Sin embargo, el cron debe ejecutarse con más frecuencia para mantener todo sincronizado.</span><span class="sxs-lookup"><span data-stu-id="919b0-198">However, the cron must run more frequently to keep everything in sync.</span></span>

1. <span data-ttu-id="919b0-199">Vuelva a la página de administración de complementos, Administración del **sitio > Complementos > Microsoft 365 integración** y seleccione la **Teams Configuración** página.</span><span class="sxs-lookup"><span data-stu-id="919b0-199">Return to the plugins administration page, **Site administration > Plugins > Microsoft 365 Integration**, and select the **Teams Settings** page.</span></span>

1. <span data-ttu-id="919b0-200">En la **Teams Configuración,** configure la configuración necesaria para habilitar la integración Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="919b0-200">On the **Teams Settings** page, configure the required settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="919b0-201">Para habilitar **OpenID Conectar**,  seleccione el vínculo Administrar autenticación y seleccione el icono de ojo en la línea Conectar **OpenId** si está gris.</span><span class="sxs-lookup"><span data-stu-id="919b0-201">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="919b0-202">Para habilitar la incrustación de fotogramas, seleccione el vínculo **Seguridad HTTP** y, a continuación, active la casilla situada junto a Permitir incrustación **de fotogramas**.</span><span class="sxs-lookup"><span data-stu-id="919b0-202">To enable frame embedding, select the **HTTP Security** link, and then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="919b0-203">Para habilitar los servicios web, que habilita  las características de la API de Moodle, seleccione el vínculo Características avanzadas y, a continuación, asegúrese de que la casilla situada junto a Habilitar servicios **web** esté seleccionada.</span><span class="sxs-lookup"><span data-stu-id="919b0-203">To enable web services, which enables the Moodle API features, select the **Advanced Features** link, and then ensure the checkbox next to **Enable web services** is selected.</span></span>
    1. <span data-ttu-id="919b0-204">Para habilitar los servicios externos para Microsoft 365, seleccione el vínculo **Servicios** externos y, a continuación:</span><span class="sxs-lookup"><span data-stu-id="919b0-204">To enable the external services for Microsoft 365, select the **External services** link, and then:</span></span>  

        <span data-ttu-id="919b0-205">✔ Seleccione **Editar en** la **fila Moodle Microsoft 365 Webservices.**</span><span class="sxs-lookup"><span data-stu-id="919b0-205">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>

        <span data-ttu-id="919b0-206">✔ Seleccione la casilla situada junto a **Habilitado** y, a continuación, **seleccione Guardar cambios**</span><span class="sxs-lookup"><span data-stu-id="919b0-206">✔ Select the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="919b0-207">Edite los permisos de usuario autenticados para permitirles crear tokens de servicio web.</span><span class="sxs-lookup"><span data-stu-id="919b0-207">Edit your authenticated user permissions to allow them to create web service tokens.</span></span>

        <span data-ttu-id="919b0-208">✔ Seleccione el vínculo **Editar rol Usuario autenticado.**</span><span class="sxs-lookup"><span data-stu-id="919b0-208">✔ Select the **Editing role Authenticated user** link.</span></span>

        <span data-ttu-id="919b0-209">✔ desplácese hacia abajo y busque **la funcionalidad Crear un token de** servicio web y active la **casilla** Permitir.</span><span class="sxs-lookup"><span data-stu-id="919b0-209">✔ Scroll down and find the **Create a web service token** capability and select the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="919b0-210">3. Implementar el bot asistente de Moodle en Azure</span><span class="sxs-lookup"><span data-stu-id="919b0-210">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="919b0-211">El bot asistente de Moodle gratuito para Microsoft Teams ayuda a los profesores y alumnos a responder preguntas sobre sus cursos, asignaciones, calificaciones y otra información en Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-211">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades, and other information in Moodle.</span></span> <span data-ttu-id="919b0-212">El bot también envía notificaciones de Moodle a alumnos y profesores dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="919b0-212">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="919b0-213">El bot es un proyecto de código abierto mantenido por Microsoft y está disponible en [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span><span class="sxs-lookup"><span data-stu-id="919b0-213">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
>
> * <span data-ttu-id="919b0-214">Implemente recursos en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="919b0-214">Deploy resources to your Azure subscription.</span></span> <span data-ttu-id="919b0-215">Todos los recursos se configuraron mediante **el nivel** gratuito.</span><span class="sxs-lookup"><span data-stu-id="919b0-215">All resources were configured using the **free** tier.</span></span> <span data-ttu-id="919b0-216">Según el uso del bot, es posible que deba escalar estos recursos.</span><span class="sxs-lookup"><span data-stu-id="919b0-216">Depending on the usage of your bot, you may have to scale these resources.</span></span>
>
> * <span data-ttu-id="919b0-217">Para usar la pestaña Moodle sin el bot, vaya a [4](#4-deploy-your-microsoft-teams-app).</span><span class="sxs-lookup"><span data-stu-id="919b0-217">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="919b0-218">Flujo de información del bot de Moodle</span><span class="sxs-lookup"><span data-stu-id="919b0-218">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="919b0-219">Para instalar el bot, debe registrarlo en la [Plataforma de identidad de Microsoft](https://identity.microsoft.com/Landing).</span><span class="sxs-lookup"><span data-stu-id="919b0-219">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="919b0-220">Esto permite que el bot se autentique con los puntos de conexión de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="919b0-220">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="919b0-221">**Para registrar el bot**</span><span class="sxs-lookup"><span data-stu-id="919b0-221">**To register your bot**</span></span>

1. <span data-ttu-id="919b0-222">Vaya a la página de administración de complementos y, a continuación, seleccione **Complementos**.</span><span class="sxs-lookup"><span data-stu-id="919b0-222">Go to the plugins administration page, and then select **Plugins**.</span></span> <span data-ttu-id="919b0-223">En **Microsoft 365 integración,** seleccione la **Teams Configuración** pestaña.</span><span class="sxs-lookup"><span data-stu-id="919b0-223">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="919b0-224">Seleccione el **vínculo Portal de registro de aplicaciones** de Microsoft e inicie sesión con su id. de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="919b0-224">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="919b0-225">Escribe un nombre para la aplicación, como MoodleBot y selecciona el **botón** Crear.</span><span class="sxs-lookup"><span data-stu-id="919b0-225">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="919b0-226">Copie el **identificador de aplicación** y péguelo en el campo **Id.** de aplicación bot de la página **De Configuración** equipo.</span><span class="sxs-lookup"><span data-stu-id="919b0-226">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="919b0-227">Seleccione el **botón Generar nueva contraseña.**</span><span class="sxs-lookup"><span data-stu-id="919b0-227">Select the **Generate New Password** button.</span></span> <span data-ttu-id="919b0-228">Copie la contraseña generada y péguela en el campo **Bot Application Password** de la página Team **Configuración.**</span><span class="sxs-lookup"><span data-stu-id="919b0-228">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="919b0-229">Desplácese hasta la parte inferior del formulario y seleccione **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="919b0-229">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="919b0-230">Después de generar el identificador de aplicación y la contraseña, implemente el bot en Azure:</span><span class="sxs-lookup"><span data-stu-id="919b0-230">After generating your application ID and password, deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="919b0-231">Seleccione **Implementar en Azure** y complete el formulario con la información necesaria, como el identificador de aplicación bot, la contraseña de la aplicación bot y el secreto de Estado de ánimo en la **Teams Configuración** web.</span><span class="sxs-lookup"><span data-stu-id="919b0-231">Select **Deploy to Azure** and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password, and the Moodle Secret on the **Teams Settings** page.</span></span> <span data-ttu-id="919b0-232">La información de Azure se encuentra en la **página Configuración.**</span><span class="sxs-lookup"><span data-stu-id="919b0-232">The Azure information is on the **Setup** page.</span></span> 
> * <span data-ttu-id="919b0-233">Después de completar el formulario, selecciona la casilla para aceptar los términos y condiciones.</span><span class="sxs-lookup"><span data-stu-id="919b0-233">After completing the form, select the checkbox to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="919b0-234">Seleccione **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="919b0-234">Select **Purchase**.</span></span> <span data-ttu-id="919b0-235">Todos los recursos de Azure se implementan en el nivel gratuito.</span><span class="sxs-lookup"><span data-stu-id="919b0-235">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="919b0-236">Una vez que los recursos hayan completado la implementación en Azure, debe configurar los complementos Microsoft 365 Moodle con un punto de conexión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="919b0-236">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugins with a messaging endpoint.</span></span> <span data-ttu-id="919b0-237">Debe obtener el punto de conexión del bot en Azure:</span><span class="sxs-lookup"><span data-stu-id="919b0-237">You must get the endpoint from your bot in Azure:</span></span>

1. <span data-ttu-id="919b0-238">Inicie sesión en el [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="919b0-238">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="919b0-239">En el panel izquierdo, seleccione **Grupos de recursos** y seleccione el grupo de recursos que usó o creó, mientras implementa el bot.</span><span class="sxs-lookup"><span data-stu-id="919b0-239">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="919b0-240">Seleccione el **recurso Bot de WebApp** de la lista de recursos del grupo.</span><span class="sxs-lookup"><span data-stu-id="919b0-240">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="919b0-241">Copie el **extremo de mensajería** de la sección **Información** general.</span><span class="sxs-lookup"><span data-stu-id="919b0-241">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="919b0-242">En Moodle, abra la **página De Configuración** equipo de su Microsoft 365 Complementos de Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-242">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugins.</span></span>

1. <span data-ttu-id="919b0-243">En el **campo Bot Endpoint,** pegue la dirección URL que acaba de copiar y cambie los mensajes *de palabra* a *webhook*.</span><span class="sxs-lookup"><span data-stu-id="919b0-243">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="919b0-244">La dirección URL debe aparecer de la siguiente manera: `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="919b0-244">The URL must appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="919b0-245">Seleccione **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="919b0-245">Select **Save Changes**.</span></span>

1. <span data-ttu-id="919b0-246">Después de guardar los cambios, vuelve **a** la pestaña  Configuración equipo, selecciona el botón Descargar archivo de manifiesto y guarda el paquete de manifiesto de la aplicación en el equipo para usarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="919b0-246">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="919b0-247">4. Implementar la aplicación Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="919b0-247">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="919b0-248">Después de que el bot se implemente en Azure y esté configurado para hablar con el servidor de Moodle, debe implementar la aplicación Microsoft Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="919b0-248">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="919b0-249">Para ello, debes cargar el archivo de manifiesto de la aplicación que descargaste de la página Microsoft 365 página de Configuración de complementos de Moodle en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="919b0-249">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugins Team Settings page in the previous step.</span></span>

<span data-ttu-id="919b0-250">Antes de instalar la aplicación, debes asegurarte de habilitar las aplicaciones externas y la carga de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="919b0-250">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="919b0-251">Para obtener más información, vea [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="919b0-251">For more information, see [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span> 

<span data-ttu-id="919b0-252">**Para implementar la aplicación**</span><span class="sxs-lookup"><span data-stu-id="919b0-252">**To deploy your app**</span></span> 

1. <span data-ttu-id="919b0-253">Abra **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="919b0-253">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="919b0-254">Selecciona el **icono Aplicación** en el área inferior izquierda de la barra de navegación.</span><span class="sxs-lookup"><span data-stu-id="919b0-254">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="919b0-255">Selecciona el **Upload de una aplicación** personalizada de la lista de opciones.</span><span class="sxs-lookup"><span data-stu-id="919b0-255">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="919b0-256">Si has iniciado sesión como administrador global, debes tener la opción de cargar la aplicación en el catálogo de aplicaciones de tu organización, de lo contrario solo puedes cargar la aplicación para un equipo en el que seas miembro.</span><span class="sxs-lookup"><span data-stu-id="919b0-256">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="919b0-257">Seleccione el `manifest.zip` paquete que descargó anteriormente y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="919b0-257">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="919b0-258">Si no has descargado el paquete de manifiesto de la aplicación, puedes descargar desde la pestaña De **Configuración** equipo de la página de configuración de complementos de Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-258">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugins configuration page in Moodle.</span></span>

<span data-ttu-id="919b0-259">Ahora que tienes instalada la aplicación, puedes agregar la pestaña a cualquier canal al que tenga acceso.</span><span class="sxs-lookup"><span data-stu-id="919b0-259">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="919b0-260">Para ello, vaya al canal, seleccione el símbolo **más** (➕) y seleccione la aplicación en la lista.</span><span class="sxs-lookup"><span data-stu-id="919b0-260">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="919b0-261">Sigue las indicaciones para terminar de agregar la pestaña de curso de Moodle a un canal.</span><span class="sxs-lookup"><span data-stu-id="919b0-261">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="919b0-262">5. Permitir la creación automática de pestañas de Moodle en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="919b0-262">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="919b0-263">Aunque las pestañas de Moodle se crean manualmente en Microsoft Teams, puede decidir crearlas automáticamente cuando se creen equipos a partir de la sincronización del curso.</span><span class="sxs-lookup"><span data-stu-id="919b0-263">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to create them automatically when teams are created from course synchronization.</span></span> <span data-ttu-id="919b0-264">Para ello, debes configurar el identificador de la aplicación Microsoft Teams carga en Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-264">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle.</span></span>

<span data-ttu-id="919b0-265">**Para permitir la creación automática de pestañas de Moodle**</span><span class="sxs-lookup"><span data-stu-id="919b0-265">**To allow automatic creation of Moodle tabs**</span></span>

1. <span data-ttu-id="919b0-266">Abra Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="919b0-266">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="919b0-267">Selecciona el icono Aplicaciones en el área inferior izquierda de la barra de navegación.</span><span class="sxs-lookup"><span data-stu-id="919b0-267">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="919b0-268">Busque la aplicación **de Moodle** cargada > el icono **de** opciones > seleccione **copiar vínculo**.</span><span class="sxs-lookup"><span data-stu-id="919b0-268">Locate the uploaded **Moodle app** > select the **options** icon > select **copy link**.</span></span>

1. <span data-ttu-id="919b0-269">En un editor de texto, pegue el contenido copiado.</span><span class="sxs-lookup"><span data-stu-id="919b0-269">In a text editor, paste the copied content.</span></span> <span data-ttu-id="919b0-270">Debe contener una dirección URL como ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span><span class="sxs-lookup"><span data-stu-id="919b0-270">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="919b0-271">Copia la última parte de la dirección URL, como `00112233-4455-6677-8899-aabbccddeeff` , que es el identificador de la Microsoft Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="919b0-271">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="919b0-272">En Moodle, abre la pestaña Teams de la aplicación **Moodle** desde la Microsoft 365 configuración de Complementos de Moodle.</span><span class="sxs-lookup"><span data-stu-id="919b0-272">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugins configuration page.</span></span>

1. <span data-ttu-id="919b0-273">Pegue el identificador de la Microsoft Teams en el campo Id. de aplicación de Moodle y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="919b0-273">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="919b0-274">Cuando se sincroniza un curso de Moodle, Microsoft Teams instala automáticamente la aplicación Moodle en el equipo, crea una pestaña Moodle en el canal general de Teams y la configura para que contenga la página del curso de Moodle desde la que está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="919b0-274">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, creates a Moodle tab in the General channel of Teams, and configures it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="919b0-275">Ahora puede empezar a trabajar con los cursos de Moodle directamente desde Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="919b0-275">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="919b0-276">Para compartir cualquier solicitud de característica o comentarios con nosotros, visite nuestra página [De voz de usuario](https://microsoftteams.uservoice.com/forums/916759-moodle).</span><span class="sxs-lookup"><span data-stu-id="919b0-276">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="919b0-277">Consulte también</span><span class="sxs-lookup"><span data-stu-id="919b0-277">See also</span></span>

- [<span data-ttu-id="919b0-278">Integrar aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="919b0-278">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
- [<span data-ttu-id="919b0-279">Moodle</span><span class="sxs-lookup"><span data-stu-id="919b0-279">Moodle</span></span>](https://moodle.org/)
- <span data-ttu-id="919b0-280">[Documentación de Moodle](https://docs.moodle.org/34/en/Installing_plugins).</span><span class="sxs-lookup"><span data-stu-id="919b0-280">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>

