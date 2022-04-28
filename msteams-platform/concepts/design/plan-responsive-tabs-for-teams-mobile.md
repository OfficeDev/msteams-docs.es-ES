---
title: Planeamiento de Teams móvil
author: surbhigupta
description: Guía para planear la creación de una aplicación en Teams móvil
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: v-abirade
ms.openlocfilehash: e260d3d4a1afcc625d588e6918eb9a01acfdea77
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103933"
---
# <a name="plan-responsive-tabs-for-teams-mobile"></a>Planear pestañas con capacidad de respuesta para dispositivo móvil de Teams

 Teams plataforma ofrece la oportunidad de crear aplicaciones en dispositivos móviles y de escritorio. Los usuarios de la aplicación pueden preferir el escritorio o el móvil, o ambos. Los usuarios pueden preparar datos en el escritorio, pero consumir y compartir más datos mediante dispositivos móviles. La clave para compilar cualquier aplicación es comprender y satisfacer las necesidades de los usuarios. Hay funcionalidades como bots, extensiones de mensajes y conectores que funcionan sin problemas en dispositivos móviles y de escritorio. Sin embargo, la creación de pestañas y módulos de tareas requiere planear el hospedaje de la experiencia web en Teams móvil. Las guías de artículos para planear las páginas web con capacidad de respuesta en Teams móvil.

## <a name="identify-apps-scope"></a>Identificación del ámbito de las aplicaciones

En la lista siguiente se proporciona la información clave para planear la creación de aplicaciones para Teams móvil:

* Considere la funcionalidad entre dispositivos de Teams aplicación. Por ejemplo, si tiene una aplicación de buen rendimiento en el escritorio, puede explorar para crear una aplicación similar en dispositivos móviles. Inicialmente, puede ser difícil cambiar toda la experiencia de escritorio en el móvil. Puede empezar con escenarios básicos pero comunes. Agregue funcionalidades y funcionalidades después de recopilar más información y comentarios del usuario.

* Asegúrese de dirigirse a la persona de usuario adecuada en el móvil. Por ejemplo, si va a crear una aplicación que proporciona servicio a los usuarios finales y también proporciona acceso a datos a desarrolladores y administradores sénior, los usuarios finales pueden usar la aplicación más mientras empieza a compilar la aplicación en Teams móvil. Sin embargo, puedes atender a todas las personas que tienes en tu aplicación de escritorio, pero se recomienda empezar por persona con una base más grande y posibles usuarios pioneros para una experiencia de pantalla más pequeña. Según el ejemplo, los usuarios finales son los usuarios adecuados. Puede agregar funcionalidades gradualmente para admitir a otros usuarios en su Teams móvil.

## <a name="understand-different-stages-to-build-apps"></a>Descripción de las distintas fases para compilar aplicaciones

Después de identificar el ámbito de la aplicación, es el momento de comprender las tres fases siguientes para planear cualquier aplicación en Teams móvil y mejorar la experiencia del usuario:

1. **Consumo**

   Ver aplicaciones en dispositivos móviles. Para compilar una aplicación en dispositivos móviles, puede empezar con la experiencia de consumo. Dado que el mundo móvil ha convertido el desplazamiento por contenido en una práctica común, puede mostrar información relevante. Use mecanismos de interacción, como notificaciones para informar sobre las actualizaciones.

2. **Acciones rápidas**

   Use la aplicación en el móvil. Después de que los usuarios empiecen a consumir el contenido en dispositivos móviles, puede escalar la aplicación al siguiente nivel mediante la migración de algunas acciones desde la aplicación de escritorio. Puede optimizar y compilar nuevas acciones para dispositivos móviles.

3. **Activación**

   Proporcionar experiencias de aplicación completas para interactuar en dispositivos móviles. A medida que los usuarios interactúan con la aplicación, proporcione una experiencia inmersiva completa en dispositivos móviles, ya sea a la par o mejor que la experiencia de escritorio. Para proporcionar una buena experiencia a los usuarios, haga que todos los casos de uso respondan en el móvil.

> [!TIP]
> Para obtener información sobre las directrices de diseño, consulte [proceso de diseño para Teams aplicaciones](design-teams-app-process.md).

## <a name="use-cases"></a>Casos de uso

Veamos los siguientes casos de uso para comprender cómo planear diferentes tipos de aplicaciones para Teams móvil:

<br>

<details>

<summary><b>Aplicaciones de visualización de datos y paneles</b></summary>

Puede comprender cómo planear pestañas con capacidad de respuesta para aplicaciones de visualización de datos y paneles en Teams plataforma móvil.

Consumo:

En la primera fase, puede implementar la experiencia de consumo más básica para ver los datos. El propósito de cualquier aplicación del dominio es mostrar datos en forma de visualizaciones. En la aplicación, puede mostrar visualizaciones vistas recientemente en el escritorio o una lista de todos los gráficos autorizados para los usuarios. Después de crear paneles en el escritorio, los usuarios pueden acceder a la información mediante dispositivos móviles. Puede mostrar una vista detallada de cualquier gráfico seleccionado por el usuario como una vista expandida en las pestañas o mediante módulos de tareas.

Puede mostrar la siguiente información:

* Paneles y resúmenes
* Objetos visuales, mapas e infografías de datos
* Gráficos, gráficos y tablas

![Consumo de aplicaciones de visualización de datos y paneles](../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-consumption.png)

Acciones rápidas:

En la segunda fase, los usuarios pueden trabajar en los gráficos y objetos visuales existentes desde la experiencia de escritorio. Puede introducir las siguientes acciones:

* Buscar contenido
* Filtrar datos
* Crear marcadores

![Acciones rápidas de aplicaciones de visualización de datos y paneles](../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-quick-actions.png)

Habilitación:

En la tercera fase, permita a los usuarios crear contenido, como gráficos y gráficos desde cero. Asegúrese de presentar todas las funcionalidades de la aplicación para dispositivos móviles. Por ejemplo, puede usar módulos de tareas para ayudar a acceder a elementos de datos específicos con una vista detallada.

Puede proporcionar el siguiente acceso a los usuarios:

* Modificar título y descripción
* Insertar elementos de datos para crear visualizaciones
* Compartir visualizaciones en un canal o chat de grupo

![Habilitación de aplicaciones de visualización de datos y paneles](../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-enablement.png)

<br>

</details>

<br>

<details>

<summary><b>Aplicaciones de incorporación de tareas</b></summary>

Puede comprender cómo planear pestañas con capacidad de respuesta para aplicaciones de incorporación de tareas en Teams plataforma móvil.

Consumo:

En la primera fase, la aplicación puede mostrar la lista de tareas al usuario en una pila vertical. Si hay varias categorías de tareas, como **Propuesto**, **Activo** y **Cerrado** , proporcione filtros para mostrar tareas agrupadas o como encabezados para ver las tareas agrupadas.

![Consumo de aplicaciones de incorporación de tareas](../../assets/images/app-fundamentals/taskboarding-apps-consumption.png)

Acciones rápidas:

En la segunda fase, puede proporcionar a los usuarios el siguiente acceso a la aplicación:

* Creación de tareas o elementos con los campos obligatorios para reducir la carga cognitiva de los usuarios
* Cambiar el tipo de placa o la vista
* Revisar las tareas expandiendo la vista
* Uso de módulos de tareas para ver la vista detallada
* Mover las tareas a distintas categorías
* Compartir tareas relevantes en chats y canales a través de correos electrónicos y fuente de actividad

![Acciones rápidas de las aplicaciones de incorporación de tareas](../../assets/images/app-fundamentals/taskboarding-apps-quick-actions.png)

Habilitación:

En la tercera fase, puede habilitar la experiencia de los usuarios con las siguientes actividades:

* Incorporación de nuevos proyectos y paneles
* Agregar y modificar diferentes categorías, como **Propuesto**, **Activo** y **Cerrado**
* Configuración de las tareas para comentarios, datos adjuntos y otras características complejas

![Habilitación de aplicaciones de incorporación de tareas](../../assets/images/app-fundamentals/taskboarding-apps-enablement.png)
<br>

</details>

<br>

<details>

<summary><b>Coautoría y pizarra de aplicaciones</b></summary>

Puede comprender cómo planear pestañas con capacidad de respuesta para la coautoría y la pizarra de aplicaciones en Teams plataforma móvil.

Consumo:

En la primera fase, puede considerar la experiencia de escritorio para mostrar el contenido y los recursos de la aplicación.  Puede mostrar las siguientes funciones:

* Comentarios o comentarios
* Acercar o alejar
* Fase actual o progreso de un documento pendiente

![Coautoría y consumo de aplicaciones de pizarra](../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-consumption.png)

Acciones rápidas:

En la segunda fase, puede introducir las siguientes acciones:

* Creación de un nuevo panel para la colaboración o nuevos documentos para la firma
* Compartir paneles internamente y también con invitados
* Configuración de permisos de administrador

> [!TIP]
> Se exponen acciones, que se pueden mostrar fácilmente en las pantallas pequeñas.

![Acciones rápidas de las aplicaciones de coautoría y pizarra](../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-quick-actions.png)

Habilitación:

En la tercera fase, proporcione una experiencia completa a los usuarios. Puede habilitar la experiencia de los usuarios con las siguientes actividades:

* Adición de texto, formas y notas rápidas
* Navegar por el contenido
* Adición de capas y filtros
* Operaciones de eliminación, deshacer y rehacer
* Acceda a la cámara y al micrófono mediante las API del SDK de JS. Para obtener más información sobre las funcionalidades del dispositivo, consulte [Información general sobre las funcionalidades del dispositivo](../device-capabilities/device-capabilities-overview.md).

![Habilitación de aplicaciones de coautoría y pizarra](../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-enablement.png)

<br>

</details>

## <a name="see-also"></a>Vea también

Las siguientes directrices de diseño y validación ayudan en función del ámbito de la aplicación:

* [Diseño de la pestaña](../../tabs/design/tabs.md)
* [Cómo diseñar su bot](../../bots/design/bots.md)
* [Diseño de módulos de tareas](../..//task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [Directrices de validación de la tienda](../deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)
