---
title: DevTools para las pestañas de Microsoft Teams
description: Describe cómo obtener acceso al DevTools al usar el cliente de escritorio de Microsoft Teams
keywords: DevTools depurar herramientas de desarrollo de cliente para escritorio móvil Chrome
ms.openlocfilehash: 6c8ac15caf64c979b23155be847e8791988486e6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675959"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools para las pestañas de Microsoft Teams

Cuando se ejecuta Teams en un explorador, es fácil obtener acceso a la DevTools del explorador: F12 (en Windows) o Comando-opción-I (en MacOS). El DevTools proporciona acceso a:

1. Ver los registros de la consola.
1. Ver o modificar las solicitudes de HTML, CSS y red durante el tiempo de ejecución.
1. Agregue puntos de interrupción al código JavaScript y realice la depuración interactiva.

La característica solo está disponible en los clientes de escritorio y Android después de que se haya habilitado la vista previa para desarrolladores. Vea [Cómo habilito la vista previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md) para obtener más información.

## <a name="accessing-devtools-in-the-desktop"></a>Acceso a DevTools en el escritorio

Aunque la versión Web de Teams y la versión de escritorio de Teams son casi exactamente iguales, hay algunas diferencias, especialmente con respecto a la autenticación. A veces, la única forma de averiguar qué está ocurriendo es usar el DevTools. Esta es la manera de obtener acceso a ellos desde el cliente de escritorio de Microsoft Teams. Para usar DevTools en el cliente de escritorio:

1. Asegurarse de que ha habilitado la [vista previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md)
1. Abra una pestaña para tener algo que inspeccionar con el DevTools.
1. Abra el DevTools
    * En Windows, se abre DevTools a través del icono de Microsoft Teams en la bandeja del escritorio:

  ![Haga clic con el botón secundario para abrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * En MacOS, haga clic en el icono de Microsoft Teams en el Dock.

Este es el aspecto de una pestaña de muestra con el DevTools abierto y un elemento seleccionado:

![TAB y DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>Acceso a DevTools desde un cliente de Android

También puede habilitar DevTools desde el cliente de Android de Teams. Para ello:

1. Asegurarse de que ha habilitado la [vista previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md)
1. Conectar el dispositivo a su equipo de escritorio y configurar el dispositivo Android para la [depuración remota](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. En el explorador Chrome, Abra `chrome://inspect/#devices`.
1. Haga clic en **inspeccionar** debajo de la pestaña que desea depurar, como se muestra en la siguiente captura de pantalla.

![DevTools de Android](~/assets/images/android-devtools.png)
