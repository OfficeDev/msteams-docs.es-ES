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
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="cb1e2-104">DevTools para pestañas de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cb1e2-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="cb1e2-105">Cuando Teams se ejecuta en un explorador, es fácil acceder a DevTools del explorador: F12 en Windows o Command-Option-I en MacOS.</span><span class="sxs-lookup"><span data-stu-id="cb1e2-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="cb1e2-106">DevTools le proporciona acceso a:</span><span class="sxs-lookup"><span data-stu-id="cb1e2-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="cb1e2-107">Ver registros de consola.</span><span class="sxs-lookup"><span data-stu-id="cb1e2-107">View console logs.</span></span>
1. <span data-ttu-id="cb1e2-108">Ver o modificar solicitudes HTML, CSS y de red durante el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="cb1e2-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="cb1e2-109">Agregue puntos de interrupción al código JavaScript y realice la depuración interactiva.</span><span class="sxs-lookup"><span data-stu-id="cb1e2-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="cb1e2-110">La característica solo está disponible en clientes de escritorio y Android una vez habilitada la **vista previa** de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="cb1e2-110">The feature is only available in desktop and Android clients after **Developer Preview** has been enabled.</span></span> <span data-ttu-id="cb1e2-111">Para obtener más información, [vea How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="cb1e2-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-in-the-desktop"></a><span data-ttu-id="cb1e2-112">Access DevTools en el escritorio</span><span class="sxs-lookup"><span data-stu-id="cb1e2-112">Access DevTools in the Desktop</span></span>

<span data-ttu-id="cb1e2-113">Aunque la versión web y la versión de escritorio de Teams son casi exactamente iguales, existen algunas diferencias con respecto a la autenticación.</span><span class="sxs-lookup"><span data-stu-id="cb1e2-113">While the web version and the desktop version of Teams are almost exactly the same, there are some differences with respect to authentication.</span></span> <span data-ttu-id="cb1e2-114">A veces, la única forma de averiguar lo que está sucediendo es usar DevTools.</span><span class="sxs-lookup"><span data-stu-id="cb1e2-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="cb1e2-115">Para usar DevTools en el cliente de escritorio, debe:</span><span class="sxs-lookup"><span data-stu-id="cb1e2-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="cb1e2-116">Asegúrese de que ha habilitado [la vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="cb1e2-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="cb1e2-117">Abra una pestaña para que tenga algo que inspeccionar con DevTools.</span><span class="sxs-lookup"><span data-stu-id="cb1e2-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="cb1e2-118">Abra DevTools de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="cb1e2-118">Open the DevTools in one of the following ways:</span></span>
    * <span data-ttu-id="cb1e2-119">**Windows:** selecciona el icono de Teams en la bandeja de escritorio.</span><span class="sxs-lookup"><span data-stu-id="cb1e2-119">**Windows**: Select the Teams icon in the desktop tray.</span></span>
    * <span data-ttu-id="cb1e2-120">**MacOS:** seleccione el icono de Teams en dock.</span><span class="sxs-lookup"><span data-stu-id="cb1e2-120">**MacOS**: Select the Teams icon in the Dock.</span></span>
 
   <span data-ttu-id="cb1e2-121">La siguiente imagen muestra DevTools inspeccionando un elemento en un cuadro de diálogo de configuración de tabulación:</span><span class="sxs-lookup"><span data-stu-id="cb1e2-121">The following image shows DevTools inspecting an element in a tab configuration dialog:</span></span>

   ![Tab y DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a><span data-ttu-id="cb1e2-123">Access DevTools desde un cliente Android</span><span class="sxs-lookup"><span data-stu-id="cb1e2-123">Access DevTools from an Android client</span></span>

<span data-ttu-id="cb1e2-124">También puedes habilitar DevTools desde el cliente Android de Teams.</span><span class="sxs-lookup"><span data-stu-id="cb1e2-124">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="cb1e2-125">Para habilitar DevTools, debe:</span><span class="sxs-lookup"><span data-stu-id="cb1e2-125">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="cb1e2-126">Habilitar la [vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="cb1e2-126">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="cb1e2-127">Conecta el dispositivo al equipo de escritorio y configura el dispositivo Android para la [depuración remota.](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="cb1e2-127">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="cb1e2-128">En el explorador Chrome, abra `chrome://inspect/#devices` .</span><span class="sxs-lookup"><span data-stu-id="cb1e2-128">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="cb1e2-129">Seleccione **inspeccionar** debajo de la pestaña que desea depurar, como en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="cb1e2-129">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
