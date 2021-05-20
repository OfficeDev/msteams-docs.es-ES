---
title: Empaqueta tu aplicación
description: Obtén información sobre cómo empaquetar la aplicación Microsoft Teams para probar, cargar y almacenar publicaciones.
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 219e2d5341707ed51b7e0a3a8077f93df9eac640
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565217"
---
# <a name="create-a-microsoft-teams-app-package"></a><span data-ttu-id="3a015-103">Crear un paquete de aplicación Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3a015-103">Create a Microsoft Teams app package</span></span>

<span data-ttu-id="3a015-104">Necesitas un paquete de aplicación, sin embargo, planeas distribuir tu aplicación Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3a015-104">You need an app package however you plan to distribute your Microsoft Teams app.</span></span> <span data-ttu-id="3a015-105">Un paquete válido es un archivo ZIP que contiene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3a015-105">A valid package is a ZIP file that contains the following:</span></span>

* <span data-ttu-id="3a015-106">**Manifiesto de aplicación:** describe cómo está configurada la aplicación, incluidas sus capacidades, recursos necesarios y otros atributos importantes.</span><span class="sxs-lookup"><span data-stu-id="3a015-106">**App manifest**: Describes how your app is configured, including its capabilities, required resources, and other important attributes.</span></span>
* <span data-ttu-id="3a015-107">**Iconos de la aplicación:** cada paquete requiere un icono de color y contorno para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a015-107">**App icons**: Each package requires a color and outline icon for your app.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="3a015-108">Manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3a015-108">App manifest</span></span>

<span data-ttu-id="3a015-109">El archivo de manifiesto de la aplicación debe estar en el nivel superior del paquete con el nombre `manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="3a015-109">Your app manifest file must be at the top level of the package with the name `manifest.json`.</span></span> 

<span data-ttu-id="3a015-110">Al publicar en el almacén de Teams, asegúrese de que el manifiesto hace referencia al [esquema](~/resources/schema/manifest-schema.md)más reciente.</span><span class="sxs-lookup"><span data-stu-id="3a015-110">When publishing to the Teams store, make sure your manifest references the latest [schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="app-icons"></a><span data-ttu-id="3a015-111">Iconos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3a015-111">App icons</span></span>

<span data-ttu-id="3a015-112">El paquete de la aplicación debe incluir dos versiones PNG del icono de la aplicación: una versión de color y contorno.</span><span class="sxs-lookup"><span data-stu-id="3a015-112">Your app package must include two PNG versions of your app icon: A color and outline version.</span></span>

> [!Note]
> <span data-ttu-id="3a015-113">Si la aplicación tiene un bot o una extensión de mensajería, los iconos también se incluirán en el registro Microsoft Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="3a015-113">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

<span data-ttu-id="3a015-114">Para que la aplicación pase Teams revisión de la tienda, estos iconos deben cumplir los siguientes requisitos de tamaño.</span><span class="sxs-lookup"><span data-stu-id="3a015-114">For your app to pass Teams store review, these icons must meet the following size requirements.</span></span>

### <a name="color-icon"></a><span data-ttu-id="3a015-115">Icono de color</span><span class="sxs-lookup"><span data-stu-id="3a015-115">Color icon</span></span>

<span data-ttu-id="3a015-116">La versión en color del icono se muestra en la mayoría de los escenarios Teams y debe ser de 192x192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="3a015-116">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="3a015-117">Su símbolo de icono (96x96 píxeles) puede ser de cualquier color, pero debe sentarse sobre un fondo cuadrado sólido o totalmente transparente.</span><span class="sxs-lookup"><span data-stu-id="3a015-117">Your icon symbol (96x96 pixels) can be any color, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="3a015-118">Teams recorta automáticamente el icono para mostrar un cuadrado con esquinas redondeadas en varios escenarios y una forma hexagonal en escenarios de bots.</span><span class="sxs-lookup"><span data-stu-id="3a015-118">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="3a015-119">Para recortar el símbolo sin perder ningún detalle, incluye 48 píxeles de relleno alrededor de tu símbolo.</span><span class="sxs-lookup"><span data-stu-id="3a015-119">To crop the symbol without losing any detail, include 48 pixels of padding around your symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams icono de color y orientación de diseño." border="false":::

### <a name="outline-icon"></a><span data-ttu-id="3a015-121">Icono de contorno</span><span class="sxs-lookup"><span data-stu-id="3a015-121">Outline icon</span></span>

<span data-ttu-id="3a015-122">Un icono de contorno se muestra en dos escenarios:</span><span class="sxs-lookup"><span data-stu-id="3a015-122">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="3a015-123">Cuando la aplicación está en uso y "izado" en la barra de aplicaciones en el lado izquierdo de Teams.</span><span class="sxs-lookup"><span data-stu-id="3a015-123">When your app is in use and “hoisted” on the app bar on the left side of Teams.</span></span>
* <span data-ttu-id="3a015-124">Cuando un usuario ancle la extensión de mensajería de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a015-124">When a user pins your app's messaging extension.</span></span>

<span data-ttu-id="3a015-125">El icono debe ser de 32x32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="3a015-125">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="3a015-126">Puede ser blanco con un fondo transparente o transparente con un fondo blanco (no se permiten otros colores).</span><span class="sxs-lookup"><span data-stu-id="3a015-126">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="3a015-127">El icono de contorno no debe tener ningún relleno adicional alrededor del símbolo.</span><span class="sxs-lookup"><span data-stu-id="3a015-127">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams guía de diseño de iconos de contorno." border="false":::

### <a name="best-practices"></a><span data-ttu-id="3a015-129">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="3a015-129">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Ilustración que muestra cómo diseñar los iconos de la aplicación." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="3a015-131">Hacer: Siga las directrices precisas del icono de contorno</span><span class="sxs-lookup"><span data-stu-id="3a015-131">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="3a015-132">Los valores RGB de blanco utilizados en el icono deben ser Rojo: 255, Verde: 255, Azul: 255.</span><span class="sxs-lookup"><span data-stu-id="3a015-132">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="3a015-133">Todas las demás partes del icono de contorno deben ser totalmente transparentes, con el canal alfa establecido en 0.</span><span class="sxs-lookup"><span data-stu-id="3a015-133">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Ilustración que muestra cómo no diseñar los iconos de la aplicación." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="3a015-135">No: Recortar en forma cuadrada circular o redondeada</span><span class="sxs-lookup"><span data-stu-id="3a015-135">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="3a015-136">El icono de color enviado en el paquete de la aplicación debe ser cuadrado.</span><span class="sxs-lookup"><span data-stu-id="3a015-136">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="3a015-137">No redondees las esquinas de tu icono.</span><span class="sxs-lookup"><span data-stu-id="3a015-137">Don’t round the corners of your icon.</span></span> <span data-ttu-id="3a015-138">Teams ajusta automáticamente el radio de esquina.</span><span class="sxs-lookup"><span data-stu-id="3a015-138">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a><span data-ttu-id="3a015-139">No: Copiar otras marcas</span><span class="sxs-lookup"><span data-stu-id="3a015-139">Don't: Copy other brands</span></span>

<span data-ttu-id="3a015-140">Sus iconos no deben imitar ningún producto protegido por derechos de autor que no posea.</span><span class="sxs-lookup"><span data-stu-id="3a015-140">Your icons must not mimic any copyrighted products that you don't own.</span></span> <span data-ttu-id="3a015-141">Por ejemplo, un diseño similar a un producto o marca de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3a015-141">For example, a design similar to a Microsoft product or brand.</span></span>

### <a name="examples"></a><span data-ttu-id="3a015-142">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="3a015-142">Examples</span></span>

<span data-ttu-id="3a015-143">Así es como aparecen los iconos de la aplicación en diferentes capacidades y contextos de Teams.</span><span class="sxs-lookup"><span data-stu-id="3a015-143">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="3a015-144">Aplicación personal</span><span class="sxs-lookup"><span data-stu-id="3a015-144">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Ejemplo que muestra cómo se ve un icono de aplicación en una aplicación personal." border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="3a015-146">Bot (canal)</span><span class="sxs-lookup"><span data-stu-id="3a015-146">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Ejemplo que muestra cómo se ve un icono de aplicación en un bot dentro del canal." border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="3a015-148">Extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="3a015-148">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<>de texto alternativo " border="false":::

## <a name="next-step"></a><span data-ttu-id="3a015-150">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="3a015-150">Next step</span></span>

<span data-ttu-id="3a015-151">Elige cómo planeas distribuir tu aplicación:</span><span class="sxs-lookup"><span data-stu-id="3a015-151">Choose how you plan to distribute your app:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3a015-152">Descarga tu aplicación en Teams</span><span class="sxs-lookup"><span data-stu-id="3a015-152">Sideload your app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="3a015-153">Publica tu aplicación en tu organización</span><span class="sxs-lookup"><span data-stu-id="3a015-153">Publish your app to your org</span></span>](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [<span data-ttu-id="3a015-154">Publica tu aplicación en la tienda</span><span class="sxs-lookup"><span data-stu-id="3a015-154">Publish your app to the store</span></span>](~/concepts/deploy-and-publish/appsource/publish.md)
