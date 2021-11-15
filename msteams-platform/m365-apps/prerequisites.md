---
title: Configurar el entorno de desarrollo para ampliar Teams aplicaciones en Microsoft 365
description: Estos son los requisitos previos para extender las aplicaciones Teams en Microsoft 365
ms.date: 11/15/2021
ms.topic: how-to
ms.openlocfilehash: d9e6ecb9e0cdbdb4754de12dff4399c02bf88863
ms.sourcegitcommit: f77750f2e60f63d1e2f66a96c169119683c66950
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2021
ms.locfileid: "60960374"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-m365-preview"></a>Configurar el entorno de desarrollo para ampliar Teams aplicaciones en M365 (versión preliminar)

El entorno de desarrollo para extender Teams aplicaciones en Microsoft 365 es similar al que se usa para Microsoft Teams desarrollo. Este artículo describe las configuraciones específicas necesarias para ejecutar compilaciones de vista previa de aplicaciones Microsoft Teams y Microsoft Office con el fin de obtener una vista previa de las aplicaciones Teams que se ejecutan en Outlook y Office. Para configurar el entorno de desarrollo, deberá:

> [!div class="checklist"]
> * [Obtener un inquilino para desarrolladores de M365 (espacio aislado) y habilitar la instalación local](#prepare-a-developer-tenant-for-testing)
> * [Inscribir el inquilino M365 *en Office 365 versiones dirigidas*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Configurar la cuenta para obtener acceso a las versiones preliminares de Outlook y Office](#install-beta-office-apps-in-your-test-environment)
> * [Cambie a la versión de vista previa del desarrollador de Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Opcional*] [Instalar Teams Toolkit extensión para Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Preparar un inquilino para desarrolladores para pruebas

Si aún no tiene uno, cree un espacio aislado de suscripción [Microsoft 365](/office/developer-program/microsoft-365-developer-program-get-started) desarrollador u obtenga un inquilino de prueba a través de su organización.

Después de tener un inquilino, [](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading) deberá habilitar la instalación local para el inquilino iniciando sesión en [Centro de administración de Microsoft 365](https://admin.microsoft.com) y navegando a Mostrar todas las aplicaciones de > Teams > Teams > directivas de instalación > **Global**.  Activa la **opción Upload aplicaciones personalizadas** y **Guardar**.

Si tiene un inquilino existente, compruebe que la instalación local está habilitada iniciando sesión en Teams y seleccionando **Aplicaciones**. Verá la opción Upload **aplicación** personalizada si la instalación local está habilitada para el inquilino.

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="La instalación local está habilitada para el inquilino si ves la opción de &quot;Upload una aplicación personalizada&quot; desde el panel Teams &quot;Aplicaciones&quot;":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Inscribir el inquilino del desarrollador para Office 365 versiones dirigidas

> [!IMPORTANT]
> Consulta lo último de [Microsoft Teams:](https://devblogs.microsoft.com/microsoft365dev/category/teams/) blog para desarrolladores de Microsoft 365 para comprobar si outlook.com y office.com compatibilidad con Teams aplicaciones están disponibles para el inquilino de prueba.

Para obtener una vista previa Teams aplicaciones que se ejecutan en outlook.com o office.com, opte por el espacio empresarial de prueba para Office 365 [versiones dirigidas](/microsoft-365/admin/manage/release-options-in-office-365#targeted-release).

1. Inicie sesión en Centro de administración de Microsoft 365 con las credenciales del inquilino [](https://admin.microsoft.com/AdminPortal/Home?#/Settings/OrganizationProfile) de prueba y vaya a la pestaña Perfil de la organización. **Seleccione** Preferencias de versión y seleccione una de las preferencias de versión *dirigida:*

:::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Centro de administración de Microsoft 365 menú &quot;Preferencias de publicación&quot; con la opción de versión dirigida seleccionada":::

Para obtener más información sobre Office 365 de lanzamiento, vea Configurar las opciones [de](/microsoft-365/admin/manage/release-options-in-office-365) versión estándar o dirigida *en Centro de administración de Microsoft 365 ayuda*.

1. Compruebe que el inquilino es compatible con Teams pestañas personales que se ejecutan en office.com y outlook.com iniciando sesión con las credenciales de inquilino de prueba. Si ve una opción de puntos suspensivos (**...**) en la barra lateral (el punto de entrada para las pestañas Teams personales), el inquilino tiene soporte técnico.

:::image type="content" source="images/outlook-web-ellipses.png" alt-text="Elipses '...' punto de entrada a aplicaciones de Teams de pestañas de outlook.com":::

1. Compruebe la compatibilidad de inquilinos de prueba para  extensiones de mensajería en outlook.com la opción Más aplicaciones en el área de Outlook de mensajes de redacción.
``

> [!NOTE]
> Si ha optado por las versiones dirigidas pero no ve estas opciones, es probable que la compatibilidad con características de vista previa aún esté en proceso de implementarse en el espacio empresarial. Para obtener las actualizaciones más recientes, [consulte Microsoft Teams Developer Blog](https://devblogs.microsoft.com/microsoft365dev/category/teams/).

## <a name="install-beta-office-apps-in-your-test-environment"></a>Instalar aplicaciones beta Office en el entorno de prueba

> [!IMPORTANT]
> Consulte el último [Microsoft Teams:](https://devblogs.microsoft.com/microsoft365dev/category/teams/) blog para desarrolladores de Microsoft 365 para comprobar si Outlook la compatibilidad de escritorio Windows para extensiones de mensaje de Teams está disponible para el inquilino de prueba.

Puedes obtener una vista previa Teams aplicaciones que se ejecutan en Outlook en Windows escritorio mediante una compilación reciente del *Canal* Beta. Para instalar una Outlook de canal beta en el entorno [](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) de prueba, probablemente deba cambiar el canal de actualización de Aplicaciones Microsoft 365 para el inquilino de prueba.

Estos son los pasos para instalar Office 365 *de canal beta* en el entorno de prueba:

1. En el entorno de prueba, inicie sesión en Centro de administración de Microsoft 365 ( con las credenciales que creó para el inquilino de prueba (por ejemplo, dominio de nombre de usuario https://admin.microsoft.com)  @ .onmicrosoft.com).
1. En el Centro de administración, **selecciona Instalar Office** (o Ir a configuración *guiada)* para instalar aplicaciones de escritorio en el entorno de prueba. Opcionalmente, agregue un usuario de prueba (útil para las pruebas).
1. Descargue la [Office de implementación y](https://www.microsoft.com/download/details.aspx?id=49117) extraiga en una carpeta local.
1. Abra *configuration-Office365-x86.xml* (o **x64.xml*, según su entorno) en un editor de texto y actualice el *valor channel* a `BetaChannel` .
1. Desde un símbolo del sistema con privilegios elevados, ejecute `setup.exe /configure configuration-Office365-x86.xml` (o use el archivo **x64.xml,* según el programa de instalación).
1. Abra Outlook (cliente de escritorio) y configure la cuenta de correo con las credenciales de inquilino de prueba.
1. En Outlook, abra Archivo Office Cuenta acerca de Outlook y confirme que ahora está en el canal beta y que el número de compilación es  >    >   **14416** o posterior. 
1. Activa el botón **Próximamente** en la esquina de la Outlook cliente:

   :::image type="content" source="images/outlook-coming-soon.png" alt-text="Botón &quot;Próximamente&quot; en Outlook de escritorio alternado a &quot;On&quot;}":::

Puede comprobar que el inquilino admite pestañas personales que se ejecutan en Outlook para un escritorio Windows iniciando sesión con las credenciales de inquilino de prueba y buscando una opción de puntos suspensivos (**...**) en la barra lateral (el punto de entrada de las pestañas Teams personales de prueba). Teams

:::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Elipses '...' punto de entrada a aplicaciones de Teams de pestañas de Outlook para escritorio":::

Del mismo modo, puede comprobar la compatibilidad del espacio empresarial de prueba para  extensiones de mensajería en Outlook para un escritorio Windows si busca la opción Más aplicaciones en la cinta de opciones de Outlook de mensajes de redacción.

Si ha optado por las versiones dirigidas pero no ve estas opciones de puntos suspensivos, es probable que la compatibilidad con características de vista previa aún esté en proceso de implementarse en el espacio empresarial. Para obtener las actualizaciones más recientes, [consulte Microsoft Teams Developer Blog](https://devblogs.microsoft.com/microsoft365dev/category/teams/).

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Cambie a la versión de vista previa del desarrollador de Teams

Asegúrese de participar en public [*developer preview*](../resources/dev-preview/developer-preview-intro.md) desde el Microsoft Teams cliente.

1. Inicie sesión en Teams con su cuenta de espacio aislado.
1. En el menú de puntos suspensivos (**...**) junto al perfil de usuario, **seleccione** Acerca de y seleccione la opción Vista previa **del** programador.
1. Después de que aparezca el cuadro de diálogo, selecciona **Cambiar a la** vista previa del desarrollador para reiniciar Teams y comprueba que la vista previa del desarrollador está habilitada.

:::image type="content" source="images/teams-dev-preview.png" alt-text="En Teams de puntos suspensivos, abra &quot;Acerca&quot; y compruebe que la opción &quot;Vista previa del programador&quot; esté activada.":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Instalar Visual Studio Code y Teams Toolkit vista previa

Opcionalmente, puedes aprovechar las ventajas de Visual Studio Code [para](https://code.visualstudio.com/) ayudar a extender Teams aplicaciones en Office y Outlook.

La extensión Teams Toolkit para [Visual Studio Code](https://aka.ms/teams-toolkit) ( o posterior) proporciona comandos que pueden ayudar a modificar el código de Teams existente para que sea compatible con Outlook y `v2.10.0` Office. Continúe [habilitando Teams pestaña personal para Office y Outlook](extend-m365-teams-personal-tab.md) para obtener más información.

## <a name="next-steps"></a>Pasos siguientes

- [Habilitar una Teams personal para Office y Outlook](extend-m365-teams-personal-tab.md)
- [Habilitar una Teams de mensajería para Outlook](extend-m365-teams-message-extension.md)