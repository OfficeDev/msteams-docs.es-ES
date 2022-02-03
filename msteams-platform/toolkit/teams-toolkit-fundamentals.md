---
title: Teams Toolkit de información general
author: zyxiaoyuer
description: Información general sobre Teams Toolkit, instalación de Teams Toolkit y recorrido por Toolkit características
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 0a048e12167847c1cc34560531cba13da9d74f8f
ms.sourcegitcommit: 58a24422bb04a529b6629a56803ed2efabc17cb1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2022
ms.locfileid: "62323171"
---
# <a name="teams-toolkit-overview"></a>Teams Toolkit de información general

> [!NOTE]
> Actualmente, esta característica solo está disponible en **la versión preliminar del desarrollador** público.

Teams Toolkit permite crear, depurar e implementar la aplicación Teams desde Visual Studio Code. El desarrollo de aplicaciones con el kit de herramientas tiene las ventajas de:

- Identidad integrada
- Acceso al almacenamiento en la nube
- Datos de Microsoft Graph
- Azure y Microsoft 365 con enfoque de configuración cero

Teams Toolkit todas las herramientas necesarias para crear una Teams aplicación en un solo lugar.

Para Teams de aplicaciones, similar a Teams Toolkit para Visual Studio Code, puedes usar la herramienta [CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), que consta de Toolkit `teamsfx`.

## <a name="user-journey-of-teams-toolkit"></a>Recorrido de usuario de Teams Toolkit

Teams Toolkit automatiza el trabajo manual y proporciona una gran integración de Teams recursos de Azure. La siguiente imagen muestra Teams Toolkit de usuario:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey.png" alt-text="Teams Toolkit de usuario" border="true":::

Los principales hitos de este viaje son:

1. Comience creando un nuevo proyecto o probando una aplicación de Teams ejemplo.
1. Agregue funcionalidades o edite el archivo de manifiesto según sea necesario.
1. Usa Microsoft 365 cuenta para compilar y depurar tu Teams aplicación.
1. Usa la cuenta de Azure para aprovisionar e implementar la aplicación en la nube.
1. Publique la aplicación en Teams.

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Instalar Teams Toolkit para Visual Studio Code

1. Abra **Visual Studio Code.**
1. Seleccione la vista Extensiones (**Ctrl+Mayús+X** / **,⇧-X** o **Ver > extensiones**):

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="instalar":::

1. Escriba **Teams Toolkit** en el cuadro de búsqueda:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-2.png" alt-text="Kit de herramientas":::

1. Seleccione **Instalar**:
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install.png" alt-text="kit de herramientas de instalación":::

> [!TIP]
> Puede instalar Teams Toolkit desde [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

## <a name="take-a-tour-of-teams-toolkit"></a>Realizar un recorrido por Teams Toolkit

Después Toolkit instalación, verás la interfaz de usuario Teams Toolkit como se muestra en la siguiente imagen:

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teams toolkit.png" alt-text="mini funciones":::

Puedes seleccionar **Inicio rápido para** explorar el Teams Toolkit o seleccionar Crear una nueva **aplicación** de Teams para crear un Teams proyecto. Puedes ver una lista de todas las Toolkit cuando creas o abres un proyecto existente en Visual Studio Code barra lateral.

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/toolkit functions.png" alt-text="Funciones":::

Vamos a explorar Teams Toolkit características.

| Teams Toolkit características | Incluye... | Qué puede hacer |
| --- | --- | --- |
| **Accounts** | &nbsp; | &nbsp; |
| &nbsp; | Microsoft 365 cuenta | Usa tu Microsoft 365 con una suscripción E5 válida para crear la aplicación. |
| &nbsp; | Cuenta de Azure | Usa tu cuenta de Azure para implementar la aplicación en Azure. |
| **Entorno** | &nbsp; | &nbsp; |
| &nbsp; | local | Implemente la aplicación en el entorno local predeterminado con configuraciones de entorno de máquina local. |
| &nbsp; | dev | Implemente la aplicación en el entorno de desarrollo predeterminado con configuraciones de entorno remoto o en la nube. Puede crear más entornos, según lo necesite. |
| **Desarrollo** | &nbsp; | &nbsp; |
| &nbsp; | Crear una nueva Teams aplicación | Usa el asistente del kit de herramientas para preparar el scaffolding del proyecto para el desarrollo de aplicaciones. |
| &nbsp; | Ver ejemplos | Selecciona cualquiera de Teams Toolkit de las 12 aplicaciones de ejemplo. El kit de herramientas descarga el código de la aplicación GitHub y puedes crear la aplicación de ejemplo. |
| &nbsp; | Agregar funcionalidades | Agregue otras funcionalidades Teams necesarias para Teams aplicación durante el proceso de desarrollo. |
| &nbsp; | Agregar recursos en la nube | Agrega recursos en la nube opcionales adecuados para tu aplicación. |
| &nbsp; | Editar archivo de manifiesto | Edite la Teams de aplicaciones con Teams cliente. |
| **Implementación** | &nbsp; | &nbsp; |
| &nbsp; | Aprovisionar en la nube | Asigne recursos de Azure para la aplicación. Teams Toolkit está integrado con Azure Resource Manager. |
| &nbsp; | Paquete Teams metadatos zip | Crea el paquete de la aplicación que se puede cargar en Teams o portal de desarrolladores. Contiene el manifiesto de la aplicación y los iconos de la aplicación.  |
| &nbsp; | Implementar en la nube | Implemente el código fuente en Azure. |
| &nbsp; | Publicar en Teams | Publique la aplicación desarrollada y distribuyala a ámbitos, como personal, equipo, canal u organización. |
| &nbsp; | Portal para desarrolladores de Teams | Usa Portal de desarrolladores para configurar y administrar tu Teams aplicación. |
| &nbsp; | Guía de CI/CD | Automatice el flujo de trabajo de desarrollo al crear Teams aplicación. |
| **Ayuda y comentarios** | &nbsp; | &nbsp; |
| &nbsp; | Inicio rápido | Vea la ayuda Teams Toolkit inicio rápido dentro de Visual Studio Code.  |
| &nbsp; | Documentación | Seleccione para obtener acceso a la Microsoft Teams de desarrolladores. |
| &nbsp; | Notificar problemas en GitHub | Seleccione para obtener acceso GitHub página y generar cualquier problema. |
|

> [!TIP]
> Examine los problemas existentes antes de crear uno nuevo o visite la [etiqueta StackOverflow `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) para enviar comentarios.

## <a name="see-also"></a>Recursos adicionales

* [Crear un nuevo proyecto mediante Teams Toolkit](create-new-project.md)
* [Preparar cuentas para crear Teams aplicaciones](accounts.md)
* [Publicar aplicaciones de Teams con el kit de herramientas de Teams](publish.md)
* [Usar Teams Toolkit para aprovisionar recursos en la nube](provision.md)
* [Implementar en la nube](deploy.md)