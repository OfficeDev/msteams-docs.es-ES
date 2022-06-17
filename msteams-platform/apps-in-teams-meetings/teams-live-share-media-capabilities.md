---
title: Capacidades multimedia de Live Share
description: En este módulo, obtendrá más información sobre la capacidades multimedia de Live Share, además de las suspensiones y puntos de espera, la atenuación de audio y la sincronización de vídeo y audio.
ms.topic: concept
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: 662a0204793eaf2ef4702a447a4a61c79964112c
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142482"
---
---

# <a name="live-share-media-capabilities"></a>Capacidades multimedia de Live Share

El vídeo y el audio forman parte fundamental del mundo moderno y de los lugares de trabajo. Hemos escuchado comentarios muy amplios sobre qué podemos hacer más para aumentar la calidad, la accesibilidad y proteger las licencias para ver vídeos juntos en reuniones.

El SDK de Live Share permite la **sincronización multimedia** en cualquier HTML `<video>` y `<audio>` elemento de forma más sencilla que nunca. Al sincronizar medios en la capa de controles de transporte y estado del reproductor, podrá atribuir vistas y licencias individualmente, a la vez que proporciona la mayor calidad posible disponible a través de la aplicación.

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

| Clases                                                                                                                  | Descripción                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| [EphemeralMediaSession](/javascript/api/@microsoft/live-share-media/ephemeralmediasession)     | Objeto efímero personalizado diseñado para coordinar los controles de transporte multimedia y el estado de reproducción en secuencias de medios independientes. |
| [MediaPlayerSynchronizer](/javascript/api/@microsoft/live-share-media/mediaplayersynchronizer) | Sincroniza un elemento multimedia HTML local con un grupo de elementos multimedia HTML remotos para un `EphemeralMediaSession`.|

Ejemplo:

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
</body>
```

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
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
const allowedRoles = ["Organizer", "Presenter"];
await mediaSession.start(allowedRoles);
```

`EphemeralMediaSession` escucha automáticamente los cambios en el estado de reproducción del grupo y aplicará los cambios a través de `MediaPlayerSynchronizer`. Para evitar los cambios de estado de reproducción que un usuario no inició intencionadamente, como un evento de búfer, deberemos llamar a los controles de transporte a través del sincronizador, en lugar de directamente a través del reproductor.

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

 > [!Note]
 > Aunque pueda usar el objeto `EphemeralMediaSession` para sincronizar los medios directamente, use `MediaPlayerSynchronizer` a menos que desee un control más preciso de la lógica de sincronización. En función del reproductor que use en la aplicación, es posible que desee crear una corrección de compatibilidad delegada para que la interfaz del reproductor web coincida con la interfaz multimedia HTML.

## <a name="suspensions-and-wait-points"></a>Suspensiones y puntos de espera

Si desea suspender temporalmente la sincronización del objeto `EphemeralMediaSession`, puede usar suspensiones. Un objeto [MediaSessionCoordinatorSuspension](/javascript/api/@microsoft/live-share-media/ephemeralmediasessioncoordinatorsuspension) es local de forma predeterminada, lo que podría ser útil en los casos en los que un usuario pueda querer ponerse al día con algo que se perdió, tomarse un descanso, etc. Si el usuario finaliza la suspensión, la sincronización se reanudará automáticamente.

```javascript
// Suspend the media session coordinator
const suspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

Al iniciar una suspensión, también se puede incluir un parámetro opcional [CoordinationWaitPoint](/javascript/api/@microsoft/live-share-media/coordinationwaitpoint), que permite a los usuarios definir las marcas de tiempo en las que se deba producir una suspensión para todos los usuarios. La sincronización no se reanudará hasta que todos los usuarios hayan finalizado la suspensión de ese punto de espera. Esto es útil para cosas como agregar un cuestionario o una encuesta en determinados puntos del vídeo.

```javascript
// Suspend the media session coordinator
const waitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension();
// End the suspension when the user readies up
document.getElementById("ready-up-button").onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

## <a name="audio-ducking"></a>Atenuación de audio

El SDK de Live Share admite la atenuación de audio inteligente. Puede usar la característica _experimental_ en la aplicación y agregar lo siguiente al código:

```javascript
import * as microsoftTeams from "@microsoft/teams-js";

// ...

let volumeTimer;
microsoftTeams.meeting.registerSpeakingStateChangeHandler((speakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

Para habilitar la atenuación de audio, agregue los siguientes permisos [RSC](/microsoftteams/platform/graph-api/rsc/resource-specific-consent) al manifiesto de la aplicación:

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

> [!Note]
> La API `registerSpeakingStateChangeHandler` que se use para la atenuación de audio solo funcionará actualmente para los usuarios no locales que hablen.

## <a name="code-samples"></a>Ejemplos de código

| Ejemplo de nombre   | Descripción | JavaScript |
| -------------------- | ----------------------------| -----------------|
| Vídeo de React          | Ejemplo básico que muestra cómo funciona el objeto EphemeralMediaSession con vídeo HTML5.                                                        | [Ver](https://aka.ms/liveshare-reactvideo)    |
| Plantilla multimedia de React | Permitir que todos los clientes conectados vean vídeos juntos, compilen una lista de reproducción compartida, transfieran a quién está al control y anoten sobre el vídeo. | [View](https://aka.ms/liveshare-mediatemplate) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Tutorial de Agile Poker](../sbs-teams-live-share.yml)

## <a name="see-also"></a>Vea también

* [Preguntas más frecuentes sobre el SDK de Live Share](teams-live-share-faq.md)
* [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
* [Documentos de referencia del SDK multimedia de Live Share](/javascript/api/@microsoft/live-share-media/)
* [Documentos de referencia](https://aka.ms/livesharedocs)
* [Aplicaciones de Teams en las reuniones](teams-apps-in-meetings.md)
