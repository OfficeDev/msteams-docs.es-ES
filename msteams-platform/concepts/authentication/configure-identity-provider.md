---
title: Configuración de proveedores de identidades de OAuth 2.0
description: En este módulo, aprenderá a configurar proveedores de identidades con un enfoque en Microsoft Azure Active Directory (Azure AD)
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: 2d344fb5ffcbde35ad9e85eed9ea662d2a0ca9f6
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143448"
---
# <a name="configure-identity-providers"></a>Configurar proveedores de identidades

## <a name="configuring-an-application-to-use-azure-ad-as-an-identity-provider"></a>Configuración de una aplicación para usar Azure AD como proveedor de identidades

Los proveedores de identidades que admiten OAuth 2.0 no autenticarán las solicitudes de aplicaciones desconocidas; las aplicaciones deben registrarse con antelación. Para ello con Azure AD, siga estos pasos:

1. Abra el [Portal de registro de aplicaciones](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Seleccione la aplicación para ver sus propiedades o seleccione el botón "Nuevo registro". Busque la sección **URI de redirección** de la aplicación.

3. Seleccione **Web** en el menú desplegable. Actualice la dirección URL al punto de conexión de autenticación. Para las aplicaciones de ejemplo TypeScript/Node.js y C# en GitHub, las direcciones URL de redireccionamiento serán similares a las siguientes:

    URL de redireccionamiento`https://<hostname>/bot-auth/simple-start`

Reemplace `<hostname>` por el host real, que podría ser un sitio de hospedaje dedicado como Azure, Glitch o un túnel ngrok a localhost en la máquina de desarrollo, como `abcd1234.ngrok.io`. Es posible que no tenga esta información si no ha completado ni hospedado la aplicación (o la aplicación de ejemplo que se mencionó anteriormente), pero siempre puede volver a esta página cuando conozca esa información.

## <a name="other-authentication-providers"></a>Otros proveedores de autenticación

* **Linkedin:** Siga las instrucciones de [Configuración de la aplicación LinkedIn](/linkedin/talent/apply-with-linkedin).

* **Google:** Obtención de las credenciales de cliente de OAuth 2.0 desde la [consola de API de Google](https://console.developers.google.com/)

* **Proveedores de OAuth externos desde pestañas:** Para obtener más información, consulte [Uso de proveedores de OAuth externos](../../tabs/how-to/authentication/auth-oauth-provider.md).

## <a name="see-also"></a>Consulte también

* [Autenticación de un usuario en un bot de Microsoft Teams](../../resources/bot-v3/bot-authentication/auth-bot-AAD.md)
* [Compatibilidad con inicio de sesión único (SSO) para pestañas](../../tabs/how-to/authentication/tab-sso-overview.md)
* [Autenticación de un usuario en una pestaña de Microsoft Teams](../../tabs/how-to/authentication/auth-tab-aad.md)
