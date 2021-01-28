---
title: Distribuir la aplicación
description: Describe las tres opciones para distribuir la aplicación
ms.topic: conceptual
keywords: teams publish store office distribute AppSource sideload upload app
ms.openlocfilehash: 9c457608711bc491aeb9062a8ac2de58e78a90bd
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014190"
---
# <a name="distribute-your-microsoft-teams-app"></a>Distribuir la aplicación de Microsoft Teams

Una vez que hayas creado la aplicación, hay tres opciones para distribuirla:

1. [Cargue la aplicación directamente.](#upload-your-app-directly)
2. [Publique la aplicación en el catálogo de aplicaciones de su organización.](#publish-to-your-organizations-app-catalog)
3. [Publicar la aplicación a través de AppSource](#publish-to-appsource).

## <a name="enterprise-organizations"></a>Organizaciones empresariales

### <a name="upload-your-app-directly"></a>Cargar la aplicación directamente

Esta es la forma más sencilla de probar y usar la aplicación. Si es el propietario del [](/microsoftteams/admin-settings)equipo o si está habilitada la carga de aplicaciones personalizadas, puede cargar (o realizar una instalación de instalación de instalación [local)](./apps-upload.md) directamente de la aplicación y empezar a usarlo inmediatamente. Sin embargo, si quieres compartir la aplicación con otras personas, tendrás que enviarles el paquete de la aplicación y pedirles que la carguen de forma independiente.

Si quiere distribuir la aplicación de forma más amplia, Teams proporciona una galería desde la aplicación para que los usuarios puedan encontrar o descubrir aplicaciones de Teams de alta calidad. Para que la solución esté disponible [](#publish-to-your-organizations-app-catalog) en la galería, debe publicarla en el catálogo de aplicaciones de su organización o [publicarla en AppSource.](./appsource/publish.md)

### <a name="publish-to-your-organizations-app-catalog"></a>Publicar en el catálogo de aplicaciones de la organización

El catálogo de aplicaciones de la organización contiene aplicaciones exclusivas de su organización y está completamente bajo el control de su organización. Puede encontrar más información en el artículo Publicar aplicaciones en el catálogo de [*aplicaciones de su organización.*](/microsoftteams/tenant-apps-catalog-teams) Esta característica solo la pueden administrar los usuarios de Teams con Microsoft Office de administrador de inquilinos 365.

### <a name="publish-to-appsource"></a>Publicar en AppSource

AppSource (anteriormente conocido como Tienda Office) proporciona una ubicación cómoda para distribuir la aplicación de Microsoft Teams, así como otros tipos de extensibilidad de Office 365, como complementos de Office y complementos de SharePoint. Sigue nuestras directrices [para enviar tu aplicación a AppSource.](./appsource/publish.md)

## <a name="government-community-cloud-gcc-organizations"></a>Organizaciones de Government Community Cloud (GCC)

### <a name="upload-your-custom-app-directly-to-teams"></a>Cargar la aplicación personalizada directamente en Teams

 Como administrador de inquilinos de GCC, decidirá si va a cargar una aplicación personalizada en su entorno de inquilino y si desea publicarla en el catálogo de aplicaciones del espacio empresarial. Microsoft no posee ni controla las aplicaciones personalizadas, por lo tanto, debe asegurarse de que todos los puntos de conexión cumplen con los requisitos de su organización. Además, si la solución de la aplicación incluye un bot o una extensión de mensaje, deberá completar el registro de [Bot Framework](https://dev.botframework.com/) de la siguiente manera:

1. En la **página Conectar a canales,** en **Agregar un canal destacado,** seleccione **Teams**.
1. Vaya a la **página Configurar MSTeams** *(vea a continuación).*
1. En **Mensajería,** seleccione el **botón de radio Microsoft Teams para clientes gubernamentales.**
1. En la esquina inferior izquierda de la página, seleccione **Guardar**.  

>[!IMPORTANT]
> No puede usar la configuración comercial de Teams para cargar o realizar una instalación de prueba de la aplicación personalizada en un entorno GCC, debe seleccionar el botón de radio Microsoft **Teams** para clientes gubernamentales para una configuración compatible con GCC.

![Página de configuración de mensajería de Teams](../../assets/images/gcc-configure.png)

> [!NOTE]
>
> * Las instrucciones de carga para entornos GCC, presentadas anteriormente, se aplican a las aplicaciones personalizadas de Teams. </br>
> * Las aplicaciones de Microsoft compatibles están habilitadas en el entorno GCC, de forma predeterminada, en Teams.
> * Las aplicaciones de terceros están deshabilitadas en el nivel de inquilino y deben administrarse a través de las directivas de permisos de [aplicación de su organización.](/microsoftteams/teams-app-permission-policies) Asegúrese de revisar todas las aplicaciones de terceros para asegurarse de que se alinean con las directivas y procedimientos de su organización.

> [!TIP]
>
> Los partners desarrolladores de Microsoft 365 proporcionan detalles de seguridad, control de datos y cumplimiento para sus aplicaciones de Microsoft Teams de terceros a través del Programa de certificación de aplicaciones [de Microsoft 365.](/microsoft-365-app-certification/overview) *Vea también certificación* [de aplicaciones de Microsoft Teams.](/microsoftteams/platform/concepts/deploy-and-publish/appsource/post-publish/application-certification)
</br></br>
