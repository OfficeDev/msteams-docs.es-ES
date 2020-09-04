---
title: Distribuir la aplicación
description: Describe las tres opciones para la distribución de la aplicación
keywords: Teams publicar AppSource de la aplicación de carga de transferencia local de Office distribute
ms.openlocfilehash: d3fd81e69f74b6332d9033412a7b6688239cd801
ms.sourcegitcommit: 02ab2cb7820dc8665bb4ec6a1a40c3b8b8f29d66
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/03/2020
ms.locfileid: "47340965"
---
# <a name="distribute-your-microsoft-teams-app"></a>Distribuir la aplicación de Microsoft Teams

Una vez que haya creado la aplicación, hay tres opciones para distribuirla:

1. [Carga la aplicación directamente](#upload-your-app-directly).
2. [Publique la aplicación en el catálogo de aplicaciones de su organización](#publish-to-your-organizations-app-catalog).
3. [Publique la aplicación a través de AppSource](#publish-to-appsource).

## <a name="enterprise-organizations"></a>Organizaciones empresariales

### <a name="upload-your-app-directly"></a>Cargar la aplicación directamente

Esta es la forma más sencilla de probar y usar la aplicación. Si es el propietario del equipo y carga las [aplicaciones personalizadas está habilitada](/microsoftteams/admin-settings), puede [cargar directamente (o transferir localmente)](./apps-upload.md) la aplicación y comenzar a usarla inmediatamente. Sin embargo, si quiere compartir la aplicación con otros usuarios, tendrá que enviarles el paquete de la aplicación y pedirle que los cargue de manera independiente.

Si quiere distribuir la aplicación de forma más amplia, Teams proporciona una galería en la aplicación para que los usuarios encuentren o descubran las aplicaciones de Microsoft Teams de alta calidad. Para que la soluci? n esté disponible en la galería, debe publicar en el [Catálogo de aplicaciones de su organización](#publish-to-your-organizations-app-catalog) o bien [publicar en AppSource](./appsource/publish.md).

### <a name="publish-to-your-organizations-app-catalog"></a>Publicar en el catálogo de aplicaciones de la organización

El catálogo de aplicaciones de su organización contiene aplicaciones exclusivas de su organización y está completamente bajo el control de su organización. Puede encontrar más información en el artículo [*publicar aplicaciones en el catálogo de aplicaciones de su organización*](/microsoftteams/tenant-apps-catalog-teams). Esta característica solo la pueden administrar los usuarios de Microsoft Teams con privilegios de administrador de inquilinos de Microsoft Office 365.

### <a name="publish-to-appsource"></a>Publicar en AppSource

AppSource (anteriormente conocida como tienda Office) proporciona una ubicación conveniente para que distribuya su aplicación de Microsoft Teams, así como otros tipos de extensibilidad de Office 365, como complementos de Office y complementos de SharePoint. Siga nuestras instrucciones para [enviar la aplicación a AppSource](./appsource/publish.md).

## <a name="government-community-cloud-gcc-organizations"></a>Organizaciones de la nube de la comunidad de administración pública (GCC)

### <a name="upload-your-custom-app-directly-to-teams"></a>Cargar la aplicación personalizada directamente en Teams

 Como administrador de inquilinos de GCC, decidirá si cargar una aplicación personalizada en el entorno del espacio empresarial y si desea publicarla en el catálogo de aplicaciones del espacio empresarial. Microsoft no tiene ni controla sus aplicaciones personalizadas, por lo tanto, debe asegurarse de que todos los extremos cumplen con los requisitos de la organización. Además, si la solución de la aplicación incluye un bot o una extensión de mensaje, deberá completar el registro de [Bot Framework](https://dev.botframework.com/) de la siguiente manera:

1. En la página **conectar con canales** , en **Agregar un canal destacado**, seleccione Microsoft **Teams**.
1. Vaya a la página **configurar MSTeams** (*vea* a continuación).
1. En **mensajes** , seleccione el botón **de opción Microsoft Teams para clientes de la administración pública** .
1. En la esquina inferior izquierda de la página, seleccione **Guardar**.  

>[!IMPORTANT]
> No puede usar la configuración comercial de Microsoft Teams para cargar o transferir localmente la aplicación personalizada a un entorno de GCC, debe seleccionar el botón de radio **Microsoft Teams para clientes de administración pública** para obtener una configuración compatible con GCC.

![Página de configuración de mensajería de Teams](../../assets/images/gcc-configure.png)

> [!NOTE]
>
> * Las instrucciones de carga para los entornos GCC, presentados anteriormente, se aplican a las aplicaciones personalizadas de Teams. </br>
> * De forma predeterminada, las aplicaciones de Microsoft compatibles están habilitadas en el entorno GCC en Teams.
> * Las aplicaciones de terceros se deshabilitan en el nivel de inquilino y deben administrarse a través de [las directivas de permisos de aplicaciones](/microsoftteams/teams-app-permission-policies)de la organización. Asegúrese de revisar todas las aplicaciones de terceros para asegurarse de que se ajustan a las directivas y los procedimientos de la organización.

> [!TIP]
>
> Los socios de Microsoft 365 Developer proporcionan seguridad, administración de datos y detalles de cumplimiento para sus aplicaciones de Microsoft Teams de terceros a través del [programa de certificación de aplicaciones 365 de Microsoft](/microsoft-365-app-certification/overview). *Consulte también* [certificación de aplicaciones de Microsoft Teams](/microsoftteams/platform/concepts/deploy-and-publish/appsource/post-publish/application-certification).
</br></br>
