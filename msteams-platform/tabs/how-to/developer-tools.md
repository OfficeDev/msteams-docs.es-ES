---
title: DevTools para pestañas de Microsoft Teams
description: Describe cómo llegar a DevTools al usar el Microsoft Teams de escritorio
localization_priority: Normal
ms.topic: how-to
keywords: herramientas de desarrollo de depuración de herramientas para desarrolladores de cliente de escritorio chrome móvil
ms.openlocfilehash: 70c9a2bab94ceb97e8dcd5cf5cdb98261d037f74
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101831"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools para pestañas de Microsoft Teams

Cuando Teams se ejecuta en un explorador, es fácil acceder a DevTools del explorador: F12 en Windows o Command-Option-I en MacOS. DevTools le proporciona acceso a:

1. Ver registros de consola.
1. Ver o modificar solicitudes HTML, CSS y de red durante el tiempo de ejecución.
1. Agregue puntos de interrupción al código JavaScript y realice la depuración interactiva.

> [!NOTE]
> La característica solo está disponible para clientes de escritorio y Android después de habilitar **la vista previa** de desarrollador. Para obtener más información, [vea How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).

## <a name="access-devtools-on-the-desktop"></a>Access DevTools en el escritorio

Aunque la versión web y la versión de escritorio de Teams son casi iguales, existen algunas diferencias con respecto a la autenticación. A veces, la única forma de averiguar lo que está sucediendo es usar DevTools. Para usar DevTools en el cliente de escritorio, debe:

1. Asegúrese de que ha habilitado [la vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md).
1. Abra una pestaña para que tenga algo que inspeccionar con DevTools.
1. Abra DevTools de una de las siguientes maneras:
    * Al Windows, abra DevTools a través del Microsoft Teams en la bandeja de escritorio:<br>
  ![Haga clic con el botón secundario para abrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)
    * En MacOS, haga clic en el Microsoft Teams en dock.

En el ejemplo siguiente se muestra DevTools abierto e inspeccionando un cuadro de diálogo de configuración de tabulación:

   ![Tab y DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-device"></a>Access DevTools desde un dispositivo Android

También puedes habilitar DevTools desde el Teams Android. Para habilitar DevTools, debe:

1. Habilitar la [vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md).
1. Conectar el dispositivo al equipo de escritorio y configura el dispositivo Android para [la depuración remota.](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. En el explorador Chrome, abra `chrome://inspect/#devices` .
1. Seleccione **inspeccionar** debajo de la pestaña que desea depurar, como en la siguiente imagen:

   ![Android DevTools](~/assets/images/android-devtools.png)
