---
title: ¿Qué son las pestañas personalizadas en Teams?
author: laujan
description: Información general sobre las pestañas personalizadas en la plataforma teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 64c6e44177f1fb598895f748dbd0ec1c0b1e3aa1
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797893"
---
# <a name="what-are-microsoft-teams-tabs"></a>¿Qué son las pestañas de Microsoft Teams?

Las pestañas son páginas web para Teams incrustadas en Microsoft Teams. Son etiquetas iframe HTML <sencillas que apuntan a dominios declarados en el manifiesto de la aplicación y se pueden agregar como parte de un canal dentro de un equipo, un chat en grupo o una aplicación personal para un usuario \> individual. Puede incluir pestañas personalizadas con su aplicación para insertar su propio contenido web en Teams o agregar funcionalidad específica de Teams a su contenido web. *Vea EL* [SDK del cliente de JavaScript de Teams.](/javascript/api/overview/msteams-client)

> [!NOTE]
> Chrome 80, programado para su lanzamiento a principios de 2020, introduce nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. *Vea* [el atributo de cookie SameSite (actualización de 2020).](../resources/samesite-cookie-update.md)

Hay dos tipos de pestañas disponibles en Teams: canal/grupo y personal. Las pestañas de canal o grupo proporcionan contenido a canales y chats de grupo, y son una excelente manera de crear espacios de colaboración en torno al contenido dedicado basado en web. Las pestañas personales, junto con los bots con ámbito personal, forman parte de aplicaciones personales y están en el ámbito de un solo usuario. Se pueden anclar a la barra de navegación izquierda para facilitar el acceso.

## <a name="lesser-known-tab-features"></a>Características de pestañas menos conocidas

> [!div class="checklist"]
>
> * Si se agrega una pestaña a una aplicación que también tiene un bot, el bot también se agrega al equipo.
> * Reconocimiento del identificador de Azure Active Directory (Azure AD) del usuario actual.
> * Reconocimiento de configuración regional para que el usuario indique el idioma, es decir, `en-us` . 
> * Funcionalidad de inicio de sesión único (SSO), si se admite.
> * Capacidad de usar bots o notificaciones de aplicaciones para vincular profundamente a la pestaña o a una sub entity dentro del servicio, por ejemplo, un elemento de trabajo individual.
> * La capacidad de abrir un módulo de tareas desde vínculos dentro de una pestaña.
> * Reutilización de elementos web de SharePoint dentro de la pestaña.

## <a name="tabs-user-scenarios"></a>Escenarios de usuario de pestañas

**Escenario:** Traer un recurso basado en web existente dentro de Teams. \
**Ejemplo:** Cree una pestaña personal en la aplicación de Teams que presente un sitio web corporativo informativo a los usuarios.

**Escenario:** Agregar páginas de soporte técnico a un bot o extensión de mensajería de Teams. \
**Ejemplo:** Se crean pestañas personales que proporcionan *información sobre el* *contenido* de la página web y ayudan a los usuarios.

**Escenario:** Proporcionar acceso a los elementos con los que interactúan los usuarios periódicamente para el diálogo y la colaboración cooperativas. \
**Ejemplo:** Crea una pestaña de canal o grupo con vínculos profundos a elementos individuales.

## <a name="how-do-tabs-work"></a>¿Cómo funcionan las pestañas?

Se declara una pestaña personalizada en el manifiesto de la aplicación del paquete de la aplicación. Para cada página web que quieras incluir como una pestaña en la aplicación, debes definir una dirección URL y un ámbito. Además, debe agregar el SDK de cliente [de JavaScript](/javascript/api/overview/msteams-client) de Teams a su página y llamar después `microsoftTeams.initialize()` de que se cargue la página. Si lo hace, le mostrará a Teams que muestre su página, le dará acceso a información específica de Teams (por ejemplo, si el cliente de Teams está ejecutando el tema *oscuro)* y le permitirá realizar acciones en función de los resultados.

Independientemente de si decide exponer la pestaña dentro del ámbito de canal o grupo o personal, deberá presentar una página de contenido HTML de iframe <en \> la pestaña. [](~/tabs/how-to/create-tab-pages/content-page.md) Para las pestañas personales, la dirección URL de contenido se establece directamente en el manifiesto de la aplicación de Teams `contentUrl` mediante la propiedad de la `staticTabs` matriz. El contenido de la pestaña será el mismo para todos los usuarios.

Para las pestañas de canal o grupo, también debe crear una página de configuración adicional que permita a los usuarios configurar la dirección URL de la página de contenido, normalmente mediante parámetros de cadena de consulta url para cargar el contenido adecuado para ese contexto. Esto se debe a que la pestaña de canal o grupo se puede agregar a varios equipos o chats de grupo diferentes. En cada instalación posterior, los usuarios podrán configurar la pestaña, lo que te permitirá adaptar la experiencia según sea necesario. Cuando los usuarios agregan o configuran una pestaña, se asocia una dirección URL con la pestaña que se presenta en la interfaz de usuario de Teams. Configurar una pestaña es simplemente agregar parámetros adicionales a esa dirección URL. Por ejemplo, cuando agrega la pestaña Paneles de Azure, la página de configuración le permite elegir qué tablero se cargará la pestaña. La dirección URL de la página de configuración se especifica mediante la  `configurationUrl` propiedad en la `configurableTabs` matriz del manifiesto de la aplicación.

Puedes tener un máximo de una (1) pestaña de canal o grupo y hasta dieciséis (16) pestañas personales por aplicación.

## <a name="mobile-clients"></a>Clientes móviles

Si decide que la pestaña de canal o grupo aparezca en los clientes móviles de Teams, la configuración debe `setSettings()` tener un valor para la `websiteUrl` propiedad. Para garantizar una experiencia de usuario óptima, debe seguir las instrucciones para las [pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md) al crear las pestañas. Las aplicaciones que se [distribuyen a través de Appsource](~/concepts/deploy-and-publish/appsource/publish.md) tienen un proceso de aprobación independiente para los clientes móviles. El comportamiento predeterminado de estas aplicaciones es el siguiente:

| **Funcionalidad de la aplicación** | **Comportamiento si se aprueba la aplicación** | **Comportamiento si la aplicación no está aprobada** |
| --- | --- | --- |
| **Pestañas estáticas** | La aplicación aparece en la barra inferior de los clientes móviles. Las pestañas se abren en el cliente de Teams. | La aplicación no aparece en la barra inferior de los clientes móviles. |
| **Pestañas configurables** | La pestaña se abre en el cliente de Teams con `contentUrl` . | La pestaña se abre en un explorador fuera del cliente de Teams con `websiteUrl` . |


>[!NOTE]
>
>- El comportamiento predeterminado de las aplicaciones solo es aplicable si se distribuyen a través de AppSource. No hay ningún proceso de aprobación para las aplicaciones distribuidas a través de otros [métodos de distribución.](~/concepts/deploy-and-publish/overview.md) De forma predeterminada, todas las pestañas se abren en el cliente de Teams.
>- Para iniciar una evaluación de la aplicación para dispositivos móviles, teamsubm@microsoft.com con los detalles de la aplicación.


> [!div class="nextstepaction"]
> [Más información: Solicitar permisos de dispositivo](/concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
>[Más información: Permisos de la galería de imágenes y cámara](/concepts/device-capabilities/mobile-camera-image-permissions.md)
