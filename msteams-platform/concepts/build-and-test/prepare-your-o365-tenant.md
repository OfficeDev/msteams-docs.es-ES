---
title: Preparar el espacio empresarial de Microsoft 365
description: En este módulo, aprenderá a empezar a trabajar con Teams en Microsoft 365 y a crear el entorno de desarrollo.
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: 241040767c610692873e5a68bd215849a8cd26a0
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144393"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Preparar el espacio empresarial de Microsoft 365

Los suscriptores de Microsoft 365 pueden desarrollar aplicaciones para Microsoft Teams con uno de los siguientes planes:

* Básico
* Estándar
* Enterprise E1, E3 y E5
* Developer
* Educación, Educación Plus y Educación E5

> [!NOTE]
>
> * Para obtener más información sobre las suscripciones de Microsoft 365, consulte [planes](https://products.office.com/business/compare-more-office-365-for-business-plans).
> * Teams también está disponible para los clientes que se suscribieron a E4 antes de su [retirada](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).

## <a name="create-your-development-environment"></a>Crear el entorno de desarrollo

Si no tiene una cuenta de Microsoft 365, debe adquirir una suscripción del [Programa para desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program). La suscripción es gratuita durante 90 días y continúa renovándose mientras se use para actividades de desarrollo. Si tiene una suscripción de Visual Studio Enterprise o Professional, ambos programas incluyen una [suscripción de desarrollador](https://aka.ms/MyVisualStudioBenefits) de Microsoft 365 gratuita. Seguirá activa mientras la suscripción a Visual Studio también lo esté. Para obtener más información, consulte [configurar una suscripción a Microsoft 365 para desarrolladores](/office/developer-program/office-365-developer-program-get-started).

## <a name="enable-teams-for-your-organization"></a>Habilitar Teams para su organización

Habilite Teams para su organización y para obtener más información, consulte [habilitar Teams para su organización](/microsoftteams/enable-features-office-365).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Habilitar aplicaciones de Teams personalizadas y activar la carga de aplicaciones personalizadas

Para activar la carga o instalación de prueba de aplicaciones personalizadas para el espacio empresarial del desarrollador:

1. Inicie sesión en el [centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.

2. Seleccione **Mostrar todo** >  **Teams**.

    ![Menú del Centro de administración](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > La opciónTeams puede tardar **hasta 24 horas** en aparecer. Puede [cargar la aplicación personalizada en un entorno de Teams](/microsoftteams/upload-custom-apps#validate) para pruebas y validación en ese momento.

3. Vaya a **aplicaciones de Teams** > **Directivas de configuración** > **Global**.

   ![Activar la vista de transferencia local](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Alterne **Carga de aplicaciones personalizadas** en la posición **Activado**.

5. Seleccione **Guardar**. El inquilino de prueba puede permitir la instalación local de aplicaciones personalizadas.

    > [!Note]
    > La instalación de prueba puede tardar hasta 24 horas en activarse. Mientras tanto, puede usar **cargar para\<your tenant>** probar la aplicación. Para cargar el archivo de paquete .zip de la aplicación, consulte [Cargar aplicaciones personalizadas](/microsoftteams/upload-custom-apps#upload).

    ![Upload vista de la aplicación](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Para obtener una información más completa sobre cómo interactúan estas configuraciones, consulte [Administrar configuración y directivas de aplicaciones personalizadas en Teams](/microsoftteams/teams-custom-app-policies-and-settings) y [Administrar directivas de configuración de aplicaciones en Teams](/microsoftteams/teams-app-setup-policies).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Elegir una configuración de prueba](~/concepts/build-and-test/debug.md)

## <a name="see-also"></a>Vea también

[Adición de datos de prueba al inquilino de prueba de Microsoft 365](~/concepts/build-and-test/test-data.md)
