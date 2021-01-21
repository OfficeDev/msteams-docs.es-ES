---
title: Diseñar la aplicación con plantillas de interfaz de usuario
author: heath-hamilton
description: Diseñe su aplicación con mayor rapidez con componentes, diseños y patrones estandarizados de la interfaz de usuario que se ven habitualmente en Microsoft Teams.
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: b4d244bbf78ac85042d5caf8ec84afe42e79b3c7
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911929"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>Diseño de la aplicación de Microsoft Teams con plantillas de interfaz de usuario

Diseñe su aplicación de Microsoft Teams más rápido con plantillas de interfaz de usuario. Las plantillas son una colección de componentes basados en la interfaz de usuario fluent que funcionan en casos de uso comunes de Teams, lo que le da más tiempo para averiguar la mejor experiencia para sus usuarios.

## <a name="getting-started-with-tools-and-samples"></a>Introducción a herramientas y ejemplos

Los siguientes recursos pueden ayudarte a diseñar y desarrollar tu aplicación mediante plantillas de interfaz de usuario.

### <a name="microsoft-teams-ui-kit"></a>Kit de interfaz de usuario de Microsoft Teams

Obtener plantillas de interfaz de usuario para el diseño de la aplicación desde el Kit de interfaz de usuario de Microsoft Teams, que también incluye amplia información sobre el uso, anatomía, accesibilidad y procedimientos recomendados.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Biblioteca de interfaz de usuario de Microsoft Teams

Ver y probar plantillas individuales de la interfaz de usuario de Teams y componentes relacionados en el explorador.

> [!div class="nextstepaction"]
> [Probar la biblioteca de la interfaz de usuario (área de prueba)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importe estas plantillas y componentes relacionados directamente en su proyecto de aplicación de Teams.

> [!div class="nextstepaction"]
> [Obtener la biblioteca de interfaz de usuario (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Aplicación de ejemplo

Instale una aplicación de ejemplo para ver el aspecto y el comportamiento de las plantillas de interfaz de usuario en los contextos de Teams.

> [!div class="nextstepaction"]
> [Obtener la aplicación de ejemplo (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a>Lista

Puede usar una lista para mostrar elementos relacionados en un formato que se pueda examinar y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Mostrar datos
* Acciones contextuales en el contenido de la aplicación

## <a name="dashboard"></a>Panel

Un panel muestra diferentes tipos de contenido en una ubicación central (pestaña o aplicación personal de Teams). Los usuarios deben poder personalizar al menos parte de lo que ven en un panel.

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de panel." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Analizar datos
* Métricas de informes
* Organizar información diferente en un solo lugar

## <a name="form"></a>Form

Los formularios se usan para recopilar, validar y enviar entradas de usuario de forma estructurada. El etiquetado claro y las agrupaciones lógicas de campos de entrada son fundamentales para una buena experiencia del usuario.

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Iniciar sesión
* Perfiles de usuario
* Configuración
* Colección de entradas de usuario

## <a name="sign-in"></a>Iniciar sesión

Puede diseñar flujos de inicio de sesión de aplicaciones para diferentes contextos de Teams y proveedores de identidades. En el siguiente ejemplo se incluye el inicio de sesión único (SSO), que se recomienda para la experiencia de autenticación más sencilla.

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de inicio de sesión." border="false":::

### <a name="top-use-case"></a>Caso de uso principal

* Autenticar usuarios

## <a name="task-board"></a>Panel de tareas

Un panel de tareas, a veces denominado tablero de kanban o pistas de nado, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales. También se puede usar para ordenar cualquier tipo de contenido en categorías. Puede editar y mover las tarjetas entre columnas.

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel de tareas." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Administración de proyectos. Asignación de tareas y estado de seguimiento
* Lluvia de ideas. Agregar ideas en distintas categorías
* Ejercicios de ordenación. Organizar cualquier tipo de información en cubos

## <a name="data-visualization"></a>Visualización de datos

Puede usar distintos tamaños de tarjeta (único, doble y completo) para apilar y organizar visualizaciones de datos en la misma página. Las tarjetas se escalan para ajustarse al diseño de columna y rellenar espacios en blanco.

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Mostrar información compleja
* Crear un panel

## <a name="wizard"></a>Asistente

Un asistente guía a un usuario a través de varias pantallas para completar una tarea (como un proceso de configuración).

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de asistente." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Instalación
* Incorporación
* Experiencias de primera ejecución

## <a name="empty-state"></a>Estado vacío

La plantilla de estado vacía se puede usar para muchos escenarios, incluido el inicio de sesión, experiencias de primera ejecución, mensajes de error y mucho más. Es muy flexible: adaptarlo para usar uno, algunos o todos los componentes del siguiente diseño.

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Iniciar sesión
* Mensajes de bienvenida y experiencias de primera ejecución
* Mensajes de éxito
* Mensajes de error

## <a name="notification-bar"></a>Barra de notificaciones

Una barra de notificaciones es un área dedicada para mostrar mensajes breves e importantes que no requieren que el usuario realice una acción inmediata. Los iconos y los colores de fondo específicos están asociados a tipos específicos de mensajes (consulta a continuación).

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="En el ejemplo se muestran las plantillas de la barra de notificaciones." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Mensajes críticos, errores y advertencias
* Mensajes de éxito
* Mensajes informativos o promocionales

## <a name="left-nav"></a>Navegación izquierda

Use el panel de navegación izquierdo para examinar varias páginas dentro de la pestaña de Teams. En el siguiente ejemplo, el panel de navegación izquierdo se encuentra entre la lista de canales y el contenido de la pestaña.

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="En el ejemplo se muestra una plantilla de navegación izquierda." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Examinar varias páginas en una pestaña de Teams
* Dividir aplicaciones complejas en varias páginas

## <a name="breadcrumb"></a>Ruta de navegación

Las rutas de navegación son una ayuda de navegación que transmite la jerarquía de la aplicación. Ayudan a los usuarios a comprender cómo se ajusta la página que están viendo a la experiencia general y permiten el acceso de un solo clic a niveles superiores de esa jerarquía.

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="En el ejemplo se muestra una plantilla de ruta de navegación." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Comunicar jerarquía
* Navegación

## <a name="toolbar"></a>Barra de herramientas

Una barra de herramientas es un contenedor para agrupar un conjunto de controles.

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="En el ejemplo se muestra una plantilla de barra de herramientas." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Acciones contextuales en el contenido de la aplicación
* Filtro contextual y búsqueda
* Navegación y rutas de navegación

## <a name="stage"></a>Etapa

La fase ofrece a los usuarios una forma de abrir una entidad (como una imagen, un archivo o un sitio web) en Teams en lugar de abrirlo en otra aplicación o explorador. El caso de uso principal de la fase es la visualización; la superficie no debe usarse para interacciones complejas.

(Nota de implementación: cree la fase con un módulo [de tareas de gran tamaño).](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="En el ejemplo se muestra una plantilla de fase." border="false":::

### <a name="top-use-cases"></a>Principales casos de uso

* Abrir una entidad en Teams en lugar de otra aplicación o explorador
* Contenido multimedia destacado u otro contenido
