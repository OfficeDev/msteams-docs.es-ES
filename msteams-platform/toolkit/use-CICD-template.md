---
title: Compatibilidad de CI o CD para desarrolladores Teams aplicaciones
author: MuyangAmigo
description: Plantillas CICD
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: acd12a96365bf97bd419045c415e71efd3a118e2
ms.sourcegitcommit: aede47694894d281f6b725083bc0b46ab0e4846d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/22/2021
ms.locfileid: "61591781"
---
# <a name="ci-or-cd-support-for-teams-application-developers"></a>Compatibilidad con CI o CD para Teams programadores de aplicaciones

TeamsFx ayuda a automatizar el flujo de trabajo de desarrollo al crear Teams aplicación. El documento proporciona herramientas y plantillas preconcebadas para empezar a configurar canalizaciones de CI o CD con las plataformas de desarrollo más populares, incluidos GitHub, Azure Devops y Jenkins.

|Herramientas y plantillas|Description|
|---|---|
|[teamsfx-cli-action](https://github.com/OfficeDev/teamsfx-cli-action)|Una acción de GitHub lista para usar que se integra con la CLI de TeamsFx.|
|[github-ci-template.yml y](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)| GitHub plantillas de CI o CD para una Teams aplicación. |
|[jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) y [jenkins-cd-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)|Plantillas de CI o CD de Jenkins para una Teams aplicación.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) y [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Plantillas de script para la automatización en cualquier lugar fuera de GitHub. |

## <a name="ci-or-cd-workflow-templates-in-github"></a>Plantillas de flujo de trabajo de CI o CD en GitHub

**Para incluir flujos de trabajo de CI** o CD para automatizar Teams de desarrollo de aplicaciones en GitHub :

1. Crear una carpeta en `.github/workflows`
1. Copie los archivos de plantilla (uno o ambos):
    * [github-ci-template.yml para flujo](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) de trabajo de CI.
    * [github-cd-template.yml para flujo](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml) de trabajo de CD.
1. Personalice estos flujos de trabajo para que se adapten a sus escenarios.

### <a name="customize-ci-workflow"></a>Personalizar flujo de trabajo de CI

Puede realizar los siguientes cambios para adaptar el flujo de trabajo del proyecto:

1. Cambiar cómo se desencadena el flujo de CI. El valor predeterminado es cuando se crea una solicitud de extracción dirigida a la `dev` rama.
1. Use un script de compilación de npm o personalice la forma en que se compila el proyecto en el código de automatización.
1. Use un script de prueba de npm que devuelva cero para el éxito y/o cambie los comandos de prueba.

### <a name="customize-cd-workflow"></a>Personalizar flujo de trabajo de CD

Los siguientes pasos para personalizar el flujo de trabajo de CD:

1. De forma predeterminada, el flujo de trabajo de CD se desencadena cuando se realizan nuevas confirmaciones en la `main` rama.
1. Cree GitHub [secretos de repositorio por](https://docs.github.com/en/actions/reference/encrypted-secrets) entorno para contener azure o Microsoft 365 credenciales de inicio de sesión. En la tabla siguiente se enumeran todos los secretos que necesita crear en GitHub y, para un uso detallado, consulte el GitHub Actions [README.md](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md).
1. Cambie los scripts de compilación si es necesario.
1. Quite los scripts de prueba si no tiene pruebas.

> [!Note]
> El paso de aprovisionamiento no se incluye en la plantilla de CD, ya que normalmente se ejecuta solo una vez. Puede ejecutar provision Within Teams Toolkit, CLI de TeamsFx o usar un flujo de trabajo separado. Recuerde confirmar después del aprovisionamiento (los resultados del aprovisionamiento se depositarán dentro de la carpeta) y guardar el contenido del archivo en secretos de repositorio de GitHub con el nombre para su uso `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` [](https://docs.github.com/en/actions/reference/encrypted-secrets) `USERDATA_CONTENT` futuro.

### <a name="environment-variables"></a>Variables de entorno

Pasos para crear variables de entorno en GitHub::

1. En la página de **Configuración** proyecto, vaya a **la sección Entornos** y seleccione **Nuevo entorno**.
1. Escriba un nombre para el entorno. El nombre de entorno predeterminado proporcionado en la plantilla es `test_environment` . Seleccione **Configurar entorno para** continuar.
1. En la página siguiente, seleccione **Agregar secreto** para agregar secretos para cada uno de los elementos enumerados en la tabla siguiente.

|Nombre|Descripción|
|---|---|
|AZURE_ACCOUNT_NAME|Nombre de cuenta de Azure que se usa para aprovisionar recursos.|
|AZURE_ACCOUNT_PASSWORD|La contraseña de la cuenta de Azure.|
|AZURE_SUBSCRIPTION_ID|Para identificar la suscripción en la que se aprovisionarán los recursos.|
|AZURE_TENANT_ID|Para identificar el espacio empresarial en el que reside la suscripción.|
|Microsoft 365_ACCOUNT_NAME|La Microsoft 365 cuenta para crear y publicar la Teams app.|
|Microsoft 365_ACCOUNT_PASSWORD|La contraseña de la Microsoft 365 cuenta.|
|Microsoft 365_TENANT_ID|Para identificar el espacio empresarial en el que se Teams se creará o publicará la aplicación. Este valor es opcional a menos que tenga una cuenta multiinquilino y desee usar otro inquilino. Obtenga más información [sobre cómo encontrar el identificador Microsoft 365 inquilino](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant).|

> [!NOTE]
> Consulte Configure [Microsoft 365/Azure Credentials](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret) para asegurarse de que ha deshabilitado multifactor Authentication and Security Defaults para las credenciales usadas en el flujo de trabajo.

## <a name="set-up-ci-or-cd-pipelines-with-azure-devops"></a>Configurar ci o cd Pipelines con Azure DevOps

Puede configurar canalizaciones automatizadas en Azure DevOps y hacer una referencia en los scripts. Siga los pasos que se indican a continuación para empezar:

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

### <a name="set-up-ci-pipeline"></a>Configurar canalización de CI

1. Agregue [scripts de CI](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) Azure DevOps repositorio y realice las personalizaciones necesarias que pueda deducir de los comentarios del archivo de script.
1. Siga los [pasos para crear su Azure DevOps pipeline para CI](/azure/devops/pipelines/create-first-pipeline).
Este es un escenario de scripts de canalización de CI comunes:

```yml
trigger:
- dev 

pool:
  vmImage: ubuntu-latest

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '14.17.0'
    checkLatest: true
  
- task: Bash@3
  inputs:
    filePath: './others-script-ci-template.sh'
```

Los posibles cambios que puede realizar para la definición de script o flujo de trabajo:

1. Cambiar cómo se desencadena el flujo de CI. El valor predeterminado es cuando se inserta una nueva confirmación en la `dev` rama.
1. Cambiar la forma de instalar node y npm.
1. Use el script de compilación npm o personalice la forma en que se compila en el código de automatización.
1. Use el script de prueba npm que devuelve cero para que se ejecuta correctamente y/o cambie los comandos de prueba.

### <a name="set-up-cd-pipeline"></a>Configurar canalización de CD

1. Agregue [scripts de CD](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) Azure DevOps repositorio y realice las personalizaciones necesarias que pueda deducir de los comentarios del archivo de script.
1. Cree la Azure DevOps para CD, como puede hacer referencia a [este vínculo](/azure/devops/pipelines/create-first-pipeline). La definición de la canalización se puede hacer referencia a la siguiente definición de ejemplo para la canalización de CI.
1. Agrega las variables necesarias [mediante Define variables](/azure/devops/pipelines/process/variables)y hazlas como secretos si es necesario.

```yml
trigger:
- main 

pool:
  vmImage: ubuntu-latest

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '14.17.0'
    checkLatest: true

- task: DownloadSecureFile@1
  name: userdata
  inputs:
    secureFile: 'staging.userdata'
- task: Bash@3
  inputs:
    targetType: 'inline'
    script: |
      mkdir -p .fx/states/
      cp $(userdata.secureFilePath) .fx/states/staging.userdata
  
- task: Bash@3
  env:
    AZURE_ACCOUNT_NAME: $(AZURE_ACCOUNT_NAME)
    AZURE_ACCOUNT_PASSWORD: $(AZURE_ACCOUNT_PASSWORD)
    AZURE_TENANT_ID: $(AZURE_TENANT_ID)
    Microsoft 365_ACCOUNT_NAME: $(Microsoft 365_ACCOUNT_NAME)
    Microsoft 365_ACCOUNT_PASSWORD: $(Microsoft 365_ACCOUNT_PASSWORD)
  inputs:
    filePath: './others-script-cd-template.sh'
```

Los posibles cambios que puede realizar para la definición de script o flujo de trabajo:

1. Cómo se desencadena el flujo de CD. De forma predeterminada, ocurre cuando se realizan nuevas confirmaciones en la **rama** principal.
1. Cambiar la forma de instalar node y npm.
1. Cambie el nombre del entorno, de forma predeterminada su **almacenamiento provisional**.
1. Asegúrese de que tiene un script de compilación npm o personalice la forma en que se compila en el código de automatización.
1. Asegúrese de que tiene un script de prueba npm que devuelve cero para el éxito y/o cambie los comandos de prueba.

> [!Note]
> El paso de aprovisionamiento no se incluye en la plantilla de CD, ya que normalmente se ejecuta solo una vez. Puede ejecutar la aprovisionamiento dentro de Teams Toolkit, CLI de TeamsFx o mediante un flujo de trabajo seperado. Recuerde confirmar después del aprovisionamiento (los resultados del aprovisionamiento se depositarán dentro de la carpeta) y cargar en Azure DevOps archivos seguros para `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` su uso futuro. [](/azure/devops/pipelines/library/secure-files)

### <a name="environment-variables-for-azure-devops"></a>Variables de entorno para Azure DevOps

Pasos para crear variables de canalización en Azure DevOps:

1. En la página Edición de canalización, seleccione **Variables** en la parte superior derecha y **seleccione Nueva variable**.
1. Escriba el par Nombre/Valor de la variable.
1. Activa la casilla mantener **este valor en secreto si** es necesario.
1. Seleccione **Aceptar** para crear la variable.

|Nombre|Descripción|
|---|---|
|AZURE_ACCOUNT_NAME|Nombre de cuenta de Azure que se usa para aprovisionar recursos.|
|AZURE_ACCOUNT_PASSWORD|La contraseña de la cuenta de Azure.|
|AZURE_SUBSCRIPTION_ID|Para identificar la suscripción en la que se aprovisionarán los recursos.|
|AZURE_TENANT_ID|Para identificar el espacio empresarial en el que reside la suscripción.|
|Microsoft 365_ACCOUNT_NAME|La Microsoft 365 cuenta para crear y publicar la Teams app.|
|Microsoft 365_ACCOUNT_PASSWORD|La contraseña de la Microsoft 365 cuenta.|
|Microsoft 365_TENANT_ID|Para identificar el espacio empresarial en el que se Teams se creará o publicará la aplicación. Este valor es opcional a menos que tenga una cuenta multiinquilino y desee usar otro inquilino. Obtenga más información [sobre cómo encontrar el identificador Microsoft 365 inquilino](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant).|

> [!NOTE]
> El paso de aprovisionamiento no se incluye en la plantilla de CD, ya que normalmente se ejecuta solo una vez. Puede ejecutar la aprovisionamiento dentro de Teams Toolkit, CLI de TeamsFx o mediante un flujo de trabajo seperado. Recuerde confirmar después del aprovisionamiento (los resultados del aprovisionamiento se depositarán dentro de la carpeta) y guardar el contenido del archivo en credenciales de Jenkins para `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` su uso futuro.

## <a name="ci-or-cd-pipeline-templates-in-jenkins"></a>Plantillas de canalización de CI o CD en Jenkins

Para agregar estas plantillas al repositorio, necesitará las versiones de [jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) y  [jenkins-cd-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile) que se ubicará en el repositorio por rama.

Además, debe crear canalizaciones de CI o CD en Jenkins que apunten al **jenkinsfile** específico correspondientemente.

Siga los pasos para comprobar cómo conectar Jenkins con diferentes plataformas SCM:

1. [Jenkins con GitHub](https://www.jenkins.io/solutions/github/)
2. [Jenkins con Azure DevOps](https://www.dragonspears.com/blog/ci-cd-with-jenkins-and-azure-devops-services)
3. [Jenkins con GitLab](https://docs.gitlab.com/ee/integration/jenkins.html)
4. [Jenkins con Bitbucket](https://medium.com/ampersand-academy/integrate-bitbucket-jenkins-c6e51103d0fe)

### <a name="customize-ci-pipeline"></a>Personalizar canalización de CI

Hay algunos posibles cambios que puede realizar para adaptar su proyecto:

1. Cambie el nombre del archivo de plantilla a **Jenkinsfile,** ya que es una práctica común y pónsele debajo de la rama de destino, por ejemplo, la **rama de** desarrollo.
1. Cambiar cómo se desencadena el flujo de CI. Usamos de forma predeterminada los desencadenadores de **pollSCM** cuando se inserta un nuevo cambio en la **rama de** desarrollo.
1. Asegúrese de que tiene un script de compilación npm o personalice la forma en que se compila en el código de automatización.
1. Asegúrese de que tiene un script de prueba npm que devuelve cero para el éxito y/o cambie los comandos de prueba.

### <a name="customize-cd-pipeline"></a>Personalizar canalización de CD

Cambie los siguientes pasos para personalizar la canalización de CD:

1. Cambie el nombre del archivo de plantilla a **Jenkinsfile,** ya que es una práctica común y pónsele debajo de la rama de destino, por ejemplo, la **rama** principal.
1. Cómo se desencadena el flujo de CD. Usamos de forma predeterminada los desencadenadores de **pollSCM** cuando se inserta un nuevo cambio en la **rama** principal.
1. Cree credenciales [de canalización de](https://www.jenkins.io/doc/book/using/using-credentials/) Jenkins para contener las credenciales de inicio de sesión de Azure/Microsoft 365 de inicio de sesión. En la tabla siguiente se enumeran todas las credenciales que necesita crear en Jenkins.
1. Cambie los scripts de compilación si es necesario.
1. Quite los scripts de prueba si no tiene pruebas.

> [!Note]
 El paso de aprovisionamiento no se incluye en la plantilla de CD, ya que normalmente se ejecuta solo una vez. Puede ejecutar provision Within Teams Toolkit, CLI de TeamsFx o usar un flujo de trabajo separado. Recuerde confirmar después del aprovisionamiento (los resultados del aprovisionamiento se depositarán dentro de la carpeta) y guardar el contenido del archivo en credenciales de Jenkins para `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` su uso futuro.

### <a name="environment-variables-for-jenkins"></a>Variables de entorno para Jenkins

Siga [using-credentials para](https://www.jenkins.io/doc/book/using/using-credentials/) crear credenciales en Jenkins.

|Nombre|Descripción|
|---|---|
|AZURE_ACCOUNT_NAME|Nombre de cuenta de Azure que se usa para aprovisionar recursos.|
|AZURE_ACCOUNT_PASSWORD|La contraseña de la cuenta de Azure.|
|AZURE_SUBSCRIPTION_ID|Para identificar la suscripción en la que se aprovisionarán los recursos.|
|AZURE_TENANT_ID|Para identificar el espacio empresarial en el que reside la suscripción.|
|Microsoft 365_ACCOUNT_NAME|La cuenta M3icrosoft 365 para crear y publicar la aplicación Teams aplicación.|
|Microsoft 365_ACCOUNT_PASSWORD|La contraseña de la Microsoft 365 cuenta.|
|Microsoft 365_TENANT_ID|Para identificar el espacio empresarial en el que se Teams se creará o publicará la aplicación. Este valor es opcional a menos que tenga una cuenta multiinquilino y desee usar otro inquilino. Obtenga más información [sobre cómo encontrar el identificador Microsoft 365 inquilino](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant).|
> Nota: Consulte Configure [Microsoft 365/Azure Credentials](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret) para asegurarse de que ha deshabilitado multifactor Authentication and Security Defaults para las credenciales usadas en la canalización.

## <a name="get-started-guide-for-other-platforms"></a>Guía de introducción para otras plataformas

Puede seguir los scripts de bash de ejemplo predefinidos enumerados para crear y personalizar canalizaciones de CI o CD en otras plataformas:

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [Scripts de CD](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) Los scripts son bastante sencillos y la mayoría de ellos son CLI multiplataforma, por lo que es fácil transformarlos a otros tipos de script, por ejemplo, PowerShell.

Los scripts se basan en una herramienta de línea de comandos teamsFx multiplataforma [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli). Puede instalarlo con `npm install -g @microsoft/teamsfx-cli` y seguir la documentación [para](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) personalizar los scripts.

> [!Note]
> Para habilitar `@microsoft/teamsfx-cli` la ejecución en modo CI, activa `CI_ENABLED` `export CI_ENABLED=true` . En el modo CI, `@microsoft/teamsfx-cli` es fácil de usar para CI o CD.

Asegúrese de establecer las credenciales de Azure y M365 en las variables de entorno de forma segura. Por ejemplo, si usa GitHub como repositorio de código fuente, puede usar los secretos de [Github](https://docs.github.com/en/actions/reference/encrypted-secrets) para almacenar de forma segura las variables de entorno.

## <a name="publish-teams-app-using-teams-developer-portal"></a>Publicar Teams aplicación con Teams Developer Portal

Si hay algún cambio relacionado con el archivo de manifiesto de Teams aplicación, es posible que quieras volver a publicar la aplicación Teams para actualizar el manifiesto.

Para publicar Teams aplicación manualmente, puedes aprovechar el Portal de [desarrolladores para Teams](https://dev.teams.microsoft.com/home).

**Para publicar la aplicación**

1. Inicie sesión [en Portal de desarrolladores Teams](https://dev.teams.microsoft.com) la cuenta correspondiente.
2. Importe el paquete de la aplicación en zip seleccionando `App -> Import app -> Replace` .
3. Selecciona la aplicación de destino en la lista de aplicaciones y irás a la página de información general.
4. Publicar la aplicación seleccionando `Publish -> Publish to your org`

### <a name="see-also"></a>Consulte también

* [Inicio rápido para GitHub acciones](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Crear la primera canalización de Azure DevOps de datos](/azure/devops/pipelines/create-first-pipeline)
* [Crear la primera canalización de Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
