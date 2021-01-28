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
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="31d06-104">DevTools para pestañas de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="31d06-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="31d06-105">Cuando Teams se ejecuta en un explorador, es fácil acceder a las DevTools del explorador: F12 (en Windows) o Command-Option-I (en MacOS).</span><span class="sxs-lookup"><span data-stu-id="31d06-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="31d06-106">Las DevTools te dan acceso a:</span><span class="sxs-lookup"><span data-stu-id="31d06-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="31d06-107">Ver registros de consola.</span><span class="sxs-lookup"><span data-stu-id="31d06-107">View console logs.</span></span>
1. <span data-ttu-id="31d06-108">Ver o modificar solicitudes html, css y de red durante el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="31d06-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="31d06-109">Agregue puntos de interrupción al código JavaScript y realice una depuración interactiva.</span><span class="sxs-lookup"><span data-stu-id="31d06-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="31d06-110">La característica solo está disponible en clientes de escritorio y Android después de habilitar la vista previa del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="31d06-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="31d06-111">Consulta [Cómo habilitar la versión preliminar del desarrollador](~/resources/dev-preview/developer-preview-intro.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="31d06-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="31d06-112">Acceso a DevTools en el escritorio</span><span class="sxs-lookup"><span data-stu-id="31d06-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="31d06-113">Aunque la versión web de Teams y la versión de escritorio de teams son prácticamente iguales, existen algunas diferencias, especialmente con respecto a la autenticación.</span><span class="sxs-lookup"><span data-stu-id="31d06-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="31d06-114">A veces, la única forma de averiguar lo que está sucediendo es usar DevTools.</span><span class="sxs-lookup"><span data-stu-id="31d06-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="31d06-115">Aquí le explicamos cómo obtener acceso a ellos desde el cliente de escritorio de Teams.</span><span class="sxs-lookup"><span data-stu-id="31d06-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="31d06-116">Para usar DevTools en el cliente de escritorio:</span><span class="sxs-lookup"><span data-stu-id="31d06-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="31d06-117">Asegúrese de que ha habilitado la vista [previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="31d06-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="31d06-118">Abre una pestaña para que tenga algo que inspeccionar con DevTools.</span><span class="sxs-lookup"><span data-stu-id="31d06-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="31d06-119">Abrir DevTools</span><span class="sxs-lookup"><span data-stu-id="31d06-119">Open the DevTools</span></span>
    * <span data-ttu-id="31d06-120">En Windows, abra DevTools a través del icono de Microsoft Teams en la bandeja de escritorio:</span><span class="sxs-lookup"><span data-stu-id="31d06-120">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span>

  ![Haga clic con el botón secundario para abrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * <span data-ttu-id="31d06-122">En MacOS, haga clic en el icono de Microsoft Teams en Dock.</span><span class="sxs-lookup"><span data-stu-id="31d06-122">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="31d06-123">Este es el aspecto de una pestaña de ejemplo con Las DevTools abiertas y un elemento seleccionado:</span><span class="sxs-lookup"><span data-stu-id="31d06-123">Here’s what a sample tab looks like with the DevTools open and an element selected:</span></span>

![Tab y DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="31d06-125">Obtener acceso a DevTools desde un cliente de Android</span><span class="sxs-lookup"><span data-stu-id="31d06-125">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="31d06-126">También puede habilitar Las DevTools desde el cliente de Teams para Android.</span><span class="sxs-lookup"><span data-stu-id="31d06-126">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="31d06-127">Para ello:</span><span class="sxs-lookup"><span data-stu-id="31d06-127">To do so:</span></span>

1. <span data-ttu-id="31d06-128">Asegúrese de que ha habilitado la vista [previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="31d06-128">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="31d06-129">Conecta el dispositivo al equipo de escritorio y configura el dispositivo Android para la [depuración remota](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="31d06-129">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="31d06-130">En el explorador Chrome, abra `chrome://inspect/#devices` .</span><span class="sxs-lookup"><span data-stu-id="31d06-130">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="31d06-131">Haga **clic en Inspeccionar** debajo de la pestaña que desea depurar, como en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="31d06-131">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![Android DevTools](~/assets/images/android-devtools.png)
