---
title: DevTools para pestañas de Microsoft Teams
description: En este módulo, obtenga información sobre cómo llegar a DevTools cuando se usa el cliente de escritorio de Microsoft Teams y la depuración
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: a0d5e3ea15fd796c2c426f1cf1457171f0abe7b2
ms.sourcegitcommit: 024be23411bc0f2573d19f48f9266021f9b76f0d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2022
ms.locfileid: "67488274"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools para pestañas de Microsoft Teams

Cuando Teams se ejecuta en un explorador, es fácil acceder a DevTools: F12 en Windows o Command-Option-I en MacOS. DevTools le ofrece acceso a:

1. Ver registros de consola.
1. Vea o modifique las solicitudes HTML, CSS y de red durante el tiempo de ejecución.
1. Agregue puntos de interrupción al código JavaScript y realice la depuración interactiva.

> [!NOTE]
> La característica solo está disponible para clientes de escritorio y Android una vez habilitada la **versión preliminar para desarrolladores**. Para obtener más información, consulte [Cómo habilitar la versión preliminar para desarrolladores](~/resources/dev-preview/developer-preview-intro.md).

## <a name="access-devtools-on-the-desktop"></a>Acceso a DevTools en el escritorio

Aunque la versión web y la versión de escritorio de Teams son casi iguales, hay algunas diferencias en cuanto a la autenticación. A veces, la única manera de averiguar lo que está pasando es usar DevTools. Para usar DevTools en el cliente de escritorio, debe:

1. Asegurarse de que ha habilitado [la versión preliminar para desarrolladores](~/resources/dev-preview/developer-preview-intro.md).
1. Abrir una pestaña para que tenga algo que inspeccionar con DevTools.
1. Abrir DevTools de una de las siguientes maneras:
    * En Windows, abra DevTools a través del icono de Microsoft Teams en la bandeja de escritorio.

      :::image type="content" source="../../assets/images/dev-preview/devtools-right-click.png" alt-text="developer-tool-windows":::

    * En MacOS, seleccione el icono de Microsoft Teams en dock.

      :::image type="content" source="../../assets/images/dev-preview/mac-os-developer-tools.PNG" alt-text="mac-os-dev-tools":::

En el ejemplo siguiente se muestra DevTools abierto e inspeccionando un cuadro de diálogo de configuración de pestaña:

   [![Pestaña y DevTools](~/assets/images/dev-preview/tab-and-devtools.png)](~/assets/images/dev-preview/tab-and-devtools.png#lightbox)

## <a name="access-devtools-from-an-android-device"></a>Acceso a DevTools desde un dispositivo Android

También puede habilitar DevTools desde el cliente Android de Teams. Para habilitar DevTools, debe:

1. Habilitar la [versión preliminar para desarrolladores](~/resources/dev-preview/developer-preview-intro.md).
1. Conectar el dispositivo en el equipo de escritorio y configurar el dispositivo Android para la [depuración remota](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).
1. En el explorador Chrome, abra `chrome://inspect/#devices`.
1. Seleccione **Inspeccionar** en la pestaña que desea depurar, como en la siguiente imagen:

   ![Android DevTools](~/assets/images/android-devtools.png)

## <a name="see-also"></a>Vea también

[Borrar la caché del cliente Teams](/microsoftteams/troubleshoot/teams-administration/clear-teams-cache)
