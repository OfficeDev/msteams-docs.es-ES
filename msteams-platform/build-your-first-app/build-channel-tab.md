---
title: 'Introducción: crear una pestaña de canal y de grupo'
author: heath-hamilton
description: Cree rápidamente una ficha de canal y de grupo de Microsoft Teams mediante el kit de herramientas de Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 46b5410a1ae7c866f8998362765dfe5462df94cb
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931767"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="3b8cb-103">Crear una pestaña de canal y de grupo para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3b8cb-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="3b8cb-104">En este tutorial, creará una ficha de *canal* básico (también conocida como una *pestaña de grupo* ), que es una página en pantalla completa para un canal o un chat de equipo.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab* ), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="3b8cb-105">A diferencia de una pestaña personal, los usuarios pueden configurar algunos aspectos de este tipo de pestaña (por ejemplo, cambiar el nombre de la ficha para que tenga sentido en su canal).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="3b8cb-106">La asignación</span><span class="sxs-lookup"><span data-stu-id="3b8cb-106">Your assignment</span></span>

<span data-ttu-id="3b8cb-107">No hace mucho tiempo, su organización ha creado una aplicación de Microsoft teams que usa una pestaña para mostrar información de contacto importante (soporte técnico, recursos humanos, etc.).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="3b8cb-108">Sin embargo, puesto que se trata de una pestaña personal, cada usuario debe instalar la pestaña para ver el resultado y la adopción es inferior a lo esperado.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="3b8cb-109">En otras palabras, hay demasiados trabajadores que todavía no saben cómo llegar al Departamento de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="3b8cb-110">Puede facilitar la búsqueda de esta información si crea una pestaña de canal, lo que eliminará la carga de requerir que todos los usuarios instalen una aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="3b8cb-111">En su lugar, un usuario puede Agregar la pestaña en un canal o chatear para beneficiar de todo el grupo.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="3b8cb-112">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="3b8cb-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="3b8cb-113">Crear un proyecto de aplicación con Microsoft Teams Toolkit para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3b8cb-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="3b8cb-114">Identificar algunas de las configuraciones de aplicación y scaffolding relevantes para las pestañas de canal y de grupo</span><span class="sxs-lookup"><span data-stu-id="3b8cb-114">Identify some of the app configurations and scaffolding relevant to channel and group tabs</span></span>
> * <span data-ttu-id="3b8cb-115">Crear contenido de ficha</span><span class="sxs-lookup"><span data-stu-id="3b8cb-115">Create tab content</span></span>
> * <span data-ttu-id="3b8cb-116">Crear contenido para la página de configuración de una pestaña</span><span class="sxs-lookup"><span data-stu-id="3b8cb-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="3b8cb-117">Proporcionar un nombre de pestaña sugerido</span><span class="sxs-lookup"><span data-stu-id="3b8cb-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="3b8cb-118">Compilar y ejecutar la aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="3b8cb-118">Build and run your app locally</span></span>
> * <span data-ttu-id="3b8cb-119">Transferir localmente la aplicación en Teams para realizar pruebas</span><span class="sxs-lookup"><span data-stu-id="3b8cb-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3b8cb-120">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="3b8cb-120">Before you begin</span></span>

<span data-ttu-id="3b8cb-121">Si aún no lo ha hecho, asegúrese [de que comprende e instala los requisitos previos de desarrollo de Microsoft Teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="3b8cb-122">1. crear un proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="3b8cb-122">1. Create your app project</span></span>

<span data-ttu-id="3b8cb-123">El kit de herramientas de Microsoft Teams ayuda a configurar la aplicación y a configurar la técnica scaffolding relevante para las pestañas de canal y grupo, incluida una página de configuración básica y una página de contenido que muestra un "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="3b8cb-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="3b8cb-124">Mensaje.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="3b8cb-125">Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. <span data-ttu-id="3b8cb-127">Cuando se le solicite, inicie sesión con su cuenta de desarrollo de 365 de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="3b8cb-128">En la pantalla **Agregar funciones** , seleccione la **pestaña** **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="3b8cb-129">Escriba un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="3b8cb-130">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-130">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="3b8cb-131">Compruebe la **pestaña personal** y las opciones de la **ficha canal de grupo o de Teams** .</span><span class="sxs-lookup"><span data-stu-id="3b8cb-131">Check the **Personal tab** and **Group or Teams channel tab** options.</span></span> <span data-ttu-id="3b8cb-132">(Pronto aprenderá por qué necesita ambos tipos de pestañas).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-132">(You'll soon learn why you need both types of tabs.)</span></span>
1. <span data-ttu-id="3b8cb-133">Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-133">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="3b8cb-134">2. identificar los componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="3b8cb-134">2. Identify relevant app project components</span></span>

<span data-ttu-id="3b8cb-135">Una gran parte de la configuración de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-135">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="3b8cb-136">Echemos un vistazo a los componentes principales para crear una ficha de canal y de grupo.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-136">Let's look at the main components for building a channel and group tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="3b8cb-137">Configuraciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3b8cb-137">App configurations</span></span>

<span data-ttu-id="3b8cb-138">Puede ver y actualizar las configuraciones de la aplicación mediante App Studio, que se incluye en el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-138">You can view and update your app configurations using App Studio, which is included in the toolkit.</span></span>

<span data-ttu-id="3b8cb-139">Durante la configuración, el kit de herramientas configuró inicialmente dos componentes básicos de las fichas de canal y de Grupo:</span><span class="sxs-lookup"><span data-stu-id="3b8cb-139">During setup, the toolkit initially configured two essential components of channel and group tabs:</span></span>

* <span data-ttu-id="3b8cb-140">**Página de configuración** : el cuadro de diálogo para agregar una pestaña a un canal o a un chat.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-140">**Configuration page** : The dialog for adding a tab to a channel or chat.</span></span> <span data-ttu-id="3b8cb-141">(En App Studio, puede encontrar esta página yendo a **pestañas > ficha equipo** ).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-141">(In App Studio, you can find this page by going to **Tabs > Team tab**.)</span></span>
* <span data-ttu-id="3b8cb-142">**Página de contenido** : donde se muestra el contenido principal.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-142">**Content page** : Where you display your primary content.</span></span> <span data-ttu-id="3b8cb-143">(En App Studio, puede encontrar esta página yendo a las **pestañas > agregar una pestaña personal** ).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-143">(In App Studio, you can find this page by going to **Tabs > Add a personal tab**.)</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="3b8cb-144">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3b8cb-144">App scaffolding</span></span>

<span data-ttu-id="3b8cb-145">El scaffolding de la aplicación proporciona los componentes para representar la pestaña personal en Teams.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-145">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="3b8cb-146">Hay muchas cosas con las que puede trabajar, pero por ahora solo necesita centrarse en lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3b8cb-146">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="3b8cb-147">Dos archivos ubicados en el `src/components` directorio del proyecto:</span><span class="sxs-lookup"><span data-stu-id="3b8cb-147">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="3b8cb-148">`Tab.js` para representar la página de contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-148">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="3b8cb-149">`TabConfig.js` para representar la página de configuración de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-149">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="3b8cb-150">SDK cliente de JavaScript de Microsoft Teams, que viene precargado en los componentes front-end del proyecto.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-150">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="3b8cb-151">3. personalizar la página de contenido de la pestaña</span><span class="sxs-lookup"><span data-stu-id="3b8cb-151">3. Customize your tab content page</span></span>

<span data-ttu-id="3b8cb-152">Copie y actualice el siguiente fragmento de código con información relevante para su organización o, por el momento, use el código tal y como está.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-152">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="3b8cb-153">Vaya al `src/components` Directorio y Abra `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="3b8cb-153">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="3b8cb-154">Busque la `render()` función y pegue el contenido dentro de `return()` (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-154">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="3b8cb-155">Agregue la siguiente regla a `App.css` (también se encuentra en `src/components` ) para que los vínculos de correo electrónico sean más fáciles de leer independientemente del tema que se use.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-155">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="3b8cb-156">4. personalizar la página de configuración de pestañas</span><span class="sxs-lookup"><span data-stu-id="3b8cb-156">4. Customize your tab configuration page</span></span>

<span data-ttu-id="3b8cb-157">Cada pestaña en un canal o chat tiene una página de configuración, un cuadro de diálogo con al menos una opción de configuración que se muestra cuando los usuarios agregan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-157">Every tab in a channel or chat has a configuration page, a dialog with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="3b8cb-158">De forma predeterminada, la página de configuración pregunta a los usuarios si quieren notificar al canal o al chat cuando se instala la ficha.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-158">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="3b8cb-159">Agregue contenido personalizado a la página de configuración.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-159">Add some custom content to your configuration page.</span></span> <span data-ttu-id="3b8cb-160">Vaya al directorio del proyecto `src/components` , Abra `TabConfig.js` y actualice el contenido del marcador de posición dentro de `return()` (como se muestra en el siguiente ejemplo).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-160">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

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
> <span data-ttu-id="3b8cb-161">Como mínimo, proporcione información breve sobre la aplicación en esta página, ya que esto puede ser la primera vez que los usuarios aprenden sobre ella.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-161">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="3b8cb-162">También puede incluir opciones de configuración personalizadas o un [flujo de trabajo de autenticación](../tabs/how-to/authentication/auth-aad-sso.md), que es común en las páginas de configuración de pestañas.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-162">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="3b8cb-163">5. proporcionar un nombre de pestaña sugerido</span><span class="sxs-lookup"><span data-stu-id="3b8cb-163">5. Provide a suggested tab name</span></span>

<span data-ttu-id="3b8cb-164">Cuando se agrega una pestaña de canal o de grupo, se muestra el nombre de la aplicación (por ejemplo, la **primera aplicación** ) de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-164">When you add a channel or group tab, by default the app name displays (for example, **first-app** ).</span></span>

<span data-ttu-id="3b8cb-165">Esto puede ser adecuado, en función de lo que llame a su aplicación, pero puede que desee proporcionar un nombre que sea más lógico en el contexto de la colaboración en grupo (por ejemplo, los **contactos del equipo** ).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-165">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts** ).</span></span>

<span data-ttu-id="3b8cb-166">En `TabConfig.js` , vaya a `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="3b8cb-166">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="3b8cb-167">Agregue la `suggestedDisplayName` propiedad con el nombre de la pestaña que desee mostrar de forma predeterminada (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-167">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="3b8cb-168">Use el nombre proporcionado o cree el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-168">Use the provided name or create your own.</span></span> <span data-ttu-id="3b8cb-169">(De forma predeterminada, los usuarios pueden cambiar el nombre si lo desean).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-169">(By default, users to change the name if they want.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="3b8cb-170">6. compilar y ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="3b8cb-170">6. Build and run your app</span></span>

<span data-ttu-id="3b8cb-171">En aras del tiempo, se creará y se ejecutará la aplicación de forma local.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-171">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="3b8cb-172">(Esta información también está disponible en el kit de herramientas `README` ).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-172">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="3b8cb-173">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="3b8cb-173">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="3b8cb-174">Ejecutar `npm start` .</span><span class="sxs-lookup"><span data-stu-id="3b8cb-174">Run `npm start`.</span></span>

<span data-ttu-id="3b8cb-175">Una vez completada la **compilación correctamente.**</span><span class="sxs-lookup"><span data-stu-id="3b8cb-175">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="3b8cb-176">mensaje en el terminal.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-176">message in the terminal.</span></span> <span data-ttu-id="3b8cb-177">La aplicación se está ejecutando en `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="3b8cb-177">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="3b8cb-178">7. transferir localmente la aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3b8cb-178">7. Sideload your app in Teams</span></span>

<span data-ttu-id="3b8cb-179">La aplicación está lista para realizar pruebas en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-179">Your app is ready to test in Teams.</span></span> <span data-ttu-id="3b8cb-180">Para ello, debe tener una cuenta que permita la transferencia local de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-180">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="3b8cb-181">(Si no está seguro de ello, obtenga información sobre cómo obtener una cuenta de desarrollo de Microsoft [Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-181">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="3b8cb-182">En Visual Studio Code, presione la tecla **F5** para iniciar un cliente web de Teams.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-182">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="3b8cb-183">Para mostrar el contenido de la aplicación en Teams, especifique que la aplicación en ejecución ( `localhost` ) sea de confianza:</span><span class="sxs-lookup"><span data-stu-id="3b8cb-183">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="3b8cb-184">Abrir una nueva pestaña en la misma ventana del explorador (Google Chrome de forma predeterminada) que se abre después de presionar **F5**.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-184">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="3b8cb-185">Vaya a `https://localhost:3000/tab` la página y continúe con ella.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-185">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="3b8cb-186">Vuelva a teams.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-186">Go back to Teams.</span></span> <span data-ttu-id="3b8cb-187">En el cuadro de diálogo, seleccione **Agregar a un equipo** o **Agregar a un chat** y busque un canal o un chat que pueda usar para las pruebas.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-187">In the dialog, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="3b8cb-188">Seleccione **configurar una pestaña**. La página de configuración se muestra en un cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-188">Select **Set up a tab**. The configuration page displays in a dialog.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Captura de pantalla de una página de configuración de ficha de canal.":::
1. <span data-ttu-id="3b8cb-190">Seleccione **Guardar** para configurar la pestaña. Se muestra la página de contenido.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-190">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Captura de pantalla de una pestaña de canal con vista de contenido estático.":::

## <a name="well-done"></a><span data-ttu-id="3b8cb-192">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="3b8cb-192">Well done</span></span>

<span data-ttu-id="3b8cb-193">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="3b8cb-193">Congratulations!</span></span> <span data-ttu-id="3b8cb-194">Tiene una aplicación de Microsoft Teams con una pestaña para mostrar contenido útil en canales y chats.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-194">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="3b8cb-195">Más información</span><span class="sxs-lookup"><span data-stu-id="3b8cb-195">Learn more</span></span>

* <span data-ttu-id="3b8cb-196">[Autenticar usuarios de pestaña con SSO](../tabs/how-to/authentication/auth-aad-sso.md): si solo quiere que los usuarios autorizados vean su pestaña, configure el inicio de sesión único (SSO) a través de Azure Active Directory (ad).</span><span class="sxs-lookup"><span data-stu-id="3b8cb-196">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="3b8cb-197">[Insertar contenido de una aplicación web o página web existente](../tabs/how-to/add-tab.md#tab-requirements): le mostramos cómo crear nuevo contenido para una pestaña personal, pero también puede cargar contenido desde una dirección URL externa.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-197">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="3b8cb-198">[Crear una experiencia sin problemas para su pestaña](../tabs/design/tabs.md): Consulte las directrices recomendadas para diseñar pestañas de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-198">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="3b8cb-199">[Crear pestañas para móviles](../tabs/design/tabs-mobile.md): comprenda cómo desarrollar pestañas para teléfonos y tabletas.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-199">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="3b8cb-200">Uso de datos de Teams con la API de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="3b8cb-200">Utilize Teams data with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="3b8cb-201">Crear una ficha sin el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="3b8cb-201">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="3b8cb-202">Lección siguiente</span><span class="sxs-lookup"><span data-stu-id="3b8cb-202">Next lesson</span></span>

<span data-ttu-id="3b8cb-203">Sabe cómo crear una pestaña para la colaboración.</span><span class="sxs-lookup"><span data-stu-id="3b8cb-203">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="3b8cb-204">¿Desea intentar compilar un tipo diferente de aplicación de Teams?</span><span class="sxs-lookup"><span data-stu-id="3b8cb-204">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b8cb-205">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="3b8cb-205">Build a bot</span></span>](../build-your-first-app/build-bot.md)
