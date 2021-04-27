---
title: Diseño de la aplicación con plantillas de interfaz de usuario
author: heath-hamilton
description: Diseña tu aplicación más rápido con componentes de interfaz de usuario estandarizados, diseños y patrones que se ven habitualmente en Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: d627ce3b29ffa071d0d7e238c572c7cb69fa4cd9
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020768"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>Diseño de la aplicación de Microsoft Teams con plantillas de interfaz de usuario

Diseña tu aplicación de Microsoft Teams más rápido con plantillas de interfaz de usuario. Las plantillas son una colección de componentes basados en fluent ui que funcionan en casos de uso comunes de Teams, lo que te da más tiempo para averiguar la mejor experiencia para los usuarios.

## <a name="getting-started-with-tools-and-samples"></a>Introducción a herramientas y ejemplos

Los siguientes recursos pueden ayudarte a diseñar y desarrollar tu aplicación con plantillas de interfaz de usuario.

### <a name="microsoft-teams-ui-kit"></a>Kit de UI de Microsoft Teams

Toma plantillas de interfaz de usuario para el diseño de la aplicación desde el Kit de interfaz de usuario de Microsoft Teams, que también incluye información extensa sobre el uso, la anatomía, la accesibilidad y los procedimientos recomendados.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Biblioteca de interfaz de usuario de Microsoft Teams

Ver y probar plantillas de interfaz de usuario individuales de Teams y componentes relacionados en el explorador.

> [!div class="nextstepaction"]
> [Pruebe la biblioteca de interfaz de usuario (área de juegos)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importe estas plantillas y componentes relacionados directamente en el proyecto de la aplicación de Teams.

> [!div class="nextstepaction"]
> [Obtener la biblioteca de interfaz de usuario (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Aplicación de ejemplo

Instala una aplicación de ejemplo para ver cómo se ven y se comportan las plantillas de interfaz de usuario en contextos de Teams.

> [!div class="nextstepaction"]
> [Obtener la aplicación de ejemplo (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a>Lista

Puede usar una lista para mostrar elementos relacionados en un formato analizable y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Mostrar datos
* Acciones contextuales en el contenido de la aplicación

## <a name="dashboard"></a>Panel

Un panel muestra diferentes tipos de contenido en una ubicación central (pestaña o aplicación personal de Teams). Los usuarios deben poder personalizar al menos parte de lo que ven en un panel.

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de panel." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Analizar datos
* Métricas de informes
* Organizar información diferente en un solo lugar

## <a name="form"></a>Form

Los formularios se usan para recopilar, validar y enviar la entrada del usuario de forma estructurada. El etiquetado claro y las agrupaciones lógicas de campos de entrada son fundamentales para una buena experiencia del usuario.

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Iniciar sesión
* Perfiles de usuario
* Configuraciones
* Colección de entrada de usuario

## <a name="sign-in"></a>Iniciar sesión

Puedes diseñar flujos de inicio de sesión de aplicaciones para diferentes contextos de Teams y proveedores de identidades. En el ejemplo siguiente se incluye el inicio de sesión único (SSO), que se recomienda para la experiencia de autenticación más sencilla.

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de inicio de sesión." border="false":::

### <a name="top-use-case"></a>Caso de uso superior

* Autenticar usuarios

## <a name="task-board"></a>Panel de tareas

Un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales. También se puede usar para ordenar cualquier tipo de contenido en categorías. Puede editar y mover las tarjetas entre columnas.

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel de tareas." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Administración de proyectos. Asignación de tareas y estado de seguimiento
* Lluvia de ideas. Agregar ideas en distintas categorías
* Ordenar ejercicios. Organizar cualquier tipo de información en cubos

## <a name="data-visualization"></a>Visualización de datos

Puede usar diferentes tamaños de tarjeta (single, double y full) para apilar y organizar visualizaciones de datos en la misma página. Las tarjetas se escalan para ajustarse al diseño de columna y rellenar espacios en blanco.

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Mostrar información compleja
* Crear un panel

## <a name="wizard"></a>Asistente

Un asistente guía a un usuario a través de varias pantallas para completar una tarea (como un proceso de instalación).

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de asistente." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Instalación
* Incorporación
* Experiencias de primera ejecución

## <a name="empty-state"></a>Estado vacío

La plantilla de estado vacío se puede usar para muchos escenarios, como inicio de sesión, experiencias de primera ejecución, mensajes de error y mucho más. Es muy flexible: adaptá para usar uno, unos pocos o todos los componentes del siguiente diseño.

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Iniciar sesión
* Mensajes de bienvenida y experiencias de primera ejecución
* Mensajes de éxito
* Mensajes de error

## <a name="notification-bar"></a>Barra de notificaciones

Una barra de notificaciones es un área dedicada para mostrar mensajes breves e importantes que no requieren que el usuario tome medidas inmediatas. Los iconos y los colores de fondo específicos están asociados con tipos específicos de mensajes (vea a continuación).

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="En el ejemplo se muestran las plantillas de la barra de notificaciones." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Mensajes críticos, errores y advertencias
* Mensajes de éxito
* Mensajes informativos o promocionales

## <a name="left-nav"></a>Navegación izquierda

Use la navegación izquierda para examinar varias páginas dentro de la pestaña Teams. En el siguiente ejemplo, la navegación izquierda se encuentra entre la lista de canales y el contenido de la pestaña.

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="En el ejemplo se muestra una plantilla de navegación izquierda." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Examinar varias páginas dentro de una pestaña de Teams
* Dividir aplicaciones complejas en varias páginas

## <a name="breadcrumb"></a>Ruta de navegación

Las rutas de navegación son una ayuda de navegación que transmite la jerarquía de la aplicación. Ayudan a los usuarios a comprender cómo la página que están viendo se ajusta a la experiencia general y ofrecen acceso con un solo clic a niveles más altos de esa jerarquía.

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Jerarquía de comunicación
* Navegación

## <a name="toolbar"></a>Barra de herramientas

Una barra de herramientas es un contenedor para agrupar un conjunto de controles.

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Acciones contextuales en el contenido de la aplicación
* Filtro contextual y búsqueda
* Navegación y rutas de navegación

## <a name="stage"></a>Etapa

Stage ofrece una forma de que los usuarios abran una entidad (como una imagen, un archivo o un sitio web) en Teams en lugar de abrirlo en otra aplicación o explorador. El caso de uso principal de la fase es la visualización; la superficie no debe usarse para interacciones complejas.

(Nota de implementación: cree la fase con un módulo [de tareas grande](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="En el ejemplo se muestra una plantilla de fase." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Abrir una entidad en Teams en lugar de otra aplicación o explorador
* Contenido multimedia destacado u otro contenido
