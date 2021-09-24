---
title: Instalar Moodle LMS
description: Cómo instalar y configurar la aplicación de integración de Moodle para Microsoft Teams
keywords: Teams Complementos de integración de aplicaciones de Moodle
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: bdf5ea5b6f08c638bd00a69df59ae2e25b76b0ad
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157076"
---
# <a name="install-moodle-lms"></a>Instalar Moodle LMS

En este artículo aprenderá a instalar el LMS de Moodle.

> [!NOTE]
> Para ayudar a los administradores de TI a configurar fácilmente La integración de Moodle y Teams, los complementos de código Microsoft 365 de Moodle se actualizan para lo siguiente:
>
> * Registro automático del servidor de Moodle [con Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).
>
> * Implementación con un solo clic del bot asistente de Moodle en Azure.
>
> * Aprovisionamiento automático de equipos y sincronización automática de las inscripciones de equipo para todos o seleccionar cursos de Moodle.
>
> * Instalación automática de la pestaña Moodle y el bot asistente de Moodle en cada equipo sincronizado.
>
> Para obtener más información sobre la funcionalidad que proporciona esta integración, vea [Microsoft Teams y Moodle](https://education.microsoft.com/resource/3dffb3a8).

## <a name="prerequisites"></a>Requisitos previos

Estos son los requisitos previos para instalar Moodle:

* Credenciales de administrador de Moodle.

* Credenciales de administrador de Azure AD.

* Una suscripción de Azure en la que puede crear nuevos recursos.

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Instalar el Microsoft 365 Complementos de Moodle

La integración de Moodle en Microsoft Teams funciona con la tecnología de código Microsoft 365 conjunto de [complementos de Moodle](https://github.com/Microsoft/o365-moodle).

### <a name="requisite-applications-and-plugins"></a>Aplicaciones y complementos necesarios

Asegúrese de instalar y descargar lo siguiente antes de continuar con la instalación Microsoft 365 complementos de Moodle:

1. Asegúrese de instalar una [versión estable actual de Moodle](https://download.moodle.org/releases/latest/).

1. Descargue y guarde los complementos de [integración de Conectar](https://moodle.org/plugins/auth_oidc) y Microsoft 365 [de Integración](https://moodle.org/plugins/local_o365) de Moodle en el equipo local.

    > [!NOTE]
    > La instalación de los Conectar OpenID y Microsoft 365 integration son necesarias para la Teams integración.
    >
    > Además, los complementos [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) son muy recomendables.

### <a name="microsoft-365-moodle-plugins"></a>Microsoft 365 Complementos de Moodle

1. Inicie sesión en el servidor de  Moodle como administrador y seleccione Administración del sitio en el bloque [Configuración](https://docs.moodle.org/22/en/Settings_block) ubicado en el panel de navegación izquierdo.

1. Selecciona la **pestaña Complementos** y, a continuación, selecciona **Instalar complementos.**

1. En la **sección Instalar complementos desde archivo ZIP,** seleccione Elegir un **archivo**.

1. Seleccione **Upload una opción de** archivo en el panel de navegación izquierdo, busque el archivo que descargó y seleccione Upload este **archivo**.

1. Seleccione **Administración del sitio** en el panel de navegación izquierdo para volver al panel de administración. Desplácese hacia abajo hasta **los complementos locales** y seleccione el vínculo Microsoft 365 **integración.**

    > [!IMPORTANT]
    >
    > * Mantenga la Microsoft 365 de configuración de Los complementos de Moodle abierta en una pestaña del explorador independiente mientras necesita volver a este conjunto de páginas a lo largo del proceso.  
    >
    > * Si no tiene un sitio de Moodle existente, vaya al repositorio [de Moodle en Azure](https://github.com/azure/moodle) e implemente rápidamente una instancia de Moodle y personalízala según sus necesidades.

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a>2. Configurar la conexión entre los complementos Microsoft 365 y Azure Active Directory (Azure AD)

Debe configurar la conexión entre los complementos Microsoft 365 y Azure AD.

### <a name="requisites"></a>Requisitos

Registre Moodle como una aplicación en Azure AD con el script de PowerShell. El script de Powershell aprovisiona lo siguiente:

* Una nueva aplicación de Azure AD para su Microsoft 365 inquilino, que usa el Microsoft 365 Complementos de Moodle.
* La aplicación de tu Microsoft 365 inquilino, configura las direcciones URL de respuesta y los permisos necesarios para la aplicación aprovisionada y devuelve `AppID` el y `Key` .

Use la página de configuración generada y Microsoft 365 complementos de Moodle para configurar el sitio de servidor `AppID` `Key` de Moodle con Azure AD.

> [!IMPORTANT]
>
> * El script de PowerShell no se actualiza con los elementos de configuración más recientes, por lo tanto, debe completar la configuración manualmente siguiendo los pasos descritos en las páginas de lanzamiento de Moodle [3.8.0.4 y 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) y [3.8.0.5 y 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release)
>
> * Para obtener más información sobre cómo registrar la instancia de Moodle manualmente, vea [Registrar la instancia de Moodle como una aplicación](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>La pestaña Moodle para Microsoft Teams flujo de información

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. En la Microsoft 365 complementos de integración, seleccione la **pestaña Configurar.**

1. Seleccione el **botón Descargar script de PowerShell** y guárdelo como una carpeta ZIP en el equipo local.

1. Prepare el script de PowerShell desde el archivo ZIP de la siguiente manera: 

    1. Descargue y extraiga el `Moodle-AzureAD-Powershell.zip` archivo.
    1. Abra la carpeta extraída.
    1. Haga clic con el botón secundario en `Moodle-AzureAD-Script.ps1` el archivo y seleccione **Propiedades**.
    1. En la **pestaña General** de la ventana Propiedades, active la casilla situada junto al atributo `Unblock` **Seguridad** situado en la parte inferior de la ventana.
    1. Seleccione **Aceptar**.
    1. Copie la ruta de acceso del directorio en la carpeta extraída.

1. Ejecute PowerShell como administrador:

    1. Seleccione Inicio.
    1. Escriba PowerShell.
    1. Haga clic con el botón secundario **en Windows PowerShell**.
    1. Seleccione **Ejecutar como administrador**.

1. Navegue al directorio descomprimido escribiendo `cd .../.../Moodle-AzureAD-Powershell` dónde está la ruta de acceso al `.../...` directorio.

1. Ejecute el script de PowerShell:

    1. Escriba `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .
    1. Escriba `./Moodle-AzureAD-Script.ps1` .
    1. Inicie sesión en su cuenta Microsoft 365 administrador en la ventana emergente.
    1. Escriba el nombre de la aplicación de Azure AD, por ejemplo, complementos de Moodle o Moodle.
    1. Escriba la dirección URL del servidor de Moodle.
    1. Copie el **identificador de aplicación ( ) `AppID` y** **la clave de aplicación( `Key` )** generados por el script y guárdelos.

1. A continuación, debe agregar `AppID` y al Microsoft 365 Complementos de `Key` Moodle. Vuelva a la página de administración de complementos, Administración del sitio > complementos > Microsoft 365 integración.

1. En la **ficha Configuración,** agregue el y `AppID` copió anteriormente y, a continuación, seleccione Guardar `Key` **cambios**. Después de actualizar la página, puede ver una nueva sección **Elegir método de conexión**.

1. En el **método Choose connection**, seleccione la casilla de verificación predeterminada y, a continuación, seleccione Guardar cambios **de** nuevo. 

1. Después de actualizar la página, puede ver otra nueva sección Consentimiento **de administrador & información adicional**.
    1. Seleccione **El vínculo Proporcionar consentimiento de** administrador, escriba su Microsoft 365 de administrador global y, a continuación, acepte para conceder los permisos. 
    1. Junto al campo **Inquilino de Azure AD,** seleccione el **botón** Detectar.
    1. Junto a la **dirección URL OneDrive para la Empresa**, seleccione el **botón** Detectar.
    1. Después de rellenar los campos, vuelva a seleccionar **el** botón Guardar cambios.

1. Seleccione el **botón** Actualizar para comprobar la instalación y, a continuación, **seleccione Guardar cambios**.

1. Sincronizar usuarios entre el servidor de Moodle y Azure AD. Para empezar:

    > [!NOTE]
    > Dependiendo del entorno, puede seleccionar diferentes opciones durante esta fase.

1. Sincronizar usuarios entre el servidor de Moodle y Azure AD. Dependiendo del entorno, puede seleccionar diferentes opciones durante esta fase. Para empezar:
    1. Cambie a la **pestaña Sincronizar Configuración**.

    1. En la **sección Sincronizar usuarios con Azure AD,** selecciona las casillas que se aplican a tu entorno. Debe seleccionar lo siguiente:  

        ✔ crear cuentas en Moodle para usuarios de Azure AD.

        ✔ todas las cuentas de Moodle para usuarios de Azure AD.

    1. En la **sección Restricción de** creación de usuarios, puede configurar un filtro para limitar los usuarios de Azure AD que están sincronizados con Moodle.
    1. La **sección Asignación de campos de** usuario permite personalizar la asignación de campos de Azure AD a Perfil de usuario de Moodle.
    1. En la **Teams sincronización,** puede seleccionar crear automáticamente grupos, como equipos para algunos o todos los cursos de Moodle existentes.

13. Para validar [los trabajos cron](https://docs.moodle.org/310/en/Cron) y ejecutarlos manualmente para la primera ejecución, seleccione el vínculo **página** Administración de tareas programadas en la sección Sincronizar usuarios con **Azure AD.** Esto le llevará a la **página Tareas programadas.**

    1. Desplácese hacia abajo y busque el trabajo **Sincronizar usuarios con Azure AD** y seleccione Ejecutar **ahora**.
    1. Si selecciona crear grupos basados en cursos existentes, también puede ejecutar el trabajo Crear grupos de usuarios **Microsoft 365** usuario.

    > [!NOTE]
    >
    > El Cron de [Moodle](https://docs.moodle.org/310/en/Cron) se ejecuta de acuerdo con la programación de tareas. La programación predeterminada es una vez al día. Sin embargo, el cron debe ejecutarse con más frecuencia para mantener todo sincronizado.

1. Vuelva a la página de administración de complementos, Administración del **sitio > Complementos > Microsoft 365 integración** y seleccione la **Teams Configuración** página.

1. En la **Teams Configuración,** configure la configuración necesaria para habilitar la integración Teams aplicación.

    1. Para habilitar **OpenID Conectar**,  seleccione el vínculo Administrar autenticación y seleccione el icono de ojo en la línea Conectar **OpenId** si está gris.
    1. Para habilitar la incrustación de fotogramas, seleccione el vínculo **Seguridad HTTP** y, a continuación, active la casilla situada junto a Permitir incrustación **de fotogramas**.
    1. Para habilitar los servicios web, que habilita  las características de la API de Moodle, seleccione el vínculo Características avanzadas y, a continuación, asegúrese de que la casilla situada junto a Habilitar servicios **web** esté seleccionada.
    1. Para habilitar los servicios externos para Microsoft 365, seleccione el vínculo **Servicios** externos y, a continuación:  

        ✔ Seleccione **Editar en** la **fila Moodle Microsoft 365 Webservices.**

        ✔ Seleccione la casilla situada junto a **Habilitado** y, a continuación, **seleccione Guardar cambios**

    1. Edite los permisos de usuario autenticados para permitirles crear tokens de servicio web.

        ✔ Seleccione el vínculo **Editar rol Usuario autenticado.**

        ✔ desplácese hacia abajo y busque **la funcionalidad Crear un token de** servicio web y active la **casilla** Permitir.

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Implementar el bot asistente de Moodle en Azure

El bot asistente de Moodle gratuito para Microsoft Teams ayuda a los profesores y alumnos a responder preguntas sobre sus cursos, asignaciones, calificaciones y otra información en Moodle. El bot también envía notificaciones de Moodle a alumnos y profesores dentro de Teams. El bot es un proyecto de código abierto mantenido por Microsoft y está disponible en [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).

> [!NOTE]
>
> * Implemente recursos en su suscripción de Azure. Todos los recursos se configuraron mediante **el nivel** gratuito. Según el uso del bot, es posible que deba escalar estos recursos.
>
> * Para usar la pestaña Moodle sin el bot, vaya a [4](#4-deploy-your-microsoft-teams-app).

### <a name="moodle-bot-information-flow"></a>Flujo de información del bot de Moodle

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

Para instalar el bot, debe registrarlo en la [Plataforma de identidad de Microsoft](https://identity.microsoft.com/Landing). Esto permite que el bot se autentique con los puntos de conexión de Microsoft. 

**Para registrar el bot**

1. Vaya a la página de administración de complementos y, a continuación, seleccione **Complementos**. En **Microsoft 365 integración,** seleccione la **Teams Configuración** pestaña.

1. Seleccione el **vínculo Portal de registro de aplicaciones** de Microsoft e inicie sesión con su id. de Microsoft.

1. Escribe un nombre para la aplicación, como MoodleBot y selecciona el **botón** Crear.

1. Copie el **identificador de aplicación** y péguelo en el campo **Id.** de aplicación bot de la página **De Configuración** equipo.

1. Seleccione el **botón Generar nueva contraseña.** Copie la contraseña generada y péguela en el campo **Bot Application Password** de la página Team **Configuración.**

1. Desplácese hasta la parte inferior del formulario y seleccione **Guardar cambios**.

Después de generar el identificador de aplicación y la contraseña, implemente el bot en Azure:

> [!div class="checklist"]
> * Seleccione **Implementar en Azure** y complete el formulario con la información necesaria, como el identificador de aplicación bot, la contraseña de la aplicación bot y el secreto de Estado de ánimo en la **Teams Configuración** web. La información de Azure se encuentra en la **página Configuración.** 
> * Después de completar el formulario, selecciona la casilla para aceptar los términos y condiciones.
> * Seleccione **Comprar**. Todos los recursos de Azure se implementan en el nivel gratuito.

Una vez que los recursos hayan completado la implementación en Azure, debe configurar los complementos Microsoft 365 Moodle con un punto de conexión de mensajería. Debe obtener el punto de conexión del bot en Azure:

1. Inicie sesión en [Azure Portal](https://portal.azure.com).

1. En el panel izquierdo, seleccione **Grupos de recursos** y seleccione el grupo de recursos que usó o creó, mientras implementa el bot.

1. Seleccione el **recurso Bot de WebApp** de la lista de recursos del grupo.

1. Copie el **extremo de mensajería** de la sección **Información** general.

1. En Moodle, abra la **página De Configuración** equipo de su Microsoft 365 Complementos de Moodle.

1. En el **campo Bot Endpoint,** pegue la dirección URL que acaba de copiar y cambie los mensajes *de palabra* a *webhook*. La dirección URL debe aparecer de la siguiente manera: `https://botname.azurewebsites.net/api/webhook`

1. Seleccione **Guardar cambios**.

1. Después de guardar los cambios, vuelve **a** la pestaña  Configuración equipo, selecciona el botón Descargar archivo de manifiesto y guarda el paquete de manifiesto de la aplicación en el equipo para usarlo más adelante.

## <a name="4-deploy-your-microsoft-teams-app"></a>4. Implementar la aplicación Microsoft Teams aplicación

Después de que el bot se implemente en Azure y esté configurado para hablar con el servidor de Moodle, debe implementar la aplicación Microsoft Teams usuario. Para ello, debes cargar el archivo de manifiesto de la aplicación que descargaste de la página Microsoft 365 página de Configuración de complementos de Moodle en el paso anterior.

Antes de instalar la aplicación, debes asegurarte de habilitar las aplicaciones externas y la carga de aplicaciones. Para obtener más información, vea [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md). 

**Para implementar la aplicación** 

1. Abra **Microsoft Teams**. 

1. Selecciona el **icono Aplicación** en el área inferior izquierda de la barra de navegación.

1. Selecciona el **Upload de una aplicación** personalizada de la lista de opciones.

   > [!NOTE]
   > Si has iniciado sesión como administrador global, debes tener la opción de cargar la aplicación en el catálogo de aplicaciones de tu organización, de lo contrario solo puedes cargar la aplicación para un equipo en el que seas miembro.

4. Seleccione el `manifest.zip` paquete que descargó anteriormente y seleccione **Guardar**. Si no has descargado el paquete de manifiesto de la aplicación, puedes descargar desde la pestaña De **Configuración** equipo de la página de configuración de complementos de Moodle.

Ahora que tienes instalada la aplicación, puedes agregar la pestaña a cualquier canal al que tenga acceso. Para ello, vaya al canal, seleccione el símbolo **más** (➕) y seleccione la aplicación en la lista. Sigue las indicaciones para terminar de agregar la pestaña de curso de Moodle a un canal.

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. Permitir la creación automática de pestañas de Moodle en Microsoft Teams

Aunque las pestañas de Moodle se crean manualmente en Microsoft Teams, puede decidir crearlas automáticamente cuando se creen equipos a partir de la sincronización del curso. Para ello, debes configurar el identificador de la aplicación Microsoft Teams carga en Moodle.

**Para permitir la creación automática de pestañas de Moodle**

1. Abra Microsoft Teams.

1. Selecciona el icono Aplicaciones en el área inferior izquierda de la barra de navegación.

1. Busque la aplicación **de Moodle** cargada > el icono **de** opciones > seleccione **copiar vínculo**.

1. En un editor de texto, pegue el contenido copiado. Debe contener una dirección URL como ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff. Copia la última parte de la dirección URL, como `00112233-4455-6677-8899-aabbccddeeff` , que es el identificador de la Microsoft Teams aplicación.

1. En Moodle, abre la pestaña Teams de la aplicación **Moodle** desde la Microsoft 365 configuración de Complementos de Moodle.

1. Pegue el identificador de la Microsoft Teams en el campo Id. de aplicación de Moodle y guarde los cambios.

Cuando se sincroniza un curso de Moodle, Microsoft Teams instala automáticamente la aplicación Moodle en el equipo, crea una pestaña Moodle en el canal general de Teams y la configura para que contenga la página del curso de Moodle desde la que está sincronizado. Ahora puede empezar a trabajar con los cursos de Moodle directamente desde Microsoft Teams.

> [!NOTE]
> Para compartir cualquier solicitud de característica o comentarios con nosotros, visite nuestra página [De voz de usuario](https://microsoftteams.uservoice.com/forums/916759-moodle).

## <a name="see-also"></a>Vea también

- [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
- [Moodle](https://moodle.org/)
- [Documentación de Moodle](https://docs.moodle.org/34/en/Installing_plugins).

