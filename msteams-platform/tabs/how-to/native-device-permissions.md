---
title: Solicitar permisos de dispositivo para la pestaña de Microsoft Teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que suelen requerir el consentimiento del usuario
keywords: desarrollo de pestañas de Microsoft Teams
ms.openlocfilehash: f0e19c0ed716147c097137c4ef0bf3454783b2eb
ms.sourcegitcommit: c4a7bc638e848a702cce92798cba84917fcecc35
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/24/2020
ms.locfileid: "42928520"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="20bed-104">Solicitar permisos de dispositivo para la pestaña de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="20bed-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="20bed-105">Es posible que quiera enriquecer su pestaña con características que requieran la funcionalidad de dispositivo nativo de Access como:</span><span class="sxs-lookup"><span data-stu-id="20bed-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

* <span data-ttu-id="20bed-106">Digital</span><span class="sxs-lookup"><span data-stu-id="20bed-106">Camera</span></span>
* <span data-ttu-id="20bed-107">Micro</span><span class="sxs-lookup"><span data-stu-id="20bed-107">Microphone</span></span>
* <span data-ttu-id="20bed-108">Ubicación</span><span class="sxs-lookup"><span data-stu-id="20bed-108">Location</span></span>
* <span data-ttu-id="20bed-109">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="20bed-109">Notifications</span></span>

![Pantalla de configuración de permisos de dispositivo](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
> <span data-ttu-id="20bed-111">Actualmente, la funcionalidad de dispositivos nativos no es compatible con las pestañas de clientes móviles, pero pronto estará disponible la compatibilidad completa.</span><span class="sxs-lookup"><span data-stu-id="20bed-111">Native device functionality is currently not supported for tabs on mobile clients but full support is coming soon.</span></span> <span data-ttu-id="20bed-112">Para prepararse para este cambio, debe seguir las [instrucciones para las pestañas de dispositivos móviles](~/tabs/design/tabs-mobile.md) al crear las pestañas.</span><span class="sxs-lookup"><span data-stu-id="20bed-112">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="20bed-113">Las aplicaciones personales (pestañas estáticas) están disponibles actualmente en [Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="20bed-113">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="20bed-114">Cuando se publica la compatibilidad completa de pestañas:</span><span class="sxs-lookup"><span data-stu-id="20bed-114">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="20bed-115">Todas las pestañas estarán siempre disponibles en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="20bed-115">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="20bed-116">El `contentUrl` **se cargará en el cliente móvil de Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="20bed-116">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="20bed-117">En las pestañas canal/grupo, los usuarios pueden abrir la pestaña en un explorador independiente `websiteUrl`a través de `contentUrl` la, pero se cargará primero.</span><span class="sxs-lookup"><span data-stu-id="20bed-117">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>  

## <a name="device-permissions"></a><span data-ttu-id="20bed-118">Permisos de dispositivo</span><span class="sxs-lookup"><span data-stu-id="20bed-118">Device permissions</span></span>

<span data-ttu-id="20bed-119">El acceso a los permisos de dispositivo de un usuario le permite crear experiencias mucho más enriquecidas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="20bed-119">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="20bed-120">Grabar y compartir vídeos breves</span><span class="sxs-lookup"><span data-stu-id="20bed-120">Record and share short videos</span></span>
* <span data-ttu-id="20bed-121">Grabe memorandos de audio cortos y guárdelos para más tarde</span><span class="sxs-lookup"><span data-stu-id="20bed-121">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="20bed-122">Usar la información de ubicación del usuario para mostrar información relevante</span><span class="sxs-lookup"><span data-stu-id="20bed-122">Use user location information to display relevant information</span></span>

<span data-ttu-id="20bed-123">Aunque el acceso a estas características es estándar en la mayoría de los exploradores Web modernos, es necesario que los equipos sepan qué características desea usar al actualizar el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="20bed-123">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="20bed-124">Esto le permitirá solicitar permisos, de la misma manera que lo haría en un explorador, mientras la aplicación se ejecuta en el cliente de escritorio de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="20bed-124">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="properties"></a><span data-ttu-id="20bed-125">Propiedades</span><span class="sxs-lookup"><span data-stu-id="20bed-125">Properties</span></span>

<span data-ttu-id="20bed-126">Actualice la aplicación `manifest.json` agregando `devicePermissions` y especificando cuál de las cinco propiedades desea usar en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="20bed-126">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="20bed-127">Cada propiedad le permitirá pedir al usuario que pida su consentimiento</span><span class="sxs-lookup"><span data-stu-id="20bed-127">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="20bed-128">Propiedad</span><span class="sxs-lookup"><span data-stu-id="20bed-128">Property</span></span>      | <span data-ttu-id="20bed-129">Descripción</span><span class="sxs-lookup"><span data-stu-id="20bed-129">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="20bed-130">Elementos multimedia</span><span class="sxs-lookup"><span data-stu-id="20bed-130">media</span></span>         | <span data-ttu-id="20bed-131">permiso para usar la cámara, el micrófono y los altavoces</span><span class="sxs-lookup"><span data-stu-id="20bed-131">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="20bed-132">geolocalización</span><span class="sxs-lookup"><span data-stu-id="20bed-132">geolocation</span></span>   | <span data-ttu-id="20bed-133">permiso para devolver la ubicación del usuario</span><span class="sxs-lookup"><span data-stu-id="20bed-133">permission to return the user's location</span></span>      |
| <span data-ttu-id="20bed-134">notificaciones</span><span class="sxs-lookup"><span data-stu-id="20bed-134">notifications</span></span> | <span data-ttu-id="20bed-135">permiso para enviar notificaciones de usuario</span><span class="sxs-lookup"><span data-stu-id="20bed-135">permission to send the user notifications</span></span>      |
| <span data-ttu-id="20bed-136">MIDI</span><span class="sxs-lookup"><span data-stu-id="20bed-136">midi</span></span>          | <span data-ttu-id="20bed-137">permiso para enviar y recibir información MIDI de un instrumento musical digital</span><span class="sxs-lookup"><span data-stu-id="20bed-137">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="20bed-138">openExternal</span><span class="sxs-lookup"><span data-stu-id="20bed-138">openExternal</span></span>  | <span data-ttu-id="20bed-139">permiso para abrir vínculos en aplicaciones externas</span><span class="sxs-lookup"><span data-stu-id="20bed-139">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="20bed-140">Comprobación de permisos en la pestaña</span><span class="sxs-lookup"><span data-stu-id="20bed-140">Checking permissions from your tab</span></span>

<span data-ttu-id="20bed-141">Una vez que haya `devicePermissions` agregado al manifiesto de la aplicación, puede comprobar los permisos mediante la API de "permisos" de HTML5 sin que se le pida confirmación.</span><span class="sxs-lookup"><span data-stu-id="20bed-141">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="20bed-142">Preguntar al usuario</span><span class="sxs-lookup"><span data-stu-id="20bed-142">Prompting the user</span></span>

<span data-ttu-id="20bed-143">Para mostrar una solicitud para obtener consentimiento para obtener acceso a los permisos del dispositivo, necesita aprovechar la API de HTML5 adecuada.</span><span class="sxs-lookup"><span data-stu-id="20bed-143">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 API.</span></span> <span data-ttu-id="20bed-144">Por ejemplo, para pedir al usuario que tenga acceso a su cámara, debe llamar a`getUserMedia`</span><span class="sxs-lookup"><span data-stu-id="20bed-144">For example, in order to prompt the user to access their camera you need to call `getUserMedia`</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="20bed-145">La ubicación geográfica mostrará una solicitud de permiso cuando llame a`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="20bed-145">Geolocation will  show a permission prompt when you call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="20bed-146">Las notificaciones le preguntarán al usuario cuando llame a`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="20bed-146">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Pestañas del mensaje de permisos de dispositivo](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="20bed-148">Comportamiento de permisos en sesiones de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="20bed-148">Permission behavior across login sessions</span></span>

<span data-ttu-id="20bed-149">Los permisos de dispositivos nativos se almacenan por sesión de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="20bed-149">Native device permissions are stored per login session.</span></span> <span data-ttu-id="20bed-150">Esto significa que si inicia sesión en otra instancia de Teams (por ejemplo: en otro equipo), los permisos de dispositivo de las sesiones anteriores no estarán disponibles.</span><span class="sxs-lookup"><span data-stu-id="20bed-150">This means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="20bed-151">En su lugar, tendrá que volver a dar su consentimiento a los permisos de dispositivo para el nuevo inicio de sesión sessoin.</span><span class="sxs-lookup"><span data-stu-id="20bed-151">Instead, you will need to re-consent to device permissions for the new login sessoin.</span></span> <span data-ttu-id="20bed-152">Esto también significa que, si sale de la sesión de Teams (o de los inquilinos de conmutador dentro de los equipos), los permisos de dispositivo se eliminarán para la sesión de inicio anterior.</span><span class="sxs-lookup"><span data-stu-id="20bed-152">This also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="20bed-153">Tenga esto en cuenta cuando desarrolle permisos de dispositivos nativos: las capacidades nativas con las que da su consentimiento son solo para su sessoin de inicio de sesión _actual_ .</span><span class="sxs-lookup"><span data-stu-id="20bed-153">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login sessoin.</span></span>