---
title: Configurar proveedores de identidades de OAuth 2.0
description: Describe cómo configurar proveedores de identidades con un enfoque en Microsoft Azure Active Directory (Azure AD)
ms.topic: how-to
ms.localizationpriority: medium
keywords: autenticación de Azure AD proveedor de identidades de oauth
ms.openlocfilehash: 36e81839b1837fca8a124b60701c3d5f95608851
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356416"
---
# <a name="configure-identity-providers"></a>Configurar proveedores de identidades

## <a name="configuring-an-application-to-use-azure-ad-as-an-identity-provider"></a>Configuración de una aplicación para usar Azure AD como proveedor de identidades

Los proveedores de identidades que admiten OAuth 2.0 no autenticarán solicitudes de aplicaciones desconocidas; las aplicaciones deben registrarse con antelación. Para hacerlo con Azure AD, siga estos pasos:

1. Abra el [Portal de registro de aplicaciones](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Selecciona la aplicación para ver sus propiedades o selecciona el botón "Nuevo registro". Busca la **sección Uri** de redireccionamiento de la aplicación.

3. Seleccione **Web** en el menú desplegable. Actualice la dirección URL al punto de conexión de autenticación. Para las aplicaciones de ejemplo TypeScript/Node.js y C# en GitHub, las direcciones URL de redireccionamiento serán similares a las siguientes:

    Direcciones URL de redireccionamiento: `https://<hostname>/bot-auth/simple-start`

Reemplace `<hostname>` por el host real, que puede ser un sitio de hospedaje dedicado como Azure, Glitch o un túnel ngrok para localhost en el equipo de desarrollo, como `abcd1234.ngrok.io`. Es posible que no tenga esta información si no ha completado o hospedado la aplicación (o la aplicación de ejemplo mencionada anteriormente), pero siempre puede volver a esta página cuando se conozca esa información.

## <a name="other-authentication-providers"></a>Otros proveedores de autenticación

* **LinkedIn:** Siga las instrucciones de [Configuración de la aplicación LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google:** Obtener credenciales de cliente de OAuth 2.0 desde la consola [de la API de Google](https://console.developers.google.com/)

* **Proveedores externos de OAuth de pestañas:** Para obtener más información, vea [Usar proveedores de OAuth externos](../../tabs/how-to/authentication/auth-oauth-provider.md)

## <a name="see-also"></a>Vea también 

* [Autenticar un usuario en un bot Microsoft Teams de autenticación](../../resources/bot-v3/bot-authentication/auth-bot-AAD.md)
* [Compatibilidad con inicio de sesión único (SSO) para pestañas](../../tabs/how-to/authentication/auth-aad-sso.md)
* [Autenticar un usuario en una Microsoft Teams pestaña](../../tabs/how-to/authentication/auth-tab-aad.md)