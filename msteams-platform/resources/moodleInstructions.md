---
title: Instalar Moodle LMS
description: Cómo instalar y configurar la aplicación de integración de Moodle para Microsoft Teams
keywords: Teams Plugins de integración de aplicaciones Moodle
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: d7fddad80ca08fd4ca8dee352cdcbc46e8e97dcd
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566722"
---
# <a name="install-moodle-lms"></a><span data-ttu-id="013fb-104">Instalar Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="013fb-104">Install Moodle LMS</span></span>

<span data-ttu-id="013fb-105">En este artículo aprenderás a instalar moodle LMS.</span><span class="sxs-lookup"><span data-stu-id="013fb-105">In this article you'll learn how to install the Moodle LMS.</span></span>

> [!NOTE]
> <span data-ttu-id="013fb-106">Para ayudar a los administradores de TI a configurar fácilmente Moodle y Teams integración, se actualizan los plugins de código abierto Microsoft 365 Moodle para lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="013fb-106">To help IT admins to easily set-up Moodle and Teams integration, open-source Microsoft 365 Moodle Plugins is updated for the following:</span></span>
>
> * <span data-ttu-id="013fb-107">Registro automático del servidor De Moodle con [Azure Active Directory (Azure AD).](https://azure.microsoft.com/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="013fb-107">Auto-registration of your Moodle server with [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).</span></span>
>
> * <span data-ttu-id="013fb-108">Implementación con un solo clic del bot de Moodle Assistant en Azure.</span><span class="sxs-lookup"><span data-stu-id="013fb-108">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
>
> * <span data-ttu-id="013fb-109">Aprovisionamiento automático de equipos y sincronización automática de inscripciones de equipo para todos o seleccionar cursos de Moodle.</span><span class="sxs-lookup"><span data-stu-id="013fb-109">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
>
> * <span data-ttu-id="013fb-110">Instalación automática de la pestaña Moodle y el bot asistente de Moodle en cada equipo sincronizado.</span><span class="sxs-lookup"><span data-stu-id="013fb-110">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>
>
> <span data-ttu-id="013fb-111">Para obtener más información sobre la funcionalidad que proporciona esta integración, consulte [Microsoft Teams y Moodle](https://education.microsoft.com/resource/3dffb3a8).</span><span class="sxs-lookup"><span data-stu-id="013fb-111">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="013fb-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="013fb-112">Prerequisites</span></span>

<span data-ttu-id="013fb-113">A continuación se indican los requisitos previos para instalar Moodle:</span><span class="sxs-lookup"><span data-stu-id="013fb-113">Following are the prerequisites to install Moodle:</span></span>

* <span data-ttu-id="013fb-114">Credenciales de administrador de Moodle.</span><span class="sxs-lookup"><span data-stu-id="013fb-114">Moodle administrator credentials.</span></span>

* <span data-ttu-id="013fb-115">Credenciales de administrador de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="013fb-115">Azure AD administrator credentials.</span></span>

* <span data-ttu-id="013fb-116">Una suscripción de Azure donde puede crear nuevos recursos.</span><span class="sxs-lookup"><span data-stu-id="013fb-116">An Azure subscription where you can create new resources.</span></span>

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="013fb-117">1. Instale los plugins Microsoft 365 Moodle</span><span class="sxs-lookup"><span data-stu-id="013fb-117">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="013fb-118">La integración de Moodle en Microsoft Teams está impulsada por el conjunto de plugins de código abierto [Microsoft 365 Moodle.](https://github.com/Microsoft/o365-moodle)</span><span class="sxs-lookup"><span data-stu-id="013fb-118">Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugins set](https://github.com/Microsoft/o365-moodle).</span></span>

### <a name="requisite-applications-and-plugins"></a><span data-ttu-id="013fb-119">Aplicaciones y plugins necesarios</span><span class="sxs-lookup"><span data-stu-id="013fb-119">Requisite applications and plugins</span></span>

<span data-ttu-id="013fb-120">Asegúrese de instalar y descargar lo siguiente antes de continuar con la instalación de los plugins Microsoft 365 Moodle:</span><span class="sxs-lookup"><span data-stu-id="013fb-120">Ensure to install and download the following before proceeding with the Microsoft 365 Moodle plugins installation:</span></span>

1. <span data-ttu-id="013fb-121">Asegúrese de instalar una [versión estable actual de Moodle](https://download.moodle.org/releases/latest/).</span><span class="sxs-lookup"><span data-stu-id="013fb-121">Ensure to install a [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="013fb-122">Descargue y guarde el Conectar De Moodle [OpenID](https://moodle.org/plugins/auth_oidc) y los plugins [de integración de Microsoft 365](https://moodle.org/plugins/local_o365) en su equipo local.</span><span class="sxs-lookup"><span data-stu-id="013fb-122">Download and save the Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins to your local computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="013fb-123">Para la integración Teams se requiere la instalación de los complementos OpenID Conectar y Microsoft 365 Integration.</span><span class="sxs-lookup"><span data-stu-id="013fb-123">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span>
    >
    > <span data-ttu-id="013fb-124">Además, los plugins [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) son muy recomendables.</span><span class="sxs-lookup"><span data-stu-id="013fb-124">In addition, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugins is highly recommended.</span></span>

### <a name="microsoft-365-moodle-plugins"></a><span data-ttu-id="013fb-125">Microsoft 365 Plugins de Moodle</span><span class="sxs-lookup"><span data-stu-id="013fb-125">Microsoft 365 Moodle plugins</span></span>

1. <span data-ttu-id="013fb-126">Inicie sesión en su servidor Moodle como administrador y seleccione **Administración del sitio** en el bloque [Configuración](https://docs.moodle.org/22/en/Settings_block) ubicado en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="013fb-126">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="013fb-127">Seleccione la pestaña **Plugins** y, a continuación, seleccione **Instalar plugins**.</span><span class="sxs-lookup"><span data-stu-id="013fb-127">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="013fb-128">En la sección **Instalar plugins desde archivo ZIP,** seleccione **Elegir un archivo**.</span><span class="sxs-lookup"><span data-stu-id="013fb-128">From the **Install plugins from ZIP file** section, select **Choose a file**.</span></span>

1. <span data-ttu-id="013fb-129">Seleccione **Upload una** opción de archivo en el panel de navegación izquierdo, busque el archivo que descargó y seleccione Upload este **archivo**.</span><span class="sxs-lookup"><span data-stu-id="013fb-129">Select **Upload a file** option from the left navigation panel, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="013fb-130">Seleccione **Administración del sitio** en el panel de navegación izquierdo para volver al panel de administración.</span><span class="sxs-lookup"><span data-stu-id="013fb-130">Select **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="013fb-131">Desplázate hacia abajo hasta los **plugins locales** y selecciona el vínculo **integración Microsoft 365.**</span><span class="sxs-lookup"><span data-stu-id="013fb-131">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span>

    > [!IMPORTANT]
    >
    > * <span data-ttu-id="013fb-132">Mantenga su página de configuración de Microsoft 365 Moodle Plugins abierta en una pestaña separada del navegador, ya que necesita volver a este conjunto de páginas durante todo el proceso.</span><span class="sxs-lookup"><span data-stu-id="013fb-132">Keep your Microsoft 365 Moodle Plugins configuration page open in a separate browser tab as you need to return to this set of pages throughout the process.</span></span>  
    >
    > * <span data-ttu-id="013fb-133">Si no tiene un sitio de Moodle existente, vaya al repositorio [de Moodle en Azure](https://github.com/azure/moodle) e implemente rápidamente una instancia de Moodle y personalícela según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="013fb-133">If you do not have an existing Moodle site, go to the [Moodle on Azure](https://github.com/azure/moodle) repo, and quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a><span data-ttu-id="013fb-134">2. Configure la conexión entre los complementos de Microsoft 365 y Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="013fb-134">2. Configure the connection between the Microsoft 365 plugins and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="013fb-135">Debe configurar la conexión entre los complementos de Microsoft 365 y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="013fb-135">You must configure the connection between the Microsoft 365 plugins and Azure AD.</span></span>

### <a name="requisites"></a><span data-ttu-id="013fb-136">Requisitos</span><span class="sxs-lookup"><span data-stu-id="013fb-136">Requisites</span></span>

<span data-ttu-id="013fb-137">Registre Moodle como una aplicación en Azure AD mediante el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="013fb-137">Register Moodle as an application in your Azure AD, using the PowerShell script.</span></span> <span data-ttu-id="013fb-138">El script de Powershell aprovisiona lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="013fb-138">The Powershell script provisions the following:</span></span>

* <span data-ttu-id="013fb-139">Una nueva aplicación de Azure AD para el inquilino de Microsoft 365, que usa los complementos de Moodle Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="013fb-139">A new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugins.</span></span>
* <span data-ttu-id="013fb-140">La aplicación para el inquilino Microsoft 365, configurar las direcciones URL de respuesta necesarias y los permisos para la aplicación aprovisionada y devuelve el `AppID` archivo and `Key` .</span><span class="sxs-lookup"><span data-stu-id="013fb-140">The app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and returns the `AppID` and `Key`.</span></span>

<span data-ttu-id="013fb-141">Use la página de configuración generada `AppID` y en su Microsoft 365 de configuración de `Key` Moodle Plugins para configurar el sitio del servidor de Moodle con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="013fb-141">Use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugins setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="013fb-142">El script de PowerShell no se actualiza con los elementos de configuración más recientes, por lo tanto, debe completar la configuración manualmente siguiendo los pasos descritos en las páginas de lanzamiento de Moodle [3.8.0.4 y 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) y [3.8.0.5 y 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release)</span><span class="sxs-lookup"><span data-stu-id="013fb-142">The PowerShell script is not updated with the latest configuration items, therefore, you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span>
>
> * <span data-ttu-id="013fb-143">Para obtener más información sobre cómo registrar la instancia de Moodle manualmente, consulte [Registrar la instancia de Moodle como una aplicación.](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)</span><span class="sxs-lookup"><span data-stu-id="013fb-143">For more information on registering your Moodle instance manually, see [Register your Moodle instance as an application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="013fb-144">La pestaña Moodle para Microsoft Teams flujo de información</span><span class="sxs-lookup"><span data-stu-id="013fb-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="013fb-145">En la página Microsoft 365 complementos de integración, seleccione la pestaña **Configuración.**</span><span class="sxs-lookup"><span data-stu-id="013fb-145">From the Microsoft 365 Integration plugins page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="013fb-146">Seleccione el botón **Descargar script de PowerShell** y guárdelo como una carpeta ZIP en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="013fb-146">Select the **Download PowerShell Script** button and save it as a ZIP folder to your local computer.</span></span>

1. <span data-ttu-id="013fb-147">Prepare el script de PowerShell desde el archivo ZIP de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="013fb-147">Prepare the PowerShell script from the ZIP file as follows:</span></span> 

    1. <span data-ttu-id="013fb-148">Descargue y extraiga el `Moodle-AzureAD-Powershell.zip` archivo.</span><span class="sxs-lookup"><span data-stu-id="013fb-148">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="013fb-149">Abra la carpeta extraída.</span><span class="sxs-lookup"><span data-stu-id="013fb-149">Open the extracted folder.</span></span>
    1. <span data-ttu-id="013fb-150">Haga clic con el botón derecho en el `Moodle-AzureAD-Script.ps1` archivo y seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="013fb-150">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="013fb-151">En la pestaña **General** de la ventana Propiedades, active la `Unblock` casilla situada junto al atributo **Seguridad** situado en la parte inferior de la ventana.</span><span class="sxs-lookup"><span data-stu-id="013fb-151">Under the **General** tab of the Properties window, select the `Unblock` checkbox next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="013fb-152">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="013fb-152">Select **OK**.</span></span>
    1. <span data-ttu-id="013fb-153">Copie la ruta de acceso del directorio a la carpeta extraída.</span><span class="sxs-lookup"><span data-stu-id="013fb-153">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="013fb-154">Ejecute PowerShell como administrador:</span><span class="sxs-lookup"><span data-stu-id="013fb-154">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="013fb-155">Seleccione Inicio.</span><span class="sxs-lookup"><span data-stu-id="013fb-155">Select Start.</span></span>
    1. <span data-ttu-id="013fb-156">Escriba PowerShell.</span><span class="sxs-lookup"><span data-stu-id="013fb-156">Type PowerShell.</span></span>
    1. <span data-ttu-id="013fb-157">Haga clic con el botón derecho en **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="013fb-157">Right-click on **Windows PowerShell**.</span></span>
    1. <span data-ttu-id="013fb-158">Seleccione **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="013fb-158">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="013fb-159">Vaya al directorio descomprimido escribiendo `cd .../.../Moodle-AzureAD-Powershell` dónde está la ruta de acceso al `.../...` directorio.</span><span class="sxs-lookup"><span data-stu-id="013fb-159">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="013fb-160">Ejecute el script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="013fb-160">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="013fb-161">Escriba `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .</span><span class="sxs-lookup"><span data-stu-id="013fb-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="013fb-162">Escriba `./Moodle-AzureAD-Script.ps1` .</span><span class="sxs-lookup"><span data-stu-id="013fb-162">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="013fb-163">Inicie sesión en su cuenta de administrador de Microsoft 365 en la ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="013fb-163">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="013fb-164">Escriba el nombre de la aplicación de Azure AD, por ejemplo, los complementos Moodle o Moodle.</span><span class="sxs-lookup"><span data-stu-id="013fb-164">Enter the name of the Azure AD Application, for example, Moodle or Moodle plugins.</span></span>
    1. <span data-ttu-id="013fb-165">Introduzca la dirección URL del servidor Moodle.</span><span class="sxs-lookup"><span data-stu-id="013fb-165">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="013fb-166">Copie el **ID de aplicación ( `AppID` )** y **la clave de aplicación ( `Key` )** generados por el script y guárdelos.</span><span class="sxs-lookup"><span data-stu-id="013fb-166">Copy the **Application ID (`AppID`)** and **Application Key(`Key`)** generated by the script and save them.</span></span>

1. <span data-ttu-id="013fb-167">A continuación, debe agregar el `AppID` y a la Microsoft 365 `Key` Moodle Plugins.</span><span class="sxs-lookup"><span data-stu-id="013fb-167">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugins.</span></span> <span data-ttu-id="013fb-168">Vuelva a la página de administración de plugins, Administración del sitio > Plugins > Microsoft 365 Integración.</span><span class="sxs-lookup"><span data-stu-id="013fb-168">Return to the plugins administration page, Site administration > Plugins > Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="013fb-169">En la pestaña **Configuración,** agregue la `AppID` y `Key` copiada anteriormente y, a continuación, seleccione **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="013fb-169">On the **Setup** tab add the `AppID` and `Key` you copied previously, and then select **Save changes**.</span></span> <span data-ttu-id="013fb-170">Después de actualizar la página, puede ver una nueva sección **Elegir método de conexión**.</span><span class="sxs-lookup"><span data-stu-id="013fb-170">After the page refreshes, you can see a new section **Choose connection method**.</span></span>

1. <span data-ttu-id="013fb-171">En el **método Elegir conexión**, seleccione la casilla de verificación **Predeterminada** y, a continuación, vuelva a seleccionar **Guardar cambios.**</span><span class="sxs-lookup"><span data-stu-id="013fb-171">In the **Choose connection method**, select the checkbox labeled **Default**, and then select **Save changes** again.</span></span>

1. <span data-ttu-id="013fb-172">Después de actualizar la página, puede ver otra nueva sección **Consentimiento de administrador & información adicional.**</span><span class="sxs-lookup"><span data-stu-id="013fb-172">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="013fb-173">Seleccione proporcionar el vínculo **de consentimiento de administrador,** escriba las credenciales de administrador global Microsoft 365 y, a continuación, **acepte** conceder los permisos.</span><span class="sxs-lookup"><span data-stu-id="013fb-173">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="013fb-174">Junto al campo **Inquilino de Azure AD,** seleccione el botón **Detectar.**</span><span class="sxs-lookup"><span data-stu-id="013fb-174">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="013fb-175">Junto a la **dirección URL de OneDrive para la Empresa**, seleccione el botón **Detectar.**</span><span class="sxs-lookup"><span data-stu-id="013fb-175">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="013fb-176">Una vez rellenados los campos, vuelva a seleccionar el botón **Guardar cambios.**</span><span class="sxs-lookup"><span data-stu-id="013fb-176">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="013fb-177">Seleccione el botón **Actualizar** para comprobar la instalación y, a continuación, seleccione **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="013fb-177">Select the **Update** button to verify the installation, and then select **Save changes**.</span></span>

1. <span data-ttu-id="013fb-178">Sincronice usuarios entre el servidor Moodle y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="013fb-178">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="013fb-179">Para empezar:</span><span class="sxs-lookup"><span data-stu-id="013fb-179">To get started:</span></span>

    > [!NOTE]
    > <span data-ttu-id="013fb-180">Dependiendo de su entorno, puede seleccionar diferentes opciones durante esta etapa.</span><span class="sxs-lookup"><span data-stu-id="013fb-180">Depending on your environment, you can select different options during this stage.</span></span>

1. <span data-ttu-id="013fb-181">Sincronice usuarios entre el servidor Moodle y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="013fb-181">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="013fb-182">Dependiendo de su entorno, puede seleccionar diferentes opciones durante esta etapa.</span><span class="sxs-lookup"><span data-stu-id="013fb-182">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="013fb-183">Para empezar:</span><span class="sxs-lookup"><span data-stu-id="013fb-183">To get started:</span></span>
    1. <span data-ttu-id="013fb-184">Cambie a la **pestaña Sincronizar Configuración**.</span><span class="sxs-lookup"><span data-stu-id="013fb-184">Switch to the **Sync Settings tab**.</span></span>

    1. <span data-ttu-id="013fb-185">En la sección **Sincronizar usuarios con Azure AD,** active las casillas de verificación que se aplican a su entorno.</span><span class="sxs-lookup"><span data-stu-id="013fb-185">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="013fb-186">Debe seleccionar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="013fb-186">You must select the following:</span></span>  

        <span data-ttu-id="013fb-187">✔ Crear cuentas en Moodle para usuarios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="013fb-187">✔ Create accounts in Moodle for users in Azure AD.</span></span>

        <span data-ttu-id="013fb-188">✔ Actualizar todas las cuentas de Moodle para los usuarios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="013fb-188">✔ Update all accounts in Moodle for users in Azure AD.</span></span>

    1. <span data-ttu-id="013fb-189">En la sección **Restricción de creación de** usuarios, puede configurar un filtro para limitar los usuarios de Azure AD que se sincroniza con Moodle.</span><span class="sxs-lookup"><span data-stu-id="013fb-189">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="013fb-190">La sección **Asignación de campos de usuario** le permite personalizar la asignación de campos de Perfil de usuario de Azure AD a Moodle.</span><span class="sxs-lookup"><span data-stu-id="013fb-190">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="013fb-191">En la sección **Teams Sync,** puede seleccionar crear automáticamente grupos, como equipos para algunos o todos los cursos de Moodle existentes.</span><span class="sxs-lookup"><span data-stu-id="013fb-191">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

13. <span data-ttu-id="013fb-192">Para validar los trabajos [cron](https://docs.moodle.org/310/en/Cron) y ejecutarlos manualmente para la primera ejecución, seleccione el vínculo **Página de administración tareas programadas** en la sección **Sincronizar usuarios con Azure AD.**</span><span class="sxs-lookup"><span data-stu-id="013fb-192">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="013fb-193">Esto le lleva a la página **Tareas programadas.**</span><span class="sxs-lookup"><span data-stu-id="013fb-193">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="013fb-194">Desplázate hacia abajo y busca el trabajo **Sincronizar usuarios con Azure AD** y selecciona Ejecutar **ahora.**</span><span class="sxs-lookup"><span data-stu-id="013fb-194">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="013fb-195">Si selecciona crear grupos en función de los cursos existentes, también puede ejecutar crear **grupos de usuarios en Microsoft 365** trabajo.</span><span class="sxs-lookup"><span data-stu-id="013fb-195">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="013fb-196">Moodle [Cron](https://docs.moodle.org/310/en/Cron) se ejecuta de acuerdo con el calendario de tareas.</span><span class="sxs-lookup"><span data-stu-id="013fb-196">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="013fb-197">La programación predeterminada es una vez al día.</span><span class="sxs-lookup"><span data-stu-id="013fb-197">The default schedule is once a day.</span></span> <span data-ttu-id="013fb-198">Sin embargo, el cron debe ejecutarse con más frecuencia para mantener todo sincronizado.</span><span class="sxs-lookup"><span data-stu-id="013fb-198">However, the cron must run more frequently to keep everything in sync.</span></span>

1. <span data-ttu-id="013fb-199">Vuelva a la página de administración de plugins, **Administración del sitio > Plugins > Microsoft 365 Integración** y seleccione la página **Teams Configuración.**</span><span class="sxs-lookup"><span data-stu-id="013fb-199">Return to the plugins administration page, **Site administration > Plugins > Microsoft 365 Integration**, and select the **Teams Settings** page.</span></span>

1. <span data-ttu-id="013fb-200">En la página **Teams Configuración,** configure la configuración necesaria para habilitar la integración de Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="013fb-200">On the **Teams Settings** page, configure the required settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="013fb-201">Para habilitar **openid Conectar**, seleccione el vínculo **Administrar autenticación** y seleccione el icono de ojo en la línea de **Conectar OpenId** si está atenuado.</span><span class="sxs-lookup"><span data-stu-id="013fb-201">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="013fb-202">Para habilitar la incrustación de fotogramas, seleccione el vínculo **Seguridad HTTP** y, a continuación, active la casilla de verificación situada junto a **Permitir incrustación de fotogramas.**</span><span class="sxs-lookup"><span data-stu-id="013fb-202">To enable frame embedding, select the **HTTP Security** link, and then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="013fb-203">Para habilitar los servicios web, que habilita las características de la API de Moodle, seleccione el vínculo **Características avanzadas** y, a continuación, asegúrese de que la casilla de verificación situada junto a Habilitar **servicios web** esté activada.</span><span class="sxs-lookup"><span data-stu-id="013fb-203">To enable web services, which enables the Moodle API features, select the **Advanced Features** link, and then ensure the checkbox next to **Enable web services** is selected.</span></span>
    1. <span data-ttu-id="013fb-204">Para habilitar los servicios externos para Microsoft 365, seleccione el vínculo **Servicios externos** y, a continuación:</span><span class="sxs-lookup"><span data-stu-id="013fb-204">To enable the external services for Microsoft 365, select the **External services** link, and then:</span></span>  

        <span data-ttu-id="013fb-205">✔ Seleccione **Editar** en la fila **Servicios web de Microsoft 365 de Moodle.**</span><span class="sxs-lookup"><span data-stu-id="013fb-205">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>

        <span data-ttu-id="013fb-206">✔ Seleccione la casilla de verificación situada junto a **Habilitado** y, a continuación, seleccione **Guardar cambios**</span><span class="sxs-lookup"><span data-stu-id="013fb-206">✔ Select the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="013fb-207">Edite los permisos de usuario autenticados para permitirles crear tokens de servicio web.</span><span class="sxs-lookup"><span data-stu-id="013fb-207">Edit your authenticated user permissions to allow them to create web service tokens.</span></span>

        <span data-ttu-id="013fb-208">✔ Seleccione el vínculo **De edición de usuario autenticado.**</span><span class="sxs-lookup"><span data-stu-id="013fb-208">✔ Select the **Editing role Authenticated user** link.</span></span>

        <span data-ttu-id="013fb-209">✔ Desplázate hacia abajo y busca la capacidad **Crear un token de servicio web** y selecciona la casilla **Permitir.**</span><span class="sxs-lookup"><span data-stu-id="013fb-209">✔ Scroll down and find the **Create a web service token** capability and select the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="013fb-210">3. Implemente el Bot asistente de Moodle en Azure</span><span class="sxs-lookup"><span data-stu-id="013fb-210">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="013fb-211">El bot asistente gratuito de Moodle para Microsoft Teams ayuda a los profesores y estudiantes a responder preguntas sobre sus cursos, tareas, calificaciones y otra información en Moodle.</span><span class="sxs-lookup"><span data-stu-id="013fb-211">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades, and other information in Moodle.</span></span> <span data-ttu-id="013fb-212">El bot también envía notificaciones de Moodle a estudiantes y profesores dentro de Teams.</span><span class="sxs-lookup"><span data-stu-id="013fb-212">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="013fb-213">El bot es un proyecto de código abierto mantenido por Microsoft y está disponible en [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span><span class="sxs-lookup"><span data-stu-id="013fb-213">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
>
> * <span data-ttu-id="013fb-214">Implemente recursos en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="013fb-214">Deploy resources to your Azure subscription.</span></span> <span data-ttu-id="013fb-215">Todos los recursos se configuraron mediante el nivel **gratuito.**</span><span class="sxs-lookup"><span data-stu-id="013fb-215">All resources were configured using the **free** tier.</span></span> <span data-ttu-id="013fb-216">Dependiendo del uso del bot, es posible que tenga que escalar estos recursos.</span><span class="sxs-lookup"><span data-stu-id="013fb-216">Depending on the usage of your bot, you may have to scale these resources.</span></span>
>
> * <span data-ttu-id="013fb-217">Para utilizar la pestaña Moodle sin el bot, vaya a [4](#4-deploy-your-microsoft-teams-app).</span><span class="sxs-lookup"><span data-stu-id="013fb-217">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="013fb-218">Flujo de información del bot Moodle</span><span class="sxs-lookup"><span data-stu-id="013fb-218">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="013fb-219">Para instalar el bot, debe registrarlo en [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span><span class="sxs-lookup"><span data-stu-id="013fb-219">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="013fb-220">Esto permite que el bot se autentique en los puntos de conexión de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="013fb-220">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="013fb-221">**Para registrar el bot**</span><span class="sxs-lookup"><span data-stu-id="013fb-221">**To register your bot**</span></span>

1. <span data-ttu-id="013fb-222">Vaya a la página de administración de plugins y, a continuación, seleccione **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="013fb-222">Go to the plugins administration page, and then select **Plugins**.</span></span> <span data-ttu-id="013fb-223">En **Integración Microsoft 365**, seleccione la pestaña **Teams Configuración.**</span><span class="sxs-lookup"><span data-stu-id="013fb-223">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="013fb-224">Seleccione el vínculo **Portal de registro de aplicaciones de Microsoft** e inicie sesión con su identificador de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="013fb-224">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="013fb-225">Escriba un nombre para la aplicación, como MoodleBot y seleccione el botón **Crear.**</span><span class="sxs-lookup"><span data-stu-id="013fb-225">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="013fb-226">Copie el **ID de aplicación** y péguelo en el campo Bot Application **ID** de la página **Team Configuración.**</span><span class="sxs-lookup"><span data-stu-id="013fb-226">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="013fb-227">Seleccione el botón **Generar nueva contraseña.**</span><span class="sxs-lookup"><span data-stu-id="013fb-227">Select the **Generate New Password** button.</span></span> <span data-ttu-id="013fb-228">Copie la contraseña generada y péguela en el campo **Contraseña de la aplicación bot** de la página Equipo **Configuración.**</span><span class="sxs-lookup"><span data-stu-id="013fb-228">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="013fb-229">Desplázate hasta la parte inferior del formulario y selecciona **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="013fb-229">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="013fb-230">Después de generar el identificador y la contraseña de la aplicación, implemente el bot en Azure:</span><span class="sxs-lookup"><span data-stu-id="013fb-230">After generating your application ID and password, deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="013fb-231">Seleccione **Implementar en Azure** y complete el formulario con la información necesaria, como el identificador de aplicación de bot, la contraseña de la aplicación bot y el secreto de Moodle en la página de **Teams Configuración.**</span><span class="sxs-lookup"><span data-stu-id="013fb-231">Select **Deploy to Azure** and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password, and the Moodle Secret on the **Teams Settings** page.</span></span> <span data-ttu-id="013fb-232">La información de Azure está en la página **Configuración.**</span><span class="sxs-lookup"><span data-stu-id="013fb-232">The Azure information is on the **Setup** page.</span></span> 
> * <span data-ttu-id="013fb-233">Después de completar el formulario, seleccione la casilla de verificación para aceptar los términos y condiciones.</span><span class="sxs-lookup"><span data-stu-id="013fb-233">After completing the form, select the checkbox to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="013fb-234">Seleccione **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="013fb-234">Select **Purchase**.</span></span> <span data-ttu-id="013fb-235">Todos los recursos de Azure se implementan en el nivel gratuito.</span><span class="sxs-lookup"><span data-stu-id="013fb-235">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="013fb-236">Una vez completados los recursos que se implementan en Azure, debe configurar los complementos Microsoft 365 Moodle con un punto de conexión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="013fb-236">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugins with a messaging endpoint.</span></span> <span data-ttu-id="013fb-237">Debe obtener el punto de conexión del bot en Azure:</span><span class="sxs-lookup"><span data-stu-id="013fb-237">You must get the endpoint from your bot in Azure:</span></span>

1. <span data-ttu-id="013fb-238">Inicie sesión en el [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="013fb-238">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="013fb-239">En el panel izquierdo, seleccione **Grupos de recursos** y seleccione el grupo de recursos que usó o creó, al implementar el bot.</span><span class="sxs-lookup"><span data-stu-id="013fb-239">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="013fb-240">Seleccione el recurso Bot de **WebApp** en la lista de recursos del grupo.</span><span class="sxs-lookup"><span data-stu-id="013fb-240">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="013fb-241">Copie el **punto de conexión** de mensajería en la sección Información **general.**</span><span class="sxs-lookup"><span data-stu-id="013fb-241">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="013fb-242">En Moodle, abre la página **de Configuración equipo** de tus plugins de Moodle Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="013fb-242">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugins.</span></span>

1. <span data-ttu-id="013fb-243">En el campo **Punto de conexión de bot,** pegue la dirección URL que acaba de copiar y cambie los *mensajes* de Word al *webhook*.</span><span class="sxs-lookup"><span data-stu-id="013fb-243">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="013fb-244">La dirección URL debe aparecer de la siguiente manera: `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="013fb-244">The URL must appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="013fb-245">Seleccione **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="013fb-245">Select **Save Changes**.</span></span>

1. <span data-ttu-id="013fb-246">Después de guardar los cambios, vuelva a la pestaña **Equipo Configuración,** seleccione el botón **Descargar archivo de manifiesto** y guarde el paquete de manifiesto de la aplicación en el equipo para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="013fb-246">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="013fb-247">4. Implemente la aplicación Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="013fb-247">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="013fb-248">Después de implementar el bot en Azure y configurarse para hablar con el servidor de Moodle, debe implementar la aplicación Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="013fb-248">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="013fb-249">Para ello debe cargar el archivo de manifiesto de la aplicación que descargó desde la página Microsoft 365 Equipo de plugins de Moodle Configuración en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="013fb-249">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugins Team Settings page in the previous step.</span></span>

<span data-ttu-id="013fb-250">Antes de instalar la aplicación debe asegurarse de habilitar aplicaciones externas y cargar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="013fb-250">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="013fb-251">Para obtener más información, consulte [Preparar el inquilino de Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="013fb-251">For more information, see [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span> 

<span data-ttu-id="013fb-252">**Para implementar la aplicación**</span><span class="sxs-lookup"><span data-stu-id="013fb-252">**To deploy your app**</span></span> 

1. <span data-ttu-id="013fb-253">Abra **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="013fb-253">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="013fb-254">Seleccione el icono **Aplicación** en el área inferior izquierda de la barra de navegación.</span><span class="sxs-lookup"><span data-stu-id="013fb-254">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="013fb-255">Seleccione la Upload un vínculo de **aplicación personalizado** de la lista de opciones.</span><span class="sxs-lookup"><span data-stu-id="013fb-255">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="013fb-256">Si ha iniciado sesión como administrador global, debe tener la opción de cargar la aplicación en el catálogo de aplicaciones de su organización, de lo contrario solo puede cargar la aplicación para un equipo en el que sea miembro.</span><span class="sxs-lookup"><span data-stu-id="013fb-256">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="013fb-257">Seleccione el `manifest.zip` paquete que descargó anteriormente y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="013fb-257">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="013fb-258">Si no ha descargado el paquete de manifiesto de la aplicación, puede descargar desde la pestaña **Equipo Configuración** de la página de configuración de plugins en Moodle.</span><span class="sxs-lookup"><span data-stu-id="013fb-258">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugins configuration page in Moodle.</span></span>

<span data-ttu-id="013fb-259">Ahora que tienes instalada la aplicación, puedes agregar la pestaña a cualquier canal al que tengas acceso.</span><span class="sxs-lookup"><span data-stu-id="013fb-259">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="013fb-260">Para ello, vaya al canal, seleccione el símbolo **más** (➕) y seleccione la aplicación de la lista.</span><span class="sxs-lookup"><span data-stu-id="013fb-260">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="013fb-261">Sigue las indicaciones para terminar de agregar la pestaña del curso de Moodle a un canal.</span><span class="sxs-lookup"><span data-stu-id="013fb-261">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="013fb-262">5. Permitir la creación automática de pestañas Moodle en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="013fb-262">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="013fb-263">Aunque las pestañas Moodle se crean manualmente en Microsoft Teams, puede decidir crearlas automáticamente cuando se crean equipos a partir de la sincronización del curso.</span><span class="sxs-lookup"><span data-stu-id="013fb-263">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to create them automatically when teams are created from course synchronization.</span></span> <span data-ttu-id="013fb-264">Para ello, debe configurar el identificador de la aplicación de Microsoft Teams cargada en Moodle.</span><span class="sxs-lookup"><span data-stu-id="013fb-264">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle.</span></span>

<span data-ttu-id="013fb-265">**Para permitir la creación automática de pestañas Moodle**</span><span class="sxs-lookup"><span data-stu-id="013fb-265">**To allow automatic creation of Moodle tabs**</span></span>

1. <span data-ttu-id="013fb-266">Abra Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="013fb-266">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="013fb-267">Seleccione el icono Aplicaciones en el área inferior izquierda de la barra de navegación.</span><span class="sxs-lookup"><span data-stu-id="013fb-267">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="013fb-268">Busque la **aplicación Moodle** cargada > seleccione el icono **de opciones** > seleccione el **vínculo copiar**.</span><span class="sxs-lookup"><span data-stu-id="013fb-268">Locate the uploaded **Moodle app** > select the **options** icon > select **copy link**.</span></span>

1. <span data-ttu-id="013fb-269">En un editor de texto, pegue el contenido copiado.</span><span class="sxs-lookup"><span data-stu-id="013fb-269">In a text editor, paste the copied content.</span></span> <span data-ttu-id="013fb-270">Debe contener una dirección URL como ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span><span class="sxs-lookup"><span data-stu-id="013fb-270">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="013fb-271">Copie la última parte de la dirección URL, como `00112233-4455-6677-8899-aabbccddeeff` , que es el identificador de la aplicación Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="013fb-271">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="013fb-272">En Moodle, abre la pestaña de la **aplicación Teams Moodle** desde tu página de configuración de Microsoft 365 Moodle Plugins.</span><span class="sxs-lookup"><span data-stu-id="013fb-272">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugins configuration page.</span></span>

1. <span data-ttu-id="013fb-273">Pegue el identificador de la aplicación Microsoft Teams en el campo Id.</span><span class="sxs-lookup"><span data-stu-id="013fb-273">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="013fb-274">Cuando se sincroniza un curso de Moodle, Microsoft Teams instala automáticamente la aplicación Moodle en el equipo, crea una pestaña Moodle en el canal General de Teams y la configura para que contenga la página del curso para el curso Moodle desde el que se sincroniza.</span><span class="sxs-lookup"><span data-stu-id="013fb-274">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, creates a Moodle tab in the General channel of Teams, and configures it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="013fb-275">Ahora puede empezar a trabajar con sus cursos de Moodle directamente desde Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="013fb-275">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="013fb-276">Para compartir cualquier solicitud de función o comentario con nosotros, visite nuestra [página de Voz del usuario](https://microsoftteams.uservoice.com/forums/916759-moodle).</span><span class="sxs-lookup"><span data-stu-id="013fb-276">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="013fb-277">Vea también</span><span class="sxs-lookup"><span data-stu-id="013fb-277">See also</span></span>

- [<span data-ttu-id="013fb-278">Integrar aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="013fb-278">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
- [<span data-ttu-id="013fb-279">Moodle</span><span class="sxs-lookup"><span data-stu-id="013fb-279">Moodle</span></span>](https://moodle.org/)
- <span data-ttu-id="013fb-280">[Documentación de Moodle](https://docs.moodle.org/34/en/Installing_plugins).</span><span class="sxs-lookup"><span data-stu-id="013fb-280">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>

