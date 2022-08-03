---
title: Limitaciones y problemas conocidos en la aplicación de control de colaboración
author: surbhigupta
description: En este módulo, obtenga información sobre las limitaciones y los problemas conocidos en la aplicación controles de colaboración para Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 6961b5fc51cc8aa2a2ad0620c8a8ef5032005f40
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2022
ms.locfileid: "67179296"
---
# <a name="limitations-and-known-issues"></a>Limitaciones y problemas conocidos

> [!NOTE]
> Actualmente, los controles de colaboración solo están disponibles en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).

A continuación se muestran las limitaciones de los controles de colaboración:

* Los componentes no se pueden usar en aplicaciones de Canvas.
* Los componentes solo admiten vistas de pestaña completas.

     :::image type="content" source="../assets/images/collaboration-control/tasks-tab.png" alt-text="Tasks" border="true":::

* No se respeta la vista de subcuadrícula seleccionada. Se mostrarán todas las tareas, reuniones o notas del registro de colaboración.

     :::image type="content" source="../assets/images/collaboration-control/subgrid-view.png" alt-text="vista de subcuadrícula" border= "true":::

* Las actividades agregadas al control de escala de tiempo no aparecen en los componentes, las tareas, las reuniones y las notas creadas en los componentes no se incluyen en el control de escala de tiempo.
* Los nuevos registros se deben guardar antes de acceder a los componentes; de lo contrario, verá una pantalla vacía.
* Los componentes no heredan los elementos temáticos del formulario o aplicación al que se agregan.
* La localización solo está disponible cuando se ejecuta la aplicación dentro de Microsoft Teams.
* No se admite el modo estricto de Microsoft Edge y se requieren cookies entre sitios.

**Administración Center no se actualiza cuando se completa la instalación o actualización**

Al seguir los pasos de instalación en [instalar controles de colaboración](~/samples/install-collaboration-control.md), se le redirigirá al Centro de administración de Power Platform. Se muestra un banner cuando se inicia la instalación, pero no se actualiza cuando se completa la instalación. El estado se muestra durante la instalación y, una vez completada la instalación, puede desaparecer de la lista. Puede ver la lista de soluciones en [https://make.powerapps.com/](https://make.preview.powerapps.com/) para confirmar que la instalación ha finalizado.

**Visualización durante la instalación:** :::image type="content" source="../assets/images/collaboration-control/view-during-installation.png" alt-text="vista durante la instalación" border="true":::

**Ver después de la instalación:** :::image type="content" source="../assets/images/collaboration-control/view-after-installation.png" alt-text="vista después de la instalación" border="true":::

Al actualizar los controles a una versión posterior, se muestra el mismo banner iniciado por la instalación, pero el estado del control permanece instalado incluso una vez completada la actualización. Puede confirmar que la actualización se ha completado comprobando la lista de soluciones en [https://make.powerapps.com/](https://make.preview.powerapps.com/), que debe tardar aproximadamente 15 minutos.

También puede ver en el historial de soluciones específicas que se instaló la versión posterior y, a continuación, se quitó la versión anterior: :::image type="content" source="../assets/images/collaboration-control/history.png" alt-text="Comprobación del historial" border="true":::

## <a name="bookings-meetings"></a>Reuniones de Bookings

El control Reuniones admite reuniones de una en una cuando se usa Bookings para interactuar con usuarios fuera de la organización. De una a muchas reuniones no se admiten en este momento mediante controles de colaboración.

**El estado de los asistentes a la reunión es incorrecto**

Cuando un asistente va a una reunión, es posible que su estado de respuesta no se muestre correctamente tanto en la vista de agenda como en los detalles de la reunión. La selección del botón de rechazo también puede devolver un mensaje de error en la pantalla.

## <a name="tasks"></a>Tareas

**Tareas: No se traduce el texto de filtro "claro"**

El texto del botón "borrar" que se muestra en el filtro Tareas no se traduce.

**Tareas: el menú contextual de cuadrícula aparece recortado**

Cuando, la cuadrícula Tareas se rellena con un número bajo de tareas, el menú contextual de la cuadrícula puede aparecer recortado y requerir el uso de barras de desplazamiento.

**Tareas: el filtro de búsqueda de palabras clave usa el operador "BeginsWith" para las tareas "Invitado".**

Al buscar tareas mediante el filtro de texto de palabra clave, las tareas "Invitado" se devuelven con el operador "BeginsWith". Las tareas "Member" se devuelven mediante el operador "Contains".

## <a name="files"></a>Archivos

Al navegar a la carpeta Archivo después de archivar archivos, los usuarios pueden experimentar carpetas de archivo duplicadas.  Navegar desde las carpetas de archivo a la vista principal de archivos resolverá el problema y los archivos archivados no se quitarán.

## <a name="controls"></a>Controles

**Los controles no se pueden guardar**

Si un control no puede guardar una tarea o reunión, la causa probable es un id. de grupo o un identificador de canal mal configurados.  

Solución 1: confirme que los identificadores son correctos y que la configuración se ha aplicado según el ejercicio de configuración.  

Solución 2: intente asegurarse de que el entorno de Power Apps y el entorno de Teams están en el mismo inquilino.  

**Los controles no se cargan o muestran un error**

Si los controles no se cargan o muestran un error, puede tratarse de un problema transitorio.

Ejemplo:

:::image type="content" source="../assets/images/collaboration-control/sync-fail.png" alt-text="error de sincronización de control":::

Esto se representaría en el registro de consola como:

:::image type="content" source="../assets/images/collaboration-control/control-fail.png" alt-text="error de control" border="true":::

Solución: actualice el explorador o, si está en la aplicación Teams, vuelva a cargar la pestaña.

Si desea cambiar el nombre, el icono o la descripción de la aplicación después de cargarlo en Teams, consulte [Personalización de la apariencia de las aplicaciones](/MicrosoftTeams/customize-apps#customize-details-of-an-app).

## <a name="error-logging"></a>Registro de errores

Los controles proporcionan los métodos siguientes para depurar la aplicación.

1. **Registro de seguimiento** de eventos de complemento cuando se invoca una API. Esta información se almacena en el entorno de Dataverse.

    1. Para habilitar el registro de seguimiento, siga estos pasos en [registro y seguimiento](/power-apps/developer/data-platform/logging-tracing?WT.mc_id=email).

1. **Registro del explorador** para los controles de interfaz de usuario. Se trata del registro de consola estándar.

    1. Se admite cuando se usa un explorador para ejecutar la aplicación de Collaboration Manager a través de Power Platform y la web de Teams.
    1. En la pestaña de consola, puede buscar errores mediante el mensaje de error Collaboration Manager o buscar nombres de control Collaboration Manager, como Tareas.

> [!TIP]
> Si se produce un error en un cliente de escritorio de Teams, intente replicar en la web de Teams para capturar el registro de errores.

## <a name="faq"></a>Preguntas más frecuentes

<br>

<details>

<summary><b>¿Cuáles son los controles de colaboración (versión preliminar)?</b></summary>

Los controles de colaboración (versión preliminar) permiten agregar funcionalidades de Microsoft 365 a las aplicaciones personalizadas de la línea de negocio de Power Apps para simplificar los flujos de trabajo de los usuarios al colaborar en procesos empresariales en Teams o Power Apps.

<br>

</details>

<br>

<details>

<summary><b>¿Cuál es la ventaja de los controles de colaboración (versión preliminar) para los fabricantes?</b></summary>

Con estos nuevos controles, como creador puede arrastrar y colocar controles que traigan la colaboración de Microsoft 365 a la aplicación.

<br>

</details>

<br>

<details>

<summary><b>¿Cuál es la ventaja de los controles de colaboración (versión preliminar) para los usuarios?</b></summary>

Los usuarios pueden experimentar mejoras de productividad y mantenerse en su flujo mediante la colaboración en aprobaciones, archivos, reuniones, notas y tareas sin salir del contexto de la aplicación.

<br>

</details>

<br>

<details>

<summary><b>Cómo obtener acceso a los controles de colaboración (versión preliminar)?</b></summary>

Solicite que el administrador de Power Platform instale los controles de AppSource en el entorno de Power Apps.

<br>

</details>

<br>

<details>

<summary><b>Cómo agregar los controles a una aplicación controlada por modelos?</b></summary>

Vaya al Diseñador de formularios y arrastre los controles desde el panel Componente a un formulario.

<br>

</details>
