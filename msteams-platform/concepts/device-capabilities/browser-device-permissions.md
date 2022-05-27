---
title: Permisos de dispositivo para el explorador
keywords: permisos de funcionalidades de aplicaciones de teams
description: Devolver de forma segura la compatibilidad con los permisos de los dispositivo para las aplicaciones en nuestro cliente web
localization_priority: medium
ms.topic: how-to
ms.openlocfilehash: 0789715aebfd1db0c9d0100ccffb2ff213a10d1d
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756747"
---
# <a name="device-permissions-for-the-browser"></a>Permisos de dispositivo para el explorador

Teams aplicación que requiere permisos de dispositivo, como el acceso a cámara o micrófono, ahora requieren que los usuarios concedan permiso manualmente en un nivel de aplicación en el explorador web. Anteriormente, el explorador se encargaba de conceder los permisos de acceso, pero ahora estos permisos se gestionan en Microsoft Teams. Esto tiene implicaciones en la forma de diseñar su aplicación y si requieren estos permisos en el explorador.

## <a name="enable-apps-device-permissions"></a>Habilitar los permisos del dispositivo de la aplicación

Si la aplicación de Teams se ha declarado en el [manifiesto de la aplicación](native-device-permissions.md#specify-permissions) que necesita permisos de dispositivo, aparecerá la opción **permisos de aplicación** para que los usuarios habiliten los permisos de dispositivo de la aplicación. La opción **permisos de aplicación** está disponible en las siguientes funcionalidades:

* **Aplicaciones personales y cuadros de diálogo de módulos de tareas**: la opción **Permisos de aplicación** está disponible en la esquina superior derecha de la página.
<img src="../../assets/images/tabs/apppermissions.png" alt="App permissions button" width="800"/>

* **Pestañas de chats, canales o reuniones**: la opción **Permisos de aplicación** está disponible en la lista desplegable de la pestaña. ![Lista desplegable Permisos de aplicación](../../assets/images/tabs/drop-downapppermissions.png)

Después de seleccionar la opción **Permisos de aplicación**, aparece un elemento emergente donde el usuario puede habilitar el botón de permisos.

Un usuario tendrá que habilitar estos permisos en el explorador para que estos permisos surtan efecto. Después de que el usuario cambie los permisos del dispositivo de la aplicación en el explorador, se le pedirá que vuelva a cargar la aplicación en Teams.

> [!IMPORTANT]
> Debe hacer que los usuarios sepan dónde deben acceder para habilitar estos **Permisos de aplicación** en Microsoft Teams.

## <a name="recommendation"></a>Recomendación

Teams aplicación que requiere permisos de dispositivo en el explorador debe mostrar instrucciones a los usuarios sobre dónde buscar y habilitar estos permisos en la interfaz de usuario de Teams. En función del contexto en el que se ejecute la aplicación, debe asegurarse de que las instrucciones apunten al usuario a la ubicación correcta para acceder a estos permisos. Los permisos difieren para aplicaciones personales, cuadros de diálogo de módulos de tareas, pestañas en chats y canales o reuniones.

</br>
<img src="../../assets/images/tabs/enable-access.png" alt="Enable camera access" width="800"/>

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | Node.js |
|----------------|-----------------|--------------|
| Permisos de dispositivo de la pestaña para el explorador | El código de ejemplo muestra cómo mostrar los permisos del dispositivo para el explorador. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../../sbs-tab-device-permissions.yml) para conceder permiso de dispositivo de pestaña en Microsoft Teams.

## <a name="see-also"></a>Consulte también

* [Información general sobre las funcionalidades del dispositivo](device-capabilities-overview.md)
* [Solicitar permisos de dispositivo](native-device-permissions.md)
