---
title: Configuración de proveedores de identidad de OAuth 2,0
description: Describe cómo configurar proveedores de identidades con un enfoque en Azure AD.
keywords: autenticación de Teams proveedor de identidades de OAuth de AAD
ms.openlocfilehash: 799b0c20cda64456a4610acbdbedf758989bee55
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676092"
---
# <a name="configuring-identity-providers"></a><span data-ttu-id="cc786-104">Configuración de proveedores de identidad</span><span class="sxs-lookup"><span data-stu-id="cc786-104">Configuring identity providers</span></span>

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="cc786-105">Configuración de una aplicación para que use Azure Active Directory como proveedor de identidades</span><span class="sxs-lookup"><span data-stu-id="cc786-105">Configuring an application to use Azure Active Directory as an identity provider</span></span>

<span data-ttu-id="cc786-106">Los proveedores de identidades que admiten OAuth 2,0 no podrán autenticar solicitudes de aplicaciones desconocidas; las aplicaciones deben registrarse antes de tiempo.</span><span class="sxs-lookup"><span data-stu-id="cc786-106">Identity providers supporting OAuth 2.0 will not authenticate requests from unknown applications; applications must be registered ahead of time.</span></span> <span data-ttu-id="cc786-107">Para hacerlo con Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="cc786-107">To do this with Azure AD, follow these steps:</span></span>

1. <span data-ttu-id="cc786-108">Abra el [portal de registro de aplicaciones](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span><span class="sxs-lookup"><span data-stu-id="cc786-108">Open the [Application Registration Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span></span>

2. <span data-ttu-id="cc786-109">Seleccione la aplicación para ver sus propiedades o haga clic en el botón "nuevo registro".</span><span class="sxs-lookup"><span data-stu-id="cc786-109">Select your app to view its properties, or click the "New Registration" button.</span></span> <span data-ttu-id="cc786-110">Busque la sección **URI de redireccionamiento** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc786-110">Find the **Redirect URI** section for the app.</span></span>

3. <span data-ttu-id="cc786-111">En el menú desplegable, asegúrese de que **Web** está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="cc786-111">In the dropdown menu, make sure **Web** is selected.</span></span> <span data-ttu-id="cc786-112">Actualice la dirección URL del punto de conexión de autenticación.</span><span class="sxs-lookup"><span data-stu-id="cc786-112">Update the URL to your authentication endpoint.</span></span> <span data-ttu-id="cc786-113">Para las aplicaciones de ejemplo de TypeScript/node. js y C# en GitHub, las direcciones URL de redireccionamiento serán similares a esta:</span><span class="sxs-lookup"><span data-stu-id="cc786-113">For the TypeScript/Node.js and C# sample apps on GitHub, the redirect URLs will be similar to this:</span></span>

    <span data-ttu-id="cc786-114">Direcciones URL de redireccionamiento:`https://<hostname>/bot-auth/simple-start`</span><span class="sxs-lookup"><span data-stu-id="cc786-114">Redirect URLs: `https://<hostname>/bot-auth/simple-start`</span></span>

<span data-ttu-id="cc786-115">Reemplace `<hostname>` por su host real.</span><span class="sxs-lookup"><span data-stu-id="cc786-115">Replace `<hostname>` with your actual host.</span></span> <span data-ttu-id="cc786-116">Puede tratarse de un sitio de hospedaje dedicado como Azure, problema o un túnel de ngrok a localhost en el equipo de desarrollo `abcd1234.ngrok.io`como.</span><span class="sxs-lookup"><span data-stu-id="cc786-116">This might be a dedicated hosting site such as Azure, Glitch, or an ngrok tunnel to localhost on your development machine such as `abcd1234.ngrok.io`.</span></span> <span data-ttu-id="cc786-117">Es posible que no tenga esta información aún si no ha completado ni hospedado la aplicación (o la aplicación de ejemplo mencionada anteriormente), pero siempre puede volver a esta página cuando se conozca dicha información.</span><span class="sxs-lookup"><span data-stu-id="cc786-117">You may not have this information yet if you have not completed or hosted your app (or the sample app mentioned above), but you can always return to this page when that information is known.</span></span>

## <a name="other-authentication-providers"></a><span data-ttu-id="cc786-118">Otros proveedores de autenticación</span><span class="sxs-lookup"><span data-stu-id="cc786-118">Other authentication providers</span></span>

* <span data-ttu-id="cc786-119">**LinkedIn** Siga las instrucciones de [configurar la aplicación de LinkedIn](https://developer.linkedin.com/docs/oauth2)</span><span class="sxs-lookup"><span data-stu-id="cc786-119">**LinkedIn** Follow the instructions in [Configuring your LinkedIn application](https://developer.linkedin.com/docs/oauth2)</span></span>

* <span data-ttu-id="cc786-120">**Google** Obtener credenciales de cliente de OAuth 2,0 desde la [consola de API de Google](https://console.developers.google.com/)</span><span class="sxs-lookup"><span data-stu-id="cc786-120">**Google** Obtain OAuth 2.0 client credentials from the [Google API Console](https://console.developers.google.com/)</span></span>
