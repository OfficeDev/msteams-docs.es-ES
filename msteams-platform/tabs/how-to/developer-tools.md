---
title: DevTools para pestañas de Microsoft Teams
description: Describe cómo llegar a DevTools al usar el cliente de escritorio de Microsoft Teams
ms.topic: how-to
keywords: herramientas de desarrollo de depuración de herramientas para desarrolladores de cliente de escritorio chrome móvil
ms.openlocfilehash: 1bf7d246136a24316309ae144ac9552c5fd4f57d
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596276"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools para pestañas de Microsoft Teams

Cuando Teams se ejecuta en un explorador, es fácil acceder a DevTools del explorador: F12 (en Windows) o Command-Option-I (en MacOS). DevTools le proporciona acceso a:

1. Ver registros de consola.
1. Ver o modificar solicitudes html, css y de red durante el tiempo de ejecución.
1. Agregue puntos de interrupción al código JavaScript y realice la depuración interactiva.

La característica solo está disponible en clientes de escritorio y Android una vez habilitada la vista previa de desarrollador. Consulta [Cómo habilitar la vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md) para obtener más información.

## <a name="accessing-devtools-in-the-desktop"></a>Acceso a DevTools en el escritorio

Aunque la versión web de Teams y la versión de escritorio de teams son casi exactamente las mismas, existen algunas diferencias, especialmente con respecto a la autenticación. A veces, la única forma de averiguar lo que está sucediendo es usar DevTools. Este es el modo de obtener acceso a ellos desde el cliente de escritorio de Teams. Para usar DevTools en el cliente de escritorio:

1. Asegúrese de que ha habilitado la [vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md)
1. Abra una pestaña para que tenga algo que inspeccionar con DevTools.
1. Abra DevTools de una de las siguientes maneras:
    * **Windows:** selecciona el icono de Teams en la bandeja de escritorio.
    * **macOS:** seleccione el icono de Teams en dock.

La siguiente captura de pantalla muestra DevTools inspeccionando un elemento en un cuadro de diálogo de configuración de tabulación:

![Tab y DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>Acceso a DevTools desde un cliente Android

También puedes habilitar DevTools desde el cliente Android de Teams.

1. Asegúrese de que ha habilitado la [vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md)
1. Conectar el dispositivo al equipo de escritorio y configurar el dispositivo Android para [la depuración remota](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. En el explorador Chrome, abra `chrome://inspect/#devices` .
1. Haga **clic en Inspeccionar** debajo de la pestaña que desea depurar, como en la captura de pantalla siguiente.

![Android DevTools](~/assets/images/android-devtools.png)
