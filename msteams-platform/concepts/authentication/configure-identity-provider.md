---
title: Configurar proveedores de identidades de OAuth 2.0
description: Describe cómo configurar proveedores de identidades con un enfoque en Azure AD
ms.topic: how-to
ms.localizationpriority: medium
keywords: autenticación de Azure AD proveedor de identidades de oauth
ms.openlocfilehash: 0e0b1e21bf3c2e877ddef790677ba2f4c227339e
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212338"
---
# <a name="configure-identity-providers"></a>Configurar proveedores de identidades

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Configuración de una aplicación para usar Azure Active Directory como proveedor de identidades

Los proveedores de identidades que admiten OAuth 2.0 no autenticarán solicitudes de aplicaciones desconocidas; las aplicaciones deben registrarse con antelación. Para hacerlo con Azure AD, siga estos pasos:

1. Abra el [Portal de registro de aplicaciones](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Selecciona la aplicación para ver sus propiedades o selecciona el botón "Nuevo registro". Busca la **sección Uri** de redireccionamiento de la aplicación.

3. Seleccione **Web** en el menú desplegable. Actualice la dirección URL al punto de conexión de autenticación. Para las aplicaciones de ejemplo TypeScript/Node.js y C# en GitHub, las direcciones URL de redireccionamiento serán similares a las siguientes:

    Direcciones URL de redireccionamiento: `https://<hostname>/bot-auth/simple-start`

Reemplace por el host real, que puede ser un sitio de hospedaje dedicado como Azure, Glitch o un túnel ngrok para localhost en el equipo de desarrollo, `<hostname>` como `abcd1234.ngrok.io` . Es posible que no tenga esta información si no ha completado o hospedado la aplicación (o la aplicación de ejemplo mencionada anteriormente), pero siempre puede volver a esta página cuando se conozca esa información.

## <a name="other-authentication-providers"></a>Otros proveedores de autenticación

* **LinkedIn:** Siga las instrucciones de [Configuración de la aplicación LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google:** Obtener credenciales de cliente de OAuth 2.0 desde la consola [de la API de Google](https://console.developers.google.com/)
