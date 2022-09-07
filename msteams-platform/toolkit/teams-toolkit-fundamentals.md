---
title: Información general del kit de herramientas de Teams
author: zyxiaoyuer
description: En este módulo, obtenga información sobre el kit de herramientas de Teams, la instalación del kit de herramientas de Teams y el recorrido del usuario del kit de herramientas de Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
ms.openlocfilehash: b614c73a9d15b058dcd01bb26b15bf35bd3030ce
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616898"
---
# <a name="teams-toolkit-overview"></a>Información general del kit de herramientas de Teams

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

## <a name="see-also"></a>Vea también

* [Creación de un nuevo proyecto de Teams](create-new-project.md)
* [Instalación del kit de herramientas de Teams](install-Teams-Toolkit.md)
* [Exploración del kit de herramientas de Teams](explore-Teams-Toolkit.md)
* [Preparación para compilar aplicaciones mediante el kit de herramientas de Microsoft Teams](build-environments.md)
