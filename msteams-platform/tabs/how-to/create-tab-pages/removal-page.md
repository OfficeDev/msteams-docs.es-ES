---
title: Creación de una etiqueta de eliminación
author: laujan
description: Cómo crear una página de eliminación de pestañas
keywords: Teams tabs group channel configurable remove delete
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8f01780dce9aa0450169d4c699471bb2ac5bd9a0
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019590"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>Modificar o quitar una pestaña de grupo de canales

Puedes ampliar y mejorar la experiencia del usuario si admites opciones de eliminación y modificación en la aplicación. Teams permite a los usuarios cambiar el nombre o quitar una pestaña de canal o grupo y puede permitir que los usuarios vuelvan a configurar la pestaña después de la instalación. Además, la experiencia de eliminación de pestañas puede incluir la designación de lo que sucede con el contenido cuando se quita la pestaña o proporcionar a los usuarios opciones posteriores a la eliminación, como eliminar o archivar el contenido.

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Habilitar la pestaña para volver a configurarse después de la instalación

El **manifest.jsen** define las características y capacidades de la pestaña. La propiedad de instancia de tabulación toma un valor booleano que indica si un usuario puede modificar o volver a configurar la `canUpdateConfiguration` pestaña después de crearla:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`canUpdateConfiguration`|Booleano|||Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de su creación. Valor predeterminado: `true`|

Cuando la pestaña se carga en un canal o chat de grupo, Teams agregará un menú desplegable con el botón secundario para la pestaña. Las opciones disponibles están determinadas por la `canUpdateConfiguration` configuración:

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Configuraciones            |   √    |       |La página se vuelve a cargar en un IFrame que permite al usuario volver a `configurationUrl` configurar la pestaña.  |
|     Cambiar nombre              |   √    |   √   | El usuario puede cambiar el nombre de la pestaña tal como aparece en la barra de pestañas.          |
|     Eliminar               |   √    |   √   |  Si la propiedad y el valor se incluyen en la página de configuración, la página de eliminación se carga en un `removeURL` IFrame y se presenta al usuario.   Si no se incluye una página de eliminación, se muestra al usuario un cuadro de diálogo de confirmación.          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>Crear una página de eliminación de pestañas para la aplicación

La página de eliminación opcional es una página HTML que hospeda y se muestra cuando se quita la pestaña. La dirección URL de la página de eliminación la designa `setSettings()` el método dentro de la página de configuración. Al igual que con todas las páginas de la aplicación, la página de eliminación debe cumplir con los requisitos [de pestaña de Teams](../../../tabs/how-to/tab-requirements.md).

### <a name="register-a-remove-handler"></a>Registrar un controlador de eliminación

Opcionalmente, dentro de la lógica de la página de eliminación, puede invocar el controlador de eventos cuando el `registerOnRemoveHandler((RemoveEvent) => {}` usuario quita una configuración de pestaña existente. El método toma la interfaz y ejecuta el código en el controlador cuando un [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) usuario intenta quitar contenido. Se usa para realizar operaciones de limpieza, como quitar el recurso subyacente que activa el contenido de la pestaña. Solo se puede registrar un controlador de eliminación a la vez.

La `RemoveEvent` interfaz describe un objeto con dos métodos:

* La `notifySuccess()` función es necesaria. Indica que la eliminación del recurso subyacente se ha hecho correctamente y se puede quitar su contenido.

* La `notifyFailure(string)` función es opcional. Indica que se ha fallado la eliminación del recurso subyacente y que no se puede quitar su contenido. El parámetro de cadena opcional especifica un motivo del error. Si se proporciona, esta cadena se muestra al usuario; de lo contrario, se muestra un error genérico.

#### <a name="use-the-getsettings-function"></a>Usar la `getSettings()` función

Puede usar para `getSettings()` designar el contenido de la pestaña que se va a quitar. La función toma el y proporciona los valores de propiedad de configuración `getSettings((Settings) =>{})` [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) válidos que se pueden recuperar.

#### <a name="use-the-getcontext-function"></a>Usar la `getContext()` función

Puede usar para `getContext()` recuperar el contexto actual en el que se ejecuta el marco. La función toma los valores de propiedad válidos que puede usar en la lógica de la página de eliminación para determinar el contenido que se va a mostrar `getContext((Context) =>{})` en la página de [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) `Context` eliminación.

#### <a name="include-authentication"></a>Incluir autenticación

Es posible que necesite autenticación antes de permitir que un usuario elimine el contenido de la pestaña. La información de contexto se puede usar para ayudar a construir solicitudes de autenticación y direcciones URL de página de autorización. Consulte [Flujo de autenticación de Microsoft Teams para las pestañas](~/tabs/how-to/authentication/auth-flow-tab.md). Asegúrese de que todos los dominios usados en las páginas de pestañas se enumeran en la `manifest.json` `validDomains` matriz.

A continuación se muestra un bloque de código de eliminación de fichas de ejemplo:

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

Cuando un usuario selecciona **Quitar** del menú desplegable de la pestaña, Teams cargará la página opcional (designada en la página de `removeUrl` configuración) en un IFrame.  Aquí, el usuario se presenta con un botón cargado con la función que llama y habilita el botón Quitar ubicado cerca de la parte inferior de la página `onClick()` `microsoftTeams.settings.setValidityState(true)` de eliminación IFrame. 

Después de la ejecución del controlador de eliminación o `removeEvent.notifySuccess()` notifica a Teams del resultado de `removeEvent.notifyFailure()` eliminación de contenido.

>[!NOTE]
>Para asegurarse de que el control de un usuario autorizado sobre una pestaña no está inhibido, Teams quitará la pestaña en los casos de éxito y error.\
>Teams habilita el **botón Quitar** después de 5 segundos, incluso si la pestaña no ha llamado `setValidityState()` a .\
>Cuando el usuario selecciona **Quitar** Teams quita la pestaña después de 30 segundos, independientemente de si las acciones se han completado.
