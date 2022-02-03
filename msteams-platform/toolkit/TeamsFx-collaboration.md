---
title: Colaborar en TeamsFx Project usar Teams Toolkit
author: yanjiang
description: Colaborar en TeamsFx Project usar Teams Toolkit
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9a39b84c3cfa94c410df5774d4a177535e1cfdd6
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212352"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>Colaborar en Teams proyecto mediante Teams Toolkit

Varios desarrolladores pueden trabajar juntos para depurar, aprovisionar e implementar para el mismo proyecto de TeamsFx, pero requiere establecer manualmente los permisos adecuados de Teams App y Azure AD App.Teams Toolkit admite la característica de colaboración para permitir que los desarrolladores y el propietario del proyecto inviten a otros desarrolladores o colaboradores al proyecto de TeamsFx para depurar, aprovisionar e implementar la misma característica  Proyecto TeamsFx.

## <a name="prerequisites"></a>Requisitos previos

* Requisitos previos de la cuenta

    Para aprovisionar recursos en la nube, debe tener las siguientes cuentas. Para obtener más información, consulta [preparar cuentas para crear Teams aplicación](accounts.md).

  * Suscripción a Microsoft 365
  * Azure con suscripción válida

* [Instale Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión 3.0.0+.

> [!TIP]
> Asegúrate de que tienes un proyecto Teams aplicación abierta en el código VS.

## <a name="collaborate-with-other-developers"></a>Colaborar con otros desarrolladores

La siguiente lista nos guía para comprender el proceso de colaboración y su limitación:

### <a name="as-project-owner"></a>Como propietario del proyecto

> [!NOTE]
> Antes de agregar colaboradores para un entorno, el propietario del proyecto debe [aprovisionar](provision.md) primero el proyecto.

* En **la sección** ENTORNO de Teams Toolkit, seleccione **colaboradores**. Muestra las opciones Agregar propietarios de la aplicación **M365 Teams (con** la aplicación AAD) y Enumerar los propietarios de la aplicación **M365 Teams (con** AAD App) como se muestra en las siguientes imágenes:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="colaboradores":::

* Selecciona **Agregar M365 Teams app (con AAD app) y** agrega otra dirección de correo electrónico de cuenta M365 como colaborador. La cuenta que se va a agregar debe estar en el mismo inquilino que el propietario del proyecto para la depuración remota, como se muestra en la imagen:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="agregar envi":::

* Para ver colaboradores en el entorno actual, seleccione Enumerar **M365 Teams App (con AAD App) Propietarios**, a continuación, los colaboradores aparecen en el canal de salida como se muestra en la siguiente imagen:

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="list":::

* Presione el proyecto para GitHub.

> [!NOTE]
> El colaborador recién agregado no recibe ninguna notificación. Project propietario debe notificar a los colaboradores.

### <a name="as-project-collaborator"></a>Como colaborador del proyecto

* Clone el proyecto desde GitHub.
* Inicie sesión en la cuenta M365.
* Inicie sesión en la cuenta de Azure, que tiene permiso de colaborador para todos los recursos de Azure que se usan en este proyecto.
* Para obtener una vista previa Teams aplicación, implemente el proyecto en remoto.
* Inicie el control remoto para tener una vista previa de la Teams aplicación.

Para obtener más información, [consulta compilar y ejecutar la aplicación Teams en un entorno remoto.](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch)

> [!NOTE]
> Los colaboradores deben iniciar sesión con la cuenta agregada por el propietario del proyecto, que está bajo el mismo inquilino con el propietario del proyecto.

### <a name="limitation"></a>Limitación

No puede quitar colaboradores directamente de Teams Toolkit extensión. Realice los siguientes pasos para quitar colaboradores manualmente:

  1. Ve a Teams Developer Portal y selecciona tu Teams por nombre o id. de aplicación.
  2. Seleccione **Propietarios** en el panel izquierdo.
  3. Seleccione y quite el colaborador.
  4. Vaya a [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), seleccione **Registro de la** aplicación en el panel izquierdo y busque la aplicación Azure AD aplicación.
  5. Selecciona **Propietarios** en el panel izquierdo en Azure AD de administración de aplicaciones.
  6. Seleccione y quite el colaborador.

> [!NOTE]
> * El colaborador agregado al proyecto no recibirá ninguna notificación. Project propietario debe notificar a los colaboradores sin conexión.
> * El administrador de suscripciones de Azure debe establecer manualmente los permisos relacionados con Azure en Azure Portal. La cuenta de Azure debe tener un rol de colaborador para la suscripción para que los desarrolladores puedan trabajar juntos para aprovisionar e implementar el proyecto de TeamsFx.

## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Implementar la aplicación de Teams en la nube](deploy.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)