---
title: DevTools para pestañas de Microsoft Teams
description: Describe cómo llegar a DevTools al usar el cliente de escritorio de Microsoft Teams
ms.topic: how-to
keywords: herramientas de desarrollo de depuración de herramientas para desarrolladores de cliente de escritorio chrome móvil
ms.openlocfilehash: 1c540c94adc080d9495097f8e3b427eeb14c56d8
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634744"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools para pestañas de Microsoft Teams

Cuando Teams se ejecuta en un explorador, es fácil acceder a DevTools del explorador: F12 en Windows o Command-Option-I en MacOS. DevTools le proporciona acceso a:

1. Ver registros de consola.
1. Ver o modificar solicitudes HTML, CSS y de red durante el tiempo de ejecución.
1. Agregue puntos de interrupción al código JavaScript y realice la depuración interactiva.

> [!NOTE]
> La característica solo está disponible en clientes de escritorio y Android una vez habilitada la **vista previa** de desarrollador. Para obtener más información, [vea How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).

## <a name="access-devtools-in-the-desktop"></a>Access DevTools en el escritorio

Aunque la versión web y la versión de escritorio de Teams son casi exactamente iguales, existen algunas diferencias con respecto a la autenticación. A veces, la única forma de averiguar lo que está sucediendo es usar DevTools. Para usar DevTools en el cliente de escritorio, debe:

1. Asegúrese de que ha habilitado [la vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md).
1. Abra una pestaña para que tenga algo que inspeccionar con DevTools.
1. Abra DevTools de una de las siguientes maneras:
    * **Windows:** selecciona el icono de Teams en la bandeja de escritorio.
    * **MacOS:** seleccione el icono de Teams en dock.
 
   La siguiente imagen muestra DevTools inspeccionando un elemento en un cuadro de diálogo de configuración de tabulación:

   ![Tab y DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a>Access DevTools desde un cliente Android

También puedes habilitar DevTools desde el cliente Android de Teams. Para habilitar DevTools, debe:

1. Habilitar la [vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md).
1. Conecta el dispositivo al equipo de escritorio y configura el dispositivo Android para la [depuración remota.](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. En el explorador Chrome, abra `chrome://inspect/#devices` .
1. Seleccione **inspeccionar** debajo de la pestaña que desea depurar, como en la siguiente imagen:

   ![Android DevTools](~/assets/images/android-devtools.png)
