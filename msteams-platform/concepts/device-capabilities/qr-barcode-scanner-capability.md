---
title: Integrar la función de escáner de código QR o de códigos de barras
author: Rajeshwari-v
description: Cómo usar Teams SDK de cliente de JavaScript para aprovechar la funcionalidad del escáner de códigos de barras o QR
keywords: Cámara media qr code qrcode bar code barcode scanner scan capabilities native device permissions
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 2bd5c5c1cfaab4e2f03423f078c04b133331de1a
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630533"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a><span data-ttu-id="03d2f-104">Integrar la función de escáner de código QR o de códigos de barras</span><span class="sxs-lookup"><span data-stu-id="03d2f-104">Integrate QR or barcode scanner capability</span></span> 

<span data-ttu-id="03d2f-105">Este documento le guía sobre cómo integrar la funcionalidad del escáner de códigos QR o de código de barras.</span><span class="sxs-lookup"><span data-stu-id="03d2f-105">This document guides you on how to integrate the QR or barcode scanner capability.</span></span> 

<span data-ttu-id="03d2f-106">El código de barras es un método para representar datos en un formulario visual y legible por máquina.</span><span class="sxs-lookup"><span data-stu-id="03d2f-106">Barcode is a method of representing data in a visual and machine-readable form.</span></span> <span data-ttu-id="03d2f-107">El código de barras contiene información sobre un producto, como un tipo, tamaño, fabricante y país de origen en forma de barras y espacios.</span><span class="sxs-lookup"><span data-stu-id="03d2f-107">The barcode contains information about a product, such as a type, size, manufacturer, and Country of origin in the form of bars and spaces.</span></span> <span data-ttu-id="03d2f-108">El código se lee con el escáner óptico de la cámara del dispositivo nativo.</span><span class="sxs-lookup"><span data-stu-id="03d2f-108">The code is read using the optical scanner on your native device camera.</span></span> <span data-ttu-id="03d2f-109">Para una experiencia de colaboración más completa, puedes integrar la funcionalidad de escáner de códigos QR o códigos de barras que se proporciona en la plataforma Teams con la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="03d2f-109">For a richer collaborative experience, you can integrate the QR or barcode scanner capability provided in the Teams platform with your Teams app.</span></span>   

<span data-ttu-id="03d2f-110">Puedes usar Microsoft Teams [SDK de cliente de JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)que proporciona las herramientas necesarias para que la aplicación pueda tener acceso a las capacidades del dispositivo nativo del [usuario.](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="03d2f-110">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="03d2f-111">Usa la `scanBarCode` API para integrar la funcionalidad del escáner dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03d2f-111">Use the `scanBarCode` API to integrate the scanner capability within your app.</span></span> 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a><span data-ttu-id="03d2f-112">Ventaja de integrar la funcionalidad de escáner de códigos DE BARRAS o QR</span><span class="sxs-lookup"><span data-stu-id="03d2f-112">Advantage of integrating QR or barcode scanner capability</span></span>

<span data-ttu-id="03d2f-113">Estas son las ventajas de la integración de las capacidades de escáner de códigos QR o de código de barras:</span><span class="sxs-lookup"><span data-stu-id="03d2f-113">Following are the advantages of integration of QR or barcode scanner capabilities:</span></span> 

* <span data-ttu-id="03d2f-114">La integración permite a los desarrolladores de aplicaciones web en Teams para aprovechar la funcionalidad de análisis de CÓDIGOS QR o códigos de barras con Teams SDK de cliente de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="03d2f-114">The integration allows web app developers on Teams platform to leverage QR or barcode scanning functionality with Teams JavaScript client SDK.</span></span>
* <span data-ttu-id="03d2f-115">Con esta característica, el usuario solo necesita alinear un QR o un código de barras dentro de un marco en el centro de la interfaz de usuario del escáner y el código se examina automáticamente.</span><span class="sxs-lookup"><span data-stu-id="03d2f-115">With this feature, the user only needs to align a QR or barcode within a frame at the center of the scanner UI and the code gets scanned automatically.</span></span> <span data-ttu-id="03d2f-116">Los datos almacenados se comparten de nuevo con la aplicación web de llamada.</span><span class="sxs-lookup"><span data-stu-id="03d2f-116">The stored data is shared back with the calling web app.</span></span> <span data-ttu-id="03d2f-117">Esto evita los inconvenientes y errores humanos de introducir códigos de producto largos u otra información relevante manualmente.</span><span class="sxs-lookup"><span data-stu-id="03d2f-117">This avoids the inconvenience and human-errors of entering lengthy product codes or other relevant information manually.</span></span>

<span data-ttu-id="03d2f-118">Para integrar la funcionalidad de escáner qr o de código de barras, debes actualizar el archivo de manifiesto de la aplicación y llamar a la `scanBarCode` API.</span><span class="sxs-lookup"><span data-stu-id="03d2f-118">To integrate QR or barcode scanner capability, you must update the app manifest file and call the `scanBarCode` API.</span></span> <span data-ttu-id="03d2f-119">Para una integración eficaz, debe [](#code-snippet) tener una buena comprensión del fragmento de código para llamar a la API, lo que le permite usar la funcionalidad nativa de escáner de códigos de barras o `scanBarCode` QR.</span><span class="sxs-lookup"><span data-stu-id="03d2f-119">For effective integration, you must have a good understanding of [code snippet](#code-snippet) for calling the `scanBarCode` API, which allows you to use native QR or barcode scanner capability.</span></span> <span data-ttu-id="03d2f-120">La API proporciona un error para un estándar de código de barras no compatible.</span><span class="sxs-lookup"><span data-stu-id="03d2f-120">The API gives an error for an unsupported barcode standard.</span></span>
<span data-ttu-id="03d2f-121">Es importante familiarizarse con los errores de respuesta [de la API](#error-handling) para controlar los errores de la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="03d2f-121">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="03d2f-122">Actualmente, Microsoft Teams compatibilidad con la funcionalidad de escáner de códigos de barras o QR solo está disponible para clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="03d2f-122">Currently, Microsoft Teams support for QR or barcode scanner capability is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="03d2f-123">Manifiesto de actualización</span><span class="sxs-lookup"><span data-stu-id="03d2f-123">Update manifest</span></span>

<span data-ttu-id="03d2f-124">Actualice el Teams aplicaciónmanifest.js[el archivo](../../resources/schema/manifest-schema.md#devicepermissions) agregando la propiedad `devicePermissions` y especificando `media` .</span><span class="sxs-lookup"><span data-stu-id="03d2f-124">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="03d2f-125">Permite que la aplicación solicite los permisos necesarios a los usuarios antes de empezar a usar la funcionalidad del escáner de códigos de barras o QR.</span><span class="sxs-lookup"><span data-stu-id="03d2f-125">It allows your app to ask for requisite permissions from users before they start using  the QR or barcode scanner capability.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="03d2f-126">El **símbolo del sistema Solicitar permisos** se muestra automáticamente cuando se inicia una API de Teams relevante.</span><span class="sxs-lookup"><span data-stu-id="03d2f-126">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="03d2f-127">Para obtener más información, consulta [Solicitar permisos de dispositivo](native-device-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="03d2f-127">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="scanbarcode-api"></a><span data-ttu-id="03d2f-128">ScanBarCode API</span><span class="sxs-lookup"><span data-stu-id="03d2f-128">ScanBarCode API</span></span>

<span data-ttu-id="03d2f-129">La API invoca el control de escáner que permite al usuario examinar diferentes tipos de código de barras `ScanBarCode` y devuelve el resultado como una cadena.</span><span class="sxs-lookup"><span data-stu-id="03d2f-129">The `ScanBarCode` API invokes scanner control that enables the user to scan different types of barcode, and returns the result as a string.</span></span>

<span data-ttu-id="03d2f-130">Para personalizar la experiencia de análisis de código de barras, la configuración de código de barras opcional se pasa como entrada a la `ScanBarCode` API.</span><span class="sxs-lookup"><span data-stu-id="03d2f-130">To customize the barcode scanning experience, optional barcode configuration is passed as input to `ScanBarCode` API.</span></span> <span data-ttu-id="03d2f-131">Puede especificar el intervalo de tiempo de espera del examen en segundos mediante `timeOutIntervalInSec` .</span><span class="sxs-lookup"><span data-stu-id="03d2f-131">You can specify the scan time-out interval in seconds using `timeOutIntervalInSec`.</span></span> <span data-ttu-id="03d2f-132">Su valor predeterminado es 30 segundos y el valor máximo es 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="03d2f-132">Its default value is 30 seconds and the maximum value is 60 seconds.</span></span>

<span data-ttu-id="03d2f-133">La **API scanBarCode()** admite los siguientes tipos de código de barras:</span><span class="sxs-lookup"><span data-stu-id="03d2f-133">The **scanBarCode()** API supports the following barcode types:</span></span>

| <span data-ttu-id="03d2f-134">Tipo de código de barras</span><span class="sxs-lookup"><span data-stu-id="03d2f-134">Barcode Type</span></span> | <span data-ttu-id="03d2f-135">Compatible con Android</span><span class="sxs-lookup"><span data-stu-id="03d2f-135">Supported on Android</span></span> | <span data-ttu-id="03d2f-136">Compatible con iOS</span><span class="sxs-lookup"><span data-stu-id="03d2f-136">Supported on iOS</span></span> |
| ---------- | ---------- | ------------ |
| <span data-ttu-id="03d2f-137">Barra de código</span><span class="sxs-lookup"><span data-stu-id="03d2f-137">Codebar</span></span> | <span data-ttu-id="03d2f-138">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-138">Yes</span></span> | <span data-ttu-id="03d2f-139">No</span><span class="sxs-lookup"><span data-stu-id="03d2f-139">No</span></span> |
| <span data-ttu-id="03d2f-140">Código 39</span><span class="sxs-lookup"><span data-stu-id="03d2f-140">Code 39</span></span> | <span data-ttu-id="03d2f-141">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-141">Yes</span></span> | <span data-ttu-id="03d2f-142">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-142">Yes</span></span> | 
| <span data-ttu-id="03d2f-143">Código 93</span><span class="sxs-lookup"><span data-stu-id="03d2f-143">Code 93</span></span> | <span data-ttu-id="03d2f-144">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-144">Yes</span></span> | <span data-ttu-id="03d2f-145">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-145">Yes</span></span> |
| <span data-ttu-id="03d2f-146">Código 128</span><span class="sxs-lookup"><span data-stu-id="03d2f-146">Code 128</span></span> | <span data-ttu-id="03d2f-147">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-147">Yes</span></span> | <span data-ttu-id="03d2f-148">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-148">Yes</span></span> |
| <span data-ttu-id="03d2f-149">EAN-13</span><span class="sxs-lookup"><span data-stu-id="03d2f-149">EAN-13</span></span> | <span data-ttu-id="03d2f-150">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-150">Yes</span></span> | <span data-ttu-id="03d2f-151">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-151">Yes</span></span> |
| <span data-ttu-id="03d2f-152">EAN-8</span><span class="sxs-lookup"><span data-stu-id="03d2f-152">EAN-8</span></span> | <span data-ttu-id="03d2f-153">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-153">Yes</span></span> | <span data-ttu-id="03d2f-154">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-154">Yes</span></span> |
| <span data-ttu-id="03d2f-155">ITF</span><span class="sxs-lookup"><span data-stu-id="03d2f-155">ITF</span></span> | <span data-ttu-id="03d2f-156">No</span><span class="sxs-lookup"><span data-stu-id="03d2f-156">No</span></span> | <span data-ttu-id="03d2f-157">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-157">Yes</span></span> |
| <span data-ttu-id="03d2f-158">Código QR</span><span class="sxs-lookup"><span data-stu-id="03d2f-158">QR Code</span></span> | <span data-ttu-id="03d2f-159">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-159">Yes</span></span> | <span data-ttu-id="03d2f-160">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-160">Yes</span></span> |
| <span data-ttu-id="03d2f-161">RSS expandido</span><span class="sxs-lookup"><span data-stu-id="03d2f-161">RSS Expanded</span></span> | <span data-ttu-id="03d2f-162">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-162">Yes</span></span> | <span data-ttu-id="03d2f-163">No</span><span class="sxs-lookup"><span data-stu-id="03d2f-163">No</span></span> |
| <span data-ttu-id="03d2f-164">RSS-14</span><span class="sxs-lookup"><span data-stu-id="03d2f-164">RSS-14</span></span> | <span data-ttu-id="03d2f-165">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-165">Yes</span></span> | <span data-ttu-id="03d2f-166">No</span><span class="sxs-lookup"><span data-stu-id="03d2f-166">No</span></span> |
| <span data-ttu-id="03d2f-167">UPC-A</span><span class="sxs-lookup"><span data-stu-id="03d2f-167">UPC-A</span></span> | <span data-ttu-id="03d2f-168">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-168">Yes</span></span> | <span data-ttu-id="03d2f-169">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-169">Yes</span></span> |
| <span data-ttu-id="03d2f-170">UPC-E</span><span class="sxs-lookup"><span data-stu-id="03d2f-170">UPC-E</span></span> | <span data-ttu-id="03d2f-171">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-171">Yes</span></span> | <span data-ttu-id="03d2f-172">Sí</span><span class="sxs-lookup"><span data-stu-id="03d2f-172">Yes</span></span> |

<span data-ttu-id="03d2f-173">**Experiencia de aplicación web para `ScanBarCode` Api para la experiencia de aplicación** web de funcionalidad de escáner de códigos de barras o QR para la funcionalidad de escáner de códigos de barras o 
 ![ qr](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span><span class="sxs-lookup"><span data-stu-id="03d2f-173">**Web app experience for `ScanBarCode` API for QR or barcode scanner capability**
![web app experience for qr or barcode scanner capability](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="03d2f-174">Control de errores</span><span class="sxs-lookup"><span data-stu-id="03d2f-174">Error handling</span></span>

<span data-ttu-id="03d2f-175">Debes asegurarte de controlar estos errores correctamente en tu Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="03d2f-175">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="03d2f-176">En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores:</span><span class="sxs-lookup"><span data-stu-id="03d2f-176">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="03d2f-177">Código de error</span><span class="sxs-lookup"><span data-stu-id="03d2f-177">Error code</span></span> |  <span data-ttu-id="03d2f-178">Nombre del error</span><span class="sxs-lookup"><span data-stu-id="03d2f-178">Error name</span></span>     | <span data-ttu-id="03d2f-179">Condición</span><span class="sxs-lookup"><span data-stu-id="03d2f-179">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="03d2f-180">**100**</span><span class="sxs-lookup"><span data-stu-id="03d2f-180">**100**</span></span> | <span data-ttu-id="03d2f-181">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="03d2f-181">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="03d2f-182">La API no se admite en la plataforma actual.</span><span class="sxs-lookup"><span data-stu-id="03d2f-182">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="03d2f-183">**500**</span><span class="sxs-lookup"><span data-stu-id="03d2f-183">**500**</span></span> | <span data-ttu-id="03d2f-184">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="03d2f-184">INTERNAL_ERROR</span></span> | <span data-ttu-id="03d2f-185">Se produce un error interno al realizar la operación necesaria.</span><span class="sxs-lookup"><span data-stu-id="03d2f-185">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="03d2f-186">**1000**</span><span class="sxs-lookup"><span data-stu-id="03d2f-186">**1000**</span></span> | <span data-ttu-id="03d2f-187">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="03d2f-187">PERMISSION_DENIED</span></span> |<span data-ttu-id="03d2f-188">El usuario deniega el permiso.</span><span class="sxs-lookup"><span data-stu-id="03d2f-188">Permission is denied by the user.</span></span>|
| <span data-ttu-id="03d2f-189">**3000**</span><span class="sxs-lookup"><span data-stu-id="03d2f-189">**3000**</span></span> | <span data-ttu-id="03d2f-190">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="03d2f-190">NO_HW_SUPPORT</span></span> | <span data-ttu-id="03d2f-191">El hardware subyacente no admite la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="03d2f-191">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="03d2f-192">**4000**</span><span class="sxs-lookup"><span data-stu-id="03d2f-192">**4000**</span></span> | <span data-ttu-id="03d2f-193">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="03d2f-193">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="03d2f-194">Uno o más argumentos no son válidos.</span><span class="sxs-lookup"><span data-stu-id="03d2f-194">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="03d2f-195">**8000**</span><span class="sxs-lookup"><span data-stu-id="03d2f-195">**8000**</span></span> | <span data-ttu-id="03d2f-196">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="03d2f-196">USER_ABORT</span></span> |<span data-ttu-id="03d2f-197">El usuario anula la operación.</span><span class="sxs-lookup"><span data-stu-id="03d2f-197">User aborts the operation.</span></span>|
| <span data-ttu-id="03d2f-198">**8001**</span><span class="sxs-lookup"><span data-stu-id="03d2f-198">**8001**</span></span> | <span data-ttu-id="03d2f-199">OPERATION_TIMED_OUT</span><span class="sxs-lookup"><span data-stu-id="03d2f-199">OPERATION_TIMED_OUT</span></span> | <span data-ttu-id="03d2f-200">No se pudo detectar el código de barras en el intervalo de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="03d2f-200">Could not detect the barcode in the given time interval.</span></span>|
| <span data-ttu-id="03d2f-201">**9000**</span><span class="sxs-lookup"><span data-stu-id="03d2f-201">**9000**</span></span> | <span data-ttu-id="03d2f-202">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="03d2f-202">OLD_PLATFORM</span></span> | <span data-ttu-id="03d2f-203">El código de la plataforma está obsoleto y no implementa esta API.</span><span class="sxs-lookup"><span data-stu-id="03d2f-203">Platform code is outdated and does not implement this API.</span></span>|

## <a name="code-snippet"></a><span data-ttu-id="03d2f-204">Fragmento de código</span><span class="sxs-lookup"><span data-stu-id="03d2f-204">Code snippet</span></span>

<span data-ttu-id="03d2f-205">**Llamada `ScanBarCode()` API** para examinar QR o código de barras con cámara:</span><span class="sxs-lookup"><span data-stu-id="03d2f-205">**Calling `ScanBarCode()` API** for scanning QR or barcode using camera:</span></span>

```javascript
const config: microsoftTeams.media.BarCodeConfig = {
  timeOutIntervalInSec: 30};
microsoftTeams.media.scanBarCode((error: microsoftTeams.SdkError, decodedText: string) => {
  if (error) {
    if (error.message) {
      output(" ErrorCode: " + error.errorCode + error.message);
    } else {
      output(" ErrorCode: " + error.errorCode);
    }
  } else if (decodedText) {
    output(decodedText);
  }
}, config);
```

## <a name="see-also"></a><span data-ttu-id="03d2f-206">Vea también</span><span class="sxs-lookup"><span data-stu-id="03d2f-206">See also</span></span>

* [<span data-ttu-id="03d2f-207">Integrar funcionalidades multimedia en Teams</span><span class="sxs-lookup"><span data-stu-id="03d2f-207">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="03d2f-208">Integrar las capacidades de ubicación en Teams</span><span class="sxs-lookup"><span data-stu-id="03d2f-208">Integrate location capabilities in Teams</span></span>](location-capability.md)
