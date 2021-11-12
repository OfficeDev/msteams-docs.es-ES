---
title: Introducción a App Studio para Microsoft Teams
description: Comience a crear aplicaciones increíbles en Microsoft Teams a través de App Studio
keywords: introducción a app studio de teams
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 92f24fbb7d4a41a192178ead1e2cb40dd7446b25
ms.sourcegitcommit: 781f34af2a95952bf437d0b7236ae995f4e14a08
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2021
ms.locfileid: "60948638"
---
# <a name="manage-your-apps-with-app-studio-for-microsoft-teams"></a>Administrar tus aplicaciones con App Studio para Microsoft Teams

> [!TIP]
> **Pruebe el Portal para desarrolladores:** App Studio ha evolucionado. Configure, distribuya y administre las aplicaciones Teams con el nuevo [Portal de desarrolladores.](https://dev.teams.microsoft.com/)

Con App Studio, puede crear o integrar sus propias aplicaciones de Microsoft Teams, ya sea que desarrolle aplicaciones personalizadas para su empresa o aplicaciones SaaS para equipos de todo el mundo, mediante la simplificación del proceso de creación del manifiesto y del paquete de su aplicación y mediante herramientas útiles como el Editor de tarjetas y una biblioteca de control de React.

> [!IMPORTANT]
> App Studio actualmente no está disponible en los siguientes tipos Teams organizaciones:
>
> * Government Community Cloud (GCC)
> * GCC High
> * DoD

## <a name="installing-app-studio"></a>Instalación de App Studio

App Studio es una aplicación de Teams que puede encontrar en la tienda de Teams. Siga este vínculo para descargar directamente [App Studio](https://aka.ms/InstallTeamsAppStudio). También puedes encontrar la aplicación en la tienda de aplicaciones.

En la tienda, busque App Studio.

![Entrada en la tienda para App Studio](~/assets/images/get-started/storeteamsappstudio.png)

Seleccione el icono de App Studio para abrir la página de instalación de la aplicación:

![Configurar App Studio](~/assets/images/get-started/teamsappstudioconfiguration.png)

Haga clic en **Instalar**.

![app studio](~/assets/images/get-started/teamsappstudio.png)

Una vez en App Studio, haga clic en la pestaña **Editor de manifiesto**, donde podrá importar una aplicación existente o crear una nueva.

## <a name="app-studio-features"></a>Características de App Studio

En esta sección se tratan las características, como la conversación, el editor de manifiestos, los detalles y las capacidades. Puedes personalizar tus capacidades mediante la personalización de la aplicación.

### <a name="conversation"></a>Conversación

Aquí puede ver el aspecto en Teams de las [tarjetas que puede crear en App Studio](#card-editor) cuando las pruebe enviándoselas a usted mismo.

### <a name="manifest-editor"></a>Editor de manifiestos

Como se indicó anteriormente, la parte más importante de un paquete de aplicaciones de Microsoft Teams es su archivo manifest.json. Este archivo, que debe cumplir con el [esquema de Teams App](~/resources/schema/manifest-schema.md), contiene metadatos que permiten a Teams presentar correctamente la aplicación a los usuarios.

La pestaña Editor de manifiesto en App Studio simplifica la creación del manifiesto, lo que le permite describir la aplicación, cargar los iconos, agregar funcionalidades de la aplicación y generar un archivo .zip que puede cargarse fácilmente en Teams para realizar pruebas o distribuirlo para que otros usuarios lo puedan usar. Tenga en cuenta que App Studio no genera código funcional para la aplicación ni hospeda la aplicación. Para que el proceso de carga de la aplicación dé como resultado una aplicación correcta, su aplicación debe estar hospedada y ejecutándose en la dirección URL que aparece en el manifiesto.

#### <a name="details"></a>Detalles

La sección de detalles del Editor de manifiesto define la descripción de alto nivel de la aplicación que va a realizar. Esto incluye aspectos como el nombre, la descripción y la marca visual de la aplicación. Puede generar automáticamente un GUID para la aplicación y proporcionar direcciones URL para su declaración de privacidad y condiciones de uso.

#### <a name="capabilities"></a>Capacidades

La sección de funciones del Editor de manifiesto es donde están definidas las funcionalidades de la aplicación y donde se muestran los detalles de cada una de esas funcionalidades.

> [!NOTE]
> Como práctica recomendada, debes proporcionar directrices de personalización para que los usuarios de la aplicación y los clientes puedan seguir al personalizar la aplicación. Para obtener más información, consulta [Personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).

##### <a name="tabs"></a>Pestañas

* **Pestañas del equipo.** Una pestaña de equipo forma parte de un canal y proporciona acceso rápido a la información y los recursos del equipo. Por ejemplo, la pestaña Planificador de un canal contiene un único plan; la pestaña Power BI se asigna a un informe específico. Los usuarios pueden explorar en profundidad el contexto correspondiente, pero no deberían poder navegar fuera de la pestaña. La pestaña Power BI, por ejemplo, no habilita la navegación a otros informes de Power BI, aunque habilita el botón *Ir al sitio web*, que inicia el informe en el sitio web principal de Power BI.

  Para las pestañas de equipo, debe proporcionar una *Configuración de dirección URL* para presentar opciones y recopilar información para que los usuarios puedan personalizar el contenido y la experiencia de su pestaña. Esta página HTML aumentada se muestra cuando un usuario primero agrega la pestaña a un canal.

  También debe proporcionar los dominios adicionales desde los que la pestaña espera cargarse o con los que se vincula.

* **Pestañas personales.** Esta sección te permite definir un conjunto de pestañas que se presentan de forma predeterminada en la experiencia de la aplicación personal (experiencia que un usuario tiene con la aplicación fuera del contexto de un equipo o canal). En esta sección, proporcione el nombre de pestaña, un identificador único, la dirección URL que apunta a la interfaz de usuario que se mostrará en Teams y, opcionalmente, la dirección URL que se usará si un usuario opta por ver la pestaña en un explorador. Con Teams pestañas, proporcione los dominios adicionales desde los que la pestaña espera cargarse o vincular a.

##### <a name="bots"></a>Bots

Esta sección le permite agregar un [bot de conversación](~/bots/what-are-bots.md) a la aplicación. Si ya tiene un bot registrado con Bot Framework, puede agregarlo haciendo clic en *Configurar* y suministrando el nombre del bot, el id. de Bot Framework y definiendo los ámbitos en los que funcionará el bot.

Si todavía no ha registrado ningún bot con Bot Framework, haga clic en **Registrarse** para crear uno nuevo. Cuando haya terminado de registrar el bot, vuelva a esta sección del Editor de manifiesto para escribir su nombre y el id. de Bot Framework.

Después de proporcionar la información del bot, ahora puedes definir opcionalmente una lista de comandos que el bot pueda sugerir a los usuarios. Agregue el nombre del comando, una descripción del comando que indique su sintaxis y argumentos, y el ámbito al que debe aplicarse este comando.

> [!NOTE]
> Si ha definido el bot para que solo admita un ámbito, se omitirán los comandos especificados para el ámbito no compatible. Puede editar el ámbito con el que admite el bot en cualquier momento.

##### <a name="connectors"></a>Conectores

Esta sección le permite agregar un conector a la aplicación. Si ya registró un Conector de Office 365, elija **Configurar** y escriba el nombre y el id. del conector. Si desea un conector nuevo haga clic en **Registrarse** para ir al Panel del desarrollador de conectores en el explorador.

##### <a name="messaging-extensions"></a>Extensiones de mensajería

Las [extensiones de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) son una forma eficaz de que los usuarios interactúen con su aplicación en Microsoft Teams. Los usuarios pueden consultar la información desde su servicio y publicar esa información en forma de tarjetas, directamente en el canal o en la conversación del chat.

Las extensiones de mensajería funcionan con tecnología de los bots de Bot Framework, por lo que requieren de un bot configurado para funcionar. Si tiene el nombre y el id. de Bot Framework del bot al que le gustaría dar el poder de la extensión de mensajería, introdúzcalos. De lo contrario, haga clic en **Registrarse** para crear uno e introduzca la información después. Seleccione si el usuario puede actualizar la configuración de una extensión de mensajería.

Una vez que haya configurado el bot subyacente, defina los comandos y parámetros que la extensión de mensajería puede aceptar.

Cada comando necesita un título y un id. De manera opcional, el comando puede contener una descripción para el usuario. Cada comando puede admitir hasta cinco parámetros, cada uno de los cuales requiere:

* Nombre del parámetro tal como aparece en el Teams cliente y se incluye en la solicitud de usuario.
* Un título fácil de usar.
* Una descripción opcional.

> [!NOTE]
> Para crear una extensión de mensajería con app studio, consulta [crear una extensión de mensajería con app studio](~/resources/create-messaging-extension-using-appstudio.md).

#### <a name="test-and-distribute"></a>Prueba y distribución

Una vez que haya terminado de definir la aplicación, la sección Prueba y distribución le permite exportar la definición de la aplicación como un archivo zip que puede compartir y cargar en el cliente de Teams para realizar pruebas. Al hacer clic en exportar, se descarga el archivo zip *nombredeapp.zip* en el directorio de descarga predeterminado.

##### <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams
En la página principal del proyecto, puede cargar la aplicación a un equipo, enviarla a la tienda de aplicaciones personalizada de la organización para los usuarios de su organización o enviarla al origen de la aplicación para todos los usuarios de Teams. El administrador de TI revisará estas entregas. Puede volver a la página *Publicar* para comprobar el estado de entrega y saber si su administrador de TI aprobó o rechazó la aplicación. Aquí también es a donde deberá acudir para enviar las actualizaciones a su aplicación o cancelar cualquier entrega activa en este momento.

### <a name="card-editor"></a>Editor de tarjetas

Una tarjeta es un contenedor para unidades de información breves o relacionadas. Microsoft Teams es compatible con las tarjetas, las cuales pueden tener varias propiedades y datos adjuntos. Las tarjetas son una forma clave de que los bots y los conectores retransmitan información que requiere acción a los usuarios. 

Para que este proceso sea más fácil y menos propenso a errores, la pestaña Editor de tarjetas te permite crear tarjetas de héroe o tarjetas en miniatura con un formulario y comprobar y probar la tarjeta resultante (exactamente como lo vería un usuario) a través de un bot. También proporciona el código JSON, C# o Node.js correspondiente para la tarjeta que puede copiar y pegar en el código fuente de la aplicación.

Si ya tiene una tarjeta que le gustaría comprobar dentro de Teams, puede pegar el JSON de esa tarjeta en la pestaña JSON en *Agregar información de tarjeta* y enviársela a sí mismo para ver su apariencia en un chat.

### <a name="react-control-library"></a>Biblioteca de controles de React

>[!Note]
> Esta React de control está en desuso en el futuro. Considera la posibilidad [de usar los Fluent de react](https://microsoft.github.io/fluent-ui-react/) de la interfaz de usuario como una alternativa anteriormente Stardust UI.

Crear una aplicación que siga los procedimientos recomendados de Teams es una forma ideal de proporcionar a la aplicación una apariencia que se ajuste perfectamente a la experiencia del cliente de Teams. Los controles de la interfaz de usuario que use son fundamentales para lograr ese fin. Para facilitar la creación de una interfaz de usuario coherente, App Studio proporciona varias categorías de controles de interfaz de usuario que siguen los principios de diseño de Teams.

Se proporcionan ejemplos de los controles y los componentes correspondientes de React y están listos para usar para crear la aplicación.

#### <a name="controls"></a>Controles

Los controles incluyen:

* Botones
* Listas desplegables
* Casillas de verificación
* Botones de radio
* Alternancias
* Áreas de texto
* Vínculos
* Pestañas
* Tablas
* Iconos

## <a name="see-also"></a>Consulte también

[Administrar tus aplicaciones con el Portal de desarrolladores para Microsoft Teams](~/concepts/build-and-test/teams-developer-portal.md)