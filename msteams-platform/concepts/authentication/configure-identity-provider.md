---
title: Configurar proveedores de identidades de OAuth 2.0
description: Describe cómo configurar proveedores de identidades con un enfoque en Azure AD
ms.topic: how-to
ms.localizationpriority: medium
keywords: autenticación de AAD proveedor de identidades de oauth
ms.openlocfilehash: cae2cc3d2feba8c17ad895864fd1b5995095f71b
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887437"
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
