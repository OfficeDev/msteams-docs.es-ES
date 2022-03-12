---
title: Crear aplicaciones con el Teams Toolkit y Visual Studio
description: Empieza a crear aplicaciones personalizadas excelentes directamente Visual Studio con el Microsoft Teams Toolkit. Aprende a configurar la aplicación en Visual Studio, validar la aplicación y publicarla desde Visual Studio y portal de desarrolladores.
keywords: Kit de herramientas de visual studio de teams
ms.localizationpriority: medium
ms.topic: overview
ms.date: 1/13/2022
ms.author: johmil
ms.openlocfilehash: c34f1113cd4da5f1b416dba6bc950b3588accecf
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453435"
---
# <a name="teams-toolkit-for-visual-studio"></a>Kit de herramientas de Teams para Visual Studio

Cree, pruebe y desarrolle para Teams dentro de su IDE.

La extensión de Teams Toolkit para Visual Studio facilita la creación de nuevos proyectos para Teams, la configuración automática de aplicaciones en el Portal de desarrolladores de Teams, la ejecución y depuración en Teams, la configuración del hospedaje en la nube y el uso de [TeamsFx](https://github.com/OfficeDev/teamsfx) desde el IDE.

## <a name="install-teams-toolkit-for-visual-studio"></a>Instalar Teams Toolkit para Visual Studio

>[!NOTE]
> Como requisito previo, asegúrese de usar Visual Studio 2022 17.1 Versión preliminar 2 o posterior para seguir las instrucciones siguientes.

1. Si ya tiene Visual Studio 2022 17.1 Preview 2 instalado, vaya al paso siguiente. De lo [contrario, Visual Studio versión preliminar de 2022](https://visualstudio.microsoft.com/vs/preview/).
2. Abra el Instalador de Visual Studio.
3. Seleccione **Modificar para** la instalación existente de VS 2022 Preview.
4. Seleccione la carga **ASP.NET de trabajo de desarrollo web y** de desarrollo web.
5. A la derecha, expanda la **sección ASP.NET desarrollo web** y seleccione Microsoft Teams **de** desarrollo en la lista Opcional de componentes.
6. Seleccione **Instalar** o **Modificar** en el Instalador de Visual Studio para completar el proceso de instalación.

![Selección de las Microsoft Teams de desarrollo en el Visual Studio instalación).](images/teams-development-tools-vs-installer.png)

## <a name="get-started-quickly-with-a-new-project"></a>Introducción rápida a un nuevo proyecto

Teams Toolkit plantillas de proyecto proporcionan todo el código, los archivos y la configuración que necesita para empezar con un proyecto de Teams aplicación.

La Microsoft Teams de proyecto de aplicación te permite especificar una cuenta de Microsoft 365 que sea necesaria para registrar y configurar automáticamente la nueva aplicación Teams aplicación.

> [!NOTE]
> Si no tiene una cuenta Microsoft 365, puede registrarse para una [suscripción Microsoft 365 Programa para desarrolladores](https://developer.microsoft.com/microsoft-365/dev-program). Es gratuito durante 90 días y se renueva siempre que lo use para la actividad de desarrollo. Si tiene una suscripción Visual Studio Enterprise o Professional, ambos programas incluyen una suscripción Microsoft 365 desarrollador [gratuita, activa](https://aka.ms/MyVisualStudioBenefits) durante la vida de su Visual Studio suscripción. Para obtener más información, consulta [Configurar una suscripción Microsoft 365 desarrollador.](/office/developer-program/office-365-developer-program-get-started)

1. Inicie Visual Studio 2022.
1. En la ventana inicio, elija **Crear un nuevo proyecto**.
1. En el **cuadro Buscar plantillas**, escriba Microsoft Teams app.
1. Seleccione la **Microsoft Teams aplicación** y seleccione **Siguiente**.
1. En la **ventana Configurar el nuevo proyecto**, escriba o escriba _HelloTeams_ en el **cuadro Project nombre**. A continuación, **seleccione Crear**.
1. En la **ventana Crear una nueva Teams** aplicación, elija o inicie sesión en una cuenta de Microsoft 365 con el selector **Elegir una** cuenta. A continuación, **seleccione Crear**.

![Crear un nuevo proyecto Microsoft Teams app en Visual Studio.](images/teams-toolkit-vs-new-project.png)

Visual Studio abrirá el nuevo proyecto y Teams Toolkit configurará el nuevo proyecto en Teams Developer Portal. El proyecto se agregará para la organización Teams vinculada a la cuenta de Microsoft 365 que eligió en los pasos anteriores y creará un nuevo registro Azure Active Directory usuario. Esto es necesario para que la aplicación se ejecute en Teams.

## <a name="run-and-debug-your-app-in-teams"></a>Ejecutar y depurar la aplicación en Teams

Puedes iniciar el proyecto de aplicación ejecutándose localmente desde Visual Studio.

1. Abra o [cree un proyecto Teams aplicación.](#get-started-quickly-with-a-new-project)
2. Presione **F5** o seleccione **Depurar > Iniciar depuración** en Visual Studio.

Visual Studio iniciará el proyecto Teams aplicación en un explorador e iniciará la depuración.

## <a name="host-your-teams-app-in-the-cloud-and-preview-it"></a>Hospedar la Teams en la nube y obtener una vista previa de ella

Puede crear y configurar automáticamente recursos en la nube para hospedar la aplicación en Azure mediante Teams Toolkit.

1. Seleccione el **Project > Teams Toolkit > Aprovisionar en el menú Nube**.
2. En la ventana Seleccionar su suscripción, elija la suscripción de Azure con la que desea crear recursos.

Teams Toolkit creará recursos de Azure en esta suscripción, pero no se implementa ningún código durante este paso. Para implementar el proyecto en estos nuevos recursos:

1. Seleccione el **Project > Teams Toolkit > implementar en el menú Nube**.

## <a name="preview-your-app-running-from-cloud-resources"></a>Vista previa de la aplicación que se ejecuta desde recursos en la nube

Puedes ejecutar la aplicación en un explorador con los recursos remotos para comprobar que todo funciona. Todavía no es posible depurar durante este escenario.

1. Selecciona el **Project > Teams Toolkit > vista Teams menú de la** aplicación.

La aplicación se abrirá en un explorador y usará los recursos creados mediante los pasos Aprovisionar e implementar.

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

En [el Portal](https://dev.teams.microsoft.com/home) de desarrolladores de Teams, puedes cargar la aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizada de tu empresa para los usuarios de tu organización o enviar la aplicación a App Source para todos los usuarios Teams usuario.

- El administrador de TI revisará estas entregas.
- Puedes volver a la **página Publicar** para comprobar el estado del envío y saber si tu administrador de TI aprobó o rechazó la aplicación. Aquí también puedes enviar actualizaciones a la aplicación o cancelar cualquier envío activo actualmente.
