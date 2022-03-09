---
title: Creación de pestañas y otras experiencias hospedadas con el SDK de cliente de JavaScript
author: heath-hamilton
ms.author: surbhigupta
description: Información general sobre el SDK Microsoft Teams cliente de JavaScript, que puede ayudarle a crear experiencias Teams aplicaciones hospedadas en un <iframe>. Incluye funciones básicas, espacio de nombres de autenticación y espacio de nombres de configuración.
ms.localizationpriority: medium
keywords: Canal de grupo de pestañas de teams configurable sdk estático JavaScript personal
ms.topic: conceptual
ms.openlocfilehash: e5dcacc4dbd3cdf63fc479f3e24fedfd3b819223
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356276"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Creación de pestañas y otras experiencias hospedadas con el SDK Microsoft Teams cliente de JavaScript

El SDK Microsoft Teams cliente de JavaScript puede ayudarte a crear experiencias hospedadas en Teams, lo que significa mostrar el contenido de la aplicación en un iframe.

El SDK es útil para desarrollar aplicaciones con cualquiera de las siguientes Teams funcionalidades:

* [Pestañas](../../tabs/what-are-tabs.md)
* [Módulos de tareas](../../task-modules-and-cards/what-are-task-modules.md)

Por ejemplo, el SDK puede hacer que la [pestaña reaccione a](../../build-your-first-app/build-personal-tab.md#3-update-your-tab-theme) los cambios en el tema que los usuarios realicen en el Teams cliente.

## <a name="getting-started"></a>Introducción

Realice una de las siguientes acciones según sus preferencias de desarrollo:

* [Instalar el SDK con npm o Yarn](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* [Clonar el SDK (GitHub)](https://github.com/OfficeDev/microsoft-teams-library-js)

## <a name="common-sdk-functions"></a>Funciones comunes de SDK

Consulta las tablas siguientes para comprender las funciones de SDK que se usan con frecuencia. La [documentación de referencia del SDK](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) proporciona información más completa.

### <a name="basic-functions"></a>Funciones básicas

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | Inicializa el SDK. Se debe llamar a esta función antes de cualquier otra llamada del SDK.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initialize&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| Obtiene el estado actual en el que se está ejecutando la página. La devolución de llamada recupera el **objeto Context** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)<br/>[context obj](/javascript/api/@microsoft/teams-js/@microsoft.teams-js?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Inicializa la biblioteca Teams y establece el contexto de marco de la [pestaña en función](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) de contentUrl y websiteUrl. Esto garantiza que la funcionalidad de ir al sitio web/recargar funciona en la dirección URL correcta.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initializewithframecontext&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | Establece el contexto de marco de [la pestaña](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) en función de contentUrl y websiteUrl. Esto garantiza que la funcionalidad de ir al sitio web/recargar funciona en la dirección URL correcta.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-setframecontext&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: Boolean)` |Controlador que se registra cuando el usuario alterna la vista de pantalla completa o ventana de una pestaña.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)<br/>[Boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |Controlador que se registra cuando el usuario selecciona el botón de **Configuración habilitado para** volver a configurar una pestaña.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Obtiene las pestañas propiedad de la aplicación. La devolución de llamada recupera el **objeto TabInformation** . El **objeto TabInstanceParameters** es un parámetro opcional.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-gettabinstances&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Obtiene las pestañas usadas más recientemente para el usuario. La devolución de llamada recupera el **objeto TabInformation** . El **objeto TabInstanceParameters** es un parámetro opcional.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-getmrutabinstances&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Toma el **objeto DeepLinkParameters** como entrada y comparte un cuadro de diálogo de vínculo profundo que un usuario puede usar para navegar al contenido *dentro de la pestaña*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-sharedeeplink&preserve-view=true)<br/>[deepLink obj](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: Boolean, reason?: string))`|Toma un **deepLink** necesario como entrada y navega al usuario a una dirección URL o desencadena una acción de cliente(como abrir o instalar) una aplicación dentro *de Teams*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-executedeeplink&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: Boolean, reason?: string))`|Toma el **objeto TabInstance** como entrada y navega a una instancia de pestaña especificada.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-navigatetotab&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>Espacio de nombres de autenticación

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Inicia una solicitud de autenticación que abre una nueva ventana con los parámetros proporcionados por el autor de la llamada. El objeto **AuthenticateParameters** define los valores de entrada opcionales.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Notifica al marco que inició la solicitud de autenticación que la solicitud se ha realizado correctamente y cierra la ventana de autenticación|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Notifica al marco que inició la solicitud de autenticación que la solicitud ha producido un error y cierra la ventana de autenticación.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.getAuthToken(authTokenRequest: AuthTokenRequest)`|Enviar solicitud para emitir Azure AD token en nombre de la aplicación. El token se puede adquirir de la memoria caché, si no ha expirado. De lo contrario, se envía una solicitud Azure AD para obtener un nuevo token.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true)|

### <a name="settings-namespace"></a>Configuración espacio de nombres

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: Boolean)`|El valor inicial es false. Activa el botón **Guardar** o **Quitar** cuando el estado de validez es true.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Obtiene la configuración de la instancia actual. La devolución de llamada recupera **el Configuración** objeto.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: Boolean, reason?: string)`|Configura la configuración de la instancia actual. La configuración válida se define mediante **Configuración** objeto.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Controlador que se registra cuando el usuario selecciona el **botón** Guardar. Este controlador debe usarse para crear o actualizar el recurso subyacente que potencia el contenido.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|Controlador que se registra cuando el usuario selecciona el **botón** Quitar. Este controlador debe usarse para quitar el recurso subyacente que potencia el contenido.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>Espacio de nombres de módulos de tareas

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Toma el **objeto TaskInfo** como entrada y permite que una aplicación abra el módulo de tareas. El **objeto submitHandler** opcional se registra cuando se completa el módulo de tareas. |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Envía el módulo de tareas. El parámetro **de cadena** de resultado opcional es el resultado enviado al bot o a la aplicación y suele ser un objeto JSON o serialización; El parámetro de cadena o matriz de cadena **appIds** opcional ayuda a validar que la llamada se originó desde el mismo appId que el que invocó el módulo de tareas.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-tasks-submittask&preserve-view=true)|
