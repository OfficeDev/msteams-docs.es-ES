---
title: Implementar en la nube
author: MuyangAmigo
description: Implementar la aplicación en la nube, Azure o SharePoint
ms.author: zhany
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 3e9368dcaa87003da2872a500ffaa281092774df
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111573"
---
# <a name="deploy-to-the-cloud"></a>Implementar en la nube

El kit de herramientas de Teams le ayuda a implementar o cargar el código frontend y backend de su aplicación en sus recursos de nube aprovisionados en Azure.

* La pestaña, como las aplicaciones de frontend se implementan en el almacenamiento de Azure y se configuran para el alojamiento web estático o un sitio de sharepoint.
* Las API de backend se implementan en Azure Functions.
* El bot o la extensión de mensajes se implementa en el servicio de aplicaciones de Azure.

## <a name="prerequisite"></a>Requisito previo

* [Instale el Kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión v3.0.0+.

> [!NOTE]
>
> * Asegúrese de que ha abierto un proyecto de aplicación de Teams en VS Code.
> * Antes de implementar el código del proyecto en la nube, [aprovisione los recursos en la nube](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Implementar aplicaciones de Teams con el kit de herramientas de Teams

Las guías de introducción le ayudarán a implementar con el kit de herramientas de Teams. Puede usar lo siguiente para implementar su aplicación de Teams:

* [Implementar la aplicación en Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Implementar la aplicación en SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Detalles sobre la carga de trabajo de la aplicación de Teams

| Carga de trabajo de la aplicación de Teams | Código fuente | Artefacto de compilación| Recurso de destino |
|-------------|----------|---------------|---------------|
|Pestañas con React </br> Carga de trabajo de front-end| `yourProjectFolder/tabs`| `tabs/build` |Almacenamiento de Azure |
|Pestañas con SharePoint </br> Carga de trabajo de front-end | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |Catálogo de aplicaciones de SharePoint |
|API en Azure Functions </br> Carga de trabajo de back-end | `yourProjectFolder/api`| No aplicable |Azure Functions |
|Bots y extensiones de mensaje </br> Carga de trabajo de back-end | `yourProjectFolder/bot` | No aplicable | Servicio de aplicaciones de Azure |

> [!NOTE]
> Cuando se incluye el recurso de administración de API en el proyecto y se desencadena la implementación. Puede publicar las API en Azure Functions en el servicio de administración de API.

## <a name="see-also"></a>Vea también

* [Agregar más recursos en la nube](add-resource.md)
* [Crear e implementar un servicio en la nube de Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Agregar más funcionalidades de la aplicación de Teams](add-capability.md)
* [Implementar código de proyecto con canalizaciones CI/CD](use-CICD-template.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)
* [Colaborar con otros desarrolladores en proyectos de Teams](TeamsFx-collaboration.md)
