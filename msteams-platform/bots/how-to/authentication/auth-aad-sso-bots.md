---
title: Compatibilidad con inicio de sesión único para bots
description: Describe cómo obtener un token de usuario. Actualmente, un desarrollador de bots puede usar una tarjeta de inicio de sesión o el servicio de bots de Azure con la compatibilidad con la tarjeta OAuth.
keywords: token, token de usuario, compatibilidad con SSO para bots
ms.topic: conceptual
ms.openlocfilehash: dad36f52a3e23c00f8725e2e906308339629bb05
ms.sourcegitcommit: 23ed7edf145df10dcfba15c43978eae9e0d451a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2021
ms.locfileid: "50753535"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="eda7f-105">Compatibilidad con inicio de sesión único (SSO) para bots</span><span class="sxs-lookup"><span data-stu-id="eda7f-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="eda7f-106">La autenticación de inicio de sesión único en Azure Active Directory (AAD) minimiza el número de veces que los usuarios necesitan escribir sus credenciales de inicio de sesión actualizando silenciosamente el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="eda7f-106">Single sign-on authentication in Azure Active Directory (AAD) minimizes the number of times users need to enter their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="eda7f-107">Si los usuarios aceptan usar la aplicación, no necesitan volver a proporcionar su consentimiento en otro dispositivo y pueden iniciar sesión automáticamente.</span><span class="sxs-lookup"><span data-stu-id="eda7f-107">If users agree to use your app, they need not provide consent again on another device and can sign in automatically.</span></span> <span data-ttu-id="eda7f-108">Sin embargo, el flujo es similar al de la compatibilidad con SSO de [pestañas](#request-a-bot-token) de [Microsoft Teams;](../../../tabs/how-to/authentication/auth-aad-sso.md)sin embargo, la diferencia está en el protocolo de cómo un bot solicita tokens y [recibe respuestas.](#receive-the-bot-token)</span><span class="sxs-lookup"><span data-stu-id="eda7f-108">The flow is similar to that of [Microsoft Teams tab SSO support](../../../tabs/how-to/authentication/auth-aad-sso.md), however, the difference is in the protocol for how a bot [requests tokens](#request-a-bot-token) and [receives responses](#receive-the-bot-token).</span></span>

>[!NOTE]
> <span data-ttu-id="eda7f-109">OAuth 2.0 es un estándar abierto para la autenticación y autorización que usa AAD y muchos otros proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="eda7f-109">OAuth 2.0 is an open standard for authentication and authorization used by AAD and many other identity providers.</span></span> <span data-ttu-id="eda7f-110">Una comprensión básica de OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams.</span><span class="sxs-lookup"><span data-stu-id="eda7f-110">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="eda7f-111">SSO de bot en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="eda7f-111">Bot SSO at runtime</span></span>

![Sso de bot en el diagrama de tiempo de ejecución](../../../assets/images/bots/bots-sso-diagram.png)

<span data-ttu-id="eda7f-113">Siga estos pasos para obtener tokens de aplicación de bot y autenticación:</span><span class="sxs-lookup"><span data-stu-id="eda7f-113">Complete the following steps to get authentication and bot application tokens:</span></span>

1. <span data-ttu-id="eda7f-114">El bot envía un mensaje con un OAuthCard que contiene la `tokenExchangeResource` propiedad.</span><span class="sxs-lookup"><span data-stu-id="eda7f-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="eda7f-115">Indica a Teams que obtenga un token de autenticación para la aplicación bot.</span><span class="sxs-lookup"><span data-stu-id="eda7f-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="eda7f-116">El usuario recibe mensajes en todos los extremos de usuario activos.</span><span class="sxs-lookup"><span data-stu-id="eda7f-116">The user receives messages at all the active user endpoints.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="eda7f-117">Un usuario puede tener más de un extremo activo a la vez.</span><span class="sxs-lookup"><span data-stu-id="eda7f-117">A user can have more than one active endpoint at a time.</span></span>
    >* <span data-ttu-id="eda7f-118">El token de bot se recibe de todos los puntos de conexión de usuario activos.</span><span class="sxs-lookup"><span data-stu-id="eda7f-118">The bot token is received from every active user endpoint.</span></span>
    >* <span data-ttu-id="eda7f-119">La aplicación debe instalarse en el ámbito personal para la compatibilidad con SSO.</span><span class="sxs-lookup"><span data-stu-id="eda7f-119">The app must be installed in personal scope for SSO support.</span></span>

2. <span data-ttu-id="eda7f-120">Si el usuario actual usa la aplicación bot por primera vez, aparece un mensaje de solicitud solicitando al usuario que realice una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="eda7f-120">If the current user is using your bot application for the first time, a request prompt appears requesting the user to do one of the following:</span></span>
    * <span data-ttu-id="eda7f-121">Proporcionar consentimiento, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="eda7f-121">Provide consent, if required.</span></span>
    * <span data-ttu-id="eda7f-122">Controla la autenticación paso a paso, como la autenticación en dos fases.</span><span class="sxs-lookup"><span data-stu-id="eda7f-122">Handle step-up authentication, such as two-factor authentication.</span></span>

3. <span data-ttu-id="eda7f-123">Teams solicita el token de aplicación bot del punto de conexión de AAD para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="eda7f-123">Teams requests the bot application token from the AAD endpoint for the current user.</span></span>

4. <span data-ttu-id="eda7f-124">AAD envía el token de aplicación bot a la aplicación teams.</span><span class="sxs-lookup"><span data-stu-id="eda7f-124">AAD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="eda7f-125">Teams envía el token al bot como parte del objeto de valor devuelto por la actividad invoke con el nombre **sign-in/tokenExchange**.</span><span class="sxs-lookup"><span data-stu-id="eda7f-125">Teams sends the token to the bot as part of the value object returned by the invoke activity with the name **sign-in/tokenExchange**.</span></span>
  
6. <span data-ttu-id="eda7f-126">El token de análisis de la aplicación bot proporciona la información necesaria, como la dirección de correo electrónico del usuario.</span><span class="sxs-lookup"><span data-stu-id="eda7f-126">The parsed token in the bot application provides the required information, such as the user's email address.</span></span>
  
## <a name="develop-an-sso-teams-bot"></a><span data-ttu-id="eda7f-127">Desarrollar un bot de SSO Teams</span><span class="sxs-lookup"><span data-stu-id="eda7f-127">Develop an SSO Teams bot</span></span>
  
<span data-ttu-id="eda7f-128">Siga estos pasos para desarrollar un bot de SSO Teams:</span><span class="sxs-lookup"><span data-stu-id="eda7f-128">Complete the following steps to develop an SSO Teams bot:</span></span>

1. <span data-ttu-id="eda7f-129">[Registrar la aplicación a través del portal de AAD](#register-your-app-through-the-aad-portal).</span><span class="sxs-lookup"><span data-stu-id="eda7f-129">[Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span>
2. <span data-ttu-id="eda7f-130">[Actualice el manifiesto de la aplicación de Teams para el bot](#update-your-teams-application-manifest-for-your-bot).</span><span class="sxs-lookup"><span data-stu-id="eda7f-130">[Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span>
3. <span data-ttu-id="eda7f-131">[Agregue el código para solicitar y recibir un token de bot](#add-the-code-to-request-and-receive-a-bot-token).</span><span class="sxs-lookup"><span data-stu-id="eda7f-131">[Add the code to request and receive a bot token](#add-the-code-to-request-and-receive-a-bot-token).</span></span>

### <a name="register-your-app-through-the-aad-portal"></a><span data-ttu-id="eda7f-132">Registrar la aplicación a través del portal de AAD</span><span class="sxs-lookup"><span data-stu-id="eda7f-132">Register your app through the AAD portal</span></span>

<span data-ttu-id="eda7f-133">Los pasos para registrar la aplicación a través del portal de AAD son similares al [flujo de SSO de tabulación.](../../../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="eda7f-133">The steps to register your app through the AAD portal are similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="eda7f-134">Siga estos pasos para registrar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="eda7f-134">Complete the following steps to register your app:</span></span>

1. <span data-ttu-id="eda7f-135">Registrar una nueva aplicación en el [portal Azure Active Directory – Registros de aplicaciones.](https://go.microsoft.com/fwlink/?linkid=2083908)</span><span class="sxs-lookup"><span data-stu-id="eda7f-135">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="eda7f-136">Seleccione **Nuevo registro**.</span><span class="sxs-lookup"><span data-stu-id="eda7f-136">Select **New Registration**.</span></span> <span data-ttu-id="eda7f-137">Aparece **la página** Registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="eda7f-137">The **Register an application** page appears.</span></span>
3. <span data-ttu-id="eda7f-138">En la **página Registrar una aplicación,** escriba los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="eda7f-138">In the **Register an application** page, enter the following values:</span></span>
    1. <span data-ttu-id="eda7f-139">Escribe un **nombre** para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eda7f-139">Enter a **Name** for your app.</span></span>
    2. <span data-ttu-id="eda7f-140">Elija los **tipos de cuenta admitidos,** seleccione un único inquilino o tipo de cuenta multiempresa.</span><span class="sxs-lookup"><span data-stu-id="eda7f-140">Choose the **Supported account types**, select single tenant or multitenant account type.</span></span>

        > [!NOTE]
        >
        > <span data-ttu-id="eda7f-141">A los usuarios no se les pide su consentimiento y se les conceden tokens de acceso de inmediato, si la aplicación AAD está registrada en el mismo inquilino donde están realizando una solicitud de autenticación en Teams.</span><span class="sxs-lookup"><span data-stu-id="eda7f-141">The users are not asked for consent and are granted access tokens right away, if the AAD app is registered in the same tenant where they are making an authentication request in Teams.</span></span> <span data-ttu-id="eda7f-142">Sin embargo, los usuarios deben dar su consentimiento a los permisos, si la aplicación de AAD está registrada en un inquilino diferente.</span><span class="sxs-lookup"><span data-stu-id="eda7f-142">However, the users must provide consent to the permissions, if the AAD app is registered in a different tenant.</span></span>

    3. <span data-ttu-id="eda7f-143">Elija **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="eda7f-143">Choose **Register**.</span></span>
4. <span data-ttu-id="eda7f-144">En la página de información general, copie y guarde el **identificador de aplicación (cliente).**</span><span class="sxs-lookup"><span data-stu-id="eda7f-144">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="eda7f-145">Lo necesitará más adelante al actualizar el manifiesto de la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="eda7f-145">You need it later when updating your Teams application manifest.</span></span>
5. <span data-ttu-id="eda7f-146">En **Administrar**, seleccione **Exponer una API**</span><span class="sxs-lookup"><span data-stu-id="eda7f-146">Under **Manage**, select **Expose an API**.</span></span> 

   > [!IMPORTANT]
    > * <span data-ttu-id="eda7f-147">Si va a crear un bot independiente, escriba el URI de id. de aplicación como `api://botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="eda7f-147">If you are building a standalone bot, enter the Application ID URI as `api://botid-{YourBotId}`.</span></span> <span data-ttu-id="eda7f-148">Aquí **YourBotId** es el identificador de aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="eda7f-148">Here **YourBotId** is your AAD application ID.</span></span>
    > * <span data-ttu-id="eda7f-149">Si estás creando una aplicación con un bot y una pestaña, escribe el URI de id. de aplicación como `api://fully-qualified-domain-name.com/botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="eda7f-149">If you are building an app with a bot and a tab, enter the Application ID URI as `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

5. <span data-ttu-id="eda7f-150">Seleccione los permisos que la aplicación necesita para el extremo de AAD y, opcionalmente, para Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="eda7f-150">Select the permissions that your application needs for the AAD endpoint and, optionally, for Microsoft Graph.</span></span>
6. <span data-ttu-id="eda7f-151">[Conceder permisos para](/azure/active-directory/develop/v2-permissions-and-consent) aplicaciones de escritorio, web y móviles de Teams.</span><span class="sxs-lookup"><span data-stu-id="eda7f-151">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
7. <span data-ttu-id="eda7f-152">Seleccione **Agregar un ámbito**.</span><span class="sxs-lookup"><span data-stu-id="eda7f-152">Select **Add a scope**.</span></span>
8. <span data-ttu-id="eda7f-153">En el panel que se abre, agregue una aplicación cliente especificando `access_as_user` como nombre de **ámbito**.</span><span class="sxs-lookup"><span data-stu-id="eda7f-153">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="eda7f-154">El ámbito "access_as_user" usado para agregar una aplicación cliente es para "Administradores y usuarios".</span><span class="sxs-lookup"><span data-stu-id="eda7f-154">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>
    >
    > <span data-ttu-id="eda7f-155">Debe tener en cuenta las siguientes restricciones importantes:</span><span class="sxs-lookup"><span data-stu-id="eda7f-155">You must be aware of the following important restrictions:</span></span>
    >
    > * <span data-ttu-id="eda7f-156">Solo se admiten permisos de api de Microsoft Graph de nivel de usuario, como correo electrónico, perfil, offline_access y OpenId.</span><span class="sxs-lookup"><span data-stu-id="eda7f-156">Only user-level Microsoft Graph API permissions, such as email, profile, offline_access, and OpenId are supported.</span></span> <span data-ttu-id="eda7f-157">Si necesita acceso a otros ámbitos de Microsoft Graph, como `User.Read` o , vea la solución alternativa `Mail.Read` [recomendada](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes).</span><span class="sxs-lookup"><span data-stu-id="eda7f-157">If you need access to other Microsoft Graph scopes, such as `User.Read` or `Mail.Read`, see [recommended workaround](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes).</span></span>
    > * <span data-ttu-id="eda7f-158">El nombre de dominio de la aplicación debe ser el mismo que el nombre de dominio que se ha registrado para la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="eda7f-158">Your application's domain name must be same as the domain name that you have registered for your AAD application.</span></span>
    > * <span data-ttu-id="eda7f-159">Actualmente, no se admiten varios dominios por aplicación.</span><span class="sxs-lookup"><span data-stu-id="eda7f-159">Multiple domains per app are currently not supported.</span></span>
    > * <span data-ttu-id="eda7f-160">Las aplicaciones que usan `azurewebsites.net` el dominio no se admiten porque es común y pueden ser un riesgo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="eda7f-160">Applications that use the `azurewebsites.net` domain are not supported because it is common and may be a security risk.</span></span>

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="eda7f-161">Actualizar Azure Portal con la conexión de OAuth</span><span class="sxs-lookup"><span data-stu-id="eda7f-161">Update the Azure portal with the OAuth connection</span></span>

<span data-ttu-id="eda7f-162">Siga estos pasos para actualizar Azure Portal con la conexión de OAuth:</span><span class="sxs-lookup"><span data-stu-id="eda7f-162">Complete the following steps to update the Azure portal with the OAuth connection:</span></span>

1. <span data-ttu-id="eda7f-163">En Azure Portal, vaya a **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="eda7f-163">In the Azure Portal, navigate to **App registrations**.</span></span>

2. <span data-ttu-id="eda7f-164">Vaya a **Permisos de API**.</span><span class="sxs-lookup"><span data-stu-id="eda7f-164">Go to **API Permissions**.</span></span> <span data-ttu-id="eda7f-165">Seleccione **Agregar permisos delegados** de Microsoft Graph y, a continuación,  >    >  agregue los siguientes permisos de la API de Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="eda7f-165">Select **Add a permission** > **Microsoft Graph** > **Delegated permissions**, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="eda7f-166">User.Read (habilitado de forma predeterminada)</span><span class="sxs-lookup"><span data-stu-id="eda7f-166">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="eda7f-167">email</span><span class="sxs-lookup"><span data-stu-id="eda7f-167">email</span></span>
    * <span data-ttu-id="eda7f-168">offline_access</span><span class="sxs-lookup"><span data-stu-id="eda7f-168">offline_access</span></span>
    * <span data-ttu-id="eda7f-169">OpenId</span><span class="sxs-lookup"><span data-stu-id="eda7f-169">OpenId</span></span>
    * <span data-ttu-id="eda7f-170">perfil</span><span class="sxs-lookup"><span data-stu-id="eda7f-170">profile</span></span>

3. <span data-ttu-id="eda7f-171">En Azure Portal, vaya a **Bot Channels Registration**.</span><span class="sxs-lookup"><span data-stu-id="eda7f-171">In the Azure Portal, navigate to **Bot Channels Registration**.</span></span>

4. <span data-ttu-id="eda7f-172">Seleccione **Configuración** en el panel izquierdo y elija **Agregar configuración en** la sección Configuración de conexión de **OAuth.**</span><span class="sxs-lookup"><span data-stu-id="eda7f-172">Select **Settings** on the left pane and choose **Add Setting** under the **OAuth Connection Settings** section.</span></span>

    ![Vista SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. <span data-ttu-id="eda7f-174">Realice los pasos siguientes para completar el **formulario Nueva configuración de** conexión:</span><span class="sxs-lookup"><span data-stu-id="eda7f-174">Perform the following steps to complete the **New Connection Setting** form:</span></span>

    >[!NOTE]
    > <span data-ttu-id="eda7f-175">**La concesión** implícita puede ser necesaria en la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="eda7f-175">**Implicit grant** may be required in the AAD application.</span></span>

    1. <span data-ttu-id="eda7f-176">Escriba un **nombre en** la página Nueva **configuración de** conexión.</span><span class="sxs-lookup"><span data-stu-id="eda7f-176">Enter a **Name** in the **New Connection Setting** page.</span></span> <span data-ttu-id="eda7f-177">Este es el nombre al que se hace referencia dentro de la configuración del código de servicio del bot en el paso *5* de [BOT SSO en tiempo de ejecución.](#bot-sso-at-runtime)</span><span class="sxs-lookup"><span data-stu-id="eda7f-177">This is the name that is referred to inside the settings of your bot service code in *step 5* of [Bot SSO at runtime](#bot-sso-at-runtime).</span></span>
    2. <span data-ttu-id="eda7f-178">En la **lista desplegable Proveedor** de servicios, seleccione Azure Active Directory **v2**.</span><span class="sxs-lookup"><span data-stu-id="eda7f-178">From the **Service Provider** drop-down, select **Azure Active Directory v2**.</span></span>
    3. <span data-ttu-id="eda7f-179">Escriba las credenciales de cliente, como **Id.** de cliente y **Secreto de cliente** para la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="eda7f-179">Enter the client credentials, such as **Client id** and **Client secret** for the AAD application.</span></span>
    4. <span data-ttu-id="eda7f-180">Para la **dirección URL de Exchange de token,** use el valor de ámbito definido en Actualizar el manifiesto de la aplicación de Teams para el [bot](#update-your-teams-application-manifest-for-your-bot).</span><span class="sxs-lookup"><span data-stu-id="eda7f-180">For the **Token Exchange URL**, use the scope value defined in [Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span> <span data-ttu-id="eda7f-181">La dirección URL de Exchange de tokens indica al SDK que esta aplicación de AAD está configurada para SSO.</span><span class="sxs-lookup"><span data-stu-id="eda7f-181">The Token Exchange URL indicates to the SDK that this AAD application is configured for SSO.</span></span>
    5. <span data-ttu-id="eda7f-182">En el **cuadro Id. de** inquilino, escriba *common*.</span><span class="sxs-lookup"><span data-stu-id="eda7f-182">In the **Tenant ID** box, enter *common*.</span></span>
    6. <span data-ttu-id="eda7f-183">Agregue todos los **ámbitos configurados** al especificar permisos para las API de nivel inferior para la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="eda7f-183">Add all the **Scopes** configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="eda7f-184">Con el identificador de cliente y el secreto de cliente proporcionados, el almacén de tokens intercambia el token para un token de gráfico con permisos definidos.</span><span class="sxs-lookup"><span data-stu-id="eda7f-184">With the Client id and Client secret provided, the token store exchanges the token for a graph token with defined permissions.</span></span>
    7. <span data-ttu-id="eda7f-185">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="eda7f-185">Select **Save**.</span></span>

    ![Vista de configuración de VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a><span data-ttu-id="eda7f-187">Actualizar el manifiesto de la aplicación de Teams para el bot</span><span class="sxs-lookup"><span data-stu-id="eda7f-187">Update your Teams application manifest for your bot</span></span>

<span data-ttu-id="eda7f-188">Si la aplicación contiene un bot independiente, use el siguiente código para agregar nuevas propiedades al manifiesto de la aplicación de Teams:</span><span class="sxs-lookup"><span data-stu-id="eda7f-188">If the application contains a standalone bot, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
<span data-ttu-id="eda7f-189">Si la aplicación contiene un bot y una pestaña, use el siguiente código para agregar nuevas propiedades al manifiesto de aplicación de Teams:</span><span class="sxs-lookup"><span data-stu-id="eda7f-189">If the application contains a bot and a tab, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

<span data-ttu-id="eda7f-190">**webApplicationInfo** es el elemento primario de los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="eda7f-190">**webApplicationInfo** is the parent of the following elements:</span></span>

* <span data-ttu-id="eda7f-191">**id:** el identificador de cliente de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eda7f-191">**id** - The client ID of the application.</span></span> <span data-ttu-id="eda7f-192">Este es el identificador de aplicación que obtuvo como parte del registro de la aplicación con AAD.</span><span class="sxs-lookup"><span data-stu-id="eda7f-192">This is the application ID that you obtained as part of registering the application with AAD.</span></span>
* <span data-ttu-id="eda7f-193">**resource:** el dominio y el subdominio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eda7f-193">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="eda7f-194">Este es el mismo URI, incluido el protocolo que registró al crear la aplicación `api://` en Register your app through the `scope` [AAD portal](#register-your-app-through-the-aad-portal).</span><span class="sxs-lookup"><span data-stu-id="eda7f-194">This is the same URI, including the `api://` protocol that you registered when creating your `scope` in [Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span> <span data-ttu-id="eda7f-195">No debe incluir la ruta `access_as_user` de acceso en el recurso.</span><span class="sxs-lookup"><span data-stu-id="eda7f-195">You must not include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="eda7f-196">La parte de dominio de este URI debe coincidir con el dominio y los subdominios usados en las direcciones URL del manifiesto de la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="eda7f-196">The domain part of this URI must match the domain and subdomains used in the URLs of your Teams application manifest.</span></span>

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a><span data-ttu-id="eda7f-197">Agregar el código para solicitar y recibir un token de bot</span><span class="sxs-lookup"><span data-stu-id="eda7f-197">Add the code to request and receive a bot token</span></span>

#### <a name="request-a-bot-token"></a><span data-ttu-id="eda7f-198">Solicitar un token de bot</span><span class="sxs-lookup"><span data-stu-id="eda7f-198">Request a bot token</span></span>

<span data-ttu-id="eda7f-199">La solicitud para obtener el token es una solicitud de mensaje POST normal mediante el esquema de mensaje existente.</span><span class="sxs-lookup"><span data-stu-id="eda7f-199">The request to get the token is a normal POST message request using the existing message schema.</span></span> <span data-ttu-id="eda7f-200">Se incluye en los datos adjuntos de un OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="eda7f-200">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="eda7f-201">El esquema de la clase OAuthCard se define en [microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) y es similar a una tarjeta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="eda7f-201">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is similar to a sign-in card.</span></span> <span data-ttu-id="eda7f-202">Teams trata esta solicitud como una adquisición de token silencioso si la `TokenExchangeResource` propiedad se rellena en la tarjeta.</span><span class="sxs-lookup"><span data-stu-id="eda7f-202">Teams treats this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="eda7f-203">Para el canal de Teams, solo se respeta la propiedad, que identifica de forma exclusiva una solicitud `Id` de token.</span><span class="sxs-lookup"><span data-stu-id="eda7f-203">For the Teams channel, only the `Id` property, which uniquely identifies a token request, is honored.</span></span>

>[!NOTE]
> <span data-ttu-id="eda7f-204">Microsoft Bot Framework `OAuthPrompt` o el es compatible con la `MultiProviderAuthDialog` autenticación sso.</span><span class="sxs-lookup"><span data-stu-id="eda7f-204">The Microsoft Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for SSO authentication.</span></span>

<span data-ttu-id="eda7f-205">Si el usuario usa la aplicación por primera vez y se requiere el consentimiento del usuario, el siguiente cuadro de diálogo parece continuar con la experiencia de consentimiento:</span><span class="sxs-lookup"><span data-stu-id="eda7f-205">If the user is using the application for the first time and user consent is required, the following dialog box appears to continue with the consent experience:</span></span>

![Cuadro de diálogo Consentimiento](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="eda7f-207">Cuando el usuario selecciona **Continuar**, se producen los siguientes eventos:</span><span class="sxs-lookup"><span data-stu-id="eda7f-207">When the user selects **Continue**, the following events occur:</span></span>

* <span data-ttu-id="eda7f-208">Si el bot define un botón de inicio de sesión, el flujo de inicio de sesión para bots se desencadena de forma similar al flujo de inicio de sesión de un botón de tarjeta OAuth en una secuencia de mensajes.</span><span class="sxs-lookup"><span data-stu-id="eda7f-208">If the bot defines a sign-in button, the sign in flow for bots is triggered similar to the sign in flow from an OAuth card button in a message stream.</span></span> <span data-ttu-id="eda7f-209">El desarrollador debe decidir qué permisos requieren el consentimiento del usuario.</span><span class="sxs-lookup"><span data-stu-id="eda7f-209">The developer must decide which permissions require user's consent.</span></span> <span data-ttu-id="eda7f-210">Este enfoque se recomienda si necesita un token con permisos más allá de `openId` .</span><span class="sxs-lookup"><span data-stu-id="eda7f-210">This approach is recommended if you require a token with permissions beyond `openId`.</span></span> <span data-ttu-id="eda7f-211">Por ejemplo, si desea intercambiar el token por recursos de gráfico.</span><span class="sxs-lookup"><span data-stu-id="eda7f-211">For example, if you want to exchange the token for graph resources.</span></span>

* <span data-ttu-id="eda7f-212">Si el bot no proporciona un botón de inicio de sesión en la tarjeta OAuth, se requiere el consentimiento del usuario para un conjunto mínimo de permisos.</span><span class="sxs-lookup"><span data-stu-id="eda7f-212">If the bot is not providing a sign-in button on the OAuth card, user consent is required for a minimal set of permissions.</span></span> <span data-ttu-id="eda7f-213">Este token es útil para la autenticación básica y para obtener la dirección de correo electrónico del usuario.</span><span class="sxs-lookup"><span data-stu-id="eda7f-213">This token is useful for basic authentication and to get the user's email address.</span></span>

##### <a name="c-token-request-without-a-sign-in-button"></a><span data-ttu-id="eda7f-214">C# de token sin un botón de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="eda7f-214">C# token request without a sign-in button</span></span>

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

#### <a name="receive-the-bot-token"></a><span data-ttu-id="eda7f-215">Recibir el token del bot</span><span class="sxs-lookup"><span data-stu-id="eda7f-215">Receive the bot token</span></span>

<span data-ttu-id="eda7f-216">La respuesta con el token se envía a través de una actividad de invocación con el mismo esquema que otras actividades de invocación que los bots reciben hoy.</span><span class="sxs-lookup"><span data-stu-id="eda7f-216">The response with the token is sent through an invoke activity with the same schema as other invoke activities that the bots receive today.</span></span> <span data-ttu-id="eda7f-217">La única diferencia es el nombre de invocación, **el inicio de sesión/tokenExchange** y el **campo de** valor.</span><span class="sxs-lookup"><span data-stu-id="eda7f-217">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field.</span></span> <span data-ttu-id="eda7f-218">El **campo** de valor contiene **el identificador**, una cadena de la solicitud inicial para obtener el token y el campo de **token,** un valor de cadena que incluye el token.</span><span class="sxs-lookup"><span data-stu-id="eda7f-218">The **value** field contains the **Id**, a string of the initial request to get the token and the **token** field, a string value including the token.</span></span>

>[!NOTE]
> <span data-ttu-id="eda7f-219">Es posible que reciba varias respuestas para una solicitud determinada si el usuario tiene varios extremos activos.</span><span class="sxs-lookup"><span data-stu-id="eda7f-219">You might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="eda7f-220">Debe deduplicar las respuestas con el token.</span><span class="sxs-lookup"><span data-stu-id="eda7f-220">You must deduplicate the responses with the token.</span></span>

##### <a name="c-code-to-handle-the-invoke-activity"></a><span data-ttu-id="eda7f-221">C# código para controlar la actividad de invocación</span><span class="sxs-lookup"><span data-stu-id="eda7f-221">C# code to handle the invoke activity</span></span>

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

<span data-ttu-id="eda7f-222">El `turnContext.activity.value` es de tipo [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) y contiene el token que puede usar el bot.</span><span class="sxs-lookup"><span data-stu-id="eda7f-222">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="eda7f-223">Debes almacenar los tokens por motivos de rendimiento y actualizarlos.</span><span class="sxs-lookup"><span data-stu-id="eda7f-223">You must store the tokens for performance reasons and refresh them.</span></span>

### <a name="token-exchange-failure"></a><span data-ttu-id="eda7f-224">Error de intercambio de tokens</span><span class="sxs-lookup"><span data-stu-id="eda7f-224">Token exchange failure</span></span>

<span data-ttu-id="eda7f-225">En caso de error de intercambio de tokens, use el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="eda7f-225">In case of token exchange failure, use the following code:</span></span>

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

<span data-ttu-id="eda7f-226">Para comprender lo que hace el bot cuando el intercambio de tokens no desencadena un mensaje de consentimiento, consulte los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="eda7f-226">To understand what the bot does when the token exchange fails to trigger a consent prompt, see the following steps:</span></span>

>[!NOTE]
> <span data-ttu-id="eda7f-227">No es necesario realizar ninguna acción de usuario a medida que el bot realiza las acciones cuando se produce un error en el intercambio de tokens.</span><span class="sxs-lookup"><span data-stu-id="eda7f-227">No user action is required to be taken as the bot takes the actions when the token exchange fails.</span></span>

1. <span data-ttu-id="eda7f-228">El cliente inicia una conversación con el bot desencadenando un escenario de OAuth.</span><span class="sxs-lookup"><span data-stu-id="eda7f-228">The client starts a conversation with the bot triggering an OAuth scenario.</span></span>
2. <span data-ttu-id="eda7f-229">El bot devuelve una tarjeta OAuth al cliente.</span><span class="sxs-lookup"><span data-stu-id="eda7f-229">The bot sends back an OAuth card to the client.</span></span>
3. <span data-ttu-id="eda7f-230">El cliente intercepta la tarjeta OAuth antes de mostrarla al usuario y comprueba si contiene una `TokenExchangeResource` propiedad.</span><span class="sxs-lookup"><span data-stu-id="eda7f-230">The client intercepts the OAuth card before displaying it to the user and checks if it contains a `TokenExchangeResource` property.</span></span>
4. <span data-ttu-id="eda7f-231">Si la propiedad existe, el cliente envía una al `TokenExchangeInvokeRequest` bot.</span><span class="sxs-lookup"><span data-stu-id="eda7f-231">If the property exists, the client sends a `TokenExchangeInvokeRequest` to the bot.</span></span> <span data-ttu-id="eda7f-232">El cliente debe tener un token intercambiable para el usuario, que debe ser un token de Azure AD v2 y cuya audiencia debe ser la misma que la `TokenExchangeResource.Uri` propiedad.</span><span class="sxs-lookup"><span data-stu-id="eda7f-232">The client must have an exchangeable token for the user, which must be an Azure AD v2 token and whose audience must be the same as `TokenExchangeResource.Uri` property.</span></span> <span data-ttu-id="eda7f-233">El cliente envía una actividad de invocación al bot con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="eda7f-233">The client sends an invoke activity to the bot with the following code:</span></span>

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

5. <span data-ttu-id="eda7f-234">El bot procesa el `TokenExchangeInvokeRequest` y devuelve `TokenExchangeInvokeResponse` una devolución al cliente.</span><span class="sxs-lookup"><span data-stu-id="eda7f-234">The bot processes the `TokenExchangeInvokeRequest` and returns a `TokenExchangeInvokeResponse` back to the client.</span></span> <span data-ttu-id="eda7f-235">El cliente debe esperar hasta que reciba el `TokenExchangeInvokeResponse` archivo .</span><span class="sxs-lookup"><span data-stu-id="eda7f-235">The client must wait till it receives the `TokenExchangeInvokeResponse`.</span></span>

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

6. <span data-ttu-id="eda7f-236">Si el `TokenExchangeInvokeResponse` tiene un de , el cliente no muestra la tarjeta `status` `200` OAuth.</span><span class="sxs-lookup"><span data-stu-id="eda7f-236">If the `TokenExchangeInvokeResponse` has a `status` of `200`, then the client does not show the OAuth card.</span></span> <span data-ttu-id="eda7f-237">Vea la [imagen de flujo normal](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="eda7f-237">See the [normal flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="eda7f-238">Para cualquier otro `status` o si no se `TokenExchangeInvokeResponse` recibe, el cliente muestra la tarjeta OAuth al usuario.</span><span class="sxs-lookup"><span data-stu-id="eda7f-238">For any other `status` or if the `TokenExchangeInvokeResponse` is not received, then the client shows the OAuth card to the user.</span></span> <span data-ttu-id="eda7f-239">Vea la [imagen de flujo de reserva](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="eda7f-239">See the [fallback flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="eda7f-240">Esto garantiza que el flujo de SSO vuelva al flujo OAuthCard normal en caso de errores o dependencias no satisfechas como el consentimiento del usuario.</span><span class="sxs-lookup"><span data-stu-id="eda7f-240">This ensures that the SSO flow falls back to normal OAuthCard flow in case of any errors or unmet dependencies like user consent.</span></span>


### <a name="update-the-auth-sample"></a><span data-ttu-id="eda7f-241">Actualizar el ejemplo de autenticación</span><span class="sxs-lookup"><span data-stu-id="eda7f-241">Update the auth sample</span></span>

<span data-ttu-id="eda7f-242">Abra [el ejemplo de autenticación de Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) y, a continuación, siga estos pasos para actualizarlo:</span><span class="sxs-lookup"><span data-stu-id="eda7f-242">Open [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) and then complete the following steps to update it:</span></span>

1. <span data-ttu-id="eda7f-243">Actualice el TeamsBot para controlar la deduping de la solicitud entrante mediante el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="eda7f-243">Update the TeamsBot to handle the deduping of the incoming request by including the following code:</span></span>

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
  
2. <span data-ttu-id="eda7f-244">Actualice para incluir la , contraseña y el nombre de conexión `appsettings.json` `botId` definidos en [Actualizar Azure Portal con la conexión de OAuth](#update-the-azure-portal-with-the-oauth-connection).</span><span class="sxs-lookup"><span data-stu-id="eda7f-244">Update `appsettings.json` to include the `botId`, password, and the connection name defined in [Update the Azure portal with the OAuth connection](#update-the-azure-portal-with-the-oauth-connection).</span></span>
3. <span data-ttu-id="eda7f-245">Actualice el manifiesto y asegúrese de `token.botframework.com` que está en la lista de dominios válidos.</span><span class="sxs-lookup"><span data-stu-id="eda7f-245">Update the manifest and ensure that `token.botframework.com` is in the valid domains list.</span></span> <span data-ttu-id="eda7f-246">Para obtener más información, vea [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span><span class="sxs-lookup"><span data-stu-id="eda7f-246">For more information, see [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>
4. <span data-ttu-id="eda7f-247">Zip the manifest with the profile images and install it in Teams.</span><span class="sxs-lookup"><span data-stu-id="eda7f-247">Zip the manifest with the profile images and install it in Teams.</span></span>

## <a name="code-sample"></a><span data-ttu-id="eda7f-248">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="eda7f-248">Code sample</span></span>
|<span data-ttu-id="eda7f-249">**Nombre de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="eda7f-249">**Sample name**</span></span> | <span data-ttu-id="eda7f-250">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="eda7f-250">**Description**</span></span> |<span data-ttu-id="eda7f-251">**.NET**</span><span class="sxs-lookup"><span data-stu-id="eda7f-251">**.NET**</span></span> | 
|----------------|-----------------|--------------|
|<span data-ttu-id="eda7f-252">SDK de marco de bots</span><span class="sxs-lookup"><span data-stu-id="eda7f-252">Bot framework SDK</span></span> | <span data-ttu-id="eda7f-253">Ejemplo para usar el SDK del marco de bots.</span><span class="sxs-lookup"><span data-stu-id="eda7f-253">Sample for using the bot framework SDK.</span></span> |[<span data-ttu-id="eda7f-254">View</span><span class="sxs-lookup"><span data-stu-id="eda7f-254">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
