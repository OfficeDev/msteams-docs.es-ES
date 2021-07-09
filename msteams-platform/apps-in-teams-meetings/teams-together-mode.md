---
title: Escenas personalizadas del modo conjunto
description: Trabajar con escenas personalizadas del modo de colaboración
ms.topic: conceptual
ms.openlocfilehash: 9b65a0ff32c2f895cd0330f49d985ba48369dccf
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335378"
---
# <a name="custom-together-mode-scenes-in-teams"></a><span data-ttu-id="97932-103">Escenas personalizadas en modo conjunto en Teams</span><span class="sxs-lookup"><span data-stu-id="97932-103">Custom Together Mode scenes in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="97932-104">Esta característica está disponible actualmente solo en [la versión preliminar del desarrollador](../resources/dev-preview/developer-preview-intro.md) público.</span><span class="sxs-lookup"><span data-stu-id="97932-104">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="97932-105">Las escenas personalizadas del modo junto en Microsoft Teams proporcionan un entorno de reunión envolvente y atractivo que reúne a las personas y les anima a activar su vídeo.</span><span class="sxs-lookup"><span data-stu-id="97932-105">Custom Together Mode scenes in Microsoft Teams provides an immersive and engaging meeting environment that brings people together and encourages them to turn on their video.</span></span> <span data-ttu-id="97932-106">Combina digitalmente a los participantes en una sola escena virtual y coloca sus secuencias de vídeo en puestos predefinidos diseñados y fijos por el creador de la escena.</span><span class="sxs-lookup"><span data-stu-id="97932-106">It digitally combines participants into a single virtual scene and places their video streams in pre-determined seats designed and fixed by the scene creator.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/MGsNmYKgeTA]

<span data-ttu-id="97932-107">Una escena en escenas personalizadas del Modo conjunto es un artefacto creado por el desarrollador de la escena mediante el estudio de escena de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="97932-107">A scene in custom Together Mode scenes is an artifact created by the scene developer using the Microsoft Scene studio.</span></span> <span data-ttu-id="97932-108">En una configuración de escena pensada, los participantes han designado puestos con secuencias de vídeo representados en esos puestos.</span><span class="sxs-lookup"><span data-stu-id="97932-108">In a conceived scene setting, participants have designated seats with video streams rendered in those seats.</span></span>

> [!NOTE]
> <span data-ttu-id="97932-109">Solo se recomiendan las aplicaciones de escena, ya que la experiencia de adquisición de estas aplicaciones es más sencilla.</span><span class="sxs-lookup"><span data-stu-id="97932-109">Scene only apps are recommended as the acquisition experience for such apps is more seamless.</span></span>

<span data-ttu-id="97932-110">El siguiente proceso proporciona información general para crear una aplicación de solo escena:</span><span class="sxs-lookup"><span data-stu-id="97932-110">The following process gives an overview to create a scene only app:</span></span>

:::image type="content" source="../assets/images/apps-in-meetings/create-together-mode-scene-flow.png" alt-text="Crear solo una aplicación de escena" border="false":::

> [!NOTE]
> * <span data-ttu-id="97932-112">Una única aplicación de escena sigue siendo una aplicación en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="97932-112">A scene only app is still an app in Microsoft Teams.</span></span> <span data-ttu-id="97932-113">Scene studio controla la creación de paquetes de aplicaciones en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="97932-113">The Scene studio handles the app package creation in the background.</span></span>
> * <span data-ttu-id="97932-114">Varias escenas de un único paquete de aplicación aparecen como una lista plana de escenas para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="97932-114">Multiple scenes in a single app package appear as a flat list of scenes to users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97932-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="97932-115">Prerequisites</span></span>

<span data-ttu-id="97932-116">Debe tener una comprensión básica de lo siguiente para usar escenas personalizadas del Modo conjunto:</span><span class="sxs-lookup"><span data-stu-id="97932-116">You must have a basic understanding of the following to use custom Together Mode scenes:</span></span>

* <span data-ttu-id="97932-117">Definición de escena y puestos en una escena.</span><span class="sxs-lookup"><span data-stu-id="97932-117">Definition of scene and seats in a scene.</span></span>
* <span data-ttu-id="97932-118">Tenga una cuenta de Microsoft Developer y familiarícese con Microsoft Teams [Developer Portal](../concepts/build-and-test/teams-developer-portal.md) y App Studio.</span><span class="sxs-lookup"><span data-stu-id="97932-118">Have a Microsoft Developer account and be familiar with the Microsoft Teams [Developer Portal](../concepts/build-and-test/teams-developer-portal.md) and App Studio.</span></span>
* <span data-ttu-id="97932-119">[Concepto de instalación local de la aplicación](../concepts/deploy-and-publish/apps-upload.md).</span><span class="sxs-lookup"><span data-stu-id="97932-119">[Concept of app sideloading](../concepts/deploy-and-publish/apps-upload.md).</span></span>
* <span data-ttu-id="97932-120">Asegúrese de que el administrador ha concedido permiso para **Upload una** aplicación personalizada y para seleccionar todos los filtros como parte de las directivas de configuración y reunión de la aplicación respectivamente.</span><span class="sxs-lookup"><span data-stu-id="97932-120">Ensure that the Administrator has granted permission to **Upload a custom app** and to select all filters as part of App Setup and Meeting policies respectively.</span></span>

## <a name="best-practices"></a><span data-ttu-id="97932-121">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="97932-121">Best practices</span></span>

<span data-ttu-id="97932-122">Antes de crear una escena, tenga en cuenta lo siguiente para tener una experiencia de creación de escena sin problemas:</span><span class="sxs-lookup"><span data-stu-id="97932-122">Prior to building a scene, consider the following to have a seamless scene building experience:</span></span>

* <span data-ttu-id="97932-123">Asegúrese de que todas las imágenes están en formato PNG.</span><span class="sxs-lookup"><span data-stu-id="97932-123">Ensure that all images are in PNG format.</span></span>
* <span data-ttu-id="97932-124">Asegúrese de que el paquete final con todas las imágenes juntas no debe superar la resolución de 1920 x 1080.</span><span class="sxs-lookup"><span data-stu-id="97932-124">Ensure that the final package with all the images put together must not exceed 1920x1080 resolution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97932-125">La resolución es un número par.</span><span class="sxs-lookup"><span data-stu-id="97932-125">The resolution is an even number.</span></span> <span data-ttu-id="97932-126">Este es un requisito para que las escenas se ilumine correctamente.</span><span class="sxs-lookup"><span data-stu-id="97932-126">This is a requirement for scenes to be lit up successfully.</span></span>

* <span data-ttu-id="97932-127">Asegúrese de que el tamaño máximo de la escena es de 10 MB.</span><span class="sxs-lookup"><span data-stu-id="97932-127">Ensure that the maximum scene size is 10 MB.</span></span>
* <span data-ttu-id="97932-128">Asegúrese de que el tamaño máximo de cada imagen es de 5 MB.</span><span class="sxs-lookup"><span data-stu-id="97932-128">Ensure that the maximum size of each image is 5 MB.</span></span>

    > [!NOTE]
    > * <span data-ttu-id="97932-129">Una escena es una colección de varias imágenes.</span><span class="sxs-lookup"><span data-stu-id="97932-129">A scene is a collection of multiple images.</span></span> <span data-ttu-id="97932-130">El límite es para cada imagen individual.</span><span class="sxs-lookup"><span data-stu-id="97932-130">The limit is for each individual image.</span></span>
    > * <span data-ttu-id="97932-131">La resolución de imagen individual también debe ser un número par.</span><span class="sxs-lookup"><span data-stu-id="97932-131">The individual image resolution must also be an even number.</span></span>
  
* <span data-ttu-id="97932-132">Asegúrese de que la **casilla Transparente** está activada si la imagen es transparente.</span><span class="sxs-lookup"><span data-stu-id="97932-132">Ensure that the **Transparent** checkbox is selected if the image is transparent.</span></span> <span data-ttu-id="97932-133">Esta casilla está disponible en el panel derecho cuando se selecciona una imagen.</span><span class="sxs-lookup"><span data-stu-id="97932-133">This checkbox is available on the right panel when an image is selected.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97932-134">Las imágenes superpuestas deben marcarse como **Transparentes** para indicar que son imágenes superpuestas en la escena.</span><span class="sxs-lookup"><span data-stu-id="97932-134">Overlapping images need to be marked as **Transparent** to indicate that they are overlapping images in the scene.</span></span>

## <a name="build-a-scene-using-the-scene-studio"></a><span data-ttu-id="97932-135">Crear una escena con scene studio</span><span class="sxs-lookup"><span data-stu-id="97932-135">Build a scene using the Scene studio</span></span>

<span data-ttu-id="97932-136">Microsoft tiene un estudio de escena que te permite crear escenas.</span><span class="sxs-lookup"><span data-stu-id="97932-136">Microsoft has a Scene studio that allows you to build scenes.</span></span> <span data-ttu-id="97932-137">Está disponible en [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).</span><span class="sxs-lookup"><span data-stu-id="97932-137">It is available on [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).</span></span>

> [!NOTE]
> <span data-ttu-id="97932-138">Este documento hace referencia a Scene studio en el Microsoft Teams Developer Portal.</span><span class="sxs-lookup"><span data-stu-id="97932-138">This document is referring to Scene studio in the Microsoft Teams Developer Portal.</span></span> <span data-ttu-id="97932-139">La interfaz y las funcionalidades son iguales en el Diseñador de escenas de App Studio.</span><span class="sxs-lookup"><span data-stu-id="97932-139">The interface and functionalities are all the same in App Studio Scene Designer.</span></span>

<span data-ttu-id="97932-140">Una escena en el contexto del estudio de escena es un artefacto que contiene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="97932-140">A scene in the context of the Scene studio is an artifact that contains the following:</span></span>

* <span data-ttu-id="97932-141">Puestos reservados para organizadores de reuniones y presentadores de reuniones.</span><span class="sxs-lookup"><span data-stu-id="97932-141">Seats reserved for meeting organizer and meeting presenters.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97932-142">El moderador no hace referencia al usuario que está compartiendo activamente.</span><span class="sxs-lookup"><span data-stu-id="97932-142">Presenter does not refer to the user who is actively sharing.</span></span> <span data-ttu-id="97932-143">Hace referencia al rol [de reunión](https://support.microsoft.com/en-us/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="97932-143">It refers to the [meeting role](https://support.microsoft.com/en-us/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

* <span data-ttu-id="97932-144">Asiento e imagen para cada participante con un ancho y alto ajustables.</span><span class="sxs-lookup"><span data-stu-id="97932-144">Seat and image for each participant with an adjustable width and height.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97932-145">PNG es el único formato compatible.</span><span class="sxs-lookup"><span data-stu-id="97932-145">PNG is the only supported format.</span></span>

* <span data-ttu-id="97932-146">Coordenadas XYZ de todos los puestos e imágenes.</span><span class="sxs-lookup"><span data-stu-id="97932-146">XYZ coordinates of all the seats and images.</span></span>
* <span data-ttu-id="97932-147">Colección de imágenes camufladas como una imagen.</span><span class="sxs-lookup"><span data-stu-id="97932-147">Collection of images that are camouflaged as one image.</span></span>

<span data-ttu-id="97932-148">Las dimensiones del asiento se convierten en el lienzo para representar la secuencia de vídeo del participante.</span><span class="sxs-lookup"><span data-stu-id="97932-148">The seat dimensions become the canvas for rendering the participant video stream.</span></span> <span data-ttu-id="97932-149">La siguiente imagen muestra cada asiento representado como un avatar para crear escenas:</span><span class="sxs-lookup"><span data-stu-id="97932-149">The following image shows each seat represented as an avatar for building scenes:</span></span>

![Scene studio](../assets/images/apps-in-meetings/scene-design-studio.png)

<span data-ttu-id="97932-151">**Para crear una escena con scene studio**</span><span class="sxs-lookup"><span data-stu-id="97932-151">**To build a scene using the Scene studio**</span></span>

1. <span data-ttu-id="97932-152">Vaya a [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).</span><span class="sxs-lookup"><span data-stu-id="97932-152">Go to [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).</span></span>

    >[!NOTE]
    > * <span data-ttu-id="97932-153">Para abrir Scene studio, puede navegar a la página principal de [Teams Developer Portal](https://dev.teams.microsoft.com/home) y seleccionar Crear escenas **personalizadas para reuniones.**</span><span class="sxs-lookup"><span data-stu-id="97932-153">To open Scene studio, you can navigate to the home page of [Teams Developer Portal](https://dev.teams.microsoft.com/home) and select **Create custom scenes for meetings**.</span></span>
    > * <span data-ttu-id="97932-154">Para abrir Scene studio, puedes navegar a la página principal de [Teams Developer Portal, seleccionar](https://dev.teams.microsoft.com/home) **Herramientas** en la sección izquierda y seleccionar **Scene studio** en la sección **Herramientas.**</span><span class="sxs-lookup"><span data-stu-id="97932-154">To open Scene studio, you can navigate to the home page of [Teams Developer Portal](https://dev.teams.microsoft.com/home), select **Tools** from the left hand section, and select **Scene studio** from the **Tools** section.</span></span>

1. <span data-ttu-id="97932-155">En la **página Editor de** escenas, seleccione Crear una nueva **escena.**</span><span class="sxs-lookup"><span data-stu-id="97932-155">In the **Scenes Editor** page, select **Create a new scene**.</span></span>

1. <span data-ttu-id="97932-156">En el **cuadro Escena,** escriba un nombre para la escena.</span><span class="sxs-lookup"><span data-stu-id="97932-156">In the **Scene** box, enter a name for the scene.</span></span>

    >[!NOTE]
    > * <span data-ttu-id="97932-157">Puede seleccionar Cerrar **para alternar** entre cerrar o volver a abrir el panel derecho.</span><span class="sxs-lookup"><span data-stu-id="97932-157">You can select **Close** to toggle between closing or reopening the right pane.</span></span>
    > * <span data-ttu-id="97932-158">Puedes acercar o alejar la escena con la barra de zoom para obtener una mejor vista de la escena.</span><span class="sxs-lookup"><span data-stu-id="97932-158">You can zoom in or zoom out of the scene using the zoom bar for a better view of the scene.</span></span>

1. <span data-ttu-id="97932-159">Arrastre y coloque la imagen en el entorno tal como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="97932-159">Drag and drop the image into the environment as displayed in the following image:</span></span>

    >[!NOTE]
    > * <span data-ttu-id="97932-160">Puede descargar los archivos [SampleScene.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip) [ ySampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) con las imágenes.</span><span class="sxs-lookup"><span data-stu-id="97932-160">You can download the [SampleScene.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip) and [SampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) files with the images.</span></span>
    > * <span data-ttu-id="97932-161">Como alternativa, puede agregar imágenes de fondo a la escena mediante **Agregar imágenes**.</span><span class="sxs-lookup"><span data-stu-id="97932-161">Alternately, you can add background images to the scene using **Add images**.</span></span>

    ![Arrastrar a la escena](../assets/images/apps-in-meetings/drag-and-drop-scene.png)

1. <span data-ttu-id="97932-163">Seleccione la imagen que ha colocado.</span><span class="sxs-lookup"><span data-stu-id="97932-163">Select the image that you have placed.</span></span>

1. <span data-ttu-id="97932-164">En el panel derecho, seleccione una alineación para la imagen o use el control deslizante **Cambiar** tamaño para ajustar el tamaño de la imagen.</span><span class="sxs-lookup"><span data-stu-id="97932-164">From the right pane, select an alignment for the image or use the **Resize** slider to adjust the image size.</span></span>

    ![Alineación de imágenes](../assets/images/apps-in-meetings/image-alignment.png)

1. <span data-ttu-id="97932-166">Seleccione un área fuera de la imagen.</span><span class="sxs-lookup"><span data-stu-id="97932-166">Select an area outside of the image.</span></span>

1. <span data-ttu-id="97932-167">En la esquina superior derecha, seleccione **Participantes en** **Capas**.</span><span class="sxs-lookup"><span data-stu-id="97932-167">In the upper-right corner, select **Participants** under **Layers**.</span></span>

1. <span data-ttu-id="97932-168">Seleccione el número de participantes para la escena en el cuadro Número de **participantes** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="97932-168">Select the number of participants for the scene from the **Number of participants** box, and select **Add**.</span></span>

    >[!NOTE]
    > * <span data-ttu-id="97932-169">Después de enviar la escena, las ubicaciones de avatar se reemplazan por secuencias de vídeo del participante real.</span><span class="sxs-lookup"><span data-stu-id="97932-169">After the scene is shipped, the avatar placements are replaced with actual participant's video streams.</span></span>
    > * <span data-ttu-id="97932-170">Puede arrastrar las imágenes de los participantes alrededor de la escena y colocarlas en la posición necesaria y cambiar su tamaño mediante la flecha de cambio de tamaño.</span><span class="sxs-lookup"><span data-stu-id="97932-170">You can drag the participant images around the scene and place them in the required position and resize them using the resize arrow.</span></span>

1. <span data-ttu-id="97932-171">Seleccione cualquier imagen de participante y active la casilla **Asignar mancha** para asignar la mancha al participante.</span><span class="sxs-lookup"><span data-stu-id="97932-171">Select any participant image, and select the **Assign Spot** check box to assign the spot to the participant.</span></span>

1. <span data-ttu-id="97932-172">Seleccione **Organizador de reuniones** o Rol de **moderador** para el participante.</span><span class="sxs-lookup"><span data-stu-id="97932-172">Select **Meeting Organizer** or **Presenter** role for the participant.</span></span>

    >[!NOTE]
    > <span data-ttu-id="97932-173">En una reunión, se debe asignar a un participante el rol de organizador de la reunión.</span><span class="sxs-lookup"><span data-stu-id="97932-173">In a meeting, one participant must be assigned the role of a meeting organizer.</span></span>

    ![Asignar spot](../assets/images/apps-in-meetings/assign-spot.png)

1. <span data-ttu-id="97932-175">Seleccione **Guardar** y **seleccione Ver en Teams** para probar rápidamente la escena en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="97932-175">Select **Save** and select **View in Teams** to quickly test your scene in Microsoft Teams.</span></span>

    >[!NOTE]
    > <span data-ttu-id="97932-176">Para eliminar una escena que creaste, **selecciona Eliminar escena** en la barra superior.</span><span class="sxs-lookup"><span data-stu-id="97932-176">To delete a scene you created, select **Delete scene** on the top bar.</span></span>

1. <span data-ttu-id="97932-177">En el **cuadro de diálogo Ver en Teams,** seleccione Vista previa en **Teams**.</span><span class="sxs-lookup"><span data-stu-id="97932-177">In the **View in Teams** dialog box, select **Preview in Teams**.</span></span>
1. <span data-ttu-id="97932-178">En el cuadro de diálogo que aparece, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="97932-178">In the dialog box that appears, select **Add**.</span></span>

    <span data-ttu-id="97932-179">Se puede probar o acceder a la escena mediante la creación de una reunión de prueba y el inicio de escenas personalizadas del Modo conjunto.</span><span class="sxs-lookup"><span data-stu-id="97932-179">The scene can be tested or accessed by creating a test meeting and launching custom Together Mode scenes.</span></span> <span data-ttu-id="97932-180">Para obtener más información, vea [Activar escenas personalizadas del modo conjunto](#activate-custom-together-mode-scenes).</span><span class="sxs-lookup"><span data-stu-id="97932-180">For more information, see [activate custom Together Mode scenes](#activate-custom-together-mode-scenes).</span></span>

    ![Iniciar escenas personalizadas del modo conjunto](../assets/images/apps-in-meetings/launchtogethermode.png)

    >[!NOTE]
    > * <span data-ttu-id="97932-182">Al seleccionar **Vista** previa, se crea automáticamente Microsoft Teams aplicación  que se puede ver en la página Aplicaciones del portal Teams desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="97932-182">Selecting **Preview** automatically creates a Microsoft Teams app that can be viewed in the **Apps** page in the Teams Developer Portal.</span></span>
    > * <span data-ttu-id="97932-183">Al seleccionar **Vista** previa, se crea automáticamente un paquete de aplicación appmanifest.jsdetrás de la escena.</span><span class="sxs-lookup"><span data-stu-id="97932-183">Selecting **Preview** automatically creates an app package that is appmanifest.json behind the scene.</span></span> <span data-ttu-id="97932-184">Como se mencionó anteriormente, esto se abstrae, pero puedes acceder al paquete de la aplicación creado automáticamente navegando a **Aplicaciones** desde el menú.</span><span class="sxs-lookup"><span data-stu-id="97932-184">As stated earlier, this is abstracted, but you can access the automatically created app package by navigating to **Apps** from the menu.</span></span>
    > * <span data-ttu-id="97932-185">A continuación, la escena se puede ver en la galería de escenas del modo conjunto personalizada.</span><span class="sxs-lookup"><span data-stu-id="97932-185">The scene can then be viewed in the custom Together Mode scenes gallery.</span></span>

1. <span data-ttu-id="97932-186">Opcionalmente, puedes seleccionar **Compartir** en el menú desplegable Guardar para crear un vínculo que se pueda compartir para distribuir fácilmente las escenas para que otras personas las usen. </span><span class="sxs-lookup"><span data-stu-id="97932-186">Optionally, you can select **Share** from the **Save** drop-down menu to create a shareable link to easily distribute your scenes for others to use.</span></span> <span data-ttu-id="97932-187">Al abrir este vínculo, se instala la escena para el usuario y pueden empezar a usarlo.</span><span class="sxs-lookup"><span data-stu-id="97932-187">Opening this link installs the scene for the user and they can start using it.</span></span>

1. <span data-ttu-id="97932-188">Después de la vista previa, la escena se puede enviar como una aplicación a Teams siguiendo los pasos para el envío de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="97932-188">After preview, the scene can be shipped as an app to Teams by following the steps for app submission.</span></span>

    >[!NOTE]
    > <span data-ttu-id="97932-189">Este paso requiere el paquete de la aplicación que es diferente del paquete de escena, para la escena que se diseñó.</span><span class="sxs-lookup"><span data-stu-id="97932-189">This step requires the app package that is different from the scene package, for the scene that was designed.</span></span> <span data-ttu-id="97932-190">El paquete de la aplicación creado automáticamente se puede encontrar en la **sección Aplicaciones** del Centro Teams desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="97932-190">The app package created automatically can be found in the **Apps** section in the Teams Developer Center.</span></span>

1. <span data-ttu-id="97932-191">Opcionalmente, el paquete de escena se puede recuperar **seleccionando Exportar** en el **menú** desplegable Guardar.</span><span class="sxs-lookup"><span data-stu-id="97932-191">Optionally, the scene package can be retrieved by selecting **Export** from the **Save** drop-down menu.</span></span> <span data-ttu-id="97932-192">Se .zip un archivo de .zip, es decir, el paquete de escena.</span><span class="sxs-lookup"><span data-stu-id="97932-192">A .zip file, that is the scene package, is downloaded.</span></span>

    ![Exportar una escena](../assets/images/apps-in-meetings/build-a-scene.png)

    >[!NOTE]
    > <span data-ttu-id="97932-194">El paquete de escena consta de un scene.jsactivo y los activos PNG usados para crear una escena.</span><span class="sxs-lookup"><span data-stu-id="97932-194">Scene package comprises of a scene.json and the PNG assets used to build a scene.</span></span> <span data-ttu-id="97932-195">El paquete de escena se puede revisar para incorporar otros cambios como se describe en la sección Ejemplo scene.jssección de este documento.</span><span class="sxs-lookup"><span data-stu-id="97932-195">The scene package can be reviewed for incorporating other changes as described in the Sample scene.json section of this document.</span></span>

<span data-ttu-id="97932-196">Una escena más compleja que aprovecha el eje Z se muestra en la muestra de introducción paso a paso.</span><span class="sxs-lookup"><span data-stu-id="97932-196">A more complex scene that leverages the Z-axis is demonstrated in the step-by-step getting started sample.</span></span>

## <a name="sample-scenejson"></a><span data-ttu-id="97932-197">Ejemplo scene.jsen</span><span class="sxs-lookup"><span data-stu-id="97932-197">Sample scene.json</span></span>

<span data-ttu-id="97932-198">Scene.jsjunto con las imágenes indican la posición exacta de los puestos.</span><span class="sxs-lookup"><span data-stu-id="97932-198">Scene.json along with the images indicate the exact position of the seats.</span></span> <span data-ttu-id="97932-199">Una escena consta de imágenes de mapa de bits, sprites y rectángulos para colocar los vídeos de los participantes.</span><span class="sxs-lookup"><span data-stu-id="97932-199">A scene consists of bitmap images, sprites, and rectangles to put participant videos in.</span></span> <span data-ttu-id="97932-200">Estos sprites y cuadros de participantes se definen en un sistema de coordenadas mundiales con el eje X apuntando a la derecha y el eje Y apuntando hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="97932-200">These sprites and participant boxes are defined in a world coordinate system with the X-axis pointing to the right and the Y-axis pointing downwards.</span></span> <span data-ttu-id="97932-201">Las escenas del Modo conjunto personalizado admiten acercamiento a los participantes actuales.</span><span class="sxs-lookup"><span data-stu-id="97932-201">Custom Together Mode scenes supports zooming in on the current participants.</span></span> <span data-ttu-id="97932-202">Esto es útil para reuniones pequeñas en una escena grande.</span><span class="sxs-lookup"><span data-stu-id="97932-202">This is helpful for small meetings in a large scene.</span></span> <span data-ttu-id="97932-203">Un sprite es una imagen de mapa de bits estática posicionada en el mundo.</span><span class="sxs-lookup"><span data-stu-id="97932-203">A sprite is a static bitmap image positioned in the world.</span></span> <span data-ttu-id="97932-204">El valor Z del sprite determina la posición del sprite.</span><span class="sxs-lookup"><span data-stu-id="97932-204">The Z value of the sprite determines the position of the sprite.</span></span> <span data-ttu-id="97932-205">La representación comienza con el sprite con el valor Z más bajo, por lo que un valor Z más alto significa que está más cerca de la cámara.</span><span class="sxs-lookup"><span data-stu-id="97932-205">Rendering starts with the sprite with lowest Z value, so higher Z value means it is closer to the camera.</span></span> <span data-ttu-id="97932-206">Cada participante tiene su propia fuente de vídeo, que se segmenta para que solo se represente el primer plano.</span><span class="sxs-lookup"><span data-stu-id="97932-206">Each participant has its own video feed, which is segmented so that only the foreground is rendered.</span></span>

<span data-ttu-id="97932-207">A continuación se muestra scene.jsejemplo:</span><span class="sxs-lookup"><span data-stu-id="97932-207">Following is the scene.json sample:</span></span>

```json
{
   "protocolVersion": "1.0",
   "id": "A",
   "autoZoom": true,
   "mirrorParticipants ": true,
   "extent":{
      "left":0.0,
      "top":0.0,
      "width":16.0,
      "height":9.0
   },
   "sprites":[
      {
         "filename":"background.png",
         "cx":8.0,
         "cy":4.5,
         "width":16.0,
         "height":9.0,
         "zOrder":0.0,
   "isAlpha":false
      },
      {
         "filename":"table.png",
         "cx":8.0,
         "cy":7.0,
         "width":12.0,
         "height":4.0,
         "zOrder":3.0,
   "isAlpha":true
      },
      {
         "filename":"row0.png",
         "cx":12.0,
         "cy":15.0,
         "width":8.0,
         "height":4.0,
         "zOrder":2.0,
   "isAlpha":true
      }

   ],
   "participants":[
      {
         "cx":5.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":0
      },
      {
         "cx":11.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":1
      }
   ]
}
```

<span data-ttu-id="97932-208">Cada escena tiene un identificador y un nombre únicos.</span><span class="sxs-lookup"><span data-stu-id="97932-208">Each scene has a unique ID and name.</span></span> <span data-ttu-id="97932-209">El JSON de la escena también contiene información sobre todos los activos usados para la escena.</span><span class="sxs-lookup"><span data-stu-id="97932-209">The scene JSON also contains information on all the assets used for the scene.</span></span> <span data-ttu-id="97932-210">Cada activo contiene un nombre de archivo, ancho, alto y posición en el eje X e Y.</span><span class="sxs-lookup"><span data-stu-id="97932-210">Each asset contains a filename, width, height, and position on the X and Y-axis.</span></span> <span data-ttu-id="97932-211">Del mismo modo, cada asiento contiene un identificador de asiento, ancho, alto y posición en los ejes X e Y.</span><span class="sxs-lookup"><span data-stu-id="97932-211">Similarly, each seat contains a seat ID, width, height, and position on the X and Y-axis.</span></span> <span data-ttu-id="97932-212">El orden de asientos se genera automáticamente y se puede modificar según las preferencias.</span><span class="sxs-lookup"><span data-stu-id="97932-212">The seating order is generated automatically and can be altered as per preference.</span></span>

> [!NOTE]
> <span data-ttu-id="97932-213">El número de pedido de asientos corresponde al orden de las personas que se unen a la llamada.</span><span class="sxs-lookup"><span data-stu-id="97932-213">Seating order number corresponds to the order of people joining the call.</span></span>

<span data-ttu-id="97932-214">ZOrder representa el orden de colocar imágenes y puestos a lo largo del eje Z.</span><span class="sxs-lookup"><span data-stu-id="97932-214">The zOrder represents the order of placing images and seats along the Z-axis.</span></span> <span data-ttu-id="97932-215">En muchos casos, proporciona una sensación de profundidad o partición si es necesario.</span><span class="sxs-lookup"><span data-stu-id="97932-215">In many cases, it gives a sense of depth or partition if required.</span></span> <span data-ttu-id="97932-216">Para obtener más información, consulte el ejemplo de introducción paso a paso.</span><span class="sxs-lookup"><span data-stu-id="97932-216">For more information, see the step-by-step getting started sample.</span></span> <span data-ttu-id="97932-217">El ejemplo aprovecha el zOrder.</span><span class="sxs-lookup"><span data-stu-id="97932-217">The sample leverages the zOrder.</span></span>

<span data-ttu-id="97932-218">Ahora que has pasado por el ejemplo scene.js, puedes activar las escenas personalizadas del Modo conjunto para participar en escenas.</span><span class="sxs-lookup"><span data-stu-id="97932-218">Now that you have gone through the sample scene.json, you can activate the custom Together Mode scenes to engage in scenes.</span></span>

## <a name="activate-custom-together-mode-scenes"></a><span data-ttu-id="97932-219">Activar escenas personalizadas del modo conjunto</span><span class="sxs-lookup"><span data-stu-id="97932-219">Activate custom Together Mode scenes</span></span>

<span data-ttu-id="97932-220">Obtenga información de un extremo a otro de cómo un usuario final interactúa con las escenas en escenas personalizadas del modo conjunto.</span><span class="sxs-lookup"><span data-stu-id="97932-220">Get end-to-end information of how an end user engages with scenes in custom Together Mode scenes.</span></span>

<span data-ttu-id="97932-221">**Para seleccionar escenas y activar escenas personalizadas del Modo conjunto**</span><span class="sxs-lookup"><span data-stu-id="97932-221">**To select scenes and activate custom Together Mode scenes**</span></span>

1. <span data-ttu-id="97932-222">Crear una nueva reunión de prueba.</span><span class="sxs-lookup"><span data-stu-id="97932-222">Create a new test meeting.</span></span>

    >[!NOTE]
    > <span data-ttu-id="97932-223">Al seleccionar **Vista previa** en el estudio de escena, la escena se instala como una aplicación en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="97932-223">On selecting **Preview** in the Scene studio, the scene is installed as an app in Microsoft Teams.</span></span> <span data-ttu-id="97932-224">Este es el modelo para que un desarrollador pruebe y pruebe las escenas del estudio scene.</span><span class="sxs-lookup"><span data-stu-id="97932-224">This is the model for a developer to test and try out scenes from the Scene studio.</span></span> <span data-ttu-id="97932-225">Después de que una escena se envíe como una aplicación, los usuarios verán estas escenas en la galería de escenas.</span><span class="sxs-lookup"><span data-stu-id="97932-225">After a scene is shipped as an app, users see these scenes in the scene gallery.</span></span>

1. <span data-ttu-id="97932-226">En la **lista** desplegable Galería de la esquina superior izquierda, seleccione **Modo conjunto**.</span><span class="sxs-lookup"><span data-stu-id="97932-226">From the **Gallery** drop-down in the upper-left corner, select **Together Mode**.</span></span> <span data-ttu-id="97932-227">Aparece **el cuadro de** diálogo Selector y la escena que se agrega está disponible.</span><span class="sxs-lookup"><span data-stu-id="97932-227">The **Picker** dialog box appears and the scene that is added is available.</span></span>

1. <span data-ttu-id="97932-228">Seleccione **Cambiar escena** para cambiar la escena predeterminada.</span><span class="sxs-lookup"><span data-stu-id="97932-228">Select **Change scene** to change the default scene.</span></span>

1. <span data-ttu-id="97932-229">En la **Galería de escenarios,** seleccione la escena que desea usar para la reunión.</span><span class="sxs-lookup"><span data-stu-id="97932-229">From the **Scene Gallery**, select the scene you want to use for your meeting.</span></span>

1. <span data-ttu-id="97932-230">Opcionalmente, el organizador de la reunión y el moderador pueden cambiar la escena de todos los **participantes** de la reunión.</span><span class="sxs-lookup"><span data-stu-id="97932-230">Optionally, the meeting organizer and presenter can **Change scene for all participants** in the meeting.</span></span>

    >[!NOTE]
    > <span data-ttu-id="97932-231">En cualquier momento, solo se puede usar una escena de forma homogénea para la reunión.</span><span class="sxs-lookup"><span data-stu-id="97932-231">At any point in time, only one scene can be used homogeneously for the meeting.</span></span> <span data-ttu-id="97932-232">Si un moderador u organizador cambia una escena, cambia para todos.</span><span class="sxs-lookup"><span data-stu-id="97932-232">If a presenter or organizer changes a scene, it  changes for all.</span></span> <span data-ttu-id="97932-233">El cambio de las escenas personalizadas del Modo conjunto es una función de los participantes individuales, pero mientras que en las escenas personalizadas del Modo conjunto, todos los participantes tienen la misma escena.</span><span class="sxs-lookup"><span data-stu-id="97932-233">Switching in or out of custom Together Mode scenes is up to individual participants, but while in custom Together Mode scenes, all participants have the same scene.</span></span>

1. <span data-ttu-id="97932-234">Seleccione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="97932-234">Select **Apply**.</span></span> <span data-ttu-id="97932-235">Teams instala la aplicación para el usuario y aplica la escena.</span><span class="sxs-lookup"><span data-stu-id="97932-235">Teams installs the app for the user and applies the scene.</span></span>

## <a name="open-a-custom-together-mode-scenes-scene-package"></a><span data-ttu-id="97932-236">Abrir un paquete de escenas de escenas de modo conjunto personalizado</span><span class="sxs-lookup"><span data-stu-id="97932-236">Open a custom Together Mode scenes Scene Package</span></span>

<span data-ttu-id="97932-237">Puedes compartir el paquete de escena que es un archivo .zip recuperado del estudio de escena a otros creadores para mejorar aún más la escena.</span><span class="sxs-lookup"><span data-stu-id="97932-237">You can share the Scene Package that is a .zip file retrieved from the Scene studio to other creators to further enhance the scene.</span></span> <span data-ttu-id="97932-238">Se **puede aprovechar la funcionalidad** Importar una escena.</span><span class="sxs-lookup"><span data-stu-id="97932-238">The **Import a Scene** functionality can be leveraged.</span></span> <span data-ttu-id="97932-239">Esta herramienta ayuda a desenvolver un paquete de escena para permitir al creador continuar con la creación de la escena.</span><span class="sxs-lookup"><span data-stu-id="97932-239">This tool helps unwrap a scene package to let the creator continue building the scene.</span></span>

![Archivo zip de escena](../assets/images/apps-in-meetings/scene-zip-file.png)

## <a name="see-also"></a><span data-ttu-id="97932-241">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="97932-241">See also</span></span>

[<span data-ttu-id="97932-242">Aplicaciones para Teams reuniones</span><span class="sxs-lookup"><span data-stu-id="97932-242">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)
