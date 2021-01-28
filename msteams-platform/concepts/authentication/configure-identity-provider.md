---
title: Configurar proveedores de identidades de OAuth 2.0
description: Describe cómo configurar proveedores de identidades centrados en Azure AD
ms.topic: how-to
keywords: Proveedor de identidad de AAD oauth de autenticación de teams
ms.openlocfilehash: b5ffd6c4c1edd2c4315ea1e31474a626de53aba1
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014470"
---
# <a name="configure-identity-providers"></a><span data-ttu-id="d180d-104">Configurar proveedores de identidades</span><span class="sxs-lookup"><span data-stu-id="d180d-104">Configure identity providers</span></span>

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="d180d-105">Configuración de una aplicación para usar Azure Active Directory como proveedor de identidades</span><span class="sxs-lookup"><span data-stu-id="d180d-105">Configuring an application to use Azure Active Directory as an identity provider</span></span>

<span data-ttu-id="d180d-106">Los proveedores de identidades compatibles con OAuth 2.0 no autenticarán solicitudes de aplicaciones desconocidas; las aplicaciones deben registrarse con antelación.</span><span class="sxs-lookup"><span data-stu-id="d180d-106">Identity providers supporting OAuth 2.0 will not authenticate requests from unknown applications; applications must be registered ahead of time.</span></span> <span data-ttu-id="d180d-107">Para ello con Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d180d-107">To do this with Azure AD, follow these steps:</span></span>

1. <span data-ttu-id="d180d-108">Abra el Portal [de registro de aplicaciones.](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)</span><span class="sxs-lookup"><span data-stu-id="d180d-108">Open the [Application Registration Portal](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).</span></span>

2. <span data-ttu-id="d180d-109">Seleccione la aplicación para ver sus propiedades o haga clic en el botón "Nuevo registro".</span><span class="sxs-lookup"><span data-stu-id="d180d-109">Select your app to view its properties, or click the "New Registration" button.</span></span> <span data-ttu-id="d180d-110">Busque la **sección URI** de redireccionamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d180d-110">Find the **Redirect URI** section for the app.</span></span>

3. <span data-ttu-id="d180d-111">En el menú desplegable, asegúrese de que **web** está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d180d-111">In the dropdown menu, make sure **Web** is selected.</span></span> <span data-ttu-id="d180d-112">Actualice la dirección URL al punto de conexión de autenticación.</span><span class="sxs-lookup"><span data-stu-id="d180d-112">Update the URL to your authentication endpoint.</span></span> <span data-ttu-id="d180d-113">Para las aplicaciones de ejemplo TypeScript/Node.js y C# en GitHub, las direcciones URL de redireccionamiento serán similares a las siguientes:</span><span class="sxs-lookup"><span data-stu-id="d180d-113">For the TypeScript/Node.js and C# sample apps on GitHub, the redirect URLs will be similar to this:</span></span>

    <span data-ttu-id="d180d-114">Direcciones URL de redireccionamiento: `https://<hostname>/bot-auth/simple-start`</span><span class="sxs-lookup"><span data-stu-id="d180d-114">Redirect URLs: `https://<hostname>/bot-auth/simple-start`</span></span>

<span data-ttu-id="d180d-115">Reemplace `<hostname>` por el host real.</span><span class="sxs-lookup"><span data-stu-id="d180d-115">Replace `<hostname>` with your actual host.</span></span> <span data-ttu-id="d180d-116">Puede ser un sitio de hospedaje dedicado como Azure, Glitch o un túnel ngrok para localhost en el equipo de desarrollo, como `abcd1234.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="d180d-116">This might be a dedicated hosting site such as Azure, Glitch, or an ngrok tunnel to localhost on your development machine such as `abcd1234.ngrok.io`.</span></span> <span data-ttu-id="d180d-117">Es posible que aún no tenga esta información si no ha completado u hospedado la aplicación (o la aplicación de ejemplo mencionada anteriormente), pero siempre puede volver a esta página cuando se conozca esa información.</span><span class="sxs-lookup"><span data-stu-id="d180d-117">You may not have this information yet if you have not completed or hosted your app (or the sample app mentioned above), but you can always return to this page when that information is known.</span></span>

## <a name="other-authentication-providers"></a><span data-ttu-id="d180d-118">Otros proveedores de autenticación</span><span class="sxs-lookup"><span data-stu-id="d180d-118">Other authentication providers</span></span>

* <span data-ttu-id="d180d-119">**LinkedIn** Siga las instrucciones de [configuración de la aplicación de LinkedIn](https://developer.linkedin.com/docs/oauth2)</span><span class="sxs-lookup"><span data-stu-id="d180d-119">**LinkedIn** Follow the instructions in [Configuring your LinkedIn application](https://developer.linkedin.com/docs/oauth2)</span></span>

* <span data-ttu-id="d180d-120">**Google** Obtener credenciales de cliente de OAuth 2.0 desde la consola [de la API de Google](https://console.developers.google.com/)</span><span class="sxs-lookup"><span data-stu-id="d180d-120">**Google** Obtain OAuth 2.0 client credentials from the [Google API Console](https://console.developers.google.com/)</span></span>
