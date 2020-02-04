---
title: Introducción a App Studio para Microsoft Teams
description: Empezar a compilar excelentes aplicaciones en Microsoft Teams con App Studio
keywords: Introducción a teams de App Studio
ms.date: 03/20/2019
ms.openlocfilehash: 9a88c6be552905a1dbd41d691c160a39f0123710
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676090"
---
# <a name="quickly-develop-apps-with-app-studio-for-microsoft-teams"></a>Desarrollar rápidamente aplicaciones con App Studio para Microsoft Teams

App Studio facilita la creación o la integración de sus propias aplicaciones de Microsoft Teams, ya sea que desarrolle aplicaciones personalizadas para sus aplicaciones empresariales o SaaS para equipos de todo el mundo mediante la optimización de la creación del manifiesto y el paquete de la aplicación y proporcionan herramientas útiles como el editor de tarjetas y una biblioteca de controles de reAct.

## <a name="installing-app-studio"></a>Instalación de App Studio

App Studio es una aplicación de Microsoft teams que se puede encontrar en el almacén de Teams. Siga este vínculo para la descarga directa: [App Studio](https://aka.ms/InstallTeamsAppStudio) (también puede encontrar la aplicación en la App Store).

En la tienda, busque App Studio.

![Entrada de la tienda para App Studio](~/assets/images/get-started/storeteamsappstudio.png)

Seleccione el icono de App Studio para abrir la página instalación de la aplicación:

![Configurar App Studio](~/assets/images/get-started/teamsappstudioconfiguration.png)

Seleccione *instalar*.

![App Studio](~/assets/images/get-started/teamsappstudio.png)

Una vez que esté en App Studio, haga clic en la pestaña del *Editor de manifiestos* , donde puede importar una aplicación existente o crear una aplicación nueva.

## <a name="app-studio-features"></a>Características de App Studio

### <a name="conversation"></a>Conversación

Aquí es donde puede ver qué [cartas crea en App Studio](#card-editor) en Teams al probarlas enviándose a sí mismo.

### <a name="manifest-editor"></a>Editor de manifiestos

Como se mencionó anteriormente, la parte más significativa de un paquete de la aplicación de Microsoft Teams es su archivo manifest. JSON. Este archivo, que debe cumplir el esquema de la [aplicación Teams](~/resources/schema/manifest-schema.md), contiene metadatos que permiten a los equipos presentar correctamente la aplicación a los usuarios.

La pestaña del editor de manifiestos de App Studio simplifica la creación del manifiesto, lo que le permite describir la aplicación, cargar los iconos, agregar funcionalidades de aplicaciones y generar un archivo. zip que se puede cargar fácilmente en Teams para su uso o distribución para otros usuarios. Tenga en cuenta que App Studio no produce código funcional para la aplicación ni hospeda la aplicación. La aplicación ya debe estar hospedada y en ejecución en la dirección URL que aparece en el manifiesto para el proceso de carga de la aplicación para dar como resultado una aplicación que funcione.

#### <a name="details"></a>Detalles

La sección Detalles del editor de manifiestos define la descripción de alto nivel de la aplicación que está realizando. Esto incluye cosas como el nombre, la descripción y la marca visual de la aplicación. Puede generar automáticamente un GUID para la aplicación y proporcionar direcciones URL para la declaración de privacidad y las condiciones de uso.

#### <a name="capabilities"></a>Capacidades

La sección funcionalidades del editor de manifiestos es donde se definen las capacidades de la aplicación y donde se enumeran los detalles de cada una de esas funcionalidades.

##### <a name="tabs"></a>Pestañas

* **Pestañas de equipo.** Una pestaña de equipo se convierte en parte de un canal y proporciona acceso rápido a la información y los recursos del equipo. Por ejemplo, la ficha Planner para un canal contiene un plan único; la pestaña Power BI se asigna a un informe específico. Los usuarios pueden explorar en profundidad hasta el contexto relevante, pero no deben poder navegar fuera de la pestaña. Por ejemplo, la pestaña Power BI no permite la navegación a otros informes de Power BI, pero habilita el botón *ir a sitio web* que inicia el informe en el sitio web principal de Power BI.

  Para las pestañas de equipo, debe proporcionar una *dirección URL de configuración* para presentar las opciones y recopilar información para que los usuarios puedan personalizar el contenido y la experiencia de la pestaña. Esta página HTML iframe se muestra cuando un usuario agrega la ficha a un canal por primera vez.

  También debe proporcionar los dominios adicionales que la pestaña espera que se carguen o que se vinculen a ellos.

* **Pestañas personales.** Esta sección le permite definir un conjunto de pestañas que se presentan de forma predeterminada en la experiencia de la aplicación personal (es decir, la experiencia que tiene un usuario con la aplicación fuera del contexto de un equipo o canal). En esta sección, especifique el nombre de la pestaña, un identificador único, la dirección URL que apunta a la interfaz de usuario que se va a mostrar en Microsoft Teams y, opcionalmente, la dirección URL que se debe usar si un usuario opta por ver la pestaña en un explorador. Al igual que con las pestañas de Microsoft Teams, proporcione los dominios adicionales de los que la pestaña espera cargar o vincular.

##### <a name="bots"></a>Bots

Esta sección le permite agregar un bot? n de [conversación](~/bots/what-are-bots.md) a su aplicación. Si ya tiene un bot registrado con bot Framework, puede agregarlo haciendo clic en *configurar* y proporcionando el nombre del bot, el identificador del marco de Bot y la definición de los ámbitos en los que funcionará el bot.

Si todavía no ha registrado un bot con el marco de trabajo de bot, haga clic en *registrar* para crear uno nuevo. Una vez que haya terminado de registrar el bot, vuelva a esta sección del editor de manifiestos para escribir su nombre y el identificador del marco de bot.

Una vez que haya proporcionado la información de su bot, puede definir opcionalmente una lista de comandos que el bot puede sugerir a los usuarios. Agregue el nombre del comando, una descripción del comando que indica la sintaxis y los argumentos, y los ámbitos a los que se debe aplicar este comando.

Tenga en cuenta que si ha definido el bot para que admita solo un ámbito, se omitirán los comandos especificados para el ámbito no admitido. Puede editar los ámbitos que admite el bot en cualquier momento.

##### <a name="connectors"></a>Conectores

Esta sección le permite agregar un conector a la aplicación. Si ya ha registrado un conector de Office 365, elija *configurar* y escriba el nombre y el identificador del conector. Si desea que un nuevo conector haga clic en *registrar* para que se vaya al panel del programador del conector en el explorador.

##### <a name="messaging-extensions"></a>Extensiones de mensajería

[Las extensiones de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) son una manera eficaz de que los usuarios participen con la aplicación en Microsoft Teams. Los usuarios pueden consultar la información de su servicio y publicarla en forma de tarjetas, directamente en la conversación de canal o chat.

Las extensiones de mensajería se alimentan mediante bots de bot Framework, por lo que necesitan un bot configurado para funcionar. Si tiene el nombre y el identificador del marco de bot de la utilidad de mensajería, escriba la extensión de mensajería. De lo contrario, haga clic en *registrar* para crear una y escriba la información posteriormente. Seleccione si el usuario puede actualizar la configuración de una extensión de mensajería.

Una vez que haya configurado el bot subyacente, defina los comandos y los parámetros que la extensión de mensajería puede aceptar.

Cada comando requiere un título y un identificador. El comando puede contener opcionalmente una descripción del usuario. Cada comando puede admitir hasta cinco parámetros, cada uno de los cuales requiere:

* El nombre del parámetro tal como aparece en el cliente de Teams y se incluye en la solicitud del usuario.
* Un título descriptivo
* Una descripción opcional

#### <a name="test-and-distribute"></a>Probar y distribuir

Una vez que haya terminado de definir la aplicación, la sección probar y distribuir permite exportar la definición de la aplicación como un archivo zip que, a continuación, se puede compartir y cargar en el cliente de Microsoft Teams para realizar las pruebas. Al hacer clic en exportar se descarga el archivo zip como *AppName. zip* en el directorio de descarga predeterminado.

### <a name="card-editor"></a>Editor de tarjetas

Una tarjeta es un contenedor de datos cortos o relacionados. Microsoft Teams admite tarjetas, que pueden tener varias propiedades y datos adjuntos. Las tarjetas son un método clave por el que los bots y conectores retransmiten información que requiere acciones a los usuarios. 

Para que este proceso sea más fácil y menos propenso a errores, la ficha Editor de tarjetas le permite crear tarjetas de héroe o de miniaturas con un formulario y comprobar y probar la tarjeta resultante (exactamente como la vería un usuario) a través de un bot. También proporciona el código JSON, C# o node. js correspondiente para la tarjeta que puede copiar o pegar en el código fuente de la aplicación.

Si ya tiene una tarjeta que desea comprobar dentro de los equipos, puede pegar el JSON de esa tarjeta en la pestaña JSON en *Agregar información de tarjeta* y enviarla a sí mismo para ver el aspecto que tiene en un chat.

### <a name="react-control-library"></a>Biblioteca de control de reAct

>[!Note]
> Esta biblioteca de control de reAct estará en desuso en el futuro. Considere la posibilidad de usar los controles de la [interfaz de usuario Fluent como alternativa](https://microsoft.github.io/fluent-ui-react/) (anteriormente Stardust UI).

La creación de una aplicación que siga los procedimientos recomendados de Microsoft Teams es una buena forma de dar a su aplicación un aspecto que se ajusta perfectamente a la experiencia del cliente de Microsoft Teams. Los controles de la interfaz de usuario que usa son fundamentales para lograr ese fin. Para que sea más fácil crear una interfaz de usuario coherente, App Studio proporciona varias categorías de controles de interfaz de usuario que siguen los principios de diseño de los equipos.

Se proporcionan ejemplos de los controles y sus componentes de reAct correspondientes, listos para usarlos en la creación de la aplicación.

#### <a name="controls"></a>Controles

Entre los controles se incluyen:

* Botones
* Desplegables
* Casillas
* Botones de opción
* Alterna
* Áreas de texto
* Vínculos
* Pestañas
* Tablas
* Iconos
