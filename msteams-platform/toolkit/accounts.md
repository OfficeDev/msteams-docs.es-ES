---
title: Preparar cuentas para crear aplicaciones de Teams
author: zyxiaoyuer
description: Preparar cuentas para crear aplicaciones de Teams
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: 21de5611daacbc00630cd7fa4b2aa3704788ed5e
ms.sourcegitcommit: ca902f505a125641c379a917ee745ab418bd1ce6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/14/2022
ms.locfileid: "63464332"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>Preparar cuentas para crear aplicaciones de Teams

Para crear una aplicación Teams y cargarla, se deben preparar las siguientes cuentas:

* [Cuenta de Microsoft 365 con una suscripción válida.](accounts.md#microsoft-365-account)
* [Cuenta de Azure para hospedar los recursos back-end en Azure](accounts.md#azure-account-to-host-backend-resources).

## <a name="microsoft-365-account"></a>Cuenta de Microsoft 365

Para crear una cuenta de Microsoft 365, regístrese para obtener una suscripción al programa para desarrolladores de Microsoft 365. La suscripción es gratuita durante 90 días y continúa renovándose mientras se use para actividades de desarrollo.

Si tiene una suscripción de Visual Studio Enterprise o Professional, ambos programas incluyen una [suscripción de desarrollador](https://aka.ms/MyVisualStudioBenefits) de Microsoft 365 gratuita. Seguirá activa mientras la suscripción a Visual Studio también lo esté. Para obtener más información, vea [suscripción de desarrollador de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).

### <a name="microsoft-365-developer-program"></a>Programa de desarrolladores de Microsoft 365

Para obtener una cuenta de desarrollador de Teams gratuita, únase al programa de desarrolladores de Microsoft 365 y realice los pasos siguientes:

1. Vaya al [programa para desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).
2. Seleccione **Unirse ahora**.
3. Seleccione **Configurar la suscripción de E5**.
4. Configure su cuenta de administrador.

   Después de completar la suscripción, se muestra la siguiente imagen:

    :::image type="content" source="./images/m365-developer-program.png" alt-text="Diagrama que muestra el programa de Microsoft 365":::

### <a name="microsoft-365-developer-account-types"></a>Tipos de cuentas de desarrollador de Microsoft 365

Puede registrarse en el programa de desarrolladores con uno de los siguientes tipos de cuenta:

- **Cuenta de Microsoft para uso personal**

    La cuenta de Microsoft le proporciona acceso a productos y servicios en la nube de Microsoft, como Outlook, Messenger, OneDrive, MSN, Xbox Live o Microsoft 365. Puede registrarse para obtener un buzón de Outlook.com y, así, crear una cuenta de Microsoft que se puede usar para acceder a Azure o a servicios en la nube de Microsoft relacionados con el consumidor.

- **Cuenta profesional de Microsoft para empresas**

     Esta cuenta proporciona acceso a todos los servicios en la nube de Microsoft tales como Azure, Microsoft Intune o Microsoft 365, para pequeñas, medianas y grandes empresas. Cuando se registra en uno de estos servicios como organización, se aprovisiona automáticamente un directorio basado en la nube en Microsoft Azure Active Directory (Azure AD) que representa a su organización.

- **Id. de usuario de Visual Studio**

    El id. de usuario creado para usar una suscripción de Visual Studio Professional o Enterprise se puede usar para unirse al programa de desarrolladores dentro de la Galería de Visual Studio para aprovechar todas las ventajas como suscriptor de Visual Studio.

## <a name="azure-account-to-host-backend-resources"></a>Cuenta de Azure para hospedar recursos back-end

La cuenta de Azure es opcional si la aplicación existente está hospedada en otro proveedor de nube y desea integrar la aplicación existente en la plataforma de Teams.

**Id. de Visual Studio**

Si desea hospedar los recursos relacionados con la aplicación o acceder a recursos en Azure, puede [crear una cuenta gratuita](https://azure.microsoft.com/free/) antes de comenzar. Como alternativa, puede seleccionar hospedar los recursos back-end con otro proveedor de nube o en sus propios servidores si están disponibles desde el dominio público.

## <a name="teams-custom-app-upload-or-sideload-permission"></a>Permiso para cargar la aplicación personalizada de Teams o para la instalación de prueba

> [!IMPORTANT]
> Después de crear la aplicación, debe cargarla en Teams sin distribuirla. Este proceso se conoce como **instalación de prueba**.

   Puede comprobar si el permiso de instalación de prueba está habilitado con Visual Studio Code o con el cliente de Teams.

* **Comprobar el permiso de instalación de prueba mediante Visual Studio Code**

    1. Abra **Visual Studio Code**.
    1. Seleccione el **Kit de herramientas de Teams** en el panel izquierdo. Si no puede ver la opción, asegúrese de que ha instalado la extensión del Kit de herramientas de Teams.
    1. Seleccione **Cuentas** e inicie sesión en su cuenta de Microsoft 365.
    1. Compruebe si puede ver la opción **Instalación de prueba habilitada** como se muestra en la siguiente imagen:

       :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="Habilitar la instalación prueba" border="true":::

* **Comprobar el permiso de instalación de prueba mediante el cliente de Teams**

    1. Abra **Microsoft Teams**.
    2. Seleccione **Aplicaciones** en el panel izquierdo.
    3. Seleccione **Publicar una aplicación**.

       :::image type="content" source="../assets/images/teams-toolkit-v2/publish.png" alt-text="Publicar una aplicación" border="true":::

    4. Compruebe si puede ver la opción **Cargar una aplicación personalizada** como se muestra en la siguiente imagen:

       :::image type="content" source="../assets/images/teams-toolkit-v2/upload.png" alt-text="Cargar una aplicación personalizada" border="true":::.

        Si no puede ver la opción **Cargar una aplicación personalizada**, esto indica que no tiene permiso para llevar a cabo la instalación de prueba.
        * Para un administrador de inquilinos, habilite la configuración de instalación de prueba para su inquilino u organización en el Centro de administración de Teams.
        * Si no es administrador de inquilinos, deberá ponerse en contacto con el administrador de inquilinos para habilitar la instalación de prueba.

### <a name="upload-your-custom-app"></a>Cargar la aplicación personalizada

> [!IMPORTANT]
> Para activar la carga o instalación de prueba de aplicaciones personalizadas para el inquilino de desarrollador, debe ser administrador del inquilino.

**Para cargar la aplicación personalizada**

1. Inicie sesión en el [centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.

2. Seleccione **Mostrar todo** >  **Teams**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/5.png" alt-text="mostrar todo." border="true":::

   > [!Note]
   > La opción **Teams** puede tardar **hasta 24 horas** en aparecer. Puede [cargar la aplicación personalizada en un entorno de Teams](/microsoftteams/upload-custom-apps) para pruebas y validación.

3. Vaya a **aplicaciones de Teams** > **Directivas de configuración**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/3.png" alt-text="establecer directivas":::

4. Establezca el botón de alternancia **Carga de aplicaciones personalizadas** en la posición **Activado**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/4.png" alt-text="alternancia":::

5. Haga clic en **Guardar**.

   > [!Note]
   > La instalación de prueba puede tardar hasta 24 horas en activarse. Mientras tanto, puede usar **cargar para el inquilino** y, así, probar la aplicación. Para cargar el archivo de paquete .zip de la aplicación, consulte [Cargar aplicaciones personalizadas](/microsoftteams/teams-app-setup-policies).

Para obtener más información, consulte [Administrar configuración y directivas de aplicaciones personalizadas en Teams](/microsoftteams/teams-custom-app-policies-and-settings) y [Administrar directivas de configuración de aplicaciones en Teams](/microsoftteams/teams-app-setup-policies).

## <a name="see-also"></a>Vea también

* [Crear una nueva aplicación de Teams con el Kit de herramientas de Teams](create-new-project.md)
* [Aprovisionar recursos en la nube](provision.md)
* [Implementar la aplicación de Teams en la nube](deploy.md)
* [Publicar la aplicación de Teams](TeamsFx-collaboration.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)