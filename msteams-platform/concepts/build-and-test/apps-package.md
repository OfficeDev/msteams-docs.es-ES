---
title: Empaquetar la aplicación
description: Obtenga información sobre cómo empaquetar la aplicación para probarla, cargarla y publicarla en Microsoft Teams.
keywords: empaquetado de aplicaciones de Microsoft Teams
ms.topic: conceptual
ms.openlocfilehash: 66131f37f9f68c8fd54412d41068f6124da94453
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2020
ms.locfileid: "44801546"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="3c6fb-104">Crear un paquete de aplicación para la aplicación de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3c6fb-104">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="3c6fb-105">Las aplicaciones en Teams se definen mediante un archivo JSON del manifiesto de la aplicación y se incluyen en un paquete de la aplicación con sus iconos.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-105">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="3c6fb-106">Necesitará un paquete de aplicaciones para cargar e instalar la aplicación en Teams, y para publicar en el catálogo de aplicaciones de línea de negocio o en AppSource.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-106">You'll need an app package to upload and install your app in Teams, and to publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="3c6fb-107">Un paquete de la aplicación Teams es un archivo. zip que contiene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3c6fb-107">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="3c6fb-108">Un archivo de manifiesto denominado "manifest.json", que especifica los atributos de la aplicación y apunta a los recursos necesarios para su experiencia, como la ubicación de la página de configuración de la pestaña o el identificador de aplicación de Microsoft para su bot.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-108">A manifest file named "manifest.json", which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="3c6fb-109">Un icono de "esquema" transparente y un icono completo de "color".</span><span class="sxs-lookup"><span data-stu-id="3c6fb-109">A transparent "outline" icon and a full "color" icon.</span></span> <span data-ttu-id="3c6fb-110">Vea los [iconos](#icons) más adelante en este tema para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-110">See [Icons](#icons) later in this topic for more information.</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="3c6fb-111">Creación de un manifiesto</span><span class="sxs-lookup"><span data-stu-id="3c6fb-111">Creating a manifest</span></span>

<span data-ttu-id="3c6fb-112">*Teams App Studio* puede ayudarle a configurar el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-112">*Teams App Studio* can help configure your manifest.</span></span> <span data-ttu-id="3c6fb-113">También contiene una biblioteca de control React y ejemplos configurables para tarjetas.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-113">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="3c6fb-114">Consulte [Introducción a App Studio](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3c6fb-114">See [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="3c6fb-115">El archivo de manifiesto debe tener el nombre "manifest.json" y estar en el nivel superior del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-115">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="3c6fb-116">Tenga en cuenta que los manifiestos y paquetes creados anteriormente podrían admitir una versión anterior del esquema.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-116">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="3c6fb-117">Para las aplicaciones de Teams y el envío de AppSource (anteriormente tienda Office), debe usar el [esquema del manifiesto](~/resources/schema/manifest-schema.md)actual.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-117">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="3c6fb-118">Especifique el esquema al principio del manifiesto para habilitar IntelliSense o compatibilidad similar desde el editor de código:</span><span class="sxs-lookup"><span data-stu-id="3c6fb-118">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`

## <a name="icons"></a><span data-ttu-id="3c6fb-119">Iconos</span><span class="sxs-lookup"><span data-stu-id="3c6fb-119">Icons</span></span>

> [!Note]
> <span data-ttu-id="3c6fb-120">Si la aplicación contiene un bot o una extensión de mensajería, los iconos usados serán los iconos cargados en el registro de bot en el marco de robots.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-120">If your app contains a bot or messaging extension, the icons used will be the icons uploaded to your bot registration in the Bot Framework.</span></span>

<span data-ttu-id="3c6fb-121">Microsoft Teams requiere dos iconos para la experiencia de la aplicación, que se usarán en el producto.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-121">Microsoft Teams requires two icons for your app experience, to be used within the product.</span></span> <span data-ttu-id="3c6fb-122">Los iconos deben incluirse en el paquete y se hace referencia a ellos mediante rutas relativas en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-122">Icons must be included in the package and referenced via relative paths in the manifest.</span></span> <span data-ttu-id="3c6fb-123">La longitud máxima de cada ruta de acceso es de 2048 bytes y el formato del icono es. png.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-123">The maximum length of each path is 2048 bytes, and the format of the icon is .png.</span></span>

### <a name="color"></a><span data-ttu-id="3c6fb-124">color</span><span class="sxs-lookup"><span data-stu-id="3c6fb-124">color</span></span>

<span data-ttu-id="3c6fb-125">El `color` icono se usa en todo Microsoft Teams (en galerías de aplicaciones y pestañas, bots, controles flotantes, etc.).</span><span class="sxs-lookup"><span data-stu-id="3c6fb-125">The `color` icon is used throughout Microsoft Teams (in app and tab galleries, bots, flyouts, and so on).</span></span> <span data-ttu-id="3c6fb-126">Este icono debe ser de 192x192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-126">This icon should be 192x192 pixels.</span></span> <span data-ttu-id="3c6fb-127">El icono puede tener cualquier color (o colores), pero el fondo debe ser el color de énfasis de la marca.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-127">Your icon can be any color (or colors), but the background should be your branded accent color.</span></span> <span data-ttu-id="3c6fb-128">También debe tener una pequeña cantidad de espacio alrededor del icono para acomodar el recorte hexagonal para la versión del bot del icono.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-128">It should also have a small amount of padding surrounding the icon to accommodate the hexagonal cropping for the bot version of the icon.</span></span>

### <a name="outline"></a><span data-ttu-id="3c6fb-129">outline</span><span class="sxs-lookup"><span data-stu-id="3c6fb-129">outline</span></span>

<span data-ttu-id="3c6fb-130">El `outline` icono se usa en estos lugares: la barra de la aplicación y las extensiones de mensajería que el usuario ha marcado como "favorito".</span><span class="sxs-lookup"><span data-stu-id="3c6fb-130">The `outline` icon is used in these places: the app bar and messaging extensions the user has marked as a "favorite."</span></span> <span data-ttu-id="3c6fb-131">Este icono debe ser de 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-131">This icon must be 32x32 pixels.</span></span> <span data-ttu-id="3c6fb-132">El icono del esquema solo debe contener blanco y transparencia (sin otros colores).</span><span class="sxs-lookup"><span data-stu-id="3c6fb-132">Your outline icon must contain only white and transparency (no other colors).</span></span> <span data-ttu-id="3c6fb-133">El icono puede ser blanco con fondo transparente o transparente con un fondo blanco.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-133">The icon can be white with transparent background or transparent with a white background.</span></span> <span data-ttu-id="3c6fb-134">El icono de esquema no debe tener espaciado adicional alrededor del icono y debe estar tan bien recortado como sea posible y mantener al mismo tiempo las dimensiones 32x32.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-134">The outline icon should not have extra padding surrounding the icon and should be as tightly cropped as possible while still maintaining the 32x32 dimensions.</span></span> <span data-ttu-id="3c6fb-135">Estos son algunos ejemplos buenos:</span><span class="sxs-lookup"><span data-stu-id="3c6fb-135">Here are a few good examples:</span></span>

![Iconos de esquema de ejemplo](~/assets/images/icons/sample20x20s.png)

<span data-ttu-id="3c6fb-137">Por ejemplo, supongamos que su compañía es contoso.</span><span class="sxs-lookup"><span data-stu-id="3c6fb-137">For example, say your company is Contoso.</span></span> <span data-ttu-id="3c6fb-138">Debe enviar dos iconos:</span><span class="sxs-lookup"><span data-stu-id="3c6fb-138">You'd submit two icons:</span></span>

![Escaparate de iconos](~/assets/images/framework/framework_submit_icon.png)

<span data-ttu-id="3c6fb-140">Esta es la forma en que los iconos aparecerán en la interfaz de usuario:</span><span class="sxs-lookup"><span data-stu-id="3c6fb-140">Here's how the icons would appear in the UI:</span></span>

#### <a name="bot-and-chiclet-in-channel-view"></a><span data-ttu-id="3c6fb-141">Bot y chiclet en la vista de canal</span><span class="sxs-lookup"><span data-stu-id="3c6fb-141">Bot and chiclet in Channel view</span></span>

![Bot y chiclet UX](~/assets/images/icons/botandchiclet.png)

#### <a name="flyout"></a><span data-ttu-id="3c6fb-143">Flotante</span><span class="sxs-lookup"><span data-stu-id="3c6fb-143">Flyout</span></span>

![Ejemplos de iconos de Contoso](~/assets/images/icons/flyout.png)

#### <a name="app-bar-and-home-screen"></a><span data-ttu-id="3c6fb-145">Barra de la aplicación y pantalla de inicio</span><span class="sxs-lookup"><span data-stu-id="3c6fb-145">App bar and home screen</span></span>

![Ejemplos de iconos de Contoso](~/assets/images/icons/appbarhomescreen.png)
