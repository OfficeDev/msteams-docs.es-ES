---
title: Integrar la función de escáner de código QR o de códigos de barras
author: Rajeshwari-v
description: Obtenga información sobre cómo usar Teams SDK de cliente de JavaScript para aprovechar la funcionalidad de escáner de códigos QR o códigos de barras y conocer las ventajas de integrar la funcionalidad de escáner de códigos QR o códigos de barras.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: d9dc35002398be047f4cd84d7600b3d149677bd3
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189625"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a>Integrar la función de escáner de código QR o de códigos de barras

El código de barras es un método de representación de datos en un formato visual y legible por máquina. El código de barras contiene información sobre un producto, como el tipo, tamaño, fabricante y país de origen en forma de barras y espacios. El código se lee mediante el escáner óptico de la cámara del dispositivo nativo. Para una experiencia colaborativa más enriquecida, puede integrar la funcionalidad QR o escáner del código de barras proporcionada en la plataforma de Teams con su aplicación de Teams.

Puede usar [el cliente de SDK JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), que proporciona las herramientas necesarias para que la aplicación acceda a las [funcionalidades nativas del dispositivo ](native-device-permissions.md) del usuario. Use la API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) para integrar la funcionalidad del escáner en la aplicación.

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a>Ventaja de la integración de la funcionalidad del escáner de QR o códigos de barras

A continuación se muestran las ventajas de la integración de las funcionalidades del escáner de QR o código de barras:

* La integración permite a los desarrolladores de aplicaciones web en la plataforma de Teams aprovechar la funcionalidad de escaneo de códigos QR o códigos de barras con el SDK de cliente de Teams JavaScript.
* Con esta característica, el usuario solo necesita alinear un QR o un código de barras dentro de un marco en el centro de la interfaz de usuario del escáner y el código se examina automáticamente. Los datos almacenados se comparten con la aplicación web que realiza la llamada. Esto evita los inconvenientes y errores humanos de escribir códigos de producto largos u otra información relevante manualmente.

Para integrar la funcionalidad QR o de escáner de códigos de barras, debe actualizar el archivo de manifiesto de la aplicación y llamar a la API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_). Para una integración eficaz, debe tener una buena comprensión del [fragmento de código](#code-snippet) para llamar a la API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_), lo que le permite usar la funcionalidad nativa de escáner de QR o códigos de barras. La API proporciona un error para un estándar de código de barras no compatible.
Es importante familiarizarse con los [errores de respuesta de la API](#error-handling) para controlar los errores en la aplicación de Teams.

> [!NOTE]
> Actualmente, la compatibilidad de Microsoft Teams con la funcionalidad de escáner QR o códigos de barras solo está disponible para clientes móviles.

## <a name="update-manifest"></a>Actualizar manifiesto

Actualice el archivo [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) de la aplicación Teams agregando la `devicePermissions` propiedad y especificando `media`. Permite que la aplicación solicite los permisos necesarios a los usuarios antes de que empiecen a usar la funcionalidad de escáner de QR o códigos de barras. La actualización del manifiesto de la aplicación es la siguiente:

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> El permiso de **solicitud de permisos** se muestra automáticamente cuando se inicia una API de Teams relevante. Para obtener más información, consulte [Solicitar permisos de dispositivo](native-device-permissions.md).

## <a name="scanbarcode-api"></a>ScanBarCode API

La API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) invoca el control de escáner que permite al usuario examinar diferentes tipos de código de barras y devuelve el resultado como una cadena.

Para personalizar la experiencia de escaneo de códigos de barras, se pasa la [configuración de código de barras](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) opcional como entrada a la API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_). Puede especificar el intervalo de tiempo de espera de examen en segundos mediante `timeOutIntervalInSec`. Su valor predeterminado es 30 segundos y el valor máximo es de 60 segundos.

La API **scanBarCode()** admite los siguientes tipos de código de barras:

| Tipo de código de barras | Compatible con Android | Compatible con iOS |
| ---------- | ---------- | ------------ |
| Barra de código | Sí | No |
| Código 39 | Sí | Sí |
| Código 93 | Sí | Sí |
| Código 128 | Sí | Sí |
| EAN-13 | Sí | Sí |
| EAN-8 | Sí | Sí |
| ITF | No | Sí |
| Código QR  | Sí | Sí |
| RSS expandido | Sí | No |
| RSS-14 | Sí | No |
| UPC-A | Sí | Sí |
| UPC-E | Sí | Sí |

En la siguiente imagen se muestra la experiencia de la aplicación web con la funcionalidad de escáner QR o código de barras:

![Experiencia de aplicación web para la funcionalidad de escáner de códigos qr o códigos de barras](../../assets/images/tabs/qr-barcode-scanner-capability.png)

## <a name="error-handling"></a>Control de errores

Debe asegurarse de controlar estos errores correctamente en la aplicación de Teams. En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores:

|Código de error |  Nombre de error     | Condición|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no se admite en la plataforma actual.|
| **500** | INTERNAL_ERROR | Se produce un error interno al realizar la operación necesaria.|
| **1 000** | PERMISSION_DENIED |El usuario deniega el permiso.|
| **3000** | NO_HW_SUPPORT | El hardware subyacente no admite la funcionalidad.|
| **4000** | InvalidArguments | Uno o más argumentos no son válidos.|
| **8000** | USER_ABORT |El usuario anula la operación.|
| **8001** | OPERATION_TIMED_OUT | No se pudo detectar el código de barras en el intervalo de tiempo especificado.|
| **9000** | OLD_PLATFORM | El código de la plataforma no está actualizado y no implementa esta API.|

## <a name="code-snippet"></a>Fragmento de código

**Llamando `ScanBarCode()` API** para escanear QR o código de barras con cámara:

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

## <a name="see-also"></a>Consulte también

* [Integrar capacidades multimedia](media-capabilities.md)
* [Integrar las capacidades de ubicación en Teams](location-capability.md)
* [Integración del selector de usuarios en Teams](people-picker-capability.md)
