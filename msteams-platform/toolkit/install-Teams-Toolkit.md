---
title: Instalación del kit de herramientas de Teams
author: zyxiaoyuer
description: En este módulo, obtenga información sobre la instalación del kit de herramientas de Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: c784e5d2242381a919500b16ab922a397bfc5d9e
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2022
ms.locfileid: "67780691"
---
# <a name="install-teams-toolkit"></a>Instalación del kit de herramientas de Teams

Teams Toolkit es una extensión tanto en Visual Studio como en Visual Studio Code. En este documento puede aprender a instalar Teams Toolkit.

::: zone pivot="visual-studio-code"

## <a name="install-teams-toolkit-for-visual-studio-code"></a>Instalar el kit de herramientas de Teams para Visual Studio Code

Antes de empezar con la instalación, debe tener instalados Visual Studio Code y el cliente de Teams.

## <a name="steps-to-install-teams-toolkit"></a>Pasos para instalar Teams Toolkit

Puede instalar Teams Toolkit desde una extensión en Visual Studio Code y desde Visual Studio Code Marketplace. Los pasos siguientes le ayudan a instalar Teams Toolkit:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abra **Visual Studio Code**.
1. Seleccione la vista Extensiones (**Ctrl+Mayús+X** / **⌘⇧-X** o **Ver extensiones >**).

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="instalar":::

1. Escriba **Teams Toolkit** en el cuadro de búsqueda.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="Kit de herramientas":::

1. Haga clic en **Instalar**.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="install toolkit 4.0.0":::

   Después de la instalación correcta del kit de herramientas de Teams en Visual Studio Code, aparece el icono kit de herramientas de Teams en la barra de herramientas de Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Después de la instalación":::

# <a name="marketplace"></a>[Mercado](#tab/marketplace)

1. Abra [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

   Aparece la página siguiente.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-ttk-marketplace.png" alt-text="instalar TTK Marketplace":::

1. Haga clic en **Instalar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Install-ttk.png" alt-text="instalar TTK":::

1. En la ventana emergente, seleccione **Abrir**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-open.png" alt-text="Seleccione la opción abrir.":::

   Aparece la siguiente página de Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ttk-in-vsc.png" alt-text="Selección de TTK en VSC":::

1. Haga clic en **Instalar**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="Seleccione Instalar TTK en VSC":::

   Después de la instalación correcta del kit de herramientas de Teams en Visual Studio Code, aparece el icono kit de herramientas de Teams en la barra de herramientas de Visual Studio Code.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="Después de la instalación":::

---

#### <a name="upgrade-teams-toolkit"></a>Actualización del kit de herramientas de Teams

Teams Toolkit se actualiza a la versión más reciente de forma predeterminada. Los pasos siguientes le ayudan a instalar una versión diferente:

* Seleccione el icono Extensiones :::image type="icon" source="../assets/images/teams-toolkit-v2/extension icon.PNG"::: .
* Escriba **Teams Toolkit**  en el cuadro de búsqueda.
* En Extensión del kit de herramientas de Teams, seleccione :::image type="icon" source="../assets/images/teams-toolkit-v2/setting icon.PNG"::: el icono .
* Seleccione **Instalar otra versión** para actualizar a la versión más reciente del kit de herramientas de Teams.

::: zone-end

::: zone pivot="visual-studio"

## <a name="install-teams-toolkit-for-visual-studio"></a>Instalar el kit de herramientas de Teams para Visual Studio

Antes de empezar con la instalación, debe instalar Instalador de Visual Studio.

Puede descargar la Instalador de Visual Studio más reciente desde la [página de descarga de Visual Studio](https://visualstudio.microsoft.com/vs/preview/).

## <a name="steps-to-install-teams-toolkit"></a>Pasos para instalar Teams Toolkit

Después de abrir la Instalador de Visual Studio, en la ventana emergente Cargas de trabajo:

1. Seleccione la carga de trabajo de **ASP.NET y desarrollo web**.
1. Seleccione las **herramientas de desarrollo de Microsoft Teams** en el panel **Detalles de instalación** .
1. Haga clic en **Instalar**.

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install_1.png" alt-text="Instalación de Visual Studio":::

1. Seleccione **Iniciar** para abrir Visual Studio.

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch_1.png" alt-text="Inicio de Visual Studio":::

   > [!IMPORTANT]
   > Se recomienda descargar Visual Studio 2022, versión 17.3.3, ya que Teams Toolkit for Visual Studio está disponible para disponibilidad general en esta versión. Este artículo está escrito para Visual Studio 2022, versión 17.3.3. Kit de herramientas de Teams versión 17.3.* o posterior.

::: zone-end

## <a name="see-also"></a>Vea también

* [Exploración del kit de herramientas de Teams](explore-Teams-Toolkit.md)
* [Crear una nueva aplicación de Teams con el Kit de herramientas de Teams](create-new-project.md)
* [Preparación para compilar aplicaciones mediante el kit de herramientas de Microsoft Teams](build-environments.md)
* [Aprovisionamiento de recursos en la nube mediante el kit de herramientas de Teams](provision.md)
* [Implementar la aplicación de Teams en la nube](deploy.md)
* [Creación de una nueva aplicación de Teams en Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Aprovisionamiento de recursos en la nube mediante Visual Studio](provision-cloud-resources.md)
* [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy-teams-app.md)
