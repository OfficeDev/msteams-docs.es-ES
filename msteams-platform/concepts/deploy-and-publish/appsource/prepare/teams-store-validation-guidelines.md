---
title: Microsoft Teams de validación del almacén
description: Describe las directrices que deben seguir todas las aplicaciones enviadas a Teams store (AppSource).
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 79cdc032ee1e7479f7737e5dc71f8f01bb024da8
ms.sourcegitcommit: 25539046d408c4270b988fd826d7cf1275f4b9dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2021
ms.locfileid: "52763118"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams de validación del almacén

Seguir estas directrices aumenta la probabilidad de que la aplicación pase el proceso Microsoft Teams envío de la tienda. Estas Teams específicas complementan las directivas de certificación del mercado comercial de [Microsoft](/legal/marketplace/certification-policies) y se actualizan con frecuencia para reflejar nuevas capacidades, comentarios de los usuarios y cambios en las reglas de negocio.

> [!NOTE]
> Es posible que algunas directrices no sean aplicables a la aplicación. Por ejemplo, si la aplicación no incluye un bot, puedes omitir las directrices relacionadas con el bot.

## <a name="value-proposition"></a>Propuesta de valor

### <a name="app-name"></a>Nombre de la aplicación

El nombre de una aplicación desempeña un papel fundamental en la forma en que los usuarios lo descubren en la tienda. Recuerde lo siguiente acerca de los nombres de aplicaciones:

* El nombre debe incluir términos relevantes para los usuarios.
* Los nombres de las Teams principales&#8212;como **Chat**, **Contactos** , **Calendario**, Llamadas , **Archivos** **,** Actividad , **Teams,** Aplicaciones y Ayuda **&#8212;** no deben incluirse en el nombre de la aplicación. 
* Los nombres comunes deben tener un prefijo o sufijo con el nombre del desarrollador (por ejemplo, Tareas de **Contoso** en lugar de **Tareas**).
* No debe usar **Teams** nombres de productos de Microsoft que puedan indicar falsamente la co-marca o la coventa. (Para obtener más información acerca de la referencia a software, productos y servicios de Microsoft, vea las Directrices de marca [y marca de Microsoft](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)).
* Si la aplicación forma parte de una asociación oficial con Microsoft, el nombre de la aplicación debe ser el primero (por ejemplo, **Contoso Connector para Microsoft Teams**).
* No debe copiar el nombre de una aplicación que aparece en la tienda u otra oferta en el mercado comercial.
* No debe contener términos profanos o despectivos. El nombre tampoco debe incluir un lenguaje racial o culturalmente insensible.
* Debe ser único. Por ejemplo, no puedes enumerar varias aplicaciones para distintas regiones con el mismo nombre y funcionalidad.

### <a name="suitable-for-workplace-consumption"></a>Adecuado para el consumo en el lugar de trabajo

El contenido de la aplicación debe ser adecuado para el consumo general del lugar de trabajo y cumplir todas las restricciones enumeradas en las directivas de certificación del mercado comercial. Está prohibido el contenido relacionado con la religión, la política, los juegos de azar y el entretenimiento prolongado. Para obtener más información, vea las directivas de [certificación del mercado comercial.](/legal/marketplace/certification-policies#10010-inappropriate-content)

La aplicación debe facilitar la colaboración en grupo, mejorar la productividad de un individuo o ambos. Las aplicaciones destinadas a la vinculación y socialización de equipos deben ser de colaboración y estar diseñadas para varios participantes. Estos tipos de aplicaciones tampoco deben requerir una inversión de tiempo considerable ni afectar perceptivamente a la productividad.

### <a name="similar-platforms-and-services"></a>Plataformas y servicios similares

Las aplicaciones deben centrarse en la experiencia Teams y no incluir los nombres, iconos o imágenes de otras plataformas o servicios de colaboración basados en chat similares, a menos que la aplicación proporciona interoperabilidad específica.

### <a name="feature-names"></a>Nombres de características

Los nombres de características de la aplicación en botones y otro texto de la interfaz de usuario no deben estar en conflicto con la terminología reservada para Teams y otros productos de Microsoft. Por ejemplo, **Start meeting**, **Make call** o Start **chat**. Incluya el nombre de la aplicación si no puede evitarlo por completo, como Iniciar reunión **de Contoso** en lugar de **Iniciar reunión**.

## <a name="security"></a>Seguridad

### <a name="microsoft-365-app-compliance-program"></a>Cumplimiento de Aplicaciones de Microsoft 365

El [Microsoft 365 cumplimiento](/microsoft-365-app-certification/overview) de aplicaciones está pensado para ayudar a las organizaciones a evaluar y administrar los riesgos mediante la evaluación de la información de seguridad y cumplimiento de la aplicación. Si vas a publicar una aplicación en la tienda Teams, debes completar los siguientes niveles del programa:

* [Publisher verificación:](/azure/active-directory/develop/publisher-verification-overview)ayuda a los administradores y usuarios finales a comprender la autenticidad de los desarrolladores de aplicaciones que se integran con el Plataforma de identidad de Microsoft. Cuando se completa, se muestra un distintivo azul "comprobado" en el cuadro de diálogo de consentimiento Azure Active Directory (Azure AD) y otras pantallas. Para obtener más información, consulta [preguntas más frecuentes,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)cómo marcar tu aplicación como editor [comprobado](/azure/active-directory/develop/mark-app-as-publisher-verified)y solucionar problemas de verificación [del editor.](/azure/active-directory/develop/troubleshoot-publisher-verification)
* [Publisher atestación:](/microsoft-365-app-certification/docs/attestation)proceso en el que comparte información general, de control de datos e información de seguridad y cumplimiento para ayudar a los clientes potenciales a tomar decisiones fundamentadas sobre el uso de la aplicación.

> [!NOTE]
> Si envías una aplicación que no se ha enumerado anteriormente, no puedes completar oficialmente la atestación Publisher hasta que la aplicación esté en la Teams tienda. Si estás actualizando una aplicación enumerada, completa Publisher atestación antes de enviar la versión más reciente de la aplicación.

### <a name="bots"></a>Bots

Para las aplicaciones que usan el servicio de bots Microsoft Azure (como bots y extensiones de mensajería), debe cumplir todos los requisitos definidos en los Términos de Microsoft [Online Services](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).

Los bots siempre deben pedir permiso para cargar un archivo y mostrar un mensaje de confirmación después de que se cargue el archivo.

### <a name="external-domains"></a>Dominios externos

En la mayoría de los casos, no debes incluir dominios fuera del control de la organización (incluidos caracteres comodín) y servicios de túnel en las configuraciones de dominio de la aplicación. Entre las excepciones siguientes se incluyen:

* Si la aplicación usa la OAuthCard del servicio de bot de Azure, debes incluir como un dominio válido o el botón Iniciar sesión `token.botframework.com` no funcionará. 
* Si la aplicación se basa en SharePoint, puedes incluir el sitio raíz asociado SharePoint como dominio válido mediante la `{teamSiteDomain}` propiedad context.

### <a name="authentication"></a>Autenticación

Para obtener información sobre cómo implementar la autenticación de aplicaciones, vea [autenticación en Teams](~/concepts/authentication/authentication.md).

#### <a name="authenticating-with-external-services"></a>Autenticación con servicios externos

Recuerde lo siguiente si la aplicación autentica a los usuarios con un servicio externo.

* **Iniciar sesión, cerrar sesión y registrar experiencias**:
  * Las aplicaciones que dependen de cuentas o servicios externos deben proporcionar experiencias de inicio de sesión, de registro y de registro claras y sencillas.
  * Cuando un usuario cierra sesión, debe cerrar la sesión solo desde la aplicación y seguir iniciando sesión en Teams.
* **Experiencias** de uso compartido de contenido: las aplicaciones que requieren autenticación con un servicio externo para compartir contenido en canales de Teams deben especificar claramente en la documentación de ayuda (o recursos similares) cómo desconectar o no compartir contenido si esa característica es compatible con el servicio externo. Esto no significa que la capacidad de no compartir contenido debe estar presente en la Teams aplicación.

#### <a name="government-community-cloud-listings"></a>Government Community Cloud listados

Para distribuir la aplicación Government Community Cloud usuarios (GCC) y evitar las listas duplicadas en el almacén de Teams, el proceso de autenticación debe identificar y enrutar a los usuarios a una dirección URL GCC específica o esperada.

### <a name="sensitive-content"></a>Contenido confidencial

La aplicación no debe publicar datos confidenciales, como datos de tarjetas de crédito o instrumentos de pago financieros. La aplicación tampoco debe mostrar el estado, el seguimiento de contactos u otra información de identificación personal (PII) a una audiencia que no está destinada a ver ese contenido.

Avisa a los usuarios antes de que la aplicación descargue archivos o archivos ejecutables (.exe) en el equipo o el entorno del usuario.

### <a name="financial-information"></a>Información financiera

Las aplicaciones no deben pedir a los usuarios que realicen pagos en la Teams usuario. Los detalles del instrumento financiero no deben transmitirse a los usuarios a través de una interfaz de bot.

Solo puedes vincularte a servicios de pago externos seguros si has hecho la divulgación adecuada en los términos de uso, la directiva de privacidad o cualquier página de perfil o sitio web antes de que el usuario haya aceptado usar la aplicación.

Las aplicaciones que se ejecutan en la versión de iOS o Android Teams deben cumplir las siguientes directrices:

* Las aplicaciones no deben incluir compras desde la aplicación, ofertas de prueba o interfaz de usuario que tienen como objetivo aumentar las ventas a versiones de pago o vínculos a tiendas en línea donde los usuarios pueden comprar o adquirir otro contenido, aplicaciones o complementos.
* Si la aplicación requiere una cuenta, los usuarios deben poder registrarse en una cuenta sin ningún cargo. Está prohibido el uso del término **cuenta** **gratuita** o gratuita.
* Puede determinar si una cuenta está activa indefinidamente o durante un tiempo limitado, pero si la cuenta expira, no se mostrará ninguna interfaz de usuario, texto o vínculos que indiquen la necesidad de pagar.
* La directiva de privacidad y las páginas de términos de uso de la aplicación deben estar libres de cualquier interfaz de usuario o vínculos relacionados con el comercio.

## <a name="general-functionality-and-performance"></a>Funcionalidad y rendimiento generales

### <a name="launching-external-functionality"></a>Iniciar la funcionalidad externa

Las aplicaciones no deben sacar a los usuarios de Teams escenarios principales de usuario. El contenido de la aplicación y las interacciones pueden producirse dentro Teams capacidades, como bots, tarjetas y módulos de tareas.

Debes vincular a los usuarios en Teams y no a un sitio o aplicación externos. Para escenarios que requieren funcionalidad externa, la aplicación debe tener permiso explícito del usuario para iniciar esa funcionalidad.

### <a name="compatibility"></a>Compatibilidad

Las aplicaciones deben ser totalmente funcionales en los siguientes sistemas operativos y exploradores:

* Microsoft Windows 7 y versiones posteriores
* macOS 10.10 y versiones posteriores
* Microsoft Edge 12 y versiones posteriores
* Mozilla Firefox 47.0 y versiones posteriores
* Google Chrome 51.0 y versiones posteriores
* iOS 9.0 y versiones posteriores
* Android 4.4 y versiones posteriores

### <a name="response-time"></a>Tiempo de respuesta

Teams aplicaciones deben responder en un plazo razonable, que varía según la funcionalidad.

* Las pestañas deben responder en tres segundos o mostrar un mensaje o advertencia de carga.
* Los bots deben responder a los comandos del usuario en un plazo de dos segundos o mostrar un indicador de escritura.
* Las extensiones de mensajería deben responder a comandos de usuario en un plazo de cinco segundos.
* Las notificaciones deben mostrarse en un plazo de cinco segundos desde la acción del usuario.

## <a name="app-package-and-store-listing"></a>Descripción del paquete y la tienda de la aplicación

Los paquetes de aplicaciones deben tener el formato correcto e incluir toda la información y los componentes necesarios.

### <a name="app-manifest"></a>Manifiesto de la aplicación

El Teams de la aplicación define las configuraciones de la aplicación.

* El manifiesto debe cumplir con el esquema de manifiesto más reciente. Para obtener información, vea la [referencia del manifiesto](~/resources/schema/manifest-schema.md).
* Si la aplicación incluye un bot o una extensión de mensajería, el manifiesto debe ser coherente con los metadatos de Bot Framework, incluidos el nombre del bot, el logotipo, el vínculo de la directiva de privacidad y los términos del servicio.
* Si la aplicación usa Azure Active Directory (Azure AD) para la autenticación, incluya el identificador de aplicación de Azure AD (cliente) en el manifiesto. Para obtener más información, vea la [referencia del manifiesto](~/resources/schema/manifest-schema.md#webapplicationinfo).

### <a name="app-icons"></a>Iconos de la aplicación

Los iconos son uno de los elementos principales que los usuarios ven al navegar por Teams tienda. Los iconos deben comunicar la marca y el propósito de la aplicación, al mismo tiempo que cumplen los siguientes requisitos:

* El paquete de la aplicación debe incluir dos versiones PNG del icono de la aplicación: un icono de color y un icono de esquema.
* La versión de color del icono se muestra en la mayoría Teams escenarios y debe ser de 192 x 192 píxeles. El símbolo del icono (96 x 96 píxeles) puede ser cualquier color o color, pero debe estar sobre un fondo cuadrado sólido o totalmente transparente.
* La versión de esquema del icono se muestra cuando la aplicación está en uso y "izada" en la barra de aplicaciones de la parte izquierda de Teams y cuando un usuario ancla la extensión de mensajería de la aplicación. Debe tener 32 x 32 píxeles y puede ser blanco con un fondo transparente o transparente con un fondo blanco (no se permiten otros colores). El icono no debe tener ningún relleno adicional alrededor del símbolo.
* Los iconos con formato y tamaño correctos deben incluirse en el paquete de la aplicación. Los iconos también deben coincidir con lo que se envía con los metadatos de la descripción de la tienda.

Para obtener más información, procedimientos recomendados y ejemplos, consulta las Teams de icono [de la aplicación.](~/concepts/build-and-test/apps-package.md#app-icons)

### <a name="app-descriptions"></a>Descripciones de aplicaciones

Debes tener una descripción corta y larga de la aplicación. Las descripciones de las configuraciones de la aplicación y el Centro de partners deben ser las mismas.

Las descripciones no deben desprestigiar directamente ni a través de la insinuación otra marca (propiedad de Microsoft o de otro modo). Asegúrese de que la descripción no incluya notificaciones que no se puedan justificar (por ejemplo, "Aumento garantizado del 200 por ciento en eficiencia").

#### <a name="short-description"></a>La descripción breve

Una breve descripción es un resumen conciso de la aplicación que resalta su propuesta de valor y se dirige a la audiencia de destino.

**Sí:**

* Mantenga la descripción corta en una oración.
* Coloque primero la información más importante.
* Incluir palabras clave que es probable que los clientes busquen.

**No:**

* Repita el nombre de la aplicación.
* Usa la palabra **aplicación** en la breve descripción.

#### <a name="long-description"></a>La descripción larga

La descripción larga puede proporcionar una narrativa atractiva que resalta la propuesta de valor de la aplicación, la audiencia principal y el sector de destino. Aunque esta descripción puede tener hasta 4.000 caracteres, la mayoría de los usuarios solo leerán entre 300 y 500 palabras.

**Sí:**

* Use [Markdown para](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) dar formato a la descripción.
* Use voz activa y hable directamente con los usuarios. Por ejemplo, *puede ...*.
* Enumera las características con puntos de viñeta para que sea más fácil examinar la descripción.
* Describa claramente limitaciones, condiciones o excepciones a las funciones, características y entregas descritas en la descripción y los materiales relacionados antes de que el usuario instale la aplicación. Las Teams que admite la aplicación deben estar relacionadas con las funciones principales que describe la descripción.
* Incluye un vínculo de ayuda o soporte técnico.
* Consulte **Microsoft 365** en lugar de **Office 365**.
* Si necesita hacer referencia a **Teams**, escriba la primera referencia como **Microsoft Teams**. Las referencias posteriores se pueden acortar **a Teams**.
* Usa el siguiente idioma al describir cómo funciona la aplicación con Teams (o Microsoft 365):
  * "... funciona con Microsoft Teams."
  * "... trabajar con Microsoft Teams."
  * "... dentro de Microsoft Teams."
  * "... para Microsoft Teams."

**No:**

* Supere las 500 palabras.
* Abreviar **Microsoft** como **MS** o **MSFT**.
* Indica que la aplicación es una oferta de Microsoft, incluido el uso de lemas o lemas de Microsoft.
* Usa nombres de marca con derechos de autor que no posees.
* Incluya errores tipográficos, gramaticales y mayúsculas innecesarias (por ejemplo, **Usuarios** en lugar de **usuarios).**
* Incluir vínculos a AppSource.
* Use el siguiente idioma a menos que sea un partner de Microsoft certificado:
  * "... integrado con Microsoft Teams"
  * "... se integra con ..."
  * "... creado para ..."
  * "... basado en ..."
  * "... se ejecuta en ..."
  * "... habilitado por ..."
  * "... certificado para ..."
  * "... desarrollado para ..."
  * "... diseñado para ..."

### <a name="screenshots"></a>Capturas de pantalla

Las capturas de pantalla proporcionan una vista previa visual destacada de la aplicación para complementar el nombre, el icono y las descripciones de la aplicación. Recuerde lo siguiente acerca de las capturas de pantalla:

* Puedes tener hasta cinco capturas de pantalla por descripción.
* Los tipos de archivo admitidos incluyen PNG, JPEG y GIF.
* Las dimensiones deben ser de 1366 x 768 píxeles.
* Tamaño máximo de 1.024 KB.

**Sí:**

* Céntrate en las capacidades de la aplicación (por ejemplo, cómo las personas pueden comunicarse con el bot).
* Incluye contenido que represente con precisión la aplicación.
* Use el texto con juicio.
* Capturas de pantalla de fotogramas con un color que refleje su marca e incluya contenido de marketing, similar al ejemplo de descripción de [Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) (los requisitos de dimensión se aplican a toda la imagen y no solo a la captura de pantalla).

**No:**

* Mostrar dispositivos específicos, como teléfonos o portátiles.
* Muestra cromo o interfaz de usuario que no esté en la aplicación.
* Captura cualquier Teams o interfaz de usuario del explorador en las capturas de pantalla.
* Incluye simulacros que reflejen inexactamente la interfaz de usuario real de la aplicación, como mostrar que la aplicación se usa fuera de Teams.

> [!TIP]
> Un vídeo puede ser la forma más eficaz de comunicar por qué las personas deben usar la aplicación. Un vídeo también es lo primero que los usuarios ven en la descripción (de forma predeterminada, se muestra un vídeo antes de las capturas de pantalla). Para obtener más información, [consulta crear un vídeo para la descripción de la tienda.](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)

### <a name="privacy-policy"></a>Directiva de privacidad

La directiva de privacidad puede ser específica de Teams aplicación o una directiva general para todos los servicios.

* Si usas una plantilla de directiva de privacidad  genérica, debes hacer referencia a **servicios,** aplicaciones y plataformas para incluir tu aplicación Teams tu servicio o sitio web.
* Debe incluir cómo se administra el almacenamiento, la retención y la eliminación de datos de usuario. También debe describir los controles de seguridad que usa para la protección de datos.
* Debe incluir su información de contacto.
* No debe contener direcciones URL rotas ni con fines beta o de almacenamiento provisional.
* No debe incluir vínculos a AppSource.

### <a name="terms-of-use"></a>Términos de uso

Sus términos de uso deben ser específicos y aplicables a su oferta.

### <a name="support-links"></a>Vínculos de soporte técnico

Las direcciones URL de soporte técnico de la aplicación no deben requerir autenticación. Por ejemplo, los usuarios no deben tener que iniciar sesión para ponerse en contacto con usted.

### <a name="localization"></a>Localización

Si la aplicación admite la localización, el paquete de la aplicación debe incluir un archivo con traducciones de idioma que se muestran en función de la configuración Teams idioma. El archivo debe cumplir con el Teams de localización. Para obtener más información, [vea el Teams de localización.](~/concepts/build-and-test/apps-localization.md)

## <a name="tabs"></a>Pestañas

Si la aplicación incluye una pestaña, asegúrate de que se adhiera a estas directrices.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulta las Teams [de diseño de pestañas.](~/tabs/design/tabs.md)

### <a name="setup"></a>Instalación

* La configuración de tabulación no debe ser un usuario nuevo. Proporcione un mensaje sobre cómo completar la acción o el flujo de trabajo.
* La autenticación debe realizarse durante la configuración de pestañas y no después.

### <a name="views"></a>Views

* El área de pantalla de inicio de sesión no debe usar logotipos grandes ni mostrar una página web completa.
* El contenido se puede simplificar desglosando en varias pestañas.
* Las pestañas no deben tener un encabezado duplicado. Quita el logotipo del iframe ya que el marco de pestañas ya muestra el icono y el nombre de la aplicación.

### <a name="navigation"></a>Navegación

* Las pestañas no deben tener más de tres niveles de navegación.
* Las pestañas no deben proporcionar navegación que entre en conflicto con la navegación Teams principal.
* Las páginas secundarias y terciarias de una pestaña deben abrirse en una vista de nivel dos y nivel tres en el área de pestaña principal, que se navega a través de rutas de navegación o navegación izquierda. También puede incluir los siguientes componentes para facilitar la navegación por pestañas:
    * Botones atrás
    * Encabezados de página
    * Menús de hamburguesa
* Tab no debe tener desplazamiento horizontal.
* Los vínculos profundos de las pestañas no deben vincularse a una página web externa, sino en algún lugar de Teams. Por ejemplo, módulos de tareas u otras pestañas.
* Las pestañas no deben permitir que los usuarios naveguen fuera Teams la experiencia principal de la aplicación.

### <a name="usability"></a>Facilidad de uso

* Las pestañas deben proporcionar valor más allá de simplemente hospedar un sitio web existente.
* Los usuarios deben poder deshacer su última acción en la pestaña.
* Las pestañas de un contexto personal pueden agregar contenido de instancias compartidas de la aplicación.
* Las pestañas deben responder a Teams temas. Cuando un usuario cambia el tema, el tema de la aplicación debe reflejar la selección.
* Las pestañas deben usar Teams de estilo, como fuentes Teams, rampas de tipo, paletas de colores, sistema de cuadrícula, movimiento, tono de voz, y así sucesivamente siempre que sea posible.
* Debe incluir una **pestaña Configuración** usuario.
* Las pestañas deben seguir Teams de interacción, como navegación en la página, posición y uso de cuadros de diálogo, jerarquías de información, y así sucesivamente siempre que sea posible.
* El contenido de tabulación en el iframe no debe incluir características que imitan Teams funcionalidades principales. Por ejemplo, bots, extensiones de mensajería, llamadas, reuniones, entre otros.

> [!TIP]
>
> * Incluye un bot personal junto con una pestaña personal.
> * Permitir que los usuarios compartan contenido desde su pestaña personal.

## <a name="bots"></a>Bots

Si la aplicación incluye un bot, asegúrate de que se adhiera a estas directrices.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulta las Teams de diseño [de bots.](~/bots/design/bots.md)

### <a name="bot-commands"></a>Comandos bot

Es difícil analizar la entrada del usuario y predecir la intención del usuario. Los comandos bot proporcionan a los usuarios un conjunto de palabras o frases que el bot entiende para que ellos (y el bot) no tengan que adivinar.

* Se recomienda enumerar los comandos de bot compatibles en las configuraciones de la aplicación. Estos comandos se muestran en el cuadro de redacción cuando un usuario intenta enviar un mensaje al bot.
* Todos los comandos compatibles con el bot deben funcionar correctamente, incluidos los comandos **Hi**, **Hello** y **Help.**

> [!TIP]
> Para los bots personales, incluya una **pestaña de** ayuda que describa más a continuación lo que el bot puede hacer.

### <a name="bot-welcome-messages"></a>Mensajes de bienvenida del bot

* Los bots casi siempre deben enviar un mensaje de bienvenida durante la primera ejecución. Para obtener la mejor experiencia, el mensaje debe incluir la propuesta de valor del bot, cómo configurar el bot y describir brevemente todos los comandos de bot admitidos. Puede mostrar el mensaje con una tarjeta adaptable con botones para una mejor facilidad de uso. Para obtener más información, [vea cómo desencadenar un mensaje de bienvenida del bot](~/bots/how-to/conversations/send-proactive-messages.md).
* Los mensajes de bienvenida del bot en canales y chats son opcionales durante la primera ejecución, especialmente si el bot está disponible para uso personal y realiza acciones similares. Si el bot envía mensajes de bienvenida, no debe enviarlos a los usuarios individualmente (esto se considera [correo no deseado).](#bot-message-spamming) El mensaje también debe mencionar a la persona que agregó el bot.
* Los bots de solo notificación deben enviar un mensaje de bienvenida que transmita que no responderá a los mensajes de los usuarios.

> [!TIP]
> En los mensajes de bienvenida a usuarios individuales, un recorrido por carrusel puede proporcionar una introducción eficaz al bot y a cualquier otra función de la aplicación. Se recomienda incluir botones para permitir que los usuarios prueben comandos bot. Por ejemplo, **Crear una tarea**.

### <a name="bot-message-spamming"></a>Correo no deseado de mensajes de bot

Los bots no deben enviar correo no deseado a los usuarios enviando varios mensajes en breve sucesión.

* **Mensajes de bot en canales y chats:** no enviar correo no deseado a los usuarios mediante la creación de publicaciones independientes. Cree una sola entrada con respuestas en el mismo subproceso.
* **Mensajes de bot en aplicaciones personales:** no envíe varios mensajes en una sucesión rápida. Envíe un mensaje con información completa. Evite conversaciones en varios turnos para completar un único flujo de trabajo. En su lugar, considere el uso de un formulario (o módulo de tareas) para recopilar todas las entradas de un usuario a la vez.
* **Mensajes de bienvenida:** no se permite repetir el mismo mensaje de bienvenida a intervalos regulares y se considera correo no deseado. Por ejemplo, cuando se agrega un nuevo miembro a un equipo, no se envía correo no deseado a los demás miembros con un mensaje de bienvenida. En su lugar, envía un mensaje personal al nuevo miembro.

### <a name="bot-notifications"></a>Notificaciones de bot

Las notificaciones de bot deben incluir contenido relevante para el ámbito definido para el bot (equipo, chat o personal).

### <a name="bots-and-adaptive-cards"></a>Bots y tarjetas adaptables

Las tarjetas adaptables son una forma muy recomendada de mostrar mensajes de bot. Las tarjetas deben ser ligeras e incluir solo de 1 a 3 acciones. Si necesita mostrar más contenido, considere la posibilidad de usar un módulo de tareas o una pestaña.

Consulte los siguientes recursos para obtener más información:

* [Diseño de tarjetas adaptables](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Referencia de tarjetas](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

## <a name="messaging-extensions"></a>Extensiones de mensajería

Si la aplicación incluye una extensión de mensajería, asegúrate de que cumple estas directrices.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulta las Teams de diseño de [extensión de mensajería.](~/messaging-extensions/design/messaging-extension-design.md)

### <a name="action-commands"></a>Comandos de acción

Las extensiones de mensajería basadas en acciones deben hacer lo siguiente:

* Permitir a los usuarios desencadenar acciones en un mensaje sin completar pasos intermedios, como iniciar sesión.
* Pase el contexto del mensaje al siguiente estado de trabajo.

### <a name="preview-links-link-unfurling"></a>Vínculos de vista previa (desamuestreo de vínculos)

Las extensiones de mensajería deben obtener una vista previa de los vínculos reconocidos en Teams cuadro de redacción. No agregue dominios que estén fuera del control (direcciones URL absolutas o caracteres comodín). Por ejemplo, `yourapp.onmicrosoft.com` es válido pero no es `*.onmicrosoft.com` válido. Los dominios de nivel superior también están prohibidos (por ejemplo, `*.com` o `*.org` ).

### <a name="search-commands"></a>Comandos de búsqueda

* Las extensiones de mensajería basadas en búsquedas deben proporcionar texto que ayude a los usuarios a realizar búsquedas de forma eficaz.
* @mention ejecutables deben ser claros, fáciles de comprender y legibles.

## <a name="task-modules"></a>Módulos de tareas

Un módulo de tareas debe incluir un icono y el nombre corto de la aplicación a la que está asociada.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulta las Teams de diseño del [módulo de tareas.](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="meeting-extensions"></a>Extensiones de reunión

Si la aplicación incluye una extensión de reunión, asegúrate de que cumple estas directrices.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulta las Teams de diseño de [extensión de reunión.](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)

### <a name="pre--and-post-meeting-experience"></a>Experiencia previa y posterior a la reunión

* Las pantallas previas y posteriores a la reunión deben cumplir las directrices generales de diseño de pestañas. Para obtener más información, vea [las Teams de diseño](~/tabs/design/tabs.md).
* Las pestañas no deben tener desplazamiento horizontal.
* Las pestañas deben tener un diseño organizado al mostrar varios elementos. Por ejemplo, más de 10 sondeos o encuestas. Vea un [diseño de ejemplo](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).
* La aplicación debe notificar a los usuarios cuando los resultados de una encuesta o sondeo se exportan indicando"Resultados descargados correctamente".

### <a name="in-meeting-experience"></a>Experiencia en la reunión

* Las aplicaciones solo deben usar un tema oscuro durante las reuniones. Para obtener más información, vea [las Teams de diseño](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming).
* Una información sobre herramientas debe mostrar el nombre de la aplicación al pasar el mouse sobre el icono de la aplicación durante las reuniones.
* Las extensiones de mensajería deben funcionar igual durante las reuniones que las externas.

### <a name="in-meeting-tabs"></a>Pestañas en la reunión

* Debe tener capacidad de respuesta. Asegúrese de mantener el relleno y los tamaños de los componentes.
* Debe tener un botón atrás si hay más de una capa de navegación.
* No debe incluir más de un botón de cierre o cierre. Esto puede confundir a los usuarios, ya que ya hay un botón de encabezado integrado para descartar la pestaña.
* No debe tener desplazamiento horizontal.

### <a name="in-meeting-dialogs"></a>Cuadros de diálogo en reunión

* Debe usarse con moderación y para escenarios ligeros y orientados a tareas.
* Debe mostrar contenido en una sola columna y no tener varios niveles de navegación.
* No debe usar módulos de tareas.
* Debe alinearse con el centro de la fase de reunión.
* Debe descartarse una vez que un usuario selecciona un botón o realiza una acción.

## <a name="notifications"></a>Notificaciones

Si la aplicación usa las API de fuente de actividades proporcionadas por [Microsoft Graph](/graph/teams-send-activityfeednotifications), asegúrese de que cumple las siguientes directrices.

### <a name="general"></a>General

* Todos los desencadenadores de notificación especificados en las configuraciones de la aplicación deben obtener una notificación en la aplicación.
* Las notificaciones deben localizarse según los idiomas compatibles configurados para la aplicación.
* Las notificaciones deben mostrarse en un plazo de cinco segundos tras la acción del usuario.

### <a name="avatars"></a>Avatares

* El avatar de notificación debe coincidir con el icono de color de la aplicación.
* Las notificaciones desencadenadas por un usuario deben incluir el avatar del usuario.

### <a name="spamming"></a>Correo no deseado

* Las aplicaciones no deben enviar más de 10 notificaciones por minuto a un usuario.
* Los bots y la fuente de actividad no deben desencadenar notificaciones duplicadas.
* Las notificaciones deben proporcionar algún valor a los usuarios y no usarse para eventos triviales o irrelevantes.

### <a name="navigation-and-layout"></a>Navegación y diseño

* Las notificaciones deben cumplir el diseño y la experiencia Teams fuente de actividad.
* Al seleccionar una notificación, el usuario debe dirigirse al contenido relevante dentro de Teams y no sacarlo de la experiencia Teams usuario.

## <a name="advertising"></a>Publicidad

Las aplicaciones no deben mostrar publicidad, incluidos anuncios dinámicos, anuncios de banner y anuncios en mensajes.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una cuenta del Centro de partners](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
