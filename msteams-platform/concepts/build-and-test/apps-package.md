---
title: Empaquetar la aplicación
description: Obtenga información sobre cómo empaquetar su aplicación de Microsoft Teams para probarlas, cargarlas y almacenar publicaciones.
ms.topic: conceptual
ms.openlocfilehash: 6929375c8d6a1602f01d83d15bfa0dab7f02a664
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605291"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="39247-103">Crear un paquete de aplicación para la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="39247-103">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="39247-104">Las aplicaciones en Teams se definen mediante un archivo JSON del manifiesto de la aplicación y se incluyen en un paquete de la aplicación con sus iconos.</span><span class="sxs-lookup"><span data-stu-id="39247-104">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="39247-105">Necesitará un paquete de aplicaciones para cargar e instalar la aplicación en Teams y publicar en el catálogo de aplicaciones de línea de negocio o en AppSource.</span><span class="sxs-lookup"><span data-stu-id="39247-105">You'll need an app package to upload and install your app in Teams and publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="39247-106">Un paquete de la aplicación Teams es un archivo. zip que contiene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="39247-106">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="39247-107">Un archivo de manifiesto denominado `manifest.json` , que especifica los atributos de la aplicación y apunta a los recursos necesarios para su experiencia, como la ubicación de la página de configuración de la pestaña o el identificador de aplicación de Microsoft para su bot.</span><span class="sxs-lookup"><span data-stu-id="39247-107">A manifest file named `manifest.json`, which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="39247-108">[Iconos de colores y contornos de la aplicación](#app-icons).</span><span class="sxs-lookup"><span data-stu-id="39247-108">[Color and outline icons for your app](#app-icons).</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="39247-109">Creación de un manifiesto</span><span class="sxs-lookup"><span data-stu-id="39247-109">Creating a manifest</span></span>

<span data-ttu-id="39247-110">*Teams App Studio* puede ayudarle a configurar el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="39247-110">*Teams App Studio* can help configure your manifest.</span></span> <span data-ttu-id="39247-111">También contiene una biblioteca de control React y ejemplos configurables para tarjetas.</span><span class="sxs-lookup"><span data-stu-id="39247-111">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="39247-112">Consulte [Introducción a App Studio](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39247-112">See [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="39247-113">El archivo de manifiesto debe tener el nombre "manifest.json" y estar en el nivel superior del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="39247-113">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="39247-114">Tenga en cuenta que los manifiestos y paquetes creados anteriormente podrían admitir una versión anterior del esquema.</span><span class="sxs-lookup"><span data-stu-id="39247-114">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="39247-115">Para las aplicaciones de Teams y el envío de AppSource (anteriormente tienda Office), debe usar el [esquema del manifiesto](~/resources/schema/manifest-schema.md)actual.</span><span class="sxs-lookup"><span data-stu-id="39247-115">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="39247-116">Especifique el esquema al principio del manifiesto para habilitar IntelliSense o compatibilidad similar desde el editor de código:</span><span class="sxs-lookup"><span data-stu-id="39247-116">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="app-icons"></a><span data-ttu-id="39247-117">Iconos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="39247-117">App icons</span></span>

<span data-ttu-id="39247-118">El paquete de la aplicación debe incluir dos versiones de PNG del icono de la aplicación: un icono en color y un icono de esquema.</span><span class="sxs-lookup"><span data-stu-id="39247-118">Your app package must include two PNG versions of your app icon—a color icon and an outline icon.</span></span> <span data-ttu-id="39247-119">Para que la aplicación pase la revisión de AppSource, estos iconos deben cumplir los siguientes requisitos de tamaño.</span><span class="sxs-lookup"><span data-stu-id="39247-119">For your app to pass the AppSource review, these icons must meet the following size requirements.</span></span>

> [!Note]
> <span data-ttu-id="39247-120">Si la aplicación tiene una extensión de bot ó n de mensajería, los iconos también se incluirán en el registro del servicio de bot de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="39247-120">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

### <a name="color-icon"></a><span data-ttu-id="39247-121">Icono de color</span><span class="sxs-lookup"><span data-stu-id="39247-121">Color icon</span></span>

<span data-ttu-id="39247-122">La versión de color del icono se muestra en la mayoría de los escenarios de Teams y debe ser de 192x192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="39247-122">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="39247-123">El símbolo de icono (96x96 píxeles) puede tener cualquier color o colores, pero debe sentarse en un fondo cuadrado sólido o totalmente transparente.</span><span class="sxs-lookup"><span data-stu-id="39247-123">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="39247-124">Microsoft Teams recorta automáticamente el icono para mostrar un cuadrado con esquinas redondeadas en varios escenarios y una forma hexagonal en los escenarios de bot.</span><span class="sxs-lookup"><span data-stu-id="39247-124">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="39247-125">Incluya 48 píxeles de relleno alrededor del símbolo para que estos cultivos puedan realizarse sin perder detalle.</span><span class="sxs-lookup"><span data-stu-id="39247-125">Include 48 pixels of padding around your symbol so these crops can be made without losing any detail.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Guía de diseño de iconos de color de Microsoft Teams." border="false":::

### <a name="outline-icon"></a><span data-ttu-id="39247-127">Icono de esquema</span><span class="sxs-lookup"><span data-stu-id="39247-127">Outline icon</span></span>

<span data-ttu-id="39247-128">Un icono de esquema se muestra en dos escenarios:</span><span class="sxs-lookup"><span data-stu-id="39247-128">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="39247-129">Cuando la aplicación esté en uso y "activada" en la barra de la aplicación a la izquierda de Teams.</span><span class="sxs-lookup"><span data-stu-id="39247-129">When your app is in use and “hoisted” on the app bar on the left of Teams.</span></span>
* <span data-ttu-id="39247-130">Cuando un usuario ancla la extensión de mensajería de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="39247-130">when a user pins your app's messaging extension.</span></span>

<span data-ttu-id="39247-131">El icono debe ser de 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="39247-131">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="39247-132">Puede ser blanca con un fondo transparente o transparente con un fondo blanco (no se permiten otros colores).</span><span class="sxs-lookup"><span data-stu-id="39247-132">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="39247-133">El icono de esquema no debe tener ningún relleno adicional alrededor del símbolo.</span><span class="sxs-lookup"><span data-stu-id="39247-133">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Guía de diseño de iconos de color de Microsoft Teams." border="false":::

### <a name="best-practices"></a><span data-ttu-id="39247-135">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="39247-135">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Ilustración que muestra cómo diseñar los iconos de la aplicación." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="39247-137">Do: siga las instrucciones del icono de esquema preciso</span><span class="sxs-lookup"><span data-stu-id="39247-137">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="39247-138">Los valores RGB de blanco usados en el icono deben tener el color rojo: 255, verde: 255, azul: 255.</span><span class="sxs-lookup"><span data-stu-id="39247-138">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="39247-139">Todas las demás partes del icono de esquema deben ser completamente transparentes, con el canal alfa establecido en 0.</span><span class="sxs-lookup"><span data-stu-id="39247-139">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Ilustración que muestra cómo no diseñar los iconos de la aplicación." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="39247-141">No: recortar en una forma cuadrada circular o redondeada</span><span class="sxs-lookup"><span data-stu-id="39247-141">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="39247-142">El icono de color enviado en el paquete de la aplicación debe ser cuadrado.</span><span class="sxs-lookup"><span data-stu-id="39247-142">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="39247-143">No Redondee las esquinas del icono.</span><span class="sxs-lookup"><span data-stu-id="39247-143">Don’t round the corners of your icon.</span></span> <span data-ttu-id="39247-144">Microsoft Teams ajusta automáticamente el radio de la esquina.</span><span class="sxs-lookup"><span data-stu-id="39247-144">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

### <a name="examples"></a><span data-ttu-id="39247-145">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="39247-145">Examples</span></span>

<span data-ttu-id="39247-146">Así es cómo aparecen los iconos de la aplicación en diferentes capacidades y contextos de Teams.</span><span class="sxs-lookup"><span data-stu-id="39247-146">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="39247-147">Aplicación personal</span><span class="sxs-lookup"><span data-stu-id="39247-147">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Ejemplo que muestra cómo se ve un icono de aplicación en una aplicación personal." border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="39247-149">Bot (canal)</span><span class="sxs-lookup"><span data-stu-id="39247-149">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Ejemplo que muestra cómo un icono de aplicación se busca en un bot dentro de un canal." border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="39247-151">Extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="39247-151">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texto alternativo>" border="false":::
