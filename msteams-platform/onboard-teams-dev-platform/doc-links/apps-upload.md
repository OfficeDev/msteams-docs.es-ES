---
title: Cargar la aplicación personalizada en Microsoft Teams
description: Describe cómo cargar la aplicación en Microsoft Teams.
keywords: Carga de aplicaciones de Microsoft Teams
ms.openlocfilehash: 1ab8d720ecb321796ede0677effec1070e5ee21d
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652213"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="cc525-104">Cargar un paquete de aplicación en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cc525-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="cc525-105">Para probar la experiencia de la aplicación en Microsoft Teams, debe cargar la aplicación en Teams.</span><span class="sxs-lookup"><span data-stu-id="cc525-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="cc525-106">La carga agrega la aplicación al equipo que seleccione, y usted y los miembros del equipo pueden interactuar con ella como los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="cc525-106">Uploading adds the app to the team you select, and you and your team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="cc525-107">Cargar un paquete actualizado para una aplicación existente con un bot no puede mostrar cambios de ficha cuando se muestra en la ventana conversaciones.</span><span class="sxs-lookup"><span data-stu-id="cc525-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the Conversations window.</span></span> <span data-ttu-id="cc525-108">Es mejor acceder a él a través de la volar con las aplicaciones o probar en un entorno de prueba limpio.</span><span class="sxs-lookup"><span data-stu-id="cc525-108">It's better to access it via the Apps fly-out, or test on a clean test environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="cc525-109">Crear el paquete de carga</span><span class="sxs-lookup"><span data-stu-id="cc525-109">Create your upload package</span></span>

<span data-ttu-id="cc525-110">Para el envío de AppSource (anteriormente tienda Office), debe crear un paquete que se pueda cargar y que contenga la información que describe su experiencia.</span><span class="sxs-lookup"><span data-stu-id="cc525-110">For development as well as AppSource (formerly Office Store) submission you must create an uploadable package that contains the information to describe your experience.</span></span> <span data-ttu-id="cc525-111">El paquete, un archivo. zip, contiene el manifiesto de aplicación y los iconos que definen su experiencia de forma exclusiva.</span><span class="sxs-lookup"><span data-stu-id="cc525-111">The package, a .zip file, contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="cc525-112">Para crear un paquete de carga, consulte [Create the Package for your Microsoft Teams App](../../concepts/build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="cc525-112">To create an upload package, see [Create the package for your Microsoft Teams app](../../concepts/build-and-test/apps-package.md).</span></span>

<span data-ttu-id="cc525-113">Una vez creado el paquete, ahora puede cargarlo en un equipo.</span><span class="sxs-lookup"><span data-stu-id="cc525-113">With your package created, you can now upload it into a team.</span></span> <span data-ttu-id="cc525-114">Una vez cargada, estará disponible para todos los usuarios del equipo seleccionado y solo para los usuarios de ese equipo.</span><span class="sxs-lookup"><span data-stu-id="cc525-114">Once uploaded it will be available for all users in the selected team, and only the users of that team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="cc525-115">Cargar el paquete en Teams</span><span class="sxs-lookup"><span data-stu-id="cc525-115">Load your package into Teams</span></span>

<span data-ttu-id="cc525-116">Puede probar el paquete al cargarlo en Teams.</span><span class="sxs-lookup"><span data-stu-id="cc525-116">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="cc525-117">Para que funcione la carga, el administrador de espacios empresariales debe [Habilitar primero la carga de aplicaciones](/microsoftteams/admin-settings).</span><span class="sxs-lookup"><span data-stu-id="cc525-117">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="cc525-118">Hay dos formas de cargar la aplicación a Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="cc525-118">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="cc525-119">Uso de la tienda</span><span class="sxs-lookup"><span data-stu-id="cc525-119">Using the Store</span></span>
* <span data-ttu-id="cc525-120">Uso de la pestaña apps</span><span class="sxs-lookup"><span data-stu-id="cc525-120">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="cc525-121">Cargar el paquete en un equipo o conversación mediante la tienda</span><span class="sxs-lookup"><span data-stu-id="cc525-121">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="cc525-122">En la esquina inferior izquierda de Microsoft Teams, elija el icono de tienda.</span><span class="sxs-lookup"><span data-stu-id="cc525-122">In the lower left corner of Teams, choose the Store icon.</span></span> <span data-ttu-id="cc525-123">En la página tienda, elija **cargar una aplicación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="cc525-123">On the Store page, choose **Upload a custom app**.</span></span>

   ![Ver equipo](../../assets/images/store-upload-a-custom-app.png)

2. <span data-ttu-id="cc525-125">En el cuadro de diálogo *abrir* , navegue hasta el paquete que desea cargar y elija *abrir*.</span><span class="sxs-lookup"><span data-stu-id="cc525-125">In the *Open* dialog, navigate to the package you want to upload and choose *Open*.</span></span>

<span data-ttu-id="cc525-126">El paquete cargado ahora debería estar disponible para su uso en el equipo o la conversación especificados en el cuadro de diálogo de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="cc525-126">The uploaded package should now be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="cc525-127">Si la aplicación no aparece, la causa más común es un error en el manifiesto, especialmente identificadores para las extensiones de aplicación, Bot y mensajería.</span><span class="sxs-lookup"><span data-stu-id="cc525-127">If your app does not appear, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span> <span data-ttu-id="cc525-128">Si la aplicación no tiene el ámbito de las conversaciones, esa opción no aparecerá.</span><span class="sxs-lookup"><span data-stu-id="cc525-128">If the app is not scoped for conversations, that option will not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="cc525-129">Aplicaciones en conversaciones se encuentra actualmente en [versión preliminar para desarrolladores](../../resources/dev-preview/developer-preview-intro.md)y la opción no aparecerá si Teams no se está ejecutando en ese modo.</span><span class="sxs-lookup"><span data-stu-id="cc525-129">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option will not appear if Teams is not running in that mode.</span></span>

![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="cc525-131">Cargar el paquete en un equipo mediante la pestaña aplicaciones</span><span class="sxs-lookup"><span data-stu-id="cc525-131">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="cc525-132">En el equipo de destino, elija *más opciones* (**&#8943;**) y elija *administrar equipo*.</span><span class="sxs-lookup"><span data-stu-id="cc525-132">In the target team, choose *More options* (**&#8943;**) and choose *Manage team*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cc525-133">Debe ser el propietario del equipo o el propietario debe permitir que los usuarios agreguen los tipos de aplicación adecuados para que aparezca esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="cc525-133">You must be the team owner, or the owner must allow users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="cc525-134">Seleccione la pestaña Aplicaciones y, a continuación, elija *cargar una aplicación personalizada* en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="cc525-134">Select the Apps tab, and then choose *Upload a custom app* on the lower right.</span></span>

   ![Cargar punto de entrada](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="cc525-136">Busca y selecciona el paquete. zip del equipo.</span><span class="sxs-lookup"><span data-stu-id="cc525-136">Browse to and select your .zip package from your computer.</span></span>

4. <span data-ttu-id="cc525-137">Tras una breve pausa, verá la aplicación cargada en la lista.</span><span class="sxs-lookup"><span data-stu-id="cc525-137">After a brief pause you will see your uploaded app in the list.</span></span>

   ![Ejemplo de bot en la lista de bots cargados](../../assets/images/botinlist.jpg)

<span data-ttu-id="cc525-139">Si la aplicación no se carga, la causa más común es un error en el manifiesto, especialmente identificadores para las extensiones de aplicación, Bot y mensajería.</span><span class="sxs-lookup"><span data-stu-id="cc525-139">If your app does not load, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span>

## <a name="accessing-your-uploaded-configurable-tab"></a><span data-ttu-id="cc525-140">Acceso a la pestaña configurable cargada</span><span class="sxs-lookup"><span data-stu-id="cc525-140">Accessing your uploaded configurable tab</span></span>

<span data-ttu-id="cc525-141">Si la aplicación contiene pestañas, los usuarios pueden anclarlos a cualquier canal de conversación o equipo mediante el flujo de la galería de pestañas estándar:</span><span class="sxs-lookup"><span data-stu-id="cc525-141">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="cc525-142">Vaya a un canal del equipo.</span><span class="sxs-lookup"><span data-stu-id="cc525-142">Go to a channel in the team.</span></span> <span data-ttu-id="cc525-143">Elija *+* (*Agregar una pestaña*) a la derecha de las pestañas existentes.</span><span class="sxs-lookup"><span data-stu-id="cc525-143">Choose *+* (*Add a tab*) to the right of the existing tabs.</span></span>

2. <span data-ttu-id="cc525-144">Seleccione su pestaña en la galería que aparece.</span><span class="sxs-lookup"><span data-stu-id="cc525-144">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="cc525-145">Acepte la solicitud de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="cc525-145">Accept the consent prompt.</span></span>

4. <span data-ttu-id="cc525-146">Configure su pestaña mediante su [Página de configuración](../../tabs/how-to/create-tab-pages/configuration-page.md) y elija *Guardar*.</span><span class="sxs-lookup"><span data-stu-id="cc525-146">Configure your tab via its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and choose *Save*.</span></span>

  ![El cuadro de diálogo Agregar una pestaña, que incluye una galería de pestañas disponibles](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a><span data-ttu-id="cc525-148">Acceso a su bot cargado</span><span class="sxs-lookup"><span data-stu-id="cc525-148">Accessing your uploaded bot</span></span>

<span data-ttu-id="cc525-149">Cuando se agrega un bot a un equipo, el usuario debe usarlo en ese equipo, dentro y fuera de los canales del equipo, según la definición del ámbito de los robots.</span><span class="sxs-lookup"><span data-stu-id="cc525-149">When you add a bot to a team, it should be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="cc525-150">Usted y otros miembros del equipo verán una publicación en el canal general que indica que el bot se ha agregado al equipo.</span><span class="sxs-lookup"><span data-stu-id="cc525-150">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="cc525-151">Para un bot habilitado para Teams, puede empezar invocando el bot @mentioning el nombre del bot, que debe Autocompletar.</span><span class="sxs-lookup"><span data-stu-id="cc525-151">For a teams-enabled bot, you can start by invoking your bot by @mentioning the name of the bot, which should autocomplete.</span></span>

<span data-ttu-id="cc525-152">Para probar chats directos con el bot, puede tener acceso a él a través de la Página principal de la aplicación, @mention en un canal o buscarlo en la nueva ventana de **chat** .</span><span class="sxs-lookup"><span data-stu-id="cc525-152">To test direct chats with your bot, you can either access it via the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="cc525-153">Cuando se agrega un bot a una conversación para probar chats directos con el bot, se puede @mention en una conversación o buscar en la nueva ventana de **chat** .</span><span class="sxs-lookup"><span data-stu-id="cc525-153">When you add your bot to a conversation To test direct chats with your bot, you can @mention it in a conversation, or search for it in the **New Chat** window.</span></span>

## <a name="accessing-your-uploaded-connector"></a><span data-ttu-id="cc525-154">Obtener acceso al conector cargado</span><span class="sxs-lookup"><span data-stu-id="cc525-154">Accessing your uploaded connector</span></span>

<span data-ttu-id="cc525-155">Con la aplicación cargada en el equipo o la conversación, los usuarios pueden configurar un conector mediante el flujo de la galería de conectores estándar:</span><span class="sxs-lookup"><span data-stu-id="cc525-155">With the app loaded in the team or conversation, users can set up a Connector using the standard connectors gallery flow:</span></span>

1. <span data-ttu-id="cc525-156">Vaya a un canal del equipo.</span><span class="sxs-lookup"><span data-stu-id="cc525-156">Go to a channel in the team.</span></span> <span data-ttu-id="cc525-157">Elija *más opciones* (*&#8943;*) y elija *conectores*.</span><span class="sxs-lookup"><span data-stu-id="cc525-157">Choose *More options* (*&#8943;*) and choose *Connectors*.</span></span>

2. <span data-ttu-id="cc525-158">Seleccione el conector en la sección **subido** que se encuentra en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="cc525-158">Select your Connector from the **Uploaded** section at the bottom.</span></span>

3. <span data-ttu-id="cc525-159">Configure el conector mediante su [Página de configuración](../../webhooks-and-connectors/how-to/connectors-creating.md) y elija *Guardar*.</span><span class="sxs-lookup"><span data-stu-id="cc525-159">Configure your Connector via its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and choose *Save*.</span></span>

  ![El cuadro de diálogo Agregar una pestaña, que incluye una galería de pestañas disponibles.](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a><span data-ttu-id="cc525-161">Obtener acceso a la extensión de mensajería cargada</span><span class="sxs-lookup"><span data-stu-id="cc525-161">Accessing your uploaded messaging extension</span></span>

<span data-ttu-id="cc525-162">Una aplicación cargada con una extensión de mensajería aparece automáticamente en el menú *más opciones* (*&#8943;*) en el cuadro de redacción.</span><span class="sxs-lookup"><span data-stu-id="cc525-162">An uploaded app with a messaging extension automatically appears in the *More options* (*&#8943;*) menu in the compose box.</span></span>

![Extensiones de mensajería](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a><span data-ttu-id="cc525-164">Quitar o actualizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="cc525-164">Removing or updating your app</span></span>

<span data-ttu-id="cc525-165">Si quiere quitar la aplicación, seleccione el icono de papelera que aparece junto al nombre de la aplicación en la lista Ver bots de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="cc525-165">If you want to remove your app, select the trash-can icon next to the app name in the View Teams bots list.</span></span>

<span data-ttu-id="cc525-166">Si cambia la información del manifiesto, primero debe quitar la aplicación y, a continuación, agregar el paquete actualizado (por [cargar el paquete en un equipo](#load-your-package-into-teams)).</span><span class="sxs-lookup"><span data-stu-id="cc525-166">If you change manifest information, you must first remove the app and then add the updated package (per [Load your package into a team](#load-your-package-into-teams)).</span></span> <span data-ttu-id="cc525-167">Tenga en cuenta que, en general, los cambios de código en el servicio no requieren que vuelva a cargar el manifiesto, a menos que estos cambios requieran actualizaciones del manifiesto (como cambios en la dirección URL o el identificador de aplicación de Microsoft para su bot).</span><span class="sxs-lookup"><span data-stu-id="cc525-167">Note that, in general, code changes on your service do not require you to re-upload your manifest, unless those changes require manifest updates (such as changes to the URL or the Microsoft app ID for its bot).</span></span>

> [!NOTE]
> <span data-ttu-id="cc525-168">No hay ninguna forma de quitar por completo un bot del contexto personal.</span><span class="sxs-lookup"><span data-stu-id="cc525-168">There is no way to completely remove a bot from personal context.</span></span> <span data-ttu-id="cc525-169">Si se quita y vuelve a agregar el bot, la comunicación adicional con el bot se agregará a la conversación anterior.</span><span class="sxs-lookup"><span data-stu-id="cc525-169">If the bot is removed and re-added, additional communication with the bot will append to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="cc525-170">Notas de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="cc525-170">Troubleshooting notes</span></span>

* <span data-ttu-id="cc525-171">Si el manifiesto no se carga, compruebe que ha seguido todas las instrucciones de [Create the package](../../concepts/build-and-test/apps-package.md) y validad The manifest en el [esquema](../../resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="cc525-171">If the manifest doesn't load, please double-check that you followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>
