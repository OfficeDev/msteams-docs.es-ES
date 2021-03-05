---
title: Solicitar permisos de dispositivo para la aplicación de Microsoft Teams
keywords: permisos de capacidades de aplicaciones de teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario
ms.topic: how-to
ms.openlocfilehash: e7c5f7ff477bc193924cdf11700c77ae620cd1c0
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449440"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="62749-104">Solicitar permisos de dispositivo para la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="62749-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="62749-105">Puedes enriquecer la aplicación de Teams con funcionalidades de dispositivo nativas, como cámara, micrófono y ubicación.</span><span class="sxs-lookup"><span data-stu-id="62749-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="62749-106">Este documento le guía sobre cómo solicitar el consentimiento del usuario y obtener acceso a los permisos de dispositivo nativo.</span><span class="sxs-lookup"><span data-stu-id="62749-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="62749-107">Para integrar las funcionalidades multimedia dentro de la aplicación móvil de Microsoft Teams, consulta [Integrar capacidades multimedia.](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="62749-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="62749-108">Para integrar la funcionalidad de escáner qr o de código de barras en la aplicación móvil de Microsoft Teams, consulta Integrar la funcionalidad [del escáner de códigos](qr-barcode-scanner-capability.md) de barras o QR en Teams</span><span class="sxs-lookup"><span data-stu-id="62749-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md)</span></span>
> * <span data-ttu-id="62749-109">Para integrar las funcionalidades de ubicación dentro de la aplicación móvil de Microsoft Teams, consulta [Integrar capacidades de ubicación.](location-capability.md)</span><span class="sxs-lookup"><span data-stu-id="62749-109">To integrate location capabilities within your Microsoft Teams mobile app, see [Integrate location capabilities](location-capability.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="62749-110">Permisos de dispositivo nativo</span><span class="sxs-lookup"><span data-stu-id="62749-110">Native device permissions</span></span>

<span data-ttu-id="62749-111">Debes solicitar los permisos del dispositivo para tener acceso a las funcionalidades nativas del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="62749-111">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="62749-112">Los permisos del dispositivo funcionan de forma similar para todas las construcciones de aplicaciones, como pestañas, módulos de tareas o extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="62749-112">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="62749-113">El usuario debe ir a la página de permisos de la configuración de Teams para administrar los permisos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="62749-113">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="62749-114">Al acceder a las capacidades del dispositivo, puedes crear experiencias más completas en la plataforma de Teams, como:</span><span class="sxs-lookup"><span data-stu-id="62749-114">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="62749-115">Capturar y ver imágenes.</span><span class="sxs-lookup"><span data-stu-id="62749-115">Capture and view images.</span></span>
* <span data-ttu-id="62749-116">Digitalizar QR o código de barras.</span><span class="sxs-lookup"><span data-stu-id="62749-116">Scan QR or barcode.</span></span>
* <span data-ttu-id="62749-117">Grabar y compartir vídeos cortos.</span><span class="sxs-lookup"><span data-stu-id="62749-117">Record and share short videos.</span></span>
* <span data-ttu-id="62749-118">Grabe notas de audio y guárdelas para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="62749-118">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="62749-119">Use la información de ubicación del usuario para mostrar información relevante.</span><span class="sxs-lookup"><span data-stu-id="62749-119">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="62749-120">Permisos de dispositivo de acceso</span><span class="sxs-lookup"><span data-stu-id="62749-120">Access device permissions</span></span>

<span data-ttu-id="62749-121">El [SDK de cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams proporciona las herramientas necesarias para que la aplicación móvil de Teams tenga acceso a los permisos de dispositivo [del](#manage-permissions) usuario y genere una experiencia más enriquecible.</span><span class="sxs-lookup"><span data-stu-id="62749-121">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="62749-122">Aunque el acceso a estas características es estándar en los exploradores web modernos, debes informar a Teams sobre las características que usas actualizando el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62749-122">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="62749-123">Esta actualización te permite pedir permisos mientras la aplicación se ejecuta en el cliente de escritorio de Teams.</span><span class="sxs-lookup"><span data-stu-id="62749-123">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="62749-124">Actualmente, la compatibilidad de Microsoft Teams con las capacidades multimedia y la funcionalidad del escáner de códigos de barras QR solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="62749-124">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="62749-125">Administrar permisos</span><span class="sxs-lookup"><span data-stu-id="62749-125">Manage permissions</span></span>

<span data-ttu-id="62749-126">Un usuario puede administrar los permisos de dispositivo en la configuración de Teams seleccionando **Permitir** o **denegar** permisos a aplicaciones específicas.</span><span class="sxs-lookup"><span data-stu-id="62749-126">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="62749-127">Escritorio</span><span class="sxs-lookup"><span data-stu-id="62749-127">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="62749-128">Abre la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="62749-128">Open your Teams app.</span></span>
1. <span data-ttu-id="62749-129">Seleccione el icono de perfil en la esquina superior derecha de la ventana.</span><span class="sxs-lookup"><span data-stu-id="62749-129">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="62749-130">Seleccione **Configuración**  >  **Permisos en** el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="62749-130">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="62749-131">Seleccione la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="62749-131">Select your desired settings.</span></span>

   ![Pantalla de configuración de escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="62749-133">Móvil</span><span class="sxs-lookup"><span data-stu-id="62749-133">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="62749-134">Abra Teams.</span><span class="sxs-lookup"><span data-stu-id="62749-134">Open Teams.</span></span>
1. <span data-ttu-id="62749-135">Vaya a **Configuración**  >  **Permisos de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="62749-135">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="62749-136">Selecciona la aplicación para la que necesitas elegir la configuración.</span><span class="sxs-lookup"><span data-stu-id="62749-136">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="62749-137">Seleccione la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="62749-137">Select your desired settings.</span></span>

    ![Pantalla de configuración móvil de permisos de dispositivos](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="62749-139">Especificar permisos</span><span class="sxs-lookup"><span data-stu-id="62749-139">Specify permissions</span></span>

<span data-ttu-id="62749-140">Actualiza las aplicaciones agregando y especificando cuáles de las cinco propiedades `manifest.json` `devicePermissions` que usas en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="62749-140">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="62749-141">Cada propiedad le permite pedir al usuario que pida su consentimiento:</span><span class="sxs-lookup"><span data-stu-id="62749-141">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="62749-142">Propiedad</span><span class="sxs-lookup"><span data-stu-id="62749-142">Property</span></span>      | <span data-ttu-id="62749-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="62749-143">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="62749-144">Elementos multimedia</span><span class="sxs-lookup"><span data-stu-id="62749-144">media</span></span>         | <span data-ttu-id="62749-145">Permiso para usar la cámara, el micrófono, los altavoces y la galería multimedia de acceso.</span><span class="sxs-lookup"><span data-stu-id="62749-145">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="62749-146">geolocalización</span><span class="sxs-lookup"><span data-stu-id="62749-146">geolocation</span></span>   | <span data-ttu-id="62749-147">Permiso para devolver la ubicación del usuario.</span><span class="sxs-lookup"><span data-stu-id="62749-147">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="62749-148">notificaciones</span><span class="sxs-lookup"><span data-stu-id="62749-148">notifications</span></span> | <span data-ttu-id="62749-149">Permiso para enviar las notificaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="62749-149">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="62749-150">midi</span><span class="sxs-lookup"><span data-stu-id="62749-150">midi</span></span>          | <span data-ttu-id="62749-151">Permiso para enviar y recibir información de interfaz digital de instrumentos musicales (MIDI) desde un instrumento musical digital.</span><span class="sxs-lookup"><span data-stu-id="62749-151">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="62749-152">openExternal</span><span class="sxs-lookup"><span data-stu-id="62749-152">openExternal</span></span>  | <span data-ttu-id="62749-153">Permiso para abrir vínculos en aplicaciones externas.</span><span class="sxs-lookup"><span data-stu-id="62749-153">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="62749-154">Comprobar los permisos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="62749-154">Check permissions from your app</span></span>

<span data-ttu-id="62749-155">Después de agregar al manifiesto de la aplicación, comprueba los permisos mediante la API de permisos `devicePermissions` **HTML5** sin causar un mensaje:</span><span class="sxs-lookup"><span data-stu-id="62749-155">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="62749-156">Usar las API de Teams para obtener permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="62749-156">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="62749-157">Aproveche la API de HTML5 o Teams apropiada para mostrar un mensaje para obtener el consentimiento para obtener acceso a los permisos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="62749-157">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="62749-158">Compatibilidad con `camera` , y está habilitada a través de `gallery` `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="62749-158">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="62749-159">Use [**la API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una única captura de imagen.</span><span class="sxs-lookup"><span data-stu-id="62749-159">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="62749-160">La compatibilidad `location` con está habilitada a través de la API [**getLocation**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="62749-160">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="62749-161">Debe usarlo para la ubicación, ya que la API de `getLocation API` geolocalización de HTML5 actualmente no es totalmente compatible con el cliente de escritorio de Teams.</span><span class="sxs-lookup"><span data-stu-id="62749-161">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="62749-162">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="62749-162">For example:</span></span>
 * <span data-ttu-id="62749-163">Para solicitar al usuario que acceda a su ubicación, debe llamar a `getCurrentPosition()` :</span><span class="sxs-lookup"><span data-stu-id="62749-163">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="62749-164">Para solicitar al usuario que acceda a su cámara en el escritorio o la web, debe llamar a `getUserMedia()` :</span><span class="sxs-lookup"><span data-stu-id="62749-164">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="62749-165">Para capturar la imagen en el móvil, Teams mobile pide permiso al llamar `captureImage()` a :</span><span class="sxs-lookup"><span data-stu-id="62749-165">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="62749-166">Las notificaciones le pedirán al usuario que `requestPermission()` llame:</span><span class="sxs-lookup"><span data-stu-id="62749-166">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="62749-167">Para usar la cámara o la galería de fotos de acceso, Teams mobile pide permiso al llamar a `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="62749-167">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="62749-168">Para usar el micrófono, Teams mobile pide permiso al llamar `selectMedia()` a :</span><span class="sxs-lookup"><span data-stu-id="62749-168">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="62749-169">Para solicitar al usuario que comparta la ubicación en la interfaz de mapa, Teams mobile pide permiso al llamar a `getLocation()` :</span><span class="sxs-lookup"><span data-stu-id="62749-169">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="62749-170">Escritorio</span><span class="sxs-lookup"><span data-stu-id="62749-170">Desktop</span></span>](#tab/desktop)

   ![Símbolo del sistema de permisos de dispositivo de escritorio de pestañas](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="62749-172">Móvil</span><span class="sxs-lookup"><span data-stu-id="62749-172">Mobile</span></span>](#tab/mobile)

   ![Símbolo del sistema de permisos de dispositivo móvil de pestañas](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="62749-174">Comportamiento de permisos en sesiones de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="62749-174">Permission behavior across login sessions</span></span>

<span data-ttu-id="62749-175">Los permisos de dispositivo se almacenan para cada sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="62749-175">Device permissions are stored for every login session.</span></span> <span data-ttu-id="62749-176">Significa que si inicia sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos de dispositivo de las sesiones anteriores no estarán disponibles.</span><span class="sxs-lookup"><span data-stu-id="62749-176">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="62749-177">Por lo tanto, debe volver a dar su consentimiento a los permisos del dispositivo para la nueva sesión.</span><span class="sxs-lookup"><span data-stu-id="62749-177">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="62749-178">También significa que, si inicias sesión en Teams o cambias de inquilinos en Teams, los permisos del dispositivo se eliminan de la sesión de inicio de sesión anterior.</span><span class="sxs-lookup"><span data-stu-id="62749-178">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="62749-179">Cuando da su consentimiento a los permisos de dispositivo nativo, solo es válido para la _sesión de_ inicio de sesión actual.</span><span class="sxs-lookup"><span data-stu-id="62749-179">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62749-180">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="62749-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="62749-181">Integrar capacidades multimedia en Teams</span><span class="sxs-lookup"><span data-stu-id="62749-181">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="62749-182">Integrar la funcionalidad del escáner de códigos DE BARRAS o QR en Teams</span><span class="sxs-lookup"><span data-stu-id="62749-182">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="62749-183">Integrar capacidades de ubicación en Teams</span><span class="sxs-lookup"><span data-stu-id="62749-183">Integrate location capabilities in Teams</span></span>](location-capability.md)
