---
title: Descripción de los requisitos de la pestaña
author: laujan
description: Todas las pestañas de Microsoft Teams deben cumplir estos requisitos.
keywords: Canal de grupo de pestañas de teams configurable
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1f5a3eaa8ca16878944288d5dbbfa78cfe9fa3ce
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797945"
---
# <a name="tab-requirements"></a>Requisitos de pestaña

Las pestañas de Teams deben cumplir los siguientes requisitos:

* Debes permitir que las páginas de pestaña se atenúen en un iFrame, a través de encabezados de respuesta HTTP X-Frame-Options o Content-Security-Policy.
  * Establecer encabezado: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Para la compatibilidad con Internet Explorer 11, establece `X-Content-Security-Policy` también.
  * Como alternativa, establezca el encabezado `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` . Este encabezado está en desuso pero sigue siendo respetado por la mayoría de los exploradores.
* Por lo general, como medida de seguridad contra el inicio de sesión de clics, las páginas de inicio de sesión no se representan en iFrames. Por lo tanto, la lógica de autenticación debe usar un método que no sea el redireccionamiento (por ejemplo, usar autenticación basada en token o basada en cookies).

> [!NOTE]
> Chrome 80, programado para su lanzamiento a principios de 2020, introduce nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. *Vea* [el atributo de cookie SameSite (actualización de 2020).](../../resources/samesite-cookie-update.md)

* Los exploradores se adhieren a una restricción de directiva del mismo origen que impide que una página web haga solicitudes a un dominio diferente del que atendía una página web. Sin embargo, es posible que deba redirigir la página de configuración o contenido a otro dominio o subdominio. La lógica de navegación entre dominios debe permitir que el cliente de Teams valide el origen con una lista validDomains estática en el manifiesto de la aplicación al cargar o comunicarse con la pestaña.

* Para crear una experiencia sin problemas, debe dar estilo a las pestañas según el tema, el diseño y la intención del cliente de Teams. Normalmente, las pestañas funcionan mejor cuando se han creado para abordar una necesidad específica y centrarse en un pequeño conjunto de tareas o en un subconjunto de datos que sea relevante para la ubicación del canal de la pestaña.

* En la página de contenido, agregue una referencia al SDK de [cliente de JavaScript](/javascript/api/overview/msteams-client) de Microsoft Teams con etiquetas de script. Después de cargar la página, realice una llamada a `microsoftTeams.initialize()` . La página no se mostrará si no lo hace.
