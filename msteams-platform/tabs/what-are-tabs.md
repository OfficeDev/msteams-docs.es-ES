---
title: ¿Qué son las pestañas personalizadas en Teams?
author: laujan
description: Información general sobre las pestañas personalizadas en la plataforma de Microsoft Teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: c9e76d13c96c48f88b555b3d740912017a8b2d0a
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818881"
---
# <a name="what-are-microsoft-teams-custom-tabs"></a>¿Qué son las pestañas personalizadas de Microsoft Teams?

Las pestañas son páginas Web compatibles con Teams incrustadas en Microsoft Teams. Son iframe sencillos que apuntan a dominios declarados en el manifiesto de la aplicación y pueden agregarse como parte de un canal dentro de un equipo, un chat en grupo o como una aplicación personal para un usuario individual. Puede incluir pestañas personalizadas con la aplicación para insertar su propio contenido web en Teams y agregar una funcionalidad específica de Teams a su contenido Web. *Vea* [TEAMs Client SDK de Teams](/javascript/api/overview/msteams-client).

> [!NOTE]
> Chrome 80, programado para su lanzamiento en principios de 2020, presenta nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. *Consulte* [SameSite cookie Attribute (2020 Update)](../resources/samesite-cookie-update.md).

Hay dos tipos de fichas disponibles en Teams: Channel/Group y personal. Una pestaña de canal o grupo entrega contenido a los canales y los chats de grupo, y es una buena manera de crear espacios de colaboración alrededor de contenido dedicado basado en Web. Las pestañas personales, junto con los bots de ámbito personal, forman parte de las aplicaciones personales y tienen un ámbito de usuario único. Se pueden anclar a la barra de navegación izquierda para facilitar el acceso.

## <a name="lesser-known-tab-features"></a>Características menos conocidas de las pestañas

> [!div class="checklist"]
>
> * Si se agrega una pestaña a una aplicación que también tiene un bot, el bot se agrega también al equipo.
> * Conocimiento del identificador de AAD del usuario actual.
> * Concienciación de la configuración regional para que el usuario indique el idioma; por ejemplo, `en-us` . 
> * Función SSO, si se admite.
> * Capacidad de usar bots o notificaciones de aplicaciones para un vínculo profundo a la ficha o a una subentidad del servicio, por ejemplo, un elemento de trabajo individual.
> * La capacidad de abrir un módulo de tareas desde los vínculos de una pestaña.
> * Reutilización de elementos Web de SharePoint dentro de la pestaña.

## <a name="tabs-user-scenarios"></a>Escenarios de usuario de pestañas

**Escenario:** Traer un recurso basado en web existente dentro de Teams. \
**Ejemplo:** Crea una pestaña personal en la aplicación de teams que presenta un sitio web corporativo informativo a los usuarios.

**Escenario:** Agregar páginas de soporte a un bot o una extensión de mensajería de Teams. \
**Ejemplo:** Puede crear pestañas personales que proporcionen información sobre el contenido de las páginas web y la ayuda para los usuarios.

**Escenario:** Proporcionar acceso a los elementos con los que interactúan los usuarios con regularidad para el diálogo cooperativo y la colaboración. \
**Ejemplo:** Cree una ficha canal/grupo con una vinculación profunda a elementos individuales.

## <a name="how-do-tabs-work"></a>¿Cómo funcionan las pestañas?

Una pestaña personalizada se declara en el manifiesto de la aplicación del paquete de la aplicación. Por cada página web que desee incluir como pestaña en la aplicación, defina una dirección URL y un ámbito. Además, debe agregar el SDK del [cliente de JavaScript de Teams](/javascript/api/overview/msteams-client) a la página y llamar `microsoftTeams.initialize()` después de que se cargue la página. Al hacerlo, le indicaremos a teams que muestre su página, le dará acceso a información específica de cada equipo (por ejemplo, si el cliente de Microsoft Teams ejecuta el tema oscuro) y le permitirá emprender acciones basadas en los resultados.

Tanto si elige exponer su pestaña dentro del ámbito de canal o de grupo como en el ámbito personal, tendrá que presentar una [Página de contenido](~/tabs/how-to/create-tab-pages/content-page.md) HTML iframe en la ficha. Para las pestañas personales, la dirección URL de contenido se establece directamente en el manifiesto mediante la `contentUrl` propiedad en la `staticTabs` matriz. El contenido de la pestaña será el mismo para todos los usuarios.

Para las fichas canal/grupo, también debe crear una página de configuración adicional que permita a los usuarios configurar la dirección URL de la página de contenido, normalmente mediante los parámetros de cadena de consulta de dirección URL para cargar el contenido adecuado para ese contexto. Esto se debe a que la ficha canal/grupo se puede Agregar a varios equipos o chats de grupo distintos. En cada instalación subsiguiente, los usuarios podrán configurar la pestaña que le permitirá personalizar la experiencia según sea necesario. Cuando los usuarios agregan o configuran una pestaña, se asocia una dirección URL a la ficha que se presenta en la interfaz de usuario de Microsoft Teams. La configuración de una pestaña es simplemente agregar parámetros adicionales a esa dirección URL. Por ejemplo, cuando se agrega la pestaña DevOps Board de Azure, la página de configuración permite elegir la tarjeta que se cargará. La dirección URL de la página de configuración se especifica mediante la  `configurationUrl` propiedad de la `configurableTabs` matriz en el manifiesto de la aplicación.

Puede tener un máximo de una (1) ficha canal/grupo y hasta dieciséis (16) pestañas personales por aplicación.

## <a name="mobile-clients"></a>Clientes móviles

Si elige que la pestaña de canal/grupo/ficha personal aparezca en los clientes móviles de Teams, la `setSettings()` configuración debe tener un valor para la `websiteUrl` propiedad. Para garantizar una experiencia del usuario óptima, debe seguir las [instrucciones para las pestañas de dispositivos móviles](~/tabs/design/tabs-mobile.md) al crear las pestañas.
