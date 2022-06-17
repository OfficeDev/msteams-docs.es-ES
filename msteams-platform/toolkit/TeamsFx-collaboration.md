---
title: Colaborar en TeamsFx Project mediante Teams Toolkit
author: yanjiang
description: En este artículo, aprenderá a colaborar en TeamsFx Project mediante Teams Toolkit y a colaborar con otros desarrolladores.
ms.author: rentu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 0f81990603b3e0275a057c489d7fac44ee0127cc
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142062"
---
# <a name="collaborate-on-teams-project-using-teams-toolkit"></a>Colaborar en un proyecto de Teams con el kit de herramientas de Teams

Varios desarrolladores pueden trabajar juntos para depurar, aprovisionar e implementar para el mismo proyecto TeamsFx, pero requiere establecer manualmente los permisos adecuados de Teams App y Microsoft Azure Active Directory (Azure AD). Teams Toolkit admite la característica de colaboración para permitir que los desarrolladores y el propietario del proyecto inviten a otros desarrolladores o colaboradores al proyecto TeamsFx para depurar, aprovisionar e implementar el mismo proyecto teamsfx.

## <a name="prerequisites"></a>Requisitos previos

* Suscripción a Microsoft 365
* Azure con una suscripción válida
  
  Para obtener más información sobre las distintas cuentas, consulte [Preparación de cuentas para compilar Teams aplicación](accounts.md).

* [Instalar Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) versión v3.0.0+

> [!TIP]
> Asegúrese de que tiene un proyecto de aplicación Teams abierto en Visual Studio Code.

## <a name="collaborate-with-other-developers"></a>Colaborar con otros desarrolladores

Las listas siguientes nos guían para comprender el proceso de colaboración y su limitación:

* Como propietario del proyecto

  > [!NOTE]
  > Antes de agregar colaboradores para un entorno, el propietario del proyecto debe [aprovisionar](provision.md) primero el proyecto.

  1. En **la sección ENTORNO** de Teams Toolkit, seleccione **colaboradores**. Muestra las opciones **Add Microsoft 365 Teams App (with Azure AD App) Owners** and List Microsoft 365 Teams App (With Azure AD App) Owners (Agregar Microsoft 365 Teams app (con aplicación de Azure AD) Owners (Con aplicación de Azure AD) y **List Microsoft 365 Teams App (with Azure AD App) Owners (Propietarios de la aplicación de Azure AD)** como se muestra en las imágenes siguientes:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/add collaborators.png" alt-text="Colaboradores":::

  2. Seleccione **Agregar propietarios de Microsoft 365 Teams App (con la aplicación de Azure AD)** y agregue otra dirección de correo electrónico de cuenta de Microsoft 365 como colaborador. La cuenta que se va a agregar debe estar en el mismo inquilino que el propietario del proyecto para la depuración remota como se muestra en la imagen:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="agregar entorno":::

  3. Para ver los colaboradores en el entorno actual, seleccione **Enumerar Microsoft 365 Teams aplicación (con la aplicación de Azure AD) Propietarios** y, a continuación, los colaboradores se muestran en el canal de salida, como se muestra en la siguiente imagen:

     :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/list of collaborators.png" alt-text="lista":::

  4. Insertar el proyecto en GitHub

     > [!NOTE]
     > Los colaboradores recién agregados no reciben ninguna notificación. El propietario Project debe notificar al colaborador.

* Como colaborador del proyecto

  1. Clone el proyecto desde GitHub.
  2. Inicie sesión en Microsoft 365 cuenta.
  3. Inicie sesión en la cuenta de Azure, tiene permiso de colaborador para todos los recursos de Azure que se usan en el proyecto.
  4. Para obtener una vista previa de la aplicación Teams, implemente el proyecto en remoto.
  5. Inicie el control remoto para tener una vista previa de la aplicación Teams.

     > [!NOTE]
     > Los colaboradores deben iniciar sesión con la cuenta que el propietario del proyecto agrega en el mismo inquilino con el propietario del proyecto. Para obtener más información, consulte [Compilación y ejecución de la aplicación Teams en un entorno remoto](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=3&branch).

### <a name="limitations"></a>Limitaciones

Si desea quitar colaboradores de Teams Toolkit extensión, debe quitarlos manualmente, ya que no puede quitarlos directamente. Realice los pasos siguientes para quitar colaboradores manualmente:

* Uso del Portal para desarrolladores

  * Vaya a [Teams Portal para desarrolladores](https://dev.teams.microsoft.com/home) y seleccione la aplicación de Teams por nombre o identificador de aplicación.
  * Seleccione **Propietarios** en el panel izquierdo.
  * Seleccione y quite el colaborador.

* Uso de Azure Active Directory

  * Vaya a [Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), seleccione **Registro de aplicaciones** en el panel izquierdo y busque la aplicación de Azure AD.
  * Seleccione **Propietarios** en el panel izquierdo en la página Administración de aplicaciones de Azure AD.
  * Seleccione y quite el colaborador.

   > [!NOTE]
   >
   > * El colaborador agregado al proyecto no recibe ninguna notificación. Project propietario debe notificar al colaborador sin conexión.
   > * El administrador de suscripciones de Azure debe establecer manualmente los permisos relacionados con Azure en Azure Portal. La cuenta de Azure debe tener el rol de colaborador de la suscripción para que los desarrolladores puedan trabajar juntos para aprovisionar e implementar el proyecto TeamsFx.

## <a name="see-also"></a>Vea también

* [Aprovisionar recursos en la nube](provision.md)
* [Implementar la aplicación de Teams en la nube](deploy.md)
* [Administrar varios entornos](TeamsFx-multi-env.md)
