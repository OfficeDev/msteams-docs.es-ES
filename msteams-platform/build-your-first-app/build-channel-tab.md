---
title: 'Introducción: crear una pestaña de canal y grupo'
author: girliemac
description: Cree rápidamente una pestaña de grupo y canal de Microsoft Teams con Microsoft Teams Toolkit.
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: 868a471499bf2015196b7b741e340d070d0ed458
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068755"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="321b6-103">Crear la primera pestaña de canal y grupo para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="321b6-103">Build your first channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="321b6-104">Este tutorial le enseña a  crear una pestaña de canal básica también conocida como pestaña de grupo *,* que es una página a pantalla completa para un canal de grupo o chat.</span><span class="sxs-lookup"><span data-stu-id="321b6-104">This tutorial teaches you to build a basic *channel tab* also known as a *group tab*, which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="321b6-105">También puede configurar algunos aspectos de este tipo de pestaña, por ejemplo, cambiar el nombre de la pestaña para que sea significativa para su canal, lo que no puede hacer en una pestaña personal.</span><span class="sxs-lookup"><span data-stu-id="321b6-105">You can also configure some aspects of this kind of tab, for example, rename the tab so it's meaningful to their channel, which you cannot do in a Personal Tab.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="321b6-106">Lo que aprenderás</span><span class="sxs-lookup"><span data-stu-id="321b6-106">What you'll learn</span></span>

* <span data-ttu-id="321b6-107">Crea un proyecto de aplicación con Microsoft Teams Toolkit para Visual Studio código.</span><span class="sxs-lookup"><span data-stu-id="321b6-107">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="321b6-108">Comprenda las configuraciones de la aplicación y los scaffolding relevantes para las pestañas de canal.</span><span class="sxs-lookup"><span data-stu-id="321b6-108">Understand the app configurations and scaffolding relevant to channel tabs.</span></span>
* <span data-ttu-id="321b6-109">Crear contenido de pestaña y configuración de pestañas.</span><span class="sxs-lookup"><span data-stu-id="321b6-109">Create tab content and tab configuration.</span></span>
* <span data-ttu-id="321b6-110">Crea y ejecuta la aplicación en teams para pruebas.</span><span class="sxs-lookup"><span data-stu-id="321b6-110">Build and run your app in teams for testing.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="321b6-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="321b6-111">Prerequisites</span></span>

<span data-ttu-id="321b6-112">Asegúrate de comprender cómo configurar y crear una aplicación sencilla de Teams.</span><span class="sxs-lookup"><span data-stu-id="321b6-112">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="321b6-113">Para obtener más información, consulta crear la primera aplicación de [Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="321b6-113">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="321b6-114">1. Crear el proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="321b6-114">1. Create your app project</span></span>

<span data-ttu-id="321b6-115">Microsoft Teams Toolkit te ayuda a configurar la aplicación y configurar el scaffolding relevante para las pestañas de canal y grupo.</span><span class="sxs-lookup"><span data-stu-id="321b6-115">The Microsoft Teams Toolkit helps you to configure your app and set up the scaffolding relevant to channel and group tabs.</span></span> <span data-ttu-id="321b6-116">También contiene una página de configuración básica y una página de contenido que muestra un "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="321b6-116">It also contains a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="321b6-117">Mensaje.</span><span class="sxs-lookup"><span data-stu-id="321b6-117">message.</span></span>

<span data-ttu-id="321b6-118">**Para crear el proyecto de aplicación**</span><span class="sxs-lookup"><span data-stu-id="321b6-118">**To create your app project**</span></span>

1. Ve a Visual Studio y selecciona **Microsoft Teams** en la barra de actividades :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: izquierda.
1. <span data-ttu-id="321b6-120">Inicie sesión con su cuenta de desarrollo de Microsoft 365 cuando se le pida que lo haga.</span><span class="sxs-lookup"><span data-stu-id="321b6-120">Sign in with your Microsoft 365 development account when prompted to do so.</span></span>
1. <span data-ttu-id="321b6-121">En la **pantalla Seleccionar proyecto,** seleccione **JS** (JavaScript) en Canal y aplicación **de grupo.**</span><span class="sxs-lookup"><span data-stu-id="321b6-121">On the **Select project** screen, select **JS** (JavaScript) under **Channel and group app**.</span></span>
1. <span data-ttu-id="321b6-122">Escribe un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="321b6-122">Enter a name for your Teams app.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="321b6-123">Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de aplicación en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="321b6-123">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>

1. <span data-ttu-id="321b6-124">Seleccione **Grupo o pestaña Canal de Teams**.</span><span class="sxs-lookup"><span data-stu-id="321b6-124">Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="321b6-125">Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto y guardar el proyecto en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="321b6-125">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="321b6-126">2. Comprender los componentes del proyecto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="321b6-126">2. Understand your app project components</span></span>

<span data-ttu-id="321b6-127">Gran parte de las configuraciones de la aplicación y los scaffolding se establecen automáticamente al crear el proyecto con el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="321b6-127">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="321b6-128">Veamos los componentes principales para crear una pestaña de canal.</span><span class="sxs-lookup"><span data-stu-id="321b6-128">Let's look at the main components for building a channel tab.</span></span>

* <span data-ttu-id="321b6-129">**Configuraciones de aplicaciones:** abre **App Studio** en el kit de herramientas para ver y actualizar las configuraciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="321b6-129">**App configurations**: Open **App Studio** in the toolkit to view and update your app configurations.</span></span>
* <span data-ttu-id="321b6-130">**Scaffolding de aplicaciones:** el scaffolding de la aplicación proporciona los componentes necesarios para representar la pestaña de canal en Teams.</span><span class="sxs-lookup"><span data-stu-id="321b6-130">**App scaffolding**: The app scaffolding provides the components needed for rendering your channel tab in Teams.</span></span> <span data-ttu-id="321b6-131">Sin embargo, hay mucho con lo que puede trabajar, por ahora vamos a centrarnos en lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="321b6-131">There's a lot you can work with, however, for now let's focus on the following:</span></span>
  * <span data-ttu-id="321b6-132">Los archivos ubicados en el `src/components` directorio del proyecto:</span><span class="sxs-lookup"><span data-stu-id="321b6-132">The files located in the `src/components` directory of your project:</span></span>
    * <span data-ttu-id="321b6-133">`Tab.js` para representar la página de contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="321b6-133">`Tab.js` for rendering your tab's content page.</span></span>
    * <span data-ttu-id="321b6-134">`TabConfig.js` para representar la página de configuración de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="321b6-134">`TabConfig.js` for rendering your tab's configuration page.</span></span>
  * <span data-ttu-id="321b6-135">SDK de cliente de JavaScript de Microsoft Teams, que viene precargado en los componentes front-end del proyecto.</span><span class="sxs-lookup"><span data-stu-id="321b6-135">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="321b6-136">3. Personalizar la página de contenido de la pestaña</span><span class="sxs-lookup"><span data-stu-id="321b6-136">3. Customize your tab content page</span></span>

1. <span data-ttu-id="321b6-137">Copie y modifique el siguiente ejemplo de código con información relevante para su organización.</span><span class="sxs-lookup"><span data-stu-id="321b6-137">Copy and modify the following code sample with information that's relevant to your organization.</span></span> <span data-ttu-id="321b6-138">También puede usar el fragmento de código tal como es:</span><span class="sxs-lookup"><span data-stu-id="321b6-138">You can also use the snippet as it is:</span></span>
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
1. <span data-ttu-id="321b6-139">Vaya al `src/components` directorio y abra el `Tab.js` archivo.</span><span class="sxs-lookup"><span data-stu-id="321b6-139">Go to the `src/components` directory and open the `Tab.js` file.</span></span> <span data-ttu-id="321b6-140">Busque la `render()` función y pegue el código dentro como se muestra en el siguiente `return()` ejemplo:</span><span class="sxs-lookup"><span data-stu-id="321b6-140">Locate the `render()` function and paste your code inside `return()` as shown in the following example:</span></span>
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
1. <span data-ttu-id="321b6-141">Vaya al directorio y actualice el archivo con el siguiente código para que los vínculos de correo electrónico sean más fáciles de `src/components` leer en cualquier tema que se `App.css` utilice:</span><span class="sxs-lookup"><span data-stu-id="321b6-141">Go to the `src/components` directory and update the `App.css` file with the following code to make the email links easier to read in any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="321b6-142">4. Personalizar la página de configuración de pestañas</span><span class="sxs-lookup"><span data-stu-id="321b6-142">4. Customize your tab configuration page</span></span>

<span data-ttu-id="321b6-143">Cada pestaña de un canal o chat tiene una página de configuración, un modal con al menos una opción de configuración que se muestra cuando los usuarios agregan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="321b6-143">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="321b6-144">De forma predeterminada, la página de configuración pregunta a los usuarios si quieren notificar al canal o al chat cuando se instala la pestaña.</span><span class="sxs-lookup"><span data-stu-id="321b6-144">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span> <span data-ttu-id="321b6-145">Puede personalizar la página de configuración agregando contenido personalizado.</span><span class="sxs-lookup"><span data-stu-id="321b6-145">You can customize the configuration page by adding custom content.</span></span>

<span data-ttu-id="321b6-146">Para agregar contenido personalizado, abra el archivo desde el directorio y actualice el contenido de marcador de posición dentro como `TabConfig.js` se muestra en el ejemplo `src/components` `return()` siguiente:</span><span class="sxs-lookup"><span data-stu-id="321b6-146">To add custom content, open `TabConfig.js` file from the `src/components` directory and update the placeholder content inside `return()` as shown in the following example:</span></span>

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
> <span data-ttu-id="321b6-147">Proporciona una breve información sobre la aplicación en esta página, ya que esta sería la primera vez que los usuarios leen sobre ella.</span><span class="sxs-lookup"><span data-stu-id="321b6-147">Give a brief information about your app on this page since this would be the first time users are reading about it.</span></span> <span data-ttu-id="321b6-148">También puede incluir opciones de configuración personalizadas o un flujo [de trabajo de autenticación,](../tabs/how-to/authentication/auth-aad-sso.md)que es común en las páginas de configuración de pestañas.</span><span class="sxs-lookup"><span data-stu-id="321b6-148">You can also include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-customize-your-tab-name"></a><span data-ttu-id="321b6-149">5. Personalizar el nombre de la pestaña</span><span class="sxs-lookup"><span data-stu-id="321b6-149">5. Customize your tab name</span></span>

<span data-ttu-id="321b6-150">Al agregar una pestaña de canal, el nombre de la aplicación se muestra de forma predeterminada, por ejemplo, **first-app**.</span><span class="sxs-lookup"><span data-stu-id="321b6-150">When you add a channel tab, the app name displays by default, for example, **first-app**.</span></span> <span data-ttu-id="321b6-151">También puede proporcionar un nombre que tenga más sentido en el contexto de la colaboración en grupo, por ejemplo, **Contactos de grupo:**</span><span class="sxs-lookup"><span data-stu-id="321b6-151">You can also provide a name that makes more sense in the context of group collaboration, for example, **Team Contacts**:</span></span>

1. <span data-ttu-id="321b6-152">Vaya al `src/components` directorio y abra el `TabConfig.js` archivo.</span><span class="sxs-lookup"><span data-stu-id="321b6-152">Go to the `src/components` directory and open the `TabConfig.js` file.</span></span>
1. <span data-ttu-id="321b6-153">Agregue la propiedad con el nombre de pestaña que desea mostrar de forma predeterminada `suggestedDisplayName` `microsoftTeams.settings.setSettings` en, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="321b6-153">Add the `suggestedDisplayName` property with the tab name you want to display by default under `microsoftTeams.settings.setSettings` as shown in the following example:</span></span>

  ```JavaScript
    microsoftTeams.settings.setSettings({
    "contentUrl": "https://localhost:3000/tab",
    "suggestedDisplayName": "Team Contacts"
  });
  ```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="321b6-154">6. Crear y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="321b6-154">6. Build and run your app</span></span>

<span data-ttu-id="321b6-155">Este tutorial te enseña a crear y ejecutar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="321b6-155">This tutorial teaches you to build and run your app locally.</span></span> 

1. <span data-ttu-id="321b6-156">Vaya al directorio raíz del proyecto de la aplicación en Terminal.</span><span class="sxs-lookup"><span data-stu-id="321b6-156">Go to the root directory of your app project in Terminal.</span></span>
1. <span data-ttu-id="321b6-157">Ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="321b6-157">Run `npm install`.</span></span>
1. <span data-ttu-id="321b6-158">Ejecute `npm start` .</span><span class="sxs-lookup"><span data-stu-id="321b6-158">Run `npm start`.</span></span>

<span data-ttu-id="321b6-159">Esta información también está presente en la `README` sección del kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="321b6-159">This information is also present in the `README` section of the toolkit.</span></span>
<span data-ttu-id="321b6-160">La aplicación se está ejecutando `https://localhost:3000` después de **la compilación correctamente.**</span><span class="sxs-lookup"><span data-stu-id="321b6-160">Your app is running on `https://localhost:3000` after the **Compiled successfully!**</span></span> <span data-ttu-id="321b6-161">mensaje aparece en el terminal.</span><span class="sxs-lookup"><span data-stu-id="321b6-161">message appears in the terminal.</span></span> 

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="321b6-162">7. Instalación local de la aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="321b6-162">7. Sideload your app in Teams</span></span>

<span data-ttu-id="321b6-163">La aplicación está lista para probarse en Teams.</span><span class="sxs-lookup"><span data-stu-id="321b6-163">Your app is ready to test in Teams.</span></span> <span data-ttu-id="321b6-164">Para ello, debes tener una cuenta que permita la instalación local de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="321b6-164">To do this, you must have an account that allows app sideloading.</span></span> 

1. <span data-ttu-id="321b6-165">Abra un cliente web de Teams en Visual Studio code con la **clave F5.**</span><span class="sxs-lookup"><span data-stu-id="321b6-165">Open a Teams web client in Visual Studio Code with the **F5** key.</span></span>
1. <span data-ttu-id="321b6-166">Agrega ( ) como confiable siguiendo estos pasos para permitir que el contenido de la aplicación `localhost` se muestre en Teams:</span><span class="sxs-lookup"><span data-stu-id="321b6-166">Add (`localhost`) as trustworthy by following these steps to enable your app content to display in Teams:</span></span>

   1. <span data-ttu-id="321b6-167">Abra una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abrió con la **tecla F5.**</span><span class="sxs-lookup"><span data-stu-id="321b6-167">Open a new tab in the same browser window (Google Chrome by default) which opened with the **F5** key.</span></span>
   1. <span data-ttu-id="321b6-168">Abra `https://localhost:3000/tab` y continúe con la página.</span><span class="sxs-lookup"><span data-stu-id="321b6-168">Open `https://localhost:3000/tab` and proceed to the page.</span></span>

1. <span data-ttu-id="321b6-169">Selecciona **Agregar a un equipo** o Agregar a un **chat** y busca un canal o chat que puedas usar para realizar pruebas desde el modal en Teams.</span><span class="sxs-lookup"><span data-stu-id="321b6-169">Select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing from the modal in Teams.</span></span>
1. <span data-ttu-id="321b6-170">Seleccione **Configurar una pestaña**. La página de configuración se muestra en un modal.</span><span class="sxs-lookup"><span data-stu-id="321b6-170">Select **Set up a tab**. The configuration page displays in a modal.</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Captura de pantalla de una página de configuración de pestaña de canal.":::

1. <span data-ttu-id="321b6-172">Seleccione **Guardar** para configurar la pestaña. Aparece la siguiente página de contenido:</span><span class="sxs-lookup"><span data-stu-id="321b6-172">Select **Save** to configure the tab. The following content page appears:</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Captura de pantalla de una pestaña de canal con vista de contenido estático.":::

## <a name="see-also"></a><span data-ttu-id="321b6-174">Consulte también</span><span class="sxs-lookup"><span data-stu-id="321b6-174">See also</span></span>

* [<span data-ttu-id="321b6-175">Crear y ejecutar la primera aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="321b6-175">Build and run your first Microsoft Teams app</span></span>](../build-your-first-app/build-and-run.md) 
* [<span data-ttu-id="321b6-176">SDK para cliente de JavaScript en Teams</span><span class="sxs-lookup"><span data-stu-id="321b6-176">Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="321b6-177">Diseño de la pestaña para escritorio y web de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="321b6-177">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="321b6-178">Diseño de la aplicación de Microsoft Teams con plantillas de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="321b6-178">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="321b6-179">Pestañas en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="321b6-179">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="321b6-180">Compatibilidad con inicio de sesión único (SSO) para pestañas</span><span class="sxs-lookup"><span data-stu-id="321b6-180">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="321b6-181">Introducción a la API de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="321b6-181">Microsoft Teams API overview</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="321b6-182">Crear una pestaña personal personalizada con Node.js y el generador de Yeoman para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="321b6-182">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="321b6-183">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="321b6-183">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="321b6-184">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="321b6-184">Build a bot</span></span>](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="321b6-185">Crear una extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="321b6-185">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)