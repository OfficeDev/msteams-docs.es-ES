---
title: Administre sus aplicaciones con el portal para desarrolladores de Microsoft Teams
description: Obtenga información sobre cómo configurar, distribuir y administrar las aplicaciones mediante el portal para desarrolladores para Microsoft Teams.
keywords: introducción a los equipos del portal para desarrolladores
ms.localizationpriority: high
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: f55ecd7e44760a353a6058e004ea3cf6cdb769b2
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111797"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a>Administre sus aplicaciones con el Portal para desarrolladores de Microsoft Teams

El <a href="https://dev.teams.microsoft.com" target="_blank">portal para desarrolladores para Teams</a> es la herramienta principal para configurar, distribuir y administrar las aplicaciones de Microsoft Teams. Con el portal para desarrolladores, puede colaborar con compañeros en la aplicación, configurar entornos en tiempo de ejecución y mucho más.

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="Captura de pantalla que muestra la página principal del portal para desarrolladores para Teams.":::

> [!NOTE]
>
> * Actualmente, el portal para desarrolladores no está disponible para inquilinos de Government Community Cloud (GCC), GCC-High o el Departamento de Defensa (DOD).
> * Sin embargo, puede usar un inquilino normal para compilar una aplicación en el portal para desarrolladores, descargar la aplicación y cargar la aplicación mediante [Microsoft Graph](/graph/api/teamsapp-publish?view=graph-rest-1.0&tabs=http&preserve-view=true) en una nube nacional. Para obtener más información, consulte [Implementaciones nacionales de nube](/graph/deployments).

## <a name="register-an-app"></a>Registrar una aplicación

El portal para desarrolladores proporciona un par de maneras de registrar una aplicación Teams:

* Registro de una nueva aplicación
* Importación de un paquete de aplicación existente

> [!NOTE]
> Si crea una aplicación con el [Kit de herramientas de Microsoft Teams para Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension), puede administrarla en el portal para desarrolladores.

## <a name="set-up-an-environment"></a>Configurar el entorno de desarrollo

Puede configurar entornos y variables globales para ayudar a realizar la transición de la aplicación del entorno de ejecución local a producción. Las variables globales se usan en todos los entornos.

Para configurar un entorno:

1. En el portal para desarrolladores, seleccione la aplicación en la que está trabajando.
2. Vaya a la página **Entornos** y seleccione **+ Agregar un entorno**.
3. Seleccione **+ Agregar una variable** para crear variables de configuración para el entorno.

Para usar variables:

Use los nombres de variable en lugar de los valores codificados de forma rígida para establecer las configuraciones de la aplicación.

1. Escriba `{{` en cualquier campo en el portal para desarrolladores. Aparece una lista desplegable con todas las variables que ha creado para el entorno elegido junto con las variables globales.  
1. Antes de descargar el paquete de la aplicación (por ejemplo, al prepararse para publicar en la tienda de Teams), seleccione el entorno que desea usar. Las configuraciones de la aplicación se actualizan automáticamente en función del entorno.

## <a name="identify-app-owners"></a>Identificación de propietarios de aplicaciones

Cada aplicación incluye una página **Propietarios**, donde puede compartir el registro de la aplicación con compañeros de su organización. El rol **Colaborador** tiene los mismos permisos que el rol **Propietario**, excepto la capacidad de eliminar una aplicación.

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>Configuración de las funcionalidades de la aplicación y otros metadatos importantes

Una aplicación Teams es una aplicación web. Al igual que todas las aplicaciones web, su código fuente se desarrolla normalmente en un IDE o editor de código y se hospeda en algún lugar de la nube (como Azure).

Para instalar y representar la aplicación en Teams, debe incluir un conjunto de configuraciones que Teams reconozca. Esto se ha hecho tradicionalmente creando un manifiesto de aplicación, un archivo JSON que contiene todos los metadatos que Teams necesita para mostrar el contenido de la aplicación. El portal para desarrolladores abstrae este proceso e incluye nuevas características y herramientas que le ayudarán a tener más éxito.

## <a name="test-your-app-directly-in-teams"></a>Pruebe la aplicación directamente en Teams

El portal para desarrolladores proporciona opciones para probar y depurar la aplicación:

* En la página **Información general**, puede ver en una instantánea si las configuraciones de la aplicación se validan en los casos de prueba de Teams tienda.
* El botón **Vista previa en Teams** permite iniciar la aplicación rápidamente en el cliente de Teams para la depuración.

## <a name="distribute-your-app"></a>Distribuir la aplicación

En el portal para desarrolladores, use el botón **Distribuir** para descargar un paquete de aplicación, publicar en su organización o publicar en el almacén de Teams.

Para más información, consulte [Cargar la aplicación en Microsoft Teams](~/concepts/deploy-and-publish/apps-publish-overview.md).

## <a name="use-tools-to-create-app-features"></a>Uso de herramientas para crear características de la aplicación

El portal para desarrolladores también incluye herramientas que le ayudarán a crear algunas características clave de las aplicaciones de Teams. Entre estas herramientas se incluyen las siguientes:

* **Estudio de escenas**: diseñe [escenas personalizadas del modo junto](~/apps-in-teams-meetings/teams-together-mode.md) para reuniones de Teams.
* **Editor de tarjetas adaptables**: cree y obtenga una vista previa de tarjetas adaptables para incluirlas con las aplicaciones.
* **Administración de la plataforma de identidad de Microsoft**: registre las aplicaciones con Azure Active Directory para ayudar a los usuarios a iniciar sesión y proporcionar acceso a las API.

## <a name="see-also"></a>Vea también

[Incluir una oferta de SaaS con la aplicación de Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
