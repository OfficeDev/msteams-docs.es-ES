---
title: Implementar en la nube
author: MuyangAmigo
description: Implementar la aplicación en la nube, Azure o SharePoint
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 35a60e718bb97cdcc24de66729e3929b2d21a59f
ms.sourcegitcommit: 2236204ff710f4eca606ceffb233572981f6edbe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/01/2022
ms.locfileid: "64614533"
---
# <a name="deploy-to-the-cloud"></a>Implementar en la nube

Teams Toolkit ayuda a implementar o cargar el código front-end y back-end de la aplicación en los recursos de nube aprovisionados en Azure.

* La pestaña, como las aplicaciones front-end, se implementan en Azure Storage y se configuran para el hospedaje web estático o un sitio de SharePoint.
* Las API back-end se implementan en funciones de Azure.
* El bot o la extensión de mensajería se implementa en el servicio de aplicaciones de Azure.

## <a name="prerequisite"></a>Requisito previo

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!NOTE]
>
> * Asegúrate de que tienes Teams proyecto de aplicación abierto en el código VS.
> * Antes de implementar código de proyecto en la nube, [aprovisione los recursos en la nube](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Implementar Teams aplicaciones con Teams Toolkit

Las guías de introducción le ayudan a implementar con Teams Toolkit. Puedes usar lo siguiente para implementar la Teams aplicación:

* [Implementar la aplicación en Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Implementar la aplicación en SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Detalles sobre la carga Teams de aplicaciones

| Teams de aplicaciones | Código fuente | Artefacto de compilación| Recurso de destino |
|-------------|----------|---------------|---------------|
|Pestañas con React </br> La carga de trabajo de front-end| `yourProjectFolder/tabs`| `tabs/build` |Almacenamiento de Azure |
|Pestañas con SharePoint </br> La carga de trabajo de front-end | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint catálogo de aplicaciones |
|API en funciones de Azure </br> La carga de trabajo back-end | `yourProjectFolder/api`| No aplicable |Funciones de Azure |
|Bots y extensiones de mensajería </br> La carga de trabajo back-end | `yourProjectFolder/bot` | No aplicable | Servicio de aplicaciones de Azure |

> [!NOTE]
> Al incluir el recurso de administración de API de Azure en el proyecto y desencadenar la implementación. Puede publicar sus API en funciones de Azure en el servicio de administración de API de Azure.

## <a name="see-also"></a>Vea también

* [Agregar más recursos en la nube](add-resource.md)
* [Crear e implementar un servicio en la nube de Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Agregar más Teams funcionalidades de la aplicación](add-capability.md)
* [Implementar código de proyecto con canalizaciones de CI/CD](use-CICD-template.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)
* [Colaborar con otros desarrolladores en proyectos de Teams](TeamsFx-collaboration.md)
