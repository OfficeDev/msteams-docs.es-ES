---
title: Instalar Moodle LMS
description: En este artículo, aprenderá a instalar y configurar la aplicación de integración de Moodle para Microsoft Teams.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 83a4b4d40ebca418b62dcac5f94f77ac30ee85d7
ms.sourcegitcommit: 904cca011c3f27d1d90ddd80c3d0300a8918e412
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/20/2022
ms.locfileid: "66895506"
---
# <a name="install-moodle-lms"></a>Instalar Moodle LMS

En este artículo, aprenderá a instalar Moodle LMS.

> [!NOTE]
> Para ayudar a los administradores de TI a configurar fácilmente la integración de Moodle y Teams, los complementos de Código abierto de Microsoft 365 Moodle se actualizan para lo siguiente:
>
> * Registro automático del servidor de Moodle con [Microsoft Azure Active Directory (Azure AD).](https://azure.microsoft.com/services/active-directory/)
>
> * Implementación con un solo clic del bot de Moodle Assistant en Azure.
>
> * Aprovisionamiento automático de equipos y sincronización automática de inscripciones de equipos para todos los cursos de Moodle o selección de ellos.
>
> * Instalación automática de la pestaña Moodle y el bot del asistente de Moodle en cada equipo sincronizado.
>
> Para más información sobre la funcionalidad que proporciona esta integración, consulte [Microsoft Teams y Moodle](https://education.microsoft.com/resource/3dffb3a8).

## <a name="prerequisites"></a>Requisitos previos

Estos son los requisitos previos para instalar Moodle:

* Credenciales de administrador de Moodle.

* Credenciales de administrador de Azure AD.

* Una suscripción de Azure en la que puede crear nuevos recursos.

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Instalar los complementos de Microsoft 365 Moodle

La integración de Moodle en Microsoft Teams cuenta con la tecnología código abierto [conjunto de complementos de Microsoft 365 Moodle](https://moodle.org/plugins/browse.php?list=set&id=72).

### <a name="requisite-applications-and-plugins"></a>Aplicaciones y complementos necesarios

Asegúrese de instalar y descargar lo siguiente antes de continuar con la instalación de complementos de Microsoft 365 Moodle:

1. Asegúrese de instalar una [versión estable actual de Moodle](https://download.moodle.org/releases/latest/).

1. Descargue y guarde moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) y los complementos de [integración de Microsoft 365](https://moodle.org/plugins/local_o365) en el equipo local.

    > [!NOTE]
    > La instalación de los complementos OpenID Connect y Microsoft 365 Integration es necesaria para la integración de Teams.
    >
    > Además, se recomienda encarecidamente el complemento [Tema de Microsoft 365 Teams](https://moodle.org/plugins/theme_boost_o365teams) .

### <a name="microsoft-365-moodle-plugins"></a>Complementos de Microsoft 365 Moodle

1. Descargue los complementos, extráigalos y cárguelos en sus carpetas correspondientes. Por ejemplo, extraiga el complemento OpenID Connect (auth_oidc) en una carpeta denominada **oidc** y cárguelo en la carpeta **de autenticación** de la raíz del documento de Moodle. 

1. Inicie sesión en el servidor de Moodle como administrador y seleccione **Administración del sitio**.

1. Después de la detección de nuevos complementos que se van a instalar, Moodle debería redirigirle a la página instalar nuevos complementos. Si esto no ocurre, en la página **Administración del sitio** , seleccione **Notificaciones** en la pestaña **General** , esto debería desencadenar la instalación de los complementos.

1. Una vez instalados los complementos, vaya a la pestaña **Complementos** de la página **Administrador del sitio** , seleccione el vínculo de sección **Autenticación** y habilite **OpenID Connect**. Está bien dejar la configuración del complemento en blanco; se rellenarán más adelante.

1. En la página **Administrador del sitio** , desplácese hacia abajo hasta la sección **Complementos locales** y seleccione el vínculo **Integración de Microsoft 365** .

    > [!IMPORTANT]
    >
    > * Mantenga abierta la página de configuración de complementos de Microsoft 365 Moodle en una pestaña independiente del explorador, ya que debe volver a este conjunto de páginas a lo largo del proceso.  
    >
    > * Si no tiene un sitio de Moodle existente, vaya al repositorio [de Moodle en Azure](https://github.com/azure/moodle) e implemente rápidamente una instancia de Moodle y personalícela según sus necesidades.

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-ad"></a>2. Configuración de la conexión entre los complementos de Microsoft 365 y Azure AD

Debe configurar la conexión entre los complementos de Microsoft 365 y Azure AD.

### <a name="requisites"></a>Requisitos

Registre Moodle como una aplicación en Azure AD mediante el script de PowerShell. El script aprovisiona lo siguiente:

* Una nueva aplicación de Azure AD para el inquilino de Microsoft 365, que usan los complementos de Moodle de Microsoft 365.
* La aplicación para el inquilino de Microsoft 365, configura las direcciones URL de respuesta y los permisos necesarios para la aplicación aprovisionada y devuelve y `AppID` `Key`.

Use el archivo generado `AppID` y `Key` en la página de configuración de complementos de Moodle de Microsoft 365 para configurar el sitio de servidor de Moodle con Azure AD.

> [!IMPORTANT]
>
> * Para obtener más información sobre cómo registrar manualmente la instancia de Moodle, consulte Registro de la [instancia de Moodle como aplicación](https://docs.moodle.org/400/en/Microsoft_365#Azure_App_Creation_and_Configuration).

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>Pestaña Moodle del flujo de información de Microsoft Teams

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. En la página Complementos de integración de Microsoft 365, seleccione la pestaña **Configuración** .

1. Seleccione el botón **Descargar script de PowerShell** y guárdelo como una carpeta ZIP en el equipo local.

1. Prepare el script de PowerShell desde el archivo ZIP de la siguiente manera:

    1. Descargue y extraiga el `Moodle-AzureAD-Powershell.zip` archivo.
    1. Abra la carpeta extraída.
    1. Haga clic con el botón derecho en el `Moodle-AzureAD-Script.ps1` archivo y seleccione **Propiedades**.
    1. En la pestaña **General** del ventana Propiedades, active la `Unblock` casilla situada junto al atributo **Seguridad** situado en la parte inferior de la ventana.
    1. Seleccione **Aceptar**.
    1. Copie la ruta de acceso del directorio a la carpeta extraída.

1. Ejecute PowerShell como administrador:

    1. Seleccione Inicio.
    1. Escriba PowerShell.
    1. Haga clic con el botón derecho en **Windows PowerShell**.
    1. Seleccione **Ejecutar como administrador**.

1. Vaya al directorio descomprimido; para ello, escriba `cd .../.../Moodle-AzureAD-Powershell` dónde `.../...` es la ruta de acceso al directorio.

1. Ejecute el script de PowerShell:

    1. Escriba `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.
    1. Escriba `./Moodle-AzureAD-Script.ps1`.
    1. Inicie sesión en su cuenta de administrador de Microsoft 365 en la ventana emergente.
    1. Escriba el nombre de la aplicación de Azure AD, por ejemplo, complementos de Moodle o Moodle.
    1. Escriba la dirección URL del servidor de Moodle.
    1. Copie el **identificador de aplicación (`AppID`)** y **la clave de aplicación (`Key`)** generados por el script y guárdelos.

1. A continuación, debe agregar y `AppID` `Key` a los complementos de Microsoft 365 Moodle. Vuelva a la página de administración de complementos, Administración del sitio > Complementos > Integración de Microsoft 365.

1. En la pestaña **Configuración** , agregue `AppID` y `Key` copió anteriormente y, a continuación, seleccione **Guardar cambios**. Después de actualizar la página, puede ver una nueva sección **Elegir método de conexión**.

1. En **Choose connection method (Elegir método de conexión**), active la casilla con la etiqueta **Default (Predeterminado**) y, a continuación, seleccione **Save changes again (Guardar cambios** de nuevo).

1. Una vez actualizada la página, puede ver otra nueva sección **Administración consentimiento & información adicional**.
    1. Seleccione **Proporcionar Administración vínculo consentimiento**, escriba sus credenciales de administrador global de Microsoft 365 y, a continuación, **Acepte** para conceder los permisos.
    1. Junto al campo **Inquilino de Azure AD** , seleccione el botón **Detectar** .
    1. Junto a la **dirección URL de OneDrive para la Empresa**, seleccione el botón **Detectar**.
    1. Después de rellenar los campos, vuelva a seleccionar el botón **Guardar cambios** .

1. Seleccione el botón **Actualizar** para comprobar la instalación y, a continuación, seleccione **Guardar cambios**.

1. Sincronice los usuarios entre el servidor de Moodle y Azure AD. Para empezar:

    > [!NOTE]
    > En función del entorno, puede seleccionar diferentes opciones durante esta fase.

    1. Cambie a la **pestaña Configuración de sincronización**.

    1. En la sección **Sincronizar usuarios con Azure AD** , active las casillas que se aplican a su entorno. Debe seleccionar lo siguiente:  

        ✔ Cree cuentas en Moodle para los usuarios de Azure AD.

        ✔ Actualice todas las cuentas de Moodle para los usuarios de Azure AD.

    1. En la sección **Restricción de creación** de usuarios, puede configurar un filtro para limitar los usuarios de Azure AD que se sincronizan con Moodle.

1. Para validar los trabajos [cron](https://docs.moodle.org/400/en/Cron) y ejecutarlos manualmente para la primera ejecución, seleccione el vínculo **De administración de tareas programadas** en la sección **Sincronizar usuarios con Azure AD** . Esto le lleva a la página **Tareas programadas** .

    1. Desplácese hacia abajo y busque el trabajo **Sincronizar usuarios con Azure AD** y seleccione **Ejecutar ahora**.
    1. Si selecciona crear grupos basados en cursos existentes, también puede ejecutar el trabajo **Crear grupos de usuarios en Microsoft 365** .

    > [!NOTE]
    >
    > Moodle [Cron](https://docs.moodle.org/310/en/Cron) se ejecuta según la programación de tareas. La programación predeterminada es una vez al día. Sin embargo, el cron debe ejecutarse con más frecuencia para mantener todo sincronizado.

1. Vuelva a la página de administración de complementos, **Administración del sitio > Complementos > Integración de Microsoft 365** y seleccione la página **Configuración de Teams** .

1. En la página **Configuración de Teams** , configure las opciones necesarias para habilitar la integración de aplicaciones de Teams haciendo clic en el vínculo **Comprobar configuración de Moodle** para actualizar todas las configuraciones necesarias para que funcione la integración de Teams. 

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Implementación del bot de Moodle Assistant en Azure

El bot asistente de Moodle gratuito para Microsoft Teams ayuda a los profesores y alumnos a responder preguntas sobre sus cursos, asignaciones, calificaciones y otra información en Moodle. El bot también envía notificaciones de Moodle a los alumnos y profesores de Teams. El bot es un proyecto de código abierto mantenido por Microsoft y está disponible en [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).

> [!NOTE]
>
> * Implemente recursos en la suscripción de Azure. Todos los recursos se configuraron mediante el nivel **gratis** . En función del uso del bot, es posible que tenga que escalar estos recursos.
>
> * Para usar la pestaña Moodle sin el bot, vaya a [4](#4-deploy-your-microsoft-teams-app).

### <a name="moodle-bot-information-flow"></a>Flujo de información del bot de Moodle

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

Para instalar el bot, debe registrarlo en la [Plataforma de identidad de Microsoft](https://identity.microsoft.com/Landing). Esto permite que el bot se autentique en los puntos de conexión de Microsoft.

Para registrar el bot:

1. Vaya a la página de administración de complementos y seleccione **Complementos**. En **Integración de Microsoft 365**, seleccione la pestaña **Configuración de Teams** .

1. Seleccione el vínculo **Portal de registro de aplicaciones de Microsoft** e inicie sesión con su identificador de Microsoft.

1. Escriba un nombre para la aplicación, como MoodleBot y seleccione el botón **Crear** .

1. Copie el **identificador de aplicación** y péguelo en el campo **Bot Application ID (Id. de aplicación del bot** ) de la página **Configuración del equipo** .

1. Seleccione el botón **Generar nueva contraseña** . Copie la contraseña generada y péguela en el campo **Bot Application Password (Contraseña de aplicación del bot** ) de la página **Configuración del equipo** .

1. Desplácese hasta la parte inferior del formulario y seleccione **Guardar cambios**.

Después de generar el identificador y la contraseña de la aplicación, implemente el bot en Azure:

> [!div class="checklist"]
>
> * Seleccione **Implementar en Azure** y complete el formulario con la información necesaria, como el identificador de aplicación del bot, la contraseña de la aplicación del bot y el secreto de Moodle en la página **Configuración de Teams** . La información de Azure se encuentra en la página **Configuración** .
> * Después de completar el formulario, active la casilla para aceptar los términos y condiciones.
> * Seleccione **Comprar**. Todos los recursos de Azure se implementan en el nivel gratuito.

Una vez que los recursos hayan completado la implementación en Azure, debe configurar los complementos de Microsoft 365 Moodle con un punto de conexión de mensajería. Debe obtener el punto de conexión del bot en Azure:

1. Inicie sesión en [Microsoft Azure Portal](https://portal.azure.com).

1. En el panel izquierdo, seleccione **Grupos de recursos** y seleccione el grupo de recursos que usó o creó, al implementar el bot.

1. Seleccione el recurso **WebApp Bot** en la lista de recursos del grupo.

1. Copie el **punto de conexión de mensajería** de la sección **Información general** .

1. En Moodle, abra la página **Configuración del equipo** de los complementos de Moodle de Microsoft 365.

1. En el campo **Punto de conexión del bot** , pegue la dirección URL que copió y cambie los *mensajes* de palabra a *webhook*. La dirección URL debe aparecer de la siguiente manera: `https://botname.azurewebsites.net/api/webhook`

1. Seleccione **Guardar cambios**.

1. Después de guardar los cambios, vuelva a la pestaña **Configuración del equipo** , seleccione el botón **Descargar archivo de manifiesto** y guarde el paquete de manifiesto de la aplicación en el equipo para su uso posterior.

## <a name="4-deploy-your-microsoft-teams-app"></a>4. Implementación de la aplicación de Microsoft Teams

Una vez implementado el bot en Azure y configurado para comunicarse con el servidor de Moodle, debe implementar la aplicación de Microsoft Teams. Para ello, debe cargar el archivo de manifiesto de aplicación que descargó de la página Configuración del equipo de complementos de Moodle de Microsoft 365 en el paso anterior.

Antes de instalar la aplicación, debe asegurarse de habilitar aplicaciones externas y cargar aplicaciones. Para obtener más información, consulte [Preparación del inquilino de Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md).

Para implementar la aplicación:

1. Abra **Microsoft Teams**.

1. Seleccione el icono **Aplicaciones** en el área inferior izquierda de la barra de navegación.

1. Seleccione el vínculo **Administrar las aplicaciones** en el menú de navegación.

1. Haga clic en **Publicar una aplicación** y seleccione **Cargar una aplicación en el catálogo de aplicaciones de su organización**.

   > [!NOTE]
   > Si ha iniciado sesión como administrador global, debe tener la opción de cargar la aplicación en el catálogo de aplicaciones de su organización; de lo contrario, solo puede cargar la aplicación para un equipo en el que sea miembro.

4. Seleccione el `manifest.zip` paquete que descargó anteriormente y seleccione **Guardar**. Si no ha descargado el paquete de manifiesto de la aplicación, puede descargarlo desde la pestaña **Configuración del equipo** de la página de configuración de complementos de Moodle.

Ahora que tiene instalada la aplicación, puede agregar la pestaña a cualquier canal al que tenga acceso. Para ello, vaya al canal, seleccione el símbolo **más** (➕) y seleccione la aplicación en la lista. Siga las indicaciones para terminar de agregar la pestaña de curso de Moodle a un canal.

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. Permitir la creación automática de pestañas de Moodle en Microsoft Teams

Aunque las pestañas de Moodle se crean manualmente en Microsoft Teams, puede decidir crearlas automáticamente cuando se creen equipos a partir de la sincronización del curso. Para ello, debe configurar el identificador de la aplicación de Microsoft Teams cargada en Moodle.

Para permitir la creación automática de pestañas de Moodle:

1. En Moodle, abra la pestaña **de la aplicación Teams Moodle** desde la página de configuración de complementos de Moodle de Microsoft 365.

1. Si la aplicación de Azure tiene el permiso recomendado, para la configuración de id. de **aplicación de Moodle** , debe mostrar un **valor detectado automáticamente** y copiar este valor en la configuración.

1. Si el valor detectado automáticamente no está presente, siga las instrucciones de la página para buscar el identificador de aplicación de Moodle y rellenar la configuración.

Cuando se sincroniza un curso de Moodle, Teams instala automáticamente la aplicación Moodle en el equipo, crea una pestaña Moodle en el canal General de Teams y la configura para que contenga la página del curso de Moodle desde la que se sincroniza. Ahora puede empezar a trabajar con los cursos de Moodle directamente desde Teams.

> [!NOTE]
> Para compartir con nosotros cualquier solicitud o comentario de características, visite nuestra [página Voz del usuario](https://support.microsoft.com/en-us/office/uservoice-pages-430e1a78-e016-472a-a10f-dc2a3df3450a).

## <a name="see-also"></a>Consulte también

* [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
* [Moodle](https://moodle.org/)
* [Documentación de Moodle](https://docs.moodle.org/400/en/Installing_plugins)
* [Página de integración de Microsoft 365 y Moodle en Moodle Docs](https://docs.moodle.org/400/en/Microsoft_365)
