---
title: Extensiones de mensajería
author: clearab
description: Información general sobre las extensiones de mensajería en la plataforma de Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2d82202c72584927fc705813151d91510a7f12c9
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696750"
---
# <a name="messaging-extensions"></a>Extensiones de mensajería

Las extensiones de mensajería permiten a los usuarios interactuar con el servicio web a través de botones y formularios en el cliente de Microsoft Teams. Pueden buscar o iniciar acciones en un sistema externo desde el área del mensaje de redacción, el cuadro de comandos o directamente desde un mensaje. Puedes devolver los resultados de esa interacción al cliente de Microsoft Teams en forma de tarjeta con un formato enriquecido. En este documento se proporciona información general sobre la extensión de mensajería, las tareas realizadas en diferentes escenarios, el trabajo de la extensión de mensajería, la acción y los comandos de búsqueda y la desamuesación de vínculos.

La siguiente imagen muestra las ubicaciones desde las que se invocan las extensiones de mensajería:

![ubicaciones de invocación de extensión de mensajería](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="scenarios-where-messaging-extensions-are-used"></a>Escenarios en los que se usan extensiones de mensajería

| Escenario | Ejemplo |
|:-----------------|:-----------------|
|Desea que algún sistema externo realice una acción y que el resultado de la acción se envíe de vuelta a la conversación.|Reserve un recurso y permita que el canal conozca la franja horaria reservada.|
|Desea encontrar algo en un sistema externo y compartir los resultados con la conversación.|Busque un elemento de trabajo en Azure DevOps y compártelo con el grupo como una tarjeta adaptable.|
|Desea completar una tarea compleja que incluya varios pasos o mucha información en un sistema externo y compartir los resultados con una conversación.|Crea un error en el sistema de seguimiento basado en un mensaje de Teams, asigna ese error a Bob y envía una tarjeta al hilo de conversación con los detalles del error.|

## <a name="understand-how-messaging-extensions-work"></a>Comprender cómo funcionan las extensiones de mensajería

Una extensión de mensajería consta de un servicio web que hospeda y un manifiesto de aplicación, que define desde dónde se invoca el servicio web en el cliente de Microsoft Teams. El servicio web aprovecha el esquema de mensajería de Bot Framework y el protocolo de comunicación seguro, por lo que debe registrar el servicio web como bot en Bot Framework. 

> [!NOTE]
> Aunque puede crear el servicio web manualmente, use [bot Framework SDK](https://github.com/microsoft/botframework) para trabajar con el protocolo.

En el manifiesto de la aplicación para la aplicación de Microsoft Teams, se define una sola extensión de mensajería con hasta diez comandos diferentes. Cada comando define un tipo, como acción o búsqueda, y las ubicaciones del cliente desde donde se invoca. Las ubicaciones de invocación son área de mensaje de redacción, barra de comandos y mensaje. Al invocar, el servicio web recibe un mensaje HTTPS con una carga JSON que incluye toda la información relevante. Responda con una carga JSON, lo que permite al cliente de Teams conocer la siguiente interacción que se habilitará. 

## <a name="types-of-messaging-extension-commands"></a>Tipos de comandos de extensión de mensajería

Hay dos tipos de comandos de extensión de mensajería, comando de acción y comando de búsqueda. El tipo de comando de extensión de mensajería define los elementos de la interfaz de usuario y los flujos de interacción disponibles para el servicio web. Algunas interacciones, como la autenticación y la configuración, están disponibles para ambos tipos de comandos.

### <a name="action-commands"></a>Comandos de acción

Los comandos action se usan para presentar a los usuarios un elemento emergente modal para recopilar o mostrar información. Cuando el usuario envía el formulario, el servicio web responde insertando un mensaje en la conversación directamente o insertando un mensaje en el área del mensaje de redacción. Después, el usuario puede enviar el mensaje. Puede encadenar varios formularios para flujos de trabajo más complejos.

Los comandos de acción se desencadenan desde el área del mensaje de redacción, el cuadro de comandos o desde un mensaje. Cuando se invoca el comando desde un mensaje, la carga JSON inicial enviada al bot incluye todo el mensaje desde el que se invocó. En la siguiente imagen se muestra el módulo de tareas de comando de acción de extensión de mensajería: módulo de tareas de comando de acción de extensión ![ de mensajería](~/assets/images/task-module.png)

### <a name="search-commands"></a>Comandos de búsqueda

Los comandos de búsqueda permiten a los usuarios buscar información en un sistema externo manualmente a través de un cuadro de búsqueda o pegando un vínculo a un dominio supervisado en el área del mensaje de redacción e insertar los resultados de la búsqueda en un mensaje. En el flujo de comandos de búsqueda más básico, el mensaje de invocación inicial incluye la cadena de búsqueda que el usuario envió. Responderá con una lista de tarjetas y vistas previas de tarjetas. El cliente de Teams representa una lista de vistas previas de tarjeta para el usuario. Cuando el usuario selecciona una tarjeta de la lista, la tarjeta de tamaño completo se inserta en el área del mensaje de redacción.

Las tarjetas se desencadenan desde el área del mensaje de redacción o el cuadro de comando y no se desencadenan desde un mensaje. No se pueden desencadenar desde un mensaje.
En la siguiente imagen se muestra el módulo de tareas de comando de búsqueda de extensión de mensajería:

![comando de búsqueda de extensión de mensajería](~/assets/images/search-extension.png)

> [!NOTE]
> Para obtener más información sobre las tarjetas, vea [what are cards](../task-modules-and-cards/what-are-cards.md).

## <a name="link-unfurling"></a>Apertura de vínculos

Se invoca un servicio web cuando se pega una dirección URL en el área del mensaje de redacción. Esta funcionalidad se conoce como desenlaznado de vínculos. Puede suscribirse para recibir una invocación cuando las direcciones URL que contienen un dominio determinado se pegan en el área del mensaje de redacción. El servicio web puede "desplegar" la dirección URL en una tarjeta detallada, lo que proporciona más información que la tarjeta de vista previa del sitio web estándar. Puedes agregar botones para permitir que los usuarios tomen medidas inmediatamente sin salir del cliente de Microsoft Teams.
Las siguientes imágenes muestran la característica de desamuestración de vínculos cuando se pega un vínculo en la extensión de mensajería:
 
![vínculo unfurl](../assets/images/messaging-extension/unfurl-link.png)

![desafusado de vínculos](../assets/images/messaging-extension/link-unfurl.gif)


## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Crear una extensión de mensajería](../build-your-first-app/build-messaging-extension.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Definir comando de extensión de mensajería de acción](~/messaging-extensions/how-to/action-commands/define-action-command.md)

> [!div class="nextstepaction"]
> [Definir comando de extensión de mensajería de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)
