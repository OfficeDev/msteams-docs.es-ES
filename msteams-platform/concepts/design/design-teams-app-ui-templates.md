---
title: Diseño de la aplicación con plantillas de interfaz de usuario
author: heath-hamilton
description: Diseñe la aplicación con más rapidez con los componentes, los diseños y los patrones de interfaz de usuario estandarizados que se suelen ver en Microsoft Teams.
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 144c18ab03d76e442a4de64a5c61af76cb2b8b5f
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606332"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>Diseño de la aplicación de Microsoft Teams con plantillas de interfaz de usuario

Diseñar la aplicación de Microsoft Teams más rápidamente con plantillas de interfaz de usuario. Las plantillas son una colección de componentes basados en la interfaz de usuario fluida que funcionan en los casos de uso comunes de Teams, lo que le da más tiempo para averiguar la mejor experiencia para los usuarios.

## <a name="microsoft-teams-ui-kit"></a>Kit de IU de Microsoft Teams

Puede obtener plantillas de interfaz de usuario desde el kit de interfaz de usuario de Microsoft Teams, que también incluye información detallada sobre el uso, la anatomía, la accesibilidad y los procedimientos recomendados.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="list"></a>Lista

Puede usar una lista para mostrar elementos relacionados en un formato que se pueda analizar y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="Ejemplo se muestra una plantilla de interfaz de usuario de lista." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Mostrar datos
* Acciones contextuales en el contenido de la aplicación

## <a name="dashboard"></a>Panel

Un panel muestra distintos tipos de contenido en una ubicación central (una aplicación personal o pestaña de Microsoft Teams). Los usuarios deben poder personalizar al menos algunos de los elementos que ven en un panel.

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="Ejemplo se muestra una plantilla de interfaz de usuario del panel." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Analizar datos
* Métricas del informe
* Organizar información distinta en un solo punto

## <a name="form"></a>Form

Los formularios se usan para recopilar, validar y enviar entradas de usuario de una manera estructurada. La etiqueta clara y la Agrupación lógica de los campos de entrada son esenciales para una buena experiencia del usuario.

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="Ejemplo muestra una plantilla de interfaz de usuario de formulario." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Iniciar sesión
* Perfiles de usuario
* Configuración
* Colección de entrada de usuario

## <a name="sign-in"></a>Iniciar sesión

Puede diseñar flujos de inicio de sesión de aplicaciones para diferentes contextos de Teams y proveedores de identidades. El siguiente ejemplo incluye el inicio de sesión único (SSO), que recomendamos para la experiencia de autenticación más sencilla.

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="Ejemplo se muestra una plantilla de interfaz de usuario de inicio de sesión." border="false":::

### <a name="top-use-case"></a>Caso de uso superior

* Autenticar usuarios

## <a name="task-board"></a>Panel de tareas

Un panel de tareas, a veces denominado tablero Kanban o carriles de nadar, es una colección de tarjetas que a menudo se usa para realizar un seguimiento del estado de los elementos de trabajo o vales. También se puede usar para ordenar cualquier tipo de contenido en categorías. Puede editar y mover las tarjetas entre las columnas.

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="Ejemplo muestra una plantilla de interfaz de usuario del panel de tareas." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Administración de proyectos. Asignación de tareas y seguimiento del estado
* Lluvia. Adición de ideas en diferentes categorías
* Ordenación de ejercicios. Organizar cualquier tipo de información en cubos

## <a name="data-visualization"></a>Visualización de datos

Puede usar diferentes tamaños de tarjeta (único, doble y completo) para apilar y organizar visualizaciones de datos en la misma página. Las tarjetas se ajustan para ajustar el diseño de columna y rellenan espacios en blanco.

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="Ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Mostrar información compleja
* Crear un panel

## <a name="wizard"></a>Asistente

Un asistente guía al usuario a través de varias pantallas para completar una tarea (por ejemplo, un proceso de instalación).

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="Ejemplo muestra una plantilla de interfaz de usuario de asistente." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Instalación
* Incorporación
* Experiencias de primera ejecución

## <a name="empty-state"></a>Estado vacío

La plantilla de estado vacía se puede usar en muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc. Es muy flexible: se adapta para usar uno, algunos o todos los componentes en el siguiente diseño.

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="Ejemplo muestra una plantilla de interfaz de usuario de asistente." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Iniciar sesión
* Mensajes de bienvenida y experiencias de primera ejecución
* Mensajes de operación correcta
* Mensajes de error

## <a name="notification-bar"></a>Barra de notificaciones

Una barra de notificación es un área dedicada para mostrar mensajes importantes breves que no requieren que el usuario realice acciones inmediatas. Los colores e iconos de fondo específicos están asociados a tipos específicos de mensajes (vea a continuación).

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="Ejemplo muestra las plantillas de la barra de notificación." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Mensajes, errores y advertencias críticos
* Mensajes de operación correcta
* Mensajes informativos o promocionales

## <a name="left-nav"></a>Panel de navegación izquierdo

Use el panel de navegación izquierdo para explorar varias páginas dentro de la pestaña de Microsoft Teams. En el siguiente ejemplo, el panel de navegación izquierdo se encuentra entre la lista de canales y el contenido de la pestaña.

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="Ejemplo muestra una plantilla de navegación izquierda." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Examinar varias páginas dentro de una pestaña de Microsoft Teams
* Dividir las aplicaciones complejas en varias páginas

## <a name="breadcrumb"></a>Ruta de navegación

Las rutas de navegación son una ayuda de navegación que transmite la jerarquía de la aplicación. Ayudan a los usuarios a comprender cómo encaja la página que están viendo en la experiencia global y permiten el acceso con un solo clic a los niveles superiores de esa jerarquía.

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="Ejemplo muestra una plantilla de ruta de navegación." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Comunicar jerarquía
* Navegación

## <a name="toolbar"></a>Barra de herramientas

Una barra de herramientas es un contenedor para agrupar un conjunto de controles.

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="Ejemplo se muestra una plantilla de barra de herramientas." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Acciones contextuales en el contenido de la aplicación
* Filtro contextual y búsqueda
* Navegación y rutas de navegación

## <a name="stage"></a>Etapa

Stage ofrece una forma de que los usuarios abran una entidad (como una imagen, un archivo o un sitio web) en Microsoft Teams, en lugar de abrirlo en otra aplicación o en un explorador. El caso de uso principal de Stage es la visualización; la superficie no debe usarse para interacciones complejas.

(Nota de implementación: cree su stage con un gran [módulo de tareas](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)).

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="Ejemplo muestra una plantilla de fase." border="false":::

### <a name="top-use-cases"></a>Casos de uso principales

* Abrir una entidad en Teams en lugar de en otra aplicación o explorador
* Resaltar medios u otro contenido

## <a name="microsoft-teams-ui-library-coming-soon"></a>Biblioteca de IU de Microsoft Teams (próximamente)

La biblioteca de la interfaz de usuario de Microsoft Teams le permitirá importar directamente estas plantillas de interfaz de usuario listas para producción en su proyecto de aplicación.
