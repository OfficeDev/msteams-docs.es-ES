---
title: Diseñar la aplicación con plantillas de interfaz de usuario
author: heath-hamilton
description: Diseñe la aplicación más rápido con componentes, diseños y patrones de interfaz de usuario estandarizados que se ven normalmente en Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 0cd5c6c4525e340f9aa53a78749211783880225a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566022"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>Diseñar la aplicación Microsoft Teams con plantillas de interfaz de usuario

Diseña tu aplicación Microsoft Teams más rápido con plantillas de interfaz de usuario. Las plantillas son una colección de componentes basados en la interfaz de usuario fluida que funcionan en casos comunes de uso Teams, lo que le da más tiempo para averiguar la mejor experiencia para los usuarios.

## <a name="getting-started-with-tools-and-samples"></a>Introducción a herramientas y muestras

Los siguientes recursos pueden ayudarle a diseñar y desarrollar la aplicación mediante plantillas de interfaz de usuario.

### <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Grabe plantillas de interfaz de usuario para el diseño de la aplicación desde el Kit de interfaz de usuario de Microsoft Teams, que también incluye información amplia sobre el uso, anatomía, accesibilidad y prácticas recomendadas.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams Biblioteca de IU

Vea y pruebe plantillas de interfaz de usuario Teams individuales y componentes relacionados en el explorador.

> [!div class="nextstepaction"]
> [Pruebe la biblioteca de interfaz de usuario (área de juegos)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importe estas plantillas y componentes relacionados directamente en el proyecto de aplicación Teams.

> [!div class="nextstepaction"]
> [Obtener la biblioteca de interfaz de usuario (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Aplicación de ejemplo

Instale una aplicación de ejemplo para ver cómo se ven y se comportan las plantillas de interfaz de usuario en contextos Teams.

> [!div class="nextstepaction"]
> [Obtener la aplicación de ejemplo (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a>Lista

Puede usar una lista para mostrar elementos relacionados en un formato escaneable y permitir a los usuarios realizar acciones en una lista completa o en elementos individuales.

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Mostrar datos
* Acciones contextuales sobre el contenido de la aplicación

## <a name="dashboard"></a>Panel

Un panel muestra diferentes tipos de contenido en una ubicación central (Teams aplicación personal o pestaña). Los usuarios deben poder personalizar al menos parte de lo que ven en un panel.

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Analizar datos
* Métricas del informe
* Organizar diferentes información en un solo lugar

## <a name="form"></a>Form

Los formularios se utilizan para recopilar, validar y enviar la entrada del usuario de forma estructurada. El etiquetado claro y las agrupaciones lógicas de los campos de entrada son fundamentales para una buena experiencia de usuario.

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Iniciar sesión
* Perfiles de usuario
* Configuración
* Recopilación de entradas de usuario

## <a name="sign-in"></a>Iniciar sesión

Puede diseñar flujos de inicio de sesión de aplicaciones para diferentes contextos Teams y proveedores de identidades. En el ejemplo siguiente se incluye el inicio de sesión único (SSO), que se recomienda para la experiencia de autenticación más sencilla.

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="En el ejemplo se muestra un inicio de sesión en la plantilla de interfaz de usuario." border="false":::

### <a name="top-use-case"></a>Estuche de uso superior

* Autenticar usuarios

## <a name="task-board"></a>Mesa de tareas

Un tablero de tareas, a veces llamado tablero kanban o carriles de natación, es una colección de tarjetas que se utilizan a menudo para rastrear el estado de los artículos de trabajo o boletos. También se puede utilizar para ordenar cualquier tipo de contenido en categorías. Puede editar y mover las tarjetas entre columnas.

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del tablero de tareas." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* administración de Project: Asignación de tareas y estado de seguimiento.
* Lluvia de ideas: Adición de ideas en diferentes categorías.
* Ejercicios de clasificación: Organización de cualquier tipo de información en cubos.

## <a name="data-visualization"></a>Visualización de datos

Puede utilizar diferentes tamaños de tarjeta (único, doble y completo) para apilar y organizar visualizaciones de datos en la misma página. Las tarjetas se escalan para ajustarse al diseño de columna y rellenar espacios en blanco.

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Mostrar información compleja
* Crear un panel

## <a name="wizard"></a>Asistente

Un asistente guía a un usuario a través de varias pantallas para completar una tarea (como un proceso de configuración).

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del asistente." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Instalación
* Incorporación
* Experiencias de primer año

## <a name="empty-state"></a>Estado vacío

La plantilla de estado vacía se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error y mucho más. Es altamente flexible: adáptalo para usar uno, unos pocos o todos los componentes del siguiente diseño.

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Iniciar sesión
* Mensajes de bienvenida y experiencias de primera ejecución
* Mensajes de éxito
* Mensajes de error

## <a name="notification-bar"></a>Barra de notificaciones

Una barra de notificaciones es un área dedicada para mostrar un breve e importante mensaje que no requiere que el usuario tome medidas inmediatas. Los colores e iconos de fondo específicos están asociados con tipos específicos de mensajes (véase más adelante).

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="En el ejemplo se muestran plantillas de barra de notificaciones." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Mensajes críticos, errores y advertencias
* Mensajes de éxito
* Mensajes informativos o promocionales

## <a name="left-nav"></a>Nav izquierdo

Utilice el navegador izquierdo para examinar varias páginas dentro de la pestaña Teams. En el ejemplo siguiente, el navegador izquierdo está entre la lista de canales y el contenido de la pestaña.

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="El ejemplo muestra una plantilla de navegación izquierda." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Examine varias páginas dentro de una pestaña de Teams.
* Descompone aplicaciones complejas en varias páginas.

## <a name="breadcrumb"></a>Ruta de navegación

Las rutas de navegación son una ayuda de navegación que transmite la jerarquía de la aplicación. Ayudan a los usuarios a entender cómo la página que están viendo encaja en la experiencia general y ofrecen acceso con un solo clic a niveles más altos en esa jerarquía.

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Comunicar jerarquía
* Navegación

## <a name="toolbar"></a>Barra de herramientas

Una barra de herramientas es un contenedor para agrupar un conjunto de controles.

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Acciones contextuales sobre el contenido de la aplicación
* Filtro contextual y hallazgo
* Navegación y migas de pan

## <a name="stage"></a>Etapa

Stage ofrece una forma para que los usuarios abran una entidad, como una imagen, un archivo o un sitio web, en Teams en lugar de abrirla en otra aplicación o navegador. El principal caso de uso de la etapa es la visualización; la superficie no debe utilizarse para interacciones complejas.

(Nota de implementación: compile el escenario utilizando un [módulo de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)grande .)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="En el ejemplo se muestra una plantilla de etapa." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Abra una entidad en Teams en lugar de otra aplicación o explorador.
* Medios destacados u otro contenido.
