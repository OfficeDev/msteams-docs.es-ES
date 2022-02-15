---
title: Compatibilidad con inicio de sesión único para bots
description: Describe cómo obtener un token de usuario. Actualmente, un desarrollador de bots puede usar una tarjeta de inicio de sesión o el servicio de bots de Azure con la compatibilidad con la tarjeta OAuth.
keywords: token, token de usuario, compatibilidad con SSO para bots, permiso, Microsoft Graph, Azure AD
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 760c9f964298e120dfaf5cfadd199f5a7d02454f
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821601"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Compatibilidad con inicio de sesión único (SSO) para bots

La autenticación de inicio de sesión único en Azure Active Directory actualiza silenciosamente el token de autenticación para minimizar el número de veces que los usuarios necesitan escribir sus credenciales de inicio de sesión. Si los usuarios aceptan usar la aplicación, no tienen que proporcionar el consentimiento de nuevo en otro dispositivo, ya que han iniciado sesión automáticamente. Las pestañas y los bots tienen un flujo similar para la compatibilidad con SSO. Pero el bot [solicita tokens](#request-a-bot-token) y [recibe respuestas](#receive-the-bot-token) con un protocolo diferente.

>[!NOTE]
> OAuth 2.0 es un estándar abierto para la autenticación y autorización que usan Azure AD y muchos otros proveedores de identidades. Un conocimiento básico de OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams.

## <a name="bot-sso-at-runtime"></a>SSO de bot en tiempo de ejecución

La siguiente imagen ilustra el flujo de SSO en bots:

![Sso de bot en el diagrama de tiempo de ejecución](../../../assets/images/bots/bots-sso-diagram.png)

Los siguientes pasos le ayudarán con la autenticación y los tokens de aplicación de bot:

1. El bot envía un mensaje a Teams con un OAuthCard que contiene `tokenExchangeResource` para obtener un token de autenticación para la aplicación bot. El usuario recibe mensajes en todos los puntos de conexión de usuario activos.

   > [!NOTE]
   >
   > * Un usuario puede tener más de un punto de conexión activo a la vez.
   > * El token del bot se recibe de cada punto de conexión de usuario activo.
   > * La aplicación debe instalarse en el ámbito personal para la compatibilidad con SSO.


1. Si el usuario actual usa la aplicación bot por primera vez, aparece un mensaje de solicitud para que realice una de las siguientes acciones:
    * Proporcione su consentimiento, si es necesario.
    * Controle la autenticación paso a paso, como la autenticación en dos fases.

1. Teams solicita el token de aplicación bot desde el punto de conexión Azure AD para el usuario actual.

1. Azure AD envía el token de aplicación bot a la Teams aplicación.

1. Teams envía el token al bot como parte del objeto value devuelto por la invocación con **sign-in/tokenExchange**.
  
1. El token analizado en la aplicación de bot proporciona la información necesaria, como la dirección de correo electrónico del usuario.
  
## <a name="develop-an-sso-teams-bot"></a>Desarrollar un bot Teams SSO
  
Los siguientes pasos le guían para desarrollar sso Teams bot:

1. [Registra la aplicación a través del Azure AD web](#register-your-app-through-the-azure-ad-portal).
1. [Actualice el manifiesto Teams aplicación para el bot](#update-your-teams-application-manifest-for-your-bot).
1. [Agregue el código para solicitar y recibir un token de bot](#add-the-code-to-request-and-receive-a-bot-token).

### <a name="register-your-app-through-the-azure-ad-portal"></a>Registrar la aplicación a través del portal Azure AD web

Los pasos para registrar la aplicación a través del portal de Azure AD son similares al flujo [de SSO de tabulación](../../../tabs/how-to/authentication/auth-aad-sso.md). Los siguientes pasos te guían para registrar la aplicación:

1. Registrar una nueva aplicación en el [portal Azure Active Directory– Registros de aplicaciones](https://go.microsoft.com/fwlink/?linkid=2083908).

1. Seleccione **Nuevo registro**. Aparece la página **Registrar una aplicación**.

    ![Nuevo registro](~/assets/images/authentication/SSO-bots-auth/app-registration.png)

1. En registrar **una aplicación**, siga estos pasos:

   > [!NOTE]
   >
   > A los usuarios no se les pide su consentimiento y se les conceden tokens de acceso inmediatamente, si la aplicación Azure AD está registrada en el mismo inquilino donde están realizando una solicitud de autenticación en Teams. Sin embargo, los usuarios deben dar su consentimiento a los permisos, si la aplicación Azure AD está registrada en un inquilino diferente.

    * Escribe **Nombre** para la aplicación.
    * Seleccione **Tipos de cuenta admitidos**, como un único inquilino o multiempresa.
    * Seleccione **Registrar**.

    ![Registrar una aplicación](~/assets/images/authentication/SSO-bots-auth/register-application.png)

1. Vaya a la página de información general.
1. Copie el valor **del identificador de aplicación (cliente**).
1. En **Administrar**, vaya a **Exponer una API**

   > [!TIP]
   > Para actualizar el manifiesto de la aplicación más adelante, guarde el valor **del identificador de aplicación (** cliente).

   > [!IMPORTANT]
   > * Si va a crear un bot independiente, escriba el URI de id. de aplicación como `api://botid-{YourBotId}`. Aquí *YourBotId* es su Azure AD de aplicación.
   > * Si va a compilar una aplicación con un bot y una pestaña, escriba el URI del identificador de aplicación como `api://fully-qualified-domain-name.com/botid-{YourBotId}`.

1. Seleccione los permisos que la aplicación necesita para el punto de conexión Azure AD y, opcionalmente, para Microsoft Graph.
1. [Conceda permisos para](/azure/active-directory/develop/v2-permissions-and-consent) Teams escritorio, web y aplicaciones móviles.
1. Seleccione **Agregar un ámbito**.
1. En el panel que se solicita, escriba `access_as_user` como nombre **de ámbito**.

   >[!NOTE]
   > El ámbito "access_as_user" usado para agregar una aplicación cliente es para "Administradores y usuarios".
   >
   > Debe tener en cuenta las siguientes restricciones importantes:
   >
   > * Solo se admiten permisos Graph API de Microsoft de nivel de usuario, como correo electrónico, perfil, offline_access y OpenId. Si necesita acceso a otros ámbitos de microsoft Graph, `User.Read` `Mail.Read`como o , vea Obtener un token de acceso [con Graph permisos](../../../tabs/how-to/authentication/auth-aad-sso.md#get-an-access-token-with-graph-permissions).
   > * El nombre de dominio de la aplicación debe ser el mismo que el nombre de dominio que se ha registrado para la Azure AD aplicación.
   > * Actualmente, no se admiten varios dominios por aplicación.
   > * Las aplicaciones que usan el `azurewebsites.net` dominio no se admiten porque es común y pueden ser un riesgo de seguridad.

1. En el **Quién puede dar su consentimiento?**, escriba **Administradores y usuarios**.
1. Escriba los siguientes detalles para configurar los mensajes de consentimiento de administrador y usuario con los valores adecuados para el `access_as_user`ámbito.
    * **Nombre para mostrar** del consentimiento de administrador: Teams puede acceder al perfil del usuario.
    * **Descripción del consentimiento del administrador**: Teams puede llamar a las API web de la aplicación como el usuario actual.
    * **Nombre para mostrar** del consentimiento del usuario: Teams puede acceder a su perfil y realizar solicitudes en su nombre.
    * **Descripción del** consentimiento del usuario: Teams llamar a las API de esta aplicación con los mismos derechos que tiene.

    ![administrador y usuarios](~/assets/images/authentication/SSO-bots-auth/add-a-scope.png)

1. Asegúrese de que el estado está establecido en **Habilitado**.

    ![Estado](~/assets/images/authentication/SSO-bots-auth/enabled-state.png)

1. Seleccione **Agregar ámbito** para guardar los detalles. La parte de dominio del **nombre de** ámbito que se muestra debe coincidir automáticamente con el URI de **id** . de aplicación establecido en el paso anterior, `/access_as_user` con anexado al final `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`.

1. En las **aplicaciones cliente autorizadas**, identifique las aplicaciones que desea autorizar para la aplicación web de la aplicación.
1. Seleccione **Agregar una aplicación cliente**.

    ![aplicación cliente](~/assets/images/authentication/SSO-bots-auth/add-client-application.png)

1. Escriba cada uno de los siguientes Id. de cliente y seleccione el ámbito autorizado que creó en el paso anterior:
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` para la aplicación móvil o de escritorio de Teams.
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` para la aplicación web de Teams.

    ![id. de cliente](~/assets/images/authentication/SSO-bots-auth/add-client-id.png)

1. Vaya a **Autenticación**.
1. En **Configuraciones de plataforma**, seleccione **Agregar una plataforma**.

    ![plataforma](~/assets/images/authentication/SSO-bots-auth/platform-configuration.png)

1. Seleccione **Web**.

    ![Configurar plataforma](~/assets/images/authentication/SSO-bots-auth/configure-platform.png)

1. Escribe los **URI de redireccionamiento** de la aplicación.

   >[!NOTE]
   > Este URI debe ser un nombre de dominio completo. También le sigue la ruta de API a la que se envía una respuesta de autenticación. Si sigue cualquiera de los ejemplos de Teams, el URI es `https://token.botframework.com/.auth/web/redirect`. Para obtener más información, consulte [Flujo de código de autorización de OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

    ![Uris de redireccionamiento](~/assets/images/authentication/SSO-bots-auth/configure-web.png)

1. Agregue los **permisos de API necesarios**.
    * Seleccione **Permisos de API** en el plano izquierdo.
    * Selecciona **Agregar una plataforma para** agregar los permisos delegados de usuario que la aplicación requiere para las API posteriores, por ejemplo, User.Read.

1. Los siguientes pasos le ayudarán a habilitar la concesión implícita:
    * Seleccione **Autenticación** en el panel izquierdo.
    * Seleccione las **casillas De acceso y** **Tokens** de id.
    
    ![Flujo de concesión](~/assets/images/authentication/SSO-bots-auth/grant-flow.png)
    
    * Seleccione **Guardar** para guardar los cambios.

#### <a name="update-manifest-in-microsoft-azure-portal"></a>Actualizar manifiesto en Microsoft Azure portal

Los siguientes pasos le guiarán para actualizar el manifiesto del bot en Azure Portal:

1. Seleccione **Manifiesto** en el panel izquierdo.
1. Asegúrese de que el elemento de configuración está **establecido en "accessTokenAcceptedVersion": 2**. Si no es así, cambie su valor a **2**.

    ![Manifiesto de actualización](~/assets/images/bots/update-manifest.png)


   >[!NOTE]
   > Si ya estás probando el bot en Teams, debes cerrar sesión desde esta aplicación y cerrar sesión desde Teams. A continuación, vuelva a iniciar sesión para ver este cambio.

1. Haga clic en **Guardar**.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Actualizar Azure Portal con la conexión de OAuth

Los pasos siguientes le guiarán para actualizar Azure Portal con la conexión de OAuth:

1. En Azure Portal, vaya a [**AzureBot**](https://ms.portal.azure.com/#create/Microsoft.AzureBot)
1. Vaya a **Configuración** en el panel izquierdo.
1. Seleccione **Agregar conexión de OAuth Configuración**.

    ![Opción de configuración](~/assets/images/authentication/SSO-bots-auth/auth-setting2.png)

1. Los siguientes pasos le guiarán para completar el **formulario Nueva configuración de** conexión:

   >[!NOTE]
   > **La concesión** implícita puede ser necesaria en la Azure AD aplicación.

    * Escriba **Nombre en** la **página Nueva configuración de** conexión.

    >[!NOTE]
    > El **nombre** se hace referencia a la configuración del código de servicio del bot en el paso *5* de [BOT SSO en tiempo de ejecución](#bot-sso-at-runtime).

    * En la **lista desplegable Proveedor** de servicios, **seleccione Azure Active Directory v2**.
    * Escriba las credenciales de cliente, como **id**. de cliente y **secreto** de cliente para la Azure AD aplicación.
    * Para la **dirección URL Exchange** token, use el valor de ámbito definido en Actualizar el [manifiesto Teams aplicación para el bot](#update-your-teams-application-manifest-for-your-bot). La dirección URL Exchange token indica al SDK que esta Azure AD está configurada para SSO.
    * En el **identificador de inquilino**, escriba *common*.
    * Agregue todos los **ámbitos configurados** al especificar permisos para las API de nivel inferior para la Azure AD aplicación. Con el identificador de cliente y el secreto de cliente proporcionados, el almacén de tokens intercambia el token para un token de gráfico con permisos definidos.
    * Haga clic en **Guardar**.
    * Seleccione **Aplicar**.
   
    ![Configuración de conexión](~/assets/images/authentication/Bot-connection-setting.png)

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

* **id**: el Id. de cliente de la aplicación. Es el identificador de aplicación que obtuvo como parte del registro de la aplicación con Azure AD. No compartas este identificador de aplicación con varias Teams aplicaciones. Crea una nueva Azure AD para cada manifiesto de aplicación que usa `webApplicationInfo`.
* **resource**: el dominio y el subdominio de la aplicación. Es el mismo URI, `api://` incluido el protocolo `scope` que registró al crear la aplicación [en Register your app through the Azure AD portal](#register-your-app-through-the-azure-ad-portal). No incluyas la ruta `access_as_user` de acceso en el recurso. La parte de dominio de este URI debe coincidir con el dominio y los subdominios usados en las direcciones URL del manifiesto Teams aplicación.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Agregar el código para solicitar y recibir un token de bot

#### <a name="request-a-bot-token"></a>Solicitar un token de bot

La solicitud para obtener el token es una solicitud de mensaje POST normal mediante el esquema de mensaje existente. Se incluye en los datos adjuntos de un OAuthCard. El esquema de la clase OAuthCard se define en [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) y es similar a una tarjeta de inicio de sesión. Teams trata esta solicitud como una adquisición de tokens silenciosos si la `TokenExchangeResource` propiedad se rellena en la tarjeta. Para el Teams, solo se `Id` respeta la propiedad, que identifica de forma única una solicitud de token.

>[!NOTE]
> El Microsoft Bot Framework `OAuthPrompt` o el es `MultiProviderAuthDialog` compatible con la autenticación de SSO.

Si el usuario usa la aplicación por primera vez y se requiere el consentimiento del usuario, el siguiente cuadro de diálogo parece continuar con la experiencia de consentimiento:

![Cuadro de diálogo Consentimiento](~/assets/images/authentication/SSO-bots-auth/bot-consent-box.png)

Cuando el usuario selecciona **Continuar**, se producen los siguientes eventos:

* Si el bot define un botón de inicio de sesión, se activa el flujo de inicio de sesión para bots que es similar al flujo de inicio de sesión de un botón de tarjeta OAuth en una secuencia de mensajes. El desarrollador debe decidir qué permisos requieren el consentimiento del usuario. Este enfoque se recomienda si necesita un token con permisos más allá de `openId`. Por ejemplo, si desea intercambiar el token por recursos de gráfico.

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

La respuesta con el token se envía a través de una actividad de invocación con el mismo esquema que otras actividades de invocación que los bots reciben hoy. La única diferencia es el nombre de invocación, **el inicio de sesión/tokenExchange** y el **campo de** valor. El **campo** de valor contiene el **identificador**, una cadena de la solicitud inicial para obtener el token y el **campo de token** , un valor de cadena que incluye el token.

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

Si hay un error de intercambio de tokens, use el siguiente código:

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
4. Si la propiedad existe, el cliente envía una al `TokenExchangeInvokeRequest` bot. El cliente debe tener un token intercambiable para el usuario, que debe ser un token Azure AD v2 y cuya audiencia debe ser la misma que la `TokenExchangeResource.Uri` propiedad. El cliente envía una actividad de invocación al bot con el código siguiente:

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

5. El bot procesa el `TokenExchangeInvokeRequest` y devuelve una devolución `TokenExchangeInvokeResponse` al cliente. El cliente debe esperar hasta que reciba el `TokenExchangeInvokeResponse`archivo .

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

6. Si el `TokenExchangeInvokeResponse` tiene un `status` de `200`, el cliente no muestra la tarjeta OAuth. Consulta la [imagen de flujo normal](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Para cualquier otro o `status` si no `TokenExchangeInvokeResponse` se recibe, el cliente muestra la tarjeta OAuth al usuario. Consulta la [imagen de flujo de reserva](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Si hay algún error o dependencias no satisfechas como el consentimiento del usuario, esta actividad garantiza que el flujo de SSO vuelva al flujo normal de OAuthCard.


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
  
2. Actualice `appsettings.json` para incluir la `botId`, contraseña y el nombre de conexión definidos en [Actualizar Azure Portal con la conexión de OAuth](#update-the-azure-portal-with-the-oauth-connection).
3. Actualice el manifiesto y asegúrese de que está `token.botframework.com` en la lista de dominios válidos. Para obtener más información, [vea Teams ejemplo de autenticación](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).
4. Zip the manifest with the profile images and install it in Teams.

## <a name="code-sample"></a>Ejemplo de código
|**Ejemplo de nombre** | **Descripción** |**.NET** | 
|----------------|-----------------|--------------|
|SDK de marco de bots | Ejemplo para usar el SDK del marco de bots. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth)|

## <a name="step-by-step-guide"></a>Guía paso a paso

Siga la [guía paso a paso](../../../sbs-bots-with-sso.yml), que le ayuda a crear un bot con autenticación de SSO habilitada.
