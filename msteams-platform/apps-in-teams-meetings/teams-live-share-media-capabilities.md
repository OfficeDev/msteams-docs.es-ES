---
title: Capacidades multimedia de Live Share
author: surbhigupta
description: En este módulo, obtendrá más información sobre la capacidades multimedia de Live Share, además de las suspensiones y puntos de espera, la atenuación de audio y la sincronización de vídeo y audio.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 0ab0bf436ce3ca27b55a68ea2c80f1451f4d967e
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425589"
---
# <a name="live-share-media-capabilities"></a>Capacidades multimedia de Live Share

:::image type="content" source="../assets/images/teams-live-share/live-share-media-capabilities-docs-feature-1.png" alt-text="Sincronización de medios de Teams Live Share":::

El vídeo y el audio forman parte fundamental del mundo moderno y de los lugares de trabajo. Hemos escuchado comentarios muy amplios sobre qué podemos hacer más para aumentar la calidad, la accesibilidad y proteger las licencias para ver vídeos juntos en reuniones.

El SDK de Live Share permite una **sincronización de medios** sólida para cualquier html `<video>` y `<audio>` elemento con solo unas pocas líneas de código. Al sincronizar medios en la capa de controles de transporte y estado del reproductor, podrá atribuir vistas y licencias individualmente, a la vez que proporciona la mayor calidad posible disponible a través de la aplicación.

## <a name="install"></a>Instalar

Para agregar la versión más reciente del SDK a la aplicación mediante npm:

```bash
npm install @microsoft/live-share --save
npm install @microsoft/live-share-media --save
```

O

Para agregar la versión más reciente del SDK a la aplicación mediante [Yarn](https://yarnpkg.com/):

```bash
yarn add @microsoft/live-share
yarn add @microsoft/live-share-media
```

## <a name="media-sync-overview"></a>Introducción a la sincronización multimedia

El SDK de Live Share tiene dos clases principales relacionadas con la sincronización de medios:

| Clases                                                                                        | Descripción                                                                                                                                       |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [EphemeralMediaSession](/javascript/api/@microsoft/live-share-media/ephemeralmediasession)     | Objeto efímero personalizado diseñado para coordinar los controles de transporte multimedia y el estado de reproducción en secuencias de medios independientes.                          |
| [MediaPlayerSynchronizer](/javascript/api/@microsoft/live-share-media/mediaplayersynchronizer) | Sincroniza cualquier objeto que implemente la `IMediaPlayer` interfaz , incluidos HTML5 `<video>` y `<audio>` , mediante `EphemeralMediaSession`. |

Ejemplo:

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
</body>
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient, UserMeetingRole } from "@microsoft/live-share";
import { EphemeralMediaSession } from "@microsoft/live-share-media";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Setup the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { mediaSession: EphemeralMediaSession },
};
const { container } = await client.joinContainer(schema);
const { mediaSession } = container.initialObjects;

// Get the player from your document and create synchronizer
const player = document.getElementById("player");
const synchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
await mediaSession.initialize(allowedRoles);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient, UserMeetingRole } from "@microsoft/live-share";
import { EphemeralMediaSession, IMediaPlayer, MediaPlayerSynchronizer } from "@microsoft/live-share-media";
import { ContainerSchema } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { mediaSession: EphemeralMediaSession },
};
const { container } = await client.joinContainer(schema);
const mediaSession = container.initialObjects.mediaSession as EphemeralMediaSession;

// Get the player from your document and create synchronizer
const player: IMediaPlayer = document.getElementById("player") as HTMLVideoElement;
const synchronizer: MediaPlayerSynchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles: UserMeetingRole[] = [UserMeetingRole.organizer, UserMeetingRole.presenter];
await mediaSession.initialize(allowedRoles);
```

---

`EphemeralMediaSession` escucha automáticamente los cambios en el estado de reproducción del grupo. `MediaPlayerSynchronizer` escucha los cambios de estado emitidos por `EphemeralMediaSession` y los aplica al objeto proporcionado `IMediaPlayer` , como un elemento HTML5 `<video>` o `<audio>` . Para evitar los cambios de estado de reproducción que un usuario no inició intencionadamente, como un evento de búfer, deberemos llamar a los controles de transporte a través del sincronizador, en lugar de directamente a través del reproductor.

Ejemplo:

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
  <div class="player-controls">
    <button id="play-button">Play</button>
    <button id="pause-button">Pause</button>
    <button id="restart-button">Restart</button>
    <button id="change-track-button">Change track</button>
  </div>
</body>
```

```javascript
// ...

document.getElementById("play-button").onclick = () => {
  synchronizer.play();
};

document.getElementById("pause-button").onclick = () => {
  synchronizer.pause();
};

document.getElementById("restart-button").onclick = () => {
  synchronizer.seekTo(0);
};

document.getElementById("change-track-button").onclick = () => {
  synchronizer.setTrack({
    trackIdentifier: "SOME_OTHER_VIDEO_SRC",
  });
};
```

> [!NOTE]
> Aunque puede usar el `EphemeralMediaSession` objeto para sincronizar los medios manualmente, por lo general se recomienda usar `MediaPlayerSynchronizer`. En función del reproductor que use en la aplicación, es posible que deba crear una corrección de compatibilidad de delegado para que la interfaz del reproductor web coincida con la interfaz [IMediaPlayer](/javascript/api/@microsoft/live-share-media/imediaplayer) .

## <a name="suspensions-and-wait-points"></a>Suspensiones y puntos de espera

:::image type="content" source="../assets/images/teams-live-share/live-share-media-out-of-sync.png" alt-text="Captura de pantalla que muestra una sincronización de suspensión con el moderador.":::

Si desea suspender temporalmente la sincronización del objeto `EphemeralMediaSession`, puede usar suspensiones. Un objeto [MediaSessionCoordinatorSuspension](/javascript/api/@microsoft/live-share-media/ephemeralmediasessioncoordinatorsuspension) es local de forma predeterminada, lo que podría ser útil en los casos en los que un usuario pueda querer ponerse al día con algo que se perdió, tomarse un descanso, etc. Si el usuario finaliza la suspensión, la sincronización se reanudará automáticamente.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
// Suspend the media session coordinator
const suspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { MediaSessionCoordinatorSuspension } from "@microsoft/live-share-media";

// Suspend the media session coordinator
const suspension: MediaSessionCoordinatorSuspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

---

Al iniciar una suspensión, también se puede incluir un parámetro opcional [CoordinationWaitPoint](/javascript/api/@microsoft/live-share-media/coordinationwaitpoint), que permite a los usuarios definir las marcas de tiempo en las que se deba producir una suspensión para todos los usuarios. La sincronización no se reanudará hasta que todos los usuarios hayan finalizado la suspensión de ese punto de espera.

Estos son algunos escenarios en los que los puntos de espera son especialmente útiles:

- Agregar un cuestionario o una encuesta en determinados puntos del vídeo.
- Esperando a que todos carguen adecuadamente un vídeo antes de que se inicie o mientras se almacena en búfer.
- Permitir que un moderador elija puntos en el vídeo para la discusión en grupo.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
// Suspend the media session coordinator
const waitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension(waitPoint);
// End the suspension when the user readies up
document.getElementById("ready-up-button").onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { MediaSessionCoordinatorSuspension, CoordinationWaitPoint } from "@microsoft/live-share-media";

// Suspend the media session coordinator
const waitPoint: CoordinationWaitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension(waitPoint);

// End the suspension when the user readies up
document.getElementById("ready-up-button")!.onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

---

## <a name="audio-ducking"></a>Atenuación de audio

El SDK de Live Share admite la atenuación de audio inteligente. Puede usar la característica _experimental_ en la aplicación agregando lo siguiente al código:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import * as microsoftTeams from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer;
microsoftTeams.meeting.registerSpeakingStateChangeHandler((speakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    // If someone in the meeting starts speaking, periodically
    // lower the volume using your MediaPlayerSynchronizer's
    // VolumeLimiter.
    synchronizer.volumeLimiter?.lowerVolume();
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    // If everyone in the meeting stops speaking and the
    // interval timer is active, clear the interval.
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer: NodeJS.Timeout | undefined;
microsoftTeams.meeting.registerSpeakingStateChangeHandler((speakingState: microsoftTeams.meeting.ISpeakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    // If someone in the meeting starts speaking, periodically
    // lower the volume using your MediaPlayerSynchronizer's
    // VolumeLimiter.
    synchronizer.volumeLimiter?.lowerVolume();
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    // If everyone in the meeting stops speaking and the
    // interval timer is active, clear the interval.
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

---

Además, agregue los siguientes permisos [de RSC](/microsoftteams/platform/graph-api/rsc/resource-specific-consent) al manifiesto de la aplicación:

```json
{
  // ...rest of your manifest here
  "authorization": {
    "permissions": {
      "resourceSpecific": [
        // ...other permissions here
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Chat",
          "type": "Delegated"
        },
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Group",
          "type": "Delegated"
        }
      ]
    }
  }
}
```

> [!NOTE]
> La API `registerSpeakingStateChangeHandler` que se use para la atenuación de audio solo funcionará actualmente para los usuarios no locales que hablen.

## <a name="code-samples"></a>Ejemplos de código

| Ejemplo de nombre          | Descripción                                                                                                                               | JavaScript                                     |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| Vídeo de React          | Ejemplo básico que muestra cómo funciona el objeto EphemeralMediaSession con vídeo HTML5.                                                        | [Ver](https://aka.ms/liveshare-reactvideo)    |
| Plantilla multimedia de React | Permitir que todos los clientes conectados vean vídeos juntos, compilen una lista de reproducción compartida, transfieran a quién está al control y anoten sobre el vídeo. | [View](https://aka.ms/liveshare-mediatemplate) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Tutorial de Agile Poker](../sbs-teams-live-share.yml)

## <a name="see-also"></a>Vea también

- [Preguntas más frecuentes sobre el SDK de Live Share](teams-live-share-faq.md)
- [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
- [Documentos de referencia del SDK multimedia de Live Share](/javascript/api/@microsoft/live-share-media/)
- [Documentos de referencia](https://aka.ms/livesharedocs)
- [Aplicaciones de Teams en las reuniones](teams-apps-in-meetings.md)
