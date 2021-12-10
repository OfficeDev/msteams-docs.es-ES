---
title: Configurar el entorno de desarrollo para ampliar Teams aplicaciones en Microsoft 365
description: Estos son los requisitos previos para extender las aplicaciones Teams en Microsoft 365
ms.date: 11/15/2021
ms.topic: how-to
ms.custom: m365apps
ms.openlocfilehash: 2b11f940eba27fb3a2f44a89f3617d9d932881a7
ms.sourcegitcommit: 97a64453410edbd2ba28e7a04e9c3a54bf48f4f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2021
ms.locfileid: "61391724"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-m365"></a>Configurar el entorno de desarrollo para ampliar Teams aplicaciones en M365

> [!NOTE]
> Extender la aplicación de teams Microsoft 365 está disponible actualmente solo en [la versión preliminar del desarrollador público.](~/resources/dev-preview/developer-preview-intro.md)

El entorno de desarrollo para extender Teams aplicaciones en Microsoft 365 es similar al Microsoft Teams desarrollo. Este artículo describe las configuraciones específicas necesarias para ejecutar compilaciones de vista previa de aplicaciones Microsoft Teams y Microsoft Office con el fin de obtener una vista previa de las aplicaciones Teams que se ejecutan en Outlook y Office.

Para configurar el entorno de desarrollo:

> [!div class="checklist"]
> * [Obtener inquilino de M365 Developer (sandbox) y habilitar la instalación local](#prepare-a-developer-tenant-for-testing)
> * [Inscribir el inquilino M365 *en Office 365 versiones dirigidas*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Configurar la cuenta para obtener acceso a las versiones preliminares de Outlook y Office](#install-office-apps-in-your-test-environment)
> * [Cambie a la versión de vista previa del desarrollador de Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Opcional*] [Instalar Teams Toolkit extensión para Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Preparar un inquilino para desarrolladores para pruebas

Necesita un espacio aislado Microsoft 365 suscripción de desarrollador para configurar el entorno de desarrollo. Si aún no tiene uno, cree un espacio aislado [o](/office/developer-program/microsoft-365-developer-program-get-started) obtenga un espacio empresarial de prueba a través de su organización.

Después de tener un inquilino, debe habilitar la instalación local para el inquilino, vea [enable sideloading](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading). Para comprobar si la instalación local está habilitada, inicie  sesión en Teams, seleccione Aplicaciones y, a continuación, compruebe si Upload **una opción de aplicación** personalizada.

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Upload una opción de aplicación personalizada":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Inscribir el inquilino del desarrollador para Office 365 versiones dirigidas

> [!IMPORTANT]
> Consulta las actualizaciones más recientes de [Microsoft Teams:](https://devblogs.microsoft.com/microsoft365dev/) blog para desarrolladores de Microsoft 365 para comprobar si la compatibilidad de Outlook.com y Office.com para Teams aplicaciones está disponible para el inquilino de prueba.

Para inscribir el inquilino de prueba Office 365 versiones dirigidas:

1. Inicie sesión en [Centro de administración de Microsoft 365](https://admin.microsoft.com) con las credenciales del inquilino de prueba.
1. Vaya a **Configuración**  >  **org Configuración** perfil de  >  **organización**.
1. Seleccione **Preferencias de versión**.
1. Seleccione cualquier *preferencia de versión dirigida:*
    1. **Versión de destino para todos**
    1. **Versión de destino para usuarios seleccionados**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Centro de administración de Microsoft 365 menú &quot;Preferencias de publicación&quot; con la opción de versión dirigida seleccionada":::
    
1. Haga clic en **Guardar**.

Para obtener más información sobre Office 365 de lanzamiento, vea Configurar las opciones [de](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release) versión estándar o dirigida *en Centro de administración de Microsoft 365 ayuda*.

## <a name="install-office-apps-in-your-test-environment"></a>Instalar Office aplicaciones en el entorno de prueba

> [!IMPORTANT]
> Consulte las actualizaciones más recientes de [Microsoft Teams:](https://devblogs.microsoft.com/microsoft365dev/) blog para desarrolladores de Microsoft 365 para comprobar si Outlook la compatibilidad de escritorio Windows para las extensiones de mensaje de Teams está disponible para el inquilino de prueba.

Puedes obtener una vista previa Teams aplicaciones que se ejecutan en Outlook en Windows escritorio mediante una compilación *reciente del Canal Beta*. Compruebe si tiene que cambiar el canal de [actualización Aplicaciones Microsoft 365](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) para que el inquilino de prueba instale una Office 365 beta channel.

Para instalar Office 365 de canal beta en el entorno de prueba:

1. Inicie sesión en el entorno de prueba con las credenciales del inquilino de prueba.
1. Descargue la [Office de implementación y](https://www.microsoft.com/download/details.aspx?id=49117) extraiga en una carpeta local.
1. Vaya a la carpeta local y abra *configuration-Office365-x86.xml* (o **x64.xml*, según su entorno) en un editor de texto y actualice el valor *channel* a `BetaChannel` .
1. Abra el símbolo del sistema y vaya a la ruta de acceso de carpeta local.
1. Ejecute `setup.exe /configure configuration-Office365-x86.xml` (o use el archivo **x64.xml,* según la configuración).
1. Abra Outlook (cliente de escritorio) y configure la cuenta de correo con las credenciales de inquilino de prueba.
1. Abrir **archivo**  >  **Office cuenta acerca** de  >  **Outlook**.  
   Si el número de compilación es **14416** o superior y el canal es *Canal beta,* estás ejecutando Microsoft 365 de canal beta.
1. En la esquina superior derecha, activa el botón **de alternancia Próximamente.**
    
    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Más aplicaciones":::

> [!NOTE]
> Es posible que deba cerrar Outlook y reiniciar el equipo para que aparezca *el botón* Próximamente.

Puede comprobar la compatibilidad de inquilinos de prueba para su cuenta de inquilino:

* Para Teams pestañas personales que se ejecutan en office.com, outlook.com y Outlook para el escritorio de Windows, inicie sesión con las credenciales de inquilino de prueba y compruebe si hay puntos suspensivos (**...**) en el panel inferior izquierdo.

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Puntos suspensivos" lightbox="images/outlook-desktop-ellipses.png":::

* Para extensiones de mensajería en outlook.com y Outlook para Windows, busca  la opción Más aplicaciones en la cinta Outlook de mensajes de redacción.

> [!NOTE]
> Si has optado por las versiones del Canal Beta pero no ves estas opciones de puntos suspensivos, es probable que la compatibilidad con las características de vista previa esté en proceso de implementarse en el espacio empresarial. Para obtener las actualizaciones más recientes, [consulte Microsoft Teams Developer Blog](https://devblogs.microsoft.com/microsoft365dev/).

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Cambie a la versión de vista previa del desarrollador de Teams

Asegúrese de cambiar a Public [Developer Preview](../resources/dev-preview/developer-preview-intro.md) desde el Microsoft Teams cliente.

1. Inicie sesión en Teams con las credenciales de espacio aislado del espacio aislado.
1. En el menú de puntos suspensivos (**...**) junto al perfil de usuario, seleccione **Acerca de la vista** previa del  >  **programador**. Aparece un cuadro de diálogo, **seleccione Cambiar a vista previa del desarrollador.**
1. Después de Teams la aplicación, ve al menú de puntos suspensivos (**...**) junto al perfil de usuario y comprueba si **está** seleccionada la vista previa del desarrollador.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Versión preliminar pública para desarrolladores" lightbox="images/teams-dev-preview.png":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Instalar Visual Studio Code y Teams Toolkit vista previa

Opcionalmente, puedes usar [Visual Studio Code](https://code.visualstudio.com/) para ampliar Teams aplicaciones en Office y Outlook.

La extensión Teams Toolkit para [Visual Studio Code](https://aka.ms/teams-toolkit) ( o posterior) proporciona comandos que pueden ayudar a modificar el código de Teams existente para que sea compatible con Outlook y `v2.10.0` Office. Para obtener más información, vea [habilitar Teams pestaña personal para Office y Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-steps"></a>Pasos siguientes

- [Habilitar una pestaña personal de Teams para Office y Outlook](extend-m365-teams-personal-tab.md)
- [Habilitar una extensión de mensajería de Teams para Outlook](extend-m365-teams-message-extension.md)