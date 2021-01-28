---
title: Cargar la aplicación personalizada
description: Describe cómo cargar la aplicación en Microsoft Teams
ms.topic: how-to
keywords: Carga de aplicaciones de teams
ms.openlocfilehash: 2e7a21dc27fdfe824ecacebabbb61a3b99ae8e79
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014344"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="54af9-104">Cargar un paquete de aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="54af9-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="54af9-105">Para probar la experiencia de la aplicación en Microsoft Teams, debe cargar la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="54af9-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="54af9-106">La carga agrega la aplicación al equipo que seleccione y usted y los miembros del equipo pueden interactuar con ella como los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="54af9-106">Uploading adds the app to the team you select, and you and your team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="54af9-107">Es posible que al cargar un paquete actualizado para una aplicación existente con un bot no se muestren cambios en las pestañas cuando se visualizan a través de la ventana Conversaciones.</span><span class="sxs-lookup"><span data-stu-id="54af9-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the Conversations window.</span></span> <span data-ttu-id="54af9-108">Es mejor acceder a él a través del control desplegable Aplicaciones o probar en un entorno de prueba limpio.</span><span class="sxs-lookup"><span data-stu-id="54af9-108">It's better to access it via the Apps fly-out, or test on a clean test environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="54af9-109">Crear el paquete de carga</span><span class="sxs-lookup"><span data-stu-id="54af9-109">Create your upload package</span></span>

<span data-ttu-id="54af9-110">Para el desarrollo, así como el envío de AppSource (anteriormente Tienda Office), debe crear un paquete que se pueda cargar que contenga la información para describir su experiencia.</span><span class="sxs-lookup"><span data-stu-id="54af9-110">For development as well as AppSource (formerly Office Store) submission you must create an uploadable package that contains the information to describe your experience.</span></span> <span data-ttu-id="54af9-111">El paquete, un archivo .zip, contiene el manifiesto de la aplicación y los iconos que definen de forma única tu experiencia.</span><span class="sxs-lookup"><span data-stu-id="54af9-111">The package, a .zip file, contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="54af9-112">Para crear un paquete de carga, [consulte Crear el paquete para su aplicación de Microsoft Teams.](../build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="54af9-112">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="54af9-113">Con el paquete creado, ahora puede cargarlo en un equipo.</span><span class="sxs-lookup"><span data-stu-id="54af9-113">With your package created, you can now upload it into a team.</span></span> <span data-ttu-id="54af9-114">Una vez cargado, estará disponible para todos los usuarios del equipo seleccionado y solo para los usuarios de ese equipo.</span><span class="sxs-lookup"><span data-stu-id="54af9-114">Once uploaded it will be available for all users in the selected team, and only the users of that team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="54af9-115">Cargar el paquete en Teams</span><span class="sxs-lookup"><span data-stu-id="54af9-115">Load your package into Teams</span></span>

<span data-ttu-id="54af9-116">Puede probar el paquete carcándoselo en Teams.</span><span class="sxs-lookup"><span data-stu-id="54af9-116">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="54af9-117">Para que la carga funcione, el administrador del espacio empresarial debe habilitar primero [la carga de aplicaciones.](/microsoftteams/admin-settings)</span><span class="sxs-lookup"><span data-stu-id="54af9-117">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="54af9-118">Hay dos formas de cargar la aplicación en Teams:</span><span class="sxs-lookup"><span data-stu-id="54af9-118">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="54af9-119">Uso de la Tienda</span><span class="sxs-lookup"><span data-stu-id="54af9-119">Using the Store</span></span>
* <span data-ttu-id="54af9-120">Uso de la pestaña Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="54af9-120">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="54af9-121">Cargar el paquete en un equipo o conversación con la Tienda</span><span class="sxs-lookup"><span data-stu-id="54af9-121">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="54af9-122">En la esquina inferior izquierda de Teams, elija el icono de la Tienda.</span><span class="sxs-lookup"><span data-stu-id="54af9-122">In the lower left corner of Teams, choose the Store icon.</span></span> <span data-ttu-id="54af9-123">En la página de la Tienda, elija "Cargar una aplicación personalizada".</span><span class="sxs-lookup"><span data-stu-id="54af9-123">On the Store page, choose "Upload a custom app".</span></span>

  ![Ver equipo](../../assets/images/store-upload-a-custom-app2.png)

2. <span data-ttu-id="54af9-125">En el *cuadro de* diálogo Abrir, vaya al paquete que desea cargar y elija *Abrir.*</span><span class="sxs-lookup"><span data-stu-id="54af9-125">In the *Open* dialog, navigate to the package you want to upload and choose *Open*.</span></span>

   ![Menú Agregar](../../assets/images/NewappAddmenudropdown.png)

<span data-ttu-id="54af9-127">El paquete cargado ahora debe estar disponible para su uso en el equipo o la conversación especificada en el cuadro de diálogo de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="54af9-127">The uploaded package should now be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="54af9-128">Si la aplicación no aparece, la razón más común es un error en el manifiesto, especialmente ids para la aplicación, bot y extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="54af9-128">If your app does not appear, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span> <span data-ttu-id="54af9-129">Si la aplicación no está en el ámbito de las conversaciones, esa opción no aparecerá.</span><span class="sxs-lookup"><span data-stu-id="54af9-129">If the app is not scoped for conversations, that option will not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="54af9-130">Las aplicaciones en conversaciones se encuentran actualmente en [la versión](../../resources/dev-preview/developer-preview-intro.md)preliminar del desarrollador y la opción no aparecerá si Teams no se ejecuta en ese modo.</span><span class="sxs-lookup"><span data-stu-id="54af9-130">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option will not appear if Teams is not running in that mode.</span></span>

![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="54af9-132">Cargar el paquete en un equipo mediante la pestaña Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="54af9-132">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="54af9-133">En el equipo de destino, elija *Más opciones* (**&#8943;**) y elija *Administrar equipo*.</span><span class="sxs-lookup"><span data-stu-id="54af9-133">In the target team, choose *More options* (**&#8943;**) and choose *Manage team*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54af9-134">Debe ser el propietario del equipo o el propietario debe permitir que los usuarios agreguen los tipos de aplicación adecuados para que esta funcionalidad aparezca.</span><span class="sxs-lookup"><span data-stu-id="54af9-134">You must be the team owner, or the owner must allow users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="54af9-135">Seleccione la pestaña Aplicaciones y, a continuación, *elija Cargar una aplicación personalizada* en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="54af9-135">Select the Apps tab, and then choose *Upload a custom app* on the lower right.</span></span>

   ![Punto de entrada de carga](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="54af9-137">Busca y selecciona el paquete .zip del equipo.</span><span class="sxs-lookup"><span data-stu-id="54af9-137">Browse to and select your .zip package from your computer.</span></span>

4. <span data-ttu-id="54af9-138">Después de una breve pausa, verás la aplicación cargada en la lista.</span><span class="sxs-lookup"><span data-stu-id="54af9-138">After a brief pause you will see your uploaded app in the list.</span></span>

   ![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

<span data-ttu-id="54af9-140">Si la aplicación no se carga, la razón más común es un error en el manifiesto, especialmente ids para la aplicación, bot y extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="54af9-140">If your app does not load, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span>

## <a name="accessing-your-uploaded-configurable-tab"></a><span data-ttu-id="54af9-141">Acceso a la pestaña configurable cargada</span><span class="sxs-lookup"><span data-stu-id="54af9-141">Accessing your uploaded configurable tab</span></span>

<span data-ttu-id="54af9-142">Si la aplicación contiene pestañas, los usuarios pueden anclarlas a cualquier conversación o canal de equipo mediante el flujo estándar de la galería de pestañas:</span><span class="sxs-lookup"><span data-stu-id="54af9-142">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="54af9-143">Vaya a un canal del equipo.</span><span class="sxs-lookup"><span data-stu-id="54af9-143">Go to a channel in the team.</span></span> <span data-ttu-id="54af9-144">Elija *+* ( Agregar una pestaña )*a* la derecha de las pestañas existentes.</span><span class="sxs-lookup"><span data-stu-id="54af9-144">Choose *+* (*Add a tab*) to the right of the existing tabs.</span></span>

2. <span data-ttu-id="54af9-145">Seleccione la pestaña de la galería que aparece.</span><span class="sxs-lookup"><span data-stu-id="54af9-145">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="54af9-146">Acepte la solicitud de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="54af9-146">Accept the consent prompt.</span></span>

4. <span data-ttu-id="54af9-147">Configure la pestaña a través de [su página de configuración](../../tabs/how-to/create-tab-pages/configuration-page.md) y elija *Guardar*.</span><span class="sxs-lookup"><span data-stu-id="54af9-147">Configure your tab via its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and choose *Save*.</span></span>

  ![El cuadro de diálogo Agregar una pestaña, con una galería de pestañas disponibles](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a><span data-ttu-id="54af9-149">Obtener acceso al bot cargado</span><span class="sxs-lookup"><span data-stu-id="54af9-149">Accessing your uploaded bot</span></span>

<span data-ttu-id="54af9-150">Cuando agrega un bot a un equipo, debe poderlo usar cualquier persona de ese equipo, dentro y fuera de los canales del equipo, según la definición del ámbito del bot.</span><span class="sxs-lookup"><span data-stu-id="54af9-150">When you add a bot to a team, it should be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="54af9-151">Usted y otros miembros del equipo verán una publicación en el canal General que indica que el bot se ha agregado al equipo.</span><span class="sxs-lookup"><span data-stu-id="54af9-151">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="54af9-152">Para un bot habilitado para equipos, puede empezar invocando el bot @mentioning nombre del bot, que debería autocompletar.</span><span class="sxs-lookup"><span data-stu-id="54af9-152">For a teams-enabled bot, you can start by invoking your bot by @mentioning the name of the bot, which should autocomplete.</span></span>

<span data-ttu-id="54af9-153">Para probar chats directos con el bot, puede acceder a él a través de la página principal de la aplicación, @mention en un canal o buscarlo en la ventana De nuevo **chat.**</span><span class="sxs-lookup"><span data-stu-id="54af9-153">To test direct chats with your bot, you can either access it via the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="54af9-154">Al agregar el bot a una conversación Para probar chats directos con el bot, puede @mention en una conversación o buscarlo en la ventana Nuevo **chat.**</span><span class="sxs-lookup"><span data-stu-id="54af9-154">When you add your bot to a conversation To test direct chats with your bot, you can @mention it in a conversation, or search for it in the **New Chat** window.</span></span>

## <a name="accessing-your-uploaded-connector"></a><span data-ttu-id="54af9-155">Acceso al conector cargado</span><span class="sxs-lookup"><span data-stu-id="54af9-155">Accessing your uploaded Connector</span></span>

<span data-ttu-id="54af9-156">Con la aplicación cargada en el equipo o la conversación, los usuarios pueden configurar un conector mediante el flujo estándar de la galería de conectores:</span><span class="sxs-lookup"><span data-stu-id="54af9-156">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="54af9-157">Vaya a un canal del equipo.</span><span class="sxs-lookup"><span data-stu-id="54af9-157">Go to a channel in the team.</span></span> <span data-ttu-id="54af9-158">Elija *Más opciones* (*&#8943;*) y elija *Conectores*.</span><span class="sxs-lookup"><span data-stu-id="54af9-158">Choose *More options* (*&#8943;*) and choose *Connectors*.</span></span>

2. <span data-ttu-id="54af9-159">Seleccione el conector en la **sección de instalación local** en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="54af9-159">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="54af9-160">Configure el conector a través de [su página de configuración](../../webhooks-and-connectors/how-to/connectors-creating.md) y elija *Guardar*.</span><span class="sxs-lookup"><span data-stu-id="54af9-160">Configure your Connector via its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and choose *Save*.</span></span>

  ![El cuadro de diálogo Agregar una pestaña, con una galería de pestañas disponibles.](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a><span data-ttu-id="54af9-162">Acceso a la extensión de mensajería cargada</span><span class="sxs-lookup"><span data-stu-id="54af9-162">Accessing your uploaded messaging extension</span></span>

<span data-ttu-id="54af9-163">Una aplicación cargada con una extensión de mensajería aparece automáticamente en el menú Más opciones *(* *&#8943;*) en el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="54af9-163">An uploaded app with a messaging extension automatically appears in the *More options* (*&#8943;*) menu in the compose box.</span></span>

![Extensiones de mensajería](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a><span data-ttu-id="54af9-165">Quitar o actualizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="54af9-165">Removing or updating your app</span></span>

<span data-ttu-id="54af9-166">Si desea quitar la aplicación, seleccione el icono de papelera junto al nombre de la aplicación en la lista Ver bots de Teams.</span><span class="sxs-lookup"><span data-stu-id="54af9-166">If you want to remove your app, select the trash-can icon next to the app name in the View Teams bots list.</span></span>

<span data-ttu-id="54af9-167">Si cambia la información del manifiesto, primero debe quitar la aplicación y, a continuación, agregar el paquete actualizado (por cargar el paquete [en un equipo).](#load-your-package-into-teams)</span><span class="sxs-lookup"><span data-stu-id="54af9-167">If you change manifest information, you must first remove the app and then add the updated package (per [Load your package into a team](#load-your-package-into-teams)).</span></span> <span data-ttu-id="54af9-168">Ten en cuenta que, en general, los cambios de código en el servicio no requieren que vuelvas a cargar el manifiesto, a menos que dichos cambios requieran actualizaciones de manifiesto (como cambios en la dirección URL o el identificador de aplicación de Microsoft para su bot).</span><span class="sxs-lookup"><span data-stu-id="54af9-168">Note that, in general, code changes on your service do not require you to re-upload your manifest, unless those changes require manifest updates (such as changes to the URL or the Microsoft app ID for its bot).</span></span>

> [!NOTE]
> <span data-ttu-id="54af9-169">No hay ninguna manera de quitar completamente un bot del contexto personal.</span><span class="sxs-lookup"><span data-stu-id="54af9-169">There is no way to completely remove a bot from personal context.</span></span> <span data-ttu-id="54af9-170">Si el bot se quita y se vuelve a agregar, la comunicación adicional con el bot se anexará a la conversación anterior.</span><span class="sxs-lookup"><span data-stu-id="54af9-170">If the bot is removed and re-added, additional communication with the bot will append to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="54af9-171">Notas de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="54af9-171">Troubleshooting notes</span></span>

* <span data-ttu-id="54af9-172">Si el manifiesto no se carga, compruebe que ha [](../../concepts/build-and-test/apps-package.md) seguido todas las instrucciones de Crear el paquete y ha validado el manifiesto con el [esquema.](../../resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="54af9-172">If the manifest doesn't load, please double-check that you followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>
