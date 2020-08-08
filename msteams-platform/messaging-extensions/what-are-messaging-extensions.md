---
title: ¿Qué son las extensiones de mensajería?
author: clearab
description: Información general sobre las extensiones de mensajería en la plataforma de Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3ea9649a22ecc134e983037d1ef109be918a26b3
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587800"
---
# <a name="what-are-messaging-extensions"></a>¿Qué son las extensiones de mensajería?

Las extensiones de mensajería permiten que los usuarios interactúen con el servicio Web a través de botones y formularios en el cliente de Microsoft Teams. Pueden buscar o iniciar acciones en un sistema externo desde el área de mensaje de redacción, el cuadro de comandos o directamente desde un mensaje. A continuación, puede enviar los resultados de la interacción de vuelta al cliente de Microsoft Teams, normalmente en forma de una tarjeta con formato enriquecido.

La captura de pantalla siguiente muestra las ubicaciones desde donde se puede invocar las extensiones de mensajería.

![ubicaciones de invocación de extensiones de mensajería](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="what-kinds-of-tasks-are-they-good-for"></a>¿Para qué tipos de tareas están bien?

**Escenario:** Necesito un sistema externo para hacer algo y quiero que el resultado de la acción se envíe de nuevo a mi conversación. \
**Ejemplo:** Reserve un recurso y deje que el canal sepa el día y la hora en que se ha reservado.

**Escenario:** Necesito encontrar algo en un sistema externo y deseo compartir los resultados con mi conversación. \
**Ejemplo:**  Buscar un elemento de trabajo en Azure DevOps y compartirlo con el grupo como una tarjeta adaptable.

**Escenario:** Tengo que completar una tarea compleja que implique varios pasos (o mucha información) en un sistema externo y los resultados se deben compartir con una conversación. \
**Ejemplo:** Cree un error en el sistema de seguimiento basado en un mensaje de Microsoft Teams, asigne ese error a Bob y, a continuación, envíe una tarjeta a la conversación de conversación con los detalles del error.

## <a name="how-do-messaging-extensions-work"></a>¿Cómo funcionan las extensiones de mensajería?

Una extensión de mensajería consta de un servicio Web que hospeda y el manifiesto de la aplicación que define desde dónde se puede invocar el servicio Web en el cliente de Microsoft Teams. Aprovechan el esquema de mensajería del marco de robots y el protocolo de comunicación segura, por lo que también necesitará registrar su servicio web como bot en el marco de trabajo de bot. Aunque puede crear el servicio Web por completo a mano, le recomendamos que aproveche el [SDK de bot Framework](https://github.com/microsoft/botframework) para facilitar el trabajo con el protocolo más sencillo.

En el manifiesto de la aplicación de su aplicación de Microsoft Teams, definirá una única extensión de mensajería con un máximo de diez comandos diferentes. Cada comando define un tipo (acción o búsqueda) y las ubicaciones en el cliente a las que se puede llamar (área de mensaje de redacción, barra de comandos o mensaje). Una vez que se haya invocado, el servicio web recibirá un mensaje HTTPS con una carga JSON que incluye toda la información relevante. Responderá con una carga JSON, lo que permitirá que el cliente de Microsoft Teams sepa qué interacción se habilitará a continuación.

## <a name="types-of-messaging-extension-commands"></a>Tipos de comandos de extensión de mensajería

El comando tipo de extensión de mensajería define los elementos de la interfaz de usuario y los flujos de interacción disponibles para el servicio Web. Algunas interacciones, como la autenticación y la configuración, están disponibles para ambos tipos de comandos.

### <a name="action-commands"></a>Comandos de acción

Los comandos de acción permiten presentar a los usuarios un elemento emergente modal para recopilar o Mostrar información. Cuando envían el formulario, el servicio web puede responder insertando un mensaje en la conversación directamente o insertando un mensaje en el área de mensaje de redacción y permitiendo al usuario enviar el mensaje. Incluso puede enlazar varios formularios entre sí para flujos de trabajo más complejos.

Se pueden desencadenar desde el área de mensaje de redacción, el cuadro de comando o un mensaje. Cuando se invoca desde un mensaje, la carga útil JSON inicial que se envía a su bot incluirá el mensaje completo desde el que se invocó.

![módulo de tareas comando de acción de extensión de mensajería](~/assets/images/task-module.png)

### <a name="search-commands"></a>Comandos de búsqueda

Los comandos de búsqueda permiten a los usuarios buscar información en un sistema externo (ya sea manualmente mediante un cuadro de búsqueda o pegando un vínculo a un dominio supervisado en el área de mensajes de redacción) y, a continuación, insertan los resultados de la búsqueda en un mensaje. En el flujo de comando de búsqueda más básico, el mensaje de invocación inicial incluirá la cadena de búsqueda enviada por el usuario. Responderá con una lista de tarjetas de visita y vistas previas de tarjetas. El cliente de Microsoft Teams representará las vistas previas de las tarjetas en una lista para que el usuario final pueda seleccionarlas. Cuando el usuario selecciona una tarjeta, se insertará la tarjeta de tamaño completo en el área de mensaje de redacción.

Se pueden desencadenar desde el área de mensaje de redacción o el cuadro de comandos. A diferencia de los comandos de acción, no se pueden desencadenar desde un mensaje.

![comando de búsqueda de extensiones de mensajería](~/assets/images/search-extension.png)

### <a name="link-unfurling"></a>Apertura de vínculos

También tiene la opción de invocar el servicio cuando se pega una dirección URL en el área de mensaje de redacción. Esta funcionalidad, conocida como **unfurling de vínculos**, le permite suscribirse para recibir una llamada cuando las direcciones URL que contienen un dominio en particular se pegan en el área de mensaje de redacción. El servicio web puede "unfurl" la dirección URL en una tarjeta detallada, lo que proporciona más información que la tarjeta de vista previa del sitio web estándar. Incluso puede agregar botones para permitir que los usuarios realicen acciones inmediatamente sin dejar el cliente de Microsoft Teams.

## <a name="get-started"></a>Introducción

¿Está listo para empezar a compilar? Pruebe con uno de nuestros tutoriales:

* **C#**
  * [Extensión de mensajería con comandos basados en acciones](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [Extensión de mensajería con comandos basados en la búsqueda](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* **JavaScript**
  * [Extensión de mensajería con comandos basados en acciones](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [Extensión de mensajería con comandos basados en la búsqueda](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

## <a name="learn-more"></a>Más información

Cree una extensión de mensajería:

* [Crear una extensión de mensajería](~/messaging-extensions/how-to/create-messaging-extension.md)
* [Comando definir extensión de mensajería de la acción](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [Comando para definir la extensión de mensajería de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)
