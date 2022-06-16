---
title: Compatibilidad con inicio de sesión único para bots
description: Describe cómo obtener un token de usuario. Actualmente, un desarrollador de bots puede usar una tarjeta de inicio de sesión o el servicio de bot de Azure con la compatibilidad con la tarjeta OAuth.
keywords: token, token de usuario, compatibilidad con SSO para bots, permiso, Microsoft Graph, Azure AD
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: c10fe639417ad71814b060ba70e6a33c4ae4038f
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123471"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Compatibilidad con inicio de sesión único (SSO) para bots

La autenticación de inicio de sesión único en Microsoft Azure Active Directory (Azure AD) actualiza de forma silenciosa el token de autenticación para minimizar el número de veces que los usuarios necesitan escribir sus credenciales de inicio de sesión. Si un usuario otorga su consentimiento para usar la aplicación, no tiene que volver a otorgarlo en otro dispositivo, ya que inicia sesión automáticamente. Las pestañas y los bots tienen un flujo similar para la compatibilidad con SSO. Pero el bot [solicita tokens](#request-a-bot-token) y [recibe respuestas](#receive-the-bot-token) con un protocolo diferente.

>[!NOTE]
> OAuth 2.0 es un estándar abierto para la autenticación y autorización usado por Azure Active Directory (Azure AD) y otros muchos proveedores de identidad. Tener conocimientos básicos del flujo de concesión implícito de OAuth 2.0 es un requisito previo para trabajar con la autenticación en pestañas de Microsoft Teams.

## <a name="bot-sso-at-runtime"></a>Bot SSO en tiempo de ejecución

En la imagen siguiente se muestra el flujo del inicio de sesión único en bots:

![Diagrama del inicio de sesión único en tiempo de ejecución del bot](../../../assets/images/bots/bots-sso-diagram.png)

Los pasos siguientes le ayudan con la autenticación y los tokens de aplicación del bot:

1. El bot envía un mensaje a Teams con una OAuthCard que contiene `tokenExchangeResource` para obtener un token de autenticación para la aplicación del bot. El usuario recibe mensajes en todos los puntos de conexión de usuario activos.

   > [!NOTE]
   >
   > * Un usuario puede tener más de un punto de conexión activo a la vez.
   > * El token del bot se recibe de cada punto de conexión de usuario activo.
   > * La aplicación debe instalarse en el ámbito personal para la compatibilidad con SSO.

1. Si el usuario actual usa la aplicación del bot por primera vez, se muestra un mensaje de solicitud que solicita al usuario que realice una de las siguientes acciones:
    * Proporcione su consentimiento, si es necesario.
    * Controle la autenticación paso a paso, como la autenticación en dos fases.

1. Microsoft Teams solicita el token de aplicación del bot desde el punto de conexión de Azure AD para el usuario actual.

1. Azure AD envía el token de aplicación del bot a la aplicación de Microsoft Teams.

1. Microsoft Teams envía el token al bot como parte del objeto de valor devuelto por la actividad de invocación con **inicio de sesión/tokenExchange**.
  
1. El token analizado en la aplicación de bot proporciona la información necesaria, como la dirección de correo electrónico del usuario.
  
## <a name="develop-an-sso-teams-bot"></a>Desarrollar un bot SSO de Teams
  
Los pasos siguientes le guían para desarrollar el bot de inicio de sesión único de Teams:

1. [Registre su aplicación a través del portal de Azure AD](#register-your-app-through-the-azure-ad-portal).
1. [Actualice el manifiesto de aplicación de Teams para el bot](#update-your-teams-application-manifest-for-your-bot).
1. [Agregue el código para solicitar y recibir un token de bot](#add-the-code-to-request-and-receive-a-bot-token).

### <a name="register-your-app-through-the-azure-ad-portal"></a>Registre su aplicación a través del portal de Azure AD

Los pasos para registrar la aplicación a través del portal de Azure AD son similares al [flujo de inicio de sesión único de pestaña](../../../tabs/how-to/authentication/tab-sso-overview.md). Los pasos siguientes le guían para registrar la aplicación:

1. Registrar una nueva aplicación en el portal [Registros de aplicaciones de Microsoft Azure Active Directory (Azure AD)](https://go.microsoft.com/fwlink/?linkid=2083908).

1. Seleccione **Nuevo registro**. Aparece la página **Registrar una aplicación**.

    ![Nuevo registro](~/assets/images/authentication/SSO-bots-auth/app-registration.png)

1. En la página **Registrar una aplicación** haga lo siguiente:

   > [!NOTE]
   >
   > A los usuarios no se les pide consentimiento y se les conceden tokens de acceso de inmediato, si la aplicación de Azure AD está registrada en el mismo inquilino donde realizan una solicitud de autenticación en Teams. Sin embargo, los usuarios deben dar su consentimiento a los permisos, si la aplicación Azure AD está registrada en un inquilino diferente.

    * Escriba un **nombre** para la aplicación.
    * Seleccione **tipos de cuenta admitidos**, como inquilino único o multiinquilino.
    * Seleccione **Registrar**.

    ![Registrar una aplicación](~/assets/images/authentication/SSO-bots-auth/register-application.png)

1. Vaya a la página de información general.
1. Copie el valor del **identificador de aplicación (cliente)**.
1. En **Administrar**, seleccione **Exponer una API**

   > [!TIP]
   > Para actualizar el manifiesto de la aplicación más adelante, guarde el valor de **identificador de aplicación (cliente)**.

   > [!IMPORTANT]
   >
   > * Si va a compilar una aplicación con un bot y una pestaña, escriba el URI del identificador de aplicación como `api://botid-{YourBotId}`. Aquí *YourBotId* tiene el identificador de aplicación Azure AD.
   > * Si va a compilar una aplicación con un bot y una pestaña, escriba el URI del identificador de aplicación como `api://fully-qualified-domain-name.com/botid-{YourBotId}`.

1. Seleccione **Agregar un ámbito**.
1. En el panel que se abre, escriba `access_as_user` como **nombre del ámbito**.

   >[!NOTE]
   > El ámbito “access_as_user” que se usa para agregar una aplicación cliente es para “Administradores y usuarios”.
   >
   > Debe tener en cuenta las siguientes restricciones importantes:
   >
   > * Solo se admiten los permisos de Microsoft Graph API de nivel de usuario, como correo electrónico, perfil, offline_access y OpenId. Si necesita acceso a otros ámbitos de Microsoft Graph, como `User.Read` o `Mail.Read`, consulte [Extensión de la aplicación de pestaña con permisos y ámbito de Microsoft Graph](../../../tabs/how-to/authentication/tab-sso-graph-api.md).
   > * Es importante que el nombre de dominio de su aplicación sea el mismo que el nombre de dominio que ha registrado para su aplicación de Azure AD.
   > * Actualmente, no se admiten varios dominios por aplicación.
   > * Las aplicaciones que usan el dominio `azurewebsites.net` no se admiten porque es común y puede ser un riesgo para la seguridad.

1. En el cuadro **¿Quién puede dar su consentimiento?**, escriba **Administradores y usuarios**.
1. Escriba los detalles en los cuadros para configurar las solicitudes de consentimiento del administrador y del usuario con los valores adecuados para el ámbito de `access_as_user`.
    * **Nombre para mostrar de consentimiento del administrador:** Teams puede acceder al perfil del usuario.
    * **Descripción del consentimiento del administrador**: Teams puede llamar a las API web de la aplicación como el usuario actual.
    * **Título de consentimiento del usuario**: Teams puede acceder a su perfil y realizar solicitudes en su nombre.
    * **Descripción del consentimiento del usuario**: Teams puede llamar a las API de esta aplicación con los mismos derechos que tiene.

    ![administrador y usuarios](~/assets/images/authentication/SSO-bots-auth/add-a-scope.png)

1. Asegúrese de que el estado se establece en **Habilitado**.

    ![Estado](~/assets/images/authentication/SSO-bots-auth/enabled-state.png)

1. Seleccione **Agregar ámbito** para guardar los detalles. La parte de dominio del **nombre de ámbito** que se muestra debajo del campo de texto debe coincidir automáticamente con el URI de **identificador de aplicación** establecido en el paso anterior, con `/access_as_user` anexado al final `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`.

1. En la sección **Aplicaciones cliente autorizadas**, identifique las aplicaciones que quiere autorizar en la aplicación web de la aplicación.
1. Seleccione **Agregar una aplicación cliente**.

    ![aplicación cliente](~/assets/images/authentication/SSO-bots-auth/add-client-application.png)

1. Escriba cada uno de los siguientes Id. de cliente y seleccione el ámbito autorizado que creó en el paso anterior:
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` para la aplicación móvil o de escritorio de Teams.
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` para la aplicación web de Teams.

    ![id. de cliente](~/assets/images/authentication/SSO-bots-auth/add-client-id.png)

1. Vaya a **Autenticación**.
1. En la sección **Configuraciones de plataforma**, seleccione el botón **Agregar una plataforma**.

    ![plataforma](~/assets/images/authentication/SSO-bots-auth/platform-configuration.png)

1. Seleccione **Web**.

    ![Configuración de la plataforma](~/assets/images/authentication/SSO-bots-auth/configure-platform.png)

1. Escriba los **URI de redireccionamiento** de la aplicación.

   >[!NOTE]
   > Este URI debe ser un nombre de dominio completo. También le sigue la ruta de API a la que se envía una respuesta de autenticación. Si sigue cualquiera de los ejemplos de Teams, el URI es `https://token.botframework.com/.auth/web/redirect`. Para obtener más información, consulte [Flujo de código de autorización de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

    ![URI de redireccionamiento](~/assets/images/authentication/SSO-bots-auth/configure-web.png)

1. Los pasos siguientes le ayudarán a habilitar la concesión implícita:
    * Seleccione **Autenticación** en el panel izquierdo.
    * Active las casillas **Tokens de acceso** y **Tokens de identificador**.

    ![Flujo de concesión](~/assets/images/authentication/SSO-bots-auth/grant-flow.png)

    * Seleccione **Guardar** para guardar los cambios.

1. Agregue los **permisos de API** necesarios.
    * Seleccione **Permisos de API** en el panel izquierdo.
    * Seleccione **Agregar una plataforma** para agregar los permisos que la aplicación requiere a las API de bajada, por ejemplo, User.Read.

#### <a name="update-manifest-in-microsoft-azure-portal"></a>Actualización del manifiesto en el portal Microsoft Azure

Los pasos siguientes le guiarán para actualizar el manifiesto del bot en el portal de Azure:

1. Seleccione **Manifiesto** en el panel izquierdo.
1. Asegúrese de que el elemento de configuración está establecido en **“accessTokenAcceptedVersion”: 2**. Si no es así, cambie su valor a **2**.

    ![Actualizar manifiesto](~/assets/images/bots/update-manifest.png)

   >[!NOTE]
   > Si ya está probando el bot en Teams, debe cerrar sesión desde esta aplicación y cerrar la sesión de Teams. A continuación, vuelva a iniciar sesión para ver este cambio.

1. Seleccione **Guardar**.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Actualice el portal de Azure con la conexión de OAuth

Los pasos siguientes le guiarán para actualizar el portal de Azure con la conexión de OAuth:

1. En el portal de Azure, vaya a [**AzureBot**](https://ms.portal.azure.com/#create/Microsoft.AzureBot)
1. Vaya a **Configuración** en el panel izquierdo.
1. Seleccione **Agregar ajustes de conexión de OAuth**.

    ![Opción de configuración](~/assets/images/authentication/SSO-bots-auth/auth-setting2.png)

1. Los pasos siguientes le guiarán para completar el formulario **Nueva configuración de conexión**:

   >[!NOTE]
   > **La concesión implícita** puede ser necesaria en la aplicación Azure AD.

    * Escriba el **nombre** en la página **Nueva configuración de conexión**.

    >[!NOTE]
    > El **nombre** hace referencia a la configuración del código de bot service en el *paso 5* del [inicio de sesión único de Bot en tiempo de ejecución](#bot-sso-at-runtime).

    * En la lista desplegable **Proveedor de servicios**, seleccione **Azure Active Directory v2**.
    * Escriba las credenciales de cliente, como **Id. de cliente** y **Secreto de cliente** para la aplicación Azure AD.
    * Para la **dirección URL de token Exchange**, use el valor de ámbito definido en [Actualizar el manifiesto de aplicación de Teams para el bot](#update-your-teams-application-manifest-for-your-bot), por ejemplo, `api://botid-<your-app-id>/`. La dirección URL de token Exchange indica al SDK que esta aplicación Azure AD está configurada para el inicio de sesión único.
    * En **Id. de inquilino**, escriba *common*.
    * Agregue todos los **ámbitos configurados** al especificar permisos para las API de nivel inferior para la aplicación de Azure AD. Con el id. de cliente y el secreto de cliente proporcionados, el almacén de tokens intercambia el token por un token de grafo con permisos definidos.
    * Seleccione **Guardar**.
    * Seleccione **Aplicar**.

    ![Configuración de conexión](~/assets/images/authentication/Bot-connection-setting.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Actualización del manifiesto de aplicación de Teams para el bot

Si la aplicación contiene un bot independiente, use el código siguiente para agregar nuevas propiedades al manifiesto de aplicación Teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```

Si la aplicación contiene un bot y una pestaña, use el código siguiente para agregar nuevas propiedades al manifiesto de aplicación de Teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**WebApplicationInfo** es el elemento primario de los siguientes elementos:

* **id**: el Id. de cliente de la aplicación. Este es el identificador de aplicación que obtuvo como parte del registro de la aplicación con Azure AD. No comparta este identificador de aplicación con varias aplicaciones Teams. Cree una nueva aplicación de Azure AD para cada manifiesto de aplicación que use `webApplicationInfo`.
* **resource**: el dominio y el subdominio de la aplicación. Es el mismo URI, incluido el protocolo `api://` que registró al crear `scope` en [Registrar la aplicación a través del portal de Azure AD](#register-your-app-through-the-azure-ad-portal). No debe incluir la ruta de acceso `access_as_user` en el recurso. La parte de dominio de este identificador URI debe coincidir con el dominio, incluidos los subdominios, que se usan en las direcciones URL del manifiesto de la aplicación de Teams.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Agregar el código para solicitar y recibir un token de bot

#### <a name="request-a-bot-token"></a>Solicitud de un token de bot

La solicitud para obtener el token de acceso implica el envío de una solicitud de mensaje HTTP POST mediante el esquema de mensaje existente. Se incluye en los datos adjuntos de OAuthCard. El esquema de la clase OAuthCard se define en el [esquema de bots de Microsoft 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) y es similar a una tarjeta de inicio de sesión. Microsoft Teams trata la solicitud como una adquisición silenciosa de tokens si la propiedad `TokenExchangeResource` se rellena en la tarjeta. Para los canales de Microsoft Teams, solo se respeta la propiedad `Id`, que identifica de forma única una solicitud de token.

>[!NOTE]
> El Microsoft Bot Framework `OAuthPrompt` o `MultiProviderAuthDialog` es compatible con la autenticación de inicio de sesión único.

Si el usuario usa la aplicación por primera vez y se requiere el consentimiento del usuario, aparece el siguiente cuadro de diálogo para continuar con la experiencia de consentimiento:

![Cuadro de diálogo de consentimiento](~/assets/images/authentication/SSO-bots-auth/bot-consent-box.png)

Cuando el usuario selecciona **Continuar**, se producen los siguientes eventos:

* Si el bot define un botón de inicio de sesión, el flujo de inicio de sesión de los bots se desencadena de forma similar al flujo de inicio de sesión desde un botón de tarjeta OAuth en una secuencia de mensajes. El desarrollador debe decidir qué permisos requieren el consentimiento del usuario. Este enfoque se recomienda si necesita un token con permisos más allá de `openId`. Por ejemplo, si desea intercambiar el token por recursos de grafos.

* Si el bot no proporciona un botón de inicio de sesión en la tarjeta OAuth, se requiere el consentimiento del usuario para un conjunto mínimo de permisos. Este token es útil para la autenticación básica y para obtener la dirección de correo electrónico del usuario.

##### <a name="c-token-request-without-a-sign-in-button"></a>Solicitud de token de C# sin botón de inicio de sesión

```csharp
    var attachment = new Attachment
            {
                Content = new OAuthCard
                {
                    TokenExchangeResource = new TokenExchangeResource
                    {
                        Id = requestId
                    }
                },
                ContentType = OAuthCard.ContentType,
            };
            var activity = MessageFactory.Attachment(attachment);

            // NOTE: This activity needs to be sent in the 1:1 conversation between the bot and the user. 
            // If the bot supports group and channel scope, this code should be updated to send the request to the 1:1 chat. 

       await turnContext.SendActivityAsync(activity, cancellationToken);
```

#### <a name="receive-the-bot-token"></a>Recepción del token del bot

La respuesta con el token se envía a través de una actividad de invocación con el mismo esquema que otras actividades de invocación que los bots reciben hoy en día. La única diferencia es el nombre de invocación, el **inicio de sesión o tokenExchange** y el campo **valor**. El campo **valor** contiene el **identificador**, una cadena de la solicitud inicial para obtener el token y el campo **token**, un valor de cadena que incluye el token.

>[!NOTE]
> Puede recibir varias respuestas para una solicitud determinada si el usuario tiene varios puntos de conexión activos. Debe desduplicar las respuestas con el token.

##### <a name="c-code-to-handle-the-invoke-activity"></a>El código de C# para controlar la actividad de invocación

```csharp
    protected override async Task<InvokeResponse> OnInvokeActivityAsync
    (ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                try
                {
                    if (turnContext.Activity.Name == SignInConstants.TokenExchangeOperationName && turnContext.Activity.ChannelId == Channels.Msteams)
                    {
                        await OnTokenResponseEventAsync(turnContext, cancellationToken);
                        return new InvokeResponse() { Status = 200 };
                    }
                    else
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken);
                    }
                }
                catch (InvokeResponseException e)
                {
                    return e.CreateInvokeResponse();
                }
            }
```

Es `turnContext.activity.value` de tipo [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) y contiene el token que puede usar el bot. Debe almacenar los tokens por motivos de rendimiento y actualizarlos.

### <a name="token-exchange-failure"></a>Error de intercambio de tokens

Si se produce un error de intercambio de tokens, use el código siguiente:

```json
{ 
    "status": "<response code>", 
    "body": 
    { 
        "id":"<unique Id>", 
        "connectionName": "<connection Name on the bot (from the OAuth card)>", 
        "failureDetail": "<failure reason if status code is not 200, null otherwise>" 
    } 
}
```

Para comprender lo que hace el bot cuando el intercambio de tokens no desencadena una solicitud de consentimiento, consulte los pasos siguientes:

>[!NOTE]
> No es necesario realizar ninguna acción de usuario, ya que el bot realiza las acciones cuando se produce un error en el intercambio de tokens.

1. El cliente inicia una conversación con el bot desencadenando un escenario de OAuth.
2. El bot devuelve una tarjeta OAuth al cliente.
3. El cliente intercepta la tarjeta de OAuth antes de mostrarla al usuario y comprueba si contiene una propiedad `TokenExchangeResource`.
4. Si la propiedad existe, el cliente envía un `TokenExchangeInvokeRequest` al bot. El cliente debe tener un token intercambiable para el usuario, que debe ser un token de Azure AD v2 y cuya audiencia debe ser la misma que la propiedad `TokenExchangeResource.Uri`. El cliente envía una actividad de invocación al bot con el código siguiente:

    ```json
    {
        "type": "Invoke",
        "name": "signin/tokenExchange",
        "value": 
        {
            "id": "<any unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "token": "<exchangeable token>"
        }
    }
    ```

5. El bot procesa `TokenExchangeInvokeRequest` y devuelve un elemento `TokenExchangeInvokeResponse` al cliente. El cliente debe esperar hasta que reciba `TokenExchangeInvokeResponse`.

    ```json
    {
        "status": "<response code>",
        "body": 
        {
            "id":"<unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "failureDetail": "<failure reason if status code is not 200, null otherwise>"
        }
    }
    ```

6. Si `TokenExchangeInvokeResponse` tiene `status` de `200`, el cliente no muestra la tarjeta de OAuth. Vea la [imagen de flujo normal](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Para cualquier otro `status` o si `TokenExchangeInvokeResponse` no se recibe, el cliente muestra la tarjeta OAuth al usuario. Consulte la [imagen de flujo de reserva](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Si hay errores o dependencias no satisfechas, como el consentimiento del usuario, esta actividad garantiza que el flujo de SSO vuelva al flujo normal de OAuthCard.

### <a name="update-the-auth-sample"></a>Actualización del ejemplo de autenticación

Abra el [ejemplo de autenticación de Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) y complete los pasos siguientes para actualizarlo:

1. Actualice TeamsBot para controlar el desduplicación de la solicitud entrante mediante la inclusión del código siguiente:

    ```csharp
        protected override async Task OnSignInInvokeAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
        protected override async Task OnTokenResponseEventAsync(ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
    ```
  
2. Actualice `appsettings.json` para incluir `botId`, la contraseña y el nombre de conexión definidos en [Actualizar el Azure Portal con la conexión de OAuth](#update-the-azure-portal-with-the-oauth-connection).
3. Actualice el manifiesto y asegúrese de que `token.botframework.com` está en la lista de dominios válidos. Para obtener más información, consulte el [ejemplo de autenticación de Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).
4. Comprima el manifiesto con las imágenes de perfil e instálelo en Teams.

## <a name="code-sample"></a>Ejemplo de código

|**Ejemplo de nombre** | **Descripción** |**.NET** |**C#** |**Node.js** |
|----------------|-----------------|--------------|--------------|--------------|
|SDK del bot framework | En este código de ejemplo se muestra cómo empezar a usar la autenticación en un bot para Microsoft Teams. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-conversation-sso-quickstart/csharp_dotnetcore/BotConversationSsoQuickstart)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-conversation-sso-quickstart/js)|

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../../../sbs-bots-with-sso.yml) para crear un bot con autenticación sso.
