---
title: Plantillas de CI/CD
author: MuyangAmigo
description: En este módulo, aprenderá a usar plantillas de canalización de CI/CD en GitHub, Azure DevOps y Jenkins para desarrolladores de aplicaciones de Teams Plantillas de CI/CD
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 04/20/2022
ms.openlocfilehash: 05f797afcf54cab2d23ee24aae2c4985f3d724f2
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806875"
---
# <a name="set-up-cicd-pipelines"></a>Configuración de canalizaciones CI/CD

TeamsFx ayuda a automatizar el flujo de trabajo de desarrollo al compilar la aplicación de Teams. A continuación se muestran las herramientas y plantillas que puede usar para configurar canalizaciones de CI/CD, crear plantillas de flujo de trabajo y personalizar el flujo de trabajo de CI/CD con GitHub, Azure DevOps, Jenkins y otras plataformas. Para aprovisionar e implementar recursos, puede crear entidades de servicio de Azure y publicar la aplicación de Teams mediante el portal para desarrolladores de Teams. Para publicar la aplicación de Teams manualmente, puede aprovechar el [portal para desarrolladores para Teams](https://dev.teams.microsoft.com/home).

|Herramientas y plantillas | Descripción |
|---|---|
|[TeamsFx-CLI-Action](https://github.com/OfficeDev/teamsfx-cli-action)|Acción de GitHub que se integra con la CLI de TeamsFx.|
|[Kit de herramientas de Teams para Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| La extensión de Visual Studio Code que le ayuda a desarrollar los flujos de trabajo de automatización y las aplicaciones de Teams para GitHub, Azure DevOps y Jenkins. |
|[TeamsFx CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) | Herramienta de línea de comandos que le ayuda a desarrollar los flujos de trabajo de automatización y las aplicaciones de Teams para GitHub, Azure DevOps y Jenkins.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) y [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Crear plantillas de scripts para la automatización fuera de GitHub, Azure DevOps o Jenkins. |

## <a name="set-up-pipelines"></a>Configuración de canalizaciones

Puede configurar canalizaciones con las siguientes plataformas:

1. [Configuración de canalizaciones con GitHub](#set-up-pipelines-with-github)
1. [Configuración de canalizaciones con Azure DevOps](#set-up-pipelines-with-azure-devops)
1. [Configuración de canalizaciones con Jenkins](#set-up-pipelines-with-jenkins)
1. [Configuración de canalizaciones para otras plataformas](#set-up-pipelines-for-other-platforms)

## <a name="set-up-pipelines-with-github"></a>Configuración de canalizaciones con GitHub

Para configurar canalizaciones con GitHub para CI/CD:

* Creación de plantillas de flujo de trabajo.

  * Visual Studio Code
  * TeamsFx CLI

* Personalización del flujo de trabajo de CI/CD.

### <a name="create-workflow-templates"></a>Creación de plantillas de flujo de trabajo

Puede crear las siguientes plantillas de flujo de trabajo con GitHub:

**Kit de herramientas de Teams para Visual Studio Code**

1. Creación de un nuevo proyecto de aplicación de Teams con el Kit de herramientas de Teams.

1. Seleccione el icono :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: **del kit de herramientas de Teams** en el panel izquierdo.

1. Seleccione **Agregar características.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/add-feature.png" alt-text="Adición de la característica":::

1. Seleccione **Agregar flujos de trabajo de CI/CD**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/toolkit-ci-cd-workflow.png" alt-text="Selección del flujo de trabajo de CI/CD":::

1. Seleccione un entorno en el símbolo del sistema.
1. Seleccione **GitHub** como proveedor de CI/CD.
1. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar o Publicar en Teams.
1. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
1. Siga los archivos LÉAME de `.github/workflows` para configurar el flujo de trabajo en GitHub.

**TeamsFx CLI**

1. Escriba `cd` en el directorio del proyecto de aplicación de Teams.
2. Escriba el comando `teamsfx add cicd` para iniciar el proceso de comando interactivo.
3. Seleccione un entorno en el símbolo del sistema.
4. Seleccione **GitHub** como proveedor de CI/CD.
5. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar o Publicar en Teams.
7. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
8. Siga los archivos LÉAME de `.github/workflows` para configurar el flujo de trabajo en GitHub.

> [!NOTE]
> Si necesita agregar plantillas de flujo de trabajo adicionales, puede seguir el mismo procedimiento para crear una plantilla de flujo de trabajo en Visual Studio Code o en la CLI de TeamsFx.

### <a name="customize-cicd-workflow"></a>Personalización del flujo de trabajo de CI/CD

Puede cambiar o quitar los scripts de prueba para personalizar el flujo de trabajo de CI/CD:

1. De forma predeterminada, el flujo de trabajo de CD se desencadena cuando se realizan nuevas confirmaciones en la rama `main`.
1. Cambie los scripts de compilación si es necesario.
1. Quite los scripts de prueba según sea necesario.

## <a name="set-up-pipelines-with-azure-devops"></a>Configuración de canalizaciones con Azure DevOps

Para configurar canalizaciones con Azure DevOps para CI/CD:

* Creación de plantillas de flujo de trabajo.

  * Visual Studio Code
  * TeamsFx CLI

* Personalización del flujo de trabajo de CI/CD.

### <a name="create-workflow-templates"></a>Creación de plantillas de flujo de trabajo

Puede crear las siguientes plantillas de flujo de trabajo con Azure DevOps:

**Kit de herramientas de Teams para Visual Studio Code**

1. Creación de un nuevo proyecto de aplicación de Teams con el Kit de herramientas de Teams.
2. Seleccione el icono :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: **del kit de herramientas de Teams** en el panel izquierdo.
1. Seleccione **Agregar flujos de trabajo de CI/CD**.
1. Seleccione un entorno en el símbolo del sistema.
1. Seleccione **Azure DevOps** como proveedor de CI/CD.
1. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar y Publicar para Teams.
1. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
1. Siga los archivos LÉAME de `.azure/pipelines` para configurar el flujo de trabajo en Azure DevOps.

**TeamsFx CLI**

1. Escriba `cd` en el directorio del proyecto de aplicación de Teams.
2. Escriba el comando `teamsfx add cicd` para iniciar el proceso de comando interactivo.
3. Seleccione un entorno en el símbolo del sistema.
4. Seleccione **Azure DevOps** como proveedor de CI/CD.
5. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar o Publicar en Teams.
7. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
8. Siga los archivos LÉAME de `.azure/pipelines` para configurar el flujo de trabajo en Azure DevOps.

> [!NOTE]
> Si necesita agregar plantillas de flujo de trabajo adicionales, puede seguir el mismo procedimiento para crear una plantilla de flujo de trabajo en Visual Studio Code o en la CLI de TeamsFx.

### <a name="customize-ci-workflow"></a>Personalización del flujo de trabajo de CI

Puede realizar los siguientes cambios para la definición de script o flujo de trabajo:

1. Use el script de compilación npm o personalice la forma de compilar en el código de automatización.
1. Use el script de prueba npm, que vuelve a ser cero para que se realice correctamente y cambie los comandos de prueba.

### <a name="customize-cd-workflow"></a>Personalización del flujo de trabajo de CD

Puede realizar los siguientes cambios para la definición de script o flujo de trabajo:

1. Asegúrese de que tiene un script de compilación npm o personalice la forma de compilar en el código de automatización.
1. Asegúrese de que tiene un script de prueba npm que vuelve a ser cero para que se realice correctamente o cambie los comandos de prueba.

## <a name="set-up-pipelines-with-jenkins"></a>Configuración de canalizaciones con Jenkins

Para configurar canalizaciones con Jenkins para CI/CD:

* Creación de plantillas de flujo de trabajo.

  * Visual Studio Code
  * TeamsFx CLI

* Personalización del flujo de trabajo de CI/CD.

### <a name="create-workflow-templates"></a>Creación de plantillas de flujo de trabajo

Puede crear las siguientes plantillas de flujo de trabajo con Jenkins:

**Kit de herramientas de Teams para Visual Studio Code**

1. Creación de un nuevo proyecto de aplicación de Teams con el Kit de herramientas de Teams.
2. Seleccione el icono :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: **del kit de herramientas de Teams** en el panel izquierdo.
3. Seleccione **Agregar flujos de trabajo de CI/CD**.
4. Seleccione un entorno en el símbolo del sistema.
5. Seleccione **Jenkins** como proveedor de CI/CD.
6. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar o Publicar en Teams.
7. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
8. Siga los archivos LÉAME de `.jenkins/pipelines` para configurar el flujo de trabajo con Jenkins.

**TeamsFx CLI**

1. Escriba `cd` en el directorio del proyecto de aplicación de Teams.
2. Escriba el comando `teamsfx add cicd` para iniciar el proceso de comando interactivo.
3. Seleccione un entorno en el símbolo del sistema.
4. Seleccione **Jenkins** como proveedor de CI/CD.
5. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar o Publicar en Teams.
7. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
8. Siga los archivos LÉAME de `.jenkins/pipelines` para configurar el flujo de trabajo con Jenkins.

> [!NOTE]
> Si necesita agregar plantillas de flujo de trabajo adicionales, puede seguir el mismo procedimiento para crear una plantilla de flujo de trabajo en Visual Studio Code o en la CLI de TeamsFx.

### <a name="customize-ci-workflow"></a>Personalización del flujo de trabajo de CI

Puede realizar los siguientes cambios en el proyecto:

1. Cambie cómo se desencadena el flujo de CI. El valor predeterminado es usar los desencadenadores de **pollSCM** cuando se inserta un nuevo cambio en la rama de **desarrollo**.
1. Asegúrese de que tiene un script de compilación npm o personalice la forma de compilar en el código de automatización.
1. Asegúrese de que tiene un script de prueba npm que vuelve a ser cero para que se realice correctamente o cambie los comandos de prueba.

### <a name="customize-cd-workflow"></a>Personalización del flujo de trabajo de CD

Siga estos pasos para personalizar la canalización de CD:

1. Cambie el flujo de CD. El valor predeterminado es usar los desencadenadores de `pollSCM` cuando se inserta un nuevo cambio en la rama `main`.
1. Cambie los scripts de compilación si es necesario.
1. Quite los scripts de prueba si no tiene pruebas.

## <a name="set-up-pipelines-for-other-platforms"></a>Configuración de canalizaciones para otras plataformas

Puede seguir los scripts de bash de ejemplo predefinidos para compilar y personalizar canalizaciones de CI/CD en las otras plataformas:

* [Scripts de CI](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [Scripts de CD](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

Los scripts se basan en una herramienta de línea de comandos TeamsFx multiplataforma [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli). Puede instalarlo con `npm install -g @microsoft/teamsfx-cli` y seguir la [documentación](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) para personalizar los scripts.

> [!NOTE]
>
> * Para habilitar la ejecución de `@microsoft/teamsfx-cli` en modo CI, active `CI_ENABLED` mediante `export CI_ENABLED=true`. En el modo CI, `@microsoft/teamsfx-cli` es fácil de usar para CI/CD.
> * Para habilitar la ejecución en modo no interactivo de `@microsoft/teamsfx-cli`, establezca una configuración global con el comando: `teamsfx config set -g interactive false`. En el modo no interactivo, `@microsoft/teamsfx-cli` no solicita entradas.

Asegúrese de configurar las credenciales de Azure y Microsoft 365 en las variables de entorno de forma segura. Por ejemplo, si usa GitHub como su repositorio de código fuente, consulte [Secretos de Github](https://docs.github.com/en/actions/reference/encrypted-secrets).

## <a name="provision-and-deploy-resources"></a>Aprovisionamiento e implementación de recursos

Para aprovisionar e implementar recursos destinados a Azure dentro de CI/CD, debe crear una entidad de servicio de Azure para su uso.

Siga estos pasos para crear entidades de servicio de Azure:

1. Registre una aplicación de Microsoft Azure Active Directory (Azure AD) en un solo inquilino.
2. Asigne un rol a la aplicación de Azure AD para acceder a su suscripción de Azure. Se recomienda el rol `Contributor`.
3. Crear una nueva aplicación de Azure AD para el complemento

> [!TIP]
> Guarde el identificador de inquilino, el identificador de aplicación (AZURE_SERVICE_PRINCIPAL_NAME) y el secreto (AZURE_SERVICE_PRINCIPAL_PASSWORD) para su uso futuro.

Para obtener más información, consulte [Directrices de entidades de servicio de Azure](/azure/active-directory/develop/howto-create-service-principal-portal). Estas son las tres maneras de crear entidades de servicio:

* [Portal de Microsoft Azure](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [CLI de Microsoft Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>Publicación de la aplicación de Teams mediante el portal para desarrolladores de Teams

Si hay cambios relacionados con el archivo de manifiesto de la aplicación de Teams, puede actualizar el manifiesto y volver a publicar la aplicación de Teams. Para publicar la aplicación de Teams manualmente, puede aprovechar el [portal para desarrolladores para Teams](https://dev.teams.microsoft.com/home).

Realice los pasos siguientes para publicar la aplicación:

1. Inicie sesión en el [portal para desarrolladores de Teams](https://dev.teams.microsoft.com) con la cuenta correspondiente.
2. Importe el paquete de la aplicación en zip y seleccione `App -> Import app -> Replace`.
3. Seleccione la aplicación de destino en la lista de aplicaciones.
4. Publique la aplicación y seleccione `Publish -> Publish to your org`.

## <a name="see-also"></a>Consulte también

* [Inicio rápido para Acciones de GitHub](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Creación de la primera canalización de Azure DevOps](/azure/devops/pipelines/create-first-pipeline)
* [Creación de la primera canalización de Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Administre sus aplicaciones con el Portal para desarrolladores de Microsoft Teams](../concepts/build-and-test/teams-developer-portal.md)
