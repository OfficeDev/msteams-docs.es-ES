---
title: Instalación de la integración de Moodle con Microsoft Teams
description: Cómo instalar y configurar la aplicación de integración Moodle para Microsoft Teams
keywords: Complemento de integración de la aplicación Teams Moodle
ms.topic: how-to
ms.author: lajanuar
author: laujan
ms.openlocfilehash: bb3de6b3897105ff3564ecd332cba28a0db85b0f
ms.sourcegitcommit: a16590b2ccc46e1b6d17cbb367762a3c16ff779c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/05/2021
ms.locfileid: "50115744"
---
# <a name="installing-the-moodle-integration-with-microsoft-teams"></a>Instalación de la integración de Moodle con Microsoft Teams

[Ahora, Moodle,](https://moodle.org/)un popular sistema de administración de aprendizaje de código abierto (LMS), se integra con Microsoft Teams. Esta integración ayuda a los formadores y profesores a colaborar en torno a los cursos de Moodle, hacer preguntas sobre calificaciones y tareas, y mantenerse actualizados con las notificaciones directamente en Teams.

Para ayudar a los administradores de TI a configurar fácilmente esta integración, hemos actualizado nuestro complemento de Microsoft 365 Moodle de código abierto con las siguientes funcionalidades:

* Registro automático del servidor Moodle con [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (Azure AD).
* Implementación con un solo clic del bot asistente de Moodle en Azure.
* Aprovisionamiento automático de equipos y sincronización automática de las inscripciones de equipo para todos los cursos de Moodle o seleccionarlo.
* Instalación automática de la pestaña Moodle y el bot asistente de Moodle en cada equipo sincronizado.

Para obtener más información sobre la  funcionalidad que proporciona esta integración, consulte [Microsoft Teams y Moodle.](https://education.microsoft.com/resource/3dffb3a8)

## <a name="prerequisites"></a>Requisitos previos

Para instalar y configurar esta aplicación necesitará:

1. Credenciales de administrador de Moodle.

1. Credenciales de administrador de Azure AD.

1. Una suscripción de Azure en la que puede crear nuevos recursos.

## <a name="step-1-install-the-microsoft-365-moodle-plugins"></a>Paso 1: Instalar los complementos de Microsoft 365 Moodle

La integración de Moodle en Microsoft Teams funciona con el conjunto de complementos de Código abierto [de Microsoft 365 Moodle.](https://github.com/Microsoft/o365-moodle) Para instalar el complemento en el servidor Moodle, debe tener instalado lo siguiente:

1. Una [versión estable actual de Moodle](https://download.moodle.org/releases/latest/).

1. Los complementos de Integración de [Microsoft 365](https://moodle.org/plugins/local_o365) [y OpenID Connect](https://moodle.org/plugins/auth_oidc) de Moodle se descargaron y guardaron en el equipo local.

> [!NOTE]
> Para la integración de Teams es necesario instalar los complementos De OpenID Connect e Integración de Microsoft 365. Además, se recomienda encarecidamente el complemento Tema de [Microsoft 365 Teams.](https://moodle.org/plugins/theme_boost_o365teams)

3. Inicie sesión en el servidor Moodle como administrador y seleccione **Administración del** sitio en el bloque Configuración [ubicado](https://docs.moodle.org/22/en/Settings_block) en el panel de navegación izquierdo.

1. Seleccione la **pestaña Complementos** y, a continuación, elija **Instalar complementos.**

1. En la **sección Instalar complemento desde archivo ZIP,** seleccione el botón Elegir **un** archivo.

1. Seleccione las **opciones cargar un archivo** en el panel de navegación izquierdo, busque el archivo que descargó anteriormente y elija Cargar este **archivo.**

1. Seleccione la **opción Administración del** sitio en el panel de navegación izquierdo para volver al panel de administración. Desplácese hacia abajo hasta **los complementos locales** y seleccione el vínculo **Integración de Microsoft 365.** **Mantenga esta página de configuración abierta en una pestaña del explorador independiente durante todo el proceso de instalación.**

You can find more information on how to install Moodle plugins in the [Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).

> [!IMPORTANT]
>
> * Mantenga abierta la página de configuración del complemento Microsoft 365 Moodle en una pestaña del explorador independiente. Volverá a este conjunto de páginas durante todo el proceso.  <br/><br/>
>* Si no tiene un sitio de Moodle existente, puede consultar Moodle en el repositorio de [Azure,](https://github.com/azure/moodle) donde puede implementar rápidamente una instancia de Moodle y personalizarla según sus necesidades.

## <a name="step-2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a>Paso 2: Configurar la conexión entre el complemento de Microsoft 365 y Azure Active Directory (Azure AD)

A continuación, tendrás que registrar Moodle como una aplicación en Azure AD. Hemos proporcionado un script de PowerShell para ayudarle a completar este proceso. El script de PowerShell aprovisiona una nueva aplicación de Azure AD para el espacio empresarial de Microsoft 365, que usará el complemento Microsoft 365 Moodle. El script aprovisionará la aplicación para su inquilino de Microsoft 365, configurará las direcciones URL de respuesta y los permisos necesarios para la aplicación aprovisionada y devolverá `AppID` el archivo y `Key` . Puede usar el complemento Generado y en la página de configuración del complemento `AppID` Microsoft 365 Moodle para configurar el sitio del servidor Dele con `Key` Azure AD.

>[!IMPORTANT]
> El script de PowerShell no se actualiza con los elementos de configuración más recientes, por lo que tendrá que completar la configuración manualmente siguiendo los pasos descritos en las páginas de lanzamiento de Moodle [3.8.0.4 y 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) y [3.8.0.5 y 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) </br></br>
> Para ver los pasos manuales que el script de PowerShell automatiza en *detalle,* vea Registrar la instancia [de Moodle como una aplicación.](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>La pestaña Moodle para el flujo de información de Microsoft Teams

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. En la página del complemento de integración de Microsoft 365, seleccione la **pestaña** Configuración.

1. Seleccione el **botón Descargar script de PowerShell** y guárdelo en el equipo local.

1. Deberá preparar el script de PowerShell desde el archivo ZIP. Para ello:

    * Descargue y extraiga el `Moodle-AzureAD-Powershell.zip` archivo.
    * Abra la carpeta extraída.
    * Haga clic con el botón secundario en `Moodle-AzureAD-Script.ps1` el archivo y seleccione **Propiedades.**
    * En la **pestaña General** de la ventana Propiedades, active la casilla situada junto al atributo `Unblock` **Seguridad** situado en la parte inferior de la ventana.
    * Seleccione **Aceptar**.
    * Copie la ruta de acceso del directorio a la carpeta extraída.

1. A continuación, ejecutará PowerShell como administrador:

    * Seleccione Inicio.
    * Escriba PowerShell.
    * Haga clic con el botón Windows PowerShell.
    * Seleccione "Ejecutar como administrador".

1. Navegue al directorio descomprimido escribiendo `cd .../.../Moodle-AzureAD-Powershell` dónde está la ruta de acceso al `.../...` directorio.

1. Ejecute el script de PowerShell:

    * Escriba `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .
    * Escriba `./Moodle-AzureAD-Script.ps1` .
    * Inicie sesión en su cuenta de administrador de Microsoft 365 en la ventana emergente.
    * Escribe el nombre de la aplicación de Azure AD (por ejemplo, el complemento Moodle/Moodle).
    * Escriba la dirección URL del servidor Moodle.
    * Copie el **identificador de aplicación** y la clave de **aplicación** generados por el script y guárdelos.

1. A continuación, tendrá que agregar el ` AppID` complemento Microsoft `Key` 365 Moodle y al complemento de Microsoft 365. Vuelva a la página de administración del complemento (administración del sitio ➡ complementos ➡ integración de Microsoft 365).

1. En la **pestaña Instalación,** agregue el identificador **de** aplicación y la clave **de** aplicación que copió anteriormente y, a continuación, seleccione **Guardar cambios.**

1. Una vez que la página se actualiza, debería ver una nueva sección **Elegir método de conexión.** Seleccione la casilla de **verificación** Predeterminada y, a continuación, vuelva a **seleccionar Guardar** cambios.

1. Una vez que se actualice la página, verá otra nueva sección: consentimiento del **administrador & información adicional.**
    * Seleccione el **vínculo Proporcionar consentimiento de** administrador, escriba sus credenciales de administrador global de Microsoft 365 y, a continuación, acepte conceder los permisos. 
    * Junto al campo **Inquilino de Azure AD,** seleccione el **botón** Detectar.
    * Junto a la **dirección URL de OneDrive** para la Empresa, seleccione el **botón** Detectar.
    * Una vez rellenados los campos, vuelva a seleccionar **el** botón Guardar cambios.

1. Seleccione el **botón** Actualizar para comprobar la instalación y, a continuación, **guarde los cambios.**

1. A continuación, tendrá que sincronizar los usuarios entre el servidor de Moodle y Azure AD. Según el entorno, puede seleccionar diferentes opciones durante esta fase. Para empezar:
    * Cambiar a la pestaña **Configuración de sincronización**
    * En la **sección Sincronizar usuarios con Azure AD,** selecciona las casillas que se aplican a tu entorno. Normalmente, como mínimo, seleccionaría lo siguiente:  

        ✔ crear cuentas en Moodle para los usuarios de Azure AD . 
        ✔ todas las cuentas de Moodle para los usuarios de Azure AD.  

    * En la **sección Restricción de creación de** usuarios, puedes configurar un filtro para limitar los usuarios de Azure AD que se sincronizarán con Moodle.
    * La **sección Asignación de campos** de usuario le permitirá personalizar la asignación de campos de perfil de usuario de Azure AD a Moodle.
    * En la **sección Sincronización de Teams,** puede elegir crear grupos automáticamente (es decir, equipos) para algunos o todos los cursos existentes de Moodle.

> [!NOTE]
> The Moodle [Cron](https://docs.moodle.org/310/en/Cron) will run according to the task schedule (once a day by default). Sin embargo, el cron debe ejecutarse con más frecuencia para mantener todo sincronizado.

13. Para validar [los trabajos cron](https://docs.moodle.org/310/en/Cron) (o ejecutarlos manualmente para  la primera ejecución), seleccione el vínculo página Administración de tareas programadas en la sección Sincronizar usuarios con **Azure AD.** Esto le llevará a la **página Tareas programadas.**

    * Desplácese hacia abajo y busque el trabajo **Sincronizar usuarios con Azure AD** y seleccione Ejecutar **ahora.**
    * Si decidió crear grupos basados en cursos existentes, también puede ejecutar el trabajo Crear grupos de usuarios **en Microsoft 365.**

1. Vuelva a la página de administración del complemento (administración del sitio ➡ complementos ➡ integración de Microsoft 365) y seleccione la página **Configuración de Teams.** Deberá configurar algunas opciones para habilitar la integración de aplicaciones de Teams.

    * Para habilitar **OpenID Connect,** seleccione el vínculo Administrar autenticación y seleccione el icono de ojo en la línea  **OpenId Connect** si está en gris.
    * A continuación, deberá habilitar la inserción de fotogramas. Seleccione el **vínculo Seguridad HTTP** y, a continuación, active la casilla junto a Permitir **incrustación de fotogramas.**
    * El siguiente paso es habilitar los servicios web que habilitarán las características de la API de Moodle. Seleccione el **vínculo Características avanzadas** y, a continuación, asegúrese de que la casilla situada junto a Habilitar servicios **web** está activada.
    * Por último, deberá habilitar los servicios externos para Microsoft 365. Seleccione el **vínculo Servicios externos** a continuación:  

        ✔ Seleccione **Editar en** la fila **Dele Microsoft 365 Webservices.**  
        ✔ marca la casilla junto **a Habilitado** y, a continuación, selecciona Guardar **cambios**

    * A continuación, tendrá que editar los permisos de usuario autenticados para permitirles crear tokens de servicio web. Seleccione el **vínculo "Usuario autenticado"** de la función de edición. Desplácese hacia abajo y busque **la funcionalidad Crear un token** de servicio web y marque la **casilla** Permitir.

## <a name="step-3-deploy-the-moodle-assistant-bot-to-azure"></a>Paso 3: Implementar el bot asistente Moodle en Azure

El bot gratuito asistente Moodle para Microsoft Teams ayuda a los profesores y alumnos a responder preguntas sobre sus cursos, tareas, calificaciones y otra información en Moodle. El bot también envía notificaciones de Moodle a los alumnos y profesores de Teams. El bot es un proyecto de código abierto mantenido por Microsoft y está disponible en [GitHub.](https://github.com/microsoft/Moodle-Teams-Bot)

> [!NOTE]
> En esta sección, implementará recursos en su suscripción de Azure. Todos los recursos se configurarán mediante el **nivel** gratuito. Según el uso del bot, es posible que deba escalar estos recursos.
> Si desea usar la pestaña Moodle sin el bot, vaya directamente al [paso 4.](#step-4-deploy-your-microsoft-teams-app)

### <a name="moodle-bot-information-flow"></a>Flujo de información del bot de Moodle

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

Para instalar el bot, primero tendrá que registrarlo en la Plataforma [de identidad de Microsoft.](https://identity.microsoft.com/Landing) Esto permite que el bot se autentique en los puntos de conexión de Microsoft. Para registrar el bot:

1. Vuelva a la página de administración del complemento (administración del sitio ➡ complementos ➡ integración de Microsoft 365) y seleccione la pestaña **Configuración de Teams.**

1. Seleccione el **vínculo Del Portal de registro de** aplicaciones de Microsoft e inicie sesión con su id. de Microsoft.

1. Escribe un nombre para la aplicación (por ejemplo, MoodleBot) y selecciona el **botón** Crear.

1. Copie el **id. de** aplicación y péguelo en el campo **Id. de** aplicación bot de la página **Configuración del** equipo.

1. Seleccione el **botón Generar nueva** contraseña. Copie la contraseña generada y péguela en el campo Contraseña de la aplicación **bot** en la página **Configuración del** equipo.

1. Desplácese hasta la parte inferior del formulario y seleccione **Guardar cambios.**

Ahora que ha generado el identificador de aplicación y la contraseña, es el momento de implementar el bot en Azure:

> [!div class="checklist"]
> * Seleccione el **botón Implementar** en Azure y complete el formulario con la información necesaria (el id. de la aplicación bot, la contraseña de la aplicación bot y el secreto de moodle están en la página Configuración **del** equipo. La información de Azure se encuentra en la **página de** instalación). 
> * Una vez completado el formulario, active la casilla para aceptar los términos y condiciones.
> * Selecciona el **botón Comprar** (todos los recursos de Azure se implementan en el nivel gratuito).

Una vez que los recursos hayan completado la implementación en Azure, deberá configurar el complemento Microsoft 365 Moodle con un punto de conexión de mensajería. Deberá obtener el punto de conexión del bot en Azure:

1. Inicie sesión en [Azure Portal.](https://portal.azure.com)

1. En el panel izquierdo, seleccione **Grupos de recursos** y elija el grupo de recursos que usó (o creó) al implementar el bot.

1. Seleccione el **recurso Bot de WebApp** en la lista de recursos del grupo.

1. Copie el extremo **de mensajería** de la **sección** Información general.

1. En Moodle, abra la **página Configuración del** equipo de su complemento Microsoft 365 Moodle.

1. En el **campo Bot Endpoint** , pegue la dirección URL que acaba de copiar y cambie los mensajes de *word* a *webhook.* La dirección URL debería aparecer ahora de la siguiente manera:  `https://botname.azurewebsites.net/api/webhook`

1. Seleccione **Guardar cambios.**

1. Una vez guardados los cambios,  vuelva a la  pestaña Configuración del equipo, seleccione el botón Descargar archivo de manifiesto y guarde el paquete de manifiesto de la aplicación en el equipo (lo usará en la siguiente sección).

## <a name="step-4-deploy-your-microsoft-teams-app"></a>Paso 4: Implementar la aplicación de Microsoft Teams

Ahora que tiene el bot implementado en Azure y configurado para hablar con su servidor Moodle, es el momento de implementar la aplicación de Microsoft Teams. Para ello, cargará el archivo de manifiesto de la aplicación que descargó de la página Configuración del equipo del complemento Dele de Microsoft 365 en el paso anterior.

Antes de poder instalar la aplicación, deberás asegurarte de que las aplicaciones externas y la carga de aplicaciones están habilitadas. Para ello, puede seguir los pasos descritos en la documentación del espacio empresarial de Microsoft [365.](../concepts/build-and-test/prepare-your-o365-tenant.md) Una vez que hayas asegurado que las aplicaciones externas están habilitadas, puedes seguir los pasos siguientes para implementar la aplicación:

1. Abra **Microsoft Teams.** 

1. Selecciona el **icono de** la aplicación en el área inferior izquierda de la barra de navegación.

1. Selecciona el **vínculo Cargar una aplicación personalizada** de la lista de opciones.

> [!Note]
> Si ha iniciado sesión como administrador global, tendrá la opción de cargar la aplicación en el catálogo de aplicaciones de su organización; de lo contrario, solo podrá cargar la aplicación para un equipo en el que sea miembro.

4. Seleccione el `manifest.zip` paquete que descargó anteriormente y seleccione **Guardar.** Si no has descargado el paquete de manifiesto de  la aplicación, puedes hacerlo desde la pestaña Configuración del equipo de la página de configuración del complemento en Moodle.

Ahora que tiene instalada la aplicación, puede agregar la pestaña a cualquier canal al que tenga acceso. Para ello, ve al canal, selecciona el símbolo **más** (➕) y selecciona la aplicación en la lista. Sigue las indicaciones para terminar de agregar la pestaña del curso Moodle a un canal.

## <a name="step-5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>Paso 5: Permitir la creación automática de pestañas Dele en Microsoft Teams

Aunque las pestañas Moodle se pueden crear manualmente en Microsoft Teams, puede decidir que se cree automáticamente cuando se crean equipos a partir de la sincronización del curso. Para ello, configurará el identificador de la aplicación de Microsoft Teams cargada en Moodle:

1. Abra Microsoft Teams.

1. Selecciona el icono Aplicaciones en el área inferior izquierda de la barra de navegación.

1. Busque la aplicación **Moodle** cargada ➡ el icono **de opciones** ➡ seleccionar **el vínculo copiar.**

1. En un editor de texto, pegue el contenido copiado. Debe contener una dirección URL como ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff. Copie la última parte de la dirección URL, por ejemplo, el id. `00112233-4455-6677-8899-aabbccddeeff` de la aplicación de Microsoft Teams.

1. En Moodle, abra la pestaña de la **aplicación Teams Moodle** desde la página de configuración del complemento Microsoft 365 Moodle.

1. Pegue el identificador de la aplicación de Microsoft Teams en el campo Id. de la aplicación Moodle y guarde los cambios.

Ahora, cuando se sincroniza un curso de Moodle, Microsoft Teams instalará automáticamente la aplicación Moodle en el equipo, creará una pestaña Moodle en el canal general de Teams y la configurará para que contenga la página del curso de Moodle desde la que se sincroniza.

### <a name="thats-it-you-and-your-team-can-now-start-working-with-your-moodle-courses-directly-from-microsoft-teams"></a>Y eso es todo. Usted y su equipo, ahora pueden empezar a trabajar con sus cursos de Moodle directamente desde Microsoft Teams.

Para compartir cualquier solicitud de características o comentarios con nosotros, visite nuestra página [de voz de usuario.](https://microsoftteams.uservoice.com/forums/916759-moodle)
