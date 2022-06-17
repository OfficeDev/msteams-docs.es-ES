---
title: Compilar aplicaciones con el kit de herramientas de Teams y Visual Studio
description: Aprenda a crear aplicaciones personalizadas directamente en Visual Studio con Teams Toolkit y aprenda a configurar la aplicación en Visual Studio, validarla y mucho más.
ms.localizationpriority: medium
ms.topic: overview
ms.date: 1/13/2022
ms.author: johmil
ms.openlocfilehash: aa7fdaad1d56966031eb13b6b05f145c8e734988
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142048"
---
# <a name="teams-toolkit-for-visual-studio"></a>Kit de herramientas de Teams para Visual Studio

Compile, pruebe y desarrolle para Teams dentro de su IDE.

La extensión del kit de herramientas de Teams para Visual Studio facilita la creación de nuevos proyectos para Teams, la configuración automática de aplicaciones en el portal para desarrolladores de Teams, la ejecución y depuración en Teams, la configuración del alojamiento en la nube y el uso de [TeamsFx](https://github.com/OfficeDev/teamsfx) desde su IDE.

## <a name="install-teams-toolkit-for-visual-studio"></a>Instalar el kit de herramientas de Teams para Visual Studio

>[!NOTE]
> Como requisito previo, asegúrese de utilizar Visual Studio 2022 17.1 Preview 2 o una versión más reciente para seguir las instrucciones a continuación.

1. Si ya tiene instalado Visual Studio 2022 17.1 Preview 2, vaya al paso siguiente. De lo contrario, [instale Visual Studio 2022 Preview](https://visualstudio.microsoft.com/vs/preview/).
2. Abra el Instalador de Visual Studio.
3. Seleccione **Modificar** para la instalación existente de VS 2022 Preview.
4. Seleccione la carga de trabajo de **ASP.NET y desarrollo web**.
5. A la derecha, expanda la sección A **SP.NET y desarrollo web** y seleccione las **herramientas de desarrollo de Microsoft Teams** en la lista opcional de componentes.
6. Seleccione **Instalar** o **Modificar** en el Instalador de Visual Studio para completar el proceso de instalación.

   ![Seleccionando las herramientas de desarrollo de Microsoft Teams en el instalador de Visual Studio.) instalado.](images/teams-development-tools-vs-installer.png)

## <a name="get-started-quickly-with-a-new-project"></a>Inicie rápidamente un nuevo proyecto

Las plantillas de proyectos del kit de herramientas de Teams proporcionan todo el código, los archivos y la configuración que necesita para comenzar con un proyecto de aplicación de Teams.

La plantilla de proyecto de la aplicación de Microsoft Teams le permite especificar una cuenta de Microsoft 365 necesaria para registrar y configurar automáticamente su nueva aplicación de Teams.

> [!NOTE]
> Si no tiene una cuenta de Microsoft 365, puede inscribirse en una suscripción al [Programa para desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program). Es gratuito durante 90 días y se renueva siempre que se utilice para la actividad de desarrollo. Si tiene una suscripción a Visual Studio Enterprise o Professional, ambos programas incluyen una suscripción gratuita a Microsoft 365 [para desarrolladores](https://aka.ms/MyVisualStudioBenefits), activa durante la vida de su suscripción a Visual Studio. Para obtener más información, consulte [configurar una suscripción a Microsoft 365 para desarrolladores](/office/developer-program/office-365-developer-program-get-started).

1. Iniciar Visual Studio 2022
1. En la ventana de inicio, elija **Crear un nuevo proyecto**.
1. En el cuadro de **Búsqueda de plantillas**, escriba aplicación de Microsoft Teams.
1. Seleccione la plantilla de la **aplicación Microsoft Teams** y seleccione **Siguiente**.
1. En la ventana **Configurar su nuevo proyecto**, escriba o introduzca _HelloTeams_ en la casilla **Nombre del proyecto**. Después, seleccione **Crear**.
1. En la ventana **Crear una nueva aplicación de Teams**, elija o inicie sesión en una cuenta de Microsoft 365 mediante el selector **Elegir una cuenta**. Después, seleccione **Crear**.

   ![Creando un nuevo proyecto de la aplicación Microsoft Teams en Visual Studio.](images/teams-toolkit-vs-new-project.png)

Visual Studio abrirá su nuevo proyecto y el kit de herramientas de Teams configurará su nuevo proyecto en el portal para desarrolladores de Teams. El proyecto se agregará para la organización de Teams vinculada a la cuenta de Microsoft 365 que eligió en los pasos anteriores y creará un nuevo registro de Azure Active Directory. Esto es necesario para que la aplicación funcione en Teams.

## <a name="run-and-debug-your-app-in-teams"></a>Ejecute y depure la aplicación en Teams

Puede iniciar su proyecto de aplicación en de forma local desde Visual Studio.

1. Abra o [cree un proyecto de aplicación Teams](#get-started-quickly-with-a-new-project).
2. Presione **F5** o seleccione **Depuración > Iniciar depuración** en Visual Studio.

Visual Studio iniciará su proyecto de aplicación de Teams en un navegador y comenzará a depurar.

## <a name="host-your-teams-app-in-the-cloud-and-preview-it"></a>Hospede su aplicación de Teams en la nube y obtenga una vista previa

Puede crear y configurar automáticamente los recursos de la nube para hospedar su aplicación en Azure usando el kit de herramientas de Teams.

1. Seleccione el menú **Proyecto > Kit de herramientas de Teams> Aprovisionamiento en la nube**.
2. En la ventana Seleccione su suscripción, elija la suscripción de Azure que desea utilizar para crear recursos.

El kit de herramientas de Teams creará recursos de Azure en esta suscripción, pero no se implementa ningún código durante este paso. Para implementar su proyecto en estos nuevos recursos:

1. Seleccione el menú **Proyecto > Kit de herramientas de Teams > Implementar en la nube**.

## <a name="preview-your-app-running-from-cloud-resources"></a>Obtenga una vista previa de su aplicación ejecutada desde los recursos de la nube

Puede iniciar su aplicación en un navegador usando los recursos remotos para verificar que todo funciona. Todavía no es posible depurar durante en este escenario.

1. Seleccione el menú **Proyecto > Kit de herramientas de Teams > Vista previa de la aplicación de Teams**.

Su aplicación se abrirá en un navegador y utilizará los recursos creados por los pasos de aprovisionamiento e implementación.

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

En el [portal para desarrolladores de Teams](https://dev.teams.microsoft.com/home), puede cargar su aplicación en un equipo, enviarla a la tienda de aplicaciones personalizada de su empresa para los usuarios de su organización, o enviarla a App Source para todos los usuarios de Teams.

- El administrador de TI revisará estas entregas.
- Puede volver a la página de **Publicar** para comprobar el estado de su envío y saber si su aplicación ha sido aprobada o rechazada por su administrador de TI. Aquí también puede enviar actualizaciones de su aplicación o cancelar cualquier envío activo.
