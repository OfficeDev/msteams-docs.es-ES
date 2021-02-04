---
title: Preparar el espacio empresarial de Microsoft 365
description: Cómo empezar a trabajar con Teams en Microsoft 365
ms.topic: how-to
keywords: Configurar la carga de Microsoft 365 Tenant Teams
ms.openlocfilehash: 50765271b93edd380d1c23672289b618baf1d346
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093946"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Preparar el espacio empresarial de Microsoft 365

Si está suscrito a Microsoft 365, puede desarrollar aplicaciones para Microsoft Teams con uno de los siguientes [planes:](https://products.office.com/business/compare-more-office-365-for-business-plans)

* Basic
* Estándar
* Enterprise E1, E3 y E5
* Developer
* Education, Education Plus y Education E5

Microsoft Teams también estará disponible para los clientes que se suscriban a E4 antes de su [retirada.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)

## <a name="just-need-a-development-environment"></a>¿Solo necesitas un entorno de desarrollo?

Si actualmente no tiene una cuenta de Microsoft 365, puede registrarse para obtener una suscripción al Programa de desarrolladores de [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program) Es gratuito *durante* 90 días y se renovará continuamente siempre que lo use para la actividad de desarrollo. Si tiene una suscripción a Visual Studio *Enterprise* o *Professional,* ambos programas incluyen una suscripción gratuita de desarrollador de Microsoft 365, activa durante el período de vida de su Visual Studio suscripción. [](https://aka.ms/MyVisualStudioBenefits) *Consulte* [Configurar una suscripción de desarrollador de Microsoft 365.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)

## <a name="enable-microsoft-teams-for-your-organization"></a>Habilitar Microsoft Teams para su organización 

Si Microsoft Teams no se ha habilitado para su organización, primero tendrá que hacerlo. Echa un vistazo a nuestras instrucciones detalladas para [habilitar Teams para tu organización.](/microsoftteams/enable-features-office-365)

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Habilitar aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas

Active la instalación de instalación local de aplicaciones personalizadas para su inquilino de desarrollador de la siguiente manera:

1. Inicie sesión en el Centro de administración de [Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con su credencial de administrador. 

2. Seleccione **Mostrar todos los**  -->  **equipos.** 

![imagen del menú del centro de administración](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> La opción "Teams" puede tardar hasta 24 horas en aparecer. Durante el período provisional, puede [cargar la aplicación personalizada en un entorno de Teams](/microsoftteams/upload-custom-apps#validate) para pruebas y validación.

3. Navegar a las **directivas de configuración** de aplicaciones de Teams global  -->    -->  **(configuración predeterminada para toda la organización)**  

![activar la vista de instalación de instalación local](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Alterna **la carga de aplicaciones personalizadas** en la **posición** de posición.

5. Seleccione **Guardar** para guardar los cambios.

Y eso es todo. El inquilino de prueba ahora permitirá la instalación de prueba de aplicaciones personalizadas.

> [!Note] 
> La instalación de instalación local puede tardar hasta 24 horas en habilitarse. Durante el período provisional, puedes usar **la carga para probar \<your tenant>** la aplicación.

![vista de aplicación updload](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Para obtener información completa sobre cómo interactúan estas opciones *de* configuración, vea , Administrar directivas y configuraciones de aplicaciones personalizadas en [Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) y Administrar directivas de configuración de aplicaciones en [Microsoft Teams.](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)
