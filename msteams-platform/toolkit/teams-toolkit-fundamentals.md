---
title: Información general del kit de herramientas de Teams
author: zyxiaoyuer
description: En este módulo, obtenga información sobre el kit de herramientas de Teams, la instalación del kit de herramientas de Teams y el recorrido del usuario del kit de herramientas de Teams.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: cb3508bdd22f9d05c48e71b1b90ec4ffbf4c56af
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833166"
---
# <a name="teams-toolkit-overview"></a>Información general del kit de herramientas de Teams

Teams Toolkit facilita la introducción al desarrollo de aplicaciones para Microsoft Teams mediante Visual Studio y Visual Studio Code.

* Comience con una plantilla de proyecto o desde un ejemplo.
* Ahorre tiempo de instalación con el registro y la configuración de aplicaciones automatizados.
* Ejecute y depure en Teams directamente desde herramientas conocidas.
* Valores predeterminados inteligentes para hospedar en Azure mediante la infraestructura como código y Bicep.
* Cree configuraciones únicas como desarrollo, pruebas y producción mediante la característica Entornos.
* Traiga la aplicación a su organización o a la App Store de Teams mediante herramientas de publicación integradas.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Recorrido del usuario del kit de herramientas de Teams" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

## <a name="available-for-visual-studio-and-visual-studio-code"></a>Disponible para Visual Studio y Visual Studio Code

Teams Toolkit está disponible de forma gratuita para Visual Studio Code y admite Visual Studio 2022 Community, Professional y Enterprise. Visite la [documentación de Instalación del kit de herramientas de Teams](./install-Teams-Toolkit.md) para obtener más información sobre la instalación y la instalación.

| Kit de herramientas de Teams | Visual Studio | Visual Studio Code |
| - | ------------- | ------------------ |
| Instalación | Disponible en el Instalador de Visual Studio | Disponible en VS Marketplace |
| Compilación con | C#, .NET, ASP.NET, Blazor | JavaScript, TypeScript, React, SPFx |

## <a name="features"></a>Características

### <a name="project-templates"></a>Plantillas de proyecto

Teams Toolkit reduce la complejidad de empezar a trabajar con plantillas para escenarios comunes de aplicaciones de línea de negocio y valores predeterminados inteligentes para acelerar el tiempo de producción. Si ya está familiarizado con el desarrollo de aplicaciones de Teams, también puede empezar directamente con plantillas centradas en la funcionalidad. Es decir, tab, bot, extensión de mensajería.

::: zone pivot="visual-studio-code"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app.png" alt-text="Crear un menú de aplicación de Teams en VS Code":::
::: zone-end

::: zone pivot="visual-studio"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app-vs.png" alt-text="Crear un menú de aplicación de Teams en VS Code":::
::: zone-end

### <a name="automatic-registration-and-configuration"></a>Registro y configuración automáticos

Ahorre tiempo y deje que el kit de herramientas registre automáticamente la aplicación en el Portal para desarrolladores de Teams y configure opciones como Azure Active Directory automáticamente al ejecutar o depurar la aplicación por primera vez. Inicie sesión con su cuenta de Microsoft 365 para controlar dónde está configurada la aplicación y personalizar el manifiesto de Azure AD incluido cuando necesite más flexibilidad.

::: zone pivot="visual-studio-code"

### <a name="multiple-environments"></a>Varios entornos

Con las características de Entornos, puede crear diferentes agrupaciones de recursos en la nube para que sea más fácil ejecutar y probar la aplicación. Use el entorno de "desarrollo" con su suscripción de Azure o cree uno nuevo con una suscripción diferente para ensayo, prueba y producción.

### <a name="quick-access-to-teams-developer-portal"></a>Acceso rápido al Portal para desarrolladores de Teams

Acceda rápidamente al Portal para desarrolladores de Teams, donde puede configurar, distribuir y administrar la aplicación. Para obtener más información, consulte [Administración de aplicaciones de Teams mediante el Portal para desarrolladores](../concepts/build-and-test/manage-your-apps-in-developer-portal.md).

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="Portal para desarrolladores":::

::: zone-end

::: zone pivot="visual-studio"

#### <a name="teamsfx-net-sdk-reference-docs"></a>Documentación de referencia del SDK de .NET de TeamsFx

* [Espacio de nombres Microsoft.Extensions.DependencyInjection](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Espacio de nombres Microsoft.TeamsFx](/../dotnet/api/Microsoft.TeamsFx)
* [Espacio de nombres Microsoft.TeamsFx.Configuration](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Espacio de nombres Microsoft.TeamsFx.Conversation](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Espacio de nombres Microsoft.TeamsFx.Helper](/../dotnet/api/Microsoft.TeamsFx.Helper)

::: zone-end

## <a name="see-also"></a>Vea también

* [Creación de una nueva aplicación de Teams en Visual Studio](create-new-project.md)
* [Aprovisionamiento de recursos en la nube mediante Visual Studio](provision-cloud-resources.md)
* [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy.md)
