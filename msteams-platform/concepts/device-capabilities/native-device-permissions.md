---
title: Solicitar permisos de dispositivo para la pestaña de Microsoft Teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que suelen requerir el consentimiento del usuario
keywords: desarrollo de pestañas de Microsoft Teams
ms.openlocfilehash: 6be183d2610616f3bd3bdf32554976322193c132
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731982"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="982b6-104">Solicitar permisos de dispositivo para la pestaña de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="982b6-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="982b6-105">Es posible que quiera enriquecer su pestaña con características que requieran acceso a la funcionalidad de dispositivos nativos como:</span><span class="sxs-lookup"><span data-stu-id="982b6-105">You might want to enrich your tab with features that require access to native device functionality like:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="982b6-106">Digital</span><span class="sxs-lookup"><span data-stu-id="982b6-106">Camera</span></span>
> * <span data-ttu-id="982b6-107">Micro</span><span class="sxs-lookup"><span data-stu-id="982b6-107">Microphone</span></span>
> * <span data-ttu-id="982b6-108">Ubicación</span><span class="sxs-lookup"><span data-stu-id="982b6-108">Location</span></span>
> * <span data-ttu-id="982b6-109">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="982b6-109">Notifications</span></span>

[!Note] <span data-ttu-id="982b6-110">Para integrar las capacidades de cámara y de imagen en la aplicación móvil de Microsoft Teams, consulte [capacidades de cámara y de imagen en Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="982b6-110">To integrate camera and image capabilities within your Microsoft Teams mobile app, refer [Camera and image capabilities in Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="982b6-111">Actualmente, el cliente móvil de Microsoft Teams solo admite el acceso a `camera` , `gallery` , `mic` y `location` a través de las funciones de dispositivos nativos, y está disponible en todas las construcciones de aplicaciones, incluidas las pestañas.</span><span class="sxs-lookup"><span data-stu-id="982b6-111">At present, Teams mobile client only supports access to `camera`, `gallery`, `mic`, and `location` through native device capabilities and is available on all app constructs including tabs.</span></span> </br>
> * <span data-ttu-id="982b6-112">Compatibilidad con `camera` , `gallery` y `mic` se habilita a través de la [**API de selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="982b6-112">Support for `camera`, `gallery`, and `mic` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="982b6-113">Para la captura de imagen única, puede usar la [**API de captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="982b6-113">For single image capture you may use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).</span></span>
> * <span data-ttu-id="982b6-114">La compatibilidad con `location` se habilita a través de la [**API de getLocation**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="982b6-114">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="982b6-115">Se recomienda usar esta API ya que actualmente la [**API de geolocalización**](../../resources/schema/manifest-schema.md#devicepermissions) no es totalmente compatible con todos los clientes de escritorio.</span><span class="sxs-lookup"><span data-stu-id="982b6-115">It's recommended you use this API as [**geolocation API**](../../resources/schema/manifest-schema.md#devicepermissions) is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="982b6-116">Permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="982b6-116">Device permissions</span></span>

<span data-ttu-id="982b6-117">El acceso a los permisos de dispositivo de un usuario le permite crear experiencias mucho más enriquecidas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="982b6-117">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="982b6-118">Grabar y compartir vídeos breves</span><span class="sxs-lookup"><span data-stu-id="982b6-118">Record and share short videos</span></span>
* <span data-ttu-id="982b6-119">Grabe memorandos de audio cortos y guárdelos para más tarde</span><span class="sxs-lookup"><span data-stu-id="982b6-119">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="982b6-120">Usar la información de ubicación del usuario para mostrar información relevante</span><span class="sxs-lookup"><span data-stu-id="982b6-120">Use user location information to display relevant information</span></span>

<span data-ttu-id="982b6-121">Aunque el acceso a estas características es estándar en la mayoría de los exploradores Web modernos, es necesario que los equipos sepan qué características le gustaría usar al actualizar el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="982b6-121">While access to these features is standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="982b6-122">Esto le permitirá solicitar permisos, de la misma manera que lo haría en un explorador, mientras la aplicación se ejecuta en el cliente de escritorio de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="982b6-122">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="982b6-123">Administrar permisos</span><span class="sxs-lookup"><span data-stu-id="982b6-123">Manage permissions</span></span>

# <a name="desktop"></a>[<span data-ttu-id="982b6-124">Escritorio</span><span class="sxs-lookup"><span data-stu-id="982b6-124">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="982b6-125">Abra Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="982b6-125">Open Teams.</span></span>
1. <span data-ttu-id="982b6-126">En la esquina superior derecha de la ventana, seleccione el icono de su perfil.</span><span class="sxs-lookup"><span data-stu-id="982b6-126">In the upper right corner of the window, select your profile icon.</span></span>
1. <span data-ttu-id="982b6-127">Seleccione **Settings**  ->  **Permissions** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="982b6-127">Select **Settings** -> **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="982b6-128">Elija la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="982b6-128">Choose your desired settings.</span></span>

![Pantalla Configuración del escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="982b6-130">Móvil</span><span class="sxs-lookup"><span data-stu-id="982b6-130">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="982b6-131">Abra Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="982b6-131">Open Teams.</span></span>
1. <span data-ttu-id="982b6-132">Vaya a **configuración**  ->  **permisos** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="982b6-132">Go to **Settings** -> **App Permissions**.</span></span>
1. <span data-ttu-id="982b6-133">Seleccione la aplicación para la que quiera elegir la configuración.</span><span class="sxs-lookup"><span data-stu-id="982b6-133">Select the app you need to choose settings for.</span></span>
1. <span data-ttu-id="982b6-134">Elija la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="982b6-134">Choose your desired settings.</span></span>

![Pantalla de configuración móvil de permisos de dispositivo](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="properties"></a><span data-ttu-id="982b6-136">Propiedades</span><span class="sxs-lookup"><span data-stu-id="982b6-136">Properties</span></span>

<span data-ttu-id="982b6-137">Actualice la aplicación `manifest.json` agregando `devicePermissions` y especificando cuál de las cinco propiedades desea usar en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="982b6-137">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```
> [!Note]
>
> <span data-ttu-id="982b6-138">Los medios también se usan para los permisos de cámara en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="982b6-138">Media is also used for camera permissions on mobile.</span></span>

<span data-ttu-id="982b6-139">Cada propiedad le permitirá solicitar al usuario que solicite su consentimiento:</span><span class="sxs-lookup"><span data-stu-id="982b6-139">Each property will allow you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="982b6-140">Propiedad</span><span class="sxs-lookup"><span data-stu-id="982b6-140">Property</span></span>      | <span data-ttu-id="982b6-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="982b6-141">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="982b6-142">medios</span><span class="sxs-lookup"><span data-stu-id="982b6-142">media</span></span>         | <span data-ttu-id="982b6-143">permiso para usar la cámara, el micrófono, los altavoces y la galería de medios de Access</span><span class="sxs-lookup"><span data-stu-id="982b6-143">permission to use the camera, microphone, speakers, and access media gallery</span></span> |
| <span data-ttu-id="982b6-144">geolocalización</span><span class="sxs-lookup"><span data-stu-id="982b6-144">geolocation</span></span>   | <span data-ttu-id="982b6-145">permiso para devolver la ubicación del usuario</span><span class="sxs-lookup"><span data-stu-id="982b6-145">permission to return the user's location</span></span>      |
| <span data-ttu-id="982b6-146">notificaciones</span><span class="sxs-lookup"><span data-stu-id="982b6-146">notifications</span></span> | <span data-ttu-id="982b6-147">permiso para enviar notificaciones de usuario</span><span class="sxs-lookup"><span data-stu-id="982b6-147">permission to send the user notifications</span></span>      |
| <span data-ttu-id="982b6-148">MIDI</span><span class="sxs-lookup"><span data-stu-id="982b6-148">midi</span></span>          | <span data-ttu-id="982b6-149">permiso para enviar y recibir información MIDI de un instrumento musical digital</span><span class="sxs-lookup"><span data-stu-id="982b6-149">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="982b6-150">openExternal</span><span class="sxs-lookup"><span data-stu-id="982b6-150">openExternal</span></span>  | <span data-ttu-id="982b6-151">permiso para abrir vínculos en aplicaciones externas</span><span class="sxs-lookup"><span data-stu-id="982b6-151">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="982b6-152">Comprobación de permisos en la pestaña</span><span class="sxs-lookup"><span data-stu-id="982b6-152">Checking permissions from your tab</span></span>

<span data-ttu-id="982b6-153">Una vez que haya agregado `devicePermissions` al manifiesto de la aplicación, puede comprobar los permisos mediante la API de "permisos" de HTML5 sin que se le pida confirmación.</span><span class="sxs-lookup"><span data-stu-id="982b6-153">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="982b6-154">Preguntar al usuario</span><span class="sxs-lookup"><span data-stu-id="982b6-154">Prompting the user</span></span>

<span data-ttu-id="982b6-155">Para mostrar una solicitud para obtener consentimiento para obtener acceso a los permisos del dispositivo, debe aprovechar la API de HTML5 o Teams adecuada.</span><span class="sxs-lookup"><span data-stu-id="982b6-155">To show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 or Teams API.</span></span> 

<span data-ttu-id="982b6-156">Por ejemplo, para solicitar al usuario que tenga acceso a su ubicación, debe llamar a `getCurrentPosition` :</span><span class="sxs-lookup"><span data-stu-id="982b6-156">For example, to prompt the user to access their location you need to call `getCurrentPosition`:</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="982b6-157">Para usar la cámara en el escritorio o en la web, Microsoft Teams mostrará una solicitud de permiso cuando llame a `getUserMedia` :</span><span class="sxs-lookup"><span data-stu-id="982b6-157">To use the camera on desktop or web, Teams will show a permission prompt when you call `getUserMedia`:</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="982b6-158">Para capturar la imagen en dispositivos móviles, Teams Mobile le pedirá permiso cuando llame a `captureImage()` :</span><span class="sxs-lookup"><span data-stu-id="982b6-158">To capture the image on mobile, Teams mobile will ask for permission when you call `captureImage()`:</span></span>

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

<span data-ttu-id="982b6-159">Las notificaciones le preguntarán al usuario cuando llame a `requestPermission` :</span><span class="sxs-lookup"><span data-stu-id="982b6-159">Notifications will prompt the user when you call `requestPermission`:</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

<span data-ttu-id="982b6-160">Para usar la cámara o la galería de fotografías de Access, Teams Mobile le pedirá permiso cuando llame a `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="982b6-160">To use camera or access photo gallery, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="982b6-161">Para usar MIC, Teams Mobile le pedirá permiso cuando llame a `selectMedia()` :</span><span class="sxs-lookup"><span data-stu-id="982b6-161">To use mic, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="982b6-162">Para solicitar al usuario que comparta la ubicación en la interfaz del mapa, Team Mobile le pedirá permiso cuando llame a `getLocation()` :</span><span class="sxs-lookup"><span data-stu-id="982b6-162">To prompt user to share location on map interface, Teams mobile will ask permission when you call `getLocation()`:</span></span>

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[<span data-ttu-id="982b6-163">Escritorio</span><span class="sxs-lookup"><span data-stu-id="982b6-163">Desktop</span></span>](#tab/desktop)

![Mensaje de pestañas de permisos de dispositivo de escritorio](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="982b6-165">Móvil</span><span class="sxs-lookup"><span data-stu-id="982b6-165">Mobile</span></span>](#tab/mobile)

![Mensaje de pestañas de permisos de dispositivo móvil](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="982b6-167">Comportamiento de permisos en sesiones de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="982b6-167">Permission behavior across login sessions</span></span>

<span data-ttu-id="982b6-168">Los permisos de dispositivos nativos se almacenan para cada sesión de inicio.</span><span class="sxs-lookup"><span data-stu-id="982b6-168">Native device permissions are stored for every login session.</span></span> <span data-ttu-id="982b6-169">Significa que si inicia sesión en otra instancia de Teams (por ejemplo: en otro equipo), los permisos de dispositivo de las sesiones anteriores no estarán disponibles.</span><span class="sxs-lookup"><span data-stu-id="982b6-169">It means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="982b6-170">En su lugar, tendrá que volver a dar su consentimiento a los permisos de dispositivo para la nueva sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="982b6-170">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="982b6-171">También significa que, si sale de la sesión de Microsoft Teams (o de los inquilinos de conmutador dentro de los equipos), los permisos de dispositivo se eliminarán para la sesión de inicio anterior.</span><span class="sxs-lookup"><span data-stu-id="982b6-171">It also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="982b6-172">Tenga esto en cuenta cuando desarrolle permisos de dispositivos nativos: las funciones nativas con las que da su consentimiento están solo para su sesión de inicio _actual_ .</span><span class="sxs-lookup"><span data-stu-id="982b6-172">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
