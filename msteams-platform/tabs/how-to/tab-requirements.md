---
title: Comprensión de los requisitos de la pestaña
author: laujan
description: Cada pestaña de Microsoft Teams debe cumplir estos requisitos.
keywords: equipos pestañas canal de grupo configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a46a80401b29b5436807c9a5b94580beca3786f0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566666"
---
# <a name="tab-requirements"></a>Requisitos de pestaña

Teams pestañas deben cumplir los siguientes requisitos:

* Debe permitir que las páginas de pestañas se sirvan en un iFrame, a través de encabezados de respuesta HTTP X-Frame-Options y/o Content-Security-Policy.
  * Establecer encabezado: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Para la compatibilidad con Internet Explorer 11, establezca `X-Content-Security-Policy` también.
  * Como alternativa, establezca el encabezado `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` . Este encabezado está en desuso, pero sigue siendo respetado por la mayoría de los navegadores.
* Normalmente, como protección contra el registro de clics, las páginas de inicio de sesión no se representan en iFrames. Por lo tanto, la lógica de autenticación debe usar un método distinto de la redirección. Por ejemplo, utilice la autenticación basada en tokens o cookies.

> [!NOTE]
> Chrome 80, programado para su lanzamiento a principios de 2020, introduce nuevos valores de cookies e impone políticas de cookies de forma predeterminada. Se recomienda establecer el uso previsto para sus cookies en lugar de confiar en el comportamiento predeterminado del navegador. Para obtener más información, consulte [Atributo de cookie SameSite (actualización de 2020).](../../resources/samesite-cookie-update.md)

* Los exploradores se adhieren a una restricción de directiva del mismo origen que impide que una página web realice solicitudes a un dominio diferente al que sirvió una página web. Sin embargo, es posible que deba redirigir la página de configuración o contenido a otro dominio o subdominio. La lógica de navegación entre dominios debe permitir que el cliente Teams valide el origen en una lista estática validDomains del manifiesto de aplicación al cargar o comunicarse con la pestaña.

* Para crear una experiencia perfecta, debe diseñar sus pestañas en función del tema, el diseño y la intención del cliente Teams. Normalmente, las pestañas funcionan mejor cuando están diseñadas para abordar una necesidad específica y centrarse en un pequeño conjunto de tareas o un subconjunto de datos que es relevante para la ubicación del canal de la pestaña.

* Dentro de la página de contenido, agregue una referencia a [Microsoft Teams SDK de cliente de JavaScript](/javascript/api/overview/msteams-client) mediante etiquetas de script. Después de la carga de la página, realice una llamada a `microsoftTeams.initialize()` . Su página no se mostrará si no lo hace.

* Para que la autenticación funcione en clientes móviles, debe actualizarlo Teams SDK de JavaScript a al menos la versión 1.4.1.

* Si decide que la pestaña de canal o grupo aparezca en Teams clientes móviles, la `setSettings()` configuración debe tener un valor para la `websiteUrl` propiedad.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Cree una pestaña personal personalizada con Node.js y el generador Yeoman para Microsoft Teams](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)