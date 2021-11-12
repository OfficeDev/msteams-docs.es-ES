---
title: Upload aplicación personalizada
description: Aprende a descargar localmente la aplicación en Microsoft Teams. La instalación local es común al probar y depurar una aplicación durante el desarrollo.
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: e14e521941d253a3f259cf93f36bff4d620d55f2
ms.sourcegitcommit: 1431dfe08d5a19a63dbf1542a2e6c661e4dd7fc1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2021
ms.locfileid: "60949064"
---
# <a name="upload-your-app-in-microsoft-teams"></a>Upload la aplicación en Microsoft Teams

Puedes descargar localmente Microsoft Teams aplicaciones sin tener que publicar en tu organización o en la Teams local. Esto tiene sentido en los siguientes escenarios:

* Quieres probar y depurar una aplicación localmente tú mismo o con otros desarrolladores.
* Has creado una aplicación solo para ti. Por ejemplo, para automatizar un flujo de trabajo.
* Has creado una aplicación para un pequeño conjunto de usuarios, como el grupo de trabajo.

> [!IMPORTANT]
> Actualmente, las aplicaciones de instalación local están disponibles en Government Community Cloud (GCC), pero no están disponibles para GCC-High y departamento de defensa (DOD).

## <a name="prerequisites"></a>Requisitos previos

* Crea el [paquete de la aplicación](~/concepts/build-and-test/apps-package.md) y [valida los](https://dev.teams.microsoft.com/appvalidation.html) errores.
* [Habilitar la carga de aplicaciones personalizadas](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) en Teams.
* Asegúrate de que la aplicación se ejecuta y se puede acceder a través de HTTP.

## <a name="upload-your-app"></a>Cargar la aplicación

Puedes descargar localmente la aplicación en un equipo, chat, reunión o para uso personal en función de cómo configuraste el ámbito de la aplicación.

1. Inicie sesión en el Teams con su [Microsoft 365 de desarrollo](~/build-your-first-app/build-and-run.md#prerequisites).
1. Selecciona **Aplicaciones** y elige **Upload una aplicación personalizada.**
1. Selecciona el paquete de la aplicación .zip archivo. Se muestra un cuadro de diálogo de instalación.
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Captura de pantalla que muestra un ejemplo de un Teams de instalación de la aplicación.":::
1. Agrega la aplicación a Teams.

## <a name="troubleshoot-upload-issues"></a>Solucionar problemas de carga

Si la aplicación no puede realizar la instalación local, haga lo siguiente hasta que se resuelva el problema:

1. Vuelva a las instrucciones para [crear el paquete de la aplicación](../../concepts/build-and-test/apps-package.md).
1. [Valide de nuevo el paquete de](https://dev.teams.microsoft.com/appvalidation.html) la aplicación.
1. Asegúrate de que el manifiesto de la aplicación coincida con el esquema [más reciente.](../../resources/schema/manifest-schema.md)

## <a name="access-your-app"></a>Acceder a la aplicación

Teams varias formas de abrir aplicaciones. Para obtener más información, [vea access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

## <a name="update-your-app"></a>Actualizar la aplicación

No tienes que volver a cargar localmente la aplicación si realizas cambios de código (estos se reflejan en Teams en tiempo real). Sin embargo, debes reinstalar si cambias las configuraciones de la aplicación.

## <a name="remove-your-app"></a>Quitar la aplicación

Para quitar la aplicación, haz clic con el botón secundario en el icono de la Teams y selecciona **Desinstalar**.

> [!NOTE]
> No puedes quitar completamente la actividad del bot personal. Si quitas la aplicación y la vuelves a agregar, la nueva comunicación con el bot se anexa a la conversación anterior con ella.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Usar la Teams aplicación](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)

## <a name="see-also"></a>Consulte también

* [Configurar las opciones de instalación predeterminadas](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [Mantener la aplicación Microsoft Teams publicada](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
