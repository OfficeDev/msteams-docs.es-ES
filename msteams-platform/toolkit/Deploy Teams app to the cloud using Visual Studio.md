---
title: Implementación de una aplicación de Teams en la nube mediante Visual Studio
author: surbhigupta
description: En este módulo, aprenderá a implementar la aplicación en la nube, Azure o SharePoint e implementar aplicaciones de Teams mediante el kit de herramientas de Teams en Visual Studio.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 4cf2267f4392289f14c3ec3438abd66cf9fb1769
ms.sourcegitcommit: 60484634f38642048e9a9a1465ac0c3322c8229a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2022
ms.locfileid: "67290123"
---
# <a name="deploy-teams-app-to-the-cloud-using-visual-studio"></a>Implementación de una aplicación de Teams en la nube mediante Visual Studio

Teams Toolkit le ayuda a implementar o cargar el código front-end y back-end de la aplicación en los recursos de nube aprovisionados de la suscripción de Azure. Después de la implementación, puede obtener una vista previa de la aplicación en el cliente de Teams o en el explorador web antes de empezar a usar. Las siguientes aplicaciones se pueden implementar en Visual Studio:

* La aplicación de pestaña, como las aplicaciones de front-end, se implementa en Azure Storage, configurada para el hospedaje web estático.
* La aplicación de bot de notificación con desencadenadores de función de Azure se puede implementar en Azure Functions.
* La aplicación de bot o la extensión de mensaje se pueden implementar en Azure App Services.

## <a name="prerequisite"></a>Requisito previo

Esta es una lista de las herramientas que necesita para compilar e implementar las aplicaciones.

| &nbsp; | Instalar | Para usar... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 2022, versión 17.3 | Puede instalar la edición enterprise de Visual Studio e instalar la carga de trabajo "ASP.NET" y las herramientas de desarrollo de Microsoft Teams. |
| &nbsp; | Kit de herramientas de Teams | Extensión de Visual Studio que crea un scaffolding de proyecto para la aplicación. Use la versión más reciente. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams para colaborar con todos los usuarios con los que trabaja a través de aplicaciones de chat, reuniones, llamadas, todo en un solo lugar. |
| &nbsp; | Herramientas de Azure y [cli de Microsoft Azure](/cli/azure/install-azure-cli) | Herramientas de Azure para acceder a datos almacenados o para implementar un back-end basado en la nube para la aplicación de Teams en Azure. |

  > [!NOTE]
  > Antes de implementar el código del proyecto en la nube, [aprovisione recursos en la nube para TTK Visual Studio](provision VS.md).

## <a name="deploy-teams-app-using-teams-toolkit"></a>Implementación de una aplicación de Teams mediante el kit de herramientas de Teams

1. Inicie Visual Studio.
1. Seleccione **Crear un nuevo proyecto** o abra un proyecto existente en la lista.
1. Haga clic con el botón derecho en el proyecto **MyTeamsApp1**.
1. Seleccione **Kit de herramientas de Teams**.
1. Seleccione **Implementar en la nube...**

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-cloud.png" alt-text="implementar en la nube":::

   > [!NOTE]
   > En este escenario, el nombre del proyecto es MyTeamsApp1.

6. Seleccione **Implementar** en el cuadro de diálogo de confirmación.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-confirmation.png" alt-text="Cuadro de diálogo de confirmación de implementación en la nube":::

7. Una vez desencadenado y completado el proceso de implementación, puede ver un elemento emergente con la confirmación de que se ha implementado correctamente. También puede comprobar el estado en la ventana de salida.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/VS-deploy-popup.png" alt-text="elemento emergente deploy to cloud (implementar en la nube)":::

Una vez que el proyecto se implemente correctamente en Azure, hay diferentes maneras de obtener una vista previa de la aplicación en teams toolkit:

1. Seleccione **Paquete de aplicación zip** **del kit** >  de herramientas de **Project** >  Teams para generar el paquete de aplicaciones de Teams.
1. Seleccione **la opción Para local** o **Para Azure** y cargue en el cliente de Teams.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-ZipApp-package.png" alt-text="Generación de un paquete de aplicación de Teams":::

**Para obtener una vista previa de la aplicación en el cliente de Teams**

1. Seleccionar **proyecto**
1. Seleccione **Kit de herramientas de Teams**.
1. Seleccione **Vista previa en Teams**.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams1.png" alt-text="Vista previa de la aplicación teams en el cliente de Teams":::

La otra manera de obtener una vista previa de la aplicación:

1. Haga clic con el botón derecho en el proyecto **MyTeamsApp1** en el panel Explorador de soluciones.
1. Seleccione **Kit de herramientas de Teams**.
1. Seleccione **Vista previa en Teams** para iniciar la aplicación teams en el explorador web.

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams.png" alt-text="Vista previa de la aplicación teams en el explorador web":::

   > [!NOTE]
   > Las mismas opciones de menú están disponibles en el menú Proyecto.

## <a name="see-also"></a>Vea también

* [Creación de una nueva aplicación de Teams en Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Aprovisionamiento de recursos en la nube mediante Visual Studio](Provision%20cloud%20resources%20using%20Visual%20Studio.md)
* [Edición del manifiesto de aplicación de Teams mediante Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Depuración local de la aplicación de Teams mediante Visual Studio](debug-teams-app-visual-studio.md)
