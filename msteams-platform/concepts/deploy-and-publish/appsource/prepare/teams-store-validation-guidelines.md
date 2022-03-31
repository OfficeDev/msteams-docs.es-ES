---
title: Directrices de validación de la tienda de Microsoft Teams
description: Describe las directrices que debe seguir toda aplicación enviada a la tienda de Teams (AppSource).
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: c395324daba877b0e8f6030f4929dbbe5ce0dc6f
ms.sourcegitcommit: d9daad3d5818d5774911b96fdc7bde45b04c9908
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2022
ms.locfileid: "64511255"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Directrices de validación de la tienda de Microsoft Teams

Seguir estas directrices aumenta las posibilidades de que la aplicación pase el proceso de envío de la tienda de Microsoft Teams. Las directrices específicas de Teams complementan las [directivas de certificación de marketplace comercial](/legal/marketplace/certification-policies) de Microsoft y se actualizan con frecuencia para reflejar nuevas funcionalidades, comentarios de los usuarios y cambios en las reglas de operación.

> [!NOTE]
>
> * Algunas directrices pueden no ser aplicables a su aplicación. Por ejemplo, si la aplicación no incluye un bot, puede omitir las directrices relacionadas con los bots.
> * Hemos cruzado estas directrices con las directivas de certificación comercial de Microsoft y hemos agregado Do’s y Don’ts con ejemplos de escenarios de superación o error encontrados en nuestro proceso de validación.
> * Algunas directrices se marcan como *Corrección obligatoria*. Si el envío de la aplicación no cumple estas directrices obligatorias, recibirás un informe de errores de nosotros con los pasos necesarios para remediarlos. El envío de la aplicación pasará la validación de la tienda de Microsoft Teams solo después de que haya corregido los problemas.
> * Otras directrices se marcan como *Solución sugerida*. Para obtener una experiencia de usuario ideal, le sugerimos que corrija los problemas; sin embargo, el envío de la aplicación no se bloqueará para que no se publique en la tienda de Teams, si decide no corregir los problemas.

## <a name="value-proposition"></a>Propuesta de valor

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de certificación comercial de Microsoft 1140.1](/legal/marketplace/certification-policies#11401-value-proposition-and-offer-requirements) y proporciona instrucciones adicionales a los desarrolladores de aplicaciones de Microsoft Teams sobre la propuesta de valor añadido de su oferta.

### <a name="app-name"></a>Nombre de la aplicación

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de certificación comercial 1140.1.1](/legal/marketplace/certification-policies#114011-app-name) de Microsoft y proporciona instrucciones adicionales a los desarrolladores sobre cómo asignar nombres a sus aplicaciones.

El nombre de una aplicación desempeña un papel fundamental a la hora de que los usuarios la descubran en la tienda. Usa las siguientes directrices para dar nombre a una aplicación:

* El nombre debe incluir términos relevantes para los usuarios.
* Los nombres de las características principales de Teams no deben incluirse en el nombre de la aplicación, como:  
  * **Chat**
  * **Contactos**
  * **Calendario**
  * **Llamadas**
  * **Files**
  * **Actividad**
  * **Aplicaciones**
  * **Help**
* Nombres comunes con prefijos o sufijos con el nombre del desarrollador. Por ejemplo, **Contoso Tasks** en lugar de **Tasks**.
* No debes usar **Teams** u otros nombres de productos de Microsoft como son Excel, PowerPoint, Word, OneDrive, SharePoint, OneNote, Azure, Surface, Xbox, etc., lo que podría indicar falsamente una marca conjunta o una venta conjunta. Para obtener más información sobre cómo hacer referencia a los productos y servicios de software de Microsoft, consulta [Microsoft Trademark y Brand Guidelines](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general).
* Si tu aplicación forma parte de una asociación oficial con Microsoft, el nombre de su aplicación debe ir en primer lugar (por ejemplo, **Contoso Connector para Microsoft Teams**).
* No debe copiar el nombre de una aplicación que aparece en la tienda u otra oferta en el mercado comercial.
* No debe contener términos profanos o despectivos. El nombre tampoco debe incluir un lenguaje racial o culturalmente insensible.
* Debe ser único. Si su aplicación (Contoso) aparece en la tienda de Microsoft Teams y Microsoft AppSource y desea enumerar otra aplicación específica de una geografía, como Contoso México, el envío debe cumplir los siguientes criterios:
  * Evoca la funcionalidad específica de la región de la aplicación en el título, los metadatos, la experiencia de la primera aplicación de respuesta y las secciones de ayuda. Por ejemplo, el título debe ser Contoso México. El título de la aplicación debe diferenciar claramente una aplicación ya existente del mismo desarrollador para evitar confusiones por parte del usuario final.
  * Al cargar el paquete de la aplicación en Centro de partners, seleccione el **mercado** adecuado en que la aplicación estará disponible en la sección **Disponibilidad**.

 > [!TIP]  
 > La personalización de marca de la aplicación en la tienda de Microsoft Teams y Microsoft AppSource incluyendo el nombre de la aplicación, el nombre del desarrollador, el icono de la aplicación, capturas de pantalla de Microsoft AppSource, vídeo, descripción breve y sitio web, ya sea por separado o juntos, no debe suplantar una oferta oficial de Microsoft a menos que la aplicación sea una oferta oficial de Microsoft 1P.

### <a name="suitable-for-workplace-consumption"></a>Apto para el consumo en el área de trabajo

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está en línea con el número de directiva de certificación comercial de Microsoft [1140.1.2](/legal/marketplace/certification-policies#114012-workplace-appropriateness), [100.8](/legal/marketplace/certification-policies#1008-significant-value) y [100.10](/legal/marketplace/certification-policies#10010-inappropriate-content) y proporciona instrucciones adicionales a los desarrolladores sobre la creación de aplicaciones adecuadas para el área de trabajo.

El contenido de la aplicación debe ser adecuado para consumo general en áreas de trabajo y seguir todas las restricciones enumeradas en las directivas de certificación del marketplace comercial. Están prohibidos los contenidos relacionados con la religión, la directiva, el juego y el entretenimiento prolongado.

La aplicación debe habilitar la colaboración en grupo, optimizar la productividad de la persona, o ambas cosas. Las aplicaciones destinadas a la unión y socialización de equipos deben ser colaborativas y estar diseñadas para múltiples participantes. Las aplicaciones no deben requerir una inversión de tiempo sustancial de más de 60 minutos por sesión ni afectar a la productividad.

### <a name="similar-platforms-and-services"></a>Plataformas y servicios similares

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la[ directiva de certificación de comercial de Microsoft 1140.1.3](/legal/marketplace/certification-policies#114013-other-platforms-and-services).

Las aplicaciones deben centrarse en la experiencia de Teams y no incluir los nombres, iconos o imágenes de otras plataformas o servicios de colaboración basados en chat similares dentro del contenido de la aplicación o en sus metadatos, a menos que la aplicación proporcione interoperabilidad específica.

### <a name="feature-names"></a>Nombres de características

Los nombres de las características de la aplicación en botones y demás texto de la interfaz de usuario no deben duplicarse con terminología reservada para Teams u otros productos de Microsoft. Por ejemplo, **Iniciar reunión**, **Realizar llamada**, o **Iniciar chat**. Si es necesario, incluya el nombre de la aplicación, como puede ser **Start Contoso meeting**.

### <a name="authentication"></a>Autenticación

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de certificación comercial de Microsoft 1140.1.4](/legal/marketplace/certification-policies#114014-access-to-services) y proporciona instrucciones a los desarrolladores sobre la autenticación de sus aplicaciones con servicios externos.

Para obtener más información sobre cómo implementar la autenticación de aplicaciones, vea [autenticación en Teams](~/concepts/authentication/authentication.md).

#### <a name="authenticating-with-external-services"></a>Autenticación con servicios externos

Si la aplicación autentica a los usuarios con un servicio externo, siga estas instrucciones:

* **Iniciar sesión, cerrar sesión y registrar experiencias**:
  * Las aplicaciones que dependen de cuentas o servicios externos deben proporcionar una experiencia de inicio de sesión, cierre de sesión y registro clara y sencilla.
  * Cuando los usuarios cierran la sesión, deben cerrar sesión solo desde la aplicación y seguir con sesión iniciada en Teams.
  * Las aplicaciones que dependen de cuentas o servicios externos deben ofrecer una manera de que los nuevos usuarios se registren o se ponga en contacto con el editor de la aplicación para obtener más información sobre los servicios y obtener acceso a los servicios.
  El camino a seguir debe estar disponible en el manifiesto de la aplicación, la descripción larga de AppSource y la experiencia de primera ejecución de la aplicación (mensaje de bienvenida del bot, configuración de pestañas o página de configuración).
  * Las aplicaciones que requieren que el administrador de inquilinos complete una instalación única deben llamar a la dependencia del administrador de inquilinos para configurar la aplicación (antes de que cualquier otro usuario del inquilino pueda instalar y usar la aplicación).  
  Se debe destacar la dependencia en el manifiesto de la aplicación, la descripción larga de AppSource, todos los puntos de contacto de la experiencia de primera ejecución (mensaje de bienvenida del bot, configuración de pestañas o página de configuración), texto de ayuda según se considere necesario como parte de la respuesta del bot, la extensión de redacción o el contenido de pestañas estáticas.
  
* **Contenido de experiencias de uso compartido**: las aplicaciones que requieren autenticación con un servicio externo para compartir contenido en canales de Teams deben indicar claramente en la documentación de ayuda (o recursos similares) cómo desconectar o dejar de compartir contenido si esa característica es compatible con el servicio externo. Esto no significa que la capacidad de no compartir contenido deba estar presente en la aplicación de Teams.

## <a name="security"></a>Seguridad


:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la[ directiva de certificación de comercial de Microsoft 1140.3](/legal/marketplace/certification-policies#11403-security).

### <a name="financial-information"></a>Información financiera

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de certificación comercial de Microsoft 1140.3.1 ](/legal/marketplace/certification-policies#114031-financial-transactions)y proporciona instrucciones sobre la transmisión de información financiera dentro de la interfaz de Teams y notifica a los desarrolladores de escenarios de pagos restringidos en la versión móvil (Android e iOS) de su aplicación de Teams.

Las aplicaciones no deben pedir a los usuarios que realicen pagos dentro de la interfaz de Teams y transmitan información financiera a los usuarios a través de una interfaz de bot.  

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![En pagos de la aplicación](~/assets/images/submission/validation-financial-information-1.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

Puede proporcionar un vínculo para proteger los servicios de pago externos solo si lo da a conocer en sus términos de uso, directiva de privacidad, página de perfil o sitio web antes de que el usuario acepte usar la aplicación.

No deberá facilitar los pagos a través de una aplicación para bienes o servicios prohibidos por [Directiva general número 100.10 Contenidos inapropiados](/legal/marketplace/certification-policies#10010-inappropriate-content).

Las aplicaciones que se ejecutan en la versión de iOS o Android de Teams deben cumplir las siguientes directrices:

* Las aplicaciones no deben incluir compras desde la aplicación, ofertas de prueba ni interfaz de usuario que pretendan incrementar ventas para usuarios a versiones de pago o tiendas en línea para comprar otros contenidos, aplicaciones o complementos.

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Compras desde la aplicación](~/assets/images/submission/validation-financial-information-in-app-purchase.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Tiendas en línea](~/assets/images/submission/validation-financial-information-online-stores.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Si la aplicación requiere una cuenta, los usuarios pueden registrarse para obtener una cuenta sin cargo alguno. Se prohíbe el uso del término **gratuito** o **cuenta gratuita**.
* Puede determinar si una cuenta está activa indefinidamente o durante un tiempo limitado. Cuando la cuenta expira, la aplicación no debe mostrar la interfaz de usuario, el texto ni los vínculos que indiquen la necesidad de pago.
* La directiva de privacidad y las condiciones de uso de la aplicación deben estar libres de cualquier interfaz de usuario o vínculo relacionado con comercio.

### <a name="bots"></a>Bots

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.3.2](/legal/marketplace/certification-policies#114032-bots-and-messaging-extension).

En el caso de las aplicaciones que utilizan el Azure Bot Service de Microsoft (como los bots y las extensiones de mensajería), debe seguir todos los requisitos definidos en los términos de [Microsoft Online Services](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).

Los bots siempre deben pedir permiso para cargar un archivo y mostrar un mensaje de confirmación.

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Mensaje de confirmación](~/assets/images/submission/validation-bot-confirmation-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="external-domains"></a>Dominios externos

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está en línea con la [directiva del marketplace comercial de Microsoft 1140.3.3](/legal/marketplace/certification-policies#114033-external-domains) y proporciona instrucciones para desarrolladores sobre el uso de dominios restringidos en la propiedad de manifiesto `validDomains`.

No incluya dominios fuera del control de la organización (incluidos los caracteres comodín) ni servicios de tunelización en las configuraciones de dominio de la aplicación. Entre las siguientes excepciones se incluyen:

* Si su aplicación utiliza la tarjeta OAuthCard de Azure Bot Service, debe incluirla `token.botframework.com` como dominio válido o el botón de **inicio de sesión** no funcionará.
* Si su aplicación depende de SharePoint, puede incluir el sitio raíz de SharePoint asociado como un dominio válido utilizando la `{teamSiteDomain}` propiedad de contexto.

#### <a name="government-community-cloud-listings"></a>Listados de Government Community Cloud

Para distribuir la aplicación a los usuarios de Government Community Cloud (GCC), el proceso de autenticación debe identificar y enrutar a los usuarios a una dirección URL específica o esperada de GCC, a la vez que se evitan listados duplicados en la tienda de Teams.

### <a name="sensitive-content"></a>Contenido confidencial

[*corrección obligatoria*]

La aplicación no debe publicar datos confidenciales, como son tarjetas de crédito, detalles de pagos financieros, estado de salud, seguimiento de contactos u otra información identificable personalmente entre un público no destinado a ver el contenido.

La aplicación debe advertir a los usuarios antes de descargar cualquier archivo o archivo ejecutable (.exe) en el equipo o entorno del usuario.

## <a name="general-functionality-and-performance"></a>Funcionalidad y rendimiento general

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4](/legal/marketplace/certification-policies#11404-functionality).

### <a name="launching-external-functionality"></a>Lanzamiento de funcionalidades externas

[*corrección obligatoria*]

Las aplicaciones no deben sacar a los usuarios de Teams para los escenarios de los usuarios principales El contenido de la aplicación y las interacciones deben producirse dentro de las funcionalidades de Teams, como son bots, tarjetas adaptables, pestañas y módulos de tareas.

Vincule a los usuarios dentro de la aplicación de Teams y no a un sitio o aplicación externos. En escenarios que requieran funcionalidad externa, la aplicación debe tener permiso de usuario explícito para iniciar la funcionalidad.

El texto de la interfaz de usuario del botón que inicia la funcionalidad externa debe incluir contenido para indicar que el usuario se ha extraído de la instancia de Teams. Por ejemplo, incluya texto como puede ser **This way to Contoso.com** o **View en Contoso.com**.

### <a name="compatibility"></a>Compatibilidad

[*corrección obligatoria*]

Las aplicaciones deben ser totalmente funcionales en las versiones más recientes de los siguientes sistemas operativos y exploradores:

* Microsoft Windows
* macOS
* Microsoft&nbsp;Edge
* Google Chrome
* iOS
* Android

La aplicación debe mostrar un mensaje de error correcto en exploradores y sistemas operativos no compatibles.

### <a name="response-time"></a>Tiempo respuesta

[*corrección obligatoria*]

Las aplicaciones de Teams deben responder en un período de tiempo razonable o mostrar un indicador de carga o escritura, o un mensaje o advertencia.

* Las pestañas deben responder en dos segundos o mostrar un mensaje de carga o una advertencia.
* Los bots deben responder a las órdenes del usuario en dos segundos o mostrar un indicador de escritura.
* Las extensiones de mensajería deben responder a los comandos de usuario en dos segundos.
* Las notificaciones deben mostrarse en los dos segundos siguientes a la acción del usuario.

## <a name="app-package-and-store-listing"></a>Paquete de aplicaciones y listado de tiendas

[*corrección obligatoria*]

Los paquetes de aplicaciones deben tener un formato correcto e incluir toda la información y los componentes requeridos.

> [!TIP]  
> Debes incluir las siguientes instrucciones de prueba detalladas para validar el envío de la aplicación:
>
> * **Pasos para configurar las cuentas de prueba de la aplicación** en caso de que la aplicación dependa de cuentas externas para la autenticación.
> * Resumen de **comportamiento esperado de la aplicación** para los flujos de trabajo principales en Teams.
> * **Describir claramente las limitaciones**, las condiciones o las excepciones a la funcionalidad, las características y los resultados de la aplicación, la descripción larga y los materiales relacionados.
> * **Énfasis en las consideraciones** para los evaluadores al validar el envío de la aplicación.  
> * **rellenar previamente las cuentas de prueba con datos ficticios** para facilitar las pruebas.

### <a name="app-manifest"></a>Manifiesto de la aplicación

[*corrección obligatoria*]

El manifiesto de la aplicación de Teams define la configuración de la aplicación.

* El manifiesto debe cumplir con un esquema de manifiesto publicado de forma pública. Para obtener más información, vea [referencia de manifiesto](~/resources/schema/manifest-schema.md). No deberá enviarse la aplicación con una versión preliminar del manifiesto.
* Si la aplicación incluye un bot o una extensión de mensajería, los detalles del manifiesto de la aplicación deben ser coherentes con los metadatos de Bot Framework, incluidos el nombre del bot, el logotipo, el vínculo a la directiva de privacidad y el vínculo a las condiciones de servicio.
* Si la aplicación usa Azure Active Directory para la autenticación, incluya el identificador de aplicación (cliente) Microsoft Azure Active Directory (Azure AD) en el manifiesto. Para obtener más información, consulte la [referencia del manifiesto](~/resources/schema/manifest-schema.md#webapplicationinfo).

### <a name="app-icons"></a>Iconos de la aplicación

[*corrección obligatoria*]

Los iconos son uno de los principales elementos que la gente ve cuando navega por la tienda de Teams. Los iconos deben comunicar la marca y el propósito de la aplicación a la vez que cumplen los siguientes requisitos:

* El paquete de la aplicación debe incluir dos versiones .png del icono de la aplicación: un icono de color y un icono de contorno.
* La versión de color del icono debe ser de 192 x 192 píxeles. El símbolo de icono puede ser cualquier color o colores, pero debe situarse sobre un fondo cuadrado sólido o totalmente transparente.
* La versión de esquema del icono se muestra en los escenarios siguientes:
  * Cuando la aplicación está en uso y **hospedada** en la barra de aplicaciones del lado izquierdo de Teams.
  * Cuando un usuario ancla la extensión de mensajería de la aplicación.

* El contorno debe ser de 32 x 32 píxeles y puede ser blanco con un fondo transparente o transparente con un fondo blanco. El icono no debe tener ningún relleno adicional alrededor del símbolo.

* El paquete de la aplicación debe incluir iconos con el formato y el tamaño correctos. Los iconos deben coincidir con la información de los metadatos de la descripción de la tienda.

Para obtener más información, vea [directrices sobre iconos](~/concepts/build-and-test/apps-package.md#app-icons).

### <a name="app-descriptions"></a>Descripciones de aplicaciones

Debe tener una descripción corta y larga de su aplicación. Las descripciones en las configuraciones de su aplicación y en el Centro de partners deben ser las mismas.

Las descripciones no deben desasignar directamente ni a través de insinuaciones otra marca (propiedad de Microsoft o de otro tipo). Cerciórese de que la descripción no incluya notificaciones que no se puedan sustanciar. Por ejemplo, **aumento garantizado del 200% en la eficiencia**.

#### <a name="short-description"></a>Descripción breve

Una descripción breve es un resumen conciso de su aplicación que destaca su propuesta de valor y se dirige a su público objetivo.

**Dos:**

* Limite la descripción a una sola frase.
* Ponga la información más importante en primer lugar.
* Incluya palabras clave que los clientes probablemente busquen.
* Haga un uso eficaz del límite de caracteres disponible. Por ejemplo, no repita el nombre de la aplicación.

**No:**

[*Corrección sugerida*]

Use la palabra **aplicación** en la descripción breve.

#### <a name="long-description"></a>Descripción larga

La descripción larga puede proporcionar una narración atractiva que destaque la propuesta de valor de su aplicación, el público principal y el sector al que se dirige. Aunque esta descripción puede tener hasta 4 000 caracteres, la mayoría de los usuarios sólo leerán entre 300 y 500 palabras.

**Dos:**

* Use [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) para dar formato a la descripción.
* Use la voz activa y hable directamente a los usuarios. Por ejemplo, **Puede ...**.
* Enumere las características con viñetas para que sea más fácil escanear la descripción.
* Describa claramente las limitaciones, características, condiciones o excepciones a la funcionalidad y los resultados en la lista y los materiales relacionados antes de que el usuario instale la aplicación. Las funcionalidades de Teams deben estar relacionadas con las funciones principales que se describen en la lista.
* Asegúrese de que la descripción de la aplicación coincide con la funcionalidad disponible dentro de la aplicación Teams. Cualquier referencia a flujos de trabajo fuera de la aplicación de Teams debe ser limitada y se debe denominar de forma distinta desde la funcionalidad de la aplicación de Teams.
* Incluya un vínculo de ayuda o soporte.
* Consulte **Microsoft 365** en lugar de **Office 365**.
* Si necesita hacer referencia a **Teams**, escriba la primera referencia como **Microsoft Teams**. Las referencias posteriores se pueden acortar a **Teams**.
* Use el siguiente lenguaje cuando describa cómo funciona la aplicación con Teams (o Microsoft 365):
  * **... funciona con Microsoft Teams.**
  * **... trabajar con Microsoft Teams.**
  * **... en Microsoft Teams.**
  * **... para Microsoft Teams.**
  * **... integrado con Microsoft Teams.**
  * **... creado para...**
  * **... desarrollado para...**
  * **.. diseñado para...**

**Don'ts:**

[*corrección obligatoria*]

* Superar las 500 palabras.
* Abreviar **Microsoft** como **MS** o **MSFT**.
* Indicar que la aplicación es una oferta de Microsoft, incluyendo el uso de eslóganes o etiquetas de Microsoft.
* Usar nombres de marca protegidos por copyrights que no posea.
* Usar el siguiente idioma a menos que sea un asociado certificado de Microsoft:
  * **... certificado para...**
  * **... con tecnología de ...**
* Incluir errores tipográficos y gramaticales.
* Poner en mayúsculas innecesariamente todo el manifiesto o la descripción larga de AppSource o el contenido de la aplicación.
* Incluir vínculos a AppSource.
* Realizar notificaciones no comprobadas. Por ejemplo, mejor, superior y clasificado, a menos que venga con el origen de la notificación.
* Comparar la oferta con otras ofertas del marketplace.

### <a name="screenshots"></a>Capturas de pantalla

Las capturas de pantalla proporcionan una vista previa visual destacada de la aplicación que complementa al nombre, el icono y las descripciones de la misma. Recuerde lo siguiente:

* Puede tener hasta cinco capturas de pantalla por anuncio.
* Los tipos de archivo admitidos son PNG, JPEG y GIF.
* Las dimensiones deben ser de 1366 x 768 píxeles.
* Tamaño máximo de 1 024 KB.

**Dos:**

* Céntrese en las funcionalidades de la aplicación. Por ejemplo, cómo los usuarios pueden comunicarse con el bot.
* Incluya contenidos que representen con precisión su aplicación.
* Use el texto con juicio.
* Capturas de pantalla enmarcadas con un color que refleja su marca e incluye contenido de marketing.

**Don'ts:**

[*Corrección sugerida*]

* Mostrar dispositivos específicos, como teléfonos o portátiles.
* Mostrar cromo o UI que no está en su aplicación.
* Capture cualquier equipo o interfaz de usuario del navegador en sus capturas de pantalla.
* Incluir maquetas que reflejen de forma imprecisa la interfaz de usuario real de la aplicación, por ejemplo, mostrando la aplicación fuera de Teams.

> [!TIP]  
> Un vídeo puede ser la manera más eficaz de comunicar por qué los usuarios deben usar la aplicación. Un vídeo también es lo primero que ven los usuarios en la descripción. Para obtener más información, consulte [crear un vídeo para mostrar la información su tienda](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video).

### <a name="privacy-policy"></a>Directiva de privacidad

[*corrección obligatoria*]

La directiva de privacidad puede ser específica de la aplicación de Teams o una directiva general para todos los servicios.

* Si usa una plantilla de directiva de privacidad genérica, debe agregar una referencia a **servicios**, **aplicaciones** o **plataformas en el ámbito de la directiva de privacidad**. No es necesario especificar la aplicación de Teams en el ámbito, si incluye una referencia a **servicios**, **aplicaciones** y **plataformas**. El proceso de validación de aplicaciones interpretará estas referencias para incluir la aplicación de Teams junto con otros servicios o sitios web.
* Debe incluir cómo maneja el almacenamiento, la retención y la eliminación de los datos de los usuarios. Debe describir los controles de seguridad para protección de datos.
* Debe incluir su información de contacto.
* No debe incluir direcciones URL que estén rotas o sean con fines beta o de ensayo.
* No debe incluir vínculos a AppSource.
* No debe requerir autenticación para acceder a la directiva de privacidad.
* No debe incluir vínculos a interfaces de usuario o tiendas comerciales.

### <a name="terms-of-use"></a>Términos de uso

[*corrección obligatoria*]

Use las siguientes directrices para escribir el Condiciones de uso:

* Debe ser específico y aplicable a su oferta.
* Debe estar hospedado en su propio dominio.
* Debe tener un vínculo seguro (HTTPS).
* El acceso a Condiciones de uso no debe requerir autenticación.

### <a name="support-links"></a>Vínculos de soporte técnico

Las direcciones URL de soporte técnico de la aplicación no deben requerir autenticación. Por ejemplo, los usuarios no podrán iniciar sesión para ponerse en contacto con usted.

Las direcciones URL de soporte técnico deben incluir los detalles de contacto o una forma de avanzar para que los usuarios generen una incidencia de soporte técnico. Por ejemplo, si la dirección URL de soporte técnico se hospeda en GitHub, la página de GitHub debe estar bajo su propiedad y debe incluir los detalles de contacto o una forma de avanzar para que los usuarios generen una incidencia de soporte técnico. [*corrección obligatoria*]

  ![Dirección URL de soporte](~/assets/images/submission/validation-supportlinks-authentication.png)  

### <a name="localization"></a>Localización

[*corrección obligatoria*]

Si su aplicación es compatible con la localización, el paquete de su aplicación debe incluir un archivo con traducciones de idiomas que se muestren en función de la configuración del idioma de Teams. El archivo debe ajustarse al esquema de localización de Teams. Para obtener más información, vea [esquema de localización de Teams](~/concepts/build-and-test/apps-localization.md).

## <a name="apps-linked-to-saas-offer"></a>Aplicaciones vinculadas a la oferta de SaaS

* Los ISV deben admitir la posibilidad de que varios usuarios (suscriptores) del mismo inquilino administren su propia suscripción y asignen licencias a los usuarios del inquilino.
*
 La oferta debe cumplir todos los [requisitos técnicos](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/include-saas-offer) para las aplicaciones de Teams vinculadas a una oferta de SaaS.
* Las aplicaciones de Teams vinculadas a la oferta de SaaS deben cumplir todos los requisitos definidos en [1000 Software as a Service (SaaS)](/legal/marketplace/certification-policies#1000-software-as-a-service-saas).
* `subscriptionOffer` detalles mencionados en el archivo de manifiesto deben ser correctos. En el manifiesto de la aplicación, agregue o actualice `subscriptionOffer` con valor añadido `publisherId.offerId`. Por ejemplo, si el identificador del publicador es `contoso1234` y el identificador de la oferta es `offer01`, el valor que especifique en el manifiesto de la aplicación debe ser `contoso1234.offer01`.
* La oferta de SaaS vinculada a la aplicación de Teams debe estar activa en AppSource y las ofertas de versión preliminar no se aceptan para la aprobación de la tienda.

### <a name="offer-metadata"></a>Ofrecer metadatos

* Los metadatos de la oferta deben coincidir en el manifiesto de Teams, la lista de aplicaciones de Teams en AppSource y la oferta de SaaS en AppSource.
* La aplicación de Teams y la oferta de SaaS deben pertenecer al mismo editor o desarrollador. La oferta de SaaS a la que se hace referencia en el manifiesto de la aplicación debe pertenecer al mismo publicador que la aplicación de Teams se envía al marketplace comercial.
* Como la oferta enviada es una aplicación de Teams vinculada a una oferta saaS, debe seleccionar **compras adicionales** como **Sí, mi producto requiere la compra de un servicio u ofrece compras adicionales desde la aplicación** en la sección de confituración de Centro de partners de su listado de ofertas.
* Las descripciones del plan y los detalles de precios deben proporcionar información suficiente para que los usuarios comprendan claramente los listados de ofertas.
* Las limitaciones, las dependencias de servicios adicionales y las excepciones a las características ofrecidas deben destacarse con precisión en las descripciones del plan.
* Las aplicaciones de Teams vinculadas a la oferta de SaaS están diseñadas para admitir licencias asignadas sobre la base de nombres y usuarios. A veces, la oferta de SaaS se crea con otro método o tiene flujos de compra especializados. Debe hacer mención claramente en los metadatos de la aplicación y los detalles del plan de suscripción sobre el método y los flujos de compra.
* La oferta de SaaS debe proporcionar mensajes e instrucciones a todos los usuarios en todos los estados aplicables de flujo de compra.

### <a name="saas-offer-home-page-and-license-management"></a>Página principal de la oferta de SaaS y administración de licencias  

* Ofrecer una introducción a los suscriptores sobre cómo usar el producto.
* Permitir que el suscriptor asigne licencias.
* Proporcione diferentes formas de interactuar con el soporte técnico para problemas, como preguntas más frecuentes, base de conocimientos y dirección de correo electrónico.
* Valide a los usuarios para asegurarse de que aún no tienen una licencia asignada a través de otro usuario.
* Notificar a los usuarios después de la asignación de licencias.
* Guíe a los usuarios a través del correo electrónico o el bot de chat de Teams sobre cómo agregar la aplicación a Teams y sobre cómo empezar.

### <a name="usability-and-functionality"></a>Facilidad de uso y funcionalidad  

* Después de adquirir y asignar licencias correctamente, debe proporcionar lo siguiente:
* Acceso a los usuarios para las características del plan suscrito.
* Valor añadido y ventajas significativas del plan de suscripción para los usuarios.
* Desde la aplicación de Teams, proporcione un vínculo a la página principal de la aplicación SaaS para que los suscriptores administren las licencias en el futuro.

### <a name="configure-and-test-saas-application"></a>Configuración y prueba de la aplicación SaaS

Si la configuración de la aplicación con fines de prueba es compleja, proporcione un documento funcional end-to-end, pasos de configuración de ofertas saaS vinculadas e instrucciones para la administración de licencias y usuarios como parte de las "Notas para la certificación".

> [!TIP]  
> Puede agregar un vídeo sobre cómo funciona la administración de licencias y aplicaciones para ayudar al equipo a realizar pruebas.

## <a name="tabs"></a>Pestañas

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.2](/legal/marketplace/certification-policies#114042-tabs).
Si la aplicación incluye una pestaña, cerciórese de que cumple estas directrices.
> [!TIP]
> Para obtener más información sobre cómo crear una experiencia de aplicación de alta calidad, consulte [Directrices de diseño de pestañas en Teams](~/tabs/design/tabs.md).

### <a name="setup"></a>Instalación

* La configuración de pestañas **no deberá dejar sin salida** a un nuevo usuario. Proporcionar un mensaje sobre cómo completar la acción o el flujo de trabajo. [*corrección obligatoria*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![Crear una cuenta nueva](~/assets/images/submission/validation-tabs-setup-create-new-account.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Falta la guía de reenvío](~/assets/images/submission/validation-tabs-missing-forward-guidance.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Nuevo registro de usuario](~/assets/images/submission/validation-tabs-setup-new-user.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Para obtener la mejor experiencia de primera ejecución, autentique a los usuarios durante la configuración de la pestaña y no después. La autenticación puede producirse fuera de la ventana de configuración de la pestaña. [*Corrección sugerida*]

* El usuario no debe dejar la experiencia de configuración de pestañas dentro de Teams para crear contenido fuera de Teams y, a continuación, volver a Teams para anclarlo. La pantalla de configuración de pestañas debe explicar el valor de la configuración y cómo realizar la configuración. [*corrección obligatoria*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![Adquirir nombre de perfil](~/assets/images/submission/validation-tabs-setup-profile-name.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* La pantalla de configuración de pestañas no debe insertar un sitio web completo. Mantenga su experiencia de configuración centrada. Por ejemplo, si va a crear una aplicación de administración de proyectos que permita a los usuarios configurar un proyecto en un canal, mantenga la pantalla de configuración de pestañas centrada en permitir que el usuario seleccione un proyecto de la aplicación para configurarlo en el canal. [*Corrección obligatoria*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![Experiencia de configuración](~/assets/images/submission/validation-tabs-setup-configuration-experience.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![Pantalla de configuración](~/assets/images/submission/validation-tabs-setup-configuration-screen.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* La pantalla de configuración de pestañas no debe pedir a los usuarios que inserten una dirección URL. Pedir a los usuarios que configuren una dirección URL durante la configuración de la pestaña es una experiencia de usuario rota, el usuario abandona la pantalla de configuración de pestañas, adquiere la dirección URL, vuelve a la pantalla de configuración y escribe la dirección URL. Una característica preexistnte de Teams ya permite a los usuarios anclar un vínculo de sitio web en el canal. Si la aplicación pide al usuario que inserte una dirección URL de sitio web durante la configuración de la pestaña y la aplicación está limitada a mostrar todo el contenido del sitio web en la pestaña del canal, la aplicación no ofrece un valor añadido significativo al usuario. [*corrección obligatoria*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![Dirección URL configurada](~/assets/images/submission/validation-tabs-setup-configured-url.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![Dirección URL configurada limitada](~/assets/images/submission/validation-tabs-setup-configured-url-two.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="views"></a>Vistas

* El área de pantalla de inicio de sesión no debe usar logotipos grandes. [*corrección obligatoria*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![Ver logotipo grande](~\assets\images\submission\validation-views-applogin.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* El contenido se puede simplificar desglosando en varias pestañas. [*Corrección sugerida*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![Varias pestañas](~/assets/images/submission/validation-views-multiple-tabs.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Las pestañas no deben tener un encabezado duplicado. Quite el logotipo duplicado del iframe, ya que el marco de pestañas ya muestra el icono y el nombre de la aplicación. [*Corrección sugerida*]

 :::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![Logotipo de encabezado duplicado](~/assets/images/submission/validation-views-duplicate-header-logo.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

### <a name="navigation"></a>Navegación

Estas son las directrices de navegación:

* Las pestañas no deben proporcionar una navegación que entre en conflicto con la navegación principal de Teams. Si proporciona un panel de navegación izquierdo en la pestaña, no debe incluir solo iconos o iconos con texto apilado. No debe ser un raíl contraíble con la opción de ver iconos con texto apilado (imitando la barra de navegación de Teams). Incluya iconos con texto en línea o solo texto, o use menús de hamburguesa en lugar del raíl izquierdo de la pestaña. [*corrección obligatoria*]

Diseñe su aplicación con componentes de UI Fluent [básicos](~/concepts/design/design-teams-app-basic-ui-components.md) y [avanzados](~\concepts\design\design-teams-app-advanced-ui-components.md).

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![Navegación izquierda](~/assets/images/submission/validation-navigation-left-navigation.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![Icono y texto](~/assets/images/submission/validation-navigation-icon-text.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Rail izquierdo contraible](~/assets/images/submission/validation-navigation-collapsable-left-rail.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Pestaña Estática](~/assets/images/submission/validation-navigation-static-tab.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Rail horizontal](~/assets/images/submission/validation-navigation-horizontal-rail.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Las pestañas con barra de herramientas en el raíl izquierdo deben dejar espaciado de 20 px desde el panel de navegación izquierdo de Teams. [*Corrección obligatoria*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Espaciado entre la barra de herramientas](~/assets/images/submission/validation-navigation-spacing-between-toolbar.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

* Las páginas secundarias y terciarias de una pestaña deben abrirse en una vista de nivel dos (L2) y nivel tres (L3) en el área de pestaña principal, que se navega a través de rutas de navegación o navegación izquierda. También puede incluir los siguientes componentes para facilitar la navegación por pestañas: [*Corrección obligatoria*]
  * Botones Atrás
  * Encabezados de página
  * Menús de hamburguesa
* La pestaña no debe tener un desplazamiento horizontal. Las aplicaciones de pizarra y otras aplicaciones que requieren un lienzo más grande para permitir a los usuarios colaborar sin una experiencia de aplicación interrumpida percibida, pueden usar el desplazamiento horizontal en función de sus necesidades empresariales. [*Corrección sugerida*]

* Los vínculos profundos de las pestañas no deben vincularse a una página web externa, sino dentro de Teams. Por ejemplo, módulos de tareas u otras pestañas. [*Corrección obligatoria*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Botón Ver no vinculado](~/assets/images/submission/validation-navigation-view-button-not-linked-static-tab.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Las pestañas no deben permitir que los usuarios naveguen fuera de Teams para la experiencia de la aplicación principal. Las pestañas pueden redirigir fuera de Teams para flujos de trabajo no principales. Por ejemplo, para generar una incidencia de soporte técnico. [*corrección obligatoria*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Flujo de trabajo principal en la pestaña Configuración](~/assets/images/submission/validation-navigation-core-workflow-within-configuration.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Flujo de trabajo principal de la aplicación redirige fuera](~/assets/images/submission/validation-navigation-core-workflow-redirects-outside.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="usability"></a>Facilidad de uso

* Las pestañas deben proporcionar valor añadido más allá de hospedar un sitio web ya existente. [*corrección obligatoria*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![La aplicación de facilidad de uso proporciona flujos de trabajo](~/assets/images/submission/validation-usability-app-provides-workflows.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![Marco I del sitio web sobre facilidad de uso](~/assets/images/submission/validation-usability-website-i-framed.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![Aplicación de Teams de facilidad de uso idéntica](~/assets/images/submission/validation-usability-teams-app-identical-website.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* El contenido no debe truncarse ni superponerse dentro de la pestaña.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![Truncamiento de contenido de facilidad de uso](~/assets/images/submission/validation-usability-content-truncation.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Los usuarios deben poder deshacer su última acción en la pestaña.

* Las pestañas en un contexto personal pueden agregar contenido de instancias compartidas de la aplicación. Por ejemplo, una aplicación de administración de proyectos con una pestaña configurable que permite a los miembros del canal comentar el proyecto en tarjetas Kanban debe agregar ese contenido y mostrarlo en la aplicación personal. [*Corrección sugerida*]

* Las pestañas deben responder a los temas de Teams. Cuando un usuario cambia el tema, el tema de la aplicación debe reflejar la selección.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![Pestañas con capacidad de respuesta de facilidad de uso](~/assets/images/submission/validation-usability-responsive-tabs.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![Pestañas que no responden a la facilidad de uso](~/assets/images/submission/validation-usability-unresponsive-tabs.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Las pestañas deben usar componentes de estilo Teams, como fuentes de Teams, rampas de tipos, paletas de colores, sistema de cuadrícula, movimiento, tono de voz, etc., siempre que sea posible. Para obtener más información, vea [Instrucciones para el diseño de pestañas](/microsoftteams/platform/tabs/design/tabs). [*Corrección sugerida*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Fuente diferente de facilidad de uso](~/assets/images/submission/validation-usability-app-uses-diff-font.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Si la funcionalidad de la aplicación requiere cambios en la configuración, incluya una pestaña de **Configuración**. [*Corrección sugerida*]
* Las pestañas deben seguir el diseño de interacción de Teams, como la navegación en la página, la posición y el uso de diálogos, jerarquías de información, etc. Para obtener más información, vea [ Kit de interfaz de usuario Fluent de Microsoft Teams](~/concepts/design/design-teams-app-basic-ui-components.md)

* El contenido de las pestañas en el iframe no debe incluir características que imiten las funciones principales de Teams. Por ejemplo, bots, extensiones de mensajería, llamadas, reuniones, etc.

* El contenido de la página de aterrizaje de las pestañas configurables debe ser contextualmente el mismo para todos los miembros del canal.

* El contenido de la página de aterrizaje de las pestañas configurables no debe tener como ámbito el uso individual y no incluir contenido personal, como **Mis tareas** o **Mi panel**.

* Si la aplicación requiere el aprovisionamiento de una vista de ámbito personal para que el usuario mejore la eficacia o la productividad del área de trabajo, use vistas filtradas, vínculos profundos a aplicaciones personales o navegue a las vistas L2 o L3 dentro de la pestaña configurable y mantenga la página de aterrizaje contextualmente igual para todos los usuarios.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![Información personal de la pestaña configurable de facilidad de uso](~/assets/images/submission/validation-usability-configurable-tab-personal-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

* Las pestañas configurables deben tener una funcionalidad centrada.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![Pestañas anidadas configurables de facilidad de uso](~/assets/images/submission/validation-usability-configurable-nested-tabs.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Las experiencias de pestañas deben tener una capacidad de respuesta total en dispositivos móviles (Android e iOS).

> [!TIP]
>
> * Incluir un bot personal junto a una ficha personal.
> * Permitir a los usuarios compartir contenidos desde su pestaña personal.

## <a name="bots"></a>Bots

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.3](/legal/marketplace/certification-policies#114043-bots).

Si la aplicación incluye un bot, cerciórese de que cumple estas directrices.

> [!TIP]
> Para obtener más información sobre cómo crear una experiencia de aplicación de alta calidad, consulte [directrices de diseño de bots de Teams](~/bots/design/bots.md).

### <a name="bot-commands"></a>Comandos bot

Analizar la entrada del usuario y predecir la intención del usuario es difícil. Los comandos de bot proporcionan a los usuarios un conjunto de palabras o frases para que el bot las entienda.

* Se recomienda encarecidamente incluir los comandos de bots compatibles en las configuraciones de la aplicación. Estos comandos aparecen en el cuadro de redacción cuando un usuario intenta enviar un mensaje a su bot.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![Comandos bot enumerados](~/assets/images/submission/validation-bot-commands-listed.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
  
:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![Comandos bot no enumerados](~/assets/images/submission/validation-bot-commands-not-listed.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Todos los comandos que admite el bot deben funcionar correctamente, incluidos los comandos genéricos como **Hi**, **Hello** y **Help**.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![Comando de ayuda del bot](~/assets/images/submission/validation-bot-help-command.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Los comandos de bot no deben llevar a un usuario a un punto de conexión, los comandos siempre deben proporcionar una forma de avanzar.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![Comando bot inactivo](~/assets/images/submission/validation-bot-commands-deadend.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

> [!TIP]
> Para los bots personales, incluye una pestaña de **Ayuda** que describa con más detalle lo que puede hacer su bot.

### <a name="bot-welcome-messages"></a>Mensajes de bienvenida de los bots

* Si la aplicación tiene un flujo de configuración complejo (requiere una licencia de empresa o carece de un flujo de registro intuitivo), los bots de estas aplicaciones siempre deben enviar un mensaje de bienvenida durante la primera ejecución. Para obtener la mejor experiencia, el mensaje de bienvenida debe incluir el valor que ofrece el bot a los usuarios, que instalaron el bot en el canal, cómo configurar el bot y describir brevemente todos los comandos de bot compatibles. Puede mostrar el mensaje de bienvenida con una tarjeta adaptable con botones para mejorar la facilidad de uso. Para obtener más información, consulte [cómo activar un mensaje de bienvenida del bot](~/bots/how-to/conversations/send-proactive-messages.md). En el caso de las aplicaciones sin un flujo de configuración complejo, puede elegir desencadenar un mensaje de bienvenida durante la primera experiencia de ejecución del bot. Sin embargo, si se desencadena un mensaje de bienvenida, debe seguir las instrucciones del mensaje de bienvenida.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Mensaje de bienvenida del bot](~/assets/images/submission/validation-bot-welcome-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![Bot sin mensaje de bienvenida](~/assets/images/submission/validation-bot-no-welcome-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Los mensajes de bienvenida del bot en los canales y chats son opcionales durante la primera ejecución, especialmente si el bot está disponible para uso personal y realiza acciones similares. El bot no debe enviar mensajes de bienvenida a los usuarios individualmente (se considera [correo no deseado](#bot-message-spamming)). El mensaje también debe mencionar a la persona que agregó el bot.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![Mensaje de bienvenida no desencadenado](~/assets/images/submission/validation-bot-welcome-message-not-triggered.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![Mensaje de bienvenida desencadenado](~/assets/images/submission/validation-bot-welcome-message-triggered.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

> [!TIP]
> En los mensajes de bienvenida a usuarios individuales, un paseo por el carrusel puede proporcionar una visión general eficaz del bot y cualquier otra característica de la aplicación para animar a los usuarios a probar los comandos bot. Por ejemplo, **Crear una tarea**.

### <a name="bot-message-spamming"></a>Mensajes de correo no deseado de bots

Los bots no deben enviar correo no deseado a los usuarios enviando varios mensajes a corto plazo.

* **Mensajes de bots en canales y chats**: No cree spam, enviando mensajes separados a los usuarios. Crear una publicación única con respuestas en el mismo hilo.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![Bot Spam Un Mensaje](~/assets/images/submission/validation-bot-message-spamming-one-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![Bot Spam Mensaje Múltiple](~/assets/images/submission/validation-bot-message-spamming-multiple-messages.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* **mensajes de bot en aplicaciones personales**:
  * No envíe varios mensajes en una duración rápida.
  * Envíe un mensaje con la información completa.
  * Evite las conversaciones de varios turnos para completar un único flujo de trabajo repetitivo.
  * Use un formulario (o módulo de tareas) para recopilar todas las entradas de un usuario a la vez.
  * Los bots de chat conversacionales basados en NLP pueden usar la conversación de varios turnos para que el diálogo sea más atractivo y complete un flujo de trabajo.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![Bot Utilizando Módulo de Tareas](~/assets/images/submission/validation-bot-messages-using-task-module.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![Bot que usa conversación múltiple](~/assets/images/submission/validation-bot-messages-using-mutliple-conversation.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* **Mensajes de bienvenida:** no repita el mismo mensaje de bienvenida en intervalos regulares. Por ejemplo, cuando se agrega un nuevo miembro a un equipo, no hay que enviar un mensaje de bienvenida a los demás miembros. Enviar un mensaje personalmente al nuevo miembro.

### <a name="bot-notifications"></a>Notificaciones de bot

Las notificaciones del bot deben incluir contenido relevante para el ámbito que se defina para el bot (equipo, chat o personal).

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![Notificación de bot relevante](~/assets/images/submission/validation-bot-notifications-relevant.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![Notificación de bot no relevante](~/assets/images/submission/validation-bot-notifications-not-relevant.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="bots-and-adaptive-cards"></a>Bots y tarjetas adaptables

Las tarjetas adaptativas son una forma muy recomendable de mostrar los mensajes de los bots. Las tarjetas deben ser ligeras y solo deben incluir un máximo de seis acciones. Para mostrar más contenido, considere la posibilidad de usar un módulo de tareas o una pestaña.

Para obtener más información acerca de las tarjetas, consulte:

* [Diseño de tarjetas adaptables](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Referencia de tarjetas](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

La experiencia del bot debe ser totalmente dinámica en dispositivos móviles. Las respuestas del bot deben proporcionar una manera de avanzar cuando corresponda. El bot debe responder y generar un error con un mensaje de error estable para los errores. Los mensajes de bot enviados en el ámbito personal a la base del usuario en los desencadenadores de un ámbito de colaboración deben proporcionar información contextual (incluido el origen del mensaje).

### <a name="notification-only-bots"></a>Bots de solo notificación

Las aplicaciones que constan de bots de solo notificación proporcionan valor añadido al usuario mediante el desencadenamiento de notificaciones de usuario basadas en determinados desencadenadores o eventos en la aplicación principal o el back-end. Por ejemplo, se agrega un nuevo cliente potencial para que el equipo de ventas realice un seguimiento.

Una notificación proporciona valor añadido en Teams si:

1. La tarjeta o el texto publicados proporcionan detalles adecuados que no requieren ninguna otra acción por parte del usuario.
1. La tarjeta o el texto publicados proporcionan información de vista previa adecuada para que un usuario tome medidas o decida ver más detalles en un vínculo que se abre fuera de Teams.

Las aplicaciones que proporcionan solo notificaciones con contenido como **Tienes una nueva notificación, haz clic para ver** y requieren que el usuario navegue fuera de Teams porque todo lo demás no proporciona un valor añadido significativo dentro de Teams.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![Información de bot inadecuada](~/assets/images/submission/validation-bot-notification-only-inadequete-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![Información de bot adecuada](~/assets/images/submission/validation-bot-notification-only-adequete-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

> [!TIP]
> Obtenga una vista previa de la información y proporcione acciones básicas de usuario insertadas en la tarjeta publicada para que el usuario no tenga que salir de Teams para realizar todas las acciones (independientemente de su complejidad).

## <a name="messaging-extensions"></a>Extensiones de mensajería

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.4](/legal/marketplace/certification-policies#114044-messaging-extensions).

Si la aplicación incluye una extensión de mensajería, cerciórese de que cumple estas directrices.

> [!TIP]
> Para obtener más información sobre cómo crear una experiencia de aplicación de alta calidad, vea las [directrices de diseño de extensiones de mensajería de Teams](~/messaging-extensions/design/messaging-extension-design.md).

### <a name="action-commands"></a>Comandos de acción

Las extensiones de mensajería basadas en acciones deben hacer lo siguiente:

* Permitir que los usuarios desencadenen acciones en un mensaje sin completar pasos intermedios, como es el inicio de sesión.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![Sin paso intermedio ](~/assets/images/submission/validation-messaging-extension-no-intermediate-step.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![Paso intermedio disponible](~/assets/images/submission/validation-messaging-extension-intermediate-step-available.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Pasar el contexto del mensaje al siguiente estado de trabajo. [*Corrección obligatoria*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![La aplicación pasa el mensaje](~/assets/images/submission/validation-messaging-extension-app-passes-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![La aplicación no pasa el mensaje](~/assets/images/submission/validation-messaging-extension-app-doesnot-pass-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Incorpore el nombre de la aplicación host en lugar de un verbo genérico para los comandos de acción que se desencadenan desde un mensaje de chat, una publicación de canal o una llamada a la acción dentro de las aplicaciones. Por ejemplo, use **Iniciar una reunión de Skype** para **Iniciar reunión**, **Cargar archivo en DocuSign** para **Cargar archivo**, etc. [*Corrección sugerida*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![Nombre de host del comando acción](~/assets/images/submission/validation-messaging-extension-action-command-host-name.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![Verbo Comando de acción](~/assets/images/submission/validation-messaging-extension-action-command-verb.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="preview-links-link-unfurling"></a>Vista previa de los vínculos (despliegue de vínculos)

Las extensiones de mensajería deben obtener una vista previa de los vínculos reconocidos en el cuadro de redacción de Teams. No agregue dominios que estén fuera de su control (direcciones URL absolutas o caracteres comodín). Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido. Los dominios de nivel superior también están prohibidos. Por ejemplo, `*.com` o `*.org`. [*corrección obligatoria*]

### <a name="search-commands"></a>Comandos de búsqueda

* Las extensiones de mensajería basadas en búsqueda deben proporcionar texto que ayude a los usuarios a buscar de forma eficaz. [*corrección obligatoria*]

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![Texto de ayuda disponible](~/assets/images/submission/validation-search-commands-text-available.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Los ejecutables de @mención deben ser claros, fáciles de entender y legibles.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![Comando de búsqueda no claro ejecutable](~/assets/images/submission/validation-search-command-unclear-executable.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="search-based-messaging-extension-only-apps"></a>Solo aplicaciones de extensión de mensajería basadas en búsquedas

[*corrección obligatoria*]

Las aplicaciones que constan de la extensión de mensajería basada en búsqueda proporcionan valor añadido al usuario mediante el uso compartido de tarjetas que permiten conversaciones contextuales sin cambiar de contexto.

Para pasar la validación de una aplicación solo de extensión de mensajes basada en búsqueda, se requiere lo siguiente como línea de base para garantizar que la experiencia del usuario no se interrumpa. Una tarjeta compartida a través de una extensión de mensajería proporciona valor añadido en Teams si:

1. La tarjeta publicada proporciona los detalles adecuados que no requieren ninguna otra acción por parte del usuario.
1. La tarjeta publicada proporciona información de vista previa adecuada para que un usuario tome medidas o decida ver más detalles en un vínculo que se abre fuera de Teams.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![Mensajería basada en búsqueda inadecuada](~/assets/images/submission/validation-search-based-messaging-ext-inadequete-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
   ![Mensajería adecuada basada en búsqueda](~/assets/images/submission/validation-search-based-messaging-ext-adequete-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

El desenlazamiento de vínculos de solo las aplicaciones no proporciona un valor añadido significativo en Teams. Considere la posibilidad de crear flujos de trabajo adicionales en la aplicación, si la aplicación solo admite la apertura de vínculos y no tiene ninguna otra funcionalidad.

## <a name="task-modules"></a>Módulos de tareas

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.5](/legal/marketplace/certification-policies#114045-task-modules).

Un módulo de tarea debe incluir un icono y el nombre corto de la aplicación a la que está asociado. Los módulos de tareas no deben insertar una aplicación completa y mostrar solo los componentes necesarios para completar una acción específica. [*corrección obligatoria*]

Para obtener más información, vea [las directrices de diseño de módulos de tareas de Teams](~\task-modules-and-cards\task-modules\design-teams-task-modules.md).

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![Módulo de tareas muestra componentes](~/assets/images/submission/validation-task-module-displays-components.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![Módulo de tareas incrusta aplicación](~/assets/images/submission/validation-task-module-embeds-app.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

> [!TIP]
> Para obtener más información sobre cómo crear una experiencia de aplicación de alta calidad, vea [directrices de diseño de módulos de tareas de Teams](~/task-modules-and-cards/task-modules/design-teams-task-modules.md).

## <a name="meeting-extensions"></a>Extensiones de reunión

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.6](/legal/marketplace/certification-policies#114046-meeting-extensions).
> [!TIP]
> Para obtener más información sobre cómo crear una experiencia de aplicación de alta calidad, vea las [directrices de diseño de la extensión de reuniones de Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md).

Use las siguientes directrices para las extensiones de reuniones:

* Las aplicaciones de extensibilidad de reuniones deben ofrecer una experiencia dinámica en la reunión y estar alineadas con la experiencia de reunión de Teams. La experiencia en la reunión es obligatoria, las experiencias previas y posteriores a la reunión no son obligatorias.

  * Con la experiencia de la aplicación previa a la reunión, los usuarios pueden buscar y agregar aplicaciones de reunión. Los usuarios también pueden realizar tareas previas a la reunión, como es desarrollar un sondeo para encuestar a los participantes de la reunión. Si la aplicación proporciona una experiencia previa a la reunión, debe ser relevante para el flujo de trabajo de la reunión.

  * Con la experiencia de la aplicación posterior a la reunión, los usuarios pueden ver los resultados de la reunión, como son los resultados de la encuesta de sondeo o los comentarios, así como otros contenidos de la aplicación. Si la aplicación proporciona una experiencia posterior a la reunión, debe ser relevante para el flujo de trabajo de la reunión.

  * Con la experiencia de la aplicación en la reunión, puede interactuar con los participantes de la reunión durante la reunión y mejorar la experiencia de la reunión para todos los asistentes. Los asistentes no deben estar fuera de la reunión de Teams para completar los flujos de trabajo de usuario principales de la aplicación.

* La aplicación debe ofrecer valor añadido que vaya más allá de proporcionar escenas personalizadas en Modo conferencia en Teams.

* La característica de fase de reunión compartida solo se puede iniciar a través de la aplicación de escritorio de Teams. Sin embargo, la experiencia de consumo de la fase de reunión compartida debe ser usable y no interrumpirse cuando se visualiza en dispositivos móviles.

> [!TIP]
> Debe declarar `groupchat` como ámbito bajo `configurableTabs` y `meetingDetailsTab`, o `meetingChatTab` y `meetingSidePanel` como propiedad de contenido en el manifiesto para habilitar su aplicación para reuniones en Teams móvil .

### <a name="pre-and-post-meeting-experience"></a>Experiencia previa y posterior a la reunión

* Las pantallas previas y posteriores a la reunión deben cumplir las directrices generales de diseño de pestañas. Para obtener más información, vea [las directrices de diseño de Teams](~/tabs/design/tabs.md).
* Las pestañas no deben tener desplazamiento horizontal.
* Las pestañas deben tener un diseño organizado cuando muestren varios elementos. Por ejemplo, más de 10 sondeos o encuestas, vea [diseño de ejemplo](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).
* La aplicación debe notificar a los usuarios cuándo se exportan los resultados de una encuesta o un sondeo indicando **resultados descargados correctamente**.

### <a name="in-meeting-experience"></a>Experiencia en la reunión

* Las aplicaciones sólo deben utilizar un tema oscuro durante las reuniones. Para obtener más información, vea [las directrices de diseño de Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming).
* Una información sobre herramientas debe mostrar el nombre de la aplicación cuando se mantenga el puntero sobre el icono de la aplicación durante las reuniones.

 :::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![Nombre de la aplicación para mostrar de información sobre herramientas](~/assets/images/submission/validation-in-meeting-exp-display-app-name.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Las extensiones de mensajería deben funcionar igual durante las reuniones que fuera de ellas.

### <a name="in-meeting-tabs"></a>Pestañas en la reunión

* Debe ser receptivo.
* Debe mantener el relleno y los tamaños de componentes.
* Debe tener un botón Atrás si hay más de una capa de navegación.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![Botón Atrás en la reunión Disponible](~/assets/images/submission/validation-in-meeting-exp-back-button.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![Botón atrás ausente en la reunión](~/assets/images/submission/validation-in-meeting-exp-back-button-absent.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* No debe incluir más de un botón cerrar. Puede confundir a los usuarios, ya que ya hay un botón de encabezado integrado para descartar la pestaña.
* No debe tener desplazamiento horizontal.

### <a name="in-meeting-dialogs"></a>Diálogos en las reuniones

* Debe usarse con moderación y para escenarios que sean ligeros y orientados a tareas.
* Debe mostrar el contenido en una sola columna y no tener varios niveles de navegación.
* No debe utilizar módulos de tareas.
* Debe alinearse con el centro del escenario de la reunión.

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![Cuadro de diálogo en reunión no alineado](~/assets/images/submission/validation-in-meeting-dialog-not-aligned.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* Debe descartarse después de que un usuario seleccione un botón o realice una acción.

* **Modo conferencia**: cerciórese de tener en cuenta los siguientes procedimientos recomendados para una experiencia de creación de escenas:
  * Todas las imágenes están en formato .png.
  * El paquete final con todas las imágenes juntas no debe superar la resolución de 1920 x 1080. La resolución es un número par. Esta resolución es un requisito para que las escenas se muestren correctamente.
  * El tamaño máximo de la escena es de 10 MB.
  * El tamaño máximo de cada imagen es de 5 MB. Una escena es una colección de varias imágenes. El límite es para cada imagen individual.
  * Seleccione **Transparente** según sea necesario. Esta casilla está disponible en el panel derecho cuando se selecciona una imagen. Las imágenes superpuestas deben marcarse como transparentes para indicar que se superponen en la escena.

## <a name="notifications"></a>Notificaciones

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.7](/legal/marketplace/certification-policies#114047-notification-apis).

Si la aplicación usa las [API de fuente de actividades proporcionadas por Microsoft Graph](/graph/teams-send-activityfeednotifications), cerciórese de que cumple las siguientes directrices.

### <a name="general"></a>General

* Todos los desencadenadores de notificación especificados en la configuración de la aplicación deben funcionar.
* Las notificaciones deben estar localizadas según los idiomas admitidos configurados para su aplicación.
* Las notificaciones deben aparecer en los cinco segundos siguientes a la acción del usuario.

### <a name="avatars"></a>Avatares

* El avatar de notificación debe coincidir con el icono de color de la aplicación.
* Las notificaciones desencadenadas por un usuario deben incluir el avatar del usuario.

### <a name="spamming"></a>Correo no deseado

* Las aplicaciones no deben enviar más de 10 notificaciones por minuto a un usuario.
* Los bots y la fuente de actividades no deben desencadenar notificaciones duplicadas.
* Las notificaciones deben aportar algún valor a los usuarios y no ser utilizadas para eventos triviales o irrelevantes.

### <a name="navigation-and-layout"></a>Navegación y diseño

* Las notificaciones deben ceñirse al diseño y la experiencia de la alimentación de la actividad de Teams.
* Al seleccionar una notificación, se debe dirigir al usuario al contenido relevante dentro de Teams.

## <a name="microsoft-365-app-compliance-program"></a>Programa de cumplimiento de aplicaciones de Microsoft 365

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la[directiva de marketplace comercial de Microsoft 1140.6](/legal/marketplace/certification-policies#11406-publisher-attestation).

El Programa de cumplimiento de aplicaciones de Microsoft 365 está destinado a ayudar a las organizaciones a evaluar y administrar el riesgo mediante la evaluación de la información de seguridad y cumplimiento de su aplicación. Si publica una aplicación en la tienda de Teams, debe completar los siguientes niveles del programa:

* **Verificación de editores**: Ayuda a los administradores y usuarios finales a comprender la autenticidad de los desarrolladores de aplicaciones que se integran en la plataforma de identidad de Microsoft. Cuando haya finalizado, se mostrará un distintivo de **verificado** en el cuadro de diálogo de consentimiento de Azure Active Directory y en otras pantallas. Para obtener más información, consulte [Marcar la aplicación como verificada por el publicador](/azure/active-directory/develop/mark-app-as-publisher-verified).  

:::row:::
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![Verificación del editor](~/assets/images/submission/validation-365-compliance-publisher-verification.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* **Certificación del editor**: Un proceso en el que usted comparte información general, de manejo de datos y de seguridad y cumplimiento para ayudar a los clientes potenciales a tomar decisiones informadas sobre el uso de su aplicación.

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Si presenta una aplicación que no ha sido incluida en la lista anteriormente, no puede completar oficialmente la certificación de editor hasta que su aplicación esté en la tienda de Teams. Si está actualizando una aplicación de la lista, complete el certificado de editor antes de enviar la última versión de la aplicación.

## <a name="advertising"></a>Publicidad

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png" border="false"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.7](/legal/marketplace/certification-policies#11407-advertising).

Las aplicaciones no deben mostrar publicidad, incluidos anuncios dinámicos, anuncios de banner y anuncios en el mensaje.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear una cuenta del Centro de partners](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)

## <a name="see-also"></a>Consulte también

* [Distribuir la aplicación](~/concepts/deploy-and-publish/apps-publish-overview.md)
* [Preparar el envío de la tienda](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [Prueba y depuración de la aplicación](~/concepts/build-and-test/debug.md)
* [Crear una cuenta de desarrollador del Centro de partners](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
