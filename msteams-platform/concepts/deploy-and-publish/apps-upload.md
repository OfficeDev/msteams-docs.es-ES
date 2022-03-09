---
title: Cargar la aplicación personalizada
description: Obtenga información sobre cómo transferir localmente la aplicación en Microsoft Teams. La transferencia local es común al probar y depurar una aplicación durante el desarrollo.
ms.topic: how-to
author: surbhigupta
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: d602750a8f41d8331f30d64e06b2aafb026e0ff4
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356283"
---
# <a name="upload-your-app-in-microsoft-teams"></a>Cargar la aplicación en Microsoft Teams

Puede cargar lateralmente las aplicaciones de Microsoft Teams sin tener que publicarlas en su organización o en la tienda de Teams. Esto tiene sentido en los siguientes escenarios:

* Quiere probar y depurar una aplicación de manera local usted mismo o con otros desarrolladores.
* Ha creado una aplicación solo para usted. Por ejemplo, para automatizar un flujo de trabajo.
* Ha creado una aplicación para un pequeño conjunto de usuarios, como el grupo de trabajo.

> [!IMPORTANT]
> En este momento, la transferencia local de aplicaciones está disponible en Government Community Cloud (GCC), pero no está disponible para GCC-High ni para el Departamento de Defensa (DOD).

## <a name="prerequisites"></a>Requisitos previos

* Cree el [paquete de la aplicación](~/concepts/build-and-test/apps-package.md) y [valídelo](https://dev.teams.microsoft.com/appvalidation.html) para encontrar errores.
* [Habilite la carga de aplicaciones personalizadas](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) en Teams.
* Asegúrese de que la aplicación se está ejecutando y que sea accesible a través de HTTPs.

## <a name="upload-your-app"></a>Cargar la aplicación

Puede transferir localmente la aplicación a un equipo, chat, reunión o para su uso personal en función de cómo haya configurado el ámbito de la aplicación.

1. Inicie sesión en el cliente de Teams con su [cuenta de desarrollo de Microsoft 365](~/build-your-first-app/build-and-run.md#prerequisites).
1. Seleccione **Aplicaciones** y elija **Cargar una aplicación personalizada**.
1. Seleccione el archivo .zip del paquete de la aplicación. Se muestra un cuadro de diálogo de instalación.
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Recorte de pantalla que muestra un ejemplo de un cuadro de diálogo de instalación de aplicación de Teams.":::
1. Agregue la aplicación a Teams.

> [!NOTE]
> El método `onInstallationUpdateActivityAsync()` se usa para obtener la configuración regional de Microsoft Teams al agregar el bot a Microsoft Teams.

## <a name="troubleshoot-upload-issues"></a>Solucionar problemas de carga

Si la aplicación no se puede transferir localmente, haga lo siguiente hasta que se resuelva el problema:

1. Vuelva a las instrucciones para [crear el paquete de la aplicación](../../concepts/build-and-test/apps-package.md).
1. Vuelva a [validar el paquete de la aplicación](https://dev.teams.microsoft.com/appvalidation.html).
1. Asegúrese de que el manifiesto de la aplicación coincide con el último [esquema](../../resources/schema/manifest-schema.md).

## <a name="access-your-app"></a>Acceder a la aplicación

Teams proporciona varias maneras de abrir aplicaciones. Para obtener más información, consulte [acceso a las aplicaciones en Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

## <a name="update-your-app"></a>Actualizar la aplicación

No tiene que transferir localmente la aplicación de nuevo si realiza cambios de código (estos se reflejan en Teams en tiempo real). Sin embargo, debe reinstalar si cambia alguna configuración de aplicación.

## <a name="remove-your-app"></a>Quitar la aplicación

Para quitar la aplicación, haga clic con el botón derecho en el icono de la aplicación en Teams y seleccione **Desinstalar**.

> [!NOTE]
> No puede eliminar por completo la actividad del bot personal. Si elimina la aplicación y la vuelve a agregar, la nueva comunicación con el bot se anexa a la conversación anterior con él.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Usar la aplicación Teams](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)

## <a name="see-also"></a>Vea también

* [Configurar las opciones de instalación predeterminadas](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [Mantener la aplicación publicada de Microsoft Teams](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
