---
title: Sugerencias y casos con errores frecuentes
description: Describe las sugerencias para el envío y la mayoría de las directivas con errores
author: laujan
ms.author: lajanuar
ms.topic: how to
keywords: Validación de las aplicaciones de Teams más errores de prueba de AppSource de aprobación rápida publicar
ms.openlocfilehash: a838d34cabd99ee5d892517c13efc4b91dbd059d
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796340"
---
# <a name="tips-for-a-successful-app-submission"></a>Sugerencias para un envío de aplicación correcto

En este artículo se tratan los motivos comunes de error de validación de aplicaciones enviadas. Aunque no se trata de ser una lista exhaustiva de todos los problemas potenciales de la aplicación, si se sigue esta guía, aumentará la probabilidad de que el envío de la aplicación pase la primera vez. *Vea* [directivas de certificación de mercado comercial](/legal/marketplace/certification-policies) para obtener una lista completa de las directivas de validación.

>[!NOTE]
>La **[sección 1140](/legal/marketplace/certification-policies#1140-teams)** es específica para Microsoft Teams y **[sub-Section 1140,4](https://docs.microsoft.com/legal/marketplace/certification-policies#11404-functionality)** requisitos de funcionalidad para las aplicaciones de Teams.

## <a name="validation-guidelines"></a>Instrucciones de validación

### <a name="9989-general-considerations"></a>Consideraciones generales sobre &#9989;

*Vea también* la [sección 100, general](/legal/marketplace/certification-policies#100-general)

* Asegúrese de que usa la versión 1.4.1 o posterior de [Microsoft Teams SDK](https://www.npmjs.com/package/@microsoft/teams-js).
* No realice cambios en la aplicación mientras el proceso de validación está en curso. Si lo hace, requerirá una revalidación completa de la aplicación.
* La aplicación no debe dejar de responder, finalizar de forma inesperada ni contener errores de programación. Si se produce un problema, la aplicación debe dar error sin problemas y proporcionar un mensaje de dirección válida de reenv? a del usuario.
* La aplicación no debe descargar, instalar ni iniciar automáticamente ningún código ejecutable en el entorno del usuario. Todas las descargas deben buscar permisos explícitos del usuario.
* Cualquier material que asocie a su experiencia, como las descripciones y la documentación de soporte técnico, debe ser preciso. La ortografía, el uso de mayúsculas y minúsculas, la puntuación y la gramática de las descripciones y materiales deben ser correctos.
* Proporcionar información de ayuda y soporte técnico. Se recomienda encarecidamente que la aplicación incluya un vínculo de ayuda/p + f para la experiencia del usuario de primera ejecución. Para todas las aplicaciones personales, le recomendamos que proporcione su página de ayuda como una pestaña personal para una mejor experiencia del usuario.
* Aumente el número de versión de la aplicación en el manifiesto si realiza cambios en el manifiesto en el envío.

### <a name="9989--provide-a-clear-and-simple-sign-insign-out-and-sign-up-experience"></a>&#9989; proporcionar una experiencia clara y simple de inicio y cierre de sesión y de suscripción

*Consulte también* la [sección 1100,5: control del cliente](/legal/marketplace/certification-policies#11005-customer-control)

* Si la aplicación o el complemento dependen de cuentas o servicios externos, la experiencia de inicio y cierre de sesión y de suscripción deben ser claras y accesibles en todas las funcionalidades de la aplicación.
* Si hay una opción de inicio de sesión explícito proporcionada al usuario, debe haber una opción de cierre de sesión correspondiente (incluso si la aplicación usa la autenticación de SSO o[silencio](~/tabs/how-to/authentication/auth-silent-aad.md)).
* La opción de cierre de sesión solo debe firmar al usuario de la capacidad de la aplicación y no del cliente de Teams.
* Como mínimo, la opción de cierre de sesión debe cerrar al usuario de las mismas funciones a las que se tiene acceso con la opción de inicio de sesión. Por ejemplo, si la opción de inicio de sesión incluye una extensión de mensajería y una ficha, la opción de cierre de sesión debe incluir la extensión de mensajería y la ficha.

* Asegúrese de que siempre hay una forma de revertir los comportamientos siguientes (o similares):
  * Sign-in => cerrar sesión.
  * Vincule una cuenta/servicio => desvincule una cuenta o servicio.
  * Conectar una cuenta/servicio => desconectar una cuenta o servicio.
  * Autorice una cuenta/servicio => desautorizar o denegar una cuenta o servicio.
  * Registrar una cuenta/servicio => anular la suscripción a una cuenta o un servicio.
* Si la aplicación requiere una cuenta o servicio, debe proporcionar un método para que el usuario pueda registrarse o crear una solicitud de suscripción. Se puede conceder una excepción si la aplicación es una aplicación de empresa.
* La funcionalidad de inicio y cierre de sesión debe funcionar en clientes móviles. Asegúrese de que está usando [Microsoft Teams SDK](https://www.npmjs.com/package/@microsoft/teams-js) versión 1.4.1 o posterior.

Para obtener más información acerca de la autenticación, consulte:

* [Documentación de autenticación](../../../authentication/authentication.md)
* [Ejemplo de autenticación de bot en node](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
* [Ejemplo de autenticación de pestaña en node](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Autenticación de Tab/bot en C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

### <a name="9989-response-times-must-be-reasonable"></a>Los tiempos de respuesta &#9989; deben ser razonables

* **Pestañas** . Si una respuesta a una acción tarda más de tres segundos, debe proporcionar un mensaje de carga o advertencia.
* **Bots** . Una respuesta a un comando de usuario debe producirse en dos segundos. Si se requiere un procesamiento más largo, la aplicación debe mostrar un indicador de escritura.
* **Crear extensiones** . Una respuesta a un comando de usuario debe producirse en cinco segundos.

> [!TIP]
> Asegúrese de que la aplicación muestra un indicador de carga o algún tipo de advertencia cuando la aplicación tarda más de lo esperado en responder.

### <a name="9989-tab-content-should-not-have-excessive-chrome-or-layered-navigation"></a>El contenido de la pestaña &#9989; no debe tener un cromo excesivo o la navegación por capas

* Las pestañas deben proporcionar contenido centrado y evitar elementos de interfaz de usuario innecesarios. En general, esto suele hacer referencia a una interfaz de usuario anidada o con capas innecesaria, una interfaz de usuario extraña o irrelevante junto al contenido o cualquier vínculo que lleve al usuario al contenido no relacionado. Por ejemplo, a continuación se muestra una vista de pestaña que omite los menús de navegación y que sólo exhibe el contenido principal:

![Vista Web de SharePoint](~/assets/images/faq/web-sp.png)  
![Vista de pestañas de SharePoint](~/assets/images/faq/tab-sp.png)

* Las pestañas deben ser de poca naturaleza y no incluir una navegación compleja.
* Las pestañas no deben presentar una barra de aplicaciones con iconos en el carril de la izquierda que entran en conflicto con la navegación principal de Microsoft Teams.
* Las pestañas que tienen capacidades de edición complejas en la aplicación deben abrir la vista del editor en varias ventanas en lugar de en la ficha.
* Si hay varias opciones de vista, considere la posibilidad de tener un menú de configuración de pestaña para que el usuario elija. Por ejemplo, en lugar de insertar un menú dentro de la pestaña, coloque el menú en la página de configuración para que la vista de pestaña real sea despejada y centrada.

![Página de configuración de la idea ancha](~/assets/images/faq/wideidea.png)

### <a name="9989-tab-configuration-must-happen-in-the-configuration-screen"></a>La configuración de la pestaña &#9989; debe ocurrir en la pantalla de configuración

* La pantalla de configuración debe explicar con claridad el valor de la experiencia y cómo configurar la ficha.
* El proceso de configuración siempre debe proporcionar una manera para que los usuarios continúen sin dejar de lado la experiencia del usuario. Por ejemplo, no muestre una tarjeta vacía después de que el usuario haya configurado la pestaña.
* El proceso de inicio de sesión del usuario debe formar parte del proceso de configuración y debe completarse en la interfaz de usuario de la pestaña. Después de que el usuario haya completado la configuración y cargado la pestaña, no es necesario realizar ninguna otra acción.
* No mostrar toda la página web en la ventana emergente de configuración de inicio de sesión.
* Un usuario siempre debe poder finalizar la experiencia de configuración, incluso si no puede encontrar inmediatamente el contenido que busca.
* La experiencia de configuración debe proporcionar opciones para que el usuario pueda buscar su contenido, anclar una dirección URL o crear contenido nuevo si no existe.
* La experiencia de configuración debe permanecer dentro del contexto de Teams. El usuario no debe dejar la experiencia de configuración para crear contenido y, a continuación, volver a Microsoft Teams para anclarlo.
* Use el área de la ventanilla disponible de manera eficaz. No lo desperdicie en usar logotipos grandes en el menú emergente configuración

![OneNote permite a los usuarios pegar un vínculo de OneNote en caso de que no se encuentren notas](~/assets/images/faq/tab-onenote-config.png)

![Los usuarios siempre pueden crear un nuevo plan en Planner, en caso de que no exista ninguno.](~/assets/images/faq/tab-planner-config.png)

![SharePoint también permite al usuario pegar directamente un vínculo de SharePoint](~/assets/images/faq/tab-sp-config.png)

### <a name="9989-bots-must-always-be-responsive-and-fail-gracefully"></a>Los bots de &#9989; deben ser siempre dinámicos y dar error correctamente

El bot debe responder a cualquier comando y no debe ser el usuario que no responde. Estas son algunas sugerencias para ayudar a que su bot responda de manera inteligente a los usuarios:

* **Usar listas de comandos** . Es difícil analizar la entrada del usuario o predecir la intención del usuario. En lugar de dejar que los usuarios adivinen lo que el bot puede hacer, proporcione una lista de comandos que comprenda el bot.

![Lista de comandos de flujo](~/assets/images/faq/flow-bot.png)

* **Incluir un comando de ayuda** . Es probable que los usuarios escriban "ayuda" cuando se pierden o cuando el bot no responde como se esperaba. Incluya un comando help que describa cómo se experimentará el valor de la aplicación junto con todos los comandos válidos.

![Comando Flow Help](~/assets/images/faq/flow-help.png)

* **Incluir contenido de ayuda o guía cuando se pierde el bot** . Cuando el bot no puede comprender la entrada del usuario, debe sugerir una acción alternativa. Por ejemplo, *"lo siento, no entiendo. Escriba "Help" para obtener más información. "* No responda con un mensaje de error o simplemente *"no entiendo"* . Use esta oportunidad para enseñar a los usuarios.

* **Usar tarjetas adaptables y módulos de tareas para que la respuesta de bot sea clara y accionable** 
 Las [tarjetas adaptables con botones al invocar módulos de tareas](/task-modules-and-cards/task-modules/task-modules-bots) mejoran la experiencia del usuario de bot. Estas tarjetas y botones son más fáciles de usar en un dispositivo móvil en lugar de que el usuario escriba los comandos

* **Piense en todos los ámbitos** . Asegúrese de que el bot proporciona las respuestas adecuadas cuando se menciona ( `@*botname*` ) en un canal y en conversaciones personales. Si el bot no proporciona un contexto significativo dentro del ámbito personal o Teams, deshabilite dicho ámbito a través del manifiesto. (Vea el `bots` bloque en la [Referencia del esquema del manifiesto de Microsoft Teams](~/resources/schema/manifest-schema.md#bots)).

### <a name="9989-personal-bots-must-send-a-welcome-message-on-first-launch"></a>&#9989; bots personales deben enviar un mensaje de bienvenida en el primer inicio

Un mensaje de bienvenida es la mejor forma de establecer el tono de su bot personal/chat. Se trata de la primera interacción que un usuario tiene con el bot. Un buen mensaje de bienvenida puede animar al usuario a seguir explorando la aplicación. Si el mensaje de bienvenida o de introducción es confuso o confuso, los usuarios no verán el valor de la aplicación de forma inmediata y perderán sus intereses.

> [!Note]
> Un mensaje de bienvenida es opcional para un bot de canal.

### <a name="welcome-message-requirements"></a>Requisitos de mensaje de bienvenida

* Incluya una propuesta de valor con el paseo de bienvenida.
* Proporcionar instrucciones de avance para usar el bot.
* Presente texto fácil de leer y diálogo directo, preferiblemente una tarjeta con un botón de bienvenida que requiere una acción que carga un módulo de tareas.
* Manténgase sencillo, evite el diálogo de palabras/chats.
* Incluya tarjetas adaptables y botones para que el mensaje de bienvenida sea más fácil de usar.
* Invocar el mensaje de bienvenida con un ping y no dos o más pings simultáneos.
* Un mensaje de bienvenida solo debe mostrarse al usuario que configuró la aplicación, preferiblemente en un chat personal de 1:1.
* No envíe nunca un chat personal a todos los miembros del equipo.
* No enviar nunca el mensaje de bienvenida más de una vez. No se permite repetir el mismo mensaje de bienvenida a intervalos regulares y se considera correo no deseado.

#### <a name="avoid-welcome-message-spamming"></a>Evitar el mensaje de bienvenida de correo no deseado

* **Mensaje de canal por bot** . No envíe correo no deseado a los usuarios mediante publicaciones de chats nuevas independientes. Cree una publicación de hilo único con respuestas en el mismo subproceso.
* **Chat personal por bot** . No enviar varios mensajes. Enviar un mensaje con la información completa.

#### <a name="notification-only-bot-welcome-messages"></a>Mensajes de bienvenida de un bot de solo notificación

Los bots de solo notificación deben enviar un mensaje de bienvenida que incluya un mensaje que indique *"soy un robot de solo notificación y no podrá contestar a sus chats"* .

#### <a name="welcome-messages-in-the-personal-scope"></a>Mensajes de bienvenida en el ámbito personal

* **Haga que el mensaje sea conciso e** informativo.  Lo más probable es que la experiencia del usuario y el conocimiento de la aplicación varíen. Un usuario puede haber usado la aplicación en otra plataforma o no ha sabido nada sobre la aplicación. Desea personalizar el mensaje para todas las audiencias y en un par de frases explicar lo que hace el bot y las formas de interactuar con él. También debe explicar el valor de la aplicación y cómo los usuarios se beneficiarán de su uso.
![Cibercafé y dinning bot](~/assets/images/faq/cafe-bot.png)

* **Hacer que el mensaje sea accionable** . Piense lo primero que quiere que realicen los usuarios después de instalar la aplicación. ¿Hay algún comando interesante que deben probar? ¿Hay alguna otra experiencia de incorporación que deba conocer? ¿Es necesario que inicien sesión? Puede Agregar acciones a una tarjeta adaptable o proporcionar ejemplos específicos como *"probar..."* , *"Esto es lo que puedo hacer..."* .

#### <a name="welcome-messages-in-the-teamchannel--scope"></a>Mensajes de bienvenida en el ámbito de equipo o canal

Las cosas son un poco diferentes cuando el bot se agrega por primera vez a un canal. Normalmente, no debería enviar un mensaje de 1:1 a todos los usuarios del equipo, pero el bot puede enviar un mensaje de bienvenida en el canal.

> [!div class="nextstepaction"]
> [Obtenga más información sobre las directivas de aprobación de aplicaciones de Teams](/legal/marketplace/certification-policies#1140-teams) 
