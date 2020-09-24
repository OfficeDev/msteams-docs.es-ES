---
author: heath-hamilton
description: Obtenga información sobre cómo crear una pestaña de canal y de grupo para su primera aplicación de Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
title: Crear una ficha de canal y de grupo de Teams
ms.openlocfilehash: d97d8c13404077bff999db48b24b773aa4bc04ca
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237814"
---
# <a name="build-a-teams-channel-and-group-tab"></a><span data-ttu-id="5cc07-103">Crear una ficha de canal y de grupo de Teams</span><span class="sxs-lookup"><span data-stu-id="5cc07-103">Build a Teams channel and group tab</span></span>

<span data-ttu-id="5cc07-104">En este tutorial, creará una ficha de *canal* básico (también conocida como una *pestaña de grupo*), que es una página en pantalla completa para un canal o un chat de equipo.</span><span class="sxs-lookup"><span data-stu-id="5cc07-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="5cc07-105">A diferencia de una pestaña personal, los usuarios pueden configurar algunos aspectos de este tipo de pestaña (por ejemplo, cambiar el nombre de la ficha para que tenga sentido en su canal).</span><span class="sxs-lookup"><span data-stu-id="5cc07-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="5cc07-106">La asignación</span><span class="sxs-lookup"><span data-stu-id="5cc07-106">Your assignment</span></span>

<span data-ttu-id="5cc07-107">No hace mucho tiempo, su organización ha creado una ficha de Microsoft Teams con información sobre cómo ponerse en contacto con las funciones importantes (Departamento de soporte técnico, recursos humanos, etc.).</span><span class="sxs-lookup"><span data-stu-id="5cc07-107">Not long ago, your organization created a Teams tab with information on how to contact important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="5cc07-108">Sin embargo, como el ámbito de la pestaña solo es para uso personal, cada usuario debe instalar la ficha para verla y la adopción es inferior a la esperada.</span><span class="sxs-lookup"><span data-stu-id="5cc07-108">However, since the tab was scoped only for personal use, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="5cc07-109">En otras palabras, hay demasiados trabajadores que todavía no saben cómo llegar al Departamento de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="5cc07-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="5cc07-110">Puede facilitar la búsqueda de esta información si crea una pestaña de canal, lo que eliminará la carga de requerir que todos los usuarios instalen una aplicación.</span><span class="sxs-lookup"><span data-stu-id="5cc07-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="5cc07-111">En su lugar, un usuario puede instalar la pestaña en un canal o chatear para obtener el beneficio de todo el grupo.</span><span class="sxs-lookup"><span data-stu-id="5cc07-111">Instead, one user can install the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="5cc07-112">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="5cc07-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="5cc07-113">Crear un proyecto de aplicación con Microsoft Teams Toolkit para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5cc07-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="5cc07-114">Identificar algunas de las propiedades del manifiesto de la aplicación y scaffolding relevantes para las pestañas de canal y de grupo</span><span class="sxs-lookup"><span data-stu-id="5cc07-114">Identify some of the app manifest properties and scaffolding relevant to channel and group tabs</span></span>
> * <span data-ttu-id="5cc07-115">Hospedar una aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="5cc07-115">Host an app locally</span></span>
> * <span data-ttu-id="5cc07-116">Crear contenido de ficha</span><span class="sxs-lookup"><span data-stu-id="5cc07-116">Create tab content</span></span>
> * <span data-ttu-id="5cc07-117">Crear contenido para la página de configuración de una pestaña</span><span class="sxs-lookup"><span data-stu-id="5cc07-117">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="5cc07-118">Permitir la configuración y la instalación de una pestaña</span><span class="sxs-lookup"><span data-stu-id="5cc07-118">Allow a tab to be configured and installed</span></span>
> * <span data-ttu-id="5cc07-119">Proporcionar un nombre de pestaña sugerido</span><span class="sxs-lookup"><span data-stu-id="5cc07-119">Provide a suggested tab name</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="5cc07-120">1. crear un proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="5cc07-120">1. Create your app project</span></span>

<span data-ttu-id="5cc07-121">El kit de herramientas de Microsoft Teams le ayudará a configurar el manifiesto de la aplicación y los scaffolding relevantes para las pestañas de canal y grupo, incluida una página de configuración básica y una página de contenido que muestra un "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="5cc07-121">The Microsoft Teams Toolkit helps you set up the app manifest and scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="5cc07-122">Mensaje.</span><span class="sxs-lookup"><span data-stu-id="5cc07-122">message.</span></span>

> [!TIP]
> <span data-ttu-id="5cc07-123">Si no ha creado antes un proyecto de aplicación de Teams, puede resultar útil seguir [estas instrucciones](../build-your-first-app/build-and-run.md) que explican los proyectos con más detalle.</span><span class="sxs-lookup"><span data-stu-id="5cc07-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. En Visual Studio Code, seleccione **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: en la barra de actividad izquierda y elija **crear una nueva aplicación de Teams**.
1. <span data-ttu-id="5cc07-125">Escriba un nombre para la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="5cc07-125">Enter a name for your Teams app.</span></span> <span data-ttu-id="5cc07-126">(Este es el nombre predeterminado de la aplicación y también el nombre del directorio del proyecto de la aplicación en el equipo local).</span><span class="sxs-lookup"><span data-stu-id="5cc07-126">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="5cc07-127">En la pantalla **Agregar funciones** **, seleccione la pestaña luego** **grupo o grupo canal de Teams**.</span><span class="sxs-lookup"><span data-stu-id="5cc07-127">On the **Add capabilities** screen, select **Tab** then **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="5cc07-128">Seleccione **Finalizar** en la parte inferior de la pantalla para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="5cc07-128">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="5cc07-129">2. identificar los componentes relevantes del proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="5cc07-129">2. Identify relevant app project components</span></span>

<span data-ttu-id="5cc07-130">La gran parte del manifiesto de la aplicación y el scaffolding se configuran automáticamente al crear el proyecto con el kit de herramientas de Teams.</span><span class="sxs-lookup"><span data-stu-id="5cc07-130">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="5cc07-131">Echemos un vistazo a los componentes principales para crear una ficha de canal y de grupo.</span><span class="sxs-lookup"><span data-stu-id="5cc07-131">Let's look at the main components for building a channel and group tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="5cc07-132">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5cc07-132">App manifest</span></span>

<span data-ttu-id="5cc07-133">El siguiente fragmento de código del manifiesto de la aplicación muestra [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) , que incluye las propiedades y los valores predeterminados pertinentes para las pestañas de canal y grupo.</span><span class="sxs-lookup"><span data-stu-id="5cc07-133">The following snippet from the app manifest shows [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs), which includes the properties and default values relevant to channel and group tabs.</span></span>

```JSON
"configurableTabs": [
    {
        "configurationUrl": "{baseUrl0}/config",
        "canUpdateConfiguration": true,
        "scopes": [
            "team",
            "groupchat"
        ]
    }
],
```

* <span data-ttu-id="5cc07-134">`configurationUrl`: La dirección URL del host de la página de configuración de pestañas (debe ser HTTPS).</span><span class="sxs-lookup"><span data-stu-id="5cc07-134">`configurationUrl`: The host URL for your tab configuration page (must be HTTPS).</span></span>
* <span data-ttu-id="5cc07-135">`canUpdateConfiguration`: Si se establece en `true` , los usuarios pueden cambiar la configuración de las pestañas, cambiar el nombre de la pestaña o quitarla de un canal o un chat.</span><span class="sxs-lookup"><span data-stu-id="5cc07-135">`canUpdateConfiguration`: If set to `true`, users can change tab settings, rename the tab, or remove it from a channel or chat.</span></span>
* <span data-ttu-id="5cc07-136">`scopes`: Especifica si los usuarios pueden instalar la aplicación en los canales ( `team` ) y los chats ( `groupchat` ).</span><span class="sxs-lookup"><span data-stu-id="5cc07-136">`scopes`: Specifies if users can install the app in channels (`team`) and chats (`groupchat`).</span></span> <span data-ttu-id="5cc07-137">Se requiere al menos un valor.</span><span class="sxs-lookup"><span data-stu-id="5cc07-137">At least one value is required.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="5cc07-138">Scaffolding de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5cc07-138">App scaffolding</span></span>

<span data-ttu-id="5cc07-139">El scaffolding de la aplicación proporciona un `TabConfig.js` archivo, que se encuentra en el `src/components` directorio del proyecto, para representar la página de configuración de la pestaña (próximamente, esto es más).</span><span class="sxs-lookup"><span data-stu-id="5cc07-139">The app scaffolding provides a `TabConfig.js` file, located in the `src/components` directory of your project, for rendering your tab's configuration page (more on this soon).</span></span>

## <a name="3-run-your-app"></a><span data-ttu-id="5cc07-140">3. ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="5cc07-140">3. Run your app</span></span>

<span data-ttu-id="5cc07-141">En aras del tiempo, se creará y se ejecutará la aplicación de forma local.</span><span class="sxs-lookup"><span data-stu-id="5cc07-141">In the interest of time, you'll build and run your app locally.</span></span>

1. <span data-ttu-id="5cc07-142">En un terminal, vaya al directorio raíz del proyecto de aplicación y ejecute `npm install` .</span><span class="sxs-lookup"><span data-stu-id="5cc07-142">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="5cc07-143">Ejecutar `npm start` .</span><span class="sxs-lookup"><span data-stu-id="5cc07-143">Run `npm start`.</span></span>

<span data-ttu-id="5cc07-144">Una vez completada la **compilación correctamente.**</span><span class="sxs-lookup"><span data-stu-id="5cc07-144">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="5cc07-145">mensaje en el terminal.</span><span class="sxs-lookup"><span data-stu-id="5cc07-145">message in the terminal.</span></span>

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="5cc07-146">4. configurar un túnel seguro a la aplicación</span><span class="sxs-lookup"><span data-stu-id="5cc07-146">4. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="5cc07-147">Para fines de prueba, vamos a hospedar su pestaña en un servidor Web local (puerto 3000).</span><span class="sxs-lookup"><span data-stu-id="5cc07-147">For testing purposes, let's host your tab on a local web server (port 3000).</span></span>

1. <span data-ttu-id="5cc07-148">En un terminal, ejecute `ngrok http 3000` .</span><span class="sxs-lookup"><span data-stu-id="5cc07-148">In a terminal, run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="5cc07-149">Copie la dirección URL HTTPS que haya proporcionado.</span><span class="sxs-lookup"><span data-stu-id="5cc07-149">Copy the HTTPS URL you're provided.</span></span>
1. <span data-ttu-id="5cc07-150">En el `.publish` directorio, Abra `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="5cc07-150">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="5cc07-151">Reemplace el `baseUrl0` valor por la dirección URL copiada.</span><span class="sxs-lookup"><span data-stu-id="5cc07-151">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="5cc07-152">(Por ejemplo, cambie `baseUrl0=http://localhost:3000` a `baseUrl0=https://85528b2b3ca5.ngrok.io` ).</span><span class="sxs-lookup"><span data-stu-id="5cc07-152">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="5cc07-153">El manifiesto de la aplicación apunta al lugar donde hospeda la pestaña.</span><span class="sxs-lookup"><span data-stu-id="5cc07-153">Your app manifest is pointing to where you're hosting the tab.</span></span>

## <a name="5-customize-your-tab-content-page"></a><span data-ttu-id="5cc07-154">5. personalizar la página de contenido de la pestaña</span><span class="sxs-lookup"><span data-stu-id="5cc07-154">5. Customize your tab content page</span></span>

<span data-ttu-id="5cc07-155">Abra el manifiesto de la aplicación ( `manifest.json` ) en el `.publish` Directorio y establezca las siguientes propiedades en [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , que define la página de contenido de la pestaña.</span><span class="sxs-lookup"><span data-stu-id="5cc07-155">Open the app manifest (`manifest.json`) in the `.publish` directory and set the following properties in [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which defines your tab's content page.</span></span>

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "My Contacts",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

<span data-ttu-id="5cc07-156">Copie y actualice el siguiente fragmento de código con información relevante para su organización o, por el momento, use el código tal y como está.</span><span class="sxs-lookup"><span data-stu-id="5cc07-156">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="5cc07-157">Vaya al `src/components` Directorio y Abra `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="5cc07-157">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="5cc07-158">Busque la `render()` función y pegue el contenido dentro de `return()` (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="5cc07-158">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="5cc07-159">Agregue la regla siguiente a para que `App.css` los vínculos de correo electrónico sean más fáciles de leer independientemente del tema que se use.</span><span class="sxs-lookup"><span data-stu-id="5cc07-159">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="6-create-your-tab-configuration-page"></a><span data-ttu-id="5cc07-160">6. crear la página de configuración de pestañas</span><span class="sxs-lookup"><span data-stu-id="5cc07-160">6. Create your tab configuration page</span></span>

<span data-ttu-id="5cc07-161">Cada pestaña en un canal o chat tiene una página de configuración, un modal con al menos una opción de configuración que se muestra cuando los usuarios instalan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5cc07-161">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users install your app.</span></span> <span data-ttu-id="5cc07-162">De forma predeterminada, la página de configuración pregunta a los usuarios si quieren notificar al canal o al chat cuando se instala la ficha.</span><span class="sxs-lookup"><span data-stu-id="5cc07-162">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="5cc07-163">Agregue contenido a la página de configuración.</span><span class="sxs-lookup"><span data-stu-id="5cc07-163">Add some content to your configuration page.</span></span> <span data-ttu-id="5cc07-164">Vaya al directorio del proyecto `src/components` , Abra `TabConfig.js` e inserte contenido dentro de `return()` (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="5cc07-164">Go to your project's `src/components` directory, open `TabConfig.js`, and insert some content inside `return()` (as shown).</span></span>

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
> <span data-ttu-id="5cc07-165">Como mínimo, proporcione información breve sobre la aplicación en esta página, ya que esto puede ser la primera vez que los usuarios aprenden sobre ella.</span><span class="sxs-lookup"><span data-stu-id="5cc07-165">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="5cc07-166">También puede incluir opciones de configuración personalizadas o un [flujo de trabajo de autenticación](../tabs/how-to/authentication/auth-aad-sso.md), que es común en las páginas de configuración de pestañas.</span><span class="sxs-lookup"><span data-stu-id="5cc07-166">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="7-allow-the-tab-to-be-configured-and-installed"></a><span data-ttu-id="5cc07-167">7. permitir la configuración y la instalación de la pestaña</span><span class="sxs-lookup"><span data-stu-id="5cc07-167">7. Allow the tab to be configured and installed</span></span>

<span data-ttu-id="5cc07-168">Para que los usuarios puedan configurar e instalar correctamente la ficha, debe agregar la [dirección URL de host seguro que configuró](#4-set-up-a-secure-tunnel-to-your-app) en el componente de página de configuración.</span><span class="sxs-lookup"><span data-stu-id="5cc07-168">For users to successfully configure and install the tab, you must add the [secure host URL you set up](#4-set-up-a-secure-tunnel-to-your-app) to the configuration page component.</span></span>

<span data-ttu-id="5cc07-169">Vaya a `TabConfig.js` y busque `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="5cc07-169">Go to `TabConfig.js` and locate `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="5cc07-170">Para `"contentUrl"` , reemplace la `localhost:3000` parte de la dirección URL con el dominio en el que hospeda el contenido de la pestaña (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="5cc07-170">For `"contentUrl"`, replace the `localhost:3000` part of the URL with the domain where you're hosting the tab content (as shown).</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

<span data-ttu-id="5cc07-171">Además, asegúrese de que `microsoftTeams.settings.setValidityState(true);` .</span><span class="sxs-lookup"><span data-stu-id="5cc07-171">Also, make sure that `microsoftTeams.settings.setValidityState(true);`.</span></span> <span data-ttu-id="5cc07-172">De forma predeterminada, pero si se establece en `false` , el botón **Guardar** se deshabilita en la página Configuración.</span><span class="sxs-lookup"><span data-stu-id="5cc07-172">It is by default, but if set to `false`, the **Save** button is disabled on the configuration page.</span></span>

## <a name="8-provide-a-suggested-tab-name"></a><span data-ttu-id="5cc07-173">8. proporcionar un nombre de pestaña sugerido</span><span class="sxs-lookup"><span data-stu-id="5cc07-173">8. Provide a suggested tab name</span></span>

<span data-ttu-id="5cc07-174">Al instalar una pestaña para uso personal, el nombre para mostrar es la `name` propiedad en la `staticTabs` parte del manifiesto de la aplicación (por ejemplo, **mis contactos**).</span><span class="sxs-lookup"><span data-stu-id="5cc07-174">When you install a tab for personal use, the display name is the `name` property in the `staticTabs` portion of the app manifest (for example, **My Contacts**).</span></span> <span data-ttu-id="5cc07-175">Al instalar una pestaña de canal, se muestra el nombre de la aplicación (por ejemplo, **primera aplicación**) de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5cc07-175">When you install a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="5cc07-176">Esto puede ser adecuado, en función de lo que llame a su aplicación, pero puede que desee proporcionar un nombre que sea más lógico en el contexto de la colaboración en grupo (por ejemplo, los **contactos del equipo**).</span><span class="sxs-lookup"><span data-stu-id="5cc07-176">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="5cc07-177">En `TabConfig.js` , vuelva a `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="5cc07-177">In `TabConfig.js`, go back to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="5cc07-178">Agregue la `suggestedDisplayName` propiedad con el nombre de la pestaña que desee mostrar de forma predeterminada (como se muestra).</span><span class="sxs-lookup"><span data-stu-id="5cc07-178">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="5cc07-179">Use el nombre proporcionado o cree el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="5cc07-179">Use the provided name or create your own.</span></span> <span data-ttu-id="5cc07-180">Recuerde que en el manifiesto está permitiendo a los usuarios cambiar el nombre si lo desean.</span><span class="sxs-lookup"><span data-stu-id="5cc07-180">Remember, in the manifest you're allowing users to change the name if they want.</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="9-view-the-tab"></a><span data-ttu-id="5cc07-181">9. ver la pestaña</span><span class="sxs-lookup"><span data-stu-id="5cc07-181">9. View the tab</span></span>

<span data-ttu-id="5cc07-182">Para ver las páginas de contenido y configuración de la pestaña, debe instalarla en un canal o chat.</span><span class="sxs-lookup"><span data-stu-id="5cc07-182">To see your tab's configuration and content pages, you must install it in a channel or chat.</span></span>

1. <span data-ttu-id="5cc07-183">En el cliente de Microsoft Teams, seleccione **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5cc07-183">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="5cc07-184">Seleccione **cargar una aplicación personalizada** y elija la aplicación `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="5cc07-184">Select **Upload a custom app** and choose your app's `Development.zip`.</span></span>
1. <span data-ttu-id="5cc07-185">Elija **Agregar a un equipo** o **Agregar a un chat** y busque un canal o un chat que pueda usar para las pruebas.</span><span class="sxs-lookup"><span data-stu-id="5cc07-185">Choose **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="5cc07-186">Seleccione **configurar una pestaña**. Aparece la página Configuración.</span><span class="sxs-lookup"><span data-stu-id="5cc07-186">Select **Set up a tab**. The configuration page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Captura de pantalla de una página de configuración de ficha de canal.":::
1. <span data-ttu-id="5cc07-188">Seleccione **Guardar** para configurar la pestaña. Se muestra el contenido.</span><span class="sxs-lookup"><span data-stu-id="5cc07-188">Select **Save** to configure the tab. The content displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Captura de pantalla de una pestaña de canal con vista de contenido estático.":::

## <a name="well-done"></a><span data-ttu-id="5cc07-190">Bien hecho</span><span class="sxs-lookup"><span data-stu-id="5cc07-190">Well done</span></span>

<span data-ttu-id="5cc07-191">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="5cc07-191">Congratulations!</span></span> <span data-ttu-id="5cc07-192">Tiene una aplicación de Microsoft Teams con una pestaña para mostrar contenido útil en canales y chats.</span><span class="sxs-lookup"><span data-stu-id="5cc07-192">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="5cc07-193">Más información</span><span class="sxs-lookup"><span data-stu-id="5cc07-193">Learn more</span></span>

* <span data-ttu-id="5cc07-194">[Autenticar usuarios de pestaña con SSO](../tabs/how-to/authentication/auth-aad-sso.md): si solo quiere que los usuarios autorizados vean su pestaña, configure el inicio de sesión único (SSO) a través de Azure Active Directory (ad).</span><span class="sxs-lookup"><span data-stu-id="5cc07-194">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="5cc07-195">[Insertar contenido de una aplicación web o página web existente](../tabs/how-to/add-tab.md#tab-requirements): le mostramos cómo crear nuevo contenido para una pestaña personal, pero también puede cargar contenido desde una dirección URL externa.</span><span class="sxs-lookup"><span data-stu-id="5cc07-195">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="5cc07-196">[Crear una experiencia sin problemas para su pestaña](../tabs/design/tabs.md): Consulte las directrices recomendadas para diseñar pestañas de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="5cc07-196">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="5cc07-197">[Crear pestañas para móviles](../tabs/design/tabs-mobile.md): comprenda cómo desarrollar pestañas para teléfonos y tabletas.</span><span class="sxs-lookup"><span data-stu-id="5cc07-197">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="5cc07-198">Crear una ficha sin el kit de herramientas</span><span class="sxs-lookup"><span data-stu-id="5cc07-198">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="5cc07-199">Lección siguiente</span><span class="sxs-lookup"><span data-stu-id="5cc07-199">Next lesson</span></span>

<span data-ttu-id="5cc07-200">Sabe cómo crear una pestaña para la colaboración.</span><span class="sxs-lookup"><span data-stu-id="5cc07-200">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="5cc07-201">¿Desea intentar compilar un tipo diferente de aplicación de Teams?</span><span class="sxs-lookup"><span data-stu-id="5cc07-201">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5cc07-202">Crear un bot</span><span class="sxs-lookup"><span data-stu-id="5cc07-202">Build a bot</span></span>](../build-your-first-app/build-bot.md)
