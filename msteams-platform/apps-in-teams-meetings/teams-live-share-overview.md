---
title: Introducción a Live Share
author: surbhigupta
description: En este módulo, aprenderá qué es el SDK de Microsoft Live Share y los escenarios del usuario.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 3738ee1037c87f283fd31ebdaba53b57f1784bb2
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425627"
---
---

# <a name="live-share-sdk"></a>SDK de Live Share

> [!NOTE]
> El SDK de Live Share está disponible actualmente en [versión preliminar para desarrolladores públicos](../resources/dev-preview/developer-preview-intro.md). Debe formar parte de la versión preliminar del desarrollador público para que Microsoft Teams use Live Share.

Live Share es un SDK diseñado para transformar las aplicaciones de Teams en experiencias multiusuario colaborativas sin necesidad de escribir código de back-end dedicado. Live Share integra perfectamente las reuniones con [Fluid Framework](https://fluidframework.com/). Fluid Framework es una colección de bibliotecas de cliente para distribuir y sincronizar el estado compartido. Live Share proporciona el servicio gratuito [Azure Fluid Relay](/azure/azure-fluid-relay/) totalmente administrado, listo para usar y respaldado por la seguridad y la importancia a escala global de Teams.

> [!div class="nextstepaction"]
> [Introducción](teams-live-share-quick-start.md)

Live Share incluye una `TeamsFluidClient` clase para conectarse a un contenedor de fluidos especial asociado a cada reunión en unas pocas líneas de código. Además de las estructuras de datos que proporciona Fluid Framework, Live Share también admite un nuevo conjunto de clases de estructura de datos distribuidos (DDS) para simplificar la creación de aplicaciones en escenarios de reunión habituales como la reproducción multimedia compartida.

:::image type="content" source="../assets/images/teams-live-share/teams-live-share-contoso-video.gif" alt-text="Experiencia de uso compartido de vídeo con Live Share":::

## <a name="why-build-apps-with-live-share"></a>¿Por qué compilar aplicaciones con Live Share?

Crear aplicaciones colaborativas puede ser un proceso difícil, lento, costoso e incluye requisitos complejos de cumplimiento a gran escala. Los usuarios de Teams dedican una gran cantidad de tiempo a revisar el trabajo con sus compañeros de equipo, ver vídeos juntos y hacer lluvias de ideas nuevas mediante el uso compartido de la pantalla. El SDK de Live Share permite transformar una aplicación en algo más colaborativo con una inversión mínima.

Estas son algunas de las principales ventajas del SDK de Live Share:

- Administración y seguridad de sesiones sin complicaciones.
- Estructuras de datos distribuidos con y sin estado
- Extensiones multimedia para sincronizar fácilmente vídeo y audio.
- Respetar los privilegios de reunión mediante la comprobación de roles.
- Servicio gratuito y totalmente administrado con baja latencia.
- Atenuación automática inteligente de audio.

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-schematics.png" alt-text="Live Share de Teams":::

Para comprender si Live Share es adecuado para su escenario de colaboración, resulta útil comprender las diferencias entre Live Share y otros marcos de colaboración, entre los que se incluyen:

- [Sockets web](#web-sockets)
- [Azure Fluid Relay](#azure-fluid-relay)
- [Live Share](#live-share-hosted-service)

### <a name="web-sockets"></a>Sockets web

Los sockets web son una tecnología ubicua para la comunicación en tiempo real en la web y algunas aplicaciones pueden preferir usar su propio back-end de socket web personalizado. A diferencia de las API REST, los sockets web mantienen una conexión abierta entre un servidor y los clientes de una sesión.

Al igual que otros servicios de API personalizados, los requisitos suelen incluir la autenticación de sesiones, la asignación regional, el mantenimiento y la escala. Muchos escenarios de colaboración también requieren mantener el estado de sesión en el servidor, lo que requiere infraestructura de almacenamiento, soluciones de conflictos, etc.

### <a name="azure-fluid-relay"></a>Azure Fluid Relay

[Azure Fluid Relay](/azure/azure-fluid-relay/) es una oferta administrada para Fluid Framework que ayuda a los desarrolladores a crear experiencias de colaboración en tiempo real y replicar el estado entre los clientes de JavaScript conectados. Microsoft Whiteboard, Loop y OneNote son todos ejemplos de aplicaciones creadas con Fluid Framework hoy en día.

Al igual que otros servicios de Azure, Azure Fluid Relay está diseñado para adaptarse a sus necesidades de proyecto individuales con una complejidad mínima. Entre los requisitos se incluyen el desarrollo de una historia de autenticación para los contenedores fluid y el cumplimiento regional. Una vez configurados, los desarrolladores pueden centrarse en ofrecer experiencias de colaboración de alta calidad.

### <a name="live-share-hosted-service"></a>Servicio hospedado de Live Share

Live Share proporciona un servicio de Azure Fluid Relay llave en clave respaldado por la seguridad de las reuniones de Microsoft Teams. Los contenedores de Live Share están restringidos a la reunión de participantes, mantienen los requisitos de residencia de inquilinos y se puede acceder a ellos en unas pocas líneas de código de cliente.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralPresence } from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { presence: EphemeralPresence },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralPresence } from "@microsoft/live-share";
import { ContainerSchema } from "fluid-framework";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { presence: EphemeralPresence },
};
const { container } = await client.joinContainer(schema);

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
| Un asesor financiero revisa documentos PDF con los clientes antes de firmar.                  | El asesor financiero comparte el contrato PDF en la fase de reunión. Todos los asistentes pueden ver cursores y texto resaltado en el PDF, después de lo cual ambas partes firman el acuerdo.        |

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
