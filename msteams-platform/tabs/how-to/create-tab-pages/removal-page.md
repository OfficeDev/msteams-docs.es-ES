---
title: Creación de una etiqueta de eliminación
author: surbhigupta
description: Aprenda a habilitar la pestaña para volver a configurarla después de la instalación. Amplíe la experiencia del usuario admitiendo las opciones de eliminación y modificación en la aplicación Microsoft Teams.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 40d6024d01b608c99347e9df65883906d7cb276d
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560452"
---
# <a name="create-a-removal-page"></a>Crear una página de eliminación

Puedes ampliar y mejorar la experiencia del usuario admitiendo opciones de eliminación y modificación en la aplicación. Teams permite a los usuarios cambiar el nombre o quitar una pestaña de canal o grupo y puede permitir que los usuarios vuelvan a configurar la pestaña después de la instalación. Además, la experiencia de eliminación de pestañas proporciona a los usuarios opciones posteriores a la eliminación para eliminar o archivar contenido.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Habilitar la pestaña para que se vuelva a configurar después de la instalación

El `manifest.json` define las características y funcionalidades de la pestaña. La propiedad de instancia `canUpdateConfiguration` de pestaña toma un valor booleano que indica si un usuario puede modificar o volver a configurar la pestaña después de crearla. En la tabla siguiente se proporcionan los detalles de la propiedad:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`canUpdateConfiguration`|Booleano|||Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña tras su creación. El valor predeterminado es `true`. |

Cuando la pestaña se carga en un canal o chat de grupo, Teams agrega un menú desplegable con el botón derecho para la pestaña. Las opciones disponibles vienen determinadas por la configuración `canUpdateConfiguration`. En la tabla siguiente se proporcionan los detalles de configuración:

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Configuración            |   √    |       |La `configurationUrl` página se vuelve a cargar en un iFrame, lo que permite al usuario volver a configurar la pestaña. |
|     Cambiar nombre              |   √    |   √   | El usuario puede cambiar el nombre de la pestaña tal como aparece en la barra de pestañas.          |
|     Eliminar               |   √    |   √   |  Si la propiedad y el  `removeURL` valor se incluyen en la **página de configuración**, la **página de eliminación** se carga en un iFrame y se presenta al usuario. Si no se incluye una página de eliminación, se muestra al usuario un cuadro de diálogo de confirmación.          |

## <a name="create-a-tab-removal-page-for-your-application"></a>Crear una página de eliminación de pestañas para la aplicación

La página de eliminación opcional es una página HTML que hospeda y se muestra cuando se quita la pestaña. La dirección URL de la página de eliminación se designa mediante el `setConfig()` método (o `setSettings()` antes de TeamsJS v.2.0.0) dentro de la página de configuración. Al igual que con todas las páginas de la aplicación, la página de eliminación debe cumplir los [requisitos previos de la pestaña Equipos](../../../tabs/how-to/tab-requirements.md).

### <a name="register-a-remove-handler"></a>Registrar un controlador de eliminación

Opcionalmente, dentro de la lógica de la página de eliminación, puede invocar el `registerOnRemoveHandler((RemoveEvent) => {}` controlador de eventos cuando el usuario quita una configuración de pestaña existente. El método toma la interfaz [`RemoveEvent`](/javascript/api/@microsoft/teams-js/pages.config.removeevent?view=msteams-client-js-latest&preserve-view=true) y ejecuta el código en el controlador cuando un usuario intenta quitar contenido. El método se usa para realizar operaciones de limpieza, como quitar el recurso subyacente que alimenta el contenido de la pestaña. A la vez solo se puede registrar un controlador de eliminación.

La interfaz `RemoveEvent` describe un objeto con dos métodos:

* Se requiere la función `notifySuccess()`. Indica que la eliminación del recurso subyacente se realizó correctamente y que se puede quitar su contenido.

* La función `notifyFailure(string)` es opcional. Indica que se produjo un error en la eliminación del recurso subyacente y que no se puede quitar su contenido. El parámetro de cadena opcional especifica un motivo del error. Si se proporciona, esta cadena se muestra al usuario; de lo contrario, se muestra un error genérico.

#### <a name="use-the-getconfig-function"></a>Use la función `getConfig()`

Puede usar `getConfig()` (anteriormente `getSettings()`) para asignar el contenido de la pestaña que se va a quitar. La `getConfig()` función devuelve una promesa que se resuelve con el objeto Config y proporciona los valores de propiedad de configuración válidos que se pueden recuperar.

#### <a name="use-the-getcontext-function"></a>Use la función `getContext()`

Puede usar `getContext()` para obtener el contexto actual en el que se ejecuta el marco. La `getContext()` función devuelve una promesa que se resolverá con el objeto Context. El objeto Context proporciona valores de propiedad válidos `Context` que puede usar en la lógica de página de eliminación para determinar el contenido que se va a mostrar en la página de eliminación.

#### <a name="include-authentication"></a>Incluir autenticación

Se requiere autenticación antes de permitir que un usuario elimine el contenido de la pestaña. La información de contexto se puede usar para ayudar a construir solicitudes de autenticación y direcciones URL de página de autorización. Consultar [Flujo de autenticación de Microsoft Teams para pestañas](~/tabs/how-to/authentication/auth-flow-tab.md) Asegúrese de que todos los dominios usados en las páginas de pestaña aparecen en la `validDomains` matriz del manifiesto de la aplicación.

A continuación se muestra un bloque de código de eliminación de pestañas de ejemplo:

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    await microsoftTeams.app.initialize();
    pages.config.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        const configPromise = pages.getConfig();
        configPromise.
            then((configuration) => {
                configuration.contentUrl = "...";
                removeEvent.notifySuccess()}).
            catch((error) => {removeEvent.notifyFailure("failure message")});
    });

    const onClick() => {
        pages.config.setValidityState(true);
    }
  </script>
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***

Cuando un usuario selecciona **Quitar** en el menú desplegable de la pestaña, Teams carga la página opcional `removeUrl` asignada en la **página de configuración** en un iFrame. Al usuario se le muestra un botón cargado con la `onClick()` función que llama `pages.config.setValidityState(true)` a y habilita el botón **Quitar** que se muestra en la parte inferior de la página de eliminación iFrame.

Después de ejecutar el controlador de eliminación, `removeEvent.notifySuccess()` o `removeEvent.notifyFailure()` notifica a Teams el resultado de la eliminación de contenido.

>[!NOTE]
>
> * Para asegurarse de que no se impide el control de un usuario autorizado sobre una pestaña, Teams quita la pestaña en los casos de éxito y de error.
> * Después de invocar el controlador de eventos `registerOnRemoveHandler`, tendrás 15 segundos para responder al método. De forma predeterminada, Teams habilita el botón **Quitar** después de cinco segundos, incluso si no llama a `setValidityState(true)`.
> * Cuando el usuario selecciona **Quitar**, Teams quita la pestaña después de 30 segundos, independientemente de si las acciones se han completado o no.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>Vea también

* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de grupo o canal personalizado](~/tabs/how-to/create-channel-group-tab.md)
* [Creación de una página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md)
