---
title: Cargar la aplicación personalizada en Microsoft Teams
description: Describe cómo cargar la aplicación en Microsoft Teams.
keywords: Carga de aplicaciones de Microsoft Teams
ms.openlocfilehash: 6fbcd7a81c113d25a26ee6db15865929a53def0d
ms.sourcegitcommit: 560bf433129c16888135879e2703dbdeb38ec99f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397711"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="90790-104">Cargar un paquete de aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="90790-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="90790-105">Para probar la experiencia de la aplicación en Microsoft Teams, debe cargar la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="90790-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="90790-106">La carga agrega la aplicación al equipo que seleccione, y usted y los miembros del equipo pueden interactuar con ella como los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="90790-106">Uploading adds the app to the team you select, and you and your team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="90790-107">Cargar un paquete actualizado para una aplicación existente con un bot no puede mostrar cambios de ficha cuando se muestra en la ventana conversaciones.</span><span class="sxs-lookup"><span data-stu-id="90790-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the Conversations window.</span></span> <span data-ttu-id="90790-108">Es mejor acceder a él a través de la volar con las aplicaciones o probar en un entorno de prueba limpio.</span><span class="sxs-lookup"><span data-stu-id="90790-108">It's better to access it via the Apps fly-out, or test on a clean test environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="90790-109">Crear el paquete de carga</span><span class="sxs-lookup"><span data-stu-id="90790-109">Create your upload package</span></span>

<span data-ttu-id="90790-110">Para el envío de AppSource (anteriormente tienda Office), debe crear un paquete que se pueda cargar y que contenga la información que describe su experiencia.</span><span class="sxs-lookup"><span data-stu-id="90790-110">For development as well as AppSource (formerly Office Store) submission you must create an uploadable package that contains the information to describe your experience.</span></span> <span data-ttu-id="90790-111">El paquete, un archivo. zip, contiene el manifiesto de aplicación y los iconos que definen su experiencia de forma exclusiva.</span><span class="sxs-lookup"><span data-stu-id="90790-111">The package, a .zip file, contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="90790-112">Para crear un paquete de carga, consulte [Create the Package for your Microsoft Teams App](../build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="90790-112">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="90790-113">Una vez creado el paquete, ahora puede cargarlo en un equipo.</span><span class="sxs-lookup"><span data-stu-id="90790-113">With your package created, you can now upload it into a team.</span></span> <span data-ttu-id="90790-114">Una vez cargada, estará disponible para todos los usuarios del equipo seleccionado y solo para los usuarios de ese equipo.</span><span class="sxs-lookup"><span data-stu-id="90790-114">Once uploaded it will be available for all users in the selected team, and only the users of that team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="90790-115">Cargar el paquete en Teams</span><span class="sxs-lookup"><span data-stu-id="90790-115">Load your package into Teams</span></span>

<span data-ttu-id="90790-116">Puede probar el paquete al cargarlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="90790-116">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="90790-117">Para que funcione la carga, el administrador de espacios empresariales debe [Habilitar primero la carga de aplicaciones](/microsoftteams/admin-settings).</span><span class="sxs-lookup"><span data-stu-id="90790-117">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="90790-118">Hay dos formas de cargar la aplicación a Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="90790-118">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="90790-119">Uso de la tienda</span><span class="sxs-lookup"><span data-stu-id="90790-119">Using the Store</span></span>
* <span data-ttu-id="90790-120">Uso de la pestaña apps</span><span class="sxs-lookup"><span data-stu-id="90790-120">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="90790-121">Cargar el paquete en un equipo o conversación mediante la tienda</span><span class="sxs-lookup"><span data-stu-id="90790-121">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="90790-122">En la esquina inferior izquierda de Microsoft Teams, elija el icono de tienda.</span><span class="sxs-lookup"><span data-stu-id="90790-122">In the lower left corner of Teams, choose the Store icon.</span></span> <span data-ttu-id="90790-123">En la página tienda, elija "cargar una aplicación personalizada".</span><span class="sxs-lookup"><span data-stu-id="90790-123">On the Store page, choose "Upload a custom app".</span></span>

  ![Ver equipo](../../assets/images/store-upload-a-custom-app2.png)

2. <span data-ttu-id="90790-125">En el cuadro de diálogo *abrir* , navegue hasta el paquete que desea cargar y elija *abrir*.</span><span class="sxs-lookup"><span data-stu-id="90790-125">In the *Open* dialog, navigate to the package you want to upload and choose *Open*.</span></span>

   ![Agregar menú](../../assets/images/NewappAddmenudropdown.png)

<span data-ttu-id="90790-127">El paquete cargado ahora debería estar disponible para su uso en el equipo o la conversación especificados en el cuadro de diálogo de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="90790-127">The uploaded package should now be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="90790-128">Si la aplicación no aparece, la causa más común es un error en el manifiesto, especialmente identificadores para las extensiones de aplicación, Bot y mensajería.</span><span class="sxs-lookup"><span data-stu-id="90790-128">If your app does not appear, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span> <span data-ttu-id="90790-129">Si la aplicación no tiene el ámbito de las conversaciones, esa opción no aparecerá.</span><span class="sxs-lookup"><span data-stu-id="90790-129">If the app is not scoped for conversations, that option will not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="90790-130">Aplicaciones en conversaciones se encuentra actualmente en [versión preliminar para desarrolladores](../../resources/dev-preview/developer-preview-intro.md)y la opción no aparecerá si Teams no se está ejecutando en ese modo.</span><span class="sxs-lookup"><span data-stu-id="90790-130">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option will not appear if Teams is not running in that mode.</span></span>

![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="90790-132">Cargar el paquete en un equipo mediante la pestaña aplicaciones</span><span class="sxs-lookup"><span data-stu-id="90790-132">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="90790-133">En el equipo de destino, elija *más opciones* (**&#8943;**) y elija *administrar equipo*.</span><span class="sxs-lookup"><span data-stu-id="90790-133">In the target team, choose *More options* (**&#8943;**) and choose *Manage team*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="90790-134">Debe ser el propietario del equipo o el propietario debe permitir que los usuarios agreguen los tipos de aplicación adecuados para que aparezca esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="90790-134">You must be the team owner, or the owner must allow users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="90790-135">Seleccione la pestaña Aplicaciones y, a continuación, elija *cargar una aplicación personalizada* en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="90790-135">Select the Apps tab, and then choose *Upload a custom app* on the lower right.</span></span>

   ![Cargar punto de entrada](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="90790-137">Busca y selecciona el paquete. zip del equipo.</span><span class="sxs-lookup"><span data-stu-id="90790-137">Browse to and select your .zip package from your computer.</span></span>

4. <span data-ttu-id="90790-138">Tras una breve pausa, verá la aplicación cargada en la lista.</span><span class="sxs-lookup"><span data-stu-id="90790-138">After a brief pause you will see your uploaded app in the list.</span></span>

   ![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

<span data-ttu-id="90790-140">Si la aplicación no se carga, la causa más común es un error en el manifiesto, especialmente identificadores para las extensiones de aplicación, Bot y mensajería.</span><span class="sxs-lookup"><span data-stu-id="90790-140">If your app does not load, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span>

## <a name="accessing-your-uploaded-configurable-tab"></a><span data-ttu-id="90790-141">Acceso a la pestaña configurable cargada</span><span class="sxs-lookup"><span data-stu-id="90790-141">Accessing your uploaded configurable tab</span></span>

<span data-ttu-id="90790-142">Si la aplicación contiene pestañas, los usuarios pueden anclarlos a cualquier canal de conversación o equipo mediante el flujo de la galería de pestañas estándar:</span><span class="sxs-lookup"><span data-stu-id="90790-142">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="90790-143">Vaya a un canal del equipo.</span><span class="sxs-lookup"><span data-stu-id="90790-143">Go to a channel in the team.</span></span> <span data-ttu-id="90790-144">Elija *+* (*Agregar una pestaña*) a la derecha de las pestañas existentes.</span><span class="sxs-lookup"><span data-stu-id="90790-144">Choose *+* (*Add a tab*) to the right of the existing tabs.</span></span>

2. <span data-ttu-id="90790-145">Seleccione su pestaña en la galería que aparece.</span><span class="sxs-lookup"><span data-stu-id="90790-145">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="90790-146">Acepte la solicitud de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="90790-146">Accept the consent prompt.</span></span>

4. <span data-ttu-id="90790-147">Configure su pestaña mediante su [Página de configuración](../../tabs/how-to/create-tab-pages/configuration-page.md) y elija *Guardar*.</span><span class="sxs-lookup"><span data-stu-id="90790-147">Configure your tab via its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and choose *Save*.</span></span>

  ![El cuadro de diálogo Agregar una pestaña, que incluye una galería de pestañas disponibles](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a><span data-ttu-id="90790-149">Acceso a su bot cargado</span><span class="sxs-lookup"><span data-stu-id="90790-149">Accessing your uploaded bot</span></span>

<span data-ttu-id="90790-150">Cuando se agrega un bot a un equipo, el usuario debe usarlo en ese equipo, dentro y fuera de los canales del equipo, según la definición del ámbito de los robots.</span><span class="sxs-lookup"><span data-stu-id="90790-150">When you add a bot to a team, it should be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="90790-151">Usted y otros miembros del equipo verán una publicación en el canal general que indica que el bot se ha agregado al equipo.</span><span class="sxs-lookup"><span data-stu-id="90790-151">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="90790-152">Para un bot habilitado para Teams, puede empezar invocando el bot @mentioning el nombre del bot, que debe Autocompletar.</span><span class="sxs-lookup"><span data-stu-id="90790-152">For a teams-enabled bot, you can start by invoking your bot by @mentioning the name of the bot, which should autocomplete.</span></span>

<span data-ttu-id="90790-153">Para probar chats directos con el bot, puede tener acceso a él a través de la Página principal de la aplicación, @mention en un canal o buscarlo en la nueva ventana de **chat** .</span><span class="sxs-lookup"><span data-stu-id="90790-153">To test direct chats with your bot, you can either access it via the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="90790-154">Cuando se agrega un bot a una conversación para probar chats directos con el bot, se puede @mention en una conversación o buscar en la nueva ventana de **chat** .</span><span class="sxs-lookup"><span data-stu-id="90790-154">When you add your bot to a conversation To test direct chats with your bot, you can @mention it in a conversation, or search for it in the **New Chat** window.</span></span>

## <a name="accessing-your-uploaded-connector"></a><span data-ttu-id="90790-155">Obtener acceso al conector cargado</span><span class="sxs-lookup"><span data-stu-id="90790-155">Accessing your uploaded Connector</span></span>

<span data-ttu-id="90790-156">Con la aplicación cargada en el equipo o la conversación, los usuarios pueden configurar un conector mediante el flujo de la galería de conectores estándar:</span><span class="sxs-lookup"><span data-stu-id="90790-156">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="90790-157">Vaya a un canal del equipo.</span><span class="sxs-lookup"><span data-stu-id="90790-157">Go to a channel in the team.</span></span> <span data-ttu-id="90790-158">Elija *más opciones* (*&#8943;*) y elija *conectores*.</span><span class="sxs-lookup"><span data-stu-id="90790-158">Choose *More options* (*&#8943;*) and choose *Connectors*.</span></span>

2. <span data-ttu-id="90790-159">Seleccione el conector de la sección **transferidas localmente** en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="90790-159">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="90790-160">Configure el conector mediante su [Página de configuración](../../webhooks-and-connectors/how-to/connectors-creating.md) y elija *Guardar*.</span><span class="sxs-lookup"><span data-stu-id="90790-160">Configure your Connector via its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and choose *Save*.</span></span>

  ![El cuadro de diálogo Agregar una pestaña, que incluye una galería de pestañas disponibles.](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a><span data-ttu-id="90790-162">Obtener acceso a la extensión de mensajería cargada</span><span class="sxs-lookup"><span data-stu-id="90790-162">Accessing your uploaded messaging extension</span></span>

<span data-ttu-id="90790-163">Una aplicación cargada con una extensión de mensajería aparece automáticamente en el menú *más opciones* (*&#8943;*) en el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="90790-163">An uploaded app with a messaging extension automatically appears in the *More options* (*&#8943;*) menu in the compose box.</span></span>

![Extensiones de mensajería](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a><span data-ttu-id="90790-165">Quitar o actualizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="90790-165">Removing or updating your app</span></span>

<span data-ttu-id="90790-166">Si quiere quitar la aplicación, seleccione el icono de papelera que aparece junto al nombre de la aplicación en la lista Ver bots de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="90790-166">If you want to remove your app, select the trash-can icon next to the app name in the View Teams bots list.</span></span>

<span data-ttu-id="90790-167">Si cambia la información del manifiesto, primero debe quitar la aplicación y, a continuación, agregar el paquete actualizado (por [cargar el paquete en un equipo](#load-your-package-into-teams)).</span><span class="sxs-lookup"><span data-stu-id="90790-167">If you change manifest information, you must first remove the app and then add the updated package (per [Load your package into a team](#load-your-package-into-teams)).</span></span> <span data-ttu-id="90790-168">Tenga en cuenta que, en general, los cambios de código en el servicio no requieren que vuelva a cargar el manifiesto, a menos que estos cambios requieran actualizaciones del manifiesto (como cambios en la dirección URL o el identificador de aplicación de Microsoft para su bot).</span><span class="sxs-lookup"><span data-stu-id="90790-168">Note that, in general, code changes on your service do not require you to re-upload your manifest, unless those changes require manifest updates (such as changes to the URL or the Microsoft app ID for its bot).</span></span>

> [!NOTE]
> <span data-ttu-id="90790-169">No hay ninguna forma de quitar por completo un bot del contexto personal.</span><span class="sxs-lookup"><span data-stu-id="90790-169">There is no way to completely remove a bot from personal context.</span></span> <span data-ttu-id="90790-170">Si se quita y vuelve a agregar el bot, la comunicación adicional con el bot se agregará a la conversación anterior.</span><span class="sxs-lookup"><span data-stu-id="90790-170">If the bot is removed and re-added, additional communication with the bot will append to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="90790-171">Notas de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="90790-171">Troubleshooting notes</span></span>

* <span data-ttu-id="90790-172">Si el manifiesto no se carga, compruebe que ha seguido todas las instrucciones de [Create the package](../../concepts/build-and-test/apps-package.md) y validad The manifest en el [esquema](../../resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="90790-172">If the manifest doesn't load, please double-check that you followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>

