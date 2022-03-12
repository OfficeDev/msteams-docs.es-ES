---
title: Preparar cuentas para crear Teams aplicaciones
author: zyxiaoyuer
description: Preparar cuentas para crear Teams aplicaciones
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9dbfa97b892f2234b53eb42b5d5764b8f6fd6e93
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452574"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>Preparar cuentas para crear Teams aplicaciones

Para desarrollar Teams aplicación, necesitas al menos una cuenta Microsoft 365 con suscripción válida. Si desea hospedar los recursos back-end en Azure, necesita una cuenta de Azure. La cuenta de Azure es opcional si la aplicación existente está hospedada en otro proveedor de nube y desea integrar la aplicación existente en Teams plataforma.

## <a name="microsoft-365-account"></a>Cuenta de Microsoft 365

Si no tiene una cuenta de Microsoft 365 existente con una suscripción válida, puede crear una uniéndose al programa [Microsoft 365 desarrollador.](https://developer.microsoft.com/microsoft-365/dev-program) El Microsoft 365 para desarrolladores incluye una suscripción Microsoft 365 E5 desarrollador que puedes usar para crear tu propio espacio aislado y desarrollar soluciones independientes del entorno de producción.

## <a name="azure-account"></a>Cuenta de Azure

Si quieres hospedar los recursos relacionados con la aplicación o acceder a recursos dentro de Azure, debes tener una suscripción a Azure. Puede crear [una cuenta gratuita antes](https://azure.microsoft.com/free/) de comenzar.

## <a name="join-microsoft-365-developer-program"></a>Unirse Microsoft 365 programa para desarrolladores

Si no tienes una cuenta Microsoft 365, debes registrarte para una suscripción Microsoft 365 [programa para desarrolladores](https://developer.microsoft.com/microsoft-365/dev-program). La suscripción es gratuita durante 90 días y continúa renovando mientras la use para la actividad de desarrollo. Si tienes una suscripción Visual Studio Enterprise o Professional, ambos programas incluyen una suscripción Microsoft 365 [desarrollador gratuita](https://aka.ms/MyVisualStudioBenefits). Está activo siempre que la suscripción Visual Studio esté activa. Para obtener más información, consulta [Configurar una suscripción Microsoft 365 desarrollador.](https://developer.microsoft.com/microsoft-365/dev-program)

1. Vaya al programa [Microsoft 365 desarrollador](https://developer.microsoft.com/microsoft-365/dev-program).
2. Seleccione **Unirse ahora**.
3. Selecciona **Configurar suscripción A5**.
4. Configurar la cuenta de administrador. Después de finalizar, debería ver la siguiente pantalla:

:::image type="content" source="./images/m365-developer-program.png" alt-text="Diagrama que muestra Microsoft 365 programa":::

## <a name="accounts-for-microsoft-365-developer-program"></a>Cuentas para Microsoft 365 programa para desarrolladores

Puede registrarse en el programa de desarrolladores con uno de los siguientes tipos de cuenta:

* **Cuenta de Microsoft para uso personal**

  Proporciona acceso a todos los productos y servicios en la nube de Microsoft orientados al consumidor, como Outlook, Messenger, OneDrive, MSN, Xbox Live o Microsoft 365. Al registrarse en un buzón de Outlook.com se crea automáticamente una cuenta de Microsoft. Después de crear una cuenta de Microsoft, puede usarla para obtener acceso a los servicios en la nube de Microsoft relacionados con el consumidor o Azure.

* **Cuenta de trabajo para empresas**

  Proporciona acceso a todos los servicios en la nube de Microsoft de nivel empresarial, mediano y pequeño, como Azure, Microsoft Intune o Microsoft 365. Cuando se registra en uno de estos servicios como organización, un directorio basado en la nube se aprovisiona automáticamente en Microsoft Azure Active Directory (Azure AD) para representar a su organización.

* **Visual Studio id.**

  Puede crear para sus suscripciones de Visual Studio Professional o Enterprise: se recomienda usar esta opción para unirse al programa de desarrolladores desde la Galería de Visual Studio para obtener todas las ventajas como suscriptor Visual Studio.

## <a name="teams-customer-app-upload-or-sideload-permission"></a>Teams de carga o instalación local de la aplicación del cliente

> [!IMPORTANT]
> Durante el desarrollo, debes cargar la aplicación dentro de tu Teams sin distribuirla. Esto se conoce como **instalación local**.

En la siguiente lista se proporcionan pasos para comprobar si está habilitado el permiso de la aplicación de instalación local. Las dos formas diferentes son las siguientes:

* **Para usar código de Microsoft Visual Studio**

    1. Abra **Visual Studio Code**.
    1. Seleccione **Teams Toolkit** desde el panel izquierdo.
    1. Seleccione **Cuentas** e inicie sesión en su Microsoft 365 cuenta.
    1. Compruebe si puede ver la opción **Instalación local habilitada** como se muestra en la imagen:

       :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="Habilitar la instalación local":::

* **Para usar Teams cuenta**

    1. Abra **Microsoft Teams**.
    2. Selecciona **Aplicaciones en** la barra izquierda.
    3. Selecciona **Publicar una aplicación**.

       :::image type="content" source="../assets/images/teams-toolkit-v2/publish.png" alt-text="Publicar una aplicación":::

    4. Comprueba si puedes ver la opción Upload **una aplicación personalizada** como se muestra en la imagen:

       :::image type="content" source="../assets/images/teams-toolkit-v2/upload.png" alt-text="Upload una aplicación personalizada":::

Si no puedes ver **una Upload aplicación** personalizada, esto indica que no tienes permiso para la instalación local. Sin permiso de instalación local, no podrá realizar ninguna depuración local o remota. Por lo tanto, es muy importante obtener el permiso de instalación local de tu cuenta antes de realizar cualquier depuración para la aplicación Teams usuario. Si es administrador de su inquilino, puede abrir la configuración de instalación local para su inquilino u organización. Si no es administrador, póngase en contacto con el administrador del espacio empresarial para obtener el permiso.

## <a name="enable-custom-app-uploading-for-your-organization"></a>Habilitar la carga de aplicaciones personalizadas para la organización

> [!IMPORTANT]
> Para activar la carga o la instalación local de la aplicación personalizada para el inquilino del desarrollador, debes ser el administrador del espacio empresarial.

1. Inicie sesión en [Centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.

2. Seleccione **Mostrar todo** >  **Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/5.png" alt-text="mostrar todo":::

> [!NOTE]
> La opción de Teams puede tardar hasta **24** horas en  aparecer. Puedes cargar [la aplicación personalizada en un entorno Teams para](/microsoftteams/upload-custom-apps) pruebas y validación en ese momento.

3. Vaya a **Teams appsSetup** >  **PoliciesGlobal** > .

   :::image type="content" source="../assets/images/teams-toolkit-v2/3.png" alt-text="set olicies":::

4. Alterna Upload aplicaciones personalizadas a la **posición Activa**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/4.png" alt-text="alternar":::

5. Seleccione **Guardar**.

> [!Note]
> La instalación local puede tardar hasta 24 horas en estar activa. Mientras tanto, puedes usar la carga **del espacio empresarial** para probar la aplicación. Para cargar el archivo .zip paquete de la aplicación, consulta [Cargar aplicaciones personalizadas](/microsoftteams/teams-app-setup-policies).

Para obtener más información, consulta [Administrar directivas](/microsoftteams/teams-custom-app-policies-and-settings) y configuraciones de aplicaciones personalizadas en Teams y [administrar directivas de configuración de aplicaciones en Teams](/microsoftteams/teams-app-setup-policies).

## <a name="see-also"></a>Vea también

* [Crear nuevo Teams proyecto](create-new-project.md)
* [Aprovisionar recursos en la nube](provision.md)
