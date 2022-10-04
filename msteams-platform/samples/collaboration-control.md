---
title: Controles de colaboración
author: surbhigupta
description: En este módulo, obtenga información sobre cómo los controles de colaboración permiten a los creadores crear aplicaciones que se integran con servicios de Microsoft 365 como Planner, Bookings y Outlook.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: fa0cb45921820a61fbfd7112a50f28eb9230fb4b
ms.sourcegitcommit: f2ac771cbd608e872604e9ac8ffec2d08f55ee1a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2022
ms.locfileid: "68373027"
---
# <a name="collaboration-controls"></a>Controles de colaboración

Los controles de colaboración permiten aplicar Microsoft 365 y Microsoft Teams para aprobaciones, archivos, reuniones, notas y tareas para habilitar la colaboración contextual en torno a los procesos empresariales. Estos controles le permiten crear experiencias de colaboración personalizadas que se pueden exponer directamente en Teams. Las soluciones que componen los controles de colaboración permiten a los creadores crear aplicaciones que se integran con servicios de Microsoft 365 como Planner, Bookings, Outlook y SharePoint de una manera de código baja.

Estos controles le proporcionan la capacidad de simplificar la colaboración de flujo de trabajo de los usuarios mediante la creación de aplicaciones de línea de negocio y el trabajo sin cambiar el contexto de la aplicación a la aplicación con lo siguiente:

* Aprobaciones
* Archivos
* Reuniones
* Notas
* Tareas

> [!NOTE]
> Actualmente, los controles de colaboración solo están disponibles en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).

A continuación se muestran algunas de las funcionalidades clave de los controles de colaboración:

* **Microsoft Planner tareas:** cree tareas y asígnelas a los miembros de un registro para que puedan ver una lista consolidada de tareas en aplicaciones controladas por modelos y aplicaciones de tareas en Microsoft Teams.

* **Tareas de dataverse:** Cree tareas que se puedan asignar a usuarios externos a su organización.

* **Notas delverso de datos:** Cree notas que estén asignadas a un registro de la aplicación.

* **Reuniones de Outlook:** Programe reuniones con clientes y empleados internos y conéctese sin problemas con otros usuarios con Microsoft Teams con una selección de un botón.

* **Archivos de SharePoint:** Comparta archivos con miembros de un registro para que pueda buscar, hacer referencia y editar artefactos pertinentes en una ubicación centralizada respaldada por SharePoint.

* **Aprobaciones:** Optimice las solicitudes dentro del equipo.

> [!NOTE]
> Al configurar y usar las distintas funcionalidades de Microsoft 365 de los controles de colaboración mencionados anteriormente, se concede permiso para que los datos de usuario pasen a través de la Graph API y [acepten los términos de uso de la API de Microsoft](/legal/microsoft-apis/terms-of-use?context=graph%2Fcontext). Para obtener más información, consulte [Microsoft Graph](/graph/overview).

## <a name="how-collaboration-controls-works"></a>Funcionamiento de los controles de colaboración

Los controles se ejecutan dentro de una aplicación controlada por modelos de Power Apps (MDA) que se puede implementar en Microsoft Teams. MDA se ejecuta en Microsoft Dataverse y se puede integrar con un modelo de datos personalizado. Los controles se integran con las tareas de Microsoft Graph para Planner, los calendarios de Outlook y Teams y los archivos de SharePoint. Los controles de colaboración no se integran directamente con orígenes externos, como un sistema de registro o un portal.

* Los datos se pueden agregar a Dataverse desde orígenes externos a través de las API estándar de OData.

* Los datos se pueden leer desde Dataverse a través de las API estándar de OData y enviarse a orígenes externos, como un sistema de registro o un portal.

:::image type="content" source="~/assets/images/collaboration-control/consumption-mda.png" alt-text="Ciclo de vida de colaboración":::
