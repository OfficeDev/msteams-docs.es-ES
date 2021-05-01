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
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="72ee8-104">DevTools para pestañas de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="72ee8-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="72ee8-105">Cuando Teams se ejecuta en un explorador, es fácil acceder a DevTools del explorador: F12 en Windows o Command-Option-I en MacOS.</span><span class="sxs-lookup"><span data-stu-id="72ee8-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="72ee8-106">DevTools le proporciona acceso a:</span><span class="sxs-lookup"><span data-stu-id="72ee8-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="72ee8-107">Ver registros de consola.</span><span class="sxs-lookup"><span data-stu-id="72ee8-107">View console logs.</span></span>
1. <span data-ttu-id="72ee8-108">Ver o modificar solicitudes HTML, CSS y de red durante el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="72ee8-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="72ee8-109">Agregue puntos de interrupción al código JavaScript y realice la depuración interactiva.</span><span class="sxs-lookup"><span data-stu-id="72ee8-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="72ee8-110">La característica solo está disponible para clientes de escritorio y Android después de habilitar **la vista previa** de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="72ee8-110">The feature is only available for desktop and Android clients after the **Developer Preview** has been enabled.</span></span> <span data-ttu-id="72ee8-111">Para obtener más información, [vea How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="72ee8-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-on-the-desktop"></a><span data-ttu-id="72ee8-112">Access DevTools en el escritorio</span><span class="sxs-lookup"><span data-stu-id="72ee8-112">Access DevTools on the desktop</span></span>

<span data-ttu-id="72ee8-113">Aunque la versión web y la versión de escritorio de Teams son casi iguales, existen algunas diferencias con respecto a la autenticación.</span><span class="sxs-lookup"><span data-stu-id="72ee8-113">While the web version and the desktop version of Teams are almost the same, there are some differences concerning authentication.</span></span> <span data-ttu-id="72ee8-114">A veces, la única forma de averiguar lo que está sucediendo es usar DevTools.</span><span class="sxs-lookup"><span data-stu-id="72ee8-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="72ee8-115">Para usar DevTools en el cliente de escritorio, debe:</span><span class="sxs-lookup"><span data-stu-id="72ee8-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="72ee8-116">Asegúrese de que ha habilitado [la vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="72ee8-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="72ee8-117">Abra una pestaña para que tenga algo que inspeccionar con DevTools.</span><span class="sxs-lookup"><span data-stu-id="72ee8-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="72ee8-118">Abra DevTools de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="72ee8-118">Open the DevTools one of the following ways:</span></span>
    * <span data-ttu-id="72ee8-119">Al Windows, abra DevTools a través del Microsoft Teams en la bandeja de escritorio:</span><span class="sxs-lookup"><span data-stu-id="72ee8-119">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span><br>
  <span data-ttu-id="72ee8-120">![Haga clic con el botón secundario para abrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)</span><span class="sxs-lookup"><span data-stu-id="72ee8-120">![Right-click to open DevTools](~/assets/images/dev-preview/devtools-right-click.png)</span></span>
    * <span data-ttu-id="72ee8-121">En MacOS, haga clic en el Microsoft Teams en dock.</span><span class="sxs-lookup"><span data-stu-id="72ee8-121">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="72ee8-122">En el ejemplo siguiente se muestra DevTools abierto e inspeccionando un cuadro de diálogo de configuración de tabulación:</span><span class="sxs-lookup"><span data-stu-id="72ee8-122">The following example shows DevTools open and inspecting a tab configuration dialog:</span></span>

   ![Tab y DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-device"></a><span data-ttu-id="72ee8-124">Access DevTools desde un dispositivo Android</span><span class="sxs-lookup"><span data-stu-id="72ee8-124">Access DevTools from an Android device</span></span>

<span data-ttu-id="72ee8-125">También puedes habilitar DevTools desde el Teams Android.</span><span class="sxs-lookup"><span data-stu-id="72ee8-125">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="72ee8-126">Para habilitar DevTools, debe:</span><span class="sxs-lookup"><span data-stu-id="72ee8-126">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="72ee8-127">Habilitar la [vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="72ee8-127">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="72ee8-128">Conectar el dispositivo al equipo de escritorio y configura el dispositivo Android para [la depuración remota.](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="72ee8-128">Connect your device to your desktop computer, and set up your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="72ee8-129">En el explorador Chrome, abra `chrome://inspect/#devices` .</span><span class="sxs-lookup"><span data-stu-id="72ee8-129">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="72ee8-130">Seleccione **inspeccionar** debajo de la pestaña que desea depurar, como en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="72ee8-130">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
