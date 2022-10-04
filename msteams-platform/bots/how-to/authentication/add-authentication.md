---
title: Agregar autenticación al bot de Teams
author: surbhigupta
description: Aprenda a habilitar la autenticación mediante un proveedor de OAuth de terceros en una aplicación de bot en Teams mediante Azure AD.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: db760f81195634431fe0d3415b1a9c3797b519e7
ms.sourcegitcommit: 176bbca74ba46b7ac298899d19a2d75087fb37c1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2022
ms.locfileid: "68376637"
---
# <a name="add-authentication-to-your-teams-bot"></a>Agregar autenticación al bot de Teams

Hay ocasiones en las que es posible que necesite crear bots en Microsoft Teams que puedan acceder a los recursos en nombre del usuario, como un servicio de correo.

En este artículo se muestra cómo usar la autenticación del SDK de Azure Bot Service v4, basada en OAuth 2.0. Esto facilita el desarrollo de un bot que puede usar tokens de autenticación basados en las credenciales del usuario. La clave en todo esto es el uso de **proveedores de identidades**, como veremos más adelante.

OAuth 2.0 es un estándar abierto para la autenticación y autorización que usan Microsoft Azure Active Directory (Azure AD) y muchos otros proveedores de identidades. Tener conocimientos básicos del flujo de concesión implícito de OAuth 2.0 es un requisito previo para trabajar con la autenticación en pestañas de Microsoft Teams.

Consulte [OAuth 2 Simplificado](https://aka.ms/oauth2-simplified) para obtener una descripción básica y [OAuth 2.0](https://oauth.net/2/) para obtener la especificación completa.

Para obtener más información sobre cómo el Azure Bot Service controla la autenticación, vea [Autenticación de usuario dentro de una conversación](https://aka.ms/azure-bot-authentication).

En este artículo, aprenderá lo siguiente:

- **Cómo crear un bot habilitado para autenticación**. Usará [cs-auth-sample][teams-auth-bot-cs] para controlar las credenciales de inicio de sesión de usuario y la generación del token de autenticación.
- **Cómo implementar el bot en Azure y asociarlo a un proveedor de identidades**. El proveedor emite un token basado en las credenciales de inicio de sesión del usuario. El bot puede usar el token para acceder a recursos, como un servicio de correo, que requiere autenticación. Para obtener más información, consulte  [Flujo de autenticación de Microsoft Teams para bots](auth-flow-bot.md).
- **Cómo integrar el bot en Microsoft Teams**. Una vez integrado el bot, puede iniciar sesión e intercambiar mensajes con él en un chat.

## <a name="prerequisites"></a>Requisitos previos

- Conocimientos sobre [los conceptos básicos del bot][concept-basics], [la administración del estado][concept-state], la [biblioteca de diálogos][concept-dialogs] y cómo [implementar el flujo de conversación secuencial][simple-dialog].
- Conocimientos sobre el desarrollo de Azure y OAuth 2.0.
- Las versiones actuales de Microsoft Visual Studio y Git.
- Cuenta de Azure. Si es necesario, puede crear una [cuenta gratuita de Azure](https://azure.microsoft.com/free/).
- El ejemplo siguiente:

    | Muestra | Versión de BotBuilder | Demuestra |
    |:---|:---:|:---|
    | **Autenticación de bot** en [cs-auth-sample][teams-auth-bot-cs] | v4 | Compatibilidad con OAuthCard |
    | **Autenticación de bots** en [js-auth-sample][teams-auth-bot-js] | v4| Compatibilidad con OAuthCard  |
    | **Autenticación de bots** en [ py-auth-sample][teams-auth-bot-py] | v4 | Compatibilidad con OAuthCard |

## <a name="create-the-resource-group"></a>Creación del grupo de recursos

El grupo de recursos y el plan de servicio no son estrictamente necesarios, pero permiten liberar cómodamente los recursos que cree. Este es un procedimiento recomendado para mantener los recursos organizados y administrables.

Use un grupo de recursos para crear recursos individuales para el Bot Framework. Para mejorar el rendimiento, asegúrese de que estos recursos se encuentran en la misma región de Azure.

1. En el explorador, inicie sesión en el [**portal de Microsoft Azure**][azure-portal].
1. En el panel de navegación izquierdo, seleccione **Grupos de recursos**.
1. En la parte superior izquierda de la ventana mostrada, seleccione la pestaña **Agregar** para crear un nuevo grupo de recursos. Se le pedirá que proporcione lo siguiente:
    1. **Suscripción**. Use su suscripción existente.
    1. **Grupo de recursos**. Escriba el nombre del grupo de recursos. Un ejemplo podría ser  *TeamsResourceGroup*. Recuerde que el nombre debe ser único.
    1. En el menú desplegable **Región**, seleccione *Oeste de EE. UU.* o una región cercana a las aplicaciones.
    1. Seleccione el botón **Revisar y crear**. Debería ver un banner que dice *Validación superada*.
    1. Seleccione el botón **Crear**. La creación del grupo de recursos puede tardar unos minutos.

> [!TIP]
> Al igual que con los recursos que creará más adelante en este tutorial, es una buena idea anclar este grupo de recursos al panel para facilitar el acceso. Si desea hacerlo, seleccione el icono de anclaje &#128204; en la esquina superior derecha del panel.

## <a name="create-the-service-plan"></a>Creación del plan de servicio

1. En el [**Azure Portal**][azure-portal], en el panel de navegación izquierdo, seleccione **Crear un recurso**.
1. En el cuadro de búsqueda, escriba *Plan de servicio de la aplicación*. Seleccione la tarjeta **Plan de servicio de la aplicación** en los resultados de la búsqueda.
1. Seleccione **Crear**.
1. Se le pedirá que proporcione la siguiente información:
    1. **Suscripción**. Puede usar una suscripción existente.
    1. **Grupo de recursos**. Seleccione el grupo que creó anteriormente.
    1. **Nombre**. Escriba el nombre del plan de servicio. Un ejemplo podría ser  *TeamsServicePlan*. Recuerde que el nombre debe ser único dentro del grupo.
    1. **Sistema operativo**. Seleccione *Windows* o el sistema operativo aplicable.
    1. **Región**. Seleccione *Oeste de EE. UU.* o una región cercana a las aplicaciones.
    1. **Plan de tarifa**. Asegúrese de que *Estándar S1* está seleccionado. Este debe ser el valor predeterminado.
    1. Seleccione el botón **Revisar y crear**. Debería ver un banner que dice *Validación superada*.
    1. Seleccione **Crear**. La creación del plan de servicio de la aplicación puede tardar unos minutos. El plan se mostrará en el grupo de recursos.

## <a name="create-azure-bot-resource-registration"></a>Creación del registro de recursos del bot de Azure

El registro de recursos de Bot de Azure registra el servicio web como bot con Bot Framework, que proporciona un identificador de aplicación de Microsoft y una contraseña de aplicación (secreto de cliente).

> [!IMPORTANT]
> Solo tiene que registrar el bot si no está hospedado en Azure. Si [creó un bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) a través del portal de Azure, ya está registrado en el servicio. Si creó el bot a través de [Bot Framework](https://dev.botframework.com/bots/new) o [el Portal para desarrolladores](../../../concepts/build-and-test/teams-developer-portal.md), el bot no está registrado en Azure.

1. Visite [**Azure Portal**][azure-portal] y busque **Bot de Azure** en la sección **Crear un recurso**.
1. Abra **Bot de Azure** y seleccione **Crear**.
1. Escriba el nombre del identificador del bot en el campo **Identificador de bot**.
1. Seleccione su **Suscripción** en la lista desplegable.
1. Seleccione el **Grupo de recursos** en la lista desplegable.
1. Seleccione **Tipo de aplicación** como **Multiinquilino** para el **Identificador de aplicación de Microsoft**.

   :::image type="content" source="../../../assets/images/adaptive-cards/multi-tenant.png" alt-text="En esta captura de pantalla se muestra cómo seleccionar varios inquilinos para Microsoft AppID.":::

1. Seleccione **Revisar y crear**.

   :::image type="content" source="../../../assets/images/adaptive-cards/create-azure-bot.png" alt-text="En esta captura de pantalla se muestra cómo crear un bot de Azure.":::

1. Si se supera la validación, seleccione **Crear**.

    El servicio de bot tarda unos minutos en aprovisionarse.

   :::image type="content" source="../../../assets/images/adaptive-cards/validation-pane.png" alt-text="En esta captura de pantalla se muestra cómo se supera la validación del bot de Azure.":::

1. Seleccione **Ir a recursos**. El bot y los recursos relacionados aparecen en el grupo de recursos.

   :::image type="content" source="../../../assets/images/adaptive-cards/go-to-resource-card.png" alt-text="En esta captura de pantalla se muestra cómo seleccionar el grupo de recursos.":::

    Ahora se crea el bot de Azure.

   :::image type="content" source="../../../assets/images/adaptive-cards/azure-bot-ui.png" alt-text="En esta captura de pantalla se muestra cómo crear recursos de bot de Azure.":::

Para crear el secreto de cliente:

1. En **Configuración**, seleccione **Configuración**. Guarde el **identificador de aplicación de Microsoft** (id. de cliente) para futuras referencias.

   :::image type="content" source="../../../assets/images/adaptive-cards/config-microsoft-app-id.png" alt-text="En esta captura de pantalla se muestra cómo agregar el identificador de aplicación de Microsoft para crear el secreto de cliente.":::

1. Junto a **Id. de aplicación de Microsoft**, seleccione **Administrar**.

   :::image type="content" source="~/assets/images/manage-bot-label.png" alt-text="En esta captura de pantalla se muestra cómo crear un bot de administración.":::

1. En la sección **Secretos de cliente**, seleccione **Nuevo secreto de cliente**. Aparece la ventana **Agregar un secreto de cliente**.

   :::image type="content" source="../../../assets/images/meetings-side-panel/newclientsecret.PNG" alt-text="En esta captura de pantalla se muestra cómo crear un nuevo secreto de cliente.":::

1. Escriba **Descripción** y seleccione **Agregar**.

   :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="En la captura de pantalla se muestra cómo escribir la descripción del secreto de cliente.":::

1. En la columna **Valor**, seleccione **Copiar en el Portapapeles** y guarde el identificador de secreto de cliente para futuras referencias.

   :::image type="content" source="../../../assets/images/adaptive-cards/client-secret-value.png" alt-text="En la captura de pantalla se muestra cómo guardar el identificador de secreto de cliente para futuras referencias.":::

Para agregar el canal de Microsoft Teams:

1. Ve a **Inicio**.

   :::image type="content" source="../../../assets/images/adaptive-cards/bot-home-page.png" alt-text="En esta captura de pantalla se muestra la página principal del bot.":::

1. Abra el bot, que aparece en la sección **Recursos recientes**.

1. Seleccione **Canales** en el panel izquierdo y seleccione **Microsoft Teams** :::image type="icon" source="../../../assets/icons/teams-icon.png":::.

   :::image type="content" source="../../../assets/images/adaptive-cards/channel-teams.png" alt-text="En esta captura de pantalla se muestra cómo seleccionar Teams en canales.":::

1. Active la casilla para aceptar los términos de servicio y seleccione **Aceptar**.</br>

   :::image type="content" source="../../../assets/images/adaptive-cards/select-terms-of-service.png" alt-text="En esta captura de pantalla se muestra cómo establecer los términos si el servicio.":::

1. Seleccione **Guardar**.

   :::image type="content" source="../../../assets/images/adaptive-cards/select-teams.png" alt-text="En esta captura de pantalla se muestra cómo agregar el canal de Microsoft Teams.":::

Para obtener más información, vea [Crear un bot para Teams](../create-a-bot-for-teams.md).

## <a name="create-the-identity-provider"></a>Creación del proveedor de identidades

Necesita un proveedor de identidades que se pueda usar para la autenticación.
En este procedimiento, usará un proveedor de Azure AD; también se pueden usar otros proveedores de identidades compatibles con Azure AD.

1. En el [**Portal de Azure**][azure-portal], en el panel de navegación izquierdo, seleccione **Azure Active Directory**.
    > [!TIP]
    > Tendrá que crear y registrar este recurso de Azure AD en un inquilino en el que pueda dar su consentimiento para delegar los permisos solicitados por una aplicación.
    > Para obtener instrucciones sobre cómo crear un inquilino, consulte [Acceso al portal y creación de un inquilino](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).
1. En el panel izquierdo, seleccione **Registros de aplicaciones**.
1. En el panel derecho, seleccione la pestaña **Nuevo registro**, en la esquina superior izquierda.
1. Se le pedirá que proporcione la siguiente información:
   1. **Nombre**. Escriba el nombre de la aplicación. Un ejemplo podría ser  *BotTeamsIdentity*. Recuerde que el nombre debe ser único.
   1. Seleccione los **tipos de cuenta admitidos** para la aplicación. Seleccione *Cuentas en cualquier directorio organizativo (Cualquier Microsoft Azure Active Directory (Azure AD): multiinquilino) y cuentas personales de Microsoft (por ejemplo, Skype, Xbox).*
   1. Para el **URI de redireccionamiento**:<br/>
       &#x2713;Select **Web**. <br/>
       &#x2713; Establezca la dirección URL en `https://token.botframework.com/.auth/web/redirect`.
   1. Seleccione **Registrar**.

1. Una vez creada, Azure muestra la página **Información general** de la aplicación. Copie y guarde la siguiente información en un archivo:

    1. El valor de la **Id. de aplicación (cliente)**. Usará este valor más adelante como *Identificador de cliente* al registrar esta aplicación de identidad de Azure con el bot.
    1. Valor del **Identificador del directorio (inquilino)**. También usará este valor más adelante como *Identificador de inquilino* para registrar esta aplicación de identidad de Azure con el bot.

1. En el panel izquierdo, seleccione **Certificados y secretos** para crear un secreto de cliente para la aplicación.

   1. En **Secretos de cliente**, seleccione &#x2795; **nuevo secreto de cliente**.
   1. Agregue una descripción para identificar este secreto de otros usuarios que pueda necesitar crear para esta aplicación, como *aplicación de identidad de bot en Teams*.
   1. Establezca la **Caducidad** respecto a la selección.
   1. Seleccione **Agregar**.
   1. Antes de salir de esta página, **registre el secreto**. Usará este valor más adelante como *secreto de cliente* al registrar la aplicación Azure AD con el bot.

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a>Configuración de la conexión del proveedor de identidades y registro con el bot

Nota: aquí hay dos opciones para los proveedores de servicios: Azure AD V1 y Azure AD V2.  Las diferencias entre los dos proveedores se resumen [aquí](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), pero en general, V2 proporciona más flexibilidad con respecto al cambio de permisos de bot.  Los permisos Graph API se muestran en el campo ámbitos y, a medida que se agregan nuevos, los bots permitirán a los usuarios dar su consentimiento a los nuevos permisos en el siguiente inicio de sesión.  Para V1, el usuario debe eliminar el consentimiento del bot para que se le soliciten nuevos permisos en el cuadro de diálogo de OAuth.

#### <a name="microsoft-azure-active-directory-azure-ad-v1"></a>Microsoft Azure Active Directory (Azure AD) V1

1. En el [**Portal de Azure**][azure-portal], seleccione el grupo de recursos en el panel.
1. Seleccione el vínculo de registro del bot.
1. Abra la página del recurso y seleccione **Configuración** en **Configuración**.
1. Seleccione el botón **Agregar ajustes de conexión de OAuth** en la pantalla Configuración.
   En la imagen siguiente se muestra la selección correspondiente en la página de recursos:

   ![Configuración de SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)

1. Complete el formulario de la siguiente manera:

    1. **Nombre**. Escriba un nombre para la conexión. Usará este nombre en el bot en el archivo `appsettings.json`. Por ejemplo, *BotTeamsAuthADv1*.
    1. **Proveedor de servicios** Seleccione **Microsoft Azure Active Directory (Azure AD)**. Una vez seleccionado, se mostrarán los campos específicos de Azure AD.
    1. **Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.
    1. **Secreto de cliente** Escriba el secreto que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.
    1. **Tipo de concesión**. Escriba `authorization_code`.
    1. **Dirección URL de inicio de sesión**. Escriba `https://login.microsoftonline.com`.
    1. **Id**. de inquilino, escriba el **identificador de directorio (inquilino)** que registró anteriormente para la aplicación de identidad de Azure o **común** en función del tipo de cuenta compatible seleccionado al crear la aplicación del proveedor de identidades. Para decidir qué valor asignar, siga estos criterios:

        - Si seleccionó *Solo cuentas en este directorio organizativo (solo Microsoft: inquilino único)* o *Cuentas en cualquier directorio organizativo (Microsoft Azure Active Directory (Azure AD): multiinquilino),* escriba el **identificador de inquilino** que registró anteriormente para el Microsoft Azure Active Directory (Azure). AD) aplicación. Este será el inquilino asociado a los usuarios que se pueden autenticar.

        - Si seleccionó *Cuentas en cualquier directorio organizativo (Cualquier Microsoft Azure Active Directory (Azure AD): cuentas de Microsoft multiinquilino y personales, por ejemplo, Skype, Xbox, Outlook,* escriba la palabra **común** en lugar de un identificador de inquilino. De lo contrario, la aplicación Azure AD (Azure AD) comprueba a través del inquilino cuyo identificador se seleccionó y excluye las cuentas personales de Microsoft.

    h. En **Dirección URL del recurso**, escriba `https://graph.microsoft.com/`. Esto no se usa en el ejemplo de código actual.  
    i. Deje **ámbitos** en blanco. La siguiente imagen es un ejemplo:

    :::image type="content" source="../../../assets/images/authentication/auth-bot-identity-connection-adv1.PNG" alt-text="En esta captura de pantalla se muestra cómo agregar la conexión de identidad de bot de autenticación de bot de Teams adv1.":::

1. Seleccione **Guardar**.

#### <a name="microsoft-azure-active-directory-azure-ad-v2"></a>Microsoft Azure Active Directory (Azure AD) V2

1. En el [**Portal de Azure**][azure-portal], seleccione el bot de Azure en el panel.
1. En la página del recurso, seleccione **Configuración** en **Configuración**.
1. Seleccione el botón **Agregar ajustes de conexión de OAuth** en la pantalla Configuración.  
   En la imagen siguiente se muestra la selección correspondiente en la página de recursos:

   :::image type="content" source="../../../assets/images/authentication/sample-app-demo-bot-configuration.png" alt-text="En esta captura de pantalla se muestra la selección correspondiente en la página de recursos.":::

1. Complete el formulario de la siguiente manera:

    1. **Nombre**. Escriba un nombre para la conexión. Usará este nombre en el bot en el archivo `appsettings.json`. Por ejemplo, *BotTeamsAuthADv2*.
    1. **Proveedor de servicios** Seleccione **Microsoft Azure Active Directory** v2. Una vez seleccionado esto, se mostrarán los campos específicos de Azure AD.
    1. **Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.
    1. **Secreto de cliente** Escriba el secreto que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.
    1. **Dirección URL de intercambio de tokens**. Déjelo en blanco.
    1. **Id**. de inquilino, escriba el **identificador de directorio (inquilino)** que registró anteriormente para la aplicación de identidad de Azure o **común** en función del tipo de cuenta compatible seleccionado al crear la aplicación del proveedor de identidades. Para decidir qué valor asignar, siga estos criterios:

        - Si seleccionó *Solo cuentas en este directorio organizativo (solo Microsoft: inquilino único)* o *Cuentas en cualquier directorio organizativo (Microsoft Azure Active Directory - Multiinquilino),* escriba el **identificador de inquilino** que registró anteriormente para la aplicación de Azure AD. Este será el inquilino asociado a los usuarios que se pueden autenticar.

        - Si seleccionó *Cuentas en cualquier directorio organizativo (Cualquier Microsoft Azure Active Directory (Azure AD): cuentas de Microsoft multiinquilino y personales, por ejemplo, Skype, Xbox, Outlook,* escriba la palabra **común** en lugar de un identificador de inquilino. De lo contrario, la aplicación de Azure AD comprueba a través del inquilino cuyo identificador se seleccionó y excluye las cuentas personales de Microsoft.

    1. En **Ámbitos**, escriba una lista delimitada por espacios de permisos de grafos que requiere esta aplicación, por ejemplo: User.Read User.ReadBasic.All Mail.Read

1. Seleccione **Guardar**.

### <a name="test-the-connection"></a>Pruebe la conexión

1. Seleccione la entrada de conexión para abrir la conexión que ha creado.
1. Seleccione **Probar conexión** en la parte superior del panel **Configuración de conexión del proveedor de servicios**.
1. La primera vez que lo haga, se abrirá una nueva ventana del explorador en la que se le pedirá que seleccione una cuenta. Seleccione el que quiera usar.
1. A continuación, se le pedirá que permita al proveedor de identidades usar los datos (credenciales). La siguiente imagen es un ejemplo:

   :::image type="content" source="../../../assets/images/authentication/auth-bot-connection-test-accept.PNG" alt-text="En la captura de pantalla se muestra cómo agregar la cadena de conexión de autenticación de bot de Teams adv1.":::

1. Seleccione **Aceptar**.
1. A continuación, debería redirigirle a una página **Probar conexión a \<your-connection-name> Correcto**. Actualice la página si recibe un error. La siguiente imagen es un ejemplo:

   :::image type="content" source="../../../assets/images/authentication/auth-bot-connection-test-token.PNG" alt-text="En la captura de pantalla se muestra cómo agregar la cadena de conexión de autenticación de aplicaciones de Teams adv1.":::

El código de bot usa el nombre de conexión para recuperar los tokens de autenticación de usuario.

## <a name="prepare-the-bot-sample-code"></a>Preparación del código de ejemplo del bot

Una vez finalizada la configuración preliminar, vamos a centrarnos en la creación del bot que se va a usar en este artículo.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

1. Clone [cs-auth-sample][teams-auth-bot-cs].
1. Inicie Visual Studio.
1. En la barra de herramientas, seleccione **Archivo -> Abrir -> proyecto o solución** y abra el proyecto del bot.
1. En C#, actualice **appsettings.json** de la siguiente manera:

    - Establezca `ConnectionName` en el nombre de la conexión del proveedor de identidades que agregó al registro del bot. El nombre que usamos en este ejemplo es *BotTeamsAuthADv1*.
    - Establezca `MicrosoftAppId` en el **identificador de aplicación del bot** que guardó en el momento del registro del bot.
    - Establezca `MicrosoftAppPassword` en el **secreto de cliente** que guardó en el momento del registro del bot.

    En función de los caracteres del secreto del bot, es posible que deba aplicar un escape XML a la contraseña. Por ejemplo, cualquier y comercial (&) tendrá que codificarse como `&amp;`.

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. En el Explorador de soluciones, vaya a la `TeamsAppManifest` carpeta, abra `manifest.json` y establezca `id` y `botId` en el identificador de **aplicación del bot** que guardó en el momento del registro del bot.

# <a name="javascript"></a>[JavaScript](#tab/node-js)

1. Clone [node-auth-sample][teams-auth-bot-js].
1. En una consola, vaya al proyecto: </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. Instalar módulos</br></br>
`npm install`
1. Actualice la configuración **.env** de la siguiente manera:

    - Establezca `MicrosoftAppId` en el **identificador de aplicación del bot** que guardó en el momento del registro del bot.
    - Establezca `MicrosoftAppPassword` en el **secreto de cliente** que guardó en el momento del registro del bot.
    - Establezca el `connectionName` en el nombre de la conexión del proveedor de identidades.
    En función de los caracteres del secreto del bot, es posible que deba aplicar un escape XML a la contraseña. Por ejemplo, cualquier y comercial (&) tendrá que codificarse como `&amp;`.

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. En la carpeta `teamsAppManifest`, abra `manifest.json` y establezca `id` en el **de id. de aplicación de Microsoft** y `botId` en el **identificador de aplicación del bot** que guardó en el momento del registro del bot.

# <a name="python"></a>[Python](#tab/python)

1. Clone [py-auth-sample][teams-auth-bot-py] desde el repositorio de GitHub.
1. Actualice **config.py**:

    - Establezca `ConnectionName` en el nombre de la configuración de conexión de OAuth que agregó al bot.
    - Establezca `MicrosoftAppId` y `MicrosoftAppPassword` en el identificador de aplicación y el secreto de aplicación del bot.

      En función de los caracteres del secreto del bot, es posible que deba aplicar un escape XML a la contraseña. Por ejemplo, cualquier y comercial (&) tendrá que codificarse como `&amp;`.

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a>Implementar el bot en Azure

Para implementar el bot, siga los pasos descritos en How to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli) (Cómo implementar el bot en Azure).

Como alternativa, mientras esté en Visual Studio, puede seguir estos pasos:

1. En Visual Studio *Explorador de soluciones*, seleccione y mantenga presionado (o haga clic con el botón derecho) el nombre del proyecto.
1. En el menú desplegable, seleccione **Publicar**.
1. En la ventana mostrada, seleccione el vínculo **Nuevo**.
1. En la ventana de diálogo, seleccione **Servicio de la aplicación** a la izquierda y **Crear nuevo** a la derecha.
1. Seleccione el botón **Publicar**.
1. En la siguiente ventana de diálogo, escriba la información necesaria. A continuación puede ver un ejemplo:

   :::image type="content" source="../../../assets/images/authentication/auth-bot-app-service.png" alt-text="En esta captura de pantalla se muestra cómo escribir la información necesaria para la autenticación de App Service.":::

1. Seleccione **Crear**.
1. Si la implementación se completa correctamente, debería verla reflejada en Visual Studio. Además, se muestra una página en el explorador predeterminado que indica *¡El bot está listo!*. La dirección URL será similar a la siguiente: `https://botteamsauth.azurewebsites.net/`. Guárdelo en un archivo.
1. En el explorador, vaya al [**Azure Portal**][azure-portal].
1. Compruebe el grupo de recursos; el bot debe aparecer junto con los demás recursos. La siguiente imagen es un ejemplo:

   :::image type="content" source="../../../assets/images/authentication/auth-bot-app-service-in-group.png" alt-text="En esta captura de pantalla se muestra cómo comprobar el grupo de recursos y el bot.":::

1. En el grupo de recursos, seleccione el nombre de registro del bot (vínculo).
1. En el panel izquierdo, seleccione **Configuración**.
1. En el cuadro **Punto de conexión de mensajería**, escriba la dirección URL obtenida anteriormente seguida de `api/messages`. Este es un ejemplo: `https://botteamsauth.azurewebsites.net/api/messages`.
    > [!NOTE]
    > Solo se permite un punto de conexión de mensajería para un bot.
1. Seleccione el botón **Guardar** en la esquina superior izquierda.

## <a name="test-the-bot-using-the-emulator"></a>Prueba del bot mediante el emulador

Si aún no lo ha hecho, instale el [Emulador de Microsoft Bot Framework](https://aka.ms/bot-framework-emulator-readme). Consulte también [Depurar con el emulador](https://aka.ms/bot-framework-emulator-debug-with-emulator).

Para que el inicio de sesión de ejemplo del bot funcione, debe configurar el emulador.

### <a name="configure-the-emulator-for-authentication"></a>Configuración del emulador para la autenticación

Si un bot requiere autenticación, debe configurar el emulador. Para configurar:

1. Inicie el emulador.
1. En el Emulator, seleccione el icono de engranaje &#9881; en la parte inferior izquierda o la pestaña **Configuración del emulador** en la esquina superior derecha.
1. Active la casilla **Use los tokens de autenticación de la versión 1.0**.
1. Escriba la ruta de acceso local a la herramienta **ngrok**. *Consulte* la [wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)) de la integración de túnel del emulador de Bot Framework/ngrok. Para obtener más información sobre las herramientas, consulte [ngrok](https://ngrok.com/).
1. Active la casilla **Ejecutar ngrok cuando el emulador se inicie**.
1. Seleccione el botón **Guardar**.

Cuando el bot muestra una tarjeta de inicio de sesión y el usuario selecciona el botón de inicio de sesión, el emulador abre una página que el usuario puede usar para iniciar sesión con el proveedor de autenticación.
Una vez que el usuario lo hace, el proveedor genera un token de usuario y lo envía al bot. Después, el bot puede actuar en nombre del usuario.

### <a name="test-the-bot-locally"></a>Probar el bot localmente

Después de configurar el mecanismo de autenticación, puede realizar las pruebas reales del bot.  

1. Ejecute el ejemplo de bot localmente en la máquina, a través de Visual Studio por ejemplo.
1. Inicie el emulador.
1. Seleccione el botón **Abrir bot**.
1. En la **dirección URL del bot**, escriba la dirección URL local del bot. Normalmente, `http://localhost:3978/api/messages`.
1. En Id **. de aplicación de Microsoft**, escriba el identificador de la aplicación del bot desde `appsettings.json`.
1. En la **contraseña de la aplicación de Microsoft** escriba la contraseña de la aplicación del bot desde el `appsettings.json`.
1. Seleccione **Conectar**.
1. Una vez que el bot esté en funcionamiento, escriba cualquier texto para mostrar la tarjeta de inicio de sesión.
1. Seleccione el botón **Iniciar sesión**.
1. Se muestra un cuadro de diálogo emergente para **Confirmar dirección URL abierta**. Esto es para permitir que el usuario del bot (usted) se autentique.  
1. Seleccione **Confirmar**.
1. Si se le pide, seleccione la cuenta del usuario aplicable.
1. Según la configuración que haya usado para el emulador, obtendrá una de las siguientes opciones:
    1. **Usar el código de verificación de inicio de sesión**  
      &#x2713; Se abre una ventana que muestra el código de validación.  
      &#x2713; Copie y escriba el código de validación en el cuadro de chat para completar el inicio de sesión.
    1. **Usar tokens de autenticación**.  
      &#x2713; Ha iniciado sesión en función de sus credenciales.

    La imagen siguiente es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:

    :::image type="content" source="../../../assets/images/authentication/auth-bot-login-emulator.PNG" alt-text="En esta captura de pantalla se muestra un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión.":::

1. Si selecciona **Sí** cuando el bot pregunta *¿Desea ver el token?* obtendrá una respuesta similar a la siguiente:

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-emulator-token.png" alt-text="En esta captura de pantalla se muestra cómo seleccionar el consentimiento.":::

1. Escriba **logout** en el cuadro de chat de entrada para cerrar la sesión. Esto libera el token de usuario y el bot no podrá actuar en su nombre hasta que vuelva a iniciar sesión.

> [!NOTE]
> La autenticación de bots requiere el uso del **Conector de servicio del bot**. El servicio accede a la información de registro de bots del bot.

## <a name="test-the-deployed-bot"></a>Probar el bot implementado

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. En el explorador, vaya al [**Azure Portal**][azure-portal].
1. Busque el grupo de recursos.
1. Seleccione el vínculo del recurso. Se muestra la página de recursos.
1. En la página de recursos, seleccione **Probar en el chat de web**. El bot se inicia y muestra los saludos predefinidos.
1. Escriba cualquier cosa en el cuadro de chat.
1. Seleccione el cuadro **Iniciar sesión**.
1. Se muestra un cuadro de diálogo emergente para **Confirmar dirección URL abierta**. Esto es para permitir que el usuario del bot (usted) se autentique.  
1. Seleccione **Confirmar**.
1. Si se le pide, seleccione la cuenta del usuario aplicable.
    La imagen siguiente es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-deployed.PNG" alt-text="En esta captura de pantalla se muestra un ejemplo de la interfaz de usuario del bot de Teams después de haber iniciado sesión.":::

1. Seleccione el botón **Sí** para mostrar el token de autenticación. La siguiente imagen es un ejemplo:

   :::image type="content" source="../../../assets/images/authentication/auth-bot-login-deployed-token.PNG" alt-text="En esta captura de pantalla se muestra cómo seleccionar el botón Sí para mostrar el token de autenticación.":::

1. Escriba logout para cerrar la sesión.

   :::image type="content" source="../../../assets/images/authentication/auth-bot-deployed-logout.PNG" alt-text="En esta captura de pantalla se muestra cómo escribir el cierre de sesión para cerrar la sesión.":::

> [!NOTE]
> Si tiene problemas para iniciar sesión, intente probar de nuevo la conexión como se describe en los pasos anteriores. Esto podría volver a crear el token de autenticación.
> Con el cliente del chat de web de Bot Framework en Azure, es posible que tenga que iniciar sesión varias veces antes de que la autenticación se establezca correctamente.

## <a name="install-and-test-the-bot-in-teams"></a>Instalar y probar el bot en Teams

1. En el proyecto de bot, asegúrese de que la carpeta `TeamsAppManifest` contiene el `manifest.json` junto con un `outline.png` y archivos `color.png`.
1. En Explorador de soluciones, vaya a la `TeamsAppManifest` carpeta . Edite `manifest.json` asignando los siguientes valores:
    1. Asegúrese de que el **identificador de la aplicación del bot** que recibió en el momento del registro del bot esté asignado a `id` y `botId`.
    1. Asigne este valor: `validDomains: [ "token.botframework.com" ]`.
1. Seleccione y **comprima** los archivos `manifest.json`, `outline.png`y `color.png`.
1. Abra **Microsoft Teams**.
1. En el panel izquierdo, en la parte inferior, seleccione el icono **Aplicaciones**.
1. En el panel derecho, en la parte inferior, seleccione **Cargar una aplicación personalizada**.
1. Vaya a la `TeamsAppManifest` carpeta y cargue el manifiesto comprimido.
Se muestra el asistente siguiente:

   :::image type="content" source="../../../assets/images/authentication/auth-bot-teams-upload.png" alt-text="En esta captura de pantalla se muestra un ejemplo del bot después de cargarlo en Teams.":::

1. Seleccione el botón **Agregar a un equipo**.
1. En la ventana siguiente, seleccione el equipo en el que desea usar el bot.
1. Seleccione el botón **Configurar un bot**.
1. Seleccione los tres puntos (&#x25cf;&#x25cf;&#x25cf;) en el panel izquierdo. A continuación, seleccione el icono **Portal para desarrolladores** .
1. Seleccione la pestaña **Editor de manifiestos**. Debería ver el icono del bot que cargó.
1. Además, debería poder ver que el bot aparece como un contacto en la lista de chats que puede usar para intercambiar mensajes con el bot.

### <a name="testing-the-bot-locally-in-teams"></a>Probando el bot localmente en Teams

Teams es un producto totalmente basado en la nube, requiere que todos los servicios a los que accede estén disponibles desde la nube mediante puntos de conexión HTTPS. Por lo tanto, para permitir que el bot (nuestro ejemplo) funcione en Teams, debe publicar el código en la nube que prefiera o hacer que una instancia de ejecución local sea accesible externamente a través de una herramienta de **tunelización**. Se recomienda  [ngrok](https://ngrok.com/download), que crea una dirección URL direccionable externamente para un puerto que se abre localmente en el equipo.
Para configurar ngrok como preparación para ejecutar la aplicación de Teams localmente, siga estos pasos:

1. En una ventana de terminal, vaya al directorio donde `ngrok.exe` ha instalado. Se recomienda configurar la ruta de la *variable de entorno* para que apunte a ella.
1. Ejecute, por ejemplo, `ngrok http 3978 --host-header=localhost:3978`. Reemplace el número de puerto según sea necesario.
Esto inicia ngrok para escuchar en el puerto que especifique. A cambio, proporciona una dirección URL direccionable externamente, válida mientras se ejecute ngrok. La siguiente imagen es un ejemplo:

   :::image type="content" source="../../../assets/images/authentication/auth-bot-ngrok-start.PNG" alt-text="En esta captura de pantalla se muestra la cadena de conexión de autenticación de la aplicación bot de Teams adv1":::

1. Copie la dirección HTTPS de reenvío. Debe ser similar a lo siguiente: `https://dea822bf.ngrok.io/`.
1. Anexar `/api/messages` para obtener `https://dea822bf.ngrok.io/api/messages`. Este es el **punto de conexión de mensajes** del bot que se ejecuta localmente en el equipo y al que se puede acceder a través de la web en un chat en Teams.
1. Un último paso que se debe realizar es actualizar el punto de conexión de mensajes del bot implementado. En el ejemplo, se implementó el bot en Azure. Se van a realizar estos pasos:
    1. En el explorador, vaya al [**Azure Portal**][azure-portal].
    1. Seleccione el **registro del bot**.
    1. En el panel izquierdo, seleccione **Configuración**.
    1. En el panel derecho, en el cuadro **Punto de conexión de mensajería**, escriba la dirección URL de ngrok, en el ejemplo, `https://dea822bf.ngrok.io/api/messages`.
1. Inicie el bot localmente, por ejemplo, en Visual Studio modo de depuración.
1. Pruebe el bot mientras se ejecuta localmente mediante el **chat web de prueba** del portal de Bot Framework. Al igual que el emulador, esta prueba no le permite acceder a la funcionalidad específica de Teams.
1. En la ventana de terminal donde se ejecuta `ngrok` puede ver el tráfico HTTP entre el bot y el cliente de chat en web. Si desea obtener una vista más detallada, en una ventana del explorador, escriba `http://127.0.0.1:4040` obtuvo de la ventana de terminal anterior. La siguiente imagen es un ejemplo:

   :::image type="content" source="../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png" alt-text="En esta captura de pantalla se muestran las pruebas de ngrok de los equipos de bot de autenticación.":::

> [!NOTE]
> Si detiene y reinicia ngrok, la dirección URL cambia. Para usar ngrok en el proyecto y, en función de las funcionalidades que use, debe actualizar todas las referencias de dirección URL.

## <a name="additional-information"></a>Información adicional

### <a name="teamsappmanifestmanifestjson"></a>TeamsAppManifest/manifest.json

Este manifiesto contiene la información necesaria por Teams para conectarse con el bot:  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "",
  "developer": {
    "name": "TeamsBotAuth",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.teams.com/privacy",
    "termsOfUseUrl": "https://www.teams.com/termsofuse"
  },
  "icons": {
    "color": "color.png",
    "outline": "outline.png"
  },
  "name": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "description": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "accentColor": "#FFFFFF",
  "bots": [
    {
      "botId": "",
      "scopes": [
        "groupchat",
        "team"
      ],
      "supportsFiles": false,
      "isNotificationOnly": false
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [ "token.botframework.com" ]
}
```

Con la autenticación, Teams se comporta de forma ligeramente diferente a otros canales, como se explica a continuación.

### <a name="handling-invoke-activity"></a>Controlar la actividad Invoke

Una **actividad invoke** se envía al bot en lugar de a la actividad de eventos que usan otros canales.
Esto se hace mediante la subclases **ActivityHandler**.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-sample)

**Bots/DialogBot.cs**

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

**Bots/TeamsBot.cs**

La *Actividad Invoke* debe reenviarse al cuadro de diálogo si se usa **OAuthPrompt**.

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a>TeamsActivityHandler.cs

```csharp

protected virtual Task OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    switch (turnContext.Activity.Name)
    {
        case "signin/verifyState":
            return OnSigninVerifyStateAsync(turnContext, cancellationToken);

        default:
            return Task.CompletedTask;
    }
}

protected virtual Task OnSigninVerifyStateAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    return Task.CompletedTask;
}
```

# <a name="javascript"></a>[JavaScript](#tab/node-js-dialog-sample)

**bots/dialogBot.js**

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

**bots/teamsBot.js**

La *Actividad Invoke* debe reenviarse al cuadro de diálogo si se usa **OAuthPrompt**.

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

**diálogos/mainDialog.js**

En un paso del cuadro de diálogo, use `beginDialog` para iniciar el aviso de OAuth, que pide al usuario que inicie sesión.

- Si el usuario ya ha iniciado sesión, se generará un evento de respuesta de token, sin preguntar al usuario.
- De lo contrario, se le pedirá al usuario que inicie sesión. El servicio de bot de Azure envía el evento de respuesta del token después de que el usuario intente iniciar sesión.

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

En el siguiente paso del cuadro de diálogo, compruebe la presencia de un token en el resultado del paso anterior. Si no es null, el usuario inició sesión correctamente.

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

**bots/logoutDialog.js**

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[Python](#tab/python-sample)

**bots/dialog_bot.py**

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

**bots/teams_bot.py**

La *Actividad Invoke* debe reenviarse al cuadro de diálogo si se usa **OAuthPrompt**.

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

**dialogs/main_dialog.py**

En un paso de diálogo, use `begin_dialog` para iniciar el aviso de OAuth, que pide al usuario que inicie sesión.

- Si el usuario ya ha iniciado sesión, se generará un evento de respuesta de token, sin preguntar al usuario.
- De lo contrario, se le pedirá al usuario que inicie sesión. El servicio de bot de Azure envía el evento de respuesta del token después de que el usuario intente iniciar sesión.

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

En el siguiente paso del cuadro de diálogo, compruebe la presencia de un token en el resultado del paso anterior. Si no es null, el usuario inició sesión correctamente.

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

**dialogs/logout_dialog.py**

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="code-sample"></a>Ejemplo de código

En esta sección se proporciona un ejemplo del SDK de Bot Authentication v3.

| **Ejemplo de nombre** | **Descripción** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| Autenticación del bot | En este ejemplo se muestra cómo empezar a usar la autenticación en un bot para Teams. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| Inicio de sesión único (SSO) de pestaña, bot y extensión de mensajes (ME) | En este ejemplo se muestra SSO para pestaña, Bot y ME: búsqueda, acción, linkunfurl. |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | No disponible |

## <a name="see-also"></a>Consulte también

[Agregar autenticación a través del servicio de bot de Azure](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: /azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: /azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: /azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: /azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth
