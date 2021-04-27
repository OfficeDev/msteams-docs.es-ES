---
title: 'Introducción: crear una pestaña de canal y grupo'
author: heath-hamilton
description: Cree rápidamente una pestaña de grupo y canal de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: lajanuar
localization_priority: Normal
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: aadab4b6826b026eadd5ed564b6e5de5c29b4b1d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020880"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="ed56a-103">Crear una pestaña de canal y grupo para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ed56a-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="ed56a-104">En este tutorial, crearás una pestaña de canal básica *(también* conocida como pestaña de *grupo),* que es una página a pantalla completa para un canal de grupo o chat.</span><span class="sxs-lookup"><span data-stu-id="ed56a-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="ed56a-105">A diferencia de una pestaña personal, los usuarios pueden configurar algunos aspectos de este tipo de pestaña (por ejemplo, cambiar el nombre de la pestaña para que sea significativa para su canal).</span><span class="sxs-lookup"><span data-stu-id="ed56a-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="ed56a-106">Su asignación</span><span class="sxs-lookup"><span data-stu-id="ed56a-106">Your assignment</span></span>

<span data-ttu-id="ed56a-107">No hace mucho tiempo, la organización creó una aplicación de Teams que usa una pestaña para mostrar información de contacto importante (servicio de soporte, recursos humanos, etc.).</span><span class="sxs-lookup"><span data-stu-id="ed56a-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="ed56a-108">Sin embargo, como es una pestaña personal, cada usuario debe instalar la pestaña para verla y la adopción es menor de lo esperado.</span><span class="sxs-lookup"><span data-stu-id="ed56a-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="ed56a-109">En otras palabras, demasiados trabajadores aún no saben cómo llegar al servicio de ayuda.</span><span class="sxs-lookup"><span data-stu-id="ed56a-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="ed56a-110">Puedes hacer que esta información sea más fácil de encontrar mediante la creación de una pestaña de canal, que eliminará la carga de requerir que todos instalen una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed56a-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="ed56a-111">En su lugar, un usuario puede agregar la pestaña en un canal o chat para beneficio de un grupo completo.</span><span class="sxs-lookup"><span data-stu-id="ed56a-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="ed56a-112">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="ed56a-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ed56a-113">Crear un proyecto de aplicación con Microsoft Teams Toolkit for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ed56a-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="ed56a-114">Identificar algunas de las configuraciones de la aplicación y los scaffolding relevantes para las pestañas de canal</span><span class="sxs-lookup"><span data-stu-id="ed56a-114">Identify some of the app configurations and scaffolding relevant to channel tabs</span></span>
> * <span data-ttu-id="ed56a-115">Crear contenido de pestaña</span><span class="sxs-lookup"><span data-stu-id="ed56a-115">Create tab content</span></span>
> * <span data-ttu-id="ed56a-116">Crear contenido para la página de configuración de una pestaña</span><span class="sxs-lookup"><span data-stu-id="ed56a-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="ed56a-117">Proporcionar un nombre de pestaña sugerido</span><span class="sxs-lookup"><span data-stu-id="ed56a-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="ed56a-118">Compilar y ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="ed56a-118">Build and run your app locally</span></span>
> * <span data-ttu-id="ed56a-119">Descargar localmente la aplicación en Teams para pruebas</span><span class="sxs-lookup"><span data-stu-id="ed56a-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ed56a-120">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ed56a-120">Before you begin</span></span>

<span data-ttu-id="ed56a-121">Si aún no lo ha hecho, asegúrese de comprender e [instalar los requisitos previos](build-first-app-overview.md#get-prerequisites)de desarrollo de Teams .</span><span class="sxs-lookup"><span data-stu-id="ed56a-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="ed56a-122">1. Crear el proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="ed56a-122">1. Create your app project</span></span>

<span data-ttu-id="ed56a-123">Microsoft Teams Toolkit ayuda a configurar la aplicación y a configurar scaffolding relevantes para las pestañas de canal y grupo, incluida una página de configuración básica y una página de contenido que muestra un "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="ed56a-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="ed56a-124">Mensaje.</span><span class="sxs-lookup"><span data-stu-id="ed56a-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="ed56a-125">Si no has creado un proyecto de aplicación de Teams [](../build-your-first-app/build-and-run.md) antes, es posible que te sea útil seguir estas instrucciones que explican los proyectos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="ed56a-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. En Visual Studio, selecciona **Microsoft Teams en** la barra de actividades izquierda y elige Crear una nueva aplicación de :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Teams**.
1. <span data-ttu-id="ed56a-127">Cuando se le pida, inicie sesión con su cuenta de desarrollo de Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="ed56a-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="ed56a-128">En la **pantalla Agregar funcionalidades,** seleccione **Ficha** y, a **continuación, Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ed56a-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="ed56a-129">Escribe un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="ed56a-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="ed56a-130">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local). Seleccione **Grupo o pestaña Canal de Teams**.</span><span class="sxs-lookup"><span data-stu-id="ed56a-130">(This is the default name for your app and also the name of the app project directory on your local machine.) Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="ed56a-131">Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ed56a-131">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="ed56a-132">2. Identificar componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="ed56a-132">2. Identify relevant app project components</span></span>

<span data-ttu-id="ed56a-133">Gran parte de las configuraciones de la aplicación y los scaffolding se establecen automáticamente al crear el proyecto con el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="ed56a-133">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="ed56a-134">Veamos los componentes principales para crear una pestaña de canal.</span><span class="sxs-lookup"><span data-stu-id="ed56a-134">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="ed56a-135">Configuraciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ed56a-135">App configurations</span></span>

<span data-ttu-id="ed56a-136">En el kit de herramientas, ve **a App Studio** para ver y actualizar las configuraciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed56a-136">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="ed56a-137">Scaffolding de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ed56a-137">App scaffolding</span></span>

<span data-ttu-id="ed56a-138">El scaffolding de la aplicación proporciona los componentes para representar la pestaña de canal en Teams.</span><span class="sxs-lookup"><span data-stu-id="ed56a-138">The app scaffolding provides the components for rendering your channel tab in Teams.</span></span> <span data-ttu-id="ed56a-139">Hay mucho con lo que puede trabajar, pero por ahora solo necesita centrarse en lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ed56a-139">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="ed56a-140">Dos archivos ubicados en el `src/components` directorio del proyecto:</span><span class="sxs-lookup"><span data-stu-id="ed56a-140">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="ed56a-141">`Tab.js` para representar la página de contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="ed56a-141">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="ed56a-142">`TabConfig.js` para representar la página de configuración de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="ed56a-142">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="ed56a-143">SDK de cliente de JavaScript de Microsoft Teams, que viene precargado en los componentes front-end del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ed56a-143">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="ed56a-144">3. Personalizar la página de contenido de la pestaña</span><span class="sxs-lookup"><span data-stu-id="ed56a-144">3. Customize your tab content page</span></span>

<span data-ttu-id="ed56a-145">Copie y actualice el siguiente fragmento de código con información relevante para su organización o, por el momento, use el código tal como está.</span><span class="sxs-lookup"><span data-stu-id="ed56a-145">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

```JSX
<div>
  <h1>Important Contacts</h1>
    <ul>
      <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
      <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
      <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
    </ul>
</div>
```

<span data-ttu-id="ed56a-146">Vaya al `src/components` directorio y abra `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="ed56a-146">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="ed56a-147">Busque la `render()` función y pegue el contenido dentro `return()` (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="ed56a-147">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

```JavaScript
render() {

    let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

    return (
    <div>
      <h1>Important Contacts</h1>
        <ul>
          <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
          <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
          <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
        </ul>
    </div>
    );
}
```

<span data-ttu-id="ed56a-148">Agregue la siguiente regla a (también ubicada en ) para que los vínculos de correo electrónico sean más fáciles de leer `App.css` `src/components` independientemente del tema que se utilice.</span><span class="sxs-lookup"><span data-stu-id="ed56a-148">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="ed56a-149">4. Personalizar la página de configuración de pestañas</span><span class="sxs-lookup"><span data-stu-id="ed56a-149">4. Customize your tab configuration page</span></span>

<span data-ttu-id="ed56a-150">Cada pestaña de un canal o chat tiene una página de configuración, un modal con al menos una opción de configuración que se muestra cuando los usuarios agregan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed56a-150">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="ed56a-151">De forma predeterminada, la página de configuración pregunta a los usuarios si quieren notificar al canal o al chat cuando se instala la pestaña.</span><span class="sxs-lookup"><span data-stu-id="ed56a-151">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="ed56a-152">Agregue contenido personalizado a la página de configuración.</span><span class="sxs-lookup"><span data-stu-id="ed56a-152">Add some custom content to your configuration page.</span></span> <span data-ttu-id="ed56a-153">Vaya al directorio del proyecto, abra y actualice el contenido del marcador de posición `src/components` `TabConfig.js` dentro `return()` (como se muestra en el ejemplo siguiente).</span><span class="sxs-lookup"><span data-stu-id="ed56a-153">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

```JavaScript
return (
    <div>
      <h1>Add My Contoso Contacts</h1>
      <div>
        Select <b>Save</b> to add our organization's important contacts to this workspace.
      </div>
    </div>
);
```
 
> [!TIP]
> <span data-ttu-id="ed56a-154">Como mínimo, proporciona información breve acerca de la aplicación en esta página, ya que puede ser la primera vez que los usuarios estén aprendiendo sobre ella.</span><span class="sxs-lookup"><span data-stu-id="ed56a-154">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="ed56a-155">También puede incluir opciones de configuración personalizadas o un flujo [de trabajo de autenticación,](../tabs/how-to/authentication/auth-aad-sso.md)que es común en las páginas de configuración de pestañas.</span><span class="sxs-lookup"><span data-stu-id="ed56a-155">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="ed56a-156">5. Proporcionar un nombre de pestaña sugerido</span><span class="sxs-lookup"><span data-stu-id="ed56a-156">5. Provide a suggested tab name</span></span>

<span data-ttu-id="ed56a-157">Cuando agregas una pestaña de canal, de forma predeterminada se muestra el nombre de la aplicación (por ejemplo, **primera aplicación).**</span><span class="sxs-lookup"><span data-stu-id="ed56a-157">When you add a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="ed56a-158">Esto puede estar bien en función de lo que llames a tu aplicación, pero es posible que quieras proporcionar un nombre que tenga más sentido en el contexto de colaboración en grupo (por ejemplo, Contactos de **grupo**).</span><span class="sxs-lookup"><span data-stu-id="ed56a-158">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

1. <span data-ttu-id="ed56a-159">En `TabConfig.js` , vaya a `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="ed56a-159">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span>
2. <span data-ttu-id="ed56a-160">Agregue la `suggestedDisplayName` propiedad con el nombre de pestaña que desea mostrar de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ed56a-160">Add the `suggestedDisplayName` property with the tab name you want to display by default.</span></span> 
3. <span data-ttu-id="ed56a-161">Use el nombre proporcionado en el ejemplo siguiente o escriba su nombre.</span><span class="sxs-lookup"><span data-stu-id="ed56a-161">Use the name provided in the following example or type your name.</span></span> <span data-ttu-id="ed56a-162">(De forma predeterminada, los usuarios pueden cambiar el nombre).</span><span class="sxs-lookup"><span data-stu-id="ed56a-162">(By default, users can change the name.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="ed56a-163">6. Crear y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="ed56a-163">6. Build and run your app</span></span>

<span data-ttu-id="ed56a-164">En el interés del tiempo, compilarás y ejecutarás la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="ed56a-164">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="ed56a-165">(Esta información también está disponible en el kit de herramientas `README` ).)</span><span class="sxs-lookup"><span data-stu-id="ed56a-165">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="ed56a-166">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="ed56a-166">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="ed56a-167">Ejecute `npm start` .</span><span class="sxs-lookup"><span data-stu-id="ed56a-167">Run `npm start`.</span></span>

<span data-ttu-id="ed56a-168">Una vez completado, hay un **compilado correctamente.**</span><span class="sxs-lookup"><span data-stu-id="ed56a-168">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="ed56a-169">en el terminal.</span><span class="sxs-lookup"><span data-stu-id="ed56a-169">message in the terminal.</span></span> <span data-ttu-id="ed56a-170">La aplicación se está ejecutando en `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="ed56a-170">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="ed56a-171">7. Instalación local de la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="ed56a-171">7. Sideload your app in Teams</span></span>

<span data-ttu-id="ed56a-172">La aplicación está lista para probarse en Teams.</span><span class="sxs-lookup"><span data-stu-id="ed56a-172">Your app is ready to test in Teams.</span></span> <span data-ttu-id="ed56a-173">Para ello, debes tener una cuenta que permita la instalación local de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed56a-173">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="ed56a-174">(Si no está seguro de que lo tiene, obtenga información sobre cómo obtener una cuenta de desarrollo [de Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)).)</span><span class="sxs-lookup"><span data-stu-id="ed56a-174">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="ed56a-175">En Visual Studio, presione la tecla **F5** para iniciar un cliente web de Teams.</span><span class="sxs-lookup"><span data-stu-id="ed56a-175">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="ed56a-176">Para mostrar el contenido de la aplicación en Teams, especifica que el lugar donde se ejecuta la aplicación ( `localhost` ) es de confianza:</span><span class="sxs-lookup"><span data-stu-id="ed56a-176">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="ed56a-177">Abra una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abrió después de presionar **F5**.</span><span class="sxs-lookup"><span data-stu-id="ed56a-177">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="ed56a-178">Vaya a `https://localhost:3000/tab` y continúe con la página.</span><span class="sxs-lookup"><span data-stu-id="ed56a-178">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="ed56a-179">Vuelva a Teams.</span><span class="sxs-lookup"><span data-stu-id="ed56a-179">Go back to Teams.</span></span> <span data-ttu-id="ed56a-180">En el modal, seleccione **Agregar a un** equipo o Agregar a un **chat** y busque un canal o chat que pueda usar para las pruebas.</span><span class="sxs-lookup"><span data-stu-id="ed56a-180">In the modal, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="ed56a-181">Seleccione **Configurar una pestaña**. La página de configuración se muestra en un modal.</span><span class="sxs-lookup"><span data-stu-id="ed56a-181">Select **Set up a tab**. The configuration page displays in a modal.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Captura de pantalla de una página de configuración de pestaña de canal.":::
1. <span data-ttu-id="ed56a-183">Seleccione **Guardar** para configurar la pestaña. Se muestra la página de contenido.</span><span class="sxs-lookup"><span data-stu-id="ed56a-183">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Captura de pantalla de una pestaña de canal con vista de contenido estático.":::

## <a name="well-done"></a><span data-ttu-id="ed56a-185">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="ed56a-185">Well done</span></span>

<span data-ttu-id="ed56a-186">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ed56a-186">Congratulations!</span></span> <span data-ttu-id="ed56a-187">Tienes una aplicación de Teams con una pestaña para mostrar contenido útil en canales y chats.</span><span class="sxs-lookup"><span data-stu-id="ed56a-187">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="ed56a-188">Más información</span><span class="sxs-lookup"><span data-stu-id="ed56a-188">Learn more</span></span>

* <span data-ttu-id="ed56a-189">Siga nuestras [directrices de diseño](../tabs/design/tabs.md) y cree con [plantillas de](../concepts/design/design-teams-app-ui-templates.md) interfaz de usuario preparadas para producción para crear una experiencia perfecta.</span><span class="sxs-lookup"><span data-stu-id="ed56a-189">Follow our [design guidelines](../tabs/design/tabs.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* <span data-ttu-id="ed56a-190">Comprender [las consideraciones móviles](../tabs/design/tabs-mobile.md) para las pestañas.</span><span class="sxs-lookup"><span data-stu-id="ed56a-190">Understand [mobile considerations](../tabs/design/tabs-mobile.md) for tabs.</span></span>
* <span data-ttu-id="ed56a-191">[Agregar autenticación de SSO a la pestaña](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="ed56a-191">[Add SSO authentication to your tab](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>
* <span data-ttu-id="ed56a-192">Utilizar datos de Teams con [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span><span class="sxs-lookup"><span data-stu-id="ed56a-192">Utilize Teams data with [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>
* [<span data-ttu-id="ed56a-193">Crear una pestaña sin el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="ed56a-193">Create a tab without the toolkit</span></span>](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a><span data-ttu-id="ed56a-194">Siguiente lección</span><span class="sxs-lookup"><span data-stu-id="ed56a-194">Next lesson</span></span>

<span data-ttu-id="ed56a-195">Ya sabes cómo crear una pestaña para la colaboración.</span><span class="sxs-lookup"><span data-stu-id="ed56a-195">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="ed56a-196">¿Quieres intentar crear un tipo diferente de aplicación de Teams?</span><span class="sxs-lookup"><span data-stu-id="ed56a-196">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed56a-197">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="ed56a-197">Build a bot</span></span>](../build-your-first-app/build-bot.md)
