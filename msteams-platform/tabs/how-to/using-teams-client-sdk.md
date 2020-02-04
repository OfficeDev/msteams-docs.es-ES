---
title: Uso del SDK del cliente de Microsoft Teams
author: laujan
description: Cómo usar el SDK del cliente de Microsoft Teams para agregar funcionalidad consciente de Teams a las pestañas personalizadas
keywords: Grupo de pestañas de Microsoft canal de grupo configurable del SDK estático personalizado JavaScript
ms.topic: conceptual
ms.openlocfilehash: eac5a8ec03ba12d926346afb40ca9bc6e9dda8d6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676190"
---
# <a name="using-the-teams-client-sdk"></a>Uso del SDK del cliente de Microsoft Teams

El **SDK del cliente** de Microsoft Teams y la **biblioteca de JavaScript de Teams** forman parte de la [plataforma para desarrolladores de Microsoft Teams](https://msdn.microsoft.com/microsoft-teams) y proporcionan herramientas y procesos para facilitar la creación de aplicaciones de Teams. El SDK del cliente de Microsoft Teams se distribuye como un paquete NPM. Puede encontrar la versión más reciente aquí: <https://www.npmjs.com/package/@microsoft/teams-js>. La biblioteca de Microsoft Teams <https://github.com/OfficeDev/microsoft-teams-library-js>se encuentra en.

En la tabla siguiente se describen las funciones de la biblioteca de teams que se usan normalmente en el desarrollo de pestañas:

## <a name="teams-sdk-public-api"></a>API pública del SDK de Microsoft Teams 

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    | -----        |
| `microsoftTeams.initialize()` | Inicializa la biblioteca de Teams. Se debe llamar a esta función antes de cualquier otra llamada a SDK.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-)|
|`microsoftTeams.getContext(callback: (context: Context)`| Obtiene el estado actual en el que se está ejecutando la página. La devolución de llamada recupera el objeto de **contexto** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-)<br/>[obj de contexto](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |El controlador que se registra cuando el usuario cambia la vista de pantalla completa o de ventana de una pestaña.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest#isfullscreen)|
|`microsoftTeams.registerChangeSettingsHandler()` |El controlador que se registra cuando el usuario selecciona el botón **configuración** habilitada para reconfigurar una pestaña.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Obtiene las pestañas que pertenecen a la aplicación. La devolución de llamada recupera el objeto **TabInformation** . El objeto **TabInstanceParameters** es un parámetro opcional.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[obj tabInfo](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Obtiene las pestañas usadas más recientemente del usuario. La devolución de llamada recupera el objeto **TabInformation** . El objeto **TabInstanceParameters** es un parámetro opcional.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[obj tabInfo](/javascript/api/@microsoft/teams-js/microsoftteams.teaminformation?view=msteams-client-js-latest)<br/>[obj tabInstance](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Toma el objeto **DeepLinkParameters** como entrada y comparte un cuadro de diálogo de vínculo profundo que puede usar un usuario para navegar hasta *el contenido dentro de la pestaña*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-)<br/>[obj de vínculo profundo](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|Toma un **vínculo profundo** obligatorio como entrada y navega a un usuario a una dirección URL o desencadena una acción del cliente (por ejemplo, abrir o instalar) una aplicación *dentro de Microsoft Teams*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|Toma el objeto **TabInstance** como entrada y se desplaza a una instancia de Tab especificada.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-)<br/>[obj tabInstance](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest)|

## <a name="authentication-namespace"></a>Espacio de nombres de autenticación

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Inicia una solicitud de autenticación que abre una nueva ventana con los parámetros proporcionados por el autor de la llamada. Los valores de entrada opcionales los define el objeto **AuthenticateParameters** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#authenticate-authenticateparameters-)<br/>[obj de autenticación](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Notifica a la trama que inició la solicitud de autenticación que la solicitud se ha realizado correctamente y cierra la ventana de autenticación|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifysuccess-string--string-)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Notifica a la trama que inició la solicitud de autenticación que la solicitud produjo un error y cierra la ventana de autenticación.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifyfailure-string--string-)|

## <a name="settings-namespace"></a>Espacio de nombres de configuración

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|El valor inicial es false. Activa el botón **Guardar** o **quitar** cuando el estado de validez es true.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setvaliditystate-boolean-)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Obtiene la configuración de la instancia actual. La devolución de llamada recupera el objeto de **configuración** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#getsettings--instancesettings--settings-----void-)<br/>[obj de configuración](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|Configura las opciones de la instancia actual. La configuración válida se define mediante el objeto **Settings** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setsettings-settings-)<br/>[obj de configuración](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Controlador que se registra cuando el usuario selecciona el botón **Guardar** . Este controlador debe usarse para crear o actualizar el recurso subyacente que enciende el contenido.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronsavehandler--evt--saveevent-----void-)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|El controlador que se registra cuando el usuario selecciona el botón **quitar** . Este controlador debe usarse para quitar el recurso subyacente que enciende el contenido.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronremovehandler--evt--removeevent-----void-)|

## <a name="tasks-namespace"></a>Espacio de nombres de tareas

| Función  | Descripción          | Documentación|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Toma el objeto **TaskInfo** como entrada y permite que una aplicación Abra el módulo de tareas. La **submitHandler** opcional se registra cuando se completa el módulo de tareas. |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#starttask-taskinfo---err--string--result--string-----void-)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Envía el módulo de tareas. El parámetro de cadena de **resultado** opcional es el resultado que se envía al bot o a la aplicación y suele ser un objeto JSON o una serialización; La cadena **appIds** opcional o el parámetro de matriz de cadenas ayuda a validar que la llamada se originó desde el mismo AppID que la que invocó el módulo de tareas.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---)|