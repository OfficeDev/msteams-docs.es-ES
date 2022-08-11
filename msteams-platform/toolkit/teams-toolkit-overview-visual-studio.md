---
title: Introducción al kit de herramientas de Teams para Visual Studio
author: surbhigupta
description: En este módulo, obtenga información general sobre el kit de herramientas de Teams para Visual Studio.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
ms.openlocfilehash: 0f51d2c44eef3ec09d48581a797c63d501be8644
ms.sourcegitcommit: f192d7685ee3ddf4a55dc9787d56744403c3f8f9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/10/2022
ms.locfileid: "67302454"
---
# <a name="teams-toolkit-overview-for-visual-studio"></a>Introducción al kit de herramientas de Teams para Visual Studio

Teams Toolkit for Visual Studio le ayuda a crear, depurar e implementar aplicaciones de Microsoft Teams. Teams Toolkit for Visual Studio es disponibilidad general en Visual Studio 2022, versión 17.3. El desarrollo de aplicaciones con Teams Toolkit tiene las ventajas de:

* Identidad integrada
* Acceso al almacenamiento en la nube
* Datos de Microsoft Graph
* Servicios de Azure y Microsoft 365 con enfoque de configuración cero

Para el desarrollo de aplicaciones de Teams, también puede usar [la herramienta de la CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), similar a Teams Toolkit for Microsoft Visual Studio code que incluye Toolkit `teamsfx`.

Teams Toolkit ofrece todas las herramientas necesarias para crear una aplicación de Teams en un solo lugar.

> [!NOTE]
> Teams Toolkit no está disponible en otras versiones.

## <a name="user-journey-of-teams-toolkit"></a>Recorrido del usuario del kit de herramientas de Teams

Teams Toolkit automatiza el trabajo manual y le proporciona una excelente integración de los recursos de Teams y Azure. En la imagen siguiente se muestra el recorrido del usuario:

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png" alt-text="Recorrido del usuario del kit de herramientas de Teams":::

Los principales hitos de este recorrido son:

1. Para empezar, cree un nuevo proyecto o pruebe a crear una aplicación de Teams de ejemplo.
1. A continuación, puede editar el código o el archivo de manifiesto según sea necesario.
1. Para compilar y depurar la aplicación de Teams, puede usar su cuenta de Microsoft 365.
1. Para aprovisionar e implementar la aplicación en la nube, puede usar su cuenta de Azure.
1. Por último, puede publicar la aplicación en Teams.

## <a name="install-teams-toolkit-for-visual-studio"></a>Instalar el kit de herramientas de Teams para Visual Studio

Puede descargar el instalador de Visual Studio más reciente desde la [página de descarga de Visual Studio](https://visualstudio.microsoft.com/vs/preview/).

> [!NOTE]
> Primero tendrá que instalar el instalador de Visual Studio antes de instalar Visual Studio.

Después de abrir el instalador de Visual Studio, en la ventana emergente Cargas de trabajo.

1. Seleccione el cuadro ASP.NET y la carga de **trabajo de desarrollo web** .
1. Seleccione el cuadro **Herramientas de desarrollo de Microsoft Teams** en el panel de detalles de la instalación.
1. Haga clic en **Instalar**.

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install1.png" alt-text="Instalación de Visual Studio":::

1. Seleccione **Iniciar** para abrir Visual Studio.

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch.png" alt-text="Inicio de Visual Studio":::

   > [!IMPORTANT]
   > Se recomienda descargar Visual Studio 2022, versión 17.3.0, ya que Teams Toolkit for Visual Studio está disponible en disponibilidad general en esta versión. Este artículo está escrito para Visual Studio 2022, versión 17.3.0. Kit de herramientas de Teams versión 17.3.* o posterior.

## <a name="take-a-tour-of-teams-toolkit"></a>Realice un recorrido por el kit de herramientas de Teams

Después de instalar Teams Toolkit, puede echar un vistazo brevemente a las distintas opciones de menú del kit de herramientas de Teams:

1. Seleccione **Proyecto**.
1. Seleccione **Kit de herramientas de Teams**.
1. Ahora puede acceder a las opciones del **menú kit de herramientas de Teams** .

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu.png" alt-text="Menú de operaciones del kit de herramientas de Teams":::

   También puede acceder al menú del kit de herramientas de Teams desde Explorador de soluciones.

4. Haga clic con el botón derecho en el **proyecto**.
5. Seleccione las opciones **del menú Kit de herramientas de Teams**  >  Toolkit.

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu1.png" alt-text="Operaciones del kit de herramientas de Teams desde Project":::

   > [!NOTE]
   > En este escenario, el nombre del proyecto es **MyTeamsApp1**.

Puede realizar las siguientes funciones en Teams Toolkit for Visual Studio:

|Función  |Descripción  |
|---------|---------|
|Creación de un proyecto de Teams     |Creación de un proyecto de Teams mediante la plantilla de Teams en Visual Studio         |
|Preparación de dependencias de aplicaciones de Teams     |Antes de realizar una depuración local, realice este paso, le ayudará a configurar las dependencias de depuración local y a registrar la aplicación de Teams en la plataforma Teams. Necesita una cuenta de Microsoft 365. Para obtener más información, vea [Depurar la aplicación de Teams localmente mediante Visual Studio](debug-teams-app-visual-studio.md).         |
|Abrir archivo de manifiesto     |Para abrir el archivo de manifiesto de Teams, puede mantener el puntero sobre los parámetros para obtener una vista previa de los valores. Para obtener más información, vea [Editar manifiesto de aplicación de Teams mediante Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md).         |
|Actualizar manifiesto en el Portal para desarrolladores de Teams     |Al actualizar el archivo de manifiesto, solo puede volver a implementar el archivo de manifiesto en Azure sin volver a implementar todo el proyecto. Use este comando para actualizar los cambios al control remoto. Para obtener más información, vea [Editar manifiesto de aplicación de Teams mediante Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md).       |
|Aprovisionamiento en la nube     |Esta opción le ayuda a crear recursos de Azure que hospedan la aplicación de Teams. Para obtener más información, consulte [Aprovisionamiento de recursos en la nube mediante Visual Studio](provision-cloud-resources.md).        |
|Implementación en la nube     |Esta opción le ayuda a copiar el código en los recursos de Azure creados cuando hizo "Aprovisionamiento en la nube". Para obtener más información, consulte [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy-teams-app.md).        |
|Versión preliminar en Teams     |Esta opción inicia el cliente web de Teams y le permite obtener una vista previa de la aplicación teams en su explorador.         |
|Paquete de aplicación zip     |Esta opción genera un paquete de aplicación de Teams en la `Build` carpeta del proyecto. Puede cargar el paquete en el cliente de Teams y ejecutar la aplicación teams.         |

Las siguientes operaciones no se admiten en El kit de herramientas de Teams para Visual Studio todavía en comparación con el kit de herramientas de Teams para Visual Studio Code, sin embargo, están planeadas en el futuro mapa de ruta del producto.

* Agregue otras funcionalidades de Teams a la aplicación de Teams.
* Incorporación de más recursos de Azure a la aplicación de Teams
* Agregue el inicio de sesión único a la aplicación de Teams.
* Agregar conexión de API a la aplicación de Teams.
* Personalización del manifiesto de Azure AD.
* Agregue canalizaciones de CI/CD.
* Administrar varios entornos de nube.
* Colaborar en proyectos de Teams.
* Publicar aplicación de Teams.

### <a name="teamsfx-net-sdk-reference-docs"></a>Documentación de referencia del SDK de .NET de TeamsFx

* [Espacio de nombres Microsoft.Extensions.DependencyInjection](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Espacio de nombres Microsoft.TeamsFx](/../dotnet/api/Microsoft.TeamsFx)
* [Espacio de nombres Microsoft.TeamsFx.Configuration](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Espacio de nombres Microsoft.TeamsFx.Conversation](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Espacio de nombres Microsoft.TeamsFx.Helper](/../dotnet/api/Microsoft.TeamsFx.Helper)

## <a name="see-also"></a>Vea también

* [Creación de una nueva aplicación de Teams en Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Aprovisionamiento de recursos en la nube mediante Visual Studio](provision-cloud-resources.md)
* [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy-teams-app.md)
