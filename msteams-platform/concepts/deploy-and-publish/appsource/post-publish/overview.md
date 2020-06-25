---
title: Publicación posterior
description: Qué hacer después de publicar la aplicación
keywords: certificado de actualización de publicación de publicaciones de Teams
ms.openlocfilehash: 77b74d77546de0ae93b0ae39aec925d2e3dec2cf
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867106"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="fcf7c-104">Mantener y admitir la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="fcf7c-104">Maintain and support your published app</span></span> 

<span data-ttu-id="fcf7c-105">Después de aprobar la aplicación y enumerarla en el catálogo de aplicaciones públicas, puede aumentar su alcance si logra la certificación de la aplicación o agrega un botón Descargar en el sitio Web.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-105">After your app is approved and listed in the public app catalog, you can increase your reach by achieving app certification, or adding a download button your website.</span></span>

## <a name="application-certificate"></a><span data-ttu-id="fcf7c-106">Certificado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="fcf7c-106">Application Certificate</span></span>

<span data-ttu-id="fcf7c-107">Microsoft proporciona un [programa de certificación de aplicaciones](./application-certification.md) que compila la información de la aplicación y la presenta en la [Página seguridad y cumplimiento de aplicaciones de Microsoft Teams](https://aka.ms/AppCertification).</span><span class="sxs-lookup"><span data-stu-id="fcf7c-107">Microsoft provides a [Application Certification program](./application-certification.md) that compiles your app information and presents it on [Microsoft Teams App Security and Compliance Page](https://aka.ms/AppCertification).</span></span> <span data-ttu-id="fcf7c-108">Esta información está destinada a ayudar a los administradores a elegir aplicaciones que sean seguras para sus organizaciones.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-108">This information is intended to help admins to choose apps that are safe for their organizations.</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="fcf7c-109">Agregar un botón Descargar al sitio del producto</span><span class="sxs-lookup"><span data-stu-id="fcf7c-109">Add a download button to your product site</span></span>

<span data-ttu-id="fcf7c-110">Si la aplicación está en la tienda Microsoft Teams, puede generar un vínculo para su sitio web que inicie Teams y que muestre un cuadro de diálogo de consentimiento e instalación para que los usuarios agreguen la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-110">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="fcf7c-111">El formato es: `https://teams.microsoft.com/l/app/<appId>` donde appID es el GUID que declaran en el manifiesto enviado.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-111">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="fcf7c-112">Ejemplo: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` es el vínculo para instalar Trello.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-112">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="fcf7c-113">Actualización de la aplicación de Teams existente</span><span class="sxs-lookup"><span data-stu-id="fcf7c-113">Updating your existing Teams app</span></span>

* <span data-ttu-id="fcf7c-114">No use el botón *Agregar una nueva aplicación* para volver a enviar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-114">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="fcf7c-115">En su lugar, use el icono de la aplicación en la pestaña Información general.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-115">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="fcf7c-116">El appId del manifiesto actualizado debe ser el mismo que el del manifiesto actual, con un número de versión incrementado.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-116">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="fcf7c-117">Aumente el número de versión en el manifiesto si realiza cambios en el manifiesto en el envío.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-117">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="fcf7c-118">Los envíos actualizados son necesarios para someterse a un nuevo proceso de revisión y validación.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-118">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="fcf7c-119">Actualizaciones de aplicaciones y flujo de consentimiento del usuario</span><span class="sxs-lookup"><span data-stu-id="fcf7c-119">App updates and the user consent flow</span></span>

<span data-ttu-id="fcf7c-120">Cuando un usuario instala la aplicación, uno de los primeros elementos que conviene dar permiso a la aplicación para acceder a los servicios y la información que la aplicación necesita para realizar su trabajo.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-120">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="fcf7c-121">En la mayoría de los casos, después de completar una actualización de la aplicación, la nueva versión aparecerá automáticamente para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-121">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="fcf7c-122">Sin embargo, hay algunas actualizaciones en el [manifiesto de la aplicación Teams](../../../../resources/schema/manifest-schema.md) que requieren la aceptación del usuario para completarse y pueden volver a desencadenar este comportamiento de consentimiento:</span><span class="sxs-lookup"><span data-stu-id="fcf7c-122">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="fcf7c-123">Se ha agregado o quitado un bot.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-123">A bot was added or removed.</span></span>
> * <span data-ttu-id="fcf7c-124">El valor único de un bot existente `botId` cambió.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-124">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="fcf7c-125">Se ha cambiado el valor booleano de un bot existente `isNotificationOnly` .</span><span class="sxs-lookup"><span data-stu-id="fcf7c-125">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="fcf7c-126">Se ha cambiado el valor booleano de un bot existente `supportsFiles` .</span><span class="sxs-lookup"><span data-stu-id="fcf7c-126">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="fcf7c-127">`composeExtensions`Se ha agregado o quitado una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-127">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="fcf7c-128">Se ha agregado un nuevo conector.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-128">A new connector was added.</span></span>
> * <span data-ttu-id="fcf7c-129">Se ha agregado una nueva pestaña estática/personal.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-129">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="fcf7c-130">Se ha agregado una nueva ficha configurable de grupo o canal.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-130">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="fcf7c-131">Los `webApplicationInfo` valores cambiados.</span><span class="sxs-lookup"><span data-stu-id="fcf7c-131">The `webApplicationInfo` values changed.</span></span>
>