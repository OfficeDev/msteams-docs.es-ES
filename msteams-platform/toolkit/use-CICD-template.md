---
title: Aprenda a usar plantillas de canalización de CI/CD en GitHub, Azure DevOps y Jenkins para desarrolladores de aplicaciones de Teams
author: MuyangAmigo
description: Plantillas de CI/CD
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 04/20/2022
ms.openlocfilehash: 66560b1f228c32b0faf6569ff0ae536a81dc33c0
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073296"
---
# <a name="set-up-cicd-pipelines"></a>Configuración de canalizaciones de CI/CD

TeamsFx ayuda a automatizar el flujo de trabajo de desarrollo al compilar Teams aplicación. A continuación se muestran las herramientas y plantillas que puede usar para configurar canalizaciones de CI/CD, crear plantillas de flujo de trabajo y personalizar el flujo de trabajo de CI/CD con GitHub, Azure DevOps, Jenkins y otras plataformas. Para aprovisionar e implementar recursos, puede crear entidades de servicio de Azure y publicar la aplicación de Teams mediante Teams Portal para desarrolladores. Para publicar Teams aplicación manualmente, puede aprovechar [el Portal para desarrolladores para Teams](https://dev.teams.microsoft.com/home).


|Herramientas y plantillas | Descripción |
|---|---|
|[TeamsFx-CLI-Action](https://github.com/OfficeDev/teamsfx-cli-action)|GitHub Acción que se integra con la CLI de TeamsFx.|
|[Teams Toolkit en Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Visual Studio Code extensión que le ayuda a desarrollar Teams aplicación, así como flujos de trabajo de automatización para GitHub, Azure DevOps y Jenkins. |
|[TeamsFx CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) | Herramienta de línea de comandos que le ayuda a desarrollar Teams aplicación, así como flujos de trabajo de automatización para GitHub, Azure DevOps y Jenkins.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) y [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Crear scripts de plantillas para la automatización fuera de GitHub, Azure DevOps o Jenkins. |


## <a name="set-up-pipelines"></a>Configuración de canalizaciones

Puede configurar canalizaciones con las siguientes plataformas:

1. [Configuración de canalizaciones con GitHub](#set-up-pipelines-with-github)
1. [Configuración de canalizaciones con Azure DevOps](#set-up-pipelines-with-azure-devops)
1. [Configuración de canalizaciones con Jenkins](#set-up-pipelines-with-jenkins)
1. [Configuración de canalizaciones para otras plataformas](#set-up-pipelines-for-other-platforms)


### <a name="set-up-pipelines-with-github"></a>Configuración de canalizaciones con GitHub

Para configurar canalizaciones con GitHub para CI/CD:

1. Crear plantillas de flujo de trabajo.

   * Visual Studio Code
   * TeamsFx CLI

1. Personalización del flujo de trabajo de CI/CD.


## <a name="create-workflow-templates-with-github"></a>Creación de plantillas de flujo de trabajo con GitHub

**Creación de plantillas de flujo de trabajo mediante el Teams Toolkit en Visual Studio Code**

1. Cree un nuevo proyecto de aplicación de Teams mediante Teams Toolkit.
1. Seleccione **Teams Toolkit** icono en la barra de actividad de Visual Studio Code.
1. Seleccione **Agregar flujos de trabajo de CI/CD**.
1. Seleccione un entorno en el símbolo del sistema.
1. Seleccione **GitHub** como proveedor de CI/CD.
1. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar o Publicar para Teams.
1. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
1. Siga los archivos LÉAME de `.github/workflows` para configurar el flujo de trabajo en GitHub.

**Creación de plantillas de flujo de trabajo mediante la CLI de TeamsFx**

1. Escriba en `cd` el directorio del proyecto de aplicación de Teams.
2. Escriba `teamsfx add cicd` el comando para iniciar el proceso de comando interactivo.
3. Seleccione un entorno en el símbolo del sistema.
4. Seleccione **GitHub** como proveedor de CI/CD.
5. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar o Publicar para Teams.
7. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
8. Siga los archivos LÉAME de `.github/workflows` para configurar el flujo de trabajo en GitHub.

> [!NOTE]
> Si necesita agregar plantillas de flujo de trabajo adicionales, puede seguir el mismo procedimiento para crear una plantilla de flujo de trabajo en Visual Studio Code o en la CLI de TeamsFx.

### <a name="customize-cicd-workflow"></a>Personalización del flujo de trabajo de CI/CD

Puede cambiar o quitar los scripts de prueba para personalizar el flujo de trabajo de CI/CD:

1. De forma predeterminada, el flujo de trabajo de CD se desencadena cuando se realizan nuevas confirmaciones en la `main` rama.
1. Cambie los scripts de compilación si es necesario.
1. Quite los scripts de prueba según sea necesario.

### <a name="set-up-pipelines-with-azure-devops"></a>Configuración de canalizaciones con Azure DevOps

Para configurar canalizaciones con Azure DevOps para CI/CD:

1. Crear plantillas de flujo de trabajo.

   * Visual Studio Code
   * TeamsFx CLI

1. Personalización del flujo de trabajo de CI/CD.


## <a name="create-workflow-templates-with-azure-devops"></a>Creación de plantillas de flujo de trabajo con Azure DevOps

**Creación de plantillas de flujo de trabajo mediante el Teams Toolkit en Visual Studio Code**

1. Cree un nuevo proyecto de aplicación de Teams mediante Teams Toolkit.
2. Seleccione **Teams Toolkit** icono en la barra de actividad de Visual Studio Code.
3. Seleccione **Agregar flujos de trabajo de CI/CD**.
4. Seleccione un entorno en el símbolo del sistema.
5. Seleccione **Azure DevOps** como proveedor de CI/CD.
6. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar y Publicar para Teams.
7. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
8. Siga los archivos LÉAME de `.azure/pipelines` para configurar el flujo de trabajo en Azure DevOps.

**Creación de plantillas de flujo de trabajo mediante la CLI de TeamsFx**

1. Escriba en `cd` el directorio del proyecto de aplicación de Teams.
2. Escriba `teamsfx add cicd` el comando para iniciar el proceso de comando interactivo.
3. Seleccione un entorno en el símbolo del sistema.
4. Seleccione **Azure DevOps** como proveedor de CI/CD.
5. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar o Publicar para Teams.
7. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
8. Siga los archivos LÉAME de `.azure/pipelines` para configurar el flujo de trabajo en Azure DevOps.

> [!NOTE]
> Si necesita agregar plantillas de flujo de trabajo adicionales, puede seguir el mismo procedimiento para crear una plantilla de flujo de trabajo en Visual Studio Code o en la CLI de TeamsFx.

### <a name="customize-ci-workflow"></a>Personalización del flujo de trabajo de CI

A continuación se muestran los cambios que puede realizar para la definición de script o flujo de trabajo:

1. Use el script de compilación npm o personalice la forma de compilar en el código de automatización.
1. Use el script de prueba npm que devuelve cero para que se realice correctamente y cambie los comandos de prueba.

### <a name="customize-cd-workflow"></a>Personalización del flujo de trabajo de CD

A continuación se muestran los cambios que puede realizar para la definición de script o flujo de trabajo:

1. Asegúrese de que tiene un script de compilación npm o personalice la forma de compilar en el código de automatización.
1. Asegúrese de que tiene un script de prueba npm que devuelve cero para que se realice correctamente o cambie los comandos de prueba.

### <a name="set-up-pipelines-with-jenkins"></a>Configuración de canalizaciones con Jenkins

Para configurar canalizaciones con Jenkins para CI/CD:

1. Crear plantillas de flujo de trabajo.

   * Visual Studio Code
   * TeamsFx CLI

1. Personalización del flujo de trabajo de CI/CD.

## <a name="create-workflow-templates-with-jenkins"></a>Creación de plantillas de flujo de trabajo con Jenkins

**Creación de plantillas de flujo de trabajo mediante el Teams Toolkit en Visual Studio Code**

1. Cree un nuevo proyecto de aplicación de Teams mediante Teams Toolkit.
2. Seleccione **Teams Toolkit** icono en la barra lateral Visual Studio Code.
3. Seleccione **Agregar flujos de trabajo de CI/CD**.
4. Seleccione un entorno en el símbolo del sistema.
5. Seleccione **Jenkins** como proveedor de CI/CD.
6. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar o Publicar para Teams.
7. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
8. Siga los archivos LÉAME de `.jenkins/pipelines` para configurar el flujo de trabajo con Jenkins.

**Creación de plantillas de flujo de trabajo mediante la CLI de TeamsFx**

1. Escriba en `cd` el directorio del proyecto de aplicación de Teams.
2. Escriba `teamsfx add cicd` el comando para iniciar el proceso de comando interactivo.
3. Seleccione un entorno en el símbolo del sistema.
4. Seleccione **Jenkins** como proveedor de CI/CD.
5. Seleccione al menos una plantilla de estas opciones: CI, CD, Aprovisionar o Publicar para Teams.
7. Abra la plantilla y personalice los flujos de trabajo que encajan en los escenarios.
8. Siga los archivos LÉAME de `.jenkins/pipelines` para configurar el flujo de trabajo con Jenkins.

> [!NOTE]
> Si necesita agregar plantillas de flujo de trabajo adicionales, puede seguir el mismo procedimiento para crear una plantilla de flujo de trabajo en Visual Studio Code o en la CLI de TeamsFx.

### <a name="customize-ci-workflow"></a>Personalización del flujo de trabajo de CI

Estos son algunos de los cambios que puede realizar en el proyecto:

1. Cambie cómo se desencadena el flujo de CI. El valor predeterminado es usar los desencadenadores de **pollSCM** cuando se inserta un nuevo cambio en la rama **de desarrollo** .
1. Asegúrese de que tiene un script de compilación npm o personalice la forma de compilar en el código de automatización.
1. Asegúrese de que tiene un script de prueba npm que devuelve cero para que se realice correctamente o cambie los comandos de prueba.


### <a name="customize-cd-workflow"></a>Personalización del flujo de trabajo de CD

Siga estos pasos para personalizar la canalización de CD:

1. Cambie el flujo de CD. El valor predeterminado es usar los desencadenadores de `pollSCM` cuando se inserta un nuevo cambio en la `main` rama.
1. Cambie los scripts de compilación si es necesario.
1. Quite los scripts de prueba si no tiene pruebas.


### <a name="set-up-pipelines-for-other-platforms"></a>Configuración de canalizaciones para otras plataformas

Puede seguir los scripts de bash de ejemplo predefinidos para compilar y personalizar canalizaciones de CI/CD en las otras plataformas:

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

Los scripts se basan en una herramienta de línea de comandos teamsfx multiplataforma [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli). Puede instalarlo con `npm install -g @microsoft/teamsfx-cli` y seguir la [documentación](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) para personalizar los scripts.

> [!NOTE]
>
> * Para habilitar `@microsoft/teamsfx-cli` la ejecución en modo CI, active `CI_ENABLED` por `export CI_ENABLED=true`. En el modo CI, `@microsoft/teamsfx-cli` es fácil de usar para CI/CD.
> * Para habilitar `@microsoft/teamsfx-cli` la ejecución en modo no interactivo, establezca una configuración global con el comando : `teamsfx config set -g interactive false`. En el modo no interactivo, `@microsoft/teamsfx-cli` no solicita entradas.

Asegúrese de configurar Azure y Microsoft 365 credenciales en las variables de entorno de forma segura. Por ejemplo, si usa GitHub como repositorio de código fuente, consulte [Secretos de Github](https://docs.github.com/en/actions/reference/encrypted-secrets).


## <a name="provision-and-deploy-resources"></a>Aprovisionamiento e implementación de recursos

Para aprovisionar e implementar recursos destinados a Azure dentro de CI/CD, debe crear una entidad de servicio de Azure para su uso.

Siga estos pasos para crear entidades de servicio de Azure:

1. Registre una aplicación de Microsoft Azure Active Directory (Azure AD) en un solo inquilino.
2. Asigne un rol a la aplicación de Azure AD para acceder a la suscripción de Azure. Se recomienda el `Contributor` rol.
3. Cree un nuevo secreto de aplicación Azure AD.

> [!TIP]
> Guarde el identificador de inquilino, el identificador de aplicación (AZURE_SERVICE_PRINCIPAL_NAME) y el secreto (AZURE_SERVICE_PRINCIPAL_PASSWORD) para su uso futuro.

Para obtener más información, consulte [Directrices de entidades de servicio de Azure](/azure/active-directory/develop/howto-create-service-principal-portal). Estas son las tres maneras de crear entidades de servicio:

* [portal de Microsoft Azure](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [CLI de Microsoft Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>Publicación de Teams aplicación mediante Teams Portal para desarrolladores

Si hay cambios relacionados con el archivo de manifiesto de Teams aplicación, puede actualizar el manifiesto y volver a publicar la aplicación de Teams.

Para publicar Teams aplicación manualmente, puede aprovechar [el Portal para desarrolladores para Teams](https://dev.teams.microsoft.com/home).

Realice los pasos siguientes para publicar la aplicación:

1. Inicie sesión en [el portal para desarrolladores para Teams](https://dev.teams.microsoft.com) con la cuenta correspondiente.
2. Para importar el paquete de la aplicación en zip, seleccione `App -> Import app -> Replace`.
3. Seleccione la aplicación de destino en la lista de aplicaciones.
4. Para publicar la aplicación, seleccione `Publish -> Publish to your org`.

### <a name="see-also"></a>Ver también

* [Inicio rápido para Acciones de GitHub](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Creación de la primera canalización de Azure DevOps](/azure/devops/pipelines/create-first-pipeline)
* [Creación de la primera canalización de Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Administre sus aplicaciones con el Portal para desarrolladores de Microsoft Teams](/concepts/build-and-test/teams-developer-portal)
