---
title: Publicación posterior
description: Qué hacer después de publicar la aplicación
keywords: certificado de actualización de publicación de publicaciones de Teams
ms.openlocfilehash: 54d0615c262e45729a36f556c3eda3b810d2a097
ms.sourcegitcommit: 2a84a3c8b10771e37ce51bf603a967633947a3e4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/10/2020
ms.locfileid: "42582863"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="862f0-104">Mantener y admitir la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="862f0-104">Maintain and support your published app</span></span> 

<span data-ttu-id="862f0-105">Después de aprobar la aplicación y enumerarla en el catálogo de aplicaciones públicas, puede aumentar su alcance si logra la certificación de la aplicación o agrega un botón Descargar en el sitio Web.</span><span class="sxs-lookup"><span data-stu-id="862f0-105">After your app is approved and listed in the public app catalog, you can increase your reach by achieving app certification, or adding a download button your website.</span></span>

## <a name="application-certificate"></a><span data-ttu-id="862f0-106">Certificado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="862f0-106">Application Certificate</span></span>

<span data-ttu-id="862f0-107">Microsoft proporciona un [programa de certificación de aplicaciones](./application-certification.md) que compila la información de la aplicación y la presenta en la [Página seguridad y cumplimiento de aplicaciones de Microsoft Teams](https://aka.ms/AppCertification).</span><span class="sxs-lookup"><span data-stu-id="862f0-107">Microsoft provides a [Application Certification program](./application-certification.md) that compiles your app information and presents it on [Microsoft Teams App Security and Compliance Page](https://aka.ms/AppCertification).</span></span> <span data-ttu-id="862f0-108">Esta información está destinada a ayudar a los administradores a elegir aplicaciones que sean seguras para sus organizaciones.</span><span class="sxs-lookup"><span data-stu-id="862f0-108">This information is intended to help admins to choose apps that are safe for their organizations.</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="862f0-109">Agregar un botón Descargar al sitio del producto</span><span class="sxs-lookup"><span data-stu-id="862f0-109">Add a download button to your product site</span></span>

<span data-ttu-id="862f0-110">Si la aplicación está en la tienda Microsoft Teams, puede generar un vínculo para su sitio web que inicie Teams y que muestre un cuadro de diálogo de consentimiento e instalación para que los usuarios agreguen la aplicación.</span><span class="sxs-lookup"><span data-stu-id="862f0-110">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="862f0-111">El formato es: `https://teams.microsoft.com/l/app/<appId>` donde appID es el GUID que declaran en el manifiesto enviado.</span><span class="sxs-lookup"><span data-stu-id="862f0-111">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="862f0-112">Ejemplo: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` es el vínculo para instalar Trello.</span><span class="sxs-lookup"><span data-stu-id="862f0-112">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="862f0-113">Actualización de la aplicación de Teams existente</span><span class="sxs-lookup"><span data-stu-id="862f0-113">Updating your existing Teams app</span></span>

* <span data-ttu-id="862f0-114">No use el botón *Agregar una nueva aplicación* para volver a enviar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="862f0-114">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="862f0-115">En su lugar, use el icono de la aplicación en la pestaña Información general.</span><span class="sxs-lookup"><span data-stu-id="862f0-115">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="862f0-116">El appId del manifiesto actualizado debe ser el mismo que el del manifiesto actual, con un número de versión incrementado.</span><span class="sxs-lookup"><span data-stu-id="862f0-116">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="862f0-117">Aumente el número de versión en el manifiesto si realiza cambios en el manifiesto en el envío.</span><span class="sxs-lookup"><span data-stu-id="862f0-117">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="862f0-118">Los envíos actualizados son necesarios para someterse a un nuevo proceso de revisión y validación.</span><span class="sxs-lookup"><span data-stu-id="862f0-118">Updated submissions are required to undergo a new review and validation process.</span></span>


### <a name="when-does-updating-your-app-trigger-the-user-consent-flow"></a><span data-ttu-id="862f0-119">¿Cuándo actualizar la aplicación desencadenar el flujo de consentimiento del usuario?</span><span class="sxs-lookup"><span data-stu-id="862f0-119">When does updating your app trigger the user consent flow?</span></span>

<span data-ttu-id="862f0-120">Cuando un usuario instala la aplicación, uno de los primeros elementos que conviene dar permiso a la aplicación para acceder a los servicios y la información que la aplicación necesita para realizar su trabajo.</span><span class="sxs-lookup"><span data-stu-id="862f0-120">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="862f0-121">Al actualizar la aplicación, se puede volver a desencadenar este comportamiento de consentimiento, especialmente si ha realizado uno o varios de los siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="862f0-121">When you update your app, that can re-trigger this consent behavior, particularly if you have made one or more of the following changes:</span></span>

* <span data-ttu-id="862f0-122">Adición de una nueva funcionalidad a una aplicación, como agregar un bot a una aplicación de solo pestaña.</span><span class="sxs-lookup"><span data-stu-id="862f0-122">Adding a new capability to an app such as adding a bot to an tab only app.</span></span>
* <span data-ttu-id="862f0-123">Cambiar la matriz de permisos en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="862f0-123">Changing the permissions array in the manifest.</span></span>
* <span data-ttu-id="862f0-124">Incrementar el número de versión de la aplicación en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="862f0-124">Incrementing your app version number in your manifest.</span></span>
