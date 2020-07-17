---
title: Publicación posterior
description: Qué hacer después de publicar la aplicación
keywords: certificado de actualización de publicación de publicaciones de Teams
ms.openlocfilehash: 887e18ac7e27cf12aa4319ac240e42f21f05fd75
ms.sourcegitcommit: e355f59d2d21a2d5ae36cc46acad5ed4765b42e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "45021576"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="0fc85-104">Mantener y admitir la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="0fc85-104">Maintain and support your published app</span></span> 

<span data-ttu-id="0fc85-105">Después de aprobar la aplicación y enumerarla en el catálogo de aplicaciones públicas, puede aumentar su alcance completando el programa de cumplimiento de aplicaciones de Microsoft 365 o agregando un botón Descargar en el sitio Web.</span><span class="sxs-lookup"><span data-stu-id="0fc85-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="m365-certified"></a><span data-ttu-id="0fc85-106">Certificado de M365</span><span class="sxs-lookup"><span data-stu-id="0fc85-106">M365 Certified</span></span>

<span data-ttu-id="0fc85-107">El [programa de cumplimiento de aplicaciones 365 de Microsoft](./application-certification.md)es un enfoque de tres niveles para la seguridad y el cumplimiento de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0fc85-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="0fc85-108">Cada nivel se basa en el siguiente, que ofrece un programa con capas para satisfacer las necesidades del cliente.</span><span class="sxs-lookup"><span data-stu-id="0fc85-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="0fc85-109">Puede obtener más información sobre la postura de seguridad y cumplimiento de las aplicaciones de Microsoft Teams visitando la [Página cumplimiento](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span><span class="sxs-lookup"><span data-stu-id="0fc85-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="0fc85-110">Agregar un botón Descargar al sitio del producto</span><span class="sxs-lookup"><span data-stu-id="0fc85-110">Add a download button to your product site</span></span>

<span data-ttu-id="0fc85-111">Si la aplicación está en la tienda Microsoft Teams, puede generar un vínculo para su sitio web que inicie Teams y que muestre un cuadro de diálogo de consentimiento e instalación para que los usuarios agreguen la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0fc85-111">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="0fc85-112">El formato es: `https://teams.microsoft.com/l/app/<appId>` donde appID es el GUID que declaran en el manifiesto enviado.</span><span class="sxs-lookup"><span data-stu-id="0fc85-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="0fc85-113">Ejemplo: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` es el vínculo para instalar Trello.</span><span class="sxs-lookup"><span data-stu-id="0fc85-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="0fc85-114">Actualización de la aplicación de Teams existente</span><span class="sxs-lookup"><span data-stu-id="0fc85-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="0fc85-115">No use el botón *Agregar una nueva aplicación* para volver a enviar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0fc85-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="0fc85-116">En su lugar, use el icono de la aplicación en la pestaña Información general.</span><span class="sxs-lookup"><span data-stu-id="0fc85-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="0fc85-117">El appId del manifiesto actualizado debe ser el mismo que el del manifiesto actual, con un número de versión incrementado.</span><span class="sxs-lookup"><span data-stu-id="0fc85-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="0fc85-118">Aumente el número de versión en el manifiesto si realiza cambios en el manifiesto en el envío.</span><span class="sxs-lookup"><span data-stu-id="0fc85-118">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="0fc85-119">Los envíos actualizados son necesarios para someterse a un nuevo proceso de revisión y validación.</span><span class="sxs-lookup"><span data-stu-id="0fc85-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="0fc85-120">Actualizaciones de aplicaciones y flujo de consentimiento del usuario</span><span class="sxs-lookup"><span data-stu-id="0fc85-120">App updates and the user consent flow</span></span>

<span data-ttu-id="0fc85-121">Cuando un usuario instala la aplicación, uno de los primeros elementos que conviene dar permiso a la aplicación para acceder a los servicios y la información que la aplicación necesita para realizar su trabajo.</span><span class="sxs-lookup"><span data-stu-id="0fc85-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="0fc85-122">En la mayoría de los casos, después de completar una actualización de la aplicación, la nueva versión aparecerá automáticamente para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="0fc85-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="0fc85-123">Sin embargo, hay algunas actualizaciones en el [manifiesto de la aplicación Teams](../../../../resources/schema/manifest-schema.md) que requieren la aceptación del usuario para completarse y pueden volver a desencadenar este comportamiento de consentimiento:</span><span class="sxs-lookup"><span data-stu-id="0fc85-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="0fc85-124">Se ha agregado o quitado un bot.</span><span class="sxs-lookup"><span data-stu-id="0fc85-124">A bot was added or removed.</span></span>
> * <span data-ttu-id="0fc85-125">El valor único de un bot existente `botId` cambió.</span><span class="sxs-lookup"><span data-stu-id="0fc85-125">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="0fc85-126">Se ha cambiado el valor booleano de un bot existente `isNotificationOnly` .</span><span class="sxs-lookup"><span data-stu-id="0fc85-126">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="0fc85-127">Se ha cambiado el valor booleano de un bot existente `supportsFiles` .</span><span class="sxs-lookup"><span data-stu-id="0fc85-127">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="0fc85-128">`composeExtensions`Se ha agregado o quitado una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0fc85-128">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="0fc85-129">Se ha agregado un nuevo conector.</span><span class="sxs-lookup"><span data-stu-id="0fc85-129">A new connector was added.</span></span>
> * <span data-ttu-id="0fc85-130">Se ha agregado una nueva pestaña estática/personal.</span><span class="sxs-lookup"><span data-stu-id="0fc85-130">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="0fc85-131">Se ha agregado una nueva ficha configurable de grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="0fc85-131">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="0fc85-132">Los `webApplicationInfo` valores cambiados.</span><span class="sxs-lookup"><span data-stu-id="0fc85-132">The `webApplicationInfo` values changed.</span></span>
>
