---
title: Integrar capacidades de ubicación
author: Rajeshwari-v
description: Aprenda a usar SDK para cliente de JavaScript en Teams para aprovechar las funcionalidades de ubicación mediante fragmentos de código y ejemplos
keywords: permisos de dispositivos nativos de las funcionalidades de mapa de ubicación
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: cea6ab31f816f41a191a93620c5b91f0b7ba56a2
ms.sourcegitcommit: 6f1bd36b1071e256bdc14e6ccb31dfdda9ca6d6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/13/2022
ms.locfileid: "66049000"
---
# <a name="integrate-location-capabilities"></a>Integrar capacidades de ubicación

Puede integrar las funcionalidades de ubicación del dispositivo nativo con la aplicación de Teams.  

Puede usar [el cliente de SDK JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), que proporciona las herramientas necesarias para que la aplicación acceda a las [funcionalidades nativas del dispositivo ](native-device-permissions.md) del usuario. Use las API de ubicación, como [getLocation](/javascript/api/@microsoft/teams-js/location.locationprops) y [showLocation](/javascript/api/@microsoft/teams-js/location.locationprops?), para integrar las funcionalidades dentro de la aplicación.

## <a name="advantages-of-integrating-location-capabilities"></a>Ventajas de la integración de funcionalidades de ubicación

La principal ventaja de integrar las funcionalidades de ubicación en las aplicaciones de Teams es que permite que los desarrolladores de aplicaciones web en la plataforma de Teams aprovechen la funcionalidad del cliente de SDK JavaScript de Microsoft Teams.

En los ejemplos siguientes se muestra cómo se usa la integración de las funcionalidades de ubicación en diferentes escenarios:

* En una fábrica, el supervisor puede realizar un seguimiento de la asistencia de los trabajadores pidiéndoles que se hagan una Selfie en las proximidades de la fábrica y la compartan a través de la aplicación especificada. Los datos de ubicación también se capturan y envían junto con la imagen.
* Las capacidades de ubicación permiten al personal de mantenimiento de un proveedor de servicios compartir datos médicos auténticos de las torres de telefonía móvil con la administración. La administración puede comparar cualquier discrepancia entre la información de ubicación capturada y los datos enviados por el personal de mantenimiento.

Para integrar las funcionalidades de ubicación, debe actualizar el archivo de manifiesto de la aplicación y llamar a las API. Para una integración eficaz, debe comprender bien [los fragmentos de código](#code-snippets) para llamar a las API de ubicación.
Es importante familiarizarse con los [errores de respuesta de la API](#error-handling) para controlar los errores en la aplicación de Teams.

> [!NOTE]
> Actualmente, Microsoft Teams admite capacidades de ubicación solo para clientes móviles.

## <a name="update-manifest"></a>Actualizar manifiesto

Actualice el archivo [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) de la aplicación Teams agregando la `devicePermissions` propiedad y especificando `geolocation`. Permite a la aplicación solicitar permisos necesarios a los usuarios antes de empezar a usar las funcionalidades de ubicación. La actualización del manifiesto de la aplicación es la siguiente:

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
>
> * El permiso de **solicitud de permisos** se muestra automáticamente cuando se inicia una API de Teams relevante. Para obtener más información, consulte [solicitar permisos de dispositivo](native-device-permissions.md).
> * Los permisos de dispositivo son diferentes en el explorador. Para obtener más información, vea [Permisos de dispositivo en el navegador](browser-device-permissions.md).

## <a name="location-apis"></a>API de ubicación

Debe usar el siguiente conjunto de API para habilitar las funcionalidades de ubicación del dispositivo:

| API      | Descripción   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/location.locationprops) | Proporciona la ubicación del dispositivo actual del usuario o abre el selector de ubicación nativa y devuelve la ubicación elegida por el usuario. |
|[showLocation](/javascript/api/@microsoft/teams-js/location.locationprops?) | Muestra la ubicación en el mapa. |

> [!NOTE]
> La API `getLocation()` incluye las siguientes [configuraciones de entrada](/javascript/api/@microsoft/teams-js/microsoftteams.location.locationprops), `allowChooseLocation` y `showMap`. <br/> Si el valor de `allowChooseLocation` es *true*, los usuarios pueden elegir cualquier ubicación de su elección.<br/>  Si el valor es *false*, los usuarios no pueden cambiar su ubicación actual.<br/> Si el valor de `showMap` es *false*, la ubicación actual se captura sin mostrar el mapa. `showMap` se omite si `allowChooseLocation` se establece como *true*.

En la imagen siguiente se muestra la experiencia de la aplicación web de las funcionalidades de ubicación:

![Experiencia de aplicación web para las funcionalidades de ubicación](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a>Fragmentos de código

**Llamada a `getLocation` la API para recuperar la ubicación:**

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

**Llamada a `showLocation` la API para mostrar la ubicación:**

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

## <a name="error-handling"></a>Control de errores

Debe asegurarse de controlar estos errores correctamente en la aplicación de Teams. En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores:

|Código de error |  Nombre de error     | Condición|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no se admite en la plataforma actual.|
| **500** | INTERNAL_ERROR | Se produce un error interno al realizar la operación necesaria.|
| **1 000** | PERMISSION_DENIED |El usuario denegó los permisos de ubicación para la aplicación de Teams o la aplicación web.|
| **4000** | InvalidArguments | La API se invoca con argumentos obligatorios incorrectos o insuficientes.|
| **8000** | USER_ABORT |El usuario canceló la operación.|
| **9000** | OLD_PLATFORM | El usuario se encuentra en una versión de plataforma antigua donde la implementación de la API no está disponible. La actualización de la versión debería resolver el problema.|

### <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Comprobación de la ubicación actual de la aplicación | Los usuarios pueden comprobar la ubicación actual y ver todas las comprobaciones de ubicación anteriores.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/csharp) | [Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/nodejs) |

## <a name="see-also"></a>Consulte también

* [Integrar funcionalidades multimedia en Teams](mobile-camera-image-permissions.md)
* [Integrar la funcionalidad de escáner de código QR o código de barras en Teams](qr-barcode-scanner-capability.md)
* [Integración del selector de usuarios en Teams](people-picker-capability.md)
