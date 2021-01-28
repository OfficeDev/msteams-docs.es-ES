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
# <a name="configure-identity-providers"></a>Configurar proveedores de identidades

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Configuración de una aplicación para usar Azure Active Directory como proveedor de identidades

Los proveedores de identidades compatibles con OAuth 2.0 no autenticarán solicitudes de aplicaciones desconocidas; las aplicaciones deben registrarse con antelación. Para ello con Azure AD, siga estos pasos:

1. Abra el Portal [de registro de aplicaciones.](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)

2. Seleccione la aplicación para ver sus propiedades o haga clic en el botón "Nuevo registro". Busque la **sección URI** de redireccionamiento de la aplicación.

3. En el menú desplegable, asegúrese de que **web** está seleccionado. Actualice la dirección URL al punto de conexión de autenticación. Para las aplicaciones de ejemplo TypeScript/Node.js y C# en GitHub, las direcciones URL de redireccionamiento serán similares a las siguientes:

    Direcciones URL de redireccionamiento: `https://<hostname>/bot-auth/simple-start`

Reemplace `<hostname>` por el host real. Puede ser un sitio de hospedaje dedicado como Azure, Glitch o un túnel ngrok para localhost en el equipo de desarrollo, como `abcd1234.ngrok.io` . Es posible que aún no tenga esta información si no ha completado u hospedado la aplicación (o la aplicación de ejemplo mencionada anteriormente), pero siempre puede volver a esta página cuando se conozca esa información.

## <a name="other-authentication-providers"></a>Otros proveedores de autenticación

* **LinkedIn** Siga las instrucciones de [configuración de la aplicación de LinkedIn](https://developer.linkedin.com/docs/oauth2)

* **Google** Obtener credenciales de cliente de OAuth 2.0 desde la consola [de la API de Google](https://console.developers.google.com/)
