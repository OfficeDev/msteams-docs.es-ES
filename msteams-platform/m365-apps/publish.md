---
title: Publicación de aplicaciones Teams para Microsoft 365
description: Haga que las aplicaciones de Teams habilitadas para Microsoft 365 sean reconocibles para los usuarios en Teams, Outlook y Office
ms.date: 05/24/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 66b5adb6162222da155318aeb818fd681a664816
ms.sourcegitcommit: 264d3cc84d6eec4ab025cf86a7a6f4865f1aed07
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2022
ms.locfileid: "65653712"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>Publicación de aplicaciones Teams para Microsoft 365

Las aplicaciones de Teams habilitadas para Microsoft 365 se admiten para su uso en producción en Microsoft Teams. Puede distribuir estas aplicaciones a audiencias en versión preliminar que *usen las versiones* de versión dirigida de outlook.com y office.com, y la compilación *del canal beta* de Outlook para Windows escritorio. Las opciones de distribución y los procesos de las aplicaciones de Teams habilitadas para Microsoft 365 son las mismas que para las aplicaciones Teams tradicionales.

Una vez publicada, la aplicación se podrá detectar como una aplicación instalable desde el Outlook y Aplicación de Office almacenes, además de la tienda Teams. La aplicación usa los permisos definidos en Teams entre Outlook y Office. Teams los administradores pueden [administrar el acceso a Teams aplicaciones en Microsoft 365](/MicrosoftTeams/manage-third-party-teams-apps) para los usuarios de su organización.

:::image type="content" source="images/outlook-office-app-store.png" alt-text="pantallas de instalación de Outlook y Office.com para las aplicaciones SurveyMonkey y MURAL Teams":::

## <a name="single-tenant-distribution"></a>Distribución de cuenta empresarial única

las extensiones de mensaje habilitadas para Outlook se pueden distribuir para los inquilinos de prueba y producción de varias maneras:

### <a name="teams-client"></a>Cliente de Teams

En el menú *Aplicaciones*, seleccione *Administrar las aplicacionesPublish* >  an **appSubmit an app to your org (Publicar una aplicaciónEnviar** >  una aplicación a su organización). Esto requiere la aprobación del administrador de TI.

### <a name="teams-developer-portal"></a>Portal para desarrolladores de Teams

Use Teams [Portal para desarrolladores](https://dev.teams.microsoft.com/) para cargar y publicar una aplicación en su organización. Esto requiere la aprobación del administrador de TI. Para obtener más información, consulte [Administración de aplicaciones con el Portal para desarrolladores para Microsoft Teams](../concepts/build-and-test/teams-developer-portal.md).

### <a name="microsoft-teams-admin-center"></a>Centro de administración de Microsoft Teams

Como administrador de Teams, puede cargar e instalar previamente el paquete de la aplicación para el inquilino de la organización desde [Teams centro de administración](https://admin.teams.microsoft.com/). Para obtener más información, consulte [Upload las aplicaciones personalizadas en el Centro de administración de Microsoft Teams](/MicrosoftTeams/upload-custom-apps).

### <a name="microsoft-admin-center"></a>Centro de administración de Microsoft

Como administrador global, puede cargar y preinstalar el paquete de la aplicación desde el [administrador de Microsoft](https://admin.microsoft.com/). Para obtener más información, vea [Probar e implementar Aplicaciones Microsoft 365 por asociados en el portal aplicaciones integradas](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

## <a name="multitenant-distribution"></a>Distribución de varias cuentas empresariales

El proceso de envío de [Microsoft AppSource](https://appsource.microsoft.com/) (Marketplace comercial de Microsoft) para Teams aplicaciones habilitadas para Outlook y Office es el mismo que para las aplicaciones de Teams tradicionales; la única diferencia es que tendrá que usar Teams versión de manifiesto de aplicación [1.13](../tabs/how-to/using-teams-client-sdk.md) en el paquete de la aplicación, lo que introduce compatibilidad con Teams  aplicaciones que se ejecutan en Microsoft 365.

> [!TIP]
> Use Teams Portal para desarrolladores para [validar el paquete de la aplicación](https://dev.teams.microsoft.com/validation) para resolver los errores o advertencias antes de enviarlo a la tienda de Teams (a través de [Microsoft Partner Network](https://partner.microsoft.com/)).

Para empezar, consulte [Distribución de la aplicación Microsoft Teams](../concepts/deploy-and-publish/apps-publish-overview.md).
