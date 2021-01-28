---
title: DevTools para pestañas de Microsoft Teams
description: Describe cómo obtener acceso a Las DevTools al usar el cliente de escritorio de Microsoft Teams
ms.topic: how-to
keywords: Herramientas de desarrollo para desarrolladores de cliente móvil de escritorio chrome de depuración
ms.openlocfilehash: 8f23a5d56faa00d40451d2bbeadde32f6a5d0f7f
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014582"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools para pestañas de Microsoft Teams

Cuando Teams se ejecuta en un explorador, es fácil acceder a las DevTools del explorador: F12 (en Windows) o Command-Option-I (en MacOS). Las DevTools te dan acceso a:

1. Ver registros de consola.
1. Ver o modificar solicitudes html, css y de red durante el tiempo de ejecución.
1. Agregue puntos de interrupción al código JavaScript y realice una depuración interactiva.

La característica solo está disponible en clientes de escritorio y Android después de habilitar la vista previa del desarrollador. Consulta [Cómo habilitar la versión preliminar del desarrollador](~/resources/dev-preview/developer-preview-intro.md) para obtener más información.

## <a name="accessing-devtools-in-the-desktop"></a>Acceso a DevTools en el escritorio

Aunque la versión web de Teams y la versión de escritorio de teams son prácticamente iguales, existen algunas diferencias, especialmente con respecto a la autenticación. A veces, la única forma de averiguar lo que está sucediendo es usar DevTools. Aquí le explicamos cómo obtener acceso a ellos desde el cliente de escritorio de Teams. Para usar DevTools en el cliente de escritorio:

1. Asegúrese de que ha habilitado la vista [previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md)
1. Abre una pestaña para que tenga algo que inspeccionar con DevTools.
1. Abrir DevTools
    * En Windows, abra DevTools a través del icono de Microsoft Teams en la bandeja de escritorio:

  ![Haga clic con el botón secundario para abrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * En MacOS, haga clic en el icono de Microsoft Teams en Dock.

Este es el aspecto de una pestaña de ejemplo con Las DevTools abiertas y un elemento seleccionado:

![Tab y DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>Obtener acceso a DevTools desde un cliente de Android

También puede habilitar Las DevTools desde el cliente de Teams para Android. Para ello:

1. Asegúrese de que ha habilitado la vista [previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md)
1. Conecta el dispositivo al equipo de escritorio y configura el dispositivo Android para la [depuración remota](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. En el explorador Chrome, abra `chrome://inspect/#devices` .
1. Haga **clic en Inspeccionar** debajo de la pestaña que desea depurar, como en la siguiente captura de pantalla.

![Android DevTools](~/assets/images/android-devtools.png)
