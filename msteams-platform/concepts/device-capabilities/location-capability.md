---
title: Integrar capacidades de ubicación
author: Rajeshwari-v
description: Cómo usar el SDK Teams cliente de JavaScript para aprovechar las funcionalidades de ubicación
keywords: capacidades de mapa de ubicación permisos de dispositivo nativos
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 3e6c4bda9a1a0024380cb295cd280db1d630f019
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211614"
---
# <a name="integrate-location-capabilities"></a><span data-ttu-id="31896-104">Integrar capacidades de ubicación</span><span class="sxs-lookup"><span data-stu-id="31896-104">Integrate location capabilities</span></span> 

<span data-ttu-id="31896-105">Puedes integrar las funcionalidades de ubicación del dispositivo nativo con la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="31896-105">You can integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="31896-106">Puedes usar Microsoft Teams [SDK de cliente de JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)que proporciona las herramientas necesarias para que la aplicación pueda tener acceso a las capacidades del dispositivo nativo del [usuario.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="31896-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="31896-107">Usa las API de ubicación, como [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) y [showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) para integrar las funcionalidades dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="31896-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) and [showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="31896-108">Ventajas de integrar las capacidades de ubicación</span><span class="sxs-lookup"><span data-stu-id="31896-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="31896-109">La principal ventaja de integrar las funcionalidades de ubicación en las aplicaciones de Teams es que permite Teams los desarrolladores de aplicaciones web en la plataforma aprovechar la funcionalidad de ubicación con Microsoft Teams SDK de cliente de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="31896-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="31896-110">Los ejemplos siguientes muestran cómo se usa la integración de las capacidades de ubicación en diferentes escenarios:</span><span class="sxs-lookup"><span data-stu-id="31896-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="31896-111">En una fábrica, el supervisor puede realizar un seguimiento de la asistencia de los trabajadores pidiéndoles que se tomen un selfi en las proximidades de la fábrica y la compartan a través de la aplicación especificada.</span><span class="sxs-lookup"><span data-stu-id="31896-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="31896-112">Los datos de ubicación también se capturan y envían junto con la imagen.</span><span class="sxs-lookup"><span data-stu-id="31896-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="31896-113">Las capacidades de ubicación permiten al personal de mantenimiento de un proveedor de servicios compartir los datos de estado auténticos de las torres de telefonía móvil con la administración.</span><span class="sxs-lookup"><span data-stu-id="31896-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="31896-114">La administración puede comparar cualquier discrepancia entre la información de ubicación capturada y los datos enviados por el personal de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="31896-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="31896-115">Para integrar las funcionalidades de ubicación, debes actualizar el archivo de manifiesto de la aplicación y llamar a las API.</span><span class="sxs-lookup"><span data-stu-id="31896-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="31896-116">Para una integración eficaz, debe tener una buena comprensión de los [fragmentos](#code-snippets) de código para llamar a las API de ubicación.</span><span class="sxs-lookup"><span data-stu-id="31896-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="31896-117">Es importante familiarizarse con los errores de respuesta [de la API](#error-handling) para controlar los errores de la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="31896-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="31896-118">Actualmente, Microsoft Teams compatibilidad con las funcionalidades de ubicación solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="31896-118">Currently, Microsoft Teams support for location capabilities is available for mobile clients only.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="31896-119">Manifiesto de actualización</span><span class="sxs-lookup"><span data-stu-id="31896-119">Update manifest</span></span>

<span data-ttu-id="31896-120">Actualice el Teams aplicaciónmanifest.js[el archivo](../../resources/schema/manifest-schema.md#devicepermissions) agregando la propiedad `devicePermissions` y especificando `geolocation` .</span><span class="sxs-lookup"><span data-stu-id="31896-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="31896-121">Permite a la aplicación solicitar los permisos necesarios a los usuarios antes de empezar a usar las funcionalidades de ubicación.</span><span class="sxs-lookup"><span data-stu-id="31896-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span> <span data-ttu-id="31896-122">La actualización del manifiesto de la aplicación es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="31896-122">The update for app manifest is as follows:</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="31896-123">El **símbolo del sistema Solicitar permisos** se muestra automáticamente cuando se inicia una API de Teams relevante.</span><span class="sxs-lookup"><span data-stu-id="31896-123">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="31896-124">Para obtener más información, consulta [solicitar permisos de dispositivo](native-device-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="31896-124">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="31896-125">API de ubicación</span><span class="sxs-lookup"><span data-stu-id="31896-125">Location APIs</span></span>

<span data-ttu-id="31896-126">Debes usar el siguiente conjunto de API para habilitar las capacidades de ubicación del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="31896-126">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="31896-127">API</span><span class="sxs-lookup"><span data-stu-id="31896-127">API</span></span>      | <span data-ttu-id="31896-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="31896-128">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="31896-129">getLocation</span><span class="sxs-lookup"><span data-stu-id="31896-129">getLocation</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | <span data-ttu-id="31896-130">Proporciona la ubicación del dispositivo actual del usuario o abre el selector de ubicación nativa y devuelve la ubicación elegida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="31896-130">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="31896-131">showLocation</span><span class="sxs-lookup"><span data-stu-id="31896-131">showLocation</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) | <span data-ttu-id="31896-132">Muestra la ubicación en el mapa.</span><span class="sxs-lookup"><span data-stu-id="31896-132">Shows location on map.</span></span> |

> [!NOTE]
> <span data-ttu-id="31896-133">La `getLocation()` API incluye las siguientes [configuraciones de entrada](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)y `allowChooseLocation` `showMap` .</span><span class="sxs-lookup"><span data-stu-id="31896-133">The `getLocation()` API comes along with following [input configurations](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="31896-134">Si el valor de `allowChooseLocation` es *true*, los usuarios pueden elegir cualquier ubicación de su elección.</span><span class="sxs-lookup"><span data-stu-id="31896-134">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="31896-135">Si el valor es *false*, los usuarios no pueden cambiar su ubicación actual.</span><span class="sxs-lookup"><span data-stu-id="31896-135">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="31896-136">Si el valor de `showMap` es *false*, se captura la ubicación actual sin mostrar el mapa.</span><span class="sxs-lookup"><span data-stu-id="31896-136">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="31896-137">`showMap` se omite si `allowChooseLocation` se establece en *true*.</span><span class="sxs-lookup"><span data-stu-id="31896-137">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span>

<span data-ttu-id="31896-138">En la siguiente imagen se muestra la experiencia de la aplicación web de las funcionalidades de ubicación:</span><span class="sxs-lookup"><span data-stu-id="31896-138">The following image depicts web app experience of location capabilities:</span></span>

![experiencia de la aplicación web para funcionalidades de ubicación](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a><span data-ttu-id="31896-140">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="31896-140">Code snippets</span></span>

<span data-ttu-id="31896-141">**Llamar `getLocation` a la API para recuperar la ubicación:**</span><span class="sxs-lookup"><span data-stu-id="31896-141">**Calling `getLocation` API to retrieve the location:**</span></span>

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

<span data-ttu-id="31896-142">**Llamar `showLocation` a la API para mostrar la ubicación:**</span><span class="sxs-lookup"><span data-stu-id="31896-142">**Calling `showLocation` API to display the location:**</span></span>

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

## <a name="error-handling"></a><span data-ttu-id="31896-143">Control de errores</span><span class="sxs-lookup"><span data-stu-id="31896-143">Error handling</span></span>

<span data-ttu-id="31896-144">Debes asegurarte de controlar estos errores correctamente en tu Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="31896-144">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="31896-145">En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores:</span><span class="sxs-lookup"><span data-stu-id="31896-145">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="31896-146">Código de error</span><span class="sxs-lookup"><span data-stu-id="31896-146">Error code</span></span> |  <span data-ttu-id="31896-147">Nombre del error</span><span class="sxs-lookup"><span data-stu-id="31896-147">Error name</span></span>     | <span data-ttu-id="31896-148">Condition</span><span class="sxs-lookup"><span data-stu-id="31896-148">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="31896-149">**100**</span><span class="sxs-lookup"><span data-stu-id="31896-149">**100**</span></span> | <span data-ttu-id="31896-150">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="31896-150">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="31896-151">La API no se admite en la plataforma actual.</span><span class="sxs-lookup"><span data-stu-id="31896-151">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="31896-152">**500**</span><span class="sxs-lookup"><span data-stu-id="31896-152">**500**</span></span> | <span data-ttu-id="31896-153">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="31896-153">INTERNAL_ERROR</span></span> | <span data-ttu-id="31896-154">Se produce un error interno al realizar la operación necesaria.</span><span class="sxs-lookup"><span data-stu-id="31896-154">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="31896-155">**1000**</span><span class="sxs-lookup"><span data-stu-id="31896-155">**1000**</span></span> | <span data-ttu-id="31896-156">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="31896-156">PERMISSION_DENIED</span></span> |<span data-ttu-id="31896-157">El usuario ha denegado los permisos de ubicación Teams app o web-app .</span><span class="sxs-lookup"><span data-stu-id="31896-157">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="31896-158">**4000**</span><span class="sxs-lookup"><span data-stu-id="31896-158">**4000**</span></span> | <span data-ttu-id="31896-159">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="31896-159">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="31896-160">La API se invoca con argumentos obligatorios incorrectos o insuficientes.</span><span class="sxs-lookup"><span data-stu-id="31896-160">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="31896-161">**8000**</span><span class="sxs-lookup"><span data-stu-id="31896-161">**8000**</span></span> | <span data-ttu-id="31896-162">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="31896-162">USER_ABORT</span></span> |<span data-ttu-id="31896-163">El usuario canceló la operación.</span><span class="sxs-lookup"><span data-stu-id="31896-163">User cancelled the operation.</span></span>|
| <span data-ttu-id="31896-164">**9000**</span><span class="sxs-lookup"><span data-stu-id="31896-164">**9000**</span></span> | <span data-ttu-id="31896-165">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="31896-165">OLD_PLATFORM</span></span> | <span data-ttu-id="31896-166">El usuario se encuentra en una compilación de plataforma antigua donde la implementación de la API no está presente.</span><span class="sxs-lookup"><span data-stu-id="31896-166">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="31896-167">La actualización de la compilación debe resolver el problema.</span><span class="sxs-lookup"><span data-stu-id="31896-167">Upgrading the build should resolve the issue.</span></span>|

## <a name="see-also"></a><span data-ttu-id="31896-168">Consulte también</span><span class="sxs-lookup"><span data-stu-id="31896-168">See also</span></span>

* [<span data-ttu-id="31896-169">Integrar funcionalidades multimedia en Teams</span><span class="sxs-lookup"><span data-stu-id="31896-169">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="31896-170">Integrar la funcionalidad de escáner de código QR o código de barras en Teams</span><span class="sxs-lookup"><span data-stu-id="31896-170">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="31896-171">Integrar la funcionalidad selector de personas en Teams</span><span class="sxs-lookup"><span data-stu-id="31896-171">Integrate People Picker capability in Teams</span></span>](people-picker-capability.md)
