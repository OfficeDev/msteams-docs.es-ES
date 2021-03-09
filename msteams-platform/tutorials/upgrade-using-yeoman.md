---
title: 'Tutorial: actualizar Teams con el generador Yeoman de Microsoft Teams'
description: Obtenga información sobre cómo usar el generador Yeoman de Microsoft Teams para actualizar Teams.
ms.topic: tutorial
ms.openlocfilehash: 0c52dd15703000a1c0f99ddd28401dd686e1b1bb
ms.sourcegitcommit: afe4bc0336663e496d03c52e4b206217c02fae63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2021
ms.locfileid: "50528638"
---
# <a name="upgrade-teams-using-microsoft-teams-yeoman-generator"></a>Actualizar Teams con el generador Yeoman de Microsoft Teams
Este tutorial le ayuda a actualizar la versión actual de la aplicación de Microsoft Teams a la versión más reciente con el generador Yeoman de Microsoft Teams.

## <a name="get-current-version-of-teams"></a>Obtener la versión actual de Teams
```PowerShell
 yo teams --version
```

## <a name="update-teams"></a>Actualizar Teams
El comando yo enumera varias opciones que van desde la creación del proyecto hasta la actualización del generador. Use el siguiente comando para seleccionar el generador de actualizaciones:
```PowerShell
 yo
```

Use las teclas de flecha para elegir **Actualizar generadores**.
![imagen de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

La lista muestra todos los generadores disponibles. Para seleccionar o anular la selección de la versión de Teams de las opciones disponibles, use la barra **espaciador** y elija un generador específico.
![imagen de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)

La instalación de Teams tarda unos segundos y minutos en completarse.

Una vez completada la instalación, use el siguiente comando para comprobar la versión instalada:

```PowerShell
yo teams --version
```

![imagen de FindVersionAfterInstallation](~/assets/images/Update-Teams/FindVersionAfterInstallation.png)

¡Felicidades! Ha actualizado Microsoft Teams.

