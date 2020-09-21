---
title: Creación de una etiqueta de eliminación
author: laujan
description: Cómo crear una página de eliminación de pestañas
keywords: Grupo de pestañas de Teams configuración de canal quitar eliminar
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4ee060b8ef1f439ed4f8e4007e63606ce34c3d24
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964595"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>Modificar o quitar una pestaña de grupo de canales

Puede ampliar y mejorar la experiencia del usuario si admite opciones de eliminación y modificación en la aplicación. Teams permite a los usuarios cambiar el nombre o quitar una ficha canal o grupo y permitir que los usuarios vuelvan a configurar la pestaña después de la instalación. Además, la experiencia de eliminación de pestañas puede incluir designar lo que ocurre con el contenido cuando se quita la pestaña o conceder a los usuarios opciones posteriores a la eliminación, como eliminar o archivar el contenido.

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Habilitar la reconfiguración de la ficha después de la instalación

El **manifest.jsen** define las características y capacidades de la pestaña. La propiedad de instancia Tab `canUpdateConfiguration` toma un valor booleano que indica si un usuario puede modificar o volver a configurar la pestaña una vez creada:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`canUpdateConfiguration`|Booleano|||Un valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de crearla. Predeterminada `true`|

Cuando se cargue la pestaña en un chat de grupo o de canal, Microsoft Teams agregará un menú desplegable con el botón secundario para la ficha. Las opciones disponibles están determinadas por la `canUpdateConfiguration` Configuración:

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Configuración            |   √    |       |La `configurationUrl` página se vuelve a cargar en un iframe, lo que permite al usuario volver a configurar la ficha.  |
|     Cambiar nombre              |   √    |   √   | El usuario puede cambiar el nombre de la pestaña tal como aparece en la barra de pestañas.          |
|     Eliminar               |   √    |   √   |  Si la  `removeURL` propiedad y el valor se incluyen en la **Página de configuración**, la página de **eliminación** se carga en un iframe y se presenta al usuario. Si no se incluye una página de eliminación, se muestra al usuario un cuadro de diálogo confirmar.          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>Crear una página de eliminación de pestañas para la aplicación

La página de eliminación opcional es una página HTML que se hospeda y se muestra cuando se quita la pestaña. La dirección URL de la página de eliminación se designa mediante el `setSettings()` método dentro de la página de configuración. Como con todas las páginas de la aplicación, la página de eliminación debe cumplir con los requisitos de la pestaña de Microsoft [Teams](~/tabs/how-to/add-tab.md).

### <a name="register-a-remove-handler"></a>Registro de un controlador de eliminación

De forma opcional, dentro de la lógica de la página de eliminación, puede invocar el `registerOnRemoveHandler((RemoveEvent) => {}` controlador de eventos cuando el usuario quita una configuración de pestaña existente. El método toma la [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) interfaz y ejecuta el código en el controlador cuando un usuario intenta quitar contenido. Se usa para realizar operaciones de limpieza, como quitar el recurso subyacente que enciende el contenido de la pestaña. Solo se puede registrar un controlador de eliminación a la vez.

La `RemoveEvent` interfaz describe un objeto con dos métodos:

* `notifySuccess()`Se requiere la función. Indica que la eliminación del recurso subyacente se ha realizado correctamente y que se puede quitar su contenido.

* La `notifyFailure(string)` función es opcional. Indica que se ha producido un error en la eliminación del recurso subyacente y no se puede quitar su contenido. El parámetro de cadena opcional especifica un motivo del error. Si se proporciona, esta cadena se muestra al usuario; de lo contrario, se muestra un error genérico.

#### <a name="use-the-getsettings-function"></a>Usar la `getSettings()` función

Puede usar `getSettings()` para designar el contenido de la pestaña que se va a quitar. La `getSettings((Settings) =>{})` función toma el [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) y proporciona los valores de propiedad de configuración válidos que se pueden recuperar.

#### <a name="use-the-getcontext-function"></a>Usar la `getContext()` función

Puede usar `getContext()` para recuperar el contexto actual en el que se ejecuta el marco. La `getContext((Context) =>{})` función toma el [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) y proporciona valores de `Context` propiedad válidos que puede usar en la lógica de la página de eliminación para determinar el contenido que se muestra en la página de eliminación.

#### <a name="include-authentication"></a>Incluir autenticación

Es posible que necesite autenticación antes de permitir que un usuario elimine el contenido de la pestaña. La información de contexto se puede usar para crear solicitudes de autenticación y direcciones URL de la página de autorización. Vea [flujo de autenticación de Microsoft Teams para pestañas](~/tabs/how-to/authentication/auth-flow-tab.md). Asegúrese de que todos los dominios usados en las páginas de pestañas se enumeran en la `manifest.json` `validDomains` matriz.

A continuación se muestra un bloque de código de eliminación de pestañas:

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    microsoftTeams.initialize();
    microsoftTeams.settings.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        microsoftTeams.settings.getSettings((settings) => {
        settings.contentUrl = "..."
        });
        removeEvent.notifySuccess();
    });

    const onClick() => {
        microsoftTeams.settings.setValidityState(true);
    }
  </script>
</body>

```

Cuando un usuario selecciona **quitar** en el menú desplegable de la pestaña, Microsoft Teams cargará la `removeUrl` Página opcional (designada en la **Página de configuración**) en un iframe. Aquí, se presenta al usuario un botón cargado con la `onClick()` función que llama `microsoftTeams.settings.setValidityState(true)` y habilita el botón **quitar** situado cerca de la parte inferior de la página iframe de eliminación.

Seguir la ejecución del controlador de eliminación `removeEvent.notifySuccess()` o `removeEvent.notifyFailure()` notifica a teams sobre el resultado de la eliminación de contenido.

>[!NOTE]
>Para asegurarse de que no se inhibi el control de un usuario autorizado en una ficha, Microsoft Teams quitará la pestaña tanto en casos correctos como erróneos. \
>Teams habilita el botón **quitar** después de 5 segundos, incluso si la ficha no ha sido llamada `setValidityState()` . \
>Cuando el usuario selecciona **quitar** Teams, la tecla Tab se quita después de 30 segundos, independientemente de si se han completado las acciones.
