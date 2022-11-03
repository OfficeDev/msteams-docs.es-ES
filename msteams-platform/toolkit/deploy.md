---
title: Implementar en la nube
author: MuyangAmigo
description: En este módulo, aprenderá a implementar la aplicación en la nube, Azure o SharePoint e implementar aplicaciones de Teams mediante el kit de herramientas de Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 17d4d1d80f9ffd634e2fdae815b8504bb6c0ca99
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833138"
---
# <a name="deploy-teams-app-to-the-cloud"></a>Implementar la aplicación de Teams en la nube

Teams Toolkit le ayuda a implementar o cargar el código front-end y back-end de la aplicación en los recursos de nube aprovisionados en Azure.

::: zone pivot="visual-studio-code"

## <a name="deploy-teams-app-to-the-cloud-using-visual-studio-code"></a>Implementación de una aplicación de Teams en la nube mediante Visual Studio Code

Puede implementar lo siguiente en la nube:

* La pestaña, como las aplicaciones front-end, se implementa en Azure Storage y se configura para el hospedaje web estático o un sitio de SharePoint.
* Las API de back-end se implementan en Azure Functions.
* La extensión de bot o mensaje se implementa en Azure App Service.

  > [!NOTE]
  > Antes de implementar el código de la aplicación en la nube de Azure, debe completar correctamente el [aprovisionamiento de recursos en la nube](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Implementar aplicaciones de Teams con el kit de herramientas de Teams

Las guías de introducción le ayudan a implementar mediante el kit de herramientas de Teams. Puede usar lo siguiente para implementar su aplicación de Teams:

* [Implementar la aplicación en Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Implementar la aplicación en SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Detalles sobre la carga de trabajo de la aplicación de Teams

| Carga de trabajo de la aplicación de Teams | Código fuente | Artefacto de compilación| Recurso de destino |
|-------------|----------|---------------|---------------|
|Pestañas con React </br> Carga de trabajo de front-end| `yourProjectFolder/tabs`| `tabs/build` |Azure Storage |
|Pestañas con SharePoint </br> Carga de trabajo de front-end | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |Catálogo de aplicaciones de SharePoint |
|API en Azure Functions </br> Carga de trabajo de back-end | `yourProjectFolder/api`| No aplicable |Azure Functions |
|Bots y extensiones de mensaje </br> Carga de trabajo de back-end | `yourProjectFolder/bot` | No aplicable | Azure App Service |

> [!NOTE]
> Al incluir el recurso de Azure API Management en el proyecto y desencadenar la implementación, puede publicar las API en Azure Functions en el servicio Azure API Management.

::: zone-end

::: zone pivot="visual-studio"

## <a name="deploy-teams-app-to-the-cloud-using-visual-studio"></a>Implementación de una aplicación de Teams en la nube mediante Visual Studio

Las siguientes aplicaciones se pueden implementar en Visual Studio:

* La aplicación de pestaña, como las aplicaciones de front-end, se implementa en Azure Storage, configurada para el hospedaje web estático.
* La aplicación del bot de notificación con desencadenadores de Azure Functions se puede implementar en Azure Functions.
* La aplicación de bot o la extensión de mensaje se pueden implementar en App de Azure Services.

Después de la implementación, puede obtener una vista previa de la aplicación en el cliente de Teams o en el explorador web antes de empezar a usar.

## <a name="deploy-teams-app-using-teams-toolkit"></a>Implementación de una aplicación de Teams mediante el kit de herramientas de Teams

1. Abra Visual Studio.
1. Seleccione **Crear un nuevo proyecto** o abra un proyecto existente en la lista.
1. Haga clic con el botón derecho en el proyecto **MyTeamsApp1** > **Teams Toolkit** > **Deploy to the cloud (Implementar en la nube**).

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-cloud.png" alt-text="implementar en la nube":::

   > [!NOTE]
   > En este escenario, el nombre del proyecto es MyTeamsApp1.

1. Seleccione **Implementar** en el cuadro de diálogo de confirmación.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-confirmation.png" alt-text="Cuadro de diálogo de confirmación de implementación en la nube":::

   Una vez completado el proceso de implementación, puede ver un elemento emergente con la confirmación de que se ha implementado correctamente. También puede comprobar el estado en la ventana de salida.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/VS-deploy-popup.png" alt-text="elemento emergente deploy to cloud (implementar en la nube)":::

### <a name="preview-your-app"></a>Vista previa de la aplicación

Para obtener una vista previa de la aplicación, primero debe crear un paquete de aplicación Zip y transferir localmente en el cliente de Teams.

1. Seleccione Paquete **de aplicación zip** **del kit de herramientas de** >  **Project** >  Teams.
1. Seleccione **la opción Para local** o **Para Azure** para generar el paquete de aplicaciones de Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-ZipApp-package1.png" alt-text="Generación de un paquete de aplicación de Teams":::

**Para obtener una vista previa de la aplicación en el cliente de Teams**

1. Seleccione Project Teams Toolkit **Preview (Versión preliminar** **del kit de herramientas de** >  **Project** >  Teams) en Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams2.png" alt-text="Vista previa de la aplicación teams en el cliente de Teams":::

   Ahora la aplicación se carga de forma local en Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/sideload-teams.png" alt-text="Transferir localmente la aplicación de Teams en el cliente de Teams":::

La otra manera de obtener una vista previa de la aplicación:

1. Haga clic con el botón derecho en el proyecto **MyTeamsApp1** en **Explorador de soluciones**.
1. Seleccione **Versión preliminar del kit de herramientas de** >  Teams **en Teams** para iniciar la aplicación teams en el explorador web.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams.png" alt-text="Vista previa de la aplicación teams en el explorador web":::

   > [!NOTE]
   > Las mismas opciones de menú están disponibles en el menú Proyecto.

   Ahora la aplicación se carga de forma local en Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/sideload-teams.png" alt-text="Transferir localmente la aplicación de Teams en el cliente de Teams":::

::: zone-end

## <a name="see-also"></a>Vea también

* [Crear e implementar un servicio en la nube de Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Creación de aplicaciones de Teams de varias funcionalidades](add-capability.md)
* [Adición de recursos en la nube a la aplicación Microsoft Teams](add-resource.md)
* [Creación de una nueva aplicación de Teams en Visual Studio](create-new-project.md#create-new-teams-app-in-visual-studio)
* [Aprovisionamiento de recursos en la nube mediante Visual Studio](provision-cloud-resources.md)
* [Edición del manifiesto de aplicación de Teams mediante Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Depuración local de la aplicación de Teams mediante Visual Studio](debug-local.md#debug-your-teams-app-locally-using-visual-studio)
