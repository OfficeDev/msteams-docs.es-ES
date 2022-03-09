---
title: Preparar el espacio empresarial de Microsoft 365
description: Cómo empezar a trabajar con Teams en Microsoft 365
ms.topic: how-to
ms.localizationpriority: medium
keywords: Configurar Microsoft 365 inquilino Teams carga
ms.openlocfilehash: 9543ef4fcd3065def2f25aa8180c157a55b1d2ba
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399131"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Preparar el espacio empresarial de Microsoft 365

Microsoft 365 suscriptores pueden desarrollar aplicaciones para Microsoft Teams con uno de los siguientes planes:

* Básico
* Estándar
* Enterprise E1, E3 y E5
* Desarrollador
* Education, Education Plus y Education E5

> [!NOTE]
>
> * Para obtener más información sobre Microsoft 365 suscripciones, vea [planes](https://products.office.com/business/compare-more-office-365-for-business-plans).
> * Teams también está disponible para los clientes que se han suscrito a E4 antes de su [retirada](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).

## <a name="create-your-development-environment"></a>Crear el entorno de desarrollo

Si no tiene una cuenta Microsoft 365, debe registrarse para una [suscripción Microsoft 365 Programa para desarrolladores](https://developer.microsoft.com/microsoft-365/dev-program). La suscripción es gratuita durante 90 días y continúa renovando mientras la use para la actividad de desarrollo. Si tienes una suscripción Visual Studio Enterprise o Professional, ambos programas incluyen una suscripción Microsoft 365 [desarrollador gratuita](https://aka.ms/MyVisualStudioBenefits). Está activo siempre que la suscripción Visual Studio esté activa. Para obtener más información, consulta [Configurar una suscripción Microsoft 365 desarrollador.](/office/developer-program/office-365-developer-program-get-started)

## <a name="enable-teams-for-your-organization"></a>Habilitar Teams para su organización

Habilite Teams para su organización y para obtener más información, [consulte enabling Teams for your organization](/microsoftteams/enable-features-office-365).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Habilitar aplicaciones Teams personalizadas y activar la carga de aplicaciones personalizadas

Para activar la carga o la instalación local de la aplicación personalizada para el inquilino del desarrollador:

1. Inicie sesión en [Centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.

2. Seleccione **Mostrar todo** >  **Teams**.

    ![Menú centro de administración](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > La opción de Teams puede tardar hasta 24 horas en  aparecer. Puedes cargar [la aplicación personalizada en un entorno Teams para](/microsoftteams/upload-custom-apps#validate) pruebas y validación en ese momento.

3. Vaya a **Teams appsSetup** >  **PoliciesGlobal** > .

   ![Activar la vista de instalación local](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Alterna **Upload aplicaciones personalizadas** a la **posición Activa**.

5. Seleccione **Guardar**. El inquilino de prueba puede permitir la instalación local de aplicaciones personalizadas.

    > [!Note]
    > La instalación local puede tardar hasta 24 horas en estar activa. In the interim, you can use **upload for to \<your tenant>** test your app. Para cargar el archivo .zip paquete de la aplicación, consulta [Cargar aplicaciones personalizadas](/microsoftteams/upload-custom-apps#upload).

    ![Upload vista de aplicación](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Para obtener información completa sobre cómo interactúan estas configuraciones, consulta Administrar las directivas y la configuración de aplicaciones personalizadas en [Teams](/microsoftteams/teams-custom-app-policies-and-settings) y administrar directivas de configuración de [aplicaciones en Teams](/microsoftteams/teams-app-setup-policies).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Elegir una configuración de prueba](~/concepts/build-and-test/debug.md)

## <a name="see-also"></a>Vea también

[Agregar datos de prueba al inquilino Microsoft 365 prueba](~/concepts/build-and-test/test-data.md)
