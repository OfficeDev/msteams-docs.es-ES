---
title: Cree un canal personalizado y agrupalice tabulador con Node.js y el generador Yeoman para Microsoft Teams
author: laujan
description: Una guía de inicio rápido para crear un canal y una pestaña de grupo con el generador Yeoman para Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 559393884e3b8a4aad1787ea4ca8f9f4de54d151
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566651"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="454f6-103">Cree una pestaña de canal y grupo personalizada con Node.js y el generador Yeoman para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="454f6-103">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="454f6-104">Esta guía de inicio rápido sigue los pasos descritos en la wiki [de compilación de la primera aplicación Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) que se encuentra en el repositorio de microsoft officedev GitHub.</span><span class="sxs-lookup"><span data-stu-id="454f6-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="454f6-105">En esta guía de inicio rápido vamos a caminar a través de la creación de un canal personalizado y la pestaña de grupo utilizando el [generador de Teams Yeoman](https://github.com/OfficeDev/generator-teams/).</span><span class="sxs-lookup"><span data-stu-id="454f6-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="454f6-106">**¿Desea crear una pestaña configurable o estática?**</span><span class="sxs-lookup"><span data-stu-id="454f6-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="454f6-107">Utilice las teclas de flecha para seleccionar la pestaña configurable.</span><span class="sxs-lookup"><span data-stu-id="454f6-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="454f6-108">**¿Qué ámbitos tiene la intención de usar para su pestaña?**</span><span class="sxs-lookup"><span data-stu-id="454f6-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="454f6-109">Puede seleccionar un equipo y/o un chat de grupo</span><span class="sxs-lookup"><span data-stu-id="454f6-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="454f6-110">**¿Desea que esta pestaña esté disponible en SharePoint Online? (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="454f6-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="454f6-111">Seleccione **n**.</span><span class="sxs-lookup"><span data-stu-id="454f6-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="454f6-112">El componente de ruta de acceso al que se hace referencia **suDefaultTabNameTab**, al que se hace referencia en esta guía de inicio rápido, es el valor que ha introducido en el generador de **Nombre de tabulación predeterminado** más la **pestaña** Word .</span><span class="sxs-lookup"><span data-stu-id="454f6-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="454f6-113">Por ejemplo: DefaultTabName: **MyTab**  =>  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="454f6-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="454f6-114">En el directorio del proyecto, vaya a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="454f6-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="454f6-115">Ahí es donde encontrarás la lógica de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="454f6-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="454f6-116">Busque el `render()` método y agregue la siguiente etiqueta y contenido a la parte superior del código `<div>` `<PanelBody>` contenedor:</span><span class="sxs-lookup"><span data-stu-id="454f6-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="454f6-117">Asegúrese de guardar el archivo actualizado.</span><span class="sxs-lookup"><span data-stu-id="454f6-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="454f6-118">Compile y ejecute su aplicación</span><span class="sxs-lookup"><span data-stu-id="454f6-118">Build and Run Your Application</span></span>

<span data-ttu-id="454f6-119">Abra un símbolo del sistema en el directorio del proyecto para completar las siguientes tareas.</span><span class="sxs-lookup"><span data-stu-id="454f6-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="454f6-120">Para ver la página de configuración de la pestaña vaya a `https://localhost:3007/<yourDefaultAppNameTab>/config.html` .</span><span class="sxs-lookup"><span data-stu-id="454f6-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="454f6-121">Debería ver lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="454f6-121">You should see the following:</span></span>

![captura de pantalla de la página de configuración](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="454f6-123">Establezca un túnel seguro a su lengüeta</span><span class="sxs-lookup"><span data-stu-id="454f6-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="454f6-124">Microsoft Teams es un producto completamente basado en la nube y requiere que el contenido de la pestaña esté disponible en la nube mediante puntos de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="454f6-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="454f6-125">Teams no permite el hospedaje local, por lo tanto, debe publicar la pestaña en una dirección URL pública o usar un proxy que expondrá su puerto local a una DIRECCIÓN URL orientada a Internet.</span><span class="sxs-lookup"><span data-stu-id="454f6-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="454f6-126">Para probar la extensión de la pestaña, usará [ngrok](https://ngrok.com/docs), que está integrado en esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="454f6-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="454f6-127">Ngrok es una herramienta de software proxy inverso que creará un túnel para los puntos de conexión HTTPS disponibles públicamente del servidor web.</span><span class="sxs-lookup"><span data-stu-id="454f6-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="454f6-128">Los puntos de conexión web del servidor estarán disponibles durante la sesión actual en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="454f6-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="454f6-129">Cuando la máquina está apagada o se va a dormir, el servicio ya no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="454f6-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="454f6-130">En el símbolo del sistema, salga de localhost e introduzca lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="454f6-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="454f6-131">Una vez que la pestaña se haya cargado en equipos de Microsoft y se haya guardado correctamente, puede verla en la galería de pestañas, agregarla a la barra de pestañas e interactuar con ella hasta que finalice la sesión del túnel de ngrok.</span><span class="sxs-lookup"><span data-stu-id="454f6-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="454f6-132">Si reinicias la sesión de ngrok, deberás actualizar la aplicación con la nueva DIRECCIÓN URL.</span><span class="sxs-lookup"><span data-stu-id="454f6-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="454f6-133">Upload la aplicación para Teams</span><span class="sxs-lookup"><span data-stu-id="454f6-133">Upload your application to Teams</span></span>

- <span data-ttu-id="454f6-134">Abra el cliente Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="454f6-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="454f6-135">Si utiliza la [versión basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end utilizando las herramientas para [desarrolladores](~/tabs/how-to/developer-tools.md)de su navegador.</span><span class="sxs-lookup"><span data-stu-id="454f6-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="454f6-136">En el panel *Tus comamos de* la izquierda, selecciona el menú situado junto al equipo que `...` usas para probar tu pestaña y selecciona **Administrar equipo.**</span><span class="sxs-lookup"><span data-stu-id="454f6-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="454f6-137">En el panel principal, seleccione **Aplicaciones** en la barra de pestañas y elija **Upload una aplicación personalizada** ubicada en la esquina inferior derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="454f6-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="454f6-138">Abra el directorio del proyecto, vaya a la carpeta **./package,** seleccione la carpeta zip del paquete de la aplicación y elija **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="454f6-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="454f6-139">La pestaña se cargará en Teams.</span><span class="sxs-lookup"><span data-stu-id="454f6-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="454f6-140">Vuelve a tu equipo, elige el canal donde quieres mostrar la pestaña, selecciona ➕ en la barra de pestañas y elige tu pestaña en la galería.</span><span class="sxs-lookup"><span data-stu-id="454f6-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="454f6-141">Siga las instrucciones para agregar una pestaña. Tenga en cuenta que hay un cuadro de diálogo de configuración personalizado para la pestaña canal/grupo.</span><span class="sxs-lookup"><span data-stu-id="454f6-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="454f6-142">Selecciona **Guardar** y la pestaña se agregará a la barra de pestañas del canal.</span><span class="sxs-lookup"><span data-stu-id="454f6-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>

## <a name="next-step"></a><span data-ttu-id="454f6-143">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="454f6-143">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="454f6-144">Cree una pestaña de canal y grupo personalizado con ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="454f6-144">Create a Custom Channel and Group Tab with ASP.NETCore</span></span>](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)