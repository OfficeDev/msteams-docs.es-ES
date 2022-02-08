---
title: Agregar autenticación al bot de Teams
author: surbhigupta
description: Cómo agregar la autenticación de OAuth a un bot en Microsoft Teams mediante Azure Active Directory. Obtenga información sobre cómo crear, implementar e integrar bots habilitados para autenticación.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
keywords: manifiesto del bot del emulador de Azure de registro de grupo de recursos
ms.openlocfilehash: 6757b355ba9821e6966d5caf88d1a881d48d3145
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435673"
---
# <a name="add-authentication-to-your-teams-bot"></a>Agregar autenticación al bot de Teams

Hay ocasiones en las que es posible que necesite crear bots en Microsoft Teams que puedan tener acceso a recursos en nombre del usuario, como un servicio de correo.

En este artículo se muestra cómo usar la autenticación del SDK de Azure Bot Service v4, basada en OAuth 2.0. Esto facilita el desarrollo de un bot que puede usar tokens de autenticación en función de las credenciales del usuario. Clave en todo esto es el uso de proveedores **de identidades**, como veremos más adelante.

OAuth 2.0 es un estándar abierto para la autenticación y autorización que usan Microsoft Azure Active Directory (Azure AD) y muchos otros proveedores de identidades. Un conocimiento básico de OAuth 2.0 es un requisito previo para trabajar con la autenticación en Teams.

Consulta [OAuth 2 Simplified para](https://aka.ms/oauth2-simplified) obtener una descripción básica y [OAuth 2.0](https://oauth.net/2/) para obtener la especificación completa.

Para obtener más información acerca de cómo el Servicio de bots de Azure controla la autenticación, consulte [Autenticación de usuario en una conversación](https://aka.ms/azure-bot-authentication).

En este artículo, aprenderá lo siguiente:

- **Cómo crear un bot habilitado para autenticación**. Usará [cs-auth-sample][teams-auth-bot-cs] para controlar las credenciales de inicio de sesión del usuario y la generación del token de autenticación.
- **Cómo implementar el bot en Azure y asociarlo con un proveedor de identidades**. El proveedor emite un token en función de las credenciales de inicio de sesión del usuario. El bot puede usar el token para obtener acceso a recursos, como un servicio de correo, que requieren autenticación. Para obtener más información[, vea Microsoft Teams de autenticación para bots](auth-flow-bot.md).
- **Cómo integrar el bot en Microsoft Teams**. Una vez integrado el bot, puedes iniciar sesión e intercambiar mensajes con él en un chat.

## <a name="prerequisites"></a>Requisitos previos

- Conocimiento de [los conceptos básicos del bot][concept-basics], [la administración del][concept-state] estado, la biblioteca de cuadros de diálogo [y][concept-dialogs] cómo [implementar el flujo secuencial de conversación][simple-dialog].
- Conocimiento del desarrollo de Azure y OAuth 2.0.
- Las versiones actuales de Microsoft Visual Studio y Git.
- Cuenta de Azure. Si es necesario, puede crear una cuenta [gratuita de Azure](https://azure.microsoft.com/free/).
- El ejemplo siguiente:

    | Muestra | Versión de BotBuilder | Demostraciones |
    |:---|:---:|:---|
    | **Autenticación de** [bot en cs-auth-sample][teams-auth-bot-cs] | v4 | Compatibilidad con OAuthCard |
    | **Autenticación de** bot [en js-auth-sample][teams-auth-bot-js] | v4| Compatibilidad con OAuthCard  |
    | **Autenticación de bot** [en py-auth-sample][teams-auth-bot-py] | v4 | Compatibilidad con OAuthCard |

## <a name="create-the-resource-group"></a>Crear el grupo de recursos

El grupo de recursos y el plan de servicio no son estrictamente necesarios, pero permiten liberar cómodamente los recursos que cree. Este es un buen procedimiento para mantener los recursos organizados y manejables.

Se usa un grupo de recursos para crear recursos individuales para Bot Framework. Para obtener rendimiento, asegúrese de que estos recursos se encuentran en la misma región de Azure.

1. En el explorador, inicie sesión en el [**Microsoft Azure web**][azure-portal].
1. En el panel de navegación izquierdo, seleccione **Grupos de recursos**.
1. En la parte superior izquierda de la ventana mostrada, seleccione **La** pestaña Agregar para crear un nuevo grupo de recursos. Se le pedirá que proporcione lo siguiente:
    1. **Suscripción**. Use la suscripción existente.
    1. **Grupo de recursos**. Escriba el nombre del grupo de recursos. Un ejemplo podría ser  *TeamsResourceGroup*. Recuerde que el nombre debe ser único.
    1. En el **menú** desplegable Región, seleccione *Oeste de EE.* UU. o una región cercana a las aplicaciones.
    1. Seleccione el **botón Revisar y** crear. Debería ver un banner que lea Validación *pasada*.
    1. Seleccione el **botón** Crear. Puede tardar unos minutos en crear el grupo de recursos.

> [!TIP]
> Al igual que con los recursos que crearás más adelante en este tutorial, es buena idea anclar este grupo de recursos al panel para facilitar el acceso. Si quieres hacerlo, selecciona el icono de patilla &#128204; en la parte superior derecha del panel.

## <a name="create-the-service-plan"></a>Crear el plan de servicio

1. En el [**portal Microsoft Azure**][azure-portal], en el panel de navegación izquierdo, seleccione **Crear un recurso**.
1. En el cuadro de búsqueda, escriba *Plan de App Service*. Seleccione la **tarjeta Plan de App Service** en los resultados de la búsqueda.
1. Seleccione **Crear**.
1. Se le pedirá que proporcione la siguiente información:
    1. **Suscripción**. Puede usar una suscripción existente.
    1. **Grupo de recursos**. Seleccione el grupo que creó anteriormente.
    1. **Nombre**. Escriba el nombre del plan de servicio. Un ejemplo podría ser  *TeamsServicePlan*. Recuerde que el nombre debe ser único, dentro del grupo.
    1. **Sistema operativo**. Seleccione *Windows* o el sistema operativo aplicable.
    1. **Región**. Seleccione *Oeste de EE. UU* . o una región cercana a las aplicaciones.
    1. **Nivel de precios**. Asegúrese de que *standard S1* está seleccionado. Este debe ser el valor predeterminado.
    1. Seleccione el **botón Revisar y** crear. Debería ver un banner que lea Validación *pasada*.
    1. Seleccione **Crear**. Puede tardar unos minutos en crear el plan de servicio de aplicaciones. El plan se enumerará en el grupo de recursos.

## <a name="create-azure-bot-resource-registration"></a>Crear registro de recursos bot de Azure

El registro de recursos bot de Azure registra el servicio web como un bot con Bot Framework, que le proporciona un identificador de aplicación de Microsoft y una contraseña de aplicación (secreto de cliente).

> [!IMPORTANT]
> Solo necesita registrar el bot si no está hospedado en Azure. Si [creó un bot a](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) través del portal Microsoft Azure, ya está registrado en el servicio. Si creó el bot a través del [Bot Framework](https://dev.botframework.com/bots/new) o [el Portal](../../../concepts/build-and-test/teams-developer-portal.md) de desarrolladores, el bot no está registrado en Azure.

1. Visite [**Microsoft Azure portal y**][azure-portal] busque **Azure Bot** en **la sección Crear un recurso**.
1. Abra el **Bot de Azure** y seleccione **Crear**.
1. Escriba el nombre del controlador del **bot en el campo Detección de** bots.
1. Selecciona tu **suscripción** en la lista desplegable.
1. Selecciona el **grupo De recursos** de la lista desplegable.
1. Selecciona **Tipo de aplicación como** **multiinquilino** para **id. de aplicación de Microsoft**.

    ![Multi Tenant](~/assets/images/adaptive-cards/multi-tenant.png)

1. Seleccione **Revisar y crear**.

    ![Crear bot de Azure](~/assets/images/adaptive-cards/create-azure-bot.png)

1. Si la validación pasa, seleccione **Crear**.

    El servicio de bots tarda unos minutos en aprovisionarse.

    ![Validación del bot de Azure](~/assets/images/adaptive-cards/validation-pane.png)

1. Seleccione **Ir a recursos**. El bot y los recursos relacionados se enumeran en el grupo de recursos.

    ![Ir al recurso](~/assets/images/adaptive-cards/go-to-resource-card.png)

    Ahora se crea el bot de Azure.
    
    ![Recurso de bot de Azure creado](~/assets/images/adaptive-cards/azure-bot-ui.png)

**Para crear un secreto de cliente**

1. En **Configuración**, seleccione **Configuración**. Guarde el **id. de aplicación de Microsoft** (id. de cliente) para la referencia futura.

    ![Id. de aplicación de Microsoft](~/assets/images/adaptive-cards/config-microsoft-app-id.png)

1. Junto al **id. de la aplicación de Microsoft**, selecciona **Administrar**.

    ![Administrar bot](~/assets/images/adaptive-cards/manage-bot-label.png)

1. En la **sección Secretos de** cliente, seleccione **Nuevo secreto de cliente**. **Aparece agregar una ventana secreta** de cliente.

    ![Nuevo secreto de cliente](~/assets/images/adaptive-cards/new-client-secret.png)

1. Escriba **Descripción** y seleccione **Agregar**.
 
    ![Secreto de cliente](~/assets/images/adaptive-cards/client-secret.png)

1. En la **columna Valor** , seleccione **Copiar en el** Portapapeles y guarde el identificador de secreto de cliente para la referencia futura.

    ![Valor secreto de cliente](~/assets/images/adaptive-cards/client-secret-value.png)
       
**Para agregar el Microsoft Teams canal**

1. Vaya a **Inicio**.

    ![Página principal del bot](~/assets/images/adaptive-cards/bot-home-page.png)

1. Abra el bot, que aparece en la **sección Recursos** recientes.
1. Seleccione **Canales** en el panel izquierdo y **seleccione Teams** <img src="~/assets/images/bots/teamsicon.png" alt="Teams icon" width="20"/>.

    ![Canal Teams](~/assets/images/adaptive-cards/channel-teams.png)

1. Active la casilla para aceptar los términos del servicio y seleccione **Aceptar**.</br>

    ![Seleccionar términos de servicio](~/assets/images/adaptive-cards/select-terms-of-service.png)

1. Seleccione **Guardar**.

    ![Seleccione Teams](~/assets/images/adaptive-cards/select-teams.png)

Para obtener más información, vea [Create a bot for Teams](../create-a-bot-for-teams.md).

## <a name="create-the-identity-provider"></a>Crear el proveedor de identidades

Necesita un proveedor de identidades que se pueda usar para la autenticación.
En este procedimiento, usará un proveedor de Azure AD y también Azure AD proveedores de identidades compatibles.

1. En el [**portal Microsoft Azure**][azure-portal], en el panel de navegación izquierdo, seleccione **Azure Active Directory**.
    > [!TIP]
    > Deberá crear y registrar este recurso Azure AD en un espacio empresarial en el que pueda dar su consentimiento para delegar los permisos solicitados por una aplicación.
    > Para obtener instrucciones sobre cómo crear un inquilino, vea [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).
1. En el panel izquierdo, selecciona **Registros de aplicaciones**.
1. En el panel derecho, seleccione la **pestaña Nuevo registro** , en la parte superior izquierda.
1. Se le pedirá que proporcione la siguiente información:
   1. **Nombre**. Escriba el nombre de la aplicación. Un ejemplo podría ser  *BotTeamsIdentity*. Recuerde que el nombre debe ser único.
   1. Seleccione los **tipos de cuenta admitidos** para la aplicación. Selecciona *Cuentas en cualquier directorio de la organización (cualquier Microsoft Azure Active Directory (Azure AD) - Multitenant) y cuentas personales de Microsoft (por ejemplo, Skype, Xbox).*.
   1. Para el **URI de redireccionamiento**:<br/>
       &#x2713;Seleccione **Web**. <br/>
       &#x2713; Establezca la dirección URL en `https://token.botframework.com/.auth/web/redirect`.
   1. Seleccione **Registrar**.

1. Una vez creado, Azure muestra la **página Información** general de la aplicación. Copie y guarde la siguiente información en un archivo:

    1. Valor **de id. de aplicación (** cliente). Este valor se usará más adelante *como identificador de* cliente al registrar esta aplicación de identidad de Azure con el bot.
    1. Valor **del id. de directorio (espacio** empresarial). También usarás este valor más adelante como identificador *de* inquilino para registrar esta aplicación de identidad de Azure con el bot.

1. En el panel izquierdo, seleccione **Certificados & secretos para** crear un secreto de cliente para la aplicación.

   1. En **Secretos de** cliente, &#x2795; **Nuevo secreto de cliente**.
   1. Agrega una descripción para identificar este secreto de otros usuarios que podrías necesitar crear para esta aplicación, como La aplicación de identidad bot *en Teams*.
   1. Establece **Expira en** la selección.
   1. Seleccione **Agregar**.
   1. Antes de salir de esta página, **registre el secreto**. Este valor se usará más adelante como secreto de  cliente al registrar la aplicación Azure AD con el bot.

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a>Configurar la conexión del proveedor de identidades y registrarla con el bot

Nota: hay dos opciones para los proveedores de servicios aquí Microsoft Azure Active Directory (Azure AD) V1 y Microsoft Azure Active Directory (Azure AD) V2.  Las diferencias entre los dos proveedores se resumen [aquí, pero](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), en general, V2 proporciona más flexibilidad con respecto a cambiar los permisos del bot.  Graph permisos de API se enumeran en el campo ámbitos y, a medida que se agregan nuevos, los bots permitirán a los usuarios dar su consentimiento a los nuevos permisos en el siguiente inicio de sesión.  Para V1, el usuario debe eliminar el consentimiento del bot para que se pidan nuevos permisos en el cuadro de diálogo OAuth. 

#### <a name="microsoft-azure-active-directory-azure-ad-v1"></a>Microsoft Azure Active Directory (Azure AD) V1

1. En el [**Microsoft Azure,**][azure-portal] seleccione el grupo de recursos en el panel.
1. Seleccione el vínculo de registro del bot.
1. Abra la página de recursos y **seleccione Configuración** **en Configuración**. 
1. Seleccione **Agregar conexión de OAuth Configuración**.    
La siguiente imagen muestra la selección correspondiente en la página de recursos:  
![Configuración de SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)
1. Complete el formulario de la siguiente manera:

    1. **Nombre**. Escriba un nombre para la conexión. Usarás este nombre en el bot en el `appsettings.json` archivo. Por ejemplo *BotTeamsAuthADv1*.
    1. **Proveedor de servicios**. Seleccione **Microsoft Azure Active Directory (Azure AD)**. Una vez seleccionado, se mostrarán Azure AD campos específicos del usuario.
    1. **Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.
    1. **Secreto de cliente**. Escriba el secreto que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.
    1. **Tipo de concesión**. Escriba `authorization_code`.
    1. **Dirección URL de inicio de sesión**. Escriba `https://login.microsoftonline.com`.
    1. **Id. de** inquilino, escriba el id. de directorio **(espacio empresarial)** que registró anteriormente para  la aplicación de identidad de Azure o común según el tipo de cuenta admitido seleccionado al crear la aplicación del proveedor de identidades. Para decidir qué valor asignar, siga estos criterios:

        - Si seleccionó Cuentas solo en este directorio de la organización *(Solo Microsoft -* Inquilino único) o Cuentas en cualquier directorio de la organización *(Microsoft Azure Active Directory (Azure AD) - Inquilino múltiple)* escriba el identificador de inquilino  que registró anteriormente para el Microsoft Azure Active Directory (Azure AD). Este será el espacio empresarial asociado con los usuarios que se pueden autenticar.

        - Si seleccionó Cuentas en cualquier directorio de la organización (Cualquier Microsoft Azure Active Directory (Azure AD) - Cuentas de Microsoft multiinquilino y personales, por ejemplo *, Skype, Xbox, Outlook)* escriba la palabra **común** en lugar de un identificador de inquilino. De lo contrario, la Microsoft Azure Active Directory (Azure AD) comprobará a través del inquilino cuyo identificador se seleccionó y excluirá las cuentas personales de Microsoft.

    h. En **Dirección URL de** recurso, escriba `https://graph.microsoft.com/`. Esto no se usa en el ejemplo de código actual.  
    i. Deje **ámbitos en** blanco. La siguiente imagen es un ejemplo:

    ![vista de cadena de conexión de la aplicación de bots de teams adv1](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. Seleccione **Guardar**.

#### <a name="microsoft-azure-active-directory-azure-ad-v2"></a>Microsoft Azure Active Directory (Azure AD) V2

1. En el [**portal Microsoft Azure**][azure-portal], seleccione el Bot de Azure en el panel.
1. En la página de recursos, seleccione **Configuración** en **Configuración**. 
1. Seleccione **Agregar conexión de OAuth Configuración**.  
La siguiente imagen muestra la selección correspondiente en la página de recursos:        
![Configuración de SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png) 

1. Complete el formulario de la siguiente manera:

    1. **Nombre**. Escriba un nombre para la conexión. Usarás este nombre en el bot en el `appsettings.json` archivo. Por ejemplo *, BotTeamsAuthADv2*.
    1. **Proveedor de servicios**. Seleccione **Microsoft Azure Active Directory v2**. Una vez seleccionado, se mostrarán los Microsoft Azure Active Directory (Azure AD) específicos del usuario.
    1. **Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.
    1. **Secreto de cliente**. Escriba el secreto que registró para la aplicación proveedora de identidades de Azure en los pasos anteriores.
    1. **Dirección URL Exchange token**. Déjelo en blanco.
    1. **Id. de** inquilino, escriba el id. de directorio **(espacio empresarial)** que registró anteriormente para  la aplicación de identidad de Azure o común según el tipo de cuenta admitido seleccionado al crear la aplicación del proveedor de identidades. Para decidir qué valor asignar, siga estos criterios:

        - Si seleccionó Cuentas solo en este directorio de la organización *(Solo Microsoft -* Inquilino único) o Cuentas en cualquier directorio de la organización *(Microsoft Azure Active Directory - Inquilino múltiple)* escriba  el identificador de inquilino que registró anteriormente para la aplicación Microsoft Azure Active Directory (Azure AD). Este será el espacio empresarial asociado con los usuarios que se pueden autenticar.

        - Si seleccionó Cuentas en cualquier directorio de la organización (Cualquier Microsoft Azure Active Directory (Azure AD) - Cuentas de Microsoft multiinquilino y personales, por ejemplo *, Skype, Xbox, Outlook)* escriba la palabra **común** en lugar de un identificador de inquilino. De lo contrario, la Microsoft Azure Active Directory (Azure AD) comprobará a través del inquilino cuyo identificador se seleccionó y excluirá las cuentas personales de Microsoft.

    1. Para **ámbitos**, escriba una lista delimitada por espacios de permisos de gráfico que esta aplicación requiere, por ejemplo: User.Read User.ReadBasic.All Mail.Read 

1. Seleccione **Guardar**.

### <a name="test-the-connection"></a>Probar la conexión

1. Seleccione la entrada de conexión para abrir la conexión que acaba de crear.
1. Seleccione **Probar conexión en** la parte superior del panel Configuración de conexión **del proveedor de** servicios.
1. La primera vez que lo hagas, se abrirá una nueva ventana del explorador que te pedirá que selecciones una cuenta. Seleccione la que desea usar.
1. A continuación, se le pedirá que permita al proveedor de identidades usar sus datos (credenciales). La siguiente imagen es un ejemplo:

    ![cadena de conexión de autenticación de bots de teams adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. Seleccione **Aceptar**.
1. A continuación, debería redirigirle a una **página Conexión de prueba \<your-connection-name> a Correcta** . Actualice la página si recibe un error. La siguiente imagen es un ejemplo:

    ![teams bots app auth connection str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

El código de bot usa el nombre de conexión para recuperar tokens de autenticación de usuario.

## <a name="prepare-the-bot-sample-code"></a>Preparar el código de ejemplo del bot

Una vez realizada la configuración preliminar, vamos a centrarnos en la creación del bot que se va a usar en este artículo.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

1. Clone [cs-auth-sample][teams-auth-bot-cs].
1. Inicie Visual Studio.
1. En la barra de herramientas, **seleccione Archivo -> Abrir -> Project/Solución** y abra el proyecto de bot.
1. En C# Update **appsettings.json** de la siguiente manera:

    - Establezca `ConnectionName` el nombre de la conexión del proveedor de identidades que agregó al registro del bot. El nombre que hemos usado en este ejemplo es *BotTeamsAuthADv1*.
    - Se `MicrosoftAppId` establece en el **identificador de aplicación del bot** que guardó en el momento del registro del bot.
    - Se `MicrosoftAppPassword` establece en el **secreto de cliente** que guardó en el momento del registro del bot.

    Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña mediante XML. Por ejemplo, cualquier ampersands (&) tendrá que codificarse como `&amp;`.

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. En el Explorador de soluciones, vaya a la `TeamsAppManifest` carpeta, abra `manifest.json` y establezca `botId` `id` y al **id**. de aplicación bot que guardó en el momento del registro del bot.

# <a name="javascript"></a>[JavaScript](#tab/node-js)

1. Clone [node-auth-sample][teams-auth-bot-js].
1. En una consola, vaya al proyecto: </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. Instalar módulos</br></br>
`npm install`
1. Actualice la **configuración .env** de la siguiente manera:

    - Se `MicrosoftAppId` establece en el **identificador de aplicación del bot** que guardó en el momento del registro del bot.
    - Se `MicrosoftAppPassword` establece en el **secreto de cliente** que guardó en el momento del registro del bot.
    - Establezca el `connectionName` valor en el nombre de la conexión del proveedor de identidades.
    Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña mediante XML. Por ejemplo, cualquier ampersands (&) tendrá que codificarse como `&amp;`.

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. En la `teamsAppManifest` carpeta, abra y `manifest.json` establezca `id`  el id. de **la aplicación de Microsoft** `botId` y el **id** . de la aplicación bot que guardó en el momento del registro del bot.

# <a name="python"></a>[Python](#tab/python)

1. Clone [py-auth-sample][teams-auth-bot-py] desde el repositorio de github.
1. Actualizar **config.py**:

    - Establezca `ConnectionName` el nombre de la configuración de conexión de OAuth que agregó al bot.
    - Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.

      Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña mediante XML. Por ejemplo, cualquier ampersands (&) tendrá que codificarse como `&amp;`.

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a>Implementar el bot en Azure

Para implementar el bot, siga los pasos descritos en el procedimiento [para implementar el bot en Azure](https://aka.ms/azure-bot-deployment-cli).

Como alternativa, mientras esté Visual Studio, puede seguir estos pasos:

1. En Visual Studio *Explorador de soluciones*, seleccione y mantenga presionado (o haga clic con el botón secundario) en el nombre del proyecto.
1. En el menú desplegable, seleccione **Publicar**.
1. En la ventana mostrada, seleccione el **vínculo** Nuevo.
1. En la ventana de diálogo, seleccione **App Service** a la izquierda y **Crear nuevo** a la derecha.
1. Seleccione el **botón** Publicar.
1. En la siguiente ventana de diálogo, escriba la información necesaria. A continuación puede ver un ejemplo:

    ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. Seleccione **Crear**.
1. Si la implementación se completa correctamente, debería verlo reflejado en Visual Studio. Además, se muestra una página en el explorador predeterminado que dice *Que el bot está listo.* La dirección URL será similar a esta: `https://botteamsauth.azurewebsites.net/`. Guárdelo en un archivo.
1. En el explorador, vaya al [**portal de Microsoft Azure web**][azure-portal].
1. Compruebe el grupo de recursos, el bot debe aparecer junto con los demás recursos. La siguiente imagen es un ejemplo:

    ![teams-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. En el grupo de recursos, seleccione el nombre de registro del bot (vínculo).
1. En el panel izquierdo, seleccione **Configuración**.
1. En el **cuadro Punto de conexión** de mensajería, escriba la dirección URL obtenida anteriormente seguida de `api/messages`. Este es un ejemplo: `https://botteamsauth.azurewebsites.net/api/messages`.
    > [!NOTE]
    > Solo se permite un extremo de mensajería para un bot
1. Seleccione el **botón** Guardar en la parte superior izquierda.

## <a name="test-the-bot-using-the-emulator"></a>Pruebe el bot con el Emulator

Si aún no lo ha hecho, instale el [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme). Vea también [Depurar con el Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).

Para que el inicio de sesión de ejemplo del bot funcione, debe configurar el Emulator.

### <a name="configure-the-emulator-for-authentication"></a>Configurar el Emulator para la autenticación

Si un bot requiere autenticación, debe configurar el Emulator. Para configurar:

1. Inicie el Emulator.
1. En el Emulator, seleccione el icono de engranaje &#9881; la parte inferior izquierda o la pestaña **Emulator Configuración** en la parte superior derecha.
1. Active la casilla Usar **tokens de autenticación de la versión 1.0**.
1. Escriba la ruta de acceso local a la **herramienta ngrok** . *Consulta* el wiki Bot Framework Emulator integración de túneles [de Bot Framework Emulator/ngrok](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)). Para obtener más información sobre la herramienta, [vea ngrok](https://ngrok.com/).
1. Active la casilla **Ejecutar ngrok cuando Emulator se inicie**.
1. Seleccione el **botón** Guardar.

Cuando el bot muestra una tarjeta de inicio de sesión y el usuario selecciona el botón de inicio de sesión, el Emulator abre una página que el usuario puede usar para iniciar sesión con el proveedor de autenticación.
Una vez que el usuario lo hace, el proveedor genera un token de usuario y lo envía al bot. Después, el bot puede actuar en nombre del usuario.

### <a name="test-the-bot-locally"></a>Probar el bot localmente

Después de configurar el mecanismo de autenticación, puede realizar las pruebas de bot reales.  

1. Ejecute el ejemplo de bot localmente en el equipo, por Visual Studio por ejemplo.
1. Inicie el Emulator.
1. Seleccione el **botón Abrir bot** .
1. En la **dirección URL del bot**, escriba la dirección URL local del bot. Normalmente, `http://localhost:3978/api/messages`.
1. En el **Id. de aplicación de Microsoft** , escriba el identificador de aplicación del bot desde `appsettings.json`.
1. En la **contraseña de Microsoft App** , escriba la contraseña de la aplicación del bot desde `appsettings.json`.
1. Seleccione **Conectar**.
1. Después de que el bot esté en funcionamiento, escriba cualquier texto para mostrar la tarjeta de inicio de sesión.
1. Seleccione el botón **Iniciar sesión**.
1. Se muestra un cuadro de diálogo emergente para **Confirmar dirección URL abierta**. Esto permite que el usuario del bot (usted) se autentique.  
1. Seleccione **Confirmar**.
1. Si se le pide, seleccione la cuenta del usuario aplicable.
1. Según la configuración que usó para la Emulator, se obtiene una de las siguientes opciones:
    1. **Uso del código de verificación de inicio de sesión**  
      &#x2713; Se abre una ventana que muestra el código de validación.  
      &#x2713; copiar y escribir el código de validación en el cuadro de chat para completar el inicio de sesión.
    1. **Uso de tokens de autenticación**.  
      &#x2713; Ha iniciado sesión en función de sus credenciales.

    La siguiente imagen es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:

    ![Emulador de inicio de sesión del bot de autenticación](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. Si selecciona Sí **cuando** el bot le pregunta ¿Le gustaría ver *el token?*, tendrá una respuesta similar a la siguiente:

    ![Token de emulador de inicio de sesión del bot de autenticación](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. Escriba **cerrar sesión en** el cuadro de chat de entrada para cerrar la sesión. Esto libera el token de usuario y el bot no podrá actuar en su nombre hasta que inicie sesión de nuevo.

> [!NOTE]
> La autenticación de bots requiere el uso del **servicio Bot Connector**. El servicio tiene acceso a la información de registro de bots para el bot.

## <a name="test-the-deployed-bot"></a>Probar el bot implementado

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. En el explorador, vaya al [**portal de Microsoft Azure web**][azure-portal].
1. Busque el grupo de recursos.
1. Seleccione el vínculo de recurso. Se muestra la página de recursos.
1. En la página de recursos, seleccione **Probar en chat web**. El bot se inicia y muestra los saludos predefinidos.
1. Escriba cualquier cosa en el cuadro de chat.
1. Seleccione el **cuadro Iniciar sesión** .
1. Se muestra un cuadro de diálogo emergente para **Confirmar dirección URL abierta**. Esto permite que el usuario del bot (usted) se autentique.  
1. Seleccione **Confirmar**.
1. Si se le pide, seleccione la cuenta del usuario aplicable.
    La siguiente imagen es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:

    ![Inicio de sesión del bot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed.PNG).

1. Seleccione el **botón Sí** para mostrar el token de autenticación. La siguiente imagen es un ejemplo:

    ![Token de inicio de sesión del bot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG).

1. Escriba cerrar sesión para cerrar sesión.

    ![Inicio de sesión implementado por el bot de autenticación](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> Si tiene problemas para iniciar sesión, intente probar la conexión de nuevo como se describe en los pasos anteriores. Esto podría volver a crear el token de autenticación.
> Con el cliente de Chat web de Bot Framework en Azure, es posible que deba iniciar sesión varias veces antes de que la autenticación se establezca correctamente.

## <a name="install-and-test-the-bot-in-teams"></a>Instalar y probar el bot en Teams

1. En el proyecto de bot, asegúrese de que la `TeamsAppManifest` carpeta contiene la `manifest.json` junto con un `outline.png` y `color.png` los archivos.
1. En el Explorador de soluciones, vaya a la `TeamsAppManifest` carpeta. Para `manifest.json` editar, asigne los siguientes valores:
    1. Asegúrese de que **el identificador de aplicación del bot** que recibió en el momento del registro del bot está asignado y `id` `botId`.
    1. Asigne este valor: `validDomains: [ "token.botframework.com" ]`.
1. Seleccione y **zip** los `manifest.json`archivos , `outline.png`y `color.png` .
1. Abra **Microsoft Teams**.
1. En el panel izquierdo, en la parte inferior, selecciona el **icono Aplicaciones**.
1. En el panel derecho, en la parte inferior, **selecciona Upload una aplicación personalizada**.
1. Vaya a la carpeta `TeamsAppManifest` y cargue el manifiesto comprimido.
Se muestra el siguiente asistente:

    ![Carga de equipos de bots de autenticación](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. Seleccione el botón **Agregar a un equipo**.
1. En la siguiente ventana, seleccione el equipo donde desea usar el bot.
1. Seleccione el **botón Configurar un bot** .
1. Seleccione los tres puntos (&#x25cf;&#x25cf;&#x25cf;) en el panel izquierdo. A continuación, **selecciona el icono de App Studio** .
1. Seleccione la **pestaña Editor de manifiestos** . Debería ver el icono del bot que ha cargado.
1. Además, deberías poder ver el bot como un contacto en la lista de chat que puedes usar para intercambiar mensajes con el bot.

### <a name="testing-the-bot-locally-in-teams"></a>Probar el bot localmente en Teams

Microsoft Teams es un producto totalmente basado en la nube, requiere que todos los servicios a los que tiene acceso estén disponibles desde la nube mediante puntos de conexión HTTPS. Por lo tanto, para permitir que el bot (nuestro ejemplo) funcione en Teams, debe publicar el código en la nube de su elección o hacer que una instancia en ejecución local sea accesible externamente a través de una herramienta  de túnel. Se recomienda  [ngrok](https://ngrok.com/download), que crea una dirección URL direccionable externamente para un puerto que se abre localmente en el equipo.
Para configurar ngrok en preparación para ejecutar la aplicación Microsoft Teams localmente, siga estos pasos:

1. En una ventana de terminal, vaya al directorio donde ha `ngrok.exe` instalado. Se recomienda establecer la *ruta de acceso de la variable* de entorno para que apunte a ella.
1. Ejecute, por ejemplo, `ngrok http 3978 --host-header=localhost:3978`. Reemplace el número de puerto según sea necesario.
Esto inicia ngrok para escuchar en el puerto especificado. A cambio, le proporciona una dirección URL direccionable externamente, válida durante el tiempo que ngrok se esté ejecutando. La siguiente imagen es un ejemplo:

    ![cadena de conexión de la aplicación bot de teams adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG).

1. Copie la dirección HTTPS de reenvío. Debe ser similar a lo siguiente: `https://dea822bf.ngrok.io/`.
1. Anexar `/api/messages` para obtener `https://dea822bf.ngrok.io/api/messages`. Este es el extremo **de mensajes** para el bot que se ejecuta localmente en el equipo y al que se puede acceder a través de la web en un chat en Microsoft Teams.
1. Un último paso para realizar es actualizar el extremo de mensajes del bot implementado. En el ejemplo, implementamos el bot en Azure. Así que vamos a realizar estos pasos:
    1. En el explorador, vaya al [**portal de Microsoft Azure navegación**][azure-portal].
    1. Seleccione el **registro del bot**.
    1. En el panel izquierdo, seleccione **Configuración**.
    1. En el panel derecho, en el cuadro **Extremo** de mensajería, escriba la dirección URL de ngrok, en nuestro ejemplo, `https://dea822bf.ngrok.io/api/messages`.
1. Inicie el bot localmente, por ejemplo, en Visual Studio modo de depuración.
1. Pruebe el bot mientras se ejecuta localmente con el chat web **de** prueba del portal de Bot Framework. Al igual que Emulator, esta prueba no permite tener acceso a Teams funcionalidad específica.
1. En la ventana de terminal donde `ngrok` se ejecuta puede ver el tráfico HTTP entre el bot y el cliente de chat web. Si desea una vista más detallada, en una ventana del explorador escriba `http://127.0.0.1:4040` que obtuvo de la ventana de terminal anterior. La siguiente imagen es un ejemplo:

    ![Pruebas de auth bot teams ngrok](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png).

> [!NOTE]
> Si detiene y reinicia ngrok, la dirección URL cambia. Para usar ngrok en el proyecto y según las capacidades que use, debe actualizar todas las referencias de dirección URL.
 

## <a name="additional-information"></a>Información adicional

### <a name="teamsappmanifestmanifestjson"></a>TeamsAppManifest/manifest.json

Este manifiesto contiene la información necesaria Microsoft Teams para conectarse con el bot:  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "",
  "packageName": "com.teams.auth.bot",
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

Con la autenticación, Teams se comporta de forma ligeramente diferente que otros canales, como se explica a continuación.

### <a name="handling-invoke-activity"></a>Controlar actividad de invocación

Se **envía una actividad Invoke** al bot en lugar de a la actividad de evento usada por otros canales.
Para ello, se subclase **ActivityHandler**.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-sample)

**Bots/DialogBot.cs**

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

**Bots/TeamsBot.cs**

La *actividad Invoke* debe reenviarse al cuadro de diálogo si **se usa OAuthPrompt** .

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

La *actividad Invoke* debe reenviarse al cuadro de diálogo si **se usa OAuthPrompt** .

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

**cuadros de diálogo/mainDialog.js**

En un paso de cuadro de diálogo, use `beginDialog` para iniciar el mensaje de OAuth, que pide al usuario que inicie sesión.

- Si el usuario ya ha iniciado sesión, se generará un evento de respuesta de token, sin preguntar al usuario.
- De lo contrario, se pedirá al usuario que inicie sesión. El Servicio de bots de Azure envía el evento de respuesta de token después de que el usuario intente iniciar sesión.

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

En el siguiente paso de diálogo, compruebe la presencia de un token en el resultado del paso anterior. Si no es null, el usuario ha iniciado sesión correctamente.

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

**bots/logoutDialog.js**

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[Python](#tab/python-sample)

**bots/dialog_bot.py**

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

**bots/teams_bot.py**

La *actividad Invoke* debe reenviarse al cuadro de diálogo si **se usa OAuthPrompt** .

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

**dialogs/main_dialog.py**

En un paso de cuadro de diálogo, use `begin_dialog` para iniciar el mensaje de OAuth, que pide al usuario que inicie sesión.

- Si el usuario ya ha iniciado sesión, se generará un evento de respuesta de token, sin preguntar al usuario.
- De lo contrario, se pedirá al usuario que inicie sesión. El Servicio de bots de Azure envía el evento de respuesta de token después de que el usuario intente iniciar sesión.

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

En el siguiente paso de diálogo, compruebe la presencia de un token en el resultado del paso anterior. Si no es null, el usuario ha iniciado sesión correctamente.

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

**dialogs/logout_dialog.py**

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="see-also"></a>Vea también

[Agregar autenticación a través del servicio bot de Azure](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: /azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: /azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: /azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: /azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
