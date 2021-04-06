---
title: Mantenimiento y soporte técnico de la aplicación publicada
description: Qué hacer después de publicar la aplicación
ms.topic: how-to
keywords: manifiesto de actualización de la aplicación de certificación de actualización de publicación de teams
ms.openlocfilehash: 8644db5e329e15d77062553eda4a41a36b2740ee
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585837"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="5a604-104">Ofrecer mantenimiento y soporte técnico de su aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="5a604-104">Maintain and support your published app</span></span> 

<span data-ttu-id="5a604-105">Después de aprobar y enumerar la aplicación en el catálogo de aplicaciones públicas, puedes aumentar tu alcance completando el Programa de cumplimiento de aplicaciones de Microsoft 365 o agregando un botón de descarga en tu sitio web.</span><span class="sxs-lookup"><span data-stu-id="5a604-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="microsoft-365-certified"></a><span data-ttu-id="5a604-106">Certificado de Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="5a604-106">Microsoft 365 Certified</span></span>

<span data-ttu-id="5a604-107">El Programa de cumplimiento de aplicaciones de [Microsoft 365](./application-certification.md)es un enfoque de tres niveles para la seguridad y el cumplimiento de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5a604-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="5a604-108">Cada nivel se basa en el siguiente: ofrece un programa por capas para satisfacer las necesidades del cliente.</span><span class="sxs-lookup"><span data-stu-id="5a604-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="5a604-109">Para obtener más información sobre la posición de seguridad y cumplimiento de las aplicaciones de Teams, visite la página [de cumplimiento](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span><span class="sxs-lookup"><span data-stu-id="5a604-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="5a604-110">Agregar un botón de descarga al sitio del producto</span><span class="sxs-lookup"><span data-stu-id="5a604-110">Add a download button to your product site</span></span>

<span data-ttu-id="5a604-111">Si la aplicación está en la tienda global de Microsoft Teams, puedes generar un vínculo para tu sitio web que inicie Teams y muestre un cuadro de diálogo de consentimiento e instalación para que los usuarios agreguen la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5a604-111">If your app is in the Microsoft Teams global store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="5a604-112">El formato es:  `https://teams.microsoft.com/l/app/<appId>` donde appID es el GUID que declaran en el manifiesto enviado.</span><span class="sxs-lookup"><span data-stu-id="5a604-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="5a604-113">Ejemplo: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` es el vínculo para instalar Trello.</span><span class="sxs-lookup"><span data-stu-id="5a604-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="5a604-114">Actualizar la aplicación de Teams existente</span><span class="sxs-lookup"><span data-stu-id="5a604-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="5a604-115">No use el *botón Agregar una nueva aplicación* para volver a enviar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5a604-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="5a604-116">Usa el icono de la aplicación en la pestaña Información general en su lugar.</span><span class="sxs-lookup"><span data-stu-id="5a604-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="5a604-117">El appId en el manifiesto actualizado debe ser el mismo que en el manifiesto actual, con un número de versión incrementado.</span><span class="sxs-lookup"><span data-stu-id="5a604-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="5a604-118">Incremente el número de versión en el manifiesto si realiza cambios en el envío, incluido el nombre de la aplicación o los metadatos del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="5a604-118">Increment your version number in the manifest if you make any changes to your submission including app name or any metadata in the manifest.</span></span>
* <span data-ttu-id="5a604-119">Los envíos actualizados son necesarios para someterse a un nuevo proceso de revisión y validación.</span><span class="sxs-lookup"><span data-stu-id="5a604-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="5a604-120">Actualizaciones de aplicaciones y flujo de consentimiento del usuario</span><span class="sxs-lookup"><span data-stu-id="5a604-120">App updates and the user consent flow</span></span>

<span data-ttu-id="5a604-121">Cuando un usuario instala la aplicación, una de las primeras cosas que hace es dar permiso a la aplicación para tener acceso a los servicios e información que la aplicación necesita para realizar su trabajo.</span><span class="sxs-lookup"><span data-stu-id="5a604-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="5a604-122">En la mayoría de los casos, después de completar una actualización de la aplicación, la nueva versión aparecerá automáticamente para los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="5a604-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="5a604-123">Sin embargo, hay algunas actualizaciones en el manifiesto de la aplicación [de Teams](../../../../resources/schema/manifest-schema.md) que requieren la aceptación del usuario para completarse y pueden volver a desencadenar este comportamiento de consentimiento:</span><span class="sxs-lookup"><span data-stu-id="5a604-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="5a604-124">Se agrega o quita un bot.</span><span class="sxs-lookup"><span data-stu-id="5a604-124">A bot is added or removed.</span></span>
> * <span data-ttu-id="5a604-125">Se cambia el valor único de un bot `botId` existente.</span><span class="sxs-lookup"><span data-stu-id="5a604-125">An existing bot's unique `botId` value is changed.</span></span>
> * <span data-ttu-id="5a604-126">Se cambia el valor `isNotificationOnly` booleano de un bot existente.</span><span class="sxs-lookup"><span data-stu-id="5a604-126">An existing bot's `isNotificationOnly` boolean value is changed.</span></span>
> * <span data-ttu-id="5a604-127">Se cambia el valor booleano o de un `supportsFiles` `supportsCalling` bot existente.</span><span class="sxs-lookup"><span data-stu-id="5a604-127">An existing bot's `supportsFiles` or `supportsCalling` boolean value is changed.</span></span>
> * <span data-ttu-id="5a604-128">Se agrega o `composeExtensions` quita una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="5a604-128">A messaging extension `composeExtensions` is added or removed.</span></span>
> * <span data-ttu-id="5a604-129">Se agrega un nuevo conector.</span><span class="sxs-lookup"><span data-stu-id="5a604-129">A new connector is added.</span></span>
> * <span data-ttu-id="5a604-130">Se agrega una nueva pestaña estática o personal.</span><span class="sxs-lookup"><span data-stu-id="5a604-130">A new static or personal tab is added.</span></span>
> * <span data-ttu-id="5a604-131">Se agrega una nueva pestaña de canal o grupo configurable.</span><span class="sxs-lookup"><span data-stu-id="5a604-131">A new configurable group or channel tab is added.</span></span>
> * <span data-ttu-id="5a604-132">Las propiedades dentro `webApplicationInfo` se cambian.</span><span class="sxs-lookup"><span data-stu-id="5a604-132">The properties inside `webApplicationInfo` are changed.</span></span> <span data-ttu-id="5a604-133">Para los cambios en `webApplicationInfo` , el consentimiento solo es necesario en el ámbito de Teams.</span><span class="sxs-lookup"><span data-stu-id="5a604-133">For changes to `webApplicationInfo`, consent is only required in the Teams scope.</span></span>

### <a name="images-of-user-consent-flow"></a><span data-ttu-id="5a604-134">Imágenes del flujo de consentimiento del usuario:</span><span class="sxs-lookup"><span data-stu-id="5a604-134">Images of user consent flow:</span></span>

<span data-ttu-id="5a604-135">**Configurar un conector:** esta pantalla solo aparecerá para los usuarios de Teams.</span><span class="sxs-lookup"><span data-stu-id="5a604-135">**Set up a connector** —  This screen will appear only for Teams users.</span></span>

![Configuración del flujo de consentimiento de un diagrama de conector](../../../../assets/images/connector-teams-consentflow.png)

<span data-ttu-id="5a604-137">**Flujo de consentimiento del** usuario: esta pantalla es común para el ámbito personal y de grupo.</span><span class="sxs-lookup"><span data-stu-id="5a604-137">**User consent flow** - This screen is common for both personal and group scope.</span></span> <span data-ttu-id="5a604-138">Aquí, active la casilla **Consentimiento en nombre de su organización** y elija **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5a604-138">Here, select the **Consent on behalf of your organization** checkbox and choose **Accept**.</span></span>

![Diagrama de permisos](../../../../assets/images/user-consent-flow.png)
