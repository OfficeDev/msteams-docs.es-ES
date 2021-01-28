---
title: Mantenimiento y soporte técnico de la aplicación publicada
description: Qué hacer después de publicar la aplicación
ms.topic: how-to
keywords: Manifiesto de actualización de la aplicación de certificación de actualización posterior a la publicación de teams
ms.openlocfilehash: ce63b840307f7e12a5cd05a1c67aed017cf6199b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014330"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="f9bae-104">Ofrecer mantenimiento y soporte técnico de su aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="f9bae-104">Maintain and support your published app</span></span> 

<span data-ttu-id="f9bae-105">Después de que la aplicación se apruebe y aparezca en el catálogo de aplicaciones público, puede aumentar su alcance completando el Programa de cumplimiento de aplicaciones de Microsoft 365 o agregando un botón de descarga en su sitio web.</span><span class="sxs-lookup"><span data-stu-id="f9bae-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="microsoft-365-certified"></a><span data-ttu-id="f9bae-106">Certificado de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="f9bae-106">Microsoft 365 Certified</span></span>

<span data-ttu-id="f9bae-107">El [Programa de cumplimiento de aplicaciones de Microsoft 365](./application-certification.md)es un enfoque de tres niveles para la seguridad y el cumplimiento de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f9bae-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="f9bae-108">Cada nivel se basa en el siguiente: ofrece un programa en capas para satisfacer las necesidades del cliente.</span><span class="sxs-lookup"><span data-stu-id="f9bae-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="f9bae-109">Puede obtener más información sobre la posición de seguridad y cumplimiento de las aplicaciones de Teams visitando la página [de cumplimiento.](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)</span><span class="sxs-lookup"><span data-stu-id="f9bae-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="f9bae-110">Agregar un botón de descarga al sitio del producto</span><span class="sxs-lookup"><span data-stu-id="f9bae-110">Add a download button to your product site</span></span>

<span data-ttu-id="f9bae-111">Si la aplicación está en la tienda global de Microsoft Teams, puede generar un vínculo para su sitio web que inicie Teams y muestre un cuadro de diálogo de consentimiento e instalación para que los usuarios agreguen la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9bae-111">If your app is in the Microsoft Teams global store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="f9bae-112">El formato es:  `https://teams.microsoft.com/l/app/<appId>` donde appID es el GUID que declaran en el manifiesto enviado.</span><span class="sxs-lookup"><span data-stu-id="f9bae-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="f9bae-113">Ejemplo: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` es el vínculo para instalar Trello.</span><span class="sxs-lookup"><span data-stu-id="f9bae-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="f9bae-114">Actualizar la aplicación de Teams existente</span><span class="sxs-lookup"><span data-stu-id="f9bae-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="f9bae-115">No use el *botón Agregar una nueva aplicación* para volver a enviar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9bae-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="f9bae-116">En su lugar, usa el icono de la aplicación en la pestaña Información general.</span><span class="sxs-lookup"><span data-stu-id="f9bae-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="f9bae-117">El appId del manifiesto actualizado debe ser el mismo que en el manifiesto actual, con un número de versión incrementado.</span><span class="sxs-lookup"><span data-stu-id="f9bae-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="f9bae-118">Incremente el número de versión en el manifiesto si realiza cambios en el envío, incluido el nombre de la aplicación o los metadatos del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="f9bae-118">Increment your version number in the manifest if you make any changes to your submission including app name or any metadata in the manifest.</span></span>
* <span data-ttu-id="f9bae-119">Los envíos actualizados son necesarios para someterse a un nuevo proceso de revisión y validación.</span><span class="sxs-lookup"><span data-stu-id="f9bae-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="f9bae-120">Actualizaciones de aplicaciones y flujo de consentimiento del usuario</span><span class="sxs-lookup"><span data-stu-id="f9bae-120">App updates and the user consent flow</span></span>

<span data-ttu-id="f9bae-121">Cuando un usuario instala la aplicación, una de las primeras cosas que hace es dar permiso a la aplicación para acceder a los servicios e información que la aplicación necesita para realizar su trabajo.</span><span class="sxs-lookup"><span data-stu-id="f9bae-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="f9bae-122">En la mayoría de los casos, después de completar una actualización de la aplicación, la nueva versión aparecerá automáticamente para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="f9bae-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="f9bae-123">Sin embargo, hay algunas actualizaciones en el manifiesto de la aplicación [de Teams](../../../../resources/schema/manifest-schema.md) que requieren la aceptación del usuario para completarse y pueden volver a desencadenar este comportamiento de consentimiento:</span><span class="sxs-lookup"><span data-stu-id="f9bae-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="f9bae-124">Se ha agregado o quitado un bot.</span><span class="sxs-lookup"><span data-stu-id="f9bae-124">A bot was added or removed.</span></span>
> * <span data-ttu-id="f9bae-125">Se cambió el valor único de un `botId` bot existente.</span><span class="sxs-lookup"><span data-stu-id="f9bae-125">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="f9bae-126">Se cambió el valor `isNotificationOnly` booleano de un bot existente.</span><span class="sxs-lookup"><span data-stu-id="f9bae-126">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="f9bae-127">Se cambió el valor `supportsFiles` booleano de un bot existente.</span><span class="sxs-lookup"><span data-stu-id="f9bae-127">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="f9bae-128">Se agregó o quitó una extensión de mensajería ( `composeExtensions` ).</span><span class="sxs-lookup"><span data-stu-id="f9bae-128">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="f9bae-129">Se ha agregado un nuevo conector.</span><span class="sxs-lookup"><span data-stu-id="f9bae-129">A new connector was added.</span></span>
> * <span data-ttu-id="f9bae-130">Se agregó una nueva pestaña estática/personal.</span><span class="sxs-lookup"><span data-stu-id="f9bae-130">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="f9bae-131">Se agregó una nueva pestaña de grupo o canal configurable.</span><span class="sxs-lookup"><span data-stu-id="f9bae-131">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="f9bae-132">Los `webApplicationInfo` valores han cambiado.</span><span class="sxs-lookup"><span data-stu-id="f9bae-132">The `webApplicationInfo` values changed.</span></span>
>

### <a name="images-of-user-consent-flow"></a><span data-ttu-id="f9bae-133">Imágenes del flujo de consentimiento del usuario:</span><span class="sxs-lookup"><span data-stu-id="f9bae-133">Images of user consent flow:</span></span>

<span data-ttu-id="f9bae-134">**Configurar un conector:** esta pantalla solo aparecerá para los usuarios de Teams.</span><span class="sxs-lookup"><span data-stu-id="f9bae-134">**Set up a connector** —  This screen will appear only for Teams users.</span></span>

![Configuración de flujo de consentimiento de un diagrama de conector](../../../../assets/images/connector-teams-consentflow.png)

<span data-ttu-id="f9bae-136">**Flujo de consentimiento del** usuario: esta pantalla es común tanto para el ámbito personal como para el de grupo.</span><span class="sxs-lookup"><span data-stu-id="f9bae-136">**User consent flow** - This screen is common for both personal and group scope.</span></span> <span data-ttu-id="f9bae-137">Aquí, active la casilla **Consentimiento en nombre de su organización** y elija **Aceptar.**</span><span class="sxs-lookup"><span data-stu-id="f9bae-137">Here, select the **Consent on behalf of your organization** checkbox and choose **Accept**.</span></span>

![Diagrama de permisos](../../../../assets/images/user-consent-flow.png)
