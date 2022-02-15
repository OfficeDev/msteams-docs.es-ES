---
title: Compatibilidad de CI o CD para desarrolladores Teams aplicaciones
author: MuyangAmigo
description: Plantillas CICD
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 1ae613332f7a07ae0d0ae9ed65b75429db64b429
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821580"
---
# <a name="cicd-guide"></a>Guía de CI/CD

TeamsFx ayuda a automatizar el flujo de trabajo de desarrollo al crear Teams aplicación. El documento proporciona herramientas y plantillas para empezar a configurar canalizaciones de CI o CD con GitHub, Azure Devops y Jenkins.

|Herramientas y plantillas|Descripción| 
|---|---|
|[teamsfx-cli-action](https://github.com/OfficeDev/teamsfx-cli-action)|GitHub acción que se integra con la CLI de TeamsFx.|
|[github-ci-template.yml y](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)| GitHub plantillas de CI o CD para Teams aplicación. |
|[jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) y [jenkins-cd-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)|Plantillas de CI o CD de Jenkins para una Teams aplicación.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) y [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Plantillas de script para la automatización fuera de GitHub. |

## <a name="ci-or-cd-workflow-templates-in-github"></a>Plantillas de flujo de trabajo de CI o CD en GitHub

**Para incluir flujos de trabajo de CI o CD para automatizar Teams de desarrollo de aplicaciones en GitHub**:

1. Crear carpeta en `.github/workflows`
1. Copie uno de los siguientes archivos de plantilla:
    * [github-ci-template.yml para flujo](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) de trabajo de CI.
    * [github-cd-template.yml para flujo](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml) de trabajo de CD.
1. Personalice los flujos de trabajo que se ajustan a sus escenarios.

### <a name="customize-ci-workflow"></a>Personalizar flujo de trabajo de CI

Realice los siguientes pasos para adaptar el flujo de trabajo del proyecto:

1. Cambiar el flujo de CI. 
1. Use el script de compilación npm o personalice la forma en que compila el proyecto en el código de automatización.
1. Use el script de prueba npm que devuelve cero para el éxito y cambie los comandos de prueba.

### <a name="customize-cd-workflow"></a>Personalizar flujo de trabajo de CD

Siga estos pasos para personalizar el flujo de trabajo de CD:

1. De forma predeterminada, el flujo de trabajo de CD se desencadena cuando se realizan nuevas confirmaciones en la `main` rama.
1. Cree GitHub [secretos de repositorio por](https://docs.github.com/en/actions/reference/encrypted-secrets) entorno para contener la entidad de seguridad de servicio de Azure y Microsoft 365 de inicio de sesión de la cuenta. Para obtener más información, [vea GitHub Actions](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md).
1. Cambie los scripts de compilación si es necesario.
1. Quite los scripts de prueba según sea necesario.

> [!NOTE]
> El paso de aprovisionamiento no se incluye en la plantilla de CD, ya que normalmente se ejecuta solo una vez. Puede ejecutar la aprovisionamiento en Teams Toolkit, CLI de TeamsFx o mediante un flujo de trabajo independiente. Asegúrese de confirmar después del aprovisionamiento. Los resultados del aprovisionamiento se depositan en carpeta `.fx` .

### <a name="github-secrets"></a>Secretos de Github

En la tabla siguiente se enumeran todos los secretos que necesita para crear un entorno en GitHub:

1. Seleccione **Configuración**.
1. Vaya a **la sección Entornos** .
1. Seleccione **Nuevo entorno**.
1. Escriba un nombre para el entorno. El nombre de entorno predeterminado proporcionado en la plantilla es `test_environment`. 
1. Seleccione **Configurar entorno**.
1. Seleccione **Agregar secreto**.

En la tabla siguiente se enumeran todos los secretos necesarios para crear un entorno:

|Nombre|Descripción|
|---|---|
|`AZURE_SERVICE_PRINCIPAL_NAME`|El nombre principal de servicio de Azure usado para aprovisionar recursos.|
|`AZURE_SERVICE_PRINCIPAL_PASSWORD`|La contraseña de la entidad de servicio de Azure.|
|`AZURE_SUBSCRIPTION_ID`|Para identificar la suscripción en la que se aprovisionarán los recursos.|
|`AZURE_TENANT_ID`|Para identificar el espacio empresarial en el que reside la suscripción.|
|`M365_ACCOUNT_NAME`|Cuenta Microsoft 365 para crear y publicar Teams aplicación.|
|`M365_ACCOUNT_PASSWORD`|La contraseña de la Microsoft 365 cuenta.|
|`M365_TENANT_ID`|Para identificar el espacio empresarial en el que se Teams se creará o publicará la aplicación. Este valor es opcional a menos que tenga una cuenta multiinquilino y desee usar otro inquilino. Para obtener más información, [vea cómo buscar el identificador Microsoft 365 inquilino](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant).|

> [!NOTE]
> Actualmente, la entidad de servicio para Azure se usa en flujos de trabajo de CI/CD. Para obtener más información, consulte [Create Azure service principles](#create-azure-service-principals).

## <a name="set-up-ci-or-cd-pipelines-with-azure-devops"></a>Configurar canalizaciones de CI o CD con Azure DevOps

Puede configurar canalizaciones automatizadas en Azure DevOps y hacer una referencia en los scripts.

Realice los siguientes pasos para empezar:

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

### <a name="set-up-ci-pipeline"></a>Configurar canalización de CI

1. Agregue [scripts de CI](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) Azure DevOps repositorio y realice las personalizaciones necesarias que pueda deducir de los comentarios del archivo de script.
1. Siga los [pasos para crear la canalización Azure DevOps para CI](/azure/devops/pipelines/create-first-pipeline).
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

Los siguientes son los cambios que puede realizar para el script o la definición de flujo de trabajo:

1. Cambiar el flujo de CI. El valor predeterminado es cuando se inserta una nueva confirmación en la `dev` rama.
1. Cambiar la forma de instalar node y npm.
1. Use el script de compilación npm o personalice la forma en que se compila en el código de automatización.
1. Use el script de prueba npm que devuelve cero para el éxito y cambie los comandos de prueba.

### <a name="set-up-cd-pipeline"></a>Configurar canalización de CD

1. Agregue [scripts de CD](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) Azure DevOps repositorio y realice las personalizaciones necesarias que pueda deducir de los comentarios del archivo de script.
1. Cree la canalización Azure DevOps para CD. Para obtener más información, consulte [Create first pipeline](/azure/devops/pipelines/create-first-pipeline). La definición de la canalización se puede hacer referencia a la siguiente definición de ejemplo para la canalización de CI.
1. Agregue las variables necesarias [mediante Definir variables](/azure/devops/pipelines/process/variables) y consévelas como secretos si es necesario.

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
  
- task: Bash@3
  env:
    SP_NAME: $(AZURE_SERVICE_PRINCIPAL_NAME)
    SP_PASSWORD: $(AZURE_SERVICE_PRINCIPAL_PASSWORD)
    TENANT_ID: $(AZURE_TENANT_ID)
    AZURE_SUBSCRIPTION_ID: $(AZURE_SUBSCRIPTION_ID)
    M365_ACCOUNT_NAME: $(M365_ACCOUNT_NAME)
    M365_ACCOUNT_PASSWORD: $(M365_ACCOUNT_PASSWORD)
  inputs:
    filePath: './others-script-cd-template.sh'
```

Los siguientes son los cambios que puede realizar para el script o la definición de flujo de trabajo:

1. Cómo se desencadena el flujo de CD. De forma predeterminada, ocurre cuando se realizan nuevas confirmaciones en la **rama** principal.
1. Cambiar la forma de instalar node y npm.
1. Cambie el nombre del entorno, de forma predeterminada, su **almacenamiento provisional**.
1. Asegúrese de que tiene un script de compilación npm o personalice la forma en que se compila en el código de automatización.
1. Asegúrese de que tiene un script de prueba npm que devuelve cero para el éxito y/o cambie los comandos de prueba.

### <a name="pipeline-variables-for-azure-devops"></a>Variables de canalización para Azure DevOps

Realice los siguientes pasos para crear variables de canalización en Azure DevOps:

1. En la página Edición de canalización, **seleccione Variables** y **seleccione Nueva variable**.
1. Escriba El par Nombre o Valor de la variable.
1. Activa la casilla mantener **este valor en secreto si** es necesario.
1. Seleccione **Aceptar** para crear la variable.

|Nombre|Descripción|
|---|---|
|`AZURE_SERVICE_PRINCIPAL_NAME`|El nombre principal de servicio de Azure usado para aprovisionar recursos.|
|`AZURE_SERVICE_PRINCIPAL_PASSWORD`|La contraseña de la entidad de servicio de Azure.|
|`AZURE_SUBSCRIPTION_ID`|Para identificar la suscripción en la que se aprovisionarán los recursos.|
|`AZURE_TENANT_ID`|Para identificar el espacio empresarial en el que reside la suscripción.|
|`M365_ACCOUNT_NAME`|La Microsoft 365 cuenta para crear y publicar la Teams app.|
|`M365_ACCOUNT_PASSWORD`|La contraseña de la Microsoft 365 cuenta.|
|`M365_TENANT_ID`|Para identificar el espacio empresarial en el que se Teams se creará o publicará la aplicación. Este valor es opcional a menos que tenga una cuenta multiinquilino y desee usar otro inquilino. Obtenga más información [sobre cómo encontrar el identificador Microsoft 365 inquilino](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant).|

## <a name="ci-or-cd-pipeline-templates-in-jenkins"></a>Plantillas de canalización de CI o CD en Jenkins

Para agregar estas plantillas al repositorio, necesita las versiones de [jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) y  [jenkins-cd-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile) que se ubicará en el repositorio por rama.

Además, debe crear canalizaciones de CI o CD en Jenkins que apunten al **jenkinsfile** específico correspondientemente.

Siga los pasos para comprobar cómo conectar Jenkins con diferentes plataformas SCM:

1. [Jenkins con GitHub](https://www.jenkins.io/solutions/github/)
2. [Jenkins con Azure DevOps](https://www.dragonspears.com/blog/ci-cd-with-jenkins-and-azure-devops-services)
3. [Jenkins con GitLab](https://docs.gitlab.com/ee/integration/jenkins.html)
4. [Jenkins con Bitbucket](https://medium.com/ampersand-academy/integrate-bitbucket-jenkins-c6e51103d0fe)

### <a name="customize-ci-pipeline"></a>Personalizar canalización de CI

Estos son algunos de los cambios que puede realizar para adaptar su proyecto:

1. Cambie el nombre del archivo de plantilla **a Jenkinsfile** y colódelo en la rama de destino, por ejemplo, la **rama de** desarrollo.
1. Cambiar cómo se desencadena el flujo de CI. Usamos de forma predeterminada los desencadenadores de **pollSCM** cuando se inserta un nuevo cambio en la **rama de** desarrollo.
1. Asegúrese de que tiene un script de compilación npm o personalice la forma en que se compila en el código de automatización.
1. Asegúrese de que tiene un script de prueba npm que devuelve cero para el éxito y/o cambie los comandos de prueba.

### <a name="customize-cd-pipeline"></a>Personalizar canalización de CD

Realice los pasos siguientes para personalizar la canalización de CD:

1. Cambie el nombre del archivo de plantilla **a Jenkinsfile** y colódelo debajo de la rama de destino, por ejemplo, la **rama** principal.
1. Cambiar el flujo de CD. Usamos de forma predeterminada los desencadenadores de **pollSCM** cuando se inserta un nuevo cambio en la **rama** principal.
1. Cree credenciales [de canalización de](https://www.jenkins.io/doc/book/using/using-credentials/) Jenkins para contener la entidad de servicio de Azure y Microsoft 365 de inicio de sesión de la cuenta.
1. Cambie los scripts de compilación si es necesario.
1. Quite los scripts de prueba si no tiene pruebas.

### <a name="credentials-for-jenkins"></a>Credenciales para Jenkins

Siga [using-credentials para](https://www.jenkins.io/doc/book/using/using-credentials/) crear credenciales en Jenkins.

|Nombre|Descripción|
|---|---|
|`AZURE_SERVICE_PRINCIPAL_NAME`|El nombre principal de servicio de Azure usado para aprovisionar recursos.|
|`AZURE_SERVICE_PRINCIPAL_PASSWORD`|La contraseña de la entidad de servicio de Azure.|
|`AZURE_SUBSCRIPTION_ID`|Para identificar la suscripción en la que se aprovisionarán los recursos.|
|`AZURE_TENANT_ID`|Para identificar el espacio empresarial en el que reside la suscripción.|
|`M365_ACCOUNT_NAME`|La Microsoft 365 cuenta para crear y publicar la Teams app.|
|`M365_ACCOUNT_PASSWORD`|La contraseña de la Microsoft 365 cuenta.|
|`M365_TENANT_ID`|Para identificar el espacio empresarial en el que se crea Teams o se publica la aplicación. El valor es opcional a menos que tenga una cuenta multiinquilino y desee usar otro inquilino. Obtenga más información [sobre cómo encontrar el identificador Microsoft 365 inquilino](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant).|

## <a name="get-started-guide-for-other-platforms"></a>Guía de introducción para otras plataformas

Puede seguir los scripts de bash de ejemplo predefinidos enumerados para crear y personalizar canalizaciones de CI o CD en otras plataformas:

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

Los scripts se basan en una herramienta de línea de comandos teamsFx multiplataforma [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli). Puede instalarlo con y `npm install -g @microsoft/teamsfx-cli` seguir la [documentación para](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) personalizar los scripts.

> [!NOTE]
> * Para habilitar la `@microsoft/teamsfx-cli` ejecución en modo CI, activa `CI_ENABLED` `export CI_ENABLED=true`. En el modo CI, `@microsoft/teamsfx-cli` es fácil de usar para CI o CD.
> * Para habilitar la `@microsoft/teamsfx-cli` ejecución en modo no interactivo, establezca una configuración global con el comando : `teamsfx config set -g interactive false`. En modo no interactivo, `@microsoft/teamsfx-cli` no hará preguntas sobre entradas de forma interactiva.

Asegúrese de establecer las credenciales de Azure y Microsoft365 en las variables de entorno de forma segura. Por ejemplo, si usa GitHub como repositorio de código fuente. Para obtener más información, vea [Secretos de Github](https://docs.github.com/en/actions/reference/encrypted-secrets).

## <a name="create-azure-service-principals"></a>Crear entidades de servicio de Azure

Para aprovisionar e implementar recursos destinados a Azure dentro de CI/CD, debe crear una entidad de servicio de Azure para su uso.

Realice los siguientes pasos para crear entidades de servicio de Azure:
1. Registrar una aplicación Microsoft Azure Active Directory (Azure AD) en un único inquilino.
2. Asigne un rol a la aplicación Azure AD para obtener acceso a la suscripción de Azure y `Contributor` se recomienda el rol. 
3. Cree un nuevo secreto Azure AD aplicación.

> [!TIP]
> Guarde el identificador de inquilino, el identificador de aplicación(AZURE_SERVICE_PRINCIPAL_NAME) y el secreto(AZURE_SERVICE_PRINCIPAL_PASSWORD) para su uso futuro.

Para obtener más información, consulte [Azure service principals guidelines](/azure/active-directory/develop/howto-create-service-principal-portal). Las siguientes son las tres formas de crear la entidad de servicio: 
* [Microsoft Azure portal](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>Publicar Teams aplicación con Teams Developer Portal
Si hay algún cambio relacionado con el archivo de manifiesto de Teams aplicación, es posible que quieras volver a publicar la aplicación Teams para actualizar el manifiesto.

Para publicar Teams aplicación manualmente, puedes aprovechar [el Portal de desarrolladores para Teams](https://dev.teams.microsoft.com/home).

Realice los siguientes pasos para publicar la aplicación:
1. Inicie sesión en [el portal de desarrolladores Teams](https://dev.teams.microsoft.com) la cuenta correspondiente.
2. Importe el paquete de la aplicación en zip seleccionando `App -> Import app -> Replace`.
3. Selecciona la aplicación de destino en la lista de aplicaciones.
4. Publicar la aplicación seleccionando `Publish -> Publish to your org`

### <a name="see-also"></a>Vea también

* [Inicio rápido para GitHub acciones](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Crear la primera canalización de Azure DevOps de datos](/azure/devops/pipelines/create-first-pipeline)
* [Crear la primera canalización de Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Administre sus aplicaciones con el Portal para desarrolladores de Microsoft Teams](/concepts/build-and-test/teams-developer-portal)
