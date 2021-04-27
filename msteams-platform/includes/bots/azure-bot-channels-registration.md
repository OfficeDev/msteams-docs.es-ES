---
title: Registro del canal de bot de Azure
description: describe los canales de bot de Azure para el registro
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta12
ms.openlocfilehash: 3cbbd204daf98f1c3528dcb6efcfde299a402912
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020952"
---
1. <span data-ttu-id="0cb81-103">En [Azure Portal](https://ms.portal.azure.com/#home), en Servicios de Azure, seleccione **Crear un recurso**.</span><span class="sxs-lookup"><span data-stu-id="0cb81-103">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select **Create a resource**.</span></span>
1. <span data-ttu-id="0cb81-104">En el cuadro de búsqueda, escriba "bot".</span><span class="sxs-lookup"><span data-stu-id="0cb81-104">In the search box enter "bot".</span></span> <span data-ttu-id="0cb81-105">Y en la lista desplegable, seleccione **Registro de canales de bot.**</span><span class="sxs-lookup"><span data-stu-id="0cb81-105">And in the drop-down list, select **Bot Channels Registration**.</span></span>
1. <span data-ttu-id="0cb81-106">Seleccione el **botón** Crear.</span><span class="sxs-lookup"><span data-stu-id="0cb81-106">Select the **Create** button.</span></span>
1. <span data-ttu-id="0cb81-107">En la **hoja Registro del canal bot,** proporcione la información solicitada sobre el bot.</span><span class="sxs-lookup"><span data-stu-id="0cb81-107">In the **Bot Channel Registration** blade, provide the requested information about your bot.</span></span>
1. <span data-ttu-id="0cb81-108">Deje el **cuadro Punto de conexión** de mensajería vacío por ahora, escribirá la dirección URL necesaria después de implementar el bot.</span><span class="sxs-lookup"><span data-stu-id="0cb81-108">Leave the **Messaging endpoint** box empty for now, you will enter the required URL after deploying the bot.</span></span> <span data-ttu-id="0cb81-109">En la siguiente imagen se muestra un ejemplo de la configuración de registro:</span><span class="sxs-lookup"><span data-stu-id="0cb81-109">The following picture shows an example of the registration settings:</span></span>

    ![Registro de canales de aplicación bot](../../assets/images/authentication/auth-bot-channels-registration.png)

1. <span data-ttu-id="0cb81-111">Haga clic **en Id. de aplicación y contraseña** de Microsoft **y, a continuación, cree nuevo**.</span><span class="sxs-lookup"><span data-stu-id="0cb81-111">Click **Microsoft App ID and password** and then **Create New**.</span></span>

    <span data-ttu-id="0cb81-112">![Crear id. de aplicación de Microsoft ](../../assets/images/authentication/CreateMicrosoftAppID.png) ![ Crear nuevo id. de aplicación de Microsoft](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span><span class="sxs-lookup"><span data-stu-id="0cb81-112">![Create Microsoft App ID](../../assets/images/authentication/CreateMicrosoftAppID.png) ![Create New Microsoft App ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span></span>    

1. <span data-ttu-id="0cb81-113">Haz **clic en Crear id. de aplicación en el vínculo Portal de registro de** aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0cb81-113">Click **Create App ID in the App Registration Portal** link.</span></span>

   ![Registros de aplicaciones](../../assets/images/authentication/AppRegistration.png)
   
1. <span data-ttu-id="0cb81-115">En la ventana **de registro de aplicaciones mostrada,** haga clic en la pestaña Nuevo **registro** de la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="0cb81-115">In the displayed **App registration** window, click the **New registration** tab in the upper left.</span></span>
1. <span data-ttu-id="0cb81-116">Escriba el nombre de la aplicación bot que está registrando, hemos usado *BotTeamsAuth* (necesita seleccionar su propio nombre único).</span><span class="sxs-lookup"><span data-stu-id="0cb81-116">Enter the name of the bot application you are registering, we used *BotTeamsAuth* (you need to select your own unique name).</span></span>
1. <span data-ttu-id="0cb81-117">Para los tipos de cuentas **compatibles,** seleccione Cuentas en cualquier directorio de la organización (cualquier directorio de Azure AD - Multitenant) y cuentas personales de *Microsoft (por ejemplo, Skype, Xbox).*</span><span class="sxs-lookup"><span data-stu-id="0cb81-117">For the **Supported account types** select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
1. <span data-ttu-id="0cb81-118">Haga clic en **el botón** Registrar.</span><span class="sxs-lookup"><span data-stu-id="0cb81-118">Click the **Register** button.</span></span> <span data-ttu-id="0cb81-119">Una vez completada, Azure muestra la *página Información* general de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0cb81-119">Once completed, Azure displays the *Overview* page for the application.</span></span>
1. <span data-ttu-id="0cb81-120">Copie y guarde en un archivo el valor del identificador de aplicación **(cliente).**</span><span class="sxs-lookup"><span data-stu-id="0cb81-120">Copy and save to a file the **Application (client) ID** value.</span></span>
1. <span data-ttu-id="0cb81-121">En el panel izquierdo, haga clic **en Certificado y secretos**.</span><span class="sxs-lookup"><span data-stu-id="0cb81-121">In the left panel, click **Certificate and secrets**.</span></span>
    1. <span data-ttu-id="0cb81-122">En *Secretos de cliente,* haga clic **en Nuevo secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="0cb81-122">Under *Client secrets*, click **New client secret**.</span></span>
    1. <span data-ttu-id="0cb81-123">Agrega una descripción para identificar este secreto de otros usuarios que podrías necesitar crear para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="0cb81-123">Add a description to identify this secret from others you might need to create for this app.</span></span>
    1. <span data-ttu-id="0cb81-124">Establece *Expira en* la selección.</span><span class="sxs-lookup"><span data-stu-id="0cb81-124">Set *Expires* to your selection.</span></span>
    1. <span data-ttu-id="0cb81-125">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0cb81-125">Click **Add**.</span></span>
    1. <span data-ttu-id="0cb81-126">Copie el secreto de cliente y guárdelo en un archivo.</span><span class="sxs-lookup"><span data-stu-id="0cb81-126">Copy the client secret and save it to a file.</span></span>
1. <span data-ttu-id="0cb81-127">Vuelva a la ventana **Registro** del canal bot  y copie el *identificador* de aplicación y el secreto de cliente en los cuadros **Id.** de aplicación de Microsoft y **Contraseña,** respectivamente.</span><span class="sxs-lookup"><span data-stu-id="0cb81-127">Go back to the **Bot Channel Registration** window and copy the *App ID* and the *Client secret* in the **Microsoft App ID** and **Password** boxes, respectively.</span></span>
1. <span data-ttu-id="0cb81-128">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0cb81-128">Click **OK**.</span></span>
1. <span data-ttu-id="0cb81-129">Por último, haga clic **en Crear**.</span><span class="sxs-lookup"><span data-stu-id="0cb81-129">Finally, click **Create**.</span></span>

<span data-ttu-id="0cb81-130">Después de que Azure haya creado el recurso de registro, se incluirá en la lista de grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="0cb81-130">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![Grupo de registro de canales de aplicación bot](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

<span data-ttu-id="0cb81-132">Una vez creado el registro de los canales del bot, deberá habilitar el canal de Teams.</span><span class="sxs-lookup"><span data-stu-id="0cb81-132">Once your bot channels registration is created, you'll need to enable the Teams channel.</span></span>

1. <span data-ttu-id="0cb81-133">En [Azure Portal](https://ms.portal.azure.com/#home), en Servicios de Azure, seleccione el registro del **canal bot** que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="0cb81-133">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select the **Bot Channel Registration** you just created.</span></span>
1. <span data-ttu-id="0cb81-134">En el panel izquierdo, haga clic en **Canales**.</span><span class="sxs-lookup"><span data-stu-id="0cb81-134">In the left panel, click **Channels**.</span></span>
1. <span data-ttu-id="0cb81-135">Haga clic en el icono de Microsoft Teams y, a continuación, **elija Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0cb81-135">Click the Microsoft Teams icon, then choose **Save**.</span></span>
