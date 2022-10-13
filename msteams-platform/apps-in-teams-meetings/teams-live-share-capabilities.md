---
title: Introducción a Live Share
author: surbhigupta
description: En este módulo, obtenga más información sobre las funcionalidades del SDK de recursos compartidos en vivo, los permisos de RSC y las estructuras de datos en directo.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 0e2c2a41eee5bf77dfeaf7150eede97a4b60ded8
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560627"
---
# <a name="live-share-core-capabilities"></a>Funcionalidades principales de Live Share

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-core-capabilities-hero.png" alt-text="Captura de pantalla que muestra un ejemplo de los usuarios que juegan un juego de póquer ágil en una reunión de Teams, que muestra la funcionalidad de recursos compartidos en vivo.":::

El SDK de Live Share se puede agregar a los contextos de `sidePanel` y `meetingStage` de la extensión de reunión con un esfuerzo mínimo. Este artículo se centra en cómo integrar el SDK de Live Share en la aplicación y las funcionalidades clave del SDK.

## <a name="install-the-javascript-sdk"></a>Instalación del SDK de JavaScript

El [SDK de Live Share](https://github.com/microsoft/live-share-sdk) es un paquete de JavaScript publicado en [npm](https://www.npmjs.com/package/@microsoft/live-share) y se puede descargar a través de npm o Yarn.

### <a name="npm"></a>npm

```bash
npm install @microsoft/live-share@next --save
```

### <a name="yarn"></a>Hilo

```bash
yarn add @microsoft/live-share@next
```

## <a name="register-rsc-permissions"></a>Registrar permisos de RSC

Para habilitar el SDK de Live Share para la extensión de reunión, primero debe agregar los siguientes permisos RSC al manifiesto de la aplicación:

```json
{
  // ...rest of your manifest here
  "configurableTabs": [
    {
        "configurationUrl": "<<YOUR_CONFIGURATION_URL>>",
        "canUpdateConfiguration": true,
        "scopes": [
            "groupchat"
        ],
        "context": [
            "meetingSidePanel",
            "meetingStage"
        ]
    }
  ],
  "validDomains": [
    "<<BASE_URI_ORIGIN>>"
  ],
  "authorization": {
    "permissions": {
      "resourceSpecific": [
        // ...other permissions here
        {
          "name": "LiveShareSession.ReadWrite.Chat",
          "type": "Delegated"
        },
        {
          "name": "LiveShareSession.ReadWrite.Group",
          "type": "Delegated"
        },
        {
          "name": "MeetingStage.Write.Chat",
          "type": "Delegated"
        },
        {
          "name": "ChannelMeetingStage.Write.Group",
          "type": "Delegated"
        }
      ]
    }
  }
}
```

## <a name="join-a-meeting-session"></a>Unirse a una sesión de reunión

Siga los pasos para unirse a una sesión asociada a la reunión de un usuario:

1. Inicialice [LiveShareClient](/javascript/api/@microsoft/live-share/liveshareclient).
2. Defina las estructuras de datos que desea sincronizar. Por ejemplo, `SharedMap`.
3. Únase al contenedor.

Ejemplo:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

---

Eso es todo lo que se necesita para configurar el contenedor y unirse a la sesión de la reunión. Ahora, vamos a revisar los distintos tipos de _estructuras de datos distribuidos_ que puede usar con el SDK de Live Share.

> [!TIP]
> Asegúrese de que el SDK de cliente de Teams se inicialice antes de usar las API de Live Share.

## <a name="fluid-distributed-data-structures"></a>Estructuras de datos distribuidos fluidos

El SDK de Live Share admite cualquier estructura de [datos distribuida](https://fluidframework.com/docs/data-structures/overview/) incluida en Fluid Framework. Esta es una introducción rápida a algunos de los distintos tipos de objetos disponibles:

| Objeto compartido                                                                       | Descripción                                                                                                                             |
| ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [SharedMap](https://fluidframework.com/docs/data-structures/map/)                   | Almacén de clave-valor distribuido. Establezca cualquier objeto serializable con JSON para que una clave determinada sincronice ese objeto para todos los usuarios de la sesión. |
| [SharedSegmentSequence](https://fluidframework.com/docs/data-structures/sequences/) | Estructura de datos de tipo lista para almacenar un conjunto de elementos (denominados segmentos) en posiciones de conjunto.                                               |
| [SharedString](https://fluidframework.com/docs/data-structures/string/)             | Secuencia de cadena distribuida optimizada para editar la edición de texto del documento.                                                                |

Veamos cómo funciona `SharedMap`. En este ejemplo, hemos usado `SharedMap` para crear una característica de lista de reproducción.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { playlistMap: SharedMap },
};
const { container } = await liveShare.joinContainer(schema);
const playlistMap = container.initialObjects.playlistMap as SharedMap;

// Register listener for changes to values in the map
playlistMap.on("valueChanged", (changed, local) => {
  const video = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video) {
  // Add video to map
  playlistMap.set(video.id, video);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap, IValueChanged } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await liveShare.joinContainer(schema);
const playlistMap = container.initialObjects.playlistMap as SharedMap;

// Declare interface for object being stored in map
interface IVideo {
  id: string;
  url: string;
}

// Register listener for changes to values in the map
playlistMap.on("valueChanged", (changed: IValueChanged, local: boolean) => {
  const video: IVideo | undefined = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video: IVideo) {
  // Add video to map
  playlistMap.set(video.id, video);
}
```

---

> [!NOTE]
> Los objetos DDS de Core Fluid Framework no admiten la comprobación de roles de reunión. Todos los miembros de la reunión pueden cambiar los datos almacenados a través de estos objetos.

## <a name="live-share-data-structures"></a>Estructuras de datos de Live Share

El SDK de Live Share incluye un conjunto de nuevas clases de Live Share `SharedObject` , que proporcionan objetos con estado y sin estado que no se almacenan en el contenedor fluid. Por ejemplo, si desea crear una característica de puntero láser en la aplicación, como la popular integración de PowerPoint Live, puede usar nuestros objetos `LiveEvent` o `LiveState`.

| Objeto Live                                                        | Descripción                                                                                                                             |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| [LivePresence](/javascript/api/@microsoft/live-share/livepresence) | Vea qué usuarios están en línea, establezca propiedades personalizadas para cada usuario y difunda los cambios en su presencia.                               |
| [LiveEvent](/javascript/api/@microsoft/live-share/liveevent)       | Difunda eventos individuales con atributos de datos personalizados en la carga.                                                             |
| [Livestate](/javascript/api/@microsoft/live-share/livestate)       | De forma similar a SharedMap, un almacén de clave-valor distribuido que permite cambios de estado restringidos en función del rol, por ejemplo, el moderador. |
| [LiveTimer](/javascript/api/@microsoft/live-share/livetimer)       | Sincronice un temporizador de cuenta atrás para un intervalo determinado.                                                                                     |

### <a name="livepresence-example"></a>Ejemplo de LivePresence

:::image type="content" source="../assets/images/teams-live-share/live-share-presence.png" alt-text="Captura de pantalla que muestra un ejemplo de personas que están disponibles en una sesiónTeams mediante la presencia de Live Share.":::

La `LivePresence` clase hace que el seguimiento de quién está en la sesión sea más fácil que nunca. Al llamar a los `.initialize()` métodos o `.updatePresence()` , puede asignar metadatos personalizados para ese usuario, como el nombre o la imagen de perfil. Al escuchar `presenceChanged` eventos, cada cliente recibe el objeto más reciente `LivePresenceUser` y contrae todas las actualizaciones de presencia en un único registro para cada único `userId`.

> [!NOTE]
> El valor predeterminado `userId` asignado a cada `LivePresenceUser` uno es un UUID aleatorio y no está directamente asociado a una identidad de AAD. Para invalidarlo, establezca una personalizada `userId` para que sea la clave principal, como se muestra en el ejemplo siguiente.

Ejemplo:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import {
  LiveShareClient,
  LivePresence,
  PresenceState,
} from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: {
    presence: LivePresence,
  },
};
const { container } = await liveShare.joinContainer(schema);
const presence = container.initialObjects.presence;

// Register listener for changes to presence
presence.on("presenceChanged", (userPresence, local) => {
  // Update UI with presence
});

// Start tracking presence
presence.initialize("YOUR_CUSTOM_USER_ID", {
  name: "Anonymous",
  picture: "DEFAULT_PROFILE_PICTURE_URL",
});

function onUserDidLogIn(userName, profilePicture) {
  presence.updatePresence(PresenceState.online, {
    name: userName,
    picture: profilePicture,
  });
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import {
  LiveShareClient,
  LivePresence,
  PresenceState,
  LivePresenceUser,
} from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomUserData {
  name: string;
  picture: string;
}

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: {
    presence: LivePresence<ICustomUserData>,
  },
};
const { container } = await liveShare.joinContainer(schema);
const presence = container.initialObjects.presence as LivePresence<ICustomUserData>;

// Register listener for changes to presence
presence.on("presenceChanged", (userPresence: LivePresenceUser<ICustomUserData>, local: boolean) => {
  // Update UI with presence
});

// Start tracking presence
presence.initialize("YOUR_CUSTOM_USER_ID", {
  name: "Anonymous",
  picture: "DEFAULT_PROFILE_PICTURE_URL",
});

function onUserDidLogIn(userName: string, profilePicture: string) {
  presence.updatePresence(PresenceState.online, {
    name: userName,
    picture: profilePicture,
  });
}
```

---

### <a name="liveevent-example"></a>Ejemplo de LiveEvent

:::image type="content" source="../assets/images/teams-live-share/live-share-event.png" alt-text="Captura de pantalla que muestra un ejemplo de cliente de Teams que muestra una notificación cuando hay un cambio en el evento.":::

`LiveEvent` es una excelente manera de enviar eventos simples a otros clientes en una reunión. Es útil para escenarios como el envío de notificaciones de sesión.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveEvent, LiveShareClient } from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { notifications: LiveEvent },
};
const { container } = await liveShare.joinContainer(schema);
const { notifications } = container.initialObjects;

// Register listener for incoming notifications
notifications.on("received", (event, local) => {
  let notificationToDisplay;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start listening for incoming notifications
await notifications.initialize();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, LiveEvent, ILiveEvent } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomEvent extends ILiveEvent {
  senderName: string;
  text: string;
}

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: {
    notifications: LiveEvent<ICustomEvent>,
  },
};
const { container } = await liveShare.joinContainer(schema);
const notifications = container.initialObjects.notifications as LiveEvent<ICustomEvent>;

// Register listener for incoming notifications
notifications.on("received", (event: ICustomEvent, local: boolean) => {
  let notificationToDisplay: string;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start listening for incoming notifications
await notifications.initialize();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

---

### <a name="livetimer-example"></a>Ejemplo de LiveTimer

:::image type="content" source="../assets/images/teams-live-share/live-share-timer.png" alt-text="Captura de pantalla que muestra un ejemplo de un temporizador de recuento inactivo con 9 segundos restantes.":::

`LiveTimer` permite escenarios que tienen un límite de tiempo, como un temporizador de meditación en grupo o un temporizador de ronda para un juego.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, LiveTimer } from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { timer: LiveTimer },
};
const { container } = await liveShare.joinContainer(schema);
const { timer } = container.initialObjects;

// Register listener for when the timer starts its countdown
timer.on("started", (config, local) => {
  // Update UI to show timer has started
});

// Register listener for when a paused timer has resumed
timer.on("played", (config, local) => {
  // Update UI to show timer has resumed
});

// Register listener for when a playing timer has paused
timer.on("paused", (config, local) => {
  // Update UI to show timer has paused
});

// Register listener for when a playing timer has finished
timer.on("finished", (config) => {
  // Update UI to show timer is finished
});

// Register listener for the timer progressed by 20 milliseconds
timer.on("onTick", (milliRemaining) => {
  // Update UI to show remaining time
});

// Start synchronizing timer events for users in session
await timer.initialize();

// Start a 60 second timer
const durationInMilliseconds = 1000 * 60;
timer.start(durationInMilliseconds);

// Pause the timer for users in session
timer.pause();

// Resume the timer for users in session
timer.play();
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import {
  LiveShareClient,
  LiveTimer,
  LiveTimerEvents,
  ITimerConfig,
} from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { timer: LiveTimer },
};
const { container } = await liveShare.joinContainer(schema);
const timer = container.initialObjects.timer as LiveTimer;

// Register listener for when the timer starts its countdown
timer.on(LiveTimerEvents.started, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has started
});

// Register listener for when a paused timer has resumed
timer.on(LiveTimerEvents.played, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has resumed
});

// Register listener for when a playing timer has paused
timer.on(LiveTimerEvents.paused, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has paused
});

// Register listener for when a playing timer has finished
timer.on(LiveTimerEvents.finished, (config: ITimerConfig) => {
  // Update UI to show timer is finished
});

// Register listener for the timer progressed by 20 milliseconds
timer.on(LiveTimerEvents.onTick, (milliRemaining: number) => {
  // Update UI to show remaining time
});

// Start synchronizing timer events
await timer.initialize();

// Start a 60 second timer for users in session
const durationInMilliseconds = 1000 * 60;
timer.start(durationInMilliseconds);

// Pause the timer for users in session
timer.pause();

// Resume the timer for users in session
timer.play();
```

---

## <a name="role-verification-for-live-data-structures"></a>Comprobación de roles para estructuras de datos activas

Las reuniones en Teams pueden abarcar desde llamadas uno a uno hasta reuniones de todas las manos, y pueden incluir miembros de organizaciones. Los objetos dinámicos están diseñados para admitir la comprobación de roles, lo que le permite definir los roles que pueden enviar mensajes para cada objeto dinámico individual. Por ejemplo, podría elegir que solo los organizadores y moderadores de reuniones puedan controlar la reproducción de vídeo, pero permitir que los invitados y asistentes soliciten vídeos para verlos a continuación.

> [!NOTE]
> La `LivePresence` clase no admite la comprobación de roles. El `LivePresenceUser` objeto tiene un `getRoles` método , que devuelve los roles de reunión para un usuario determinado.

Ejemplo con `LiveState`:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, LiveState, UserMeetingRole } from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { appState: LiveState },
};
const { container } = await liveShare.joinContainer(schema);
const { appState } = container.initialObjects;

// Register listener for changes to state and corresponding custom data
appState.on("stateChanged", (state, data, local) => {
  // Update local app state
});

// Set roles who can change state and start listening for changes
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.initialize(allowedRoles);

function onSelectEditMode(documentId) {
  appState.changeState("editing", {
    documentId,
  });
}

function onSelectPresentMode(documentId) {
  appState.changeState("presenting", {
    documentId,
    presentingUserId: "LOCAL_USER_ID",
  });
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, LiveState, UserMeetingRole } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomState {
  documentId: string;
  presentingUserId?: string;
}

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: {
    appState: LiveState<ICustomState>,
  },
};
const { container } = await liveShare.joinContainer(schema);
const appState = container.initialObjects.appState as LiveState<ICustomState>;

// Register listener for changes to state and corresponding custom data
appState.on("stateChanged", (state: string, data: ICustomState | undefined, local: boolean) => {
  // Update local app state
});

// Set roles who can change state and start listening for changes
const allowedRoles: UserMeetingRole[] = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.initialize(allowedRoles);

function onSelectEditMode(documentId: string) {
  appState.changeState("editing", {
    documentId,
  });
}

function onSelectPresentMode(documentId: string) {
  appState.changeState("presenting", {
    documentId,
    presentingUserId: "LOCAL_USER_ID",
  });
}
```

---

Escuche a los clientes para comprender sus escenarios antes de implementar la comprobación de roles en la aplicación, especialmente para el rol **Organizador**. No hay ninguna garantía de que un organizador de la reunión esté presente en la reunión. Como regla general, todos los usuarios serán **Organizador** o **Moderador** al colaborar dentro de una organización. Si un usuario es un **Asistente**, suele ser una decisión intencionada en nombre de un organizador de la reunión.

> [!NOTE]
> Actualmente, Live Share no admite reuniones de canal.

## <a name="code-samples"></a>Ejemplos de código

| Ejemplo de nombre | Descripción                                                     | JavaScript                                  |
| ----------- | --------------------------------------------------------------- | ------------------------------------------- |
| Dice Roller | Habilite a todos los clientes conectados para que lancen el dado y vean el resultado. | [Ver](https://aka.ms/liveshare-diceroller) |
| Agile Poker | Permitir que todos los clientes conectados jueguen a Agile Poker.               | [View](https://aka.ms/liveshare-agilepoker) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Contenido multimedia de Live Share](teams-live-share-media-capabilities.md)

## <a name="see-also"></a>Vea también

- [Repositorio de GitHub](https://github.com/microsoft/live-share-sdk)
- [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
- [Documentos de referencia del SDK multimedia de Live Share](/javascript/api/@microsoft/live-share-media/)
- [Preguntas más frecuentes sobre Live Share](teams-live-share-faq.md)
- [Aplicaciones de Teams en las reuniones](teams-apps-in-meetings.md)
