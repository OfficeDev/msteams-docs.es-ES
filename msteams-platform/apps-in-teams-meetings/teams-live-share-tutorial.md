---
title: Tutorial de código de Live Share
author: surbhigupta
description: En este módulo, obtendrá información sobre cómo empezar a trabajar con el SDK de Live Share y crear un ejemplo de Dice Roller con el SDK de Live Share.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: stevenic
ms.date: 04/07/2022
ms.openlocfilehash: 0210962126604733c4d66ba0db4276ff36cfd6b7
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841802"
---
# <a name="dice-roller-code-tutorial"></a>Tutorial de código de Dice Roller

En la aplicación de ejemplo de Dice Roller, se muestra a los usuarios un dado con un botón para lanzarlo. Cuando se lanza el dado, el SDK de Live Share usa el marco de Fluid para sincronizar los datos entre los clientes, de modo que todos vean el mismo resultado. Para sincronizar datos, realice los pasos siguientes en el archivo [app.js](https://github.com/microsoft/live-share-sdk/blob/main/samples/01.dice-roller/src/app.js):

1. [Configurar la aplicación](#set-up-the-application)
2. [Unir un contenedor de Fluid](#join-a-fluid-container)
3. [Escribir la vista extendida](#write-the-stage-view)
4. [Conectar la vista extendida a los datos de Fluid](#connect-stage-view-to-fluid-data)
5. [Escribir la vista del panel lateral](#write-the-side-panel-view)
6. [Escribir la vista de configuración](#write-the-settings-view)

:::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="Ejemplo de Dice Roller":::

## <a name="set-up-the-application"></a>Configurar la aplicación

Para empezar, importe los módulos necesarios. En el ejemplo, se usa [DDS SharedMap](https://fluidframework.com/docs/data-structures/map/) del marco Fluid y [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient) del SDK de Live Share. El ejemplo admite la extensibilidad de las reuniones de Teams, por lo que tendremos que incluir el [SDK del cliente de Teams](https://github.com/OfficeDev/microsoft-teams-library-js). Por último, el ejemplo está diseñado para ejecutarse localmente, en una reunión de Teams, por lo que tendremos que incluir algunas piezas adicionales del marco de Fluid necesarias para [probar el ejemplo localmente](https://fluidframework.com/docs/testing/testing/#azure-fluid-relay-as-an-abstraction-for-tinylicious).
  
Las aplicaciones crean contenedores de Fluid mediante un esquema que define un conjunto de *objetos iniciales* que estarán disponibles para el contenedor. En el ejemplo, se usa un SharedMap para almacenar el valor del dado más reciente que se obtuvo. Para obtener más información, consulte [Modelado de datos](https://fluidframework.com/docs/build/data-modeling/).

Las aplicaciones de reuniones de Teams requieren varias vistas (contenido, configuración y escena). Crearemos una función `start()` para ayudar a identificar la vista que se va a representar y a realizar cualquier inicialización necesaria. Queremos que nuestra aplicación admita la ejecución local en un explorador web y desde una reunión de Teams a fin de que la función `start()` busque un parámetro de consulta `inTeams=true` para determinar si se ejecuta en Teams. Al ejecutarse en Teams, la aplicación debe llamar a `app.initialize()` antes de llamar a cualquier otro método de teams-js.

Además del parámetro de consulta `inTeams=true`, podemos usar un parámetro de consulta `view=content|config|stage` para determinar la vista que debe representarse.

```js
import { SharedMap } from "fluid-framework";
import { TeamsFluidClient } from "@microsoft/live-share";
import { app, pages } from "@microsoft/teams-js";
import { LOCAL_MODE_TENANT_ID } from "@fluidframework/azure-client";
import { InsecureTokenProvider } from "@fluidframework/test-client-utils";

const searchParams = new URL(window.location).searchParams;
const root = document.getElementById("content");

// Define container schema

const diceValueKey = "dice-value-key";

const containerSchema = {
  initialObjects: { diceMap: SharedMap }
};

function onContainerFirstCreated(container) {
  // Set initial state of the rolled dice to 1.
  container.initialObjects.diceMap.set(diceValueKey, 1);
}


// STARTUP LOGIC

async function start() {

  // Check for page to display
  let view = searchParams.get('view') || 'stage';

  // Check if we are running on stage.
  if (!!searchParams.get('inTeams')) {

    // Initialize teams app
    await app.initialize();

    // Get our frameContext from context of our app in Teams
    const context = await app.getContext();
    if (context.page.frameContext == 'meetingStage') {
      view = 'stage';
    }
  }

  // Load the requested view
  switch (view) {
    case 'content':
      renderSidePanel(root);
      break;
    case 'config':
      renderSettings(root);
      break;
    case 'stage':
    default:
      const { container } = await joinContainer();
      renderStage(container.initialObjects.diceMap, root);
      break;
  }
}

start().catch((error) => console.error(error));
```

## <a name="join-a-fluid-container"></a>Unir un contenedor de Fluid

No todas las vistas de aplicación tendrán que ser colaborativas. La vista `stage` *siempre* necesita características de colaboración, la vista `content` *puede* necesitar características de colaboración y la vista `config`*nunca* necesita características de colaboración. Para las vistas que necesitan características de colaboración, deberá unir un contenedor Fluid asociado a la reunión actual.

Unir el contenedor para la reunión es tan sencillo como crear un nuevo [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient) y, a continuación, llamar al método [joinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer).  Al ejecutar localmente, tendrá que pasar una configuración de conexión personalizada con un `LOCAL_MODE_TENANT_ID` especial, pero unir un contenedor local es lo mismo que unir un contenedor en Teams.

```js
async function joinContainer() {
  // Are we running in teams?
  let client;
  if (!!searchParams.get('inTeams')) {
      // Create client
      client = new TeamsFluidClient();
  } else {
      // Create client and configure for testing
      client = new TeamsFluidClient({
        connection: {
          tenantId: LOCAL_MODE_TENANT_ID,
          tokenProvider: new InsecureTokenProvider("", { id: "123", name: "Test User" }),
          orderer: "http://localhost:7070",
          storage: "http://localhost:7070",
        }
      });
  }

  // Join container
  return await client.joinContainer(containerSchema, onContainerFirstCreated);
}
```

> [!NOTE]
> Al realizar pruebas localmente, TeamsFluidClient actualiza la dirección URL del explorador para que contenga el identificador del contenedor de prueba que se creó. Copiar ese vínculo a otras pestañas del explorador hace que TeamsFluidClient se una al contenedor de prueba que se creó. Si la modificación de la dirección URL de la aplicación interfiere con su funcionamiento, la estrategia usada para almacenar el identificador de contenedores de prueba se puede personalizar mediante las opciones [setLocalTestContainerId](/javascript/api/@microsoft/live-share/iteamsfluidclientoptions#@microsoft-live-share-iteamsfluidclientoptions-setlocaltestcontainerid) y [getLocalTestContainerId](/javascript/api/@microsoft/live-share/iteamsfluidclientoptions#@microsoft-live-share-iteamsfluidclientoptions-getlocaltestcontainerid) que se pasan a TeamsFluidClient.

## <a name="write-the-stage-view"></a>Escribir la vista extendida

Muchas aplicaciones de extensibilidad de reuniones de Teams están diseñadas para usar React para su marco de vista, pero esto no es obligatorio. Por ejemplo, en este ejemplo, se usan métodos HTML/DOM estándar para representar una vista.

### <a name="start-with-a-static-view"></a>Empezar con una vista estática

Es fácil crear la vista con datos locales sin ninguna funcionalidad de Fluid y, a continuación, agregar Fluid cambiando algunas partes clave de la aplicación.

La función `renderStage` anexa `stageTemplate` al elemento HTML que se pasó y crea un lanzador de dados que funciona con un valor de dados aleatorio cada vez que se selecciona el botón **Roll**. `diceMap` se usa en los pasos siguientes.

```js
const stageTemplate = document.createElement("template");

stageTemplate["innerHTML"] = `
  <div class="wrapper">
    <div class="dice"></div>
    <button class="roll"> Roll </button>
  </div>
`
function renderStage(diceMap, elem) {
    elem.appendChild(stageTemplate.content.cloneNode(true));
    const rollButton = elem.querySelector(".roll");
    const dice = elem.querySelector(".dice");

    rollButton.onclick = () => updateDice(Math.floor(Math.random() * 6)+1);

    const updateDice = (value) => {
        // Unicode 0x2680-0x2685 are the sides of a die (⚀⚁⚂⚃⚄⚅).
        dice.textContent = String.fromCodePoint(0x267f + value);
    };
    updateDice(1);
}
```

## <a name="connect-stage-view-to-fluid-data"></a>Conectar la vista extendida a los datos de Fluid

### <a name="modify-fluid-data"></a>Modificar los datos de Fluid

Para empezar a usar Fluid en la aplicación, lo primero que hay que cambiar es lo que sucede cuando el usuario selecciona `rollButton`. En lugar de actualizar el estado local directamente, el botón actualiza el número almacenado en la clave `value` del objeto pasado en `diceMap`. Dado que `diceMap` es un `SharedMap` de Fluid, los cambios se distribuyen a todos los clientes. Cualquier cambio en `diceMap` hará que se emita un evento `valueChanged` y un controlador de eventos puede desencadenar una actualización de la vista.

Este patrón es común en Fluid porque permite que la vista se comporte de la misma manera para los cambios locales y remotos.

```js
    rollButton.onclick = () => diceMap.set("dice-value-key", Math.floor(Math.random() * 6)+1);
```

### <a name="rely-on-fluid-data"></a>Confiar en los datos de Fluid

El siguiente cambio que debe realizarse es cambiar la función `updateDice` para que ya no acepte un valor arbitrario. Esto significa que la aplicación ya no puede modificar directamente el valor local del dado. En su lugar, el valor se recupera del `SharedMap` cada vez que se llama a `updateDice`.

```js
    const updateDice = () => {
        const diceValue = diceMap.get("dice-value-key");
        dice.textContent = String.fromCodePoint(0x267f + diceValue);
    };
    updateDice();
```

### <a name="handle-remote-changes"></a>Control de cambios remotos

Los valores devueltos por `diceMap` son solo una instantánea en el tiempo. Para mantener los datos actualizados a medida que cambian, se debe establecer un controlador de eventos en `diceMap` para llamar a `updateDice` cada vez que se envía el evento `valueChanged`. Para obtener una lista de eventos desencadenados y los valores pasados a esos eventos, consulte [SharedMap](https://fluidframework.com/docs/data-structures/map/).

```js
    diceMap.on("valueChanged", updateDice);
```

## <a name="write-the-side-panel-view"></a>Escribir la vista del panel lateral

La vista del panel lateral, cargada a través de la pestaña `contentUrl` con el contexto del marco `sidePanel`, se muestra al usuario en un panel lateral cuando abre la aplicación dentro de una reunión. El objetivo de esta vista es permitir que un usuario seleccione contenido para la aplicación antes de compartir la aplicación en la escena de reunión. Para las aplicaciones del SDK de Live Share, la vista del panel lateral también se puede usar como experiencia complementaria para la aplicación. Llamar a [joinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer) desde la vista del panel lateral conecta al mismo contenedor de Fluid al que está conectada la vista extendida. A continuación, este contenedor se puede usar para comunicarse con la vista extendida. Asegúrese de que se está comunicando con la vista extendida *y* la vista del panel lateral de todos los usuarios.

La vista del panel lateral del ejemplo solicita al usuario que seleccione el botón Compartir en escena

```js
const sidePanelTemplate = document.createElement("template");

sidePanelTemplate["innerHTML"] = `
  <style>
    .wrapper { text-align: center }
    .title { font-size: large; font-weight: bolder; }
    .text { font-size: medium; }
  </style>
  <div class="wrapper">
    <p class="title">Lets get started</p>
    <p class="text">Press the share to stage button to share Dice Roller to the meeting stage.</p>
  </div>
`;

function renderSidePanel(elem) {
    elem.appendChild(sidePanelTemplate.content.cloneNode(true));
}
```

## <a name="write-the-settings-view"></a>Escribir la vista de configuración

La vista de configuración, cargada mediante `configurationUrl` en el manifiesto de la aplicación, se muestra a un usuario cuando agrega la aplicación por primera vez a una reunión de Teams. Esta vista permite al desarrollador configurar `contentUrl` para la pestaña que está anclada a la reunión en función de la entrada del usuario. Esta página es necesaria actualmente incluso si no se requiere ninguna entrada del usuario para establecer `contentUrl`.

> [!Important]
> No se admite [joinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer) del SDK de Live Share en el contexto de pestaña`settings`.

La vista de configuración del ejemplo solicita al usuario que seleccione el botón Guardar.

```js
const settingsTemplate = document.createElement("template");

settingsTemplate["innerHTML"] = `
  <style>
    .wrapper { text-align: center }
    .title { font-size: large; font-weight: bolder; }
    .text { font-size: medium; }
  </style>
  <div class="wrapper">
    <p class="title">Welcome to Dice Roller!</p>
    <p class="text">Press the save button to continue.</p>
  </div>
`;

function renderSettings(elem) {
    elem.appendChild(settingsTemplate.content.cloneNode(true));

    // Save the configurable tab
    pages.config.registerOnSaveHandler(saveEvent => {
      pages.config.setConfig({
        websiteUrl: window.location.origin,
        contentUrl: window.location.origin + '?inTeams=1&view=content',
        entityId: 'DiceRollerFluidLiveShare',
        suggestedDisplayName: 'DiceRollerFluidLiveShare'
      });
      saveEvent.notifySuccess();
    });

    // Enable the Save button in config dialog
    pages.config.setValidityState(true);
}
```

## <a name="test-locally"></a>Probar localmente

Puede probar la aplicación localmente mediante `npm run start`. Para obtener más información, consulte la [Guía de inicio rápido](./teams-live-share-quick-start.md).

## <a name="test-in-teams"></a>Probar en Teams

Después de empezar a ejecutar la aplicación localmente con `npm run start`, puede probar la aplicación en Teams. Si quiere probar la aplicación sin implementación, descargue y use el servicio de túnel [`ngrok`](https://ngrok.com/).

### <a name="create-a-ngrok-tunnel-to-allow-teams-to-reach-your-app"></a>Creación de un túnel ngrok para permitir que Teams llegue a la aplicación

1. [Descargue ngrok](https://ngrok.com/download).

1. Use ngrok para crear un túnel con el puerto 8080. Ejecute el siguiente comando:

    ```
     `ngrok http 8080 --host-header=localhost`
    ```

    Se abre un nuevo terminal ngrok con una nueva dirección URL, por ejemplo `https:...ngrok.io`. La nueva dirección URL es el túnel que apunta a la aplicación y que debe actualizarse en `manifest.json` de la aplicación.

### <a name="create-the-app-package-to-sideload-into-teams"></a>Crear el paquete de la aplicación para transferir localmente a Teams

1. Vaya a la carpeta `\live-share-sdk\samples\01.dice-roller` de ejemplo de Dice Roller en el equipo. También puede revisar [`.\manifest\manifest.json`](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller/manifest) del ejemplo de Dice Roller en GitHub.

1. Abra manifest.json y actualice la dirección URL de configuración.

   Reemplace `https://<<BASE_URI_DOMAIN>>` por el punto de conexión HTTP de ngrok.

1. Puede actualizar los campos siguientes:
   * Configure `developer.name` con su nombre.
   * Actualice `developer.websiteUrl` con su sitio web.
   * Actualice `developer.privacyUrl` con su directiva de privacidad.
   * Actualice `developer.termsOfUseUrl` con sus condiciones de uso.

1. Comprima el contenido de la carpeta de manifiesto para crear `manifest.zip`. Asegúrese de que `manifest.zip` contiene solo el archivo de origen `manifest.json`, el icono `color` y el icono `outline`.

   1. En Windows, seleccione todos los archivos del directorio `.\manifest` y comprimalos.
  
   > [!NOTE]
   >
   > * No comprima la carpeta contenedora.
   > * Asigne un nombre descriptivo al archivo ZIP. Por ejemplo, `DiceRollerLiveShare`.
  
   Para obtener más información sobre el manifiesto, visite la [documentación del manifiesto de Teams](../resources/schema/manifest-schema.md).

### <a name="sideload-your-app-into-a-meeting"></a>Transferir localmente la aplicación a una reunión

1. Abra Teams.

1. Programe una reunión del calendario en Teams. Asegúrese de invitar al menos a un asistente a la reunión.

1. Únase a la reunión.

1. En la ventana de reunión de la parte superior, seleccione **+ Aplicaciones** > **Administrar aplicaciones**.

1. En el panel **Administrar aplicaciones**, seleccione **Cargar una aplicación personalizada**.

   1. Si no ve la opción **Upload una aplicación personalizada**, siga las [instrucciones](/microsoftteams/teams-custom-app-policies-and-settings) para habilitar aplicaciones personalizadas en la cuenta empresarial.

1. Seleccione el botón `manifest.zip` y elija un archivo del equipo.

1. Seleccione **Agregar** para agregar la aplicación de ejemplo a la reunión.

1. Seleccione **+ Aplicaciones**, escriba Dice Roller en el cuadro de búsqueda **Buscar una aplicación**.

1. Seleccione la aplicación para activarla en la reunión.

1. Seleccione **Guardar**.

   La aplicación Dice Roller se agrega al panel de reunión Teams.

1. En el panel lateral, seleccione el icono compartir en la escena. Teams inicia una sincronización en directo con los usuarios en la escena de la reunión.

   :::image type="content" source="../assets/images/teams-live-share/teams-live-share-to-stage.png" alt-text="icono compartir en la escena":::

   Ahora debería ver un lanzador de dados en la escena de reunión.

   :::image type="content" source="../assets/images/teams-live-share/teams-live-share-meeting-stage.png" alt-text="imagen de la escena de reunión":::

Los usuarios invitados a la reunión pueden ver la aplicación en la escena cuando se unan a la reunión.

## <a name="deployment"></a>Implementación

Una vez que esté listo para implementar el código, puede usar [Teams Toolkit](../toolkit/provision.md#provision-using-teams-toolkit) o el [Portal para desarrolladores de Teams](https://dev.teams.microsoft.com/apps) para aprovisionar y cargar el archivo ZIP de la aplicación.

> [!NOTE]
> Debe agregar el appId aprovisionado a `manifest.json` antes de cargar o distribuir la aplicación.

## <a name="code-samples"></a>Ejemplos de código

| Ejemplo de nombre | Descripción                                                      | JavaScript                                                                           |
| :---------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Dice Roller | Habilite a todos los clientes conectados para que lancen el dado y vean el resultado. | [View](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Funcionalidades básicas](teams-live-share-capabilities.md)

## <a name="see-also"></a>Vea también

* [Repositorio de GitHub](https://github.com/microsoft/live-share-sdk)
* [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
* [Documentos de referencia del SDK multimedia de Live Share](/javascript/api/@microsoft/live-share-media/)
* [Preguntas más frecuentes sobre Live Share](teams-live-share-faq.md)
* [Aplicaciones de Teams en las reuniones](teams-apps-in-meetings.md)
