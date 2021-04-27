---
title: Preparar el espacio empresarial de Microsoft 365
description: Cómo empezar a trabajar con Teams en Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Configurar la carga de Microsoft 365 tenant Teams
ms.openlocfilehash: 45d6dfb57fd2faa5bb303aac1dff86be142d0dc2
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019947"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Preparar el espacio empresarial de Microsoft 365

Los suscriptores de Microsoft 365 pueden desarrollar aplicaciones para Microsoft Teams con uno de los siguientes planes:

* Basic
* Estándar
* Enterprise E1, E3 y E5
* Developer
* Education, Education Plus y Education E5

> [!NOTE]
> * Para obtener más información sobre las suscripciones de Microsoft 365, vea [planes](https://products.office.com/business/compare-more-office-365-for-business-plans).
> * Teams también está disponible para los clientes que se han suscrito a E4 antes de su [retirada.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)

## <a name="create-your-development-environment"></a>Crear el entorno de desarrollo

Si no tiene una cuenta de Microsoft 365, debe registrarse para obtener una suscripción al Programa para desarrolladores de [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program) La suscripción es gratuita durante 90 días y continúa renovando mientras la use para la actividad de desarrollo. Si tiene una suscripción Visual Studio Enterprise o Professional, ambos programas incluyen una suscripción gratuita para desarrolladores [de](https://aka.ms/MyVisualStudioBenefits)Microsoft 365 . Está activo siempre que la suscripción Visual Studio esté activa. Para obtener más información, [consulta Configurar una suscripción de desarrollador de Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).

## <a name="enable-teams-for-your-organization"></a>Habilitar Teams para su organización

Habilite Teams para su organización y para obtener más información, vea [habilitar Teams para su organización.](/microsoftteams/enable-features-office-365)

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Habilitar aplicaciones personalizadas de Teams y activar la carga de aplicaciones personalizadas

**Para activar la carga o la instalación local de la aplicación personalizada para el inquilino del desarrollador**

1. Inicie sesión en [el Centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.

2. Seleccione **Mostrar todos los**  >  **equipos**.

    ![Menú centro de administración](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > La opción **Teams** puede tardar hasta 24 horas en aparecer. Puedes cargar [la aplicación personalizada en un entorno de Teams para](/microsoftteams/upload-custom-apps#validate) realizar pruebas y validación en ese momento.

3. Vaya a **Directivas de instalación de aplicaciones** de Teams  >    >  **Global**.

   ![Activar la vista de instalación local](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Alterna **Cargar aplicaciones personalizadas** a **la posición Activa.**

5. Seleccione **Guardar**. El inquilino de prueba puede permitir la instalación local de aplicaciones personalizadas.

    > [!Note]
    > La instalación local puede tardar hasta 24 horas en estar activa. In the interim, you can use **upload for to \<your tenant>** test your app. Para cargar el archivo de paquete .zip de la aplicación, consulta [Cargar aplicaciones personalizadas.](/microsoftteams/upload-custom-apps#upload)

    ![Vista Cargar aplicación](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Para obtener información completa sobre cómo interactúan estas configuraciones, consulta Administrar directivas y configuraciones de aplicaciones personalizadas en [Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) y administrar directivas de configuración [de aplicaciones en Teams.](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"] 
> [Elegir una configuración de prueba](~/concepts/build-and-test/debug.md)

