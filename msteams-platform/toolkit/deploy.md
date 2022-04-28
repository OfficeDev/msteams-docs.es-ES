---
title: Implementar en la nube
author: MuyangAmigo
description: Implementación de una aplicación en la nube, Azure o SharePoint
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 1d0ade9abed4be212abfb96068626172c4f0f03e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104150"
---
# <a name="deploy-to-the-cloud"></a>Implementar en la nube

Teams Toolkit le ayuda a implementar o cargar el código front-end y back-end de la aplicación en los recursos de nube aprovisionados en Azure.

* La pestaña, como las aplicaciones de front-end, se implementa en Azure Storage y se configura para el hospedaje web estático o un sitio de SharePoint.
* Las API de back-end se implementan en las funciones de Azure.
* La extensión de bot o mensaje se implementa en Azure App Service.

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión v3.0.0+.

> [!NOTE]
>
> * Asegúrese de que ha abierto Teams proyecto de aplicación en vs code.
> * Antes de implementar el código del proyecto en la nube, [aprovisione los recursos en la nube](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Implementación de aplicaciones Teams mediante Teams Toolkit

Las guías de introducción le ayudan a implementar mediante Teams Toolkit. Puede usar lo siguiente para implementar la aplicación de Teams:

* [Implementación de la aplicación en Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Implementación de la aplicación en SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Detalles sobre Teams carga de trabajo de la aplicación

| Teams carga de trabajo de la aplicación | Código fuente | Artefacto de compilación| Recurso de destino |
|-------------|----------|---------------|---------------|
|Pestañas con React </br> Carga de trabajo de front-end| `yourProjectFolder/tabs`| `tabs/build` |Azure Storage |
|Pestañas con SharePoint </br> Carga de trabajo de front-end | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |catálogo de aplicaciones de SharePoint |
|API en Azure Functions </br> La carga de trabajo de back-end | `yourProjectFolder/api`| No aplicable |Funciones de Azure |
|Bots y extensiones de mensajes </br> La carga de trabajo de back-end | `yourProjectFolder/bot` | No aplicable | Azure App Service |

> [!NOTE]
> Cuando se incluye el recurso de Azure API Management en el proyecto y se desencadena la implementación. Puede publicar las API en Azure Functions en el servicio Azure API Management.

## <a name="see-also"></a>Vea también

* [Incorporación de más recursos en la nube](add-resource.md)
* [Creación e implementación de un servicio en la nube de Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Agregar más funcionalidades de aplicación Teams](add-capability.md)
* [Implementación de código de proyecto con canalizaciones de CI/CD](use-CICD-template.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)
* [Colaborar con otros desarrolladores en proyectos de Teams](TeamsFx-collaboration.md)
