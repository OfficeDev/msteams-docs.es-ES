---
title: Combinación de bots con pestañas
description: En este artículo se describe cómo usar pestañas y bots juntos.
keywords: Desarrollo de pestañas de bots de teams
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 03/15/2018
ms.openlocfilehash: 9ec2c37417d6c16edf4ead521dea91655ba11165
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123734"
---
# <a name="combine-bots-with-tabs"></a>Combinación de bots con pestañas

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Los bots y las pestañas funcionan juntos y, a menudo, se combinan en un único servicio back-end. En esta sección se describen los procedimientos recomendados y los patrones comunes para usar pestañas y bots juntos.

## <a name="associating-user-identities-across-bot-and-tab"></a>Asociación de identidades de usuario entre bots y pestañas

Por ejemplo: supongamos que la aplicación de pestaña usa un sistema de identificadores propietario para proteger su contenido. Supongamos que también tiene un bot que puede interactuar con el usuario. Normalmente, querrá mostrar contenido en la pestaña que sea específico del usuario de visualización. El desafío es que es probable que el identificador de usuario del sistema sea diferente del identificador de usuario Microsoft Teams. ¿Cómo asocia estas dos identidades?
En general, el enfoque recomendado es iniciar sesión con el bot con el mismo sistema de identidad que se usa para proporcionar autenticación para el contenido de la pestaña. Puede implementar a través de la acción de inicio de sesión, que normalmente inicia sesión en el usuario a través de un flujo de OAuth.

Este flujo funciona mejor si el proveedor de identidades implementa el protocolo OAuth 2.0. A continuación, puede asociar el identificador de usuario de Teams a las credenciales del usuario de su propio servicio de identidad.

   ![Asociar identidades](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>Creación de vínculos profundos a pestañas en mensajes del bot

Quiere usar pestañas para mostrar más contenido del que cabe dentro de una tarjeta o proporcionar una manera de completar tareas complejas de relleno de formularios mediante el lienzo de pestañas. Por ejemplo, considere la posibilidad de navegar al usuario a la pestaña cuando hace clic en la tarjeta desde el bot. Para que esto suceda, deberá codificar el mensaje del bot para incluir una dirección URL de [vínculo profundo](~/concepts/build-and-test/deep-links.md) , ya sea a través del marcado o como destino de la acción openUrl.

Los vínculos profundos se basan en un entityId, que es un valor opaco que se asigna a una entidad única del sistema. Cuando se crea la pestaña, lo ideal es almacenar un estado simple; por ejemplo, marca en el back-end que indica que la pestaña se ha creado en el canal. Cuando el bot construye un mensaje, puede tener como destino el entityId asociado a esa pestaña.

> [!NOTE]
> en los chats personales, dado que las pestañas son "estáticas" e instaladas con la aplicación, siempre se puede asumir su existencia y, por tanto, construir vínculos profundos en consecuencia.

## <a name="sending-notifications-for-tab-updates"></a>Envío de notificaciones para actualizaciones de pestañas

A menudo, querrá notificar al usuario final cada vez que se produzca una actualización o una acción de usuario en una pestaña. Un escenario de ejemplo consiste en asignar una tarea o un vale a un miembro del equipo y, a continuación, notificar a ese miembro del equipo.

Hay dos maneras de lograr este escenario:

1. Si desea notificar a un canal completo, el bot puede publicar de forma asincrónica un mensaje en el canal. No hay ninguna manera de que un bot cree proactivamente la conversación de pestaña si no se creó con la pestaña.

2. Si solo desea notificar al destinatario o a las partes interesadas implicadas en la acción, el bot puede enviar un mensaje de chat personal al usuario. Primero debe comprobar si existe una conversación personal entre el bot y el usuario. Si no es así, puede llamar `CreateConversation` a para iniciar el chat personal.

En ambos casos, use las notificaciones de eventos con prudencia y nunca envíe correo no deseado al usuario con actualizaciones innecesarias.
