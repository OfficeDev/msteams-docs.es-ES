---
title: Instalar Moodle LMS
description: Cómo instalar y configurar la aplicación de integración de Moodle para Microsoft Teams
keywords: Complemento de integración de aplicaciones de Teams Moodle
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 091192054c5add7cfbdc1e7baabc86e34cef7631
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020600"
---
# <a name="install-moodle-lms"></a>Instalar Moodle LMS

Moodle es un popular sistema de administración de aprendizaje de código abierto (LMS). Ahora está integrado con Microsoft Teams. Esta integración ayuda a los formadores y profesores a colaborar en torno a los cursos de Moodle, hacer preguntas sobre calificaciones y asignaciones y mantenerse actualizados con las notificaciones directamente en Teams.

Para ayudar a los administradores de TI a configurar fácilmente esta integración, el complemento de Microsoft 365 Moodle de código abierto se actualiza con las siguientes funcionalidades:

* Registro automático del servidor de Moodle con [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (Azure AD).
* Implementación con un solo clic del bot asistente de Moodle en Azure.
* Aprovisionamiento automático de equipos y sincronización automática de las inscripciones de equipo para todos o seleccionar cursos de Moodle.
* Instalación automática de la pestaña Moodle y el bot asistente de Moodle en cada equipo sincronizado.

Para obtener más información sobre la funcionalidad que proporciona esta integración, vea [Microsoft Teams y Moodle](https://education.microsoft.com/resource/3dffb3a8).

## <a name="prerequisites"></a>Requisitos previos

A continuación se indican los requisitos previos para instalar y configurar la aplicación Moodle: 

1. Credenciales de administrador de Moodle.

1. Credenciales de administrador de Azure AD.

1. Una suscripción de Azure en la que puede crear nuevos recursos.

**Para instalar y configurar la aplicación Moodle** 

Realice los siguientes pasos para instalar y configurar la aplicación Moodle: 

## <a name="1-install-the-microsoft-365-moodle-plugins"></a>1. Instalar los complementos de Microsoft 365 Moodle

La integración de Moodle en Microsoft Teams está basada en el conjunto de complementos [de Microsoft 365 Moodle de](https://github.com/Microsoft/o365-moodle)código abierto. Para instalar el complemento en el servidor de Moodle, debe tener instaladas las siguientes aplicaciones:

1. Una [versión estable actual de Moodle](https://download.moodle.org/releases/latest/).

1. Los complementos de Integración de [Microsoft 365](https://moodle.org/plugins/local_o365) y [OpenID Connect](https://moodle.org/plugins/auth_oidc) de Moodle se descargaron y guardaron en el equipo local.

   > [!NOTE]
   > La instalación de los complementos OpenID Connect y Microsoft 365 Integration es necesaria para la integración de Teams. Además, se recomienda encarecidamente el complemento Tema de [Microsoft 365 Teams.](https://moodle.org/plugins/theme_boost_o365teams)

1. Inicie sesión en el servidor de Moodle como administrador y seleccione **Administración** del sitio en el bloque Configuración [ubicado](https://docs.moodle.org/22/en/Settings_block) en el panel de navegación izquierdo.

1. Selecciona la **pestaña Complementos** y, a continuación, selecciona **Instalar complementos.**

1. En la **sección Instalar complemento desde archivo ZIP,** selecciona Elegir un botón **de** archivo.

1. Seleccione **Cargar un archivo en** la navegación izquierda, busque el archivo que descargó y seleccione Cargar este **archivo**.

1. Seleccione la **administración del sitio** en el panel de navegación izquierdo para volver al panel de administración. Desplácese hacia abajo hasta **los complementos locales** y seleccione el vínculo Integración de Microsoft **365.** 

> [!IMPORTANT]
>
> * Mantenga abierta la página de configuración del complemento de Microsoft 365 Moodle en una pestaña del explorador independiente mientras tiene que volver a este conjunto de páginas durante todo el proceso.  <br/><br/>
> * Si no tiene un sitio de Moodle existente, puede consultar El repositorio de Moodle en [Azure](https://github.com/azure/moodle) donde puede implementar rápidamente una instancia de Moodle y personalizarla según sus necesidades.

## <a name="2-configure-the-connection-between-the-microsoft-365-plugin-and-azure-active-directory-azure-ad"></a>2. Configurar la conexión entre el complemento de Microsoft 365 y Azure Active Directory (Azure AD)

Debe registrar Moodle como una aplicación en Azure AD. Use el script de PowerShell para completar este proceso. El script de PowerShell aprovisiona una nueva aplicación de Azure AD para el inquilino de Microsoft 365, que usa el complemento Microsoft 365 Moodle. El script aprovisiona la aplicación para el inquilino de Microsoft 365, configura las direcciones URL de respuesta y los permisos necesarios para la aplicación aprovisionada y devuelve `AppID` el y `Key` . Puede usar el generado y en la página de configuración del complemento `AppID` de Microsoft 365 Moodle para configurar el sitio del servidor `Key` de Moodle con Azure AD.

> [!IMPORTANT]
> * El script de PowerShell no se actualiza con los elementos de configuración más recientes, por lo que debe completar la configuración manualmente siguiendo los pasos descritos en las páginas de lanzamiento de Moodle [3.8.0.4 y 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) y [3.8.0.5 y 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) </br></br>
> * Para ver los pasos manuales que el script de PowerShell automatiza en detalle, vea [Register your Moodle instance as an Application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a>La pestaña Moodle para el flujo de información de Microsoft Teams

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. En la página Complemento de integración de Microsoft 365, seleccione la **pestaña** Configurar.

1. Seleccione el **botón Descargar script de PowerShell** y guárdelo en el equipo local.

1. Debe preparar el script de PowerShell desde el archivo ZIP. Realice los pasos siguientes para preparar el script de PowerShell desde el archivo ZIP:

    1. Descargue y extraiga el `Moodle-AzureAD-Powershell.zip` archivo.
    1. Abra la carpeta extraída.
    1. Haga clic con el botón secundario en `Moodle-AzureAD-Script.ps1` el archivo y seleccione **Propiedades**.
    1. En la **pestaña General** de la ventana Propiedades, active la casilla situada junto al atributo `Unblock` **Security** ubicado en la parte inferior de la ventana.
    1. Seleccione **Aceptar**.
    1. Copie la ruta de acceso del directorio en la carpeta extraída.

1. Ejecute PowerShell como administrador:

    1. Seleccione Inicio.
    1. Escriba PowerShell.
    1. Haga clic con el botón Windows PowerShell.
    1. Seleccione **Ejecutar como administrador**.

1. Navegue al directorio descomprimido escribiendo `cd .../.../Moodle-AzureAD-Powershell` dónde está la ruta de acceso al `.../...` directorio.

1. Ejecute el script de PowerShell:

    1. Escriba `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .
    1. Escriba `./Moodle-AzureAD-Script.ps1` .
    1. Inicie sesión en su cuenta de administrador de Microsoft 365 en la ventana emergente.
    1. Escriba el nombre de la aplicación de Azure AD (por ejemplo, el complemento Moodle/Moodle).
    1. Escriba la dirección URL del servidor de Moodle.
    1. Copie el **identificador de aplicación** y la clave de **aplicación** generados por el script y guárdelos.

1. A continuación, debes agregar `AppID` y al complemento de Microsoft `Key` 365 Moodle. Vuelva a la página de administración del complemento. El flujo es: Administración de sitios ➡ complementos ➡ Integración de Microsoft 365.

1. En la **ficha Configuración,** agregue el **identificador de** aplicación y la clave **de** aplicación que copió anteriormente y, a continuación, seleccione **Guardar cambios**.

1. Después de actualizar la página, puede ver una nueva sección **Elegir método de conexión**. Seleccione la casilla predeterminada **y,** a continuación, **vuelva a seleccionar Guardar cambios.**

1. Después de actualizar la página, puede ver otra nueva sección Consentimiento **de administrador & información adicional**.
    1. Seleccione **El vínculo Proporcionar consentimiento de** administrador, escriba sus credenciales de administrador global de Microsoft 365 y, a continuación, Acepte para conceder los permisos. 
    1. Junto al campo **Inquilino de Azure AD,** seleccione el **botón** Detectar.
    1. Junto a la **dirección URL de OneDrive para la** Empresa, seleccione el **botón** Detectar.
    1. Después de rellenar los campos, vuelva a seleccionar **el** botón Guardar cambios.

1. Seleccione el **botón** Actualizar para comprobar la instalación y, a continuación, **Guarde los cambios**.

1. Sincronizar usuarios entre el servidor de Moodle y Azure AD. Dependiendo del entorno, puede seleccionar diferentes opciones durante esta fase. Para empezar:
    1. Cambiar a la **pestaña Configuración de sincronización**
    1. En la **sección Sincronizar usuarios con Azure AD,** selecciona las casillas que se aplican a tu entorno. Debe seleccionar lo siguiente:  

        ✔ crear cuentas en Moodle para usuarios en Azure AD . 
        ✔ todas las cuentas de Moodle para usuarios de Azure AD.  

    1. En la **sección Restricción de** creación de usuarios, puede configurar un filtro para limitar los usuarios de Azure AD que están sincronizados con Moodle.
    1. La **sección Asignación de campos de** usuario permite personalizar la asignación de campos de Azure AD a Perfil de usuario de Moodle.
    1. En la **sección Sincronización de Teams,** puede seleccionar crear automáticamente grupos, como equipos para algunos o todos los cursos de Moodle existentes.

> [!NOTE]
> El Cron de [Moodle](https://docs.moodle.org/310/en/Cron) se ejecuta de acuerdo con la programación de tareas. La programación predeterminada es una vez al día. Sin embargo, el cron debe ejecutarse con más frecuencia para mantener todo sincronizado.

13. Para validar [los trabajos cron](https://docs.moodle.org/310/en/Cron) y ejecutarlos manualmente para la primera ejecución, seleccione el vínculo **página** Administración de tareas programadas en la sección Sincronizar usuarios con **Azure AD.** Esto le llevará a la **página Tareas programadas.**

    1. Desplácese hacia abajo y busque el trabajo **Sincronizar usuarios con Azure AD** y seleccione Ejecutar **ahora**.
    1. Si selecciona crear grupos basados en cursos existentes, también puede ejecutar el trabajo Crear grupos de usuarios **en Microsoft 365.**

1. Vuelva a la página de administración del complemento. El flujo de navegación es: Administración de sitios ➡ complementos ➡ Microsoft 365 Integratio. A continuación, seleccione la **página Configuración de** Teams. Debes configurar algunas opciones para habilitar la integración de la aplicación de Teams.

    1. Para habilitar **OpenID Connect,** seleccione el vínculo Administrar autenticación y seleccione el icono de ojo en la línea  **OpenId Connect** si está gris.
    1. Habilitar la inserción de fotogramas. Seleccione el **vínculo Seguridad HTTP** y, a continuación, active la casilla situada junto a Permitir **incrustación de fotogramas**.
    1. Habilitar servicios web que habilitan las características de la API de Moodle. Seleccione el **vínculo Características avanzadas** y, a continuación, asegúrese de que la casilla situada junto a Habilitar servicios **web** está activada.
    1. Habilite los servicios externos para Microsoft 365. Seleccione el **vínculo Servicios externos** a continuación:  

        ✔ Seleccione **Editar en** la fila Servicios web de **Microsoft 365 de Moodle.**  
        ✔ marca la casilla junto a **Habilitado** y, a continuación, selecciona **Guardar cambios**

    1. Edite los permisos de usuario autenticados para permitirles crear tokens de servicio web. Seleccione el **vínculo Función de edición "Usuario** autenticado". Desplácese hacia abajo y busque **la funcionalidad Crear un token de servicio web** y marque la **casilla** Permitir.

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a>3. Implementar el bot asistente de Moodle en Azure

El bot asistente de Moodle gratuito para Microsoft Teams ayuda a los profesores y alumnos a responder preguntas sobre sus cursos, tareas, calificaciones y otra información en Moodle. El bot también envía notificaciones de Moodle a alumnos y profesores de Teams. El bot es un proyecto de código abierto mantenido por Microsoft y está disponible en [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).

> [!NOTE]
> * En esta sección debe implementar recursos en su suscripción de Azure. Todos los recursos están configurados mediante **el nivel** gratuito. Según el uso del bot, debe escalar estos recursos.
> * Para usar la pestaña Moodle sin el bot, vaya a [4](#4-deploy-your-microsoft-teams-app).

### <a name="moodle-bot-information-flow"></a>Flujo de información del bot de Moodle

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

Para instalar el bot, debe registrarlo en la [Plataforma de identidad de Microsoft](https://identity.microsoft.com/Landing). Esto permite que el bot se autentique con los puntos de conexión de Microsoft. 

**Para registrar el bot**:

1. Vaya a la página de administración del complemento. Vaya a **Complementos**. En **Integración de Microsoft 365,** seleccione la pestaña **Configuración de Teams.**

1. Seleccione el **vínculo Portal de registro de aplicaciones** de Microsoft e inicie sesión con su id. de Microsoft.

1. Escribe un nombre para la aplicación, como MoodleBot y selecciona el **botón** Crear.

1. Copie el **identificador de aplicación** y péguelo en el campo **Id. de** aplicación bot de la página Configuración **del** equipo.

1. Seleccione el **botón Generar nueva contraseña.** Copie la contraseña generada y péguela en el campo **Contraseña de** la aplicación bot de la página **Configuración del** equipo.

1. Desplácese hasta la parte inferior del formulario y seleccione **Guardar cambios**.

A medida que generó el identificador de aplicación y la contraseña, el siguiente paso es implementar el bot en Azure:

> [!div class="checklist"]
> * Seleccione el **botón Implementar en Azure** y complete el formulario con la información necesaria, como el identificador de aplicación bot, la contraseña de la aplicación bot y el secreto de Estado de ánimo están en la página Configuración **del** equipo. La información de Azure se encuentra en la **página Configuración).** 
> * Después de completar el formulario, active la casilla para aceptar los términos y condiciones.
> * Seleccione el **botón Comprar.** Todos los recursos de Azure se implementan en el nivel gratuito.

Una vez que los recursos hayan completado la implementación en Azure, debe configurar el complemento Microsoft 365 Moodle con un punto de conexión de mensajería. Debe obtener el punto de conexión del bot en Azure:

**Configurar el complemento Microsoft 365 Moodle con un punto de conexión de mensajería**  
1. Inicie sesión en el [Azure Portal](https://portal.azure.com).

1. En el panel izquierdo, seleccione **Grupos de recursos** y seleccione el grupo de recursos que usó o creó, mientras implementa el bot.

1. Seleccione el **recurso Bot de WebApp** de la lista de recursos del grupo.

1. Copie el **extremo de mensajería** de la sección **Información** general.

1. En Moodle, abre la **página Configuración del** equipo de tu complemento de Microsoft 365 Moodle.

1. En el **campo Bot Endpoint,** pegue la dirección URL que acaba de copiar y cambie los mensajes *de palabra* a *webhook*. La dirección URL debería aparecer ahora de la siguiente manera: `https://botname.azurewebsites.net/api/webhook`

1. Seleccione **Guardar cambios**.

1. Después de guardar los cambios, vuelve a  la pestaña Configuración del equipo, selecciona el botón Descargar archivo de manifiesto y guarda el paquete de manifiesto de la aplicación en el equipo para usarlo más adelante. 

## <a name="4-deploy-your-microsoft-teams-app"></a>4. Implementar la aplicación de Microsoft Teams

Después de que el bot se implemente en Azure y esté configurado para hablar con el servidor de Moodle, debes implementar la aplicación de Microsoft Teams. Para ello, debe cargar el archivo de manifiesto de la aplicación que descargó de la página Configuración del equipo del complemento de Microsoft 365 Moodle en el paso anterior.

Antes de instalar la aplicación, debes asegurarte de habilitar las aplicaciones externas y la carga de aplicaciones. Para ello, puede seguir los pasos de la documentación del inquilino de Microsoft 365 de Teams [Prepare your Microsoft 365.](../concepts/build-and-test/prepare-your-o365-tenant.md) Puedes realizar los siguientes pasos para implementar la aplicación: 

**Para implementar la aplicación**

1. Abra **Microsoft Teams**. 

1. Selecciona el **icono Aplicación** en el área inferior izquierda de la barra de navegación.

1. Selecciona el **vínculo Cargar una aplicación personalizada** de la lista de opciones.

   > [!NOTE]
   > Si has iniciado sesión como administrador global, debes tener la opción de cargar la aplicación en el catálogo de aplicaciones de tu organización, de lo contrario solo puedes cargar la aplicación para un equipo en el que seas miembro.

4. Seleccione el `manifest.zip` paquete que descargó anteriormente y seleccione **Guardar**. Si no has descargado el paquete de manifiesto  de la aplicación, puedes descargarlo desde la pestaña Configuración del equipo de la página de configuración del complemento en Moodle.

Ahora que tienes instalada la aplicación, puedes agregar la pestaña a cualquier canal al que tenga acceso. Para ello, vaya al canal, seleccione el símbolo **más** (➕) y seleccione la aplicación en la lista. Sigue las indicaciones para terminar de agregar la pestaña de curso de Moodle a un canal.

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a>5. Permitir la creación automática de pestañas de Moodle en Microsoft Teams

Aunque las pestañas de Moodle se crean manualmente en Microsoft Teams, puede decidir que se crean automáticamente cuando se crean equipos a partir de la sincronización del curso. Para ello, debes configurar el identificador de la aplicación de Microsoft Teams cargada en Moodle:

1. Abra Microsoft Teams.

1. Selecciona el icono Aplicaciones en el área inferior izquierda de la barra de navegación.

1. Busque la aplicación **de Moodle** cargada ➡ el icono **de opciones** ➡ seleccione **copiar vínculo**.

1. En un editor de texto, pegue el contenido copiado. Debe contener una dirección URL como ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff. Copie la última parte de la dirección URL, como  `00112233-4455-6677-8899-aabbccddeeff` , que es el identificador de la aplicación de Microsoft Teams.

1. En Moodle, abre la pestaña de la aplicación **Teams Moodle** desde la página de configuración del complemento de Microsoft 365 Moodle.

1. Pegue el identificador de la aplicación de Microsoft Teams en el campo Id. de aplicación de Moodle y guarde los cambios.

Cuando se sincroniza un curso de Moodle, Microsoft Teams instala automáticamente la aplicación Moodle en el equipo, crea una pestaña Moodle en el canal general de Teams y configúrelo para que contenga la página del curso de Moodle desde la que está sincronizado. Ahora puede empezar a trabajar con los cursos de Moodle directamente desde Microsoft Teams.

Para compartir cualquier solicitud de característica o comentarios con nosotros, visite nuestra página [De voz de usuario](https://microsoftteams.uservoice.com/forums/916759-moodle).

## <a name="see-also"></a>Consulte también

> [!div class="nextstepaction"]
> [Integrar aplicaciones web](~/samples/integrate-web-apps-overview.md)

> [!div class="nextstepaction"]
> [Moodle](https://moodle.org/)

> [!div class="nextstepaction"]
> [Documentación de Moodle](https://docs.moodle.org/34/en/Installing_plugins).
