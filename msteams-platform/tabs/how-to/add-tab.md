---
title: Ampliar la aplicación de Microsoft Teams con una pestaña personalizada
author: laujan
description: Guía para crear una pestaña
keywords: canal de grupo de pestañas de Teams configurable
ms.topic: conceptual
ms.author: ''
ms.openlocfilehash: 3f3b0ac8bc141672f25d9db2470cb71a856e0ed8
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675970"
---
# <a name="extend-your-teams-app-with-a-custom-tab"></a>Ampliar la aplicación de Microsoft Teams con una pestaña personalizada

Las pestañas personalizadas permiten servir contenido web que se hospeda en el canal, el chat en grupo y los usuarios personales. En un nivel alto, deberá completar los siguientes pasos para crear una pestaña:

1. Prepare el entorno de desarrollo.
1. Cree su página o páginas.
1. Hospedar el servicio de aplicaciones.
1. Crear el paquete de la aplicación y cargarlo en Microsoft Teams.

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-pages"></a>Crear las páginas

Si presenta su pestaña dentro del ámbito personal o de canal o grupo, estará compuesto por una o más páginas HTML hospedadas. Las pestañas con un ámbito personal constan de una sola página de contenido, mientras que las pestañas con un ámbito de canal o de grupo requerirán una página de configuración que establezca la dirección URL de la página de contenido en función de los datos introducidos por el usuario en el momento de la instalación.

Hay tres tipos de páginas de ficha. Consulte la página de documentación correspondiente para obtener detalles completos sobre cómo crearlos.

1. [Página de contenido](~/tabs/how-to/create-tab-pages/content-page.md), la página que se muestra en una pestaña.
1. Página de [configuración](~/tabs/how-to/create-tab-pages/configuration-page.md), la página utilizada para establecer o actualizar la dirección URL de la página de contenido y agregarla a una ficha canal o grupo.
1. [Página de eliminación](~/tabs/how-to/create-tab-pages/removal-page.md), una página opcional que se muestra cuando se quita una ficha de canal o de grupo.

### <a name="tab-requirements"></a>Requisitos de la pestaña

Independientemente del tipo de página, la pestaña tendrá que cumplir con los siguientes requisitos:

* Debe permitir que las páginas se sirvan en un IFrame, a través de los encabezados de respuesta HTTP X-Frame-Options o Content-Security-Policy.

* Por lo general, como protección contra clics, las páginas de inicio de sesión no se representan en IFrames. Por lo tanto, la lógica de autenticación debe usar un método que no sea Redirect (por ejemplo, usar autenticación basada en tokens o basada en cookies).

> [!NOTE]
> Chrome 80, programado para su lanzamiento en principios de 2020, presenta nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. *Consulte* [SameSite cookie Attribute (2020 Update)](../../resources/samesite-cookie-update.md).

* Los exploradores cumplen con una restricción de directiva del mismo origen que impide que una página web realice solicitudes a un dominio diferente del que sirvió para una página web. Sin embargo, es posible que deba redirigir la página de contenido o de configuración a otro dominio o subdominio. La lógica de navegación entre dominios debe permitir al cliente de Teams validar el origen con una lista de validDomains estática en el manifiesto de la aplicación al cargar o comunicarse con la pestaña.

* Para crear una experiencia sin problemas, debe aplicar un estilo a las pestañas en función del tema, diseño y propósito del cliente de Microsoft Teams. Normalmente, las pestañas funcionan mejor cuando se crean para solucionar una necesidad específica y se centran en un pequeño conjunto de tareas o en un subconjunto de datos que es relevante para la ubicación del canal de la pestaña.

* En la página de contenido, agregue una referencia al [SDK del cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client) mediante etiquetas de script. Después de cargar la página, realice una llamada `microsoftTeams.initialize()`a. La página no se mostrará si no lo hace.

## <a name="host-your-app-service"></a>Hospedar el servicio de aplicaciones

El contenido debe hospedarse en una dirección URL disponible públicamente disponible mediante HTTPS. Para las pruebas, puede usar un proxy inverso, como [ngrok](https://ngrok.com/), para exponer el puerto local a una dirección URL con conexión a Internet.

## <a name="create-your-app-package-with-app-studio"></a>Crear el paquete de la aplicación con App Studio

Puede usar la aplicación de App Studio desde el cliente de Microsoft Teams para ayudar a crear el manifiesto de la aplicación. Si no tiene instalado App Studio en Microsoft Teams, seleccione **** ![aplicación](/microsoftteams/platform/assets/images/tab-images/storeApp.png) de la tienda de aplicaciones en la esquina inferior izquierda de la aplicación Teams y busque App Studio. Una vez que encuentre el icono, selecciónelo y elija instalar en el cuadro de diálogo ventana emergente.

1. Abrir el cliente de Microsoft Teams: el uso de la [versión basada en Web](https://teams.microsoft.com) le permitirá inspeccionar el código Front-end con las [herramientas de desarrollo](~/tabs/how-to/developer-tools.md)de su explorador.
1. Abra App Studio y seleccione la pestaña **Editor de manifiestos** .
1. Elija el icono **crear una nueva aplicación** .
1. Agregue los detalles de la aplicación (vea la [definición del esquema del manifiesto](~/resources/schema/manifest-schema.md) para obtener una descripción completa de cada campo).
1. En la sección capacidades, seleccione **pestañas**.
    * Para una pestaña personal, elija *Agregar una pestaña personal* y seleccione **Agregar**. Aparecerá una ventana de cuadro de diálogo emergente en la que podrá agregar los detalles de su pestaña.
    * Para una ficha canal/grupo, en la *ficha equipo* , seleccione **Agregar** y rellene los campos detalles de la pestaña en la ventana emergente de la pestaña equipo. Asegúrese de que la *configuración puede actualizarse. *Los cuadros equipo y *grupo de chat* están seleccionados y seleccione **Guardar**.
1. En la sección *dominios y permisos* , los *dominios del campo de pestañas* deben contener la dirección URL de proxy o host inverso sin el prefijo https.
1. En la pestaña **Finalizar** => **prueba y distribución** puede **Descargar** el paquete de la aplicación, **instalar** el paquete en un equipo o **enviarlo** a la tienda de aplicaciones de Microsoft Teams para su aprobación. *Si usa un proxy inverso, recibirá una advertencia en el campo **Descripción** de la derecha. Se puede omitir la advertencia mientras se prueba la pestaña*.

## <a name="create-your-app-package-manually"></a>Crear el paquete de la aplicación manualmente

Al igual que con los bots y las extensiones de mensajería, se actualiza el manifiesto de la [aplicación](~/resources/schema/manifest-schema.md) para incluir las propiedades de la pestaña. Estas propiedades rigen los ámbitos en los que está disponible la pestaña, las direcciones URL que se usarán y otras propiedades.

### <a name="personal-tabs"></a>Pestañas personales

El contenido que se muestra para las pestañas personales es el mismo para todos los usuarios `staticTabs` y está configurado en la matriz. Puede declarar hasta dieciséis (16) pestañas personales en una aplicación.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`entityId`|String|64 caracteres|✔|Un identificador único para la entidad que muestra la pestaña.|
|`name`|String|128 caracteres|✔|El nombre para mostrar de la pestaña en la interfaz de canal.|
|`contentUrl`|String|2048 caracteres|✔|Dirección URL de https://que señala a la interfaz de usuario de la entidad que se va a mostrar en el lienzo de Microsoft Teams.|
|`websiteUrl`|String|2048 caracteres||La dirección URL de https://para apuntar a si un usuario opta por verlo en un explorador.|
|`scopes`|Matriz de enum|1 |✔|Las pestañas estáticas `personal` solo admiten el ámbito, lo que significa que solo se puede aprovisionar como parte de una aplicación personal.|

#### <a name="simple-personal-tab-manifest-example"></a>Ejemplo de manifiesto de ficha personal simple

El siguiente ejemplo muestra solo la `staticTabs` matriz de un manifiesto de la aplicación.

```json
...
"staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name for tab",
      "contentUrl": "https:// yourURL.com/content ",
      "websiteUrl": "https://yourURL.com/website",
      "scopes": [ "personal" ]
    }
...
```

### <a name="channelgroup-tabs"></a>Fichas canal/grupo

Las fichas canal/grupo se agregan `configurableTabs` en la matriz. Solo puede declarar una ficha de canal o de grupo en `configurableTabs` la matriz.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`configurationUrl`|String|2048 caracteres|✔|La dirección URL de https://a la página de configuración.|
|`canUpdateConfiguration`|Boolean|||Un valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de crearla. Predeterminada`true`|
|`scopes`|Matriz de enum|1 |✔|Las pestañas configurables solo admiten los `team` ámbitos y `groupchat` . |

#### <a name="simple-channelgroup-tab-manifest-example"></a>Ejemplo de manifiesto de ficha de grupo/canal simple

El siguiente ejemplo muestra solo la `configurableTabs` matriz de un manifiesto de la aplicación.

```json
...
"configurableTabs": [
    {
      "configurationUrl": "https://yourURL.com/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
...
```

Una vez que haya completado `manifest.json` el empaquetamiento del paquete en una carpeta ZIP junto con los dos iconos necesarios.

### <a name="upload-app-package-directly-to-a-team"></a>Cargar el paquete de la aplicación directamente a un equipo

1. Abra el cliente de Microsoft Teams. Si usa la [versión basada en Web](https://teams.microsoft.com) , puede inspeccionar el código Front-end con las [herramientas de desarrollo](~/tabs/how-to/developer-tools.md)de su explorador.
1. En el panel de *YourTeams* de la izquierda, seleccione `...` el menú situado junto al equipo que está usando para probar la pestaña y elija **administrar equipo**.
1. En el panel principal, seleccione **aplicaciones** en la barra de pestañas y elija **cargar una aplicación personalizada** ubicada en la esquina inferior derecha de la página.
1. Abra el directorio del proyecto, vaya a la carpeta **./Package** , seleccione la carpeta ZIP del paquete de la aplicación y elija **abrir**. La pestaña se cargará en Teams.

### <a name="view-your-tab-in-teams"></a>Ver la pestaña en Teams

1. Ver su pestaña personal:
    * En la barra de exploración situada en el extremo izquierdo del cliente de Microsoft Teams `...` , seleccione el menú y elija la aplicación en la lista.

1. Ver la ficha canal o Grupo:
    * Vuelva a su equipo, elija el canal en el que desea mostrar la pestaña, seleccione ➕ de la barra de pestañas y elija la pestaña de la galería.
    * Siga las instrucciones para agregar una pestaña. tenga en cuenta que hay un cuadro de diálogo de configuración personalizada para la ficha canal o grupo. Seleccione **Guardar** y la pestaña se agregará a la barra de pestañas del canal.

## <a name="learn-more"></a>Más información

* [Crear una página de contenido para la pestaña](~/tabs/how-to/create-tab-pages/content-page.md)
* [Crear una página de configuración para la pestaña](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [Actualizar o quitar una pestaña](~/tabs/how-to/create-tab-pages/removal-page.md)
