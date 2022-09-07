---
title: Exploración del kit de herramientas de Teams
author: zyxiaoyuer
description: En este módulo, aprenderá a explorar el kit de herramientas de Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: 0ef95064a1715a64d8f719c54aced7cdc74ecb23
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617351"
---
# <a name="explore-teams-toolkit"></a>Exploración del kit de herramientas de Teams

En este documento puede comprender los diferentes elementos de la interfaz de usuario junto con la descripción y el uso básico en el kit de herramientas de Teams.

## <a name="teams-toolkit-basic-ui-elements"></a>Elementos básicos de la interfaz de usuario del kit de herramientas de Teams

Después de la instalación del kit de herramientas de Teams, verá la interfaz de usuario del kit de herramientas de Teams como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/overview1.png" alt-text="Introducción al kit de herramientas de Teams":::

| Número de serie | Elementos de la interfaz de usuario | Definición |
| --- | --- |
| 1 | **Introducción** | Explore el kit de herramientas de Teams. |
| &nbsp; | **Tutoriales** | Acceda a diferentes tutoriales. |
| &nbsp; | **Documentación** | Acceda a la documentación para desarrolladores de Microsoft Teams. |
| 2 | **Creación de una nueva aplicación de Teams** | Cree una nueva aplicación de Teams según sus necesidades. |
| 3 | **Ver ejemplos** | Cree diferentes tipos de aplicación en función de los ejemplos existentes. |
| 4 | **Abrir carpeta** | Abra la aplicación de Teams existente. |
| 5 | **Nuevo archivo** | Cree un nuevo archivo. |
| &nbsp; | **Abrir archivo** | Abra el archivo existente. |
| &nbsp; | **Abrir carpeta** | Abra la carpeta existente. |
| 6 | **Reciente** | Vea los archivos recientes. |

### <a name="exploring-the-teams-toolkit-task-pane"></a>Exploración del panel de tareas del kit de herramientas de Teams

Puede explorar más elementos de la interfaz de usuario desde el panel de tareas del kit de herramientas de Teams. El panel de tareas solo está visible después de crear una aplicación mediante el kit de herramientas de Teams. El siguiente vídeo le ayuda a conocer el proceso de creación de una nueva aplicación de Teams y, después de este proceso, puede ver el panel de tareas en El kit de herramientas de Teams.

   ![Crear una aplicación de Teams](~/assets/videos/javascript-tab-app1.gif)

Después de crear una nueva aplicación de Teams, puede ver la estructura de directorios de la aplicación en el panel izquierdo y el archivo léame en el panel derecho.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/first-page.png" alt-text="Primera página del kit de herramientas de Teams":::

Vamos a realizar un recorrido por la interfaz de usuario del kit de herramientas de Teams.

 En Visual Studio Code barra de herramientas, los iconos siguientes son relevantes para el kit de herramientas de Teams:

| Icono | Descripción |
| --- | --- |
| **Explorador** :::image type="icon" source="../assets/images/teams-toolkit-v2/file-explorer-icon.PNG":::  | Para ver la estructura de directorios de la aplicación. |
| **Ejecución y depuración** :::image type="icon" source="../assets/images/teams-toolkit-v2/run-debug-icon.PNG":::  | Para iniciar el proceso de depuración local o remota. |
| **Kit de herramientas de Teams** :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: | Para ver el panel de tareas en El kit de herramientas de Teams. |

En el panel de tareas puede ver las secciones siguientes:

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/accounts1.png" alt-text="sección accounts":::
   :::column-end:::
   :::column span="":::

        Para desarrollar una aplicación de Teams, necesita las cuentas siguientes:
        
        * **Iniciar sesión en M365**: use su cuenta de Microsoft 365 con una suscripción E5 válida para compilar la aplicación.

        * **Inicio de sesión en Azure**: use su cuenta de Azure para implementar la aplicación en Azure. Puede [crear una cuenta gratuita de Azure](https://azure.microsoft.com/free/) antes de empezar.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/environment1.png" alt-text="Sección Entorno":::
   :::column-end:::
   :::column span="":::

        Para implementar la aplicación de Teams, necesita los siguientes entornos:
        
       * **local**: implemente la aplicación en el entorno local predeterminado con configuraciones de entorno de máquina local.

        * **desarrollo**: implemente la aplicación en el entorno de desarrollo predeterminado con configuraciones de entorno remoto o en la nube. Podrá crear más entornos, según sea necesario.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/development.png" alt-text="Sección desarrollo":::
   :::column-end:::
   :::column span="":::

        Para crear y personalizar la aplicación de Teams, necesita las siguientes características:
        
       * **Crear una nueva aplicación de Teams**: use el asistente del kit de herramientas para preparar el scaffolding del proyecto para el desarrollo de aplicaciones.

        * **Ver ejemplos**: seleccione cualquiera de las aplicaciones de ejemplo del kit de herramientas de Teams. El kit de herramientas descarga el código de la aplicación de GitHub para que pueda compilar la aplicación de ejemplo.
        
        * **Agregar características**: agregue otras funcionalidades necesarias de Teams a la aplicación Teams durante el proceso de desarrollo y agregue recursos en la nube opcionales adecuados para la aplicación.
       
        * **Editar archivo de manifiesto**: edite la integración de aplicaciones de Teams con el cliente de Teams.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deployment1.png" alt-text="Sección Implementación":::
   :::column-end:::
   :::column span="":::

        Para aprovisionar, implementar y publicar la aplicación de Teams, necesita las siguientes características:
        
        * **Aprovisionamiento en la nube**: asigne recursos de Azure para la aplicación. El kit de herramientas de Teams se integra con Azure Resource Manager.

        * **Paquete de metadatos de Teams zip**: cree el paquete de la aplicación que se puede cargar en Teams o en el Portal para desarrolladores. Contiene el manifiesto de la aplicación y los iconos de la aplicación.
        
        * **Implementación en la nube**: implemente el código fuente en Azure.
       
        * **Publicar en Teams**: publique la aplicación desarrollada y distribúyala a ámbitos, como personal, equipo, canal u organización.
        
        * **Portal para desarrolladores para Teams**: use el Portal para desarrolladores para configurar y administrar la aplicación de Teams. 
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/help-and-feedback1.png" alt-text="Sección ayuda y comentarios":::
   :::column-end:::
   :::column span="":::

        Para obtener más información sobre el kit de herramientas de Teams. necesita la siguiente documentación y recursos.
        
        * **Introducción**: vea la ayuda introducción al kit de herramientas de Teams en Visual Studio Code.

        * **Tutoriales**: seleccione esta opción para acceder a diferentes tutoriales.
        
        * **Documentación**: seleccione esta opción para acceder a la documentación para desarrolladores de Microsoft Teams.
       
        * **Notificar problemas en GitHub**: seleccione esta opción para acceder a la página de GitHub y generar cualquier problema.
   :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vea también

* [Instalación del kit de herramientas de Teams](install-Teams-Toolkit.md)
* [Crear una nueva aplicación de Teams con el Kit de herramientas de Teams](create-new-project.md)
* [Preparación para compilar aplicaciones mediante el kit de herramientas de Microsoft Teams](build-environments.md)
* [Aprovisionamiento de recursos en la nube mediante el kit de herramientas de Teams](provision.md)

<!--  
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ui-elements.png" alt-text="UI Elements":::

|Section|Features|Details
|---------|---------|--------|
| **1. ACCOUNTS** | &nbsp; | &nbsp; |
| &nbsp; |Microsoft 365 account|  Use your Microsoft 365 account with a valid E5 subscription for building your app.|
| &nbsp; | Azure Account |  Use your Azure account for deploying app on Azure. You can [create a free Azure account](https://azure.microsoft.com/free/) before you start.|
|**2.ENVIRONMENT** |  &nbsp; | &nbsp;|
| &nbsp; |Local |Deploy your app in the default local environment with local machine environment configurations.|
| &nbsp; | Dev |Deploy your app in the default dev environment with remote or cloud environment configurations. You can create more environments, as you need.|
| **3.DEVELOPMENT** | &nbsp; | &nbsp; |
| &nbsp; | Create a new Teams app | Teams Toolkit helps you to create and customize your Teams app project that makes the Teams app development work simpler. Create a new Teams app helps you to start with Teams app development by creating new Teams project using Teams Toolkit either by using **Create new project**|
| &nbsp; | View Samples | Select any of Teams Toolkit's sample apps. The toolkit downloads the app code from GitHub, and you can build the sample app.|
| &nbsp; | Add Features | It helps you to add additional Teams capabilities such as **Tab** or **Bot** or **Message extension** or **Command bot** or **Notification bot**, or **SSO enabled tab** optionally add Azure resources such as **Azure SQL Database** or **Azure Key Vault**, or **Azure function** or **Azure API Management** which fits your development needs to your current Teams app. You can also add **API connection** or **Single Sign-on** or **CI/CD workflows** for your Teams app.
| &nbsp; | Edit Manifest file | It helps you customize manifest file based on the app requirements |
| **4.DEPLOYMENT** | &nbsp; | &nbsp; |
| &nbsp;| Provision in the cloud | Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager.|
| &nbsp; | Zip Teams metadata package| Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons. |
| &nbsp; | Deploy to the cloud| Deploy the source code to Azure.|
| &nbsp; | Publish to Teams| Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization.|
| &nbsp; | Developer Portal for Teams| It is the primary tool for configuring, distributing, and managing your Microsoft Teams apps. You can collaborate with colleagues on your app, set up runtime environments, and much more. |
| **5.HELP AND FEEDBACK** | &nbsp; | &nbsp; |
| &nbsp; | Get Started |  View the Teams Toolkit Get started help within Visual Studio Code.|
| &nbsp; | Tutorials| Select to access different tutorials.|
| &nbsp; | Documentation| Select to access the Microsoft Teams Developer Documentation.|
| &nbsp; | Report issues on GitHub| It helps to get **Quick support** from product expert. Browse the existing issues before you create a new one, or visit [StackOverflow tag `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) to submit feedback.|
| **6.Explorer** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | It helps to view the directory structure of your app.|
| **7.Run and Debug** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | To start the local or remote debug process.|
-->
