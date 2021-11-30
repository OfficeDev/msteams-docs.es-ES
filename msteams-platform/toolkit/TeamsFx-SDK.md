---
title: TeamsFx SDK
author: MuyangAmigo
description: Acerca del SDK de TeamsFx
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 63c5fad9c795c513b476f305c09d94ffad7c5d61
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228187"
---
# <a name="teamsfx-sdk-for-typescript-or-javascript"></a>SDK de TeamsFx para TypeScript o JavaScript

TeamsFx tiene como objetivo reducir las tareas de implementación de identidad y acceso a recursos en la nube hasta instrucciones de una sola línea con "configuración cero".

Use la biblioteca para:

- Obtenga acceso a las funcionalidades principales en el entorno de cliente y servidor de forma similar.
- Escribir código de autenticación de usuario de forma simplificada.

   * [Código fuente](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk) 
   * [Paquete (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx) 
   * [Documentación de referencia de API](https://aka.ms/teamsfx-sdk-help) 
   * [Muestras](https://github.com/OfficeDev/TeamsFx-Samples)

## <a name="get-started"></a>Introducción

El SDK de TeamsFx está preconfigurado en un proyecto con scaffolding mediante el kit de herramientas de TeamsFx o la CLI.
Para obtener más información sobre Teams proyecto de aplicación, vea [README](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md).

### <a name="prerequisites"></a>Requisitos previos

- Node.js versión `10.x.x` anterior o posterior.
- Si el proyecto ha instalado paquetes relacionados como dependencias, asegúrese de `botbuilder` que son de la misma versión y de la versión [](https://github.com/Microsoft/botbuilder-js#packages) `>= 4.9.3` . ([Problema: todos los paquetes botbuilder deben ser la misma versión](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548))

> [!TIP]
> Un proyecto creado por el kit de herramientas de TeamsFx VS Code extensión o herramienta CLI.

### <a name="install-the-microsoftteamsfx-package"></a>Instalar el `@microsoft/teamsfx` paquete

Instale el SDK de TeamsFx para TypeScript o JavaScript con `npm` :

```bash
npm install @microsoft/teamsfx
```

### <a name="create-and-authenticate-a-microsoftgraphclient"></a>Crear y autenticar una `MicrosoftGraphClient`

Para crear un objeto de cliente de gráfico para obtener acceso a la API de Microsoft Graph, necesitará la credencial para realizar la autenticación. El SDK proporciona varias clases de credenciales para elegir que cumplen varios requisitos. Debe cargar la configuración antes de usar las credenciales.

- En el entorno del explorador, debe pasar explícitamente los parámetros de configuración. El proyecto scaffolded React ha proporcionado variables de entorno para su uso.

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
```

- En entornos NodeJS como Azure Function, solo puede llamar a `loadConfiguration` . Se cargará desde variables de entorno de forma predeterminada.

```ts
loadConfiguration();
```

#### <a name="using-teams-app-user-credential"></a>Uso Teams credencial de usuario de la aplicación

Use el fragmento de código siguiente:

> [Nota] Solo puedes usar esta clase de credencial en la aplicación de explorador como Teams tab app.

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential = new TeamsUserCredential();
const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
const profile = await graphClient.api("/me").get();
```

#### <a name="using-microsoft-365-tenant-credential"></a>Usar Microsoft 365 de inquilino

No requiere la interacción con el Teams app. Puede llamar a Microsoft Graph como aplicación.
Use el fragmento de código siguiente:

```ts
loadConfiguration();
const credential = new M365TenantCredential();
const graphClient = createMicrosoftGraphClient(credential);
const profile = await graphClient.api("/users/{object_id_of_another_people}").get();
```

## <a name="core-concepts-and-code-structure"></a>Conceptos básicos y estructura de código

### <a name="credentials"></a>Credenciales

Hay 3 clases de credenciales ubicadas en [la carpeta de](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential) credenciales para ayudar a simplificar la autenticación. 

Las clases de credenciales `TokenCredential` implementan una interfaz que se usa ampliamente en las API de biblioteca de Azure. Están diseñados para proporcionar token de acceso para ámbitos específicos.
Las clases de credenciales representan una identidad diferente en determinados escenarios.

`TeamsUserCredential`representan Teams identidad del usuario actual. El uso de esta credencial solicitará el consentimiento del usuario por primera vez.
`M365TenantCredential`representar Microsoft 365 de inquilino. Normalmente se usa cuando el usuario no está implicado como trabajo de automatización desencadenado por el tiempo.
`OnBehalfOfUserCredential` usa en nombre del flujo. Necesita un token de acceso y puede obtener un token nuevo para distinto ámbito. Está diseñado para usarse en escenarios de Función de Azure o Bot.

### <a name="bots"></a>Bots

Las clases relacionadas con bots se almacenan en [la carpeta bot.](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot)

`TeamsBotSsoPrompt` tiene una buena integración con el marco bot. Simplifica el proceso de autenticación al desarrollar la aplicación bot.

### <a name="helper-functions"></a>Funciones auxiliares

El SDK de TeamsFx proporciona funciones auxiliares para facilitar la configuración de bibliotecas de terceros. Se encuentran en la [carpeta](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core) principal.

### <a name="error-handling"></a>Control de errores

La API se producirá `ErrorWithCode` si se produce un error. Cada `ErrorWithCode` uno contiene código de error y mensaje de error.

Por ejemplo, para filtrar un error específico, puede usar la siguiente comprobación:

```ts
try {
  const credential = new TeamsUserCredential();
  await credential.login("User.Read");
} catch (err: unknown) {
  if (err instanceof ErrorWithCode && err.code !== ErrorCode.ConsentFailed) {
    throw err;
  } else {
    // Silently fail because user cancels the consent dialog
    return;
  }
}
```

Y si la instancia de credenciales se usa en otra biblioteca como Microsoft Graph, es posible que el error se captura y se transforma.

```ts
try {
  const credential = new TeamsUserCredential();
  const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
  const profile = await graphClient.api("/me").get();
} catch (err: unknown) {
  // ErrorWithCode is handled by Graph client
  if (err instanceof GraphError && err.code?.includes(ErrorCode.UiRequiredError)) {
    this.setState({
      showLoginBtn: true,
    });
  }
}
```

## <a name="scenarios"></a>Escenarios

Las secciones siguientes proporcionan varios fragmentos de código que cubren algunos de los escenarios más comunes:

- [Usar Graph API en la aplicación de pestañas](#use-graph-api-in-tab-app)
- [Llamar a la función de Azure en la aplicación de pestaña](#call-azure-function-in-tab-app)
- [Access SQL base de datos en función de Azure](#access-sql-database-in-azure-function)
- [Usar la autenticación basada en certificados en la función de Azure](#use-certificate-based-authentication-in-azure-function)
- [Usar Graph API en la aplicación Bot](#use-graph-api-in-bot-application)

### <a name="use-graph-api-in-tab-app"></a>Usar Graph API en la aplicación de pestañas

Use `TeamsUserCredential` y `createMicrosoftGraphClient` .

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential: any = new TeamsUserCredential();
const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

### <a name="call-azure-function-in-tab-app"></a>Llamar a la función de Azure en la aplicación de pestaña

Use `axios` la biblioteca para realizar una solicitud HTTP a la función de Azure.

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential: any = new TeamsUserCredential();
const token = credential.getToken(""); // Get SSO token for the user
// Call API hosted in Azure Functions on behalf of user
const apiConfig = getResourceConfiguration(ResourceType.API);
const response = await axios.default.get(apiConfig.endpoint + "api/httptrigger1", {
  headers: {
    authorization: "Bearer " + token,
  },
});
```

### <a name="access-sql-database-in-azure-function"></a>Access SQL base de datos en función de Azure

Use `tedious` la biblioteca para obtener acceso SQL y aprovechar que administra la `DefaultTediousConnectionConfiguration` autenticación.
Además de , también puede crear configuraciones de conexión de `tedious` otras bibliotecas SQL basadas en el resultado de `sqlConnectionConfig.getConfig()` .

```ts
loadConfiguration();
const sqlConnectConfig = new DefaultTediousConnectionConfiguration();
const config = await sqlConnectConfig.getConfig();
const connection = new Connection(config);
connection.on("connect", (error) => {
  if (error) {
    console.log(error);
  }
});
```

### <a name="use-certificate-based-authentication-in-azure-function"></a>Usar la autenticación basada en certificados en la función de Azure

```ts
loadConfiguration({
  authentication: {
    clientId: process.env.M365_CLIENT_ID,
    certificateContent: "The content of a PEM-encoded public/private key certificate",
    authorityHost: process.env.M365_AUTHORITY_HOST,
    tenantId: process.env.M365_TENANT_ID,
  },
});
```

### <a name="use-graph-api-in-bot-application"></a>Usar Graph API en la aplicación Bot

Agregar `TeamsBotSsoPrompt` al conjunto de cuadros de diálogo.

```ts
const { ConversationState, MemoryStorage } = require("botbuilder");
const { DialogSet, WaterfallDialog } = require("botbuilder-dialogs");
const { TeamsBotSsoPrompt } = require("@microsoft/teamsfx");

const convoState = new ConversationState(new MemoryStorage());
const dialogState = convoState.createProperty("dialogState");
const dialogs = new DialogSet(dialogState);

loadConfiguration();
dialogs.add(
  new TeamsBotSsoPrompt("TeamsBotSsoPrompt", {
    scopes: ["User.Read"],
  })
);

dialogs.add(
  new WaterfallDialog("taskNeedingLogin", [
    async (step) => {
      return await step.beginDialog("TeamsBotSsoPrompt");
    },
    async (step) => {
      const token = step.result;
      if (token) {
        // ... continue with task needing access token ...
      } else {
        await step.context.sendActivity(`Sorry... We couldn't log you in. Try again later.`);
        return await step.endDialog();
      }
    },
  ])
);
```

## <a name="troubleshooting"></a>Solución de problemas

### <a name="configure-log"></a>Configurar registro

Puede establecer el nivel de registro del cliente y redirigir los resultados al usar esta biblioteca.
El registro está desactivado de forma predeterminada, puede activarlo estableciendo el nivel de registro.

#### <a name="enable-log-by-setting-log-level"></a>Habilitar el registro estableciendo el nivel de registro

Cuando se establece el nivel de registro, el registro está habilitado. Imprime información de registro en la consola de forma predeterminada.

Establezca el nivel de registro con el fragmento de código siguiente:

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

Puede redirigir el resultado del registro estableciendo la función de registro o registrador personalizado.

##### <a name="redirect-by-setting-custom-logger"></a>Redirigir mediante la configuración del registrador personalizado

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

##### <a name="redirect-by-setting-custom-log-function"></a>Redirigir estableciendo la función de registro personalizada

Tenga en cuenta que la función de registro no tendrá efecto si establece un registrador personalizado.

```ts
setLogLevel(LogLevel.Info);
// Only log error message to Application Insights in bot application.
setLogFunction((level: LogLevel, message: string) => {
  if (level === LogLevel.Error) {
    this.telemetryClient.trackTrace({
      message: message,
      severityLevel: Severity.Error,
    });
  }
});
```

## <a name="see-also"></a>Consulte también

[Galería de ejemplo de Microsoft TeamsFx](https://github.com/OfficeDev/TeamsFx-Samples)