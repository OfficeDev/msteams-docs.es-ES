---
title: Preguntas más frecuentes sobre Live Share
description: En este módulo, obtendrá más información sobre las preguntas más frecuentes de Live Share.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: 0c51d88ba08dea50e23b0b8eb451f84557f1f867
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189301"
---
---

# <a name="live-share-sdk-faq"></a>Preguntas más frecuentes sobre el SDK de Live Share

Obtenga respuestas a preguntas comunes al usar Live Share.<br>

<br>

<details>

<summary><b>¿Puedo usar mi propio servicio de Azure Fluid Relay?</b></summary>

Sí. Al construir la clase `TeamsFluidClient`, puede definir su propio `AzureConnectionConfig`. Live Share asocia los contenedores que cree a las reuniones, pero deberá crear su propio Azure `ITokenProvider` para firmar tokens para los contenedores y los requisitos regionales. Para más información, consulte la documentación de Azure [Fluid Relay](/azure/azure-fluid-relay/).

<br>

</details>

<details>

<summary><b>¿Cuánto tiempo son accesibles los datos almacenados en el servicio hospedado de Live Share?</b></summary>

Los datos enviados o almacenados a través de contenedores de Fluid creados por el servicio Azure Fluid Relay hospedado de Live Share son accesibles durante 24 horas. Si quiere conservar los datos más allá de 24 horas, puede reemplazar nuestro servicio Azure Fluid Relay hospedado por el suyo propio. Como alternativa, puede usar su propio proveedor de almacenamiento en paralelo al servicio hospedado de Live Share.

<br>

</details>

<details>

<summary><b>¿Qué tipos de reuniones admite Live Share?</b></summary>

Actualmente, solo se admiten reuniones programadas y todos los participantes deben estar en el calendario de la reunión. No se admiten los tipos de reunión, como llamadas uno a uno, llamadas grupales y reuniones.

<br>

</details>

<details>

<summary><b>¿Funcionará el paquete multimedia de Live Share con contenido DRM?</b></summary>

No. Actualmente, Teams no admite medios cifrados para aplicaciones de pestañas.

<br>

</details>

<details>
<summary><b>¿Cuántas personas pueden asistir a una sesión de Live Share?</b></summary>

Actualmente, Live Share admite un máximo de 100 asistentes por sesión.

<br>

</details>

## <a name="have-more-questions-or-feedback"></a>¿Tiene preguntas o comentarios?

Envíe problemas y solicitudes de características al repositorio del SDK para [SDK de Live Share](https://github.com/microsoft/live-share-sdk). Use la etiqueta `live-share` y `microsoft-teams` para publicar preguntas de procedimientos sobre el SDK en [Stack Overflow](https://stackoverflow.com/questions/tagged/live-share+microsoft-teams).

## <a name="see-also"></a>Vea también

- [Repositorio de GitHub](https://github.com/microsoft/live-share-sdk)
- [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
- [Documentos de referencia del SDK multimedia de Live Share](/javascript/api/@microsoft/live-share-media/)
- [Aplicaciones de Teams en las reuniones](teams-apps-in-meetings.md)
