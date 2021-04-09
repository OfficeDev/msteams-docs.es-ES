---
title: Preparar el espacio empresarial de Microsoft 365
description: Cómo empezar a trabajar con Teams en Microsoft 365
ms.topic: how-to
keywords: Configurar la carga de Microsoft 365 tenant Teams
ms.openlocfilehash: aa7f994744f8b1c62aa32122a5006cfa0f22d391
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634763"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Preparar el espacio empresarial de Microsoft 365

Los suscriptores de Microsoft 365 pueden desarrollar aplicaciones para Microsoft Teams con uno de los siguientes planes:

* Basic
* Estándar
* Enterprise E1, E3 y E5
* Developer
* Education, Education Plus y Education E5

> [!NOTE]
> Para obtener más información sobre las suscripciones de Microsoft 365, vea [planes](https://products.office.com/business/compare-more-office-365-for-business-plans).
> 
> Microsoft Teams también está disponible para los clientes que se han suscrito a E4 antes de su [retirada.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)

## <a name="create-your-development-environment"></a>Crear el entorno de desarrollo

Si no tiene una cuenta de Microsoft 365, debe registrarse para obtener una suscripción al Programa para desarrolladores de [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program) La suscripción es gratuita durante 90 días y continúa renovando mientras la use para la actividad de desarrollo. Si tiene una suscripción Visual Studio Enterprise o Professional, ambos programas incluyen una suscripción gratuita para desarrolladores [de](https://aka.ms/MyVisualStudioBenefits)Microsoft 365 . Está activo durante el tiempo que la suscripción Visual Studio esté activa. Para obtener más información, consulta Configurar una suscripción para desarrolladores de [Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).

## <a name="enable-microsoft-teams-for-your-organization"></a>Habilitar Microsoft Teams para su organización

Habilita Microsoft Teams para tu organización y echa un vistazo a nuestras instrucciones detalladas para habilitar [Teams para tu organización.](/microsoftteams/enable-features-office-365)

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Habilitar aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas

**Para activar la carga o la instalación local de la aplicación personalizada para el inquilino del desarrollador**

1. Inicie sesión en [el Centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.

2. Seleccione **Mostrar todos los**  >  **equipos**.

    ![imagen del menú del Centro de administración](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > La opción **Teams** puede tardar hasta 24 horas en aparecer. Puedes cargar [la aplicación personalizada en un entorno de Teams para](/microsoftteams/upload-custom-apps#validate) realizar pruebas y validación en ese momento.

3. Vaya a **Directivas de instalación de aplicaciones** de Teams  >    >  **Global**.

   ![Activar la vista de instalación local](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Alterna **la carga de aplicaciones personalizadas** en la **posición** activa.

5. Seleccione **Guardar**.
   El inquilino de prueba puede permitir la instalación local de aplicaciones personalizadas.

    > [!Note]
    > La instalación local puede tardar hasta 24 horas en estar activa. Durante el período provisional, puedes usar **la carga para probar \<your tenant>** la aplicación.

    ![vista de aplicación updload](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Para obtener información completa sobre cómo interactúan estas configuraciones, consulta Administrar directivas y configuraciones de aplicaciones personalizadas en [Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) y Administrar directivas de configuración de aplicaciones en [Microsoft Teams.](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"] 
> [Elegir una configuración de prueba](~/concepts/build-and-test/debug.md)
> 


