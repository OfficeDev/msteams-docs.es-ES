---
title: Combinar bots con pestañas
description: Describe cómo usar pestañas y bots juntos
keywords: equipos bots pestañas desarrollo
ms.topic: conceptual
localization_priority: Normal
ms.date: 03/15/2018
ms.openlocfilehash: 3273369ad1122355b792dc3d429c3a4eff7e1d47
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566456"
---
# <a name="combine-bots-with-tabs"></a>Combinar bots con pestañas

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Los bots y las pestañas funcionan bien juntos y a menudo se combinan en un único servicio back-end. En esta sección se describen las prácticas recomendadas y los patrones comunes para usar pestañas y bots juntos.

## <a name="associating-user-identities-across-bot-and-tab"></a>Asociación de identidades de usuario a través de bots y pestañas

Por ejemplo: supongamos que la aplicación de pestañas utiliza un sistema de ID propietario para proteger su contenido. Supongamos que también tiene un bot que puede interactuar con el usuario. Normalmente, querrá mostrar contenido en la pestaña que es específica del usuario visual. El desafío es que el ID de usuario en su sistema es probablemente diferente del ID de usuario Microsoft Teams. Entonces, ¿cómo asocias estas dos identidades?
En general, el enfoque recomendado es iniciar sesión con el usuario con el bot utilizando el mismo sistema de identidad utilizado para proporcionar autenticación para el contenido de la pestaña. Puede implementar esto a través de la acción de inicio de sesión, que normalmente inicia sesión en el usuario a través de un flujo OAuth.

Este flujo funciona mejor si el proveedor de identidades implementa el protocolo OAuth 2.0. A continuación, puede asociar el id. Teams de usuario con las credenciales del usuario desde su propio servicio de identidad.

   ![Asociación de identidades](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>Construir vínculos profundos a pestañas en mensajes desde el bot

Es posible que desee utilizar pestañas para mostrar más contenido del que cabe dentro de una tarjeta o proporcionar una manera de completar tareas complejas de llenado de formularios mediante el lienzo de la pestaña. Por ejemplo, considere la posibilidad de navegar por el usuario a la pestaña cuando haga clic en la tarjeta desde el bot. Para que esto suceda, deberá codificar el mensaje del bot para incluir una dirección URL de [vínculo profundo,](~/concepts/build-and-test/deep-links.md) ya sea a través del marcado o como destino de la acción openUrl.

Los vínculos profundos se basan en un entityId, que es un valor opaco que se asigna a una entidad única en el sistema. Cuando se crea la pestaña, lo ideal es almacenar algún estado simple, por ejemplo, marcar en el back-end indicando que la pestaña se ha creado en el canal. Cuando el bot construye un mensaje, puede tener como destino el entityId asociado a esa pestaña.

> [!NOTE]
> en los chats personales, porque las pestañas son "estáticas" e instaladas con la aplicación, siempre se puede asumir su existencia y así construir vínculos profundos en consecuencia.

## <a name="sending-notifications-for-tab-updates"></a>Envío de notificaciones para actualizaciones de pestañas

A menudo querrá notificar al usuario final cada vez que se produzca una actualización o una acción de usuario en una pestaña. Un escenario de ejemplo es asignar una tarea o un ticket a un miembro del equipo y, a continuación, notificar a ese miembro del equipo.

Hay dos maneras de lograr este escenario:

1. Si desea notificar a todo un canal, el bot puede publicar un mensaje de forma asincrónica en el canal. No hay manera de que un bot cree proactivamente la conversación de la pestaña si no se creó con la pestaña.

2. Si solo desea notificar al destinatario o a las partes interesadas involucradas en la acción, su bot puede enviar un mensaje de chat personal al usuario. Primero debe comprobar si existe una conversación personal entre el bot y el usuario. Si no es así, puede llamar `CreateConversation` para iniciar el chat personal.

En ambos casos, utilice las notificaciones de eventos sabiamente y nunca envíe spam al usuario con actualizaciones innecesarias.
