---
title: Empaquetar la aplicación
description: Obtén información sobre cómo empaquetar la aplicación de Microsoft Teams para probar, cargar y almacenar la publicación.
ms.topic: conceptual
ms.openlocfilehash: 222ea5459b3496c00b1186f15a68c3288ce419f7
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922513"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="1023c-103">Crear un paquete de aplicación para la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1023c-103">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="1023c-104">Las aplicaciones de Teams se definen mediante un archivo JSON de manifiesto de aplicación y se agrupan en un paquete de aplicación con sus iconos.</span><span class="sxs-lookup"><span data-stu-id="1023c-104">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="1023c-105">Necesitarás un paquete de aplicación para cargar e instalar la aplicación en Teams y publicarla en el catálogo de aplicaciones de línea de negocio o en AppSource.</span><span class="sxs-lookup"><span data-stu-id="1023c-105">You'll need an app package to upload and install your app in Teams and publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="1023c-106">Un paquete de aplicación de Teams es un archivo .zip que contiene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1023c-106">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="1023c-107">Un archivo de manifiesto denominado , que especifica los atributos de la aplicación y apunta a los recursos necesarios para la experiencia, como la ubicación de su página de configuración de pestañas o el identificador de aplicación de Microsoft para `manifest.json` su bot.</span><span class="sxs-lookup"><span data-stu-id="1023c-107">A manifest file named `manifest.json`, which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="1023c-108">[Iconos de color y esquema de la aplicación](#app-icons).</span><span class="sxs-lookup"><span data-stu-id="1023c-108">[Color and outline icons for your app](#app-icons).</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="1023c-109">Creación de un manifiesto</span><span class="sxs-lookup"><span data-stu-id="1023c-109">Creating a manifest</span></span>

<span data-ttu-id="1023c-110">**Teams App Studio puede** ayudar a configurar el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="1023c-110">**Teams App Studio** can help configure your manifest.</span></span> <span data-ttu-id="1023c-111">También contiene una biblioteca de control React y ejemplos configurables para tarjetas.</span><span class="sxs-lookup"><span data-stu-id="1023c-111">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="1023c-112">Para obtener más información, consulta [Introducción a App Studio](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1023c-112">For more information, see [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="1023c-113">El archivo de manifiesto debe llamarse "manifest.js" y estar en el nivel superior del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="1023c-113">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="1023c-114">Tenga en cuenta que los manifiestos y paquetes creados anteriormente pueden admitir una versión anterior del esquema.</span><span class="sxs-lookup"><span data-stu-id="1023c-114">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="1023c-115">Para las aplicaciones de Teams y, especialmente, el envío de AppSource (anteriormente Tienda Office), debe usar el esquema de [manifiesto actual.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="1023c-115">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="1023c-116">Especifique el esquema al principio del manifiesto para habilitar la IntelliSense o similar desde el editor de código:</span><span class="sxs-lookup"><span data-stu-id="1023c-116">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",`
 
## <a name="app-icons"></a><span data-ttu-id="1023c-117">Iconos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1023c-117">App icons</span></span>

<span data-ttu-id="1023c-118">El paquete de la aplicación debe incluir dos versiones PNG del icono de la aplicación: un icono de color y un icono de esquema.</span><span class="sxs-lookup"><span data-stu-id="1023c-118">Your app package must include two PNG versions of your app icon—a color icon and an outline icon.</span></span> <span data-ttu-id="1023c-119">Para que la aplicación pase la revisión de AppSource, estos iconos deben cumplir los siguientes requisitos de tamaño.</span><span class="sxs-lookup"><span data-stu-id="1023c-119">For your app to pass the AppSource review, these icons must meet the following size requirements.</span></span>

> [!Note]
> <span data-ttu-id="1023c-120">Si la aplicación tiene un bot o una extensión de mensajería, los iconos también se incluirán en el registro del Servicio de bots de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1023c-120">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

### <a name="color-icon"></a><span data-ttu-id="1023c-121">Icono de color</span><span class="sxs-lookup"><span data-stu-id="1023c-121">Color icon</span></span>

<span data-ttu-id="1023c-122">La versión de color del icono se muestra en la mayoría de los escenarios de Teams y debe tener 192 x 192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="1023c-122">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="1023c-123">El símbolo del icono (96 x 96 píxeles) puede ser cualquier color o color, pero debe estar sobre un fondo cuadrado sólido o totalmente transparente.</span><span class="sxs-lookup"><span data-stu-id="1023c-123">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="1023c-124">Teams recorta automáticamente el icono para mostrar un cuadrado con esquinas redondeadas en varios escenarios y una forma hexagonal en escenarios de bot.</span><span class="sxs-lookup"><span data-stu-id="1023c-124">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="1023c-125">Incluye 48 píxeles de relleno alrededor del símbolo para que estos recortes se puedan realizar sin perder ningún detalle.</span><span class="sxs-lookup"><span data-stu-id="1023c-125">Include 48 pixels of padding around your symbol so these crops can be made without losing any detail.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Instrucciones de diseño de iconos de color de Teams." border="false":::

### <a name="outline-icon"></a><span data-ttu-id="1023c-127">Icono esquema</span><span class="sxs-lookup"><span data-stu-id="1023c-127">Outline icon</span></span>

<span data-ttu-id="1023c-128">Un icono de esquema se muestra en dos escenarios:</span><span class="sxs-lookup"><span data-stu-id="1023c-128">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="1023c-129">Cuando la aplicación está en uso y "izada" en la barra de aplicaciones a la izquierda de Teams.</span><span class="sxs-lookup"><span data-stu-id="1023c-129">When your app is in use and “hoisted” on the app bar on the left of Teams.</span></span>
* <span data-ttu-id="1023c-130">cuando un usuario ancla la extensión de mensajería de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1023c-130">when a user pins your app's messaging extension.</span></span>

<span data-ttu-id="1023c-131">El icono debe ser de 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="1023c-131">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="1023c-132">Puede ser blanco con un fondo transparente o transparente con un fondo blanco (no se permiten otros colores).</span><span class="sxs-lookup"><span data-stu-id="1023c-132">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="1023c-133">El icono de esquema no debe tener ningún relleno adicional alrededor del símbolo.</span><span class="sxs-lookup"><span data-stu-id="1023c-133">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Instrucciones de diseño de iconos de esquema de Teams." border="false":::

### <a name="best-practices"></a><span data-ttu-id="1023c-135">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="1023c-135">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Ilustración que muestra cómo diseñar los iconos de la aplicación." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="1023c-137">Do: Follow the precise outline icon guidelines</span><span class="sxs-lookup"><span data-stu-id="1023c-137">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="1023c-138">Los valores RGB de blanco usados en el icono deben ser Rojo: 255, Verde: 255, Azul: 255.</span><span class="sxs-lookup"><span data-stu-id="1023c-138">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="1023c-139">Todas las demás partes del icono de esquema deben ser totalmente transparentes, con el canal alfa establecido en 0.</span><span class="sxs-lookup"><span data-stu-id="1023c-139">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Ilustración que muestra cómo no diseñar los iconos de la aplicación." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="1023c-141">No: Recortar en una forma cuadrada circular o redondeada</span><span class="sxs-lookup"><span data-stu-id="1023c-141">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="1023c-142">El icono de color enviado en el paquete de la aplicación debe ser cuadrado.</span><span class="sxs-lookup"><span data-stu-id="1023c-142">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="1023c-143">No redondee las esquinas del icono.</span><span class="sxs-lookup"><span data-stu-id="1023c-143">Don’t round the corners of your icon.</span></span> <span data-ttu-id="1023c-144">Teams ajusta automáticamente el radio de esquina.</span><span class="sxs-lookup"><span data-stu-id="1023c-144">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

### <a name="examples"></a><span data-ttu-id="1023c-145">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="1023c-145">Examples</span></span>

<span data-ttu-id="1023c-146">Este es el modo en que los iconos de la aplicación aparecen en diferentes contextos y capacidades de Teams.</span><span class="sxs-lookup"><span data-stu-id="1023c-146">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="1023c-147">Aplicación personal</span><span class="sxs-lookup"><span data-stu-id="1023c-147">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Ejemplo que muestra cómo se ve un icono de aplicación en una aplicación personal." border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="1023c-149">Bot (canal)</span><span class="sxs-lookup"><span data-stu-id="1023c-149">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Ejemplo que muestra cómo se ve un icono de aplicación en un bot dentro del canal." border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="1023c-151">Extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="1023c-151">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texto alternativo>" border="false":::
