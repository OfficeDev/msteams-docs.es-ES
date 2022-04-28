---
title: Configuración del entorno de desarrollo para ampliar las aplicaciones de Teams entre Microsoft 365
description: Estos son los requisitos previos para ampliar las aplicaciones de Teams entre Microsoft 365
ms.date: 02/11/2022
ms.openlocfilehash: 094da29fdb871ef4af091e32e123e2d644b7445f
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104073"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Configuración del entorno de desarrollo para ampliar las aplicaciones de Teams entre Microsoft 365

> [!NOTE]
> La extensión de la aplicación de teams entre Microsoft 365 solo está disponible actualmente en versión [preliminar para desarrolladores públicos](~/resources/dev-preview/developer-preview-intro.md).

El entorno de desarrollo para ampliar Teams aplicaciones entre Microsoft 365 es similar al desarrollo de Microsoft Teams. En este artículo se describen las configuraciones específicas necesarias para ejecutar compilaciones en versión preliminar de aplicaciones de Microsoft Teams y Microsoft Office con el fin de obtener una vista previa de las aplicaciones Teams que se ejecutan en Outlook y Office.

Para configurar el entorno de desarrollo:

> [!div class="checklist"]
>
> * [Obtener Microsoft 365 inquilino del desarrollador (espacio aislado) y habilitar la instalación local](#prepare-a-developer-tenant-for-testing)
> * [Inscribir el inquilino de Microsoft 365 en *Office 365 versiones dirigidas*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Configuración de la cuenta para acceder a las versiones preliminares de Outlook y Office](#install-office-apps-in-your-test-environment)
> * [Cambie a la versión preliminar para desarrolladores de Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Opcional*] [Instalar Teams Toolkit extensión para código de Microsoft Visual Studio](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Preparación de un inquilino para desarrolladores para pruebas

Necesita un inquilino de espacio aislado de Microsoft 365 suscripción de desarrollador para configurar el entorno de desarrollo. Si aún no tiene uno, cree un [inquilino de espacio aislado](/office/developer-program/microsoft-365-developer-program-get-started) o obtenga un inquilino de prueba a través de su organización.

Después de tener un inquilino, debe habilitar la instalación local para el inquilino; consulte [Habilitación de la instalación local](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading). Para comprobar si la instalación de prueba está habilitada, inicie sesión en Teams, seleccione **Aplicaciones** y, a continuación, compruebe **Upload una opción de aplicación personalizada**.

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Upload una opción de aplicación personalizada":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Inscripción del inquilino para desarrolladores para Office 365 versiones dirigidas

> [!IMPORTANT]
> Consulte las actualizaciones más recientes de [Microsoft Teams- Microsoft 365 Blog para desarrolladores](https://devblogs.microsoft.com/microsoft365dev/) para comprobar si Outlook.com y Office.com admiten aplicaciones Teams están disponibles para el inquilino de prueba.

Para inscribir el inquilino de prueba para Office 365 versiones dirigidas:

1. Inicie sesión en [Centro de administración de Microsoft 365](https://admin.microsoft.com) con las credenciales del inquilino de prueba.
1. Vaya a **Configuración** >  **Org Configuración** >  **Perfil de organización**.
1. Seleccione **Preferencias de versión**.
1. Seleccione cualquier preferencia *de versión dirigida* :
    1. **Versión de destino para todos**
    1. **Versión de destino para usuarios seleccionados**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Centro de administración de Microsoft 365 menú &quot;Preferencias de versión&quot; con la opción de versión dirigida seleccionada":::

1. Seleccione **Guardar**.

Para obtener más información sobre Office 365 opciones de versión, consulte [Configuración de las opciones de versión estándar o de destino](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release) en *Centro de administración de Microsoft 365 ayuda*.

## <a name="install-office-apps-in-your-test-environment"></a>Instalación de aplicaciones Office en el entorno de prueba

> [!IMPORTANT]
> Consulte las actualizaciones más recientes de [Microsoft Teams- Microsoft 365 Blog para desarrolladores](https://devblogs.microsoft.com/microsoft365dev/) para comprobar si Outlook para Windows compatibilidad con el escritorio para Teams extensiones de mensaje está disponible para el inquilino de prueba.

Puede obtener una vista previa de Teams aplicaciones que se ejecutan en Outlook en Windows escritorio mediante una *compilación reciente del canal beta*. Compruebe si tiene que [cambiar el canal de actualización de Aplicaciones Microsoft 365](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) para que el inquilino de prueba instale una compilación de Office 365 canal beta.

Para instalar Office 365 aplicaciones de canal beta en el entorno de prueba:

1. Inicie sesión en el entorno de prueba con las credenciales del inquilino de prueba.
1. Descargue la [herramienta de implementación de Office](https://www.microsoft.com/download/details.aspx?id=49117) y extráigala en una carpeta local.
1. Vaya a la carpeta local y abra *configuration-Office365-x86.xml* (o **x64.xml*, dependiendo del entorno) en un editor de texto y actualice el valor *channel* a `BetaChannel`.
1. Abra el símbolo del sistema y vaya a la ruta de acceso de la carpeta local.
1. Ejecute `setup.exe /configure configuration-Office365-x86.xml` (o use el archivo **x64.xml* , en función de la configuración).
1. Abra Outlook (cliente de escritorio) y configure la cuenta de correo con las credenciales del inquilino de prueba.
1. Abra **File** >  **Office AccountAbout** >  **Outlook**.  
   Si el número de compilación es **14416** o superior y el canal es *Beta Channel*, ejecuta Microsoft 365 compilación de canal beta.
1. En la esquina superior derecha, active el botón de alternancia **Próximamente** .

    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Opción de alternancia &quot;Próximamente&quot; en Outlook":::

> [!NOTE]
> Es posible que tenga que cerrar Outlook y reiniciar el equipo para que aparezca el botón *Próximamente*.

Puede comprobar la compatibilidad de inquilinos de prueba para la cuenta de inquilino:

* Para Teams pestañas personales que se ejecutan en office.com, outlook.com y Outlook para Windows escritorio, inicie sesión con las credenciales del inquilino de prueba y compruebe si hay puntos suspensivos (**...**) en la barra lateral izquierda de Office o Outlook.

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Opción Puntos suspensivos ('...') en la barra lateral izquierda de Outlook":::

* En el caso de las extensiones de mensaje en outlook.com y Outlook para Windows, busque la opción **Más aplicaciones** en la parte inferior del panel Outlook redactar mensaje.

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Opción &quot;Más aplicaciones&quot; en el panel de mensajes Outlook redacción":::

> [!NOTE]
> Si ha optado por las versiones del canal beta, pero no ve estas opciones de puntos suspensivos, es probable que la compatibilidad con características en versión preliminar esté en proceso de implementación en el inquilino. Para obtener las actualizaciones más recientes, consulte [Microsoft Teams Blog para desarrolladores](https://devblogs.microsoft.com/microsoft365dev/).

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Cambie a la versión preliminar para desarrolladores de Teams

Asegúrese de cambiar a la [versión preliminar del desarrollador público](../resources/dev-preview/developer-preview-intro.md) desde el cliente de Microsoft Teams.

1. Inicie sesión en Teams con sus credenciales de inquilino de espacio aislado.
1. En el menú de puntos suspensivos (**...**) situado junto al perfil de usuario, seleccione **AboutDeveloper** preview (Acerca  > **de la versión preliminar del desarrollo**). Aparecerá un cuadro de diálogo y seleccione **Cambiar a la versión preliminar del desarrollador**.
1. Después de reiniciar la aplicación Teams, vaya al menú de puntos suspensivos (**...**) situado junto al perfil de usuario y compruebe si está seleccionada **la versión preliminar del desarrollador**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Opción de versión preliminar para desarrolladores públicos en Teams":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Instalar Visual Studio Code y Teams Toolkit extensión de versión preliminar

Opcionalmente, puede usar [Visual Studio Code](https://code.visualstudio.com/) para ampliar Teams aplicaciones a Office y Outlook.

La Teams Toolkit de extensión [para Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0` o posterior) proporciona comandos que pueden ayudar a modificar el código de Teams existente para que sea compatible con Outlook y Office. Para obtener más información, consulte [habilitar Teams pestaña personal para Office y Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-steps"></a>Siguientes pasos

* [Habilitar una pestaña personal de Teams para Office y Outlook](extend-m365-teams-personal-tab.md)
* [Habilitación de una extensión de mensaje de Teams para Outlook](extend-m365-teams-message-extension.md)
