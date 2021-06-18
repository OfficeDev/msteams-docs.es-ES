---
title: Solicitar permisos de dispositivo para la Microsoft Teams aplicación
keywords: permisos de capacidades de aplicaciones de teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 920ab47a60340fd9a14e4f5dfb2e39a8ad8f3a89
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994353"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="01693-104">Solicitar permisos de dispositivo para la Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="01693-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="01693-105">Puedes enriquecer tu aplicación Teams con funcionalidades de dispositivo nativas, como cámara, micrófono y ubicación.</span><span class="sxs-lookup"><span data-stu-id="01693-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="01693-106">Este documento le guía sobre cómo solicitar el consentimiento del usuario y obtener acceso a los permisos de dispositivo nativo.</span><span class="sxs-lookup"><span data-stu-id="01693-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="01693-107">Para integrar las funcionalidades multimedia dentro de Microsoft Teams móvil, consulta [Integrar funcionalidades multimedia.](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="01693-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="01693-108">Para integrar la funcionalidad de escáner de códigos QR o código de barras dentro de la aplicación móvil Microsoft Teams, consulta Integrar la funcionalidad del escáner de códigos DE BARRAS o [QR en Teams](qr-barcode-scanner-capability.md).</span><span class="sxs-lookup"><span data-stu-id="01693-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md).</span></span>
> * <span data-ttu-id="01693-109">Para integrar las funcionalidades de ubicación dentro Microsoft Teams aplicación móvil, consulta [Integrar capacidades de ubicación.](location-capability.md)</span><span class="sxs-lookup"><span data-stu-id="01693-109">To integrate location capabilities within your Microsoft Teams mobile app, see [Integrate location capabilities](location-capability.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="01693-110">Permisos de dispositivo nativo</span><span class="sxs-lookup"><span data-stu-id="01693-110">Native device permissions</span></span>

<span data-ttu-id="01693-111">Debes solicitar los permisos del dispositivo para tener acceso a las funcionalidades nativas del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="01693-111">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="01693-112">Los permisos del dispositivo funcionan de forma similar para todas las construcciones de aplicaciones, como pestañas, módulos de tareas o extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="01693-112">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="01693-113">El usuario debe ir a la página de permisos en Teams configuración para administrar los permisos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="01693-113">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="01693-114">Al obtener acceso a las capacidades del dispositivo, puedes crear experiencias más completas en la Teams, como:</span><span class="sxs-lookup"><span data-stu-id="01693-114">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="01693-115">Capturar y ver imágenes.</span><span class="sxs-lookup"><span data-stu-id="01693-115">Capture and view images.</span></span>
* <span data-ttu-id="01693-116">Digitalizar QR o código de barras.</span><span class="sxs-lookup"><span data-stu-id="01693-116">Scan QR or barcode.</span></span>
* <span data-ttu-id="01693-117">Grabar y compartir vídeos cortos.</span><span class="sxs-lookup"><span data-stu-id="01693-117">Record and share short videos.</span></span>
* <span data-ttu-id="01693-118">Grabe notas de audio y guárdelas para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="01693-118">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="01693-119">Use la información de ubicación del usuario para mostrar información relevante.</span><span class="sxs-lookup"><span data-stu-id="01693-119">Use the location information of the user to display relevant information.</span></span>

> [!NOTE]
> <span data-ttu-id="01693-120">Actualmente, Teams no admite permisos de dispositivo para aplicaciones de varias ventanas, pestañas y el panel lateral de la reunión.</span><span class="sxs-lookup"><span data-stu-id="01693-120">Currently, Teams does not support device permissions for multi window apps, tabs, and the meeting sidepanel.</span></span> 

## <a name="access-device-permissions"></a><span data-ttu-id="01693-121">Permisos de dispositivo de acceso</span><span class="sxs-lookup"><span data-stu-id="01693-121">Access device permissions</span></span>

<span data-ttu-id="01693-122">El SDK Microsoft Teams cliente [de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) proporciona las herramientas necesarias para que la aplicación móvil de Teams tenga acceso a los permisos de dispositivo [del](#manage-permissions) usuario y cree una experiencia más enriquecible.</span><span class="sxs-lookup"><span data-stu-id="01693-122">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="01693-123">Aunque el acceso a estas características es estándar en los exploradores web modernos, debes informar a Teams sobre las características que usas actualizando el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01693-123">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="01693-124">Esta actualización te permite pedir permisos mientras la aplicación se ejecuta en el Teams escritorio.</span><span class="sxs-lookup"><span data-stu-id="01693-124">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="01693-125">Actualmente, Microsoft Teams compatibilidad con las capacidades multimedia y la funcionalidad del escáner de códigos de barras QR solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="01693-125">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="01693-126">Administrar permisos</span><span class="sxs-lookup"><span data-stu-id="01693-126">Manage permissions</span></span>

<span data-ttu-id="01693-127">Un usuario puede administrar los permisos de dispositivo en  Teams configuración **seleccionando Permitir** o denegar permisos a aplicaciones específicas.</span><span class="sxs-lookup"><span data-stu-id="01693-127">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="01693-128">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01693-128">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="01693-129">Abre tu Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="01693-129">Open your Teams app.</span></span>
1. <span data-ttu-id="01693-130">Seleccione el icono de perfil en la esquina superior derecha de la ventana.</span><span class="sxs-lookup"><span data-stu-id="01693-130">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="01693-131">Seleccione **Configuración**  >  **permisos** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="01693-131">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="01693-132">Seleccione la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="01693-132">Select your desired settings.</span></span>

   ![Pantalla de configuración de escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="01693-134">Móvil</span><span class="sxs-lookup"><span data-stu-id="01693-134">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="01693-135">Abra Teams.</span><span class="sxs-lookup"><span data-stu-id="01693-135">Open Teams.</span></span>
1. <span data-ttu-id="01693-136">Vaya a **Configuración**  >  **App Permissions**.</span><span class="sxs-lookup"><span data-stu-id="01693-136">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="01693-137">Selecciona la aplicación para la que necesitas elegir la configuración.</span><span class="sxs-lookup"><span data-stu-id="01693-137">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="01693-138">Seleccione la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="01693-138">Select your desired settings.</span></span>

    ![Pantalla de configuración móvil de permisos de dispositivos](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="01693-140">Especificar permisos</span><span class="sxs-lookup"><span data-stu-id="01693-140">Specify permissions</span></span>

<span data-ttu-id="01693-141">Actualiza las aplicaciones agregando y especificando cuáles de las cinco propiedades `manifest.json` `devicePermissions` que usas en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="01693-141">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="01693-142">Cada propiedad le permite pedir al usuario que pida su consentimiento:</span><span class="sxs-lookup"><span data-stu-id="01693-142">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="01693-143">Propiedad</span><span class="sxs-lookup"><span data-stu-id="01693-143">Property</span></span>      | <span data-ttu-id="01693-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="01693-144">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="01693-145">medios</span><span class="sxs-lookup"><span data-stu-id="01693-145">media</span></span>         | <span data-ttu-id="01693-146">Permiso para usar la cámara, el micrófono, los altavoces y la galería multimedia de acceso.</span><span class="sxs-lookup"><span data-stu-id="01693-146">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="01693-147">geolocalización</span><span class="sxs-lookup"><span data-stu-id="01693-147">geolocation</span></span>   | <span data-ttu-id="01693-148">Permiso para devolver la ubicación del usuario.</span><span class="sxs-lookup"><span data-stu-id="01693-148">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="01693-149">notificaciones</span><span class="sxs-lookup"><span data-stu-id="01693-149">notifications</span></span> | <span data-ttu-id="01693-150">Permiso para enviar las notificaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="01693-150">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="01693-151">midi</span><span class="sxs-lookup"><span data-stu-id="01693-151">midi</span></span>          | <span data-ttu-id="01693-152">Permiso para enviar y recibir información de interfaz digital de instrumentos musicales (MIDI) desde un instrumento musical digital.</span><span class="sxs-lookup"><span data-stu-id="01693-152">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="01693-153">openExternal</span><span class="sxs-lookup"><span data-stu-id="01693-153">openExternal</span></span>  | <span data-ttu-id="01693-154">Permiso para abrir vínculos en aplicaciones externas.</span><span class="sxs-lookup"><span data-stu-id="01693-154">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="01693-155">Comprobar los permisos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="01693-155">Check permissions from your app</span></span>

<span data-ttu-id="01693-156">Después de agregar al manifiesto de la aplicación, comprueba los permisos mediante la API de permisos `devicePermissions` **HTML5** sin causar un mensaje:</span><span class="sxs-lookup"><span data-stu-id="01693-156">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="01693-157">Usar Teams API para obtener permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="01693-157">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="01693-158">Aproveche html5 o API Teams, para mostrar un mensaje para obtener el consentimiento para obtener acceso a los permisos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="01693-158">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="01693-159">Compatibilidad con `camera` , y está habilitada a través de `gallery` `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="01693-159">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="01693-160">Use [**la API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una única captura de imagen.</span><span class="sxs-lookup"><span data-stu-id="01693-160">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="01693-161">La compatibilidad `location` con está habilitada a través de la API [**getLocation**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="01693-161">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="01693-162">Debe usarlo para la ubicación, ya que la API de geolocalización de HTML5 actualmente no es totalmente `getLocation API` compatible con Teams cliente de escritorio.</span><span class="sxs-lookup"><span data-stu-id="01693-162">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="01693-163">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="01693-163">For example:</span></span>
 * <span data-ttu-id="01693-164">Para solicitar al usuario que acceda a su ubicación, debe llamar a `getCurrentPosition()` :</span><span class="sxs-lookup"><span data-stu-id="01693-164">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="01693-165">Para solicitar al usuario que acceda a su cámara en el escritorio o la web, debe llamar a `getUserMedia()` :</span><span class="sxs-lookup"><span data-stu-id="01693-165">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="01693-166">Para capturar la imagen en el móvil, Teams móvil pide permiso al llamar `captureImage()` a :</span><span class="sxs-lookup"><span data-stu-id="01693-166">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="01693-167">Las notificaciones le pedirán al usuario que `requestPermission()` llame:</span><span class="sxs-lookup"><span data-stu-id="01693-167">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="01693-168">Para usar la cámara o la galería de fotos de acceso, Teams móvil pide permiso al llamar a `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="01693-168">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="01693-169">Para usar el micrófono, Teams móvil pide permiso al llamar `selectMedia()` a :</span><span class="sxs-lookup"><span data-stu-id="01693-169">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="01693-170">Para solicitar al usuario que comparta la ubicación en la interfaz de mapa, Teams móvil pide permiso al llamar `getLocation()` a :</span><span class="sxs-lookup"><span data-stu-id="01693-170">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="01693-171">Escritorio</span><span class="sxs-lookup"><span data-stu-id="01693-171">Desktop</span></span>](#tab/desktop)

   ![Símbolo del sistema de permisos de dispositivo de escritorio de pestañas](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="01693-173">Móvil</span><span class="sxs-lookup"><span data-stu-id="01693-173">Mobile</span></span>](#tab/mobile)

   ![Símbolo del sistema de permisos de dispositivo móvil de pestañas](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="01693-175">Comportamiento de permisos en sesiones de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="01693-175">Permission behavior across login sessions</span></span>

<span data-ttu-id="01693-176">Los permisos de dispositivo se almacenan para cada sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="01693-176">Device permissions are stored for every login session.</span></span> <span data-ttu-id="01693-177">Esto significa que si inicias sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos del dispositivo de las sesiones anteriores no estarán disponibles.</span><span class="sxs-lookup"><span data-stu-id="01693-177">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="01693-178">Por lo tanto, debe volver a dar su consentimiento a los permisos del dispositivo para la nueva sesión.</span><span class="sxs-lookup"><span data-stu-id="01693-178">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="01693-179">También significa que, si sale de Teams o cambia de inquilino en Teams, los permisos del dispositivo se eliminan de la sesión de inicio de sesión anterior.</span><span class="sxs-lookup"><span data-stu-id="01693-179">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="01693-180">Cuando da su consentimiento a los permisos de dispositivo nativo, solo es válido para la _sesión de_ inicio de sesión actual.</span><span class="sxs-lookup"><span data-stu-id="01693-180">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01693-181">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="01693-181">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="01693-182">Integrar funcionalidades multimedia en Teams</span><span class="sxs-lookup"><span data-stu-id="01693-182">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="01693-183">Integrar la funcionalidad de escáner de códigos QR o códigos de barras en Teams</span><span class="sxs-lookup"><span data-stu-id="01693-183">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="01693-184">Integrar las capacidades de ubicación en Teams</span><span class="sxs-lookup"><span data-stu-id="01693-184">Integrate location capabilities in Teams</span></span>](location-capability.md)
