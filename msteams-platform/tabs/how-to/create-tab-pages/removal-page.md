---
title: Creación de una etiqueta de eliminación
author: surbhigupta
description: En este módulo, aprenderá a crear una página de eliminación de pestañas y a habilitar la pestaña para volver a configurarla después de la instalación.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: cc2d08176d4da365eac9d5a5fd48ff53dbf84461
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2022
ms.locfileid: "66485219"
---
# <a name="tab-re-configuration-and-removal-page"></a>Página de re-configuración y eliminación de pestañas

Puedes ampliar y mejorar la experiencia del usuario admitiendo opciones de eliminación y modificación en la aplicación. Teams permite a los usuarios cambiar el nombre o quitar una pestaña de canal o grupo y puede permitir que los usuarios vuelvan a configurar la pestaña después de la instalación. Además, la experiencia de eliminación de pestañas proporciona a los usuarios opciones posteriores a la eliminación para eliminar o archivar contenido.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Habilitar la pestaña para que se vuelva a configurar después de la instalación

El `manifest.json` define las características y funcionalidades de la pestaña. La propiedad de instancia `canUpdateConfiguration` de pestaña toma un valor booleano que indica si un usuario puede modificar o volver a configurar la pestaña después de crearla. En la tabla siguiente se proporcionan los detalles de la propiedad:

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`canUpdateConfiguration`|Booleano|||El valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de la creación. El valor predeterminado es `true`. |

Cuando la pestaña se carga en un canal o chat de grupo, Teams agrega un menú desplegable con el botón derecho para la pestaña. Las opciones disponibles vienen determinadas por la configuración `canUpdateConfiguration`. En la tabla siguiente se proporcionan los detalles de configuración:

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Configuración            |   √    |       |La página `configurationUrl` se vuelve a cargar en un IFrame, lo que permite al usuario volver a configurar la pestaña. |
|     Cambiar nombre              |   √    |   √   | El usuario puede cambiar el nombre de la pestaña tal como aparece en la barra de pestañas.          |
|     Eliminar               |   √    |   √   |  Si la propiedad `removeURL` se incluyen en la **página de configuración**, la página **removal** se carga en un IFrame y se presenta al usuario. Si no se incluye una página de eliminación, se muestra al usuario un cuadro de diálogo de confirmación.          |

## <a name="create-a-tab-removal-page-for-your-application"></a>Crear una página de eliminación de pestañas para la aplicación

La página de eliminación opcional es una página HTML que hospeda y se muestra cuando se quita la pestaña. La dirección URL de la página de eliminación se designa mediante el `setConfig()` método (anteriormente `setSettings()`) dentro de la página de configuración. Al igual que con todas las páginas de la aplicación, la página de eliminación debe cumplir los [requisitos previos de la pestaña Equipos](../../../tabs/how-to/tab-requirements.md).

### <a name="register-a-remove-handler"></a>Registrar un controlador de eliminación

Opcionalmente, dentro de la lógica de la página de eliminación, puede invocar el `registerOnRemoveHandler((RemoveEvent) => {}` controlador de eventos cuando el usuario quita una configuración de pestaña existente. El método toma la interfaz [`RemoveEvent`](/javascript/api/@microsoft/teams-js/pages.config.removeevent?view=msteams-client-js-latest&preserve-view=true) y ejecuta el código en el controlador cuando un usuario intenta quitar contenido. El método se usa para realizar operaciones de limpieza, como quitar el recurso subyacente que alimenta el contenido de la pestaña. A la vez, solo se puede registrar un controlador de eliminación.

La interfaz `RemoveEvent` describe un objeto con dos métodos:

* Se requiere la función `notifySuccess()`. Indica que la eliminación del recurso subyacente se realizó correctamente y que se puede quitar su contenido.

* La función `notifyFailure(string)` es opcional. Indica que se produjo un error en la eliminación del recurso subyacente y que no se puede quitar su contenido. El parámetro de cadena opcional especifica un motivo del error. Si se proporciona, esta cadena se muestra al usuario; de lo contrario, se muestra un error genérico.

#### <a name="use-the-getconfig-function"></a>Use la función `getConfig()`

Puede usar `getConfig()` (anteriormente `getSettings()`) para asignar el contenido de la pestaña que se va a quitar. La `getConfig()` función devuelve una promesa que se resuelve con el objeto Config y proporciona los valores de propiedad de configuración válidos que se pueden recuperar.

#### <a name="use-the-getcontext-function"></a>Use la función `getContext()`

Puede usar `getContext()` para obtener el contexto actual en el que se ejecuta el marco. La `getContext()` función devuelve una promesa que se resolverá con el objeto Context. El objeto Context proporciona valores de propiedad válidos `Context` que puede usar en la lógica de página de eliminación para determinar el contenido que se va a mostrar en la página de eliminación.

#### <a name="include-authentication"></a>Incluir autenticación

Se requiere autenticación antes de permitir que un usuario elimine el contenido de la pestaña. La información de contexto se puede usar para ayudar a construir solicitudes de autenticación y direcciones URL de página de autorización. Consultar [Flujo de autenticación de Microsoft Teams para pestañas](~/tabs/how-to/authentication/auth-flow-tab.md) Asegúrese de que todos los dominios usados en las páginas de pestañas aparecen en la matriz `manifest.json` y `validDomains`.

A continuación se muestra un bloque de código de eliminación de pestañas de ejemplo:

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    app.initialize();
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

Cuando un usuario selecciona **Quitar** en el menú desplegable de la pestaña, Teams carga la página opcional `removeUrl` asignada en la **configuración**, en un IFrame. Se muestra al usuario un botón cargado con la función `onClick()` que llama a `pages.config.setValidityState(true)` y habilita el botón **Quitar** que se muestra en la parte inferior del IFrame de la página de eliminación.

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
