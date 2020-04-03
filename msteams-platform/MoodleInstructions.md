---
title: Instalación de la integración de Moodle con Microsoft Teams
description: Cómo instalar y configurar la aplicación de integración de Moodle para Microsoft Teams
keywords: Complemento de integración de aplicaciones de Microsoft Teams moodle
ms.date: 01/31/2019
ms.openlocfilehash: 2b48cfb0bbef9a531e69ae5620c11a8258acdc64
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2020
ms.locfileid: "43120300"
---
# <a name="installing-the-moodle-integration-with-microsoft-teams"></a>Instalación de la integración de Moodle con Microsoft Teams

> [!VIDEO https://www.youtube.com/embed/OHlPt22nKoE]

[Moodle](https://moodle.org/), el sistema de administración de aprendizaje (LMS) más popular y de código abierto en el mundo, ahora está integrado con Microsoft Teams. Esta integración ayuda a los educadores y a los profesores a colaborar con cursos de Moodle, formular preguntas sobre sus calificaciones y tareas y mantenerse actualizados con las notificaciones, directamente en Microsoft Teams.

Para ayudar a los administradores de ti a configurar fácilmente esta integración, hemos actualizado nuestro complemento Office 365 moodle de código abierto con las siguientes capacidades:

* Registro automático del servidor Moodle con Azure AD.
* Implementación de un solo clic del bot de Moodle Assistant a Azure.
* Aprovisionamiento automático de Teams y sincronización automática de inpuestas en equipo para todos los cursos o seleccione moodle.
* Instalación automática de la pestaña Moodle y el bot? el Asistente de Moodle en cada equipo sincronizado. (Próximamente)
* Publicación de un solo clic de la aplicación de Moodle en la tienda de aplicaciones privada de Microsoft Teams. (Próximamente)

Para obtener más información sobre la funcionalidad que proporciona esta integración, vaya [aquí](https://education.microsoft.com/resource/3dffb3a8).

## <a name="prerequisites"></a>Requisitos previos

Para poder instalar y configurar esta aplicación, necesitará:

1. Credenciales de administrador de moodle
2. Credenciales de administrador de Azure AD
3. Una suscripción de Azure puede crear nuevos recursos en

## <a name="step-1-install-the-office-365-moodle-plugin"></a>Paso 1: instalar el complemento Office 365 moodle

> [!VIDEO https://www.youtube.com/embed/SETEC5nzMgk]

La integración de Moodle en Microsoft Teams funciona con el [conjunto de complementos Office 365 moodle](https://github.com/Microsoft/o365-moodle)de código abierto. Para instalar el complemento en el servidor de Moodle:

1. En primer lugar, descargue el [conjunto de complementos de Office 365](https://moodle.org/plugins/pluginversions.php?plugin=local_o365) y guárdelo en su equipo local. Debe usar la versión 3,5 o posterior.
    * Al instalar el complemento de local_o365, también se instalarán los complementos de [auth_oidc](https://moodle.org/plugins/auth_oidc) y [boost_o365Teams](https://moodle.org/plugins/pluginversions.php?plugin=theme_boost_o365teams) .
1. Inicie sesión en el servidor de Moodle como administrador y seleccione **Administración del sitio** en el panel de navegación de la izquierda.
1. Seleccione la pestaña **Complementos** y, a continuación, haga clic en **instalar complementos**.
1. En la sección **Instalar complemento del archivo zip** , haga clic en el botón **elegir un archivo** .
1. Seleccione las opciones **cargar un archivo** del panel de navegación de la izquierda, busque el archivo descargado anteriormente y haga clic en **cargar este archivo**.
1. Seleccione la opción **Administración del sitio** de nuevo en el panel de navegación izquierdo para volver al panel de administración. Desplácese hacia abajo hasta los **Complementos locales** y haga clic en el vínculo **Microsoft Office 365 Integration** . Mantenga esta página de configuración abierta en una pestaña del explorador independiente, ya que la usará en el resto de este proceso.

Puede encontrar más información sobre cómo instalar los complementos de Moodle en la [documentación de Moodle](https://docs.moodle.org/34/en/Installing_plugins).

**Nota importante:** Mantenga la página de configuración del complemento Office 365 moodle abierta en una pestaña del explorador independiente, ya que volverá a este conjunto de páginas a lo largo de este proceso.

*¿Todavía no tiene un sitio de moodle?* Es posible que quiera consultar nuestro [repositorio](https://github.com/azure/moodle) de Moodle en Azure, donde puede implementar rápidamente una instancia de Moodle en Azure y personalizarla según sus necesidades.

## <a name="step-2-configure-the-connection-between-the-office-365-plugin-and-azure-active-directory"></a>Paso 2: configurar la conexión entre el complemento de Office 365 y Azure Active Directory

> [!VIDEO https://www.youtube.com/embed/FpGEezaJ3SA]

A continuación, deberá registrar moodle como una aplicación en su Azure Active Directory. Hemos proporcionado un script de PowerShell para ayudarle a completar este proceso. El script de PowerShell aprovisiona una nueva aplicación de Azure AD para su inquilino de Office 365, que usará el complemento Office 365 moodle. El script aprovisionará la aplicación para el inquilino de O365, configure todas las direcciones URL de respuesta y los permisos necesarios para la aplicación aprovisionada y devuelva el AppID y la clave. Puede usar el AppID y la clave generados en la página Configuración del complemento de O365 Moodle para configurar el servidor de Moodle con Azure AD. Si desea ver los pasos manuales detallados que el script de PowerShell está automatizando, puede encontrarlos en la [documentación completa del complemento](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).

### <a name="moodle-tab-for-microsoft-teams-information-flow"></a>Pestaña Moodle para flujo de información de Microsoft Teams

<img width="530px" src="~/assets/images/MoodleTabInformationFlow.png" title="Pestaña Moodle para flujo de información de Microsoft Teams" />

1. En la página del complemento de integración de 365 de Microsoft Office, seleccione la pestaña **configurar** .
1. Haga clic en el botón **descargar script de PowerShell** y guárdelo en el equipo local.
1. Deberá preparar el script de PowerShell desde el archivo ZIP. Para ello:
    * Descargue y extraiga el `Moodle-AzureAD-Powershell.zip` archivo.
    * Abra la carpeta extraída.
    * Haga clic con el botón `Moodle-AzureAD-Script.ps1` derecho en el archivo y seleccione **propiedades**.
    * En la pestaña **General** de la ventana Propiedades, active la `Unblock` casilla situada junto al atributo **seguridad** en la parte inferior.
    * Haga clic en **Aceptar**.
    * Copie la ruta de acceso del directorio de la carpeta extraída.
1. A continuación, ejecutará PowerShell como administrador:
    * Haga clic en Iniciar.
    * Escriba PowerShell.
    * Haga clic con el botón secundario en Windows PowerShell.
    * Haga clic en "ejecutar como administrador".
1. Vaya al directorio descomprimido escribiendo `cd ...\...\Moodle-AzureAD-Powershell` donde `...\...` es la ruta de acceso al directorio.
1. Ejecute el script de PowerShell de la siguiente manera:
    * Entrar `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.
    * Entrar `.\Moodle-AzureAD-Script.ps1`.
    * Inicie sesión en su cuenta de administrador de O365 en la ventana emergente.
    * Escriba el nombre de la aplicación de Azure AD (ex. Complemento moodle/Moodle).
    * Escriba la dirección URL del servidor moodle.
    * Copie el **identificador** de la aplicación y la **clave de aplicación** generados por el script y guárdelos.
1. A continuación, tendrá que agregar el identificador y la clave al complemento Office 365 moodle. Vuelva a la página de administración del complemento (administración de sitios > complementos > integración de Microsoft Office 365).
1. En la ficha **configurar** , agregue el **identificador de aplicación** y la clave de **aplicación** que copió anteriormente y, a continuación, haga clic en **Guardar cambios**.
1. Una vez que se actualiza la página, ahora debería ver una sección nueva **elegir el método de conexión**. Haga clic en la casilla etiquetada **predeterminada** y, a continuación, haga clic en **Guardar cambios** nuevamente.
1. Una vez que se actualice la página, verá otra sección nueva de administración de la sección **& información adicional**.
    * Haga clic en el vínculo **proporcionar consentimiento del administrador** , escriba sus credenciales de administrador global de Office3 365 y, a continuación, **acepte** para conceder los permisos.
    * Junto al campo **inquilino de Azure ad** , haga clic en el botón **detectar** .
    * Junto a la **dirección URL de OneDrive para la empresa** , haga clic en el botón **detectar** .
    * Una vez rellenados los campos, haga clic de nuevo en el botón **Guardar cambios** .
1. Haga clic en el botón **Actualizar** para comprobar la instalación y, a continuación, **guarde los cambios**.
1. A continuación, tendrá que sincronizar los usuarios entre el servidor de Moodle y Azure Active Directory. En función de su entorno, puede seleccionar distintas opciones durante esta etapa. Tenga en cuenta que la configuración que establezca se ejecutará con cada moodle de cron (normalmente una vez al día) para mantener todo sincronizado. Para empezar:
    * Cambiar a la **pestaña Configuración de sincronización**
    * En la sección **sincronizar usuarios con Azure ad** , active las casillas correspondientes a su entorno. Normalmente, debe seleccionar al menos:
        * Crear cuentas en Moodle para los usuarios en Azure AD
        * Actualizar todas las cuentas de Moodle para los usuarios en Azure AD
    * En la sección **restricción de creación de usuarios** puede configurar un filtro para limitar los usuarios de Azure ad que se sincronizarán con moodle.
    * La sección de **asignación de campos de usuario** le permitirá personalizar Azure ad para Moodle la asignación de campos de Perfil de usuario.
    * En la sección de sincronización de Microsoft **Teams** , puede elegir crear automáticamente grupos (es decir, Teams) para algunos o todos los cursos de Moodle existentes.
1. Para validar los trabajos de cron (y ejecutarlos manualmente si desea para la primera ejecución), haga clic en el vínculo de la **página Administración de tareas programadas** en la sección **sincronizar usuarios con Azure ad** . Esto le llevará a la página **tareas programadas** .
    * Desplácese hacia abajo y busque el trabajo **sincronizar usuarios con el trabajo de Azure ad** y haga clic en **Ejecutar ahora**.
    * Si decide crear grupos basados en los cursos existentes, también puede ejecutar el trabajo **crear grupos de usuarios en Office 365** .
1. Vuelva a la página de administración del complemento (administración de sitios > complementos > integración de Microsoft Office 365) y seleccione la página de configuración de Microsoft **Teams** . Deberá configurar algunas opciones de seguridad para habilitar la integración de aplicaciones de Microsoft Teams.
    * Para habilitar OpenID Connect, haga clic en el vínculo **Manage Authentication** y haga clic en el icono de ojo en la línea de **OpenID Connect** si está atenuada.
    * A continuación, deberá habilitar la incrustación de Marcos. Haga clic en el vínculo **Seguridad http** y, a continuación, haga clic en la casilla al lado de **permitir incrustar fotogramas**.
    * El paso siguiente es habilitar los servicios web que habilitarán las características de la API de moodle. Haga clic en el vínculo **características avanzadas** y, a continuación, asegúrese de que la casilla de verificación situada junto a **habilitar servicios web** está seleccionada.
    * Por último, tendrá que habilitar los servicios externos para Office 365. Haga clic en el vínculo **servicios externos** :
        * Haga clic en **Editar** en la fila **moodle Office 365 webservices** .
        * Marque la casilla de verificación situada junto a **habilitado**y haga clic en **Guardar cambios** .
    * A continuación, tendrá que editar los permisos de usuario autenticado para permitirles crear tokens de servicio Web. Haga clic en el vínculo **Editar rol ' usuario autenticado '** . Desplácese hacia abajo y busque la opción **crear un token de servicio Web** y marque la casilla **permitir** .

## <a name="step-3-deploy-the-moodle-assistant-bot-to-azure"></a>Paso 3: implementar el bot? moodle Assistant en Azure

> [!VIDEO https://www.youtube.com/embed/gbkJxf8FlfY]

El bot? n gratuito de Moodle Assistant para Microsoft Teams ayuda a los profesores y alumnos a responder preguntas sobre sus cursos, tareas, calificaciones y otra información en moodle. El bot también envía notificaciones de Moodle a alumnos y profesores directamente en Microsoft Teams. Este bot es un proyecto de código abierto mantenido por Microsoft y está [disponible en github](https://github.com/microsoft/Moodle-Teams-Bot).

> [!NOTE]
> En esta sección, va a implementar recursos en su suscripción a Azure y todos los recursos se configurarán con el nivel **gratuito** . Según el uso del bot, es posible que necesite escalar estos recursos.
> Si solo desea usar la pestaña moodle sin el bot, vaya al [paso 4](#step-4-deploy-your-microsoft-teams-app).

### <a name="moodle-bot-information-flow"></a>Flujo de información de bot de moodle

<img width="530px" src="~/assets/images/MoodleBotInformationFlow.png" title="Moodle bot para el flujo de información de Microsoft Teams" />

Para instalar el bot, primero tendrá que registrarlo en la plataforma de [identidad de Microsoft](https://identity.microsoft.com/Landing). Esto permite a su bot autenticarse en los puntos de conexión de Microsoft. Para registrar el bot:

1. Vuelva a la página de administración del complemento (administración de sitios > complementos > integración de Microsoft Office 365) y seleccione la pestaña Configuración de Microsoft **Teams** .
1. Haga clic en el vínculo **portal de registro de aplicaciones de Microsoft** y inicie sesión con el identificador de Microsoft.
1. Escriba un nombre para la aplicación (por ejemplo, MoodleBot) y haga clic en el botón **crear** .
1. Copie el **identificador de aplicación** y péguelo en el campo ID de la **aplicación de bot** en la página **configuración del equipo** .
1. Haga clic en el botón **generar nueva contraseña** . Copie la contraseña generada y péguela en el campo **contraseña** de la aplicación de bot en la página **configuración del equipo** .
1. Desplácese hasta la parte inferior del formulario y haga clic en **Guardar cambios**.

Ahora que ha generado el identificador de aplicación y la contraseña, es el momento de implementar el bot en Azure. Haga clic en el botón **implementar en Azure** y rellene el formulario con la información necesaria (el identificador de la aplicación de bot, la contraseña de la aplicación bot y el secreto moodle se encuentran en la página **configuración del equipo** y la información de Azure se encuentra en la página **configuración** ). Una vez que haya rellenado el formulario, haga clic en la casilla para aceptar los términos y condiciones y, a continuación, haga clic en el botón **comprar** (todos los recursos de Azure se implementan en el nivel gratuito).

Una vez que los recursos hayan terminado de implementarse en Azure, tendrá que configurar el complemento Office 365 Moodle con su punto de conexión de mensajería. En primer lugar, necesitará obtener el punto de conexión de su bot en Azure. Para ello:

1. Si aún no lo ha hecho, inicie sesión en [Azure portal](https://portal.azure.com).
2. En el panel izquierdo, seleccione **grupos de recursos**.
3. En la lista, seleccione el grupo de recursos que acaba de usar (o que creó) al implementar el bot.
4. Seleccione el recurso **Bot de webapp** de la lista de recursos del grupo.
5. Copie el **extremo de mensajería** de la sección **información general** .
6. En Moodle, abra la página **configuración del equipo** del complemento Office 365 moodle.
7. En el campo **punto de conexión del bot** , pegue la dirección URL que acaba de copiar y cambie los *mensajes* de Word a *webhook*. La dirección URL ahora debería ser similar a`https://botname.azurewebsites.net/api/webhook`
8. Haga clic en **Guardar cambios**
9. Una vez que los cambios se hayan guardado, vuelva a la pestaña **configuración del equipo** , haga clic en el botón **Descargar archivo de manifiesto** y guarde el paquete del manifiesto en el equipo (lo utilizará en la sección siguiente).

## <a name="step-4-deploy-your-microsoft-teams-app"></a>Paso 4: implementar la aplicación de Microsoft Teams

> [!VIDEO https://www.youtube.com/embed/2rMb7gtM_ZM]

Ahora que ha implementado el bot en Azure y configurado para comunicarse con el servidor de Moodle, es el momento de implementar su aplicación de Microsoft Teams. Para ello, debe cargar el archivo de manifiesto que ha descargado de la página Configuración del equipo de complementos de Office 365 Moodle en el paso anterior.

Antes de poder instalar la aplicación, debe asegurarse de que las aplicaciones externas y la carga de aplicaciones están habilitadas. Para ello, puede seguir [estos pasos](https://docs.microsoft.com/microsoftteams/platform/get-started/get-started-tenant). Una vez que se haya asegurado de que las aplicaciones externas están habilitadas, puede seguir los pasos siguientes para implementar la aplicación.

1. Abra Microsoft Teams.
2. Haga clic en el icono de la **tienda** de la parte inferior izquierda de la barra de navegación.
3. Haga clic en el vínculo **cargar una aplicación personalizada** de la lista de opciones. *Nota:* Si ha iniciado sesión como una administración global, tendrá la opción de cargar la aplicación en la tienda de aplicaciones de su organización; de lo contrario, solo podrá cargar la aplicación para un equipo del que sea miembro.
4. Seleccione el `manifest.zip` paquete que ha descargado anteriormente y haga clic en **Guardar**. Si aún no ha descargado el paquete del manifiesto, puede hacerlo desde la pestaña **configuración del equipo** de la página Configuración del complemento en moodle.

Ahora que se ha instalado la aplicación, puede Agregar la ficha a cualquier canal al que tenga acceso. Para ello, navegue hasta el canal, haga clic **+** en el símbolo y seleccione la aplicación en la lista. Siga las instrucciones para terminar de agregar la ficha del curso moodle a un canal.

Y eso es todo. Usted y su equipo ahora pueden empezar a trabajar con los cursos de Moodle directamente desde Microsoft Teams.

Para compartir las solicitudes o comentarios de las características con nosotros, visite nuestra [Página de voz de usuario](https://microsoftteams.uservoice.com/forums/916759-moodle).
