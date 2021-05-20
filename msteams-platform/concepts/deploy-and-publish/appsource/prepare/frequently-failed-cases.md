---
title: Consejos de envío de aplicaciones y casos con frecuencia fallidos
description: describe los consejos para un envío exitoso de Teams tienda y las razones comunes por las que los envíos fallan
ms.topic: reference
localization_priority: Normal
ms.author: lajanuar
keywords: consejos de envío de aplicaciones con frecuencia fallan las directrices de validación de casos
ms.openlocfilehash: 50bbd2af3b4c834e2ac4776e1fc7db1d8bf45173
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565276"
---
# <a name="tips-for-a-successful-microsoft-teams-app-submission"></a>Sugerencias para un envío exitoso de aplicaciones Microsoft Teams

>[!NOTE]
>Esta página estará en desuso en mayo de 2021. Para obtener más información sobre cómo publicar correctamente la aplicación, consulte las [directrices de validación de la tienda Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).

Este artículo aborda las razones comunes por las que las aplicaciones enviadas fallan en la validación. Aunque no está destinado a ser una lista exhaustiva de todos los problemas potenciales con la aplicación, seguir esta guía aumentará la probabilidad de que el envío de la aplicación pase la primera vez. Para obtener más información, consulte [Políticas de certificación de Marketplace comercial](/legal/marketplace/certification-policies) para obtener una extensa lista de directivas de validación.

>[!NOTE]
>**[La sección 1140](/legal/marketplace/certification-policies#1140-teams)** es específica para Microsoft Teams y **[la subsección 1140.4](/legal/marketplace/certification-policies#11404-functionality)** aborda los requisitos de funcionalidad para aplicaciones Teams.

## <a name="validation-guidelines--most-failed-test-cases"></a>Las directrices de validación & los casos de prueba más fallidos

### <a name="9989-general-considerations"></a>&#9989; Consideraciones generales

* Asegúrese de que está utilizando la versión 1.4.1 o posterior del [SDK de Microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js).
* No realice cambios en la aplicación mientras el proceso de validación esté en curso. Para ello, será necesario una revalidación completa de la aplicación.
* La aplicación no debe dejar de responder, finalizar de forma inesperada ni contener errores de programación. Si se produce un problema, la aplicación debe producir un error y proporcionar información válida para el acceso al usuario.
* La aplicación no debe descargar, instalar ni iniciar automáticamente ningún código ejecutable en el entorno de usuario. Todas las descargas deben solicitar permiso explícito al usuario.
* Cualquier material que asocie con su experiencia, como descripciones y documentación de soporte técnico, debe ser preciso. La ortografía, el uso de mayúsculas y minúsculas, la puntuación y la gramática de las descripciones y materiales deben ser correctos.
* Proporcione información de ayuda y soporte técnico. Se recomienda encarecidamente que la aplicación incluya un vínculo de ayuda o preguntas frecuentes para la experiencia de usuario de la primera ejecución. Para todas las aplicaciones personales, le recomendamos que proporcione su página de ayuda como una pestaña personal para una mejor experiencia de usuario.
* Todas las aplicaciones deben tener un recorrido visual, como **Take a Tour** o una Guía de **aplicaciones** en su pantalla de configuración que hable sobre las características de la aplicación y la integración necesaria en los siguientes lugares:
    * La página de listado de la tienda (Descripción larga).
    * Pantalla de configuración de pestañas.
    * Mensaje de bienvenida para un bot.
    * Metadatos de origen de la aplicación.
    * Pantalla de configuración del conector.

* El recorrido visual puede ser un vídeo, una captura de pantalla, un enlace a una pestaña estática con detalles de la aplicación. Todas estas referencias deben estar dentro del entorno Teams.

    ![Ejemplo de aplicación 1 ](../../../../assets/images/faq/Sampleapp1.png) ![ aplicación de ejemplo 2](../../../../assets/images/faq/Sampleapp2.png)

* Incremente el número de versión de la aplicación en el manifiesto si realiza cambios manifiestos en el envío.
* La aplicación no debe sacar a los usuarios de Teams para escenarios de usuario principales. Los destinos de vínculos en aplicaciones no deben vincularse a un explorador externo. Los destinos de vínculo deben vincularse a elementos div contenidos en Teams, por ejemplo, módulos de tareas y pestañas. 
* Se sugiere el uso de módulos de tareas o pestañas para mostrar información a los usuarios dentro de Teams.
* Todos los escenarios principales y no principales deben completarse dentro del entorno Teams excepto:
  * Directiva de privacidad
  * Condiciones de uso (TOU)
  * Enlace al sitio web
  * Proceso de inscripción

* Las aplicaciones personales permiten a los usuarios compartir contenido desde una experiencia de aplicación personal con otros miembros del equipo.

### <a name="9989-provide-a-clear-and-simple-sign-in-sign-out-and-sign-up-experience"></a>&#9989; Proporcionar una experiencia clara y sencilla de inicio de sesión, inicio de sesión e inscripción

* Si la aplicación o el complemento depende de cuentas o servicios externos, la experiencia de inicio de sesión, cierre de sesión e registro debe ser evidente y accesible en todas las funcionalidades de la aplicación.
* Si se proporciona una opción de inicio de sesión explícito al usuario, debe haber una opción de cierre de sesión correspondiente (incluso si la aplicación usa [autenticación silenciosa).](../../../../tabs/how-to/authentication/auth-silent-aad.md)
* La opción de cierre de sesión solo debe cerrar sesión en la funcionalidad de la aplicación y no fuera del cliente Teams.
* Como mínimo, la opción de cierre de sesión debe cerrar sesión con el usuario de las mismas capacidades a las que se accede con la opción de inicio de sesión. Por ejemplo, si la opción de inicio de sesión incluye tanto la extensión de mensajería como la pestaña, la opción de cierre de sesión debe incluir tanto la extensión de mensajería como la pestaña.

* Asegúrese de que siempre hay una manera de revertir los siguientes comportamientos (o similares):
  * Inicio de sesión => cierre de sesión.
  * Vincular una cuenta/servicio => desvincular una cuenta o servicio.
  * Conectar una cuenta/servicio => desconectar una cuenta/servicio.
  * Autorizar una cuenta/servicio => desautorizar/denegar una cuenta/servicio.
  * Registre una cuenta/servicio => desregistro/anule la suscripción a una cuenta/servicio.
* Si la aplicación requiere una cuenta o un servicio, debe proporcionar una manera para que el usuario se registre o cree una solicitud de registro. Se puede conceder una excepción si la aplicación requiere una licencia para usarla. En estos escenarios, proporcione instrucciones claras para que un nuevo usuario se registre.
* Proporcione instrucciones claras sobre el camino a seguir a un nuevo usuario sobre cómo registrarse para usar los servicios de la aplicación. Si no hay un vínculo de registro listo, proporcione orientación precisa en las siguientes áreas:

> [!div class="checklist"]
>
> * dentro de la sección de descripción de la aplicación.
> * en el mensaje de bienvenida de la aplicación.
> * en el mensaje de ayuda de la aplicación.
> * en la ventana donde se le pide a un usuario que inicie sesión en sus servicios.

* Las aplicaciones sin un flujo de registro fácil también deben incluir una pestaña de ayuda o un vínculo a una página web, donde un nuevo usuario puede ver instrucciones detalladas sobre cómo configurar la aplicación Teams. Proporcione información detallada para asegurarse de que un nuevo usuario no está bloqueado al probar la aplicación por primera vez.
* La funcionalidad de inicio de sesión y cierre de sesión debe funcionar en clientes móviles. Asegúrese de usar la versión 1.4.1 o posterior [del SDK de Microsoft Teams.](https://www.npmjs.com/package/@microsoft/teams-js)

Para obtener información adicional sobre la autenticación, consulte:

* [Documentación de autenticación](../../../authentication/authentication.md)
* [Ejemplo de autenticación de bots en el nodo](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
* [Ejemplo de autenticación de pestañas en el nodo](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Autenticación de tabulador/bot en C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

### <a name="9989-response-times-must-be-reasonable"></a>&#9989; Los tiempos de respuesta deben ser razonables

* **Pestañas**. Si una respuesta a una acción tarda más de tres segundos, debe proporcionar un mensaje de carga o una advertencia.
* **Bots**. Una respuesta a un comando de usuario debe producirse en un plazo de dos segundos. Si se requiere un procesamiento más largo, la aplicación debe mostrar un indicador de escritura.
* **Componer extensiones**. Una respuesta a un comando de usuario debe producirse en un plazo de cinco segundos.

> [!TIP]
> Asegúrese de que la aplicación muestre un indicador de carga o algún tipo de advertencia cuando la aplicación tarda más de lo esperado en responder.

### <a name="9989-tab-content-must-not-have-excessive-chrome-or-layered-navigation"></a>&#9989; Contenido de tabulador no debe tener un cromo excesivo o navegación en capas

* Las pestañas deben proporcionar contenido enfocado y evitar elementos de interfaz de usuario innecesarios. Esto normalmente se refiere a la navegación anidada o en capas innecesaria, una interfaz de usuario innecesaria o irrelevante junto al contenido o cualquier vínculo que lleve al usuario al contenido no relacionado. Por ejemplo, la siguiente vista de pestaña omite los menús de navegación y solo muestra el contenido principal:

![SharePoint vista web](../../../../assets/images/faq/web-sp.png)  
![vista de pestaña SharePoint](../../../../assets/images/faq/tab-sp.png)

* Las pestañas deben ser de naturaleza ligera y no incluir navegación compleja.
* Las pestañas de canal que tienen capacidades de edición complejas dentro de la aplicación deben abrir la vista del editor en una ventana múltiple en lugar de una pestaña.
* Las pestañas de canal no deben proporcionar una barra de aplicaciones con iconos en el carril izquierdo que entren en conflicto con la navegación principal Teams.
* Las pestañas no deben presentar una barra de aplicaciones con iconos en el carril izquierdo que entren en conflicto con la navegación principal Teams.
* Las pestañas que tienen capacidades de edición complejas dentro de la aplicación deben abrir la vista del editor en una ventana múltiple en lugar de en la pestaña.
* Si hay varias opciones de vista, considere la posibilidad de tener un menú de configuración de pestañas para que el usuario elija. Por ejemplo, en lugar de incrustar un menú dentro de la pestaña, coloque el menú en la página de configuración para que la vista de pestaña real esté limpia y enfocada.
* Incluya una pestaña *ayuda* como pestaña estática para aconsejar a los usuarios cómo configurar, registrarse y usar la aplicación.
* Incluya una *pestaña Configuración* que esté disponible en el encabezado de la aplicación.

![Página de configuración de ideas amplias](../../../../assets/images/faq/wideidea.png)

### <a name="9989-tab-configuration-must-happen-in-the-configuration-screen"></a>&#9989; configuración de tabulación debe ocurrir en la pantalla de configuración

* La pantalla de configuración debe explicar claramente el valor de la experiencia y cómo configurar la pestaña.
* El proceso de configuración siempre debe proporcionar una manera para que los usuarios continúen y no finalicen la experiencia del usuario. Por ejemplo, no muestre una placa vacía después de que el usuario haya configurado la pestaña.
* El proceso de inicio de sesión del usuario debe formar parte del proceso de configuración. Asegúrese de completarlo en la interfaz de usuario de tabulación. Una vez que el usuario ha completado la configuración y cargado la pestaña, no se requiere ninguna otra acción.
* No muestre toda la página web dentro de la ventana emergente configuración de inicio de sesión.
* Un usuario siempre debe ser capaz de terminar la experiencia de configuración, incluso si no puede encontrar inmediatamente el contenido que está buscando.
* La experiencia de configuración debe proporcionar opciones para que el usuario encuentre su contenido, ancle una dirección URL o cree contenido nuevo si no existe.
* La experiencia de configuración debe permanecer dentro del contexto Teams. El usuario no debería tener que dejar la experiencia de configuración para crear contenido y, a continuación, volver a Teams para anclarlo.
* Utilice el área de ventana gráfica disponible de forma eficiente. No lo desperdicie en el uso de logotipos enormes dentro de la configuración emergente.

![OneNote permite a los usuarios pegar un enlace de OneNote en caso de que no se puedan encontrar notas](../../../../assets/images/faq/tab-onenote-config.png)

![Los usuarios siempre pueden crear un nuevo plan en el planificador en caso de que no haya otros existentes](../../../../assets/images/faq/tab-planner-config.png)

![SharePoint también permite al usuario pegar directamente un enlace de SharePoint](../../../../assets/images/faq/tab-sp-config.png)

### <a name="9989-tabs-in-channel---member-access"></a>pestañas de &#9989; en canal - Acceso de miembros

* Una pestaña configurada por un miembro en un ámbito de canal debe ser accesible para los demás miembros sin tener que buscar permisos del miembro que configuró la pestaña.
* La aplicación debe proporcionar las opciones de administración de permisos por adelantado si la pestaña es para uso privado o restringido o requiere permisos del miembro que configuró la pestaña.

### <a name="9989-bots-must-always-be-responsive-and-fail-gracefully"></a>&#9989; Bots siempre deben ser receptivos y fallar con gracia

El bot debe responder a cualquier comando y no al usuario sin salida. Estos son algunos consejos para ayudar a su bot a responder inteligentemente a los usuarios:

* **Utilice listas de comandos**. Analizar la entrada del usuario o predecir la intención del usuario es difícil. En lugar de permitir que los usuarios adivinen lo que el bot puede hacer, proporcione una lista de comandos que el bot entienda.

![lista de comandos de Flow](../../../../assets/images/faq/flow-bot.png)

* **Incluya un comando de ayuda**. Es probable que los usuarios escriban "Ayuda" cuando se pierdan o cuando el bot no responda como se esperaba. Incluya un comando de ayuda que describa cómo se experimentará el valor de la aplicación junto con todos los comandos válidos.

![Flow comando de ayuda](../../../../assets/images/faq/flow-help.png)

* **Incluya contenido de ayuda u orientación cuando se pierda el bot.** Cuando el bot no puede comprender la entrada del usuario, debe sugerir una acción alternativa. Por ejemplo, *"Lo siento, no lo entiendo. Escriba "ayuda" para obtener más información."* No responda con un mensaje de error o simplemente, *"No entiendo".*

### <a name="9989-help-command-response"></a>respuesta del comando ayuda &#9989;

* Comando de ayuda debe ser preciso y las respuestas de la aplicación deben estar en un formato de tarjeta adaptable con un contenido procesable para al menos seis comandos.
* Si una aplicación tiene menos de seis comandos, compruebe si todos los comandos están presentes en la tarjeta adaptable.

  ![Ejemplo de comando de ayuda](../../../../assets/images/faq/helpcommand.png)

* **Utilice tarjetas adaptables y módulos de tareas para que la respuesta del bot sea clara y procesable** 
 [Las tarjetas adaptables con botones que invocan módulos de tareas](/task-modules-and-cards/task-modules/task-modules-bots.md) mejoran la experiencia del usuario del bot. Estas tarjetas y botones son más fáciles de usar en un dispositivo móvil en lugar de que el usuario escriba los comandos. Además, las respuestas de bot no deben ser textuales con texto largo. Los bots deben hacer uso de tarjetas adaptables y módulos de tareas en lugar de interfaz de usuario basada en chat conversacional y respuestas de texto largas.

* **Piense en todos los ámbitos.** Asegúrese de que el bot proporcione las respuestas adecuadas cuando se mencione ( `@*botname*` ) en un canal y en conversaciones personales. Si el bot no proporciona un contexto significativo dentro del ámbito personal o de los equipos, deshabilite ese ámbito a través del manifiesto. (Consulte el `bots` bloque en la referencia de esquema de manifiesto [Microsoft Teams](../../../../resources/schema/manifest-schema.md#bots).)

* **Incluya el equipo, el chat de grupo o la conversación 1:1.** Las notificaciones de bots deben incluir un equipo, un chat de grupo o una conversación uno a uno con contenido relevante para su audiencia.

* **No inserte datos confidenciales.** Los bots no deben insertar datos confidenciales en un equipo, un chat de grupo o una conversación 1:1, donde hay una audiencia que no debe ver esos datos.

* **Proporcione un mensaje de bienvenida.** Bot debe proporcionar un mensaje de bienvenida FRE que incluya un tutorial interactivo con tarjetas de carrusel o botones "pruébalo", para fomentar la interacción.

### <a name="9989-personal-bots-must-always-send-a-welcome-message-on-first-launch"></a>&#9989; Los bots personales siempre deben enviar un mensaje de bienvenida en el primer lanzamiento

Un mensaje de bienvenida es la mejor manera de establecer el tono para su bot de chat personal. Esta es la primera interacción que un usuario tiene con el bot. Un buen mensaje de bienvenida puede animar al usuario a seguir explorando la aplicación. Si el mensaje de bienvenida o introductorio es confuso o poco claro, los usuarios no verán el valor de la aplicación inmediatamente y perderán interés.
Consulte la siguiente sección para obtener los requisitos de mensajes de bienvenida:

> [!Note]
> Un mensaje de bienvenida es opcional para un bot de canal.

### <a name="welcome-message-requirements"></a>Requisitos de mensajes de bienvenida

* Incluya una propuesta de valor con el tour de bienvenida.
* Proporcione instrucciones de avance para usar la aplicación.
* Incluya instrucciones sobre cómo registrarse y configurar la aplicación.
* Presente texto fácil de leer y diálogo directo, preferiblemente una tarjeta con un botón de visita de bienvenida accionable que carga un módulo de tareas.
* Manténgalo simple y utilizable con botones y tarjetas: evite el texto largo, el diálogo conversativo.
* Incluya tarjetas y botones adaptables para hacer que el mensaje de bienvenida sea más utilizable.
* Invoque el mensaje de bienvenida con un ping, no dos o más pings simultáneos.
* Un mensaje de bienvenida sólo debe mostrarse al usuario que configuró la aplicación, preferiblemente en un chat personal 1:1.
* Las aplicaciones personales siempre deben proporcionar un mensaje de bienvenida a un usuario.
* Nunca envíes un chat personal a todos los miembros del equipo; se considera spam.
* Nunca envíe el mensaje de bienvenida más de una vez. No se permite repetir el mismo mensaje de bienvenida a intervalos regulares y se considera spam.

#### <a name="avoid-welcome-message-spamming"></a>Evite el spam de mensajes de bienvenida

* **Mensaje de canal por bot**. No spam usuarios mediante la creación de nuevas publicaciones de chat independientes. Cree una sola publicación de subproceso con respuestas en el mismo subproceso.
* **Chat personal por bot**. No envíes varios mensajes. Envíe un mensaje con información completa. No se permite repetir el mismo mensaje de bienvenida a intervalos regulares y se considera spam.

#### <a name="notification-only-bot-welcome-messages"></a>Mensajes de bienvenida de bots solo de notificación

Los bots de solo notificación deben enviar un mensaje de bienvenida que incluya un mensaje que *transmita: "Soy un bot solo de notificación y no podré responder a tus chats".*

#### <a name="welcome-messages-in-the-personal-scope"></a>Mensajes de bienvenida en el ámbito personal

   * **Haga que su mensaje sea conciso e informativo.** La experiencia del usuario y el conocimiento de la aplicación variarán. Un usuario puede haber usado la aplicación en otra plataforma o no saber nada sobre la aplicación. Quieres adaptar tu mensaje a todas las audiencias y en un par de frases explicar lo que hace tu bot y las formas de interactuar con él. También debe explicar el valor de la aplicación y cómo los usuarios se beneficiarán de su uso.
![Bot de café y comedor](../../../../assets/images/faq/cafe-bot.png)

* **Haga que su mensaje sea procesable.** Piensa en lo primero que quieres que hagan los usuarios después de instalar la aplicación. ¿Hay un comando genial que deben probar? ¿Hay otra experiencia de incorporación que deban conocer? ¿Necesitan iniciar sesión? Puede agregar acciones en una tarjeta adaptable o proporcionar ejemplos específicos como *"Intentar preguntar...",* *"Esto es lo que puedo hacer...".*

#### <a name="welcome-messages-in-the-team-or-channel--scope"></a>Mensajes de bienvenida en el equipo o alcance del canal

Las cosas son un poco diferentes cuando el bot se agrega por primera vez a un canal. Normalmente, no debe enviar un mensaje 1:1 a todos los miembros del equipo, pero el bot puede enviar un mensaje de bienvenida en el canal.

### <a name="9989-mobile-responsiveness-no-direct-upsell-or-payment"></a>&#9989; capacidad de respuesta móvil, sin alza directa ni pago

* Las pestañas, las tarjetas adaptables, los mensajes de bot y el contenido de los módulos de tareas deben responder para una variedad de tamaños de pantallas de dispositivos móviles.
* Las aplicaciones que admiten iOS deben ser completamente funcionales en los últimos iPad dispositivo con la versión más reciente de iOS.
* No debe incluir referencias directas a compras dentro de la aplicación, ofertas de prueba, ofertas para versiones de pago o enlaces a cualquier tienda en línea donde los usuarios puedan comprar o adquirir otro contenido, aplicaciones o complementos de su aplicación Teams en el sistema operativo móvil (Android, iOS).
* La versión para iOS o Android del complemento no debe mostrar ninguna interfaz de usuario o idioma ni enlace a ninguna otra aplicación, complemento o sitio web que pida al usuario que pague.
* Las páginas de política de privacidad y términos de uso asociadas también deben estar libres de cualquier interfaz de usuario comercial o enlaces de la Tienda.

### <a name="9989-do-not-post-sensitive-data-to-an-audience-not-intended-to-view-the-data"></a>&#9989; No publique datos confidenciales en una audiencia no destinada a ver los datos

Su aplicación de Teams no debe publicar datos confidenciales como tarjeta de crédito o instrumento de pago financiero, información de identificación personal (PIN), salud o información de seguimiento de contactos a una audiencia no destinada a ver esos datos.

### <a name="9989-do-not-transmit-financial-payment-details-or-complete-financial-transactions-via-your-teams-app"></a>&#9989; No transmita detalles de pago financiero ni complete transacciones financieras a través de su aplicación de Teams

* La aplicación Teams no debe pedir a los usuarios que realicen un pago directamente dentro de Teams interfaz.
* Es posible que las aplicaciones no transmitan detalles del instrumento financiero a través del usuario en la interfaz de la aplicación. Las aplicaciones solo pueden transmitir enlaces a servicios de pago seguros a los usuarios si esto se revela en los Términos de uso de la aplicación, la Política de privacidad y cualquier página de perfil o sitio web de la aplicación antes de que un usuario acepte usar la aplicación.

### <a name="9989-clear-warning-before-downloading-any-files-or-executable-exe-into-a-users-environment"></a>&#9989; Advertencia clara antes de descargar archivos o ejecutables ( `.exe` ) en el entorno de un usuario

Advierta a los usuarios antes de que la aplicación descargue cualquier archivo o ejecutable ( `.exe`  ) en el equipo o entorno del usuario.

### <a name="9989-messaging-extensions-must-provide-help-text-and-be-easy-to-read"></a>&#9989; Extensiones de mensajería deben proporcionar texto de ayuda y ser fáciles de leer

* La extensión de mensajería basada en búsqueda debe proporcionar texto de ayuda sobre cómo buscar eficazmente (por ejemplo, mostrar entrada de ejemplo).
* Los módulos de tareas deben incluir un icono y un nombre corto en el que estén contenidos o creados desde la aplicación.
* Los ejecutables de extensión de mensaje `@mention` deben ser claros, fáciles de entender y fáciles de leer.
![Extensión de mensaje](../../../../assets/images/faq/message-extension.png)

## <a name="m365-publisher-attestation"></a>M365 Publisher Atestación

### <a name="9989-complete-the-publisher-attestation-in-partner-center"></a>&#9989; Completar la Publisher Attestation en el Centro de Partners

* Consulte la documentación completa del programa [Publisher Attestation](/microsoft-365-app-certification/docs/attestation) para obtener más detalles.
* Siga los pasos de la [sección Flujo de trabajo de atestación Publisher](/microsoft-365-app-certification/docs/userguide#3publisher-attestation-workflow) para completar el proceso de certificación del publicador. Escriba a appcert@microsoft.com para cualquier pregunta.
* Refiera a la [guía de troubleshooting](/azure/active-directory/develop/troubleshoot-publisher-verification) para la información adicional.
* Completa la autoatestación a través del centro asociado. Rellene el cuestionario de Self-Assessment en **Cumplimiento de aplicaciones.**

## <a name="see-also"></a>Vea también

* [Obtén más información sobre las directivas de aprobación de aplicaciones Teams](/legal/marketplace/certification-policies#1140-teams)
* [Sección 100 — General](/legal/marketplace/certification-policies#100-general)
* [Sección 1100.5 — Control del cliente](/legal/marketplace/certification-policies#11005-customer-control)
