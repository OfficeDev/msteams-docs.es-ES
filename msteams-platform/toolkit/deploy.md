---
title: Implementar en la nube
author: MuyangAmigo
description: Implementar en la nube
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 3f7dc4b320bccfa8a6017f87045b27a37d8199f7
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227793"
---
# <a name="deploy-to-the-cloud"></a>Implementar en la nube

Teams Toolkit ayuda a implementar o cargar el código front-end y back-end de la aplicación en los recursos de nube aprovisionados en Azure.

* La pestaña, como las aplicaciones front-end, se implementan en Azure Storage y se configuran para el hospedaje web estático o un SharePoint web.
* Las API back-end se implementan en Azure Functions.
* Bot o extensión de mensajería se implementa en Azure App Service.

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Ya debería tener abierto un proyecto Teams aplicación en el código VS.

> [!NOTE]
> Antes de implementar código de proyecto en la nube, realice primero los pasos [de aprovisionar recursos en](provision.md) la nube.


## <a name="deploy-teams-apps-using-teams-toolkit"></a>Implementar Teams aplicaciones con Teams Toolkit

En los tutoriales de introducción, hay guías paso a paso sobre cómo implementar con Teams Toolkit. Puedes usar lo siguiente para implementar la Teams aplicación:

* [Implementar la aplicación en Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Implementar la aplicación en SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workloads"></a>Detalles sobre las Teams de aplicaciones

| Teams de aplicaciones| Código fuente | Crear Artifacts| Recursos de destino |
|-------------|----------|---------------|---------------|
|Pestañas con React </br> La carga de trabajo de front-end| `yourProjectFolder/tabs`| `tabs/build` |Azure Storage |
|Pestañas con SharePoint </br> La carga de trabajo de front-end | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint de aplicaciones |
|API en Azure Functions </br> La carga de trabajo back-end | `yourProjectFolder/api`| N/D |Azure Functions |
|Bots y extensiones de mensajería </br> La carga de trabajo back-end | `yourProjectFolder/bot` | N/D | Azure App Service |

> [!NOTE]
> Al incluir el recurso de administración de API de Azure en el proyecto y desencadenar la implementación. Puede publicar sus API en Azure Functions en el Servicio de administración de API de Azure.

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Agregar más recursos en la nube](add-resource.md)

> [!div class="nextstepaction"]
> [Agregar más Teams funcionalidades de la aplicación](add-capability.md)

> [!div class="nextstepaction"]
> [Implementar código de proyecto con canalizaciones de CI/CD](use-CICD-template.md)

> [!div class="nextstepaction"]
> [Administrar varios entornos](TeamsFx-multi-env.md)

> [!div class="nextstepaction"]
> [Colaborar con otros desarrolladores en Teams proyecto](TeamsFx-collaboration.md)
