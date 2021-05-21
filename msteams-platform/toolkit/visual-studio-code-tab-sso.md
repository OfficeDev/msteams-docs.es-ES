---
title: Autenticación de inicio de sesión único con Teams Toolkit y Visual Studio Code para pestañas
description: Cree una pestaña que admita el inicio de sesión único y microsoft Graph llamadas directamente dentro de Visual Studio Code con el Microsoft Teams Toolkit
keywords: Teams visual studio code toolkit tabs sso graph authentication Azure identity platform
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 11e642ce335dae4344f1c730b73763e9172fd76c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566834"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Autenticación de inicio de sesión único con Teams Toolkit y Visual Studio Code para pestañas

La Microsoft Teams Toolkit permite crear la autenticación de inicio de sesión único (SSO) para aplicaciones de pestañas directamente en Visual Studio Code. El kit de herramientas lo guía a través del proceso y proporciona todo lo que necesita, incluido el aprovisionamiento Plataforma de identidad de Microsoft registro en Azure Portal.

## <a name="get-started--create-a-project"></a>Introducción: crear un proyecto

1. Cree un nuevo proyecto en el kit de herramientas.
1. Seleccione la pestaña como el tipo de extensión que desea crear.
1. Seleccione la opción para admitir SSO.

> [!TIP]
> Después de la instalación, debería ver el Teams Toolkit en la barra Visual Studio Code actividad. Si no es así, haga clic con el botón secundario en la barra de actividades **y seleccione Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.

## <a name="configure-your-project"></a>Configurar el proyecto

1. Para habilitar SSO en Teams, la aplicación debe tener un recurso de registro de aplicaciones de Azure. El Teams Toolkit aprovisionará el registro de la aplicación en su nombre.
1. Escribe la dirección URL donde se hospedará la aplicación y selecciona **siguiente**. El registro de la aplicación se configurará con la dirección URL proporcionada.
1. Los detalles de configuración del registro de la aplicación se almacenarán en `.env` los archivos del código fuente del proyecto.

Si desea obtener más información sobre cómo se aprovisionará  el registro de la aplicación de Azure, consulte nuestra documentación sobre el inicio de sesión único [(SSO) para las pestañas.](../tabs/how-to/authentication/auth-aad-sso.md)

> [!TIP]
> Tendrá que ir a Registros de aplicaciones de **Azure** y actualizar el URI de *la API* y redirigir las direcciones *URL* siempre que cambie esta dirección URL.

## <a name="run-your-project"></a>Ejecutar el proyecto

1. Seleccione **npm install** en la `api-server` carpeta. A **continuación, npm start**.
1. Seleccione **npm install** en la `.src` carpeta. A **continuación, npm start**.
1. Si usa un servicio de túnel como [ngrok,](https://ngrok.com/)ejecutelo y asegúrese de que la dirección URL coincida con lo que ha escrito en el asistente para la creación del proyecto. Si no lo hace, deberá actualizar el URI de _la API_ y redirigir la _dirección URL_ en el registro de la aplicación que se creó en Azure.
1. Vaya a la barra de actividades de la parte izquierda de la ventana Visual Studio Code actividad.
1. Seleccione el **icono Ejecutar** para mostrar la vista **Ejecutar y** depurar.
1. También puede usar el método abreviado de **teclado Ctrl+Mayús+D**.

> [!TIP]
> Es posible que no veas el diálogo de instalación de la aplicación en el explorador si las ventanas emergentes están deshabilitadas para el explorador. Si esto sucede, habilita las ventanas emergentes y actualiza la página.

## <a name="see-also"></a>Consulte también

- [Crear aplicaciones con el Microsoft Teams Toolkit y Visual Studio Code](visual-studio-code-overview.md)
