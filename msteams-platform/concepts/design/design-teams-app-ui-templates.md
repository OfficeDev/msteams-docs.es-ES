---
title: Diseño de la aplicación con plantillas de interfaz de usuario
author: heath-hamilton
description: Diseña tu aplicación más rápido con componentes de interfaz de usuario estandarizados, diseños y patrones que se ven comúnmente en Microsoft Teams.
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 7d46829be50e6c88dc7629376437878a4b5fecf93d82e805a12093c96b3677ba
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57702893"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>Diseñar la aplicación Microsoft Teams con plantillas de interfaz de usuario

Diseña tu aplicación Microsoft Teams más rápido con plantillas de interfaz de usuario. Las plantillas son una colección de Fluent componentes basados en la interfaz de usuario que funcionan en casos de uso Teams comunes, lo que te da más tiempo para averiguar la mejor experiencia para los usuarios.

## <a name="getting-started-with-tools-and-samples"></a>Introducción a herramientas y ejemplos

Los siguientes recursos pueden ayudarte a diseñar y desarrollar tu aplicación con plantillas de interfaz de usuario.

### <a name="microsoft-teams-ui-kit"></a>Kit de interfaz de usuario de Microsoft Teams

Toma plantillas de interfaz de usuario para el diseño de la aplicación desde el kit de interfaz de usuario de Microsoft Teams, que también incluye información extensa sobre el uso, la anatomía, la accesibilidad y los procedimientos recomendados.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams Biblioteca de interfaz de usuario

Ver y probar plantillas de Teams de interfaz de usuario individuales y componentes relacionados en el explorador.

> [!div class="nextstepaction"]
> [Pruebe la biblioteca de interfaz de usuario (área de juegos)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importe estas plantillas y componentes relacionados directamente en el proyecto Teams aplicación.

> [!div class="nextstepaction"]
> [Obtener la biblioteca de interfaz de usuario (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Aplicación de ejemplo

Instala una aplicación de ejemplo para ver cómo se ven y se comportan las plantillas de interfaz de usuario en Teams contextos.

> [!div class="nextstepaction"]
> [Obtener la aplicación de ejemplo (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="dashboard"></a>Panel

Un panel muestra diferentes tipos de contenido en una ubicación central (Teams aplicación o pestaña personal). Los usuarios deben poder personalizar al menos parte de lo que ven en un panel.

### <a name="top-use-cases"></a>Casos de uso principales

* Analizar datos
* Métricas de informes
* Organizar información diferente en un solo lugar

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de panel en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de panel en el móvil." border="false":::

---

## <a name="data-visualization"></a>Visualización de datos

Puede usar diferentes tamaños de tarjeta (single, double y full) para apilar y organizar visualizaciones de datos en la misma página. Las tarjetas se escalan para ajustarse al diseño de columna y rellenar espacios en blanco.

### <a name="top-use-cases"></a>Casos de uso principales

* Mostrar información compleja
* Crear un panel

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos en el móvil." border="false":::

---

## <a name="empty-state"></a>Estado vacío

La plantilla de estado vacío se puede usar para muchos escenarios, como inicio de sesión, experiencias de primera ejecución, mensajes de error y mucho más. Es muy flexible: adaptá para usar uno, unos pocos o todos los componentes del siguiente diseño.

### <a name="top-use-cases"></a>Casos de uso principales

* Iniciar sesión
* Mensajes de bienvenida y experiencias de primera ejecución
* Mensajes de éxito
* Mensajes de error

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía en el móvil." border="false":::

---

## <a name="filter"></a>Filtro

Un filtro le permite reducir la información que ve en función de los criterios seleccionados. Puede incluir filtros con tablas, listas, tarjetas y otros componentes que organizan el contenido.

### <a name="top-use-cases"></a>Casos de uso principales

Organizar contenido en:

* Listas
* Tablas
* Paneles
* Visualización de datos

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="En el ejemplo se muestra una plantilla de filtro." border="false":::

## <a name="form"></a>Form

Los formularios se usan para recopilar, validar y enviar la entrada del usuario de forma estructurada. El etiquetado claro y las agrupaciones lógicas de campos de entrada son fundamentales para una buena experiencia del usuario.

### <a name="top-use-cases"></a>Casos de uso principales

* Iniciar sesión
* Perfiles de usuario
* Configuración
* Colección de entrada de usuario

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario en el móvil." border="false":::

---

## <a name="list"></a>List

Puede usar una lista para mostrar elementos relacionados en un formato analizable y permitir a los usuarios realizar acciones en una lista completa o elementos individuales.

### <a name="top-use-cases"></a>Casos de uso principales

* Mostrar datos
* Acciones contextuales en el contenido de la aplicación

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista en el móvil." border="false":::

---

## <a name="sign-in"></a>Iniciar sesión

Puedes diseñar flujos de inicio de sesión de aplicaciones para diferentes Teams contextos y proveedores de identidades. En el ejemplo siguiente se incluye el inicio de sesión único (SSO), que se recomienda para la experiencia de autenticación más sencilla.

### <a name="top-use-case"></a>Caso de uso superior

* Autenticar usuarios

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de inicio de sesión en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de inicio de sesión en el móvil." border="false":::

---

## <a name="settings"></a>Configuración

Configuración pantallas son donde los usuarios pueden configurar sus preferencias con la aplicación. (Nota: Configuración es un contenedor para componentes de interfaz [de usuario básicos](~/concepts/design/design-teams-app-basic-ui-components.md).)

### <a name="top-use-case"></a>Caso de uso superior

* Administrar características de la aplicación

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="En el ejemplo se muestra una plantilla de configuración." border="false":::

## <a name="task-board"></a>Panel de tareas

Un panel de tareas, a veces denominado tablero de kanban o carriles de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los elementos de trabajo o los vales. También se puede usar para ordenar cualquier tipo de contenido en categorías. Puede editar y mover las tarjetas entre columnas.

### <a name="top-use-cases"></a>Casos de uso principales

* Administración de proyectos. Asignación de tareas y estado de seguimiento
* Lluvia de ideas. Agregar ideas en distintas categorías
* Ordenar ejercicios. Organizar cualquier tipo de información en cubos

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel de tareas en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel de tareas en el móvil." border="false":::

---

## <a name="wizard"></a>Asistente

Un asistente guía a un usuario a través de varias pantallas para completar una tarea (como un proceso de instalación).

### <a name="top-use-cases"></a>Casos de uso principales

* Configuración
* Incorporación
* Experiencias de primera ejecución

# <a name="desktop"></a>[Escritorio](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del asistente en el escritorio." border="false":::

# <a name="mobile"></a>[Móvil](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de asistente en el móvil." border="false":::

---
