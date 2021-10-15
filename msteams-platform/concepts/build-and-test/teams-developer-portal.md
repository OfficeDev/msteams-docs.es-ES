---
title: Administrar las aplicaciones con el Portal de desarrolladores
description: Aprende a administrar tus aplicaciones mediante el Portal de desarrolladores para Microsoft Teams.
keywords: introducción a los equipos del portal de desarrolladores
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 41aade2eaedee2095e60288a7e4021897bb1a3fa
ms.sourcegitcommit: ece03efbb0e9d1fea5bd01c9c05a2bc232c1a1c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2021
ms.locfileid: "60378915"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a>Administrar tus aplicaciones con el Portal de desarrolladores para Microsoft Teams

Portal <a href="https://dev.teams.microsoft.com" target="_blank">para desarrolladores para Teams</a> es la herramienta principal para configurar, distribuir y administrar las aplicaciones Microsoft Teams aplicaciones. Con el Portal de desarrolladores, puedes colaborar con compañeros de la aplicación, configurar entornos en tiempo de ejecución y mucho más.

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="Captura de pantalla que muestra la página principal del Portal de desarrolladores para Teams.":::

## <a name="register-an-app"></a>Registrar una aplicación

Puedes registrar la aplicación Teams en el Portal de desarrolladores de las siguientes maneras:

* Registrar una nueva aplicación
* Importar un paquete de aplicación existente

> [!NOTE]
> Si creas una aplicación con el [Microsoft Teams Toolkit para Visual Studio Code,](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)puedes administrarla en el Portal de desarrolladores.

## <a name="set-up-an-environment"></a>Configurar un entorno

Puedes configurar entornos y variables globales para ayudar a la transición de la aplicación desde el tiempo de ejecución local a la producción. Las variables globales se usan en todos los entornos.

**Para configurar un entorno**

1. En el Portal de desarrolladores, selecciona la aplicación en la que estás trabajando.
2. Vaya a **Entornos** y seleccione **+ Agregar un entorno**.
3. Seleccione **+ Agregar una variable** para crear variables de configuración para su entorno.

**Para usar variables**

Usa los nombres de las variables en lugar de los valores codificados de forma automática para establecer las configuraciones de la aplicación.

1. Escriba `{{` en cualquier campo del Portal de desarrolladores. Aparece un desplegable con todas las variables creadas para el entorno elegido junto con las variables globales.  
1. Antes de descargar el paquete de la aplicación (por ejemplo, al prepararse para publicar en la tienda Teams), selecciona el entorno que quieras usar. Las configuraciones de la aplicación se actualizan automáticamente en función del entorno. 

## <a name="identify-app-owners"></a>Identificar propietarios de aplicaciones

Cada aplicación incluye **Propietarios,** donde puedes compartir el registro de la aplicación con compañeros de la organización. El **rol Colaborador** tiene los mismos permisos que el rol **Propietario,** excepto la capacidad de eliminar una aplicación.

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>Configurar las capacidades de la aplicación y otros metadatos importantes

Una Teams es una aplicación web. Al igual que todas las aplicaciones web, su código fuente normalmente se desarrolla en un IDE o editor de código y se hospeda en algún lugar de la nube (como Azure).

Para instalar y representar la aplicación en Teams, debes incluir un conjunto de configuraciones que Teams reconoce. Esto se ha hecho tradicionalmente mediante la creación de un manifiesto de aplicación, un archivo JSON que contiene todos los metadatos que Teams para mostrar el contenido de la aplicación. El Portal de desarrolladores abstrae este proceso e incluye nuevas características y herramientas para ayudarle a tener más éxito.

### <a name="basic-app-configuration"></a>Configuración básica de la aplicación 

**Información básica de la aplicación:** Los usuarios ven en la página de detalles de la aplicación en Teams, como id. de aplicación, nombres de aplicaciones, descripciones, información para desarrolladores, versión, direcciones URL de la aplicación e id. de red de partners de Microsoft.

**Personal de marca:** Las aplicaciones requieren el color y el icono de esquema en formato PNG. Para publicar la aplicación en la Teams, los iconos deben cumplir requisitos de tamaño específicos.

**Características:** Teams características que puedes incluir en la aplicación. Puedes agregar una o más características según los casos de uso de la aplicación.

**Permisos:** Especifica a qué deben dar su consentimiento los usuarios al usar la aplicación.

**Inicio de sesión único:** Configura la aplicación para autenticar usuarios con inicio de sesión único (SSO).

**Dominios:** Enumerar todos los dominios a los que debe navegar la aplicación. Use caracteres comodín para incluir varios subdominios. Por ejemplo, `*.example.com`.

### <a name="advanced-app-configuration"></a>Configuración avanzada de la aplicación

**Contenido de la aplicación:** Configura las características opcionales, como el indicador de carga y el modo de pantalla completa para la aplicación.

**Personalización de la aplicación:** Selecciona las propiedades que Teams los administradores pueden personalizar acerca de la aplicación.

**Configuración del primer usuario:** Características para aplicaciones de primera persona que se extienden más allá de la funcionalidad pública.

### <a name="distribute-your-app"></a>Distribuir la aplicación

**Paquete de la aplicación:** El paquete de la aplicación describe la configuración de la aplicación, las capacidades, los recursos necesarios y otros atributos importantes. Por ejemplo, el esquema de manifiesto.

**Vuelos:** Controlar quién obtiene las actualizaciones de la aplicación. Por ejemplo, puede publicar una actualización a los empleados de Microsoft para identificar y corregir errores antes de publicarla al público.

**Publicar en su organización (Microsoft):** Haz que la aplicación esté disponible para los usuarios de tu organización. Una vez aprobado por el administrador de TI, la aplicación aparecerá en Teams en Aplicaciones > integradas para tu organización.

**Publicar en el Teams:** La herramienta de validación de aplicaciones comprueba el paquete de la aplicación en los casos de prueba que Usa Microsoft al revisar la aplicación. Resuelva errores o advertencias y lea la lista de comprobación antes de enviarla.

## <a name="test-your-app-directly-in-teams"></a>Prueba la aplicación directamente en Teams

El Portal de desarrolladores proporciona opciones para probar y depurar la aplicación:

* En **Overview**, puedes ver una instantánea de si las configuraciones de la aplicación se validan en Teams casos de prueba de la tienda.
* **La vista previa en Teams** permite iniciar la aplicación rápidamente en el Teams de depuración.

## <a name="distribute-your-app"></a>Distribuir la aplicación

Desde el Portal de desarrolladores, usa **Distribuir** para descargar un paquete de aplicación, publicar en tu organización o publicar en la Teams aplicación.

Para obtener más información, [consulta distribuir la Teams aplicación](~/concepts/deploy-and-publish/apps-publish-overview.md).

## <a name="analyze-your-apps-usage"></a>Analizar el uso de la aplicación

En **Información** general, puedes ver el número total de usuarios activos de la aplicación. Estas métricas están disponibles para las aplicaciones publicadas en la tienda Teams o en el catálogo de aplicaciones de una organización a través del Portal de desarrolladores y están en el ámbito del identificador de la aplicación.

| Métrica | Definición |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *R30 mensual* | Métrica de uso predeterminada. Muestra el recuento de usuarios activos únicos que han usado la aplicación dentro de esa ventana de 30 días en UTC. |
| *Diario* | Muestra el recuento de usuarios activos únicos que han usado la aplicación en un día determinado en UTC. |

El uso mensual y diario se muestra durante los últimos siete días, 30 días y 60 días. Debería ver el uso reflejado durante un día determinado en un plazo de 24-48 horas. El uso de nuevas aplicaciones puede tardar entre 3 y 5 días en mostrarse.

## <a name="use-tools-to-create-app-features"></a>Usar herramientas para crear características de la aplicación

El Portal de desarrolladores también incluye herramientas que le ayudarán a crear algunas características clave de Teams aplicaciones. Algunas de estas herramientas incluyen:

* **Scene studio:** [diseñe escenas personalizadas](~/apps-in-teams-meetings/teams-together-mode.md) del Modo conjunto para Teams reuniones.
* **Editor de tarjetas adaptables:** crea y previsualiza tarjetas adaptables para incluir con tus aplicaciones.
* **Plataforma de identidad de Microsoft:** registre sus aplicaciones con Azure Active Directory (Azure AD) para ayudar a los usuarios a iniciar sesión y proporcionar acceso a las API.

## <a name="see-also"></a>Vea también

[Incluir una oferta SaaS con tu Microsoft Teams aplicación](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
