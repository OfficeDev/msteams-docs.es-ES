---
title: Preparar el inquilino de Office 365
description: Introducción a teams en Office 365
keywords: Configurar la carga de equipos del inquilino de Office 365
ms.openlocfilehash: a246b13ae3a12a486a06ff9d98d37d4d147e4ed4
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874866"
---
# <a name="prepare-your-office-365-tenant"></a>Preparar el inquilino de Office 365

Si es suscriptor de Office 365, puede desarrollar aplicaciones para Microsoft Teams con uno de los siguientes [planes](https://products.office.com/business/compare-more-office-365-for-business-plans):

* Empresa Essentials
* Empresa Premium
* Enterprise E1, E3 y E5
* Developer
* Educación, educación Plus y educación E5

Microsoft Teams también estará disponible para los clientes que se suscribieron a E4 antes de su [jubilación](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).

## <a name="just-need-a-development-environment"></a>¿Solo necesita un entorno de desarrollo?

Si actualmente no tiene una cuenta de Office 365, puede registrarse para obtener una suscripción al [programa de desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program) . Es *gratuita* durante 90 días y se renovará continuamente siempre que la use para la actividad de desarrollo. Si tiene una suscripción de Visual Studio *Enterprise* o *Professional* , ambos programas incluyen una suscripción gratuita al [desarrollador](https://aka.ms/MyVisualStudioBenefits)de Microsoft 365, activa durante la vida de su suscripción a Visual Studio. *Consulte* [configurar una suscripción de desarrollador de Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).

## <a name="enable-microsoft-teams-for-your-organization"></a>Habilitación de Microsoft Teams para la organización 

Si Microsoft Teams no se ha habilitado para su organización, deberá hacerlo primero. Eche un vistazo a nuestras instrucciones detalladas para [Habilitar Microsoft Teams en su organización](/microsoftteams/enable-features-office-365).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Habilitar las aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas

Active la transferencia local de aplicaciones personalizada para su inquilino de desarrollador de la siguiente manera:

1. Inicie sesión en el [centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador. 

2. Seleccione **Mostrar todos los**  -->  **equipos**. 

![imagen del menú del centro de administración](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> La opción "Teams" puede tardar hasta 24 horas en aparecer. Durante la versión provisional, puede [cargar su aplicación personalizada en un entorno de Microsoft Teams](/microsoftteams/upload-custom-apps#validate) para realizar pruebas y validaciones.

3. Vaya a directivas de configuración global de aplicaciones de Microsoft **Teams**  -->  **Setup Policies**  -->  **(valor predeterminado para toda la organización)**  

![activar la vista de transferencia local](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Alternar **cargar aplicaciones personalizadas** en la posición **activado** .

Y eso es todo. El inquilino de prueba permitirá ahora la versión de prueba de aplicaciones personalizada.

> [!Note] 
> Puede tardar hasta 24 horas antes de que se habilite la transferencia local. Durante la versión provisional, puede usar **cargar \<your tenant> para** para probar la aplicación.

![vista de aplicación updload](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Para obtener información completa sobre cómo interactúa esta configuración *See*, vea [Administrar directivas y configuraciones de aplicaciones personalizadas en Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) y [Administrar directivas de configuración de aplicaciones en Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).
