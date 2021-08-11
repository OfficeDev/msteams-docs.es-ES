---
title: Compatibilidad con inicio de sesión único para bots
description: Describe cómo obtener un token de usuario. Actualmente, un desarrollador de bots puede usar una tarjeta de inicio de sesión o el servicio de bots de Azure con la compatibilidad con la tarjeta OAuth.
keywords: token, token de usuario, compatibilidad con SSO para bots
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 30a92de9f7d5ad9615ef2f86244b8607a47cea356030ebfb93ed3c1ffcb127a8
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57709623"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Compatibilidad con inicio de sesión único (SSO) para bots

La autenticación de inicio de sesión único en Azure Active Directory (AAD) minimiza el número de veces que los usuarios necesitan escribir sus credenciales de inicio de sesión actualizando silenciosamente el token de autenticación. Si los usuarios aceptan usar la aplicación, no necesitan volver a proporcionar su consentimiento en otro dispositivo y pueden iniciar sesión automáticamente. El flujo es similar al de la compatibilidad de SSO Microsoft Teams [pestaña, sin](../../../tabs/how-to/authentication/auth-aad-sso.md)embargo, la diferencia está en el protocolo de cómo un bot solicita [tokens](#request-a-bot-token) y [recibe respuestas.](#receive-the-bot-token)

>[!NOTE]
> OAuth 2.0 es un estándar abierto para la autenticación y autorización que usa AAD y muchos otros proveedores de identidades. Un conocimiento básico de OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams.

## <a name="bot-sso-at-runtime"></a>SSO de bot en tiempo de ejecución

![Sso de bot en el diagrama de tiempo de ejecución](../../../assets/images/bots/bots-sso-diagram.png)

Siga estos pasos para obtener tokens de aplicación de bot y autenticación:

1. El bot envía un mensaje con una OAuthCard que contiene la propiedad `tokenExchangeResource`. Indica a Teams obtener un token de autenticación para la aplicación bot. El usuario recibe mensajes en todos los puntos de conexión de usuario activos.

    > [!NOTE]
    >* Un usuario puede tener más de un punto de conexión activo a la vez.
    >* El token del bot se recibe de cada punto de conexión de usuario activo.
    >* La aplicación debe instalarse en el ámbito personal para la compatibilidad con SSO.

1. Si el usuario actual usa la aplicación bot por primera vez, aparece un mensaje de solicitud solicitando al usuario que realice una de las siguientes acciones:
    * Proporcionar consentimiento, si es necesario.
    * Controle la autenticación paso a paso, como la autenticación en dos fases.

1. Teams solicita el token de aplicación bot desde el punto de conexión de AAD para el usuario actual.

1. AAD envía el token de aplicación bot a la Teams aplicación.

1. Teams envía el token al bot como parte del objeto de valor devuelto por la actividad de invocación con el nombre **sign-in/tokenExchange**.
  
1. El token analizado en la aplicación de bot proporciona la información necesaria, como la dirección de correo electrónico del usuario.
  
## <a name="develop-an-sso-teams-bot"></a>Desarrollar un bot Teams SSO
  
Complete los siguientes pasos para desarrollar un bot Teams SSO:

1. [Registrar la aplicación a través del portal de AAD](#register-your-app-through-the-aad-portal).
1. [Actualice el manifiesto Teams aplicación para el bot](#update-your-teams-application-manifest-for-your-bot).
1. [Agregue el código para solicitar y recibir un token de bot](#add-the-code-to-request-and-receive-a-bot-token).

### <a name="register-your-app-through-the-aad-portal"></a>Registrar la aplicación a través del portal de AAD

Los pasos para registrar la aplicación a través del portal de AAD son similares al [flujo de SSO de tabulación.](../../../tabs/how-to/authentication/auth-aad-sso.md) Siga estos pasos para registrar la aplicación:

1. Registrar una nueva aplicación en el [portal Azure Active Directory – Registros de aplicaciones.](https://go.microsoft.com/fwlink/?linkid=2083908)
2. Seleccione **Nuevo registro**. Aparece **la página** Registrar una aplicación.
3. En la **página Registrar una aplicación,** escriba los siguientes valores:
    1. Escribe un **nombre** para la aplicación.
    2. Elija los **tipos de cuenta admitidos,** seleccione un único inquilino o tipo de cuenta multiempresa.

        > [!NOTE]
        >
        > A los usuarios no se les pide su consentimiento y se les conceden tokens de acceso inmediatamente, si la aplicación AAD está registrada en el mismo espacio empresarial donde están realizando una solicitud de autenticación en Teams. Sin embargo, los usuarios deben dar su consentimiento a los permisos, si la aplicación de AAD está registrada en un inquilino diferente.

    3. Elija **Registrar**.
4. En la página de información general, copie y guarde el **identificador de aplicación (cliente).** Lo necesitará más adelante al actualizar el manifiesto Teams aplicación.
5. En **Administrar**, seleccione **Exponer una API** 

   > [!IMPORTANT]
    > * Si va a crear un bot independiente, escriba el URI de id. de aplicación como `api://botid-{YourBotId}` . Aquí **YourBotId** es el identificador de aplicación de AAD.
    > * Si estás creando una aplicación con un bot y una pestaña, escribe el URI de id. de aplicación como `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

5. Seleccione los permisos que la aplicación necesita para el punto de conexión de AAD y, opcionalmente, para Microsoft Graph.
6. [Conceda permisos para](/azure/active-directory/develop/v2-permissions-and-consent) Teams escritorio, web y aplicaciones móviles.
7. Seleccione **Agregar un ámbito**.
8. En el panel que se abre, agregue una aplicación cliente especificando `access_as_user` como nombre de **ámbito**.

    >[!NOTE]
    > El ámbito "access_as_user" usado para agregar una aplicación cliente es para "Administradores y usuarios".
    >
    > Debe tener en cuenta las siguientes restricciones importantes:
    >
    > * Solo se admiten permisos Graph API de Microsoft de nivel de usuario, como correo electrónico, perfil, offline_access y OpenId. Si necesita acceso a otros ámbitos de microsoft Graph, como o , vea Obtener un token de acceso `User.Read` `Mail.Read` con Graph [permisos](../../../tabs/how-to/authentication/auth-aad-sso.md#get-an-access-token-with-graph-permissions).
    > * El nombre de dominio de la aplicación debe ser el mismo que el nombre de dominio que se ha registrado para la aplicación de AAD.
    > * Actualmente, no se admiten varios dominios por aplicación.
    > * Las aplicaciones que usan `azurewebsites.net` el dominio no se admiten porque es común y pueden ser un riesgo de seguridad.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Actualizar Azure Portal con la conexión de OAuth

Siga estos pasos para actualizar Azure Portal con la conexión de OAuth:

1. En Azure Portal, vaya a **Registros de aplicaciones**.

2. Vaya a **Permisos de API**. Seleccione **Agregar un permiso** Microsoft  >  **Graph**  >  **permisos delegados** y, a continuación, agregue los siguientes permisos de la API Graph Microsoft:
    * User.Read (habilitado de forma predeterminada)
    * correo electrónico
    * offline_access
    * OpenId
    * perfil

3. En Azure Portal, vaya a **Bot Channels Registration**.

4. Seleccione **Configuración** en el panel izquierdo y elija **Agregar configuración** en la sección Configuración Configuración **OAuth.**

    ![Vista SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. Realice los pasos siguientes para completar el **formulario Nueva configuración de** conexión:

    >[!NOTE]
    > **La concesión** implícita puede ser necesaria en la aplicación de AAD.

    1. Escriba un **nombre en** la página Nueva **configuración de** conexión. Este es el nombre al que se hace referencia dentro de la configuración del código de servicio del bot en el paso *5* de [BOT SSO en tiempo de ejecución.](#bot-sso-at-runtime)
    2. En la **lista desplegable Proveedor** de servicios, seleccione Azure Active Directory **v2**.
    3. Escriba las credenciales de cliente, como **Id.** de cliente y **Secreto de cliente** para la aplicación de AAD.
    4. Para la **dirección URL Exchange** token, use el valor de ámbito definido en Actualizar el manifiesto Teams aplicación para el [bot](#update-your-teams-application-manifest-for-your-bot). La dirección URL Exchange token indica al SDK que esta aplicación de AAD está configurada para SSO.
    5. En el **cuadro Id. de** inquilino, escriba *common*.
    6. Agregue todos los **ámbitos configurados** al especificar permisos para las API de nivel inferior para la aplicación de AAD. Con el identificador de cliente y el secreto de cliente proporcionados, el almacén de tokens intercambia el token para un token de gráfico con permisos definidos.
    7. Seleccione **Guardar**.

    ![Vista de configuración de VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Actualizar el manifiesto Teams aplicación para el bot

Si la aplicación contiene un bot independiente, use el siguiente código para agregar nuevas propiedades al manifiesto Teams aplicación:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
Si la aplicación contiene un bot y una pestaña, use el siguiente código para agregar nuevas propiedades al manifiesto Teams aplicación:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** es el elemento primario de los siguientes elementos:

* **id:** el identificador de cliente de la aplicación. Este es el identificador de aplicación que obtuvo como parte del registro de la aplicación con AAD.
* **resource:** el dominio y el subdominio de la aplicación. Este es el mismo URI, incluido el protocolo que registró al crear la aplicación `api://` en Register your app through the `scope` [AAD portal](#register-your-app-through-the-aad-portal). No debe incluir la ruta `access_as_user` de acceso en el recurso. La parte de dominio de este URI debe coincidir con el dominio y los subdominios usados en las direcciones URL del manifiesto Teams aplicación.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Agregar el código para solicitar y recibir un token de bot

#### <a name="request-a-bot-token"></a>Solicitar un token de bot

La solicitud para obtener el token es una solicitud de mensaje POST normal mediante el esquema de mensaje existente. Se incluye en los datos adjuntos de un OAuthCard. El esquema de la clase OAuthCard se define en [microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) y es similar a una tarjeta de inicio de sesión. Teams trata esta solicitud como una adquisición de tokens silenciosos si la `TokenExchangeResource` propiedad se rellena en la tarjeta. Para el Teams, solo se respeta la propiedad, que identifica de forma única una solicitud de `Id` token.

>[!NOTE]
> El Microsoft Bot Framework `OAuthPrompt` o el es compatible con la `MultiProviderAuthDialog` autenticación de SSO.

Si el usuario usa la aplicación por primera vez y se requiere el consentimiento del usuario, el siguiente cuadro de diálogo parece continuar con la experiencia de consentimiento:

![Cuadro de diálogo Consentimiento](../../../assets/images/bots/bots-consent-dialogbox.png)

Cuando el usuario selecciona **Continuar**, se producen los siguientes eventos:

* Si el bot define un botón de inicio de sesión, el flujo de inicio de sesión para bots se desencadena de forma similar al flujo de inicio de sesión de un botón de tarjeta OAuth en una secuencia de mensajes. El desarrollador debe decidir qué permisos requieren el consentimiento del usuario. Este enfoque se recomienda si necesita un token con permisos más allá de `openId` . Por ejemplo, si desea intercambiar el token por recursos de gráfico.

* Si el bot no proporciona un botón de inicio de sesión en la tarjeta OAuth, se requiere el consentimiento del usuario para un conjunto mínimo de permisos. Este token es útil para la autenticación básica y para obtener la dirección de correo electrónico del usuario.

##### <a name="c-token-request-without-a-sign-in-button"></a>C# de token sin un botón de inicio de sesión

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

#### <a name="receive-the-bot-token"></a>Recibir el token del bot

La respuesta con el token se envía a través de una actividad de invocación con el mismo esquema que otras actividades de invocación que los bots reciben hoy. La única diferencia es el nombre de invocación, **el inicio de sesión/tokenExchange** y el **campo de** valor. El **campo** de valor contiene **el identificador**, una cadena de la solicitud inicial para obtener el token y el campo de **token,** un valor de cadena que incluye el token.

>[!NOTE]
> Es posible que reciba varias respuestas para una solicitud determinada si el usuario tiene varios extremos activos. Debe deduplicar las respuestas con el token.

##### <a name="c-code-to-handle-the-invoke-activity"></a>C# código para controlar la actividad de invocación

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

El `turnContext.activity.value` es de tipo [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) y contiene el token que puede usar el bot. Debes almacenar los tokens por motivos de rendimiento y actualizarlos.

### <a name="token-exchange-failure"></a>Error de intercambio de tokens

En caso de error de intercambio de tokens, use el código siguiente:

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

Para comprender lo que hace el bot cuando el intercambio de tokens no desencadena un mensaje de consentimiento, consulte los pasos siguientes:

>[!NOTE]
> No es necesario realizar ninguna acción de usuario a medida que el bot realiza las acciones cuando se produce un error en el intercambio de tokens.

1. El cliente inicia una conversación con el bot desencadenando un escenario de OAuth.
2. El bot devuelve una tarjeta OAuth al cliente.
3. El cliente intercepta la tarjeta OAuth antes de mostrarla al usuario y comprueba si contiene una `TokenExchangeResource` propiedad.
4. Si la propiedad existe, el cliente envía una al `TokenExchangeInvokeRequest` bot. El cliente debe tener un token intercambiable para el usuario, que debe ser un token de Azure AD v2 y cuya audiencia debe ser la misma que la `TokenExchangeResource.Uri` propiedad. El cliente envía una actividad de invocación al bot con el código siguiente:

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

5. El bot procesa el `TokenExchangeInvokeRequest` y devuelve `TokenExchangeInvokeResponse` una devolución al cliente. El cliente debe esperar hasta que reciba el `TokenExchangeInvokeResponse` archivo .

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

6. Si el `TokenExchangeInvokeResponse` tiene un de , el cliente no muestra la tarjeta `status` `200` OAuth. Vea la [imagen de flujo normal](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Para cualquier otro `status` o si no se `TokenExchangeInvokeResponse` recibe, el cliente muestra la tarjeta OAuth al usuario. Vea la [imagen de flujo de reserva](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Esto garantiza que el flujo de SSO vuelva al flujo OAuthCard normal en caso de errores o dependencias no satisfechas como el consentimiento del usuario.


### <a name="update-the-auth-sample"></a>Actualizar el ejemplo de autenticación

Abra [Teams ejemplo de autenticación](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) y, a continuación, siga estos pasos para actualizarlo:

1. Actualice el TeamsBot para controlar la deduping de la solicitud entrante mediante el código siguiente:

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
  
2. Actualice para incluir la , contraseña y el nombre de conexión `appsettings.json` `botId` definidos en [Actualizar Azure Portal con la conexión de OAuth](#update-the-azure-portal-with-the-oauth-connection).
3. Actualice el manifiesto y asegúrese de `token.botframework.com` que está en la lista de dominios válidos. Para obtener más información, [vea Teams ejemplo de autenticación](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).
4. Zip the manifest with the profile images and install it in Teams.

## <a name="code-sample"></a>Ejemplo de código
|**Ejemplo de nombre** | **Descripción** |**.NET** | 
|----------------|-----------------|--------------|
|SDK de marco de bots | Ejemplo para usar el SDK del marco de bots. |[Ver](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
