---
title: Creación de pestañas y otras experiencias alojadas con el SDK de cliente de JavaScript
author: heath-hamilton
ms.author: surbhigupta
description: Descripción general del SDK de cliente de JavaScript Microsoft Teams, que puede ayudarle a crear experiencias de aplicación Teams alojadas en un <iframe>.
localization_priority: Normal
keywords: equipos pestañas canal de grupo configurable ESTÁTICA SDK JavaScript personal
ms.topic: conceptual
ms.openlocfilehash: d3dfadda7f2a56e32ecf8e5b67df3b9831c52739
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566659"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Creación de pestañas y otras experiencias alojadas con el SDK de cliente de JavaScript Microsoft Teams

El SDK de cliente de JavaScript Microsoft Teams puede ayudarle a crear experiencias hospedadas en Teams, lo que significa mostrar el contenido de la aplicación en un iframe.

El SDK es útil para desarrollar aplicaciones con cualquiera de las siguientes capacidades de Teams:

* [Pestañas](../../tabs/what-are-tabs.md)
* [Módulos de tareas](../../task-modules-and-cards/what-are-task-modules.md)

Por ejemplo, el SDK puede hacer que la [pestaña reaccione a los cambios](../../build-your-first-app/build-personal-tab.md) de tema que realizan los usuarios en el cliente Teams.

## <a name="getting-started"></a>Introducción

Realice una de las siguientes acciones en función de sus preferencias de desarrollo:

* [Instale el SDK con npm o Yarn](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)

## <a name="common-sdk-functions"></a>Funciones comunes del SDK

Consulte las tablas siguientes para comprender las funciones de SDK de uso común. La [documentación de referencia del SDK](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) proporciona información más completa:


### <a name="basic-functions"></a>Funciones básicas

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | Inicializa el SDK. Se debe llamar a esta función antes de cualquier otra llamada al SDK.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| Obtiene el estado actual en el que se ejecuta la página. La devolución de llamada recupera el **context** objeto.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-&preserve-view=true)<br/>[contexto obj](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Inicializa la biblioteca de Teams y establece el contexto de [fotogramas](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) de la pestaña en función de contentUrl y websiteUrl. Esto garantiza que la funcionalidad de ir al sitio web o recargar funcione en la DIRECCIÓN URL correcta.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | Establece el contexto de [fotogramas](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) de la pestaña en función de contentUrl y websiteUrl. Esto garantiza que la funcionalidad de ir al sitio web o recargar funcione en la DIRECCIÓN URL correcta.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |Controlador que se registra cuando el usuario alterna la vista de pantalla completa o ventana de una pestaña.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-&preserve-view=true)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerFullScreenHandler__isFullScreen__boolean_____void_&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |El controlador que se registra cuando el usuario selecciona el botón **Configuración** habilitado para volver a configurar una pestaña.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Obtiene las pestañas propiedad de la aplicación. La devolución de llamada recupera el objeto **TabInformation.** El objeto **TabInstanceParameters** es un parámetro opcional.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Obtiene las pestañas usadas más recientemente para el usuario. La devolución de llamada recupera el objeto **TabInformation.** El objeto **TabInstanceParameters** es un parámetro opcional.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Toma el objeto **DeepLinkParameters** como entrada y comparte un cuadro de diálogo de vínculo profundo que un usuario puede usar para navegar al contenido *dentro de la pestaña*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-&preserve-view=true)<br/>[deepLink obj](/javascript/api/@microsoft/teams-js/deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|Toma un **deepLink** necesario como entrada y navega por el usuario a una dirección URL o desencadena una acción de cliente, como abrir o instalar, una aplicación *dentro de Teams*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|Toma el objeto **TabInstance** como entrada y navega a una instancia de pestaña especificada.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>Espacio de nombres de autenticación

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Inicia una solicitud de autenticación que abre una nueva ventana con los parámetros proporcionados por el llamador. Los valores de entrada opcionales se definen mediante el **authenticateparameters** objeto.|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](/javascript/api/@microsoft/teams-js/authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Notifica el marco que inició la solicitud de autenticación que la solicitud se realizó correctamente y cierra la ventana de autenticación|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Notifica el marco que inició la solicitud de autenticación que la solicitud falló y cierra la ventana de autenticación.|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|

### <a name="settings-namespace"></a>espacio de nombres Configuración

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|El valor inicial es false. Activa el botón **Guardar** o **quitar** cuando el estado de validez es true.|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Obtiene la configuración de la instancia actual. La devolución de llamada recupera el objeto **Configuración.**|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[ajustes obj](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|Configura la configuración de la instancia actual. La configuración válida se define mediante el objeto **Configuración.**|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[ajustes obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Controlador que se registra cuando el usuario selecciona el botón **Guardar.** Este controlador debe usarse para crear o actualizar el recurso subyacente que alimenta el contenido.|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|El controlador que se registra cuando el usuario selecciona el botón **Quitar.** Este controlador debe usarse para quitar el recurso subyacente que alimenta el contenido.|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>Espacio de nombres de módulos de tareas

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Toma el objeto **TaskInfo** como entrada y permite que una aplicación abra el módulo de tareas. El **submitHandler** opcional se registra cuando se completa el módulo de tareas. |[function](/javascript/api/@microsoft/teams-js/tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Envía el módulo de tareas. El parámetro de cadena **de resultado** opcional es el resultado enviado al bot o a la aplicación y suele ser un objeto JSON o serialización; El parámetro opcional **appIds** string o string array ayuda a validar que la llamada se originó desde el mismo appId que el que invocó el módulo de tareas.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)|
