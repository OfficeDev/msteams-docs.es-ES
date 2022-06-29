---
title: Introducción a App Studio para Microsoft Teams
description: En este artículo, aprenderá a compilar y administrar las aplicaciones con App Studio para Microsoft Teams e instalar App Studio.
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 6ec2e1dfc064302de096cb356641a773e7dceb35
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2022
ms.locfileid: "66485709"
---
# <a name="manage-your-apps-with-app-studio-for-microsoft-teams"></a>Administración de aplicaciones con App Studio para Microsoft Teams

> [!WARNING]
> **Pruebe el Portal para desarrolladores**: App Studio ha evolucionado. Configurar, distribuir y administrar las aplicaciones de Teams con el nuevo [Portal para desarrolladores](https://dev.teams.microsoft.com/). <br> App Studio estará en desuso el 01 de agosto de 2022.

Con App Studio, puede crear o integrar sus propias aplicaciones de Microsoft Teams, ya sea que desarrolle aplicaciones personalizadas para su empresa o aplicaciones SaaS para equipos de todo el mundo, mediante la simplificación del proceso de creación del manifiesto y del paquete de su aplicación y mediante herramientas útiles como el Editor de tarjetas y una biblioteca de control de React.

> [!IMPORTANT]
> App Studio no está disponible actualmente en los siguientes tipos de organizaciones de Teams:
>
> * Government Community Cloud (GCC)
> * GCC High
> * DoD

## <a name="installing-app-studio"></a>Instalación de App Studio

App Studio es una aplicación de Teams que se puede encontrar en la tienda de Teams. Siga este vínculo para descargar directamente [App Studio](https://aka.ms/InstallTeamsAppStudio). También puede encontrar la aplicación en la tienda de aplicaciones.

En la tienda, busque App Studio.

:::image type="content" source="../../assets/images/get-started/StoreTeamsAppStudio.png" alt-text="Entrada en la tienda para App Studio":::

Seleccione el icono de App Studio para abrir la página de instalación de la aplicación:

:::image type="content" source="../../assets/images/get-started/teamsAppStudioConfiguration.png" alt-text="Configurar App Studio":::

Haga clic en **Instalar**.

:::image type="content" source="../../assets/images/get-started/TeamsAppStudio.png" alt-text="app studio":::

Una vez que esté en App Studio, seleccione en la pestaña **Editor de manifiestos** , donde puede importar una aplicación existente o crear una nueva aplicación.

## <a name="app-studio-features"></a>Características de App Studio

En esta sección se tratan características como la conversación, el editor de manifiestos, los detalles y las funcionalidades. Puede personalizar sus funcionalidades mediante la personalización de la aplicación.

### <a name="conversation"></a>Conversación

Aquí puede ver el aspecto en Teams de las [tarjetas que puede crear en App Studio](#card-editor) cuando las pruebe enviándoselas a usted mismo.

### <a name="manifest-editor"></a>Editor de manifiestos

Como se mencionó anteriormente, la parte más importante de un paquete de aplicación de Teams es su archivo manifest.json. Este archivo, que debe cumplir el esquema de la [aplicación de Teams](~/resources/schema/manifest-schema.md), contiene metadatos, lo que permite a Teams presentar correctamente la aplicación a los usuarios.

La pestaña Editor de manifiestos de App Studio simplifica la creación del manifiesto, lo que le permite describir la aplicación, cargar los iconos, agregar funcionalidades de la aplicación y generar un archivo de .zip, que se puede cargar fácilmente en Teams para probar o distribuir para que otros usuarios lo usen. App Studio no genera código funcional para la aplicación ni hospeda la aplicación. Para que el proceso de carga de la aplicación dé como resultado una aplicación correcta, su aplicación debe estar hospedada y ejecutándose en la dirección URL que aparece en el manifiesto.

#### <a name="details"></a>Detalles

La sección de detalles del Editor de manifiestos define la descripción de alto nivel de la aplicación que está realizando. Esto incluye aspectos como el nombre, la descripción y la marca visual de la aplicación. Puede generar automáticamente un GUID para la aplicación y proporcionar direcciones URL para su declaración de privacidad y condiciones de uso.

#### <a name="capabilities"></a>Capacidades

La sección de funciones del Editor de manifiesto es donde están definidas las funcionalidades de la aplicación y donde se muestran los detalles de cada una de esas funcionalidades.

> [!NOTE]
> Como procedimiento recomendado, debes proporcionar directrices de personalización para que los usuarios y los clientes de la aplicación lo sigan al personalizar la aplicación. Para obtener más información, consulte [Personalización de aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).

##### <a name="tabs"></a>Pestañas

* **Pestañas del equipo.** Una pestaña de equipo forma parte de un canal y proporciona acceso rápido a la información y los recursos del equipo. Por ejemplo, la pestaña Planificador de un canal contiene un único plan; la pestaña Power BI se asigna a un informe específico. Los usuarios pueden explorar en profundidad el contexto pertinente, pero no deben poder navegar fuera de la pestaña. Por ejemplo, la pestaña Power BI no permite la navegación a otros informes de Power BI, pero sí el botón *Ir al sitio web* que inicia el informe en el sitio web principal de Power BI.

  Para las pestañas de equipo, debe proporcionar una *Configuración de dirección URL* para presentar opciones y recopilar información para que los usuarios puedan personalizar el contenido y la experiencia de su pestaña. Esta página HTML aumentada se muestra cuando un usuario primero agrega la pestaña a un canal.

  También debe proporcionar los dominios adicionales desde los que la pestaña espera cargarse o con los que se vincula.

* **Pestañas personales.** Puedes definir un conjunto de pestañas que se presentan de forma predeterminada en la experiencia de la aplicación personal (experiencia que un usuario tiene con la aplicación fuera del contexto de un equipo o canal). En esta sección, proporcione el nombre de pestaña, un identificador único, la dirección URL que apunta a la interfaz de usuario que se mostrará en Teams y, opcionalmente, la dirección URL que se usará si un usuario opta por ver la pestaña en un explorador. Con las pestañas de Teams, proporcione los dominios adicionales desde los que la pestaña espera cargarse desde o vincularse.

##### <a name="bots"></a>Bots

Esta sección le permite agregar un [bot de conversación](~/bots/what-are-bots.md) a la aplicación. Si ya tiene un bot registrado con Bot Framework, puede agregarlo haciendo clic en *Configurar* y proporcionando el nombre del bot, el identificador de Bot Framework y definiendo los ámbitos en los que funciona el bot.

Si aún no ha registrado un bot con Bot Framework, seleccione **Registrar** para crear uno nuevo. Cuando haya terminado de registrar el bot, vuelva a esta sección del Editor de manifiesto para escribir su nombre y el id. de Bot Framework.

Después de proporcionar la información del bot, ahora puede definir opcionalmente una lista de comandos que el bot puede sugerir a los usuarios. Agregue el nombre del comando, una descripción del comando, que indica su sintaxis y argumentos, y los ámbitos a los que se debe aplicar este comando.

> [!NOTE]
> Si ha definido el bot para que solo admita un ámbito, se omiten los comandos especificados para el ámbito no admitido. Puede editar el ámbito con el que admite el bot en cualquier momento.

##### <a name="connectors"></a>Conectores

Esta sección le permite agregar un conector a la aplicación. Si ya registró un Conector de Office 365, elija **Configurar** y escriba el nombre y el id. del conector. Si desea un nuevo conector, seleccione **Registrar** para ir al panel del desarrollador del conector en el explorador.

##### <a name="message-extensions"></a>Extensiones de mensaje

[Las extensiones de mensaje](~/messaging-extensions/what-are-messaging-extensions.md) son una manera eficaz de que los usuarios interactúen con la aplicación en Teams. Los usuarios pueden consultar la información desde su servicio y publicar esa información en forma de tarjetas, directamente en el canal o en la conversación del chat.

Las extensiones de mensaje tienen tecnología de bots de Bot Framework, por lo que requieren un bot configurado para funcionar. Si tiene el nombre y el identificador de Bot Framework del bot que le gustaría potenciar la extensión del mensaje, escriba esta. De lo contrario, seleccione **Registrar** para crear uno y escriba la información posteriormente. Seleccione si el usuario puede actualizar la configuración de una extensión de mensaje.

Una vez configurado el bot subyacente, defina los comandos y parámetros que puede aceptar la extensión de mensaje.

Cada comando necesita un título y un id. De manera opcional, el comando puede contener una descripción para el usuario. Cada comando puede admitir hasta cinco parámetros, cada uno de los cuales requiere:

* Nombre del parámetro tal como aparece en el cliente de Teams y se incluye en la solicitud de usuario.
* Un título fácil de usar.
* Una descripción opcional.

> [!NOTE]
> Para crear una extensión de mensaje mediante App Studio, consulte [Creación de una extensión de mensaje mediante App Studio](~/resources/create-messaging-extension-using-appstudio.md).

#### <a name="test-and-distribute"></a>Prueba y distribución

Una vez que haya terminado de definir la aplicación, la sección Prueba y distribución le permite exportar la definición de la aplicación como un archivo ZIP, que luego se puede compartir y cargar en el cliente de Teams para realizar pruebas. Al hacer clic en exportar, se descarga el archivo zip *nombredeapp.zip* en el directorio de descarga predeterminado.

##### <a name="publish-your-app-to-teams"></a>Publicar la aplicación en Teams

En la página principal del proyecto, puede cargar la aplicación a un equipo, enviarla a la tienda de aplicaciones personalizada de la organización para los usuarios de su organización o enviarla al origen de la aplicación para todos los usuarios de Teams. El administrador de TI revisa estos envíos. Puede volver a la página *Publicar* para comprobar el estado de entrega y saber si su administrador de TI aprobó o rechazó la aplicación. Aquí también es a donde deberá acudir para enviar las actualizaciones a su aplicación o cancelar cualquier entrega activa en este momento.

### <a name="card-editor"></a>Editor de tarjetas

Una tarjeta es un contenedor para unidades de información breves o relacionadas. Teams admite tarjetas, que pueden tener varias propiedades y datos adjuntos. Las tarjetas son una forma clave de que los bots y los conectores retransmitan información que requiere acción a los usuarios.

Para que este proceso sea más fácil y menos propenso a errores, la pestaña Editor de tarjetas le permite crear tarjetas prominentes o tarjetas en miniatura mediante un formulario y comprobar y probar la tarjeta resultante (exactamente como lo vería un usuario) a través de un bot. También proporciona el código JSON, C# o Node.js correspondiente para la tarjeta que puede copiar y pegar en el código fuente de la aplicación.

Si ya tiene una tarjeta que le gustaría comprobar dentro de Teams, puede pegar el JSON de esa tarjeta en la pestaña JSON en *Agregar información de tarjeta* y enviársela a sí mismo para ver su apariencia en un chat.

### <a name="react-control-library"></a>Biblioteca de controles de React

>[!Note]
> Esta biblioteca de control de React está en desuso en el futuro. Considere la posibilidad de usar [los controles react de Fluent-UI como alternativa](https://microsoft.github.io/fluent-ui-react/) a la interfaz de usuario de Stardust anteriormente.

Crear una aplicación que siga los procedimientos recomendados de Teams es una forma ideal de proporcionar a la aplicación una apariencia que se ajuste perfectamente a la experiencia del cliente de Teams. Los controles de la interfaz de usuario que use son fundamentales para lograr ese fin. Para facilitar la creación de una interfaz de usuario coherente, App Studio proporciona varias categorías de controles de interfaz de usuario, que siguen los principios de diseño de Teams.

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

## <a name="app-studio-to-developer-portal"></a>Portal de App Studio para desarrolladores

App Studio estará en desuso, puede usar el Portal para desarrolladores. En la tabla siguiente se proporciona la información detallada de las características admitidas en el Portal para desarrolladores:

| Características | App Studio | Portal para desarrolladores |
| --- | --- | --- |
| Análisis de aplicaciones* | ❌ | ✔️ |
| Funcionalidades de la aplicación: bots | ✔️ | ✔️ |
| Funcionalidades de la aplicación: conectores | ✔️ | ✔️ |
| Funcionalidades de la aplicación: extensión de mensajería | ✔️ | ✔️ |
| Funcionalidades de la aplicación: extensión de reunión | ❌ | ✔️ |
| Funcionalidades de la aplicación:Aplicaciones personales | ✔️ | ✔️ |
| Funcionalidades de la aplicación: pestañas | ✔️ | ✔️ |
| Entornos de aplicación | ❌ | ✔️ |
| Idiomas de la aplicación | ✔️ | ✔️ |
| Versión preliminar y descarga del manifiesto de aplicación | ✔️ | ✔️ |
| Planes de aplicación y precios | ❌ | ✔️ |
| Publicación de aplicaciones | ✔️ | ✔️ |
| Permisos de aplicación | ❌ | ✔️ |
| Uso compartido de aplicaciones con co-desarrolladores | ❌ | ✔️ |
| Validación de aplicaciones | ✔️ | ✔️ |
| Creación de una nueva aplicación | ✔️ | ✔️ |
| Impartir un paquete zip | ✔️ | ✔️ |

\**El análisis de aplicaciones estará disponible para disponibilidad general pronto.*

## <a name="see-also"></a>Vea también

[Administre sus aplicaciones con el Portal para desarrolladores de Microsoft Teams](~/concepts/build-and-test/teams-developer-portal.md)
