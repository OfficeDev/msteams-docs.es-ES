---
title: ¿Qué son las pestañas personalizadas en Teams?
author: laujan
description: Información general sobre las pestañas personalizadas en la plataforma de Microsoft Teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: e89f07133f86b6c0700e6a71d8e53bf6d9831196
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576851"
---
# <a name="what-are-microsoft-teams-custom-tabs"></a>¿Qué son las pestañas personalizadas de Microsoft Teams?

Las pestañas son páginas Web compatibles con Teams incrustadas en Microsoft Teams. Son etiquetas HTML sencillas <iframe \> que apuntan a dominios declarados en el manifiesto de la aplicación y pueden agregarse como parte de un canal dentro de un equipo, chat de grupo o aplicación personal para un usuario individual. Puede incluir pestañas personalizadas con la aplicación para insertar su propio contenido web en Teams o agregar una funcionalidad específica de Teams a su contenido Web. *Vea* [TEAMs Client SDK de Teams](/javascript/api/overview/msteams-client).

> [!NOTE]
> Chrome 80, programado para su lanzamiento en principios de 2020, presenta nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. *Consulte* [SameSite cookie Attribute (2020 Update)](../resources/samesite-cookie-update.md).

Hay dos tipos de fichas disponibles en Microsoft Teams: canal/grupo y personal. Las pestañas canal/grupo entregan contenido a los canales y los chats de grupo, y son una excelente manera de crear espacios de colaboración alrededor de contenido dedicado basado en Web. Las pestañas personales, junto con los bots de ámbito personal, forman parte de las aplicaciones personales y tienen un ámbito de usuario único. Se pueden anclar a la barra de navegación izquierda para facilitar el acceso.

## <a name="lesser-known-tab-features"></a>Características menos conocidas de las pestañas

> [!div class="checklist"]
>
> * Si se agrega una pestaña a una aplicación que también tiene un bot, el bot se agrega también al equipo.
> * Conocimiento del identificador de Azure Active Directory (Azure AD) del usuario actual.
> * Concienciación de la configuración regional para que el usuario indique el idioma; por ejemplo, `en-us` . 
> * Función de inicio de sesión único (SSO), si se admite.
> * Capacidad de usar bots o notificaciones de aplicaciones para un vínculo profundo a la ficha o a una subentidad del servicio, por ejemplo, un elemento de trabajo individual.
> * La capacidad de abrir un módulo de tareas desde los vínculos de una pestaña.
> * Reutilización de elementos Web de SharePoint dentro de la pestaña.

## <a name="tabs-user-scenarios"></a>Escenarios de usuario de pestañas

**Escenario:** Traer un recurso basado en web existente dentro de Teams. \
**Ejemplo:** Crea una pestaña personal en la aplicación de teams que presenta un sitio web corporativo informativo a los usuarios.

**Escenario:** Agregar páginas de soporte a un bot o una extensión de mensajería de Teams. \
**Ejemplo:** Puede crear pestañas personales que proporcionen *información sobre* el contenido de las páginas web y la *ayuda* para los usuarios.

**Escenario:** Proporcionar acceso a los elementos con los que interactúan los usuarios con regularidad para el diálogo cooperativo y la colaboración. \
**Ejemplo:** Cree una ficha canal/grupo con una vinculación profunda a elementos individuales.

## <a name="how-do-tabs-work"></a>¿Cómo funcionan las pestañas?

Una pestaña personalizada se declara en el manifiesto de la aplicación del paquete de la aplicación. Por cada página web que desee incluir como pestaña en la aplicación, defina una dirección URL y un ámbito. Además, debe agregar el SDK del [cliente de JavaScript de Teams](/javascript/api/overview/msteams-client) a la página y llamar `microsoftTeams.initialize()` después de que se cargue la página. Al hacerlo, le indicaremos a teams que muestre su página, le dará acceso a información específica de cada equipo (por ejemplo, si el cliente de Microsoft Teams ejecuta el *tema oscuro*) y le permitirá emprender acciones basadas en los resultados.

Tanto si elige exponer su pestaña dentro del ámbito de canal o de grupo como en el ámbito personal, tendrá que presentar una \> <[Página de contenido](~/tabs/how-to/create-tab-pages/content-page.md) HTML iframe en la pestaña. Para las pestañas personales, la dirección URL de contenido se establece directamente en el manifiesto de la aplicación de Teams por la `contentUrl` propiedad de la `staticTabs` matriz. El contenido de la pestaña será el mismo para todos los usuarios.

Para las fichas canal/grupo, también debe crear una página de configuración adicional que permita a los usuarios configurar la dirección URL de la página de contenido, normalmente mediante los parámetros de cadena de consulta de dirección URL para cargar el contenido adecuado para ese contexto. Esto se debe a que la ficha canal/grupo se puede Agregar a varios equipos o chats de grupo distintos. En cada instalación subsiguiente, los usuarios podrán configurar la pestaña, lo que le permitirá personalizar la experiencia según sea necesario. Cuando los usuarios agregan o configuran una pestaña, se asocia una dirección URL a la ficha que se presenta en la interfaz de usuario de Microsoft Teams. La configuración de una pestaña es simplemente agregar parámetros adicionales a esa dirección URL. Por ejemplo, cuando se agrega la pestaña de Azure Boards, la página de configuración le permite elegir la tarjeta que se cargará en la pestaña. La dirección URL de la página de configuración se especifica mediante la  `configurationUrl` propiedad de la `configurableTabs` matriz en el manifiesto de la aplicación.

Puede tener un máximo de una (1) ficha canal/grupo y hasta dieciséis (16) pestañas personales por aplicación.

## <a name="mobile-clients"></a>Clientes móviles

Si elige que la ficha canal o grupo aparezca en los clientes móviles de Teams, la `setSettings()` configuración debe tener un valor para la `websiteUrl` propiedad. Para garantizar una experiencia del usuario óptima, debe seguir las [instrucciones para las pestañas de dispositivos móviles](~/tabs/design/tabs-mobile.md) al crear las pestañas.

> [!div class="nextstepaction"]
> [Más información: solicitar permisos de dispositivo](/concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
>[Más información: permisos de galería de imágenes y cámaras](/concepts/device-capabilities/mobile-camera-image-permissions.md)