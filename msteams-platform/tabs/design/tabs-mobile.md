---
title: Pestañas en dispositivos móviles
description: Obtenga información sobre cómo funcionan las pestañas en los clientes de Microsoft Teams (móvil) de Android e iOS, su autenticación, su conexión de ancho de banda bajo, las pruebas o la distribución.
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 604d1ed8cabd745359e4714bc1b5fe82e67c7662
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450481"
---
# <a name="tabs-on-mobile"></a>Pestañas en dispositivos móviles

Al compilar una aplicación de Microsoft Teams que incluye una pestaña, debe probar cómo funciona la pestaña en los clientes de Microsoft Teams de Android e iOS. En este artículo se describen algunos de los escenarios clave que debe tener en cuenta.

Si decide que la pestaña de canal o grupo aparezca en los clientes móviles de Teams, la [`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true) configuración debe tener un valor para la `websiteUrl` propiedad . Para garantizar una experiencia de usuario óptima, debe seguir las instrucciones de las pestañas en el móvil de este artículo al crear las pestañas.

Las aplicaciones [distribuidas a través de la tienda teams](~/concepts/deploy-and-publish/appsource/publish.md) tienen un proceso de aprobación independiente para los clientes móviles. El comportamiento predeterminado de estas aplicaciones es el siguiente:

| **Funcionalidad de la aplicación** | **Comportamiento si se aprueba la aplicación** | **Comportamiento si no se aprueba la aplicación** |
| --- | --- | --- |
| **Pestañas personales** | La aplicación aparece en la barra inferior de los clientes móviles. Las pestañas se abren en el cliente de Teams. | La aplicación no aparece en la barra inferior de los clientes móviles. |
| **Pestañas de canal y grupo** | La pestaña se abre en el cliente de Teams mediante `contentUrl`. | La pestaña se abre en un explorador fuera del cliente de Teams mediante `websiteUrl`. |

> [!NOTE]
>
> * Las aplicaciones enviadas a [AppSource](https://appsource.microsoft.com) para su publicación en Teams se evalúan automáticamente para la capacidad de respuesta móvil. Para cualquier consulta, póngase en contacto con teamsubm@microsoft.com.
> * Para todas las aplicaciones que no se distribuyen a través de AppSource, las pestañas se abren en una vista web dentro de la aplicación dentro de los clientes de Teams de forma predeterminada y no se requiere ningún proceso de aprobación independiente.
> * El comportamiento predeterminado de las aplicaciones solo es aplicable si se distribuye a través del almacén de Teams. De forma predeterminada, todas las pestañas se abren en el cliente de Teams.
> * Para iniciar una evaluación de la aplicación para la facilidad de uso móvil, póngase en contacto con teamsubm@microsoft.com con los detalles de la aplicación.

## <a name="authentication"></a>Autenticación

Para que la autenticación funcione en clientes móviles, debe actualizar el SDK de JavaScript de Teams a la versión 1.4.1 como mínimo.

## <a name="low-bandwidth-and-intermittent-connections"></a>Ancho de banda bajo y conexiones intermitentes

Los clientes móviles funcionan con un ancho de banda bajo y conexiones intermitentes. La aplicación debe controlar los tiempos de espera correctamente proporcionando un mensaje contextual al usuario. También debe usar indicadores de progreso para proporcionar comentarios a los usuarios sobre los procesos de ejecución prolongada.

## <a name="testing-on-mobile-clients"></a>Pruebas en clientes móviles

Debe validar que la pestaña funciona correctamente en dispositivos móviles de varios tamaños y calidades. En el caso de los dispositivos Android, puede usar [DevTools](~/tabs/how-to/developer-tools.md) para depurar la pestaña mientras se ejecuta. Se recomienda probar en dispositivos de alto y bajo rendimiento, incluida una tableta.

## <a name="distribution"></a>Distribución

Las aplicaciones que aparecen en la tienda de Teams deben aprobarse para que el uso móvil funcione correctamente en el cliente móvil de Teams. La disponibilidad y el comportamiento de las pestañas depende de si la aplicación está aprobada.

### <a name="apps-on-teams-store-approved-for-mobile"></a>Aplicaciones en la tienda teams aprobadas para dispositivos móviles

En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación aparece en la tienda de Teams y se aprueba para su uso móvil:

|Funcionalidad   |¿Disponibilidad móvil?   |Comportamiento móvil|
|----------|-----------|------------|
|Canal <br /> y pestaña de grupo|Yes|La pestaña se abre en el cliente móvil de Teams mediante la configuración de la `contentUrl` aplicación.|
|Aplicación personal|Yes|Cada pestaña de la pestaña aplicación personal se abre en el cliente móvil de Teams con su configuración respectiva `contentUrl` .|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Aplicaciones en la tienda teams no aprobadas para dispositivos móviles

En la tabla siguiente se describe la disponibilidad y el comportamiento de las pestañas cuando la aplicación aparece en la tienda de Teams, pero no se aprueba para su uso móvil:

| Funcionalidad | ¿Disponibilidad móvil? | Comportamiento móvil |
|----------|-----------|------------|
|Pestaña Canal y grupo|Yes|La pestaña se abre en el explorador predeterminado del dispositivo en lugar del cliente móvil de Teams mediante la configuración de la `websiteUrl` aplicación, que también debe incluirse en la [función](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace) del `setSettings()` código fuente. Sin embargo, los usuarios pueden ver la pestaña en el cliente móvil de Teams seleccionando **Más** junto a la aplicación y eligiendo **Abrir**, lo que desencadena la configuración de la `contentUrl` aplicación.|
|Aplicación personal|No|No aplicable|

### <a name="apps-not-on-teams-store"></a>Aplicaciones que no están en el almacén de Teams

Si va a transferir localmente la aplicación o publicarla en el catálogo de aplicaciones de una organización, el comportamiento de las pestañas es el mismo que el de las aplicaciones de la tienda de Teams aprobadas por Microsoft para dispositivos móviles.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Obtención del contexto de Teams para la pestaña](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>Vea también

* [Directrices de diseño de pestañas](~/tabs/design/tabs.md)
* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de grupo o de canal](~/tabs/how-to/create-channel-group-tab.md)
* [Planeamiento de dispositivos móviles de Teams: Teams](~/concepts/design/plan-responsive-tabs-for-teams-mobile.md)
