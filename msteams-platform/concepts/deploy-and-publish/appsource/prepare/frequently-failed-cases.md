---
title: Sugerencias y casos con errores frecuentes
description: Describe las sugerencias para el envío y la mayoría de las directivas con errores
keywords: Preguntas más frecuentes sobre la publicación de equipos errores frecuentes de sugerencia sugerencias
ms.openlocfilehash: ffb472c918a205bdcf921b967269a80fcaa93338
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676048"
---
# <a name="tips-and-frequently-failed-cases"></a>Sugerencias y casos con errores frecuentes 

En este artículo se describen algunos de los motivos más comunes por los que las aplicaciones producen errores de validación. No pretende ser una lista exhaustiva de todos los problemas potenciales de la aplicación. Sin embargo, si sigue esta guía, la probabilidad de que se pase por primera vez aumentará en gran medida. Vea la lista completa de directivas aquí: [directivas de validación de AppSource](https://dev.office.com/officestore/docs/validation-policies). Las directivas de la sección 14 de las directivas de validación generales de AppSource son específicas de las aplicaciones de Microsoft Teams.

## <a name="tips-for-successful-app-submission"></a>Sugerencias para un envío de aplicación correcto

* Asegúrese de que usa la versión 1.4.1 o posterior del SDK de Microsoft Teams.
* No realice cambios en la aplicación mientras la validación está en curso. Esto requerirá que se vuelva a validar completamente la aplicación.
* La aplicación no debe dejar de responder, finalizar de forma inesperada ni contener errores de programación. Si hay un problema, debe producirse un error sin problemas con un mensaje de reenvío de forma válida al usuario.
* La aplicación no debe descargar, instalar ni iniciar automáticamente ningún código ejecutable en el entorno del usuario. Cualquier descarga debe solicitar un permiso explícito del usuario.
* Cualquier material que asocie a su experiencia, como las descripciones y la documentación de soporte técnico, debe ser preciso. La ortografía, el uso de mayúsculas y minúsculas, la puntuación y la gramática de las descripciones y materiales deben ser correctos.
* Ayuda y soporte técnico: es muy recomendable tener el vínculo de ayuda/preguntas más frecuentes de la aplicación de Microsoft Teams y proporcionar este vínculo en la primera ejecución de la experiencia del usuario. Para todas las aplicaciones personales, le recomendamos que proporcione su página de ayuda como una pestaña personal para una mejor experiencia del usuario.

## <a name="policy-112-sign-up-sign-in-and-sign-out"></a>Directiva 11,2: registrarse, iniciar sesión y cerrar sesión

Descripción: las aplicaciones deben proporcionar una experiencia clara y sencilla de inicio y cierre de sesión y (cuando corresponda). La experiencia debe ser accesible en todas las funciones de la aplicación.

* Si hay una opción de inicio de sesión explícito proporcionada al usuario, debe haber una opción de cierre de sesión (incluso si la aplicación usa la autenticación de SSO o silenciosa)
* La opción de cierre de sesión solo debe cerrar la sesión del usuario de la capacidad de la aplicación, y no del cliente de Teams.
* Todos los ámbitos que tienen un inicio de sesión también deben tener un inicio de sesión. Como mínimo, la opción de cierre de sesión debe cerrar al usuario de las mismas funciones en las que la opción de inicio de sesión los firmó. Por ejemplo, si la opción de inicio de sesión firma al usuario en una extensión de mensajería y una ficha, la opción cerrar sesión debe desproteger al usuario de la extensión de mensaje y la ficha.

* Asegúrese de que siempre hay una forma de revertir los comportamientos siguientes (o similares):
  * Sign-in => cierre de sesión
  * Vincular una cuenta/servicio => quitar el vínculo de una cuenta o servicio
  * Conectar una cuenta/servicio => desconectar la cuenta o el servicio
  * Autorizar una cuenta/servicio => de/anular la autorización de la cuenta o el servicio
  * Registrar una cuenta/servicio => cancelar el registro de la cuenta o el servicio
* Si la aplicación requiere una cuenta o servicio, debe proporcionar un método para que el usuario pueda registrarse o solicitar el registro. Se puede buscar una excepción para un proceso de registro si la aplicación se ajusta a la categoría de aplicación "empresa".
* La funcionalidad de inicio y cierre de sesión debe funcionar en clientes móviles. Asegúrese de que ha actualizado el SDK de JavaScript de Teams a la versión 1.4.1 o posterior.

Para obtener más información acerca de la autenticación, consulte:

* [Documentación de autenticación](~/concepts/authentication/authentication.md)
* [Ejemplo de autenticación de bot en node](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
* [Ejemplo de autenticación de pestaña en node](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Autenticación de Tab/bot en C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

## <a name="policy-145-microsoft-teams-apps-must-respond-in-a-reasonable-timeframe"></a>Directiva 14,5: las aplicaciones de Microsoft Teams deben responder en un período de tiempo razonable.

* 14.5.1: para las pestañas, si una respuesta a una acción tarda más de tres segundos, debe proporcionar un mensaje o advertencia de carga.
* 14.5.2: para los bots, debe producirse una respuesta a un comando de usuario en dos segundos. Si se requiere un procesamiento más largo, debe usar un indicador de escritura.
* 14.5.3: para redactar extensiones, debe producirse una respuesta a un comando de usuario en cinco segundos.

> [!TIP]
> Asegúrese de incluir el indicador de carga cuando la aplicación tarda demasiado tiempo.

## <a name="policy-14153-content-in-a-tab-should-not-have-superfluousunnecessary-ui-aka-ui-chrome-or-layered-navigation"></a>Directiva 14.15.3: el contenido de una pestaña no debe tener una interfaz de usuario superflua o innecesaria (aka: cromo de IU) o navegación por capas

Las pestañas deben proporcionar contenido centrado y evitar elementos de la interfaz de usuario que no están relacionados con este contenido. En general, esto suele hacer referencia a una navegación anidada o en capas innecesaria, la interfaz de usuario no relacionada o irrelevante junto al contenido, o cualquier vínculo que lleve al usuario al contenido no relacionado con el contenido de la pestaña. Por ejemplo, SharePoint eliminó los menús de navegación y solo exhiba el contenido principal de la pestaña.

![Vista de pestañas de SharePoint de vista](~/assets/images/faq/web-sp.png)
![Web de SharePoint](~/assets/images/faq/tab-sp.png)

Si hay varias opciones de vista, considere la posibilidad de tener un menú de configuración de pestaña para que el usuario elija. Por ejemplo, en lugar de insertar un menú dentro de la pestaña, las ideas anchas colocan el menú en la página de configuración para que la vista de pestaña real esté limpia y tenga un enfoque.

![Página de configuración de la idea ancha](~/assets/images/faq/wideidea.png)

## <a name="policy-14157-bots-must-respond-to-any-command-and-must-not-dead-end-the-user"></a>Directiva 14.15.7: los bots deben responder a cualquier comando y no deben finalizar el usuario

El bot siempre debe responder. Estas son algunas sugerencias para ayudar a su bot a responder de manera más inteligente a los usuarios.

**Usar la lista de comandos:** La entrada del usuario de análisis o la predicción del usuario es difícil. En lugar de dejar que el usuario Adivine qué puede hacer el bot, proporcione a los usuarios una lista de los comandos que puede entender el bot.

![Lista de comandos de flujo](~/assets/images/faq/flow-bot.png)

**Incluir un comando de ayuda:** Es muy probable que los usuarios escriban "ayuda" cuando se pierden o cuando el bot no responde con lo que esperan. Incluya un comando de ayuda que proporcione su propuesta de valor junto con todos los comandos válidos.

![Comando Flow Help](~/assets/images/faq/flow-help.png)

**Incluir contenido de ayuda o guía cuando se pierde el bot:** Cuando no comprenda los datos proporcionados por el usuario, proporcione al usuario algo que pueda hacer en su lugar. Por ejemplo "lo siento, no entiendo. Escriba "Help" para obtener más información. " No responda con un mensaje de error o simplemente "no entiendo". Use esta oportunidad para enseñar a los usuarios.

**Piense en ambos ámbitos:** Asegúrese de que el bot proporciona las respuestas adecuadas cuando se menciona (@*botname*) en un canal y en las conversaciones personales según sea necesario. Si el bot no proporciona un contexto significativo dentro del ámbito personal o Teams, deshabilite dicho ámbito a través del manifiesto. (Vea el `bots` bloque en la [Referencia del esquema del manifiesto de Microsoft Teams](~/resources/schema/manifest-schema.md#bots)).

## <a name="policy-14159-bot-must-send-welcome-messages-on-the-first-launch"></a>Directiva 14.15.9: bot debe enviar mensajes de bienvenida en el primer inicio

Los mensajes de bienvenida son la mejor forma de establecer el tono. Esta es la primera interacción que el usuario tiene con el bot. Un buen mensaje de bienvenida puede animar al usuario a seguir explorando la aplicación mientras una malato confunda el uso y los usuarios podrían perder sus intereses si no pueden ver inmediatamente el valor de la aplicación.

### <a name="personal-scope"></a>Ámbito personal

En el primer inicio de bot, el usuario debe obtener un mensaje de bienvenida del bot incluso antes de iniciar sesión. Un par de sugerencias que considerar al diseñar el mensaje de bienvenida:

**Haga que el mensaje sea conciso e** informativo: Es posible que los usuarios tengan experiencias y conocimientos muy diferentes sobre la aplicación. Es posible que hayan usado la aplicación en otra plataforma o que no sepan nada sobre la aplicación. Desea personalizar el mensaje para todos los usuarios y en un par de oraciones explicar lo que hace el bot y cómo interactuar con él. También debe explicar el valor de la aplicación y cómo los usuarios se beneficiarán de su uso.
![Cibercafé y dinning bot](~/assets/images/faq/cafe-bot.png)

**Hacer que el mensaje sea accionable:** Piense en qué es lo primero que quiere que hagan los usuarios después de instalar la aplicación. ¿Hay algún comando interesante que deba probar? ¿Hay alguna otra experiencia de incorporación que deba conocer? ¿Es necesario que inicien sesión? Puede Agregar acciones a una tarjeta adaptable o proporcionar ejemplos específicos como "probar...", "Esto es lo que puedo hacer...".

### <a name="team-scope"></a>Ámbito de equipo

Las cosas son un poco diferentes cuando el bot se agrega por primera vez a un canal. Normalmente, no debería enviar un mensaje de 1:1 a todos los usuarios del equipo, pero el bot puede enviar un mensaje de bienvenida en el canal.

## <a name="policy-141510-tab-configuration-ui-should-not-dead-end-the-experience-and-always-provide-a-way-for-a-user-to-continue"></a>Directiva 14.15.10: la interfaz de usuario de configuración de la pestaña no debe dar de alta la experiencia y proporcionar siempre una manera para que un usuario continúe

Un usuario siempre debe poder finalizar la experiencia de configuración, incluso si no puede encontrar inmediatamente el contenido que busca. La experiencia de configuración debe proporcionar al usuario opciones para encontrar su contenido o anclar una dirección URL, o bien crear nuevo contenido si no existe. El usuario no debe dejar la experiencia de configuración para crear contenido y, a continuación, volver a Microsoft Teams para anclarlo.

![OneNote permite a los usuarios pegar un vínculo de OneNote en caso de que no se encuentren notas](~/assets/images/faq/tab-onenote-config.png)

![Los usuarios siempre pueden crear un nuevo plan en Planner, en caso de que no exista ninguno.](~/assets/images/faq/tab-planner-config.png)

![SharePoint también permite al usuario pegar directamente un vínculo de SharePoint](~/assets/images/faq/tab-sp-config.png)