---
title: Solicitar permisos de dispositivo para la aplicación de Microsoft Teams
keywords: permisos de capacidades de aplicaciones de teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario
ms.topic: how-to
ms.openlocfilehash: 60c28e1170e8bbdf664145bde7f7de585bd55a45
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294750"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="aa27a-104">Solicitar permisos de dispositivo para la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="aa27a-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="aa27a-105">Puedes enriquecer la aplicación de Teams con capacidades de dispositivo nativas, como cámara, micrófono y ubicación.</span><span class="sxs-lookup"><span data-stu-id="aa27a-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="aa27a-106">Este documento le guía sobre cómo solicitar el consentimiento del usuario y obtener acceso a los permisos de dispositivo nativo.</span><span class="sxs-lookup"><span data-stu-id="aa27a-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="aa27a-107">Para integrar las funcionalidades multimedia dentro de la aplicación móvil de Microsoft Teams, consulta [Integrar capacidades multimedia.](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="aa27a-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="aa27a-108">Para integrar la funcionalidad de escáner qr o de código de barras en la aplicación móvil de Microsoft Teams, consulta Integrar la funcionalidad [del escáner de códigos](qr-barcode-scanner-capability.md) de barras o QR en Teams</span><span class="sxs-lookup"><span data-stu-id="aa27a-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md)</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="aa27a-109">Permisos de dispositivo nativo</span><span class="sxs-lookup"><span data-stu-id="aa27a-109">Native device permissions</span></span>

<span data-ttu-id="aa27a-110">Debes solicitar los permisos del dispositivo para tener acceso a las funcionalidades nativas del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aa27a-110">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="aa27a-111">Los permisos del dispositivo funcionan de forma similar para todas las construcciones de aplicaciones, como pestañas, módulos de tareas o extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="aa27a-111">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="aa27a-112">El usuario debe ir a la página de permisos de la configuración de Teams para administrar los permisos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aa27a-112">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="aa27a-113">Al acceder a las capacidades del dispositivo, puedes crear experiencias más completas en la plataforma de Teams, como:</span><span class="sxs-lookup"><span data-stu-id="aa27a-113">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="aa27a-114">Capturar y ver imágenes.</span><span class="sxs-lookup"><span data-stu-id="aa27a-114">Capture and view images.</span></span>
* <span data-ttu-id="aa27a-115">Digitalizar QR o código de barras.</span><span class="sxs-lookup"><span data-stu-id="aa27a-115">Scan QR or barcode.</span></span>
* <span data-ttu-id="aa27a-116">Grabar y compartir vídeos cortos.</span><span class="sxs-lookup"><span data-stu-id="aa27a-116">Record and share short videos.</span></span>
* <span data-ttu-id="aa27a-117">Grabe notas de audio y guárdelas para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="aa27a-117">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="aa27a-118">Use la información de ubicación del usuario para mostrar información relevante.</span><span class="sxs-lookup"><span data-stu-id="aa27a-118">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="aa27a-119">Permisos de dispositivo de acceso</span><span class="sxs-lookup"><span data-stu-id="aa27a-119">Access device permissions</span></span>

<span data-ttu-id="aa27a-120">El [SDK de cliente de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams proporciona las herramientas necesarias para que la aplicación móvil de Teams tenga acceso a los permisos de dispositivo [del](#manage-permissions) usuario y genere una experiencia más enriquecible.</span><span class="sxs-lookup"><span data-stu-id="aa27a-120">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="aa27a-121">Aunque el acceso a estas características es estándar en los exploradores web modernos, debes informar a Teams sobre las características que usas actualizando el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aa27a-121">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="aa27a-122">Esta actualización te permite pedir permisos mientras la aplicación se ejecuta en el cliente de escritorio de Teams.</span><span class="sxs-lookup"><span data-stu-id="aa27a-122">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="aa27a-123">Actualmente, la compatibilidad de Microsoft Teams con las capacidades multimedia y la funcionalidad del escáner de códigos de barras QR solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="aa27a-123">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="aa27a-124">Administrar permisos</span><span class="sxs-lookup"><span data-stu-id="aa27a-124">Manage permissions</span></span>

<span data-ttu-id="aa27a-125">Un usuario puede administrar los permisos de dispositivo en la configuración de Teams seleccionando **Permitir** o **denegar** permisos a aplicaciones específicas.</span><span class="sxs-lookup"><span data-stu-id="aa27a-125">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="aa27a-126">Escritorio</span><span class="sxs-lookup"><span data-stu-id="aa27a-126">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="aa27a-127">Abre la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="aa27a-127">Open your Teams app.</span></span>
1. <span data-ttu-id="aa27a-128">Seleccione el icono de perfil en la esquina superior derecha de la ventana.</span><span class="sxs-lookup"><span data-stu-id="aa27a-128">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="aa27a-129">Seleccione **Configuración**  >  **Permisos en** el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="aa27a-129">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="aa27a-130">Seleccione la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="aa27a-130">Select your desired settings.</span></span>

   ![Pantalla de configuración de escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="aa27a-132">Móvil</span><span class="sxs-lookup"><span data-stu-id="aa27a-132">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="aa27a-133">Abra Teams.</span><span class="sxs-lookup"><span data-stu-id="aa27a-133">Open Teams.</span></span>
1. <span data-ttu-id="aa27a-134">Vaya a **Configuración**  >  **Permisos de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="aa27a-134">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="aa27a-135">Selecciona la aplicación para la que necesitas elegir la configuración.</span><span class="sxs-lookup"><span data-stu-id="aa27a-135">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="aa27a-136">Seleccione la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="aa27a-136">Select your desired settings.</span></span>

    ![Pantalla de configuración móvil de permisos de dispositivos](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="aa27a-138">Especificar permisos</span><span class="sxs-lookup"><span data-stu-id="aa27a-138">Specify permissions</span></span>

<span data-ttu-id="aa27a-139">Actualiza las aplicaciones agregando y especificando cuáles de las cinco propiedades `manifest.json` `devicePermissions` que usas en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="aa27a-139">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="aa27a-140">Cada propiedad le permite pedir al usuario que pida su consentimiento:</span><span class="sxs-lookup"><span data-stu-id="aa27a-140">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="aa27a-141">Propiedad</span><span class="sxs-lookup"><span data-stu-id="aa27a-141">Property</span></span>      | <span data-ttu-id="aa27a-142">Descripción</span><span class="sxs-lookup"><span data-stu-id="aa27a-142">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="aa27a-143">Elementos multimedia</span><span class="sxs-lookup"><span data-stu-id="aa27a-143">media</span></span>         | <span data-ttu-id="aa27a-144">Permiso para usar la cámara, el micrófono, los altavoces y la galería multimedia de acceso.</span><span class="sxs-lookup"><span data-stu-id="aa27a-144">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="aa27a-145">geolocalización</span><span class="sxs-lookup"><span data-stu-id="aa27a-145">geolocation</span></span>   | <span data-ttu-id="aa27a-146">Permiso para devolver la ubicación del usuario.</span><span class="sxs-lookup"><span data-stu-id="aa27a-146">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="aa27a-147">notificaciones</span><span class="sxs-lookup"><span data-stu-id="aa27a-147">notifications</span></span> | <span data-ttu-id="aa27a-148">Permiso para enviar las notificaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="aa27a-148">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="aa27a-149">midi</span><span class="sxs-lookup"><span data-stu-id="aa27a-149">midi</span></span>          | <span data-ttu-id="aa27a-150">Permiso para enviar y recibir información de interfaz digital de instrumentos musicales (MIDI) desde un instrumento musical digital.</span><span class="sxs-lookup"><span data-stu-id="aa27a-150">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="aa27a-151">openExternal</span><span class="sxs-lookup"><span data-stu-id="aa27a-151">openExternal</span></span>  | <span data-ttu-id="aa27a-152">Permiso para abrir vínculos en aplicaciones externas.</span><span class="sxs-lookup"><span data-stu-id="aa27a-152">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="aa27a-153">Comprobar los permisos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="aa27a-153">Check permissions from your app</span></span>

<span data-ttu-id="aa27a-154">Después de agregar al manifiesto de la aplicación, comprueba los permisos mediante la API de permisos `devicePermissions` **HTML5** sin causar un mensaje:</span><span class="sxs-lookup"><span data-stu-id="aa27a-154">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="aa27a-155">Usar las API de Teams para obtener permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="aa27a-155">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="aa27a-156">Aproveche la API de HTML5 o Teams apropiada para mostrar un mensaje para obtener el consentimiento para obtener acceso a los permisos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aa27a-156">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="aa27a-157">Compatibilidad con `camera` , y está habilitada a través de `gallery` `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="aa27a-157">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="aa27a-158">Use [**la API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) para una única captura de imagen.</span><span class="sxs-lookup"><span data-stu-id="aa27a-158">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="aa27a-159">La compatibilidad `location` con está habilitada a través de la API [**getLocation**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="aa27a-159">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="aa27a-160">Debe usarlo para la ubicación, ya que la API de `getLocation API` geolocalización de HTML5 actualmente no es totalmente compatible con el cliente de escritorio de Teams.</span><span class="sxs-lookup"><span data-stu-id="aa27a-160">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="aa27a-161">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="aa27a-161">For example:</span></span>
 * <span data-ttu-id="aa27a-162">Para solicitar al usuario que acceda a su ubicación, debe llamar a `getCurrentPosition()` :</span><span class="sxs-lookup"><span data-stu-id="aa27a-162">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="aa27a-163">Para solicitar al usuario que acceda a su cámara en el escritorio o la web, debe llamar a `getUserMedia()` :</span><span class="sxs-lookup"><span data-stu-id="aa27a-163">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="aa27a-164">Para capturar la imagen en el móvil, Teams mobile pide permiso al llamar `captureImage()` a :</span><span class="sxs-lookup"><span data-stu-id="aa27a-164">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="aa27a-165">Las notificaciones le pedirán al usuario que `requestPermission()` llame:</span><span class="sxs-lookup"><span data-stu-id="aa27a-165">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="aa27a-166">Para usar la cámara o la galería de fotos de acceso, Teams mobile pide permiso al llamar a `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="aa27a-166">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="aa27a-167">Para usar el micrófono, Teams mobile pide permiso al llamar `selectMedia()` a :</span><span class="sxs-lookup"><span data-stu-id="aa27a-167">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="aa27a-168">Para solicitar al usuario que comparta la ubicación en la interfaz de mapa, Teams mobile pide permiso al llamar a `getLocation()` :</span><span class="sxs-lookup"><span data-stu-id="aa27a-168">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="aa27a-169">Escritorio</span><span class="sxs-lookup"><span data-stu-id="aa27a-169">Desktop</span></span>](#tab/desktop)

   ![Símbolo del sistema de permisos de dispositivo de escritorio de pestañas](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="aa27a-171">Móvil</span><span class="sxs-lookup"><span data-stu-id="aa27a-171">Mobile</span></span>](#tab/mobile)

   ![Símbolo del sistema de permisos de dispositivo móvil de pestañas](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="aa27a-173">Comportamiento de permisos en sesiones de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="aa27a-173">Permission behavior across login sessions</span></span>

<span data-ttu-id="aa27a-174">Los permisos de dispositivo se almacenan para cada sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="aa27a-174">Device permissions are stored for every login session.</span></span> <span data-ttu-id="aa27a-175">Significa que si inicia sesión en otra instancia de Teams, por ejemplo, en otro equipo, los permisos de dispositivo de las sesiones anteriores no estarán disponibles.</span><span class="sxs-lookup"><span data-stu-id="aa27a-175">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="aa27a-176">Por lo tanto, debe volver a dar su consentimiento a los permisos del dispositivo para la nueva sesión.</span><span class="sxs-lookup"><span data-stu-id="aa27a-176">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="aa27a-177">También significa que, si inicias sesión en Teams o cambias de inquilinos en Teams, los permisos del dispositivo se eliminan de la sesión de inicio de sesión anterior.</span><span class="sxs-lookup"><span data-stu-id="aa27a-177">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="aa27a-178">Cuando da su consentimiento a los permisos de dispositivo nativo, solo es válido para la _sesión de_ inicio de sesión actual.</span><span class="sxs-lookup"><span data-stu-id="aa27a-178">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa27a-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aa27a-179">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa27a-180">Integrar capacidades multimedia en Teams</span><span class="sxs-lookup"><span data-stu-id="aa27a-180">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa27a-181">Integrar la funcionalidad del escáner de códigos DE BARRAS o QR en Teams</span><span class="sxs-lookup"><span data-stu-id="aa27a-181">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
