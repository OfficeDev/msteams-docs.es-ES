---
title: Integrar capacidades de ubicación
author: Rajeshwari-v
description: Cómo usar Teams SDK de cliente de JavaScript para aprovechar las capacidades de ubicación
keywords: capacidades de mapa de ubicación permisos de dispositivos nativos
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: b85f19e74d0a8121dd290fc395c1018178437b3a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566190"
---
# <a name="integrate-location-capabilities"></a><span data-ttu-id="b4eb8-104">Integrar capacidades de ubicación</span><span class="sxs-lookup"><span data-stu-id="b4eb8-104">Integrate location capabilities</span></span> 

<span data-ttu-id="b4eb8-105">Este documento le guía sobre cómo integrar las capacidades de ubicación del dispositivo nativo con su aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-105">This document guides you on how to integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="b4eb8-106">Puede usar [Microsoft Teams SDK de cliente de JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)que proporciona las herramientas necesarias para que la aplicación acceda a las capacidades de dispositivo [nativo](native-device-permissions.md)del usuario.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="b4eb8-107">Use las API de ubicación, como [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) y [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) para integrar las capacidades dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) and [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="b4eb8-108">Ventajas de integrar capacidades de ubicación</span><span class="sxs-lookup"><span data-stu-id="b4eb8-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="b4eb8-109">La principal ventaja de integrar capacidades de ubicación en sus aplicaciones de Teams es que permite a los desarrolladores de aplicaciones web en Teams plataforma aprovechar la funcionalidad de ubicación con Microsoft Teams SDK de cliente JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="b4eb8-110">En los ejemplos siguientes se muestra cómo se utiliza la integración de las capacidades de ubicación en diferentes escenarios:</span><span class="sxs-lookup"><span data-stu-id="b4eb8-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="b4eb8-111">En una fábrica, el supervisor puede rastrear la asistencia de los trabajadores pidiéndoles que se hagan un selfie en las inmediaciones de la fábrica y lo compartan a través de la aplicación especificada.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="b4eb8-112">Los datos de ubicación también se capturan y envían junto con la imagen.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="b4eb8-113">Las capacidades de ubicación permiten al personal de mantenimiento de un proveedor de servicios compartir datos de salud auténticos de torres celulares con la administración.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="b4eb8-114">La administración puede comparar cualquier discrepancia entre la información de ubicación capturada y los datos enviados por el personal de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="b4eb8-115">Para integrar las capacidades de ubicación, debe actualizar el archivo de manifiesto de la aplicación y llamar a las API.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="b4eb8-116">Para una integración eficaz, debe tener una buena comprensión de [los fragmentos de código](#code-snippets) para llamar a las API de ubicación.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="b4eb8-117">Es importante familiarizarse con los errores de respuesta de la [API](#error-handling) para controlar los errores en la aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="b4eb8-118">Actualmente, Microsoft Teams soporte para las capacidades de ubicación solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-118">Currently, Microsoft Teams support for location capabilities is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="b4eb8-119">Manifiesto de actualización</span><span class="sxs-lookup"><span data-stu-id="b4eb8-119">Update manifest</span></span>

<span data-ttu-id="b4eb8-120">Actualice la aplicación Teams [manifest.jsen el](../../resources/schema/manifest-schema.md#devicepermissions) archivo agregando la propiedad y `devicePermissions` especificando `geolocation` .</span><span class="sxs-lookup"><span data-stu-id="b4eb8-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="b4eb8-121">Permite a la aplicación pedir permisos necesarios a los usuarios antes de que empiecen a usar las capacidades de ubicación.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="b4eb8-122">La solicitud **Permisos de solicitud** se muestra automáticamente cuando se inicia una API de Teams relevante.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-122">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="b4eb8-123">Para obtener más información, consulte [Solicitar permisos de dispositivo.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="b4eb8-123">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="b4eb8-124">API de ubicación</span><span class="sxs-lookup"><span data-stu-id="b4eb8-124">Location APIs</span></span>

<span data-ttu-id="b4eb8-125">Debe usar el siguiente conjunto de API para habilitar las capacidades de ubicación del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="b4eb8-125">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="b4eb8-126">API</span><span class="sxs-lookup"><span data-stu-id="b4eb8-126">API</span></span>      | <span data-ttu-id="b4eb8-127">Descripción</span><span class="sxs-lookup"><span data-stu-id="b4eb8-127">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="b4eb8-128">getLocation</span><span class="sxs-lookup"><span data-stu-id="b4eb8-128">getLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | <span data-ttu-id="b4eb8-129">Proporciona la ubicación actual del dispositivo del usuario o abre el selector de ubicación nativo y devuelve la ubicación elegida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-129">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="b4eb8-130">showLocation</span><span class="sxs-lookup"><span data-stu-id="b4eb8-130">showLocation</span></span>](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | <span data-ttu-id="b4eb8-131">Muestra la ubicación en el mapa.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-131">Shows location on map.</span></span> |

> [!NOTE]

> <span data-ttu-id="b4eb8-132">La `getLocation()` API viene junto con las siguientes [configuraciones de entrada](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)y `allowChooseLocation` `showMap` .</span><span class="sxs-lookup"><span data-stu-id="b4eb8-132">The `getLocation()` API comes along with following [input configurations](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="b4eb8-133">Si el valor de `allowChooseLocation` es *true*, los usuarios pueden elegir cualquier ubicación de su elección.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-133">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="b4eb8-134">Si el valor es *false,* los usuarios no pueden cambiar su ubicación actual.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-134">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="b4eb8-135">Si el valor de `showMap` es *false,* la ubicación actual se recupera sin mostrar el mapa.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-135">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="b4eb8-136">`showMap` se omite si `allowChooseLocation` se establece en *true*.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-136">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span>

<span data-ttu-id="b4eb8-137">**Experiencia en aplicaciones web para capacidades** 
 ![ de ubicación experiencia de la aplicación web para las capacidades de ubicación](../../assets/images/tabs/location-capability.png)</span><span class="sxs-lookup"><span data-stu-id="b4eb8-137">**Web app experience for location capabilities**
![web app experience for location capabilities](../../assets/images/tabs/location-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="b4eb8-138">Control de errores</span><span class="sxs-lookup"><span data-stu-id="b4eb8-138">Error handling</span></span>

<span data-ttu-id="b4eb8-139">Debe asegurarse de controlar estos errores adecuadamente en la aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-139">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="b4eb8-140">En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores:</span><span class="sxs-lookup"><span data-stu-id="b4eb8-140">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="b4eb8-141">Código de error</span><span class="sxs-lookup"><span data-stu-id="b4eb8-141">Error code</span></span> |  <span data-ttu-id="b4eb8-142">Nombre del error</span><span class="sxs-lookup"><span data-stu-id="b4eb8-142">Error name</span></span>     | <span data-ttu-id="b4eb8-143">Condición</span><span class="sxs-lookup"><span data-stu-id="b4eb8-143">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="b4eb8-144">**100**</span><span class="sxs-lookup"><span data-stu-id="b4eb8-144">**100**</span></span> | <span data-ttu-id="b4eb8-145">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="b4eb8-145">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="b4eb8-146">La API no es compatible con la plataforma actual.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-146">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="b4eb8-147">**500**</span><span class="sxs-lookup"><span data-stu-id="b4eb8-147">**500**</span></span> | <span data-ttu-id="b4eb8-148">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="b4eb8-148">INTERNAL_ERROR</span></span> | <span data-ttu-id="b4eb8-149">Se encuentra un error interno al realizar la operación necesaria.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-149">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="b4eb8-150">**1000**</span><span class="sxs-lookup"><span data-stu-id="b4eb8-150">**1000**</span></span> | <span data-ttu-id="b4eb8-151">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="b4eb8-151">PERMISSION_DENIED</span></span> |<span data-ttu-id="b4eb8-152">El usuario denegó permisos de ubicación a la aplicación Teams o a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-152">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="b4eb8-153">**4000**</span><span class="sxs-lookup"><span data-stu-id="b4eb8-153">**4000**</span></span> | <span data-ttu-id="b4eb8-154">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="b4eb8-154">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="b4eb8-155">La API se invoca con argumentos obligatorios incorrectos o insuficientes.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-155">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="b4eb8-156">**8000**</span><span class="sxs-lookup"><span data-stu-id="b4eb8-156">**8000**</span></span> | <span data-ttu-id="b4eb8-157">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="b4eb8-157">USER_ABORT</span></span> |<span data-ttu-id="b4eb8-158">El usuario canceló la operación.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-158">User cancelled the operation.</span></span>|
| <span data-ttu-id="b4eb8-159">**9000**</span><span class="sxs-lookup"><span data-stu-id="b4eb8-159">**9000**</span></span> | <span data-ttu-id="b4eb8-160">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="b4eb8-160">OLD_PLATFORM</span></span> | <span data-ttu-id="b4eb8-161">El usuario está en la compilación de plataforma antigua donde la implementación de la API no está presente.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-161">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="b4eb8-162">La actualización de la compilación debe resolver el problema.</span><span class="sxs-lookup"><span data-stu-id="b4eb8-162">Upgrading the build should resolve the issue.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="b4eb8-163">Fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="b4eb8-163">Code snippets</span></span>

<span data-ttu-id="b4eb8-164">**Llamar `getLocation` a la API para recuperar la ubicación:**</span><span class="sxs-lookup"><span data-stu-id="b4eb8-164">**Calling `getLocation` API to retrieve the location:**</span></span>

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

<span data-ttu-id="b4eb8-165">**Llamar `showLocation` a la API para mostrar la ubicación:**</span><span class="sxs-lookup"><span data-stu-id="b4eb8-165">**Calling `showLocation` API to display the location:**</span></span>

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

## <a name="see-also"></a><span data-ttu-id="b4eb8-166">Vea también</span><span class="sxs-lookup"><span data-stu-id="b4eb8-166">See also</span></span>

* [<span data-ttu-id="b4eb8-167">Integrar capacidades de medios en Teams</span><span class="sxs-lookup"><span data-stu-id="b4eb8-167">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="b4eb8-168">Integrar la capacidad del escáner de código de barras o código de barras en Teams</span><span class="sxs-lookup"><span data-stu-id="b4eb8-168">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
