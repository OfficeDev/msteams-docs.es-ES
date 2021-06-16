---
title: Administrar las aplicaciones con el Portal de desarrolladores
description: Aprende a administrar tus aplicaciones mediante el Portal de desarrolladores para Microsoft Teams.
keywords: introducción a los equipos del portal de desarrolladores
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 6dca8723248441c3cf672931295b4b68e02cc24c
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949689"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a>Administrar tus aplicaciones con el Portal de desarrolladores para Microsoft Teams

> [!NOTE]
> El Portal de desarrolladores para Teams está actualmente en [la versión preliminar del desarrollador público.](~/resources/dev-preview/developer-preview-intro.md)

Portal <a href="https://dev.teams.microsoft.com" target="_blank">para desarrolladores para Teams</a> es la herramienta principal para configurar, distribuir y administrar las aplicaciones Microsoft Teams aplicaciones. Con el Portal de desarrolladores, puedes colaborar con compañeros de la aplicación, configurar entornos en tiempo de ejecución y mucho más.

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="Captura de pantalla que muestra la página principal del Portal de desarrolladores para Teams.":::

## <a name="register-an-app"></a>Registrar una aplicación

El Portal de desarrolladores proporciona un par de formas de registrar una Teams aplicación:

* Registrar una aplicación nueva
* Importar un paquete de aplicación existente

> [!NOTE]
> Si creas una aplicación con el [Microsoft Teams Toolkit para Visual Studio Code,](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)puedes administrarla en el Portal de desarrolladores.

## <a name="set-up-an-environment"></a>Configurar un entorno

Puedes configurar entornos y variables globales para ayudar a la transición de la aplicación de tu tiempo de ejecución local a la producción. Las variables globales se usan en todos los entornos.

**Para configurar un entorno**

1. En el Portal de desarrolladores, selecciona la aplicación en la que estás trabajando.
2. Vaya a la **página Entornos** y seleccione **+ Agregar un entorno**.
3. Seleccione **+ Agregar una variable** para crear variables de configuración para su entorno.

**Para usar variables**

Usa los nombres de las variables en lugar de los valores codificados de forma automática para establecer las configuraciones de la aplicación.

1. Escriba `{{` en cualquier campo del Portal de desarrolladores. Aparece un desplegable con todas las variables creadas para el entorno elegido junto con las variables globales.  
1. Antes de descargar el paquete de la aplicación (por ejemplo, al prepararse para publicar en la tienda Teams), selecciona el entorno que quieras usar. Las configuraciones de la aplicación se actualizan automáticamente en función del entorno. 

## <a name="identify-app-owners"></a>Identificar propietarios de aplicaciones

Cada aplicación incluye una **página Propietarios,** donde puedes compartir el registro de la aplicación con compañeros de la organización. El **rol Colaborador** tiene los mismos permisos que el rol **Propietario,** excepto la capacidad de eliminar una aplicación.

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>Configurar las capacidades de la aplicación y otros metadatos importantes

Una Teams es una aplicación web. Al igual que todas las aplicaciones web, su código fuente normalmente se desarrolla en un IDE o editor de código y se hospeda en algún lugar de la nube (como Azure).

Para instalar y representar la aplicación en Teams, debes incluir un conjunto de configuraciones que Teams reconoce. Esto se ha hecho tradicionalmente mediante la creación de un manifiesto de aplicación, un archivo JSON que contiene todos los metadatos Teams debe mostrar el contenido de la aplicación. El Portal de desarrolladores abstrae este proceso e incluye nuevas características y herramientas para ayudarle a tener más éxito.

## <a name="test-your-app-directly-in-teams"></a>Prueba la aplicación directamente en Teams

El Portal de desarrolladores proporciona opciones para probar y depurar la aplicación:

* En la **página Información** general, puedes ver una instantánea de si las configuraciones de la aplicación se validan Teams casos de prueba de la tienda.
* El **botón Vista previa Teams** permite iniciar la aplicación rápidamente en el Teams de depuración.

## <a name="distribute-your-app"></a>Distribuir la aplicación

En el Portal de  desarrolladores, usa el botón Distribuir para descargar un paquete de aplicación, publicar en tu organización o publicar en la Teams aplicación.

Para obtener más información, [consulta distribuir la Teams aplicación](~/concepts/deploy-and-publish/apps-publish-overview.md).

## <a name="analyze-your-apps-usage"></a>Analizar el uso de la aplicación

En la **página Información** general, puedes ver el número total de usuarios activos de la aplicación. Estas métricas están disponibles para las aplicaciones publicadas en la tienda Teams o en el catálogo de aplicaciones de una organización a través del Portal de desarrolladores y están en el ámbito del identificador de la aplicación.

| Métrica | Definición |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *R30 mensual* | Métrica de uso predeterminada. Muestra el recuento de usuarios activos únicos que usaron la aplicación dentro de esa ventana móvil de 30 días en UTC. |
| *Diario* | Muestra el recuento de usuarios activos únicos que usaron la aplicación en un día determinado en UTC. |

El uso mensual y diario se muestra durante los últimos siete, 30 días y 60 días. Debería ver el uso reflejado durante un día determinado en un plazo de 24-48 horas. El uso de nuevas aplicaciones puede tardar entre 3 y 5 días en mostrarse.

## <a name="use-tools-to-create-app-features"></a>Usar herramientas para crear características de la aplicación

El Portal de desarrolladores también incluye herramientas que le ayudarán a crear algunas características clave de Teams aplicaciones. Algunas de estas herramientas incluyen:

* **Scene studio:** [diseñe escenas personalizadas](~/apps-in-teams-meetings/teams-together-mode.md) del Modo conjunto para Teams reuniones.
* **Editor de tarjetas adaptables:** crea y previsualiza tarjetas adaptables para incluir con tus aplicaciones.
* **Plataforma de identidad de Microsoft:** registre sus aplicaciones con Azure Active Directory (Azure AD) para ayudar a los usuarios a iniciar sesión y proporcionar acceso a las API.
