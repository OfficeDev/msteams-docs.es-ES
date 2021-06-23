---
title: Crear un canal personalizado y una pestaña de grupo con Node.js y el generador de Yeoman para Microsoft Teams
author: surbhigupta
description: Guía de inicio rápido para crear una pestaña de canal y grupo con el Generador de Yeoman para Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 6b3b5e513f91afae47364c37eb2b037a13438d35
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069113"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="ce10b-103">Cree una pestaña de canal y grupo personalizada con Node.js y el generador de Yeoman para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ce10b-103">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="ce10b-104">Esta guía de inicio rápido sigue los pasos descritos en el wiki crear la primera [aplicación](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Microsoft Teams que se encuentra en el repositorio GitHub Microsoft OfficeDev.</span><span class="sxs-lookup"><span data-stu-id="ce10b-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="ce10b-105">En esta guía de inicio rápido, crearemos un canal personalizado y una pestaña de grupo con el generador [de Yeoman Teams de Yeoman.](https://github.com/OfficeDev/generator-teams/)</span><span class="sxs-lookup"><span data-stu-id="ce10b-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="ce10b-106">**¿Desea crear una pestaña configurable o estática?**</span><span class="sxs-lookup"><span data-stu-id="ce10b-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="ce10b-107">Use las teclas de flecha para seleccionar la pestaña configurable.</span><span class="sxs-lookup"><span data-stu-id="ce10b-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="ce10b-108">**¿Qué ámbitos tiene previsto usar para la pestaña?**</span><span class="sxs-lookup"><span data-stu-id="ce10b-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="ce10b-109">Puede seleccionar un equipo o un chat de grupo</span><span class="sxs-lookup"><span data-stu-id="ce10b-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="ce10b-110">**¿Desea que esta pestaña esté disponible en SharePoint Online? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="ce10b-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="ce10b-111">Seleccione **n**.</span><span class="sxs-lookup"><span data-stu-id="ce10b-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="ce10b-112">El componente de ruta de acceso **yourDefaultTabNameTab**, al que se hace referencia en esta guía de inicio rápido, es el valor que escribió en el generador para **Default Tab Name** más la palabra **Tab**.</span><span class="sxs-lookup"><span data-stu-id="ce10b-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="ce10b-113">Por ejemplo: DefaultTabName: **MyTab**  =>  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="ce10b-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="ce10b-114">En el directorio del proyecto, vaya a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ce10b-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="ce10b-115">Ahí es donde encontrará la lógica de tabulación.</span><span class="sxs-lookup"><span data-stu-id="ce10b-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="ce10b-116">Busque el `render()` método y agregue la siguiente etiqueta y contenido a la parte superior del código `<div>` `<PanelBody>` contenedor:</span><span class="sxs-lookup"><span data-stu-id="ce10b-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="ce10b-117">Asegúrese de guardar el archivo actualizado.</span><span class="sxs-lookup"><span data-stu-id="ce10b-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="ce10b-118">Crear y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="ce10b-118">Build and Run Your Application</span></span>

<span data-ttu-id="ce10b-119">Abra un símbolo del sistema en el directorio del proyecto para completar las siguientes tareas.</span><span class="sxs-lookup"><span data-stu-id="ce10b-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="ce10b-120">Para ver la página de configuración de pestañas, vaya a `https://localhost:3007/<yourDefaultAppNameTab>/config.html` .</span><span class="sxs-lookup"><span data-stu-id="ce10b-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="ce10b-121">Debería ver lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ce10b-121">You should see the following:</span></span>

![captura de pantalla de página de configuración](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="ce10b-123">Establecer un túnel seguro en la pestaña</span><span class="sxs-lookup"><span data-stu-id="ce10b-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="ce10b-124">Microsoft Teams es un producto totalmente basado en la nube y requiere que el contenido de la pestaña esté disponible desde la nube mediante puntos de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ce10b-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="ce10b-125">Teams no permite el hospedaje local, por lo tanto, debe publicar la pestaña en una dirección URL pública o usar un proxy que exponga el puerto local a una dirección URL orientada a Internet.</span><span class="sxs-lookup"><span data-stu-id="ce10b-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="ce10b-126">Para probar la extensión de pestaña, usará [ngrok](https://ngrok.com/docs), que está integrado en esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="ce10b-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="ce10b-127">Ngrok es una herramienta de software de proxy inverso que creará un túnel para los puntos de conexión HTTPS del servidor web que se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="ce10b-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="ce10b-128">Los puntos de conexión web del servidor estarán disponibles durante la sesión actual en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="ce10b-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="ce10b-129">Cuando la máquina se apaga o se queda en modo de suspensión, el servicio ya no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="ce10b-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="ce10b-130">En el símbolo del sistema, salga de localhost y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ce10b-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="ce10b-131">Después de cargar la pestaña en Microsoft teams y guardarla correctamente, puede verlo en la galería de pestañas, agregarla a la barra de pestañas e interactuar con ella hasta que finalice la sesión del túnel ngrok.</span><span class="sxs-lookup"><span data-stu-id="ce10b-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="ce10b-132">Si reinicias la sesión de ngrok, tendrás que actualizar la aplicación con la nueva dirección URL.</span><span class="sxs-lookup"><span data-stu-id="ce10b-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="ce10b-133">Upload la aplicación a Teams</span><span class="sxs-lookup"><span data-stu-id="ce10b-133">Upload your application to Teams</span></span>

- <span data-ttu-id="ce10b-134">Abra el Microsoft Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="ce10b-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="ce10b-135">Si usa la versión [basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end con las herramientas de desarrollo [del explorador.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="ce10b-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="ce10b-136">En el panel *YourTeams* de la izquierda, seleccione el menú situado junto al equipo que está usando para probar la pestaña y `...` elija Administrar **equipo**.</span><span class="sxs-lookup"><span data-stu-id="ce10b-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="ce10b-137">En el panel principal, selecciona **Aplicaciones** en la barra de pestañas y Upload **una** aplicación personalizada ubicada en la esquina inferior derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="ce10b-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="ce10b-138">Abra el directorio del proyecto, vaya a **la carpeta ./package,** seleccione la carpeta zip del paquete de la aplicación y elija **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="ce10b-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="ce10b-139">La pestaña se cargará en Teams.</span><span class="sxs-lookup"><span data-stu-id="ce10b-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="ce10b-140">Vuelva a su equipo, elija el canal en el que desea mostrar la pestaña, seleccione ➕ en la barra de pestañas y elija la pestaña de la galería.</span><span class="sxs-lookup"><span data-stu-id="ce10b-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="ce10b-141">Siga las instrucciones para agregar una pestaña. Tenga en cuenta que hay un cuadro de diálogo de configuración personalizado para la pestaña canal o grupo.</span><span class="sxs-lookup"><span data-stu-id="ce10b-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="ce10b-142">Selecciona **Guardar** y la pestaña se agregará a la barra de pestañas del canal.</span><span class="sxs-lookup"><span data-stu-id="ce10b-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>

## <a name="next-step"></a><span data-ttu-id="ce10b-143">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="ce10b-143">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ce10b-144">Crear un canal personalizado y una pestaña de grupo con ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="ce10b-144">Create a Custom Channel and Group Tab with ASP.NETCore</span></span>](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)
