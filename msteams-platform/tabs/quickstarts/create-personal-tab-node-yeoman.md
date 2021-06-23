---
title: 'Inicio rápido: cree una pestaña personal personalizada con Node.js y el generador de Yeoman para Microsoft Teams'
author: surbhigupta
description: Guía de inicio rápido para crear una pestaña personal con el Generador de Yeoman para Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 220d1018f174fc935a10311723a730ebc74ccc33
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069200"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="b7701-103">Crear una pestaña personal personalizada con Node.js y el generador de Yeoman para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b7701-103">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="b7701-104">Esta guía de inicio rápido sigue los pasos descritos en el wiki crear la primera [aplicación](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Microsoft Teams que se encuentra en el repositorio GitHub Microsoft OfficeDev.</span><span class="sxs-lookup"><span data-stu-id="b7701-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="b7701-105">En esta guía de inicio rápido crearemos una pestaña personal personalizada con [el generador de Yeoman Teams de Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="b7701-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="b7701-106">También cargaremos la aplicación en Team.</span><span class="sxs-lookup"><span data-stu-id="b7701-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="b7701-107">**Crear una pestaña configurable o estática**</span><span class="sxs-lookup"><span data-stu-id="b7701-107">**Create a configurable or static tab**</span></span>

<span data-ttu-id="b7701-108">Use las teclas de flecha para seleccionar la pestaña estática.</span><span class="sxs-lookup"><span data-stu-id="b7701-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b7701-109">El componente de ruta de acceso *yourDefaultTabNameTab*, al que se hace referencia en esta guía de inicio rápido, es el valor que escribió en el generador para *Default Tab Name* más la palabra *Tab*.</span><span class="sxs-lookup"><span data-stu-id="b7701-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="b7701-110">Por ejemplo: DefaultTabName: *MyTab*  =>  */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="b7701-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="b7701-111">Crear la pestaña personal</span><span class="sxs-lookup"><span data-stu-id="b7701-111">Create your personal tab</span></span>

<span data-ttu-id="b7701-112">Para agregar una pestaña personal a esta aplicación, creará una página de contenido y actualizará los archivos existentes:</span><span class="sxs-lookup"><span data-stu-id="b7701-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="b7701-113">En el editor de código, cree un nuevo archivo HTML, **personal.html** y agregue el siguiente marcado:</span><span class="sxs-lookup"><span data-stu-id="b7701-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="b7701-114">Guarde **personal.html** en la carpeta web de **la** aplicación:</span><span class="sxs-lookup"><span data-stu-id="b7701-114">Save **personal.html** in your application's **web** folder:</span></span>

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- <span data-ttu-id="b7701-115">Abra **manifest.jsen** el editor de código:</span><span class="sxs-lookup"><span data-stu-id="b7701-115">Open **manifest.json** in your code editor:</span></span>

    ```bash
    ./src/manifest/manifest.json/
    ```

<span data-ttu-id="b7701-116">Agregue lo siguiente a la matriz `staticTabs` vacía ( ) y agregue el siguiente objeto `staticTabs":[]` JSON:</span><span class="sxs-lookup"><span data-stu-id="b7701-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="b7701-117">Recuerde actualizar el componente de ruta **de acceso "contentURL"** **yourDefaultTabNameTab** con el nombre de la pestaña real.</span><span class="sxs-lookup"><span data-stu-id="b7701-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="b7701-118">Guarde el archivo **manifest.jsen**.</span><span class="sxs-lookup"><span data-stu-id="b7701-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="b7701-119">La página de contenido debe servirse en un IFrame.</span><span class="sxs-lookup"><span data-stu-id="b7701-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="b7701-120">Abra **Tab.ts en** el editor de código:</span><span class="sxs-lookup"><span data-stu-id="b7701-120">Open **Tab.ts** in your code editor:</span></span>

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- <span data-ttu-id="b7701-121">Agregue lo siguiente a la lista de decoradores de IFrame:</span><span class="sxs-lookup"><span data-stu-id="b7701-121">Add the following to the list of IFrame decorators:</span></span>

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- <span data-ttu-id="b7701-122">Asegúrese de guardar el archivo **Tab.ts actualizado.**</span><span class="sxs-lookup"><span data-stu-id="b7701-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="b7701-123">El código de pestaña se ha completado.</span><span class="sxs-lookup"><span data-stu-id="b7701-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="b7701-124">Crear y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="b7701-124">Build and Run Your Application</span></span>

<span data-ttu-id="b7701-125">Abra un símbolo del sistema en el directorio del proyecto para completar las siguientes tareas.</span><span class="sxs-lookup"><span data-stu-id="b7701-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="b7701-126">Para ver la pestaña personal, vaya a `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="b7701-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![captura de pantalla de pestaña personal](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="b7701-128">Establecer un túnel seguro en la pestaña</span><span class="sxs-lookup"><span data-stu-id="b7701-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="b7701-129">Microsoft Teams es un producto totalmente basado en la nube y requiere que el contenido de la pestaña esté disponible desde la nube mediante puntos de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b7701-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="b7701-130">Teams no permite el hospedaje local, por lo tanto, debe publicar la pestaña en una dirección URL pública o usar un proxy que exponga el puerto local a una dirección URL orientada a Internet.</span><span class="sxs-lookup"><span data-stu-id="b7701-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="b7701-131">Para probar la extensión de pestaña, usará [ngrok](https://ngrok.com/docs), que está integrado en esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7701-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="b7701-132">Ngrok es una herramienta de software de proxy inverso que creará un túnel para los puntos de conexión HTTPS del servidor web que se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="b7701-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="b7701-133">Los puntos de conexión web del servidor estarán disponibles durante la sesión actual en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="b7701-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="b7701-134">Cuando la máquina se apaga o se queda en modo de suspensión, el servicio ya no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="b7701-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="b7701-135">En el símbolo del sistema, salga de localhost y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b7701-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="b7701-136">Después de cargar la pestaña en Microsoft teams, a través de **ngrok** y guardarla correctamente, puede verlo en Teams hasta que finalice la sesión de túnel.</span><span class="sxs-lookup"><span data-stu-id="b7701-136">After your tab has been uploaded to Microsoft teams, via **ngrok**, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="b7701-137">Upload la aplicación a Teams</span><span class="sxs-lookup"><span data-stu-id="b7701-137">Upload your application to Teams</span></span>

- <span data-ttu-id="b7701-138">Abra el Microsoft Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="b7701-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="b7701-139">Si usa la versión [basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end con las herramientas de desarrollo [del explorador.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="b7701-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="b7701-140">En el panel **YourTeams** de la izquierda, seleccione el menú situado junto al equipo que está usando para probar la pestaña y `...` elija Administrar **equipo**.</span><span class="sxs-lookup"><span data-stu-id="b7701-140">In the **YourTeams** panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="b7701-141">En el panel principal, selecciona **Aplicaciones** en la barra de pestañas y Upload **una** aplicación personalizada ubicada en la esquina inferior derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="b7701-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="b7701-142">Abra el directorio del proyecto, vaya a **la carpeta ./package,** seleccione la carpeta zip, haga clic con el botón secundario y elija **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="b7701-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="b7701-143">La pestaña se cargará en Teams.</span><span class="sxs-lookup"><span data-stu-id="b7701-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="b7701-144">Ver las pestañas personales</span><span class="sxs-lookup"><span data-stu-id="b7701-144">View your personal tabs</span></span>

<span data-ttu-id="b7701-145">En la barra de navegación situada en el extremo izquierdo del cliente Teams, seleccione el menú y elija la `...` aplicación de la lista.</span><span class="sxs-lookup"><span data-stu-id="b7701-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>

## <a name="next-step"></a><span data-ttu-id="b7701-146">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="b7701-146">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b7701-147">Crear una pestaña personal con ASP.NETCore</span><span class="sxs-lookup"><span data-stu-id="b7701-147">Create a personal tab using ASP.NETCore</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
