---
title: Autenticación de inicio de sesión único con Team Toolkit y Visual Studio Code para pestañas
description: Crear una pestaña que admita el inicio de sesión único y las llamadas de Microsoft Graph directamente en Visual Studio Code con el kit de herramientas de Microsoft Teams
keywords: Teams Visual Studio Code Toolkit pestañas autenticación de gráfico de SSO plataforma de identidad de Azure
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: fe734143975688cd35c510cd68cd0779a2200a18
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2020
ms.locfileid: "49477739"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Autenticación de inicio de sesión único con Team Toolkit y Visual Studio Code para pestañas

El kit de herramientas de Microsoft Teams le permite crear una autenticación de inicio de sesión único (SSO) para las aplicaciones de pestaña directamente en Visual Studio Code. El kit de herramientas le guiará a través del proceso y le proporcionará todo lo que necesita, incluido el aprovisionamiento del registro de la plataforma de identidad de Microsoft en Azure portal.

## <a name="get-started--create-a-project"></a>Introducción: crear un proyecto

1. Cree un proyecto nuevo en el kit de herramientas.
1. Seleccione Tab como el tipo de extensión que quiera crear.
1. Seleccione la opción para admitir SSO.

> [!TIP]
> Después de la instalación, debería ver Team Toolkit en la barra de actividad del código de Visual Studio. Si no es así, haga clic con el botón derecho en la barra de actividad y seleccione **Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.

## <a name="configure-your-project"></a>Configurar el proyecto

1. Para habilitar el SSO dentro de Teams, la aplicación debe tener un recurso de registro de la aplicación de Azure. El kit de herramientas de Teams aprovisionará el registro de la aplicación en su nombre.
1. Escriba la dirección URL donde se hospedará la aplicación y seleccione **siguiente**. El registro de la aplicación se configurará con la dirección URL proporcionada.
1. Los detalles de configuración del registro de la aplicación se almacenarán en los `.env` archivos del código fuente del proyecto.

Si desea obtener más información sobre cómo se aprovisionará el registro de la aplicación de Azure, _consulte_  nuestra documentación [de pestañas de inicio de sesión único (SSO)](../tabs/how-to/authentication/auth-aad-sso.md) .

> [!TIP]
> Tendrá que ir a los registros de la **aplicación de Azure** y actualizar el URI de la *API* y *redirigir las direcciones URL* siempre que cambie esta dirección URL.

## <a name="run-your-project"></a>Ejecutar el proyecto

1. Seleccione **NPM install** desde la `api-server` carpeta. A continuación, **NPM Start**.
1. Seleccione **NPM install** desde la `.src` carpeta. A continuación, **NPM Start**.
1. Si usa un servicio de túnel como [ngrok](https://ngrok.com/), ejecútelo y asegúrese de que la dirección URL coincida con lo que escribió en el Asistente para creación de proyectos. Si no es así, tendrá que actualizar el URI de la _API_ y la _dirección URL de redireccionamiento_ en el registro de la aplicación que se creó en Azure.
1. Navegue a la barra de actividades en el lado izquierdo de la ventana de Visual Studio Code.
1. Seleccione el icono **Ejecutar** para mostrar la vista **Ejecutar y depurar** .
1. También puede usar el método abreviado de teclado **Ctrl + Mayús + D**.

> [!TIP]
> Es posible que no vea el cuadro de diálogo de instalación de la aplicación en el explorador si las ventanas emergentes están deshabilitadas para el explorador. Si esto ocurre, habilite las ventanas emergentes y actualice la página.

> [!div class="nextstepaction"]
> [Más información: crear aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio Code](visual-studio-code-overview.md)
