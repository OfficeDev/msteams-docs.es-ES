---
title: Permisos de dispositivo para el explorador
keywords: permisos de capacidades de aplicaciones de teams
description: Devolver de forma segura la compatibilidad con permisos de dispositivo para aplicaciones en nuestro cliente web
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: b2e83ca784e5459edfd80a3862610ebab2f8df30
ms.sourcegitcommit: ce956267b620f807e15e6d2df7afa022ffacc22f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2021
ms.locfileid: "60496251"
---
# <a name="device-permissions-for-the-browser"></a>Permisos de dispositivo para el explorador

> [!NOTE]
> El cambio en la forma en que los permisos de dispositivo se controlan en el explorador está disponible actualmente solo en [la versión preliminar del desarrollador](../../resources/dev-preview/developer-preview-intro.md) público. Este cambio estará disponible generalmente (GA) antes del 21 de enero de 2022.

Las aplicaciones que requieren permisos de dispositivo ,como el acceso a cámara o micrófono, ahora requieren que los usuarios concedan el consentimiento manualmente en un nivel de aplicación en el explorador web. Anteriormente, el explorador controló cómo se concedieron estos permisos, pero ahora estos permisos se controlarán en Microsoft Teams. Esto tiene implicaciones en el diseño de la aplicación si requieren estos permisos en el explorador.

## <a name="change-in-behavior"></a>Cambio de comportamiento
Si la aplicación ha declarado que necesita permisos de dispositivo en el manifiesto de la [aplicación,](native-device-permissions.md)se mostrará a los usuarios una opción "permisos de aplicación" donde puedan habilitar los permisos de dispositivo de una aplicación. La opción "permisos de aplicación" se puede encontrar en aplicaciones personales, cuadros de diálogo del módulo de tareas y pestañas en chats, canales o reuniones.

### <a name="personal-apps-and-task-module-dialogs"></a>Cuadros de diálogo de módulos de tareas y aplicaciones personales
La configuración "permisos de aplicación" se encuentra en la parte superior derecha.
<img src="../../assets/images/tabs/apppermissions.png" alt="App permissions button" width="800"/>

### <a name="chat-channel-or-meeting-tabs"></a>Pestañas de chat, canal o reunión
La configuración "permisos de aplicación" se puede encontrar en el desplegable de pestañas.
![Lista desplegable de permisos de aplicación](../../assets/images/tabs/drop-downapppermissions.png)

Un usuario tendrá que habilitar estos permisos en el explorador para que estos permisos entren en vigor. Cuando un usuario cambie los permisos de dispositivo de una aplicación en el explorador, se le pedirá que vuelva a cargar la aplicación en Teams. Es importante que los usuarios conozcan a dónde ir para habilitar estos permisos en Microsoft Teams.

## <a name="recommendation"></a>Recomendación
Microsoft Teams aplicaciones que requieren permisos de dispositivo en el explorador deben mostrar instrucciones a los usuarios sobre dónde buscar y habilitar estos permisos en la interfaz Teams usuario. Según el contexto en el que se ejecute la aplicación, deberá asegurarse de que las instrucciones indican al usuario que corrija la ubicación para obtener acceso a estos permisos, ya que difieren en aplicaciones personales, cuadros de diálogo de módulos de tareas y pestañas en chats, canales o reuniones.

<img src="../../assets/images/tabs/enable-access.png" alt="Enable camera access" width="800"/>

## <a name="see-also"></a>Vea también

* [Introducción a las funcionalidades de dispositivos](device-capabilities-overview.md)
* [Solicitar permisos de dispositivo](native-device-permissions.md)
