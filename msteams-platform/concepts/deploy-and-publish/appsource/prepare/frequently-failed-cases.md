---
title: Sugerencias de envío de aplicaciones y casos con errores frecuentes
description: Describe sugerencias para un envío correcto de la tienda de Teams y los motivos comunes por los que los envíos fallan.
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: Publicación rápida de appsource de validación de aplicaciones de Teams con la mayoría de los casos de prueba con errores
ms.openlocfilehash: ad1818bbe2f085f5f1dc1bbef5f6a7b7b9ba08af
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014449"
---
# <a name="tips-for-a-successful-microsoft-teams-app-submission"></a>Sugerencias para un envío de aplicación de Microsoft Teams correcto

En este artículo se abordan los motivos comunes por los que las aplicaciones enviadas no pueden validarse. Aunque no está pensado para ser una lista exhaustiva de todos los posibles problemas con la aplicación, seguir esta guía aumentará la probabilidad de que el envío de la aplicación pase la primera vez. *Vea las* [directivas de certificación del mercado](/legal/marketplace/certification-policies) comercial para obtener una amplia lista de directivas de validación.

>[!NOTE]
>**[La sección 1140](/legal/marketplace/certification-policies#1140-teams)** es específica de Microsoft Teams y la **[subsección 1140.4](https://docs.microsoft.com/legal/marketplace/certification-policies#11404-functionality)** aborda los requisitos de funcionalidad para las aplicaciones de Teams.

## <a name="validation-guidelines--most-failed-test-cases"></a>Directrices de validación & casos de prueba con errores

### <a name="9989-general-considerations"></a>&#9989; consideraciones generales

*Vea también la* [sección 100: General](/legal/marketplace/certification-policies#100-general)

* Asegúrese de que está usando la versión 1.4.1 o posterior del [SDK de Microsoft Teams.](https://www.npmjs.com/package/@microsoft/teams-js)
* No realices cambios en la aplicación mientras el proceso de validación esté en curso. Si lo haces, necesitarás una revalidación completa de la aplicación.
* La aplicación no debe dejar de responder, finalizar inesperadamente o contener errores de programación. Si se produce un problema, la aplicación debería producir un error correctamente y proporcionar un mensaje de avance válido al usuario.
* La aplicación no debe descargar, instalar ni iniciar automáticamente ningún código ejecutable en el entorno del usuario. Todas las descargas deben solicitar permiso explícito al usuario.
* Cualquier material que asocie con su experiencia, como descripciones y documentación de soporte técnico, debe ser preciso. La ortografía, el uso de mayúsculas y minúsculas, la puntuación y la gramática de las descripciones y materiales deben ser correctos.
* Proporcionar información de ayuda y soporte técnico. Se recomienda encarecidamente que la aplicación incluya un vínculo de ayuda o preguntas más frecuentes para la experiencia del usuario de primera ejecución. Para todas las aplicaciones personales, te recomendamos que proporciones tu página de ayuda como una pestaña personal para mejorar la experiencia del usuario.
* Las aplicaciones no deben sacar al usuario de Teams para escenarios de usuario principales. Se recomienda usar módulos o pestañas de tareas para mostrar información a los usuarios de Teams.
* Incrementa el número de versión de la aplicación en el manifiesto si realizas cambios en el manifiesto en el envío.
* La aplicación no debe sacar a los usuarios de Teams para escenarios de usuario principales. Los destinos de vínculos de las aplicaciones no deben vincularse a un explorador externo, sino que deben vincularse a elementos div contenidos en Teams, por ejemplo, dentro de módulos de tareas y pestañas.
* Las aplicaciones personales permiten a los usuarios compartir contenido de una experiencia de aplicación personal con otros miembros del equipo.

### <a name="9989--provide-a-clear-and-simple-sign-insign-out-and-sign-up-experience"></a>&#9989; proporcionar una experiencia clara y sencilla de inicio y cerrar sesión y registro

*Vea también la* [sección 1100.5: Control de clientes](/legal/marketplace/certification-policies#11005-customer-control)

* Si la aplicación o el complemento dependen de cuentas o servicios externos, la experiencia de inicio y salida y registro debe ser aparente y accesible en todas las funcionalidades de la aplicación.
* Si se proporciona una opción de inicio de sesión explícita al usuario, debe haber una opción de cerrar sesión correspondiente (incluso si la aplicación usa la autenticación [silenciosa).](../../../../tabs/how-to/authentication/auth-silent-aad.md)
* La opción de cerrar sesión solo debe cerrar la sesión del usuario en la funcionalidad de la aplicación y no en el cliente de Teams.
* Como mínimo, la opción de cerrar sesión debe cerrar la sesión del usuario de las mismas funcionalidades a las que se accede con la opción de inicio de sesión. Por ejemplo, si la opción de inicio de sesión incluye una extensión de mensajería y una pestaña, la opción de cerrar sesión debe incluir tanto la extensión de mensajería como la pestaña.

* Asegúrese de que siempre hay una manera de invertir los siguientes comportamientos (o similares):
  * Inicio de sesión => cerrar sesión.
  * Vincular una cuenta/servicio => desvincular una cuenta o servicio.
  * Conectar una cuenta/servicio => desconectar una cuenta o servicio.
  * Autorizar una cuenta/servicio => autorizar o denegar una cuenta o servicio.
  * Registrar una cuenta/servicio => anular el registro o cancelar la suscripción de una cuenta o servicio.
* Si la aplicación requiere una cuenta o un servicio, debes proporcionar una forma para que el usuario se suscriba o cree una solicitud de registro. Se puede conceder una excepción si la aplicación requiere una licencia para usar. Sin embargo, en estos escenarios, debe proporcionarse un camino claro para un nuevo registro de usuario.
* Asegúrate de proporcionar instrucciones claras a un nuevo usuario sobre cómo registrarte para usar los servicios de aplicaciones. Si un vínculo de registro listo no está disponible, se puede proporcionar una forma clara de avanzar en las siguientes áreas

> [!div class="checklist"]
>
> * dentro de las secciones de descripción de la aplicación;
> * en el mensaje de bienvenida de la aplicación;
> * en el mensaje de ayuda de la aplicación;
> * en la ventana donde se pide a un usuario que inicie sesión en sus servicios;

* Las aplicaciones que no tienen un flujo de registro fácil también pueden incluir una pestaña de ayuda o un vínculo a una página web donde un nuevo usuario puede ver instrucciones detalladas sobre cómo configurar la aplicación con Microsoft Teams.  Esto es para garantizar que un nuevo usuario no se bloquee al probar la aplicación por primera vez.
* La funcionalidad de inicio y salida de sesión debe funcionar en clientes móviles. Asegúrese de que usa la versión 1.4.1 o posterior del SDK de [Microsoft Teams.](https://www.npmjs.com/package/@microsoft/teams-js)

Para obtener información adicional sobre la autenticación, vea:

* [Documentación de autenticación](../../../authentication/authentication.md)
* [Ejemplo de autenticación de bot en Node](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
* [Ejemplo de autenticación de pestañas en Node](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Autenticación de pestaña/bot en C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

### <a name="9989-response-times-must-be-reasonable"></a>&#9989; tiempos de respuesta deben ser razonables

* **Fichas**. Si una respuesta a una acción tarda más de tres segundos, debe proporcionar un mensaje o advertencia de carga.
* **Bots**. Una respuesta a un comando de usuario debe producirse en un plazo de dos segundos. Si se requiere un procesamiento más largo, la aplicación debe mostrar un indicador de escritura.
* **Extensiones de redacción**. Una respuesta a un comando de usuario debe producirse en cinco segundos.

> [!TIP]
> Asegúrate de que la aplicación muestra un indicador de carga o algún tipo de advertencia cuando la aplicación tarda más de lo esperado en responder.

### <a name="9989-tab-content-must-not-have-excessive-chrome-or-layered-navigation"></a>&#9989; contenido de la pestaña no debe tener un cromo excesivo o una navegación en capas

* Las pestañas deben proporcionar contenido centrado y evitar los elementos de interfaz de usuario necesarios. En general, esto suele hacer referencia a la navegación anidada o en capas innecesaria, una interfaz de usuario irrelevante o innecesaria junto al contenido o cualquier vínculo que lleve al usuario a contenido no relacionado. Por ejemplo, a continuación se muestra una vista de pestaña que omite los menús de navegación y solo muestra el contenido principal:

![Vista web de SharePoint](../../../../assets/images/faq/web-sp.png)  
![Vista de pestaña de SharePoint](../../../../assets/images/faq/tab-sp.png)

* Las pestañas deben ser ligeras y no incluir navegación compleja.
* Las pestañas de canal que tienen funciones de edición complejas dentro de la aplicación deben abrir la vista de editor en una ventana múltiple en lugar de una pestaña.
* Las pestañas de canal no deben proporcionar una barra de aplicaciones con iconos en la barra izquierda que entre en conflicto con la navegación principal de Teams.
* Las pestañas no deben presentar una barra de aplicaciones con iconos en la barra izquierda que entren en conflicto con la navegación principal de Teams.
* Las pestañas que tienen funciones de edición complejas dentro de la aplicación deben abrir la vista de editor en una ventana múltiple en lugar de en la pestaña.
* Si hay varias opciones de vista, considere la posibilidad de tener un menú de configuración de pestaña para que el usuario pueda elegir. Por ejemplo, en lugar de insertar un menú dentro de la pestaña, coloque el menú en la página de configuración para que la vista de pestaña real esté limpia y centrada.
* Incluya una pestaña *de* Ayuda como una pestaña estática para informar a los usuarios sobre cómo configurar, registrarse y usar la aplicación.
* Incluya una pestaña *Configuración* que esté disponible desde el encabezado de la aplicación.

![Página de configuración de idea ancha](../../../../assets/images/faq/wideidea.png)

### <a name="9989-tab-configuration-must-happen-in-the-configuration-screen"></a>&#9989; configuración de la pestaña debe producirse en la pantalla de configuración

* La pantalla de configuración debe explicar claramente el valor de la experiencia y cómo configurar la pestaña.
* El proceso de configuración siempre debe proporcionar una forma de que los usuarios continúen sin dejar de usar la experiencia del usuario. Por ejemplo, no mostrar un tablero vacío después de que el usuario haya configurado la pestaña
* El proceso de inicio de sesión del usuario debe formar parte del proceso de configuración y debe completarse en la interfaz de usuario de la pestaña. Cuando el usuario haya completado la configuración y cargado la pestaña, no será necesario realizar ninguna otra acción.
* No muestre toda la página web en la ventana emergente de configuración de inicio de sesión.
* Un usuario siempre debe poder finalizar la experiencia de configuración, incluso si no puede encontrar inmediatamente el contenido que está buscando.
* La experiencia de configuración debe proporcionar opciones para que el usuario encuentre su contenido, anclar una dirección URL o cree contenido nuevo si no existe.
* La experiencia de configuración debe permanecer en el contexto de Teams. El usuario no debe tener que dejar la experiencia de configuración para crear contenido y, a continuación, volver a Teams para anclarlo.
* Usa el área de ventanilla disponible de forma eficaz. No desaperdes al usar logotipos enormes dentro de la ventana emergente de configuración

![OneNote permite a los usuarios pegar un vínculo de OneNote en caso de que no se puedan encontrar notas](../../../../assets/images/faq/tab-onenote-config.png)

![Los usuarios siempre pueden crear un plan nuevo en planner en caso de que no haya ninguno existente](../../../../assets/images/faq/tab-planner-config.png)

![SharePoint también permite al usuario pegar directamente un vínculo de SharePoint](../../../../assets/images/faq/tab-sp-config.png)

### <a name="9989-bots-must-always-be-responsive-and-fail-gracefully"></a>&#9989; bots deben ser siempre dinámicos y producir errores correctamente

El bot debe responder a cualquier comando y no al usuario. Estas son algunas sugerencias para ayudar al bot a responder de forma inteligente a los usuarios:

* **Use listas de comandos.** El análisis de la entrada del usuario o la previsión de la intención del usuario es difícil. En lugar de permitir a los usuarios adivinar lo que puede hacer el bot, proporcione una lista de los comandos que el bot entiende.

![Lista de comandos de flujo](../../../../assets/images/faq/flow-bot.png)

* **Incluya un comando de ayuda.** Es probable que los usuarios escriban "Ayuda" cuando se pierden o cuando el bot no responde según lo esperado. Incluye un comando de ayuda que describa cómo se experimentará el valor de la aplicación junto con todos los comandos válidos.

![Comando de ayuda de flujo](../../../../assets/images/faq/flow-help.png)

* **Incluya contenido de ayuda o instrucciones cuando se pierda el bot.** Cuando el bot no puede comprender la entrada del usuario, debe sugerir una acción alternativa. Por ejemplo, *"Lo sentimos, no lo sé. Escriba "ayuda" para obtener más información".* No responda con un mensaje de error o *simplemente, "No lo entenderé".* Use esta oportunidad para enseñar a los usuarios.

* **Usar tarjetas adaptables y módulos de tareas para que la respuesta del bot sea clara y fácil de usar** 
 [Las tarjetas adaptables con botones que invocan módulos de tareas](/task-modules-and-cards/task-modules/task-modules-bots) mejoran la experiencia del usuario del bot. Estas tarjetas y botones son más fáciles de usar en un dispositivo móvil en lugar de que el usuario escriba los comandos. Además, las respuestas del bot no deben ser textuales con texto largo. Los bots deben usar tarjetas adaptables & módulos de tareas en lugar de interfaz de usuario basada en chat conversacional y respuestas de texto largas

* **Piense en todos los ámbitos.** Asegúrese de que el bot proporciona las respuestas adecuadas cuando se menciona ( ) en `@*botname*` un canal y en conversaciones personales. Si el bot no proporciona contexto significativo dentro del ámbito personal o de equipos, deshabilite dicho ámbito a través del manifiesto. (Vea el bloque en la referencia del esquema de `bots` [manifiesto de Microsoft Teams).](../../../../resources/schema/manifest-schema.md#bots)

* **Incluir el equipo, el chat en grupo o la conversación 1:1**. Las notificaciones de bot deben incluir un equipo, un chat en grupo o una conversación uno a uno con contenido relevante para su audiencia.

* **No insertar datos confidenciales.** Los bots no deben insertar datos confidenciales en un equipo, un chat en grupo o una conversación 1:1 en la que haya una audiencia que no pueda ver los datos

* **Proporcione un mensaje de bienvenida.** El bot debe proporcionar un mensaje de bienvenida de FRE que incluya un tutorial interactivo con tarjetas de carrusel o botones de "pruébalo", para fomentar la participación.

### <a name="9989-personal-bots-must-always-send-a-welcome-message-on-first-launch"></a>&#9989; bots personales deben enviar siempre un mensaje de bienvenida en el primer inicio

Un mensaje de bienvenida es la mejor manera de establecer el tono de su bot personal o de chat. Esta es la primera interacción que un usuario tiene con el bot. Un buen mensaje de bienvenida puede animar al usuario a seguir explorando la aplicación. Si el mensaje de bienvenida o introductorio es confuso o no está claro, los usuarios no verán el valor de la aplicación inmediatamente y perderán intereses.
Consulte la sección siguiente para ver los requisitos de los mensajes de bienvenida.

> [!Note]
> Un mensaje de bienvenida es opcional para un bot de canal.

### <a name="welcome-message-requirements"></a>Requisitos de mensaje de bienvenida

* Incluye una propuesta de valor con el paseo de bienvenida.
* Proporcionar instrucciones para el uso de la aplicación.
* Incluir instrucciones sobre cómo registrarse y configurar la aplicación
* Presenta texto fácil de leer y diálogo sencillo, preferiblemente una tarjeta con un botón de bienvenida que puede actuar y que carga un módulo de tareas.
* Mantenlo sencillo y fácil de usar con botones y tarjetas: evita el texto largo, el diálogo con chats.
* Incluye botones y tarjetas adaptables para que el mensaje de bienvenida sea más utilizable.
* Invoque el mensaje de bienvenida con un ping, no con dos o más pings simultáneos.
* Un mensaje de bienvenida solo debe mostrarse al usuario que configuró la aplicación, preferiblemente en un chat personal 1:1.
* Las aplicaciones personales siempre deben proporcionar un mensaje de bienvenida a un usuario.
* No envíe nunca un chat personal a todos los miembros del equipo, lo que se considera correo no deseado.
* No envíe nunca el mensaje de bienvenida más de una vez. No se permite repetir el mismo mensaje de bienvenida en intervalos regulares y se considera correo no deseado.

#### <a name="avoid-welcome-message-spamming"></a>Evitar el correo no deseado de mensajes de bienvenida

* **Mensaje de canal por bot**. No enviar correo no deseado a los usuarios mediante la creación de nuevas publicaciones de chat independientes. Cree una publicación de subproceso único con respuestas en el mismo hilo.
* **Chat personal por bot.** No envíes varios mensajes. Envíe un mensaje con información completa. No se permite repetir el mismo mensaje de bienvenida en intervalos regulares y se considera correo no deseado.

#### <a name="notification-only-bot-welcome-messages"></a>Mensajes de bienvenida del bot de solo notificación

Los bots de solo notificación deben enviar un mensaje de bienvenida que incluya un mensaje que transmita: "Soy un bot de solo notificación y no podrá responder *a los chats".*

#### <a name="welcome-messages-in-the-personal-scope"></a>Mensajes de bienvenida en el ámbito personal

* **Haga que el mensaje sea conciso e informativo.**  Lo más probable es que la experiencia del usuario y el conocimiento de la aplicación variarán. Un usuario puede haber usado la aplicación en otra plataforma o no saber nada sobre la aplicación. Quiere adaptar el mensaje a todas las audiencias y en un par de frases explicar lo que hace el bot y las formas de interactuar con él. También debes explicar el valor de la aplicación y cómo los usuarios se beneficiarán de su uso.
![Bot de café y dinning](../../../../assets/images/faq/cafe-bot.png)

* **Haga que el mensaje sea que se puede realizar una acción.** Piensa en lo primero que quieres que hagan los usuarios después de instalar la aplicación. ¿Hay un comando interesante que deberían probar? ¿Hay otra experiencia de incorporación que deban conocer? ¿Necesitan iniciar sesión? Puede agregar acciones en una tarjeta adaptable o proporcionar ejemplos específicos como *"Intente preguntar...",*"Esto es *lo que puedo hacer...".*

#### <a name="welcome-messages-in-the-teamchannel--scope"></a>Mensajes de bienvenida en el ámbito de equipo o canal

Las cosas son un poco diferentes cuando el bot se agrega por primera vez a un canal. Normalmente, no debe enviar un mensaje de 1:1 a todos los miembros del equipo, pero el bot puede enviar un mensaje de bienvenida en el canal.

### <a name="9989-mobile-responsiveness-no-direct-upsell-or-payment"></a>&#9989; capacidad de respuesta móvil, sin ventas directas ni pagos

* Las pestañas, las tarjetas adaptables, los mensajes de bot y el contenido de los módulos de tareas deben tener capacidad de respuesta para una variedad de tamaños de pantallas de dispositivos móviles.
* Las aplicaciones que admiten iOS deben funcionar completamente en el dispositivo iPad más reciente con la versión más reciente de iOS.
* No debe incluir referencias directas a compras desde la aplicación, ofertas de prueba, ofertas para versiones de pago o vínculos a ninguna tienda en línea donde los usuarios puedan comprar o adquirir otro contenido, aplicaciones o complementos desde su aplicación de Teams en el sistema operativo móvil (Android, iOS).
* La versión de iOS o Android del complemento no debe mostrar ninguna interfaz de usuario o idioma ni vínculo a ninguna otra aplicación, complemento o sitio web que pida al usuario que pague.
* La directiva de privacidad asociada y las páginas de términos de uso también deben estar libres de cualquier interfaz de usuario comercial o vínculos a la Tienda.

### <a name="9989-do-not-post-sensitive-data-to-an-audience-not-intended-to-view-the-data"></a>&#9989; no publicar datos confidenciales en una audiencia que no está pensada para ver los datos

La aplicación de Teams no debe publicar datos confidenciales como tarjeta de crédito o instrumento de pago financiero, información de identificación personal (PIN), estado o información de seguimiento de contactos a una audiencia que no está pensada para ver esos datos.

### <a name="9989-do-not-transmit-financial-payment-details-or-complete-financial-transactions-via-your-teams-app"></a>&#9989; no transmitir detalles de pagos financieros ni completar transacciones financieras a través de su aplicación de Teams

* La aplicación de Teams no debe pedir a los usuarios que realicen un pago directamente en la interfaz de Teams
* Es posible que las aplicaciones no transmitan detalles del instrumento financiero a través del usuario en la interfaz de la aplicación. Las aplicaciones solo pueden transmitir vínculos a servicios de pago seguros a los usuarios si esto se revela en los Términos de uso, la Directiva de privacidad y cualquier página de perfil o sitio web de la aplicación antes de que un usuario acepte usar la aplicación.

### <a name="9989-clear-warning-before-downloading-any-files-or-executable-exe-into-a-users-environment"></a>&#9989; borrar la advertencia antes de descargar cualquier archivo o ejecutable ( `.exe` ) en el entorno de un usuario

Advierto a los usuarios antes de que la aplicación descargue archivos o archivos ejecutables ( )en el equipo o el entorno `.exe`  del usuario.

### <a name="9989-messaging-extensions-should-provide-help-text-and-be-easy-to-read"></a>&#9989; extensiones de mensajería deben proporcionar texto de ayuda y ser fáciles de leer

* La extensión de mensajería basada en búsquedas debe proporcionar texto de ayuda sobre cómo realizar búsquedas de forma eficaz (por ejemplo, mostrar una entrada de ejemplo).
* Los módulos de tareas deben incluir un icono y un nombre corto que estén contenidos o creados desde la aplicación.
* Los archivos ejecutables de extensión de mensaje deben ser `@mention` claros, fáciles de entender y fáciles de leer.
![Extensión de mensaje](../../../../assets/images/faq/message-extension.png)

## <a name="m365-publisher-attestation"></a>Atestación de M365 Publisher

### <a name="9989-complete-the-publisher-attestation-in-partner-center"></a>&#9989; completar la atestación del editor en el Centro de partners

* Consulte la documentación [del programa de atestación completa de](/microsoft-365-app-certification/docs/attestation) Publisher para obtener más información.
* Siga los pasos de la sección Flujo de [trabajo de atestación](/microsoft-365-app-certification/docs/userguide#3publisher-attestation-workflow) de editor para completar el proceso de atestación del editor. Escribe en appcert@microsoft.com para cualquier pregunta.
* Consulte la guía [de solución de problemas](/azure/active-directory/develop/troubleshoot-publisher-verification) para obtener información adicional.
* Completa la autoaestación a través del Centro de partners. Rellene el cuestionario Self-Assessment en **Cumplimiento de la aplicación.**

> [!div class="nextstepaction"]
> [Más información sobre las directivas de aprobación de aplicaciones de Teams](/legal/marketplace/certification-policies#1140-teams)
