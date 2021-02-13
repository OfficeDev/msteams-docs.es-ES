---
title: Solicitar permisos de dispositivo para la aplicación de Microsoft Teams
keywords: Permisos de capacidades de aplicaciones de teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario
ms.topic: how-to
ms.openlocfilehash: 0343754eacbb6088a3e44fa5df8ec90e3b10b076
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231613"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="f5cdb-104">Solicitar permisos de dispositivo para la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f5cdb-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="f5cdb-105">Puede enriquecer su aplicación de Teams con funcionalidades de dispositivo nativo, como cámara, micrófono y ubicación.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="f5cdb-106">Este documento le guiará sobre cómo solicitar el consentimiento del usuario y obtener acceso a los permisos de dispositivo nativo.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="f5cdb-107">Para integrar las capacidades multimedia dentro de la aplicación móvil de Microsoft Teams, vea [Integrar capacidades multimedia.](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="f5cdb-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="f5cdb-108">Permisos de dispositivo nativo</span><span class="sxs-lookup"><span data-stu-id="f5cdb-108">Native device permissions</span></span>

<span data-ttu-id="f5cdb-109">Debes solicitar los permisos del dispositivo para acceder a las funcionalidades de dispositivo nativo.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-109">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="f5cdb-110">Los permisos de dispositivo funcionan de forma similar para todas las construcciones de aplicaciones, como pestañas, módulos de tareas o extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-110">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="f5cdb-111">El usuario debe ir a la página de permisos en la configuración de Teams para administrar los permisos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-111">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="f5cdb-112">Al acceder a las capacidades del dispositivo, puede crear experiencias más completas en la plataforma de Teams, como:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-112">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="f5cdb-113">Capturar y ver imágenes.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-113">Capture and view images.</span></span>
* <span data-ttu-id="f5cdb-114">Grabar y compartir vídeos cortos.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-114">Record and share short videos.</span></span>
* <span data-ttu-id="f5cdb-115">Grabe los memos de audio y guárdelos para usarlos más adelante.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-115">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="f5cdb-116">Use la información de ubicación del usuario para mostrar información relevante.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-116">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="f5cdb-117">Permisos de dispositivo de acceso</span><span class="sxs-lookup"><span data-stu-id="f5cdb-117">Access device permissions</span></span>

<span data-ttu-id="f5cdb-118">El SDK del cliente [de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams proporciona las herramientas necesarias para que la aplicación móvil de Teams tenga acceso a los permisos de dispositivo [del](#manage-permissions) usuario y cree una experiencia más completa.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-118">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="f5cdb-119">Aunque el acceso a estas características es estándar en exploradores web modernos, debe informar a Teams sobre las características que usa actualizando el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-119">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="f5cdb-120">Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en el cliente de escritorio de Teams.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-120">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="f5cdb-121">Actualmente, la compatibilidad de Microsoft Teams con las funcionalidades multimedia solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-121">Currently, Microsoft Teams support for media capabilities is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="f5cdb-122">Administrar permisos</span><span class="sxs-lookup"><span data-stu-id="f5cdb-122">Manage permissions</span></span>

<span data-ttu-id="f5cdb-123">Un usuario puede administrar los permisos de dispositivo en la configuración de Teams **seleccionando Permitir** o denegar **permisos** a aplicaciones específicas.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-123">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="f5cdb-124">Escritorio</span><span class="sxs-lookup"><span data-stu-id="f5cdb-124">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="f5cdb-125">Abra su aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-125">Open your Teams app.</span></span>
1. <span data-ttu-id="f5cdb-126">Seleccione el icono de perfil en la esquina superior derecha de la ventana.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-126">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="f5cdb-127">Seleccione **Permisos**  >  **de configuración** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-127">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="f5cdb-128">Selecciona la configuración que quieras.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-128">Select your desired settings.</span></span>

   ![Pantalla de configuración de escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="f5cdb-130">Móvil</span><span class="sxs-lookup"><span data-stu-id="f5cdb-130">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="f5cdb-131">Abra Teams.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-131">Open Teams.</span></span>
1. <span data-ttu-id="f5cdb-132">Vaya a **Configuración de** permisos  >  **de aplicación.**</span><span class="sxs-lookup"><span data-stu-id="f5cdb-132">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="f5cdb-133">Selecciona la aplicación para la que necesitas elegir la configuración.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-133">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="f5cdb-134">Selecciona la configuración que quieras.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-134">Select your desired settings.</span></span>

    ![Pantalla de configuración móvil de permisos de dispositivo](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="f5cdb-136">Especificar permisos</span><span class="sxs-lookup"><span data-stu-id="f5cdb-136">Specify permissions</span></span>

<span data-ttu-id="f5cdb-137">Actualiza las aplicaciones `manifest.json` agregando y especificando cuál de las cinco propiedades que `devicePermissions` usas en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-137">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="f5cdb-138">Cada propiedad le permite pedir al usuario que solicite su consentimiento:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-138">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="f5cdb-139">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f5cdb-139">Property</span></span>      | <span data-ttu-id="f5cdb-140">Descripción</span><span class="sxs-lookup"><span data-stu-id="f5cdb-140">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="f5cdb-141">medios</span><span class="sxs-lookup"><span data-stu-id="f5cdb-141">media</span></span>         | <span data-ttu-id="f5cdb-142">Permiso para usar la cámara, el micrófono, los altavoces y el acceso a la galería multimedia.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-142">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="f5cdb-143">geolocalización</span><span class="sxs-lookup"><span data-stu-id="f5cdb-143">geolocation</span></span>   | <span data-ttu-id="f5cdb-144">Permiso para devolver la ubicación del usuario.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-144">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="f5cdb-145">notifications</span><span class="sxs-lookup"><span data-stu-id="f5cdb-145">notifications</span></span> | <span data-ttu-id="f5cdb-146">Permiso para enviar notificaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-146">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="f5cdb-147">midi</span><span class="sxs-lookup"><span data-stu-id="f5cdb-147">midi</span></span>          | <span data-ttu-id="f5cdb-148">Permiso para enviar y recibir información de interfaz digital de instrumentos música (MIDI) de un instrumento música digital.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-148">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="f5cdb-149">openExternal</span><span class="sxs-lookup"><span data-stu-id="f5cdb-149">openExternal</span></span>  | <span data-ttu-id="f5cdb-150">Permiso para abrir vínculos en aplicaciones externas.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-150">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="f5cdb-151">Comprobar los permisos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f5cdb-151">Check permissions from your app</span></span>

<span data-ttu-id="f5cdb-152">Después de agregar al manifiesto de la aplicación, compruebe los permisos mediante la API de permisos `devicePermissions` **de HTML5** sin causar un mensaje:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-152">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

``` Javascript
// Different query options:
navigator.permissions.query({ name: 'camera' });
navigator.permissions.query({ name: 'microphone' });
navigator.permissions.query({ name: 'geolocation' });
navigator.permissions.query({ name: 'notifications' });
navigator.permissions.query({ name: 'midi', sysex: true });

// Example:
navigator.permissions.query({name:'geolocation'}).then(function(result) {
  if (result.state == 'granted') {
    // Access granted
  } else if (result.state == 'prompt') {
    // Access has not been granted
  }
});
```

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="f5cdb-153">Usar las API de Teams para obtener permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="f5cdb-153">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="f5cdb-154">Aproveche la API de HTML5 o Teams adecuada para mostrar un mensaje para obtener el consentimiento para obtener acceso a los permisos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-154">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="f5cdb-155">Compatibilidad con `camera` , y se habilita a través de la API `gallery` `microphone` [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f5cdb-155">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="f5cdb-156">Usa [**la API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una captura de imagen única.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-156">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="f5cdb-157">La compatibilidad con `location` se habilita a través de la API [**getLocation**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f5cdb-157">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="f5cdb-158">Debe usarlo para la ubicación, ya que la API de geolocalización de HTML5 actualmente no es totalmente compatible con el cliente `getLocation API` de escritorio de Teams.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-158">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="f5cdb-159">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-159">For example:</span></span>
 * <span data-ttu-id="f5cdb-160">Para solicitar al usuario que acceda a su ubicación, debe llamar `getCurrentPosition()` a:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-160">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="f5cdb-161">Para solicitar al usuario que acceda a su cámara en el escritorio o en la web, debes llamar `getUserMedia()` a:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-161">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="f5cdb-162">Para capturar la imagen en dispositivos móviles, Teams Mobile pide permiso al `captureImage()` llamar:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-162">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="f5cdb-163">Las notificaciones preguntarán al usuario cuando `requestPermission()` llame:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-163">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="f5cdb-164">Para usar la cámara o acceder a la galería de fotos, teams móvil pide permiso al `selectMedia()` llamar:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-164">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="f5cdb-165">Para usar el micrófono, el móvil de Teams pide permiso al `selectMedia()` llamar:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-165">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="f5cdb-166">Para solicitar al usuario que comparta la ubicación en la interfaz de mapa, Teams Mobile pide permiso al `getLocation()` llamar:</span><span class="sxs-lookup"><span data-stu-id="f5cdb-166">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="f5cdb-167">Escritorio</span><span class="sxs-lookup"><span data-stu-id="f5cdb-167">Desktop</span></span>](#tab/desktop)

   ![Mensaje de permisos de dispositivo de escritorio de pestañas](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="f5cdb-169">Móvil</span><span class="sxs-lookup"><span data-stu-id="f5cdb-169">Mobile</span></span>](#tab/mobile)

   ![Mensaje de permisos de dispositivo móvil de pestañas](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="f5cdb-171">Comportamiento de permisos en sesiones de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="f5cdb-171">Permission behavior across login sessions</span></span>

<span data-ttu-id="f5cdb-172">Los permisos de dispositivo se almacenan para cada sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-172">Device permissions are stored for every login session.</span></span> <span data-ttu-id="f5cdb-173">Esto significa que si inicia sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos de dispositivo de las sesiones anteriores no estarán disponibles.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-173">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="f5cdb-174">Por lo tanto, debe volver a dar su consentimiento a los permisos del dispositivo para la nueva sesión.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-174">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="f5cdb-175">También significa que, si sale de Teams o cambia de inquilino en Teams, los permisos de su dispositivo se eliminan de la sesión de inicio de sesión anterior.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-175">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="f5cdb-176">Cuando da su consentimiento a los permisos de dispositivo nativo, solo es válido para la sesión de inicio _de sesión_ actual.</span><span class="sxs-lookup"><span data-stu-id="f5cdb-176">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-step"></a><span data-ttu-id="f5cdb-177">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="f5cdb-177">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f5cdb-178">Integrar capacidades multimedia en Teams</span><span class="sxs-lookup"><span data-stu-id="f5cdb-178">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
