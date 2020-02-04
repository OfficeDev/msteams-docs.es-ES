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
# <a name="configuring-identity-providers"></a>Configuración de proveedores de identidad

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Configuración de una aplicación para que use Azure Active Directory como proveedor de identidades

Los proveedores de identidades que admiten OAuth 2,0 no podrán autenticar solicitudes de aplicaciones desconocidas; las aplicaciones deben registrarse antes de tiempo. Para hacerlo con Azure AD, siga estos pasos:

1. Abra el [portal de registro de aplicaciones](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Seleccione la aplicación para ver sus propiedades o haga clic en el botón "nuevo registro". Busque la sección **URI de redireccionamiento** de la aplicación.

3. En el menú desplegable, asegúrese de que **Web** está seleccionado. Actualice la dirección URL del punto de conexión de autenticación. Para las aplicaciones de ejemplo de TypeScript/node. js y C# en GitHub, las direcciones URL de redireccionamiento serán similares a esta:

    Direcciones URL de redireccionamiento:`https://<hostname>/bot-auth/simple-start`

Reemplace `<hostname>` por su host real. Puede tratarse de un sitio de hospedaje dedicado como Azure, problema o un túnel de ngrok a localhost en el equipo de desarrollo `abcd1234.ngrok.io`como. Es posible que no tenga esta información aún si no ha completado ni hospedado la aplicación (o la aplicación de ejemplo mencionada anteriormente), pero siempre puede volver a esta página cuando se conozca dicha información.

## <a name="other-authentication-providers"></a>Otros proveedores de autenticación

* **LinkedIn** Siga las instrucciones de [configurar la aplicación de LinkedIn](https://developer.linkedin.com/docs/oauth2)

* **Google** Obtener credenciales de cliente de OAuth 2,0 desde la [consola de API de Google](https://console.developers.google.com/)
