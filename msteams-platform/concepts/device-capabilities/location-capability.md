---
title: Integrar capacidades de ubicación
description: Cómo usar el SDK de cliente de JavaScript de Teams para aprovechar las capacidades de ubicación
keywords: capacidades de mapa de ubicación permisos de dispositivo nativos
ms.author: lajanuar
ms.openlocfilehash: fccf39c37c785be716bfff26907f9184c0d9beec
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449640"
---
# <a name="integrate-location-capabilities"></a><span data-ttu-id="fb36e-104">Integrar capacidades de ubicación</span><span class="sxs-lookup"><span data-stu-id="fb36e-104">Integrate location capabilities</span></span> 

<span data-ttu-id="fb36e-105">Este documento te guía sobre cómo integrar las capacidades de ubicación del dispositivo nativo con la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="fb36e-105">This document guides you on how to integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="fb36e-106">Puedes usar el SDK de cliente javaScript de [Microsoft Teams,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)que proporciona las herramientas necesarias para que la aplicación pueda acceder a las capacidades nativas del dispositivo del [usuario.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="fb36e-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="fb36e-107">Usa las API de ubicación, como [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_) y [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_) para integrar las funcionalidades dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fb36e-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_) and [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="fb36e-108">Ventajas de integrar las capacidades de ubicación</span><span class="sxs-lookup"><span data-stu-id="fb36e-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="fb36e-109">La principal ventaja de integrar las capacidades de ubicación en las aplicaciones de Teams es que permite a los desarrolladores de aplicaciones web en la plataforma Teams aprovechar la funcionalidad de ubicación con el SDK de cliente javaScript de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="fb36e-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="fb36e-110">Los ejemplos siguientes muestran cómo se usa la integración de las capacidades de ubicación en diferentes escenarios:</span><span class="sxs-lookup"><span data-stu-id="fb36e-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="fb36e-111">En una fábrica, el supervisor puede realizar un seguimiento de la asistencia de los trabajadores pidiéndoles que se tomen un selfi en las proximidades de la fábrica y la compartan a través de la aplicación especificada.</span><span class="sxs-lookup"><span data-stu-id="fb36e-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="fb36e-112">Los datos de ubicación también se capturan y envían junto con la imagen.</span><span class="sxs-lookup"><span data-stu-id="fb36e-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="fb36e-113">Las capacidades de ubicación permiten al personal de mantenimiento de un proveedor de servicios compartir los datos de estado auténticos de las torres de telefonía móvil con la administración.</span><span class="sxs-lookup"><span data-stu-id="fb36e-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="fb36e-114">La administración puede comparar cualquier discrepancia entre la información de ubicación capturada y los datos enviados por el personal de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="fb36e-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="fb36e-115">Para integrar las funcionalidades de ubicación, debes actualizar el archivo de manifiesto de la aplicación y llamar a las API.</span><span class="sxs-lookup"><span data-stu-id="fb36e-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="fb36e-116">Para una integración eficaz, debe tener una buena comprensión de los [fragmentos](#code-snippets) de código para llamar a las API de ubicación.</span><span class="sxs-lookup"><span data-stu-id="fb36e-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="fb36e-117">Es importante familiarizarse con los errores de respuesta [de la API](#error-handling) para controlar los errores de la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="fb36e-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="fb36e-118">Actualmente, la compatibilidad de Microsoft Teams con las capacidades de ubicación solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="fb36e-118">Currently, Microsoft Teams support for location capabilities is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="fb36e-119">Manifiesto de actualización</span><span class="sxs-lookup"><span data-stu-id="fb36e-119">Update manifest</span></span>

<span data-ttu-id="fb36e-120">Actualice la aplicación de Teams [manifest.jsarchivo](../../resources/schema/manifest-schema.md#devicepermissions) agregando la propiedad `devicePermissions` y especificando `geolocation` .</span><span class="sxs-lookup"><span data-stu-id="fb36e-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="fb36e-121">Permite a la aplicación solicitar los permisos necesarios a los usuarios antes de empezar a usar las funcionalidades de ubicación.</span><span class="sxs-lookup"><span data-stu-id="fb36e-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="fb36e-122">El **símbolo del sistema Solicitar permisos** se muestra automáticamente cuando se inicia una API de Teams relevante.</span><span class="sxs-lookup"><span data-stu-id="fb36e-122">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="fb36e-123">Para obtener más información, consulta [solicitar permisos de dispositivo](native-device-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="fb36e-123">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="fb36e-124">API de ubicación</span><span class="sxs-lookup"><span data-stu-id="fb36e-124">Location APIs</span></span>

<span data-ttu-id="fb36e-125">Debes usar el siguiente conjunto de API para habilitar las capacidades de ubicación del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="fb36e-125">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="fb36e-126">API</span><span class="sxs-lookup"><span data-stu-id="fb36e-126">API</span></span>      | <span data-ttu-id="fb36e-127">Descripción</span><span class="sxs-lookup"><span data-stu-id="fb36e-127">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="fb36e-128">getLocation</span><span class="sxs-lookup"><span data-stu-id="fb36e-128">getLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_) | <span data-ttu-id="fb36e-129">Proporciona la ubicación del dispositivo actual del usuario o abre el selector de ubicación nativa y devuelve la ubicación elegida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="fb36e-129">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="fb36e-130">showLocation</span><span class="sxs-lookup"><span data-stu-id="fb36e-130">showLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation) | <span data-ttu-id="fb36e-131">Muestra la ubicación en el mapa</span><span class="sxs-lookup"><span data-stu-id="fb36e-131">Shows location on map</span></span> |

> [!NOTE]

> <span data-ttu-id="fb36e-132">La `getLocation()` API incluye las siguientes [configuraciones de entrada](https://docs.microsoft.com/en-us/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest)y `allowChooseLocation` `showMap` .</span><span class="sxs-lookup"><span data-stu-id="fb36e-132">The `getLocation()` API comes along with following [input configurations](https://docs.microsoft.com/en-us/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="fb36e-133">Si el valor de `allowChooseLocation` es *true*, los usuarios pueden elegir cualquier ubicación de su elección.</span><span class="sxs-lookup"><span data-stu-id="fb36e-133">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="fb36e-134">Si el valor es *false*, los usuarios no pueden cambiar su ubicación actual.</span><span class="sxs-lookup"><span data-stu-id="fb36e-134">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="fb36e-135">Si el valor de `showMap` es *false*, se captura la ubicación actual sin mostrar el mapa.</span><span class="sxs-lookup"><span data-stu-id="fb36e-135">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="fb36e-136">`showMap` se omite si `allowChooseLocation` se establece en *true*.</span><span class="sxs-lookup"><span data-stu-id="fb36e-136">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span> 

<span data-ttu-id="fb36e-137">**Experiencia de aplicación web para funcionalidades de ubicación** 
 ![ experiencia de la aplicación web para funcionalidades de ubicación](../../assets/images/tabs/location-capability.png)</span><span class="sxs-lookup"><span data-stu-id="fb36e-137">**Web app experience for location capabilities**
![web app experience for location capabilities](../../assets/images/tabs/location-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="fb36e-138">Control de errores</span><span class="sxs-lookup"><span data-stu-id="fb36e-138">Error handling</span></span>

<span data-ttu-id="fb36e-139">Debes asegurarte de controlar estos errores correctamente en la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="fb36e-139">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="fb36e-140">En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores:</span><span class="sxs-lookup"><span data-stu-id="fb36e-140">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="fb36e-141">Código de error</span><span class="sxs-lookup"><span data-stu-id="fb36e-141">Error code</span></span> |  <span data-ttu-id="fb36e-142">Nombre del error</span><span class="sxs-lookup"><span data-stu-id="fb36e-142">Error name</span></span>     | <span data-ttu-id="fb36e-143">Condition</span><span class="sxs-lookup"><span data-stu-id="fb36e-143">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="fb36e-144">**100**</span><span class="sxs-lookup"><span data-stu-id="fb36e-144">**100**</span></span> | <span data-ttu-id="fb36e-145">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="fb36e-145">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="fb36e-146">La API no se admite en la plataforma actual.</span><span class="sxs-lookup"><span data-stu-id="fb36e-146">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="fb36e-147">**500**</span><span class="sxs-lookup"><span data-stu-id="fb36e-147">**500**</span></span> | <span data-ttu-id="fb36e-148">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="fb36e-148">INTERNAL_ERROR</span></span> | <span data-ttu-id="fb36e-149">Se produce un error interno al realizar la operación necesaria.</span><span class="sxs-lookup"><span data-stu-id="fb36e-149">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="fb36e-150">**1000**</span><span class="sxs-lookup"><span data-stu-id="fb36e-150">**1000**</span></span> | <span data-ttu-id="fb36e-151">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="fb36e-151">PERMISSION_DENIED</span></span> |<span data-ttu-id="fb36e-152">El usuario ha denegado los permisos de ubicación a teams app o web-app .</span><span class="sxs-lookup"><span data-stu-id="fb36e-152">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="fb36e-153">**4000**</span><span class="sxs-lookup"><span data-stu-id="fb36e-153">**4000**</span></span> | <span data-ttu-id="fb36e-154">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="fb36e-154">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="fb36e-155">La API se invoca con argumentos obligatorios incorrectos o insuficientes.</span><span class="sxs-lookup"><span data-stu-id="fb36e-155">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="fb36e-156">**8000**</span><span class="sxs-lookup"><span data-stu-id="fb36e-156">**8000**</span></span> | <span data-ttu-id="fb36e-157">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="fb36e-157">USER_ABORT</span></span> |<span data-ttu-id="fb36e-158">El usuario canceló la operación.</span><span class="sxs-lookup"><span data-stu-id="fb36e-158">User cancelled the operation.</span></span>|
| <span data-ttu-id="fb36e-159">**9000**</span><span class="sxs-lookup"><span data-stu-id="fb36e-159">**9000**</span></span> | <span data-ttu-id="fb36e-160">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="fb36e-160">OLD_PLATFORM</span></span> | <span data-ttu-id="fb36e-161">El usuario se encuentra en una compilación de plataforma antigua donde la implementación de la API no está presente.</span><span class="sxs-lookup"><span data-stu-id="fb36e-161">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="fb36e-162">La actualización de la compilación debe resolver el problema.</span><span class="sxs-lookup"><span data-stu-id="fb36e-162">Upgrading the build should resolve the issue.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="fb36e-163">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="fb36e-163">Code snippets</span></span>

<span data-ttu-id="fb36e-164">**Llamar `getLocation` a la API para recuperar la ubicación:**</span><span class="sxs-lookup"><span data-stu-id="fb36e-164">**Calling `getLocation` API to retrieve the location:**</span></span>

```javascript
let locationProps = {"allowChooseLocation":true,"showMap":true};
microsoftTeams.location.getLocation(locationProps, (err: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
          if (err) {
            output(err);
            return;
          }
          output(JSON.stringify(location));
});
```

<span data-ttu-id="fb36e-165">**Llamar `showLocation` a la API para mostrar la ubicación:**</span><span class="sxs-lookup"><span data-stu-id="fb36e-165">**Calling `showLocation` API to display the location:**</span></span>

```javascript
let location = {"latitude":17,"longitude":17};
microsoftTeams.location.showLocation(location, (err: microsoftTeams.SdkError, result: boolean) => {
          if (err) {
            output(err);
            return;
          }
     output(result);
});
```

## <a name="see-also"></a><span data-ttu-id="fb36e-166">Vea también</span><span class="sxs-lookup"><span data-stu-id="fb36e-166">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb36e-167">Integrar capacidades multimedia en Teams</span><span class="sxs-lookup"><span data-stu-id="fb36e-167">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb36e-168">Integrar la funcionalidad del escáner de códigos DE BARRAS o QR en Teams</span><span class="sxs-lookup"><span data-stu-id="fb36e-168">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)