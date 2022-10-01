---
title: Instalación del kit de herramientas de Teams
author: zyxiaoyuer
description: En este módulo, obtenga información sobre la instalación del kit de herramientas de Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 03d101df114d3f7564c78c433d01191172e180c9
ms.sourcegitcommit: 3aaccc48906fc6f6fbf79916af5664bf55537250
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2022
ms.locfileid: "68295987"
---
# <a name="install-teams-toolkit"></a>Instalación del kit de herramientas de Teams

En este artículo se describe cómo instalar la extensión kit de herramientas de Teams.

## <a name="prerequisites"></a>Requisitos previos

::: zone pivot="visual-studio-code"

Antes de instalar Teams Toolkit for Visual Studio Code, deberá [descargar e instalar Visual Studio Code](https://code.visualstudio.com/Download).

::: zone-end

::: zone pivot="visual-studio"

Antes de instalar Teams Toolkit for Visual Studio, deberá [descargar e instalar Visual Studio 2022](https://aka.ms/VSDownload) mediante el Instalador de Visual Studio.

::: zone-end

::: zone pivot="visual-studio-code"

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Instalar el kit de herramientas de Teams para Visual Studio Code

Puede instalar Teams Toolkit mediante la ventana Extensiones de Visual Studio Code o instalarlo desde Visual Studio Marketplace.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Inicie **Visual Studio Code**.
1. Abra la ventana Extensiones (**Ctrl+Mayús+X** / **⌘⇧-X** o **Ver extensiones >**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="Captura de pantalla que muestra cómo instalar.":::

1. Escriba **Teams Toolkit** en el cuadro de búsqueda.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="Captura de pantalla que muestra el kit de herramientas.":::

1. Seleccione **Instalar**.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="Captura de pantalla que muestra el kit de herramientas de instalación 4.0.0.":::

   Después de la instalación correcta del kit de herramientas de Teams en Visual Studio Code, aparece un icono del kit de herramientas de Teams en la barra de herramientas de Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Captura de pantalla que muestra después de la vista de instalación.":::

# <a name="marketplace"></a>[Mercado](#tab/marketplace)

1. Vaya a [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) en un explorador web.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-ttk-marketplace.png" alt-text="Captura de pantalla que muestra la instalación de TTK Marketplace.":::

1. Seleccione **Instalar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Install-ttk.png" alt-text="Captura de pantalla que muestra cómo instalar TTK.":::

1. En la ventana emergente, seleccione **Abrir** para iniciar Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-open.png" alt-text="Captura de pantalla que muestra para seleccionar el archivo abierto.":::

   La página de extensión del kit de herramientas de Teams se muestra en Visual Studio Code:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ttk-in-vsc.png" alt-text="Captura de pantalla que muestra cómo seleccionar TTK en VSC.":::

1. Seleccione **Instalar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="Captura de pantalla que muestra cómo seleccionar Instalar TTK en VSC.":::

   Después de la instalación correcta del kit de herramientas de Teams en Visual Studio Code, aparece un icono del kit de herramientas de Teams en la barra de herramientas de Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Captura de pantalla que muestra la vista después de la instalación.":::

---

## <a name="installing-a-different-release-version"></a>Instalación de una versión de versión diferente

De forma predeterminada, Visual Studio Code mantiene el kit de herramientas de Teams actualizado automáticamente. Si desea instalar una versión diferente, siga estos pasos:

* Seleccione el icono Extensiones (:::image type="icon" source="../assets/images/teams-toolkit-v2/extension icon.PNG":::) en la barra de herramientas de Visual Studio Code.
* Escriba **Teams Toolkit**  en el cuadro de búsqueda.
* En la página Kit de herramientas de Teams, seleccione la flecha desplegable situada junto al botón **Desinstalar** .
* Seleccione **Instalar otra versión...** en el menú y elija la versión que se va a instalar.

## <a name="installing-a-pre-release-version"></a>Instalación de una versión preliminar

La extensión Teams Toolkit for Visual Studio Code también está disponible en GitHub. Para descargar versiones preliminares, vaya a la [página Versiones en GitHub](https://github.com/OfficeDev/TeamsFx/releases) y busque descargas de extensiones marcadas como Versión preliminar.

::: zone-end

::: zone pivot="visual-studio"

## <a name="install-teams-toolkit-for-visual-studio"></a>Instalar el kit de herramientas de Teams para Visual Studio

   > [!IMPORTANT]
   > Se recomienda usar La versión 17.3.3 o posterior de Visual Studio 2022 para Teams Toolkit, que es la versión más reciente para corregir varios problemas conocidos en versiones anteriores de Visual Studio.

1. [Descargue el instalador de Visual Studio](https://aka.ms/VSDownload) o ábralo si ya está instalado.
2. Seleccione **Instalar** o **Modificar** si Visual Studio ya está instalado.
3. Seleccione la pestaña **Cargas de trabajo** y, a continuación, seleccione la carga de trabajo **ASP.NET y desarrollo web** .
4. A la derecha, seleccione las **herramientas de desarrollo de Microsoft Teams** en la sección **Opcional** del panel **Detalles** de la instalación.
5. Seleccione **Modificar** o **Instalar** para completar la instalación.

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install_1.png" alt-text="Captura de pantalla que muestra cómo instalar Visual Studio.":::

6. Una vez completada la instalación, seleccione **Iniciar** para abrir Visual Studio.

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch_1.png" alt-text="Captura de pantalla que muestra cómo iniciar Visual Studio.":::

::: zone-end

## <a name="next-steps"></a>Pasos siguientes

Ahora que el kit de herramientas de Teams está instalado, visite [Creación de un nuevo proyecto de Teams](create-new-project.md) para empezar.

## <a name="see-also"></a>Vea también

* [Exploración del kit de herramientas de Teams](explore-Teams-Toolkit.md)
* [Crear una nueva aplicación de Teams con el Kit de herramientas de Teams](create-new-project.md)
* [Preparación para compilar aplicaciones mediante el kit de herramientas de Microsoft Teams](build-environments.md)
* [Aprovisionamiento de recursos en la nube mediante el kit de herramientas de Teams](provision.md)
* [Implementar la aplicación de Teams en la nube](deploy.md)
* [Creación de una nueva aplicación de Teams en Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Aprovisionamiento de recursos en la nube mediante Visual Studio](provision-cloud-resources.md)
* [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy-teams-app.md)
