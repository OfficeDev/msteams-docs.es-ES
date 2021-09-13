---
title: Comprender las funcionalidades de la aplicación
author: heath-hamilton
description: Teams de aplicaciones explicadas
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: a10c991c374392afca0ce793c0c34ea3fc0ca611
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157152"
---
# <a name="understand-microsoft-teams-app-capabilities"></a>Comprender Microsoft Teams funcionalidades de la aplicación

La extensibilidad o los puntos de entrada son diferentes formas en las que una aplicación puede manifestarse a un usuario. Por ejemplo, un usuario puede interactuar con una aplicación en una pestaña de lienzo para realizar una actividad o puede optar por hacer lo mismo con un bot de conversación. Las distintas funcionalidades que se usan para crear Teams aplicación te permite aumentar su ámbito de uso.

Hay varias maneras de ampliar Teams, por lo que cada aplicación es única. Algunos solo tienen una funcionalidad, como un webhook, mientras que otros tienen más de una característica para ofrecer a los usuarios varias opciones. Por ejemplo, la aplicación puede mostrar datos en  una ubicación central, es decir, la pestaña y presentar esa misma información a través de una interfaz conversacional, es decir, el **bot**.

## <a name="app-capabilities"></a>Capacidades de la aplicación

Las Teams tienen una o todas las siguientes funcionalidades principales:

* [Pestañas](../tabs/what-are-tabs.md)
* [Extensiones de mensajería](../messaging-extensions/what-are-messaging-extensions.md)
* [Bots](../bots/what-are-bots.md)
* [Webhooks y conectores](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

La aplicación también puede aprovechar las capacidades avanzadas, como la API de [Microsoft Graph para Teams](/graph/teams-concept-overview).

La siguiente ilustración te ofrece una idea de qué funcionalidades proporcionarán las características que quieras en la aplicación:

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="Mapa de la mente que ilustra Teams funcionalidades de la aplicación.":::

## <a name="always-consider-your-user"></a>Tenga en cuenta siempre al usuario

A medida que te familiarices Teams desarrollo de aplicaciones, comprendes sus fundamentos básicos. Comprende que hay más de una forma de crear determinadas características. En estos escenarios, considere cómo puede proporcionar una experiencia más nativa al usuario.
Por ejemplo, puedes recopilar la entrada del usuario en un formulario creado como una pestaña en la aplicación. También puede hacerlo con un módulo de tareas sin cambiar las vistas y interrumpir el flujo de trabajo del usuario. Es importante elegir puntos de extensión que proporcionen una desviación mínima del flujo de trabajo normal de un usuario.

## <a name="government-community-cloud-gcc"></a>Government Community Cloud (GCC)

Government Community Cloud es una copia del entorno comercial centrada en el gobierno. El Departamento de Defensa (DOD) y los contratistas federales deben cumplir con los estrictos requisitos de seguridad cibernética y cumplimiento. Para este fin, GCC-High se creó para satisfacer las necesidades de los contratistas federales y del DEPARTAMENTO de Defensa. GCC-High es una copia de la nube de DOD, pero existe en su propio entorno soberana. La nube de DOD se ha creado solo para el Departamento de Defensa.

En la tabla siguiente se Teams características y disponibilidad para GCC, GCC-High y DOD:

| Características   | GCC | GCC-High | DOD |
|-------------|---------|
| Teams propias como en las aplicaciones desarrolladas internamente | ✔️ app está habilitada si tiene GCC. | ✔️ app está habilitada si tiene GCC-High. | ✔️ app está habilitada si tiene DOD. |
| Aplicaciones de Microsoft | ✔️ aplicaciones de Microsoft compatibles con GCC | ✔️ aplicaciones de Microsoft compatibles con GCC-High | ✔️ aplicaciones de Microsoft compatibles con DOD |
| Aplicaciones 3p o de terceros | ✔️ aplicaciones de terceros están disponibles. Deshabilitado de forma predeterminada y el administrador de inquilinos usa su propia discreción para habilitarlo. | ❌ | ❌ |
| Bots | ✔️ | ❌ | ❌ |
| Aplicaciones de pestañas personalizadas o lob |  ✔️ | ✔️ | ✔️ |
| Instalación local de aplicaciones | ✔️ | ❌ | ❌ |
| Bots personalizados o lob | ✔️ | ❌ | ❌ |
| Extensiones de mensajería personalizadas | ❌ | ❌ | ❌ |
| Conectores personalizados | ❌ | ❌ | ❌ |

La siguiente lista ayuda a identificar la disponibilidad de GCC, GCC-High y DOD para las características:

* Para aplicaciones de terceros, consulta [aplicaciones web y](../samples/integrating-web-apps.md) extensibilidad de aplicaciones de [reunión.](../apps-in-teams-meetings/meeting-app-extensibility.md)
* Para los bots, vea build [your first conversational bot for Teams](../get-started/first-app-bot.md), [designing your Teams bot](../bots/design/bots.md), add [bots to Microsoft Teams apps](../resources/bot-v3/bots-overview.md)y [bots in Teams](../bots/what-are-bots.md).
* Para las aplicaciones de instalación local, consulta habilitar la aplicación [Teams](../concepts/design/enable-app-customization.md) [personalizada,](../concepts/deploy-and-publish/apps-publish-overview.md)distribuir la aplicación Microsoft Teams y Upload la aplicación en [Teams](../concepts/deploy-and-publish/apps-upload.md).
* Para los conectores personalizados, vea [create Office 365 connectors for Teams](../webhooks-and-connectors/how-to/connectors-creating.md).

## <a name="see-also"></a>Consulte también

[Crear aplicaciones para Teams](../overview.md) 
 [Crear la primera Microsoft Teams aplicación](../build-your-first-app/build-first-app-overview.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Puntos de entrada de la aplicación de Teams](../concepts/extensibility-points.md)
