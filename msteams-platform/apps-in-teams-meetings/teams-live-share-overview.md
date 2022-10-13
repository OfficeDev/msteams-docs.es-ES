---
title: Introducción a Live Share
author: surbhigupta
description: En este módulo, aprenderá qué es el SDK de Microsoft Live Share y los escenarios del usuario.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: c242faa57809bb967a29b7ab224e6cc0e859247b
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560557"
---
---

# <a name="live-share-sdk"></a>SDK de Live Share

> [!VIDEO https://www.youtube.com/embed/971YIvosuUk]

Live Share es un SDK diseñado para transformar las aplicaciones de Teams en experiencias multiusuario colaborativas sin necesidad de escribir código de back-end dedicado. Con Live Share, los usuarios pueden co-ver, co-crear y editar conjuntamente durante las reuniones.

A veces, el uso compartido de pantalla no es suficiente, por lo que Microsoft ha creado herramientas como PowerPoint Live y Whiteboard directamente en Teams. Al llevar la aplicación web directamente a la fase central de la interfaz de reunión, los usuarios pueden colaborar sin problemas durante reuniones y llamadas.

> [!div class="nextstepaction"]
> [Introducción](teams-live-share-quick-start.md)

## <a name="feature-overview"></a>Información general sobre la característica

Live Share tiene tres paquetes que admiten escenarios de colaboración ilimitados. Estos paquetes exponen un conjunto de estructuras de datos distribuidas (DDS), incluidos los bloques de creación primitivos y los escenarios de clave de giro.

Live Share integra perfectamente las reuniones con [Fluid Framework](https://fluidframework.com/). Fluid Framework es una colección de bibliotecas de cliente para distribuir y sincronizar el estado compartido. Live Share proporciona el servicio gratuito [Azure Fluid Relay](/azure/azure-fluid-relay/) totalmente administrado, listo para usar y respaldado por la seguridad y la importancia a escala global de Teams.

### <a name="live-share-core"></a>Núcleo de Live Share

Live Share permite conectarse a un contenedor fluido especial asociado a cada reunión en unas pocas líneas de código. Además de las estructuras de datos proporcionadas por Fluid Framework, Live Share también admite un nuevo conjunto de clases DDS para simplificar la sincronización del estado de la aplicación en reuniones.

Entre las características admitidas por el paquete principal de Live Share se incluyen:

- Únase a la sesión de Live Share de una reunión con `LiveShareClient`.
- Realice un seguimiento de la presencia de la reunión y sincronice los metadatos de usuario con `LivePresence`.
- Envíe eventos en tiempo real a otros clientes de la sesión con `LiveEvent`.
- Coordine el estado de la aplicación que desaparece cuando los usuarios abandonan la sesión con `LiveState`.
- Sincronice un temporizador de cuenta atrás con `LiveTimer`.
- Aproveche cualquier característica de Fluid Framework, como `SharedMap` y `SharedString`.

Puede encontrar más información sobre este paquete en la [página de funcionalidades principales](./teams-live-share-capabilities.md).

### <a name="live-share-media"></a>Contenido multimedia de Live Share

:::image type="content" source="../assets/images/teams-live-share/teams-live-share-contoso-video.gif" alt-text="Captura de pantalla que muestra un ejemplo de experiencia de uso compartido de vídeo de Live Share.":::

El vídeo y el audio forman parte fundamental del mundo moderno y de los lugares de trabajo. Live Share Media permite la **sincronización de medios** para cualquier reproductor multimedia con solo unas pocas líneas de código. Al sincronizar los medios en la capa de controles de transporte y estado del reproductor, puede atribuir vistas individualmente, a la vez que proporciona la máxima calidad posible disponible a través de la aplicación. Dado que Microsoft no retransmite de nuevo el contenido multimedia, los requisitos de licencia y acceso se mantienen intactos.

Entre las características admitidas por los medios de Live Share se incluyen:

- Sincronice el estado del reproductor multimedia y realice un seguimiento con `MediaPlayerSynchronizer`.
- Ajustes inteligentes en el volumen multimedia a medida que los usuarios hablan durante la reunión.
- Limitar qué usuarios pueden modificar el estado del reproductor.
- Suspende y reanude la sincronización de medios sobre la marcha o en los puntos de espera programados.

Puede encontrar más información sobre este paquete en la [página multimedia de Live Share](./teams-live-share-media-capabilities.md).

> [!NOTE]
> Live Share no retransmite de nuevo el contenido multimedia. Está diseñado para su uso con reproductores web incrustados, como HTML5 `<video>` o Azure Media Player.

### <a name="live-share-canvas"></a>Lienzo de Live Share

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-schematics.png" alt-text="Capturas de pantalla que muestran un ejemplo de varios usuarios dibujando en un lienzo durante una reunión.":::

Al colaborar en reuniones, es esencial que los usuarios puedan señalar y enfatizar el contenido en la pantalla. Live Share Canvas facilita la incorporación de entrada manuscrita, punteros láser y cursores a la aplicación para una colaboración perfecta.

Entre las características admitidas por el lienzo de Live Share se incluyen:

- Agregue una colaboración `<canvas>` a la aplicación con `LiveCanvas`.
- Transmita ideas mediante el lápiz, el resaltador, la línea y las herramientas de flecha.
- Presente de forma eficaz con el puntero láser.
- Siga junto con los cursores del mouse en tiempo real.
- Configure los valores de los dispositivos variables y los estados de vista.
- Use entradas de mouse, táctiles y de lápiz totalmente compatibles.

Puede encontrar más información sobre este paquete en la [página lienzo de Live Share](./teams-live-share-canvas.md).

## <a name="why-build-apps-with-live-share"></a>¿Por qué compilar aplicaciones con Live Share?

Crear aplicaciones colaborativas puede ser un proceso difícil, lento, costoso e incluye requisitos complejos de cumplimiento a gran escala. Los usuarios de Teams dedican una gran cantidad de tiempo a revisar el trabajo con sus compañeros de equipo, ver vídeos juntos y hacer lluvias de ideas nuevas mediante el uso compartido de la pantalla. El SDK de Live Share permite transformar una aplicación en algo más colaborativo con una inversión mínima.

Estas son algunas de las principales ventajas del SDK de Live Share:

- Administración y seguridad de sesiones sin complicaciones.
- Estructuras de datos distribuidos con y sin estado
- Extensiones multimedia para sincronizar fácilmente vídeo y audio.
- Entrada manuscrita llave en mano, punteros láser y cursores.
- Respetar los privilegios de reunión mediante la comprobación de roles.
- Servicio gratuito y totalmente administrado con baja latencia.

Para comprender si Live Share es adecuado para su escenario de colaboración, resulta útil comprender las diferencias entre Live Share y otros marcos de colaboración, entre los que se incluyen:

- [Sockets web](#web-sockets)
- [Azure Fluid Relay](#azure-fluid-relay)
- [Live Share](#live-share-hosted-service)

### <a name="web-sockets"></a>Sockets web

Los sockets web son una tecnología ubicua para la comunicación en tiempo real en la web y algunas aplicaciones pueden preferir usar su propio back-end de socket web personalizado. A diferencia de las API REST, los sockets web mantienen una conexión abierta entre un servidor y los clientes de una sesión.

Al igual que otros servicios de API personalizados, los requisitos suelen incluir la autenticación de sesiones, la asignación regional, el mantenimiento y la escala. Muchos escenarios de colaboración también requieren mantener el estado de sesión en el servidor, lo que requiere infraestructura de almacenamiento, soluciones de conflictos, etc.

Al usar Live Share, obtiene toda la potencia de los sockets web sin ninguna sobrecarga.

### <a name="azure-fluid-relay"></a>Azure Fluid Relay

[Azure Fluid Relay](/azure/azure-fluid-relay/) es una oferta administrada para Fluid Framework que ayuda a los desarrolladores a crear experiencias de colaboración en tiempo real y replicar el estado entre los clientes de JavaScript conectados. Microsoft Whiteboard, Loop y OneNote son todos ejemplos de aplicaciones creadas con Fluid Framework hoy en día.

Al igual que otros servicios de Azure, Azure Fluid Relay está diseñado para adaptarse a sus necesidades de proyecto individuales con una complejidad mínima. Entre los requisitos se incluyen el desarrollo de una historia de autenticación para los contenedores fluid y el cumplimiento regional. Una vez configurados, los desarrolladores pueden centrarse en ofrecer experiencias de colaboración de alta calidad.

### <a name="live-share-hosted-service"></a>Servicio hospedado de Live Share

Live Share proporciona un servicio de Azure Fluid Relay llave en clave respaldado por la seguridad de las reuniones de Microsoft Teams. Los contenedores de Live Share están restringidos a la reunión de participantes, mantienen los requisitos de residencia de inquilinos y se puede acceder a ellos en unas pocas líneas de código de cliente.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, LivePresence } from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { presence: LivePresence },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, LivePresence } from "@microsoft/live-share";
import { ContainerSchema } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { presence: LivePresence },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

---

> [!IMPORTANT]
> Los datos enviados o almacenados a través del servicio Azure Fluid Relay hospedado del SDK de Live Share son accesibles hasta 24 horas. Para obtener más información, consulte [Preguntas más frecuentes de Live Share](teams-live-share-faq.md).

#### <a name="using-a-custom-azure-fluid-relay-service"></a>Uso de un servicio de Azure Fluid Relay personalizado

Aunque a la mayoría le parece preferible usar nuestro servicio hospedado gratuito, todavía hay situaciones en las que resulta beneficioso usar su propio servicio De Azure Fluid Relay para la aplicación Live Share.

Considere la posibilidad de usar un servicio personalizado si:

- Requerir almacenamiento de datos en contenedores Fluid más allá de la duración de una reunión.
- Transmitir datos confidenciales a través del servicio que requiere una directiva de seguridad personalizada.
- Desarrolle características a través de Fluid Framework, por ejemplo, `SharedMap`, para la aplicación fuera de Teams.

Para obtener más información, consulte la [guía de procedimientos del](./teams-live-share-how-to/how-to-custom-azure-fluid-relay.md) servicio Azure Fluid Relay personalizada.

## <a name="user-scenarios"></a>Escenarios de usuario

| Escenario                                                                                | Ejemplo                                                                                                                                                                                            |
| :-------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Durante una revisión de marketing, un usuario quiere recopilar comentarios sobre su última edición de vídeo. | El usuario comparte el vídeo en la fase de reunión e inicia el vídeo. Según sea necesario, el usuario pausa el vídeo para analizar la escena y los participantes dibujan partes de la pantalla para enfatizar los puntos clave. |
| Un jefe de proyecto juega Agile Poker con su equipo durante la planificación.                    | El administrador comparte una aplicación agile poker en la fase de reunión que permite jugar al juego de planificación hasta que el equipo tenga consenso.                                                                        |
| Un asesor financiero revisa documentos PDF con los clientes antes de firmar.                  | El asesor financiero comparte el contrato PDF en la fase de reunión. Todos los asistentes pueden ver los cursores del otro y el texto resaltado en el PDF, después de lo cual ambas partes firman el acuerdo.        |

> [!IMPORTANT]
> Live Share tiene licencia bajo la [licencia del SDK de Microsoft Live Share](https://github.com/microsoft/live-share-sdk/blob/main/LICENSE). Para usar estas funcionalidades en la aplicación, primero debe leer y aceptar estos términos.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Introducción](teams-live-share-quick-start.md)

## <a name="see-also"></a>Vea también

- [Repositorio de GitHub](https://github.com/microsoft/live-share-sdk)
- [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
- [Documentos de referencia del SDK multimedia de Live Share](/javascript/api/@microsoft/live-share-media/)
- [Capacidades de Live Share](teams-live-share-capabilities.md)
- [Funcionalidades de medios de Live Share](teams-live-share-media-capabilities.md)
- [Preguntas más frecuentes sobre Live Share](teams-live-share-faq.md)
- [Aplicaciones de Teams en las reuniones](teams-apps-in-meetings.md)
