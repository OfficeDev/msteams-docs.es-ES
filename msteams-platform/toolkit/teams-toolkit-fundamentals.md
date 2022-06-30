---
title: Información general del kit de herramientas de Teams
author: zyxiaoyuer
description: En este módulo, obtenga información sobre el kit de herramientas de Teams, la instalación del kit de herramientas de Teams y el recorrido del usuario del kit de herramientas de Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
ms.openlocfilehash: fe9bbbb7a6d3668f43c31322ad8099bf994051b1
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558334"
---
# <a name="teams-toolkit-overview"></a>Información general del kit de herramientas de Teams

El kit de herramientas de Teams para Visual Studio Code de Microsoft le ayuda a crear e implementar aplicaciones de Teams con identidad integrada, acceso al almacenamiento en la nube, datos de Microsoft Graph y otros servicios en Azure y Microsoft 365 con un enfoque de configuración cero. Para el desarrollo de aplicaciones de Teams, de forma similar al kit de herramientas de Teams para Visual Studio, puede usar la [herramienta CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), que consta del kit de herramientas `teamsfx`.
El kit de herramientas de Teams le permite crear, depurar e implementar su aplicación de Teams directamente desde Visual Studio Code. El desarrollo de aplicaciones con el kit de herramientas tiene las siguientes ventajas:

* Identidad integrada
* Acceso al almacenamiento en la nube
* Datos de Microsoft Graph
* Servicios de Azure y Microsoft 365 con enfoque de configuración cero.

El kit de herramientas de Teams ofrece todas las herramientas necesarias para poder crear una aplicación de Teams en un solo lugar.

## <a name="user-journey-of-teams-toolkit"></a>Recorrido del usuario del kit de herramientas de Teams

El kit de herramientas de Teams automatiza el trabajo manual y proporciona una excelente integración de Teams con los recursos de Azure. En la imagen siguiente se muestra el recorrido del usuario con el kit de herramientas de Teams:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey1.png" alt-text="Recorrido del usuario del kit de herramientas de Teams" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

Los principales hitos de este recorrido son:

1. Se empieza por crear un nuevo proyecto o probar una aplicación de Teams de ejemplo.
1. Se agregan funcionalidades o se edita el archivo de manifiesto según corresponda.
1. Se usa la cuenta de Microsoft 365 para compilar y depurar la aplicación de Teams.
1. Se usa la cuenta de Azure para aprovisionar e implementar la aplicación en la nube.
1. Se publica la aplicación en Teams.

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Instalar el kit de herramientas de Teams para Visual Studio Code

1. Abra **Visual Studio Code.**
1. Seleccione la vista Extensiones (**Ctrl+Mayús+X** / **⌘⇧-X** o **Ver extensiones >**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="instalar":::

1. Escriba **Teams Toolkit** en el cuadro de búsqueda.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="Kit de herramientas":::

1. Haga clic en **Instalar**.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit.png" alt-text="install toolkit 4.0.0":::

> [!TIP]
> Puede instalar el kit de herramientas de Teams desde [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

## <a name="take-a-tour-of-teams-toolkit"></a>Realice un recorrido por el kit de herramientas de Teams

Después de la instalación del kit de herramientas, verá la interfaz de usuario del kit de herramientas de Teams tal como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/Teams-toolkit.png" alt-text="mini funciones":::

Puede seleccionar **Introducción** para explorar el kit de herramientas de Teams o seleccionar **Crear una nueva aplicación de Teams** para crear un proyecto de Teams. Si tiene un proyecto de Teams creado por Teams Toolkit abierto en Visual Studio Code, verá la interfaz de usuario del kit de herramientas de Teams con todas las funcionalidades, como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamstookit1.png" alt-text="Captura de pantalla del kit de herramientas de equipos":::

Vamos a realizar un recorrido por los temas tratados en este documento.

## <a name="accounts"></a>Cuentas

Para desarrollar una aplicación de Teams, se necesita al menos una cuenta de Microsoft 365 con una suscripción válida. Si desea hospedar los recursos de back-end en Azure, también será necesario una cuenta de Azure. Teams Toolkit admite la experiencia integrada para iniciar sesión, aprovisionar e implementar recursos de Azure. Puede [crear una cuenta gratuita de Azure](https://azure.microsoft.com/free/) antes de empezar.

## <a name="environment"></a>Entorno

El kit de herramientas de Teams le ayuda a crear y administrar varios entornos, aprovisionar e implementar artefactos en el entorno de destino para la aplicación de Teams.

### <a name="teamsfx-collaboration"></a>Colaboración de TeamsFx

Permite que los desarrolladores y el propietario del proyecto inviten a otros colaboradores al proyecto TeamsFx para depurar, aprovisionar e implementar el mismo proyecto TeamsFx.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamsfx.png" alt-text="Proyecto teamsfx":::

## <a name="development"></a>Desarrollo

El kit de herramientas de Teams ayuda a crear y personalizar el proyecto de aplicación de Teams, lo que simplifica el trabajo de desarrollo de aplicaciones de Teams.

### <a name="create-a-new-teams-app"></a>Crear una nueva aplicación de Teams

Le ayuda a empezar con el desarrollo de aplicaciones de Teams mediante la creación de un nuevo proyecto de Teams mediante el kit de herramientas de Teams mediante **Crear nuevo proyecto** o **Iniciar desde un ejemplo**.

### <a name="add-features"></a>Agregar características

Le ayuda a agregar de forma incremental funcionalidades adicionales de Teams, como **Tab** o **Bot**, u opcionalmente agregar recursos de Azure, como **Azure SQL Database** o **Azure Key Vault**, que se adapten a sus necesidades de desarrollo a la aplicación actual de Teams. También puede agregar flujos **de trabajo de inicio de sesión único** o **CI/CD** para la aplicación de Teams.

### <a name="edit-manifest-file"></a>Editar archivo de manifiesto

Le ayuda a editar la integración de la aplicación de Teams con el cliente de Teams.

## <a name="deployment"></a>Implementación

Durante o después del desarrollo, asegúrese de aprovisionar, implementar y publicar la aplicación de Teams antes de que sea accesible para los usuarios.

### <a name="provision-in-the-cloud"></a>Aprovisionamiento en la nube

Se integra con Azure Resource Manager que le permite aprovisionar recursos de Azure, que la aplicación necesita para el enfoque de código.

### <a name="deploy-to-the-cloud"></a>Implementar en la nube

 Le ayuda a implementar el código fuente en Azure.

### <a name="publish-to-teams"></a>Publicar en Teams

Después de crear la aplicación, puede distribuirla a un ámbito diferente, por ejemplo, individual, equipo, organización o cualquier usuario. Publicar en Teams le ayuda a publicar la aplicación desarrollada.

#### <a name="teamsfx-cli"></a>TeamsFx CLI

Es una interfaz de línea de comandos basada en texto que acelera el desarrollo de aplicaciones de Teams y habilita un escenario de CI/CD donde se puede integrar la CLI en scripts para la automatización.

#### <a name="teamsfx-sdk"></a>TeamsFx SDK

Ayuda a reducir las tareas de implementación de identidad y acceso a los recursos en la nube a instrucciones de una sola línea con configuración cero.

## <a name="help-and-feedback"></a>Ayuda y comentarios

En esta sección, encontrará la documentación y los recursos que necesita. Puede seleccionar **Notificar problemas en GitHub** en el kit de herramientas de Teams para obtener **Soporte técnico rápido** de un experto en productos. Examine los problemas antes de crear uno nuevo o visite la [etiqueta StackOverflow](https://stackoverflow.com/questions/tagged/teams-toolkit)`teams-toolkit` para enviar comentarios.
<!--  
Let's explore Teams Toolkit features.

| Teams Toolkit Features | Includes | What you can do |
| --- | --- | --- |
| **Accounts** | &nbsp; | &nbsp; |
| &nbsp; | Microsoft 365 account | Use your Microsoft 365 account with a valid E5 subscription for building your app. |
| &nbsp; | Azure account | Use your Azure account for deploying app on Azure. |
| **Environment** | &nbsp; | &nbsp; |
| &nbsp; | local | Deploy your app in the default local environment with local machine environment configurations. |
| &nbsp; | dev | Deploy your app in the default dev environment with remote or cloud environment configurations. You can create more environments, as you need. |
| **Development** | &nbsp; | &nbsp; |
| &nbsp; | Create a new Teams app | Use the toolkit wizard to prepare project scaffolding for app development. |
| &nbsp; | View samples | Select any of Teams Toolkit's 12 sample apps. The toolkit downloads the app code from GitHub, and you can build the sample app. |
| &nbsp; | Add Features | - Add other required Teams capabilities to Teams app during development process. </br> - Add optional cloud resources suitable for your app. |
| &nbsp; | Edit manifest file | Edit the Teams app integration with Teams client. |
| **Deployment** | &nbsp; | &nbsp; |
| &nbsp; | Provision in the cloud | Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager. |
| &nbsp; | Zip Teams metadata package | Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons.  |
| &nbsp; | Deploy to the cloud | Deploy the source code to Azure. |
| &nbsp; | Publish to Teams | Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization. |
| &nbsp; | Developer Portal for Teams | Use Developer Portal to configure and manage your Teams app. |
| **Help and Feedback** | &nbsp; | &nbsp; |
| &nbsp; | Quick start | View the Teams Toolkit Quick start help within Visual Studio Code.  |
| &nbsp; | Tutorial | Select to access different tutorials. |
| &nbsp; | Documentation | Select to access the Microsoft Teams Developer Documentation. |
| &nbsp; | Report issues on GitHub | Select to access GitHub page and raise any issues. |

-->
> [!TIP]
> Examine los problemas ya notificados antes de crear uno nuevo o visite la [etiqueta StackOverflow `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) para enviar comentarios.

## <a name="see-also"></a>Vea también

* [Crear un nuevo proyecto con el kit de herramientas de Teams](create-new-project.md)
* [Preparar cuentas para crear aplicaciones de Teams](accounts.md)
* [Publicar aplicaciones de Teams con el kit de herramientas de Teams](publish.md)
* [usar el kit de herramientas de Teams para aprovisionar recursos en la nube](provision.md)
* [Implementar en la nube](deploy.md)
