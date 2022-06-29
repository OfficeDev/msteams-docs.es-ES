---
title: Diseño de la aplicación con plantillas de interfaz de usuario
author: heath-hamilton
description: Aprenda a diseñar la aplicación más rápido con componentes, diseños y patrones de interfaz de usuario estandarizados que se suelen ver en Microsoft Teams.
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: reference
ms.openlocfilehash: 497385a8fa87714c8c87409d9d42bb88c294918a
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2022
ms.locfileid: "66484826"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>Diseño de la aplicación de Microsoft Teams con plantillas de interfaz de usuario

Diseñe la aplicación de Microsoft Teams más rápido con plantillas de interfaz de usuario. Las plantillas son una colección de componentes basados en la interfaz de usuario de Fluent que funcionan en casos de uso comunes de Teams, lo que proporciona más tiempo para averiguar la mejor experiencia para los usuarios.

## <a name="getting-started-with-tools-and-samples"></a>Introducción a herramientas y ejemplos

Los siguientes recursos pueden ayudarle a diseñar y desarrollar la aplicación mediante plantillas de interfaz de usuario.

### <a name="microsoft-teams-ui-kit"></a>Kit de interfaz de usuario de Microsoft Teams

Obtenga plantillas de interfaz de usuario para el diseño de la aplicación desde el kit de interfaz de usuario de Microsoft Teams, que también incluye información extensa sobre el uso, la anatomía, la accesibilidad y los procedimientos recomendados.

> [!div class="nextstepaction"]
> [Obtener el kit de interfaz de usuario (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams de interfaz de usuario

La biblioteca de interfaz de usuario de Microsoft Teams le ayuda a ver y probar plantillas de interfaz de usuario de Teams individuales y componentes relacionados en el explorador.

> [!div class="nextstepaction"]
> [Pruebe la biblioteca de interfaz de usuario (área de juegos)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importe estas plantillas y componentes relacionados directamente en el proyecto de aplicación de Teams.

> [!div class="nextstepaction"]
> [Obtener la biblioteca de interfaz de usuario (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Aplicación de ejemplo

Instale una aplicación de ejemplo para ver cómo se ven y se comportan las plantillas de interfaz de usuario en los contextos de Teams.

> [!div class="nextstepaction"]
> [Obtener la aplicación de ejemplo (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="calendar"></a>Calendario

En Teams, un calendario es donde un usuario ve, programa y administra eventos próximos y pasados para ellos mismos o para un grupo.

### <a name="top-use-cases"></a>Casos de uso principales

* Programar reuniones y eventos
* Obtenga recordatorios de las próximas reuniones y eventos.
* Ver programaciones

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/desktop-calendar.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de calendario en el escritorio." border="false":::

## <a name="dashboard"></a>Panel

Un panel muestra diferentes tipos de contenido en una ubicación central (por ejemplo, una pestaña o una aplicación personal de Teams). Los usuarios deben poder personalizar al menos parte de lo que ven en un panel.

### <a name="top-use-cases"></a>Casos de uso principales

* Análisis de datos
* Métricas de informe
* Organice información diferente en un solo lugar.

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de panel en dispositivos móviles." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de panel en el escritorio." border="false":::

## <a name="data-visualization"></a>Visualización de datos

Puede usar diferentes tamaños de tarjeta (único, doble y completo) para apilar y organizar visualizaciones de datos en la misma página. Las tarjetas se escalan para ajustarse al diseño de columna y rellenar espacios en blanco.

### <a name="top-use-cases"></a>Casos de uso principales

* Mostrar información compleja.
* Cree un panel.

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos en dispositivos móviles." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de visualización de datos en el escritorio." border="false":::

## <a name="empty-state"></a>Estado vacío

La plantilla de estado vacío se puede usar para muchos escenarios, incluidos el inicio de sesión, las experiencias de primera ejecución, los mensajes de error, etc. Es muy flexible: adaptálo para usar uno, algunos o todos los componentes del siguiente diseño.

### <a name="top-use-cases"></a>Casos de uso principales

* Iniciar sesión
* Mensajes de bienvenida y experiencias de primera ejecución.
* Mensajes correctos
* Mensajes de error

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía en el móvil." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de estado vacía en el escritorio." border="false":::

## <a name="filter"></a>Filtro

Un filtro le permite reducir la información que ve en función de los criterios seleccionados. Puede incluir filtros con tablas, listas, tarjetas y otros componentes que organicen el contenido.

### <a name="top-use-cases"></a>Casos de uso principales

Organización del contenido en:

* Listas
* Tablas
* Paneles
* Visualización de datos

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="En el ejemplo se muestra una plantilla de filtro." border="false":::

## <a name="form"></a>Formulario

Los formularios se usan para recopilar, validar y enviar entradas de usuario de forma estructurada. El etiquetado claro y las agrupaciones lógicas de los campos de entrada son fundamentales para una buena experiencia del usuario.

### <a name="top-use-cases"></a>Casos de uso principales

* Iniciar sesión
* Perfiles de usuario
* Configuraciones
* Colección de entradas de usuario

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario en el móvil." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/form.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de formulario en el escritorio." border="false":::

## <a name="list"></a>Lista

Puede usar una lista para mostrar elementos relacionados en un formato escaneable y permitir que los usuarios realicen acciones en una lista completa o en elementos individuales.

### <a name="top-use-cases"></a>Casos de uso principales

* Mostrar datos
* Acciones contextuales en el contenido de la aplicación

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista en dispositivos móviles." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de lista en el escritorio." border="false":::

## <a name="sign-in"></a>Iniciar sesión

Puede diseñar flujos de inicio de sesión de aplicaciones para diferentes contextos de Teams y proveedores de identidades. En el ejemplo siguiente se incluye el inicio de sesión único (SSO), que se recomienda para la experiencia de autenticación más sencilla.

### <a name="top-use-case"></a>Caso de uso superior

* Autenticación de usuarios

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de inicio de sesión en dispositivos móviles." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario de inicio de sesión en el escritorio." border="false":::

## <a name="settings"></a>Configuraciones

Las pantallas de configuración son donde los usuarios pueden configurar sus preferencias con la aplicación. (Nota: La configuración es un contenedor para [los componentes básicos de la interfaz de usuario](~/concepts/design/design-teams-app-basic-ui-components.md)).

### <a name="top-use-case"></a>Caso de uso superior

* Administración de características de la aplicación

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="En el ejemplo se muestra una plantilla de configuración." border="false":::

## <a name="task-board"></a>Panel de tareas

Un panel de tareas, a veces denominado tablero kanban o pistas de natación, es una colección de tarjetas que se usan a menudo para realizar un seguimiento del estado de los artículos de trabajo o boletos. También se puede usar para ordenar cualquier tipo de contenido en categorías. Puede editar y mover las tarjetas entre columnas.

### <a name="top-use-cases"></a>Casos de uso principales

* Administración de proyectos. Asignación de tareas y estado de seguimiento.
* Brainstorming. Agregar ideas en diferentes categorías.
* Ejercicios de ordenación. Organizar cualquier tipo de información en cubos.

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel de tareas en dispositivos móviles." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del panel de tareas en el escritorio." border="false":::

## <a name="wizard"></a>Asistente

Un asistente guía a un usuario a través de varias pantallas para completar una tarea (por ejemplo, un proceso de configuración).

### <a name="top-use-cases"></a>Casos de uso principales

* Instalación
* Incorporación
* Experiencias de primera ejecución

### <a name="mobile"></a>Móvil

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del asistente en dispositivos móviles." border="false":::

### <a name="desktop"></a>Escritorio

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="En el ejemplo se muestra una plantilla de interfaz de usuario del asistente en el escritorio." border="false":::

## <a name="see-also"></a>Vea también

* [Diseño de la aplicación con componentes básicos de la interfaz de usuario de Fluent](~/concepts/design/design-teams-app-basic-ui-components.md)
* [Diseño de la aplicación de Microsoft Teams con componentes avanzados de la interfaz de usuario](~/concepts/design/design-teams-app-advanced-ui-components.md)
* [Formatear los mensajes del bot](~/bots/how-to/format-your-bot-messages.md)
