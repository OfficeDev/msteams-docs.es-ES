---
title: Instalar Controles de colaboración
author: surbhigupta
description: En este módulo, aprenderá a instalar controles de colaboración con power apps y Microsoft 365 E3 y a instalar soluciones de controles de colaboración.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: ae7e3e93576e14f07784e8ded65858940e2cea21
ms.sourcegitcommit: 14fb175842e49888fc99ae813ce8a2b85fe1ff94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617981"
---
# <a name="install-collaboration-controls"></a>Instalar Controles de colaboración

> [!NOTE]
> Actualmente, los controles de colaboración solo están disponibles en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).

En este artículo, aprenderá a instalar controles de colaboración. Se requiere lo siguiente para compilar e implementar aplicaciones Collaboration Manager mediante los controles de colaboración:

* **Power Apps**: para compilar y ejecutar aplicaciones controladas por modelos mediante los controles de colaboración.
* **M365 E3 o superior**: para implementar aplicaciones personalizadas en Microsoft Teams y almacenar tareas en Planner, archivos en SharePoint y reuniones en Outlook.

Para instalar los componentes en un entorno de Power Platform, se requieren los siguientes roles:

* Personalizador del sistema
* Creador de entorno

Para obtener más información sobre los privilegios de rol, consulte [Configuración de la seguridad del usuario en un entorno](/power-platform/admin/database-security#predefined-security-roles).

## <a name="install-the-collaboration-controls-solutions"></a>Instalación de las soluciones de controles de colaboración

Instalará los controles de colaboración en el entorno de dataverse a través de [Microsoft AppSource.](https://appsource.microsoft.com/en-us/product/dynamics-365/mscm.collaboration-toolkit-preview?flightCodes=collaborationcontrols&signInModalType=2&ctaType=1)


Solo podrá configurar y usar los componentes de su propia aplicación basada en modelos después de examinar [Microsoft AppSource](https://appsource.microsoft.com/en-us/product/dynamics-365/mscm.collaboration-toolkit-preview?flightCodes=collaborationcontrols&signInModalType=2&ctaType=1)  e instalar controles de colaboración en el entorno de dataverse.

Los controles de colaboración incluyen las siguientes soluciones:

|**Soluciones de configuración** | **Finalidad** |
|---|---|
| Configuración de controles de colaboración | Mantener la infraestructura de configuración que impulsa los controles de colaboración |
| Objetos de configuración de controles de colaboración | Proporciona valores de configuración predefinidos que usan los controles de colaboración.|

|**Soluciones de colaboración** | **Finalidad** |
|---|---|
| Tareas de controles de colaboración  | Incluye el control PCF de tareas (marco de componentes de Power Apps). |
| Eventos de controles de colaboración | Incluye el control pcf de eventos para las citas de reuniones y reservas de Outlook y Teams. |
| Notas de controles de colaboración | Incluye el control PCF notes, que almacena notas en Dataverse. |
| Archivos de controles de colaboración | Incluye el control PCF Files para acceder a archivos en SharePoint. |
| Núcleo de controles de colaboración |Incluye API de colaboración personalizadas, el modelo de datos de colaboración y tablas virtuales para eventos, archivos y controles de tareas. |
| Controles de colaboración Aprobaciones | Incluye el nuevo control PCF aprobaciones. |
| Conector de controles de colaboración | Incluye el nuevo conector de Power Automate de colaboración |

> [!NOTE]
> Si tiene una versión existente de los controles instalados en el entorno, es posible que tenga que crear un entorno nuevo y completar una nueva instalación para actualizar correctamente a la versión más reciente.

Antes de la instalación, debe estar en un entorno de Power Platform o en un inquilino de administrador. Necesitará un entorno de dataverse con una base de datos. Si no tiene uno, deberá [crear uno nuevo](/power-platform/admin/create-environment) para continuar con la instalación.

Para instalar las soluciones, vaya a [Microsoft AppSource](https://appsource.microsoft.com/en-us/product/dynamics-365/mscm.collaboration-toolkit-preview?flightCodes=collaborationcontrols&signInModalType=2&ctaType=1) y complete los pasos siguientes:

1. Seleccione **el botón Obtener ahora** .

   :::image type="content" source="../assets/images/collaboration-control/preview-form.png" alt-text="Formulario de vista previa "border="true":::

1. Inicie sesión con su cuenta, rellene el formulario y seleccione **Continuar**.

   :::image type="content" source="../assets/images/collaboration-control/overview.png" alt-text="Información general sobre el control de colaboración" border="true":::

   :::image type="content" source="../assets/images/collaboration-control/collaboration-controls-preview.png" alt-text="Vista previa del control de colaboración" border="true":::

1. Se le dirigirá al Centro de Administración de Power Platform. Seleccione un entorno en el menú desplegable y acepte los términos y las instrucciones de directiva.

   > [!TIP]
   > Si ve un error de permisos al seleccionar el entorno, intente seleccionar fuera del menú desplegable del entorno para ver si resuelve el problema.

   :::image type="content" source="../assets/images/collaboration-control/install-environment.png" alt-text="Instalación del entorno de control de colaboración" border="true":::

1. Seleccione **Instalar**; la instalación puede tardar aproximadamente 15 minutos en completarse.

1. Ir a [https://make.powerapps.com/](https://make.powerapps.com/), [https://make.preview.powerapps.com/](https://make.preview.powerapps.com/) también se admite si se ha registrado en la versión preliminar de Power Apps.

1. Asegúrese de que está en el entorno en el que están instalados los controles, ya que puede ver el entorno y cambiarlo si es necesario en la parte superior derecha del portal de Power Apps.

1. Seleccione la pestaña **Soluciones** para ver todas las soluciones que ha instalado en el entorno adecuado.

   :::image type="content" source="../assets/images/collaboration-control/solutions.png" alt-text="control de colaboración de soluciones" border= "true":::

> [!NOTE]
> Los controles de colaboración son una vista previa y los elementos pueden cambiar con el tiempo con la posibilidad de cambios importantes. Los controles de colaboración no se admiten en entornos de producción.

Después de instalar correctamente todas las soluciones de colaboración en su entorno, podrá crear una nueva aplicación basada en modelos que pueda aprovechar las funcionalidades de control de colaboración.
