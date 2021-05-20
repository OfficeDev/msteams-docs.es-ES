---
title: Instalar Moodle LMS
description: Cómo instalar y configurar la aplicación de integración de Moodle para Microsoft Teams
keywords: Teams Plugins de integración de aplicaciones Moodle
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: d7fddad80ca08fd4ca8dee352cdcbc46e8e97dcd
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566722"
---
# <a name="install-moodle-lms"></a>Instalar Moodle LMS

En este artículo aprenderás a instalar moodle LMS.

> [!NOTE]
> Para ayudar a los administradores de TI a configurar fácilmente Moodle y Teams integración, se actualizan los plugins de código abierto Microsoft 365 Moodle para lo siguiente:
>
> * Registro automático del servidor De Moodle con [Azure Active Directory (Azure AD).](https://azure.microsoft.com/services/active-directory/)
>
> * Implementación con un solo clic del bot de Moodle Assistant en Azure.
>
> * Aprovisionamiento automático de equipos y sincronización automática de inscripciones de equipo para todos o seleccionar cursos de Moodle.
>
> * Instalación automática de la pestaña Moodle y el bot asistente de Moodle en cada equipo sincronizado.
>
> Para obtener más información sobre la funcionalidad que proporciona esta integración, consulte [Microsoft Teams y Moodle](https://education.microsoft.com/resource/3dffb3a8).

## <a name="prerequisites"></a>Requisitos previos

A continuación se indican los requisitos previos para instalar Moodle:

* Credenciales de administrador de Moodle.

* Credenciales de administrador de Azure AD.

* Una suscripción de Azure donde puede crear nuevos recursos.

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Instale los plugins Microsoft 365 Moodle

La integración de Moodle en Microsoft Teams está impulsada por el conjunto de plugins de código abierto [Microsoft 365 Moodle.](https://github.com/Microsoft/o365-moodle)

### <a name="requisite-applications-and-plugins"></a>Aplicaciones y plugins necesarios

Asegúrese de instalar y descargar lo siguiente antes de continuar con la instalación de los plugins Microsoft 365 Moodle:

1. Asegúrese de instalar una [versión estable actual de Moodle](https://download.moodle.org/releases/latest/).

1. Descargue y guarde el Conectar De Moodle [OpenID](https://moodle.org/plugins/auth_oidc) y los plugins [de integración de Microsoft 365](https://moodle.org/plugins/local_o365) en su equipo local.

    > [!NOTE]
    > Para la integración Teams se requiere la instalación de los complementos OpenID Conectar y Microsoft 365 Integration.
    >
    > Además, los plugins [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) son muy recomendables.

### <a name="microsoft-365-moodle-plugins"></a>Microsoft 365 Plugins de Moodle

1. Inicie sesión en su servidor Moodle como administrador y seleccione **Administración del sitio** en el bloque [Configuración](https://docs.moodle.org/22/en/Settings_block) ubicado en el panel de navegación izquierdo.

1. Seleccione la pestaña **Plugins** y, a continuación, seleccione **Instalar plugins**.

1. En la sección **Instalar plugins desde archivo ZIP,** seleccione **Elegir un archivo**.

1. Seleccione **Upload una** opción de archivo en el panel de navegación izquierdo, busque el archivo que descargó y seleccione Upload este **archivo**.

1. Seleccione **Administración del sitio** en el panel de navegación izquierdo para volver al panel de administración. Desplázate hacia abajo hasta los **plugins locales** y selecciona el vínculo **integración Microsoft 365.**

    > [!IMPORTANT]
    >
    > * Mantenga su página de configuración de Microsoft 365 Moodle Plugins abierta en una pestaña separada del navegador, ya que necesita volver a este conjunto de páginas durante todo el proceso.  
    >
    > * Si no tiene un sitio de Moodle existente, vaya al repositorio [de Moodle en Azure](https://github.com/azure/moodle) e implemente rápidamente una instancia de Moodle y personalícela según sus necesidades.

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a>2. Configure la conexión entre los complementos de Microsoft 365 y Azure Active Directory (Azure AD)

Debe configurar la conexión entre los complementos de Microsoft 365 y Azure AD.

### <a name="requisites"></a>Requisitos

Registre Moodle como una aplicación en Azure AD mediante el script de PowerShell. El script de Powershell aprovisiona lo siguiente:

* Una nueva aplicación de Azure AD para el inquilino de Microsoft 365, que usa los complementos de Moodle Microsoft 365.
* La aplicación para el inquilino Microsoft 365, configurar las direcciones URL de respuesta necesarias y los permisos para la aplicación aprovisionada y devuelve el `AppID` archivo and `Key` .

Use la página de configuración generada `AppID` y en su Microsoft 365 de configuración de `Key` Moodle Plugins para configurar el sitio del servidor de Moodle con Azure AD.

> [!IMPORTANT]
>
> * El script de PowerShell no se actualiza con los elementos de configuración más recientes, por lo tanto, debe completar la configuración manualmente siguiendo los pasos descritos en las páginas de lanzamiento de Moodle [3.8.0.4 y 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) y [3.8.0.5 y 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release)
>
> * Para obtener más información sobre cómo registrar la instancia de Moodle manualmente, consulte [Registrar la instancia de Moodle como una aplicación.](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>La pestaña Moodle para Microsoft Teams flujo de información

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. En la página Microsoft 365 complementos de integración, seleccione la pestaña **Configuración.**

1. Seleccione el botón **Descargar script de PowerShell** y guárdelo como una carpeta ZIP en el equipo local.

1. Prepare el script de PowerShell desde el archivo ZIP de la siguiente manera: 

    1. Descargue y extraiga el `Moodle-AzureAD-Powershell.zip` archivo.
    1. Abra la carpeta extraída.
    1. Haga clic con el botón derecho en el `Moodle-AzureAD-Script.ps1` archivo y seleccione **Propiedades**.
    1. En la pestaña **General** de la ventana Propiedades, active la `Unblock` casilla situada junto al atributo **Seguridad** situado en la parte inferior de la ventana.
    1. Seleccione **Aceptar**.
    1. Copie la ruta de acceso del directorio a la carpeta extraída.

1. Ejecute PowerShell como administrador:

    1. Seleccione Inicio.
    1. Escriba PowerShell.
    1. Haga clic con el botón derecho en **Windows PowerShell**.
    1. Seleccione **Ejecutar como administrador**.

1. Vaya al directorio descomprimido escribiendo `cd .../.../Moodle-AzureAD-Powershell` dónde está la ruta de acceso al `.../...` directorio.

1. Ejecute el script de PowerShell:

    1. Escriba `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .
    1. Escriba `./Moodle-AzureAD-Script.ps1` .
    1. Inicie sesión en su cuenta de administrador de Microsoft 365 en la ventana emergente.
    1. Escriba el nombre de la aplicación de Azure AD, por ejemplo, los complementos Moodle o Moodle.
    1. Introduzca la dirección URL del servidor Moodle.
    1. Copie el **ID de aplicación ( `AppID` )** y **la clave de aplicación ( `Key` )** generados por el script y guárdelos.

1. A continuación, debe agregar el `AppID` y a la Microsoft 365 `Key` Moodle Plugins. Vuelva a la página de administración de plugins, Administración del sitio > Plugins > Microsoft 365 Integración.

1. En la pestaña **Configuración,** agregue la `AppID` y `Key` copiada anteriormente y, a continuación, seleccione **Guardar cambios**. Después de actualizar la página, puede ver una nueva sección **Elegir método de conexión**.

1. En el **método Elegir conexión**, seleccione la casilla de verificación **Predeterminada** y, a continuación, vuelva a seleccionar **Guardar cambios.**

1. Después de actualizar la página, puede ver otra nueva sección **Consentimiento de administrador & información adicional.**
    1. Seleccione proporcionar el vínculo **de consentimiento de administrador,** escriba las credenciales de administrador global Microsoft 365 y, a continuación, **acepte** conceder los permisos.
    1. Junto al campo **Inquilino de Azure AD,** seleccione el botón **Detectar.**
    1. Junto a la **dirección URL de OneDrive para la Empresa**, seleccione el botón **Detectar.**
    1. Una vez rellenados los campos, vuelva a seleccionar el botón **Guardar cambios.**

1. Seleccione el botón **Actualizar** para comprobar la instalación y, a continuación, seleccione **Guardar cambios**.

1. Sincronice usuarios entre el servidor Moodle y Azure AD. Para empezar:

    > [!NOTE]
    > Dependiendo de su entorno, puede seleccionar diferentes opciones durante esta etapa.

1. Sincronice usuarios entre el servidor Moodle y Azure AD. Dependiendo de su entorno, puede seleccionar diferentes opciones durante esta etapa. Para empezar:
    1. Cambie a la **pestaña Sincronizar Configuración**.

    1. En la sección **Sincronizar usuarios con Azure AD,** active las casillas de verificación que se aplican a su entorno. Debe seleccionar lo siguiente:  

        ✔ Crear cuentas en Moodle para usuarios de Azure AD.

        ✔ Actualizar todas las cuentas de Moodle para los usuarios de Azure AD.

    1. En la sección **Restricción de creación de** usuarios, puede configurar un filtro para limitar los usuarios de Azure AD que se sincroniza con Moodle.
    1. La sección **Asignación de campos de usuario** le permite personalizar la asignación de campos de Perfil de usuario de Azure AD a Moodle.
    1. En la sección **Teams Sync,** puede seleccionar crear automáticamente grupos, como equipos para algunos o todos los cursos de Moodle existentes.

13. Para validar los trabajos [cron](https://docs.moodle.org/310/en/Cron) y ejecutarlos manualmente para la primera ejecución, seleccione el vínculo **Página de administración tareas programadas** en la sección **Sincronizar usuarios con Azure AD.** Esto le lleva a la página **Tareas programadas.**

    1. Desplázate hacia abajo y busca el trabajo **Sincronizar usuarios con Azure AD** y selecciona Ejecutar **ahora.**
    1. Si selecciona crear grupos en función de los cursos existentes, también puede ejecutar crear **grupos de usuarios en Microsoft 365** trabajo.

    > [!NOTE]
    >
    > Moodle [Cron](https://docs.moodle.org/310/en/Cron) se ejecuta de acuerdo con el calendario de tareas. La programación predeterminada es una vez al día. Sin embargo, el cron debe ejecutarse con más frecuencia para mantener todo sincronizado.

1. Vuelva a la página de administración de plugins, **Administración del sitio > Plugins > Microsoft 365 Integración** y seleccione la página **Teams Configuración.**

1. En la página **Teams Configuración,** configure la configuración necesaria para habilitar la integración de Teams aplicación.

    1. Para habilitar **openid Conectar**, seleccione el vínculo **Administrar autenticación** y seleccione el icono de ojo en la línea de **Conectar OpenId** si está atenuado.
    1. Para habilitar la incrustación de fotogramas, seleccione el vínculo **Seguridad HTTP** y, a continuación, active la casilla de verificación situada junto a **Permitir incrustación de fotogramas.**
    1. Para habilitar los servicios web, que habilita las características de la API de Moodle, seleccione el vínculo **Características avanzadas** y, a continuación, asegúrese de que la casilla de verificación situada junto a Habilitar **servicios web** esté activada.
    1. Para habilitar los servicios externos para Microsoft 365, seleccione el vínculo **Servicios externos** y, a continuación:  

        ✔ Seleccione **Editar** en la fila **Servicios web de Microsoft 365 de Moodle.**

        ✔ Seleccione la casilla de verificación situada junto a **Habilitado** y, a continuación, seleccione **Guardar cambios**

    1. Edite los permisos de usuario autenticados para permitirles crear tokens de servicio web.

        ✔ Seleccione el vínculo **De edición de usuario autenticado.**

        ✔ Desplázate hacia abajo y busca la capacidad **Crear un token de servicio web** y selecciona la casilla **Permitir.**

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Implemente el Bot asistente de Moodle en Azure

El bot asistente gratuito de Moodle para Microsoft Teams ayuda a los profesores y estudiantes a responder preguntas sobre sus cursos, tareas, calificaciones y otra información en Moodle. El bot también envía notificaciones de Moodle a estudiantes y profesores dentro de Teams. El bot es un proyecto de código abierto mantenido por Microsoft y está disponible en [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).

> [!NOTE]
>
> * Implemente recursos en la suscripción de Azure. Todos los recursos se configuraron mediante el nivel **gratuito.** Dependiendo del uso del bot, es posible que tenga que escalar estos recursos.
>
> * Para utilizar la pestaña Moodle sin el bot, vaya a [4](#4-deploy-your-microsoft-teams-app).

### <a name="moodle-bot-information-flow"></a>Flujo de información del bot Moodle

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

Para instalar el bot, debe registrarlo en [Microsoft Identity Platform](https://identity.microsoft.com/Landing). Esto permite que el bot se autentique en los puntos de conexión de Microsoft. 

**Para registrar el bot**

1. Vaya a la página de administración de plugins y, a continuación, seleccione **Plugins**. En **Integración Microsoft 365**, seleccione la pestaña **Teams Configuración.**

1. Seleccione el vínculo **Portal de registro de aplicaciones de Microsoft** e inicie sesión con su identificador de Microsoft.

1. Escriba un nombre para la aplicación, como MoodleBot y seleccione el botón **Crear.**

1. Copie el **ID de aplicación** y péguelo en el campo Bot Application **ID** de la página **Team Configuración.**

1. Seleccione el botón **Generar nueva contraseña.** Copie la contraseña generada y péguela en el campo **Contraseña de la aplicación bot** de la página Equipo **Configuración.**

1. Desplázate hasta la parte inferior del formulario y selecciona **Guardar cambios**.

Después de generar el identificador y la contraseña de la aplicación, implemente el bot en Azure:

> [!div class="checklist"]
> * Seleccione **Implementar en Azure** y complete el formulario con la información necesaria, como el identificador de aplicación de bot, la contraseña de la aplicación bot y el secreto de Moodle en la página de **Teams Configuración.** La información de Azure está en la página **Configuración.** 
> * Después de completar el formulario, seleccione la casilla de verificación para aceptar los términos y condiciones.
> * Seleccione **Comprar**. Todos los recursos de Azure se implementan en el nivel gratuito.

Una vez completados los recursos que se implementan en Azure, debe configurar los complementos Microsoft 365 Moodle con un punto de conexión de mensajería. Debe obtener el punto de conexión del bot en Azure:

1. Inicie sesión en el [Azure Portal](https://portal.azure.com).

1. En el panel izquierdo, seleccione **Grupos de recursos** y seleccione el grupo de recursos que usó o creó, al implementar el bot.

1. Seleccione el recurso Bot de **WebApp** en la lista de recursos del grupo.

1. Copie el **punto de conexión** de mensajería en la sección Información **general.**

1. En Moodle, abre la página **de Configuración equipo** de tus plugins de Moodle Microsoft 365.

1. En el campo **Punto de conexión de bot,** pegue la dirección URL que acaba de copiar y cambie los *mensajes* de Word al *webhook*. La dirección URL debe aparecer de la siguiente manera: `https://botname.azurewebsites.net/api/webhook`

1. Seleccione **Guardar cambios**.

1. Después de guardar los cambios, vuelva a la pestaña **Equipo Configuración,** seleccione el botón **Descargar archivo de manifiesto** y guarde el paquete de manifiesto de la aplicación en el equipo para su uso posterior.

## <a name="4-deploy-your-microsoft-teams-app"></a>4. Implemente la aplicación Microsoft Teams

Después de implementar el bot en Azure y configurarse para hablar con el servidor de Moodle, debe implementar la aplicación Microsoft Teams. Para ello debe cargar el archivo de manifiesto de la aplicación que descargó desde la página Microsoft 365 Equipo de plugins de Moodle Configuración en el paso anterior.

Antes de instalar la aplicación debe asegurarse de habilitar aplicaciones externas y cargar aplicaciones. Para obtener más información, consulte [Preparar el inquilino de Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md). 

**Para implementar la aplicación** 

1. Abra **Microsoft Teams**. 

1. Seleccione el icono **Aplicación** en el área inferior izquierda de la barra de navegación.

1. Seleccione la Upload un vínculo de **aplicación personalizado** de la lista de opciones.

   > [!NOTE]
   > Si ha iniciado sesión como administrador global, debe tener la opción de cargar la aplicación en el catálogo de aplicaciones de su organización, de lo contrario solo puede cargar la aplicación para un equipo en el que sea miembro.

4. Seleccione el `manifest.zip` paquete que descargó anteriormente y seleccione **Guardar**. Si no ha descargado el paquete de manifiesto de la aplicación, puede descargar desde la pestaña **Equipo Configuración** de la página de configuración de plugins en Moodle.

Ahora que tienes instalada la aplicación, puedes agregar la pestaña a cualquier canal al que tengas acceso. Para ello, vaya al canal, seleccione el símbolo **más** (➕) y seleccione la aplicación de la lista. Sigue las indicaciones para terminar de agregar la pestaña del curso de Moodle a un canal.

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. Permitir la creación automática de pestañas Moodle en Microsoft Teams

Aunque las pestañas Moodle se crean manualmente en Microsoft Teams, puede decidir crearlas automáticamente cuando se crean equipos a partir de la sincronización del curso. Para ello, debe configurar el identificador de la aplicación de Microsoft Teams cargada en Moodle.

**Para permitir la creación automática de pestañas Moodle**

1. Abra Microsoft Teams.

1. Seleccione el icono Aplicaciones en el área inferior izquierda de la barra de navegación.

1. Busque la **aplicación Moodle** cargada > seleccione el icono **de opciones** > seleccione el **vínculo copiar**.

1. En un editor de texto, pegue el contenido copiado. Debe contener una dirección URL como ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff. Copie la última parte de la dirección URL, como `00112233-4455-6677-8899-aabbccddeeff` , que es el identificador de la aplicación Microsoft Teams.

1. En Moodle, abre la pestaña de la **aplicación Teams Moodle** desde tu página de configuración de Microsoft 365 Moodle Plugins.

1. Pegue el identificador de la aplicación Microsoft Teams en el campo Id.

Cuando se sincroniza un curso de Moodle, Microsoft Teams instala automáticamente la aplicación Moodle en el equipo, crea una pestaña Moodle en el canal General de Teams y la configura para que contenga la página del curso para el curso Moodle desde el que se sincroniza. Ahora puede empezar a trabajar con sus cursos de Moodle directamente desde Microsoft Teams.

> [!NOTE]
> Para compartir cualquier solicitud de función o comentario con nosotros, visite nuestra [página de Voz del usuario](https://microsoftteams.uservoice.com/forums/916759-moodle).

## <a name="see-also"></a>Vea también

- [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)
- [Moodle](https://moodle.org/)
- [Documentación de Moodle](https://docs.moodle.org/34/en/Installing_plugins).

