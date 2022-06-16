---
title: Agregar inicio de sesión único a las aplicaciones de Teams
author: zyxiaoyuer
description: Describe Agregar inicio de sesión único de Teams Toolkit
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: e9b45f1bd95140eae8da851544dfa4ee87646225
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123450"
---
# <a name="add-single-sign-on-to-teams-app"></a>Agregar inicio de sesión único a la aplicación de Teams

Microsoft Teams proporciona una función de inicio de sesión único para que la aplicación obtenga el token de usuario Teams que ha iniciado sesión para acceder a Microsoft Graph y a otras API. Teams Toolkit facilita la interacción mediante la abstracción de algunos de los flujos e integraciones de Azure AD detrás de algunas API sencillas. Esto le permite agregar fácilmente características de inicio de sesión único (SSO) a la aplicación de Teams.

En el caso de las aplicaciones que interactúan con el usuario en un chat, un equipo o un canal, el inicio de sesión único se manifiesta como una tarjeta adaptable con la que el usuario puede interactuar para invocar el flujo de consentimiento de Azure AD.

## <a name="enable-sso-support"></a>Habilitación de la compatibilidad con SSO

Teams Toolkit le ayuda a agregar sso a las siguientes funcionalidades de Teams:

* Tab
* Bot
* Bot de notificación: restify server
* Bot de comandos

### <a name="add-sso-using-visual-studio-code"></a>Incorporación del inicio de sesión único mediante Visual Studio Code

Los pasos siguientes le ayudan a agregar el inicio de sesión único mediante Teams Toolkit en Visual Studio Code

1. Abrir **Microsoft Visual Studio Code**.
2. Seleccione Teams Toolkit :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/teams-toolkit-sidebar-icon.png" alt-text="sso add sidebar (Agregar barra lateral de inicio de sesión único)"::: en la barra de navegación izquierda.
3. Seleccione **Agregar características** en **DESARROLLO**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-add features.png" alt-text="sso add features":::

    * También puede abrir la paleta de comandos y seleccionar **Teams: Agregar características**

4. Seleccione **Inicio de sesión único**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-select features.png" alt-text="sso select":::

### <a name="add-sso-using-teamsfx-cli"></a>Incorporación del inicio de sesión único mediante la CLI de TeamsFx

Puede ejecutar el `teamsfx add sso` comando en el **directorio raíz del proyecto**.

> [!Note]
> La característica habilita el inicio de sesión único para todas las funcionalidades aplicables existentes. Siga los mismos pasos para habilitar el inicio de sesión único si agrega funcionalidad más adelante al proyecto.

## <a name="customize-your-project-using-teams-toolkit"></a>Personalización del proyecto mediante Teams Toolkit

En la tabla siguiente se enumeran los cambios Teams Toolkit realizados en el proyecto:

   |**Tipo**|**Archivo**|**Finalidad**|
   |--------|--------|-----------|
   |Crear|`aad.template.json` Bajo `template/appPackage`|El manifiesto de aplicación de Azure AD representa la aplicación de Azure AD. `template/appPackage` ayuda a registrar una aplicación de Azure AD durante la fase de depuración o aprovisionamiento local.|
   |Modify|`manifest.template.json` Bajo `template/appPackage`|Se agrega un `webApplicationInfo` objeto a la plantilla de manifiesto de aplicación de Teams. Teams requiere este campo para habilitar el inicio de sesión único. El cambio está en vigor cuando se desencadena la depuración o el aprovisionamiento locales.|
   |Crear|`auth/tab`|El código de referencia, las páginas de redirección de autenticación y un `README.md` archivo se generan en esta ruta de acceso para un proyecto de pestaña.|
   |Crear|`auth/bot`|El código de referencia, las páginas de redirección de autenticación y un `README.md` archivo se generan en esta ruta de acceso para un proyecto de bot.|

> [!Note]
> Al agregar sso, Teams Toolkit no cambia nada en la nube hasta que se desencadena la depuración local. Actualice el código para asegurarse de que el inicio de sesión único funciona en el proyecto.

## <a name="update-your-application-to-use-sso"></a>Actualización de la aplicación para usar el inicio de sesión único

Los pasos siguientes le ayudan a habilitar el inicio de sesión único en la aplicación.

> [!NOTE]
> Estos cambios se basan en las plantillas que aplicamos al scaffolding.

---
<br>
<br><details>
<summary><b>Proyecto de tabulación </b></summary>

1. Copie `auth-start.html` y `auth-end.htm`** en la carpeta en `auth/public` `tabs/public/`. Teams Toolkit registra estos dos puntos de conexión en Azure AD para el flujo de redireccionamiento de Azure AD.

2. Copie `sso` la carpeta en `auth/tab` en `tabs/src/sso/`.

    * `InitTeamsFx`: el archivo implementa una función que inicializa el SDK de TeamsFx y abre `GetUserProfile` el componente después de inicializar el SDK.

    * `GetUserProfile`: el archivo implementa una función que llama a Microsoft Graph API para obtener información del usuario.

3. Ejecute `npm install @microsoft/teamsfx-react` en `tabs/`.

4. Agregue las líneas siguientes a `tabs/src/components/sample/Welcome.tsx` para importar `InitTeamsFx`:

    ```Bash

    import { InitTeamsFx } from "../../sso/InitTeamsFx";

    ```

5. Reemplace la línea siguiente: `<AddSSO />` por `<InitTeamsFx />` para reemplazar el `AddSso` componente por `InitTeamsFx` el componente.

</details>
<details>
<summary><b>Proyecto de bot </b></summary>

1. Copie `auth/bot/public` la carpeta en `bot/src`. Las dos carpetas contienen páginas HTML usadas para la redirección de autenticación; es necesario modificar `bot/src/index` el archivo para agregar enrutamiento a estas páginas.

2. Copie `auth/bot/sso` la carpeta en `bot/src`. Las dos carpetas contienen tres archivos como referencia para la implementación de SSO:

    * `showUserInfo`: implementa una función para obtener información del usuario con el token de SSO. Puede seguir esto para crear su propio método que requiera el token de SSO.

    * `ssoDialog`: crea un [ComponentDialog](/javascript/api/botbuilder-dialogs/componentdialog?view=botbuilder-ts-latest&preserve-view=true) que se usa para el inicio de sesión único.

    * `teamsSsoBot`: crea un [TeamsActivityHandler](/javascript/api/botbuilder/teamsactivityhandler?view=botbuilder-ts-latest&preserve-view=true) con `ssoDialog` y agrega `showUserInfo` como un comando que se puede desencadenar.

3. Siga el ejemplo de código y registre su propio comando con `addCommand` en este archivo (opcional).

4. Ejecute `npm install isomorphic-fetch` en `bot/`.

5. Ejecute `npm install copyfiles` en `bot/` y reemplace la siguiente línea en package.json:
  
   ```JSON

   "build": "tsc --build",

    ```

   Con

   ```JSON

   "build": "tsc --build && copyfiles public/*.html lib/",

   ```

   Las páginas HTML usadas para la redirección de autenticación se copian al compilar este proyecto de bot.

6. Después de agregar los siguientes archivos, debe crear una nueva `teamsSsoBot` instancia en `bot/src/index` el archivo. Reemplace el código siguiente:

   ```Bash
  
   // Process Teams activity with Bot Framework.
   server.post("/api/messages", async (req, res) => {
   await commandBot.requestHandler(req, res);
   });  

   ```

   Con

   ```Bash

   const handler = new TeamsSsoBot();
   // Process Teams activity with Bot Framework.
   server.post("/api/messages", async (req, res) => {
       await commandBot.requestHandler(req, res, async (context)=> {
           await handler.run(context);
       });
   });

   ```

7. Agregue las rutas HTML en el `bot/src/index` archivo:

   ```Bash

   server.get(
       "/auth-*.html",
       restify.plugins.serveStatic({
           directory: path.join(__dirname, "public"),
       })
   );

   ```

8. Agregue las líneas siguientes a `bot/src/index` para importar `teamsSsoBot` y `path`:

   ```Bash

   // For ts:
   import { TeamsSsoBot } from "./sso/teamsSsoBot";
   const path = require("path");

   // For js:
   const { TeamsSsoBot } = require("./sso/teamsSsoBot");
   const path = require("path");

   ```

9. Registre el comando en el manifiesto de la aplicación Teams. Abra `templates/appPackage/manifest.template.json`y agregue las siguientes líneas en `command` en `commandLists` del bot:

   ```JSON

   {
       "title": "show",
       "description": "Show user profile using Single Sign On feature"
   }

   ```

</details>
<details>
<summary><b>Adición de un nuevo comando al bot </b></summary>

> [!NOTE]
> Actualmente, estas instrucciones se aplican a `command bot`. Si comienza con , `bot`consulte [el ejemplo bot-sso](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/bot-sso).

Los pasos siguientes le ayudan a agregar un nuevo comando, después de agregar el inicio de sesión único en el proyecto:

1. Cree un nuevo archivo (`todo.ts` o `todo.js`) en `bot/src/` y agregue su propia lógica de negocios para llamar a Graph API:

# <a name="typescript"></a>[TypeScript](#tab/typescript)

   ```typescript
   // for TypeScript:
export async function showUserImage(
    context: TurnContext,
    ssoToken: string,
    param: any[]
): Promise<DialogTurnResult> {
    await context.sendActivity("Retrieving user photo from Microsoft Graph ...");

    // Init TeamsFx instance with SSO token
    const teamsfx = new TeamsFx().setSsoToken(ssoToken);

    // Update scope here. For example: Mail.Read, etc.
    const graphClient = createMicrosoftGraphClient(teamsfx, param[0]);
    
    // You can add following code to get your photo:
    // let photoUrl = "";
    // try {
    //   const photo = await graphClient.api("/me/photo/$value").get();
    //   photoUrl = URL.createObjectURL(photo);
    // } catch {
    //   // Could not fetch photo from user's profile, return empty string as placeholder.
    // }
    // if (photoUrl) {
    //   await context.sendActivity(
    //     `You can find your photo here: ${photoUrl}`
    //   );
    // } else {
    //   await context.sendActivity("Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.");
    // }

    return;
}  
   ```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

   ```javaScript
   // for JavaScript:
export async function showUserImage(context, ssoToken, param) {
    await context.sendActivity("Retrieving user photo from Microsoft Graph ...");

    // Init TeamsFx instance with SSO token
    const teamsfx = new TeamsFx().setSsoToken(ssoToken);

    // Update scope here. For example: Mail.Read, etc.
    const graphClient = createMicrosoftGraphClient(teamsfx, param[0]);
    
    // You can add following code to get your photo:
    // let photoUrl = "";
    // try {
    //   const photo = await graphClient.api("/me/photo/$value").get();
    //   photoUrl = URL.createObjectURL(photo);
    // } catch {
    //   // Could not fetch photo from user's profile, return empty string as placeholder.
    // }
    // if (photoUrl) {
    //   await context.sendActivity(
    //     `You can find your photo here: ${photoUrl}`
    //   );
    // } else {
    //   await context.sendActivity("Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.");
    // }

    return;
}
   ```

---

2. Registro de un nuevo comando

   * Agregue la siguiente línea para el nuevo registro de comandos mediante `addCommand` en `teamsSsoBot`:

     ```bash

     this.dialog.addCommand("ShowUserProfile", "show", showUserInfo);

     ```

   * Agregue las líneas siguientes después de la línea anterior para registrar un nuevo comando `photo` y enlazar con el método `showUserImage` agregado anteriormente:

     ```bash

     // As shown here, you can add your own parameter into the `showUserImage` method
     // You can also use regular expression for the command here
     const scope = ["User.Read"];
     this.dialog.addCommand("ShowUserPhoto", new RegExp("photo\s*.*"), showUserImage, scope);

     ```

3. Registre el comando en el manifiesto de la aplicación Teams. Abra `templates/appPackage/manifest.template.json`y agregue las siguientes líneas en `command` en `commandLists` del bot:

   ```JSON

   {
       "title": "photo",
       "description": "Show user photo using Single Sign On feature"
   }

   ```

</details>
<br>

## <a name="debug-your-application"></a>Depure su aplicación

Presione F5 para depurar la aplicación. Teams Toolkit usa el archivo de manifiesto de Azure AD para registrar una aplicación de Azure AD para el inicio de sesión único. Para obtener Teams Toolkit funcionalidades de depuración local, consulte [Depuración local de la aplicación de Teams](debug-local.md).

## <a name="customize-azure-ad-application-registration"></a>Personalización del registro de aplicaciones de Azure AD

El [manifiesto de aplicación de Azure AD](/azure/active-directory/develop/reference-app-manifest) permite personalizar varios aspectos del registro de aplicaciones. Puede actualizar el manifiesto según sea necesario. Si necesita incluir permisos de API adicionales para acceder a las API deseadas, consulte [Permisos de API para acceder a las API deseadas](https://github.com/OfficeDev/TeamsFx/wiki/#customize-aad-manifest-template).
Para ver la aplicación de Azure AD en Azure Portal, consulte [Visualización de la aplicación de Azure AD en Azure Portal](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#How-to-view-the-AAD-app-on-the-Azure-portal).

## <a name="sso-authentication-concepts"></a>Conceptos de autenticación de SSO

Los siguientes conceptos le ayudan a realizar la autenticación de SSO:

### <a name="working-of-sso-in-teams"></a>Trabajo del inicio de sesión único en Teams

La autenticación de inicio de sesión único (SSO) en Microsoft Azure Active Directory (Azure AD) actualiza de forma silenciosa el token de autenticación para minimizar el número de veces que los usuarios necesitan escribir sus credenciales de inicio de sesión. Si un usuario otorga su consentimiento para usar la aplicación, no tiene que volver a otorgarlo en otro dispositivo, ya que inicia sesión automáticamente.

Teams pestañas y bots tienen un flujo similar para la compatibilidad con SSO. Para obtener más información, consulte:

1. [Autenticación de inicio de sesión único (SSO) en pestañas](../tabs/how-to/authentication/tab-sso-overview.md)
2. [Autenticación de inicio de sesión único (SSO) en Bots](../bots/how-to/authentication/auth-aad-sso-bots.md)

### <a name="simplified-sso-with-teamsfx"></a>Inicio de sesión único simplificado con TeamsFx

TeamsFx ayuda a reducir las tareas de desarrollador mediante el inicio de sesión único y el acceso a los recursos en la nube hasta instrucciones de una sola línea con cero configuración.

Con el SDK de TeamsFx, puede escribir código de autenticación de usuario de forma simplificada mediante Credenciales:

1. Identidad de usuario en el entorno del explorador: `TeamsUserCredential` representa Teams identidad del usuario actual.
2. Identidad de usuario en Node.js entorno: `OnBehalfOfUserCredentail` usa el flujo en nombre de y el token de SSO.
3. Identidad de aplicación en Node.js entorno: `AppCredential` representa la identidad de la aplicación.

Para obtener más información sobre el SDK de TeamsFx, consulte:

* [Referencia de API o SDK de TeamsFx](TeamsFx-SDK.md) [](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true)
* [Galería de ejemplo de Microsoft Teams Framework (TeamsFx)](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2)

## <a name="see-also"></a>Consulte también

* [Preparar cuentas para crear aplicaciones de Teams](accounts.md)
