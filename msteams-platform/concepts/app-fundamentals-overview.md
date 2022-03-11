---
title: Información general sobre el planeamiento de la aplicación
author: heath-hamilton
description: Presente los elementos de la planificación de una aplicación, comprendiendo los casos de uso, las funcionalidades de la aplicación y otras características de Teams.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
keywords: puntos de entrada extensibilidad casos de uso capacidad del dispositivo
ms.openlocfilehash: 02a41631931f24fa23e2ddaaadaf2a94c63c5b23
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399173"
---
# <a name="plan-your-app-with-teams-features"></a>Planear la aplicación con las características de Teams

Crear una aplicación impresionante para Teams consiste en encontrar la combinación adecuada de características para satisfacer las necesidades de los usuarios. El diseño, las características y las funcionalidades de una aplicación se derivan de este propósito.

En esencia, Teams es una plataforma de colaboración. También es una plataforma social, es nativamente multiplataforma, se sitúa en el centro de Office 365 y ofrece un lienzo personal para que usted pueda crear aplicaciones.

En esta sección, aprenderá a:

* Identificar y asignar los casos de uso a las características de los equipos.
* Usar la lista de comprobación de la planificación.
* Planificar más allá de la implementación de la aplicación.

## <a name="plan-with-teams"></a>Planificar con Teams

Teams como plataforma le ofrece kits de herramientas, bibliotecas y aplicaciones en cada fase del desarrollo de aplicaciones. Vamos a desglosarlo en el ciclo de vida de creación de aplicaciones:

:::image type="content" source="../assets/images/app-fundamentals/plan-app.png" alt-text=" La ilustración muestra la planificación de la aplicación " border="true":::

* [Antes de la creación](#before-you-build)
* [Durante la creación ](#during-build)
* [Después de la creación](#post-build)
* [Lista de comprobación de la planificación](../concepts/design/planning-checklist.md)

### <a name="before-you-build"></a>Antes de la creación

Entender a los usuarios y sus preocupaciones son los primeros indicadores de cómo puede ayudar una aplicación de Teams. Construya su caso de uso en torno al problema, determine cómo puede resolverlo una aplicación y diseñe una solución.

* **Comprenda su caso de uso y las características de la aplicación Teams**: comprenda los requisitos de su usuario y podrá identificar las características adecuadas.

* **Mapear los casos de uso**: asigne casos de uso comunes a las características de Teams en función de los requisitos, como el uso compartido, la colaboración, los flujos de trabajo, las plataformas sociales pertinentes y mucho más.

* **Planifique pestañas con capacidad de respuesta para Teams para dispositivos móviles**: cubre los escenarios más comunes y ayuda a planificar las aplicaciones para Teams para dispositivos móviles.

### <a name="during-build"></a>Durante la creación

* **Cree y compile el proyecto de la aplicación**: con Teams, puede elegir el entorno de compilación que mejor se adapte a sus requisitos de aplicación. Use el kit de herramientas de Teams u otros SDK, como C#, Blazor, Node.js, etc. para empezar.

* **Diseñar la interfaz de usuario de la aplicación**: use el kit de herramientas de interfaz de usuario de Teams y la biblioteca de interfaz de usuario para diseñar el formato de su aplicación.

* **Use Teams como plataforma**: la plataforma Teams le ayuda a crear una aplicación de una o varias funcionalidades. La aplicación de Teams está respaldada por los productos y servicios integrados que refuerzan la experiencia de la aplicación.

    :::image type="content" source="../assets/images/overview/teams-solution.png" alt-text="Representación conceptual de la solución de Teams." border="true":::

    Las aplicaciones aparecen en Teams como pestañas, bots, extensiones de mensajería, conectores y webhooks, o como una aplicación de varias capacidades. Estas funcionalidades se basan en el back-end de Azure, Microsoft Graph, SharePoint y Power Apps que ayudan a automatizar tareas y procesos.

    Juntas, estas funcionalidades dan vida a la solución de la aplicación.

* **Integrate las funcionalidades del dispositivo**: puede integrar las funcionalidades nativas del dispositivo en su aplicación, como la cámara, el escáner de códigos de barras o QR, la galería de fotos, el micrófono y la localización.

### <a name="post-build"></a>Después de la creación

* Integre su aplicación con Teams y otras aplicaciones, como Microsoft 365, Microsoft Graph y mucho más.
* Use Portal para desarrolladores para configurar, administrar e implementar la aplicación.

<details>
<summary><b>Más información sobre Government Community Cloud (GCC)</b></summary>

Government Community Cloud es una copia centrada en el gobierno del entorno comercial. El Departamento de Defensa (DOD) y los contratistas federales deben cumplir con los estrictos requisitos de ciberseguridad y cumplimiento. Para ello, se creó el GCC-High para satisfacer las necesidades del DOD y de los contratistas federales. GCC-High es una copia de la nube del DOD pero existe en su propio entorno soberano. La nube del DOD se crea solo para el Departamento de Defensa.

En la tabla siguiente se incluyen las características y la disponibilidad de Teams para GCC, GCC-High y DOD:

| Características   | GCC | GCC-High | DOD |
|-------------|---------|---|---|
| Aplicaciones propiedad de Teams como en aplicaciones desarrolladas internamente | ✔️ La aplicación está habilitada si tiene GCC. | ✔️ La aplicación está habilitada si tiene GCC-High. | ✔️ La aplicación está habilitada si tiene DOD. |
| Aplicaciones de Microsoft | ✔️ Aplicaciones de Microsoft compatibles con GCC | ✔️ Aplicaciones de Microsoft compatibles con GCC-High | ✔️ Aplicaciones de Microsoft compatibles con DOD |
| Aplicaciones de 3p o de terceros | ✔️ Hay aplicaciones de terceros disponibles. Deshabilitado de forma predeterminada y el administrador de inquilinos usa su discreción para habilitarlo. | ❌ | ❌ |
| Bots | ✔️ | ❌ | ❌ |
| Aplicaciones de pestaña Personalizadas o Lob |  ✔️ | ✔️ | ✔️ |
| Aplicaciones de instalación de prueba:  | ✔️ | ❌ | ❌ |
| Bots personalizados o Lob | ✔️ | ❌ | ❌ |
| Extensiones de mensajería personalizadas | ❌ | ❌ | ❌ |
| Conectores personalizados | ❌ | ❌ | ❌ |

La lista siguiente ayuda a identificar la disponibilidad de GCC, GCC-High y DOD para las características:

* Para aplicaciones de terceros, consulte [aplicaciones web](../samples/integrating-web-apps.md) y [extensibilidad de aplicaciones de reuniones](../apps-in-teams-meetings/meeting-app-extensibility.md).
* Para bots, consulte [crear su primer bot de conversación para Teams](../get-started/first-app-bot.md), [diseñar el bot de Teams](../bots/design/bots.md), [agregar bots a aplicaciones de Microsoft Teams](../resources/bot-v3/bots-overview.md)y [bots en Teams](../bots/what-are-bots.md).
* Para las aplicaciones de instalación de prueba, vea [habilitar la personalización de la aplicación de Teams para](../concepts/design/enable-app-customization.md), [distribuir la aplicación de Microsoft Teams](../concepts/deploy-and-publish/apps-publish-overview.md)y [Cargar la aplicación en Teams](../concepts/deploy-and-publish/apps-upload.md).
* Para los conectores personalizados, consulte [crear conectores de Office 365 para Teams](../webhooks-and-connectors/how-to/connectors-creating.md).

</details>

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Usar casos y características de Teams](design/understand-use-cases.md)

## <a name="see-also"></a>Consulte también

* [Lista de comprobación de la planificación](../concepts/design/planning-checklist.md)
* [Consideraciones para la integración de Teams](../samples/integrating-web-apps.md)
* [Crear su primera aplicación de Microsoft Teams](../build-your-first-app/build-first-app-overview.md)
