---
title: Información general del kit de herramientas de Teams
author: zyxiaoyuer
description: En este módulo, obtenga información sobre el kit de herramientas de Teams, la instalación del kit de herramientas de Teams y el recorrido del usuario del kit de herramientas de Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: ca65a34796886ff8eb6a0c13aaa11af319739dc8
ms.sourcegitcommit: 1db4429f34da213aa749e483a4ceb83c14b07de3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2022
ms.locfileid: "68158266"
---
# <a name="teams-toolkit-overview"></a>Información general del kit de herramientas de Teams

Teams Toolkit es una característica de funcionalidad que permite realizar varias funciones tanto en Microsoft Visual Studio Code como en Visual Studio. Con la ayuda del kit de herramientas de Teams, puede automatizar el proceso desde la creación hasta la implementación y personalización de la aplicación. Las distintas características y ventajas del kit de herramientas de Teams se describen en la documentación correspondiente para los entornos que elija.

::: zone pivot="visual-studio-code"

## <a name="teams-toolkit-overview-for--visual-studio-code"></a>Introducción al kit de herramientas de Teams para Visual Studio Code

Teams Toolkit le permite crear, depurar e implementar la aplicación de Teams directamente desde Visual Studio Code. El desarrollo de aplicaciones con el kit de herramientas tiene las siguientes ventajas:

* Identidad integrada
* Acceso al almacenamiento en la nube
* Datos de Microsoft Graph
* Servicios de Azure y Microsoft 365 con enfoque de configuración cero.

Para el desarrollo de aplicaciones de Teams, de forma similar al kit de herramientas de Teams para Visual Studio, puede usar la [herramienta CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), que consta del kit de herramientas `teamsfx`.

## <a name="user-journey-of-teams-toolkit"></a>Recorrido del usuario del kit de herramientas de Teams

El kit de herramientas de Teams automatiza el trabajo manual y proporciona una excelente integración de Teams con los recursos de Azure. En la imagen siguiente se muestra el recorrido del usuario con el kit de herramientas de Teams:

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Recorrido del usuario del kit de herramientas de Teams" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

Los principales hitos de este recorrido son:

1. Se empieza por crear un nuevo proyecto o probar una aplicación de Teams de ejemplo.
1. Se agregan funcionalidades o se edita el archivo de manifiesto según corresponda.
1. Se usa la cuenta de Microsoft 365 para compilar y depurar la aplicación de Teams.
1. Se usa la cuenta de Azure para aprovisionar e implementar la aplicación en la nube.
1. Se publica la aplicación en Teams.

La tabla siguiente le ayuda a obtener información general del kit de herramientas de Teams en Visual Studio Code:

| Proceso | Descripción |
| ---- | ---- |
| Instalación del kit de herramientas de Teams | Puede instalar Teams Toolkit de dos maneras: <br> - Uso de Visual Studio Code <br> - Uso de Visual Studio Code Marketplace|
| Compatibilidad con entornos de compilación | Tiene dos tipos diferentes de entorno: <br> - Javascript o Typescript <br> - SPFx |
| Compatibilidad con los tipos de aplicación y la función de Azure | Hay dos tipos diferentes de aplicaciones: <br> - Aplicación basada en funcionalidad, como pestaña, bot, extensión de mensaje  <br> - Aplicación de Teams basada en escenarios, como bot de notificación, bot de comandos y pestaña personal habilitada para SSO |
| Desarrollo de la aplicación de Teams | Contiene: <br> - Agregar y administrar el entorno <br> - Creación de una aplicación de varias funcionalidades <br> - Creación de recursos en la nube basados en funcionalidades <br> - Integración de api de terceros <br> - Personalización del archivo de manifiesto <br> - SDK de TeamsFx |
| Depurar la aplicación de Teams | Contiene: <br> : depuración local de la aplicación de Teams <br> - Depuración del proceso en segundo plano|
| Hospedar la aplicación de Teams | Contiene: <br> - Aprovisionamiento de recursos en la nube <br> - Implementación en la nube|
| Prueba de la aplicación de Teams | Contiene: <br> - Integración y collabrate <br> - Paquete de metadatos zip de Teams <br> - Instalación local y prueba de la aplicación en el entorno de Teams <br> - Probar el comportamiento de la aplicación en un entorno diferente|
| Publicar la aplicación de Teams | Contiene: <br> - Publicación de la aplicación <br> - Administración de la aprobación del administrador <br> - Publicar para almacenar <br> - Integración con el Portal para desarrolladores |

### <a name="entities-integrated-with-teams-toolkit"></a>Entidades integradas con Teams Toolkit
 
Teams Toolkit es una extensión de Visual Studio Code. Se integra con las siguientes entidades dentro del kit de herramientas de Teams, como Azure AD y Microsoft 365, el Portal para desarrolladores y Microsoft Graph. Todas las entidades se integran en Teams Toolkit y ayudan a los usuarios a crear una aplicación.

| Entidades | Descripción |
| ---- | ---- |
| Azure AD  | Azure Active Directory (Azure AD) es un servicio de administración de identidades y acceso basado en la nube. Este servicio ayuda a los empleados a acceder a recursos externos, como Microsoft 365, el Azure Portal y miles de otras aplicaciones SaaS. |
| Microsoft 365  | Cuenta de desarrollador de Teams al desarrollar una aplicación.|
| Portal para desarrolladores | El portal para desarrolladores para Teams es la herramienta principal para configurar, distribuir y administrar las aplicaciones de Microsoft Teams. Con el portal para desarrolladores, puede colaborar con compañeros en la aplicación, configurar entornos en tiempo de ejecución y mucho más. |
| Microsoft Graph | Microsoft Graph es la puerta de enlace a datos y la inteligencia de Microsoft 365. Le proporciona un modelo de programación unificado que puede usar para acceder a la gran cantidad de datos en Microsoft 365, Windows y Enterprise Mobility + Security. |

El kit de herramientas de Teams ofrece todas las herramientas necesarias para poder crear una aplicación de Teams en un solo lugar.

## <a name="manage-your-apps-using-developer-portal"></a>Administración de aplicaciones mediante el Portal para desarrolladores

A medida que Teams Toolkit se integra con el Portal para desarrolladores, puede configurar, distribuir y administrar la aplicación mediante [el Portal para desarrolladores para Teams](../concepts/build-and-test/teams-developer-portal.md) en IMPLEMENTACIÓN después de crear una aplicación. Para obtener más información, consulte [Administración de aplicaciones de Teams mediante el Portal para desarrolladores](../concepts/build-and-test/manage-your-apps-in-developer-portal.md).

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="Portal para desarrolladores":::

::: zone-end

::: zone pivot="visual-studio"

## <a name="teams-toolkit-overview-for-visual-studio"></a>Introducción al kit de herramientas de Teams para Visual Studio

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

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png" alt-text="Recorrido del usuario del kit de herramientas de Teams" lightbox="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png":::

Los principales hitos de este recorrido son:

1. Para empezar, cree un nuevo proyecto o pruebe a crear una aplicación de Teams de ejemplo.
1. A continuación, puede editar el código o el archivo de manifiesto según sea necesario.
1. Para compilar y depurar la aplicación de Teams, puede usar su cuenta de Microsoft 365.
1. Para aprovisionar e implementar la aplicación en la nube, puede usar su cuenta de Azure.
1. Por último, puede publicar la aplicación en Teams.

Las siguientes operaciones no se admiten en Teams Toolkit for Visual Studio todavía en comparación con Teams Toolkit for Microsoft Visual Studio Code, pero están planeadas en el futuro mapa de ruta del producto.

* Agregue otras funcionalidades de Teams a la aplicación de Teams.
* Incorporación de más recursos de Azure a la aplicación de Teams
* Agregue el inicio de sesión único (SSO) a la aplicación de Teams.
* Agregar conexión de API a la aplicación de Teams.
* Personalice el manifiesto de Microsoft Azure Active Directory (Azure AD).
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

::: zone-end

## <a name="see-also"></a>Consulte también

* [Creación de una nueva aplicación de Teams en Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Aprovisionamiento de recursos en la nube mediante Visual Studio](provision-cloud-resources.md)
* [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy-teams-app.md)

