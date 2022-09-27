---
title: Uso del kit de herramientas de Teams para aprovisionar recursos en la nube mediante El kit de herramientas de Teams para Visual Studio
author: surbhigupta
description: En este módulo, aprenderá a aprovisionar recursos en la nube mediante el kit de herramientas de Teams. También para crear recursos y personalizar el aprovisionamiento de recursos en Visual Studio
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 00e021e3e42eed6eeb5881d258a9884a7e579377
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027496"
---
# <a name="provision-cloud-resources-using-visual-studio"></a>Aprovisionamiento de recursos en la nube mediante Visual Studio

TeamsFx se integra con La nube de Azure y Microsoft 365 que permite colocar la aplicación en Azure con un solo comando. TeamsFx se integra con Azure Resource Manager que le permite aprovisionar recursos de Azure. Para el enfoque de código, la aplicación necesita los recursos en la nube.

## <a name="prerequisites"></a>Requisitos previos

Esta es una lista de herramientas que necesita para aprovisionar los recursos en la nube:

| &nbsp; | Instalar | Para usar... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 2022, versión 17.3 | Puede instalar la edición enterprise de Visual Studio e instalar la carga de trabajo "ASP.NET" y las herramientas de desarrollo de Microsoft Teams. |
| &nbsp; | [Cuenta de desarrollador de Microsoft 365](https://developer.microsoft.com/en-us/microsoft-365/dev-program) | Acceso a la cuenta de Teams con los permisos adecuados para instalar una aplicación. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams para colaborar con todos los usuarios con los que trabaja a través de aplicaciones de chat, reuniones, llamadas, todo en un solo lugar. |
| &nbsp; | Kit de herramientas de Teams | Extensión de Visual Studio que crea un scaffolding de proyecto para la aplicación. Use la versión más reciente. |
| &nbsp; | [Cuenta de Azure](https://portal.azure.com/) | Cuenta de Azure con una suscripción válida. |

## <a name="steps-to-provision-cloud-resources"></a>Pasos para aprovisionar recursos en la nube

Los pasos siguientes le ayudan a aprovisionar recursos en la nube mediante Visual Studio:

### <a name="sign-in-to-your-microsoft-365-account"></a>Inicio de sesión en su cuenta de Microsoft 365

1. Visual Studio 2022.
2. Abra el proyecto de aplicación de Microsoft Teams.
3. Seleccione **Proyecto**.
4. Seleccione **Kit de herramientas de Teams**.
5. Seleccione **Preparar dependencias de aplicaciones de Teams**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare-app-dependencies.png" alt-text="Preparación de dependencias de aplicaciones de Teams":::

7. Seleccione **Iniciar sesión...** para iniciar sesión en su cuenta de Azure.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare1.png" alt-text="Inicio de sesión en Microsoft 365":::

    > [!NOTE]
    > Si ya ha iniciado sesión, se muestra el nombre de usuario o puede seleccionar el mismo para cambiar su cuenta.

8. Se abre el explorador web predeterminado para permitirle [iniciar sesión en](https://developer.microsoft.com/en-us/microsoft-365/dev-program) la cuenta.
9. Seleccione **Continuar** después de iniciar sesión en su cuenta.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-signin-M365.png" alt-text="Para confirmar, seleccione Continuar.":::

### <a name="sign-in-to-your-azure-account"></a>Inicio de sesión en su cuenta de Azure

1. Abra Visual Studio 2022.
2. Abra el proyecto Aplicación de Teams.
3. Seleccione **Proyecto**.
4. Seleccione **Kit de herramientas de Teams**.
5. Seleccione **Aprovisionar en la nube**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud.png" alt-text="Inicio de sesión en la cuenta de Azure":::

6. Seleccione **Iniciar sesión...** para iniciar sesión en su cuenta de Azure.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-start.png" alt-text="Inicio de sesión en su cuenta de Azure":::

   > [!NOTE]
   > Si ya ha iniciado sesión, se muestra el nombre de usuario o tiene la opción de cambiar de cuenta.

7. Inicie sesión en la cuenta de Azure con sus credenciales. El explorador se cierra automáticamente.

### <a name="to-provision-cloud-resources"></a>Para aprovisionar recursos en la nube

1. Después de abrir el proyecto en Visual Studio, seleccione **Proyecto**.
2. Selección **del kit de herramientas de Teams**
3. Seleccione **Aprovisionar en la nube**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud1.png" alt-text="Aprovisionamiento en la nube":::

4. En el cuadro de diálogo **Aprovisionar** , puede ver una lista de todas las suscripciones de la cuenta de Azure.
5. Puede seleccionar o crear un nuevo **grupo de recursos**.
6. Seleccione **Aprovisionar**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-select-subscription1.png" alt-text="Seleccionar grupo de recursos":::

7. El cuadro de diálogo le advierte de que se pueden agregar cargos según el uso de Azure. Seleccione **Aprovisionar**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-warning.png" alt-text="Advertencia de aprovisionamiento":::

   El proceso de aprovisionamiento de la creación de los recursos en la nube de Azure puede tardar algún tiempo.

8. Compruebe la ventana de salida del kit de herramientas de Teams para supervisar el progreso.
9. Se le pedirá una vez completado el aprovisionamiento. Seleccione **Ver recursos aprovisionados** para ver todos los recursos aprovisionados.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-provision-success.png" alt-text="Visualización de recursos aprovisionados":::

### <a name="create-resources"></a>Creación de recursos

Al desencadenar el comando de aprovisionamiento en Teams Toolkit o la CLI de TeamsFx, puede crear los siguientes recursos:

* Microsoft Azure Active Directory aplicación (Azure AD) en el inquilino de Microsoft 365.
* Registro de aplicaciones de Teams en la plataforma de Teams del inquilino de Microsoft 365.
* Recursos de Azure en la suscripción de Azure seleccionada.

Al crear un nuevo proyecto, también debe crear recursos de Azure. Las plantillas de Azure Resource Manager (ARM) definen todos los recursos de Azure y le ayudan a crear los recursos de Azure necesarios durante el aprovisionamiento.

### <a name="create-resource-for-teams-tab-application"></a>Creación de un recurso para una aplicación de pestaña de Teams

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Plan de App Service | Hospeda la aplicación web de la pestaña. | No aplicable |
| App Service | Hospeda la aplicación de pestaña Blazor y el servidor de autenticación simple que ayuda a obtener acceso a otros servicios. | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. |
| Administrar identidad | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |

### <a name="create-resources-for-teams-message-extension-application"></a>Creación de recursos para la aplicación de extensión de mensajes de Teams

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| plan de App Service | Hospeda la aplicación de bot web. | No aplicable |
| App Service | Hospeda la aplicación de bot. | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. |
| Administrar identidad | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |

### <a name="create-resources-for-teams-command-bot-application"></a>Creación de recursos para la aplicación de bot de comandos de Teams

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| Plan de App Service | Hospeda la aplicación de bot web. | No aplicable |
| App Service | Hospeda la aplicación de bot. | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. |
| Administrar identidad | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |

### <a name="create-resources-for-teams-notification-bot-with-http-trigger-web-api-server-application"></a>Creación de recursos para el bot de notificaciones de Teams con una aplicación de desencadenador HTTP (servidor de API web)

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| Plan de App Service | Hospeda la aplicación de bot web. | No aplicable |
| App Service | Hospede la aplicación de bot. | Añade la identidad asignada por el usuario para acceder a otros recursos de Azure. |
| Identidad administrada | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |

### <a name="create-resource-for-teams-notification-bot-with-http-trigger-azure-function-application"></a>Creación de un recurso para el bot de notificación de Teams con una aplicación de desencadenador HTTP (función de Azure)

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| Administrar identidad | Autentica las solicitudes de servicio a servicio de Azure. | Compartido entre diferentes funcionalidades y recursos. |
| Cuenta de almacenamiento | Ayuda a crear la aplicación de funciones. | No aplicable |
| Plan de App Service | Hospeda la aplicación del bot de función. | No aplicable |
| Aplicación de funciones | Hospeda la aplicación de bot. | -Agrega la identidad asignada por el usuario para acceder a otros recursos de Azure.<br>-Agrega la regla de uso compartido de recursos entre orígenes (CORS) para permitir solicitudes desde la aplicación de pestaña.<br>-Agrega la configuración de autenticación que solo permite las solicitudes de la aplicación de Teams.<br>-Agrega la configuración de la aplicación requerida por el SDK de TeamsFx. |

### <a name="create-resource-for-teams-notification-bot-with-timer-trigger-azure-function-application"></a>Creación de un recurso para el bot de notificación de Teams con una aplicación de desencadenador de temporizador (función de Azure)

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| Administrar identidad | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |
| Cuenta de almacenamiento | Ayuda a crear la aplicación de funciones. | No procede. |
| Plan de App Service | Hospeda la aplicación de bot de función. | No aplicable |
| Aplicación de funciones | Hospeda la aplicación de bot. | -Agrega la identidad asignada por el usuario para acceder a otros recursos de Azure.<br>-Agrega la regla de uso compartido de recursos entre orígenes (CORS) para permitir solicitudes desde la aplicación de pestaña.<br>-Agrega la configuración de autenticación que solo permite las solicitudes de la aplicación de Teams.<br>-Agrega la configuración de la aplicación requerida por el SDK de TeamsFx. |

### <a name="create-resources-for-teams-notification-bot-with-http-trigger--timer-trigger-azure-function-application"></a>Creación de recursos para el bot de notificación de Teams con la aplicación desencadenador HTTP y desencadenador de temporizador (función de Azure)

| Resource | Objetivo | Descripción |
| --- | --- | --- |
| Bot de Azure | Registra la aplicación como un bot con bot framework. | Conecta el bot a Teams. |
| Administrar identidad | Autentique las solicitudes de servicio a servicio de Azure. | Recursos compartidos entre diferentes funcionalidades y recursos. |
| Cuenta de almacenamiento | Ayuda a crear la aplicación de funciones. | No aplicable |
| Plan de App Service | Hospeda la aplicación de bot de función. | No aplicable |
| Function App | Hospeda la aplicación de bot. | -Agrega la identidad asignada por el usuario para acceder a otros recursos de Azure.<br>-Agrega la regla de uso compartido de recursos entre orígenes (CORS) para permitir solicitudes desde la aplicación de pestaña.<br>-Agrega la configuración de autenticación que solo permite las solicitudes de la aplicación de Teams.<br>-Agrega la configuración de la aplicación requerida por el SDK de TeamsFx. |

### <a name="manage-your-resources"></a>Administrar los recursos

Puede iniciar sesión para [Azure Portal](https://portal.azure.com/) y administrar todos los recursos creados por Teams Toolkit.

* Puede seleccionar el grupo de recursos de la lista existente o el nuevo grupo de recursos que ha creado.
* Puede ver los detalles del grupo de recursos que ha seleccionado en la sección de información general de la tabla de contenido.

### <a name="customize-resource-provision"></a>Personalización del aprovisionamiento de recursos

Teams Toolkit le permite usar una infraestructura para el enfoque de código para definir los recursos de Azure que desea aprovisionar. Puede cambiar la configuración en el kit de herramientas de Teams según sus necesidades.

Teams Toolkit usa una plantilla de ARM para definir recursos de Azure. La plantilla de ARM es un conjunto de archivos bicep que define la infraestructura y configuración del proyecto. Puede personalizar los recursos de Azure modificando la plantilla de ARM. Para obtener más información, consulte la [documentación de bicep](/azure/azure-resource-manager/bicep).

Aprovisionar con ARM implica cambiar los siguientes conjuntos de archivos, parámetros y plantillas:

* Archivos de parámetros de ARM (`azure.parameters.{your_env_name}.json`) ubicados en `.fx/configs` la carpeta para pasar parámetros a plantillas.
* Los archivos de plantilla de ARM ubicados en `templates/azure` la carpeta contienen los siguientes archivos:

| Archivo | Función | Permitir personalización |
| --- | --- | --- |
| main.bicep | Proporcione un punto de entrada para el recurso de Azure. Provisión | Sí |
| provision.bicep | Cree y configure recursos de Azure. | Sí |
| config.bicep | Agregue las configuraciones necesarias de TeamsFx a los recursos de Azure. | Sí |
| provision/xxx.bicep | Cree y configure cada recurso de Azure consumido por `provision.bicep`. | Sí |
| teamsfx/xxx.bicep | Agregue las configuraciones necesarias de TeamsFx a cada recurso de Azure consumido por `config.bicep`.| No |

> [!NOTE]
> Después de agregar recursos o funcionalidades al proyecto, `teamsfx/xxx.bicep` se vuelve a generar. Para modificar los archivos de bicep, puede usar Git para realizar un seguimiento de los cambios en `teamsfx/xxx.bicep` los archivos. Esto no hace que pierda ningún cambio al agregar recursos o funcionalidades al proyecto.

Los archivos de plantilla de ARM usan marcadores de posición para los parámetros. El propósito de los marcadores de posición es asegurarse de que se pueden crear nuevos recursos en el nuevo entorno. Los valores reales se resuelven desde el `.fx/states/state.{env}.json` archivo.

### <a name="azure-ad-application-related-parameters"></a>Parámetros relacionados con la aplicación de Azure AD

| Nombre del parámetro | Marcador de posición de valor predeterminado | Significado del marcador de posición | Cómo personalizar |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | El identificador de cliente de la aplicación de Azure AD creado durante el aprovisionamiento. | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | El secreto de cliente de la aplicación de Azure AD creado durante el aprovisionamiento. | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | Identificador de inquilino de la aplicación de Azure AD. | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | Host de autoridad de OAuth de la aplicación de Azure AD de la aplicación. | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | Identificador de cliente de la aplicación de Azure AD del bot creado durante el aprovisionamiento. | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | Secreto de cliente de la aplicación de Azure AD del bot creado durante el aprovisionamiento. | [Personalice el valor](#use-an-existing-azure-ad-app-for-your-bot) |

### <a name="reference-environment-variables-in-parameter-files"></a>Variables de entorno de referencia en archivos de parámetros

Cuando el valor es secreto, no es necesario codificarlos de forma rígida en el archivo de parámetros. los archivos de parámetros admiten referenciar valores de las variables de entorno. Puede usar esta sintaxis `{{$env.YOUR_ENV_VARIABLE_NAME}}` en los valores de parámetro del kit de herramientas de Teams para resolver a partir de la variable de entorno actual.

En el ejemplo siguiente se lee el valor del parámetro `mySelfHostedDbConnectionString` de la variable de entorno `DB_CONNECTION_STRING`:

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

### <a name="customize-arm-template-files"></a>Personalización de archivos de plantilla de ARM

Si las plantillas predefinidas no cumplen los requisitos de la aplicación, puede personalizar las plantillas de ARM en `templates/azure` la carpeta . Por ejemplo, puede personalizar la plantilla de ARM para crear algunos recursos adicionales de Azure para la aplicación. Debe tener conocimientos básicos del lenguaje bicep, que se usa para crear una plantilla de ARM.

Para asegurarse de que la herramienta TeamsFx funciona correctamente, personalice la plantilla de ARM que satisfaga el siguiente requisito:

* Asegúrese de que la estructura de carpetas y el nombre de archivo permanecen sin cambios. La herramienta puede anexar contenido nuevo a los archivos existentes al agregar más recursos o funcionalidades al proyecto.
* Asegúrese de que el nombre de los parámetros generados automáticamente y sus nombres de propiedad permanecen sin voladizo. Puede que se usen los parámetros generados automáticamente al añadir más recursos o funcionalidades al proyecto.
* Asegúrese de que la salida de la plantilla de ARM generada automáticamente también no cambia. Puede agregar más salidas a la plantilla de ARM. La salida es `.fx/states/state.{env}.json` y se puede usar en otras características, como implementar y validar el archivo de manifiesto.

### <a name="customize-teams-app"></a>Personalización de la aplicación Teams

Puede personalizar el bot o la aplicación de Teams agregando fragmentos de código de configuración para usar una aplicación de Azure AD creada por usted. Puede realizar de las siguientes maneras:

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>Uso de una aplicación de Azure AD existente para el bot

Puede agregar el siguiente fragmento de código de `.fx/configs/config.{env}.json` configuración para usar una aplicación de Azure AD creada por usted para la aplicación de Teams. Para crear una aplicación de Azure AD, siga el vínculo <https://aka.ms/teamsfx-existing-aad-doc>.

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

Después de agregar el fragmento de código, agregue el secreto de cliente a la variable de entorno relacionada para que teams Toolkit pueda resolver el secreto de cliente real durante el aprovisionamiento.

> [!NOTE]
> Asegúrese de no compartir la misma aplicación Azure AD en varios entornos. Si no tiene permiso para actualizar la aplicación de Azure AD, recibirá una advertencia con instrucciones para actualizar manualmente la aplicación de Azure AD. Siga estas instrucciones para actualizar la aplicación de Azure AD después del aprovisionamiento.

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Uso de una aplicación de Azure AD existente para su aplicación de Teams

Puede agregar el siguiente fragmento de código de configuración para `.fx/configs/config.{env}.json` usar la aplicación de Azure AD creada para el bot:

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

Después de agregar el fragmento de código, agregue el secreto de cliente a la variable de entorno relacionada para que Teams Toolkit resuelva el secreto de cliente real durante el aprovisionamiento.

#### <a name="skip-adding-user-for-sql-database"></a>Omisión de la adición de usuario a la base de datos SQL

Si recibe un error de permiso insuficiente cuando Teams Toolkit intenta agregar un usuario a SQL Database, puede agregar el siguiente fragmento de código de configuración para `.fx/configs/config.{env}.json` omitir la adición de un usuario de base de datos SQL:

```json
"skipAddingSqlUser": true
```

## <a name="see-also"></a>Vea también

* [Implementación de una aplicación de Teams en la nube mediante Visual Studio](deploy-teams-app.md)
* [Edición del manifiesto de aplicación de Teams mediante Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Depuración local de aplicaciones de Teams para Visual Studio](debug-teams-app-visual-studio.md)
