---
title: Combinar bots con pestañas
description: Describe cómo usar fichas y bots juntos
keywords: desarrollo de pestañas de Microsoft Teams
ms.date: 03/15/2018
ms.openlocfilehash: 59ae8bc01f82c70dd7ea6869cb870e26acae1293
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676005"
---
# <a name="combine-bots-with-tabs"></a>Combinar bots con pestañas

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Los bots y las pestañas funcionan bien juntos y, a menudo, se combinan en un único servicio back-end. En esta sección se describen los procedimientos recomendados y los patrones comunes para usar fichas y bots juntos.

## <a name="associating-user-identities-across-bot-and-tab"></a>Asociación de identidades de usuario en el bot y la ficha

Por ejemplo: Supongamos que la aplicación de pestaña usa un sistema de identificación de propietario para proteger su contenido. Supongamos que también tiene un bot que puede interactuar con el usuario. Normalmente, querrá Mostrar contenido en la pestaña que es específico del usuario de visualización. El desafío es que el identificador de usuario del sistema es probablemente diferente del identificador de usuario de Microsoft Teams. ¿Cómo se asocian estas dos identidades?
En general, el enfoque recomendado es iniciar sesión del usuario con el bot usando el mismo sistema de identidad usado para proporcionar autenticación para el contenido de la pestaña. Puede implementar esto mediante la acción de inicio de sesión, que normalmente se registra en el usuario a través de un flujo de OAuth.

Este flujo funciona mejor si el proveedor de identidades implementa el protocolo OAuth 2,0. A continuación, puede asociar el identificador de usuario de Teams a las credenciales del usuario desde su propio servicio de identidad.

   ![Asociar identidades](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>Creación de vínculos profundos a pestañas en los mensajes de su bot

Es posible que desee usar pestañas para mostrar más contenido del que cabe dentro de una tarjeta o proporcionar una forma de completar tareas complejas de rellenado de formularios mediante el lienzo de tabulación. Por ejemplo, considere la posibilidad de navegar por el usuario a la pestaña cuando haga clic en la tarjeta de su bot. Para que esto suceda, deberá codificar el mensaje del bot para incluir una dirección URL de [vínculo profundo](~/concepts/build-and-test/deep-links.md) , ya sea mediante marcado o como destino de la acción openUrl.

Los vínculos profundos dependen de una entityId, que es un valor opaco que se asigna a una entidad única en el sistema. Cuando se crea la pestaña, lo ideal es almacenar un estado sencillo (por ejemplo, indicador) en el back-end en el que se indica que la pestaña se ha creado en el canal. Cuando el bot construye un mensaje, puede dirigirse al entityId asociado a esa ficha.

**Nota:** en chats personales, dado que las pestañas son "estáticas" y se instalan con la aplicación, siempre puede suponer que existe y, por lo tanto, crear vínculos profundos en consecuencia.

## <a name="sending-notifications-for-tab-updates"></a>Envío de notificaciones de actualizaciones de pestañas

A menudo, deseará notificar al usuario final siempre que se produzca una actualización o una acción del usuario en una pestaña. Un escenario de ejemplo consiste en asignar una tarea o un tíquet a un compañero integrante del equipo y, a continuación, notificar a ese miembro del equipo.

Hay dos formas de lograr este escenario:

1. Si desea notificar a todo el canal, su bot puede enviar un mensaje al canal de forma asincrónica. No hay forma de que un bot cree proactivamente la conversación de pestaña si no se creó con la ficha.

2. Si sólo desea notificar al destinatario o a las partes interesadas implicadas en la acción, el bot puede enviar un mensaje de chat personal al usuario. Primero debe comprobar si existe una conversación personal entre su bot y el usuario. Si no es así, puede `CreateConversation` llamar para iniciar el chat personal.

En ambos casos, use las notificaciones de eventos de manera inteligente y nunca el usuario no tiene actualizaciones innecesarias.
