---
title: Implementar en la nube
author: MuyangAmigo
description: En este módulo, aprenderá a implementar la aplicación en la nube, Azure o SharePoint e implementar aplicaciones de Teams mediante el kit de herramientas de Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9ad2c9d16901990344ca521599b94b84b0e76217
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616929"
---
# <a name="deploy-teams-app-to-the-cloud"></a>Implementar la aplicación de Teams en la nube

El kit de herramientas de Teams le ayuda a implementar o cargar el código frontend y backend de su aplicación en sus recursos de nube aprovisionados en Azure. Puede implementar lo siguiente en la nube:

* La pestaña, como las aplicaciones de frontend se implementan en el almacenamiento de Azure y se configuran para el alojamiento web estático o un sitio de sharepoint.
* Las API de backend se implementan en Azure Functions.
* El bot o la extensión de mensajes se implementa en el servicio de aplicaciones de Azure.

  > [!NOTE]
  > Antes de implementar el código de la aplicación en la nube de Azure, debe completar correctamente el [aprovisionamiento de recursos en la nube](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Implementar aplicaciones de Teams con el kit de herramientas de Teams

Las guías de introducción le ayudan a implementar mediante el kit de herramientas de Teams. Puede usar lo siguiente para implementar su aplicación de Teams:

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
> Al incluir el recurso de Azure API Management en el proyecto y desencadenar la implementación, puede publicar las API en Azure Functions en el servicio Azure API Management.

## <a name="see-also"></a>Vea también

* [Crear e implementar un servicio en la nube de Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Creación de aplicaciones de Teams de varias funcionalidades](add-capability.md)
* [Adición de recursos en la nube a la aplicación Microsoft Teams](add-resource.md)
