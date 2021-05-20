---
title: Creación de una etiqueta de eliminación
author: laujan
description: Cómo crear una página de eliminación de pestañas
keywords: equipos pestañas canal de grupo configurable eliminar eliminar
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: e1a1f38a2bcb3b5bc4bc54f469c8727e44d8695e
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566673"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>Modificar o eliminar una pestaña de grupo de canales

Puede ampliar y mejorar la experiencia del usuario mediante la compatibilidad con las opciones de eliminación y modificación en la aplicación. Teams permite a los usuarios cambiar el nombre o quitar una pestaña de canal/grupo y puede permitir que los usuarios reconfiguran la pestaña después de la instalación. Además, la experiencia de eliminación de pestañas puede incluir la des designador lo que sucede con el contenido cuando se quita la pestaña o dar a los usuarios opciones posteriores a la eliminación, como eliminar o archivar el contenido.

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Habilite la pestaña para que se reconfigure después de la instalación

El **manifest.jsdefine** las características y capacidades de la pestaña. La propiedad tab instance `canUpdateConfiguration` toma un valor booleano que indica si un usuario puede modificar o volver a configurar la pestaña después de crearla:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`canUpdateConfiguration`|Booleano|||Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de la creación. predeterminado: `true`|

Cuando la pestaña se carga en un canal o chat de grupo, Teams agregará un menú desplegable con el botón derecho del ratón para la pestaña. Las opciones disponibles están determinadas por la `canUpdateConfiguration` configuración:

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Configuración            |   √    |       |La `configurationUrl` página se vuelve a cargar en un IFrame que permite al usuario reconfigurar la pestaña.  |
|     Cambiar nombre              |   √    |   √   | El usuario puede cambiar el nombre de la pestaña tal como aparece en la barra de pestañas.          |
|     Eliminar               |   √    |   √   |  Si la  `removeURL` propiedad y el valor se incluyen en la página de **configuración,** la **página de eliminación** se carga en un IFrame y se presenta al usuario. Si no se incluye una página de eliminación, el usuario se presenta con un cuadro de diálogo confirmar.          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>Cree una página de eliminación de pestañas para la aplicación

La página de eliminación opcional es una página HTML que hospeda y se muestra cuando se quita la pestaña. La dirección URL de la página de eliminación se designa mediante el `setSettings()` método dentro de la página de configuración. Al igual que con todas las páginas de la aplicación, la página de eliminación debe cumplir con [los requisitos de Teams pestaña.](../../../tabs/how-to/tab-requirements.md)

### <a name="register-a-remove-handler"></a>Registrar un controlador remove

Opcionalmente, dentro de la lógica de la página de eliminación, puede invocar el `registerOnRemoveHandler((RemoveEvent) => {}` controlador de eventos cuando el usuario quita una configuración de pestaña existente. El método toma la [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) interfaz y ejecuta el código en el controlador cuando un usuario intenta quitar contenido. Se utiliza para realizar operaciones de limpieza, como quitar el recurso subyacente que alimenta el contenido de la pestaña. Solo se puede registrar un controlador remove a la vez.

La `RemoveEvent` interfaz describe un objeto con dos métodos:

* Se `notifySuccess()` requiere la función. Indica que la eliminación del recurso subyacente se realizó correctamente y se puede quitar su contenido.

* La `notifyFailure(string)` función es opcional. Indica que se ha fallado en la eliminación del recurso subyacente y no se puede quitar su contenido. El parámetro de cadena opcional especifica un motivo del error. Si se proporciona, esta cadena se muestra al usuario; de lo contrario, se muestra un error genérico.

#### <a name="use-the-getsettings-function"></a>Utilice la `getSettings()` función

Puede utilizar `getSettings()` para designar el contenido de la pestaña que se va a quitar. La `getSettings((Settings) =>{})` función toma y proporciona los valores de propiedad de configuración [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) válidos que se pueden recuperar.

#### <a name="use-the-getcontext-function"></a>Utilice la `getContext()` función

Puede usar `getContext()` para recuperar el contexto actual en el que se ejecuta el marco. La `getContext((Context) =>{})` función toma y proporciona valores de propiedad [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) válidos que puede usar en la lógica `Context` de la página de eliminación para determinar el contenido que se mostrará en la página de eliminación.

#### <a name="include-authentication"></a>Incluir autenticación

Es posible que necesite autenticación antes de permitir que un usuario elimine el contenido de la pestaña. La información de contexto se puede usar para ayudar a construir solicitudes de autenticación y direcciones URL de página de autorización. Consulte [Microsoft Teams flujo de autenticación para las pestañas](~/tabs/how-to/authentication/auth-flow-tab.md). Asegúrese de que todos los dominios utilizados en las páginas de pestañas aparecen en la `manifest.json` `validDomains` matriz.

A continuación se muestra un bloque de código de eliminación de pestañas de ejemplo:

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

Cuando un usuario selecciona **Quitar** en el menú desplegable de la pestaña, Teams cargará la página opcional `removeUrl` (designada en la **página de configuración)** en un IFrame. Aquí, el usuario se presenta con un botón cargado con la `onClick()` función que llama y `microsoftTeams.settings.setValidityState(true)` habilita el botón **Quitar** situado cerca de la parte inferior de la página de eliminación IFrame.

Después de la ejecución del controlador remove, `removeEvent.notifySuccess()` o `removeEvent.notifyFailure()` notifica Teams del resultado de eliminación de contenido.

>[!NOTE]
> * Para asegurarse de que no se inhibe el control de un usuario autorizado sobre una pestaña, Teams quitará la pestaña tanto en casos de éxito como de error.\
> * Teams activa el botón **Quitar** después de 5 segundos, incluso si la pestaña no ha llamado `setValidityState()` a .\
> * Cuando el usuario selecciona **Quitar** Teams quita la pestaña después de 30 segundos, independientemente de si las acciones se han completado.
