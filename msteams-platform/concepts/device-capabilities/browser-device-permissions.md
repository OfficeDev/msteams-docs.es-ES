---
title: Permisos de dispositivo para el explorador
keywords: permisos de capacidades de aplicaciones de teams
description: Devolver de forma segura la compatibilidad con permisos de dispositivo para aplicaciones en nuestro cliente web
localization_priority: medium
ms.topic: how-to
ms.openlocfilehash: 18843d9d4981e83cf83472e37519344706f599bb
ms.sourcegitcommit: 20b84e13b5cb6899f4eb54ca90a13b6da7a3e3d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/16/2022
ms.locfileid: "62855889"
---
# <a name="device-permissions-for-the-browser"></a>Permisos de dispositivo para el explorador

> [!NOTE]
> La actualización más reciente sobre cómo se administran los permisos de dispositivo en el explorador está disponible solo en [la versión preliminar del desarrollador](../../resources/dev-preview/developer-preview-intro.md) público. Esta actualización estará disponible generalmente (GA) a partir del 01 de febrero de 2022 y finalizará a finales de febrero.


Teams que requieren permisos de dispositivo, como acceso a cámara o micrófono, ahora requieren que los usuarios concedan permisos manualmente a un nivel de aplicación en el explorador web. Anteriormente, el explorador controló cómo conceder permisos de acceso, pero ahora estos permisos se controlan en Microsoft Teams. Esto tiene implicaciones en el diseño de la aplicación y si requieren estos permisos en el explorador.

## <a name="enable-apps-device-permissions"></a>Habilitar los permisos de dispositivo de la aplicación
Si la aplicación Teams ha declarado en el manifiesto de la [](native-device-permissions.md#specify-permissions) aplicación que necesita permisos de dispositivo, aparecerá la opción Permisos  de la aplicación para que los usuarios habiliten los permisos de dispositivo de la aplicación. La **opción Permisos de** la aplicación está disponible en las siguientes funcionalidades: 

* **Cuadros de diálogo de módulos** de tareas y aplicaciones personales: la opción **Permisos de** la aplicación está disponible en la esquina superior derecha de la página.
<img src="../../assets/images/tabs/apppermissions.png" alt="App permissions button" width="800"/>

* **Pestañas de chat, canal** o reunión: la **opción Permisos** de la aplicación está disponible en el desplegable de la pestaña. ![ Lista desplegable de permisos de aplicación](../../assets/images/tabs/drop-downapppermissions.png)

Una vez **seleccionada la** opción Permisos de la aplicación, aparece un elemento emergente donde el usuario puede habilitar el botón de permisos.

Un usuario tendrá que habilitar estos permisos en el explorador para que estos permisos entren en vigor. Después de que el usuario cambie los permisos de dispositivo de la aplicación en el explorador, se le pedirá que vuelva a cargar la aplicación en Teams.

> [!IMPORTANT]
> Debes hacer que los usuarios conozcan a dónde ir para habilitar estos permisos **de** aplicación en Microsoft Teams.

## <a name="recommendation"></a>Recomendación
Teams que requieren permisos de dispositivo en el explorador deben mostrar instrucciones a los usuarios sobre dónde buscar y habilitar estos permisos en la interfaz Teams usuario. Según el contexto en el que se ejecute la aplicación, debe asegurarse de que las instrucciones indican al usuario que corrija la ubicación para tener acceso a estos permisos, ya que difieren en aplicaciones personales, cuadros de diálogo de módulos de tareas, pestañas en chats y canales o reuniones.

</br>
<img src="../../assets/images/tabs/enable-access.png" alt="Enable camera access" width="800"/>

## <a name="code-sample"></a>Ejemplo de código

|Ejemplo de nombre | Descripción | Node.js |
|----------------|-----------------|--------------|
| Permisos de dispositivo de tabulación para el explorador | El código de ejemplo muestra cómo mostrar los permisos del dispositivo para el explorador. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso para](../../sbs-tab-device-permissions.yml) conceder permiso de dispositivo de pestaña en Microsoft Teams.

## <a name="see-also"></a>Vea también

* [Introducción a las funcionalidades de dispositivos](device-capabilities-overview.md)
* [Solicitar permisos de dispositivo](native-device-permissions.md)
