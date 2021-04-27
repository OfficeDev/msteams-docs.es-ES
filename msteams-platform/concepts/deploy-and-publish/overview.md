---
title: Distribuir la aplicación
description: Describe las tres opciones para distribuir la aplicación
ms.topic: conceptual
localization_priority: Normal
keywords: teams publish store office distribute AppSource sideload upload app
ms.openlocfilehash: a033b90be436fbf20ef11fe95059d04388cefdf8
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020782"
---
# <a name="distribute-your-microsoft-teams-app"></a>Distribuir la aplicación de Microsoft Teams

Una vez creada la aplicación, hay tres opciones para distribuirla:

1. [Cargue la aplicación directamente](#upload-your-app-directly).
2. [Publique la aplicación en el catálogo de](#publish-to-your-organizations-app-catalog)aplicaciones de su organización.
3. [Publicar la aplicación a través de AppSource](#publish-to-appsource).

## <a name="enterprise-organizations"></a>Organizaciones empresariales

### <a name="upload-your-app-directly"></a>Cargar la aplicación directamente

Esta es la forma más sencilla de probar y usar la aplicación. Si eres el propietario del equipo o la carga de aplicaciones personalizadas está [habilitada,](/microsoftteams/admin-settings)puedes cargar directamente (o descargar [localmente)](./apps-upload.md) la aplicación y empezar a usarlo inmediatamente. Sin embargo, si quieres compartir la aplicación con otros usuarios, tendrás que enviarles el paquete de la aplicación y pedirles que la carguen de forma independiente.

Si quieres distribuir la aplicación de forma más amplia, Teams proporciona una galería desde la aplicación para que los usuarios encuentren o descubran aplicaciones de Teams de alta calidad. Para que la solución esté disponible [](#publish-to-your-organizations-app-catalog) en la galería, debe publicar en el catálogo de aplicaciones de su organización o [publicar en AppSource](./appsource/publish.md).

### <a name="publish-to-your-organizations-app-catalog"></a>Publicar en el catálogo de aplicaciones de la organización

El catálogo de aplicaciones de la organización contiene aplicaciones únicas para su organización y está completamente bajo el control de su organización. Puedes encontrar más información en el artículo Publicar aplicaciones en el catálogo de aplicaciones [*de tu organización.*](/microsoftteams/tenant-apps-catalog-teams) Esta característica solo la pueden administrar los usuarios de Teams con Microsoft Office 365 privilegios de administrador de inquilinos.

### <a name="publish-to-appsource"></a>Publicar en AppSource

AppSource (anteriormente conocida como Tienda Office) proporciona una ubicación conveniente para distribuir la aplicación de Microsoft Teams, así como otros tipos de extensibilidad de Office 365, como complementos de Office y complementos de SharePoint. Siga nuestras directrices [para enviar la aplicación a AppSource](./appsource/publish.md).

## <a name="government-community-cloud-gcc-organizations"></a>Organizaciones de la nube de la comunidad gubernamental (GCC)

### <a name="upload-your-custom-app-directly-to-teams"></a>Cargar la aplicación personalizada directamente en Teams

 Como administrador de inquilinos de GCC, decidirás si quieres cargar una aplicación personalizada en el entorno de inquilino y si quieres publicarla en el catálogo de aplicaciones de inquilino. Microsoft no es propietario ni controla las aplicaciones personalizadas, por lo tanto, debe asegurarse de que todos los puntos de conexión cumplen con los requisitos de su organización. Además, si la solución de la aplicación incluye un bot o una extensión de mensaje, tendrás que completar el registro [de Bot Framework](https://dev.botframework.com/) de la siguiente manera:

1. En la **página Conectar a canales,** en Agregar un **canal destacado,** seleccione **Teams**.
1. Vaya a la **página Configurar MSTeams** *(vea a continuación).*
1. En **Mensajería,** seleccione el botón **de radio Microsoft Teams para clientes** gubernamentales.
1. En la esquina inferior izquierda de la página, seleccione **Guardar**.  

>[!IMPORTANT]
> No puede usar la configuración comercial de Teams para cargar o cargar localmente la aplicación personalizada en un entorno GCC, debe seleccionar el botón de radio **Microsoft Teams para** clientes gubernamentales para una configuración compatible con GCC.

![Página de configuración de mensajería de Teams](../../assets/images/gcc-configure.png)

> [!NOTE]
>
> * Las instrucciones de carga para entornos GCC, que se han presentado anteriormente, se aplican a las aplicaciones personalizadas de Teams. </br>
> * Las aplicaciones de Microsoft compatibles están habilitadas en el entorno GCC, de forma predeterminada, en Teams.
> * Las aplicaciones de terceros están deshabilitadas en el nivel de inquilino y deben administrarse a través de las directivas de permisos [de aplicaciones de la organización.](/microsoftteams/teams-app-permission-policies) Asegúrese de revisar todas las aplicaciones de terceros para asegurarse de que se alinean con las directivas y procedimientos de su organización.

> [!TIP]
>
> Los partners para desarrolladores de Microsoft 365 proporcionan detalles de seguridad, control de datos y cumplimiento para sus aplicaciones de Teams de terceros a través del Programa de certificación de aplicaciones de [Microsoft 365](/microsoft-365-app-certification/overview). *Vea también Microsoft* [Teams App Certification](/microsoftteams/platform/concepts/deploy-and-publish/appsource/post-publish/application-certification).
</br></br>
