---
title: Introducción a Live Share
description: En este módulo, aprenderá qué es el SDK de Microsoft Live Share y los escenarios del usuario.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: dc05093f69627cc5872e25113e1ca2ca680c07c7
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142503"
---
---

# <a name="live-share-sdk"></a>SDK de Live Share

> [!Note]
> El SDK de Live Share solo está disponible actualmente en [versión preliminar pública para desarrolladores](../resources/dev-preview/developer-preview-intro.md). Debe formar parte de la versión preliminar pública para desarrolladores de Microsoft Teams para usar el SDK de Live Share.

Live Share es un SDK diseñado para transformar las aplicaciones de Teams en experiencias multiusuario colaborativas sin necesidad de escribir código de back-end dedicado. El SDK de Live Share integra fácilmente reuniones con [Fluid Framework](https://fluidframework.com/). Fluid Framework es una colección de bibliotecas de cliente para distribuir y sincronizar el estado compartido. Live Share proporciona el servicio gratuito [Azure Fluid Relay](/azure/azure-fluid-relay/) totalmente administrado, listo para usar y respaldado por la seguridad y la importancia a escala global de Teams.

> [!div class="nextstepaction"]
> [Introducción](teams-live-share-quick-start.md)

El SDK de Live Share proporciona una clase `TeamsFluidClient` para conectarse a un contenedor fluido especial asociado a cada reunión con unas pocas líneas de código. Además de las estructuras de datos que proporciona Fluid Framework, Live Share también admite un nuevo conjunto de clases de estructura de datos distribuidos (DDS) para simplificar la creación de aplicaciones en escenarios de reunión habituales como la reproducción multimedia compartida.

:::image type="content" source="../assets/images/teams-live-share/teams-live-share-contoso-video.gif" alt-text="Experiencia de uso compartido de vídeo con Live Share":::

## <a name="why-build-apps-using-the-live-share-sdk"></a>Razones para crear aplicaciones mediante el SDK de Live Share.

Crear aplicaciones colaborativas puede ser un proceso difícil, lento, costoso e incluye requisitos complejos de cumplimiento a gran escala. Los usuarios de Teams dedican una gran cantidad de tiempo a revisar el trabajo con sus compañeros de equipo, ver vídeos juntos y hacer lluvias de ideas nuevas mediante el uso compartido de la pantalla. El SDK de Live Share permite transformar una aplicación en algo más colaborativo con una inversión mínima.

Estas son algunas de las principales ventajas del SDK de Live Share:

* Administración y seguridad de sesiones sin complicaciones.
* Estructuras de datos distribuidos con y sin estado
* Extensiones multimedia para sincronizar fácilmente vídeo y audio.
* Respetar los privilegios de reunión mediante la comprobación de roles.
* Servicio gratuito y totalmente administrado con baja latencia.
* Atenuación automática inteligente de audio.

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-schematics.png" alt-text="Live Share de Teams":::

## <a name="user-scenarios"></a>Escenarios de usuario

|Escenario|Ejemplo|
| :------- | :--------------------- |
| Los usuarios y sus compañeros de trabajo han programado una reunión para presentar un primer borrador de un vídeo sobre marketing en una revisión de liderazgo que se llevará a cabo próximamente y quieren resaltar algunas secciones específicas para recibir comentarios. | Los usuarios comparten el vídeo en la escena de reunión y lo inician. El usuario va pausando el vídeo para analizar la escena según lo necesite. Los usuarios se pueden ir turnando para dibujar en distintas partes de la pantalla y enfatizar los puntos clave.|
| Imagine que es el jefe de proyecto de un equipo ágil que juega a Agile Poker con su equipo para calcular la cantidad de trabajo necesario para un próximo sprint.| Comparte una aplicación de planeamiento de Agile Poker en la escena de reunión que usa el SDK de Live Share y juega al juego de planeación hasta que el equipo llegue a un consenso.|

> [!IMPORTANT]
> Se puede acceder durante 24 horas a los datos enviados o almacenados a través del servicio Azure Fluid Relay hospedado del SDK de Live Share. Para obtener más información, consulte [Preguntas más frecuentes de Live Share](teams-live-share-faq.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Introducción](teams-live-share-quick-start.md)

## <a name="see-also"></a>Vea también

* [Repositorio de GitHub](https://github.com/microsoft/live-share-sdk)
* [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
* [Documentos de referencia del SDK multimedia de Live Share](/javascript/api/@microsoft/live-share-media/)
* [Capacidades de Live Share](teams-live-share-capabilities.md)
* [Funcionalidades de medios de Live Share](teams-live-share-media-capabilities.md)
* [Preguntas más frecuentes sobre Live Share](teams-live-share-faq.md)
* [Aplicaciones de Teams en las reuniones](teams-apps-in-meetings.md)
