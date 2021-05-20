---
title: Autenticación de inicio de sesión único con Teams Toolkit y Visual Studio Code para pestañas
description: Cree una pestaña que admita llamadas de inicio de sesión único y Microsoft Graph directamente dentro de Visual Studio Code con la Microsoft Teams Toolkit
keywords: equipos visual studio toolkit pestañas sso graph authentication Plataforma de identidad de Azure
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

El Microsoft Teams Toolkit le permite crear autenticación de inicio de sesión único (SSO) para aplicaciones de pestañas directamente dentro de Visual Studio Code. El kit de herramientas le guía a través del proceso y proporciona todo lo que necesita, incluido el aprovisionamiento del registro de Plataforma de identidad de Microsoft en Azure Portal.

## <a name="get-started--create-a-project"></a>Empezar: cree un proyecto

1. Cree un nuevo proyecto en el kit de herramientas.
1. Seleccione la pestaña como el tipo de extensión que desea crear.
1. Seleccione la opción para admitir SSO.

> [!TIP]
> Después de la instalación, debería ver la Teams Toolkit en la barra de actividades Visual Studio Code. Si no es así, haga clic con el botón derecho en la barra de actividades y seleccione **Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.

## <a name="configure-your-project"></a>Configure el proyecto

1. Para habilitar SSO dentro de Teams, la aplicación debe tener un recurso de registro de aplicaciones de Azure. El Teams Toolkit aprovisionará el registro de la aplicación en su nombre.
1. Escriba la dirección URL donde se hospedará la aplicación y seleccione **la siguiente**. El registro de la aplicación se configurará con la dirección URL proporcionada.
1. Los detalles de configuración del registro de la aplicación se almacenarán en los `.env` archivos del código fuente del proyecto.

Si desea obtener más información sobre cómo se aprovisionará el registro de la aplicación de Azure, _consulte_ nuestra [compatibilidad con el inicio de sesión único (SSO) para obtener documentación sobre pestañas.](../tabs/how-to/authentication/auth-aad-sso.md)

> [!TIP]
> Deberá ir a **Azure App Registrations** y actualizar el *URI* de la API y *redirigir las direcciones URL* cada vez que cambie esta dirección URL.

## <a name="run-your-project"></a>Ejecute su proyecto

1. Seleccione **npm install** en la `api-server` carpeta. A **continuación, npm iniciar**.
1. Seleccione **npm install** en la `.src` carpeta. A **continuación, npm iniciar**.
1. Si está utilizando un servicio de tunelización como [ngrok,](https://ngrok.com/)ejecute y asegúrese de que la dirección URL coincide con lo que ha especificado en el asistente de creación de proyectos. Si no es así, deberá actualizar el _URI_ de la API y _redirigir_ la dirección URL en el registro de la aplicación que se creó en Azure.
1. Vaya a la barra de actividades en el lado izquierdo de la ventana de Visual Studio Code.
1. Seleccione el icono **Ejecutar** para mostrar la vista **Ejecutar y depurar.**
1. También puede utilizar el método abreviado de teclado **Ctrl+Mayús+D**.

> [!TIP]
> Es posible que no vea el diálogo de instalación de la aplicación en el explorador si las ventanas emergentes están deshabilitadas para su navegador. Si esto sucede, habilite las ventanas emergentes y actualice la página.

## <a name="see-also"></a>Vea también

- [Cree aplicaciones con el Microsoft Teams Toolkit y el Visual Studio Code](visual-studio-code-overview.md)
