---
title: Preparar cuentas para crear Teams aplicaciones
author: zyxiaoyuer
description: Preparar cuentas para crear Teams aplicaciones
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 6a215922ff4b89c4afdce187be9b03479e6a54e6
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228167"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>Preparar cuentas para crear Teams aplicaciones

Para desarrollar una aplicación Teams, se necesita al menos Microsoft 365 cuenta con una suscripción válida. Si desea hospedar los recursos back-end en Azure, también se necesita una cuenta de Azure. La cuenta de Azure es opcional si la aplicación existente está hospedada en otro proveedor de nube y desea integrar la aplicación existente en Teams plataforma.

## <a name="microsoft-365-account"></a>Microsoft 365 cuenta

Si no tiene una cuenta de Microsoft 365 existente con una suscripción [válida,](https://developer.microsoft.com/microsoft-365/dev-program)puede crear una uniéndose al programa Microsoft 365 desarrollador . El programa de desarrolladores de Microsoft 365 incluye una suscripción para desarrolladores de Microsoft 365 E5 que puede usar para crear su propio espacio aislado y desarrollar soluciones independientes de su entorno de producción.

## <a name="azure-account"></a>Cuenta de Azure

Si quieres hospedar los recursos relacionados con la aplicación o acceder a recursos dentro de **Azure,** debes tener una suscripción a Azure. Puede crear [una cuenta gratuita antes](https://azure.microsoft.com/free/) de comenzar.

## <a name="join-microsoft-365-developer-program"></a>Unirse Microsoft 365 programa para desarrolladores 

Si no tienes una cuenta Microsoft 365, debes registrarte para una suscripción Microsoft 365 [programa para desarrolladores.](https://developer.microsoft.com/microsoft-365/dev-program) La suscripción es gratuita durante 90 días y continúa renovando mientras la use para la actividad de desarrollo. Si tiene una suscripción Visual Studio Enterprise o Professional, ambos programas incluyen una suscripción Microsoft 365 [desarrollador gratuita.](https://aka.ms/MyVisualStudioBenefits) Está activo siempre que la suscripción Visual Studio esté activa. Para obtener más información, vea [Configurar una Microsoft 365 de desarrollador](https://developer.microsoft.com/microsoft-365/dev-program).

1. Vaya al programa [Microsoft 365 desarrollador](https://developer.microsoft.com/microsoft-365/dev-program).
2. Selecciona **Unirse ahora** y sigue las instrucciones en pantalla.
3. En la pantalla de bienvenida, seleccione **Configurar la suscripción de E5**.
4. Configurar la cuenta de administrador. Después de finalizar, debería ver la siguiente pantalla:

:::image type="content" source="./images/m365-developer-program.png" alt-text="Diagrama que muestra el programa microsoft m365":::

## <a name="accounts-for-microsoft-365-developer-program"></a>Cuentas para Microsoft 365 programa para desarrolladores

Puede registrarse en el programa de desarrolladores con uno de los siguientes tipos de cuenta:

- **Cuenta de Microsoft** 

Puede crear para uso personal: proporciona acceso a todos los productos y servicios en la nube de Microsoft orientados al consumidor, como Outlook, Messenger, OneDrive, MSN, Xbox Live o Microsoft 365. Al registrarse en un buzón de Outlook.com se crea automáticamente una cuenta de Microsoft. Después de crear una cuenta de Microsoft, puede usarla para obtener acceso a los servicios en la nube de Microsoft relacionados con el consumidor o Azure.

- **Cuenta de trabajo**

 El administrador puede emitir para el uso empresarial: proporciona acceso a todos los servicios en la nube de Microsoft de nivel empresarial pequeño, mediano y empresarial, como Azure, Microsoft Intune o Microsoft 365. Cuando inicia sesión como una organización en uno de estos servicios, un directorio en la nube se aprovisiona automáticamente en Azure Active Directory para representar a su organización.

- **Visual Studio id.**

Puede crear para sus suscripciones de Visual Studio Professional o Enterprise: se recomienda usar esta opción para unirse al programa de desarrolladores desde la Galería de Visual Studio para obtener todas las ventajas como suscriptor Visual Studio.

## <a name="teams-customer-app-uploading-sideloading-permission-check"></a>Teams de carga de aplicaciones de cliente (permiso de instalación local)

> [!IMPORTANT]
> Durante el desarrollo, debes cargar la aplicación dentro del Teams sin distribuirla. Esto se conoce como **sideloading**.

Una de las formas de comprobar si tienes una cuenta Teams, comprueba si puedes realizar la instalación local de aplicaciones en Teams:

1. En el Teams, seleccione **Aplicaciones en** la barra izquierda.
2. Selecciona **Administrar las aplicaciones**.
3. Comprueba si puedes ver la opción Upload **una aplicación personalizada** como se muestra en la imagen:

:::image type="content" source="./images/sideload-check.png" alt-text="Diagrama que muestra para cargar una aplicación personalizada":::

Si no puedes ver **Upload una opción de** aplicación personalizada, esto indica que no tienes permiso de instalación local. Sin permiso de instalación local, no podrá realizar ninguna depuración local o remota. Por lo tanto, es muy importante obtener el permiso de instalación local de tu cuenta antes de realizar cualquier depuración para la aplicación Teams usuario. Si es administrador de su inquilino, puede abrir la configuración de instalación local para su inquilino o organización, mientras que si no es administrador, póngase en contacto con el administrador del espacio empresarial para obtener el permiso.

## <a name="enable-custom-app-uploading-sideloading--for-your-organization"></a>Habilitar la carga de aplicaciones personalizadas (instalación local) para la organización

> [!IMPORTANT]
> Para activar la carga o la instalación local de la aplicación personalizada para el inquilino del desarrollador, debes ser el administrador del espacio empresarial.

1. Inicie sesión en [Centro de administración de Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) con sus credenciales de administrador.

2. Seleccione **Mostrar todo**  >  **Teams**.

:::image type="content" source="./images/admin-center-teams.png" alt-text="Diagrama que muestra Teams centro de administración":::

> [!NOTE]
> La opción de Teams puede tardar  hasta **24** horas. Puedes cargar [la aplicación personalizada en un entorno Teams para](/microsoftteams/upload-custom-apps) pruebas y validación en ese momento.

3. Vaya a **Teams directivas de** instalación de  >  **aplicaciones**  >  **globales**.

:::image type="content" source="./images/teams-setup-policy.png" alt-text="Diagrama que muestra la directiva de configuración para Teams":::

4. Alterna Upload aplicaciones personalizadas a **la posición Activa.**

:::image type="content" source="./images/turn-on-sideload.png" alt-text="Diagrama que muestra para activar la instalación local":::

5. Seleccione **Guardar**. El inquilino de prueba puede permitir la instalación local de aplicaciones personalizadas.

:::image type="content" source="./images/save-sideload.png" alt-text="Diagrama que muestra la opción guardar":::

> [!Note]
> La instalación local puede tardar hasta 24 horas en estar activa. Mientras tanto, puedes usar **[cargar para el espacio empresarial]** para probar la aplicación. Para cargar el archivo .zip paquete de la aplicación, consulta [Cargar aplicaciones personalizadas](/microsoftteams/teams-app-setup-policies).

Para obtener más información, consulta Administrar directivas y configuraciones de aplicaciones personalizadas [en Teams](/microsoftteams/teams-custom-app-policies-and-settings) y administrar directivas de configuración de aplicaciones en [Teams](/microsoftteams/teams-app-setup-policies).

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Crear nuevo Teams proyecto](create-new-project.md)

> [!div class="nextstepaction"]
> [Aprovisionar recursos en la nube](provision.md)
