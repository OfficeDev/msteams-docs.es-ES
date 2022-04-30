---
title: Configure el entorno de desarrollo para ampliar las aplicaciones de Teams en Microsoft 365
description: Estos son los requisitos previos para ampliar las aplicaciones de Teams en Microsoft 365
ms.date: 02/11/2022
ms.localizationpriority: high
ms.openlocfilehash: 483ae6982dd51a16573655ed14dc93577642ba4b
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111503"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Configure el entorno de desarrollo para ampliar las aplicaciones de Teams en Microsoft 365

> [!NOTE]
> La extensión de la aplicación de Teams en Microsoft 365 solo está disponible actualmente en [versión preliminar pública para desarrolladores](~/resources/dev-preview/developer-preview-intro.md).

El entorno de desarrollo para extender las aplicaciones de Teams en Microsoft 365 es similar al desarrollo de Microsoft Teams. En este artículo se describen las configuraciones específicas necesarias para ejecutar versiones preliminares de Microsoft Teams y aplicaciones de Microsoft Office con el fin de obtener una vista previa de las aplicaciones de Teams que se ejecutan en Outlook y Office.

Para configurar el entorno de desarrollo:

> [!div class="checklist"]
>
> * [Obtener el espacio empresarial de Microsoft 365 para desarrollador (Sandbox) y habilitar la carga lateral](#prepare-a-developer-tenant-for-testing)
> * [Inscribir el espacio empresarial de Microsoft 365 en *Versiones dirigidas de Office 365*](#enroll-your-developer-tenant-for-office-365-targeted-releases) 
> * [Configurar su cuenta para acceder a las versiones preliminares de Outlook y Office](#install-office-apps-in-your-test-environment)
> * [Cambiar a la versión preliminar para desarrolladores de Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Opcional*] [Instalar la extensión del kit de herramientas de Teams para Microsoft Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Preparar un inquilino de desarrollador para pruebas

Necesita un inquilino de espacio aislado de suscripción de desarrollador de Microsoft 365 para configurar el entorno de desarrollo. Si aún no tiene uno, cree un [inquilino de espacio aislado](/office/developer-program/microsoft-365-developer-program-get-started) u obtenga un inquilino de prueba a través de su organización.

Una vez tenga un inquilino, debe habilitar la instalación de prueba para el inquilino. Consulte [habilitar la instalación de prueba](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading). Para comprobar si la instalación de prueba está habilitada, inicie sesión en Teams, seleccione **Aplicaciones** y, a continuación, busque la opción **Cargar una aplicación personalizada**.

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Opción Cargar una aplicación personalizada":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Inscribir su espacio empresarial para desarrolladores en versiones dirigidas de Office 365

> [!IMPORTANT]
> Consulte las actualizaciones más recientes de [Microsoft Teams: blog de Microsoft 365 para desarrolladores](https://devblogs.microsoft.com/microsoft365dev/) para comprobar si la compatibilidad de Outlook.com y Office.com con aplicaciones de Teams está disponible para su cuenta empresarial de prueba.

Para inscribir el inquilino de prueba para las versiones dirigidas de Office 365:

1. Inicie sesión en [Centro de administración de Microsoft 365](https://admin.microsoft.com) con sus credenciales de inquilino de prueba.
1. Vaya a **Configuración** > **Configuración de la organización** > **Perfil de la organización**.
1. Seleccione **Preferencias de versión**.
1. Seleccione cualquier preferencia de *Versión dirigida*:
    1. **Versión dirigida para todos los usuarios**
    1. **Versión dirigida para los usuarios seleccionados**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Menú &quot;Preferencias de versión&quot; del Centro de administración de Microsoft 365 con la opción de versión dirigida seleccionada":::

1. Seleccione **Guardar**.

Para obtener más información sobre las opciones de versión de Office 365, consulte [Configurar las opciones de versión estándar o dirigida](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release) en la *ayuda del Centro de administración de Microsoft 365*.

## <a name="install-office-apps-in-your-test-environment"></a>Instalar aplicaciones de Office en el entorno de prueba

> [!IMPORTANT]
> Consulte las actualizaciones más recientes en [Microsoft Teams: blog de Microsoft 365 para desarrolladores](https://devblogs.microsoft.com/microsoft365dev/) para comprobar si la compatibilidad de escritorio de Outlook en Windows con las extensiones de mensaje de Teams está disponible para su espacio empresarial de prueba.

Puede obtener una vista previa de las aplicaciones de Teams que se ejecutan en Outlook en el escritorio de Windows mediante una *Compilación de Canal beta* reciente. Compruebe si tiene que [Cambiar el canal de actualización de aplicaciones de Microsoft 365](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) para que el inquilino de prueba instale una compilación de Office 365 Canal beta.

Para instalar aplicaciones de Office 365 Canal beta en el entorno de prueba:

1. Inicie sesión en el entorno de prueba con sus credenciales de inquilino de prueba.
1. Descargue la [Herramienta de implementación de Office](https://www.microsoft.com/download/details.aspx?id=49117) y extráigala en una carpeta local.
1. Vaya a la carpeta local y abra *configuration-Office365-x86.xml* (o **x64.xml*, en función de su entorno) en un editor de texto y actualice el valor del *Canal* a `BetaChannel`.
1. Abra el símbolo del sistema y vaya a la ruta de acceso de la carpeta local.
1. Ejecute `setup.exe /configure configuration-Office365-x86.xml` (o use el archivo **x64.xml*, según la configuración).
1. Abra Outlook (cliente de escritorio) y configure la cuenta de correo con sus credenciales de inquilino de prueba.
1. Abra **Archivo** > **Cuenta de Office** > **Acerca de Outlook**.  
   Si el número de compilación es **14416** o superior y el canal es *Canal beta*, está ejecutando la compilación de Canal beta de Microsoft 365.
1. En la esquina superior derecha, active el botón de alternancia en **Próximamente**.

    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Opción de alternancia &quot;Próximamente&quot; en Outlook":::

> [!NOTE]
> Es posible que tenga que cerrar Outlook y reiniciar el equipo para que aparezca el botón *Próximamente*.

Puede comprobar la compatibilidad del inquilino de prueba con su cuenta de inquilino:

* Para las pestañas personales de Teams que se ejecutan en office.com, outlook.com y Outlook para el escritorio de Windows, inicie sesión con las credenciales de inquilino de prueba y busque la opción de puntos suspensivos (**...**) en la barra lateral izquierda de Office o Outlook.

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Opción de puntos suspensivos (&quot;...&quot;) en la barra lateral izquierda de Outlook":::

* Para las extensiones de mensaje en outlook.com y Outlook para Windows, busque la opción **Más aplicaciones** en la parte inferior del panel de redacción de mensajes de Outlook.

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Opción &quot;Más aplicaciones&quot; en el panel de redacción de mensajes de Outlook":::

> [!NOTE]
> Si ha optado por versiones de Canal beta, pero no ve estas opciones de puntos suspensivos, es probable que la compatibilidad con características en versión preliminar esté en proceso de implementación en el inquilino. Para obtener las actualizaciones más recientes, consulte el [Blog para desarrolladores de Microsoft Teams](https://devblogs.microsoft.com/microsoft365dev/).

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Cambiar a la versión preliminar para desarrolladores de Teams

Asegúrese de cambiar a la [Versión preliminar pública para desarrolladores](../resources/dev-preview/developer-preview-intro.md) desde el cliente de Microsoft Teams.

1. Inicie sesión en Teams con sus credenciales de inquilino de espacio aislado.
1. En el menú de puntos suspensivos (**...**) situado junto a su perfil de usuario, seleccione **Acerca de** > **Versión preliminar del desarrollador**. Aparecerá un cuadro de diálogo, seleccione **Cambiar a la versión preliminar del desarrollador**.
1. Una vez reiniciada la aplicación de Teams, vaya al menú de puntos suspensivos (**...**) junto a su perfil de usuario y compruebe si la opción **Versión preliminar del desarrollador** está seleccionada.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Opción Versión preliminar pública para desarrolladores en Teams":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Instalar Visual Studio Code y la extensión de la versión preliminar del kit de herramientas de Teams

Opcionalmente, puede usar [Visual Studio Code](https://code.visualstudio.com/) para extender las aplicaciones de Teams a Office y Outlook.

La extensión [Kit de herramientas de Teams para Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0` o versiones posteriores) proporciona comandos que pueden ayudar a modificar el código de Teams existente para que sea compatible con Outlook y Office. Para obtener más información, consulte [habilitar la pestaña personal de Teams para Office y Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-steps"></a>Pasos siguientes

* [Habilitar una pestaña personal de Teams para Office y Outlook](extend-m365-teams-personal-tab.md)
* [Habilitar una extensión de mensaje de Teams para Outlook](extend-m365-teams-message-extension.md)
