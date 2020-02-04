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
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="0f47b-104">DevTools para las pestañas de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0f47b-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="0f47b-105">Cuando se ejecuta Teams en un explorador, es fácil obtener acceso a la DevTools del explorador: F12 (en Windows) o Comando-opción-I (en MacOS).</span><span class="sxs-lookup"><span data-stu-id="0f47b-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="0f47b-106">El DevTools proporciona acceso a:</span><span class="sxs-lookup"><span data-stu-id="0f47b-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="0f47b-107">Ver los registros de la consola.</span><span class="sxs-lookup"><span data-stu-id="0f47b-107">View console logs.</span></span>
1. <span data-ttu-id="0f47b-108">Ver o modificar las solicitudes de HTML, CSS y red durante el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0f47b-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="0f47b-109">Agregue puntos de interrupción al código JavaScript y realice la depuración interactiva.</span><span class="sxs-lookup"><span data-stu-id="0f47b-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="0f47b-110">La característica solo está disponible en los clientes de escritorio y Android después de que se haya habilitado la vista previa para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="0f47b-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="0f47b-111">Vea [Cómo habilito la vista previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0f47b-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="0f47b-112">Acceso a DevTools en el escritorio</span><span class="sxs-lookup"><span data-stu-id="0f47b-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="0f47b-113">Aunque la versión Web de Teams y la versión de escritorio de Teams son casi exactamente iguales, hay algunas diferencias, especialmente con respecto a la autenticación.</span><span class="sxs-lookup"><span data-stu-id="0f47b-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="0f47b-114">A veces, la única forma de averiguar qué está ocurriendo es usar el DevTools.</span><span class="sxs-lookup"><span data-stu-id="0f47b-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="0f47b-115">Esta es la manera de obtener acceso a ellos desde el cliente de escritorio de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0f47b-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="0f47b-116">Para usar DevTools en el cliente de escritorio:</span><span class="sxs-lookup"><span data-stu-id="0f47b-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="0f47b-117">Asegurarse de que ha habilitado la [vista previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="0f47b-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="0f47b-118">Abra una pestaña para tener algo que inspeccionar con el DevTools.</span><span class="sxs-lookup"><span data-stu-id="0f47b-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="0f47b-119">Abra el DevTools</span><span class="sxs-lookup"><span data-stu-id="0f47b-119">Open the DevTools</span></span>
    * <span data-ttu-id="0f47b-120">En Windows, se abre DevTools a través del icono de Microsoft Teams en la bandeja del escritorio:</span><span class="sxs-lookup"><span data-stu-id="0f47b-120">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span>

  ![Haga clic con el botón secundario para abrir DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * <span data-ttu-id="0f47b-122">En MacOS, haga clic en el icono de Microsoft Teams en el Dock.</span><span class="sxs-lookup"><span data-stu-id="0f47b-122">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="0f47b-123">Este es el aspecto de una pestaña de muestra con el DevTools abierto y un elemento seleccionado:</span><span class="sxs-lookup"><span data-stu-id="0f47b-123">Here’s what a sample tab looks like with the DevTools open and an element selected:</span></span>

![TAB y DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="0f47b-125">Acceso a DevTools desde un cliente de Android</span><span class="sxs-lookup"><span data-stu-id="0f47b-125">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="0f47b-126">También puede habilitar DevTools desde el cliente de Android de Teams.</span><span class="sxs-lookup"><span data-stu-id="0f47b-126">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="0f47b-127">Para ello:</span><span class="sxs-lookup"><span data-stu-id="0f47b-127">To do so:</span></span>

1. <span data-ttu-id="0f47b-128">Asegurarse de que ha habilitado la [vista previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="0f47b-128">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="0f47b-129">Conectar el dispositivo a su equipo de escritorio y configurar el dispositivo Android para la [depuración remota](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="0f47b-129">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="0f47b-130">En el explorador Chrome, Abra `chrome://inspect/#devices`.</span><span class="sxs-lookup"><span data-stu-id="0f47b-130">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="0f47b-131">Haga clic en **inspeccionar** debajo de la pestaña que desea depurar, como se muestra en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="0f47b-131">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![DevTools de Android](~/assets/images/android-devtools.png)
