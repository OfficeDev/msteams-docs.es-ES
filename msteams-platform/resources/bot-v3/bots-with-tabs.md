---
title: Combinar bots con pestañas
description: Describe cómo usar pestañas y bots juntos
keywords: desarrollo de pestañas de bots de teams
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

Bots and tabs work well together, and are often combined into a single back-end service. En esta sección se describen los procedimientos recomendados y los patrones comunes para usar juntos pestañas y bots.

## <a name="associating-user-identities-across-bot-and-tab"></a>Asociación de identidades de usuario entre bot y pestaña

Por ejemplo: supongamos que la aplicación de pestaña usa un sistema de id. de propietario para proteger su contenido. Supongamos que también tiene un bot que puede interactuar con el usuario. Normalmente, querrás mostrar contenido en la pestaña que es específico del usuario de visualización. El desafío es que el identificador de usuario en el sistema es probablemente diferente del Microsoft Teams de usuario. Entonces, ¿cómo asocia estas dos identidades?
En general, el enfoque recomendado es iniciar sesión con el bot con el mismo sistema de identidad usado para proporcionar autenticación para el contenido de la pestaña. Puede implementar esto a través de la acción de inicio de sesión, que normalmente inicia sesión en el usuario a través de un flujo de OAuth.

Este flujo funciona mejor si el proveedor de identidades implementa el protocolo OAuth 2.0. A continuación, puede asociar el Teams de usuario con las credenciales del usuario desde su propio servicio de identidad.

   ![Asociación de identidades](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>Crear vínculos profundos a pestañas en mensajes desde el bot

Es posible que desee usar pestañas para mostrar más contenido del que cabe dentro de una tarjeta, o proporcionar una forma de completar tareas complejas de rellenado de formularios con el lienzo de pestañas. Por ejemplo, considere la posibilidad de navegar al usuario a la pestaña cuando haga clic en la tarjeta desde el bot. Para que esto suceda, tendrás que codificar el mensaje del bot para incluir una dirección [URL](~/concepts/build-and-test/deep-links.md) de vínculo profundo, ya sea a través del marcado o como el destino de la acción openUrl.

Los vínculos profundos dependen de un entityId, que es un valor opaco que se asigna a una entidad única en el sistema. Cuando se crea la pestaña, lo ideal es almacenar un estado sencillo, por ejemplo, marcar en el back-end que indica que la pestaña se ha creado en el canal. Cuando el bot crea un mensaje, puede dirigirse a la entidadId asociada a esa pestaña.

> [!NOTE]
> en chats personales, dado que las pestañas son "estáticas" e instaladas con la aplicación, siempre puedes asumir su existencia y, por lo tanto, crear vínculos profundos en consecuencia.

## <a name="sending-notifications-for-tab-updates"></a>Enviar notificaciones para actualizaciones de pestañas

A menudo, querrás notificar al usuario final siempre que se produzca una actualización o una acción de usuario en una pestaña. Un escenario de ejemplo es asignar una tarea o vale a un miembro del equipo y, a continuación, notificar a ese miembro del equipo.

Hay dos formas de lograr este escenario:

1. Si desea notificar a todo un canal, el bot puede publicar un mensaje de forma asincrónica en el canal. No hay forma de que un bot cree proactivamente la conversación de tabulación si no se creó con la pestaña.

2. Si solo desea notificar al destinatario o a las partes interesadas implicadas en la acción, el bot puede enviar un mensaje de chat personal al usuario. Primero debe comprobar si existe una conversación personal entre el bot y el usuario. Si no es así, puedes llamar `CreateConversation` para iniciar el chat personal.

En ambos casos, usa las notificaciones de eventos con prudencia y nunca envías correo no deseado al usuario con actualizaciones innecesarias.
