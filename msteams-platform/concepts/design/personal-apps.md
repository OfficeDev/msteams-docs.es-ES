---
title: Referencia de directrices de diseño
description: Describe las instrucciones para diseñar una aplicación personal
keywords: guías de diseño de Microsoft Teams referencia de aplicaciones personales
ms.openlocfilehash: 6a07b618d78a3ad79850713052c88ef178c1ecc1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675783"
---
# <a name="personal-apps"></a><span data-ttu-id="1de66-104">Aplicaciones personales</span><span class="sxs-lookup"><span data-stu-id="1de66-104">Personal apps</span></span>

> [!Important]
> <span data-ttu-id="1de66-105">Pronto estará disponible la compatibilidad completa con las pestañas de los clientes móviles.</span><span class="sxs-lookup"><span data-stu-id="1de66-105">Full support for tabs on mobile clients is coming soon.</span></span> <span data-ttu-id="1de66-106">Para prepararse para este cambio, debe seguir las [instrucciones para las pestañas de dispositivos móviles](~/tabs/design/tabs-mobile.md) al crear las pestañas.</span><span class="sxs-lookup"><span data-stu-id="1de66-106">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="1de66-107">Las aplicaciones personales (pestañas estáticas) están disponibles actualmente en [Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="1de66-107">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="1de66-108">Cuando se publica la compatibilidad completa de pestañas:</span><span class="sxs-lookup"><span data-stu-id="1de66-108">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="1de66-109">Todas las pestañas estarán siempre disponibles en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="1de66-109">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="1de66-110">El `contentUrl` **se cargará en el cliente móvil de Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="1de66-110">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="1de66-111">En las pestañas canal/grupo, los usuarios pueden abrir la pestaña en un explorador independiente `websiteUrl`a través de `contentUrl` la, pero se cargará primero.</span><span class="sxs-lookup"><span data-stu-id="1de66-111">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>

<span data-ttu-id="1de66-112">Una aplicación personal es una aplicación con un ámbito personal.</span><span class="sxs-lookup"><span data-stu-id="1de66-112">A personal app is an app with a personal scope.</span></span> <span data-ttu-id="1de66-113">Como desarrollador de aplicaciones, tiene la opción de proporcionar una versión de la aplicación que se crea para el usuario individual.</span><span class="sxs-lookup"><span data-stu-id="1de66-113">As an app developer, you have the option to provide a version of your app that is built for the individual user.</span></span> <span data-ttu-id="1de66-114">En esta versión, la colección de pestañas (y el bot, si ha incluido uno), están diseñados para la persona.</span><span class="sxs-lookup"><span data-stu-id="1de66-114">In this version, the collection of tabs (and the bot, if you've included one), are designed for the person.</span></span> <span data-ttu-id="1de66-115">De este modo, podrá crear una interacción de uno en uno con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1de66-115">This way, you're able to create a one-on-one interaction with your users.</span></span>

<span data-ttu-id="1de66-116">Una aplicación personal es donde alguien puede ver todo lo que es y todos los elementos que ha visto recientemente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1de66-116">A personal app is where someone can see everything that's theirs, and all the items they've recently viewed in the app.</span></span> <span data-ttu-id="1de66-117">Coloca todo en un solo punto.</span><span class="sxs-lookup"><span data-stu-id="1de66-117">It puts everything in one place.</span></span> <span data-ttu-id="1de66-118">En la siguiente captura de pantalla, contoso es una aplicación personal en el flotante de la aplicación personal.</span><span class="sxs-lookup"><span data-stu-id="1de66-118">In the following screenshot, Contoso is a personal app in the personal app flyout.</span></span>

![imagen del menú de desbordamiento de la aplicación](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a><span data-ttu-id="1de66-120">Instrucciones</span><span class="sxs-lookup"><span data-stu-id="1de66-120">Guidelines</span></span>

<span data-ttu-id="1de66-121">Una aplicación personal suele contener las siguientes pestañas:</span><span class="sxs-lookup"><span data-stu-id="1de66-121">A personal app typically contains the following tabs:</span></span>

### <a name="your-tab"></a><span data-ttu-id="1de66-122">La pestaña</span><span class="sxs-lookup"><span data-stu-id="1de66-122">Your tab</span></span>

<span data-ttu-id="1de66-123">Aquí es donde los usuarios verán todo su contenido.</span><span class="sxs-lookup"><span data-stu-id="1de66-123">This is where your users will see all their stuff.</span></span> <span data-ttu-id="1de66-124">Su espacio personal.</span><span class="sxs-lookup"><span data-stu-id="1de66-124">It's their personal space.</span></span> <span data-ttu-id="1de66-125">La pestaña se puede organizar como una lista, una cuadrícula, columnas o un solo lienzo... lo que mejor se adapte a su aplicación.</span><span class="sxs-lookup"><span data-stu-id="1de66-125">The tab can be arranged as a list, a grid, columns, or a single canvas...whatever works best for your application.</span></span> <span data-ttu-id="1de66-126">Para obtener más información sobre el diseño de pestañas efectivas, vea: [diseño de pestañas (~/Tabs/Design/Tabs.MD).</span><span class="sxs-lookup"><span data-stu-id="1de66-126">For additional information on designing effective tabs see: [Tabs design(~/tabs/design/tabs.md).</span></span>

<span data-ttu-id="1de66-127">Como esta pestaña puede mostrar elementos de varios canales, cada elemento debería mostrar su propio equipo, canal y pestaña para que el usuario pueda ver fácilmente dónde se originó.</span><span class="sxs-lookup"><span data-stu-id="1de66-127">Since this tab can show items from multiple channels, each item should display its own team, channel, and tab so the user can easily see where it originated.</span></span>

![Ficha tareas personales](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a><span data-ttu-id="1de66-129">Posterior</span><span class="sxs-lookup"><span data-stu-id="1de66-129">Recent</span></span>

<span data-ttu-id="1de66-130">La pestaña **reciente** permite a un usuario examinar todo lo que haya visto recientemente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1de66-130">The **Recent** tab lets someone browse everything they've recently viewed in your app.</span></span> <span data-ttu-id="1de66-131">Aparece en orden cronológico (de mayor a menos reciente).</span><span class="sxs-lookup"><span data-stu-id="1de66-131">It's listed in chronological order (from most to least recent).</span></span> <span data-ttu-id="1de66-132">Al hacer clic en un elemento de esta lista, se desplazará al usuario hasta el canal y la ficha del elemento.</span><span class="sxs-lookup"><span data-stu-id="1de66-132">Clicking on an item in this list will navigate the user to that item's channel and tab.</span></span>

![Pestaña reciente](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a><span data-ttu-id="1de66-134">Todo</span><span class="sxs-lookup"><span data-stu-id="1de66-134">All</span></span>

<span data-ttu-id="1de66-135">Esta es una lista de todas las pestañas de la organización de la persona (a las que tienen acceso, en cualquier caso).</span><span class="sxs-lookup"><span data-stu-id="1de66-135">This is a list of all your tabs in the person's organization (the ones they have access to, anyway).</span></span> <span data-ttu-id="1de66-136">Es decir, los muestra en todas partes donde se usa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1de66-136">In other words, it shows them everywhere the app is being used.</span></span> <span data-ttu-id="1de66-137">Como en la ficha **reciente** , al seleccionar un elemento de la lista, el usuario pasa directamente al canal y a la ficha correspondientes.</span><span class="sxs-lookup"><span data-stu-id="1de66-137">As with the **Recent** tab, selecting something in the list will bring the user straight to the relevant channel and tab.</span></span>

### <a name="bot"></a><span data-ttu-id="1de66-138">Bot</span><span class="sxs-lookup"><span data-stu-id="1de66-138">Bot</span></span>

<span data-ttu-id="1de66-139">Un bot no es necesario, pero es una buena forma de comunicarse directa y privadamente con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1de66-139">A bot isn't required, but it's a great way to communicate directly and privately with your users.</span></span> <span data-ttu-id="1de66-140">La notificación es una de las funciones más importantes de una aplicación personal y la mejor forma de notificarla que con la comunicación directa.</span><span class="sxs-lookup"><span data-stu-id="1de66-140">Notification is one of the most important functions of a personal app, and what better way to notify than with direct communication?</span></span>

<span data-ttu-id="1de66-141">Los bots entregan mensajes en forma de tarjetas, que pueden proporcionar información específica (por ejemplo, una alerta de que el contenido nuevo está disponible) o actualizaciones amplias (como una lista de tareas pendientes diaria).</span><span class="sxs-lookup"><span data-stu-id="1de66-141">Bots deliver messages in the form of cards, which can provide specific information (like an alert that new content is available) or broad updates (like a daily to-do list).</span></span> <span data-ttu-id="1de66-142">Para obtener más información sobre el diseño de bots efectivos, consulte: [diseño de Bot (~/bots/Design/bots.MD).</span><span class="sxs-lookup"><span data-stu-id="1de66-142">For additional information on designing effective bots see: [Bot design(~/bots/design/bots.md).</span></span>

![Saludo de bot](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a><span data-ttu-id="1de66-144">Ayuda y configuración</span><span class="sxs-lookup"><span data-stu-id="1de66-144">Help and Settings</span></span>

<span data-ttu-id="1de66-145">El contenido de la ayuda permite a los usuarios descubrir los matices de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1de66-145">Help content enables users to discover the nuances of your app.</span></span> <span data-ttu-id="1de66-146">Agregue una pestaña de **configuración** para darles la capacidad de personalizarla.</span><span class="sxs-lookup"><span data-stu-id="1de66-146">Add a **Settings** tab to give them the ability to further customize it.</span></span>

### <a name="about"></a><span data-ttu-id="1de66-147">Acerca de</span><span class="sxs-lookup"><span data-stu-id="1de66-147">About</span></span>

<span data-ttu-id="1de66-148">Incluya una ficha **acerca** de para proporcionar información como el número de versión, las capacidades, la privacidad y los vínculos de permisos.</span><span class="sxs-lookup"><span data-stu-id="1de66-148">Include an **About** tab to provide information like version number, capabilities, privacy, and permissions links.</span></span>

## <a name="best-practices"></a><span data-ttu-id="1de66-149">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="1de66-149">Best practices</span></span>

### <a name="communicate-directly-with-your-users"></a><span data-ttu-id="1de66-150">Comunicarse directamente con los usuarios</span><span class="sxs-lookup"><span data-stu-id="1de66-150">Communicate directly with your users</span></span>

<span data-ttu-id="1de66-151">Usar un bot para notificar a los usuarios los cambios y las nuevas características.</span><span class="sxs-lookup"><span data-stu-id="1de66-151">Use a bot to notify users of changes and new features.</span></span>

### <a name="customize-your-tabs"></a><span data-ttu-id="1de66-152">Personalice sus pestañas...</span><span class="sxs-lookup"><span data-stu-id="1de66-152">Customize your tabs...</span></span>

<span data-ttu-id="1de66-153">No dude en agregar otras pestañas que ayuden a los usuarios a realizar tareas específicas.</span><span class="sxs-lookup"><span data-stu-id="1de66-153">Feel free to add other tabs that will help your users accomplish specific tasks.</span></span>

### <a name="and-make-them-relevant-to-every-user"></a><span data-ttu-id="1de66-154">... y hacer que sean relevantes para todos los usuarios</span><span class="sxs-lookup"><span data-stu-id="1de66-154">...and make them relevant to every user</span></span>

<span data-ttu-id="1de66-155">Cada pestaña que declare en el manifiesto de la aplicación será visible para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1de66-155">Every tab you declare in your app manifest will be visible to all users.</span></span> <span data-ttu-id="1de66-156">Por ejemplo, si la aplicación personal es una herramienta de informes de gastos que usan tanto los administradores como los empleados, una ficha de **aprobación** debe proporcionar contenido que sea significativo para ambas funciones.</span><span class="sxs-lookup"><span data-stu-id="1de66-156">For example, if your personal app is an expense reporting tool that is used by both managers and employees, an **Approval** tab should provide content that is meaningful to both roles.</span></span>
