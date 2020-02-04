---
title: 'Inicio rápido: crear una pestaña personal personalizada con node. js y el generador de Yeoman para Microsoft Teams'
author: laujan
description: Una guía de inicio rápido para crear una pestaña personal con el generador de Yeoman para Microsoft Teams.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 2d1b17360b92a161179091c1f6ba06ffa194e958
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675704"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="f5be5-103">Inicio rápido: crear una pestaña personal personalizada con node. js y el generador de Yeoman para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f5be5-103">Quickstart: Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="f5be5-104">En este tutorial, se siguen los pasos descritos en el sitio de creación de la [primera aplicación Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) wiki que se encuentra en el repositorio de github de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f5be5-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="f5be5-105">En este tutorial rápido, vamos a crear una pestaña personal personalizada mediante el [generador Yeoman de Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span><span class="sxs-lookup"><span data-stu-id="f5be5-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="f5be5-106">También cargaremos la aplicación en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f5be5-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="f5be5-107">**¿Desea crear una pestaña configurable o una etiqueta estática?**</span><span class="sxs-lookup"><span data-stu-id="f5be5-107">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="f5be5-108">Use las teclas de dirección para seleccionar la pestaña estática.</span><span class="sxs-lookup"><span data-stu-id="f5be5-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f5be5-109">El componente de ruta de *yourDefaultTabNameTab*, al que se hace referencia en este tutorial rápido, es el valor que escribió en el generador para el nombre de la *pestaña predeterminada* más la *pestaña*de Word.</span><span class="sxs-lookup"><span data-stu-id="f5be5-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="f5be5-110">Por ejemplo: DefaultTabName: *MyTab* => */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="f5be5-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="f5be5-111">Crear una pestaña personal</span><span class="sxs-lookup"><span data-stu-id="f5be5-111">Create your personal tab</span></span>

<span data-ttu-id="f5be5-112">Para agregar una pestaña personal a esta aplicación, deberá crear una página de contenido y actualizar los archivos existentes:</span><span class="sxs-lookup"><span data-stu-id="f5be5-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="f5be5-113">En el editor de código, cree un nuevo archivo HTML, **personal. html** y agregue el siguiente marcado:</span><span class="sxs-lookup"><span data-stu-id="f5be5-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="f5be5-114">Guarde **personal. html** en la carpeta **Web** de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="f5be5-114">Save **personal.html** in your application's **web** folder:</span></span>

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- <span data-ttu-id="f5be5-115">Abra **manifest. JSON** en el editor de código:</span><span class="sxs-lookup"><span data-stu-id="f5be5-115">Open **manifest.json** in your code editor:</span></span>

```bash
./src/manifest/manifest.json/
```

<span data-ttu-id="f5be5-116">Agregue lo siguiente a la matriz `staticTabs` vacía (`staticTabs":[]`) y agregue el siguiente objeto JSON:</span><span class="sxs-lookup"><span data-stu-id="f5be5-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="f5be5-117">Recuerde actualizar el componente de ruta **"contentURL"** **yourDefaultTabNameTab** con el nombre de la pestaña real.</span><span class="sxs-lookup"><span data-stu-id="f5be5-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="f5be5-118">Guarde el **manifiesto manifest. JSON**actualizado.</span><span class="sxs-lookup"><span data-stu-id="f5be5-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="f5be5-119">La página de contenido debe atenderse en un IFrame.</span><span class="sxs-lookup"><span data-stu-id="f5be5-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="f5be5-120">Abra la **pestaña. ts** en el editor de código:</span><span class="sxs-lookup"><span data-stu-id="f5be5-120">Open **Tab.ts** in your code editor:</span></span>

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- <span data-ttu-id="f5be5-121">Agregue lo siguiente a la lista de decoradores IFrame:</span><span class="sxs-lookup"><span data-stu-id="f5be5-121">Add the following to the list of IFrame decorators:</span></span>

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- <span data-ttu-id="f5be5-122">Asegúrese de guardar el archivo **Tab. ts** actualizado.</span><span class="sxs-lookup"><span data-stu-id="f5be5-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="f5be5-123">El código de pestaña está completo.</span><span class="sxs-lookup"><span data-stu-id="f5be5-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="f5be5-124">Compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="f5be5-124">Build and Run Your Application</span></span>

<span data-ttu-id="f5be5-125">Abra un símbolo del sistema en el directorio del proyecto para completar las tareas siguientes.</span><span class="sxs-lookup"><span data-stu-id="f5be5-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="f5be5-126">Para ver tu pestaña personal, ve a`http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="f5be5-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![captura de pantalla de pestaña personal](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="f5be5-128">Establecer un túnel seguro a la pestaña</span><span class="sxs-lookup"><span data-stu-id="f5be5-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="f5be5-129">Microsoft Teams es un producto basado en la nube completamente y requiere que el contenido de la pestaña esté disponible en la nube con puntos de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f5be5-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="f5be5-130">Teams no permite el hospedaje local, por lo tanto, debe publicar su ficha en una dirección URL pública o usar un proxy que expondrá el puerto local a una dirección URL con conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="f5be5-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="f5be5-131">Para probar la extensión de pestañas, usará [ngrok](https://ngrok.com/docs), que está integrado en esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5be5-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="f5be5-132">Ngrok es una herramienta de software de proxy inverso que creará un túnel a los puntos de conexión HTTPS disponibles públicamente del servidor Web que se ejecutan de forma local.</span><span class="sxs-lookup"><span data-stu-id="f5be5-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="f5be5-133">Los puntos de conexión web del servidor estarán disponibles durante la sesión actual en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="f5be5-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="f5be5-134">Cuando el equipo se apaga o entra en suspensión, el servicio dejará de estar disponible.</span><span class="sxs-lookup"><span data-stu-id="f5be5-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="f5be5-135">En el símbolo del sistema, salga de localhost y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5be5-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="f5be5-136">Una vez que se haya cargado la pestaña en Microsoft Teams, a través de *ngrok*, y se haya guardado correctamente, podrá verla en Teams hasta que finalice la sesión de túnel.</span><span class="sxs-lookup"><span data-stu-id="f5be5-136">After your tab has been uploaded to Microsoft teams, via *ngrok*, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="f5be5-137">Cargar la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="f5be5-137">Upload your application to Teams</span></span>

- <span data-ttu-id="f5be5-138">Abra el cliente de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f5be5-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="f5be5-139">Si usa la [versión basada en Web](https://teams.microsoft.com) , puede inspeccionar el código Front-end con las [herramientas de desarrollo](~/tabs/how-to/developer-tools.md)de su explorador.</span><span class="sxs-lookup"><span data-stu-id="f5be5-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="f5be5-140">En el panel de *YourTeams* de la izquierda, seleccione `...` el menú situado junto al equipo que está usando para probar la pestaña y elija **administrar equipo**.</span><span class="sxs-lookup"><span data-stu-id="f5be5-140">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="f5be5-141">En el panel principal, seleccione **aplicaciones** en la barra de pestañas y elija **cargar una aplicación personalizada** ubicada en la esquina inferior derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="f5be5-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="f5be5-142">Abra el directorio del proyecto, vaya a la carpeta **./Package** , seleccione la carpeta ZIP, haga clic con el botón secundario y elija **abrir**.</span><span class="sxs-lookup"><span data-stu-id="f5be5-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="f5be5-143">La pestaña se cargará en Teams.</span><span class="sxs-lookup"><span data-stu-id="f5be5-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="f5be5-144">Ver las pestañas personales</span><span class="sxs-lookup"><span data-stu-id="f5be5-144">View your personal tabs</span></span>

<span data-ttu-id="f5be5-145">En la barra de exploración situada en el extremo izquierdo del cliente de Microsoft Teams `...` , seleccione el menú y elija la aplicación en la lista.</span><span class="sxs-lookup"><span data-stu-id="f5be5-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>
