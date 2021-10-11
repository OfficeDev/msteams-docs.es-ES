---
title: Directrices de validación de la tienda de Microsoft Teams
description: Describe las directrices que debe seguir toda aplicación enviada a la tienda de Teams (AppSource).
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: e0d2edea9cdfcdba2cc7c65c15085903bd0d483c
ms.sourcegitcommit: c04a1a792773a9d5c61169c5702d94a8c478ad1c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2021
ms.locfileid: "60260536"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Directrices de validación de la tienda de Microsoft Teams

Al seguir estas directrices, se incrementa la probabilidad de que la aplicación pase el proceso de envío a la tienda de Microsoft Teams. Estas directrices específicas de Teams complementan las [directivas de certificación del mercado comercial](/legal/marketplace/certification-policies) de Microsoft y se actualizan con frecuencia para reflejar las nuevas capacidades, los comentarios de los usuarios y los cambios en las normas empresariales.

> [!NOTE]
> Algunas directrices pueden no ser aplicables a su aplicación. Por ejemplo, si la aplicación no incluye un bot, puede omitir las directrices relacionadas con los bots.

## <a name="value-proposition"></a>Propuesta de valor

### <a name="app-name"></a>Nombre de la aplicación

El nombre de una aplicación desempeña un papel fundamental a la hora de que los usuarios puedan encontrarla en la tienda. Recuerde lo siguiente:

* El nombre debe incluir términos relevantes para los usuarios.
* Los nombres de las funciones principales de Teams&#8212;como **Chat**, **Contactos**, **Calendario**, **Llamadas**, **Archivos**, **Actividad**, **Teams**, **Aplicaciones** y **Ayuda**&#8212;no deben incluirse en el nombre de su aplicación.
* Los sustantivos comunes deben llevar el prefijo o sufijo del nombre del desarrollador (por ejemplo, **Tareas de Contoso** en lugar de **Tareas**).
* No debe utilizar **Teams** u otros nombres de productos de Microsoft que puedan indicar de forma errónea que se trata de una marca compartida o una venta conjunta. (Para obtener más información sobre cómo hacer referencia al software, los productos y los servicios de Microsoft, consulte las [Directrices sobre marcas comerciales y marcas de Microsoft](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)).
* Si su aplicación forma parte de una asociación oficial con Microsoft, el nombre de su aplicación debe ir en primer lugar (por ejemplo, **Contoso Connector para Microsoft Teams**).
* No debe copiar el nombre de una aplicación que aparece en la tienda u otra oferta en el mercado comercial.
* No debe contener términos profanos o despectivos. El nombre tampoco debe incluir un lenguaje racial o culturalmente insensible.
* Debe ser único. Por ejemplo, no puede enumerar varias aplicaciones para diferentes regiones con el mismo nombre y funcionalidad.

### <a name="suitable-for-workplace-consumption"></a>Apto para el consumo en el área de trabajo

El contenido de la aplicación debe ser adecuado para el consumo general en el lugar de trabajo y cumplir con todas las restricciones enumeradas en las directivas de certificación del mercado comercial. Están prohibidos los contenidos relacionados con la religión, la directiva, el juego y el entretenimiento prolongado. Para más información, consulte las [directivas de certificación del mercado comercial](/legal/marketplace/certification-policies#10010-inappropriate-content).

Su aplicación debe facilitar la colaboración en grupo, mejorar la productividad de un individuo o ambas cosas. Las aplicaciones destinadas a la unión y socialización de equipos deben ser colaborativas y estar diseñadas para múltiples participantes. Este tipo de aplicaciones tampoco debería requerir una inversión de tiempo considerable ni afectar de forma perceptible a la productividad.

### <a name="similar-platforms-and-services"></a>Plataformas y servicios similares

Las aplicaciones deben centrarse en la experiencia de Teams y no incluir los nombres, iconos o imágenes de otras plataformas o servicios de colaboración similares basados en el chat, a menos que su aplicación ofrezca una interoperabilidad específica.

### <a name="feature-names"></a>Nombres de características

Los nombres de las funciones de la aplicación en los botones y otros textos de la interfaz de usuario no deben entrar en conflicto con la terminología reservada para Teams y otros productos de Microsoft. Por ejemplo, **Iniciar reunión**, **Realizar llamada**, o **Iniciar chat**. Incluya el nombre de su aplicación si no puede evitarlo por completo, como por ejemplo **Iniciar reunión de Contoso** en lugar de **Iniciar reunión**.

## <a name="security"></a>Seguridad

### <a name="microsoft-365-app-compliance-program"></a>Programa de cumplimiento de aplicaciones de Microsoft 365

El [Programa de cumplimiento de aplicaciones de Microsoft 365](/microsoft-365-app-certification/overview) está destinado a ayudar a las organizaciones a evaluar y administrar el riesgo mediante la evaluación de la información de seguridad y cumplimiento de su aplicación. Si publica una aplicación en la tienda de Teams, debe completar los siguientes niveles del programa:

* [Verificación de editores](/azure/active-directory/develop/publisher-verification-overview): Ayuda a los administradores y usuarios finales a comprender la autenticidad de los desarrolladores de aplicaciones que se integran en la plataforma de identidad de Microsoft. Una vez completado, aparecerá un distintivo azul de "verificado" en el diálogo de consentimiento de Azure Active Directory (Azure AD) y en otras pantallas. Para obtener más información, consulte [las preguntas más frecuentes](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [cómo marcar su aplicación como verificada por el editor](/azure/active-directory/develop/mark-app-as-publisher-verified), y [cómo solucionar el problema de la verificación del editor](/azure/active-directory/develop/troubleshoot-publisher-verification).
* [Certificación del editor](/microsoft-365-app-certification/docs/attestation): Un proceso en el que usted comparte información general, de manejo de datos y de seguridad y cumplimiento para ayudar a los clientes potenciales a tomar decisiones informadas sobre el uso de su aplicación.

> [!NOTE]
> Si presenta una aplicación que no ha sido incluida en la lista anteriormente, no puede completar oficialmente la certificación de editor hasta que su aplicación esté en la tienda de Teams. Si está actualizando una aplicación de la lista, complete el certificado de editor antes de enviar la última versión de la aplicación.

### <a name="bots"></a>Bots

En el caso de las aplicaciones que utilizan el Azure Bot Service de Microsoft (como los bots y las extensiones de mensajería), debe seguir todos los requisitos definidos en los términos de [Microsoft Online Services](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).

Los bots siempre deben pedir permiso para subir un archivo y mostrar un mensaje de confirmación después de que se cargue el archivo.

### <a name="external-domains"></a>Dominios externos

En la mayoría de los casos, no debe incluir dominios fuera del control de su organización (incluyendo comodines) ni servicios de túnel en las configuraciones de dominio de su aplicación. Se incluyen las siguientes excepciones:

* Si su aplicación utiliza la tarjeta OAuthCard de Azure Bot Service, debe incluirla `token.botframework.com` como dominio válido o el botón de **inicio de sesión** no funcionará.
* Si su aplicación depende de SharePoint, puede incluir el sitio raíz de SharePoint asociado como un dominio válido utilizando la `{teamSiteDomain}` propiedad de contexto.

### <a name="authentication"></a>Autenticación

Para obtener información sobre cómo implementar la autenticación de la aplicación, consulte la [autenticación en Teams](~/concepts/authentication/authentication.md).

#### <a name="authenticating-with-external-services"></a>Autenticación con servicios externos

Recuerde lo siguiente si su aplicación autentifica a los usuarios con un servicio externo.

* **Iniciar sesión, cerrar sesión y registrar experiencias**:
  * Las aplicaciones que dependen de cuentas o servicios externos deben ofrecer experiencias claras y sencillas de entrada, salida y registro.
  * Cuando un usuario cierra la sesión, debe cerrar la sesión solo desde la aplicación y permanecer conectado a Teams.
* **Contenido de experiencias de uso compartido**: las aplicaciones que requieren autenticación con un servicio externo para compartir contenido en canales de Teams deben indicar claramente en la documentación de ayuda (o recursos similares) cómo desconectar o dejar de compartir contenido si esa característica es compatible con el servicio externo. Esto no significa que la capacidad de dejar de compartir contenido debe estar presente en la aplicación de Teams.

#### <a name="government-community-cloud-listings"></a>Listados de Government Community Cloud

Para distribuir su aplicación a los usuarios de Government Community Cloud (GCC) y evitar al mismo tiempo la duplicación de listas en la tienda de Teams, el proceso de autenticación debe identificar y dirigir a los usuarios a una URL específica de GCC o esperada.

### <a name="sensitive-content"></a>Contenido confidencial

Su aplicación no debe publicar datos confidenciales, como datos de tarjetas de crédito o de instrumentos financieros de pago. La aplicación tampoco debe mostrar información sobre la salud, el rastreo de contactos u otra información personal identificable (PII) a un público no destinado a ver ese contenido.

Advierta a los usuarios antes de que su aplicación descargue archivos o ejecutables (.exe) en la máquina o el entorno del usuario.

### <a name="financial-information"></a>Información financiera

Las aplicaciones no deben pedir a los usuarios que realicen pagos dentro de la interfaz de Teams. Los detalles de los instrumentos financieros no deben transmitirse a los usuarios a través de una interfaz de bots.

Usted puede enlazar con servicios de pago seguros y externos sólo si hizo la divulgación apropiada en sus condiciones de uso, directiva de privacidad, o cualquier página de perfil o sitio web antes de que el usuario aceptara usar la aplicación.

Las aplicaciones que se ejecutan en la versión de iOS o Android de Teams deben cumplir las siguientes directrices:

* Las aplicaciones no deben incluir compras dentro de la aplicación, ofertas de prueba o una interfaz de usuario que tenga como objetivo la venta de versiones de pago o enlaces a tiendas en línea donde los usuarios puedan comprar o adquirir otros contenidos, aplicaciones o complementos.
* Si su aplicación requiere una cuenta, los usuarios deben poder registrarse en una cuenta sin coste alguno. Se prohíbe el uso del término **gratuito** o **cuenta gratuita**.
* Puede determinar si una cuenta está activa indefinidamente o por un tiempo limitado, pero si la cuenta caduca, no se mostrará ninguna interfaz de usuario, texto o vínculos que indiquen la necesidad de pagar.
* La directiva de privacidad y las páginas de condiciones de uso de su aplicación deben estar libres de cualquier interfaz de usuario o enlace relacionado con el comercio.

## <a name="general-functionality-and-performance"></a>Funcionalidad y rendimiento general

### <a name="launching-external-functionality"></a>Lanzamiento de funcionalidades externas

Las aplicaciones no deben sacar a los usuarios de Teams para los escenarios de los usuarios principales El contenido de la aplicación y las interacciones pueden ocurrir dentro de las capacidades de Teams, como los bots, las tarjetas y los módulos de tareas.

Debe vincular a los usuarios en algún lugar de Teams y no a un sitio o aplicación externa. Para los escenarios que requieren funcionalidad externa, su aplicación debe tener permiso explícito del usuario para lanzar esa funcionalidad.

### <a name="compatibility"></a>Compatibilidad

Las aplicaciones deben ser totalmente funcionales en los siguientes sistemas operativos y exploradores:

* Microsoft Windows 7 y posterior
* macOS 10.10 y posterior.
* Microsoft Edge 12 y posterior
* Mozilla Firefox 47.0 y posterior
* Google Chrome 51.0 y posterior
* iOS 9.0 y posterior
* Android 4.4 y posterior

### <a name="response-time"></a>Tiempo respuesta

Las aplicaciones de Teams deben responder en un plazo razonable, que varía en función de la capacidad.

* Las pestañas deben responder antes de tres segundos o mostrar un mensaje de carga o advertencia.
* Los bots deben responder a las órdenes del usuario en dos segundos o mostrar un indicador de escritura.
* Las extensiones de mensajería deben responder a los comandos del usuario antes de cinco segundos.
* Las notificaciones deben aparecer en los cinco segundos siguientes a la acción del usuario.

## <a name="app-package-and-store-listing"></a>Paquete de aplicaciones y listado de tiendas

Los paquetes de aplicaciones deben tener un formato correcto e incluir toda la información y los componentes requeridos.

### <a name="app-manifest"></a>Manifiesto de la aplicación

El manifiesto de la aplicación Teams define las configuraciones de tu aplicación.

* Su manifiesto debe ajustarse al último esquema de manifiesto. Para más información, consulte la [referencia del manifiesto](~/resources/schema/manifest-schema.md).
* Si su aplicación incluye un bot o una extensión de mensajería, su manifiesto debe ser coherente con los metadatos de Bot Framework, incluidos el nombre del bot, el logotipo, el vínculo de la directiva de privacidad y el vínculo de las condiciones de servicio.
* Si la aplicación usa Azure Active Directory (Azure AD) para la autenticación, incluya el identificador de aplicación (cliente) Azure AD en el manifiesto. Para obtener más información, consulte la referencia [manifiesto](~/resources/schema/manifest-schema.md#webapplicationinfo).

### <a name="app-icons"></a>Iconos de la aplicación

Los iconos son uno de los principales elementos que la gente ve cuando navega por la tienda de Teams. Sus iconos deben comunicar la marca y el propósito de su aplicación, a la vez que se adhieren a los siguientes requisitos:

* El paquete de su aplicación debe incluir dos versiones PNG del icono de su aplicación: Un icono de color y un icono de contorno.
* La versión en color de su icono se muestra en la mayoría de los escenarios de Teams y debe tener 192x192 píxeles. Su símbolo de icono (96x96 píxeles) puede ser de cualquier color o colores, pero debe situarse sobre un fondo cuadrado sólido o totalmente transparente.
* La versión del contorno de su icono se muestra cuando su aplicación está en uso y se "eleva" en la barra de aplicaciones en el lado izquierdo de Teams y cuando un usuario fija la extensión de mensajería de su aplicación. Debe tener 32x32 píxeles y puede ser blanco con fondo transparente o transparente con fondo blanco (no se permiten otros colores). El icono no debe tener ningún relleno adicional alrededor del símbolo.
* El paquete de la aplicación debe incluir iconos de tamaño y formato correctos. Los iconos también deben coincidir con lo que se envía con los metadatos del listado de la tienda.

Para obtener más información, mejores prácticas y ejemplos, consulte las [directrices de los iconos](~/concepts/build-and-test/apps-package.md#app-icons) de la aplicación Teams.

### <a name="app-descriptions"></a>Descripciones de aplicaciones

Debe tener una descripción corta y larga de su aplicación. Las descripciones en las configuraciones de su aplicación y en el Centro de partners deben ser las mismas.

Las descripciones no deben despreciar directamente o mediante insinuaciones a otra marca (propiedad de Microsoft o no). Asegúrese de que su descripción no incluya afirmaciones que no puedan ser corroboradas (por ejemplo, "aumento garantizado del 200% de la eficiencia").

#### <a name="short-description"></a>Descripción breve

Una descripción breve es un resumen conciso de su aplicación que destaca su propuesta de valor y se dirige a su público objetivo.

**Sí:**

* Limite la descripción a una sola frase.
* Ponga la información más importante en primer lugar.
* Incluya palabras clave que los clientes probablemente busquen.

**No:**

* Repita el nombre de la aplicación.
* Use la palabra **aplicación** en la descripción breve.

#### <a name="long-description"></a>Descripción larga

La descripción larga puede proporcionar una narración atractiva que destaque la propuesta de valor de su aplicación, el público principal y el sector al que se dirige. Aunque esta descripción puede tener hasta 4 000 caracteres, la mayoría de los usuarios sólo leerán entre 300 y 500 palabras.

**Sí:**

* Use [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) para dar formato a la descripción.
* Use la voz activa y hable directamente a los usuarios. Por ejemplo, *Puede ...*.
* Enumere las características con viñetas para que sea más fácil escanear la descripción.
* Describa las limitaciones de forma clara, condiciones o excepciones a la funcionalidad, las características y los resultados descritos en el listado y los materiales relacionados antes de que el usuario instale su aplicación.. Las funciones de Teams que admita su aplicación deben estar relacionadas con las funciones principales que describe su listado.
* Asegúrese de que la descripción de la aplicación coincide con la funcionalidad disponible dentro de la aplicación Teams. Cualquier referencia a flujos de trabajo fuera de la aplicación Teams debe estar limitada y debe llamarse de forma clara desde la funcionalidad de la aplicación Teams.
* Incluya un vínculo de ayuda o soporte.
* Consulte **Microsoft 365** en lugar de **Office 365**.
* Si necesita hacer referencia a **Teams**, escriba la primera referencia como **Microsoft Teams**. Las referencias posteriores pueden acortarse a **Teams**.
* Use el siguiente lenguaje cuando describa cómo funciona la aplicación con Teams (o Microsoft 365):
  * "... funciona con Microsoft Teams."
  * "... trabajando con Microsoft Teams."
  * "... dentro de Microsoft Teams."
  * "... para Microsoft Teams."
  * "... integrado con Microsoft Teams."
  * "... creado para... "
  * "... desarrollado para... "
  * "... diseñado para..."


**No:**

* Superar las 500 palabras.
* Abreviar **Microsoft** como **MS** o **MSFT**.
* Indicar que la aplicación es una oferta de Microsoft, incluyendo el uso de eslóganes o etiquetas de Microsoft.
* Usar nombres de marcas con derechos de autor que no son de su propiedad.
 * Usar el siguiente lenguaje a menos que sea un partner certificado de Microsoft:
  * "... certificado para ..."
  * "... proporcionado por ..."
* Incluir errores tipográficos, gramaticales y mayúsculas innecesarias, como **Usuarios** en lugar de **usuarios.**
* Incluir vínculos a AppSource.
* Incluir afirmaciones no comprobadas (por ejemplo: mejor, superior, clasificada), a menos que vaya acompañada por la fuente de dicha afirmación.
* Comparar la oferta con otras ofertas del marketplace.



### <a name="screenshots"></a>Capturas de pantalla

Las capturas de pantalla proporcionan una destacada vista previa de su aplicación que complementa al nombre, el icono y las descripciones de la misma:

* Puede tener hasta cinco capturas de pantalla por anuncio.
* Los tipos de archivo admitidos son PNG, JPEG y GIF.
* Las dimensiones deben ser de 1366x768 píxeles.
* Tamaño máximo de 1 024 KB.

**Sí:**

* Concéntrese en las capacidades de su aplicación (por ejemplo, cómo la gente puede comunicarse con su bot).
* Incluya contenidos que representen con precisión su aplicación.
* Use el texto con juicio.
* Enmarque las capturas de pantalla con un color que refleje su marca e incluya contenido de marketing, similar al ejemplo del [listado de Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) (los requisitos de dimensión se aplican a toda la imagen y no sólo a la captura de pantalla).

**No:**

* Mostrar dispositivos específicos, como teléfonos o portátiles.
* Mostrar cromo o UI que no está en su aplicación.
* Capture cualquier equipo o interfaz de usuario del navegador en sus capturas de pantalla.
* Incluir maquetas que reflejen de forma imprecisa la interfaz de usuario real de la aplicación, por ejemplo, mostrando la aplicación fuera de Teams.

> [!TIP]
> Un vídeo puede ser la forma más eficaz de comunicar por qué la gente debería usar su aplicación. Un vídeo también es lo primero que ven los usuarios en su anuncio (de forma predeterminada, un vídeo aparece antes que las capturas de pantalla). Para obtener más información, consulte [crear un vídeo para mostrar la información su tienda](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video).

### <a name="privacy-policy"></a>Directiva de privacidad

La directiva de privacidad puede ser específica de la aplicación de Teams o una directiva general para todos los servicios.

* Si usa una plantilla de directiva de privacidad genérica, debe hacer referencia a los **servicios**, **aplicaciones**, y **plataformas** para incluir su aplicación de Teams y su servicio o sitio web.
* Debe incluir cómo maneja el almacenamiento, la retención y la eliminación de los datos de los usuarios. También debe describir los controles de seguridad que utiliza para la protección de datos.
* Debe incluir su información de contacto.
* No debe contener direcciones URL que estén rotas o para propósitos de beta o provisionales.
* No debe incluir vínculos a AppSource.

### <a name="terms-of-use"></a>Términos de uso

Sus condiciones de uso deben ser específicas y aplicables a su oferta.

### <a name="support-links"></a>Vínculos de soporte técnico

Las direcciones URL de soporte de su aplicación no deben requerir autenticación. Por ejemplo, los usuarios no deberían tener que iniciar sesión para ponerse en contacto con usted.

### <a name="localization"></a>Localización

Si su aplicación es compatible con la localización, el paquete de su aplicación debe incluir un archivo con traducciones de idiomas que se muestren en función de la configuración del idioma de Teams. El archivo debe ajustarse al esquema de localización de Teams. Para obtener más información, consulte el [esquema de localización de Teams](~/concepts/build-and-test/apps-localization.md).

## <a name="tabs"></a>Pestañas

Si su aplicación incluye una pestaña, asegúrese de que se adhiere a estas directrices.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulte las [directrices de diseño de la pestaña Teams](~/tabs/design/tabs.md).

### <a name="setup"></a>Instalación

* La configuración de las pestañas no debe ser un callejón sin salida para el nuevo usuario. Proporcionar un mensaje sobre cómo completar la acción o el flujo de trabajo.
* La autenticación debería producirse durante la configuración de la pestaña y no después.

### <a name="views"></a>Vistas

* El área de pantalla de inicio de sesión no debe utilizar logotipos grandes ni mostrar una página web completa.
* El contenido puede simplificarse dividiéndolo en varias pestañas.
* Las pestañas no deben tener un encabezado duplicado. Quite el logotipo del iframe, ya que el marco de pestañas ya muestra el icono y el nombre de la aplicación.

### <a name="navigation"></a>Navegación

* Las pestañas no deben tener más de tres niveles de navegación.
* Las pestañas no deben proporcionar una navegación que entre en conflicto con la navegación principal de Teams.
* Las páginas secundarias y terciarias de una pestaña deben abrirse en una vista de nivel dos y tres en el área de la pestaña principal, por la que se navega a través de rutas de navegación o de la navegación izquierda. También podría incluir los siguientes componentes para facilitar la navegación por pestañas:
    * Botones Atrás
    * Encabezados de página
    * Menús de hamburguesa
* La pestaña no debe tener desplazamiento horizontal.
* Los vínculos profundos en las pestañas no deben enlazar con una página web externa sino con algún sitio dentro de Teams. Por ejemplo, módulos de tareas u otras pestañas.
* Las pestañas no deben permitir a los usuarios navegar fuera de Teams para la experiencia de la aplicación principal.

### <a name="usability"></a>Facilidad de uso

* Las pestañas deben aportar un valor que vaya más allá del simple alojamiento de un sitio web existente.
* Los usuarios deben poder deshacer su última acción en la pestaña.
* Las pestañas en un contexto personal pueden agregar contenido de instancias compartidas de la aplicación.
* Las pestañas deben responder a los temas de Teams. Cuando un usuario cambia el tema, el tema de la aplicación debe reflejar la selección.
* Las pestañas deben utilizar, siempre que sea posible, componentes de estilo Teams, como fuentes, rampas tipográficas, paletas de colores, sistema de cuadrícula, movimiento, tono de voz, etc.
* Si la funcionalidad de la aplicación requiere cambios en la configuración, incluya una pestaña de **Configuración**.
* Las pestañas deben seguir el diseño de interacción de Teams, como la navegación dentro de la página, la posición y el uso de los diálogos, las jerarquías de información, etc., siempre que sea posible.
* El contenido de las pestañas en el iframe no debe incluir características que imiten las funciones principales de Teams. Por ejemplo, bots, extensiones de mensajería, llamadas, reuniones, etc.

> [!TIP]
>
> * Incluir un bot personal junto a una ficha personal.
> * Permitir a los usuarios compartir contenidos desde su pestaña personal.

## <a name="bots"></a>Bots

Si su aplicación incluye un bot, asegúrese de que se adhiere a estas directrices.

> [!TIP]
> Para obtener información sobre la creación de una experiencia de aplicación de alta calidad, consulte las [directrices de diseño del bot de Teams](~/bots/design/bots.md).

### <a name="bot-commands"></a>Comandos bot

Analizar las entradas del usuario y predecir sus intenciones es complicado. Los comandos de bot proporcionan a los usuarios un conjunto de palabras o frases que el bot entiende para que ni ellos ni el bot tengan que estar adivinando.

* Se recomienda encarecidamente incluir los comandos de bots compatibles en las configuraciones de la aplicación. Estos comandos aparecen en el cuadro de redacción cuando un usuario intenta enviar un mensaje a su bot.
* Todos los comandos que admite su bot deben funcionar correctamente, incluyendo el comando **Hola**, **Saludos**, y **Ayuda**.

> [!TIP]
> Para los bots personales, incluye una pestaña de **Ayuda** que describa con más detalle lo que puede hacer su bot.

### <a name="bot-welcome-messages"></a>Mensajes de bienvenida de los bots

* Los bots deberían enviar casi siempre un mensaje de bienvenida durante la primera ejecución. Para obtener la mejor experiencia, el mensaje debe incluir la propuesta de valor de su bot, cómo configurar el bot y describir brevemente todos los comandos de bot admitidos. Puede mostrar el mensaje mediante una tarjeta adaptable con botones para una mayor facilidad de uso. Para obtener más información, consulte [cómo activar un mensaje de bienvenida del bot](~/bots/how-to/conversations/send-proactive-messages.md).
* Los mensajes de bienvenida del bot en los canales y chats son opcionales durante la primera ejecución, especialmente si el bot está disponible para uso personal y realiza acciones similares. Si el bot envía mensajes de bienvenida, no debe enviarlos a los usuarios individualmente (esto se considera [correo no deseado](#bot-message-spamming)). El mensaje también debe mencionar a la persona que agregó el bot.
* Los bots de sólo notificación deben enviar un mensaje de bienvenida que transmita que no responderá a los mensajes de los usuarios.

> [!TIP]
> En los mensajes de bienvenida a los usuarios individuales, un recorrido en carrusel puede proporcionar una visión general eficaz de su bot y cualquier otra característica de la aplicación. Se recomienda incluir botones para que los usuarios prueben los comandos del bot. Por ejemplo, **Crear una tarea**.

### <a name="bot-message-spamming"></a>Mensajes de correo no deseado de bots

Los bots no deben hacer spam a los usuarios enviando múltiples mensajes en una corta sucesión.

* **Mensajes de bots en canales y chats**: No cree spam, enviando mensajes separados a los usuarios. Crear una publicación única con respuestas en el mismo hilo.
* **Mensajes bot en aplicaciones personales**: No envíe varios mensajes seguidos. Envíe un mensaje con la información completa. Evite las conversaciones extendidas para completar un único flujo de trabajo. En su lugar, considere la posibilidad de utilizar un formulario (o módulo de tareas) para recoger todas las entradas de un usuario de una sola vez.
* **Mensajes de bienvenida**: Repetir el mismo mensaje de bienvenida a intervalos regulares no está permitido y se considera correo no deseao. Por ejemplo, cuando se agrega un nuevo miembro a un equipo, no hay que enviar un mensaje de bienvenida a los demás miembros. En su lugar, envíe un mensaje personal al nuevo miembro.

### <a name="bot-notifications"></a>Notificaciones de bot

Las notificaciones del bot deben incluir contenido relevante para el ámbito que se defina para el bot (equipo, chat o personal).

### <a name="bots-and-adaptive-cards"></a>Bots y tarjetas adaptables

Las tarjetas adaptativas son una forma muy recomendable de mostrar los mensajes de los bots. Sus cartas deben ser ligeras e incluir sólo de 1 a 3 acciones. Si necesita mostrar más contenido, considere la posibilidad de utilizar un módulo de tareas o una pestaña.

Consulte los siguientes recursos para obtener más información:

* [Diseño de tarjetas adaptables](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Referencia de tarjetas](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

## <a name="messaging-extensions"></a>Extensiones de mensajería

Si su aplicación incluye una extensión de mensajería, asegúrese de que se adhiere a estas directrices.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de alta calidad en la aplicación, consulte las [Directrices de diseño de la extensión de mensajería de Teams](~/messaging-extensions/design/messaging-extension-design.md).

### <a name="action-commands"></a>Comandos de acción

Las extensiones de mensajería basadas en acciones deben hacer lo siguiente:

* Permitir a los usuarios desencadenar acciones en un mensaje sin completar pasos intermedios, como el inicio de sesión.
* Pasar el contexto del mensaje al siguiente estado de trabajo.

### <a name="preview-links-link-unfurling"></a>Vista previa de los vínculos (despliegue de vínculos)

Las extensiones de mensajería deberían previsualizar los vínculos reconocidos en el cuadro de redacción de Teams. No agregue dominios que estén fuera de su control (ya sean direcciones URL absolutas o comodines). Por ejemplo, `yourapp.onmicrosoft.com` es válido pero `*.onmicrosoft.com` no es válido. Los dominios de nivel superior también están prohibidos (por ejemplo, `*.com` o `*.org`).

### <a name="search-commands"></a>Comandos de búsqueda

* Las extensiones de mensajería basadas en la búsqueda deben proporcionar un texto que ayude a los usuarios a realizar una búsqueda eficaz.
* Los ejecutables de @mención deben ser claros, fáciles de entender y legibles.

## <a name="task-modules"></a>Módulos de tareas

Un módulo de tarea debe incluir un icono y el nombre corto de la aplicación a la que está asociado.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulte las [Directrices de diseño del módulo de tareas de Teams](~/task-modules-and-cards/task-modules/design-teams-task-modules.md).

## <a name="meeting-extensions"></a>Extensiones de reunión

Si su aplicación incluye una extensión de la reunión, asegúrese de que se cumplen estas directrices.

> [!TIP]
> Para obtener información sobre cómo crear una experiencia de aplicación de alta calidad, consulte las [Directrices de diseño de la extensión de la reunión de Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md).

### <a name="pre--and-post-meeting-experience"></a>Experiencia previa y posterior a la reunión

* Las pantallas previas y posteriores a la reunión deben respetar las directrices generales de diseño de las fichas. Para más información, consulte las [Directrices de diseño de Teams](~/tabs/design/tabs.md).
* Las pestañas no deben tener desplazamiento horizontal.
* Las pestañas deben tener un diseño organizado cuando se muestran varios elementos. Por ejemplo, más de 10 encuestas o sondeos. Vea un [diseño de ejemplo](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).
* Su aplicación debe notificar a los usuarios cuando se exporten los resultados de una encuesta o sondeo indicando: "Resultados descargados con éxito".

### <a name="in-meeting-experience"></a>Experiencia en la reunión

* Las aplicaciones sólo deben utilizar un tema oscuro durante las reuniones. Para más información, consulte las [Directrices de diseño de Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming).
* La información sobre herramientas debería mostrar el nombre de la aplicación cuando se pasa por encima del icono de la misma durante las reuniones.
* Las extensiones de mensajería deben funcionar igual durante las reuniones que fuera de ellas.

### <a name="in-meeting-tabs"></a>Pestañas en la reunión

* Deben tener capacidad de respuesta. Asegúrese de mantener el espaciado y los tamaños del componente.
* Debe tener un botón para volver atrás si hay más de una capa de navegación.
* No debe incluir más de un botón de descartar o cerrar. Esto puede confundir a los usuarios, puesto que ya existe un botón de encabezado para descartar la pestaña.
* No debe tener desplazamiento horizontal.

### <a name="in-meeting-dialogs"></a>Diálogos en las reuniones

* Debe usarse con moderación y para escenarios simples y orientados a las tareas.
* Debe mostrar el contenido en una sola columna y no tener varios niveles de navegación.
* No debe utilizar módulos de tareas.
* Debe alinearse con el centro del escenario de la reunión.
* Debe ser descartado una vez que el usuario selecciona un botón o realiza una acción.

## <a name="notifications"></a>Notificaciones

Si su aplicación utiliza las [API de alimentación de actividad proporcionadas por Microsoft Graph](/graph/teams-send-activityfeednotifications), asegúrese de que cumplen las siguientes directrices.

### <a name="general"></a>General

* Todos los activadores de notificaciones especificados en las configuraciones de su aplicación deberían recibir una notificación en la aplicación.
* Las notificaciones deben estar localizadas según los idiomas admitidos configurados para su aplicación.
* Las notificaciones deben aparecer en los cinco segundos siguientes a la acción del usuario.

### <a name="avatars"></a>Avatares

* El avatar de la notificación debe coincidir con el icono de color de su aplicación.
* Las notificaciones activadas por un usuario deben incluir el avatar del mismo.

### <a name="spamming"></a>Correo no deseado

* Las aplicaciones no deben enviar más de 10 notificaciones por minuto a un usuario.
* Los bots y la fuente de actividades no deberían provocar notificaciones duplicadas.
* Las notificaciones deben aportar algún valor a los usuarios y no ser utilizadas para eventos triviales o irrelevantes.

### <a name="navigation-and-layout"></a>Navegación y diseño

* Las notificaciones deben ceñirse al diseño y la experiencia de la alimentación de la actividad de Teams.
* Al seleccionar una notificación, el usuario debe ser dirigido al contenido relevante dentro de Teams y no ser sacado de la experiencia de Teams.

## <a name="advertising"></a>Publicidad

Las aplicaciones no deben mostrar publicidad, incluidos los anuncios dinámicos, los banners y los anuncios en los mensajes.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una cuenta del Centro de partners](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
