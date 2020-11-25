---
title: Sugerencias y casos con errores frecuentes
description: Describe las sugerencias para el envío y la mayoría de las directivas con errores
author: laujan
ms.author: lajanuar
ms.topic: how to
keywords: Validación de las aplicaciones de Teams más errores de prueba de AppSource de aprobación rápida publicar
ms.openlocfilehash: b1333448eb8b8e1e2310114bf95404b74aa95b58
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409109"
---
# <a name="tips-for-a-successful-app-submission"></a>Sugerencias para un envío de aplicación correcto

En este artículo se tratan los motivos comunes de error de validación de aplicaciones enviadas. Aunque no se trata de ser una lista exhaustiva de todos los problemas potenciales de la aplicación, si se sigue esta guía, aumentará la probabilidad de que el envío de la aplicación pase la primera vez. *Vea* [directivas de certificación de mercado comercial](/legal/marketplace/certification-policies) para obtener una lista completa de las directivas de validación.

>[!NOTE]
>La **[sección 1140](/legal/marketplace/certification-policies#1140-teams)** es específica para Microsoft Teams y **[sub-Section 1140,4](https://docs.microsoft.com/legal/marketplace/certification-policies#11404-functionality)** requisitos de funcionalidad para las aplicaciones de Teams.

## <a name="validation-guidelines--most-failed-test-cases"></a>Instrucciones de validación & la mayoría de los casos de prueba con errores

### <a name="9989-general-considerations"></a>Consideraciones generales sobre &#9989;

*Vea también* la [sección 100, general](/legal/marketplace/certification-policies#100-general)

* Asegúrese de que usa la versión 1.4.1 o posterior de [Microsoft Teams SDK](https://www.npmjs.com/package/@microsoft/teams-js).
* No realice cambios en la aplicación mientras el proceso de validación está en curso. Si lo hace, requerirá una revalidación completa de la aplicación.
* La aplicación no debe dejar de responder, finalizar de forma inesperada ni contener errores de programación. Si se produce un problema, la aplicación debe dar error sin problemas y proporcionar un mensaje de dirección válida de reenv? a del usuario.
* La aplicación no debe descargar, instalar ni iniciar automáticamente ningún código ejecutable en el entorno del usuario. Todas las descargas deben buscar permisos explícitos del usuario.
* Cualquier material que asocie a su experiencia, como las descripciones y la documentación de soporte técnico, debe ser preciso. La ortografía, el uso de mayúsculas y minúsculas, la puntuación y la gramática de las descripciones y materiales deben ser correctos.
* Proporcionar información de ayuda y soporte técnico. Se recomienda encarecidamente que la aplicación incluya un vínculo de ayuda/p + f para la experiencia del usuario de primera ejecución. Para todas las aplicaciones personales, le recomendamos que proporcione su página de ayuda como una pestaña personal para una mejor experiencia del usuario.
* Las aplicaciones no deben sacar al usuario de Microsoft Teams para los escenarios de usuario principales. Se recomienda el uso de módulos de tareas o pestañas para mostrar información a los usuarios de Microsoft Teams.
* Aumente el número de versión de la aplicación en el manifiesto si realiza cambios en el manifiesto en el envío.
* La aplicación no debe sacar a los usuarios de Microsoft Teams para los escenarios de usuario principales. Los destinos de vínculo en las aplicaciones no deben vincularse a un explorador externo, pero deben vincularse a los elementos div contenidos en Teams, por ejemplo, dentro de los módulos de tareas y las pestañas.
* Las aplicaciones personales permiten a los usuarios compartir contenido desde una experiencia de la aplicación personal con otros miembros del equipo.

### <a name="9989--provide-a-clear-and-simple-sign-insign-out-and-sign-up-experience"></a>&#9989; proporcionar una experiencia clara y simple de inicio y cierre de sesión y de suscripción

*Consulte también* la [sección 1100,5: control del cliente](/legal/marketplace/certification-policies#11005-customer-control)

* Si la aplicación o el complemento dependen de cuentas o servicios externos, la experiencia de inicio y cierre de sesión y de suscripción deben ser claras y accesibles en todas las funcionalidades de la aplicación.
* Si hay una opción de inicio de sesión explícito proporcionada al usuario, debe haber una opción de cierre de sesión correspondiente (incluso si la aplicación usa la [autenticación silenciosa](../../../../tabs/how-to/authentication/auth-silent-aad.md)).
* La opción de cierre de sesión solo debe firmar al usuario de la capacidad de la aplicación y no del cliente de Teams.
* Como mínimo, la opción de cierre de sesión debe cerrar al usuario de las mismas funciones a las que se tiene acceso con la opción de inicio de sesión. Por ejemplo, si la opción de inicio de sesión incluye una extensión de mensajería y una ficha, la opción de cierre de sesión debe incluir la extensión de mensajería y la ficha.

* Asegúrese de que siempre hay una forma de revertir los comportamientos siguientes (o similares):
  * Sign-in => cerrar sesión.
  * Vincule una cuenta/servicio => desvincule una cuenta o servicio.
  * Conectar una cuenta/servicio => desconectar una cuenta o servicio.
  * Autorice una cuenta/servicio => desautorizar o denegar una cuenta o servicio.
  * Registrar una cuenta/servicio => anular la suscripción a una cuenta o un servicio.
* Si la aplicación requiere una cuenta o servicio, debe proporcionar un método para que el usuario pueda registrarse o crear una solicitud de suscripción. Se puede conceder una excepción si la aplicación requiere una licencia de uso. Pero estos escenarios constituyen un método claro hacia delante para un nuevo registro de usuario que se debe proporcionar.
* Asegúrese de proporcionar a un nuevo usuario orientación para el modo de desplazamientos sobre cómo registrarse para usar los servicios de la aplicación. Si no hay disponible un vínculo de registro listo, es posible que se proporcione un método transparente en las siguientes áreas.

> [!div class="checklist"]
>
> * dentro de las secciones de descripción de la aplicación;
> * en el mensaje de bienvenida de la aplicación;
> * en el mensaje de ayuda de la aplicación;
> * en la ventana en la que se pide a un usuario que inicie sesión en sus servicios;

* Las aplicaciones que no tienen un flujo de inscripción sencillo también pueden incluir una pestaña de ayuda o un vínculo a una página web en la que un usuario nuevo puede ver instrucciones detalladas sobre cómo configurar la aplicación con Microsoft Teams.  Esto es para garantizar que un nuevo usuario no se bloquee al intentar la aplicación por primera vez.
* La funcionalidad de inicio y cierre de sesión debe funcionar en clientes móviles. Asegúrese de que está usando [Microsoft Teams SDK](https://www.npmjs.com/package/@microsoft/teams-js) versión 1.4.1 o posterior.

Para obtener más información acerca de la autenticación, consulte:

* [Documentación de autenticación](../../../authentication/authentication.md)
* [Ejemplo de autenticación de bot en node](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
* [Ejemplo de autenticación de pestaña en node](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Autenticación de Tab/bot en C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

### <a name="9989-response-times-must-be-reasonable"></a>Los tiempos de respuesta &#9989; deben ser razonables

* **Pestañas**. Si una respuesta a una acción tarda más de tres segundos, debe proporcionar un mensaje de carga o advertencia.
* **Bots**. Una respuesta a un comando de usuario debe producirse en dos segundos. Si se requiere un procesamiento más largo, la aplicación debe mostrar un indicador de escritura.
* **Crear extensiones**. Una respuesta a un comando de usuario debe producirse en cinco segundos.

> [!TIP]
> Asegúrese de que la aplicación muestra un indicador de carga o algún tipo de advertencia cuando la aplicación tarda más de lo esperado en responder.

### <a name="9989-tab-content-must-not-have-excessive-chrome-or-layered-navigation"></a>El contenido de la pestaña &#9989; no debe tener un cromo o navegación por capas excesivo

* Las pestañas deben proporcionar contenido centrado y evitar elementos de interfaz de usuario innecesarios. En general, esto suele hacer referencia a una interfaz de usuario anidada o con capas innecesaria, una interfaz de usuario extraña o irrelevante junto al contenido o cualquier vínculo que lleve al usuario al contenido no relacionado. Por ejemplo, a continuación se muestra una vista de pestaña que omite los menús de navegación y que sólo exhibe el contenido principal:

![Vista Web de SharePoint](../../../../assets/images/faq/web-sp.png)  
![Vista de pestañas de SharePoint](../../../../assets/images/faq/tab-sp.png)

* Las pestañas deben ser de poca naturaleza y no incluir una navegación compleja.
* Las pestañas de canal que tienen capacidades de edición complejas en la aplicación deben abrir la vista del editor en una ventana múltiple en lugar de en una pestaña.
* Las pestañas de canal no deben proporcionar una barra de aplicaciones con iconos en el raíl izquierdo que entran en conflicto con la navegación principal de Microsoft Teams.
* Las pestañas no deben presentar una barra de aplicaciones con iconos en el carril de la izquierda que entran en conflicto con la navegación principal de Microsoft Teams.
* Las pestañas que tienen capacidades de edición complejas en la aplicación deben abrir la vista del editor en una ventana múltiple en lugar de en la ficha.
* Si hay varias opciones de vista, considere la posibilidad de tener un menú de configuración de pestaña para que el usuario elija. Por ejemplo, en lugar de insertar un menú dentro de la pestaña, coloque el menú en la página de configuración para que la vista de pestaña real sea despejada y centrada.
* Incluya una pestaña de *ayuda* como una pestaña estática para informar a los usuarios sobre cómo configurar, registrarse y usar la aplicación.
* Incluya una pestaña de *configuración* que esté disponible en el encabezado de la aplicación.

![Página de configuración de la idea ancha](../../../../assets/images/faq/wideidea.png)

### <a name="9989-tab-configuration-must-happen-in-the-configuration-screen"></a>La configuración de la pestaña &#9989; debe ocurrir en la pantalla de configuración

* La pantalla de configuración debe explicar con claridad el valor de la experiencia y cómo configurar la ficha.
* El proceso de configuración siempre debe proporcionar una manera para que los usuarios continúen sin dejar de lado la experiencia del usuario. Por ejemplo, no muestre una tarjeta vacía después de que el usuario haya configurado la pestaña.
* El proceso de inicio de sesión del usuario debe formar parte del proceso de configuración y debe completarse en la interfaz de usuario de la pestaña. Después de que el usuario haya completado la configuración y cargado la pestaña, no es necesario realizar ninguna otra acción.
* No mostrar toda la página web en la ventana emergente de configuración de inicio de sesión.
* Un usuario siempre debe poder finalizar la experiencia de configuración, incluso si no puede encontrar inmediatamente el contenido que busca.
* La experiencia de configuración debe proporcionar opciones para que el usuario pueda buscar su contenido, anclar una dirección URL o crear contenido nuevo si no existe.
* La experiencia de configuración debe permanecer dentro del contexto de Teams. El usuario no debe dejar la experiencia de configuración para crear contenido y, a continuación, volver a Microsoft Teams para anclarlo.
* Use el área de la ventanilla disponible de manera eficaz. No lo desperdicie en usar logotipos grandes en el menú emergente configuración

![OneNote permite a los usuarios pegar un vínculo de OneNote en caso de que no se encuentren notas](../../../../assets/images/faq/tab-onenote-config.png)

![Los usuarios siempre pueden crear un nuevo plan en Planner, en caso de que no exista ninguno.](../../../../assets/images/faq/tab-planner-config.png)

![SharePoint también permite al usuario pegar directamente un vínculo de SharePoint](../../../../assets/images/faq/tab-sp-config.png)

### <a name="9989-bots-must-always-be-responsive-and-fail-gracefully"></a>Los bots de &#9989; deben ser siempre dinámicos y dar error correctamente

El bot debe responder a cualquier comando y no debe ser el usuario que no responde. Estas son algunas sugerencias para ayudar a que su bot responda de manera inteligente a los usuarios:

* **Usar listas de comandos**. Es difícil analizar la entrada del usuario o predecir la intención del usuario. En lugar de dejar que los usuarios adivinen lo que el bot puede hacer, proporcione una lista de comandos que comprenda el bot.

![Lista de comandos de flujo](../../../../assets/images/faq/flow-bot.png)

* **Incluir un comando de ayuda**. Es probable que los usuarios escriban "ayuda" cuando se pierden o cuando el bot no responde como se esperaba. Incluya un comando help que describa cómo se experimentará el valor de la aplicación junto con todos los comandos válidos.

![Comando Flow Help](../../../../assets/images/faq/flow-help.png)

* **Incluir contenido de ayuda o guía cuando se pierde el bot**. Cuando el bot no puede comprender la entrada del usuario, debe sugerir una acción alternativa. Por ejemplo, *"lo siento, no entiendo. Escriba "Help" para obtener más información. "* No responda con un mensaje de error o simplemente *"no entiendo"*. Use esta oportunidad para enseñar a los usuarios.

* **Usar tarjetas adaptables y módulos de tareas para que la respuesta de bot sea clara y accionable** 
 Las [tarjetas adaptables con botones al invocar módulos de tareas](/task-modules-and-cards/task-modules/task-modules-bots) mejoran la experiencia del usuario de bot. Estas tarjetas y botones son más fáciles de usar en un dispositivo móvil, en lugar de que el usuario escriba los comandos. Además, las respuestas de bot no deben ser textuales con texto largo. Los bots deben usar tarjetas adaptables & módulos de tareas en lugar de la interfaz de usuario basada en chats de conversación y las respuestas de texto largas

* **Piense en todos los ámbitos**. Asegúrese de que el bot proporciona las respuestas adecuadas cuando se menciona ( `@*botname*` ) en un canal y en conversaciones personales. Si el bot no proporciona un contexto significativo dentro del ámbito personal o Teams, deshabilite dicho ámbito a través del manifiesto. (Vea el `bots` bloque en la [Referencia del esquema del manifiesto de Microsoft Teams](../../../../resources/schema/manifest-schema.md#bots)).

* **Incluir equipo, chat de grupo o conversación de 1:1**. Las notificaciones de bot deben incluir un equipo, un chat en grupo o una conversación de uno a uno con el contenido relevante para la audiencia.

* **No se insertan datos confidenciales**. Los bots no deben insertar datos confidenciales en un equipo, un chat en grupo o una conversación de 1:1 donde hay una audiencia que no debe poder ver los datos

* **Proporcionar un mensaje de bienvenida**. Bot debe proporcionar un mensaje de bienvenida de FRE que incluya un tutorial interactivo con tarjetas de carrusel o botones "pruébelos" para alentar la contratación.

### <a name="9989-personal-bots-must-always-send-a-welcome-message-on-first-launch"></a>&#9989; bots personales siempre deben enviar un mensaje de bienvenida en el primer inicio

Un mensaje de bienvenida es la mejor forma de establecer el tono de su bot personal/chat. Se trata de la primera interacción que un usuario tiene con el bot. Un buen mensaje de bienvenida puede animar al usuario a seguir explorando la aplicación. Si el mensaje de bienvenida o de introducción es confuso o confuso, los usuarios no verán el valor de la aplicación de forma inmediata y perderán sus intereses.
Consulte la sección siguiente para conocer los requisitos de mensaje de bienvenida.

> [!Note]
> Un mensaje de bienvenida es opcional para un bot de canal.

### <a name="welcome-message-requirements"></a>Requisitos de mensaje de bienvenida

* Incluya una propuesta de valor con el paseo de bienvenida.
* Proporcionar instrucciones sobre la forma de avanzar para usar la aplicación.
* Incluir instrucciones sobre cómo registrarse y configurar la aplicación
* Presente texto fácil de leer y diálogo directo, preferiblemente una tarjeta con un botón de bienvenida que requiere una acción que carga un módulo de tareas.
* Mantener su sencillez y uso con botones y tarjetas: Evite el diálogo de chats de texto largo.
* Incluya tarjetas adaptables y botones para que el mensaje de bienvenida sea más fácil de usar.
* Invocar el mensaje de bienvenida con un ping y no dos o más pings simultáneos.
* Un mensaje de bienvenida solo debe mostrarse al usuario que configuró la aplicación, preferiblemente en un chat personal de 1:1.
* Las aplicaciones personales siempre deben proporcionar un mensaje de bienvenida a un usuario.
* No envíe nunca un chat personal a todos los miembros del equipo, lo que se considera correo no deseado.
* No enviar nunca el mensaje de bienvenida más de una vez. No se permite repetir el mismo mensaje de bienvenida a intervalos regulares y se considera correo no deseado.

#### <a name="avoid-welcome-message-spamming"></a>Evitar el mensaje de bienvenida de correo no deseado

* **Mensaje de canal por bot**. No envíe correo no deseado a los usuarios mediante publicaciones de chats nuevas independientes. Cree una publicación de hilo único con respuestas en el mismo subproceso.
* **Chat personal por bot**. No enviar varios mensajes. Enviar un mensaje con la información completa. No se permite repetir el mismo mensaje de bienvenida a intervalos regulares y se considera correo no deseado.

#### <a name="notification-only-bot-welcome-messages"></a>Mensajes de bienvenida de un bot de solo notificación

Los bots de solo notificación deben enviar un mensaje de bienvenida que incluya un mensaje que indique *"soy un robot de solo notificación y no podrá contestar a sus chats"*.

#### <a name="welcome-messages-in-the-personal-scope"></a>Mensajes de bienvenida en el ámbito personal

* **Haga que el mensaje sea conciso e** informativo.  Lo más probable es que la experiencia del usuario y el conocimiento de la aplicación varíen. Un usuario puede haber usado la aplicación en otra plataforma o no ha sabido nada sobre la aplicación. Desea personalizar el mensaje para todas las audiencias y en un par de frases explicar lo que hace el bot y las formas de interactuar con él. También debe explicar el valor de la aplicación y cómo los usuarios se beneficiarán de su uso.
![Cibercafé y dinning bot](../../../../assets/images/faq/cafe-bot.png)

* **Hacer que el mensaje sea accionable**. Piense lo primero que quiere que realicen los usuarios después de instalar la aplicación. ¿Hay algún comando interesante que deben probar? ¿Hay alguna otra experiencia de incorporación que deba conocer? ¿Es necesario que inicien sesión? Puede Agregar acciones a una tarjeta adaptable o proporcionar ejemplos específicos como *"probar..."*, *"Esto es lo que puedo hacer..."*.

#### <a name="welcome-messages-in-the-teamchannel--scope"></a>Mensajes de bienvenida en el ámbito de equipo o canal

Las cosas son un poco diferentes cuando el bot se agrega por primera vez a un canal. Normalmente, no debería enviar un mensaje de 1:1 a todos los usuarios del equipo, pero el bot puede enviar un mensaje de bienvenida en el canal.

### <a name="9989-mobile-responsiveness-no-direct-upsell-or-payment"></a>&#9989; respuesta móvil, no hay pagos ni ventas directos

* Las pestañas, tarjetas adaptables, mensajes de Bot y contenido de los módulos de tareas deben ser dinámicos para una variedad de tamaños de pantalla para dispositivos móviles.
* Las aplicaciones compatibles con iOS deben ser completamente funcionales en el dispositivo iPad más reciente con la última versión de iOS.
* No debe incluir ninguna referencia directa a las compras desde la aplicación, ofertas de prueba, ofertas para versiones pagadas o vínculos a cualquier tienda en línea en la que los usuarios puedan comprar o adquirir otro contenido, aplicaciones o complementos desde la aplicación de Teams en Mobile OS (Android, iOS).
* La versión de iOS o Android del complemento no debe mostrar ninguna interfaz de usuario ni ningún otro idioma ni vínculo a ninguna otra aplicación, complementos o sitio web que pida al usuario que pague.
* Las páginas de la Directiva de privacidad asociada y las condiciones de uso también deben estar libres de los vínculos de la interfaz de usuario de Commerce o de la tienda.

### <a name="9989-do-not-post-sensitive-data-to-an-audience-not-intended-to-view-the-data"></a>&#9989; no se exponen datos confidenciales a una audiencia que no está pensada para ver los datos

La aplicación de Microsoft Teams no debe exponer datos confidenciales como instrumento de tarjeta de crédito/pago financiero, información de identificación personal (PIN), estado o información de seguimiento de contactos a una audiencia que no está destinada a ver dichos datos.

### <a name="9989-do-not-transmit-financial-payment-details-or-complete-financial-transactions-via-your-teams-app"></a>&#9989; no transmitir detalles de pago financiero o transacciones financieras completas a través de la aplicación de Teams

* La aplicación de Microsoft Teams no debe pedir a los usuarios que realicen un pago directamente en la interfaz de Microsoft Teams
* Es posible que las aplicaciones no transmitan detalles del instrumento financiero a través del usuario en la interfaz de la aplicación. Las aplicaciones solo pueden transmitir vínculos a los servicios de pago seguro a los usuarios si esto se revela en las condiciones de uso, la Directiva de privacidad y cualquier página de perfil o sitio web de la aplicación antes de que un usuario acepte usar la aplicación.

### <a name="9989-clear-warning-before-downloading-any-files-or-executable-exe-into-a-users-environment"></a>&#9989; desactive la advertencia antes de descargar archivos o ejecutables ( `.exe` ) en el entorno de un usuario

Avise a los usuarios antes de que la aplicación descargue archivos o ejecutables ( `.exe`  ) en el entorno o el equipo del usuario.

### <a name="9989-messaging-extensions-should-provide-help-text-and-be-easy-to-read"></a>Las extensiones de mensajería de &#9989; deben proporcionar texto de ayuda y ser fáciles de leer

* La extensión de mensajería basada en búsquedas debe proporcionar texto de ayuda sobre cómo realizar búsquedas con eficacia (por ejemplo, Mostrar entradas de ejemplo).
* Los módulos de tareas deben incluir un icono y un nombre corto en los que estén contenidos o creados desde la aplicación.
* Los ejecutables de extensión de mensajes `@mention` deben ser claros, fáciles de comprender y fáciles de leer.
![Extensión de mensajes](../../../../assets/images/faq/message-extension.png)

> [!div class="nextstepaction"]
> [Obtenga más información sobre las directivas de aprobación de aplicaciones de Teams](/legal/marketplace/certification-policies#1140-teams)
