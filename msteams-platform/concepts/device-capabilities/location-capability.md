---
title: Integrar capacidades de ubicación
author: Rajeshwari-v
description: Cómo usar el SDK de cliente de JavaScript de Teams para aprovechar las capacidades de ubicación
keywords: capacidades de mapa de ubicación permisos de dispositivo nativos
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 98d37c4f34f638f129c07b012d98ec54c7c8e44f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019863"
---
# <a name="integrate-location-capabilities"></a>Integrar capacidades de ubicación 

Este documento te guía sobre cómo integrar las capacidades de ubicación del dispositivo nativo con la aplicación de Teams.  

Puedes usar el SDK de cliente javaScript de [Microsoft Teams,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)que proporciona las herramientas necesarias para que la aplicación pueda acceder a las capacidades nativas del dispositivo del [usuario.](native-device-permissions.md) Usa las API de ubicación, como [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) y [showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) para integrar las funcionalidades dentro de la aplicación. 

## <a name="advantages-of-integrating-location-capabilities"></a>Ventajas de integrar las capacidades de ubicación

La principal ventaja de integrar las capacidades de ubicación en las aplicaciones de Teams es que permite a los desarrolladores de aplicaciones web en la plataforma Teams aprovechar la funcionalidad de ubicación con el SDK de cliente javaScript de Microsoft Teams. 

Los ejemplos siguientes muestran cómo se usa la integración de las capacidades de ubicación en diferentes escenarios:
* En una fábrica, el supervisor puede realizar un seguimiento de la asistencia de los trabajadores pidiéndoles que se tomen un selfi en las proximidades de la fábrica y la compartan a través de la aplicación especificada. Los datos de ubicación también se capturan y envían junto con la imagen.
* Las capacidades de ubicación permiten al personal de mantenimiento de un proveedor de servicios compartir los datos de estado auténticos de las torres de telefonía móvil con la administración. La administración puede comparar cualquier discrepancia entre la información de ubicación capturada y los datos enviados por el personal de mantenimiento.

Para integrar las funcionalidades de ubicación, debes actualizar el archivo de manifiesto de la aplicación y llamar a las API. Para una integración eficaz, debe tener una buena comprensión de los [fragmentos](#code-snippets) de código para llamar a las API de ubicación. Es importante familiarizarse con los errores de respuesta [de la API](#error-handling) para controlar los errores de la aplicación de Teams.

> [!NOTE] 
> Actualmente, la compatibilidad de Microsoft Teams con las capacidades de ubicación solo está disponible para clientes móviles.

## <a name="update-manifest"></a>Manifiesto de actualización

Actualice la aplicación de Teams [manifest.jsarchivo](../../resources/schema/manifest-schema.md#devicepermissions) agregando la propiedad `devicePermissions` y especificando `geolocation` . Permite a la aplicación solicitar los permisos necesarios a los usuarios antes de empezar a usar las funcionalidades de ubicación.

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> El **símbolo del sistema Solicitar permisos** se muestra automáticamente cuando se inicia una API de Teams relevante. Para obtener más información, consulta [solicitar permisos de dispositivo](native-device-permissions.md).

## <a name="location-apis"></a>API de ubicación

Debes usar el siguiente conjunto de API para habilitar las capacidades de ubicación del dispositivo:

| API      | Descripción   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | Proporciona la ubicación del dispositivo actual del usuario o abre el selector de ubicación nativa y devuelve la ubicación elegida por el usuario. |
|[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation&preserve-view=true) | Muestra la ubicación en el mapa |

> [!NOTE]

> La `getLocation()` API incluye las siguientes [configuraciones de entrada](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)y `allowChooseLocation` `showMap` . <br/> Si el valor de `allowChooseLocation` es *true*, los usuarios pueden elegir cualquier ubicación de su elección.<br/>  Si el valor es *false*, los usuarios no pueden cambiar su ubicación actual.<br/> Si el valor de `showMap` es *false*, se captura la ubicación actual sin mostrar el mapa. `showMap` se omite si `allowChooseLocation` se establece en *true*. 


**Experiencia de aplicación web para funcionalidades de ubicación** 
 ![ experiencia de la aplicación web para funcionalidades de ubicación](../../assets/images/tabs/location-capability.png)

## <a name="error-handling"></a>Control de errores

Debes asegurarte de controlar estos errores correctamente en la aplicación de Teams. En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores: 

|Código de error |  Nombre del error     | Condición|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no se admite en la plataforma actual.|
| **500** | INTERNAL_ERROR | Se produce un error interno al realizar la operación necesaria.|
| **1000** | PERMISSION_DENIED |El usuario ha denegado los permisos de ubicación a teams app o web-app .|
| **4000** | INVALID_ARGUMENTS | La API se invoca con argumentos obligatorios incorrectos o insuficientes.|
| **8000** | USER_ABORT |El usuario canceló la operación.|
| **9000** | OLD_PLATFORM | El usuario se encuentra en una compilación de plataforma antigua donde la implementación de la API no está presente. La actualización de la compilación debe resolver el problema.|

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

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Integrar capacidades multimedia en Teams](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Integrar la funcionalidad del escáner de códigos DE BARRAS o QR en Teams](qr-barcode-scanner-capability.md)
