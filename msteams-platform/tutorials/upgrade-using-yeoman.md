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
# <a name="upgrade-teams-using-microsoft-teams-yeoman-generator"></a><span data-ttu-id="778d1-103">Actualizar Teams con el generador Yeoman de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="778d1-103">Upgrade Teams using Microsoft Teams Yeoman generator</span></span>
<span data-ttu-id="778d1-104">Este tutorial le ayuda a actualizar la versión actual de la aplicación de Microsoft Teams a la versión más reciente con el generador Yeoman de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="778d1-104">This tutorial helps you to upgrade your current Microsoft Teams app version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

## <a name="get-current-version-of-teams"></a><span data-ttu-id="778d1-105">Obtener la versión actual de Teams</span><span class="sxs-lookup"><span data-stu-id="778d1-105">Get current version of Teams</span></span>
```PowerShell
 yo teams --version
```

## <a name="update-teams"></a><span data-ttu-id="778d1-106">Actualizar Teams</span><span class="sxs-lookup"><span data-stu-id="778d1-106">Update Teams</span></span>
<span data-ttu-id="778d1-107">El comando yo enumera varias opciones que van desde la creación del proyecto hasta la actualización del generador.</span><span class="sxs-lookup"><span data-stu-id="778d1-107">The yo command lists out various options ranging from creating project to updating generator.</span></span> <span data-ttu-id="778d1-108">Use el siguiente comando para seleccionar el generador de actualizaciones:</span><span class="sxs-lookup"><span data-stu-id="778d1-108">Use the following command to select update generator:</span></span>
```PowerShell
 yo
```

<span data-ttu-id="778d1-109">Use las teclas de flecha para elegir **Actualizar generadores**.</span><span class="sxs-lookup"><span data-stu-id="778d1-109">Use the arrow keys to choose **Update Generators**.</span></span>
<span data-ttu-id="778d1-110">![imagen de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span><span class="sxs-lookup"><span data-stu-id="778d1-110">![image of YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)</span></span>

<span data-ttu-id="778d1-111">La lista muestra todos los generadores disponibles.</span><span class="sxs-lookup"><span data-stu-id="778d1-111">The list displays all the available generators.</span></span> <span data-ttu-id="778d1-112">Para seleccionar o anular la selección de la versión de Teams de las opciones disponibles, use la barra **espaciador** y elija un generador específico.</span><span class="sxs-lookup"><span data-stu-id="778d1-112">To select or unselect Teams version from the available options, use the **space bar** and choose a specific generator.</span></span>
<span data-ttu-id="778d1-113">![imagen de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span><span class="sxs-lookup"><span data-stu-id="778d1-113">![image of UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)</span></span>

<span data-ttu-id="778d1-114">La instalación de Teams tarda unos segundos y minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="778d1-114">It takes few seconds to minutes for Teams installation to complete.</span></span>

<span data-ttu-id="778d1-115">Una vez completada la instalación, use el siguiente comando para comprobar la versión instalada:</span><span class="sxs-lookup"><span data-stu-id="778d1-115">After the installation is complete, use the following command to check the installed version:</span></span>

```PowerShell
yo teams --version
```

![imagen de FindVersionAfterInstallation](~/assets/images/Update-Teams/FindVersionAfterInstallation.png)

<span data-ttu-id="778d1-117">¡Felicidades!</span><span class="sxs-lookup"><span data-stu-id="778d1-117">Congrats!</span></span> <span data-ttu-id="778d1-118">Ha actualizado Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="778d1-118">You have upgraded Microsoft Teams.</span></span>

