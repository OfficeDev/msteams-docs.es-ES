---
title: Preparar el inquilino de Office 365
description: Introducción a teams en Office 365
keywords: Configurar la carga de equipos del inquilino de Office 365
ms.openlocfilehash: e07ffe7f5325be1293a49934669f36c81613278b
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914570"
---
# <a name="prepare-your-office-365-tenant"></a>Preparar el inquilino de Office 365

Si es suscriptor de Office 365, puede desarrollar aplicaciones para Microsoft Teams con uno de los siguientes [planes](https://products.office.com/business/compare-more-office-365-for-business-plans):

* Empresa Essentials
* Empresa Premium
* Enterprise E1, E3 y E5
* Programador
* Educación, educación Plus y educación E5

Microsoft Teams también estará disponible para los clientes que se suscribieron a E4 antes de su [jubilación](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).

## <a name="just-need-a-development-environment"></a>¿Solo necesita un entorno de desarrollo?

Si actualmente no tiene una cuenta de Office 365, puede registrarse para obtener una suscripción al [programa de desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program) . Es *gratuita* durante 90 días y se renovará continuamente siempre que la use para la actividad de desarrollo. Si tiene una suscripción de Visual Studio *Enterprise* o *Professional* , ambos programas incluyen una suscripción gratuita al [desarrollador](https://aka.ms/MyVisualStudioBenefits)de Microsoft 365, activa durante la vida de su suscripción a Visual Studio. *Consulte* [configurar una suscripción de desarrollador de Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).

## <a name="enable-microsoft-teams-for-your-organization"></a>Habilitación de Microsoft Teams para la organización

Si Microsoft Teams no se ha habilitado para su organización, deberá hacerlo primero. Eche un vistazo a nuestras instrucciones detalladas para [Habilitar Microsoft Teams en su organización](https://docs.microsoft.com/microsoftteams/enable-features-office-365).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Habilitar las aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas

> [!Note] 
> Si usa la plataforma de desarrollador de Office 365 para compilar la aplicación, esta configuración ya debe estar configurada para permitirle crear, cargar y probar la aplicación.

Hay tres opciones de configuración relevantes para la habilitación de aplicaciones personalizadas y la carga de aplicaciones personalizadas:

* **Configuración** => de aplicación personalizada para toda la organización**permitir la interacción con aplicaciones** => personalizadas **: esta** configuración habilita o deshabilita las aplicaciones personalizadas para su organización. Debe estar activada. 
* **Configuración** => de la aplicación personalizada de equipo**permitir a los miembros cargar aplicaciones** => personalizadas**activado/desactivado** : esta configuración se aplica a cada equipo individual dentro de Microsoft Teams. Si quiere instalar la aplicación para un equipo específico, esto tendrá que estar activado para ese equipo.
* **User custom app policy** => El usuario de la Directiva de aplicación personalizada => **del** usuario**puede cargar aplicaciones personalizadas**: esta configuración controla los permisos de un usuario individual. Deberá habilitar esto para los usuarios que tengan permiso para cargar aplicaciones personalizadas.

Para obtener información completa sobre cómo interactúa esta configuración, *consulte* [administrar la configuración y las directivas de la aplicación personalizada en Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) y [administrar las directivas de configuración de aplicaciones en Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).
