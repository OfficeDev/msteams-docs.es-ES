---
title: Crear aplicaciones con el Teams Toolkit y Visual Studio
description: Introducción a la creación de excelentes aplicaciones personalizadas directamente Visual Studio con el Microsoft Teams Toolkit
keywords: Kit de herramientas de visual studio de teams
localization_priority: Normal
ms.topic: overview
ms.author: johmil
ms.openlocfilehash: 6a0f466ba0d95312695be8b5460fc949e3f70811
ms.sourcegitcommit: 4ac93d69927791a8ccf678ca5ee83e63b51566b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/23/2021
ms.locfileid: "53095517"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>Crear aplicaciones con el Teams Toolkit y Visual Studio

El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de desarrollo integrado (IDE) de Visual Studio. El kit de herramientas de Microsoft Teams le orienta en el proceso y le ofrece todo lo que necesita para crear, depurar e iniciar su aplicación de Teams.

## <a name="prerequisites"></a>Requisitos previos

1. [Habilitar la vista previa del desarrollador](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).

2. Asegúrese de que el **<span>ASP.NET</span> y el** módulo de desarrollo web se han agregado a la instancia Visual Studio web. Para obtener más información, [vea Modify Visual Studio by adding or removing workloads and components](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true).

![Módulo de asp.net Visual studio](../assets/images/visual-studio-web-dev-module.png)

## <a name="install-the-teams-toolkit"></a>Instale el Teams Toolkit

El Microsoft Teams Toolkit para Visual Studio está disponible para su descarga desde [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit) o directamente desde el menú **Extensiones** de Visual Studio.

## <a name="use-the-toolkit"></a>Usar el kit de herramientas

- [Configurar un nuevo proyecto](#set-up-a-new-teams-project)
- [Configurar la aplicación](#configure-your-app)
- [Ejecute la aplicación en Teams](#install-and-run-your-app-locally)
- [Valide su aplicación](#validate-your-app)
- [Publicar la aplicación](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurar un nuevo proyecto Teams proyecto

1. Inicie Visual Studio 2019.
2. Seleccione **Crear un nuevo proyecto**.
3. Busque la **Microsoft Teams y** seleccione **Siguiente**.
4. En Configure **your new project**, escriba el nombre **Project**, **Location** y **Solution name**.
5. Selecciona **Siguiente** para escribir un nombre para la aplicación.
6. En la pantalla Información adicional, escribe **un** nombre de aplicación y un nombre de **desarrollador** o compañía para tu Teams aplicación.

## <a name="configure-your-app"></a>Configurar la aplicación

En su núcleo, la aplicación Teams abarca tres componentes:

- El Microsoft Teams (web, de escritorio o móvil) donde los usuarios interactúan con la aplicación.
- Un servidor que responde a las solicitudes de contenido que se muestran en Teams. Por ejemplo, contenido de pestaña HTML o una tarjeta adaptable de bot.
- Un Teams de la aplicación consta de tres archivos:

    > [!div class="checklist"]
    >
    > - El manifest.jsen
    > - Icono [de color para](../resources/schema/manifest-schema.md#icons) que la aplicación se muestre en el catálogo de aplicaciones públicas u de la organización.
    > - Icono [de esquema para](../resources/schema/manifest-schema.md#icons) mostrar en la barra Teams actividad.

Cuando se instala una aplicación, el cliente Teams analiza el archivo de manifiesto para determinar la información necesaria, como el nombre de la aplicación y la dirección URL donde se encuentran los servicios.

> [!NOTE]
>Si aún no lo ha hecho, debe iniciar sesión en su cuenta de Microsoft 365 para continuar con el proceso de desarrollo.
>
> Si no tiene una cuenta Microsoft 365, puede registrarse para una suscripción Microsoft 365 [Programa para desarrolladores.](https://developer.microsoft.com/microsoft-365/dev-program) Es gratuito durante 90 días y se renueva siempre que lo use para la actividad de desarrollo. Si tiene una suscripción Visual Studio Enterprise o Professional, ambos programas incluyen una suscripción Microsoft 365 desarrollador [gratuita,](https://aka.ms/MyVisualStudioBenefits)activa durante la vida de su Visual Studio suscripción. Para obtener más información, vea [Configurar una Microsoft 365 de desarrollador](/office/developer-program/office-365-developer-program-get-started).

### <a name="configuration-steps"></a>Pasos de la configuración 

1. Para configurar la aplicación, selecciona el menú **Project > TeamsFx > Configurar para SSO....**

Cuando se le pida, inicie sesión en su cuenta microsoft que tenga un inquilino M365.

## <a name="install-and-run-your-app-locally"></a>Instalar y ejecutar la aplicación localmente

Presione F5 para iniciar la depuración. El cuadro de diálogo de instalación de la aplicación aparece en el Teams cliente.

## <a name="validate-your-app"></a>Valide su aplicación

El **Project > TeamsFx Validate > Teams manifest** permite comprobar que el paquete de la aplicación es válido.

## <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

En el Portal de desarrolladores de [Teams,](https://dev.teams.microsoft.com/home)puedes cargar la aplicación en un equipo, enviar la aplicación a la tienda de aplicaciones personalizada de tu empresa para los usuarios de tu organización o enviar la aplicación a App Source para todos los usuarios Teams usuario.

- El administrador de TI revisará estas entregas.
- Puedes volver a la **página Publicar** para comprobar el estado del envío y saber si tu administrador de TI aprobó o rechazó la aplicación. Aquí también puedes enviar actualizaciones a la aplicación o cancelar cualquier envío activo actualmente.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear y ejecutar la primera aplicación Microsoft Teams con Blazor](../get-started/first-app-blazor.md)
