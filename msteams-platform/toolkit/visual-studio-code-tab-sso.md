---
title: Autenticación de inicio de sesión único con Teams Toolkit y Visual Studio código para pestañas
description: Crear una pestaña que admita el inicio de sesión único y las llamadas de Microsoft Graph directamente dentro de Visual Studio Code con Microsoft Teams Toolkit
keywords: Teams visual studio code toolkit tabs sso graph authentication Azure identity platform
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: daf9a1b0bb64fee9584d0f58d749cf2b1ccaa4ef
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018428"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Autenticación de inicio de sesión único con Teams Toolkit y Visual Studio código para pestañas

Microsoft Teams Toolkit le permite crear autenticación de inicio de sesión único (SSO) para aplicaciones de pestañas directamente en Visual Studio código. El kit de herramientas le guía a través del proceso y proporciona todo lo que necesita, incluido el aprovisionamiento del registro de la plataforma de identidad de Microsoft en Azure Portal.

## <a name="get-started--create-a-project"></a>Introducción: crear un proyecto

1. Cree un nuevo proyecto en el kit de herramientas.
1. Seleccione la pestaña como el tipo de extensión que desea crear.
1. Seleccione la opción para admitir SSO.

> [!TIP]
> Después de la instalación, debería ver Teams Toolkit en la barra de Visual Studio de actividad Code. Si no es así, haga clic con el botón secundario en la barra de actividades y seleccione **Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.

## <a name="configure-your-project"></a>Configurar el proyecto

1. Para habilitar SSO en Teams, la aplicación debe tener un recurso de registro de aplicaciones de Azure. Teams Toolkit aprovisionará el registro de la aplicación en su nombre.
1. Escribe la dirección URL donde se hospedará la aplicación y selecciona **siguiente**. El registro de la aplicación se configurará con la dirección URL proporcionada.
1. Los detalles de configuración del registro de la aplicación se almacenarán en `.env` los archivos del código fuente del proyecto.

Si desea obtener más información sobre cómo se aprovisionará  el registro de la aplicación de Azure, consulte nuestra documentación sobre el inicio de sesión único [(SSO) para las pestañas.](../tabs/how-to/authentication/auth-aad-sso.md)

> [!TIP]
> Tendrá que ir a Registros de aplicaciones de **Azure** y actualizar el URI de *la API* y redirigir las direcciones *URL* siempre que cambie esta dirección URL.

## <a name="run-your-project"></a>Ejecutar el proyecto

1. Seleccione **npm install** en la `api-server` carpeta. A **continuación, npm start**.
1. Seleccione **npm install** en la `.src` carpeta. A **continuación, npm start**.
1. Si usa un servicio de túnel como [ngrok,](https://ngrok.com/)ejecutelo y asegúrese de que la dirección URL coincida con lo que ha escrito en el asistente para la creación del proyecto. Si no lo hace, deberá actualizar el URI de _la API_ y redirigir la _dirección URL_ en el registro de la aplicación que se creó en Azure.
1. Vaya a la barra de actividades en el lado izquierdo de la ventana Visual Studio Código.
1. Seleccione el **icono Ejecutar** para mostrar la vista **Ejecutar y** depurar.
1. También puede usar el método abreviado de **teclado Ctrl+Mayús+D**.

> [!TIP]
> Es posible que no veas el diálogo de instalación de la aplicación en el explorador si las ventanas emergentes están deshabilitadas para el explorador. Si esto sucede, habilita las ventanas emergentes y actualiza la página.

> [!div class="nextstepaction"]
> [Más información: Crear aplicaciones con Microsoft Teams Toolkit y Visual Studio code](visual-studio-code-overview.md)
