---
title: Cargar la aplicación personalizada
description: Describe cómo cargar la aplicación en Microsoft Teams
ms.topic: how-to
ms.author: lajanuar
keywords: carga de aplicaciones de teams
ms.openlocfilehash: 3ca086cf8dbb992de84b22b7499f739d7c80b9d6
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479888"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="db7b6-104">Cargar un paquete de aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="db7b6-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="db7b6-105">Para probar la experiencia de la aplicación en Microsoft Teams, debes cargar la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="db7b6-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="db7b6-106">La carga agrega la aplicación al equipo seleccionado y todos los miembros del equipo pueden interactuar con ella como usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="db7b6-106">Uploading adds the app to the selected team and all the team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="db7b6-107">Es posible que cargar un paquete actualizado para una aplicación existente con un bot no muestre cambios de pestaña cuando se ve a través de la ventana de conversaciones.</span><span class="sxs-lookup"><span data-stu-id="db7b6-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the conversations window.</span></span> <span data-ttu-id="db7b6-108">Puedes acceder a la aplicación a través de las aplicaciones desvía o prueba en un entorno limpio.</span><span class="sxs-lookup"><span data-stu-id="db7b6-108">You can access the app through the apps fly-out or test in a clean environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="db7b6-109">Crear el paquete de carga</span><span class="sxs-lookup"><span data-stu-id="db7b6-109">Create your upload package</span></span>

<span data-ttu-id="db7b6-110">Para el desarrollo y el envío de AppSource, debe crear un paquete que pueda cargar.</span><span class="sxs-lookup"><span data-stu-id="db7b6-110">For development and AppSource submission, you must create a package that you can upload.</span></span> <span data-ttu-id="db7b6-111">El paquete debe contener la información para describir su experiencia.</span><span class="sxs-lookup"><span data-stu-id="db7b6-111">The package must contain the information to describe your experience.</span></span> <span data-ttu-id="db7b6-112">El paquete es un archivo .zip que contiene el manifiesto de la aplicación y los iconos que definen de forma única la experiencia.</span><span class="sxs-lookup"><span data-stu-id="db7b6-112">The package is a .zip file that contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="db7b6-113">Para crear un paquete de carga, consulta [Crear el paquete para la aplicación de Microsoft Teams](../build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="db7b6-113">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="db7b6-114">Después de crear el paquete, cárbalo en un equipo.</span><span class="sxs-lookup"><span data-stu-id="db7b6-114">After you create the package, upload it into a team.</span></span> <span data-ttu-id="db7b6-115">El paquete cargado solo está disponible para los usuarios del equipo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="db7b6-115">The uploaded package is only available to the users of the selected team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="db7b6-116">Cargar el paquete en Teams</span><span class="sxs-lookup"><span data-stu-id="db7b6-116">Load your package into Teams</span></span>

<span data-ttu-id="db7b6-117">Para probar el paquete, cárbalo en Teams.</span><span class="sxs-lookup"><span data-stu-id="db7b6-117">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="db7b6-118">Para que la carga funcione, el administrador del espacio empresarial debe habilitar primero [la carga de aplicaciones](/microsoftteams/admin-settings).</span><span class="sxs-lookup"><span data-stu-id="db7b6-118">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="db7b6-119">Hay dos formas de cargar la aplicación en Teams:</span><span class="sxs-lookup"><span data-stu-id="db7b6-119">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="db7b6-120">Uso de la Tienda</span><span class="sxs-lookup"><span data-stu-id="db7b6-120">Using the Store</span></span>
* <span data-ttu-id="db7b6-121">Uso de la pestaña Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="db7b6-121">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="db7b6-122">Cargar el paquete en un equipo o conversación con la Tienda</span><span class="sxs-lookup"><span data-stu-id="db7b6-122">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="db7b6-123">En la esquina inferior izquierda de Teams, elija el **icono De** la Tienda.</span><span class="sxs-lookup"><span data-stu-id="db7b6-123">In the lower left corner of Teams, choose the **Store** icon.</span></span> <span data-ttu-id="db7b6-124">En la página Tienda, elija **Cargar una aplicación personalizada.**</span><span class="sxs-lookup"><span data-stu-id="db7b6-124">On the Store page, choose **Upload a custom app**.</span></span>

  ![Ver equipo](../../assets/images/store-upload-a-custom-app2.png)

2. <span data-ttu-id="db7b6-126">En el **cuadro de** diálogo Abrir, vaya al paquete que desea cargar y elija Abrir.</span><span class="sxs-lookup"><span data-stu-id="db7b6-126">In the **Open** dialog, navigate to the package you want to upload and choose Open.</span></span>

   ![Menú Agregar](../../assets/images/NewappAddmenudropdown.png)

<span data-ttu-id="db7b6-128">El paquete cargado debe estar disponible para su uso en el equipo o conversación especificado en el cuadro de diálogo de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="db7b6-128">The uploaded package must be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="db7b6-129">Si la aplicación no aparece, el motivo más común es un error en el manifiesto, en particular los IDs de las extensiones de aplicación, bot y mensajería.</span><span class="sxs-lookup"><span data-stu-id="db7b6-129">If your app does not appear, the most common reason is an error in the manifest, particularly IDs for the app, bot, and messaging extensions.</span></span> <span data-ttu-id="db7b6-130">Si la aplicación no está en el ámbito de las conversaciones, esa opción no aparece.</span><span class="sxs-lookup"><span data-stu-id="db7b6-130">If the app is not scoped for conversations that option does not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="db7b6-131">Las aplicaciones en conversaciones se encuentran actualmente en [Developer Preview](../../resources/dev-preview/developer-preview-intro.md)y la opción no aparece si Teams no se ejecuta en ese modo.</span><span class="sxs-lookup"><span data-stu-id="db7b6-131">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option does not appear if Teams is not running in that mode.</span></span>

![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="db7b6-133">Cargar el paquete en un equipo mediante la pestaña Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="db7b6-133">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="db7b6-134">En el equipo de destino, elija **Más opciones** (**&#8943;**) y seleccione **Administrar equipo**.</span><span class="sxs-lookup"><span data-stu-id="db7b6-134">In the target team, choose **More options** (**&#8943;**) and select **Manage team**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="db7b6-135">Debes ser el propietario del equipo o el propietario debe dar acceso a los usuarios para agregar los tipos de aplicación adecuados para que aparezca esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="db7b6-135">You must be the team owner or the owner must give access to users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="db7b6-136">Selecciona la **pestaña** Aplicaciones y elige **Cargar una aplicación personalizada** en la parte inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="db7b6-136">Select the **Apps** tab and choose **Upload a custom app** on the lower right.</span></span>

   ![Punto de entrada de carga](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="db7b6-138">Seleccione el paquete .zip del equipo.</span><span class="sxs-lookup"><span data-stu-id="db7b6-138">Select your .zip package from the computer.</span></span>

4. <span data-ttu-id="db7b6-139">Puedes ver la aplicación cargada en la lista.</span><span class="sxs-lookup"><span data-stu-id="db7b6-139">You can see your uploaded app in the list.</span></span>

   ![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

<span data-ttu-id="db7b6-141">Si la aplicación no se carga, el motivo más común es un error en el manifiesto, en particular los IDs de las extensiones de aplicación, bot y mensajería.</span><span class="sxs-lookup"><span data-stu-id="db7b6-141">If your app does not load, the most common reason is an error in the manifest, particularly IDs for the app, bot, and messaging extensions.</span></span>

## <a name="access-your-uploaded-configurable-tab"></a><span data-ttu-id="db7b6-142">Acceder a la pestaña configurable cargada</span><span class="sxs-lookup"><span data-stu-id="db7b6-142">Access your uploaded configurable tab</span></span>

<span data-ttu-id="db7b6-143">Si la aplicación contiene pestañas, los usuarios pueden anclarlas a cualquier conversación o canal de grupo mediante el flujo de galería de pestañas estándar:</span><span class="sxs-lookup"><span data-stu-id="db7b6-143">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="db7b6-144">Vaya a un canal del equipo.</span><span class="sxs-lookup"><span data-stu-id="db7b6-144">Go to a channel in the team.</span></span> <span data-ttu-id="db7b6-145">Elija **+** agregar una pestaña a la derecha de las pestañas existentes.</span><span class="sxs-lookup"><span data-stu-id="db7b6-145">Choose **+** to add a tab to the right of the existing tabs.</span></span>

2. <span data-ttu-id="db7b6-146">Seleccione la pestaña de la galería que aparece.</span><span class="sxs-lookup"><span data-stu-id="db7b6-146">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="db7b6-147">Acepte el símbolo del sistema de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="db7b6-147">Accept the consent prompt.</span></span>

4. <span data-ttu-id="db7b6-148">Configure la pestaña a través de [su página de configuración](../../tabs/how-to/create-tab-pages/configuration-page.md) y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="db7b6-148">Configure your tab through its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and select **Save**.</span></span>

  ![Cuadro de diálogo Agregar una pestaña con una galería de pestañas disponibles](../../assets/images/tab_gallery.png)

## <a name="access-your-uploaded-bot"></a><span data-ttu-id="db7b6-150">Obtener acceso al bot cargado</span><span class="sxs-lookup"><span data-stu-id="db7b6-150">Access your uploaded bot</span></span>

<span data-ttu-id="db7b6-151">Después de agregar el bot a un equipo, debe ser usable por cualquiera de ese equipo, dentro y fuera de los canales del equipo, según la definición del ámbito del bot.</span><span class="sxs-lookup"><span data-stu-id="db7b6-151">After adding the bot to a team, it must be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="db7b6-152">Todos los miembros del equipo pueden ver una publicación en el **canal General** que indica que el bot se ha agregado al equipo.</span><span class="sxs-lookup"><span data-stu-id="db7b6-152">All team members can see a post in the **General** channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="db7b6-153">Para un bot de Teams, puede empezar invocando el bot @mentioning el nombre del bot.</span><span class="sxs-lookup"><span data-stu-id="db7b6-153">For a Teams bot, you can start by invoking your bot by @mentioning the name of the bot.</span></span>

<span data-ttu-id="db7b6-154">Para probar chats directos con el bot, puedes acceder a él a través de la página principal de la aplicación, @mention en un canal o buscarlo en la ventana Nuevo **chat.**</span><span class="sxs-lookup"><span data-stu-id="db7b6-154">To test direct chats with your bot, you can either access it through the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="db7b6-155">Puedes @mention bot en una conversación o buscarlo en la ventana Nuevo **chat** para probar chats directos con el bot.</span><span class="sxs-lookup"><span data-stu-id="db7b6-155">You can @mention the bot in a conversation or search for it in the **New Chat** window to test direct chats with your bot.</span></span>

## <a name="access-your-uploaded-connector"></a><span data-ttu-id="db7b6-156">Obtener acceso al conector cargado</span><span class="sxs-lookup"><span data-stu-id="db7b6-156">Access your uploaded Connector</span></span>

<span data-ttu-id="db7b6-157">Con la aplicación cargada en el equipo o la conversación, los usuarios pueden configurar un conector con el flujo de galería de conectores estándar:</span><span class="sxs-lookup"><span data-stu-id="db7b6-157">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="db7b6-158">Vaya a un canal del equipo.</span><span class="sxs-lookup"><span data-stu-id="db7b6-158">Go to a channel in the team.</span></span> <span data-ttu-id="db7b6-159">Elija **Más opciones** (*&#8943;*) y elija **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="db7b6-159">Choose **More options** (*&#8943;*) and choose **Connectors**.</span></span>

2. <span data-ttu-id="db7b6-160">Seleccione el conector en la **sección Sideloaded** en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="db7b6-160">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="db7b6-161">Configure el conector a través de su [página de configuración](../../webhooks-and-connectors/how-to/connectors-creating.md) y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="db7b6-161">Configure your connector through its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and select **Save**.</span></span>

  ![El cuadro de diálogo Agregar una pestaña, con una galería de pestañas disponibles.](../../assets/images/connector_gallery.png)

## <a name="access-your-uploaded-messaging-extension"></a><span data-ttu-id="db7b6-163">Obtener acceso a la extensión de mensajería cargada</span><span class="sxs-lookup"><span data-stu-id="db7b6-163">Access your uploaded messaging extension</span></span>

<span data-ttu-id="db7b6-164">Una aplicación cargada con una extensión de mensajería aparece automáticamente en el menú Más **opciones** (*&#8943;*) en el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="db7b6-164">An uploaded app with a messaging extension automatically appears in the **More options** (*&#8943;*) menu in the compose box.</span></span>

![Extensiones de mensajería](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="add-a-default-install-scope-and-group-capability"></a><span data-ttu-id="db7b6-166">Agregar un ámbito de instalación predeterminado y una funcionalidad de grupo</span><span class="sxs-lookup"><span data-stu-id="db7b6-166">Add a default install scope and group capability</span></span>

> [!NOTE]
> <span data-ttu-id="db7b6-167">Actualmente, el ámbito de instalación predeterminado y la funcionalidad de grupo solo están disponibles en la versión preliminar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="db7b6-167">The default install scope and group capability is currently available in developer preview only.</span></span>

<span data-ttu-id="db7b6-168">Aunque la instalación de una aplicación en el ámbito personal funciona para la mayoría de las aplicaciones, algunas de las aplicaciones de la Tienda Teams admiten ámbitos personales y de equipo.</span><span class="sxs-lookup"><span data-stu-id="db7b6-168">Although installing an app in the personal scope works for most apps, some of the apps in Teams Store support both personal and team scopes.</span></span>
<span data-ttu-id="db7b6-169">Algunas de estas aplicaciones están diseñadas para trabajar en un equipo, reuniones o un chat en grupo, con una experiencia de aplicación personal secundaria.</span><span class="sxs-lookup"><span data-stu-id="db7b6-169">Some of these apps are intended to work in a team, meetings, or a groupchat, with personal app experience being secondary.</span></span>
<span data-ttu-id="db7b6-170">La selección predeterminada del ámbito de instalación te ayuda a especificar las `defaultInstallScope` aplicaciones que publicas.</span><span class="sxs-lookup"><span data-stu-id="db7b6-170">The default install scope selection helps you to specify the `defaultInstallScope` for the apps that you publish.</span></span> <span data-ttu-id="db7b6-171">La experiencia de instalación de la aplicación hace que las opciones predeterminadas estén disponibles para el usuario, mientras que el resto se mueve debajo del galón como se resalta en la imagen.</span><span class="sxs-lookup"><span data-stu-id="db7b6-171">The app installation experience makes the default options available to the user, while the rest is moved under the chevron as highlighted in the image.</span></span>

![Agregar una aplicación](../../assets/images/compose-extensions/addanapp.png)

<span data-ttu-id="db7b6-173">La `defaultInstallScope` propiedad admite valores, como personal, team, groupchat o reuniones.</span><span class="sxs-lookup"><span data-stu-id="db7b6-173">The `defaultInstallScope` property supports values, such as personal, team, groupchat, or meetings.</span></span>

> [!NOTE]
><span data-ttu-id="db7b6-174">`defaultGroupCapability` proporciona la funcionalidad predeterminada que se agrega al equipo, el chat de grupo o las reuniones.</span><span class="sxs-lookup"><span data-stu-id="db7b6-174">`defaultGroupCapability` provides the default capability that is added to the team, groupchat or meetings.</span></span> <span data-ttu-id="db7b6-175">Elige una pestaña, bot o conector como la funcionalidad predeterminada de la aplicación, pero debes asegurarte de que has proporcionado la funcionalidad seleccionada en la definición de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="db7b6-175">Choose a tab, bot, or connector as the default capability for your app, but you must ensure that you have provided the selected capability in your app definition.</span></span>

## <a name="remove-or-update-your-app"></a><span data-ttu-id="db7b6-176">Quitar o actualizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="db7b6-176">Remove or update your app</span></span>

<span data-ttu-id="db7b6-177">Para quitar la aplicación, selecciona el icono eliminar situado junto al nombre de la aplicación en la lista Ver bots de **Teams.**</span><span class="sxs-lookup"><span data-stu-id="db7b6-177">To remove your app, select the delete icon next to the app name in the **View Teams** bots list.</span></span> <span data-ttu-id="db7b6-178">Si cambias la información del manifiesto, primero quitas la aplicación y luego agregas el paquete actualizado, consulta [Cargar el paquete en un equipo](#load-your-package-into-teams).</span><span class="sxs-lookup"><span data-stu-id="db7b6-178">If you change manifest information, first remove the app and then add the updated package, see [Load your package into a team](#load-your-package-into-teams).</span></span> <span data-ttu-id="db7b6-179">Los cambios de código en el servicio no requieren que vuelva a cargar el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="db7b6-179">Code changes on your service do not require you to upload your manifest again.</span></span> <span data-ttu-id="db7b6-180">Sin embargo, si los cambios de código requieren actualizaciones de manifiesto, como cambios en la dirección URL o el identificador de aplicación de Microsoft para su bot, debes cargar el manifiesto de nuevo.</span><span class="sxs-lookup"><span data-stu-id="db7b6-180">However, if the code changes require manifest updates, such as changes to the URL or the Microsoft app ID for its bot, you must upload the manifest again.</span></span>

> [!NOTE]
> <span data-ttu-id="db7b6-181">No se puede quitar un bot de un contexto personal por completo.</span><span class="sxs-lookup"><span data-stu-id="db7b6-181">You cannot remove a bot from a personal context entirely.</span></span> <span data-ttu-id="db7b6-182">Si el bot se quita y se agrega de nuevo, la comunicación adicional con el bot se anexa a la conversación anterior.</span><span class="sxs-lookup"><span data-stu-id="db7b6-182">If the bot is removed and added again, additional communication with the bot appends to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="db7b6-183">Notas de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="db7b6-183">Troubleshooting notes</span></span>

<span data-ttu-id="db7b6-184">Si el manifiesto no se carga, compruebe si ha seguido todas las instrucciones de [Crear el](../../concepts/build-and-test/apps-package.md) paquete y validó el manifiesto con el [esquema](../../resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="db7b6-184">If the manifest fails to load, check if you have followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>
