---
title: Colaborar en el proyecto TeamsFx mediante el kit de herramientas de Teams
author: surbhigupta
description: En este artículo, aprenderá a colaborar en TeamsFx Project mediante Teams Toolkit y a colaborar con otros desarrolladores.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 90ccd073e45649f715751e81835747bfb95d7806
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616851"
---
# <a name="collaborate-on-teams-project-using-microsoft-teams-toolkit"></a>Colaborar en el proyecto de Teams mediante el kit de herramientas de Microsoft Teams

Varios desarrolladores pueden trabajar juntos para depurar, aprovisionar e implementar para el mismo proyecto TeamsFx, pero requiere establecer manualmente los permisos adecuados de la aplicación teams y Microsoft Azure Active Directory (Azure AD). Teams Toolkit admite la característica de colaboración para permitir que los desarrolladores y el propietario del proyecto inviten a otros desarrolladores o colaboradores al proyecto TeamsFx para depurar, aprovisionar e implementar el mismo proyecto teamsfx.

## <a name="collaborate-with-other-developers"></a>Colaborar con otros desarrolladores

Las secciones siguientes nos guían para comprender el proceso de colaboración como propietario o colaborador del proyecto:

### <a name="as-project-owner"></a>Como propietario del proyecto

  > [!NOTE]
  > Antes de agregar colaboradores para un entorno, el propietario del proyecto debe [aprovisionar](provision.md) primero el proyecto.

  1. Seleccione **Kit de herramientas de Teams** en la barra de actividad.
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-teams-toolkit.png" alt-text="Selección del kit de herramientas de teams en la barra de actividad":::

  1. En la sección **ENTORNO** , seleccione colaboradores, que se muestra como opción **1** **Agregar propietarios de aplicaciones de Microsoft 365 Teams (con aplicación de Azure AD)** y **2** **Enumerar propietarios de aplicaciones de Microsoft 365 Teams (con aplicación de Azure AD),** como se muestra en la siguiente imagen:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="Colaboradores":::

  2. Seleccione **Agregar propietarios de aplicaciones de Microsoft 365 Teams (con aplicación de Azure AD)** y agregue otra dirección de correo electrónico de cuenta de Microsoft 365 como colaborador. La cuenta que se va a agregar debe estar en el mismo inquilino que el propietario del proyecto para la depuración remota como se muestra en la imagen:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add-owner.png" alt-text="Agregar propietario del proyecto":::

  3. Para ver los colaboradores en el entorno actual, seleccione **Enumerar propietarios de aplicaciones de Microsoft 365 Teams (con aplicación de Azure AD)** y, a continuación, puede ver los colaboradores que aparecen en el canal de salida, como se muestra en la siguiente imagen:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="list":::

  4. Inserte el proyecto en GitHub.

     > [!NOTE]
     > Los colaboradores recién agregados no reciben ninguna notificación. El propietario del proyecto debe notificar al colaborador.

### <a name="as-project-collaborator"></a>Como colaborador del proyecto

  1. Clone el proyecto desde GitHub.
  2. Inicie sesión en la cuenta de Microsoft 365.
  3. Inicie sesión en la cuenta de Azure, tiene permiso de colaborador para todos los recursos de Azure que se usan en el proyecto.
  4. Para obtener una vista previa de la aplicación de Teams, implemente el proyecto en remoto.
  5. Inicie el control remoto para tener una vista previa de la aplicación de Teams.

     > [!NOTE]
     > Los colaboradores deben iniciar sesión con la cuenta que el propietario del proyecto agrega en el mismo inquilino con el propietario del proyecto. Para obtener más información, consulte [Compilación y ejecución de la aplicación de Teams en un entorno remoto](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch).

## <a name="remove-collaborators"></a>Quitar colaboradores

Si desea quitar colaboradores de la extensión Teams Toolkit, debe quitarlos manualmente, ya que no puede quitarlos directamente. Realice los pasos siguientes para quitar colaboradores manualmente:

* Uso del Portal para desarrolladores

  * Vaya al [Portal para desarrolladores de Teams](https://dev.teams.microsoft.com/home) y seleccione la aplicación de Teams por nombre o identificador de aplicación.
  * Seleccione **Propietarios** en el panel izquierdo.
  * Seleccione y quite el colaborador.

* Uso de Azure Active Directory

  * Vaya a [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), seleccione **Registro de aplicaciones** en el panel izquierdo y busque la aplicación de Azure AD.
  * Seleccione **Propietarios** en el panel izquierdo en la página Administración de aplicaciones de Azure AD.
  * Seleccione y quite el colaborador.

    > [!NOTE]
    >
    > * El colaborador agregado al proyecto no recibe ninguna notificación. El propietario del proyecto debe notificar al colaborador sin conexión.
    > * El administrador de suscripciones de Azure debe establecer manualmente los permisos relacionados con Azure en Azure Portal.
    > * La cuenta de Azure debe tener el rol de colaborador de la suscripción para que los desarrolladores puedan trabajar juntos para aprovisionar e implementar el proyecto TeamsFx.

## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Implementar la aplicación de Teams en la nube](deploy.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)
