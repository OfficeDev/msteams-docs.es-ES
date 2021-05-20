---
title: Microsoft Teams las directrices de validación de la tienda
description: Describe las directrices que debe seguir cada aplicación enviada a la tienda de Teams (AppSource).
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 4daa8b027d7525f0fb3223c2000eee301043398a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565140"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams las directrices de validación de la tienda

Seguir estas directrices aumenta la probabilidad de que la aplicación pase el proceso de envío de la tienda Microsoft Teams. Estas directrices específicas de Teams complementan las [directivas](/legal/marketplace/certification-policies) de certificación del mercado comercial de Microsoft y se actualizan con frecuencia para reflejar nuevas capacidades, comentarios de usuarios y cambios en las reglas de negocio.

> [!NOTE]
> Es posible que algunas directrices no sean aplicables a la aplicación. Por ejemplo, si la aplicación no incluye un bot, puede omitir las directrices relacionadas con bots.

## <a name="10-value-proposition"></a>1.0 Propuesta de valor

### <a name="11-app-name"></a>1.1 Nombre de la aplicación

El nombre de una aplicación juega un papel fundamental en la forma en que los usuarios la descubren en la tienda. Recuerde lo siguiente acerca de los nombres de aplicación:

* El nombre debe incluir términos relevantes para los usuarios.
* Los nombres de las características principales de Teams&#8212;como **chat,** **contactos,** **calendario,** **llamadas,** **archivos,** **actividad,** **Teams,** **aplicaciones** y&#8212;**de ayuda** no deben incluirse en el nombre de la aplicación.
* Los sustantivos comunes deben tener el prefijo o el sufijo con el nombre del desarrollador (por ejemplo, **Tareas de Contoso** en lugar de **tareas).**
* No debe usar **Teams** u otros nombres de productos de Microsoft que puedan indicar falsamente la co-marca o la co-venta. (Para obtener más información acerca de cómo hacer referencia al software, los productos y los servicios de Microsoft, consulte las [Directrices de marcas comerciales y marcas de Microsoft).](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)
* Si la aplicación forma parte de una asociación oficial con Microsoft, el nombre de la aplicación debe ser el primero (por ejemplo, **Contoso Connector para Microsoft Teams).**
* No debe copiar el nombre de una aplicación que aparece en la tienda u otra oferta en el mercado comercial.
* No debe contener términos profanos o despectivos. El nombre tampoco debe incluir un lenguaje racial o culturalmente insensible.
* Debe ser único. Por ejemplo, no puede enumerar varias aplicaciones para diferentes regiones con el mismo nombre y funcionalidad.

### <a name="12-suitable-for-workplace-consumption"></a>1.2 Adecuado para el consumo en el lugar de trabajo

El contenido de la aplicación debe ser adecuado para el consumo general en el lugar de trabajo y cumplir con todas las restricciones enumeradas en las políticas de certificación del mercado comercial. Está prohibido el contenido relacionado con la religión, la política, los juegos de azar y el entretenimiento prolongado. Para obtener más información, consulte las [políticas de certificación del mercado comercial.](/legal/marketplace/certification-policies#10010-inappropriate-content)

La aplicación debe facilitar la colaboración en grupo, mejorar la productividad de un individuo o ambos. Las aplicaciones destinadas a la vinculación y socialización de equipos deben ser colaborativas y diseñadas para varios participantes. Este tipo de aplicaciones tampoco deben requerir una inversión de tiempo sustancial o afectar perceptivamente a la productividad.

### <a name="13-similar-platforms-and-services"></a>1.3 Plataformas y servicios similares

Las aplicaciones deben centrarse en la experiencia Teams y no incluir los nombres, iconos o imágenes de otras plataformas o servicios de colaboración basados en chat similares a menos que la aplicación proporcione interoperabilidad específica.

### <a name="14-feature-names"></a>1.4 Nombres de características

Los nombres de características de la aplicación en los botones y otro texto de la interfaz de usuario no deben entrar en conflicto con la terminología reservada para Teams y otros productos de Microsoft. Por ejemplo, **Iniciar reunión**, **Realizar llamada** o Iniciar **chat**. Incluya el nombre de la aplicación si no puede evitarlo por completo, como **Iniciar reunión de Contoso** en lugar de Iniciar **reunión.**

## <a name="20-security"></a>2.0 Seguridad

### <a name="21-microsoft-365-app-compliance-program"></a>2.1 programa de cumplimiento de aplicaciones Microsoft 365

El [programa de cumplimiento de aplicaciones de Microsoft 365](/microsoft-365-app-certification/overview) está destinado a ayudar a las organizaciones a evaluar y administrar el riesgo mediante la evaluación de la información de seguridad y cumplimiento sobre la aplicación. Si va a publicar una aplicación en la tienda Teams, debe completar los siguientes niveles del programa:

* [Publisher Verificación:](/azure/active-directory/develop/publisher-verification-overview)Ayuda a los administradores y usuarios finales a comprender la autenticidad de los desarrolladores de aplicaciones que se integran con el Plataforma de identidad de Microsoft. Cuando se completa, se muestra una insignia azul "verificada" en el cuadro de diálogo de consentimiento de Azure Active Directory (Azure AD) y otras pantallas. Para obtener más información, consulta [las preguntas más frecuentes,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions) [cómo marcar la aplicación como editor verificado](/azure/active-directory/develop/mark-app-as-publisher-verified)y solucionar problemas de verificación [del editor.](/azure/active-directory/develop/troubleshoot-publisher-verification)
* [Publisher Attestation:](/microsoft-365-app-certification/docs/attestation)un proceso en el que comparte información general de seguridad y cumplimiento de datos para ayudar a los clientes potenciales a tomar decisiones informadas sobre el uso de la aplicación.

> [!NOTE]
> Si envías una aplicación que no se ha enumerado anteriormente, no puedes completar oficialmente Publisher Attestation hasta que la aplicación esté en la tienda Teams. Si estás actualizando una aplicación listada, completa Publisher Attestation antes de enviar la versión más reciente de la aplicación.

### <a name="22-bots"></a>2.2 Bots

Para las aplicaciones que usan el servicio de bots Microsoft Azure (como bots y extensiones de mensajería), debe seguir todos los requisitos definidos en los Términos de Servicios [en línea de](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)Microsoft.

Los bots siempre deben pedir permiso para cargar un archivo y mostrar un mensaje de confirmación después de que se cargue el archivo.

### <a name="23-external-domains"></a>2.3 Dominios externos

En la mayoría de los casos, no debe incluir dominios fuera del control de la organización (incluidos comodines) y servicios de tunelización en las configuraciones de dominio de la aplicación. Las siguientes excepciones incluyen:

* Si la aplicación usa la OAuthCard del Servicio de bots de Azure, debe `token.botframework.com` incluirla como dominio válido o el botón **Iniciar sesión** no funcionará.
* Si la aplicación se basa en SharePoint, puede incluir el sitio de SharePoint raíz asociado como un dominio válido mediante la `{teamSiteDomain}` propiedad context.

### <a name="24-authentication"></a>2.4 Autenticación

Para obtener información sobre cómo implementar la autenticación de aplicaciones, consulte [autenticación en Teams](~/concepts/authentication/authentication.md).

#### <a name="241-authenticating-with-external-services"></a>2.4.1 Autenticación con servicios externos

Recuerde lo siguiente si la aplicación autentica a los usuarios con un servicio externo.

* **Inicie sesión, inicie sesión e inscríbase en experiencias:**
  * Las aplicaciones que dependen de cuentas o servicios externos deben proporcionar una iniciación de sesión clara y sencilla, iniciar sesión e inscribirse experiencias.
  * Cuando un usuario cierra sesión, solo debe cerrar sesión desde la aplicación y permanecer iniciado sesión en Teams.
* **Experiencias de uso compartido de contenido:** las aplicaciones que requieren autenticación con un servicio externo para compartir contenido en canales Teams deben indicar claramente en la documentación de ayuda (o recursos similares) cómo desconectar o no compartir contenido si esa característica es compatible con el servicio externo. Esto no significa que la capacidad de no compartir contenido debe estar presente en su aplicación Teams.

#### <a name="242-government-community-cloud-listings"></a>2.4.2 Government Community Cloud listados

Para distribuir la aplicación a usuarios Government Community Cloud (GCC) evitando la duplicación de anuncios en el almacén de Teams, el proceso de autenticación debe identificar y enrutar a los usuarios a una dirección URL GCC específica o esperada.

### <a name="25-sensitive-content"></a>2.5 Contenido confidencial

La aplicación no debe publicar datos confidenciales, como datos de tarjetas de crédito o instrumentos de pago financiero. La aplicación tampoco debe mostrar estado, seguimiento de contacto u otra información de identificación personal (PII) a un público no destinado a ver ese contenido.

Advierta a los usuarios antes de que la aplicación descargue archivos o ejecutables (.exe) en el equipo o entorno del usuario.

### <a name="26-financial-information"></a>2.6 Información financiera

Las aplicaciones no deben pedir a los usuarios que realicen pagos dentro de la interfaz de Teams. Los detalles del instrumento financiero no deben transmitirse a los usuarios a través de una interfaz de bot.

Puede vincular a servicios de pago externos seguros solo si realizó la divulgación adecuada en sus términos de uso, política de privacidad o cualquier página de perfil o sitio web antes de que el usuario aceptara usar la aplicación.

Las aplicaciones que se ejecutan en la versión para iOS o Android de Teams deben cumplir las siguientes directrices:

* Las aplicaciones no deben incluir compras dentro de la aplicación, ofertas de prueba o interfaz de usuario que tiene como objetivo aumentar el ventas a versiones de pago o enlaces a tiendas en línea donde los usuarios pueden comprar o adquirir otro contenido, aplicaciones o complementos.
* Si la aplicación requiere una cuenta, los usuarios deben poder registrarse para obtener una cuenta sin cargo alguno. Está prohibido el uso del término cuenta **gratuita** o **gratuita.**
* Puede determinar si una cuenta está activa indefinidamente o por un tiempo limitado, pero si la cuenta expira, no se puede mostrar ninguna interfaz de usuario, texto o vínculos que indiquen la necesidad de pago.
* La política de privacidad y los términos de uso de las páginas de la aplicación deben estar libres de cualquier interfaz de usuario o enlaces relacionados con el comercio.

## <a name="30-general-functionality-and-performance"></a>3.0 Funcionalidad y rendimiento generales

### <a name="31-launching-external-functionality"></a>3.1 Lanzamiento de funcionalidad externa

Las aplicaciones no deben sacar a los usuarios de Teams para escenarios de usuario principales. El contenido de la aplicación y las interacciones pueden producirse dentro de Teams capacidades, como bots, tarjetas y módulos de tareas.

Debe vincular usuarios en algún lugar de Teams y no a un sitio o aplicación externo. Para escenarios que requieren funcionalidad externa, la aplicación debe tener permiso de usuario explícito para iniciar esa funcionalidad.

### <a name="32-compatibility"></a>3.2 Compatibilidad

Las aplicaciones deben ser completamente funcionales en los siguientes sistemas operativos y navegadores:

* Microsoft Windows 7 y versiones posteriores
* macOS 10.10 y posteriores
* Microsoft Edge 12 y versiones posteriores
* Mozilla Firefox 47.0 y versiones posteriores
* Google Chrome 51.0 y versiones posteriores
* iOS 9.0 y posteriores
* Android 4.4 y versiones posteriores

### <a name="33-response-time"></a>3.3 Tiempo de respuesta

Teams aplicaciones deben responder dentro de un plazo razonable, que varía en función de la capacidad.

* Las pestañas deben responder en un plazo de tres segundos o mostrar un mensaje de carga o advertencia.
* Los bots deben responder a los comandos del usuario en un plazo de dos segundos o mostrar un indicador de escritura.
* Las extensiones de mensajería deben responder a los comandos de usuario en un plazo de cinco segundos.
* Las notificaciones deben mostrarse dentro de los cinco segundos posteriores a la acción del usuario.

## <a name="40-app-package-and-store-listing"></a>4.0 Paquete de aplicaciones y listado de tiendas

Los paquetes de aplicaciones deben tener el formato correcto e incluir toda la información y componentes necesarios.

### <a name="41-app-manifest"></a>4.1 Manifiesto de la aplicación

El manifiesto de aplicación Teams define las configuraciones de la aplicación.

* El manifiesto debe ajustarse al esquema de manifiesto más reciente. Para obtener información, consulte la [referencia de manifiesto](~/resources/schema/manifest-schema.md).
* Si la aplicación incluye un bot o una extensión de mensajería, el manifiesto debe ser coherente con los metadatos de Bot Framework, incluido el nombre del bot, el logotipo, el vínculo de política de privacidad y los términos del vínculo de servicio.
* Si la aplicación usa Azure Active Directory (Azure AD) para la autenticación, incluya el identificador de aplicación (cliente) de Azure AD en el manifiesto. Para obtener más información, consulte la referencia de [manifiesto](~/resources/schema/manifest-schema.md#webapplicationinfo).

### <a name="42-app-icons"></a>4.2 Iconos de la aplicación

Los iconos son uno de los principales elementos que las personas ven al navegar por la tienda Teams. Los iconos deben comunicar la marca y el propósito de la aplicación, al tiempo que se adhieren a los siguientes requisitos:

* El paquete de la aplicación debe incluir dos versiones PNG del icono de la aplicación: un icono de color y un icono de contorno.
* La versión en color del icono se muestra en la mayoría de los escenarios Teams y debe ser de 192x192 píxeles. Su símbolo de icono (96x96 píxeles) puede ser de cualquier color o color, pero debe sentarse sobre un fondo cuadrado sólido o totalmente transparente.
* La versión de esquema del icono se muestra cuando la aplicación está en uso y "izado" en la barra de aplicaciones en el lado izquierdo de Teams y cuando un usuario anclar la extensión de mensajería de la aplicación. Debe ser de 32x32 píxeles y puede ser blanco con un fondo transparente o transparente con un fondo blanco (no se permiten otros colores). El icono no debe tener ningún relleno adicional alrededor del símbolo.
* Los iconos con tamaño y formato correctos deben incluirse en el paquete de la aplicación. Los iconos también deben coincidir con lo que se envía con los metadatos de la lista de la tienda.

Para obtener más información, prácticas recomendadas y ejemplos, consulte las directrices de [iconos](~/concepts/build-and-test/apps-package.md#app-icons)de Teams aplicación.

### <a name="43-app-descriptions"></a>4.3 Descripciones de aplicaciones

Debe tener una descripción corta y larga de la aplicación. Las descripciones de las configuraciones de la aplicación y del Centro de partners deben ser las mismas.

Las descripciones no deben ser directas o a través de insinuación menospreciar otra marca (propiedad de Microsoft o de otro modo). Asegúrese de que su descripción no incluya notificaciones que no se puedan justificar (por ejemplo, "Aumento garantizado del 200 por ciento en la eficiencia").

#### <a name="431-short-description"></a>4.3.1 Breve descripción

Una breve descripción es un resumen conciso de la aplicación que resalta su propuesta de valor y está dirigida a su público objetivo.

**Sí:**

* Mantenga la breve descripción en una oración.
* Coloque primero la información más importante.
* Incluya palabras clave que es probable que los clientes busquen.

**No:**

* Repita el nombre de la aplicación.
* Utilice la **aplicación** word en la breve descripción.

#### <a name="432-long-description"></a>4.3.2 Larga descripción

La descripción larga puede proporcionar una narrativa atractiva que resalte la propuesta de valor de la aplicación, el público principal y la industria objetivo. Aunque esta descripción puede tener hasta 4.000 caracteres, la mayoría de los usuarios solo leerán entre 300 y 500 palabras.

**Sí:**

* Utilice [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) para dar formato a su descripción.
* Utilice la voz activa y hable directamente con los usuarios. Por ejemplo, *Puede ...*.
* Enumere las entidades con viñetas para que sea más fácil escanear la descripción.
* Describa claramente las limitaciones, condiciones o excepciones a la funcionalidad, características y entregables descritos en la lista y materiales relacionados antes de que el usuario instale la aplicación. Las Teams capacidades que admite la aplicación deben relacionarse con las funciones principales que describe la lista.
* Incluya un enlace de ayuda o soporte técnico.
* Consulte **Microsoft 365** en lugar de **Office 365**.
* Si necesita hacer referencia a **Teams**, escriba la primera referencia como **Microsoft Teams**. Las referencias posteriores se pueden acortar a **Teams**.
* Utilice el siguiente idioma al describir cómo funciona la aplicación con Teams (o Microsoft 365):
  * "... trabaja con Microsoft Teams."
  * "... trabajando con Microsoft Teams."
  * "... dentro de Microsoft Teams."
  * "... para Microsoft Teams."

**No:**

* Supera las 500 palabras.
* Abreviar **Microsoft** como **MS** o **MSFT**.
* Indica que la aplicación es una oferta de Microsoft, incluido el uso de eslóganes o eslóganes de Microsoft.
* Usa marcas con derechos de autor que no poseas.
* Incluya errores tipográficos, errores gramaticales y mayúsculas innecesarias (por ejemplo, **Usuarios** en lugar de **usuarios).**
* Incluya vínculos a AppSource.
* Utilice el siguiente idioma a menos que sea un asociado certificado de Microsoft:
  * "... integrado con Microsoft Teams"
  * "... se integra con ..."
  * "... construido para ..."
  * "... construido sobre ..."
  * "... se ejecuta en ..."
  * "... habilitado por ..."
  * "... certificado para ..."
  * "... desarrollado para ..."
  * "... diseñado para ..."

### <a name="44-screenshots"></a>4.4 Capturas de pantalla

Las capturas de pantalla proporcionan una vista previa visual destacada de la aplicación para complementar el nombre, el icono y las descripciones de la aplicación. Recuerde lo siguiente acerca de las capturas de pantalla:

* Puede tener hasta cinco capturas de pantalla por anuncio.
* Los tipos de archivo compatibles incluyen PNG, JPEG y GIF.
* Las dimensiones deben ser de 1366x768 píxeles.
* Tamaño máximo de 1.024 KB.

**Sí:**

* Céntrate en las capacidades de la aplicación (por ejemplo, cómo las personas pueden comunicarse con el bot).
* Incluya contenido que represente con precisión la aplicación.
* Utilice el texto con criterio.
* Capturas de pantalla de fotogramas con un color que refleja tu marca e incluye contenido de marketing, similar al ejemplo [de listado de Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) (los requisitos de dimensión se aplican a toda la imagen y no solo a la captura de pantalla).

**No:**

* Mostrar dispositivos específicos, como teléfonos o computadoras portátiles.
* Muestra chrome o interfaz de usuario que no está en tu aplicación.
* Captura cualquier interfaz de usuario de Teams o navegador en tus capturas de pantalla.
* Incluya maquetas que reflejen inexactamente la interfaz de usuario real de la aplicación, como mostrar que la aplicación se usa fuera de Teams.

> [!TIP]
> Un vídeo puede ser la forma más eficaz de comunicar por qué las personas deben usar la aplicación. Un video también es lo primero que los usuarios ven en tu anuncio (de forma predeterminada, un video se muestra antes de las capturas de pantalla). Para obtener más información, consulta [crear un vídeo para tu anuncio de tienda.](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)

### <a name="45-privacy-policy"></a>4.5 Política de privacidad

La política de privacidad puede ser específica de su aplicación Teams o una política general para todos sus servicios.

* Si utiliza una plantilla de política de privacidad genérica, debe hacer referencia a **servicios,** **aplicaciones** y **plataformas** para incluir su aplicación Teams y su servicio o sitio web.
* Debe incluir cómo controlar el almacenamiento, la retención y la eliminación de datos de usuario. También debe describir los controles de seguridad que utiliza para la protección de datos.
* Debe incluir su información de contacto.
* No debe contener direcciones URL que estén rotas o con fines beta o de ensayo.
* No debe incluir vínculos a AppSource.

### <a name="46-terms-of-use"></a>4.6 Condiciones de uso

Sus términos de uso deben ser específicos y aplicables a su oferta.

### <a name="47-support-links"></a>4.7 Enlaces de soporte

Las direcciones URL de soporte técnico de la aplicación no deben requerir autenticación. Por ejemplo, los usuarios no deben tener que iniciar sesión para ponerse en contacto con usted.

### <a name="48-localization"></a>4.8 Localización

Si la aplicación admite la localización, el paquete de la aplicación debe incluir un archivo con traducciones de idioma que se muestren en función de la configuración de idioma Teams. El archivo debe ajustarse al esquema de localización Teams. Para obtener más información, vea el [esquema de localización Teams](~/concepts/build-and-test/apps-localization.md).

## <a name="50-tabs"></a>5.0 Pestañas

Si la aplicación incluye una pestaña, asegúrate de que se adhiere a estas directrices.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulte las [directrices de diseño de la pestaña Teams.](~/tabs/design/tabs.md)

### <a name="51-setup"></a>Configuración 5.1

* La configuración de tabulación no debe poner en callejón sin salida a un nuevo usuario. Proporcione un mensaje sobre cómo completar la acción o el flujo de trabajo.
* La autenticación debe ocurrir durante la configuración de la pestaña y no después.

### <a name="52-views"></a>5.2 Vistas

* El área de la pantalla de inicio de sesión no debe usar logotipos grandes ni mostrar toda una página web.
* El contenido se puede simplificar descomponiéndolo en varias pestañas.
* Las pestañas no deben tener un encabezado duplicado. Quite el logotipo del iframe, ya que el marco de pestañas ya muestra el icono y el nombre de la aplicación.

### <a name="53-navigation"></a>5.3 Navegación

* Las pestañas no deben tener más de tres niveles de navegación.
* Las pestañas no deben proporcionar navegación que entre en conflicto con la navegación Teams principal.
* Las páginas secundarias y terciarias de una pestaña deben abrirse en una vista de nivel dos y nivel tres en el área de tabulación principal, que se navega a través de migas de pan o navegación izquierda. También puede incluir los siguientes componentes para ayudar a la navegación en ficha:
    * Botones traseros
    * Encabezados de página
    * Menús de hamburguesas
* Tabulador no debe tener desplazamiento horizontal.
* Los vínculos profundos en pestañas no deben vincularse a una página web externa, sino a algún lugar dentro de Teams. Por ejemplo, módulos de tareas u otras pestañas.
* Las pestañas no deben permitir a los usuarios navegar fuera de Teams para la experiencia principal de la aplicación.

### <a name="54-usability"></a>5.4 Usabilidad

* Las pestañas deben proporcionar valor más allá de hospedar un sitio web existente.
* Los usuarios deben poder deshacer su última acción en la pestaña.
* Las pestañas de un contexto personal pueden agregar contenido de instancias compartidas de la aplicación.
* Las pestañas deben responder a Teams temas. Cuando un usuario cambia el tema, el tema de la aplicación debe reflejar la selección.
* Las pestañas deben usar componentes de estilo Teams, como fuentes Teams, rampas de tipo, paletas de colores, sistema de cuadrícula, movimiento, tono de voz, etc. siempre que sea posible.
* Debe incluir una **pestaña Configuración.**
* Las pestañas deben seguir Teams diseño de interacción, como la navegación en la página, la posición y el uso de cuadros de diálogo, jerarquías de información, etc. siempre que sea posible.
* El contenido de la pestaña en el iframe no debe incluir características que imiten Teams capacidades principales. Por ejemplo, bots, extensiones de mensajería, llamadas, reuniones, etc.

> [!TIP]
>
> * Incluya un bot personal junto a una pestaña personal.
> * Permita que los usuarios compartan contenido desde su pestaña personal.

## <a name="60-bots"></a>6.0 Bots

Si la aplicación incluye un bot, asegúrate de que cumple estas directrices.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulte las [directrices de diseño de bots Teams](~/bots/design/bots.md).

### <a name="61-bot-commands"></a>6.1 Comandos bot

Analizar la entrada del usuario y predecir la intención del usuario es difícil. Los comandos bot proporcionan a los usuarios un conjunto de palabras o frases que el bot entiende para que ellos (y el bot) no tengan que adivinar.

* Es muy recomendable enumerar los comandos de bot admitidos en las configuraciones de la aplicación. Estos comandos se muestran en el cuadro de composición cuando un usuario intenta enviar un mensaje al bot.
* Todos los comandos compatibles con el bot deben funcionar correctamente, incluido el comando **Hola,** **Hola** y **Ayuda.**

> [!TIP]
> Para bots personales, incluya una pestaña **ayuda** que describa aún más lo que puede hacer el bot.

### <a name="62-bot-welcome-messages"></a>6.2 Mensajes de bienvenida bot

* Los bots casi siempre deben enviar un mensaje de bienvenida durante la primera ejecución. Para obtener la mejor experiencia, el mensaje debe incluir la propuesta de valor del bot, cómo configurar el bot y describir brevemente todos los comandos de bot admitidos. Puede mostrar el mensaje utilizando una tarjeta adaptable con botones para una mejor usabilidad. Para obtener más información, consulte [cómo desencadenar un mensaje de bienvenida de bot.](~/bots/how-to/conversations/send-proactive-messages.md)
* Los mensajes de bienvenida de bot en canales y chats son opcionales durante la primera ejecución, especialmente si el bot está disponible para uso personal y realiza acciones similares. Si el bot envía mensajes de bienvenida, no debe enviarlos a los usuarios individualmente (esto se considera [spamming).](#63-bot-message-spamming) El mensaje también debe mencionar a la persona que agregó el bot.
* Los bots de solo notificación deben enviar un mensaje de bienvenida que lo transmita que no responderá a los mensajes de los usuarios.

> [!TIP]
> En los mensajes de bienvenida a usuarios individuales, un recorrido por carrusel puede proporcionar una visión general efectiva de su bot y cualquier otra característica de la aplicación. Se recomienda incluir botones para permitir a los usuarios probar comandos de bot. Por ejemplo, **crear una tarea**.

### <a name="63-bot-message-spamming"></a>6.3 Spam de mensajes bot

Los bots no deben enviar varios mensajes en breve.

* **Mensajes de bot en canales y chats:** No spam de usuarios mediante la creación de publicaciones separadas. Cree una sola publicación con respuestas en el mismo subproceso.
* **Mensajes de bot en aplicaciones personales:** No envíes varios mensajes en rápida sucesión. Envíe un mensaje con información completa. Evite conversaciones de varias vueltas para completar un único flujo de trabajo. En su lugar, considere la posibilidad de usar un formulario (o módulo de tareas) para recopilar todas las entradas de un usuario a la vez.
* **Mensajes de bienvenida:** No se permite repetir el mismo mensaje de bienvenida a intervalos regulares y se considera spam. Por ejemplo, cuando se agrega un nuevo miembro a un equipo, no envíe un spam a los demás miembros con un mensaje de bienvenida. Envíe un mensaje personalmente al nuevo miembro.

### <a name="64-bot-notifications"></a>6.4 Notificaciones bot

Las notificaciones de bot deben incluir contenido relevante para el ámbito que defina para el bot (equipo, chat o personal).

### <a name="65-bots-and-adaptive-cards"></a>6.5 Bots y tarjetas adaptables

Las tarjetas adaptables son una forma muy recomendable de mostrar mensajes de bot. Tus cartas deben ser ligeras e incluir solo 1-3 acciones. Si necesita mostrar más contenido, considere la posibilidad de usar un módulo de tareas o una pestaña.

Consulte los siguientes recursos para obtener más información:

* [Diseño de tarjetas adaptables](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Referencia de tarjetas](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

## <a name="70-messaging-extensions"></a>7.0 Extensiones de mensajería

Si la aplicación incluye una extensión de mensajería, asegúrate de que se adhiere a estas directrices.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulte las [directrices de diseño de la extensión de mensajería Teams](~/messaging-extensions/design/messaging-extension-design.md).

### <a name="71-action-commands"></a>7.1 Comandos de acción

Las extensiones de mensajería basadas en acciones deben hacer lo siguiente:

* Permita a los usuarios desencadenar acciones en un mensaje sin completar pasos intermedios, como iniciar sesión.
* Pase el contexto del mensaje al siguiente estado de trabajo.

### <a name="72-preview-links-link-unfurling"></a>7.2 Vista previa de enlaces (despliegue de enlaces)

Las extensiones de mensajería deben obtener una vista previa de los vínculos reconocidos en el cuadro de composición de Teams. No agregue dominios que estén fuera del control (urls absolutas o comodines). Por ejemplo, `yourapp.onmicrosoft.com` es válido pero no es `*.onmicrosoft.com` válido. Los dominios de nivel superior también están prohibidos (por ejemplo, `*.com` o `*.org` ).

### <a name="73-search-commands"></a>7.3 Comandos de búsqueda

* Las extensiones de mensajería basadas en búsquedas deben proporcionar texto que ayude a los usuarios a buscar eficazmente.
* @mention ejecutables deben ser claros, fáciles de entender y legibles.

## <a name="80-task-modules"></a>8.0 Módulos de tareas

Un módulo de tareas debe incluir un icono y el nombre corto de la aplicación a la que está asociado.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulte las [directrices de diseño del módulo de tareas Teams](~/task-modules-and-cards/task-modules/design-teams-task-modules.md).

## <a name="90-meeting-extensions"></a>9.0 Ampliaciones de reuniones

Si la aplicación incluye una extensión de reunión, asegúrate de que se adhiere a estas directrices.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulte las [directrices de diseño de extensión de reunión Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md).

### <a name="91-pre--and-post-meeting-experience"></a>9.1 Experiencia previa y posterior a la reunión

* Las pantallas previas y posteriores a la reunión deben cumplir con las directrices generales de diseño de pestañas. Para obtener más información, consulte las [directrices de diseño de Teams](~/tabs/design/tabs.md).
* Las pestañas no deben tener desplazamiento horizontal.
* Las pestañas deben tener un diseño organizado al mostrar varios elementos. Por ejemplo, más de 10 encuestas o encuestas. Consulte un [diseño de ejemplo](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).
* La aplicación debe notificar a los usuarios cuando se exporten los resultados de una encuesta o encuesta indicando" Resultados descargados correctamente".

### <a name="92-in-meeting-experience"></a>9.2 Experiencia en la reunión

* Las aplicaciones solo deben usar un tema oscuro durante las reuniones. Para obtener más información, consulte las [directrices de diseño de Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming).
* Una información sobre herramientas debe mostrar el nombre de la aplicación al pasar el cursor sobre el icono de la aplicación durante las reuniones.
* Las extensiones de mensajería deben funcionar igual durante las reuniones que las reuniones externas.

### <a name="93-in-meeting-tabs"></a>9.3 Pestañas de reunión

* Debe ser receptivo. Asegúrese de mantener el relleno y los tamaños de componentes.
* Debe tener un botón atrás si hay más de una capa de navegación.
* No debe incluir más de un botón de descarte o cierre. Esto puede confundir a los usuarios ya que ya hay un botón de encabezado integrado para descartar la pestaña.
* No debe tener desplazamiento horizontal.

### <a name="94-in-meeting-dialogs"></a>9.4 Diálogos en la reunión

* Debe utilizarse con moderación y para escenarios que estén orientados a la luz y a las tareas.
* Debe mostrar contenido en una sola columna y no tener varios niveles de navegación.
* No debe utilizar módulos de tareas.
* Debe alinearse con el centro de la etapa de reunión.
* Debe descartarse una vez que un usuario selecciona un botón o realiza una acción.

## <a name="100-notifications"></a>10.0 Notificaciones

Si la aplicación usa las [API de fuente de actividad proporcionadas por Microsoft Graph,](/graph/teams-send-activityfeednotifications)asegúrese de que cumple las siguientes directrices.

### <a name="101-general"></a>10.1 General

* Todos los desencadenadores de notificación especificados en las configuraciones de la aplicación deben recibir una notificación en la aplicación.
* Las notificaciones deben estar localizadas según los idiomas admitidos configurados para la aplicación.
* Las notificaciones deben mostrarse dentro de los cinco segundos posteriores a la acción del usuario.

### <a name="102-avatars"></a>10.2 Avatares

* El avatar de notificación debe coincidir con el icono de color de la aplicación.
* Las notificaciones activadas por un usuario deben incluir el avatar del usuario.

### <a name="103-spamming"></a>10.3 Spamming

* Las aplicaciones no deben enviar más de 10 notificaciones por minuto a un usuario.
* Los bots y la fuente de actividad no deben desencadenar notificaciones duplicadas.
* Las notificaciones deben proporcionar algún valor a los usuarios y no usarse para eventos triviales o irrelevantes.

### <a name="104-navigation-and-layout"></a>10.4 Navegación y diseño

* Las notificaciones deben cumplir con el diseño y la experiencia de la fuente de actividad Teams.
* Al seleccionar una notificación, el usuario debe dirigirse al contenido relevante dentro de Teams y no sacarse de la experiencia Teams.

## <a name="110-advertising"></a>11.0 Publicidad

Las aplicaciones no deben mostrar publicidad, incluidos anuncios dinámicos, anuncios de banner y anuncios en mensajes.

## <a name="see-also"></a>Vea también

[4.0 Paquete de aplicaciones y listado de tiendas](#40-app-package-and-store-listing)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una cuenta del Centro de partners](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
