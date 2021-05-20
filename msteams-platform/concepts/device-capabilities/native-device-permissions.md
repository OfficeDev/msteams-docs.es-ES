---
title: Solicitar permisos de dispositivo para la aplicación Microsoft Teams
keywords: permisos de capacidades de aplicaciones de equipos
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 34f84285dc883cc474cf1720c42b1699f76c6653
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566183"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="7df4a-104">Solicitar permisos de dispositivo para la aplicación Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7df4a-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="7df4a-105">Puede enriquecer la aplicación Teams con capacidades de dispositivo nativas, como cámara, micrófono y ubicación.</span><span class="sxs-lookup"><span data-stu-id="7df4a-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="7df4a-106">Este documento le guía sobre cómo solicitar el consentimiento del usuario y acceder a los permisos del dispositivo nativo.</span><span class="sxs-lookup"><span data-stu-id="7df4a-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="7df4a-107">Para integrar las capacidades de medios dentro de la aplicación móvil Microsoft Teams, consulte [Integrar capacidades de medios.](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="7df4a-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="7df4a-108">Para integrar la capacidad del escáner QR o de código de barras dentro de su aplicación móvil Microsoft Teams, consulte [Integrar la capacidad del escáner QR o de código de barras en Teams.](qr-barcode-scanner-capability.md)</span><span class="sxs-lookup"><span data-stu-id="7df4a-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md).</span></span>
> * <span data-ttu-id="7df4a-109">Para integrar capacidades de ubicación dentro de la aplicación móvil Microsoft Teams, consulte [Integrar capacidades de ubicación.](location-capability.md)</span><span class="sxs-lookup"><span data-stu-id="7df4a-109">To integrate location capabilities within your Microsoft Teams mobile app, see [Integrate location capabilities](location-capability.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="7df4a-110">Permisos de dispositivo nativo</span><span class="sxs-lookup"><span data-stu-id="7df4a-110">Native device permissions</span></span>

<span data-ttu-id="7df4a-111">Debe solicitar los permisos del dispositivo para acceder a las capacidades de dispositivos nativos.</span><span class="sxs-lookup"><span data-stu-id="7df4a-111">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="7df4a-112">Los permisos de dispositivo funcionan de forma similar para todas las construcciones de aplicaciones, como pestañas, módulos de tareas o extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="7df4a-112">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="7df4a-113">El usuario debe ir a la página de permisos en Teams configuración para administrar los permisos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7df4a-113">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="7df4a-114">Al acceder a las capacidades del dispositivo, puede crear experiencias más enriquecidas en la plataforma Teams, como:</span><span class="sxs-lookup"><span data-stu-id="7df4a-114">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="7df4a-115">Capturar y ver imágenes.</span><span class="sxs-lookup"><span data-stu-id="7df4a-115">Capture and view images.</span></span>
* <span data-ttu-id="7df4a-116">Escanea QR o código de barras.</span><span class="sxs-lookup"><span data-stu-id="7df4a-116">Scan QR or barcode.</span></span>
* <span data-ttu-id="7df4a-117">Graba y comparte vídeos cortos.</span><span class="sxs-lookup"><span data-stu-id="7df4a-117">Record and share short videos.</span></span>
* <span data-ttu-id="7df4a-118">Graba notas de audio y guárdalas para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="7df4a-118">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="7df4a-119">Utilice la información de ubicación del usuario para mostrar la información relevante.</span><span class="sxs-lookup"><span data-stu-id="7df4a-119">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="7df4a-120">Permisos de dispositivo de acceso</span><span class="sxs-lookup"><span data-stu-id="7df4a-120">Access device permissions</span></span>

<span data-ttu-id="7df4a-121">El [SDK de cliente de JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) proporciona las herramientas necesarias para que la aplicación móvil Teams acceda a los permisos de [dispositivo](#manage-permissions) del usuario y cree una experiencia más enriquecida.</span><span class="sxs-lookup"><span data-stu-id="7df4a-121">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="7df4a-122">Aunque el acceso a estas características es estándar en los navegadores web modernos, debe informar a Teams sobre las características que usa actualizando el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7df4a-122">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="7df4a-123">Esta actualización le permite solicitar permisos mientras la aplicación se ejecuta en el cliente de escritorio Teams.</span><span class="sxs-lookup"><span data-stu-id="7df4a-123">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="7df4a-124">Actualmente, Microsoft Teams soporte para capacidades de medios y la capacidad del escáner de código de barras QR solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="7df4a-124">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="7df4a-125">Administrar permisos</span><span class="sxs-lookup"><span data-stu-id="7df4a-125">Manage permissions</span></span>

<span data-ttu-id="7df4a-126">Un usuario puede administrar permisos de dispositivo en Teams configuración seleccionando **Permitir** o **Denegar** permisos a aplicaciones específicas.</span><span class="sxs-lookup"><span data-stu-id="7df4a-126">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="7df4a-127">Escritorio</span><span class="sxs-lookup"><span data-stu-id="7df4a-127">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="7df4a-128">Abre la aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="7df4a-128">Open your Teams app.</span></span>
1. <span data-ttu-id="7df4a-129">Seleccione el icono de perfil en la esquina superior derecha de la ventana.</span><span class="sxs-lookup"><span data-stu-id="7df4a-129">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="7df4a-130">Seleccione **Configuración**  >  **Permisos** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="7df4a-130">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="7df4a-131">Seleccione la configuración deseada.</span><span class="sxs-lookup"><span data-stu-id="7df4a-131">Select your desired settings.</span></span>

   ![Pantalla de configuración de escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="7df4a-133">Móvil</span><span class="sxs-lookup"><span data-stu-id="7df4a-133">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="7df4a-134">Abra Teams.</span><span class="sxs-lookup"><span data-stu-id="7df4a-134">Open Teams.</span></span>
1. <span data-ttu-id="7df4a-135">Vaya a **Configuración**  >  **Permisos de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="7df4a-135">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="7df4a-136">Seleccione la aplicación para la que debe elegir la configuración.</span><span class="sxs-lookup"><span data-stu-id="7df4a-136">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="7df4a-137">Seleccione la configuración deseada.</span><span class="sxs-lookup"><span data-stu-id="7df4a-137">Select your desired settings.</span></span>

    ![Pantalla de configuración móvil de permisos de dispositivo](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="7df4a-139">Especificar permisos</span><span class="sxs-lookup"><span data-stu-id="7df4a-139">Specify permissions</span></span>

<span data-ttu-id="7df4a-140">Actualice la aplicación `manifest.json` agregando `devicePermissions` y especificando cuál de las cinco propiedades que usa en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="7df4a-140">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="7df4a-141">Cada propiedad le permite solicitar al usuario que pida su consentimiento:</span><span class="sxs-lookup"><span data-stu-id="7df4a-141">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="7df4a-142">Propiedad</span><span class="sxs-lookup"><span data-stu-id="7df4a-142">Property</span></span>      | <span data-ttu-id="7df4a-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="7df4a-143">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="7df4a-144">Elementos multimedia</span><span class="sxs-lookup"><span data-stu-id="7df4a-144">media</span></span>         | <span data-ttu-id="7df4a-145">Permiso para usar la cámara, el micrófono, los altavoces y la galería de medios de acceso.</span><span class="sxs-lookup"><span data-stu-id="7df4a-145">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="7df4a-146">geolocalización</span><span class="sxs-lookup"><span data-stu-id="7df4a-146">geolocation</span></span>   | <span data-ttu-id="7df4a-147">Permiso para devolver la ubicación del usuario.</span><span class="sxs-lookup"><span data-stu-id="7df4a-147">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="7df4a-148">notificaciones</span><span class="sxs-lookup"><span data-stu-id="7df4a-148">notifications</span></span> | <span data-ttu-id="7df4a-149">Permiso para enviar las notificaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="7df4a-149">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="7df4a-150">midi</span><span class="sxs-lookup"><span data-stu-id="7df4a-150">midi</span></span>          | <span data-ttu-id="7df4a-151">Permiso para enviar y recibir información de la Interfaz Digital de Instrumento Musical (MIDI) de un instrumento musical digital.</span><span class="sxs-lookup"><span data-stu-id="7df4a-151">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="7df4a-152">openExternal</span><span class="sxs-lookup"><span data-stu-id="7df4a-152">openExternal</span></span>  | <span data-ttu-id="7df4a-153">Permiso para abrir vínculos en aplicaciones externas.</span><span class="sxs-lookup"><span data-stu-id="7df4a-153">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="7df4a-154">Compruebe los permisos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="7df4a-154">Check permissions from your app</span></span>

<span data-ttu-id="7df4a-155">Después de agregar `devicePermissions` al manifiesto de la aplicación, compruebe los permisos mediante la API de permisos **HTML5** sin provocar un mensaje:</span><span class="sxs-lookup"><span data-stu-id="7df4a-155">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="7df4a-156">Use Teams API para obtener permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="7df4a-156">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="7df4a-157">Aproveche html5 o Teams API adecuados para mostrar un mensaje para obtener consentimiento para acceder a los permisos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7df4a-157">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="7df4a-158">Compatibilidad con `camera` , y está habilitado a través de `gallery` `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="7df4a-158">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="7df4a-159">Utilice [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una sola captura de imagen.</span><span class="sxs-lookup"><span data-stu-id="7df4a-159">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="7df4a-160">La compatibilidad `location` con la compatibilidad con [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)está habilitada.</span><span class="sxs-lookup"><span data-stu-id="7df4a-160">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="7df4a-161">Debe usar esto `getLocation API` para la ubicación, ya que la API de geolocalización HTML5 no es totalmente compatible con Teams cliente de escritorio.</span><span class="sxs-lookup"><span data-stu-id="7df4a-161">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="7df4a-162">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7df4a-162">For example:</span></span>
 * <span data-ttu-id="7df4a-163">Para solicitar al usuario que acceda a su ubicación, debe llamar a `getCurrentPosition()` :</span><span class="sxs-lookup"><span data-stu-id="7df4a-163">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="7df4a-164">Para pedir al usuario que acceda a su cámara en el escritorio o la web debe llamar `getUserMedia()` a:</span><span class="sxs-lookup"><span data-stu-id="7df4a-164">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="7df4a-165">Para capturar la imagen en el móvil, Teams móvil pide permiso cuando se llama `captureImage()` a:</span><span class="sxs-lookup"><span data-stu-id="7df4a-165">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="7df4a-166">Las notificaciones le preguntarán al usuario cuando `requestPermission()` llame:</span><span class="sxs-lookup"><span data-stu-id="7df4a-166">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="7df4a-167">Para utilizar la cámara o acceder a la galería de fotos, Teams móvil pide permiso cuando se `selectMedia()` llama:</span><span class="sxs-lookup"><span data-stu-id="7df4a-167">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="7df4a-168">Para utilizar el micrófono, Teams móvil pide permiso cuando se `selectMedia()` llama:</span><span class="sxs-lookup"><span data-stu-id="7df4a-168">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="7df4a-169">Para pedir al usuario que comparta la ubicación en la interfaz del mapa, Teams móvil pide permiso al `getLocation()` llamar:</span><span class="sxs-lookup"><span data-stu-id="7df4a-169">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="7df4a-170">Escritorio</span><span class="sxs-lookup"><span data-stu-id="7df4a-170">Desktop</span></span>](#tab/desktop)

   ![Solicitud de permisos de dispositivo de escritorio en pestañas](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="7df4a-172">Móvil</span><span class="sxs-lookup"><span data-stu-id="7df4a-172">Mobile</span></span>](#tab/mobile)

   ![Solicitud de permisos de dispositivos móviles en pestañas](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="7df4a-174">Comportamiento de permisos en las sesiones de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="7df4a-174">Permission behavior across login sessions</span></span>

<span data-ttu-id="7df4a-175">Los permisos de dispositivo se almacenan para cada sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="7df4a-175">Device permissions are stored for every login session.</span></span> <span data-ttu-id="7df4a-176">Esto significa que si inicia sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos de dispositivo de las sesiones anteriores no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="7df4a-176">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="7df4a-177">Por lo tanto, debe volver a dar su consentimiento a los permisos de dispositivo para la nueva sesión.</span><span class="sxs-lookup"><span data-stu-id="7df4a-177">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="7df4a-178">También significa que, si cierra sesión en Teams o cambia de inquilino en Teams, los permisos de dispositivo se eliminan de la sesión de inicio de sesión anterior.</span><span class="sxs-lookup"><span data-stu-id="7df4a-178">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="7df4a-179">Cuando acepta los permisos de dispositivo nativo, solo es válido para la sesión de inicio de sesión _actual._</span><span class="sxs-lookup"><span data-stu-id="7df4a-179">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7df4a-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7df4a-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7df4a-181">Integrar capacidades de medios en Teams</span><span class="sxs-lookup"><span data-stu-id="7df4a-181">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="7df4a-182">Integrar la capacidad del escáner QR o de código de barras en Teams</span><span class="sxs-lookup"><span data-stu-id="7df4a-182">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="7df4a-183">Integrar capacidades de ubicación en Teams</span><span class="sxs-lookup"><span data-stu-id="7df4a-183">Integrate location capabilities in Teams</span></span>](location-capability.md)
