---
title: Ofrecer mantenimiento y soporte técnico de su aplicación publicada
description: Qué pensar una vez que la tienda aparece en la Teams y AppSource.
ms.topic: conceptual
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 57b57e268a4f2eafc14d0372b8b8383e410a80d5
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101754"
---
# <a name="maintain-your-published-microsoft-teams-app"></a><span data-ttu-id="69c46-103">Mantener la aplicación Microsoft Teams publicada</span><span class="sxs-lookup"><span data-stu-id="69c46-103">Maintain your published Microsoft Teams app</span></span>

<span data-ttu-id="69c46-104">Con la aplicación incluida en la Microsoft Teams, empieza a pensar en cómo mantendrás la aplicación en el futuro y aumentarás las descargas y el uso.</span><span class="sxs-lookup"><span data-stu-id="69c46-104">With your app listed on the Microsoft Teams store, start thinking about how you'll maintain the app going forward and increase downloads and usage.</span></span>

## <a name="publish-updates-to-your-app"></a><span data-ttu-id="69c46-105">Publicar actualizaciones en la aplicación</span><span class="sxs-lookup"><span data-stu-id="69c46-105">Publish updates to your app</span></span>

<span data-ttu-id="69c46-106">Puedes enviar cambios a la aplicación (como nuevas características o incluso metadatos) en el Centro de partners.</span><span class="sxs-lookup"><span data-stu-id="69c46-106">You can submit changes to your app (such as new features or even metadata) in Partner Center.</span></span> <span data-ttu-id="69c46-107">Estos cambios requieren un nuevo proceso de revisión.</span><span class="sxs-lookup"><span data-stu-id="69c46-107">These changes requires a new review process.</span></span>

<span data-ttu-id="69c46-108">Asegúrese de lo siguiente al publicar actualizaciones:</span><span class="sxs-lookup"><span data-stu-id="69c46-108">Ensure the following when publishing updates:</span></span>

* <span data-ttu-id="69c46-109">No cambies el identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69c46-109">Don't change your app ID.</span></span>
* <span data-ttu-id="69c46-110">Incremente el número de versión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69c46-110">Increment your app's version number.</span></span>
* <span data-ttu-id="69c46-111">En el Centro de partners, no seleccione **Agregar una nueva aplicación** para realizar la actualización.</span><span class="sxs-lookup"><span data-stu-id="69c46-111">In Partner Center, don't select **Add a new app** to do the update.</span></span> <span data-ttu-id="69c46-112">En su lugar, ve a la página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69c46-112">Go to your app's page instead.</span></span>

### <a name="app-updates-requiring-user-consent"></a><span data-ttu-id="69c46-113">Actualizaciones de aplicaciones que requieren el consentimiento del usuario</span><span class="sxs-lookup"><span data-stu-id="69c46-113">App updates requiring user consent</span></span>

<span data-ttu-id="69c46-114">Cuando un usuario instala la aplicación, debe conceder a la aplicación permiso para tener acceso a los servicios e información que la aplicación necesita para funcionar.</span><span class="sxs-lookup"><span data-stu-id="69c46-114">When a user installs your app, they must give the app permission to access the services and information the app requires to function.</span></span> <span data-ttu-id="69c46-115">En la mayoría de los casos, los usuarios solo tienen que hacerlo una vez y las nuevas versiones de la aplicación se instalan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="69c46-115">In most cases, users only have to do this once and new versions of your app install automatically.</span></span>

<span data-ttu-id="69c46-116">Sin embargo, si realizas alguno de los siguientes cambios en la aplicación, los usuarios existentes deben aceptar otra solicitud de permiso para instalar la actualización:</span><span class="sxs-lookup"><span data-stu-id="69c46-116">If you make any of the following changes to your app, however, your existing users must accept another permission request to install the update:</span></span>

* <span data-ttu-id="69c46-117">Agregar o quitar un bot.</span><span class="sxs-lookup"><span data-stu-id="69c46-117">Add or remove a bot.</span></span>
* <span data-ttu-id="69c46-118">Cambie el identificador del bot.</span><span class="sxs-lookup"><span data-stu-id="69c46-118">Change the bot ID.</span></span>
* <span data-ttu-id="69c46-119">Modifique la configuración de notificaciones uni-way de un bot.</span><span class="sxs-lookup"><span data-stu-id="69c46-119">Modify a bot's one-way notification configuration.</span></span>
* <span data-ttu-id="69c46-120">Modificar la compatibilidad de un bot para cargar y descargar archivos.</span><span class="sxs-lookup"><span data-stu-id="69c46-120">Modify a bot's support for uploading and downloading files.</span></span>
* <span data-ttu-id="69c46-121">Agregar o quitar una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="69c46-121">Add or remove a messaging extension.</span></span>
* <span data-ttu-id="69c46-122">Agregue una pestaña personal.</span><span class="sxs-lookup"><span data-stu-id="69c46-122">Add a personal tab.</span></span>
* <span data-ttu-id="69c46-123">Agregue una pestaña de canal y grupo.</span><span class="sxs-lookup"><span data-stu-id="69c46-123">Add a channel and group tab.</span></span>
* <span data-ttu-id="69c46-124">Agregue un conector.</span><span class="sxs-lookup"><span data-stu-id="69c46-124">Add a connector.</span></span>
* <span data-ttu-id="69c46-125">Modifique las configuraciones relacionadas con el registro Azure Active Directory aplicación (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="69c46-125">Modify configurations related to your Azure Active Directory (Azure AD) app registration.</span></span> <span data-ttu-id="69c46-126">Para obtener más información, vea [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo) .</span><span class="sxs-lookup"><span data-stu-id="69c46-126">For more information, see [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo).</span></span>

## <a name="fix-issues-with-your-published-app"></a><span data-ttu-id="69c46-127">Corregir problemas con la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="69c46-127">Fix issues with your published app</span></span>

<span data-ttu-id="69c46-128">Microsoft ejecuta pruebas de automatización diarias en las aplicaciones que aparecen en la Teams tienda.</span><span class="sxs-lookup"><span data-stu-id="69c46-128">Microsoft runs daily automation tests on apps listed on the Teams store.</span></span> <span data-ttu-id="69c46-129">Si se identifican problemas con la aplicación, nos comunicaremos contigo con un informe detallado sobre cómo reproducir los problemas y recomendaciones para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="69c46-129">If issues with your app are identified, we contact you with a detailed report on how to reproduce the issues and recommendations to resolve them.</span></span> <span data-ttu-id="69c46-130">Si no puedes solucionar los problemas en una escala de tiempo indicada, es posible que la descripción de la aplicación se quite de la tienda.</span><span class="sxs-lookup"><span data-stu-id="69c46-130">If you can't fix the problems within a stated timeline, your app listing may be removed from the store.</span></span>

## <a name="promote-your-app-on-another-site"></a><span data-ttu-id="69c46-131">Promocionar la aplicación en otro sitio</span><span class="sxs-lookup"><span data-stu-id="69c46-131">Promote your app on another site</span></span>

<span data-ttu-id="69c46-132">Cuando la aplicación aparezca en la Teams, puedes crear un vínculo que inicie Teams y muestre un cuadro de diálogo para instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69c46-132">When your app is listed in the Teams store, you can create a link that launches Teams and displays a dialog to install your app.</span></span> <span data-ttu-id="69c46-133">Puede incluir este vínculo, por ejemplo, con un botón de descarga en la página de marketing del producto.</span><span class="sxs-lookup"><span data-stu-id="69c46-133">You could include this link, for example, with a download button on your product's marketing page.</span></span>

<span data-ttu-id="69c46-134">Crea el vínculo con la siguiente dirección URL anexada con el identificador de la aplicación: `https://teams.microsoft.com/l/app/<your-app-id>` .</span><span class="sxs-lookup"><span data-stu-id="69c46-134">Create the link using the following URL appended with your app ID: `https://teams.microsoft.com/l/app/<your-app-id>`.</span></span>

## <a name="complete-microsoft-365-certification"></a><span data-ttu-id="69c46-135">Certificación Microsoft 365 completa</span><span class="sxs-lookup"><span data-stu-id="69c46-135">Complete Microsoft 365 Certification</span></span>

<span data-ttu-id="69c46-136">[Microsoft 365 Certification](/microsoft-365-app-certification/docs/certification) ofrece garantías de que los datos y la privacidad están protegidos y protegidos adecuadamente cuando se instala un Aplicación de Office o complemento de terceros en su ecosistema de Microsoft 365 usuario.</span><span class="sxs-lookup"><span data-stu-id="69c46-136">[Microsoft 365 Certification](/microsoft-365-app-certification/docs/certification) offers assurances that data and privacy are adequately secured and protected when a third-party Office app or add-in is installed in your Microsoft 365 ecosystem.</span></span> <span data-ttu-id="69c46-137">La certificación confirma que la aplicación es compatible con las tecnologías de Microsoft, cumple con los procedimientos recomendados de seguridad de aplicaciones en la nube y es compatible con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="69c46-137">Certification confirms that your app is compatible with Microsoft technologies, compliant with cloud app security best practices, and supported by Microsoft.</span></span>

## <a name="see-also"></a><span data-ttu-id="69c46-138">Vea también</span><span class="sxs-lookup"><span data-stu-id="69c46-138">See also</span></span>

* [<span data-ttu-id="69c46-139">Monetizar su aplicación a través del Marketplace comercial de Microsoft</span><span class="sxs-lookup"><span data-stu-id="69c46-139">Monetize your app through Microsoft Commercial Marketplace</span></span>](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
