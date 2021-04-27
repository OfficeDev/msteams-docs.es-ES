---
title: Configurar proveedores de identidades de OAuth 2.0
description: Describe cómo configurar proveedores de identidades con un enfoque en Azure AD
ms.topic: how-to
localization_priority: Normal
keywords: Proveedor de identidades de AAD oauth de autenticación de teams
ms.openlocfilehash: ffcf376ea6c4f1a94d797413af22af867dbd5b53
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020859"
---
# <a name="configure-identity-providers"></a>Configurar proveedores de identidades

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Configuración de una aplicación para usar Azure Active Directory como proveedor de identidades

Los proveedores de identidades que admiten OAuth 2.0 no autenticarán solicitudes de aplicaciones desconocidas; las aplicaciones deben registrarse con antelación. Para ello con Azure AD, siga estos pasos:

1. Abra el [Portal de registro de aplicaciones](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Selecciona la aplicación para ver sus propiedades o haz clic en el botón "Nuevo registro". Busca la **sección Uri** de redireccionamiento de la aplicación.

3. En el menú desplegable, asegúrese de **que web** está seleccionado. Actualice la dirección URL al punto de conexión de autenticación. Para las aplicaciones de ejemplo TypeScript/Node.js y C# en GitHub, las direcciones URL de redireccionamiento serán similares a las siguientes:

    Direcciones URL de redireccionamiento: `https://<hostname>/bot-auth/simple-start`

Reemplace `<hostname>` por el host real. Puede ser un sitio de hospedaje dedicado, como Azure, Glitch o un túnel ngrok para localhost en el equipo de desarrollo, como `abcd1234.ngrok.io` . Es posible que aún no tenga esta información si no ha completado o hospedado la aplicación (o la aplicación de ejemplo mencionada anteriormente), pero siempre puede volver a esta página cuando se conozca esa información.

## <a name="other-authentication-providers"></a>Otros proveedores de autenticación

* **LinkedIn** Siga las instrucciones de [Configuración de la aplicación LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google** Obtener credenciales de cliente de OAuth 2.0 desde la consola [de la API de Google](https://console.developers.google.com/)
