---
title: Publicar aplicaciones de Teams para Microsoft 365
description: En este artículo, sabe cómo hacer que las aplicaciones de Teams habilitadas para Microsoft 365 sean reconocibles para los usuarios de Teams, Outlook y Office.
ms.date: 05/24/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: c99114ed397b9c20f699ffee165189ec7c4fd26d
ms.sourcegitcommit: 4ba6392eced76ba6baeb6d6dd9ba426ebf4ab24f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2022
ms.locfileid: "66919819"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>Publicar aplicaciones de Teams para Microsoft 365

Las aplicaciones de Teams habilitadas para Microsoft 365 se admiten para su uso en producción en Microsoft Teams. Puede distribuir estas aplicaciones a audiencias en versión preliminar que *usen las versiones* de versión dirigida de outlook.com y office.com, y la compilación *del canal beta* de Outlook para el escritorio de Windows. Las opciones de distribución y los procesos de las aplicaciones de Teams habilitadas para Microsoft 365 son las mismas que para las aplicaciones tradicionales de Teams.

Una vez publicada, la aplicación se podrá detectar como una aplicación instalable desde las tiendas de aplicaciones de Outlook y Office, además de la tienda de Teams. La aplicación usa los permisos definidos en Teams en Outlook y Office. Los administradores de Teams pueden [administrar el acceso a las aplicaciones de Teams en Microsoft 365](/MicrosoftTeams/manage-third-party-teams-apps) para los usuarios de su organización.

:::image type="content" source="images/outlook-office-app-store.png" alt-text="La captura de pantalla es un ejemplo que muestra Las pantallas de instalación de Outlook y Office.com para las aplicaciones SurveyMonkey y MURAL Teams.":::

## <a name="single-tenant-distribution"></a>Distribución de cuenta empresarial única

Las extensiones de mensajes habilitadas para Outlook se pueden distribuir para los inquilinos de prueba y producción de varias maneras:

### <a name="teams-client"></a>Cliente de Teams

En el menú **Aplicaciones** , seleccione **Administrar las aplicaciones** > **Publicar una aplicación** > **Enviar una aplicación a su organización**. Esto requiere la aprobación del administrador de TI.

### <a name="teams-developer-portal"></a>Portal para desarrolladores de Teams

Use el [Portal para desarrolladores de Teams](https://dev.teams.microsoft.com/) para cargar y publicar una aplicación en su organización. Esto requiere la aprobación del administrador de TI. Para obtener más información, consulte [Administración de aplicaciones con el Portal para desarrolladores para Microsoft Teams](../concepts/build-and-test/teams-developer-portal.md).

### <a name="microsoft-teams-admin-center"></a>Centro de administración de Microsoft Teams

Como administrador de Teams, puede cargar y preinstalar el paquete de la aplicación para el inquilino de su organización desde el [Centro de administración de Teams](https://admin.teams.microsoft.com/). Para obtener más información, consulte [Carga de aplicaciones personalizadas en el Centro de administración de Microsoft Teams](/MicrosoftTeams/upload-custom-apps).

### <a name="microsoft-admin-center"></a>Centro de administración de Microsoft

Como administrador global, puede cargar y preinstalar el paquete de la aplicación desde el [administrador de Microsoft](https://admin.microsoft.com/). Para obtener más información, vea [Probar e implementar Aplicaciones Microsoft 365 por asociados en el portal aplicaciones integradas](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

## <a name="multitenant-distribution"></a>Distribución de varias cuentas empresariales

El proceso de envío [de Microsoft AppSource](https://appsource.microsoft.com/) (Marketplace comercial de Microsoft) para las aplicaciones de Teams habilitadas para Outlook y Office es el mismo que las aplicaciones tradicionales de Teams. La única diferencia es que tendrá que usar la [versión 1.13](../tabs/how-to/using-teams-client-sdk.md) del manifiesto de aplicación de Teams en el paquete de la aplicación, lo que introduce compatibilidad con las aplicaciones de Teams que se ejecutan en Microsoft 365.

> [!TIP]
> Use el Portal para desarrolladores de Teams para [validar el paquete de la aplicación](https://dev.teams.microsoft.com/validation) para resolver los errores o advertencias antes de enviarlo al almacén de Teams (a través de [Microsoft Partner Network](https://partner.microsoft.com/)).

Para empezar, consulte [Distribución de la aplicación de Microsoft Teams](../concepts/deploy-and-publish/apps-publish-overview.md).
