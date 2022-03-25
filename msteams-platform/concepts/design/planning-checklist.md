---
title: Preguntas para ayudar a planear el desarrollo de aplicaciones de Teams
author: heath-hamilton
description: Preguntas a tener en cuenta mientras planifica su aplicación, entender al usuario y sus necesidades, comprender los problemas del usuario que resolvería su aplicación, planificar la autenticación del usuario y su experiencia de incorporación
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: 6a2440ea05c1a89f4e1306b6fb54635287fb2d6d
ms.sourcegitcommit: 65cea59cc0602269395a2f87e023a4057d9cc55e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2022
ms.locfileid: "63765935"
---
# <a name="teams-app-planning-checklist"></a>Lista de comprobación de planeamiento de la aplicación de Teams

El ciclo de vida de una aplicación se extiende desde la planificación de la misma hasta su eventual Implementación, y mucho más. Para planificar la aplicación se necesita algo más que conocer al usuario y los requisitos. En función de las necesidades de la aplicación, también puede considerar la posibilidad de planear futuras actualizaciones.

Echemos un vistazo práctico al planeamiento del ciclo de vida de una aplicación.

## <a name="relevant-questions"></a>Preguntas relevantes

Esta es una lista de comprobación de preguntas que se deben tener en cuenta al planear la aplicación. Úselo como guía para asegurarse de que el plan cubre los detalles importantes del desarrollo de aplicaciones.

<br>
<br>
<details>
<summary>Comprenda al usuario</summary>

| # | Considere: |
| --- | --- |
| 1 | ¿Son los usuarios principalmente trabajadores directos con clientes móviles? |
| 2 | ¿Espera que muchos usuarios invitados necesiten acceso a la aplicación? |
| 3 | ¿Usan equipos y canales o, principalmente, chats grupales? |
| 4 | ¿Qué grado de sofisticación técnica tienen sus usuarios principales? |
| 5 | ¿Necesita una experiencia de incorporación completa o le bastan unos cuantos consejos? |

</details>
<br>
<details>
<summary>Comprender el problema</summary>

| # | Considere: |
|--- | --- |
| 1 | ¿Cuáles son las ventajas y desventajas del estado actual del sistema que usan sus usuarios? |
| 2 | ¿Cuáles son los problemas a los que se enfrentan los usuarios que desea solucionar? |
| 3 | ¿Qué características o funcionalidades les gustan y les encantan a sus usuarios en la forma actual de realizar el proceso? |

</details>
<br>
<details>
<summary>Comprender las limitaciones de la aplicación</summary>

| # | Considere: |
| --- | --- |
| 1 | ¿Cuáles son los retos que plantea la integración del back-end de la aplicación actual? |
| 2 | ¿Quién es el propietario de los datos del back-end: la empresa o terceros? |
| 3 | ¿Hay firewalls que afecten al funcionamiento de la aplicación? |
| 4 | ¿Existen API para acceder a los datos que necesita para el funcionamiento de su aplicación? |

</details>
<br>
<details>
<summary>Proporcionar autenticación</summary>

| # | Considere:|
|--- | --- |
| 1 | ¿Accederán los usuarios a diferentes vistas de los datos en función de sus funciones? |
| 2 | ¿Hay datos personales involucrados? |
| 3 | ¿Las interacciones también se basarán en los roles de usuario? |
| 4 | ¿Podrán los usuarios externos acceder a la aplicación? |

</details>
<br>
<details>
<summary>Planear la experiencia de incorporación</summary>

| # | Considere: |
| --- | --- |
| 1 | ¿Qué ocurre cuando un usuario configura por primera vez la pestaña en un canal? |
| 2 | Si está compartiendo tarjetas con una extensión de mensajería, ¿tiene sentido agregar un pequeño vínculo a una página de información para ayudar a presentar a los usuarios qué otras cosas puede hacer la aplicación? |
| 3 | ¿Espera que la mayoría de la gente tenga ya algún contexto de para qué sirve la aplicación, o que ya haya usado sus servicios en otro contexto? |
| 4 | ¿Llegan a la aplicación sin conocimientos previos? |

</details>
<br>
<details>
<summary>Aplicaciones de ámbito personal</summary>

| # | Considere: |
| --- | --- |
| 1 | ¿Se requiere una interacción individual con la aplicación por razones de privacidad u otros motivos? Por ejemplo, la comprobación del saldo de las vacaciones u otra información privada. |
| 2 | ¿Va a haber colaboración entre usuarios que pueden no tener ningún Teams en común? Por ejemplo, encontrar los próximos eventos de toda la organización en una empresa. |
| 3 | ¿Hay notificaciones o mensajes personalizados que deban enviarse al usuario a lo largo de la experiencia de la aplicación Teams? |

</details>
<br>
<details>
<summary>Aplicaciones de ámbito compartido</summary>

| # | Considere: |
| --- | --- |
| 1 | ¿La información que presenta la aplicación, ya sea en ficha o a través de un bot, es relevante y útil para la mayoría de los miembros de un equipo? Por ejemplo, la aplicación Scrum. |
| 2 | ¿Podría cambiar el contexto de la aplicación en función del equipo al que se agregue? Por ejemplo, las tareas de Planner son diferentes para distintos equipos. |
| 3 | ¿Es posible que todos los miembros de un rol que necesiten colaborar formen parte de un único equipo? Por ejemplo, agentes que trabajan en la solución de un vale. |

</details>
<br>
<details>
<summary>Elección del entorno de compilación</summary>

Sugerencia: opciones que ayudan a seleccionar el entorno correcto en función de las necesidades de la aplicación.
</details>
<br>
<details>
<summary>Planear la aplicación de prueba</summary>

Sugerencia: opciones que ayudan a determinar el mejor entorno de prueba para la aplicación.
</details>
<br>
<details>
<summary>Planear la distribución de aplicaciones</summary>

Sugerencia: opciones que ayudan a determinar el mejor modelo de distribución.

</details>

## <a name="plan-for-hosting-your-teams-app"></a>Planear el hospedaje de la aplicación de Teams

Teams no hospeda la aplicación. Cuando un usuario instala la aplicación en Teams, instala un paquete de aplicación que contiene un solo archivo de configuración (también conocido como manifiesto de aplicación) y los iconos de la aplicación. La lógica y el almacenamiento de datos de la aplicación se hospedan en otro lugar, como localhost durante el desarrollo y Azure Web Services. Teams accede a estos recursos a través de HTTPS.

:::image type="content" source="../../assets/images/teams-app-host.png" alt-text="Ilustración que muestra el hospedaje de aplicaciones para aplicación de Teams" border="true":::

## <a name="plan-beyond-app-building"></a>Planear más allá de la compilación de aplicaciones

- **Decida qué va a entrar en Teams**: tanto si se trata de una nueva aplicación como de una ya existente, compruebe si quiere que toda la aplicación esté dentro del cliente de Teams. Si integra solo una parte de la aplicación, céntrese en el uso compartido, la colaboración, el inicio y la supervisión de flujos de trabajo.

- **Planifique la experiencia de incorporación**: diseñe su experiencia de incorporación teniendo en cuenta a sus usuarios clave. La forma de incorporar un bot de chat instalado en un canal con mil personas, es diferente a cuando se instala en un chat individual.

- **Planifique el futuro**: identifique nuevas características que el usuario prefiera en la solución actual. Las nuevas características pueden afectar al diseño y la arquitectura de la aplicación.
