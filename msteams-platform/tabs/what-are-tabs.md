---
title: Pestañas de Microsoft Teams
author: surbhigupta
description: Aprenda a crear pestañas, páginas web incrustadas en Microsoft Teams. Cree una página de contenido como parte de la pestaña personal, de canal o de grupo. Además, aprenda a crear pestañas con tarjetas adaptables.
ms.localizationpriority: high
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: d175e9c1a9f8515db57c54503fd3f83cb7970777
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450397"
---
# <a name="build-tabs-for-teams"></a>Pestañas de compilación para Teams

Las pestañas son páginas web compatibles con Teams insertadas en Microsoft Teams. Son simples etiquetas HTML `<iframe\>` que apuntan a los dominios declarados en el manifiesto de la aplicación y que pueden agregarse como parte de un canal dentro de un equipo, un chat de grupo o una aplicación personal para un usuario individual. Puede incluir pestañas personalizadas con la aplicación para insertar su propio contenido web en Teams o agregar una funcionalidad específica de Teams a su contenido web. Para obtener más información, vea [SDK de cliente de JavaScript de Teams](/javascript/api/overview/msteams-client).

> [!IMPORTANT]
> Actualmente, las pestañas personalizadas están disponibles en Government Community Cloud (GCC), GCC-High y Department of Defense (DOD).

En la imagen siguiente se muestran las pestañas personales:

:::image type="content" source="../assets/images/tabs/personaltab.png" alt-text="Pestaña personal" lightbox="../assets/images/tabs/personaltab.png":::

En la imagen siguiente se muestran las pestañas de canal de Contoso:

:::image type="content" source="../assets/images/tabs/tabs.png" alt-text="Pestañas de canal o grupo" lightbox="../assets/images/tabs/tabs.png":::

Hay algunos requisitos previos que debe cumplir antes de trabajar en pestañas.

Hay dos tipos de pestañas disponibles en Teams, personal y canal o grupo. Las [pestañas personales](~/tabs/how-to/create-personal-tab.md), junto con los bots de ámbito personal, forman parte de las aplicaciones personales y se limitan a un solo usuario. Se pueden anclar a la barra de navegación izquierda para facilitar el acceso. [Pestañas de canal o grupo](~/tabs/how-to/create-channel-group-tab.md) entregar contenido a canales y chats grupales, y son una excelente manera de crear espacios de colaboración en torno a contenido dedicado basado en web.

Puede [crear una página de contenido](~/tabs/how-to/create-tab-pages/content-page.md) como parte de una pestaña personal, una pestaña de canal o de grupo o un módulo de tareas. Puede [crear una página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md) que permita a los usuarios configurar la aplicación de Microsoft Teams y usarla para configurar una pestaña de chat de canal o de grupo, una extensión de mensajería o un Conector de Office 365. Puede permitir que los usuarios vuelvan a configurar la pestaña después de la instalación y [crear una página de eliminación de pestañas](~/tabs/how-to/create-tab-pages/removal-page.md) para la aplicación. Al compilar una aplicación de Teams que incluye una pestaña, debe probar cómo funciona la pestaña [en los clientes de Teams de iOS y Android](~/tabs/design/tabs-mobile.md). La pestaña debe [obtener contexto](~/tabs/how-to/access-teams-context.md) a través de información básica, información de temas y configuración regional, y `entityId` o `subEntityId` que identifique lo que hay en la pestaña.

Puede crear pestañas con tarjetas adaptables y centralizar todas las funcionalidades de la aplicación Teams eliminando la necesidad de un back-end diferente para los bots y pestañas. [Vista de fases](~/tabs/tabs-link-unfurling.md) es un nuevo componente de la interfaz de usuario que le permite representar el contenido abierto en pantalla completa en Teams y anclado como una pestaña. El servicio existente de [apertura de vínculos](~/tabs/tabs-link-unfurling.md) fue actualizado, por lo que se usa para convertir las direcciones URL en pestañas mediante una tarjeta adaptable y los servicios de chat. Puede crear [pestañas](~/tabs/how-to/conversational-tabs.md) conversacionales con sub-entidades conversacionales que permitan a los usuarios tener conversaciones sobre sub entidades en la pestaña, como tareas específicas, pacientes y oportunidades de ventas, en lugar de analizar toda la pestaña. Puedes realizar cambios en los [márgenes de tabulación](~/resources/removing-tab-margins.md) para mejorar la experiencia del desarrollador al crear aplicaciones. Puede arrastrar la pestaña y colocarla en la posición deseada para intercambiar las posiciones de las pestañas dentro de sus aplicaciones personales y chats de canal o de grupo.

> [!NOTE]
> Las **Publicaciones** y **Archivos** no se pueden mover de sus posiciones.

## <a name="tab-features"></a>Características de pestañas

Las características de pestañas son las siguientes:

* Si se agrega una pestaña a una aplicación que también tiene un bot, el bot también se agrega al equipo.
* Reconocimiento del id. del usuario actual de Microsoft Azure Active Directory (Azure AD).
* Reconocimiento de configuración regional para que el usuario indique el idioma que es `en-us`.
* Funcionalidad de inicio de sesión único (SSO), si se admite.
* Capacidad de usar bots o notificaciones de aplicación para vincular en profundidad a la pestaña o a una subentidad dentro del servicio, por ejemplo, un elemento de trabajo individual.
* La capacidad de abrir un módulo de tareas desde vínculos dentro de una pestaña.
* Reutilizar elementos web de SharePoint en la pestaña.

## <a name="tabs-user-scenarios"></a>Escenarios de usuario de pestañas

**Escenario:** traer un recurso basado en web ya existente dentro de Teams. \
**Ejemplo:** crea una pestaña personal en la aplicación de Teams que presenta un sitio web corporativo informativo a los usuarios.

**Escenario:** agregar páginas de soporte técnico a un bot de Teams o una extensión de mensajería. \
**Ejemplo:** crea pestañas personales que proporcionan **sobre** y **ayudan a** contenido de página web a los usuarios.

**Escenario:** proporcionar acceso a los elementos con los que los usuarios interactúan periódicamente para el diálogo cooperativo y la colaboración. \
**Ejemplo:** crea una pestaña de canal o grupo con vinculación profunda a elementos individuales.

## <a name="understand-how-tabs-work"></a>Comprender cómo funcionan las pestañas

Puede usar uno de los métodos siguientes para crear pestañas:

* [Declarar pestaña personalizada en el manifiesto de la aplicación](#declare-custom-tab-in-app-manifest)
* [Usar tarjeta adaptable para crear pestañas](~/tabs/how-to/build-adaptive-card-tabs.md)

### <a name="declare-custom-tab-in-app-manifest"></a>Declarar pestaña personalizada en el manifiesto de la aplicación

Se declara una pestaña personalizada en el manifiesto de la aplicación del paquete de la aplicación. Para cada página web que quiera incluir como pestaña en la aplicación, define una dirección URL y un ámbito. Además, puede agregar el SDK de cliente de JavaScript de [Teams](/javascript/api/overview/msteams-client) a la página y llamar a `microsoftTeams.initialize()` después de cargar la página. Teams muestra su página y proporciona acceso a información específica de Teams, por ejemplo, el cliente de Teams está ejecutando el tema oscuro.

Tanto si elige exponer la pestaña dentro del ámbito del canal o del grupo, como del ámbito personal, debe presentar una página de contenido \> HTML [<iframe>](~/tabs/how-to/create-tab-pages/content-page.md) en la pestaña. En el caso de las pestañas personales, la URL del contenido se establece directamente en el manifiesto de la aplicación Teams mediante la `contentUrl`propiedad `staticTabs` del array. El contenido de la pestaña es el mismo para todos los usuarios.

Para las pestañas de canal o grupo, también puede crear una página de configuración adicional. Esta página le permite configurar la dirección URL de la página de contenido, normalmente mediante el uso de parámetros de cadena de consulta de dirección URL para cargar el contenido adecuado para ese contexto. Ello se debe a que su pestaña de canal o grupo se puede agregar a varios equipos o chats de grupo. En cada instalación posterior, los usuarios pueden configurar la pestaña, lo que le permite adaptar la experiencia según sea necesario. Cuando los usuarios agregan o configuran una pestaña, se asocia una dirección URL a la pestaña que se presenta en la interfaz de usuario (UI) de Teams. La configuración de una pestaña simplemente agrega más parámetros a esa dirección URL. Por ejemplo, al agregar la pestaña Azure Boards, la página de configuración le permite elegir qué panel carga la pestaña. La dirección URL de la página de configuración se especifica mediante la  `configurationUrl` propiedad en la `configurableTabs` matriz del manifiesto de la aplicación.

Puede tener varios canales o pestañas de grupo y hasta 16 pestañas personales por aplicación.

### <a name="tools-to-build-tabs"></a>Herramientas para crear pestañas

* [Kit de herramientas de Teams para Microsoft Visual Studio Code](../toolkit/visual-studio-code-overview.md)
* [Kit de herramientas de Teams para Visual Studio](../toolkit/visual-studio-overview.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Requisitos previos](~/tabs/how-to/tab-requirements.md)

## <a name="see-also"></a>Vea también

* [Pestañas personalizadas en Microsoft Teams](/microsoftteams/built-in-custom-tabs#develop-custom-tabs)
* [Solicitar permisos de dispositivo](../concepts/device-capabilities/native-device-permissions.md)
* [Integrar capacidades multimedia](../concepts/device-capabilities/media-capabilities.md)
* [Integrar un escáner qr o de código de barras](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Integrar capacidades de ubicación](../concepts/device-capabilities/location-capability.md)
* [Pestañas en dispositivos móviles](design/tabs-mobile.md#tabs-on-mobile)
