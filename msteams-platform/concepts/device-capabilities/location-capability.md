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
# <a name="integrate-location-capabilities"></a>Integrar capacidades de ubicación 

Este documento le guía sobre cómo integrar las capacidades de ubicación del dispositivo nativo con su aplicación Teams.  

Puede usar [Microsoft Teams SDK de cliente de JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)que proporciona las herramientas necesarias para que la aplicación acceda a las capacidades de dispositivo [nativo](native-device-permissions.md)del usuario. Use las API de ubicación, como [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) y [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) para integrar las capacidades dentro de la aplicación. 

## <a name="advantages-of-integrating-location-capabilities"></a>Ventajas de integrar capacidades de ubicación

La principal ventaja de integrar capacidades de ubicación en sus aplicaciones de Teams es que permite a los desarrolladores de aplicaciones web en Teams plataforma aprovechar la funcionalidad de ubicación con Microsoft Teams SDK de cliente JavaScript. 

En los ejemplos siguientes se muestra cómo se utiliza la integración de las capacidades de ubicación en diferentes escenarios:
* En una fábrica, el supervisor puede rastrear la asistencia de los trabajadores pidiéndoles que se hagan un selfie en las inmediaciones de la fábrica y lo compartan a través de la aplicación especificada. Los datos de ubicación también se capturan y envían junto con la imagen.
* Las capacidades de ubicación permiten al personal de mantenimiento de un proveedor de servicios compartir datos de salud auténticos de torres celulares con la administración. La administración puede comparar cualquier discrepancia entre la información de ubicación capturada y los datos enviados por el personal de mantenimiento.

Para integrar las capacidades de ubicación, debe actualizar el archivo de manifiesto de la aplicación y llamar a las API. Para una integración eficaz, debe tener una buena comprensión de [los fragmentos de código](#code-snippets) para llamar a las API de ubicación. Es importante familiarizarse con los errores de respuesta de la [API](#error-handling) para controlar los errores en la aplicación Teams.

> [!NOTE] 
> Actualmente, Microsoft Teams soporte para las capacidades de ubicación solo está disponible para clientes móviles.

## <a name="update-manifest"></a>Manifiesto de actualización

Actualice la aplicación Teams [manifest.jsen el](../../resources/schema/manifest-schema.md#devicepermissions) archivo agregando la propiedad y `devicePermissions` especificando `geolocation` . Permite a la aplicación pedir permisos necesarios a los usuarios antes de que empiecen a usar las capacidades de ubicación.

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> La solicitud **Permisos de solicitud** se muestra automáticamente cuando se inicia una API de Teams relevante. Para obtener más información, consulte [Solicitar permisos de dispositivo.](native-device-permissions.md)

## <a name="location-apis"></a>API de ubicación

Debe usar el siguiente conjunto de API para habilitar las capacidades de ubicación del dispositivo:

| API      | Descripción   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | Proporciona la ubicación actual del dispositivo del usuario o abre el selector de ubicación nativo y devuelve la ubicación elegida por el usuario. |
|[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | Muestra la ubicación en el mapa. |

> [!NOTE]

> La `getLocation()` API viene junto con las siguientes [configuraciones de entrada](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)y `allowChooseLocation` `showMap` . <br/> Si el valor de `allowChooseLocation` es *true*, los usuarios pueden elegir cualquier ubicación de su elección.<br/>  Si el valor es *false,* los usuarios no pueden cambiar su ubicación actual.<br/> Si el valor de `showMap` es *false,* la ubicación actual se recupera sin mostrar el mapa. `showMap` se omite si `allowChooseLocation` se establece en *true*.

**Experiencia en aplicaciones web para capacidades** 
 ![ de ubicación experiencia de la aplicación web para las capacidades de ubicación](../../assets/images/tabs/location-capability.png)

## <a name="error-handling"></a>Control de errores

Debe asegurarse de controlar estos errores adecuadamente en la aplicación Teams. En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores: 

|Código de error |  Nombre del error     | Condición|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no es compatible con la plataforma actual.|
| **500** | INTERNAL_ERROR | Se encuentra un error interno al realizar la operación necesaria.|
| **1000** | PERMISSION_DENIED |El usuario denegó permisos de ubicación a la aplicación Teams o a la aplicación web.|
| **4000** | INVALID_ARGUMENTS | La API se invoca con argumentos obligatorios incorrectos o insuficientes.|
| **8000** | USER_ABORT |El usuario canceló la operación.|
| **9000** | OLD_PLATFORM | El usuario está en la compilación de plataforma antigua donde la implementación de la API no está presente. La actualización de la compilación debe resolver el problema.|

## <a name="code-snippets"></a>Fragmentos de código

**Llamar `getLocation` a la API para recuperar la ubicación:**

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

**Llamar `showLocation` a la API para mostrar la ubicación:**

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

## <a name="see-also"></a>Vea también

* [Integrar capacidades de medios en Teams](mobile-camera-image-permissions.md)
* [Integrar la capacidad del escáner de código de barras o código de barras en Teams](qr-barcode-scanner-capability.md)
