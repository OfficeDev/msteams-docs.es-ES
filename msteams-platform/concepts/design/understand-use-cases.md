---
title: Descripción de los casos de uso y las características de Teams de la aplicación
author: heath-hamilton
description: En este artículo, obtendrá información sobre las funcionalidades de la aplicación Microsoft Teams, planeará la aplicación de Teams, comprenderá al usuario de la aplicación y sus necesidades, entenderá los problemas de usuario que resolvería la aplicación Teams y planeará la autenticación de usuario y su experiencia de incorporación.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: dbed78461fd39f4442c67ac7ec7523ca5cc09ba5
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104381"
---
# <a name="understand-your-use-cases"></a>Entender los casos de uso

En el marco social colaborativo de Teams, hay una amplia variedad de necesidades de usuario que puede resolver con una aplicación de Teams. Por ejemplo, una aplicación que cubre la brecha a la hora de lograr una colaboración eficaz es una buena opción.

El usuario de la aplicación y los requisitos de la aplicación son las directrices básicas que determinan todas las opciones de aplicación que se van a tomar. La creación del diseño de aplicaciones, la selección de funcionalidades, la determinación del entorno de compilación y prueba y la distribución de aplicaciones siguen los requisitos del usuario de la aplicación.

Si va a cumplir los requisitos de usuario con la aplicación, primero debe comprenderlos.

- **Comprender al usuario**:
  - Reconozca problemas de usuario e identifique las soluciones a algunos problemas comunes a los que se enfrentan los usuarios.
  - Cree su aplicación de Teams buscando la combinación adecuada de características de Teams para satisfacer las necesidades de su usuario.
  - Comprenda los casos de uso para saber cómo interactúa un usuario final con la aplicación.

- **Comprenda el problema**: vea el problema principal que debe resolver la aplicación.

- **Considere la posibilidad de integrar**: identifique las aplicaciones y los servicios que requiere la aplicación, como la autenticación, Microsoft Graph o las aplicaciones web.

## <a name="microsoft-teams-app-features"></a>Características de aplicaciones de Microsoft Teams

Hay varias maneras de ampliar Teams para que cada aplicación sea única. Oferta de características de aplicaciones de Teams:

- [Capacidades de la aplicación](#app-capabilities)
- [Ámbito de la aplicación](#app-scope)

### <a name="app-capabilities"></a>Capacidades de la aplicación

Las funcionalidades son las capacidades principales que se pueden compilar en la aplicación. También se denominan puntos de entrada o extensión porque permiten la integración y la interacción.

Las aplicaciones de Teams tienen una o todas las funcionalidades principales siguientes:

:::row:::
   :::column span="":::

#### <a name="personal-apps"></a>Aplicaciones personales

Una [aplicación personal](../../concepts/design/personal-apps.md) es un espacio dedicado o un bot para ayudar a los usuarios a centrarse en sus propias tareas o ver actividades relevantes.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-personal-apps-2021.png" alt-text="Representación conceptual de cómo son las aplicaciones personales en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

#### <a name="tabs"></a>Pestañas

Muestre el contenido basado en la web en una [pestaña](../../tabs/what-are-tabs.md) donde los usuarios puedan analizarlo y trabajar en él juntos.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-channel-chat-apps-2021.png" alt-text="Representación conceptual de cómo son las pestañas en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

#### <a name="bots"></a>Bots

Las conversaciones suelen dar lugar a la necesidad de hacer algo (generar un pedido, revisar código, comprobar el estado del vale, etc.). Un [bot](../../bots/what-are-bots.md) puede iniciar estos tipos de flujos de trabajo directamente dentro de Teams.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-bots-2021.png" alt-text="Representación conceptual de cómo son los bots en el cliente de Teams." border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

#### <a name="message-extensions"></a>Extensiones de mensajes

Con [extensiones de mensajes](../../messaging-extensions/what-are-messaging-extensions.md) puede buscar y compartir información externa. También puede actuar sobre un mensaje, como crear una incidencia de ayuda basada en el contenido de una publicación del canal.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-messaging-extensions-2021.png" alt-text="Representación conceptual del aspecto de las extensiones de mensaje en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="meeting-extensions"></a>Extensiones de reunión

Hay algunas opciones para [incorporar la aplicación a la experiencia de llamada de Teams](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md).

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-meeting-extensions-2021.png" alt-text="Representación conceptual de cómo son las extensiones de reunión en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="webhooks-and-connectors"></a>Webhooks y conectores

[Los webhooks entrantes](../../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) son una manera sencilla de enviar automáticamente notificaciones desde otra aplicación a un canal de Teams. Con [webhooks salientes](../../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), puede enviar un mensaje al servicio web con una @mención.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-connectors.png" alt-text="Representación conceptual de cómo son los conectores en el cliente de Teams." border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="microsoft-graph-for-teams"></a>Microsoft Graph para Teams

La [API de Microsoft Graph para Teams](/graph/teams-concept-overview) proporciona acceso a información sobre equipos, canales, usuarios y mensajes que le ayudan a crear o mejorar características para su aplicación.

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-graph.png" alt-text="Representación conceptual de la API de Microsoft Graph para Teams." border="false":::

   :::column-end:::
:::row-end:::

> [!NOTE]
> La tienda de Teams ha evolucionado:
>
> Anteriormente, las aplicaciones LOB se actualizaban seleccionando los puntos suspensivos en el icono. Con la experiencia actualizada de la tienda de Teams, ahora puede actualizar las aplicaciones LOB iniciando sesión en el [Centro de administración de Teams](https://admin.teams.microsoft.com).

### <a name="app-scope"></a>Ámbito de la aplicación

La aplicación puede tener uno de los siguientes ámbitos:

- **Experiencia de aplicación personal**: una aplicación personal es un bot o un espacio dedicado para ayudar a los usuarios a centrarse en sus propias tareas o ver actividades importantes para ellos.
- **Experiencia de aplicación compartida**: el equipo, el canal y el chat son espacios de colaboración. Las aplicaciones en estos contextos están disponibles para todos los usuarios de ese espacio. Normalmente, los espacios de colaboración se centran en los flujos de trabajo para las interacciones de la aplicación o para desbloquear nuevas interacciones sociales.

Una aplicación puede existir en distintos ámbitos. Por ejemplo:

- La aplicación puede mostrar datos en una ubicación compartida central, es decir, una pestaña.
- También puede presentar esa misma información a través de una interfaz conversacional personal, es decir, un bot.

Un usuario puede interactuar con una aplicación en una pestaña de lienzo para realizar una actividad o puede optar por hacer lo mismo con un bot de conversación.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Asignar los casos de uso](../../concepts/design/map-use-cases.md)

## <a name="see-also"></a>Consulte también

[Integrar las funcionalidades del dispositivo](~/concepts/device-capabilities/device-capabilities-overview.md)
