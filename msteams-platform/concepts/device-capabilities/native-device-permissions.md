---
title: Solicitar permisos de dispositivo para la pestaña
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que normalmente requieren el consentimiento del usuario
ms.topic: how-to
keywords: desarrollo de pestañas de teams
ms.openlocfilehash: a2893fb2905584eac4b398287d431f406c23b12b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014533"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="f4e2c-104">Solicitar permisos de dispositivo para la pestaña de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f4e2c-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="f4e2c-105">Es posible que quieras enriquecer la pestaña con características que requieren acceso a la funcionalidad de dispositivo nativo, como:</span><span class="sxs-lookup"><span data-stu-id="f4e2c-105">You might want to enrich your tab with features that require access to native device functionality like:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="f4e2c-106">Cámara</span><span class="sxs-lookup"><span data-stu-id="f4e2c-106">Camera</span></span>
> * <span data-ttu-id="f4e2c-107">Micrófono</span><span class="sxs-lookup"><span data-stu-id="f4e2c-107">Microphone</span></span>
> * <span data-ttu-id="f4e2c-108">Ubicación</span><span class="sxs-lookup"><span data-stu-id="f4e2c-108">Location</span></span>
> * <span data-ttu-id="f4e2c-109">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="f4e2c-109">Notifications</span></span>

> [!NOTE]
> <span data-ttu-id="f4e2c-110">Para integrar las capacidades de cámara e imagen dentro de la aplicación móvil de Microsoft Teams, vea las funciones de cámara [e imagen en Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="f4e2c-110">To integrate camera and image capabilities within your Microsoft Teams mobile app, see [Camera and image capabilities in Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="f4e2c-111">Actualmente, el cliente móvil de Teams solo admite el acceso a , y a través de las capacidades de dispositivo nativo y está disponible en todas las construcciones de `camera` `gallery` `mic` `location` aplicaciones, incluidas las pestañas.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-111">At present, Teams mobile client only supports access to `camera`, `gallery`, `mic`, and `location` through native device capabilities and is available on all app constructs including tabs.</span></span> </br>
> * <span data-ttu-id="f4e2c-112">Compatibilidad con `camera` , y se habilita a través de la API de `gallery` `mic` [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f4e2c-112">Support for `camera`, `gallery`, and `mic` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="f4e2c-113">Para la captura de imagen única, puede usar [**la API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f4e2c-113">For single image capture you may use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).</span></span>
> * <span data-ttu-id="f4e2c-114">La compatibilidad con `location` se habilita a través de la API [**getLocation**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f4e2c-114">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="f4e2c-115">Se recomienda usar esta API, ya que la [**API de geolocalización**](../../resources/schema/manifest-schema.md#devicepermissions) no es totalmente compatible actualmente con todos los clientes de escritorio.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-115">It's recommended you use this API as [**geolocation API**](../../resources/schema/manifest-schema.md#devicepermissions) is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="f4e2c-116">Permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="f4e2c-116">Device permissions</span></span>

<span data-ttu-id="f4e2c-117">El acceso a los permisos de dispositivo de un usuario le permite crear experiencias mucho más enriqueciendo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f4e2c-117">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="f4e2c-118">Grabar y compartir vídeos cortos</span><span class="sxs-lookup"><span data-stu-id="f4e2c-118">Record and share short videos</span></span>
* <span data-ttu-id="f4e2c-119">Grabar notas breves de audio y guardarlas para más adelante</span><span class="sxs-lookup"><span data-stu-id="f4e2c-119">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="f4e2c-120">Usar la información de ubicación del usuario para mostrar información relevante</span><span class="sxs-lookup"><span data-stu-id="f4e2c-120">Use user location information to display relevant information</span></span>

<span data-ttu-id="f4e2c-121">Aunque el acceso a estas características es estándar en la mayoría de los exploradores web modernos, necesita que Teams sepa qué características desea usar mediante la actualización del manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-121">While access to these features is standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="f4e2c-122">Esto le permitirá solicitar permisos, del mismo modo que lo haría en un explorador, mientras la aplicación se ejecuta en el cliente de escritorio de Teams.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-122">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="f4e2c-123">Administrar permisos</span><span class="sxs-lookup"><span data-stu-id="f4e2c-123">Manage permissions</span></span>

# <a name="desktop"></a>[<span data-ttu-id="f4e2c-124">Escritorio</span><span class="sxs-lookup"><span data-stu-id="f4e2c-124">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="f4e2c-125">Abra Teams.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-125">Open Teams.</span></span>
1. <span data-ttu-id="f4e2c-126">En la esquina superior derecha de la ventana, seleccione el icono de perfil.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-126">In the upper right corner of the window, select your profile icon.</span></span>
1. <span data-ttu-id="f4e2c-127">Seleccione **Permisos**  ->  **de configuración** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-127">Select **Settings** -> **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="f4e2c-128">Elige la configuración que quieras.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-128">Choose your desired settings.</span></span>

![Pantalla de configuración de escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="f4e2c-130">Móvil</span><span class="sxs-lookup"><span data-stu-id="f4e2c-130">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="f4e2c-131">Abra Teams.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-131">Open Teams.</span></span>
1. <span data-ttu-id="f4e2c-132">Vaya a **Configuración de** permisos  ->  **de aplicación.**</span><span class="sxs-lookup"><span data-stu-id="f4e2c-132">Go to **Settings** -> **App Permissions**.</span></span>
1. <span data-ttu-id="f4e2c-133">Selecciona la aplicación para la que necesitas elegir la configuración.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-133">Select the app you need to choose settings for.</span></span>
1. <span data-ttu-id="f4e2c-134">Elige la configuración que quieras.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-134">Choose your desired settings.</span></span>

![Pantalla de configuración móvil de permisos de dispositivo](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="properties"></a><span data-ttu-id="f4e2c-136">Propiedades</span><span class="sxs-lookup"><span data-stu-id="f4e2c-136">Properties</span></span>

<span data-ttu-id="f4e2c-137">Actualiza las aplicaciones agregando y especificando cuál de las cinco propiedades `manifest.json` te gustaría usar en la `devicePermissions` aplicación:</span><span class="sxs-lookup"><span data-stu-id="f4e2c-137">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

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
> <span data-ttu-id="f4e2c-138">Los medios también se usan para permisos de cámara en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-138">Media is also used for camera permissions on mobile.</span></span>

<span data-ttu-id="f4e2c-139">Cada propiedad te permitirá pedir al usuario que solicite su consentimiento:</span><span class="sxs-lookup"><span data-stu-id="f4e2c-139">Each property will allow you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="f4e2c-140">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f4e2c-140">Property</span></span>      | <span data-ttu-id="f4e2c-141">Descripción</span><span class="sxs-lookup"><span data-stu-id="f4e2c-141">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="f4e2c-142">medios</span><span class="sxs-lookup"><span data-stu-id="f4e2c-142">media</span></span>         | <span data-ttu-id="f4e2c-143">permiso para usar la cámara, el micrófono, los altavoces y la galería multimedia de acceso</span><span class="sxs-lookup"><span data-stu-id="f4e2c-143">permission to use the camera, microphone, speakers, and access media gallery</span></span> |
| <span data-ttu-id="f4e2c-144">geolocalización</span><span class="sxs-lookup"><span data-stu-id="f4e2c-144">geolocation</span></span>   | <span data-ttu-id="f4e2c-145">permiso para devolver la ubicación del usuario</span><span class="sxs-lookup"><span data-stu-id="f4e2c-145">permission to return the user's location</span></span>      |
| <span data-ttu-id="f4e2c-146">notifications</span><span class="sxs-lookup"><span data-stu-id="f4e2c-146">notifications</span></span> | <span data-ttu-id="f4e2c-147">permiso para enviar notificaciones de usuario</span><span class="sxs-lookup"><span data-stu-id="f4e2c-147">permission to send the user notifications</span></span>      |
| <span data-ttu-id="f4e2c-148">midi</span><span class="sxs-lookup"><span data-stu-id="f4e2c-148">midi</span></span>          | <span data-ttu-id="f4e2c-149">permiso para enviar y recibir información midi de un instrumento digital</span><span class="sxs-lookup"><span data-stu-id="f4e2c-149">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="f4e2c-150">openExternal</span><span class="sxs-lookup"><span data-stu-id="f4e2c-150">openExternal</span></span>  | <span data-ttu-id="f4e2c-151">permiso para abrir vínculos en aplicaciones externas</span><span class="sxs-lookup"><span data-stu-id="f4e2c-151">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="f4e2c-152">Comprobar los permisos de la pestaña</span><span class="sxs-lookup"><span data-stu-id="f4e2c-152">Checking permissions from your tab</span></span>

<span data-ttu-id="f4e2c-153">Una vez que haya agregado al manifiesto de la aplicación, puede comprobar los permisos mediante la API de "permisos" de HTML5 sin causar `devicePermissions` ningún mensaje.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-153">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="f4e2c-154">Preguntar al usuario</span><span class="sxs-lookup"><span data-stu-id="f4e2c-154">Prompting the user</span></span>

<span data-ttu-id="f4e2c-155">Para mostrar un mensaje para obtener el consentimiento para obtener acceso a los permisos de dispositivo, debe aprovechar la API de HTML5 o Teams adecuada.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-155">To show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 or Teams API.</span></span> 

<span data-ttu-id="f4e2c-156">Por ejemplo, para solicitar al usuario que acceda a su ubicación, debe llamar `getCurrentPosition` a:</span><span class="sxs-lookup"><span data-stu-id="f4e2c-156">For example, to prompt the user to access their location you need to call `getCurrentPosition`:</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="f4e2c-157">Para usar la cámara en el escritorio o en la web, Teams mostrará un mensaje de permiso cuando llame `getUserMedia` a:</span><span class="sxs-lookup"><span data-stu-id="f4e2c-157">To use the camera on desktop or web, Teams will show a permission prompt when you call `getUserMedia`:</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="f4e2c-158">Para capturar la imagen en dispositivos móviles, Teams mobile pedirá permiso al `captureImage()` llamar:</span><span class="sxs-lookup"><span data-stu-id="f4e2c-158">To capture the image on mobile, Teams mobile will ask for permission when you call `captureImage()`:</span></span>

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

<span data-ttu-id="f4e2c-159">Las notificaciones preguntarán al usuario cuando `requestPermission` llame:</span><span class="sxs-lookup"><span data-stu-id="f4e2c-159">Notifications will prompt the user when you call `requestPermission`:</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

<span data-ttu-id="f4e2c-160">Para usar la cámara o acceder a la galería de fotos, Teams mobile pedirá permiso al `selectMedia()` llamar:</span><span class="sxs-lookup"><span data-stu-id="f4e2c-160">To use camera or access photo gallery, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="f4e2c-161">Para usar micrófono, Teams Mobile pedirá permiso cuando `selectMedia()` llame:</span><span class="sxs-lookup"><span data-stu-id="f4e2c-161">To use mic, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="f4e2c-162">Para solicitar al usuario que comparta la ubicación en la interfaz de mapa, teams móvil solicitará permiso cuando `getLocation()` llame:</span><span class="sxs-lookup"><span data-stu-id="f4e2c-162">To prompt user to share location on map interface, Teams mobile will ask permission when you call `getLocation()`:</span></span>

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[<span data-ttu-id="f4e2c-163">Escritorio</span><span class="sxs-lookup"><span data-stu-id="f4e2c-163">Desktop</span></span>](#tab/desktop)

![Mensaje de permisos de dispositivo de escritorio de pestañas](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="f4e2c-165">Móvil</span><span class="sxs-lookup"><span data-stu-id="f4e2c-165">Mobile</span></span>](#tab/mobile)

![Mensaje de permisos de dispositivo móvil de pestañas](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="f4e2c-167">Comportamiento de permisos en sesiones de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="f4e2c-167">Permission behavior across login sessions</span></span>

<span data-ttu-id="f4e2c-168">Los permisos de dispositivo nativo se almacenan para cada sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-168">Native device permissions are stored for every login session.</span></span> <span data-ttu-id="f4e2c-169">Esto significa que si inicia sesión en otra instancia de Teams (por ejemplo, en otro equipo), los permisos de dispositivo de las sesiones anteriores no estarán disponibles.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-169">It means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="f4e2c-170">En su lugar, tendrá que volver a dar su consentimiento a los permisos del dispositivo para la nueva sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-170">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="f4e2c-171">También significa que, si cierra sesión en Teams (o cambia de espacio empresarial dentro de Teams), los permisos del dispositivo se eliminarán para esa sesión de inicio de sesión anterior.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-171">It also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="f4e2c-172">Ten esto en cuenta al desarrollar permisos de dispositivo nativo: las funcionalidades nativas que consientes son solo para la sesión de inicio _de sesión_ actual.</span><span class="sxs-lookup"><span data-stu-id="f4e2c-172">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
