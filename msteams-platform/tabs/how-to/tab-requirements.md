---
title: Requisitos previos
author: surbhigupta
description: Todas las pestañas Microsoft Teams deben cumplir estos requisitos.
keywords: Canal de grupo de pestañas de teams configurable
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: eeb83f6bdd335c4d536f18915cff8b04a85761a5
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399194"
---
# <a name="prerequisites"></a>Requisitos previos

Teams pestañas deben cumplir los siguientes requisitos previos:

* Debe permitir que las páginas de pestañas se muestran en un iFrame, con encabezados de respuesta HTTP X-Frame-Options y Content-Security-Policy.
  * Establecer encabezado: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Para la compatibilidad con Internet Explorer 11, establezca `X-Content-Security-Policy`.
  * Como alternativa, establezca el encabezado `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`. Este encabezado está en desuso pero sigue siendo aceptado por la mayoría de los exploradores.

* Normalmente, como medida de protección contra el robo de clics, las páginas de inicio de sesión no se representan en iFrames. La lógica de autenticación debe usar un método que no sea el redireccionamiento. Por ejemplo, use la autenticación basada en token o basada en cookies.

    > [!NOTE]
    > Chrome 80, programado para su lanzamiento a principios de 2020, introduce nuevos valores de cookies e impone directivas de cookies de forma predeterminada. Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. Para obtener más información, consulte [SameSite cookie attribute](../../resources/samesite-cookie-update.md).

* Los exploradores cumplen una restricción de directiva del mismo origen. Impide que las páginas web soliciten dominios distintos de la página web servida. Sin embargo, puede redirigir la página de configuración o contenido a otro dominio o subdominio. La lógica de navegación entre dominios debe permitir que el cliente de Teams `validDomains` valide el origen con una lista estática en el manifiesto de la aplicación al cargar o comunicarse con la pestaña.

* Debe dar estilo a las pestañas en función Teams tema, diseño e intención del cliente. Normalmente, las pestañas funcionan mejor cuando se construyen para abordar una necesidad específica y centrarse en un pequeño conjunto de tareas o un subconjunto de datos que es relevante para la ubicación del canal de la pestaña.

* En la página de contenido, agregue una referencia a [Microsoft Teams SDK de cliente de JavaScript](/javascript/api/overview/msteams-client) mediante etiquetas de script. Después de que se cargue la página, realice una llamada `microsoftTeams.initialize()`a , de lo contrario, no se mostrará la página.

* Para que la autenticación funcione en clientes móviles, debe actualizar Teams SDK de JavaScript a al menos la versión 1.4.1.

* Si decide que la pestaña canal o grupo aparezca en Teams móviles, `setSettings()` la configuración debe tener un valor para la `websiteUrl` propiedad.

* La pestaña Teams MS no admite la capacidad de cargar sitios web de intranet que usan certificados autofirmados.

## <a name="tools-you-can-use-to-build-tabs"></a>Herramientas que puede usar para crear pestañas

* [Kit de herramientas de Teams para Microsoft Visual Studio Code](../../toolkit/visual-studio-code-overview.md)
* [Kit de herramientas de Teams para Visual Studio](../../toolkit/visual-studio-overview.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)

## <a name="see-also"></a>Vea también

* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Compile su primera aplicación con JavaScript](../../get-started/first-app-react.md)
* [Cree la primera aplicación con SPFx](../../get-started/first-app-spfx.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)
