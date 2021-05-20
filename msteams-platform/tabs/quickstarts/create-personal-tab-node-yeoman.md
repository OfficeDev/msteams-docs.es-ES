---
title: 'Inicio rápido: Crea una pestaña personal personalizada con Node.js y el generador Yeoman para Microsoft Teams'
author: laujan
description: Una guía de inicio rápido para crear una pestaña personal con el generador Yeoman para Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 88ad05aacaed69d695bc918e3e8a44ec18e560ae
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566612"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="04ace-103">Cree una pestaña personal personalizada con Node.js y el generador Yeoman para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="04ace-103">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="04ace-104">Esta guía de inicio rápido sigue los pasos descritos en la wiki [de compilación de la primera aplicación Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) que se encuentra en el repositorio de microsoft officedev GitHub.</span><span class="sxs-lookup"><span data-stu-id="04ace-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="04ace-105">En esta guía de inicio rápido vamos a caminar a través de la creación de una pestaña personal personalizada utilizando el [generador de Teams Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="04ace-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="04ace-106">También subiremos la aplicación al equipo.</span><span class="sxs-lookup"><span data-stu-id="04ace-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="04ace-107">**Crear una pestaña configurable o estática**</span><span class="sxs-lookup"><span data-stu-id="04ace-107">**Create a configurable or static tab**</span></span>

<span data-ttu-id="04ace-108">Utilice las teclas de flecha para seleccionar la pestaña estática.</span><span class="sxs-lookup"><span data-stu-id="04ace-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="04ace-109">El componente de ruta de acceso al que se hace referencia *suDefaultTabNameTab*, al que se hace referencia en esta guía de inicio rápido, es el valor que ha introducido en el generador de *Nombre de tabulación predeterminado* más la *pestaña* Word .</span><span class="sxs-lookup"><span data-stu-id="04ace-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="04ace-110">Por ejemplo: DefaultTabName: *MyTab*  =>  */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="04ace-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="04ace-111">Crea tu pestaña personal</span><span class="sxs-lookup"><span data-stu-id="04ace-111">Create your personal tab</span></span>

<span data-ttu-id="04ace-112">Para agregar una pestaña personal a esta aplicación creará una página de contenido y actualizará los archivos existentes:</span><span class="sxs-lookup"><span data-stu-id="04ace-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="04ace-113">En el editor de código, cree un nuevo archivo HTML, **personal.html** y agregue el siguiente marcado:</span><span class="sxs-lookup"><span data-stu-id="04ace-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

- <span data-ttu-id="04ace-114">Guarde **personal.html** en la carpeta **web** de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="04ace-114">Save **personal.html** in your application's **web** folder:</span></span>

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- <span data-ttu-id="04ace-115">Abramanifest.jsen **el** editor de código:</span><span class="sxs-lookup"><span data-stu-id="04ace-115">Open **manifest.json** in your code editor:</span></span>

    ```bash
    ./src/manifest/manifest.json/
    ```

<span data-ttu-id="04ace-116">Agregue lo siguiente a la matriz vacía `staticTabs` ( ) y agregue el siguiente objeto `staticTabs":[]` JSON:</span><span class="sxs-lookup"><span data-stu-id="04ace-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="04ace-117">Recuerde actualizar el componente de ruta de acceso **"contentURL"** **yourDefaultTabNameTab** con su nombre de pestaña real.</span><span class="sxs-lookup"><span data-stu-id="04ace-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="04ace-118">Guarde lamanifest.jsactualizada **en**.</span><span class="sxs-lookup"><span data-stu-id="04ace-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="04ace-119">La página de contenido debe servirse en un IFrame.</span><span class="sxs-lookup"><span data-stu-id="04ace-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="04ace-120">Abra **Tab.ts** en el editor de código:</span><span class="sxs-lookup"><span data-stu-id="04ace-120">Open **Tab.ts** in your code editor:</span></span>

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- <span data-ttu-id="04ace-121">Agregue lo siguiente a la lista de decoradores de IFrame:</span><span class="sxs-lookup"><span data-stu-id="04ace-121">Add the following to the list of IFrame decorators:</span></span>

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- <span data-ttu-id="04ace-122">Asegúrese de guardar el archivo **Tab.ts** actualizado.</span><span class="sxs-lookup"><span data-stu-id="04ace-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="04ace-123">El código de la pestaña está completo.</span><span class="sxs-lookup"><span data-stu-id="04ace-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="04ace-124">Compile y ejecute su aplicación</span><span class="sxs-lookup"><span data-stu-id="04ace-124">Build and Run Your Application</span></span>

<span data-ttu-id="04ace-125">Abra un símbolo del sistema en el directorio del proyecto para completar las siguientes tareas.</span><span class="sxs-lookup"><span data-stu-id="04ace-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="04ace-126">Para ver tu pestaña personal, ve a `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="04ace-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![captura de pantalla de pestaña personal](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="04ace-128">Establezca un túnel seguro a su lengüeta</span><span class="sxs-lookup"><span data-stu-id="04ace-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="04ace-129">Microsoft Teams es un producto completamente basado en la nube y requiere que el contenido de la pestaña esté disponible en la nube mediante puntos de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="04ace-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="04ace-130">Teams no permite el hospedaje local, por lo tanto, debe publicar la pestaña en una dirección URL pública o usar un proxy que expondrá su puerto local a una DIRECCIÓN URL orientada a Internet.</span><span class="sxs-lookup"><span data-stu-id="04ace-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="04ace-131">Para probar la extensión de la pestaña, usará [ngrok](https://ngrok.com/docs), que está integrado en esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="04ace-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="04ace-132">Ngrok es una herramienta de software proxy inverso que creará un túnel para los puntos de conexión HTTPS disponibles públicamente del servidor web.</span><span class="sxs-lookup"><span data-stu-id="04ace-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="04ace-133">Los puntos de conexión web del servidor estarán disponibles durante la sesión actual en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="04ace-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="04ace-134">Cuando la máquina está apagada o se va a dormir, el servicio ya no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="04ace-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="04ace-135">En el símbolo del sistema, salga de localhost e introduzca lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="04ace-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="04ace-136">Una vez que la pestaña se haya cargado en equipos de Microsoft, a través de **ngrok** y guardada correctamente, puede verla en Teams hasta que finalice la sesión del túnel.</span><span class="sxs-lookup"><span data-stu-id="04ace-136">After your tab has been uploaded to Microsoft teams, via **ngrok**, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="04ace-137">Upload la aplicación para Teams</span><span class="sxs-lookup"><span data-stu-id="04ace-137">Upload your application to Teams</span></span>

- <span data-ttu-id="04ace-138">Abra el cliente Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="04ace-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="04ace-139">Si utiliza la [versión basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end utilizando las herramientas para [desarrolladores](~/tabs/how-to/developer-tools.md)de su navegador.</span><span class="sxs-lookup"><span data-stu-id="04ace-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="04ace-140">En el panel **Tus comamos de** la izquierda, selecciona el menú situado junto al equipo que `...` usas para probar tu pestaña y selecciona **Administrar equipo.**</span><span class="sxs-lookup"><span data-stu-id="04ace-140">In the **YourTeams** panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="04ace-141">En el panel principal, seleccione **Aplicaciones** en la barra de pestañas y elija **Upload una aplicación personalizada** ubicada en la esquina inferior derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="04ace-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="04ace-142">Abra el directorio del proyecto, vaya a la carpeta **./package,** seleccione la carpeta zip, haga clic con el botón derecho y elija **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="04ace-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="04ace-143">La pestaña se cargará en Teams.</span><span class="sxs-lookup"><span data-stu-id="04ace-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="04ace-144">Ver sus pestañas personales</span><span class="sxs-lookup"><span data-stu-id="04ace-144">View your personal tabs</span></span>

<span data-ttu-id="04ace-145">En la barra de navegación situada a la izquierda del cliente Teams, seleccione el `...` menú y elija la aplicación de la lista.</span><span class="sxs-lookup"><span data-stu-id="04ace-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>

## <a name="next-step"></a><span data-ttu-id="04ace-146">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="04ace-146">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04ace-147">Cree una pestaña personal con ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="04ace-147">Create a personal tab using ASP.NETCore</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
