---
title: Configure el entorno de desarrollo para ampliar las aplicaciones de Teams en Microsoft 365
description: Estos son los requisitos previos para ampliar las aplicaciones de Teams en Microsoft 365
ms.date: 05/24/2022
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: aede01c48f9e5e4ddbfbfebac9a5fa504225ca62
ms.sourcegitcommit: 1e77573e47fad51a19545949fdac1241b13052e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656183"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Configure el entorno de desarrollo para ampliar las aplicaciones de Teams en Microsoft 365

El entorno de desarrollo para extender las aplicaciones de Teams en Microsoft 365 es similar al desarrollo de Microsoft Teams. En este artículo se describen las configuraciones específicas necesarias para ejecutar versiones preliminares de Microsoft Teams y aplicaciones de Microsoft Office con el fin de obtener una vista previa de las aplicaciones de Teams que se ejecutan en Outlook y Office.

Para configurar el entorno de desarrollo:

> [!div class="checklist"]
>
> * [Obtener el espacio empresarial de Microsoft 365 para desarrollador (Sandbox) y habilitar la carga lateral](#prepare-a-developer-tenant-for-testing)
> * [Inscribir el espacio empresarial de Microsoft 365 en *Versiones dirigidas de Office 365*](#enroll-your-developer-tenant-for-office-365-targeted-releases) 
> * [Instalar compilaciones del Canal beta de Aplicaciones de Microsoft 365 en el entorno de prueba](#install-office-apps-in-your-test-environment)
> * [Cambiar a la versión preliminar para desarrolladores de Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Opcional*] [Instalar la extensión del kit de herramientas de Teams para Microsoft Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Preparar un inquilino de desarrollador para pruebas

Necesita un inquilino de espacio aislado de suscripción de desarrollador de Microsoft 365 para configurar el entorno de desarrollo. Si aún no tiene uno, cree un [inquilino de espacio aislado](/office/developer-program/microsoft-365-developer-program-get-started) u obtenga un inquilino de prueba a través de su organización.

También deberá habilitar la instalación de prueba para el inquilino:

1. Inicie sesión en el centro de administración de Microsoft 365 (https://admin.microsoft.com) con las credenciales del inquilino de prueba y seleccione **Teams** desde el panel lateral para abrir el *centro de administración de Microsoft Teams*
1. Seleccione: Aplicaciones de Teams > Administrar aplicaciones > **Configuración de la aplicación para toda la organización**
1. En **Aplicaciones personalizadas**, active la opción *Interacción con aplicaciones personalizadas*

    :::image type="content" source="images/teams-admin-enable-sideloading.png" alt-text="Habilitar la instalación de prueba para aplicaciones personalizadas desde el centro de administración de Teams":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Inscribir su espacio empresarial para desarrolladores en versiones dirigidas de Office 365

> [!Important]
> Puede tardar hasta cinco días después de crear un [espacio aislado de desarrollador de Microsoft 365](/office/developer-program/microsoft-365-developer-program-get-started) e inscribirse en [versiones de Office 365 dirigidas](#enroll-your-developer-tenant-for-office-365-targeted-releases) para que las aplicaciones de Teams transferidas localmente aparezcan en Outlook y Office.

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

Puede obtener una vista previa de las aplicaciones de Teams que se ejecutan en Outlook en el escritorio de Windows mediante una *Compilación de Canal beta* reciente. Compruebe si tiene que [Cambiar el canal de actualización de aplicaciones de Microsoft 365](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) para que el inquilino de prueba instale una compilación de Office 365 Canal beta.

Para instalar aplicaciones de Office 365 Canal beta en el entorno de prueba:

1. Inicie sesión en el entorno de prueba con sus credenciales de inquilino de prueba.
1. Descargue la [Herramienta de implementación de Office](https://www.microsoft.com/download/details.aspx?id=49117) y extráigala en una carpeta local.
1. Vaya a la carpeta local y abra *configuration-Office365-x86.xml* (o **x64.xml*, en función de su entorno) en un editor de texto y actualice el valor del *Canal* a `BetaChannel`.
1. Abra el símbolo del sistema y vaya a la ruta de acceso de la carpeta local.
1. Ejecute `setup.exe /configure configuration-Office365-x86.xml` (o use el archivo **x64.xml*, según la configuración).
1. Abra Outlook (cliente de escritorio) y configure la cuenta de correo con sus credenciales de inquilino de prueba.
1. Abrir **Archivo** > **Cuenta de Office** > **Acerca de Outlook** para confirmar que está ejecutando una compilación de Outlook del *Canal beta* de Microsoft 365.

    :::image type="content" source="images/outlook-about-beta-channel.png" alt-text="Vaya a &quot;Acerca de Outlook&quot; desde la cuenta de Office para comprobar que está ejecutando una compilación del Canal beta.":::

1. Compruebe que *Microsoft Edge WebView2 Runtime* esté instalado. En Windows, abra **Inicio** > **Aplicaciones y características** y busque **vista web**:

    :::image type="content" source="images/windows-addremove-webview2.png" alt-text="Buscar &quot;vista web&quot; en &quot;Aplicaciones y características&quot; en la configuración de Windows":::

    Si no aparece, instale [Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) en el entorno de prueba.

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Cambiar a la versión preliminar para desarrolladores de Teams

Asegúrese de cambiar a la [Versión preliminar pública para desarrolladores](../resources/dev-preview/developer-preview-intro.md) desde el cliente de Microsoft Teams.

1. Inicie sesión en Teams con sus credenciales de inquilino de espacio aislado.
1. En el menú de puntos suspensivos (**...**) situado junto a su perfil de usuario, seleccione **Acerca de** > **Versión preliminar del desarrollador**. Aparecerá un cuadro de diálogo, seleccione **Cambiar a la versión preliminar del desarrollador**.
1. Una vez reiniciada la aplicación de Teams, vaya al menú de puntos suspensivos (**...**) junto a su perfil de usuario y compruebe si la opción **Versión preliminar del desarrollador** está seleccionada.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Opción Versión preliminar pública para desarrolladores en Teams":::

## <a name="install-visual-studio-code-and-teams-toolkit-extension"></a>Instalar Visual Studio Code y la extensión kit de herramientas de Teams

Opcionalmente, puede usar [Visual Studio Code](https://code.visualstudio.com/) para extender las aplicaciones de Teams a Office y Outlook.

La extensión [Kit de herramientas de Teams para Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0` o posterior) proporciona comandos que pueden ayudar a modificar el código de Teams existente para que sea compatible con Outlook y Office. Para obtener más información, vea [habilitar la pestaña Personal de Teams para Office y Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-step"></a>Paso siguiente

Crear o actualizar una aplicación de Teams para que se ejecute en Microsoft 365:

* [Habilitar una pestaña personal de Teams para Office y Outlook](extend-m365-teams-personal-tab.md)
* [Habilitar una extensión de mensaje de Teams para Outlook](extend-m365-teams-message-extension.md)
