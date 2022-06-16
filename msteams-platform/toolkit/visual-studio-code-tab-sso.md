---
title: Autenticación de inicio de sesión único con el kit de herramientas de Teams y Visual Studio Code para pestañas
description: Cree una pestaña que admita el inicio de sesión único y las llamadas de Microsoft Graph directamente dentro de Visual Studio Code con el Microsoft Teams Toolkit.
keywords: las pestañas del kit de herramientas de visual Studio Code de teams firman la autenticación de grafos de la plataforma de identidad de Azure
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 7cca78c2ca3669d647dd76dd71e0a2b999b09dd1
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123874"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a>Autenticación de inicio de sesión único con el kit de herramientas de Teams y Visual Studio Code para pestañas

> [!IMPORTANT]
> **Este documento hace referencia a una versión anterior de Teams Toolkit**
>
> Para obtener información actual, lea los [requisitos previos](../get-started/prerequisites.md) y siga uno de los tutoriales más recientes.

El Microsoft Teams Toolkit permite crear la autenticación de inicio de sesión único (SSO) para las aplicaciones de pestaña directamente dentro de Visual Studio Code. El kit de herramientas le guía por el proceso y proporciona todo lo que necesita, incluido el aprovisionamiento del registro de Plataforma de identidad de Microsoft en el portal de Microsoft Azure.

## <a name="get-started--create-a-project"></a>Comenzar: creación de un proyecto

1. Cree un nuevo proyecto en el kit de herramientas.
1. Seleccione la pestaña como el tipo de extensión que desea crear.
1. Seleccione la opción para admitir el inicio de sesión único.

> [!TIP]
> Después de la instalación, debería ver el Teams Toolkit en la barra de actividad de Visual Studio Code. Si no es así, haga clic con el botón derecho en la barra de actividad y seleccione **Microsoft Teams** para anclar el kit de herramientas para facilitar el acceso.

## <a name="configure-your-project"></a>Configuración del proyecto

1. Para habilitar el inicio de sesión único en Teams, la aplicación debe tener un recurso de registro de aplicaciones de Azure. El Teams Toolkit aprovisionará el registro de la aplicación en su nombre.
1. Escriba la dirección URL donde se hospedará la aplicación y seleccione **Siguiente**. El registro de la aplicación se configurará mediante la dirección URL proporcionada.
1. Los detalles de configuración del registro de la aplicación se almacenarán en los `.env` archivos del código fuente del proyecto.

Si desea obtener más información sobre cómo se aprovisionará el registro de aplicaciones de Azure, *consulte*  nuestra documentación sobre [la compatibilidad del inicio de sesión único (SSO) con pestañas](../tabs/how-to/authentication/tab-sso-overview.md) .

> [!TIP]
> Tendrá que ir a **App de Azure Registros** y actualizar el *URI de API* y *las direcciones URL de redireccionamiento* cada vez que cambie esta dirección URL.

## <a name="run-your-project"></a>Ejecución del proyecto

1. Seleccione **npm instalar** en la `api-server` carpeta . A continuación **, npm empezar**.
1. Seleccione **npm instalar** en la `.src` carpeta . A continuación **, npm empezar**.
1. Si usa un servicio de tunelización como [ngrok](https://ngrok.com/), ejecútelo y asegúrese de que la dirección URL coincida con lo que especificó en el Asistente para la creación de proyectos. Si no es así, deberá actualizar el *URI de API* y la *dirección URL de redireccionamiento* en el registro de la aplicación que se creó en Azure.
1. Vaya a la barra de actividad del lado izquierdo de la ventana de Visual Studio Code.
1. Seleccione el icono **Ejecutar** para mostrar la vista **Ejecutar y depurar** .
1. También puede usar el método abreviado de teclado **Ctrl+Mayús+D**.

> [!TIP]
> Es posible que no vea el cuadro de diálogo de instalación de la aplicación en el explorador si las ventanas emergentes están deshabilitadas para el explorador. Si esto sucede, habilite las ventanas emergentes y actualice la página.

## <a name="see-also"></a>Consulte también

[Crear aplicaciones con el kit de herramientas de Microsoft Teams y Visual Studio Code](visual-studio-code-overview.md)
