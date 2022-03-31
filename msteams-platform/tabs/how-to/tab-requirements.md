---
title: Requisitos previos
author: surbhigupta
description: Todas las pestañas Microsoft Teams deben cumplir estos requisitos.
keywords: Canal de grupo de pestañas de teams configurable
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: fe72691465ca785cefb6a96c8eb4005a64601a17
ms.sourcegitcommit: 3dc9b539c6f7fbfb844c47a78e3b4d2200dabdad
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/31/2022
ms.locfileid: "64571519"
---
# <a name="prerequisites"></a>Requisitos previos

Asegúrese de cumplir los siguientes requisitos previos al crear la Teams personal y de canal o grupo:

* Permitir que las páginas de pestañas se descubran en un iFrame, con encabezados de respuesta HTTP X-Frame-Options y Content-Security-Policy.
  * Establecer encabezado: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Para la compatibilidad con Internet Explorer 11, establezca `X-Content-Security-Policy`.
  * Como alternativa, establezca el encabezado `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`. Este encabezado está en desuso pero sigue siendo aceptado por la mayoría de los exploradores.

* Las páginas de inicio de sesión no se representan en iFrames, como medida de protección contra el robo de clics. La lógica de autenticación debe usar un método que no sea el redireccionamiento. Por ejemplo, use la autenticación basada en token o basada en cookies.

    > [!NOTE]
    > Se recomienda establecer el uso previsto para las cookies en lugar de basarse en el comportamiento predeterminado del explorador. Para obtener más información, consulte [SameSite cookie attribute](../../resources/samesite-cookie-update.md).

* La restricción de directiva del mismo origen de los exploradores impide que las páginas web soliciten dominios distintos de la página web servida. Por lo tanto, puede redirigir la página de configuración o contenido a otro dominio o subdominio. La lógica de navegación entre dominios debe permitir que el cliente de Teams `validDomains` valide el origen con una lista estática en el manifiesto de la aplicación al cargar o comunicarse con la pestaña.

* Estilo de las pestañas en función Teams tema, diseño e intención del cliente. Las pestañas funcionan mejor cuando se construyen para abordar una necesidad específica y centrarse en un pequeño conjunto de tareas o un subconjunto de datos que es relevante para la ubicación del canal de la pestaña.

* En la página de contenido, agregue una referencia a [Microsoft Teams SDK de cliente de JavaScript](/javascript/api/overview/msteams-client) mediante etiquetas de script. Después de que se cargue la página, realice una llamada `microsoftTeams.initialize()`a , de lo contrario, no se mostrará la página.

* Para que la autenticación funcione en clientes móviles, debe actualizar a Teams SDK de JavaScript 1.4.1 y versiones posteriores.

* Si elige que la pestaña canal o grupo aparezca en Teams cliente móvil, `setSettings()` la configuración debe tener un valor para la `websiteUrl` propiedad.

* Microsoft Teams pestaña no admite la capacidad de cargar sitios web de intranet que usan certificados autofirmados.

## <a name="tools-to-build-tabs"></a>Herramientas para crear pestañas

| &nbsp; | Instalar | Para usar... |
| --- | --- | --- |
| **Required** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | Entorno de tiempo de ejecución de JavaScript back-end. Use la versión más reciente de LTS de v14.|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge) (recomendado) o [Google Chrome](https://www.google.com/chrome/) | Un explorador con herramientas de desarrollador. |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript, TypeScript o SharePoint Framework (SPFx) de compilación. |
| &nbsp; | [Visual Studio 2019](https://visualstudio.com/download), **desarrollo ASP.NET web** o carga de trabajo de desarrollo **multiplataforma de .NET Core** | .NET. Puede instalar la edición de la comunidad gratuita de Visual Studio 2019. |
| &nbsp; | [Git](https://git-scm.com/downloads) | Git para usar el repositorio de aplicaciones de ejemplo GitHub. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app) | Microsoft Teams colaborar con todos los usuarios con los que trabajes a través de aplicaciones para chat, reuniones, llamadas, todo en un solo lugar. |
| &nbsp; | [ngrok](https://ngrok.com/download) | Ngrok es una herramienta de software de proxy inverso. Ngrok crea un túnel para los puntos de conexión HTTPS del servidor web que se ejecuta localmente. Los puntos de conexión web del servidor están disponibles durante la sesión actual en el equipo. Cuando el equipo se apaga o se queda en reposo, el servicio ya no está disponible. |
| &nbsp; | [Portal para desarrolladores de Teams](https://dev.teams.microsoft.com/) | Portal basado en web para configurar, administrar y distribuir la aplicación Teams aplicación, incluida la organización o la Teams almacén. |

### <a name="build-your-teams-tab"></a>Crear la pestaña Teams usuario

Ahora vamos a crear la pestaña. Pero primero selecciona la pestaña que elijas para crear:

> [!div class="nextstepaction"]
> [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
> [!div class="nextstepaction"]
> [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>Consulte también

* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Pestañas en dispositivos móviles](~/tabs/design/tabs-mobile.md)