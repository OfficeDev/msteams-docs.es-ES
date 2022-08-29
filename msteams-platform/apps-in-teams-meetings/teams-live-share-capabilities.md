---
title: Introducción a Live Share
author: surbhigupta
description: En este módulo, obtendrá más información sobre las funcionalidades del SDK de Live Share, los permisos de RSC y las estructuras de datos esféricas.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 35b39f062bcdaf79e0c32d33260dbd0940a4fe2c
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425606"
---
# <a name="live-share-core-capabilities"></a>Funcionalidades principales de Live Share

El SDK de Live Share se puede agregar a los contextos de `sidePanel` y `meetingStage` de la extensión de reunión con un esfuerzo mínimo. Este artículo se centra en cómo integrar el SDK de Live Share en la aplicación y las funcionalidades clave del SDK.

> [!NOTE]
> Actualmente, solo se admiten reuniones programadas y todos los participantes deben estar en el calendario de la reunión. Actualmente no se admiten los tipos de reunión, como llamadas uno a uno, llamadas grupales y reuniones.

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-dashboard.png" alt-text="Live Share de Teams":::

## <a name="install-the-javascript-sdk"></a>Instalación del SDK de JavaScript

El [SDK de Live Share](https://github.com/microsoft/live-share-sdk) es un paquete de JavaScript publicado en [npm](https://www.npmjs.com/package/@microsoft/live-share) y se puede descargar a través de npm o Yarn.

### <a name="npm"></a>npm

```bash
npm install @microsoft/live-share --save
```

### <a name="yarn"></a>Hilo

```bash
yarn add @microsoft/live-share
```

## <a name="register-rsc-permissions"></a>Registrar permisos de RSC

Para habilitar el SDK de Live Share para la extensión de reunión, primero debe agregar los siguientes permisos RSC al manifiesto de la aplicación:

```json
{
  // ...rest of your manifest here
  "configurableTabs": [
    {
        "configurationUrl": "https://<<BASE_URI_ORIGIN>>/config",
        "canUpdateConfiguration": false,
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

1. Inicialice el SDK de cliente de Teams.
2. Inicialice [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient).
3. Defina las estructuras de datos que desea sincronizar. Por ejemplo, `SharedMap`.
4. Únase al contenedor.

Ejemplo:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

---

Eso es todo lo que se necesita para configurar el contenedor y unirse a la sesión de la reunión. Ahora, vamos a revisar los distintos tipos de _estructuras de datos distribuidos_ que puede usar con el SDK de Live Share.

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
import { TeamsFluidClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { playlistMap: SharedMap },
};
const { container } = await client.joinContainer(schema);
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
import { TeamsFluidClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap, IValueChanged } from "fluid-framework";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);
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

## <a name="live-share-ephemeral-data-structures"></a>Estructuras de datos efímeras de Live Share

El SDK de Live Share incluye un conjunto de nuevas clases de `SharedObject` efímeras, que proporcionan objetos con y sin estado que no se almacenan en el contenedor Fluid. Por ejemplo, si desea crear una característica de puntero láser en la aplicación, como la popular integración de PowerPoint Live, puede usar nuestros objetos `EphemeralEvent` o `EphemeralState`.

| Objeto efímero                                                             | Descripción                                                                                                                             |
| ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [EphemeralPresence](/javascript/api/@microsoft/live-share/ephemeralpresence) | Vea qué usuarios están en línea, establezca propiedades personalizadas para cada usuario y difunda los cambios en su presencia.                               |
| [EphemeralEvent](/javascript/api/@microsoft/live-share/ephemeralevent)       | Difunda eventos individuales con atributos de datos personalizados en la carga.                                                             |
| [EphemeralState](/javascript/api/@microsoft/live-share/ephemeralstate)       | De forma similar a SharedMap, un almacén de clave-valor distribuido que permite cambios de estado restringidos en función del rol, por ejemplo, el moderador. |

### <a name="ephemeralpresence-example"></a>Ejemplo de EphemeralPresence

La `EphemeralPresence` clase hace que el seguimiento de quién está en la sesión sea más fácil que nunca. Al llamar a los `.initialize()` métodos o `.updatePresence()` , puede asignar metadatos personalizados para ese usuario, como el nombre o la imagen de perfil. Al escuchar `presenceChanged` eventos, cada cliente recibe el objeto más reciente `EphemeralPresenceUser` y contrae todas las actualizaciones de presencia en un único registro para cada único `userId`.

> [!NOTE]
> El valor predeterminado `userId` asignado a cada `EphemeralPresenceUser` uno es un UUID aleatorio y no está directamente asociado a una identidad de AAD. Para invalidarlo, establezca una personalizada `userId` para que sea la clave principal, como se muestra en el ejemplo siguiente.

Ejemplo:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import {
  TeamsFluidClient,
  EphemeralPresence,
  PresenceState,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    presence: EphemeralPresence,
  },
};
const { container } = await client.joinContainer(schema);
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
import { TeamsFluidClient, EphemeralPresence, PresenceState, EphemeralPresenceUser } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomUserData {
  name: string;
  picture: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    presence: EphemeralPresence<ICustomUserData>,
  },
};
const { container } = await client.joinContainer(schema);
const presence = container.initialObjects.presence as EphemeralPresence<ICustomUserData>;

// Register listener for changes to presence
presence.on("presenceChanged", (userPresence: EphemeralPresenceUser<ICustomUserData>, local: boolean) => {
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

### <a name="ephemeralevent-example"></a>Ejemplo de EphemeralEvent

`EphemeralEvent` es una excelente manera de enviar eventos simples a otros clientes en una reunión. Es útil para escenarios como el envío de notificaciones de sesión.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralEvent } from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { notifications: EphemeralEvent },
};
const { container } = await client.joinContainer(schema);
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
import { TeamsFluidClient, EphemeralEvent, IEphemeralEvent } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomEvent extends IEphemeralEvent {
  senderName: string;
  text: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    notifications: EphemeralEvent<ICustomEvent>,
  },
};
const { container } = await client.joinContainer(schema);
const notifications = container.initialObjects.notifications as EphemeralEvent<ICustomEvent>;

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

### <a name="ephemeraltimer-example"></a>Ejemplo de EphemeralTimer

`EphemeralTimer` permite escenarios que tienen un límite de tiempo, como un temporizador de meditación en grupo o un temporizador de ronda para un juego.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralTimer } from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { timer: EphemeralTimer },
};
const { container } = await client.joinContainer(schema);
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
  TeamsFluidClient,
  EphemeralTimer,
  EphemeralTimerEvents,
  ITimerConfig,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { timer: EphemeralTimer },
};
const { container } = await client.joinContainer(schema);
const timer = container.initialObjects.timer as EphemeralTimer;

// Register listener for when the timer starts its countdown
timer.on(EphemeralTimerEvents.started, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has started
});

// Register listener for when a paused timer has resumed
timer.on(EphemeralTimerEvents.played, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has resumed
});

// Register listener for when a playing timer has paused
timer.on(EphemeralTimerEvents.paused, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has paused
});

// Register listener for when a playing timer has finished
timer.on(EphemeralTimerEvents.finished, (config: ITimerConfig) => {
  // Update UI to show timer is finished
});

// Register listener for the timer progressed by 20 milliseconds
timer.on(EphemeralTimerEvents.onTick, (milliRemaining: number) => {
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

## <a name="role-verification-for-ephemeral-data-structures"></a>Comprobación de roles para estructuras de datos efímeras

Las reuniones en Teams pueden abarcar desde llamadas uno a uno hasta reuniones de todas las manos, y pueden incluir miembros de organizaciones. Los objetos efímeros están diseñados para admitir la comprobación de roles, lo que permite definir los roles que pueden enviar mensajes para cada objeto efímero individual. Por ejemplo, podría elegir que solo los organizadores y moderadores de reuniones puedan controlar la reproducción de vídeo, pero permitir que los invitados y asistentes soliciten vídeos para verlos a continuación.

> [!NOTE]
> La `EphemeralPresence` clase no admite la comprobación de roles. El `EphemeralPresenceUser` objeto tiene un `getRoles` método , que devuelve los roles de reunión para un usuario determinado.

Ejemplo con `EphemeralState`:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import {
  TeamsFluidClient,
  EphemeralState,
  UserMeetingRole,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { appState: EphemeralState },
};
const { container } = await client.joinContainer(schema);
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
import { TeamsFluidClient, EphemeralState, UserMeetingRole } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomState {
  documentId: string;
  presentingUserId?: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    appState: EphemeralState<ICustomState>,
  },
};
const { container } = await client.joinContainer(schema);
const appState = container.initialObjects.appState as EphemeralState<ICustomState>;

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

## <a name="code-samples"></a>Ejemplos de código

| Ejemplo de nombre | Descripción                                                     | JavaScript                                  |
| ----------- | --------------------------------------------------------------- | ------------------------------------------- |
| Dice Roller | Habilite a todos los clientes conectados para que lancen el dado y vean el resultado. | [Ver](https://aka.ms/liveshare-diceroller) |
| Agile Poker | Permitir que todos los clientes conectados jueguen a Agile Poker.               | [View](https://aka.ms/liveshare-agilepoker) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Funcionalidades de medios de Live Share](teams-live-share-media-capabilities.md)

## <a name="see-also"></a>Vea también

* [Repositorio de GitHub](https://github.com/microsoft/live-share-sdk)
* [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
* [Documentos de referencia del SDK multimedia de Live Share](/javascript/api/@microsoft/live-share-media/)
* [Preguntas más frecuentes sobre Live Share](teams-live-share-faq.md)
* [Aplicaciones de Teams en las reuniones](teams-apps-in-meetings.md)
