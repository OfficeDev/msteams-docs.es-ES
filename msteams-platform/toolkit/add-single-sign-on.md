---
title: Incorporación del inicio de sesión único a las aplicaciones de Teams
author: zyxiaoyuer
description: En este módulo, obtenga información sobre cómo agregar el inicio de sesión único (SSO) de Teams Toolkit, habilitar la compatibilidad con SSO y actualizar la aplicación para que use el inicio de sesión único
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 7318ffbfe6c0fff852f493c90afe9a832a827110
ms.sourcegitcommit: e5c45071421d257d68a73406137edff5bdc5a722
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2022
ms.locfileid: "68654515"
---
# <a name="add-single-sign-on-to-teams-app"></a>Agregar inicio de sesión único a la aplicación de Teams

Microsoft Teams proporciona una función de inicio de sesión único para que la aplicación obtenga el token de usuario de Teams que ha iniciado sesión para acceder a Microsoft Graph y a otras API. Teams Toolkit facilita la interacción mediante la abstracción de algunos de los flujos e integraciones de Azure AD detrás de algunas API sencillas. Esto le permite agregar fácilmente características de inicio de sesión único (SSO) a la aplicación teams.

En el caso de las aplicaciones que interactúan con el usuario en un chat, un equipo o un canal, el inicio de sesión único se manifiesta como una tarjeta adaptable con la que el usuario puede interactuar para invocar el flujo de consentimiento de Azure AD.

## <a name="enable-sso-support"></a>Habilitación de la compatibilidad con SSO

Teams Toolkit le ayuda a agregar el inicio de sesión único a las siguientes funcionalidades de Teams:

* Tab
* Bot
* Bot de notificación: restify server
* Bot de comandos
* Extensión de mensaje

### <a name="add-sso-using-visual-studio-code"></a>Incorporación del inicio de sesión único mediante Visual Studio Code

Para agregar el inicio de sesión único mediante Teams Toolkit en Visual Studio Code, siga estos pasos:

1. Abrir **Microsoft Visual Studio Code**.
2. Seleccione :::image type="content" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png" alt-text="Captura de pantalla del kit de herramientas de Teams: ejemplo de la opción Kit de herramientas de Teams en Visual Studio Code."::: desde la barra de navegación izquierda.
3. Seleccione **Agregar características** en **DESARROLLO**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-add features.png" alt-text="Captura de pantalla que muestra la opción Agregar características en la opción Desarrollo de la Visual Studio Code.":::

   * También puede abrir la paleta de comandos y seleccionar **Teams: Agregar características**.

4. Seleccione **Inicio de sesión único**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-select features.png" alt-text="Captura de pantalla que muestra la característica inicio de sesión único resaltada en rojo en el Visual Studio Code.":::

### <a name="add-sso-using-teamsfx-cli"></a>Incorporación del inicio de sesión único mediante la CLI de TeamsFx

Puede ejecutar el `teamsfx add sso` comando en el **directorio raíz del proyecto**.

> [!NOTE]
> La característica habilita el inicio de sesión único para todas las funcionalidades aplicables existentes. Siga los mismos pasos para habilitar el inicio de sesión único si agrega funcionalidad más adelante al proyecto.

## <a name="customize-your-project-using-teams-toolkit"></a>Personalización del proyecto mediante el kit de herramientas de Teams

En la tabla siguiente se enumeran los cambios realizados por Teams Toolkit en el proyecto:

| **Tipo** | **Archivo**                                             | **Finalidad**                                                                                                                                                                               |
| -------- | ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Crear   | `aad.template.json` Bajo `template/appPackage`      | El manifiesto de aplicación de Azure AD representa la aplicación de Azure AD. `template/appPackage` ayuda a registrar una aplicación de Azure AD durante la fase de depuración o aprovisionamiento local.                                |
| Modify   | `manifest.template.json` Bajo `template/appPackage` | Se agrega un `webApplicationInfo` objeto a la plantilla de manifiesto de aplicación de Teams. Teams requiere este campo para habilitar el inicio de sesión único. El cambio está en vigor cuando se desencadena la depuración o el aprovisionamiento locales. |
| Crear   | `auth/tab`                                           | El código de referencia, las páginas de redireccionamiento de autenticación y `README.md` los archivos se generan en esta ruta de acceso para un proyecto de pestaña.                                                                                  |
| Crear   | `auth/bot`                                           | El código de referencia, las páginas de redireccionamiento de autenticación y `README.md` los archivos se generan en esta ruta de acceso para un proyecto de bot.                                                                                  |

> [!NOTE]
> Al agregar el inicio de sesión único, Teams Toolkit no cambia nada en la nube hasta que se desencadena la depuración local. Actualice el código para asegurarse de que el inicio de sesión único funciona en el proyecto.

## <a name="update-your-application-to-use-sso"></a>Actualización de la aplicación para usar el inicio de sesión único

Para habilitar el inicio de sesión único en la aplicación, siga estos pasos:

> [!NOTE]
> Estos cambios se basan en las plantillas que aplicamos al scaffolding.

---

<br>
<br><details>
<summary><b>Proyecto de tabulación </b></summary>

1. Copie `auth-start.html` y `auth-end.htm`\*\* en la carpeta en .`auth/public` `tabs/public/` Teams Toolkit registra estos dos puntos de conexión en Azure AD para el flujo de redireccionamiento de Azure AD.

2. Copie `sso` la carpeta en `auth/tab` en `tabs/src/sso/`.

   * `InitTeamsFx`: el archivo implementa una función que inicializa el SDK de TeamsFx y abre `GetUserProfile` el componente después de inicializar el SDK.

   * `GetUserProfile`: el archivo implementa una función que llama a Microsoft Graph API para obtener información del usuario.

3. Ejecute `npm install @microsoft/teamsfx-react` en `tabs/`.

4. Agregue las líneas siguientes a `tabs/src/components/sample/Welcome.tsx` para importar `InitTeamsFx`:

   ```Bash

   import { InitTeamsFx } from "../../sso/InitTeamsFx";

   ```

5. Reemplace la línea siguiente:

   `<AddSSO />` con `<InitTeamsFx />` para reemplazar el `AddSso` componente por `InitTeamsFx` el componente.

</details>
<details>
<summary><b>Proyecto de bot </b></summary>

#### <a name="set-up-the-azure-ad-redirects"></a>Configuración de las redirecciones de Azure AD

1. Mueva la `auth/bot/public` carpeta a `bot/src`. Esta carpeta contiene páginas HTML que hospeda la aplicación bot. Cuando se inicia el flujo de inicio de sesión único con Azure AD, redirige al usuario a las páginas HTML.
1. Modifique para `bot/src/index` agregar las rutas adecuadas `restify` a las páginas HTML.

   ```ts
   const path = require("path");

   server.get(
     "/auth-*.html",
     restify.plugins.serveStatic({
       directory: path.join(__dirname, "public"),
     })
   );
   ```

#### <a name="update-your-app"></a>Actualizar la aplicación

El controlador de `ProfileSsoCommandHandler` comandos sso usa un token de Azure AD para llamar a Microsoft Graph. Este token se obtiene mediante el token de usuario de Teams que ha iniciado sesión. El flujo se reúne en un cuadro de diálogo que muestra un cuadro de diálogo de consentimiento si es necesario.

1. Mueva el `profileSsoCommandHandler` archivo de la `auth/bot/sso` carpeta a `bot/src`. `ProfileSsoCommandHandler` class es un controlador de comandos sso para obtener información del usuario con el token de SSO, seguir este método y crear su propio controlador de comandos sso.
1. Abra el `package.json` archivo y asegúrese de que la versión del SDK de teamsfx >= 1.2.0.
1. Ejecute el `npm install isomorphic-fetch --save` comando en la `bot` carpeta .
1. Para el script ts, ejecute el `npm install copyfiles --save-dev` comando en la `bot` carpeta y reemplace las líneas siguientes en `package.json`:

   ```json
   "build": "tsc --build && shx cp -r ./src/adaptiveCards ./lib/src",
   ```

   Con

   ```json
   "build": "tsc --build && shx cp -r ./src/adaptiveCards ./lib/src && copyfiles src/public/*.html lib/",
   ```

   Esto copia las páginas HTML que se usan para la redirección de autenticación al compilar el proyecto de bot.

1. Para que el flujo de consentimiento de SSO funcione, reemplace el código siguiente en el `bot/src/index` archivo:

   ```ts
   server.post("/api/messages", async (req, res) => {
     await commandBot.requestHandler(req, res);
   });
   ```

   Con

   ```ts
   server.post("/api/messages", async (req, res) => {
     await commandBot.requestHandler(req, res).catch((err) => {
       // Error message including "412" means it is waiting for user's consent, which is a normal process of SSO, sholdn't throw this error.
       if (!err.message.includes("412")) {
         throw err;
       }
     });
   });
   ```

1. Reemplace las opciones de, por `ConversationBot` ejemplo, en `bot/src/internal/initialize` para agregar la configuración de SSO y el controlador de comandos sso:

   ```ts
   export const commandBot = new ConversationBot({
       ...
       command: {
           enabled: true,
           commands: [new HelloWorldCommandHandler()],
       },
   });
   ```

   Con

   ```ts
   import { ProfileSsoCommandHandler } from "../profileSsoCommandHandler";

   export const commandBot = new ConversationBot({
       ...
       // To learn more about ssoConfig, please refer teamsfx sdk document: https://docs.microsoft.com/microsoftteams/platform/toolkit/teamsfx-sdk
       ssoConfig: {
           aad :{
               scopes:["User.Read"],
           },
       },
       command: {
           enabled: true,
           commands: [new HelloWorldCommandHandler() ],
           ssoCommands: [new ProfileSsoCommandHandler()],
       },
   });
   ```

1. Registre el comando en el manifiesto de aplicación de Teams. Abra `templates/appPackage/manifest.template.json`y agregue las siguientes líneas en `commands` en `commandLists` del bot:

   ```json
   {
     "title": "profile",
     "description": "Show user profile using Single Sign On feature"
   }
   ```

#### <a name="add-a-new-sso-command-to-the-bot-optional"></a>Adición de un nuevo comando sso al bot (opcional)

Después de agregar correctamente el inicio de sesión único en el proyecto, puede agregar un nuevo comando sso.

1. Cree un archivo `photoSsoCommandHandler.ts` como o `photoSsoCommandHandler.js` en `bot/src/` y agregue su propio controlador de comandos de SSO para llamar a Graph API:

   ```TypeScript
   // for TypeScript:
   import { Activity, TurnContext, ActivityTypes } from "botbuilder";
   import "isomorphic-fetch";
   import {
       CommandMessage,
       TriggerPatterns,
       TeamsFx,
       createMicrosoftGraphClient,
       TeamsFxBotSsoCommandHandler,
       TeamsBotSsoPromptTokenResponse,
   } from "@microsoft/teamsfx";

   export class PhotoSsoCommandHandler implements TeamsFxBotSsoCommandHandler {
       triggerPatterns: TriggerPatterns = "photo";

       async handleCommandReceived(
           context: TurnContext,
           message: CommandMessage,
           tokenResponse: TeamsBotSsoPromptTokenResponse,
       ): Promise<string | Partial<Activity> | void> {
           await context.sendActivity("Retrieving user information from Microsoft Graph ...");

           const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

           const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);

           let photoUrl = "";
           try {
               const photo = await graphClient.api("/me/photo/$value").get();
               const arrayBuffer = await photo.arrayBuffer();
               const buffer=Buffer.from(arrayBuffer, 'binary');
               photoUrl = "data:image/png;base64," + buffer.toString("base64");
           } catch {
               // Could not fetch photo from user's profile, return empty string as placeholder.
           }
           if (photoUrl) {
               const photoMessage: Partial<Activity> = {
                   type: ActivityTypes.Message,
                   text: 'This is your photo:',
                   attachments: [
                       {
                           name: 'photo.png',
                           contentType: 'image/png',
                           contentUrl: photoUrl
                       }
                   ]
               };
               return photoMessage;
           } else {
               return "Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.";
           }
       }
   }
   ```

   ```javascript
   // for JavaScript:
   const { ActivityTypes } = require("botbuilder");
   require("isomorphic-fetch");
   const {
     createMicrosoftGraphClient,
     TeamsFx,
   } = require("@microsoft/teamsfx");

   class PhotoSsoCommandHandler {
     triggerPatterns = "photo";

     async handleCommandReceived(context, message, tokenResponse) {
       await context.sendActivity(
         "Retrieving user information from Microsoft Graph ..."
       );

       const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

       const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);

       let photoUrl = "";
       try {
         const photo = await graphClient.api("/me/photo/$value").get();
         const arrayBuffer = await photo.arrayBuffer();
         const buffer = Buffer.from(arrayBuffer, "binary");
         photoUrl = "data:image/png;base64," + buffer.toString("base64");
       } catch {
         // Could not fetch photo from user's profile, return empty string as placeholder.
       }
       if (photoUrl) {
         const photoMessage = {
           type: ActivityTypes.Message,
           text: "This is your photo:",
           attachments: [
             {
               name: "photo.png",
               contentType: "image/png",
               contentUrl: photoUrl,
             },
           ],
         };
         return photoMessage;
       } else {
         return "Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.";
       }
     }
   }

   module.exports = {
     PhotoSsoCommandHandler,
   };
   ```

1. Agregue `PhotoSsoCommandHandler` una instancia a la `ssoCommands` matriz en `bot/src/internal/initialize.ts`:

   ```ts
   // for TypeScript:
   import { PhotoSsoCommandHandler } from "../photoSsoCommandHandler";

   export const commandBot = new ConversationBot({
       ...
       command: {
           ...
           ssoCommands: [new ProfileSsoCommandHandler(), new PhotoSsoCommandHandler()],
       },
   });
   ```

   ```javascript
   // for JavaScript:
   ...
   const { PhotoSsoCommandHandler } = require("../photoSsoCommandHandler");

   const commandBot = new ConversationBot({
       ...
       command: {
           ...
           ssoCommands: [new ProfileSsoCommandHandler(), new PhotoSsoCommandHandler()]
       },
   });
   ...

   ```

1. Registre el comando en el manifiesto de aplicación de Teams. Abra `templates/appPackage/manifest.template.json`y agregue las siguientes líneas en `commands` en `commandLists` del bot:

   ```JSON

   {
       "title": "photo",
       "description": "Show user photo using Single Sign On feature"
   }

   ```

</details>

<details>
<summary><b>Proyecto de extensión de mensaje </b></summary>

La lógica de negocios de ejemplo proporciona un controlador `TeamsBot` que extiende TeamsActivityHandler e invalida `handleTeamsMessagingExtensionQuery`.

Puede actualizar la lógica de consulta en con token `handleMessageExtensionQueryWithToken` , que se obtiene mediante el token de usuario de Teams que ha iniciado sesión.

Para que esto funcione en la aplicación:

1. Mueva la `auth/bot/public` carpeta a `bot`. Esta carpeta contiene páginas HTML que hospeda la aplicación bot. Cuando se inician flujos de inicio de sesión único con Azure AD, Azure AD redirigirá al usuario a estas páginas.

1. Modifique para `bot/index` agregar las rutas adecuadas `restify` a estas páginas.

    ```ts
    const path = require("path");

    server.get(
        "/auth-*.html",
        restify.plugins.serveStatic({
            directory: path.join(__dirname, "public"),
        })
    );
    ```

1. Invalide la `handleTeamsMessagingExtensionQuery` interfaz en `bot/teamsBot`. Puede seguir el código de ejemplo de `handleMessageExtensionQueryWithToken` para realizar su propia lógica de consulta.

1. Abra `bot/package.json`, asegúrese de que `@microsoft/teamsfx` la versión >= 1.2.0

1. Instale `isomorphic-fetch` paquetes npm en el proyecto de bot.

1. (Solo para ts) Instale `copyfiles` paquetes npm en el proyecto del bot, agregue o actualice el script de `bot/package.json` la `build` siguiente manera:

    ```json
    "build": "tsc --build && copyfiles ./public/*.html lib/",
    ```

    Al hacerlo, las páginas HTML usadas para la redirección de autenticación se copiarán al compilar este proyecto de bot.

1. Actualice `templates/appPackage/aad.template.json` los ámbitos que se usan en `handleMessageExtensionQueryWithToken`.

    ```json
    "requiredResourceAccess": [
        {
            "resourceAppId": "Microsoft Graph",
            "resourceAccess": [
                {
                    "id": "User.Read",
                    "type": "Scope"
                }
            ]
        }
    ]
    ```

</details>

<br>

## <a name="debug-your-application"></a>Depure su aplicación

Presione F5 para depurar la aplicación. Teams Toolkit usa el archivo de manifiesto de Azure AD para registrar una aplicación de Azure AD para el inicio de sesión único. Para conocer las funcionalidades de depuración local del kit de herramientas de Teams, consulte [Depuración local de la aplicación de Teams](debug-local.md).

## <a name="customize-azure-ad-application-registration"></a>Personalización del registro de aplicaciones de Azure AD

El [manifiesto de aplicación de Azure AD](/azure/active-directory/develop/reference-app-manifest) permite personalizar varios aspectos del registro de aplicaciones. Puede actualizar el manifiesto según sea necesario. Si necesita incluir más permisos de API para acceder a las API deseadas, consulte [Permisos de API para acceder a las API deseadas](https://github.com/OfficeDev/TeamsFx/wiki/#customize-aad-manifest-template).
Para ver la aplicación de Azure AD en Azure Portal, consulte [Visualización de la aplicación de Azure AD en Azure Portal](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#How-to-view-the-AAD-app-on-the-Azure-portal).

## <a name="sso-authentication-concepts"></a>Conceptos de autenticación de SSO

Los siguientes conceptos le ayudan con la autenticación de SSO:

### <a name="working-of-sso-in-teams"></a>Trabajo del inicio de sesión único en Teams

La autenticación de inicio de sesión único (SSO) en Microsoft Azure Active Directory (Azure AD) actualiza de forma silenciosa el token de autenticación para minimizar el número de veces que los usuarios necesitan escribir sus credenciales de inicio de sesión. Si un usuario otorga su consentimiento para usar la aplicación, no tiene que volver a otorgarlo en otro dispositivo, ya que inicia sesión automáticamente.

Las pestañas y los bots de Teams tienen un flujo similar para la compatibilidad con SSO. Para obtener más información, consulte:

1. [Autenticación de inicio de sesión único (SSO) en pestañas](../tabs/how-to/authentication/tab-sso-overview.md)
1. [Autenticación de inicio de sesión único (SSO) en Bots](../bots/how-to/authentication/auth-aad-sso-bots.md)

### <a name="simplified-sso-with-teamsfx"></a>Inicio de sesión único simplificado con TeamsFx

TeamsFx ayuda a reducir las tareas de desarrollador mediante el inicio de sesión único y el acceso a los recursos en la nube hasta instrucciones de una sola línea con cero configuración.

Con el SDK de TeamsFx, puede escribir código de autenticación de usuario de forma simplificada mediante Credenciales:

1. Identidad de usuario en el entorno del explorador: `TeamsUserCredential` representa la identidad del usuario actual de Teams.
1. Identidad de usuario en Node.js entorno: `OnBehalfOfUserCredential` usa el flujo en nombre de y el token de SSO.
1. Identidad de aplicación en Node.js entorno: `AppCredential` representa la identidad de la aplicación.

Para obtener más información sobre el SDK de TeamsFx, consulte:

* [Referencia de API o SDK de TeamsFx](TeamsFx-SDK.md) [](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true)
* [Galería de ejemplos de Microsoft Teams Framework (TeamsFx)](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2)

## <a name="see-also"></a>Vea también

[Requisitos previos para crear la aplicación de Teams](tools-prerequisites.md)
