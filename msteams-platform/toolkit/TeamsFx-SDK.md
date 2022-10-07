---
title: TeamsFx SDK
author: surbhigupta
description: En este módulo, obtenga información sobre el SDK de TeamsFx, los conceptos básicos y la estructura de código, la personalización avanzada y los escenarios
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: e28e726a1915cdbc8fddf501b0352d160673516c
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499170"
---
# <a name="teamsfx-sdk"></a>TeamsFx SDK

TeamsFx ayuda a reducir las tareas mediante el inicio de sesión único (SSO de Teams) de Microsoft Teams y el acceso a los recursos en la nube a instrucciones de línea única sin configuración. Puede usar el SDK de TeamsFx en el explorador y Node.js entorno. Se puede acceder a las funcionalidades principales de TeamsFx en el entorno de cliente y servidor. Puede escribir código de autenticación de usuario de forma simplificada para:

* Pestaña Teams
* Bot de Teams
* Función de Azure

## <a name="prerequisites"></a>Requisitos previos

Debe instalar las siguientes herramientas y configurar el entorno de desarrollo:

| &nbsp; | Instalar | Para usar... |
   | --- | --- | --- |
   | &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | Entornos de compilación de JavaScript, TypeScript o SharePoint Framework (SPFx). Use la versión 1.55 o posterior. |
   | &nbsp; | [Kit de herramientas de Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Extensión de Microsoft Visual Studio Code que crea un scaffolding de proyecto para la aplicación. Use la versión 4.0.0. |
   | &nbsp; | [Node.js](https://nodejs.org/en/download/) | Entorno de tiempo de ejecución de JavaScript de back-end. Use la versión v16 LTS más reciente.|
   | &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams para colaborar con todos los usuarios con los que trabaja a través de aplicaciones de chat, reuniones, llamadas, todo en un solo lugar.|
   | &nbsp; | [Microsoft&nbsp; Edge](https://www.microsoft.com/edge) (recomendado) o [Google Chrome](https://www.google.com/chrome/) | Un explorador con herramientas de desarrollo. |

> [!NOTE]
> Si el proyecto ha instalado `botbuilder` [paquetes](https://github.com/Microsoft/botbuilder-js#packages) relacionados como dependencias, asegúrese de que son de la misma versión.

Debe tener conocimientos prácticos de:

* [Código fuente](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)
* [Paquete (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx)
* [Documentación de referencia de API](https://aka.ms/teamsfx-sdk-help)
* [Ejemplos](https://github.com/OfficeDev/TeamsFx-Samples)

## <a name="get-started"></a>Comenzar

El SDK de TeamsFx está preconfigurado en un proyecto con scaffolding mediante el kit de herramientas de TeamsFx o la CLI.
Para obtener más información, consulte [Proyecto de la aplicación de Teams](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md).

### <a name="install-the-microsoftteamsfx-package"></a>Instale el paquete `@microsoft/teamsfx`.

Instale el SDK de TeamsFx para TypeScript o JavaScript con `npm`:

```bash
npm install @microsoft/teamsfx
```

## <a name="teamsfx-core-functionalities"></a>Funcionalidades básicas de TeamsFx

### <a name="teamsfx-class"></a>Clase TeamsFx

La instancia de la clase TeamsFx accede a todas las configuraciones de TeamsFx desde las variables de entorno de forma predeterminada. También puede establecer valores de configuración personalizados para invalidar los valores predeterminados. Compruebe la [configuración de invalidación](#override-configuration) para obtener más detalles.
Al crear una instancia de TeamsFx, también debe especificar el tipo de identidad.
Hay dos tipos de identidad:

* **Identidad de usuario**: representa el usuario actual de Teams.
* **Identidad de** la aplicación: representa la propia aplicación.

    > [!NOTE]
    > Para estos dos tipos de identidad, los constructores y métodos de TeamsFx no son los mismos.

Puede obtener más información sobre la identidad de usuario y la identidad de la aplicación en la sección siguiente:

<details>
<summary><b> Identidad de usuario </b></summary>

| Comando | Descripción |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| La aplicación se autentica como usuario actual de Teams. |
| `TeamsFx:setSsoToken()`| Identidad del usuario en el entorno Node.js (sin explorador). |
| `TeamsFx:getUserInfo()` | Para obtener la información de base del usuario. |
| `TeamsFx:login()` | Se usa para permitir que el usuario realice el proceso de consentimiento, si desea usar SSO para obtener el token de acceso para determinados ámbitos de OAuth. |

> [!NOTE]
> Puede acceder a los recursos en nombre del usuario actual de Teams.
</details>

<details>
<summary><b> Identidad de la aplicación </b></summary>

| Comando | Descripción |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| Application  is authenticated as an application. The permission usually needs administrator's approval.|
| `TeamsFx:getCredential()`| Proporciona instancias de credenciales que corresponden automáticamente al tipo de identidad. |

> [!NOTE]
> Necesita el consentimiento del administrador para los recursos.
</details>

### <a name="credential"></a>Credential

Para inicializar TeamsFx, debe elegir el tipo de identidad necesario. Después de especificar el SDK de tipo de identidad, se usa otro tipo de clase de credencial. Representan la identidad y obtienen el token de acceso mediante el flujo de autenticación correspondiente. Las clases de credenciales implementan una `TokenCredential` interfaz que se usa ampliamente en las API de biblioteca de Azure diseñadas para proporcionar tokens de acceso para ámbitos específicos. Otras API se basan en la llamada de credencial `TeamsFx:getCredential()` para obtener una instancia de `TokenCredential`. Para obtener más información sobre las clases relacionadas con credenciales y flujos de autenticación, consulte [carpeta de credenciales](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential).

Hay tres clases de credenciales para simplificar la autenticación. Estos son los escenarios correspondientes para cada destino de clase de credencial.

<details>
<summary><b> Identidad de usuario en el entorno del explorador </b></summary>

`TeamsUserCredential` representa la identidad del usuario actual de Teams. Por primera vez se autentican las credenciales del usuario, el inicio de sesión único de Teams realiza el flujo en nombre de para el intercambio de tokens. El SDK usa esta credencial al elegir la identidad de usuario en el entorno del explorador.

Las configuraciones necesarias son: `initiateLoginEndpoint` y `clientId`.
</details>

<details>
<summary><b> Identidad de usuario en Node.js entorno </b></summary>

`OnBehalfOfUserCredential` usa el flujo en nombre de y requiere el token de INICIO de sesión único de Teams, en escenarios de bot o función de Azure. El SDK de TeamsFx usa la siguiente credencial al elegir la identidad de usuario en Node.js entorno.

Configuración necesaria: `authorityHost`, `tenantId`, `clientId``clientSecret` o `certificateContent`.
</details>

<details>
<summary><b> Identidad de la aplicación en Node.js entorno </b></summary>

`AppCredential` representa la identidad de la aplicación. Puede usar la identidad de la aplicación cuando el usuario no esté implicado, por ejemplo, en un trabajo de automatización desencadenado por el tiempo. El SDK de TeamsFx usa la siguiente credencial al elegir la identidad de la aplicación en Node.js entorno.

Configuración necesaria: `tenantId`, `clientId`, `clientSecret` o `certificateContent`.
</details>

### <a name="bot-sso"></a>Inicio de sesión único de bot

Las clases relacionadas con bots se almacenan en la [carpeta bot](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot).

`TeamsBotSsoPrompt` se integra con bot framework. Simplifica el proceso de autenticación al desarrollar una aplicación bot y desea usar el inicio de sesión único del bot.

Configuración necesaria: `initiateLoginEndpoint`, `tenantId`, `clientId` y `applicationIdUri`.

### <a name="supported-functions"></a>Funciones compatibles

TeamsFx SDK provides several functions to ease the configuration for third-party libraries. They're located under [core folder](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core).

* Microsoft Graph Service:`createMicrosoftGraphClient` y `MsGraphAuthProvider` ayuda para crear una instancia autenticada de Graph.
* SQL:`getTediousConnectionConfig` devuelve una configuración de conexión tediosa.

    Configuración necesaria:

  * Si desea usar la identidad de usuario, se `sqlServerEndpoint`requiere y `sqlPassword` `sqlUsername` .
  * Si desea usar la identidad MSI, se `sqlServerEndpoint`requiere y `sqlIdentityId` .

### <a name="override-configuration"></a>Invalidación de la configuración

Puede pasar la configuración personalizada al crear una nueva `TeamsFx` instancia para invalidar la configuración predeterminada o establecer los campos obligatorios cuando `environment variables` faltan.

<details>
<summary><b> Para el proyecto de pestaña </b> </summary>

Si ha creado un proyecto de pestaña con Microsoft Visual Studio Code Toolkit, se usarán los siguientes valores de configuración a partir de variables de entorno preconfiguradas:

* authorityHost (REACT_APP_AUTHORITY_HOST)
* tenantId (REACT_APP_TENANT_ID)
* clientId (REACT_APP_CLIENT_ID)
* initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL)
* applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL)
* apiEndpoint (REACT_APP_FUNC_ENDPOINT) // solo se usa cuando hay una función back-end
* apiName (REACT_APP_FUNC_NAME) // solo se usa cuando hay una función back-end

</details>

<details>
<summary><b> Para el proyecto de bot o función de Azure </b></summary>

Si ha creado una función de Azure o un proyecto de bot con Visual Studio Code Toolkit, se usarán los siguientes valores de configuración a partir de variables de entorno preconfiguradas:

* initiateLoginEndpoint (INITIATE_LOGIN_ENDPOINT)
* authorityHost (M365_AUTHORITY_HOST)
* tenantId (M365_TENANT_ID)
* clientId (M365_CLIENT_ID)
* clientSecret (M365_CLIENT_SECRET)
* applicationIdUri (M365_APPLICATION_ID_URI)
* apiEndpoint (API_ENDPOINT)

* sqlServerEndpoint (SQL_ENDPOINT) // solo se usa cuando hay una instancia de sql
* sqlUsername (SQL_USER_NAME) // solo se usa cuando hay una instancia de sql
* sqlPassword (SQL_PASSWORD) // solo se usa cuando hay una instancia de sql
* sqlDatabaseName (SQL_DATABASE_NAME) // solo se usa cuando hay una instancia de sql
* sqlIdentityId (IDENTITY_ID) // solo se usa cuando hay una instancia de sql

</details>

### <a name="error-handling"></a>Control de errores

El tipo básico de respuesta de error de API es `ErrorWithCode`, que contiene el código de error y el mensaje de error. Por ejemplo, para filtrar un error específico, puede usar el siguiente fragmento de código:

```typescript
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

## <a name="microsoft-graph-scenarios"></a>Escenarios de Microsoft Graph

En esta sección se proporcionan varios fragmentos de código para escenarios comunes relacionados con Microsoft Graph. En estos escenarios, el usuario puede llamar a las API mediante permisos diferentes en distintos extremos (front-end/back-end).

* Permiso delegado de usuario en front-end (Usar TeamsUserCredential) <details>
    <summary><b>Uso de Graph API en la aplicación de pestaña</b></summary>

    Este fragmento de código muestra cómo usar `TeamsFx` y `createMicrosoftGraphClient` obtener perfiles de usuario de Microsoft Graph. También muestra cómo detectar y resolver un objeto `GraphError`.

    1. Importe las clases necesarias.

    ```typescript
    import {
      createMicrosoftGraphClient,
      TeamsFx,
    } from "@microsoft/teamsfx";
    ```

    2. Use `TeamsFx.login()` para obtener el consentimiento del usuario.

    ```typescript
    // Put these code in a call-to-action callback function to avoid browser blocking automatically showing up pop-ups.
    await teamsfx.login(["User.Read"]); // Login with scope
    ```

    3. Puede inicializar una instancia de TeamsFx y un cliente de grafos y obtener información de MS Graph por parte de este cliente.

    ```typescript
    try {
      const teamsfx = new TeamsFx();
      const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
      const profile = await graphClient.api("/me").get();
    } catch (err: unknown) {
      // ErrorWithCode is handled by Graph client
      if (err instanceof GraphError && err.code?.includes(ErrorCode.UiRequiredError)) {
        // Need to show login button to ask for user consent.
      }
    }
    ```

    Para obtener más información sobre el ejemplo para usar Graph API en la aplicación de pestañas, consulte el [ejemplo hello-world-tab](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab).

    </details>

    <details>
    <summary><b>Integración con Microsoft Graph Toolkit</b></summary>

    La biblioteca [del kit de herramientas de Microsoft Graph](https://aka.ms/mgt) es una colección de diversos proveedores de autenticación y componentes de interfaz de usuario con tecnología de Microsoft Graph.

    El `@microsoft/mgt-teamsfx-provider` paquete expone la clase que usa `TeamsFx` la `TeamsFxProvider` clase para iniciar sesión a los usuarios y adquirir tokens para usarlos con Microsoft Graph.

    1. Puede instalar los siguientes paquetes necesarios:

    ```bash
    npm install @microsoft/mgt-element @microsoft/mgt-teamsfx-provider @microsoft/teamsfx
    ```

    2. Inicialice el proveedor dentro del componente.

    ```typescript
     // Import the providers and credential at the top of the page
    import {Providers} from '@microsoft/mgt-element';
    import {TeamsFxProvider} from '@microsoft/mgt-teamsfx-provider';
    import {TeamsUserCredential} from "@microsoft/teamsfx";

    const scope = ["User.Read"];
    const teamsfx = new TeamsFx();
    const provider = new TeamsFxProvider(teamsfx, scope);
    Providers.globalProvider = provider;   
    ```

    3. Puede usar el método para obtener el `teamsfx.login(scopes)` token de acceso necesario.

    ```typescript
    // Put these code in a call-to-action callback function to avoid browser blocking automatically showing up pop-ups. 
    await teamsfx.login(this.scope);
    Providers.globalProvider.setState(ProviderState.SignedIn);
    ```

    4. Ahora puede agregar cualquier componente en la página HTML o en el `render()` método con React para usar el `TeamsFx` contexto para acceder a Microsoft Graph.

    ```html
    <mgt-person query="me" view="threeLines"></mgt-person>
    ```

    ```typescript
    public render(): void {
    return (
        <div>
            <Person personQuery="me" view={PersonViewType.threelines}></Person>
        </div>
    );
    }    
    ```

    Para obtener más información sobre el ejemplo para inicializar el proveedor TeamsFx, vea el [ejemplo De exportador de contactos](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/graph-toolkit-contact-exporter).

    </details>

* Permiso delegado de usuario en back-end (use OnBehalfOfUserCredential) <details>
    <summary><b>Uso de Graph API en la aplicación bot</b></summary>

    Este fragmento de código muestra cómo usar `TeamsBotSsoPrompt` para establecer un cuadro de diálogo y, a continuación, iniciar sesión para obtener un token de acceso.

    1. Inicializar y agregar `TeamsBotSsoPrompt` al conjunto de diálogos.

    ```typescript
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
    ```

    2. Inicie el cuadro de diálogo e inicie sesión.

    ```typescript
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

    Para obtener más información sobre el ejemplo para usar Graph API en la aplicación bot, consulte [ejemplo bot-sso](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/bot-sso).

    </details>

    <details>
    <summary><b>Uso de Graph API en la extensión de mensaje</b></summary>

    Este fragmento de código muestra cómo invalidar `handleTeamsMessagingExtensionQuery` las extensiones de `TeamsActivityHandler`y el uso `handleMessageExtensionQueryWithToken` proporcionado por el sdk de TeamsFx para iniciar sesión para obtener un token de acceso:

    ```typescript
    public async handleTeamsMessagingExtensionQuery(context: TurnContext, query: any): Promise<any> {
      return await handleMessageExtensionQueryWithToken(context, null, 'User.Read', 
        async (token: MessageExtensionTokenResponse) => {
          // ... continue to query with access token ...
        });
    }    
    ```

    Para obtener más información sobre el ejemplo para usar graph API en la extensión de mensaje, consulte [message-extension-sso-sample](https://aka.ms/teamsfx-me-sso-sample).
    </details>

    <details>
    <summary><b>Uso de Graph API en el bot de comandos</b></summary>

    Este fragmento de código muestra cómo implementar `TeamsFxBotSsoCommandHandler` para que el bot de comandos llame a La API de Microsoft.

    ```typescript
    import { Activity, TurnContext } from "botbuilder";
    import {
      CommandMessage,
      TriggerPatterns,
      TeamsFx,
      createMicrosoftGraphClient,
      TeamsFxBotSsoCommandHandler,
      TeamsBotSsoPromptTokenResponse,
    } from "@microsoft/teamsfx";

    export class ProfileSsoCommandHandler implements TeamsFxBotSsoCommandHandler {
      triggerPatterns: TriggerPatterns = "profile";

      async handleCommandReceived(
        context: TurnContext,
        message: CommandMessage,
        tokenResponse: TeamsBotSsoPromptTokenResponse,
      ): Promise<string | Partial<Activity> | void> {
        // Init TeamsFx instance with SSO token
        const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

        // Add scope for your Azure AD app. For example: Mail.Read, etc.
        const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
      
        // Call graph api use `graph` instance to get user profile information
        const me = await graphClient.api("/me").get();

        if (me) {
          // Bot will send the user profile info to user
          return `Your command is '${message.text}' and you're logged in as ${me.displayName}`;
        } else {
          return "Could not retrieve profile information from Microsoft Graph.";
        }
      }
    }    
    ```

    Para obtener más información sobre cómo usar esta clase en el bot de comandos, consulte [Agregar inicio de sesión único a la aplicación Teams](add-single-sign-on.md). Y también hay un proyecto de ejemplo [command-bot-with-sso](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/command-bot-with-sso) , que puede probar el bot de comandos de sso.

    </details>

    <details>
    <summary><b>Llamada a la función de Azure en la aplicación de pestaña: flujo en nombre de</b></summary>

    Este fragmento de código muestra cómo usar `CreateApiClient` o `axios` biblioteca para llamar a Azure Function y cómo llamar a Graph API en la función de Azure para obtener perfiles de usuario.

    1. Puede usar `CreateApiClient` el sdk de TeamsFx para llamar a Azure Function:

    ```typescript
    async function callFunction(teamsfx?: TeamsFx) {
      const teamsfx = new TeamsFx();

      // Get the credential.
      const credential = teamsfx.getCredential(); 
      // Create an API client by providing the token and endpoint.
      const apiClient = CreateApiClient(
        teamsfx.getConfig("YOUR_API_ENDPOINT"), // Create an API Client that uses SSO token to authenticate requests
        new BearerTokenAuthProvider(async () =>  (await credential.getToken(""))!.token) // Call API hosted in Azure Functions on behalf of user to inject token to request header
      );

      // Send a GET request to "RELATIVE_API_PATH", "/api/functionName" for example.
      const response = await apiClient.get("RELATIVE_API_PATH");
      return response.data;
    }    
    ```

    También puede usar `axios` la biblioteca para llamar a Azure Function.

    ```typescript
    async function callFunction(teamsfx?: TeamsFx) {
      const accessToken = await teamsfx.getCredential().getToken(""); // Get SSO token 
      // teamsfx.getConfig("apiEndpoint") will read REACT_APP_FUNC_ENDPOINT environment variable 
      const endpoint = teamsfx.getConfig("apiEndpoint");
      const response = await axios.default.get(endpoint + "/api/" + functionName, {
        headers: {
          authorization: "Bearer " + accessToken.token,
        },
      });
      return response.data;
    }    
    ```

    2. Llame a Graph API en la función de Azure en nombre del usuario en respuesta.

    ```typescript
    export default async function run(
      context: Context,
      req: HttpRequest,
      teamsfxContext: TeamsfxContext
    ): Promise<Response> {
      const res: Response = { status: 200, body: {},};
      // ...
      teamsfx = new TeamsFx().setSsoToken(accessToken);
      // Query user's information from the access token.
      try {
        const currentUser: UserInfo = await teamsfx.getUserInfo();
        if (currentUser && currentUser.displayName) {
          res.body.userInfoMessage = `User display name is ${currentUser.displayName}.`;
        } else {
          res.body.userInfoMessage = "No user information was found in access token.";
        }
      } catch (e) {
      }
      // Create a graph client to access user's Microsoft 365 data after user has consented.
      try {
        const graphClient: Client = createMicrosoftGraphClient(teamsfx, [".default"]);
        const profile: any = await graphClient.api("/me").get();
        res.body.graphClientMessage = profile;
      } catch (e) {
      }
      return res;
    }    
    ```

    Para obtener más información sobre el ejemplo para usar Graph API en la aplicación bot, consulte  [ejemplo hello-world-tab-with-backend](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab-with-backend).

    </details>

* Permiso de aplicación en back-end <details>
    <summary><b>Uso de la autenticación basada en certificados en Azure Function</b></summary>

    Este fragmento de código muestra cómo usar el permiso de aplicación basado en certificados para obtener el token que se puede usar para llamar a Graph API.

    1. Puede inicializar `authConfig` proporcionando un `PEM-encoded key certificate`objeto .

    ```typescript
    const authConfig = {
      clientId: process.env.M365_CLIENT_ID,
      certificateContent: "The content of a PEM-encoded public/private key certificate",
      authorityHost: process.env.M365_AUTHORITY_HOST,
      tenantId: process.env.M365_TENANT_ID,
    };    
    ```

    2. Puede usar para `authConfig` obtener el token.

    ```typescript
    const teamsfx = new TeamsFx(IdentityType.App);
    teamsfx.setCustomeConfig(authConfig);
    const token = teamsfx.getCredential().getToken();    
    ```

    </details>

    <details>
    <summary><b>Uso de la autenticación de secreto de cliente en Azure Function</b></summary>

    Este fragmento de código muestra cómo usar el permiso de aplicación secreta de cliente para obtener el token que se puede usar para llamar a Graph API.

    1. Puede inicializar `authConfig` proporcionando un `client secret`objeto .

    ```typescript
    const authConfig = {
      clientId: process.env.M365_CLIENT_ID,
      clientSecret: process.env.M365_CLIENT_SECRET,
      authorityHost: process.env.M365_AUTHORITY_HOST,
      tenantId: process.env.M365_TENANT_ID,
    };    
    ```

    2. Puede usar para `authConfig` obtener el token.

    ```typescript
    const teamsfx = new TeamsFx(IdentityType.App);
    teamsfx.setCustomeConfig(authConfig);
    const token = teamsfx.getCredential().getToken();    
    ```

    Para obtener más información sobre el ejemplo para usar Graph API en la aplicación bot, consulte el [ejemplo hello-world-tab-with-backend](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab-with-backend).

    </details>

## <a name="other-scenarios"></a>Otros escenarios

En esta sección se proporcionan varios fragmentos de código para otros escenarios relacionados con Microsoft Graph. Puede crear un cliente de API en Bot o Azure Function y acceder a SQL Database en Azure Function.

  <details>
  <summary><b>Creación de un cliente de API para llamar a la API existente en Bot o Azure Function</b></summary>

  Este fragmento de código muestra cómo llamar a una API existente en Bot by `ApiKeyProvider`.

  ```typescript
  const teamsfx = new TeamsFx();

  // Create an API Key auth provider. In addition to APiKeyProvider, following auth providers are also available:
  // BearerTokenAuthProvider, BasicAuthProvider, CertificateAuthProvider.
  const authProvider = new ApiKeyProvider("YOUR_API_KEY_NAME",
    teamsfx.getConfig("YOUR_API_KEY_VALUE"), // This reads the value of YOUR_API_KEY_VALUE environment variable.
    ApiKeyLocation.Header
  );

  // Create an API client using above auth provider.
  // You can also implement AuthProvider interface and use it here.
  const apiClient = createApiClient(
    teamsfx.getConfig("YOUR_API_ENDPOINT"), // This reads YOUR_API_ENDPOINT environment variable.
    authProvider
  );

  // Send a GET request to "RELATIVE_API_PATH", "/api/apiname" for example.
  const response = await apiClient.get("RELATIVE_API_PATH");  
  ```

  </details>

  <details>
  <summary><b>Acceso a la base de datos SQL en Azure Function</b></summary>

  Use `tedious` la biblioteca para acceder a SQL y usar `DefaultTediousConnectionConfiguration` que administre la autenticación. También puede crear la configuración de conexión de otras bibliotecas SQL en función del resultado de `sqlConnectionConfig.getConfig()`.

  1. Establezca la configuración de conexión.

  ```typescript
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
  const config2 = await getTediousConnectionConfig(teamsfx, "your database name");  
  ```

  2. Conéctese a la base de datos.

  ```typescript
  const connection = new Connection(config);
  connection.on("connect", (error) => {
    if (error) {
      console.log(error);
    }
  });  
  ```

  > [!NOTE]
  > Para obtener más información sobre el ejemplo para acceder a sql database en la función de Azure, consulte [ejemplo de share-now](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/share-now).

</details>

## <a name="advanced-customization"></a>Personalización avanzada

### <a name="configure-log"></a>Configuración del registro

Puede establecer el nivel de registro del cliente y redirigir las salidas al usar esta biblioteca.

> [!NOTE]
> El registro está desactivado de forma predeterminada, puede activarlo estableciendo el nivel de registro.

#### <a name="enable-log-by-setting-log-level"></a>Habilitación del registro mediante la configuración del nivel de registro

Cuando se establece el nivel de registro, el registro se habilita. Imprime información de registro en la consola de forma predeterminada.

Establezca el nivel de registro mediante el siguiente fragmento de código:

```typescript
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

> [!NOTE]
> Puede redirigir la salida del registro estableciendo una función de registro o registrador personalizada.

#### <a name="redirect-by-setting-custom-logger"></a>Redireccionamiento mediante la configuración del registrador personalizado

```typescript
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>Redireccionamiento mediante la configuración de la función de registro personalizada

```typescript
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

> [!NOTE]
> Las funciones de registro no surten efecto si establece un registrador personalizado.

## <a name="upgrade-latest-sdk-version"></a>Actualizar la versión más reciente del SDK

Si usa la versión del SDK que tiene `loadConfiguration()`, puede seguir estos pasos para actualizar a la versión más reciente del SDK:

1. Quite `loadConfiguration()` y pase la configuración personalizada mediante `new TeamsFx(IdentityType.User, { ...customConfig })`
2. Reemplazar `new TeamsUserCredential()` por `new TeamsFx()`.
3. Reemplazar `new M365TenantCredential()` por `new TeamsFx(IdentityType.App)`.
4. Reemplazar `new OnBehalfOfUserCredential(ssoToken)` por `new TeamsFx().setSsoToken(ssoToken)`.
5. Pase la instancia de `TeamsFx` a las funciones auxiliares para reemplazar la instancia de credenciales.

## <a name="next-step"></a>Paso siguiente

Para obtener ejemplos detallados sobre cómo usar el proyecto de [ejemplos](https://github.com/OfficeDev/TeamsFx-Samples) del SDK de TeamsFx.

## <a name="see-also"></a>Consulte también

[Galería de muestra de Microsoft TeamsFx](https://github.com/OfficeDev/TeamsFx-Samples).
