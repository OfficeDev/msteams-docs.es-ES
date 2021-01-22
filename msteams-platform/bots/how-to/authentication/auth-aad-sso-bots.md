---
title: Compatibilidad con inicio de sesión único para bots
description: Describe cómo obtener un token de usuario. Actualmente, un desarrollador de bots puede usar una tarjeta de inicio de sesión o el servicio de bot de Azure con la compatibilidad con la tarjeta OAuth.
keywords: token, token de usuario, compatibilidad con SSO para bots
ms.topic: conceptual
ms.openlocfilehash: 8537cf41cdd7218b9bf7618fccf0e1704ac6b815
ms.sourcegitcommit: 92fa912a51f295bb8a2dc1593a46ce103752dcdd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/21/2021
ms.locfileid: "49917592"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Compatibilidad con inicio de sesión único (SSO) para bots

La autenticación de inicio de sesión único en Azure Active Directory (AAD) minimiza el número de veces que los usuarios necesitan escribir sus credenciales de inicio de sesión actualizando silenciosamente el token de autenticación. Si los usuarios aceptan usar la aplicación, no necesitan volver a proporcionar su consentimiento en otro dispositivo y pueden iniciar sesión automáticamente. El flujo es similar al de la compatibilidad con SSO de la pestaña de [Microsoft Teams,](../../../tabs/how-to/authentication/auth-aad-sso.md)pero la diferencia está en el protocolo de cómo un bot solicita [tokens](#request-a-bot-token) y [recibe respuestas.](#receive-the-bot-token)

>[!NOTE]
> OAuth 2.0 es un estándar abierto para la autenticación y autorización que usa AAD y muchos otros proveedores de identidades. Un conocimiento básico de OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams.

## <a name="bot-sso-at-runtime"></a>SSO de bot en tiempo de ejecución

![Diagrama de SSO de bot en tiempo de ejecución](../../../assets/images/bots/bots-sso-diagram.png)

Complete los siguientes pasos para obtener tokens de aplicación de bot y autenticación:

1. El bot envía un mensaje con un OAuthCard que contiene la `tokenExchangeResource` propiedad. Indica a Teams que obtenga un token de autenticación para la aplicación bot. El usuario recibe mensajes en todos los extremos de usuario activos.

    > [!NOTE]
    >* Un usuario puede tener más de un punto de conexión activo a la vez.
    >* El token de bot se recibe de cada extremo de usuario activo.
    >* La aplicación debe instalarse en el ámbito personal para admitir SSO.

2. Si el usuario actual usa la aplicación de bot por primera vez, aparece un mensaje de solicitud solicitando al usuario que realice una de las siguientes acciones:
    * Proporcionar consentimiento, si es necesario.
    * Controlar la autenticación paso a paso, como la autenticación en dos fases.

3. Teams solicita el token de aplicación de bot del punto de conexión de AAD para el usuario actual.

4. AAD envía el token de aplicación de bot a la aplicación teams.

5. Teams envía el token al bot como parte del objeto de valor devuelto por la actividad de invocación con el nombre **inicio de sesión/tokenExchange**.
  
6. El token analizado en la aplicación bot proporciona la información necesaria, como la dirección de correo electrónico del usuario.
  
## <a name="develop-an-sso-teams-bot"></a>Desarrollar un bot de SSO teams
  
Complete los siguientes pasos para desarrollar un bot de SSO teams:

1. [Registre la aplicación a través del portal de AAD.](#register-your-app-through-the-aad-portal)
2. [Actualice el manifiesto de la aplicación de Teams para el bot.](#update-your-teams-application-manifest-for-your-bot)
3. [Agregue el código para solicitar y recibir un token de bot.](#add-the-code-to-request-and-receive-a-bot-token)

### <a name="register-your-app-through-the-aad-portal"></a>Registrar la aplicación a través del portal de AAD

Los pasos para registrar la aplicación a través del portal de AAD son similares al flujo [de SSO de la pestaña.](../../../tabs/how-to/authentication/auth-aad-sso.md) Siga estos pasos para registrar la aplicación:

1. Registrar una nueva aplicación en el portal de registros de aplicaciones [de Azure Active Directory.](https://go.microsoft.com/fwlink/?linkid=2083908)
2. Seleccione **Nuevo registro.** Aparece **la página Registrar una** aplicación.
3. En la **página Registrar una aplicación,** escriba los siguientes valores:
    1. Escribe un **nombre** para la aplicación.
    2. Elija los **tipos de cuenta admitidos,** seleccione un único inquilino o tipo de cuenta multiempresa.

        > [!NOTE]
        >
        > No se pide consentimiento a los usuarios y se les conceden tokens de acceso inmediatamente, si la aplicación AAD está registrada en el mismo inquilino donde están realizando una solicitud de autenticación en Teams. Sin embargo, los usuarios deben dar su consentimiento a los permisos, si la aplicación AAD está registrada en un inquilino diferente.

    3. Elija **Registrar**.
4. En la página de información general, copie y guarde el identificador **de aplicación (cliente).** Lo necesitará más adelante al actualizar el manifiesto de la aplicación de Teams.
5. En **Administrar**, seleccione **Exponer una API** 

   > [!IMPORTANT]
    > * Si va a crear un bot independiente, escriba el URI de id. de aplicación como `api://botid-{YourBotId}` . Aquí **YourBotId** es el id. de aplicación de AAD.
    > * Si está creando una aplicación con un bot y una pestaña, escriba el URI de id. de aplicación como `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

5. Seleccione los permisos que la aplicación necesita para el punto de conexión de AAD y, opcionalmente, para Microsoft Graph.
6. [Conceda permisos para](/azure/active-directory/develop/v2-permissions-and-consent) aplicaciones móviles, web y de escritorio de Teams.
7. Seleccione **Agregar un ámbito.**
8. En el panel que se abre, agregue una aplicación cliente; para ello, escriba `access_as_user` el nombre **del ámbito.**

    >[!NOTE]
    > El ámbito "access_as_user" usado para agregar una aplicación cliente es para "Administradores y usuarios".
    >
    > Debe conocer las siguientes restricciones importantes:
    >
    > * Solo se admiten permisos de la API de Microsoft Graph de nivel de usuario, como correo electrónico, perfil, offline_access y OpenId. Si necesita obtener acceso a otros ámbitos de Microsoft Graph, como `User.Read` o , vea la solución alternativa `Mail.Read` [recomendada.](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes)
    > * El nombre de dominio de la aplicación debe ser el mismo que el nombre de dominio registrado para la aplicación de AAD.
    > * Actualmente, no se admiten varios dominios por aplicación.
    > * Las aplicaciones que usan `azurewebsites.net` el dominio no son compatibles porque es común y puede ser un riesgo para la seguridad.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Actualizar Azure Portal con la conexión de OAuth

Complete los siguientes pasos para actualizar Azure Portal con la conexión de OAuth:

1. En Azure Portal, vaya a **Registro de canales de bot.**

2. Vaya a **Permisos de API.** Seleccione **Agregar permisos delegados** de Microsoft Graph y, a continuación, agregue los siguientes  >    >  permisos de la API de Microsoft Graph:
    * User.Read (habilitado de forma predeterminada)
    * email
    * offline_access
    * OpenId
    * perfil

3. Seleccione **Configuración en** el panel izquierdo y elija Agregar configuración **en** la sección Configuración de conexión **de OAuth.**

    ![Vista SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

4. Realice los pasos siguientes para completar el formulario **Nueva configuración de** conexión:

    >[!NOTE]
    > **La concesión** implícita puede ser necesaria en la aplicación AAD.

    1. Escriba un **nombre en** la página Nueva **configuración de** conexión. Este es el nombre al que se hace referencia dentro de la configuración del código de servicio de bot en el paso *5* de [BOT SSO en tiempo de ejecución.](#bot-sso-at-runtime)
    2. En la **lista desplegable Proveedor** de servicios, seleccione Azure Active Directory **v2**.
    3. Escriba las credenciales de cliente, como id. **de** cliente y secreto **de** cliente para la aplicación de AAD.
    4. Para la **dirección URL de Exchange de token,** use el valor de ámbito definido en Actualizar el manifiesto de la aplicación de Teams para el [bot.](#update-your-teams-application-manifest-for-your-bot) La dirección URL de Token Exchange indica al SDK que esta aplicación de AAD está configurada para SSO.
    5. En el **cuadro Id. de** inquilino, *escriba common*.
    6. Agregue todos los **ámbitos configurados** al especificar permisos para las API de bajada de la aplicación de AAD. Con el identificador de cliente y el secreto de cliente proporcionados, el almacén de tokens intercambia el token por un token de gráfico con permisos definidos.
    7. Seleccione **Guardar**.

    ![Vista de configuración DesOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Actualizar el manifiesto de la aplicación de Teams para el bot

Si la aplicación contiene un bot independiente, use el siguiente código para agregar nuevas propiedades al manifiesto de la aplicación de Teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
Si la aplicación contiene un bot y una pestaña, use el siguiente código para agregar nuevas propiedades al manifiesto de la aplicación teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** es el elemento principal de los siguientes elementos:

* **id:** id. de cliente de la aplicación. Este es el identificador de aplicación que obtuvo como parte del registro de la aplicación con AAD.
* **recurso:** el dominio y el subdominio de la aplicación. Este es el mismo URI, incluido el protocolo que registró al crear la aplicación en Registrar la aplicación a través `api://` `scope` del portal de [AAD.](#register-your-app-through-the-aad-portal) No debe incluir la ruta `access_as_user` de acceso en el recurso. La parte de dominio de este URI debe coincidir con el dominio y los subdominios usados en las direcciones URL del manifiesto de la aplicación de Teams.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Agregar el código para solicitar y recibir un token de bot

#### <a name="request-a-bot-token"></a>Solicitar un token de bot

La solicitud para obtener el token es una solicitud de mensaje POST normal mediante el esquema de mensaje existente. Se incluye en los datos adjuntos de un OAuthCard. El esquema de la clase OAuthCard se define en el esquema de bot de [Microsoft 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) y es similar a una tarjeta de inicio de sesión. Teams trata esta solicitud como una adquisición de token silenciosa si `TokenExchangeResource` la propiedad se rellena en la tarjeta. Para el canal de Teams, solo se respeta la propiedad, que identifica de forma exclusiva `Id` una solicitud de token.

>[!NOTE]
> Microsoft Bot Framework `OAuthPrompt` o el es compatible con la `MultiProviderAuthDialog` autenticación SSO.

Si el usuario usa la aplicación por primera vez y se requiere el consentimiento del usuario, aparece el siguiente cuadro de diálogo para continuar con la experiencia de consentimiento:

![Cuadro de diálogo Consentimiento](../../../assets/images/bots/bots-consent-dialogbox.png)

Cuando el usuario selecciona **Continuar**, se producen los siguientes eventos:

* Si el bot define un botón de inicio de sesión, el flujo de inicio de sesión de los bots se desencadena de forma similar al flujo de inicio de sesión desde un botón de tarjeta OAuth en una secuencia de mensajes. El desarrollador debe decidir qué permisos requieren el consentimiento del usuario. Este enfoque se recomienda si necesita un token con permisos `openId` posteriores. Por ejemplo, si desea intercambiar el token por recursos de gráfico.

* Si el bot no proporciona un botón de inicio de sesión en la tarjeta OAuth, se requiere el consentimiento del usuario para un conjunto mínimo de permisos. Este token es útil para la autenticación básica y para obtener la dirección de correo electrónico del usuario.

##### <a name="c-token-request-without-a-sign-in-button"></a>Solicitud de token de C# sin un botón de inicio de sesión

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

#### <a name="receive-the-bot-token"></a>Recibir el token de bot

La respuesta con el token se envía a través de una actividad de invocación con el mismo esquema que otras actividades de invocación que los bots reciben hoy. La única diferencia es el nombre de invocación, **el inicio de sesión/tokenExchange** y el **campo de** valor. El **campo** de valor contiene el **identificador,** una cadena de la solicitud inicial para obtener el token y el **campo de token,** un valor de cadena que incluye el token.

>[!NOTE]
> Es posible que reciba varias respuestas para una solicitud determinada si el usuario tiene varios puntos de conexión activos. Debe desduplicar las respuestas con el token.

##### <a name="c-code-to-handle-the-invoke-activity"></a>Código C# para controlar la actividad de invocación

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

El `turnContext.activity.value` es de tipo [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) y contiene el token que puede usar el bot. Debe almacenar los tokens por motivos de rendimiento y actualizarlos.

### <a name="update-the-auth-sample"></a>Actualizar el ejemplo de autenticación

Abra [el ejemplo de autenticación de Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) y, a continuación, siga estos pasos para actualizarlo:

1. Actualice el TeamsBot para controlar el desduprimido de la solicitud entrante incluyendo el código siguiente:

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
  
2. Actualizar para incluir el , contraseña y el nombre de conexión definidos `appsettings.json` en Actualizar Azure Portal con la conexión de `botId` [OAuth](#update-the-azure-portal-with-the-oauth-connection).
3. Actualice el manifiesto y asegúrese de que `token.botframework.com` está en la lista de dominios válidos. Para obtener más información, vea [el ejemplo de autenticación de Teams.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)
4. Zip the manifest with the profile images and install it in Teams.

#### <a name="additional-code-samples"></a>Ejemplos de código adicionales

* [Ejemplo de C# con el SDK de Bot Framework](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore).

* [Ejemplo de C# con el SDK de Bot Framework para desduplicar la solicitud de token.](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682)

* [Ejemplo de C# sin usar el almacén](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)de tokens del SDK de Bot Framework .
