---
title: Upload la aplicación personalizada
description: Obtén información sobre cómo descargar tu aplicación de forma lateral en Microsoft Teams. La carga lateral es común al probar y depurar una aplicación durante el desarrollo.
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 39e94317ceb615ecd7d5481276ffafed5afe5cde
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565196"
---
# <a name="upload-your-app-in-microsoft-teams"></a>Upload la aplicación en Microsoft Teams

Puede descargar Microsoft Teams aplicaciones sin tener que publicar en su organización o en la tienda de Teams. Esto tiene sentido en los siguientes escenarios:

* Desea probar y depurar una aplicación localmente usted mismo o con otros desarrolladores.
* Usted construyó una aplicación sólo para usted. Por ejemplo, para automatizar un flujo de trabajo.
* Ha creado una aplicación para un pequeño conjunto de usuarios, como el grupo de trabajo.

## <a name="prerequisites"></a>Requisitos previos

* Cree el [paquete de la aplicación](~/concepts/build-and-test/apps-package.md) y valide para [errores.](https://dev.teams.microsoft.com/appvalidation.html)
* [Habilite la carga de aplicaciones personalizadas](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) en Teams.
* Asegúrese de que la aplicación se está ejecutando y accesible a través de HTTPs.

## <a name="upload-your-app"></a>Cargar la aplicación

Puedes descargar tu aplicación en un equipo, chatear, reunión o para uso personal en función de cómo hayas configurado el ámbito de la aplicación.

1. Inicie sesión en el cliente Teams con su [cuenta de desarrollo de Microsoft 365.](~/build-your-first-app/build-and-run.md#prerequisites)
1. Seleccione **Aplicaciones** y elija **Upload una aplicación personalizada.**
1. Seleccione el paquete de la aplicación .zip archivo. Aparece un cuadro de diálogo de instalación.
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Captura de pantalla que muestra un ejemplo de un cuadro de diálogo de instalación de Teams aplicación.":::
1. Agrega tu aplicación a Teams.

## <a name="troubleshoot-upload-issues"></a>Solucionar problemas de carga

Si la aplicación no se puede descargar de lado, haga lo siguiente hasta que se resuelva el problema:

1. Vuelve a consultar las instrucciones para [crear el paquete de la aplicación.](../../concepts/build-and-test/apps-package.md)
1. [Valide el paquete de la aplicación](https://dev.teams.microsoft.com/appvalidation.html) de nuevo.
1. Asegúrese de que el manifiesto de la aplicación coincida con el [esquema](../../resources/schema/manifest-schema.md)más reciente.

## <a name="access-your-app"></a>Accede a tu aplicación

Teams proporciona varias maneras de abrir aplicaciones. Para obtener más información, consulta [acceder a tus aplicaciones en Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

## <a name="update-your-app"></a>Actualiza tu aplicación

No es que volver a cargar la aplicación si realiza cambios de código (estos se reflejan en Teams en tiempo real). Sin embargo, debe reinstalar si cambia las configuraciones de la aplicación.

## <a name="remove-your-app"></a>Elimina tu aplicación

Para quitar la aplicación, haga clic con el botón derecho en el icono de la aplicación en Teams y seleccione **Desinstalar**.

> [!NOTE]
> No puede eliminar por completo la actividad personal del bot. Si quitas la aplicación y la vuelves a agregar, la nueva comunicación con el bot se anexa a la conversación anterior con ella.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Usa tu aplicación de Teams](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
