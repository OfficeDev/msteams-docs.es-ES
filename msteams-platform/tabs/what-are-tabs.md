---
title: ¿Qué son las pestañas personalizadas en Teams?
author: laujan
description: Información general sobre las pestañas personalizadas en la plataforma de Teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: d72d70ac97a7da427f22ef7e84c73f235dc395c6
ms.sourcegitcommit: f6e4a303828224a702138753a8e5e27c8a094c82
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/24/2021
ms.locfileid: "51176966"
---
# <a name="what-are-microsoft-teams-tabs"></a>¿Qué son las pestañas de Microsoft Teams?

Las pestañas son páginas web para Teams incrustadas en Microsoft Teams. Son etiquetas sencillas html <iframe que apuntan a dominios declarados en el manifiesto de la aplicación y se pueden agregar como parte de un canal dentro de un equipo, chat de grupo o aplicación personal para un usuario \> individual. Puedes incluir pestañas personalizadas con la aplicación para insertar tu propio contenido web en Teams o agregar funcionalidad específica de Teams al contenido web. *Consulte* [SDK de cliente de JavaScript de Teams](/javascript/api/overview/msteams-client).

> [!NOTE]
> Chrome 80, programado para su lanzamiento a principios de 2020, introduce nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. *Consulte* [Atributo de cookie SameSite (actualización de 2020).](../resources/samesite-cookie-update.md)

Hay dos tipos de pestañas disponibles en Teams: canal/grupo y personal. Las pestañas canal o grupo entregan contenido a canales y chats de grupo, y son una excelente forma de crear espacios de colaboración en torno al contenido basado en web dedicado. Las pestañas personales, junto con los bots de ámbito personal, forman parte de aplicaciones personales y están en el ámbito de un solo usuario. Se pueden anclar a la barra de navegación izquierda para facilitar el acceso.

## <a name="lesser-known-tab-features"></a>Características de pestañas menos conocidas

> [!div class="checklist"]
>
> * Si se agrega una pestaña a una aplicación que también tiene un bot, el bot también se agrega al equipo.
> * Reconocimiento del identificador de Azure Active Directory (Azure AD) del usuario actual.
> * Reconocimiento de configuración regional para que el usuario indique el idioma, es decir, `en-us` . 
> * Funcionalidad de inicio de sesión único (SSO), si es compatible.
> * Capacidad de usar bots o notificaciones de aplicaciones para vincular profundamente a la pestaña o a una sub entidad dentro del servicio, por ejemplo, un elemento de trabajo individual.
> * La capacidad de abrir un módulo de tareas desde vínculos dentro de una pestaña.
> * Reutilización de elementos web de SharePoint dentro de la pestaña.

## <a name="tabs-user-scenarios"></a>Escenarios de usuario de pestañas

**Escenario:** Traer un recurso basado en web existente dentro de Teams. \
**Ejemplo:** Creas una pestaña personal en la aplicación de Teams que presenta un sitio web corporativo informativo a los usuarios.

**Escenario:** Agregar páginas de soporte técnico a un bot de Teams o una extensión de mensajería. \
**Ejemplo:** Se crean pestañas personales que proporcionan *información sobre* *el* contenido de la página web y ayudan a los usuarios.

**Escenario:** Proporcionar acceso a elementos con los que los usuarios interactúan regularmente para el diálogo y la colaboración cooperativos. \
**Ejemplo:** Se crea una pestaña de canal o grupo con vínculos profundos a elementos individuales.

## <a name="how-do-tabs-work"></a>¿Cómo funcionan las pestañas?

Se declara una pestaña personalizada en el manifiesto de la aplicación del paquete de la aplicación. Para cada página web que quieras incluir como pestaña en la aplicación, defines una dirección URL y un ámbito. Además, debe agregar el SDK de [cliente de JavaScript de Teams](/javascript/api/overview/msteams-client) a la página y llamar después de que se cargue la `microsoftTeams.initialize()` página. Si lo hace, le dirá a Teams que muestre su página, le dará acceso a información específica de Teams (por ejemplo, si el cliente de Teams ejecuta el tema *oscuro)* y le permitirá realizar acciones en función de los resultados.

Independientemente de si elige exponer la pestaña dentro del ámbito de canal o grupo o personal, deberá presentar una página de contenido HTML de iframe <en \> la pestaña. [](~/tabs/how-to/create-tab-pages/content-page.md) Para las pestañas personales, la dirección URL de contenido se establece directamente en el manifiesto de la aplicación de Teams mediante la `contentUrl` propiedad de la `staticTabs` matriz. El contenido de la pestaña será el mismo para todos los usuarios.

Para las pestañas de canal o grupo, también debe crear una página de configuración adicional que permita a los usuarios configurar la dirección URL de la página de contenido, normalmente mediante parámetros de cadena de consulta url para cargar el contenido adecuado para ese contexto. Esto se debe a que la pestaña canal o grupo se puede agregar a varios equipos o chats de grupo diferentes. En cada instalación posterior, los usuarios podrán configurar la pestaña, lo que le permitirá adaptar la experiencia según sea necesario. Cuando los usuarios agregan o configuran una pestaña, se asocia una dirección URL a la pestaña que se presenta en la interfaz de usuario de Teams. Configurar una pestaña es simplemente agregar parámetros adicionales a esa dirección URL. Por ejemplo, cuando agrega la pestaña Azure Boards, la página de configuración le permite elegir qué placa se cargará la pestaña. La dirección URL de la página de configuración la especifica la  `configurationUrl` propiedad en la `configurableTabs` matriz del manifiesto de la aplicación.

Puedes tener varios canales o pestañas de grupo y hasta dieciséis pestañas personales por aplicación.

## <a name="mobile-clients"></a>Clientes móviles

Si decide que la pestaña canal o grupo aparezca en los clientes móviles de Teams, la configuración `setSettings()` debe tener un valor para la `websiteUrl` propiedad. Para garantizar una experiencia de usuario óptima, debe seguir las instrucciones para las [pestañas](~/tabs/design/tabs-mobile.md) en el móvil al crear las pestañas. Las aplicaciones [distribuidas a través de Appsource](~/concepts/deploy-and-publish/appsource/publish.md) tienen un proceso de aprobación independiente para clientes móviles. El comportamiento predeterminado de estas aplicaciones es el siguiente:

| **Tipo de tabulación** | **Comportamiento de la aplicación si está optimizada para clientes móviles** | **Comportamiento de la aplicación si no está optimizada para clientes móviles** |
|:-----|:-----|:-----|
| **Pestañas estáticas** o **pestañas personales**|La aplicación aparece en la barra inferior de los clientes móviles. Las pestañas se abren en una vista web desde la aplicación dentro del cliente de Teams. | La aplicación no aparece en clientes móviles. |
| **Pestañas configurables** | Las pestañas se abren en una vista web desde la aplicación dentro del cliente de Teams mediante `contentUrl` el . | Si selecciona **Tab,** se abre el contenido con `websiteUrl` el explorador web predeterminado del dispositivo. |


> [!NOTE]
>
> * [Las aplicaciones enviadas a AppSource para su publicación en Teams ](../concepts/deploy-and-publish/overview.md#publish-to-appsource) se evalúan automáticamente para la capacidad de respuesta móvil. Para cualquier consulta, llegue a teamsubm@microsoft.com.
> * Para todas las aplicaciones que no se distribuyen a través de [AppSource](../concepts/deploy-and-publish/overview.md), las pestañas se abren en una vista web desde la aplicación dentro de los clientes de Teams de forma predeterminada y no se requiere ningún proceso de aprobación independiente.

> [!div class="nextstepaction"]
> [Más información: Solicitar permisos de dispositivo](../concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
> [Más información: Integrar funcionalidades multimedia](../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Más información: Integrar la funcionalidad del escáner de códigos de barras o QR en Teams](../concepts/device-capabilities/qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [Más información: Integrar las funcionalidades de ubicación en Teams](../concepts/device-capabilities/location-capability.md)
