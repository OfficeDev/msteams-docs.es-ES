---
title: Creación de una etiqueta de eliminación
author: surbhigupta
description: Cómo crear una página de eliminación de pestañas
keywords: Teams tabs group channel configurable remove delete
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: fbff927687fd19de273ef801ef34e77dda7a83a5
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452728"
---
# <a name="create-a-removal-page"></a>Crear una página de eliminación

Puedes ampliar y mejorar la experiencia del usuario si admites opciones de eliminación y modificación en la aplicación. Teams permite a los usuarios cambiar el nombre o quitar una pestaña de canal o grupo y puede permitir que los usuarios vuelvan a configurar la pestaña después de la instalación. Además, la experiencia de eliminación de pestañas proporciona a los usuarios opciones posteriores a la eliminación para eliminar o archivar contenido.

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Habilitar la pestaña para volver a configurarse después de la instalación

El **archivo manifest.json** define las características y capacidades de la pestaña. La propiedad de instancia `canUpdateConfiguration` de tabulación toma un valor booleano que indica si un usuario puede modificar o volver a configurar la pestaña después de crearla. En la tabla siguiente se proporcionan los detalles de la propiedad:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`canUpdateConfiguration`|Booleano|||Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña tras su creación. El valor predeterminado es `true`. |

Cuando la pestaña se carga en un canal o chat de grupo, Teams un menú desplegable con el botón secundario del ratón para la pestaña. Las opciones disponibles están determinadas por la `canUpdateConfiguration` configuración. En la tabla siguiente se proporcionan los detalles de configuración:

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Configuraciones            |   √    |       |La `configurationUrl` página se vuelve a cargar en un IFrame que permite al usuario volver a configurar la pestaña. |
|     Cambiar nombre              |   √    |   √   | El usuario puede cambiar el nombre de la pestaña tal como aparece en la barra de pestañas.          |
|     Eliminar               |   √    |   √   |  Si la `removeURL` propiedad y el valor se incluyen en la página **de** configuración, la página de eliminación se carga en un IFrame y se presenta al usuario. Si no se incluye una página de eliminación, se muestra al usuario un cuadro de diálogo de confirmación.          |

## <a name="create-a-tab-removal-page-for-your-application"></a>Crear una página de eliminación de pestañas para la aplicación

La página de eliminación opcional es una página HTML que hospeda y se muestra cuando se quita la pestaña. La dirección URL de la página de eliminación la designa el método `setSettings()` dentro de la página de configuración. Al igual que con todas las páginas de la aplicación, la página de eliminación debe cumplir los [requisitos previos Teams pestaña.](../../../tabs/how-to/tab-requirements.md)

### <a name="register-a-remove-handler"></a>Registrar un controlador de eliminación

Opcionalmente, dentro de la lógica de la página de eliminación, puede invocar `registerOnRemoveHandler((RemoveEvent) => {}` el controlador de eventos cuando el usuario quita una configuración de pestaña existente. El método toma la interfaz [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) y ejecuta el código en el controlador cuando un usuario intenta quitar contenido. El método se usa para realizar operaciones de limpieza, como quitar el recurso subyacente que activa el contenido de la pestaña. A la vez, solo se puede registrar un controlador de eliminación.

La `RemoveEvent` interfaz describe un objeto con dos métodos:

* La `notifySuccess()` función es necesaria. Indica que la eliminación del recurso subyacente se ha hecho correctamente y se puede quitar su contenido.

* La `notifyFailure(string)` función es opcional. Indica que se ha fallado la eliminación del recurso subyacente y que no se puede quitar su contenido. El parámetro de cadena opcional especifica un motivo del error. Si se proporciona, esta cadena se muestra al usuario; si no se muestra un error genérico.

#### <a name="use-the-getsettings-function"></a>Usar la `getSettings()` función

Puede usar para `getSettings()`asignar el contenido de la pestaña que se va a quitar. La `getSettings((Settings) =>{})` función toma el y [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) proporciona los valores de propiedad de configuración válidos que se pueden recuperar.

#### <a name="use-the-getcontext-function"></a>Usar la `getContext()` función

Puede usar para `getContext()` obtener el contexto actual en el que se está ejecutando el marco. La `getContext((Context) =>{})` función toma el [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true). La función proporciona valores de `Context` propiedad válidos que puede usar en la lógica de la página de eliminación para determinar el contenido que se va a mostrar en la página de eliminación.

#### <a name="include-authentication"></a>Incluir autenticación

La autenticación es necesaria antes de permitir que un usuario elimine el contenido de la pestaña. La información de contexto se puede usar para ayudar a construir solicitudes de autenticación y direcciones URL de página de autorización. Consulte [Microsoft Teams de autenticación para las pestañas](~/tabs/how-to/authentication/auth-flow-tab.md). Asegúrese de que todos los dominios usados en las páginas de pestañas se enumeran en la `manifest.json` `validDomains` matriz.

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

Cuando un usuario selecciona **Quitar** del menú desplegable de la pestaña, `removeUrl` Teams carga la página opcional asignada en la página de **configuración, en** un IFrame. Se muestra al usuario un botón cargado con `onClick()` `microsoftTeams.settings.setValidityState(true)` la función que llama y habilita el **botón** Quitar que se muestra en la parte inferior de la página de eliminación IFrame.

Después de ejecutar el controlador de eliminación o `removeEvent.notifySuccess()` `removeEvent.notifyFailure()` notificar Teams el resultado de eliminación de contenido.

>[!NOTE]
>
> * Para asegurarse de que no se inhiba el control de un usuario autorizado sobre una pestaña, Teams elimina la pestaña en los casos de éxito y error.
> * Después de invocar el controlador `registerOnRemoveHandler` de eventos, tendrás 15 segundos para responder al método. De forma predeterminada, Teams el **botón Quitar** después de cinco segundos, incluso si no llama a `setValidityState(true)`.
> * Cuando el usuario selecciona **Quitar**, Teams la pestaña después de 30 segundos, independientemente de si las acciones se han completado o no.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>Vea también

* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
* [Creación de una página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md)
