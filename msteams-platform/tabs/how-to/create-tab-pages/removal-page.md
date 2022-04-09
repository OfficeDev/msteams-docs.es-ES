---
title: Creación de una etiqueta de eliminación
author: surbhigupta
description: Cómo crear una página de eliminación de pestañas
keywords: Eliminación de eliminación configurable del canal de grupo de pestañas de teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: ea29959bf79b5e46e876f75570dcb437fa56888f
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2022
ms.locfileid: "64736867"
---
# <a name="create-a-removal-page"></a>Crear una página de eliminación

Puede ampliar y mejorar la experiencia del usuario si admite las opciones de eliminación y modificación en la aplicación. Teams permite a los usuarios cambiar el nombre o quitar una pestaña de canal o grupo y puede permitir que los usuarios vuelvan a configurar la pestaña después de la instalación. Además, la experiencia de eliminación de pestañas proporciona a los usuarios opciones posteriores a la eliminación para eliminar o archivar contenido.

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Habilitación de la pestaña para volver a configurarla después de la instalación

Define `manifest.json` las características y funcionalidades de la pestaña. La propiedad tab instance `canUpdateConfiguration` toma un valor booleano que indica si un usuario puede modificar o volver a configurar la pestaña después de crearla. En la tabla siguiente se proporcionan los detalles de la propiedad:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`canUpdateConfiguration`|Booleano|||Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña tras su creación. El valor predeterminado es `true`. |

Cuando la pestaña se carga en un canal o chat de grupo, Teams agrega un menú desplegable con el botón derecho para la pestaña. La configuración determina las `canUpdateConfiguration` opciones disponibles. En la tabla siguiente se proporcionan los detalles de la configuración:

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Configuraciones            |   √    |       |La `configurationUrl` página se vuelve a cargar en un IFrame, lo que permite al usuario volver a configurar la pestaña. |
|     Cambiar nombre              |   √    |   √   | El usuario puede cambiar el nombre de la pestaña tal como aparece en la barra de pestañas.          |
|     Eliminar               |   √    |   √   |  Si la propiedad y el  `removeURL` valor se incluyen en la **página de configuración**, la **página de eliminación** se carga en un IFrame y se presenta al usuario. Si no se incluye una página de eliminación, se muestra al usuario un cuadro de diálogo de confirmación.          |

## <a name="create-a-tab-removal-page-for-your-application"></a>Crear una página de eliminación de pestañas para la aplicación

La página de eliminación opcional es una página HTML que se hospeda y se muestra cuando se quita la pestaña. La dirección URL de la página de eliminación se designa mediante el método dentro de la `setSettings()` página de configuración. Al igual que con todas las páginas de la aplicación, la página de eliminación debe cumplir Teams [requisitos previos de tabulación](../../../tabs/how-to/tab-requirements.md).

### <a name="register-a-remove-handler"></a>Registro de un controlador de eliminación

Opcionalmente, dentro de la lógica de la página de eliminación, puede invocar el `registerOnRemoveHandler((RemoveEvent) => {}` controlador de eventos cuando el usuario quita una configuración de pestaña existente. El método toma la [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) interfaz y ejecuta el código en el controlador cuando un usuario intenta quitar contenido. El método se usa para realizar operaciones de limpieza, como quitar el recurso subyacente que alimenta el contenido de la pestaña. A la vez, solo se puede registrar un controlador de eliminación.

La `RemoveEvent` interfaz describe un objeto con dos métodos:

* La `notifySuccess()` función es necesaria. Indica que la eliminación del recurso subyacente se realizó correctamente y que se puede quitar su contenido.

* La `notifyFailure(string)` función es opcional. Indica que se produjo un error en la eliminación del recurso subyacente y que no se puede quitar su contenido. El parámetro de cadena opcional especifica un motivo para el error. Si se proporciona, esta cadena se muestra al usuario; De lo contrario, se muestra un error genérico.

#### <a name="use-the-getsettings-function"></a>Uso de la `getSettings()` función

Puede usar `getSettings()`para asignar el contenido de la pestaña que se va a quitar. La `getSettings((Settings) =>{})` función toma y [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) proporciona los valores de propiedad de configuración válidos que se pueden recuperar.

#### <a name="use-the-getcontext-function"></a>Uso de la `getContext()` función

Puede usar `getContext()` para obtener el contexto actual en el que se ejecuta el marco. La `getContext((Context) =>{})` función toma .[`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) La función proporciona valores de propiedad válidos `Context` que puede usar en la lógica de página de eliminación para determinar el contenido que se va a mostrar en la página de eliminación.

#### <a name="include-authentication"></a>Incluir autenticación

La autenticación es necesaria antes de permitir que un usuario elimine el contenido de la pestaña. La información de contexto se puede usar para ayudar a construir solicitudes de autenticación y direcciones URL de página de autorización. Consulte [Microsoft Teams flujo de autenticación para ver las pestañas](~/tabs/how-to/authentication/auth-flow-tab.md). Asegúrese de que todos los dominios usados en las páginas de pestaña aparecen en la `manifest.json` `validDomains` matriz.

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

Cuando un usuario selecciona **Quitar** en el menú desplegable de la pestaña, Teams carga la página opcional `removeUrl` asignada en la **página de configuración** en un IFrame. Al usuario se le muestra un botón cargado con la `onClick()` función que llama `microsoftTeams.settings.setValidityState(true)` a y habilita el botón **Quitar** que se muestra en la parte inferior de la página de eliminación IFrame.

Una vez que se ejecuta el controlador de eliminación, `removeEvent.notifySuccess()` o `removeEvent.notifyFailure()` notifica a Teams el resultado de la eliminación de contenido.

>[!NOTE]
>
> * Para asegurarse de que no se inhiba el control de un usuario autorizado sobre una pestaña, Teams quita la pestaña en casos de éxito y errores.
> * Después de invocar el `registerOnRemoveHandler` controlador de eventos, tendrá 15 segundos para responder al método . De forma predeterminada, Teams habilita el botón **Quitar** después de cinco segundos, incluso si no llama a `setValidityState(true)`.
> * Cuando el usuario selecciona **Quitar**, Teams quita la pestaña después de 30 segundos, independientemente de si las acciones se han completado o no.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>Consulte también

* [pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
* [Creación de una página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md)
