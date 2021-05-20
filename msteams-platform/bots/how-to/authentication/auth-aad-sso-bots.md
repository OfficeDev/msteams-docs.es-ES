---
title: Compatibilidad con inicio de sesión único para bots
description: Describe cómo obtener un token de usuario. Actualmente, un desarrollador de bots puede usar una tarjeta de inicio de sesión o el servicio de bots de Azure con el soporte técnico de la tarjeta OAuth.
keywords: token, token de usuario, compatibilidad con SSO para bots
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: a43c2a46561149ff97d039a3ba8fe9f4472e2073
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566097"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Soporte de inicio de sesión único (SSO) para bots

La autenticación de inicio de sesión único en Azure Active Directory (AAD) minimiza el número de veces que los usuarios necesitan escribir sus credenciales de inicio de sesión actualizando silenciosamente el token de autenticación. Si los usuarios aceptan usar la aplicación, no deben volver a dar su consentimiento en otro dispositivo y pueden iniciar sesión automáticamente. El flujo es similar al de Microsoft Teams compatibilidad con SSO de [tabulación,](../../../tabs/how-to/authentication/auth-aad-sso.md)sin embargo, la diferencia está en el protocolo de cómo un bot [solicita tokens](#request-a-bot-token) y [recibe respuestas.](#receive-the-bot-token)

>[!NOTE]
> OAuth 2.0 es un estándar abierto para la autenticación y autorización utilizado por AAD y muchos otros proveedores de identidades. Una comprensión básica de OAuth 2.0 es un requisito previo para trabajar con autenticación en Teams.

## <a name="bot-sso-at-runtime"></a>Bot SSO en tiempo de ejecución

![Bot SSO en el diagrama de tiempo de ejecución](../../../assets/images/bots/bots-sso-diagram.png)

Complete los pasos siguientes para obtener tokens de autenticación y aplicación de bots:

1. El bot envía un mensaje con un OAuthCard que contiene la `tokenExchangeResource` propiedad. Indica a Teams que obtenga un token de autenticación para la aplicación bot. El usuario recibe mensajes en todos los puntos de conexión de usuario activos.

    > [!NOTE]
    >* Un usuario puede tener más de un punto de conexión activo a la vez.
    >* El token de bot se recibe de todos los puntos de conexión de usuario activos.
    >* La aplicación debe instalarse en el ámbito personal para la compatibilidad con SSO.

1. Si el usuario actual está utilizando la aplicación bot por primera vez, aparece un mensaje de solicitud solicitando al usuario que realice una de las siguientes acciones:
    * Proporcionar consentimiento, si es necesario.
    * Controle la autenticación de paso a paso, como la autenticación de dos factores.

1. Teams solicita el token de aplicación de bot desde el punto de conexión de AAD para el usuario actual.

1. AAD envía el token de aplicación de bot a la aplicación Teams.

1. Teams envía el token al bot como parte del objeto value devuelto por la actividad invoke con el nombre **sign-in/tokenExchange**.
  
1. El token analizado en la aplicación bot proporciona la información necesaria, como la dirección de correo electrónico del usuario.
  
## <a name="develop-an-sso-teams-bot"></a>Desarrollar un bot de Teams de SSO
  
Complete los siguientes pasos para desarrollar un bot de Teams de SSO:

1. [Registre la aplicación a través del portal de AAD.](#register-your-app-through-the-aad-portal)
1. [Actualice el manifiesto de aplicación Teams para el bot.](#update-your-teams-application-manifest-for-your-bot)
1. [Agregue el código para solicitar y reciba un token de bot.](#add-the-code-to-request-and-receive-a-bot-token)

### <a name="register-your-app-through-the-aad-portal"></a>Registre la aplicación a través del portal de AAD

Los pasos para registrar la aplicación a través del portal de AAD son similares a la [pestaña Flujo de SSO.](../../../tabs/how-to/authentication/auth-aad-sso.md) Complete los siguientes pasos para registrar la aplicación:

1. Registre una nueva aplicación en el portal [Azure Active Directory – Registros de aplicaciones.](https://go.microsoft.com/fwlink/?linkid=2083908)
2. Seleccione **Nuevo registro**. Aparece la página **Registrar una aplicación.**
3. En la página **Registrar una aplicación,** escriba los siguientes valores:
    1. Escriba un **nombre** para la aplicación.
    2. Elija los **tipos de cuenta admitidos,** seleccione un único inquilino o un tipo de cuenta multitenente.

        > [!NOTE]
        >
        > A los usuarios no se les pide el consentimiento y se les conceden tokens de acceso de inmediato, si la aplicación AAD está registrada en el mismo inquilino donde están realizando una solicitud de autenticación en Teams. Sin embargo, los usuarios deben dar su consentimiento a los permisos, si la aplicación AAD está registrada en un inquilino diferente.

    3. Elija **Registrar**.
4. En la página de resumen, copie y guarde el **ID de aplicación (cliente).** Más adelante lo necesita al actualizar el manifiesto de la aplicación Teams.
5. En **Administrar**, seleccione **Exponer una API** 

   > [!IMPORTANT]
    > * Si está creando un bot independiente, escriba el URI de ID de aplicación como `api://botid-{YourBotId}` . Aquí **YourBotId** es su ID de aplicación AAD.
    > * Si está creando una aplicación con un bot y una pestaña, escriba el URI de IDENTIFICADOR de aplicación como `api://fully-qualified-domain-name.com/botid-{YourBotId}` .

5. Seleccione los permisos que necesita la aplicación para el punto de conexión de AAD y, opcionalmente, para Microsoft Graph.
6. [Conceda permisos](/azure/active-directory/develop/v2-permissions-and-consent) para aplicaciones de escritorio, web y móviles Teams.
7. Seleccione **Agregar un ámbito**.
8. En el panel que se abre, agregue una aplicación cliente introduciendo `access_as_user` como **nombre de ámbito.**

    >[!NOTE]
    > El ámbito "access_as_user" utilizado para agregar una aplicación cliente es para "Administradores y usuarios".
    >
    > Debe tener en cuenta las siguientes restricciones importantes:
    >
    > * Solo se admiten permisos de API de Microsoft Graph de nivel de usuario, como correo electrónico, perfil, offline_access y OpenId. Si necesita acceso a otros ámbitos de Microsoft Graph, por `User.Read` ejemplo, vea `Mail.Read` la solución [alternativa recomendada.](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes)
    > * El nombre de dominio de la aplicación debe ser el mismo que el nombre de dominio que ha registrado para la aplicación AAD.
    > * Actualmente no se admiten varios dominios por aplicación.
    > * Las aplicaciones que usan el `azurewebsites.net` dominio no se admiten porque es común y pueden ser un riesgo de seguridad.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Actualice Azure Portal con la conexión OAuth

Complete los pasos siguientes para actualizar Azure Portal con la conexión OAuth:

1. En Azure Portal, vaya a **Registros de aplicaciones.**

2. Vaya a **Permisos de API**. Seleccione **Agregar un permiso** Microsoft  >  **Graph** Permisos  >  **delegados** y, a continuación, agregue los siguientes permisos desde microsoft Graph API:
    * User.Read (habilitado de forma predeterminada)
    * email
    * offline_access
    * OpenId
    * perfil

3. En Azure Portal, vaya a **Registro de canales de bot.**

4. Seleccione **Configuración** en el panel izquierdo y elija **Agregar configuración** en la sección Configuración de conexión de **OAuth.**

    ![Vista SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. Realice los pasos siguientes para completar el formulario **Nueva configuración de conexión:**

    >[!NOTE]
    > **Puede** ser necesaria una concesión implícita en la aplicación AAD.

    1. Escriba un **nombre** en la página **Nueva configuración de conexión.** Este es el nombre al que se hace referencia dentro de la configuración del código de servicio de bot en el *paso 5* de [Bot SSO en tiempo de ejecución.](#bot-sso-at-runtime)
    2. En el menú desplegable **Proveedor de** servicios, seleccione **Azure Active Directory v2**.
    3. Escriba las credenciales de cliente, como **identificador de cliente** y secreto de **cliente** para la aplicación AAD.
    4. Para la **dirección URL de Exchange token,** utilice el valor de ámbito definido en Actualizar el manifiesto de aplicación Teams para el [bot](#update-your-teams-application-manifest-for-your-bot). La dirección URL de token Exchange indica al SDK que esta aplicación AAD está configurada para SSO.
    5. En el cuadro **Identificador de inquilino,** especifique *common*.
    6. Agregue todos los **ámbitos configurados** al especificar permisos a las API de nivel inferior para la aplicación AAD. Con el identificador de cliente y el secreto de cliente proporcionados, el almacén de tokens intercambia el token por un token de gráfico con permisos definidos.
    7. Seleccione **Guardar**.

    ![Vista de configuración de VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Actualice el manifiesto de la aplicación Teams para el bot

Si la aplicación contiene un bot independiente, utilice el código siguiente para agregar nuevas propiedades al manifiesto de aplicación Teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
Si la aplicación contiene un bot y una pestaña, utilice el código siguiente para agregar nuevas propiedades al manifiesto de aplicación Teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** es el elemento primario de los siguientes elementos:

* **id:** el ID de cliente de la aplicación. Este es el IDENTIFICADOR de aplicación que obtuvo como parte del registro de la aplicación con AAD.
* **recurso:** el dominio y el subdominio de la aplicación. Este es el mismo URI, incluido el `api://` protocolo que registró al crear la aplicación en Registrar la aplicación a través del portal de `scope` [AAD.](#register-your-app-through-the-aad-portal) No debe incluir la `access_as_user` ruta de acceso en el recurso. La parte de dominio de este URI debe coincidir con el dominio y los subdominios utilizados en las direcciones URL del manifiesto de aplicación Teams.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Agregue el código para solicitar y recibir un token de bot

#### <a name="request-a-bot-token"></a>Solicitar un token de bot

La solicitud para obtener el token es una solicitud de mensaje POST normal mediante el esquema de mensaje existente. Se incluye en los archivos adjuntos de una OAuthCard. El esquema de la clase OAuthCard se define en [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) y es similar a una tarjeta de inicio de sesión. Teams trata esta solicitud como una adquisición silenciosa de tokens si la `TokenExchangeResource` propiedad se rellena en la tarjeta. Para el canal de Teams, solo se respeta la `Id` propiedad, que identifica de forma única una solicitud de token.

>[!NOTE]
> El Microsoft Bot Framework `OAuthPrompt` o el es compatible con la autenticación `MultiProviderAuthDialog` SSO.

Si el usuario utiliza la aplicación por primera vez y se requiere el consentimiento del usuario, aparece el siguiente cuadro de diálogo para continuar con la experiencia de consentimiento:

![Cuadro de diálogo Consentimiento](../../../assets/images/bots/bots-consent-dialogbox.png)

Cuando el usuario selecciona **Continuar,** se producen los siguientes eventos:

* Si el bot define un botón de inicio de sesión, el flujo de inicio de sesión para bots se desencadena de forma similar al flujo de inicio de sesión desde un botón de tarjeta OAuth en una secuencia de mensajes. El desarrollador debe decidir qué permisos requieren el consentimiento del usuario. Se recomienda este enfoque si necesita un token con permisos más `openId` allá. Por ejemplo, si desea cambiar el token por recursos de gráfico.

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

#### <a name="receive-the-bot-token"></a>Recibir el token de bot

La respuesta con el token se envía a través de una actividad de invocación con el mismo esquema que otras actividades de invocación que reciben los bots hoy en día. La única diferencia es el nombre de la invocación, **el inicio de sesión/tokenExchange** y el campo **de valor.** El campo **value** contiene el **Id**, una cadena de la solicitud inicial para obtener el token y el campo **token,** un valor de cadena que incluye el token.

>[!NOTE]
> Es posible que reciba varias respuestas para una solicitud determinada si el usuario tiene varios puntos de conexión activos. Debe deduplicar las respuestas con el token.

##### <a name="c-code-to-handle-the-invoke-activity"></a>Código de C# para controlar la actividad de invocación

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

`turnContext.activity.value`Es de tipo [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) y contiene el token que puede usar el bot. Debe almacenar los tokens por motivos de rendimiento y actualizarlos.

### <a name="token-exchange-failure"></a>Error de intercambio de tokens

En caso de error de intercambio de tokens, utilice el código siguiente:

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

Para comprender lo que hace el bot cuando el intercambio de tokens no puede desencadenar un mensaje de consentimiento, consulte los pasos siguientes:

>[!NOTE]
> No es necesario realizar ninguna acción de usuario a medida que el bot realiza las acciones cuando se produce un error en el intercambio de tokens.

1. El cliente inicia una conversación con el bot desencadenando un escenario OAuth.
2. El bot devuelve una tarjeta OAuth al cliente.
3. El cliente intercepta la tarjeta OAuth antes de mostrarla al usuario y comprueba si contiene una `TokenExchangeResource` propiedad.
4. Si la propiedad existe, el cliente envía a `TokenExchangeInvokeRequest` al bot. El cliente debe tener un token intercambiable para el usuario, que debe ser un token de Azure AD v2 y cuyo público debe ser el mismo que la `TokenExchangeResource.Uri` propiedad. El cliente envía una actividad de invocación al bot con el código siguiente:

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

5. El bot procesa el `TokenExchangeInvokeRequest` y devuelve una copia de seguridad al `TokenExchangeInvokeResponse` cliente. El cliente debe esperar hasta que reciba el `TokenExchangeInvokeResponse` archivo .

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

6. Si el `TokenExchangeInvokeResponse` tiene un de , después el cliente no muestra la tarjeta `status` `200` OAuth. Consulte la [imagen de flujo normal](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Para cualquier otro `status` o si no se `TokenExchangeInvokeResponse` recibe, el cliente muestra la tarjeta OAuth al usuario. Consulte la imagen de [flujo de reserva.](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true) Esto garantiza que el flujo SSO vuelva al flujo normal de OAuthCard en caso de errores o dependencias insatisfechas como el consentimiento del usuario.


### <a name="update-the-auth-sample"></a>Actualizar el ejemplo de autenticación

Abra [Teams ejemplo de autenticación](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) y, a continuación, complete los pasos siguientes para actualizarlo:

1. Actualice teamsbot para controlar el desduping de la solicitud entrante mediante la inclusión del código siguiente:

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
  
2. Actualizar `appsettings.json` para incluir el nombre de conexión y la contraseña `botId` definidos en Actualizar Azure Portal con la [conexión OAuth](#update-the-azure-portal-with-the-oauth-connection).
3. Actualice el manifiesto y asegúrese de que `token.botframework.com` está en la lista de dominios válidos. Para obtener más información, consulte [ejemplo de autenticación Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).
4. Comprima el manifiesto con las imágenes de perfil e instálelo en Teams.

## <a name="code-sample"></a>Ejemplo de código
|**Nombre de la muestra** | **Descripción** |**.NET** | 
|----------------|-----------------|--------------|
|Bot framework SDK | Ejemplo para usar el SDK de bot Framework. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
