---
title: Agregue autenticación al bot de Teams
author: clearab
description: Cómo agregar autenticación OAuth a un bot en Microsoft Teams.
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 36cb6f3de6f97af1d01512175923b79f69f630ad
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566005"
---
# <a name="add-authentication-to-your-teams-bot"></a>Agregue autenticación al bot de Teams

Hay ocasiones en las que es posible que deba crear bots en Microsoft Teams que puedan tener acceso a recursos en nombre del usuario, como un servicio de correo.

En este artículo se muestra cómo usar la autenticación del SDK de Azure Bot Service v4, basada en OAuth 2.0. Esto facilita el desarrollo de un bot que puede usar tokens de autenticación basados en las credenciales del usuario. La clave en todo esto es el uso de proveedores de **identidades,** como veremos más adelante.

OAuth 2.0 es un estándar abierto para la autenticación y autorización usado por Azure Active Directory (Azure AD) y otros muchos proveedores de identidad. Una comprensión básica de OAuth 2.0 es un requisito previo para trabajar con autenticación en Teams.

Consulte [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) para obtener una comprensión básica y [OAuth 2.0](https://oauth.net/2/) para obtener la especificación completa.

Para obtener más información acerca de cómo Azure Bot Service controla la autenticación, consulte [Autenticación de usuario dentro de una conversación.](https://aka.ms/azure-bot-authentication)

En este artículo, aprenderá lo siguiente:

- **Cómo crear un bot habilitado para autenticación.** Usará [cs-auth-sample][teams-auth-bot-cs] para controlar las credenciales de inicio de sesión del usuario y la generación del token de autenticación.
- **Cómo implementar el bot en Azure y asociarlo a un proveedor de identidades.** El proveedor emite un token basado en credenciales de inicio de sesión de usuario. El bot puede usar el token para tener acceso a recursos, como un servicio de correo, que requieren autenticación. Para obtener más información, consulte [flujo de autenticación Microsoft Teams para bots.](auth-flow-bot.md)
- **Cómo integrar el bot dentro de Microsoft Teams**. Una vez integrado el bot, puede iniciar sesión e intercambiar mensajes con él en un chat.

## <a name="prerequisites"></a>Requisitos previos

- Conocimiento de los conceptos básicos del [bot,][concept-basics] [la administración del estado,][concept-state]la [biblioteca de cuadros de diálogo][concept-dialogs]y cómo implementar el flujo [secuencial de conversaciones.][simple-dialog]
- Conocimiento del desarrollo de Azure y OAuth 2.0.
- Las versiones actuales de Visual Studio y Git.
- Cuenta de Azure. Si es necesario, puede crear una [cuenta gratuita de Azure.](https://azure.microsoft.com/free/)
- La siguiente muestra:

    | Muestra | Versión de BotBuilder | Demuestra |
    |:---|:---:|:---|
    | **Autenticación de bots** en [cs-auth-sample][teams-auth-bot-cs] | v4 | Soporte de OAuthCard |
    | **Autenticación de bots** en [js-auth-sample][teams-auth-bot-js] | v4| Soporte de OAuthCard  |
    | **Autenticación de bots** en [py-auth-sample][teams-auth-bot-py] | v4 | Soporte de OAuthCard |

## <a name="create-the-resource-group"></a>Crear el grupo de recursos

El grupo de recursos y el plan de servicio no son estrictamente necesarios, pero le permiten liberar convenientemente los recursos que cree. Esta es una buena práctica para mantener sus recursos organizados y manejables.

Utilice un grupo de recursos para crear recursos individuales para Bot Framework. Para el rendimiento, asegúrese de que estos recursos se encuentran en la misma región de Azure.

1. En el explorador, inicie sesión en [**Azure Portal.**][azure-portal]
1. En el panel de navegación izquierdo, seleccione **Grupos de recursos**.
1. En la parte superior izquierda de la ventana mostrada, seleccione **agregar** ficha para crear un nuevo grupo de recursos. Se le pedirá que proporcione lo siguiente:
    1. **Suscripción**. Use su suscripción existente.
    1. **Grupo de recursos**. Escriba el nombre del grupo de recursos. Un ejemplo podría ser  *TeamsResourceGroup*. Recuerde que el nombre debe ser único.
    1. En el menú desplegable **Región,** seleccione *Ee. UU. occidental* o una región cercana a las aplicaciones.
    1. Seleccione el botón **Revisar y crear.** Debería ver un banner que lee *Validación pasada.*
    1. Seleccione el botón **Crear.** Puede tardar unos minutos en crear el grupo de recursos.

> [!TIP]
> Al igual que con los recursos que creará más adelante en este tutorial, es una buena idea anclar este grupo de recursos al panel para facilitar el acceso. Si desea hacerlo, seleccione el icono de pin &#128204; en la parte superior derecha del panel.

## <a name="create-the-service-plan"></a>Crear el plan de servicio

1. En [**Azure Portal**][azure-portal], en el panel de navegación izquierdo, seleccione **Crear un recurso**.
1. En el cuadro de búsqueda, escriba *Plan de App Service*. Seleccione la tarjeta Plan de **App Service** en los resultados de búsqueda.
1. Seleccione **Crear**.
1. Se le pedirá que proporcione la siguiente información:
    1. **Suscripción**. Puede usar una suscripción existente.
    1. **Grupo de recursos**. Seleccione el grupo que creó anteriormente.
    1. **Nombre**. Escriba el nombre del plan de servicio. Un ejemplo podría ser  *TeamsServicePlan*. Recuerde que el nombre debe ser único, dentro del grupo.
    1. **Sistema operativo**. Seleccione *Windows* o su sistema operativo aplicable.
    1. **Región**. Seleccione *Oeste de EE. UU.* o una región cercana a las aplicaciones.
    1. **Nivel de precios**. Asegúrese de que *el estándar S1* está seleccionado. Este debe ser el valor predeterminado.
    1. Seleccione el botón **Revisar y crear.** Debería ver un banner que lee *Validación pasada.*
    1. Seleccione **Crear**. Puede tardar unos minutos en crear el plan de servicio de aplicaciones. El plan aparecerá en el grupo de recursos.

## <a name="create-the-bot-channels-registration"></a>Cree el registro de canales de bot

El registro de canales de bot registra el servicio web como un bot con Bot Framework, siempre que tenga un identificador de aplicación de Microsoft y una contraseña de aplicación (secreto de cliente).

> [!IMPORTANT]
> Solo debe registrar el bot si no está hospedado en Azure. Si [creó un bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) a través de Azure Portal, ya está registrado con el servicio. Si creó el bot a través de [Bot Framework](https://dev.botframework.com/bots/new) o [AppStudio,](~/concepts/build-and-test/app-studio-overview.md) el bot no está registrado en Azure.

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> El recurso Registro de canales de bot mostrará la región **Global** incluso si seleccionó Oeste de EE. UU. Esto se espera.

Para obtener más información, consulte [Crear un bot para Teams](../create-a-bot-for-teams.md).

## <a name="create-the-identity-provider"></a>Crear el proveedor de identidades

Necesita un proveedor de identidades que se pueda usar para la autenticación.
En este procedimiento usará un proveedor de Azure AD; también se pueden usar otros proveedores de identidades compatibles con Azure AD.

1. En [**Azure Portal**][azure-portal], en el panel de navegación izquierdo, seleccione **Azure Active Directory**.
    > [!TIP]
    > Deberá crear y registrar este recurso de Azure AD en un inquilino en el que puede dar su consentimiento para delegar los permisos solicitados por una aplicación.
    > Para obtener instrucciones sobre cómo crear un inquilino, consulte [Acceso al portal y crear un inquilino](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).
1. En el panel izquierdo, seleccione **Registros de aplicaciones**.
1. En el panel derecho, seleccione la pestaña **Nuevo registro,** en la parte superior izquierda.
1. Se le pedirá que proporcione la siguiente información:
   1. **Nombre**. Escriba el nombre de la aplicación. Un ejemplo podría ser  *BotTeamsIdentity*. Recuerde que el nombre debe ser único.
   1. Seleccione los **tipos de cuenta compatibles** para la aplicación. Seleccione *Cuentas en cualquier directorio de organización (cualquier directorio de Azure AD - Multitenant) y cuentas personales de Microsoft (por ejemplo, Skype, Xbox).*
   1. Para el **URI de redirección**:<br/>
       &#x2713;Seleccione **Web**. <br/>
       &#x2713; Establezca la dirección URL en `https://token.botframework.com/.auth/web/redirect` .
   1. Seleccione **Registrar**.

1. Una vez creado, Azure muestra la página **Información general de** la aplicación. Copie y guarde la siguiente información en un archivo:

    1. El valor **del IDENTIFICADOR de aplicación (cliente).** Usará este valor más adelante como *identificador de cliente* al registrar esta aplicación de identidad de Azure con el bot.
    1. El valor **de identificador directorio (inquilino).** También usará este valor más adelante como *identificador de inquilino* para registrar esta aplicación de identidad de Azure con el bot.

1. En el panel izquierdo, seleccione **Certificados & secretos** para crear un secreto de cliente para la aplicación.

   1. En **Secretos de cliente**, seleccione &#x2795; Nuevo secreto de **cliente**.
   1. Agregue una descripción para identificar este secreto de otras personas que podría necesitar crear para esta aplicación, como *bot identity app en Teams*.
   1. Establezca **Expiraciones** en la selección.
   1. Seleccione **Agregar**.
   1. Antes de salir de esta página, **registre el secreto.** Usará este valor más adelante como _secreto de cliente_ al registrar la aplicación de Azure AD con el bot.

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a>Configure la conexión del proveedor de identidades y regístrela con el bot

Tenga en cuenta que hay dos opciones para proveedores de servicios aquí-Azure AD V1 y Azure AD V2.  Las diferencias entre los dos proveedores se resumen [aquí,](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)pero en general, V2 proporciona más flexibilidad con respecto a los permisos de bot cambiantes.  Graph Los permisos de API se enumeran en el campo ámbitos y, a medida que se agregan otros nuevos, los bots permitirán a los usuarios dar su consentimiento para los nuevos permisos en el siguiente inicio de sesión.  Para V1, el usuario debe eliminar el consentimiento del bot para que se soliciten nuevos permisos en el cuadro de diálogo OAuth. 

#### <a name="azure-ad-v1"></a>Azure AD V1

1. En [**Azure Portal,**][azure-portal]seleccione el grupo de recursos en el panel.
1. Seleccione el vínculo de registro del canal del bot.
1. Abra la página de recursos y seleccione **Configuración** en **Configuración**. 
1. Seleccione **Agregar Configuración de conexión de OAuth**.    
La siguiente imagen muestra la selección correspondiente en la página de recursos:  
![Configuración de SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)
1. Complete el formulario de la siguiente manera:

    1. **Nombre**. Escriba un nombre para la conexión. Usará este nombre en el bot del `appsettings.json` archivo. Por ejemplo *BotTeamsAuthADv1*.
    1. **Proveedor de servicios**. Seleccione **Azure Active Directory**. Una vez seleccionado esto, se mostrarán los campos específicos de Azure AD.
    1. **Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.
    1. **Secreto de cliente**. Escriba el secreto que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.
    1. **Tipo de concesión**. Escriba `authorization_code` .
    1. **URL de inicio de sesión**. Escriba `https://login.microsoftonline.com` .
    1. **Identificador de inquilino**, escriba el **identificador de directorio (inquilino)** que registró anteriormente para la aplicación de identidad de Azure o **común** en función del tipo de cuenta admitido seleccionado al crear la aplicación del proveedor de identidades. Para decidir qué valor asignar sigue estos criterios:

        - Si seleccionó *Solo cuentas en este directorio de organización (solo Microsoft - inquilino único)* o Cuentas en cualquier directorio de organización *(directorio de Microsoft AAD - Multi tenant)* escriba el identificador de **inquilino** que registró anteriormente para la aplicación AAD. Este será el inquilino asociado a los usuarios que se pueden autenticar.

        - Si seleccionó *Cuentas en cualquier directorio de organización (cualquier directorio AAD : cuentas de Microsoft multiinquilino y personales, por ejemplo, Skype, Xbox, Outlook)* escriba la palabra **común** en lugar de un identificador de inquilino. De lo contrario, la aplicación AAD comprobará a través del inquilino cuyo identificador se seleccionó y excluirá las cuentas personales de Microsoft.

    h. En **Dirección URL de recurso**, escriba `https://graph.microsoft.com/` . Esto no se utiliza en el ejemplo de código actual.  
    i. Deje **los ámbitos** en blanco. La siguiente imagen es un ejemplo:

    ![equipos bots aplicación auth cadena de conexión adv1 vista](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. Seleccione **Guardar**.

#### <a name="azure-ad-v2"></a>Azure AD V2

1. En [**Azure Portal,**][azure-portal]seleccione el grupo de recursos en el panel.
1. Seleccione el vínculo de registro del canal del bot.
1. Abra la página de recursos y seleccione **Configuración** en **Configuración**. 
1. Seleccione **Agregar Configuración de conexión de OAuth**.  
La siguiente imagen muestra la selección correspondiente en la página de recursos:        
![Configuración de SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png) 

1. Complete el formulario de la siguiente manera:

    1. **Nombre**. Escriba un nombre para la conexión. Usará este nombre en el bot del `appsettings.json` archivo. Por ejemplo *BotTeamsAuthADv2*.
    1. **Proveedor de servicios**. Seleccione **Azure Active Directory v2**. Una vez seleccionado esto, se mostrarán los campos específicos de Azure AD.
    1. **Id. de cliente**. Escriba el identificador de aplicación (cliente) que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.
    1. **Secreto de cliente**. Escriba el secreto que registró para la aplicación del proveedor de identidades de Azure en los pasos anteriores.
    1. **Url de Exchange de tokens**. Deja esto en blanco.
    1. **Identificador de inquilino**, escriba el **identificador de directorio (inquilino)** que registró anteriormente para la aplicación de identidad de Azure o **común** en función del tipo de cuenta admitido seleccionado al crear la aplicación del proveedor de identidades. Para decidir qué valor asignar sigue estos criterios:

        - Si seleccionó *Solo cuentas en este directorio de organización (solo Microsoft - inquilino único)* o Cuentas en cualquier directorio de organización *(directorio de Microsoft AAD - Multi tenant)* escriba el identificador de **inquilino** que registró anteriormente para la aplicación AAD. Este será el inquilino asociado a los usuarios que se pueden autenticar.

        - Si seleccionó *Cuentas en cualquier directorio de organización (cualquier directorio AAD : cuentas de Microsoft multiinquilino y personales, por ejemplo, Skype, Xbox, Outlook)* escriba la palabra **común** en lugar de un identificador de inquilino. De lo contrario, la aplicación AAD comprobará a través del inquilino cuyo identificador se seleccionó y excluirá las cuentas personales de Microsoft.

    1. En **Scopes**, escriba una lista delimitada por espacio de permisos de gráfico que esta aplicación requiere, por ejemplo: User.Read User.ReadBasic.All Mail.Read 

1. Seleccione **Guardar**.

### <a name="test-the-connection"></a>Probar la conexión

1. Seleccione la entrada de conexión para abrir la conexión que acaba de crear.
1. Seleccione **Probar conexión** en la parte superior del panel Configuración de conexión del proveedor **de** servicios.
1. La primera vez que lo hagas abrirá una nueva ventana del navegador pidiéndote que selecciones una cuenta. Seleccione el que desea utilizar.
1. A continuación, se le pedirá que permita al proveedor de identidades usar los datos (credenciales). La siguiente imagen es un ejemplo:

    ![equipos bot auth cadena de conexión adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. Seleccione **Aceptar**.
1. A continuación, esto debe redirigir a una conexión de prueba a la página **\<your-connection-name> correcta.** Actualice la página si recibe un error. La siguiente imagen es un ejemplo:

    ![equipos bots aplicación auth conexión str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

El código de bot usa el nombre de conexión para recuperar tokens de autenticación de usuario.

## <a name="prepare-the-bot-sample-code"></a>Prepare el código de ejemplo del bot

Con la configuración preliminar realizada, vamos a centrarnos en la creación del bot para usar en este artículo.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

1. Clonar [cs-auth-sample][teams-auth-bot-cs].
1. Inicie Visual Studio.
1. En la barra de herramientas, seleccione **Archivo -> Abrir -> Project/Solución** y abra el proyecto de bot.
1. En C# Update **appsettings.jsactivado** de la siguiente manera:

    - Estad en `ConnectionName` el nombre de la conexión del proveedor de identidades que agregó al registro del canal del bot. El nombre que usamos en este ejemplo es *BotTeamsAuthADv1*.
    - Estad en `MicrosoftAppId` el **id.**
    - Establezca `MicrosoftAppPassword` en el secreto de **cliente** que guardó en el momento del registro del canal del bot.

    Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña. Por ejemplo, cualquier amperaciones (&) deberá codificarse como `&amp;` .

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. En el Explorador de soluciones, vaya a la `TeamsAppManifest` carpeta, abra `manifest.json` y establezca y en el identificador de aplicación del `id` `botId` **bot** que guardó en el momento del registro del canal del bot.

# <a name="javascript"></a>[JavaScript](#tab/node-js)

1. Clonar [node-auth-sample][teams-auth-bot-js].
1. En una consola, vaya al proyecto: </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. Instalar módulos</br></br>
`npm install`
1. Actualice la configuración **.env** de la siguiente manera:

    - Estad en `MicrosoftAppId` el **id.**
    - Establezca `MicrosoftAppPassword` en el secreto de **cliente** que guardó en el momento del registro del canal del bot.
    - Establezca el `connectionName` nombre de la conexión del proveedor de identidades.
    Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña. Por ejemplo, cualquier amperaciones (&) deberá codificarse como `&amp;` .

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. En la `teamsAppManifest` carpeta, abra `manifest.json` y establezca en el IDENTIFICADOR de la aplicación de `id` **Microsoft** y en el identificador de aplicación `botId` del **bot** que guardó en el momento del registro del canal del bot.

# <a name="python"></a>[Python](#tab/python)

1. Clone [py-auth-sample][teams-auth-bot-py] desde el repositorio de github.
1. Actualizar **config.py**:

    - Estadúrle `ConnectionName` en el nombre de la configuración de conexión de OAuth que agregó al bot.
    - Establece `MicrosoftAppId` y en el ID de aplicación y el secreto de la aplicación del `MicrosoftAppPassword` bot.

      Dependiendo de los caracteres del secreto del bot, es posible que deba escapar de la contraseña. Por ejemplo, cualquier amperaciones (&) deberá codificarse como `&amp;` .

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a>Implementar el bot en Azure

Para implementar el bot, siga los pasos descritos en cómo [implementar el bot en Azure](https://aka.ms/azure-bot-deployment-cli).

Como alternativa, mientras está en Visual Studio, puede seguir estos pasos:

1. En Visual Studio *Explorador de soluciones,* seleccione y mantenga pulsado (o haga clic con el botón derecho) el nombre del proyecto.
1. En el menú desplegable, seleccione **Publicar**.
1. En la ventana mostrada, seleccione el vínculo **Nuevo.**
1. En la ventana de diálogo, seleccione **App Service** a la izquierda y **Crear nuevo** a la derecha.
1. Seleccione el botón **Publicar.**
1. En la siguiente ventana de diálogo, escriba la información necesaria. A continuación puede ver un ejemplo:

    ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. Seleccione **Crear**.
1. Si la implementación se completa correctamente, debería verlo reflejado en Visual Studio. Por otra parte, se muestra una página en su navegador predeterminado diciendo *Su bot está listo!*. La URL será similar a esto: `https://botteamsauth.azurewebsites.net/` . Guárdelo en un archivo.
1. En el explorador, vaya a [**Azure Portal**][azure-portal].
1. Compruebe el grupo de recursos, el bot debe aparecer junto con los demás recursos. La siguiente imagen es un ejemplo:

    ![equipos-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. En el grupo de recursos, seleccione el nombre de registro del canal bot (vínculo).
1. En el panel izquierdo, seleccione **Configuración**.
1. En el cuadro **Punto de conexión mensajería,** escriba la dirección URL obtenida anteriormente seguida de `api/messages` . Este es un ejemplo: `https://botteamsauth.azurewebsites.net/api/messages` .
1. Seleccione el botón **Guardar** en la parte superior izquierda.

## <a name="test-the-bot-using-the-emulator"></a>Pruebe el bot usando el emulador

Si aún no lo ha hecho, instale el [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme). Vea también [Depurar con el emulador](https://aka.ms/bot-framework-emulator-debug-with-emulator).

Para que el inicio de sesión del ejemplo del bot funcione usted debe configurar el emulador.

### <a name="configure-the-emulator-for-authentication"></a>Configure el emulador para la autenticación

Si un bot requiere autenticación, debe configurar el emulador. Para configurar:

1. Inicie el emulador.
1. En el emulador, seleccione el icono de engranaje &#9881; en la parte inferior izquierda, o la pestaña **Emulador Configuración** en la parte superior derecha.
1. Marque la casilla Por **usar tokens de autenticación de la versión 1.0**.
1. Introduzca la ruta local a la herramienta **ngrok.** *Consulte* la Bot Framework Emulator / ngrok integración de [túneles Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)). Para obtener más información sobre herramientas, consulte [ngrok](https://ngrok.com/).
1. Marque la casilla Por **Ejecutar ngrok cuando se inicie el emulador**.
1. Seleccione el botón **Guardar.**

Cuando el bot muestra una tarjeta de inicio de sesión y el usuario selecciona el botón de inicio de sesión, el emulador abre una página que el usuario puede usar para iniciar sesión con el proveedor de autenticación.
Una vez que el usuario lo hace, el proveedor genera un token de usuario y lo envía al bot. Después de eso, el bot puede actuar en nombre del usuario.

### <a name="test-the-bot-locally"></a>Pruebe el bot localmente

Después de configurar el mecanismo de autenticación, puede realizar las pruebas de bot reales.  

1. Ejecute el ejemplo de bot localmente en el equipo, a través de Visual Studio por ejemplo.
1. Inicie el emulador.
1. Seleccione el botón **Abrir bot.**
1. En la DIRECCIÓN URL del **bot,** escriba la dirección URL local del bot. Por lo general, `http://localhost:3978/api/messages` .
1. En el **IDENTIFICADOR de aplicación de Microsoft,** escriba el identificador de aplicación del bot desde `appsettings.json` .
1. En la contraseña de la **aplicación de Microsoft,** escriba la contraseña de la aplicación del bot desde `appsettings.json` el archivo .
1. Seleccione **Conectar**.
1. Después de que el bot esté en funcionamiento, escriba cualquier texto para mostrar la tarjeta de inicio de sesión.
1. Seleccione el botón **Iniciar sesión.**
1. Se muestra un cuadro de diálogo emergente para **confirmar la URL abierta.** Esto es para permitir que el usuario del bot (usted) sea autenticado.  
1. Seleccione **Confirmar**.
1. Si se le solicita, seleccione la cuenta del usuario aplicable.
1. Dependiendo de la configuración que haya utilizado para el emulador, obtendrá una de las siguientes opciones:
    1. **Uso del código de verificación de inicio de sesión**  
      &#x2713; Se abre una ventana que muestra el código de validación.  
      &#x2713; Copiar e introduzca el código de validación en el cuadro de chat para completar el inicio de sesión.
    1. **Uso de tokens de autenticación**.  
      &#x2713; Ha iniciado sesión en función de sus credenciales.

    La siguiente imagen es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:

    ![emulador de inicio de sesión de bot auth](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. Si selecciona **Sí** cuando el bot le pregunta *¿Desea ver el token?*, obtendrá una respuesta similar a la siguiente:

    ![Token de emulador de inicio de sesión de bot de autenticación](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. Escriba **cerrar sesión** en el cuadro de chat de entrada para cerrar sesión. Esto libera el token de usuario y el bot no podrá actuar en su nombre hasta que vuelva a iniciar sesión.

> [!NOTE]
> La autenticación de bots requiere el uso del **servicio bot connector**. El servicio tiene acceso a la información de registro de canales de bot para el bot.

## <a name="test-the-deployed-bot"></a>Pruebe el bot implementado

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. En el explorador, vaya a [**Azure Portal**][azure-portal].
1. Busque el grupo de recursos.
1. Seleccione el vínculo de recursos. Se muestra la página de recursos.
1. En la página de recursos, seleccione **Probar en chat web**. El bot se inicia y muestra los saludos predefinidos.
1. Escriba cualquier cosa en el cuadro de chat.
1. Seleccione el cuadro **Iniciar sesión.**
1. Se muestra un cuadro de diálogo emergente para **confirmar la URL abierta.** Esto es para permitir que el usuario del bot (usted) sea autenticado.  
1. Seleccione **Confirmar**.
1. Si se le solicita, seleccione la cuenta del usuario aplicable.
    La siguiente imagen es un ejemplo de la interfaz de usuario del bot después de haber iniciado sesión:

    ![inicio de sesión del bot de autenticación implementado](../../../assets/images/authentication/auth-bot-login-deployed.PNG).

1. Seleccione el botón **Sí** para mostrar el token de autenticación. La siguiente imagen es un ejemplo:

    ![Token implementado de inicio de sesión del bot de autenticación](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG).

1. Escriba cerrar sesión para cerrar sesión.

    ![auth bot desplegado cierre de sesión](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> Si tiene problemas para iniciar sesión, intente probar la conexión de nuevo como se describe en los pasos anteriores. Esto podría volver a crear el token de autenticación.
> Con el cliente de Bot Framework Web Chat en Azure, es posible que deba iniciar sesión varias veces antes de que la autenticación se establezca correctamente.

## <a name="install-and-test-the-bot-in-teams"></a>Instale y pruebe el bot en Teams

1. En el proyecto de bot, asegúrese de que la `TeamsAppManifest` carpeta contiene el junto con un archivo `manifest.json` `outline.png` `color.png` y.
1. En el Explorador de soluciones, vaya a la `TeamsAppManifest` carpeta. Edite `manifest.json` asignando los siguientes valores:
    1. Asegúrese de que el **ID de aplicación** del bot que recibió en el momento del registro del canal del bot está asignado y `id` `botId` .
    1. Asigne este valor: `validDomains: [ "token.botframework.com" ]` .
1. Seleccione y **comprima** los `manifest.json` archivos y `outline.png` `color.png` archivos.
1. Abra **Microsoft Teams**.
1. En el panel izquierdo, en la parte inferior, seleccione el **icono Aplicaciones**.
1. En el panel derecho, en la parte inferior, seleccione **Upload una aplicación personalizada.**
1. Vaya a la `TeamsAppManifest` carpeta y cargue el manifiesto comprimido.
Se muestra el siguiente asistente:

    ![auth equipos de bots cargar](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. Seleccione el botón **Agregar a un equipo**.
1. En la siguiente ventana, seleccione el equipo donde desea utilizar el bot.
1. Seleccione el botón **Configurar un bot.**
1. Seleccione los tres puntos (&#x25cf;&#x25cf;&#x25cf;) en el panel izquierdo. A continuación, seleccione el icono **de App Studio.**
1. Seleccione la pestaña **Editor de manifiestos.** Debería ver el icono del bot que ha cargado.
1. Además, debería poder ver el bot que aparece como un contacto en la lista de chat que puede usar para intercambiar mensajes con el bot.

### <a name="testing-the-bot-locally-in-teams"></a>Probar el bot localmente en Teams

Microsoft Teams es un producto completamente basado en la nube, requiere que todos los servicios a los que accede estén disponibles desde la nube mediante puntos de conexión HTTPS. Por lo tanto, para permitir que el bot (nuestro ejemplo) funcione en Teams, debe publicar el código en la nube de su elección o hacer que una instancia de ejecución local sea accesible externamente a través de una herramienta **de tunelización.** Se recomienda  [ngrok](https://ngrok.com/download), que crea una dirección URL direccionable externamente para un puerto que se abre localmente en el equipo.
Para configurar ngrok en preparación para ejecutar la aplicación Microsoft Teams localmente, siga estos pasos:

1. En una ventana de terminal, vaya al directorio donde ha `ngrok.exe` instalado. Sugerimos establecer la ruta de acceso *de la variable* de entorno para que apunte a ella.
1. Ejecute, por ejemplo, `ngrok http 3978 --host-header=localhost:3978` . Reemplace el número de puerto según sea necesario.
Esto inicia ngrok para escuchar en el puerto que especifique. A cambio, le proporciona una dirección URL direccionable externamente, válida durante el tiempo que ngrok se esté ejecutando. La siguiente imagen es un ejemplo:

    ![equipos bot app auth cadena de conexión adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG).

1. Copie la dirección HTTPS de reenvío. Debe ser similar a lo siguiente: `https://dea822bf.ngrok.io/` .
1. `/api/messages`Anexar para obtener `https://dea822bf.ngrok.io/api/messages` . Este es el **punto de conexión de mensajes** para el bot que se ejecuta localmente en el equipo y accesible a través de la web en un chat en Microsoft Teams.
1. Un último paso a realizar es actualizar el punto de conexión de mensajes del bot implementado. En el ejemplo, implementamos el bot en Azure. Así que vamos a realizar estos pasos:
    1. En el explorador, vaya a [**Azure Portal**][azure-portal].
    1. Seleccione el **registro del canal de bot.**
    1. En el panel izquierdo, seleccione **Configuración**.
    1. En el panel derecho, en el cuadro **Punto de conexión mensajería,** escriba la dirección URL de ngrok, en nuestro ejemplo, `https://dea822bf.ngrok.io/api/messages` .
1. Inicie el bot localmente, por ejemplo en Visual Studio modo de depuración.
1. Pruebe el bot mientras se ejecuta localmente mediante el **chat web** de prueba del portal de Bot Framework. Al igual que el emulador, esta prueba no le permite acceder a Teams funcionalidad específica.
1. En la ventana del terminal donde `ngrok` se está ejecutando puede ver el tráfico HTTP entre el bot y el cliente de chat web. Si desea una vista más detallada, en una ventana del navegador introduzca `http://127.0.0.1:4040` la obtenida de la ventana de terminal anterior. La siguiente imagen es un ejemplo:

    ![auth bot teams ngrok pruebas](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png).

> [!NOTE]
> Si detiene y reinicia ngrok, la dirección URL cambia. Para usar ngrok en el proyecto y, en función de las capacidades que esté utilizando, debe actualizar todas las referencias de DIRECCIÓN URL.
 

## <a name="additional-information"></a>Información adicional

### <a name="teamsappmanifestmanifestjson"></a>TeamsAppManifest/manifest.jsen

Este manifiesto contiene la información necesaria por Microsoft Teams para conectarse con el bot:  

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

Con la autenticación, Teams se comporta ligeramente diferente que otros canales, como se explica a continuación.

### <a name="handling-invoke-activity"></a>Manejo de la actividad de invocación

Una **actividad de invocación** se envía al bot en lugar de la actividad de eventos utilizada por otros canales.
Esto se hace subclasificando el **ActivityHandler**.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-sample)

**Bots/DialogBot.cs**

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

**Bots/TeamsBot.cs**

La *actividad invoke* debe reenviarse al cuadro de diálogo si se utiliza **OAuthPrompt.**

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

La *actividad invoke* debe reenviarse al cuadro de diálogo si se utiliza **OAuthPrompt.**

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

**diálogos/mainDialog.js**

Dentro de un paso de diálogo, use `beginDialog` para iniciar el símbolo del sistema OAuth, que pide al usuario que inicie sesión.

- Si el usuario ya ha iniciado sesión, esto generará un evento de respuesta de token, sin preguntar al usuario.
- De lo contrario, esto pedirá al usuario que inicie sesión. Azure Bot Service envía el evento de respuesta de token después de que el usuario intente iniciar sesión.

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

En el siguiente paso de diálogo, compruebe la presencia de un token en el resultado del paso anterior. Si no es null, el usuario ha iniciado sesión correctamente.

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

**bots/logoutDialog.js**

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[Python](#tab/python-sample)

**bots/dialog_bot.py**

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

**bots/teams_bot.py**

La *actividad invoke* debe reenviarse al cuadro de diálogo si se utiliza **OAuthPrompt.**

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

**diálogos/main_dialog.py**

Dentro de un paso de diálogo, use `begin_dialog` para iniciar el símbolo del sistema OAuth, que pide al usuario que inicie sesión.

- Si el usuario ya ha iniciado sesión, esto generará un evento de respuesta de token, sin preguntar al usuario.
- De lo contrario, esto pedirá al usuario que inicie sesión. Azure Bot Service envía el evento de respuesta de token después de que el usuario intente iniciar sesión.

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

En el siguiente paso de diálogo, compruebe la presencia de un token en el resultado del paso anterior. Si no es null, el usuario ha iniciado sesión correctamente.

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

**diálogos/logout_dialog.py**

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="see-also"></a>Vea también

[Agregar autenticación a través de Azure Bot Service](https://aka.ms/azure-bot-add-authentication)

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
