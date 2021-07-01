---
title: Solicitar permisos de dispositivo para la Microsoft Teams aplicación
keywords: permisos de capacidades de aplicaciones de teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 37312912b4901cd31feeb9b0ee9bc76a3e03826a
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211621"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="34052-104">Solicitar permisos de dispositivo para la Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="34052-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="34052-105">Puedes enriquecer tu aplicación Teams con funcionalidades de dispositivo nativas, como cámara, micrófono y ubicación.</span><span class="sxs-lookup"><span data-stu-id="34052-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="34052-106">Este documento le guía sobre cómo solicitar el consentimiento del usuario y obtener acceso a los permisos de dispositivo nativo.</span><span class="sxs-lookup"><span data-stu-id="34052-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="34052-107">Para integrar las funcionalidades multimedia dentro de Microsoft Teams móvil, consulta [Integrar funcionalidades multimedia.](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="34052-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="34052-108">Para integrar la funcionalidad de escáner de códigos QR o código de barras dentro de la aplicación móvil Microsoft Teams, consulta Integrar la funcionalidad del escáner de códigos DE BARRAS o [QR en Teams](qr-barcode-scanner-capability.md).</span><span class="sxs-lookup"><span data-stu-id="34052-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md).</span></span>
> * <span data-ttu-id="34052-109">Para integrar las funcionalidades de ubicación dentro Microsoft Teams aplicación móvil, consulta [Integrar capacidades de ubicación.](location-capability.md)</span><span class="sxs-lookup"><span data-stu-id="34052-109">To integrate location capabilities within your Microsoft Teams mobile app, see [Integrate location capabilities](location-capability.md).</span></span>
> * <span data-ttu-id="34052-110">Para integrar la funcionalidad selector de personas dentro de la Microsoft Teams móvil, consulta Integrar la funcionalidad selector de personas [en Teams](people-picker-capability.md).</span><span class="sxs-lookup"><span data-stu-id="34052-110">To integrate People Picker capability within your Microsoft Teams mobile app, see [Integrate People Picker capability in Teams](people-picker-capability.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="34052-111">Permisos de dispositivo nativo</span><span class="sxs-lookup"><span data-stu-id="34052-111">Native device permissions</span></span>

<span data-ttu-id="34052-112">Debes solicitar los permisos del dispositivo para tener acceso a las funcionalidades nativas del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="34052-112">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="34052-113">Los permisos del dispositivo funcionan de forma similar para todas las construcciones de aplicaciones, como pestañas, módulos de tareas o extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="34052-113">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="34052-114">El usuario debe ir a la página de permisos en Teams configuración para administrar los permisos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="34052-114">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="34052-115">Al obtener acceso a las capacidades del dispositivo, puedes crear experiencias más completas en la Teams, como:</span><span class="sxs-lookup"><span data-stu-id="34052-115">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="34052-116">Capturar y ver imágenes.</span><span class="sxs-lookup"><span data-stu-id="34052-116">Capture and view images.</span></span>
* <span data-ttu-id="34052-117">Digitalizar QR o código de barras.</span><span class="sxs-lookup"><span data-stu-id="34052-117">Scan QR or barcode.</span></span>
* <span data-ttu-id="34052-118">Grabar y compartir vídeos cortos.</span><span class="sxs-lookup"><span data-stu-id="34052-118">Record and share short videos.</span></span>
* <span data-ttu-id="34052-119">Grabe notas de audio y guárdelas para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="34052-119">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="34052-120">Use la información de ubicación del usuario para mostrar información relevante.</span><span class="sxs-lookup"><span data-stu-id="34052-120">Use the location information of the user to display relevant information.</span></span>

> [!NOTE]
> <span data-ttu-id="34052-121">Actualmente, Teams no admite permisos de dispositivo para aplicaciones de varias ventanas, pestañas y el panel lateral de la reunión.</span><span class="sxs-lookup"><span data-stu-id="34052-121">Currently, Teams does not support device permissions for multi window apps, tabs, and the meeting sidepanel.</span></span> 

## <a name="access-device-permissions"></a><span data-ttu-id="34052-122">Permisos de dispositivo de acceso</span><span class="sxs-lookup"><span data-stu-id="34052-122">Access device permissions</span></span>

<span data-ttu-id="34052-123">El SDK Microsoft Teams cliente [de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) proporciona las herramientas necesarias para que la aplicación móvil de Teams tenga acceso a los permisos de dispositivo [del](#manage-permissions) usuario y cree una experiencia más enriquecible.</span><span class="sxs-lookup"><span data-stu-id="34052-123">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="34052-124">Aunque el acceso a estas características es estándar en los exploradores web modernos, debes informar a Teams sobre las características que usas actualizando el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="34052-124">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="34052-125">Esta actualización te permite pedir permisos mientras la aplicación se ejecuta en el Teams escritorio.</span><span class="sxs-lookup"><span data-stu-id="34052-125">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="34052-126">Actualmente, Microsoft Teams compatibilidad con las capacidades multimedia y la funcionalidad del escáner de códigos de barras QR solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="34052-126">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="34052-127">Administrar permisos</span><span class="sxs-lookup"><span data-stu-id="34052-127">Manage permissions</span></span>

<span data-ttu-id="34052-128">Un usuario puede administrar los permisos de dispositivo en  Teams configuración **seleccionando Permitir** o denegar permisos a aplicaciones específicas.</span><span class="sxs-lookup"><span data-stu-id="34052-128">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="34052-129">Escritorio</span><span class="sxs-lookup"><span data-stu-id="34052-129">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="34052-130">Abre tu Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="34052-130">Open your Teams app.</span></span>
1. <span data-ttu-id="34052-131">Seleccione el icono de perfil en la esquina superior derecha de la ventana.</span><span class="sxs-lookup"><span data-stu-id="34052-131">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="34052-132">Seleccione **Configuración**  >  **permisos** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="34052-132">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="34052-133">Seleccione la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="34052-133">Select your desired settings.</span></span>

   ![Pantalla de configuración de escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="34052-135">Móvil</span><span class="sxs-lookup"><span data-stu-id="34052-135">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="34052-136">Abra Teams.</span><span class="sxs-lookup"><span data-stu-id="34052-136">Open Teams.</span></span>
1. <span data-ttu-id="34052-137">Vaya a **Configuración**  >  **App Permissions**.</span><span class="sxs-lookup"><span data-stu-id="34052-137">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="34052-138">Selecciona la aplicación para la que necesitas elegir la configuración.</span><span class="sxs-lookup"><span data-stu-id="34052-138">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="34052-139">Seleccione la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="34052-139">Select your desired settings.</span></span>

    ![Pantalla de configuración móvil de permisos de dispositivos](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="34052-141">Especificar permisos</span><span class="sxs-lookup"><span data-stu-id="34052-141">Specify permissions</span></span>

<span data-ttu-id="34052-142">Actualiza las aplicaciones agregando y especificando cuál de las cinco propiedades siguientes `manifest.json` `devicePermissions` que usas en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="34052-142">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the following five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="34052-143">Cada propiedad le permite pedir al usuario que pida su consentimiento:</span><span class="sxs-lookup"><span data-stu-id="34052-143">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="34052-144">Propiedad</span><span class="sxs-lookup"><span data-stu-id="34052-144">Property</span></span>      | <span data-ttu-id="34052-145">Descripción</span><span class="sxs-lookup"><span data-stu-id="34052-145">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="34052-146">medios</span><span class="sxs-lookup"><span data-stu-id="34052-146">media</span></span>         | <span data-ttu-id="34052-147">Permiso para usar la cámara, el micrófono, los altavoces y la galería multimedia de acceso.</span><span class="sxs-lookup"><span data-stu-id="34052-147">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="34052-148">geolocalización</span><span class="sxs-lookup"><span data-stu-id="34052-148">geolocation</span></span>   | <span data-ttu-id="34052-149">Permiso para devolver la ubicación del usuario.</span><span class="sxs-lookup"><span data-stu-id="34052-149">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="34052-150">notificaciones</span><span class="sxs-lookup"><span data-stu-id="34052-150">notifications</span></span> | <span data-ttu-id="34052-151">Permiso para enviar las notificaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="34052-151">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="34052-152">midi</span><span class="sxs-lookup"><span data-stu-id="34052-152">midi</span></span>          | <span data-ttu-id="34052-153">Permiso para enviar y recibir información de interfaz digital de instrumentos musicales (MIDI) desde un instrumento musical digital.</span><span class="sxs-lookup"><span data-stu-id="34052-153">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="34052-154">openExternal</span><span class="sxs-lookup"><span data-stu-id="34052-154">openExternal</span></span>  | <span data-ttu-id="34052-155">Permiso para abrir vínculos en aplicaciones externas.</span><span class="sxs-lookup"><span data-stu-id="34052-155">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="34052-156">Comprobar los permisos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="34052-156">Check permissions from your app</span></span>

<span data-ttu-id="34052-157">Después de agregar al manifiesto de la aplicación, comprueba los permisos mediante la API de permisos `devicePermissions` **HTML5** sin causar un mensaje:</span><span class="sxs-lookup"><span data-stu-id="34052-157">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="34052-158">Usar Teams API para obtener permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="34052-158">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="34052-159">Aproveche html5 o API Teams, para mostrar un mensaje para obtener el consentimiento para obtener acceso a los permisos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="34052-159">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="34052-160">Compatibilidad con `camera` , y está habilitada a través de `gallery` `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="34052-160">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="34052-161">Use [**la API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una única captura de imagen.</span><span class="sxs-lookup"><span data-stu-id="34052-161">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="34052-162">La compatibilidad `location` con está habilitada a través de la API [**getLocation**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="34052-162">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="34052-163">Debe usarlo para la ubicación, ya que la API de geolocalización de HTML5 actualmente no es totalmente `getLocation API` compatible con Teams cliente de escritorio.</span><span class="sxs-lookup"><span data-stu-id="34052-163">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="34052-164">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="34052-164">For example:</span></span>
 * <span data-ttu-id="34052-165">Para solicitar al usuario que acceda a su ubicación, debe llamar a `getCurrentPosition()` :</span><span class="sxs-lookup"><span data-stu-id="34052-165">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="34052-166">Para solicitar al usuario que acceda a su cámara en el escritorio o la web, debe llamar a `getUserMedia()` :</span><span class="sxs-lookup"><span data-stu-id="34052-166">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="34052-167">Para capturar la imagen en el móvil, Teams móvil pide permiso al llamar `captureImage()` a :</span><span class="sxs-lookup"><span data-stu-id="34052-167">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="34052-168">Las notificaciones le pedirán al usuario que `requestPermission()` llame:</span><span class="sxs-lookup"><span data-stu-id="34052-168">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="34052-169">Para usar la cámara o la galería de fotos de acceso, Teams móvil pide permiso al llamar a `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="34052-169">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="34052-170">Para usar el micrófono, Teams móvil pide permiso al llamar `selectMedia()` a :</span><span class="sxs-lookup"><span data-stu-id="34052-170">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="34052-171">Para solicitar al usuario que comparta la ubicación en la interfaz de mapa, Teams móvil pide permiso al llamar `getLocation()` a :</span><span class="sxs-lookup"><span data-stu-id="34052-171">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="34052-172">Escritorio</span><span class="sxs-lookup"><span data-stu-id="34052-172">Desktop</span></span>](#tab/desktop)

   ![Símbolo del sistema de permisos de dispositivo de escritorio de pestañas](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="34052-174">Móvil</span><span class="sxs-lookup"><span data-stu-id="34052-174">Mobile</span></span>](#tab/mobile)

   ![Símbolo del sistema de permisos de dispositivo móvil de pestañas](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="34052-176">Comportamiento de permisos en sesiones de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="34052-176">Permission behavior across login sessions</span></span>

<span data-ttu-id="34052-177">Los permisos de dispositivo se almacenan para cada sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="34052-177">Device permissions are stored for every login session.</span></span> <span data-ttu-id="34052-178">Esto significa que si inicias sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos del dispositivo de las sesiones anteriores no estarán disponibles.</span><span class="sxs-lookup"><span data-stu-id="34052-178">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="34052-179">Por lo tanto, debe volver a dar su consentimiento a los permisos del dispositivo para la nueva sesión.</span><span class="sxs-lookup"><span data-stu-id="34052-179">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="34052-180">También significa que, si sale de Teams o cambia de inquilino en Teams, los permisos del dispositivo se eliminan de la sesión de inicio de sesión anterior.</span><span class="sxs-lookup"><span data-stu-id="34052-180">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="34052-181">Cuando da su consentimiento a los permisos de dispositivo nativo, solo es válido para la _sesión de_ inicio de sesión actual.</span><span class="sxs-lookup"><span data-stu-id="34052-181">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34052-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34052-182">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="34052-183">Integrar funcionalidades multimedia en Teams</span><span class="sxs-lookup"><span data-stu-id="34052-183">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="34052-184">Integrar la funcionalidad de escáner de códigos QR o códigos de barras en Teams</span><span class="sxs-lookup"><span data-stu-id="34052-184">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="34052-185">Integrar las capacidades de ubicación en Teams</span><span class="sxs-lookup"><span data-stu-id="34052-185">Integrate location capabilities in Teams</span></span>](location-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="34052-186">Integrar la funcionalidad selector de personas en Teams</span><span class="sxs-lookup"><span data-stu-id="34052-186">Integrate People Picker capability in Teams</span></span>](people-picker-capability.md)
