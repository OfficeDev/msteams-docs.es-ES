---
title: TeamsFx SDK
author: MuyangAmigo
description: Acerca del SDK de TeamsFx
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ade31e39d48b92cca4309b16762dc95afccf1925
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073100"
---
# <a name="teamsfx-sdk"></a>TeamsFx SDK

TeamsFx ayuda a reducir las tareas de desarrollador aprovechando Teams inicio de sesión único y accediendo a los recursos en la nube hasta instrucciones de una sola línea con cero configuración. El SDK de TeamsFx está creado para usarse en el explorador y Node.js entorno, entre los escenarios comunes se incluyen:

* Teams aplicación de pestaña
* Función de Azure
* bot de Teams

Puede usar el SDK de TeamsFx para:

* Acceso a las funcionalidades principales en el entorno de cliente y servidor 
* Escritura de código de autenticación de usuario de forma simplificada

## <a name="prerequisites"></a>Requisitos previos

Instale las herramientas siguientes y configure el entorno de desarrollo:

* Versión más reciente de Node.js
* Si el proyecto ha instalado `botbuilder` [paquetes](https://github.com/Microsoft/botbuilder-js#packages) relacionados como dependencias, asegúrese de que son de la misma versión. Actualmente, la versión necesaria es la 4.15.0 o posterior. Para obtener más información, consulte [Bot Builder packages should be of the same version (Los paquetes del generador de bots deben ser de la misma versión](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548)).

Debe tener conocimientos prácticos de lo siguiente:

* [Código fuente](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)
* [Paquete (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx)
* [Documentación de referencia de API](https://aka.ms/teamsfx-sdk-help)
* [Muestras](https://github.com/OfficeDev/TeamsFx-Samples)

## <a name="get-started"></a>Introducción

El SDK de TeamsFx está preconfigurado en el proyecto con scaffolding mediante TeamsFx Toolkit o la CLI.
Para obtener más información, consulte [Teams proyecto de aplicación](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md).

### <a name="install-the-microsoftteamsfx-package"></a>Instalación del `@microsoft/teamsfx` paquete

Instale el SDK de TeamsFx para TypeScript o JavaScript con `npm`:

```bash
npm install @microsoft/teamsfx
```

### <a name="create-microsoftgraphclient-service"></a>Creación de `MicrosoftGraphClient` un servicio

Para crear un objeto de cliente de Graph y acceder a microsoft Graph API, necesita las credenciales para autenticarse. El SDK proporciona API para configurar para desarrolladores.

<br>

<details>
<summary><b>Invocar Graph API en nombre de Teams usuario (identidad de usuario)</b></summary>

Use el siguiente fragmento de código:

```ts
// Equivalent to:
// const teamsfx = new TeamsFx(IdentityType.User, {
//   initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
//   clientId: process.env.REACT_APP_CLIENT_ID,
// }
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
const profile = await graphClient.api("/me").get(); // Get the profile of current user
```

</details>

<br>

<details>
<summary><b>Invocar Graph API sin usuario (identidad de aplicación)</b></summary>

No requiere la interacción con Teams usuario. Puede llamar a Microsoft Graph como identidad de aplicación.

Use el siguiente fragmento de código:

```ts
// Equivalent to:
// const teamsfx = new TeamsFx(IdentityType.App, {
//   initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
//   clientId: process.env.REACT_APP_CLIENT_ID,
// });
const teamsfx = new TeamsFx(IdentityType.App);
const graphClient = createMicrosoftGraphClient(teamsfx);
const profile = await graphClient.api("/users/{object_id_of_another_people}").get(); // Get the profile of certain user
```

</details>

<br>

## <a name="core-concepts-and-code-structure"></a>Conceptos básicos y estructura de código

### <a name="teamsfx-class"></a>TeamsFx (clase)

La instancia de la clase TeamsFx accede a todas las configuraciones de TeamsFx desde variables de entorno de forma predeterminada. También puede establecer valores de configuración personalizados para invalidar los valores predeterminados. Compruebe [la configuración de invalidación](#override-configuration) para obtener más información. Al crear una instancia de TeamsFx, también debe especificar el tipo de identidad. Hay dos tipos de identidad:

* Identidad de usuario
* Identidad de la aplicación

#### <a name="user-identity"></a>Identidad de usuario

| Comando | Descripción |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| La aplicación se autentica como usuario Teams actual. |
| `TeamsFx:setSsoToken()`| Identidad de usuario en Node.js entorno (sin explorador). |
| `TeamsFx:getUserInfo()` | Para obtener la información base del usuario. |
| `TeamsFx:login()` | Se usa para permitir que el usuario realice el proceso de consentimiento, si desea usar el inicio de sesión único para obtener el token de acceso para determinados ámbitos de OAuth. |

> [!NOTE]
> Puede acceder a los recursos en nombre del usuario Teams actual.

#### <a name="application-identity"></a>Identidad de la aplicación

| Comando | Descripción |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| La aplicación se autentica como una aplicación. El permiso normalmente necesita la aprobación del administrador.|
| `TeamsFx:getCredential()`| Proporciona instancias de credenciales que corresponden automáticamente al tipo de identidad. |

> [!NOTE]
> Necesita el consentimiento del administrador para los recursos.

### <a name="credential"></a>Credential

Debe elegir el tipo de identidad al inicializar TeamsFx. Después de especificar el tipo de identidad al inicializar TeamsFx, el SDK usa diferentes tipos de clase de credencial para representar la identidad y obtener el token de acceso mediante el flujo de autenticación correspondiente.

Hay tres clases de credenciales para simplificar la autenticación. [carpeta de credenciales](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential). Las clases de credenciales implementan la `TokenCredential` interfaz, que se usa ampliamente en las API de biblioteca de Azure, diseñada para proporcionar tokens de acceso para ámbitos específicos. Otras API se basan en la llamada `TeamsFx:getCredential()` a credenciales para obtener una instancia de `TokenCredential`.

Estos son los escenarios correspondientes para cada destino de clase de credencial.

#### <a name="user-identity-in-browser-environment"></a>Identidad de usuario en el entorno del explorador
`TeamsUserCredential`representa Teams identidad del usuario actual. El uso de esta credencial solicitará el consentimiento del usuario por primera vez. Aprovecha el Teams sso y el flujo en nombre de para realizar el intercambio de tokens. El SDK usa esta credencial cuando el desarrollador elige la identidad de usuario en el entorno del explorador.

Configuración necesaria: `initiateLoginEndpoint`, `clientId`.

#### <a name="user-identity-in-nodejs-environment"></a>Identidad de usuario en Node.js entorno
`OnBehalfOfUserCredential`usa el flujo en nombre de y necesita Teams token de SSO. Está diseñado para usarse en escenarios de azure function o bot. El SDK usa esta credencial cuando el desarrollador elige la identidad de usuario en Node.js entorno.

Configuración necesaria: `authorityHost`, `tenantId`, `clientId``clientSecret` o `certificateContent`.

#### <a name="application-identity-in-nodejs-environment"></a>Identidad de la aplicación en Node.js entorno
`AppCredential` representa la identidad de la aplicación. Normalmente se usa cuando el usuario no está implicado, como el trabajo de automatización desencadenada por el tiempo. El SDK usa esta credencial cuando el desarrollador elige Identidad de aplicación en Node.js entorno.

Configuración necesaria: `tenantId`, `clientId``clientSecret` o `certificateContent`.

### <a name="bot-sso"></a>Inicio de sesión único de Bot

Las clases relacionadas con bots se almacenan en la [carpeta bot](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot).

`TeamsBotSsoPrompt` tiene una buena integración con bot framework. Simplifica el proceso de autenticación al desarrollar una aplicación de bot y quiere aprovechar el inicio de sesión único del bot.

Configuración necesaria: `initiateLoginEndpoint`, `tenantId`, `clientId`y `applicationIdUri`.

### <a name="supported-functions"></a>Funciones admitidas

El SDK de TeamsFx proporciona varias funciones para facilitar la configuración de bibliotecas de terceros. Se encuentran en la [carpeta principal](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core).

*  Microsoft Graph Service:`createMicrosoftGraphClient` y `MsGraphAuthProvider` ayuda para crear una instancia de Graph autenticada.
*  SQL:`getTediousConnectionConfig` devuelve una configuración de conexión tediosa.

Configuración necesaria:
* `sqlServerEndpoint`, `sqlUsername`, `sqlPassword` si desea usar la identidad de usuario
* `sqlServerEndpoint`, `sqlIdentityId` si desea usar la identidad MSI

### <a name="error-handling"></a>Control de errores

La respuesta de error de API es `ErrorWithCode`, que contiene el código de error y el mensaje de error. Por ejemplo, para filtrar un error específico, puede usar el siguiente fragmento de código:

```ts
try {
  const teamsfx = new TeamsFx();
  await teamsfx.login("User.Read");
} catch (err: unknown) {
  if (err instanceof ErrorWithCode && err.code !== ErrorCode.ConsentFailed) {
    throw err;
  } else {
    // Silently fail because user cancels the consent dialog
        return;
  }
}
```

Si se usa la instancia de credenciales en otra biblioteca, como Microsoft Graph, es posible que el error se detecte y transforme.

```ts
try {
  const teamsfx = new TeamsFx();
  const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
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

En la sección siguiente se proporcionan varios fragmentos de código para escenarios comunes:

<br>

<details>
<summary><b>Uso de Graph API en la aplicación de pestaña</b></summary>
 
Use `TeamsFx` y `createMicrosoftGraphClient`.

```ts
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

</details>

<br>

<details>
<summary><b>Llamada a La función de Azure en la aplicación de pestaña</b></summary>

Use `axios` la biblioteca para realizar una solicitud HTTP a La función de Azure.

```ts
const teamsfx = new TeamsFx();
const token = teamsfx.getCredential().getToken(""); // Get SSO token for the use
// Call API hosted in Azure Functions on behalf of user
const apiEndpoint = teamsfx.getConfig("apiEndpoint");
const response = await axios.default.get(apiEndpoint + "api/httptrigger1", {
  headers: {
    authorization: "Bearer " + token,
  },
});
```

</details>

<br>

<details>
<summary><b>Acceso a SQL base de datos en Azure Function</b></summary>


Use `tedious` la biblioteca para acceder a SQL y aprovechar `DefaultTediousConnectionConfiguration` que administra la autenticación.
Además de `tedious`, también puede crear la configuración de conexión de otras bibliotecas de SQL en función del resultado de `sqlConnectionConfig.getConfig()`.

```ts
// Equivalent to:
// const sqlConnectConfig = new DefaultTediousConnectionConfiguration({
//    sqlServerEndpoint: process.env.SQL_ENDPOINT,
//    sqlUsername: process.env.SQL_USER_NAME,
//    sqlPassword: process.env.SQL_PASSWORD,
// });
const teamsfx = new TeamsFx();
// If there's only one SQL database
const config = await getTediousConnectionConfig(teamsfx);
// If there are multiple SQL databases
const config2 = await getTediousConnectionConfig(teamsfx "your database name");
const connection = new Connection(config);
connection.on("connect", (error) => {
  if (error) {
    console.log(error);
  }
});
```

</details>

<br>

<details>
<summary><b>Uso de la autenticación basada en certificados en la función de Azure</b></summary>

```ts
const authConfig = {
  clientId: process.env.M365_CLIENT_ID,
  certificateContent: "The content of a PEM-encoded public/private key certificate",
  authorityHost: process.env.M365_AUTHORITY_HOST,
  tenantId: process.env.M365_TENANT_ID,
};
const teamsfx = new TeamsFx(IdentityType.App);
teamsfx.setCustomeConfig({
  certificateContent: "The content of a PEM-encoded public/private key certificate"
});
const token = teamsfx.getCredential().getToken();
```

</details>

<br>

<details>
<summary><b>Uso de Graph API en la aplicación bot</b></summary>

Agregar `TeamsBotSsoPrompt` al conjunto de diálogos.

```ts
const { ConversationState, MemoryStorage } = require("botbuilder");
const { DialogSet, WaterfallDialog } = require("botbuilder-dialogs");
const { TeamsBotSsoPrompt } = require("@microsoft/teamsfx");

const convoState = new ConversationState(new MemoryStorage());
const dialogState = convoState.createProperty("dialogState");
const dialogs = new DialogSet(dialogState);

const teamsfx = new TeamsFx();
dialogs.add(
  new TeamsBotSsoPrompt(teamsfx, "TeamsBotSsoPrompt", {
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

</details>

<br>

## <a name="advanced-customization"></a>Personalización avanzada

### <a name="configure-log"></a>Configuración del registro

Puede establecer el nivel de registro del cliente y redirigir las salidas al usar esta biblioteca. El registro está desactivado de forma predeterminada, puede activarlo estableciendo el nivel de registro.

#### <a name="enable-log-by-setting-log-level"></a>Habilitación del registro mediante la configuración del nivel de registro

El registro solo está habilitado cuando se establece el nivel de registro. De forma predeterminada, imprime información de registro en la consola.

Establezca el nivel de registro mediante el siguiente fragmento de código:

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

Puede redirigir la salida del registro estableciendo una función de registro o registrador personalizada.

#### <a name="redirect-by-setting-custom-logger"></a>Redireccionamiento mediante la configuración del registrador personalizado

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>Redirección mediante la configuración de la función de registro personalizada

> [!NOTE]
> La función log no surtirá efecto si establece un registrador personalizado.

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

## <a name="override-configuration"></a>Invalidación de la configuración
Puede pasar la configuración personalizada al crear una instancia de TeamsFx para invalidar la configuración predeterminada o establecer los campos obligatorios cuando faltan variables de entorno.

- Si ha creado un proyecto de pestaña con VS Code Toolkit, se usarán los siguientes valores de configuración a partir de variables de entorno preconfiguradas:
  * authorityHost (REACT_APP_AUTHORITY_HOST)
  * tenantId (REACT_APP_TENANT_ID)
  * clientId (REACT_APP_CLIENT_ID)
  * initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL)
  * applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL)
  * apiEndpoint (REACT_APP_FUNC_ENDPOINT)
  * apiName (REACT_APP_FUNC_NAME)

- Si ha creado un proyecto de bot o función de Azure mediante VS Code Toolkit, se usarán los siguientes valores de configuración a partir de variables de entorno preconfiguradas:
  * initiateLoginEndpoint (INITIATE_LOGIN_ENDPOINT)
  * authorityHost (M365_AUTHORITY_HOST)
  * tenantId (M365_TENANT_ID)
  * clientId (M365_CLIENT_ID)
  * clientSecret (M365_CLIENT_SECRET)
  * applicationIdUri (M365_APPLICATION_ID_URI)
  * apiEndpoint (API_ENDPOINT)
  * sqlServerEndpoint (SQL_ENDPOINT)
  * sqlUsername (SQL_USER_NAME)
  * sqlPassword (SQL_PASSWORD)
  * sqlDatabaseName (SQL_DATABASE_NAME)
  * sqlIdentityId (IDENTITY_ID)

## <a name="upgrade-latest-sdk-version"></a>Actualización de la versión más reciente del SDK

Si usa la versión del SDK que tiene `loadConfiguration()`, puede seguir estos pasos para actualizar a la versión más reciente del SDK.
1. Quitar `loadConfiguration()` y pasar la configuración personalizada mediante `new TeamsFx(IdentityType.User, { ...customConfig })`
2. Reemplazar por `new TeamsUserCredential()``new TeamsFx()`
3. Reemplazar por `new M365TenantCredential()``new TeamsFx(IdentityType.App)`
4. Reemplazar por `new OnBehalfOfUserCredential(ssoToken)``new TeamsFx().setSsoToken(ssoToken)`
5. Pasar la instancia de `TeamsFx` a funciones auxiliares para reemplazar la instancia de credencial

Para obtener más información, vea [TeamsFx (clase).](#teamsfx-class)

## <a name="next-step"></a>Paso siguiente

[Ejemplos](https://github.com/OfficeDev/TeamsFx-Samples) de proyecto para obtener ejemplos detallados sobre cómo usar el SDK de TeamsFx.

## <a name="see-also"></a>Ver también

[Galería de ejemplo de Microsoft TeamsFx](https://github.com/OfficeDev/TeamsFx-Samples).
