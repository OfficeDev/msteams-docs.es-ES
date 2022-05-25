---
title: Requisitos previos
author: surbhigupta
description: Cada pestaña de Microsoft Teams debe cumplir estos requisitos.
keywords: canal de grupo de pestañas de teams configurable
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 92b03146200af978f3fa5d6dc2c5e6ad27a12200
ms.sourcegitcommit: 929391b6c04d53ea84a93145e2f29d6b96a64d37
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2022
ms.locfileid: "65672932"
---
# <a name="prerequisites"></a>Requisitos previos

Asegúrese de cumplir los siguientes requisitos previos al crear la pestaña personal y de canal o grupo de Teams:

* Permite que las páginas de pestañas se detecten en un iFrame mediante los encabezados de respuesta HTTP X-Frame-Options y Content-Security-Policy.
  * Establecer encabezado: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Para obtener compatibilidad con Internet Explorer 11, establezca `X-Content-Security-Policy`.
  * Como alternativa, establezca el encabezado `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`. Este encabezado está en desuso, pero sigue siendo aceptado por la mayoría de los exploradores.

* Las páginas de inicio de sesión no se representan en iFrames, como medida de protección contra el "secuestro de clics". La lógica de autenticación debe usar un método distinto del redireccionamiento. Por ejemplo, use la autenticación basada en tokens o en cookies.

    > [!NOTE]
    > Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. Para más información, vea [Atributo de cookie SameSite](../../resources/samesite-cookie-update.md).

* La restricción de directiva del mismo origen de los exploradores impide que las páginas web realicen solicitudes a dominios diferentes de la página web atendida. Por lo tanto, puede redirigir la página de configuración o contenido a otro dominio o subdominio. La lógica de navegación entre dominios debe permitir que el cliente de Teams valide el origen con una lista de `validDomains` estática en el manifiesto de la aplicación al cargar o comunicarse con la pestaña.

* Aplique estilo a las pestañas en función del tema, el diseño y la intención del cliente de Teams. Las pestañas funcionan mejor cuando se crean para satisfacer una necesidad específica y centrarse en un pequeño conjunto de tareas o en un subconjunto de datos que es relevante para la ubicación del canal de la pestaña.

* En la página de contenido, agregue una referencia al [SDK de cliente JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client) mediante etiquetas de script. Una vez que se cargue la página, realice una llamada a `app.initialize()`, de lo contrario, no se mostrará la página.

* Para que la autenticación funcione en clientes móviles, debe actualizar al SDK de JavaScript de Teams 1.4.1 y versiones posteriores.

* Si decide que la pestaña de canal o grupo aparezca en el cliente móvil de Teams, la configuración de `setConfig()` debe tener un valor para la propiedad `websiteUrl`.

* Microsoft Teams pestaña no admite la capacidad de cargar sitios web de intranet que usan certificados autofirmados.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="tools-to-build-tabs"></a>Herramientas para crear pestañas

| &nbsp; | Instalar | Para usar... |
| --- | --- | --- |
| **Required** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | Entorno de tiempo de ejecución de JavaScript de back-end. Use la versión v16 LTS más reciente.|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge) (recomendado) o [Google Chrome](https://www.google.com/chrome/) | Un explorador con herramientas de desarrollo. |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | Entornos de compilación de JavaScript, TypeScript o SharePoint Framework (SPFx). |
| &nbsp; | Carga de trabajo de [Visual Studio 2019](https://visualstudio.com/download), **ASP.NET y desarrollo web** o **Desarrollo multiplataforma de .NET Core** | .NET. Puede instalar la edición de la comunidad gratuita de Visual Studio 2019. |
| &nbsp; | [Git](https://git-scm.com/downloads) | Git para usar el repositorio de aplicaciones de ejemplo de GitHub. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app) | Microsoft Teams para colaborar con todos los usuarios con los que trabaja a través de aplicaciones de chat, reuniones, llamadas, todo en un solo lugar. |
| &nbsp; | [ngrok](https://ngrok.com/download) | Ngrok es una herramienta de software de proxy inverso. Ngrok crea un túnel a los puntos de conexión HTTPS disponibles públicamente del servidor web en ejecución local. Los puntos de conexión web del servidor están disponibles durante la sesión actual en el equipo. Cuando el equipo se apaga o entra en suspensión, el servicio ya no está disponible. |
| &nbsp; | [Portal para desarrolladores de Teams](https://dev.teams.microsoft.com/) | Portal basado en web para configurar, administrar y distribuir la aplicación de Teams, incluida su organización o la tienda de Teams. |

### <a name="build-your-teams-tab"></a>Crear la pestaña de Teams

Ahora vamos a crear la pestaña. Pero primero seleccione la pestaña que prefiera crear:

> [!div class="nextstepaction"]
> [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
> [!div class="nextstepaction"]
> [Crear una pestaña de grupo o canal personalizado](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>Consulte también

* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)