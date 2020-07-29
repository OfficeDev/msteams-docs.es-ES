---
title: Solicitar permisos de dispositivo para la pestaña de Microsoft Teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que suelen requerir el consentimiento del usuario
keywords: desarrollo de pestañas de Microsoft Teams
ms.openlocfilehash: e69c7540730307e62035c48ac64cd977419ea5f2
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434559"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="d1ec8-104">Solicitar permisos de dispositivo para la pestaña de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d1ec8-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="d1ec8-105">Es posible que quiera enriquecer su pestaña con características que requieran la funcionalidad de dispositivo nativo de Access como:</span><span class="sxs-lookup"><span data-stu-id="d1ec8-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="d1ec8-106">Digital</span><span class="sxs-lookup"><span data-stu-id="d1ec8-106">Camera</span></span>
> * <span data-ttu-id="d1ec8-107">Micro</span><span class="sxs-lookup"><span data-stu-id="d1ec8-107">Microphone</span></span>
> * <span data-ttu-id="d1ec8-108">Ubicación</span><span class="sxs-lookup"><span data-stu-id="d1ec8-108">Location</span></span>
> * <span data-ttu-id="d1ec8-109">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="d1ec8-109">Notifications</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="d1ec8-110">Actualmente, el cliente móvil de Microsoft Teams solo admite `camera` y `location` a través de capacidades de dispositivo nativas y está disponible en todas las construcciones de aplicaciones, incluidas las pestañas.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-110">Currently, Teams mobile client only supports `camera` and `location`  through native device capabilities and is available on all app constructs including tabs.</span></span> </br>
> * <span data-ttu-id="d1ec8-111">`camera`La [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-)habilita la compatibilidad con la captura de imágenes.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-111">Support for `camera` image capture is enabled by the [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-).</span></span>
> * <span data-ttu-id="d1ec8-112">Actualmente, la [**API de ubicación geográfica**](../../resources/schema/manifest-schema.md#devicepermissions) no es totalmente compatible con todos los clientes de escritorio.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-112">The [**geolocation API**](../../resources/schema/manifest-schema.md#devicepermissions) is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="d1ec8-113">Permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="d1ec8-113">Device permissions</span></span>

<span data-ttu-id="d1ec8-114">El acceso a los permisos de dispositivo de un usuario le permite crear experiencias mucho más enriquecidas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d1ec8-114">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="d1ec8-115">Grabar y compartir vídeos breves</span><span class="sxs-lookup"><span data-stu-id="d1ec8-115">Record and share short videos</span></span>
* <span data-ttu-id="d1ec8-116">Grabe memorandos de audio cortos y guárdelos para más tarde</span><span class="sxs-lookup"><span data-stu-id="d1ec8-116">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="d1ec8-117">Usar la información de ubicación del usuario para mostrar información relevante</span><span class="sxs-lookup"><span data-stu-id="d1ec8-117">Use user location information to display relevant information</span></span>

<span data-ttu-id="d1ec8-118">Aunque el acceso a estas características es estándar en la mayoría de los exploradores Web modernos, es necesario que los equipos sepan qué características desea usar al actualizar el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-118">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="d1ec8-119">Esto le permitirá solicitar permisos, de la misma manera que lo haría en un explorador, mientras la aplicación se ejecuta en el cliente de escritorio de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-119">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="d1ec8-120">Administrar permisos</span><span class="sxs-lookup"><span data-stu-id="d1ec8-120">Manage permissions</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d1ec8-121">Escritorio</span><span class="sxs-lookup"><span data-stu-id="d1ec8-121">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="d1ec8-122">Abra Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-122">Open Teams.</span></span>
1. <span data-ttu-id="d1ec8-123">En la esquina superior derecha de la ventana, seleccione el icono de su perfil.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-123">In the upper right corner of the window, select your profile icon.</span></span>
1. <span data-ttu-id="d1ec8-124">Seleccione **Settings**  ->  **Permissions** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-124">Select **Settings** -> **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="d1ec8-125">Elija la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-125">Choose your desired settings.</span></span>

![Pantalla Configuración del escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="d1ec8-127">Móvil</span><span class="sxs-lookup"><span data-stu-id="d1ec8-127">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="d1ec8-128">Abra Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-128">Open Teams.</span></span>
1. <span data-ttu-id="d1ec8-129">En la esquina superior izquierda de la pantalla, seleccione el icono del menú &#9776;.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-129">In the upper left corner of the screen, select the &#9776; menu icon.</span></span>
1. <span data-ttu-id="d1ec8-130">Seleccione **configuración**de  ->  **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-130">Select **Settings** -> **Devices**.</span></span>
1. <span data-ttu-id="d1ec8-131">Elija la configuración que desee.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-131">Choose your desired settings.</span></span>

![Pantalla de configuración móvil de permisos de dispositivo](../../assets/images/tabs/mobile-device-permissions-screen.png)

---

## <a name="properties"></a><span data-ttu-id="d1ec8-133">Propiedades</span><span class="sxs-lookup"><span data-stu-id="d1ec8-133">Properties</span></span>

<span data-ttu-id="d1ec8-134">Actualice la aplicación `manifest.json` agregando `devicePermissions` y especificando cuál de las cinco propiedades desea usar en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="d1ec8-134">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

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
> <span data-ttu-id="d1ec8-135">Los medios también se usan para los permisos de cámara en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-135">Media is also used for camera permissions in mobile.</span></span>

<span data-ttu-id="d1ec8-136">Cada propiedad le permitirá pedir al usuario que pida su consentimiento</span><span class="sxs-lookup"><span data-stu-id="d1ec8-136">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="d1ec8-137">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d1ec8-137">Property</span></span>      | <span data-ttu-id="d1ec8-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1ec8-138">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="d1ec8-139">medios</span><span class="sxs-lookup"><span data-stu-id="d1ec8-139">media</span></span>         | <span data-ttu-id="d1ec8-140">permiso para usar la cámara, el micrófono y los altavoces</span><span class="sxs-lookup"><span data-stu-id="d1ec8-140">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="d1ec8-141">geolocalización</span><span class="sxs-lookup"><span data-stu-id="d1ec8-141">geolocation</span></span>   | <span data-ttu-id="d1ec8-142">permiso para devolver la ubicación del usuario</span><span class="sxs-lookup"><span data-stu-id="d1ec8-142">permission to return the user's location</span></span>      |
| <span data-ttu-id="d1ec8-143">notificaciones</span><span class="sxs-lookup"><span data-stu-id="d1ec8-143">notifications</span></span> | <span data-ttu-id="d1ec8-144">permiso para enviar notificaciones de usuario</span><span class="sxs-lookup"><span data-stu-id="d1ec8-144">permission to send the user notifications</span></span>      |
| <span data-ttu-id="d1ec8-145">MIDI</span><span class="sxs-lookup"><span data-stu-id="d1ec8-145">midi</span></span>          | <span data-ttu-id="d1ec8-146">permiso para enviar y recibir información MIDI de un instrumento musical digital</span><span class="sxs-lookup"><span data-stu-id="d1ec8-146">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="d1ec8-147">openExternal</span><span class="sxs-lookup"><span data-stu-id="d1ec8-147">openExternal</span></span>  | <span data-ttu-id="d1ec8-148">permiso para abrir vínculos en aplicaciones externas</span><span class="sxs-lookup"><span data-stu-id="d1ec8-148">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="d1ec8-149">Comprobación de permisos en la pestaña</span><span class="sxs-lookup"><span data-stu-id="d1ec8-149">Checking permissions from your tab</span></span>

<span data-ttu-id="d1ec8-150">Una vez que haya agregado `devicePermissions` al manifiesto de la aplicación, puede comprobar los permisos mediante la API de "permisos" de HTML5 sin que se le pida confirmación.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-150">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="d1ec8-151">Preguntar al usuario</span><span class="sxs-lookup"><span data-stu-id="d1ec8-151">Prompting the user</span></span>

<span data-ttu-id="d1ec8-152">Para mostrar una solicitud para obtener consentimiento para obtener acceso a los permisos de dispositivo necesita aprovechar la API de HTML5 o Teams adecuada.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-152">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 or Teams API.</span></span> <span data-ttu-id="d1ec8-153">Por ejemplo, para pedir al usuario que tenga acceso a su cámara, debe llamar a`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="d1ec8-153">For example, in order to prompt the user to access their camera you need to call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="d1ec8-154">Para usar la cámara en el escritorio o en la web, Microsoft Teams mostrará una solicitud de permiso cuando llame a getUserMedia</span><span class="sxs-lookup"><span data-stu-id="d1ec8-154">To use camera on desktop or web, Teams will show a permission prompt when you call getUserMedia</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="d1ec8-155">Para capturar la imagen en dispositivos móviles, Teams Mobile le pedirá permiso cuando se lo denomine captureImage ().</span><span class="sxs-lookup"><span data-stu-id="d1ec8-155">To capture image on mobile, Teams mobile will ask for permission when called captureImage()</span></span>

```Typescript
function captureImage(callback: (error: SdkError, files: File[]) => void)
```

<span data-ttu-id="d1ec8-156">Las notificaciones le preguntarán al usuario cuando llame a`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="d1ec8-156">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Pestañas del mensaje de permisos de dispositivo](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="d1ec8-158">Comportamiento de permisos en sesiones de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="d1ec8-158">Permission behavior across login sessions</span></span>

<span data-ttu-id="d1ec8-159">Los permisos de dispositivos nativos se almacenan por sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-159">Native device permissions are stored per login session.</span></span> <span data-ttu-id="d1ec8-160">Esto significa que si inicia sesión en otra instancia de Teams (por ejemplo: en otro equipo), los permisos de dispositivo de las sesiones anteriores no estarán disponibles.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-160">This means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="d1ec8-161">En su lugar, tendrá que volver a dar su consentimiento a los permisos de dispositivo para la nueva sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-161">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="d1ec8-162">Esto también significa que, si sale de la sesión de Teams (o de los inquilinos de conmutador dentro de los equipos), los permisos de dispositivo se eliminarán para la sesión de inicio anterior.</span><span class="sxs-lookup"><span data-stu-id="d1ec8-162">This also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="d1ec8-163">Tenga esto en cuenta cuando desarrolle permisos de dispositivos nativos: las funciones nativas con las que da su consentimiento están solo para su sesión de inicio _actual_ .</span><span class="sxs-lookup"><span data-stu-id="d1ec8-163">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
