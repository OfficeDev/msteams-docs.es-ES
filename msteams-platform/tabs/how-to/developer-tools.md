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
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="332d9-104">DevTools para pestañas de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="332d9-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="332d9-105">Cuando Teams se ejecuta en un explorador, es fácil acceder a DevTools del explorador: F12 (en Windows) o Command-Option-I (en MacOS).</span><span class="sxs-lookup"><span data-stu-id="332d9-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="332d9-106">DevTools le proporciona acceso a:</span><span class="sxs-lookup"><span data-stu-id="332d9-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="332d9-107">Ver registros de consola.</span><span class="sxs-lookup"><span data-stu-id="332d9-107">View console logs.</span></span>
1. <span data-ttu-id="332d9-108">Ver o modificar solicitudes html, css y de red durante el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="332d9-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="332d9-109">Agregue puntos de interrupción al código JavaScript y realice la depuración interactiva.</span><span class="sxs-lookup"><span data-stu-id="332d9-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="332d9-110">La característica solo está disponible en clientes de escritorio y Android una vez habilitada la vista previa de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="332d9-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="332d9-111">Consulta [Cómo habilitar la vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="332d9-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="332d9-112">Acceso a DevTools en el escritorio</span><span class="sxs-lookup"><span data-stu-id="332d9-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="332d9-113">Aunque la versión web de Teams y la versión de escritorio de teams son casi exactamente las mismas, existen algunas diferencias, especialmente con respecto a la autenticación.</span><span class="sxs-lookup"><span data-stu-id="332d9-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="332d9-114">A veces, la única forma de averiguar lo que está sucediendo es usar DevTools.</span><span class="sxs-lookup"><span data-stu-id="332d9-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="332d9-115">Este es el modo de obtener acceso a ellos desde el cliente de escritorio de Teams.</span><span class="sxs-lookup"><span data-stu-id="332d9-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="332d9-116">Para usar DevTools en el cliente de escritorio:</span><span class="sxs-lookup"><span data-stu-id="332d9-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="332d9-117">Asegúrese de que ha habilitado la [vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="332d9-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="332d9-118">Abra una pestaña para que tenga algo que inspeccionar con DevTools.</span><span class="sxs-lookup"><span data-stu-id="332d9-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="332d9-119">Abra DevTools de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="332d9-119">Open the DevTools one of the following ways:</span></span>
    * <span data-ttu-id="332d9-120">**Windows:** selecciona el icono de Teams en la bandeja de escritorio.</span><span class="sxs-lookup"><span data-stu-id="332d9-120">**Windows**: Select the Teams icon in the desktop tray.</span></span>
    * <span data-ttu-id="332d9-121">**macOS:** seleccione el icono de Teams en dock.</span><span class="sxs-lookup"><span data-stu-id="332d9-121">**macOS**: Select the Teams icon in the Dock.</span></span>

<span data-ttu-id="332d9-122">La siguiente captura de pantalla muestra DevTools inspeccionando un elemento en un cuadro de diálogo de configuración de tabulación:</span><span class="sxs-lookup"><span data-stu-id="332d9-122">The following screenshot shows DevTools inspecting an element in a tab configuration dialog:</span></span>

![Tab y DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="332d9-124">Acceso a DevTools desde un cliente Android</span><span class="sxs-lookup"><span data-stu-id="332d9-124">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="332d9-125">También puedes habilitar DevTools desde el cliente Android de Teams.</span><span class="sxs-lookup"><span data-stu-id="332d9-125">You can also enable the DevTools from the Teams Android client.</span></span>

1. <span data-ttu-id="332d9-126">Asegúrese de que ha habilitado la [vista previa del desarrollador](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="332d9-126">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="332d9-127">Conectar el dispositivo al equipo de escritorio y configurar el dispositivo Android para [la depuración remota](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="332d9-127">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="332d9-128">En el explorador Chrome, abra `chrome://inspect/#devices` .</span><span class="sxs-lookup"><span data-stu-id="332d9-128">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="332d9-129">Haga **clic en Inspeccionar** debajo de la pestaña que desea depurar, como en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="332d9-129">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![Android DevTools](~/assets/images/android-devtools.png)
