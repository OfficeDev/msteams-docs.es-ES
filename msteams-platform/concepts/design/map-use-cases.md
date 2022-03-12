---
title: Asignar los casos de uso a las funcionalidades y capacidades de la aplicación de Teams
author: surbhigupta
description: Identifique cómo pueden funcionar los casos de uso de la aplicación dentro de la experiencia, características y capacidades de la aplicación Teams; asigne casos de uso comunes con funcionalidades.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 8cc1694a5ce5ee8472a48f86edf09eb7255a4810
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452833"
---
# <a name="map-your-use-cases-to-teams-app-features"></a>Asignar los casos de uso a las funcionalidades de la aplicación de Teams

Un caso de uso bien definido le ayuda a trazar el marco de características que desea en la aplicación de Teams. Una vez que haya determinado los requisitos del usuario, defina el ámbito y la funcionalidad de Teams más adecuada para su aplicación.

Puede asignar el caso de uso en función de:

* El uso compartido y la colaboración en elementos de un sistema externo.
* El inicio de flujos de trabajo y el envío de notificaciones a los usuarios.
* El uso de plataformas sociales, bots de conversación y combinación de varias características.

## <a name="common-use-cases-mapped-to-teams-capabilities"></a>Casos de uso comunes asignados a las funcionalidades de Teams

El siguiente paso es hacer coincidir los casos de uso con las funcionalidades de la aplicación.

Esta es una lista de escenarios de usuario comunes asignados a las funcionalidades de Teams. No es una lista exhaustiva, pero le ayudará a pensar en algunas de las posibilidades disponibles.
</br>
</br>
<details>
<summary>Crear, compartir y colaborar en elementos de un sistema externo</summary>

Aplicaciones para interactuar con los datos

| **Si quiere...** | **Pruebe…** |
| --- | --- |
| Busque sistemas externos y comparta los resultados como una tarjeta interactiva. | Extensiones de mensajería con comandos de búsqueda |
| Recopile información para insertarla en un almacén de datos o ejecutar búsquedas avanzadas. | Extensiones de mensajería con comandos de acción |
| Cree experiencias web insertadas para ver datos, trabajar con ellos y compartirlos. | Pestañas |
| Inserte datos y envíelos fuera del cliente de Teams. | Conectores y webhooks|
| Formularios modales interactivos desde cualquier lugar donde los necesite para recopilar o mostrar información. | Módulos de tareas |

</details>
</br>
<details>
<summary>Iniciar flujos de trabajo y procesos</summary>

Una forma rápida de iniciar un proceso o flujo de trabajo en un sistema externo.

| **Si quiere...** | **Pruebe…** |
| --- | --- |
| Desencadene mensajes, lo que permite a los usuarios enviar rápidamente el contenido de un mensaje a los servicios web. | Extensiones de mensajería: comando de acción |
| Abra mensajes desde una pestaña, un bot o una extensión de mensajería para recopilar información antes de iniciar un flujo de trabajo. | Módulos de tareas |
| Interactúe con los usuarios a través de texto y tarjetas enriquecidas. | Bots de conversación |
| Una buena opción para una interacción simple cuando no es necesario crear un bot de conversación completo. |  Webhooks salientes |

</details>
</br>
<details>
<summary>Enviar notificaciones y alertas</summary>

Envíe notificaciones y alertas asincrónicas a los usuarios en Teams.

| **Si quiere...** | **Pruebe…** |
| --- | --- |
| Envíe mensajes proactivos a grupos, canales o usuarios individuales. | Bots de conversación |
| Permita que un canal se suscriba para recibir mensajes. Un conector permite a los usuarios personalizar la suscripción con una página de configuración. | Conectores y webhooks entrantes |

</details>
</br>
<details>
<summary>Formular preguntas y obtener respuestas</summary>

Conectarse con los usuarios y resolver sus consultas

| **Si quiere...** | **Pruebe…** |
| --- | --- |
| Procesamiento de lenguaje natural, inteligencia artificial, aprendizaje automático y todas las palabras de moda. Use un bot con tecnología de la nube inteligente para conectar a los usuarios a las respuestas que necesitan. | Bots de conversación |
| Inserte el portal web existente en Teams o cree una versión específica de Teams para funcionalidades adicionales. | Pestañas |

</details>

## <a name="app-capabilities-mapped-to-features"></a>Funcionalidades de la aplicación asignadas a características

La plataforma Microsoft Teams ofrece una gran variedad de características. Cada característica es una forma de interactuar con los usuarios que hace que la funcionalidad de la aplicación Teams sea relevante para las necesidades del usuario.

Echemos un vistazo a cómo las funcionalidades de Teams habilitan diferentes características para su aplicación.

:::image type="content" source="../../assets/images/overview/teams-apps-capabilities.png" alt-text="Imagen que muestra las funcionalidades de Teams" border="true":::

Por ejemplo:

* Use la capacidad de la **pestaña** para mostrar módulos de tareas, solicitar permisos de dispositivo, mostrar <`iframe`> contenido o usar vínculos profundos.
* Use la capacidad de **extensión de mensajería** para enviar tarjetas, desatar vínculos o realizar acciones en los mensajes.

## <a name="see-also"></a>Consulte también

* [Lista de comprobación de la planificación](../design/planning-checklist.md)
* [Crear su primera aplicación de Microsoft Teams](../../get-started/get-started-overview.md)
