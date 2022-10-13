---
title: Directrices de validación de la tienda de Microsoft Teams
description: Sepa cómo aumentar las posibilidades de que la aplicación pase el proceso de envío de la tienda de Microsoft Teams. Comprenda las correcciones obligatorias y sugeridas. Explore las directrices de validación.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: 0a0151c72820baf1b6bd39ee00539cacbd3fa38b
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2022
ms.locfileid: "68561210"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Directrices de validación de la tienda de Microsoft Teams

Seguir estas directrices aumenta las posibilidades de que la aplicación pase el proceso de envío de la tienda de Microsoft Teams. Las directrices específicas de Teams complementan las [directivas de certificación de marketplace comercial](/legal/marketplace/certification-policies#1140-teams) de Microsoft y se actualizan con frecuencia para reflejar nuevas funcionalidades, comentarios de los usuarios y cambios en las reglas de operación.

> [!NOTE]
>
> * Algunas directrices pueden no ser aplicables a su aplicación. Por ejemplo, si la aplicación no incluye un bot, puede omitir las directrices relacionadas con los bots.
> * Hemos cruzado estas directrices con las directivas de certificación comercial de Microsoft y hemos agregado Do’s y Don’ts con ejemplos de escenarios de superación o error encontrados en nuestro proceso de validación.
> * Algunas directrices se marcan como *Corrección obligatoria*. Si el envío de la aplicación no cumple estas directrices obligatorias, recibirás un informe de errores de nosotros con los pasos necesarios para remediarlos. El envío de la aplicación pasará la validación de la tienda de Microsoft Teams solo después de que haya corregido los problemas.
> * Other guidelines are marked as *Suggested Fix*. For an ideal user experience, we suggest that you fix the issues, however, your app submission will not be blocked from publishing on the Teams store, if you choose not to fix the issues.

:::row:::
   :::column:::
      :::image type="icon" source="../../../../assets/icons/value-proposition.png" link="#value-proposition" border="false":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../../assets/icons/security.png" link="#security" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/function.png" link="#general-functionality-and-performance" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/package.png" link="#app-package-and-store-listing" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/saas-offer.PNG" link="#apps-linked-to-saas-offer" border="false":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/tab.png" link="#tabs" border="false":::
   :::column-end:::
   :::column:::
      :::image type="icon" source="../../../../assets/icons/bot.png" link="#bots-1" border="false":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../../assets/icons/messaging-extension.png" link="#message-extensions" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/task-module.png" link="#task-modules" border="false":::
   :::column-end:::
     :::column span="":::
      :::image type="icon" source="../../../../assets/icons/meeting.png" link="#meeting-extensions" border="false":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/notifications.png" link="#notifications" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/microsoft-365.png" link="#microsoft-365-app-compliance-program" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/advertising.png" link="#advertising" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/crypto-currency-based-apps-icon.png" link="#cryptocurrency-based-apps" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/app-functionality-icon.png" link="#app-functionality" border="false":::
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/mobile-experience-icon.png" link="#mobile-experience" border="false":::
   :::column-end:::
:::row-end:::

## <a name="value-proposition"></a>Propuesta de valor

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de certificación comercial de Microsoft 1140.1](/legal/marketplace/certification-policies#11401-value-proposition-and-offer-requirements) y proporciona instrucciones adicionales a los desarrolladores de aplicaciones de Microsoft Teams sobre la propuesta de valor añadido de su oferta.

### <a name="app-name"></a>Nombre de la aplicación

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de certificación comercial 1140.1.1](/legal/marketplace/certification-policies#114011-app-name) de Microsoft y proporciona instrucciones adicionales a los desarrolladores sobre cómo asignar nombres a sus aplicaciones.
<br></br>
<details><summary>Expandir para obtener más información</summary>

El nombre de una aplicación desempeña un papel fundamental a la hora de que los usuarios la descubran en la tienda. Usa las siguientes directrices para dar nombre a una aplicación:

* El nombre debe incluir términos relevantes para los usuarios.
* Nombres comunes con prefijos o sufijos con el nombre del desarrollador. Por ejemplo, **Contoso Tasks** en lugar de **Tasks**.
* No debe usar **Teams** ni otros nombres de producto de Microsoft, como Excel, PowerPoint, Word, OneDrive, SharePoint, OneNote, Azure, Surface y Xbox, que podrían indicar falsamente la co-marca o la venta conjunta. Para obtener más información sobre cómo hacer referencia a los productos y servicios de software de Microsoft, consulta [Microsoft Trademark y Brand Guidelines](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general).
* No debe copiar el nombre de una aplicación que aparece en la tienda u otra oferta en el mercado comercial.
* No debe contener términos profanos o despectivos. El nombre tampoco debe incluir un lenguaje racial o culturalmente insensible.
* Debe ser único. Si la aplicación (Contoso) aparece en la Tienda Microsoft Teams y Microsoft AppSource y quiere enumerar otra aplicación específica de una geografía como Contoso México, el envío debe cumplir los siguientes criterios:
  * Evoca la funcionalidad específica de la región de la aplicación en el título, los metadatos, la experiencia de la primera aplicación de respuesta y las secciones de ayuda. Por ejemplo, el título debe ser Contoso México. El título de la aplicación debe diferenciar claramente una aplicación ya existente del mismo desarrollador para evitar confusiones por parte del usuario final.
  * Al cargar el paquete de la aplicación en Centro de partners, seleccione el **mercado** adecuado en que la aplicación estará disponible en la sección **Disponibilidad**.

* El nombre de la aplicación no debe dirigirse con una característica básica de Teams, como Chat, Contactos, Calendario, Llamadas, Archivos, Actividad, Teams, Aplicaciones y Ayuda. El nombre de la aplicación puede acortarse a Chat, Contactos, Calendario, Llamadas, Archivos, Actividad, Teams, Aplicaciones y Ayuda en la instalación en la navegación izquierda.

* If your app is part of an official partnership with Microsoft, the name of your app must come first. For example, **Contoso Connector for Microsoft Teams**.

* El nombre de la aplicación no debe tener ninguna referencia a los productos de Microsoft o Microsoft. No use **Teams**, **Microsoft** o **App** en el nombre de la aplicación a menos que la aplicación esté en asociación oficial con Microsoft. En tal instancia, el nombre de la aplicación debe aparecer primero antes que cualquier referencia a Microsoft. Por ejemplo, **el conector de Contoso para Microsoft Teams**.

* No use paréntesis en la nomenclatura para incluir productos de Microsoft.

* El nombre del desarrollador debe ser el mismo en el manifiesto y AppSource.

* Los manifiestos de aplicación enviados deben ser manifiestos de producción. En consecuencia, el nombre de la aplicación no debe indicar que la aplicación es una aplicación de preproducción. Por ejemplo, el nombre de la aplicación no debe contener palabras como Beta, Desarrollo, Versión preliminar y UAT.

 > [!TIP]
 > La personalización de marca de la aplicación en la tienda de Microsoft Teams y AppSource, incluidos el nombre de la aplicación, el nombre del desarrollador, el icono de la aplicación, las capturas de pantalla de AppSource, el vídeo, la descripción breve y el sitio web por separado o tomados juntos, no deben suplantar una oferta oficial de Microsoft a menos que la aplicación sea una oferta oficial de Microsoft 1P.

</details>

### <a name="suitable-for-workplace-consumption"></a>Apto para el consumo en el área de trabajo

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está en línea con el número de directiva de certificación comercial de Microsoft [1140.1.2](/legal/marketplace/certification-policies#114012-workplace-appropriateness), [100.8](/legal/marketplace/certification-policies#1008-significant-value) y [100.10](/legal/marketplace/certification-policies#10010-inappropriate-content) y proporciona instrucciones adicionales a los desarrolladores sobre la creación de aplicaciones adecuadas para el área de trabajo.
<br></br>
<details><summary>Expandir para obtener más información</summary>

El contenido de la aplicación debe ser adecuado para consumo general en áreas de trabajo y seguir todas las restricciones enumeradas en las directivas de certificación del marketplace comercial. Están prohibidos los contenidos relacionados con la religión, la directiva, el juego y el entretenimiento prolongado.

La aplicación debe habilitar la colaboración en grupo, optimizar la productividad de la persona, o ambas cosas. Las aplicaciones destinadas a la unión y socialización de equipos deben ser colaborativas y estar diseñadas para múltiples participantes. Las aplicaciones no deben requerir una inversión de tiempo sustancial de más de 60 minutos por sesión ni afectar a la productividad.

</details>

### <a name="similar-platforms-and-services"></a>Plataformas y servicios similares

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la[ directiva de certificación de comercial de Microsoft 1140.1.3](/legal/marketplace/certification-policies#114013-other-platforms-and-services).

Las aplicaciones deben centrarse en la experiencia de Teams y no incluir los nombres, iconos o imágenes de otras plataformas o servicios de colaboración basados en chat similares dentro del contenido de la aplicación o en sus metadatos, a menos que la aplicación proporcione interoperabilidad específica.

### <a name="feature-names"></a>Nombres de características

Los nombres de características de la aplicación en botones y otro texto de interfaz de usuario no deben usar terminología reservada para Teams y otros productos de Microsoft. Por ejemplo, **Iniciar reunión**, **Realizar llamada** o **Iniciar chat** son nombres de características en uso por Microsoft en Microsoft Teams. Si es necesario, incluya el nombre de la aplicación para que la distinción sea clara, como **Iniciar reunión de Contoso**.

### <a name="authentication"></a>Autenticación

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de certificación comercial de Microsoft 1140.1.4](/legal/marketplace/certification-policies#114014-access-to-services) y proporciona instrucciones a los desarrolladores sobre la autenticación de sus aplicaciones con servicios externos.

Para obtener más información sobre cómo implementar la autenticación de aplicaciones, vea [autenticación en Teams](~/concepts/authentication/authentication.md).
<br></br>
<details><summary>Expandir para obtener más información</summary>

#### <a name="authenticating-with-external-services"></a>Autenticación con servicios externos

Si la aplicación autentica a los usuarios con un servicio externo, siga estas instrucciones:

* **Iniciar sesión, cerrar sesión y registrar experiencias**:
  * Las aplicaciones que dependen de cuentas o servicios externos deben proporcionar una experiencia de inicio de sesión, cierre de sesión y registro clara y sencilla.
  * Cuando los usuarios cierran la sesión, deben cerrar sesión solo desde la aplicación y seguir con sesión iniciada en Teams.
  * Las aplicaciones que dependen de cuentas o servicios externos deben ofrecer una manera de que los nuevos usuarios se registren o se ponga en contacto con el editor de la aplicación para obtener más información sobre los servicios y obtener acceso a los servicios.
  El camino a seguir debe estar disponible en el manifiesto de la aplicación, la descripción larga de AppSource y la experiencia de primera ejecución de la aplicación (mensaje de bienvenida del bot, configuración de pestañas o página de configuración).
  * Las aplicaciones que requieren que el administrador de inquilinos complete una instalación única deben llamar a la dependencia del administrador de inquilinos para configurar la aplicación (antes de que cualquier otro usuario del inquilino pueda instalar y usar la aplicación).
  Se debe destacar la dependencia en el manifiesto de la aplicación, la descripción larga de AppSource, todos los puntos de contacto de la experiencia de primera ejecución (mensaje de bienvenida del bot, configuración de pestañas o página de configuración), texto de ayuda según se considere necesario como parte de la respuesta del bot, la extensión de redacción o el contenido de pestañas estáticas.
  
* **Experiencias de uso compartido de contenidos**: las aplicaciones que requieren autenticación con un servicio externo para compartir contenido en canales de Teams deben indicar claramente en la documentación de ayuda (o en recursos similares) cómo desconectar o dejar de compartir contenidos si esa característica se admite en el servicio externo. Esto no significa que la capacidad de no compartir contenido deba estar presente en la aplicación de Teams.

</details>

## <a name="security"></a>Seguridad

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la[ directiva de certificación de comercial de Microsoft 1140.3](/legal/marketplace/certification-policies#11403-security).

### <a name="financial-information"></a>Información financiera

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está en línea con el [número de directiva de certificación comercial de Microsoft 1140.3.1](/legal/marketplace/certification-policies#114031-financial-transactions) y proporciona instrucciones sobre la transmisión de información financiera dentro de la interfaz de Teams y notifica a los desarrolladores los escenarios de pago restringidos en la versión móvil (Android e iOS) de su aplicación de Teams.
<br></br>
<details><summary>Expandir para obtener más información</summary>

Las aplicaciones no deben pedir a los usuarios que realicen pagos dentro de la interfaz de Teams y transmitan información financiera a los usuarios a través de una interfaz de bot.

:::image type="content" source="../../../../assets/images/submission/validation-financial-information-1.png" alt-text="validation-financial-info":::

Puede proporcionar un vínculo para proteger los servicios de pago externos solo si lo da a conocer en sus términos de uso, directiva de privacidad, página de perfil o sitio web antes de que el usuario acepte usar la aplicación.

No deberá facilitar los pagos a través de una aplicación para bienes o servicios prohibidos por [Directiva general número 100.10 Contenidos inapropiados](/legal/marketplace/certification-policies#10010-inappropriate-content).

Las aplicaciones que se ejecutan en la versión de iOS o Android de Teams deben cumplir las siguientes directrices:

* Las aplicaciones no deben incluir compras desde la aplicación, ofertas de prueba ni interfaz de usuario que pretendan incrementar ventas para usuarios a versiones de pago o tiendas en línea para comprar otros contenidos, aplicaciones o complementos.

    :::image type="content" source="../../../../assets/images/submission/validation-financial-information-in-app-purchase.png" alt-text="validation-financial-info-in-app-purchase":::

    :::image type="content" source="../../../../assets/images/submission/validation-financial-information-online-stores.png" alt-text="validation-online-store":::

* Si la aplicación requiere una cuenta, los usuarios pueden registrarse para obtener una cuenta sin cargo alguno. Se prohíbe el uso del término **gratuito** o **cuenta gratuita**.
* You can determine whether an account is active indefinitely or for a limited time. When the account expires the app must not show UI, text, or links indicating the need to pay.
* La directiva de privacidad y las condiciones de uso de la aplicación deben estar libres de cualquier interfaz de usuario o vínculo relacionado con comercio.

</details>

### <a name="bots"></a>Bots

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.3.2](/legal/marketplace/certification-policies#114032-bots-and-messaging-extension).
<br></br>
<details><summary>Expandir para obtener más información</summary>

En el caso de las aplicaciones que utilizan el Azure Bot Service de Microsoft (como los bots y las extensiones de mensaje), debe seguir todos los requisitos definidos en los términos de [Microsoft Online Services](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).

Los bots siempre deben pedir permiso para cargar un archivo y mostrar un mensaje de confirmación.

:::image type="content" source="../../../../assets/images/submission/validation-bot-confirmation-message.png" alt-text="validation-bot-confirmation":::

</details>

### <a name="external-domains"></a>Dominios externos

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está en línea con la [directiva del marketplace comercial de Microsoft 1140.3.3](/legal/marketplace/certification-policies#114033-external-domains) y proporciona instrucciones para desarrolladores sobre el uso de dominios restringidos en la propiedad de manifiesto `validDomains`.
<br></br>
<details><summary>Expandir para obtener más información</summary>

Don't include domains outside of your organization's control (including wildcards) and tunneling services in your app's domain configurations. The following exceptions include:

* Si su aplicación utiliza la tarjeta OAuthCard de Azure Bot Service, debe incluirla `token.botframework.com` como dominio válido o el botón de **inicio de sesión** no funcionará.
* Si su aplicación depende de SharePoint, puede incluir el sitio raíz de SharePoint asociado como un dominio válido utilizando la `{teamSiteDomain}` propiedad de contexto.
* No use dominios de nivel superior como **.com**, **.in** y **.org** como un dominio válido. [*corrección obligatoria*]

* No use **.onmicrosoft.com ni** como un dominio válido **donde onmicrosoft** no esté bajo su control. Sin embargo, puede usar **yoursite.com** como un dominio válido donde **el sitio esté** bajo su control aunque el dominio incluya un carácter comodín. [*corrección obligatoria*]

* Si la aplicación es una powerapp basada en Microsoft Power Platform, debe incluir *apps.powerapps.com* como un dominio válido para permitir que la aplicación sea accesible y funcional dentro de Teams.

</details>

### <a name="sensitive-content"></a>Contenido confidencial

[*corrección obligatoria*]

La aplicación no debe publicar datos confidenciales, como son tarjetas de crédito, detalles de pagos financieros, estado de salud, seguimiento de contactos u otra información identificable personalmente entre un público no destinado a ver el contenido.

La aplicación debe advertir a los usuarios antes de descargar cualquier archivo o archivo ejecutable (.exe) en el equipo o entorno del usuario.

## <a name="general-functionality-and-performance"></a>Funcionalidad y rendimiento general

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4](/legal/marketplace/certification-policies#11404-functionality).

* La guía de avance es obligatoria tanto para el administrador como para los usuarios existentes. Puede agregar instrucciones paso a paso como hipervínculos para registrarse, empezar, ponerse en contacto con nosotros, vínculos de ayuda o correo electrónico.
* No es necesario llamar a la dependencia o las limitaciones de la cuenta en la funcionalidad de la aplicación, pero es obligatorio agregarla en la descripción larga del manifiesto y en la descripción de la aplicación AppSource.
* Debe llamar a cualquier dependencia de los administradores de inquilinos para los nuevos usuarios. Si no hay ninguna dependencia, es obligatorio proporcionar un registro, ponerse en contacto con nosotros, un vínculo de introducción o un correo electrónico.

### <a name="launching-external-functionality"></a>Lanzamiento de funcionalidades externas

[*corrección obligatoria*]

Las aplicaciones no deben sacar a los usuarios de Teams para los escenarios de los usuarios principales El contenido de la aplicación y las interacciones deben producirse dentro de las funcionalidades de Teams, como son bots, tarjetas adaptables, pestañas y módulos de tareas.
<br>
</br>

<details><summary>Expandir para obtener más información</summary>

* Vincule a los usuarios dentro de la aplicación de Teams y no a un sitio o aplicación externos. En escenarios que requieran funcionalidad externa, la aplicación debe tener permiso de usuario explícito para iniciar la funcionalidad.

* El texto de la interfaz de usuario del botón que inicia la funcionalidad externa debe incluir contenido para indicar que el usuario se ha extraído de la instancia de Teams. Por ejemplo, incluya texto como puede ser **This way to Contoso.com** o **View en Contoso.com**.

* Agregue el icono **emergente** para que los usuarios sepan que se están navegando fuera de Teams. Puede usar el icono :::image type="icon" source="../../../../assets/icons/pop-out-icon.png" ::: emergente situado a la derecha del vínculo.

* Si no puede agregar un icono **emergente** , puede implementar cualquiera de las siguientes opciones para que el usuario sepa que se está navegando fuera de Teams:
  * Agregue una nota en Tarjeta adaptable que indica que, cuando los usuarios **seleccionan Obtener ayuda mediante esta aplicación**, lleva al usuario fuera de Teams.
  * Agregar diálogos intersticiales.

</details>

### <a name="compatibility"></a>Compatibilidad

[*corrección obligatoria*]

Las aplicaciones deben ser totalmente funcionales en las versiones más recientes de los siguientes sistemas operativos y exploradores:

* Microsoft Windows
* macOS
* Microsoft Edge
* Google Chrome
* iOS
* Android

La aplicación debe mostrar un mensaje de error correcto en exploradores y sistemas operativos no compatibles.

### <a name="response-time"></a>Tiempo respuesta

[*corrección obligatoria*]

Las aplicaciones de Teams deben responder en un período de tiempo razonable o mostrar un indicador de carga o escritura, o un mensaje o advertencia.

* Las pestañas deben responder en dos segundos o mostrar un mensaje de carga o una advertencia.
* Los bots deben responder a las órdenes del usuario en dos segundos o mostrar un indicador de escritura.
* Las extensiones de mensaje deben responder a los comandos de usuario en dos segundos.
* Las notificaciones deben mostrarse en los dos segundos siguientes a la acción del usuario.

## <a name="app-package-and-store-listing"></a>Paquete de aplicaciones y listado de tiendas

[*corrección obligatoria*]

Los paquetes de aplicaciones deben tener un formato correcto e incluir toda la información y los componentes requeridos.

> [!TIP]
>
> * Debe asegurarse de que las cuentas de prueba proporcionadas o el entorno de prueba sean válidos a perpetuidad, es decir, hasta que la aplicación esté activa en marketplace comercial.
> * Debes incluir las siguientes instrucciones de prueba detalladas para validar el envío de la aplicación:
>
>   * **Pasos para configurar las cuentas de prueba de la aplicación** en caso de que la aplicación dependa de cuentas externas para la autenticación.
>   * Resumen de **comportamiento esperado de la aplicación** para los flujos de trabajo principales en Teams.
>   * **Describir claramente las limitaciones**, las condiciones o las excepciones a la funcionalidad, las características y los resultados de la aplicación, la descripción larga y los materiales relacionados.
>   * **Énfasis en las consideraciones** para los evaluadores al validar el envío de la aplicación.
>   * **rellenar previamente las cuentas de prueba con datos ficticios** para facilitar las pruebas.
>   * Si va a proporcionar las cuentas de prueba, asegúrese de habilitar la integración de terceros. Además, deshabilite la autenticación en dos fases o multifactor.

### <a name="app-manifest"></a>Manifiesto de la aplicación

[*corrección obligatoria*]

El manifiesto de la aplicación de Teams define la configuración de la aplicación.

* El manifiesto debe cumplir con un esquema de manifiesto publicado de forma pública. Para obtener más información, vea [referencia de manifiesto](~/resources/schema/manifest-schema.md). No deberá enviarse la aplicación con una versión preliminar del manifiesto.
* Si la aplicación incluye un bot o una extensión de mensaje, los detalles del manifiesto de la aplicación deben ser coherentes con los metadatos de Bot Framework, incluidos el nombre del bot, el logotipo, el vínculo a la directiva de privacidad y el vínculo a las condiciones de servicio.
* Si la aplicación usa Azure Active Directory para la autenticación, incluya el identificador de aplicación (cliente) Microsoft Azure Active Directory (Azure AD) en el manifiesto. Para obtener más información, consulte la [referencia del manifiesto](~/resources/schema/manifest-schema.md#webapplicationinfo).

### <a name="uses-of-latest-manifest-schema"></a>Usos del esquema de manifiesto más reciente

* Si la aplicación usa el inicio de sesión único (SSO), debe declarar el identificador de Microsoft Azure Active Directory (Azure AD) en el manifiesto para la autenticación de usuario. [*corrección obligatoria*]

* Debe usar un esquema de manifiesto publicado públicamente. Puede actualizar el paquete de la aplicación para usar una versión pública del esquema de manifiesto 1.10 o posterior. [*corrección obligatoria*]

* Al enviar una actualización de la aplicación, solo aumenta el número de versión de la aplicación. El identificador de aplicación de la aplicación actualizada debe coincidir con el identificador de aplicación de la aplicación publicada. [*corrección obligatoria*]

* La presencia de archivos adicionales en el paquete de la aplicación no es aceptable. [*corrección obligatoria*]

* El número de versión debe ser el mismo en el esquema del archivo de manifiesto y en el esquema de manifiesto de idiomas adicionales. [*corrección obligatoria*]

* Debe usar la versión 1.5 o posterior del esquema de manifiesto de Teams para localizar la aplicación. Para usar la versión 1.5 o posterior del esquema de la aplicación en el archivo manifest.json, actualice el `$schema` atributo a la versión 1.5 o posterior. Actualice la propiedad a `$schema` la `manifestVersion` versión (1.5 en este caso). [*corrección obligatoria*]

* Al agregar, actualizar o quitar una funcionalidad existente, agregar o quitar metadatos del manifiesto o del Centro de partners, debe aumentar el número de versión de la aplicación y enviar el nuevo manifiesto de aplicación en la cuenta del Centro de partners para su validación.

* La cadena de versión debe seguir el estándar de especificación de control de versiones semántico (SemVer) (MAJOR. MENOR. PATCH). [*corrección obligatoria*]

* Si la aplicación requiere que los administradores revisen los permisos y concedan consentimiento en el Centro de administración de Teams, debe declarar `webapplicationinfo` en el manifiesto. Si `webapplicationinfo` no se declara en el manifiesto, la página **Permisos** de la aplicación en el Centro de administración de Teams se muestra como **...** [*Corrección obligatoria*]

* Como parte de la certificación de aplicaciones de Teams, debe enviar una versión de producción del manifiesto de la aplicación. [*corrección obligatoria*]

* Se recomienda declarar el identificador de Microsoft Partner Network (MPN) en el manifiesto. El id. de MPN ayuda a identificar la organización asociada que compila la aplicación. [*Corrección sugerida*]

### <a name="app-icons"></a>Iconos de la aplicación

[*corrección obligatoria*]

Los iconos son uno de los principales elementos que la gente ve cuando navega por la tienda de Teams.
<br></br>
<details><summary>Expandir para obtener más información</summary>

Los iconos deben comunicar la marca y el propósito de la aplicación a la vez que cumplen los siguientes requisitos:

* El paquete de la aplicación debe incluir dos versiones .png del icono de la aplicación: un icono de color y un icono de contorno.
* La versión de color del icono debe ser de 192 x 192 píxeles. El símbolo de icono puede ser cualquier color o colores, pero debe situarse sobre un fondo cuadrado sólido o totalmente transparente.
* La versión de esquema del icono se muestra en los escenarios siguientes:
  * Cuando la aplicación está en uso y **hospedada** en la barra de aplicaciones del lado izquierdo de Teams.
  * Cuando un usuario ancla la extensión de mensaje de la aplicación.

* El contorno debe ser de 32 x 32 píxeles y puede ser blanco con un fondo transparente o transparente con un fondo blanco. El icono no debe tener ningún relleno adicional alrededor del símbolo.

* El paquete de la aplicación debe incluir iconos con el formato y el tamaño correctos. Los iconos deben coincidir con la información de los metadatos de la descripción de la tienda.

Para obtener más información, vea [directrices sobre iconos](~/concepts/build-and-test/apps-package.md#app-icons).

</details>

### <a name="app-descriptions"></a>Descripciones de aplicaciones

Debe tener una descripción corta y larga para la aplicación. Las descripciones de la configuración de la aplicación y del Centro de partners deben ser las mismas.

:::image type="content" source="../../../../assets/images/submission/validation-app-description-adequete-information.png" alt-text="El gráfico muestra un ejemplo de descripción adecuada de la aplicación en la aplicación teams.":::

:::image type="content" source="../../../../assets/images/submission/validation-app-description-inadequete.png" alt-text="El gráfico muestra un escenario con errores para una descripción inadecuada de la aplicación.":::

<br></br>
<details><summary>Expandir para obtener más información</summary>

Las descripciones no deben desasignar directamente ni a través de insinuaciones otra marca (propiedad de Microsoft o de otro tipo). Asegúrese de que la descripción no incluya notificaciones que no se puedan justificar. Por ejemplo, **aumento garantizado del 200% en la eficiencia**.

* La descripción de la aplicación no debe contener información comparativa de marketing. Por ejemplo, no use logotipos o marcas comerciales de la competencia en la lista de ofertas, incluidas etiquetas u otros metadatos que hagan referencia a ofertas o marketplaces competidores. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-comparitive-marketing-fail.png" alt-text="El gráfico muestra un ejemplo de información comparativa de marketing en la descripción de la aplicación.":::

* Detalles de contacto de hipervínculo, introducción, ayuda o registro en la descripción de la aplicación.

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-contact-deatils-hyperlinked.png" alt-text="El gráfico muestra un ejemplo de detalles de contacto con hipervínculos en las descripciones de la aplicación.":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-contact-deatils-not-hyperlinked.png" alt-text="El gráfico muestra un ejemplo de detalles de contacto que no están hipervínculos en las descripciones de la aplicación.":::

* La descripción de la aplicación debe identificar al público deseado, explicar breve y claramente su valor único y distinto, identificar los productos de Microsoft admitidos y otro software e incluir los requisitos previos o requisitos para su uso. Debe describir claramente las limitaciones, condiciones o excepciones a la funcionalidad, características y entregas, como se describe en la lista y los materiales relacionados antes de que el cliente adquiera su oferta. Las funcionalidades que declare deben estar relacionadas con las funciones principales y la descripción de la oferta. [*corrección obligatoria*]

* Si actualiza el nombre de la aplicación, reemplace el nombre de la aplicación anterior por el nuevo nombre de la aplicación en los metadatos de la oferta en el manifiesto, AppSource y siempre que corresponda. [*corrección obligatoria*]

* Las limitaciones y las dependencias de la cuenta se deben señalar en el manifiesto Descripción de la aplicación, AppSource y Centro de partners. Por ejemplo:
  * Cuenta de empresa
  * Suscripción de pago
  * Otra licencia o cuenta
  * Idioma
  * Marcado de red telefónica conmutada (RTC)
  * Dependencia regional
  * Plazo para reservar traductores o agentes en directo
  * Funcionalidad basada en roles
  * Dependencia de la aplicación nativa

  :::image type="content" source="../../../../assets/images/submission/validation-app-description-limitations-calledout-pass.png" alt-text="El gráfico muestra un ejemplo de limitaciones que se indican en la descripción de la aplicación.":::
  
  :::image type="content" source="../../../../assets/images/submission/validation-app-description-limitations-not-calledout-fail.png" alt-text="El gráfico muestra un ejemplo de limitaciones no indicadas en las descripciones de la aplicación.":::

* Si la aplicación es compatible con regiones o ubicaciones geográficas específicas, debes llamar a esa dependencia de región específica en la descripción de la aplicación en manifiesto, Centro de partners y AppSource para esa oferta.

* Si necesita hacer referencia a Teams, escriba la primera referencia en la lista de aplicaciones como Microsoft Teams. Las referencias posteriores se pueden acortar a Teams.

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-teams-reference-pass.png" alt-text="El gráfico muestra un ejemplo de referencia correcta a Teams en la descripción de la aplicación.":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-teams-reference-fail.png" alt-text="El gráfico muestra un ejemplo de referencia incorrecta a Teams en la descripción de la aplicación.":::

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

* Asegúrese de que la descripción de la aplicación coincide con la funcionalidad disponible dentro de la aplicación de Teams. Cualquier referencia a flujos de trabajo fuera de la aplicación de Teams debe ser limitada y se debe denominar de forma distinta desde la funcionalidad de la aplicación de Teams.

* Incluya un vínculo de ayuda o soporte.

* Consulte **Microsoft 365** en lugar de **Office 365**.

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

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-microsoft-abbreviated.png" alt-text="El gráfico muestra un ejemplo de abreviatura de Microsoft como MS o MSFT por primera vez en la descripción de la aplicación.":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-microsoft-not-abbreviated.png" alt-text="El gráfico muestra un ejemplo de no abreviar Microsoft como MS o MSFT por primera vez en la descripción de la aplicación.":::

* Indicar que la aplicación es una oferta de Microsoft, incluyendo el uso de eslóganes o etiquetas de Microsoft.

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-offering-from-microsoft.png" alt-text="El gráfico muestra un ejemplo de cómo no indicar la oferta de Microsoft en la descripción de la aplicación.":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-no-offering-indication-from-microsoft.png" alt-text="Gráfico que muestra un ejemplo de cómo escribir la descripción de la aplicación sin usar eslóganes y etiquetas de Microsoft.":::

* Usar el siguiente idioma a menos que sea un asociado certificado de Microsoft:
  * **... certificado para...**
  * **... con tecnología de ...**
* Incluir errores tipográficos y gramaticales.
* Poner en mayúsculas innecesariamente todo el manifiesto o la descripción larga de AppSource o el contenido de la aplicación.

   :::image type="content" source="../../../../assets/images/submission/validation-long-description-typos-pass.png" alt-text="El gráfico muestra un ejemplo de descripción larga de la aplicación sin errores.":::

   :::image type="content" source="../../../../assets/images/submission/validation-long-description-typos-fail.png" alt-text="El gráfico muestra un ejemplo de descripción larga de la aplicación con errores tipográficos y .":::

* Incluir vínculos a AppSource.

  :::image type="content" source="../../../../assets/images/submission/validation-app-description-link-to-appsource.png" alt-text="El gráfico muestra un ejemplo de un escenario de error con vínculos a AppSource en la descripción larga de la aplicación.":::

* Realizar notificaciones no comprobadas. Por ejemplo, mejor, superior y clasificado, a menos que venga con el origen de la notificación.
* Comparar la oferta con otras ofertas del marketplace.

</details>

### <a name="screenshots"></a>Capturas de pantalla

Las capturas de pantalla proporcionan una destacada vista previa de su aplicación para complementar el nombre, el icono y las descripciones de la misma.
<br></br>
<details><summary>Expandir para obtener más información</summary>

Recuerde lo siguiente:

* Puede tener hasta cinco capturas de pantalla por anuncio.
* Los tipos de archivo admitidos son PNG, JPEG y GIF.
* Las dimensiones deben ser de 1366 x 768 píxeles.
* Tamaño máximo de 1 024 KB.

**Dos:**

* Focus on your app's capabilities. For example, how people can communicate with your bot.
* Incluya contenidos que representen con precisión su aplicación.
* Use el texto con juicio.
* Capturas de pantalla enmarcadas con un color que refleja su marca e incluye contenido de marketing.
* Use capturas de pantalla de alta resolución que sean nítidas y contengan texto legible y legible. [*corrección obligatoria*]
* Use simulacros que represente con precisión la interfaz de usuario real de la aplicación en beneficio de los usuarios finales. [*corrección obligatoria*]
* Proporcione al menos tres capturas de pantalla en la lista de Marketplace de la aplicación.
* Si la aplicación de Teams es extensible a otros centros de Microsoft 365, las capturas de pantalla proporcionadas deben representar la funcionalidad de la aplicación en otros centros de Microsoft 365.
* Al menos una captura de pantalla debe representar la funcionalidad de la aplicación en dispositivos móviles.
* Se recomienda proporcionar subtítulos en las capturas de pantalla para que el usuario comprenda claramente la funcionalidad de la aplicación.

**Don'ts:**

* Incluya simulacros que reflejen inexactamente la interfaz de usuario real de la aplicación, como mostrar que la aplicación se usa fuera de Teams.

> [!TIP]
>
> * Un vídeo puede ser la manera más eficaz de comunicar por qué los usuarios deben usar la aplicación. Un vídeo también es lo primero que ven los usuarios en la descripción.
> * Si decides proporcionar un vídeo en la descripción de la aplicación, debes desactivar los anuncios en la configuración de YouTube o Vimeo antes de enviar el vínculo de vídeo en el Centro de partners. Los vídeos proporcionados en la lista de aplicaciones no deben tener más de 90 segundos de duración y solo deben mostrar la funcionalidad de la aplicación y la integración con Microsoft Teams. Para obtener más información, consulte [crear un vídeo para mostrar la información su tienda](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video).

</details>

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

[*corrección obligatoria*]

Las direcciones URL de soporte técnico de la aplicación no deben requerir autenticación. Por ejemplo, los usuarios no podrán iniciar sesión para ponerse en contacto con usted.
<br></br>
<details><summary>Expandir para obtener más información</summary>

Las direcciones URL de soporte técnico deben incluir los detalles de contacto o una forma de avanzar para que los usuarios generen una incidencia de soporte técnico. Por ejemplo, si la dirección URL de soporte técnico se hospeda en GitHub, la página de GitHub debe estar bajo su propiedad y debe incluir los detalles de contacto o una forma de avanzar para que los usuarios generen una incidencia de soporte técnico.

:::image type="content" source="../../../../assets/images/submission/validation-supportlinks-authentication.png" alt-text="validation-support-links-auth":::

</details>

### <a name="localization"></a>Localización

[*corrección obligatoria*]

* Si su aplicación es compatible con la localización, el paquete de su aplicación debe incluir un archivo con traducciones de idiomas que se muestren en función de la configuración del idioma de Teams. El archivo debe ajustarse al esquema de localización de Teams. Para obtener más información, vea [esquema de localización de Teams](~/concepts/build-and-test/apps-localization.md).

* El contenido de metadatos de la aplicación debe ser el mismo en `en-us` y en otros lenguajes de localización. [*corrección obligatoria*]

* Los idiomas admitidos deben mostrarse en la descripción de la aplicación AppSource. Por ejemplo, esta aplicación está disponible en X (X= idioma localizado). [*corrección obligatoria*]

* Si la configuración de cliente del usuario no coincide con ninguno de los idiomas adicionales, el idioma predeterminado se usa como idioma de reserva final. Actualice la `localizationInfo` propiedad con el idioma predeterminado correcto que admite la aplicación. [*corrección obligatoria*]

* Actualice la `localizationInfo` propiedad con el idioma predeterminado correcto que admite la aplicación o agregue contenido localizado para el manifiesto y la descripción larga y breve del Centro de partners. [*corrección obligatoria*]

## <a name="apps-linked-to-saas-offer"></a>Aplicaciones vinculadas a la oferta de SaaS

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la[directiva de marketplace comercial de Microsoft 1140.5](/legal/marketplace/certification-policies?branch=pr-en-us-5673). Si va a crear una aplicación de Teams vinculada a una oferta de SaaS, asegúrese de que cumple estas directrices.
<br></br>
<details><summary>General</summary>

* Los ISV deben admitir la posibilidad de que varios usuarios (suscriptores) del mismo inquilino administren su propia suscripción y asignen licencias a los usuarios del inquilino.
* La oferta debe cumplir todos los [requisitos técnicos](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/include-saas-offer) para las aplicaciones de Teams vinculadas a una oferta de SaaS.
* Las aplicaciones de Teams vinculadas a la oferta de SaaS deben cumplir todos los requisitos definidos en [1000 Software as a Service (SaaS)](/legal/marketplace/certification-policies#1000-software-as-a-service-saas).
* `subscriptionOffer` detalles mencionados en el archivo de manifiesto deben ser correctos. En el manifiesto de la aplicación, agregue o actualice `subscriptionOffer` con valor añadido `publisherId.offerId`. Por ejemplo, si el identificador del publicador es `contoso1234` y el identificador de la oferta es `offer01`, el valor que especifique en el manifiesto de la aplicación debe ser `contoso1234.offer01`.
* La oferta de SaaS vinculada a la aplicación de Teams debe estar activa en AppSource y las ofertas de versión preliminar no se aceptan para la aprobación de la tienda.

</details>

</br>
<details><summary>Ofrecer metadatos</summary>

* Los metadatos de la oferta deben coincidir en el manifiesto de Teams, la lista de aplicaciones de Teams en AppSource y la oferta de SaaS en AppSource.
* La aplicación de Teams y la oferta de SaaS deben pertenecer al mismo editor o desarrollador. La oferta de SaaS a la que se hace referencia en el manifiesto de la aplicación debe pertenecer al mismo publicador que la aplicación de Teams se envía al marketplace comercial.
* Como la oferta enviada es una aplicación de Teams vinculada a una oferta saaS, debe seleccionar **compras adicionales** como **Sí, mi producto requiere la compra de un servicio u ofrece compras adicionales desde la aplicación** en la sección de confituración de Centro de partners de su listado de ofertas.
* Las descripciones del plan y los detalles de precios deben proporcionar información suficiente para que los usuarios comprendan claramente los listados de ofertas.
* Las limitaciones, las dependencias de servicios adicionales y las excepciones a las características ofrecidas deben destacarse con precisión en las descripciones del plan.
* Las aplicaciones de Teams vinculadas a la oferta de SaaS están diseñadas para admitir licencias asignadas sobre la base de nombres y usuarios. A veces, la oferta de SaaS se crea con otro método o tiene flujos de compra especializados. Debe hacer mención claramente en los metadatos de la aplicación y los detalles del plan de suscripción sobre el método y los flujos de compra.
* La oferta de SaaS debe proporcionar mensajes e instrucciones a todos los usuarios en todos los estados aplicables de flujo de compra.

</details>
</br>

<details><summary>Página principal de la oferta de SaaS y administración de licencias</summary>

* Ofrecer una introducción a los suscriptores sobre cómo usar el producto.
* Permitir que el suscriptor asigne licencias.
* Proporcione diferentes formas de interactuar con el soporte técnico para problemas, como preguntas más frecuentes, knowledge base y correo electrónico.
* Valide a los usuarios para asegurarse de que aún no tienen una licencia asignada a través de otro usuario.
* Notificar a los usuarios después de la asignación de licencias.
* Guía a los usuarios sobre cómo agregar la aplicación a Teams y empezar a usar el bot de chat o el correo electrónico de Teams.

</details>
</br>

<details><summary>Facilidad de uso y funcionalidad</summary>

* Después de adquirir y asignar licencias correctamente, debe proporcionar lo siguiente:
  * Acceso a los usuarios para las características del plan suscrito.
  * Valor añadido y ventajas significativas del plan de suscripción para los usuarios.
  * Desde la aplicación de Teams, proporcione un vínculo a la página principal de la aplicación SaaS para que los suscriptores administren las licencias en el futuro.

</details>
</br>

<details><summary>Configuración y prueba de la aplicación SaaS</summary>

Si la configuración de la aplicación con fines de prueba es compleja, proporcione un documento funcional de un extremo a otro, pasos de configuración de la oferta SaaS vinculada e instrucciones para la administración de licencias y usuarios como parte de *las notas para la certificación*.

> [!TIP]
> Puede agregar un vídeo sobre cómo funciona la administración de licencias y aplicaciones para ayudar al equipo a realizar pruebas.

</details>

## <a name="tabs"></a>Pestañas

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.2](/legal/marketplace/certification-policies#114042-tabs).
Si la aplicación incluye una pestaña, asegúrese de que cumple estas directrices.
> [!TIP]
> Para obtener más información sobre cómo crear una experiencia de aplicación de alta calidad, consulte [Directrices de diseño de pestañas en Teams](~/tabs/design/tabs.md).

</br>
<details><summary>Instalación</summary>

* La configuración de pestañas **no deberá dejar sin salida** a un nuevo usuario. Proporcionar un mensaje sobre cómo completar la acción o el flujo de trabajo. [*corrección obligatoria*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-new-user.png" alt-text="El gráfico muestra un ejemplo de Tab con un dead-end al configurar.":::

* El usuario no debe dejar la experiencia de configuración de pestaña dentro de Teams para crear contenido fuera de Teams y, a continuación, volver a Teams para anclarlo. La pantalla de configuración de pestañas debe explicar el valor de la configuración y cómo realizar la configuración. [*corrección obligatoria*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-profile-name.png" alt-text="validation-tabs-set-up-profile-name":::

* Tab configuration screen must not embed an entire website. Keep your configuration experience focused. For example, if you're building a project management app that lets users configure a project in a channel, keep the tab configuration screen focused on allowing the user to select a project from your app to configure in the channel. [*Mandatory Fix*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-experience.png" alt-text="validation-tabs-setup-configuration-exp":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-screen.png" alt-text="validation-tabs-set-up-configuration-screen":::

* Las aplicaciones que requieren que los usuarios escriban una dirección URL al configurar una pestaña deben:
  * Proporcione una guía de avance adecuada para que el usuario adquiera o genere la dirección URL. [*corrección obligatoria*]
  * Compruebe si la dirección URL es relevante o adecuada para la funcionalidad de la aplicación según la descripción de la aplicación. [*corrección obligatoria*]

    :::image type="content" source="../../../../assets/images/submission/validation-tab-configuration-way-forward-url-pass.png" alt-text="Captura de pantalla que muestra un ejemplo de configuración de tabulación con una manera de avanzar para que el usuario genere una dirección URL.":::
  
    :::image type="content" source="../../../../assets/images/submission/validation-tab-configuration-way-forward-url-fail.png" alt-text="Captura de pantalla que muestra un ejemplo de configuración de tabulación sin una manera de avanzar para que el usuario genere una dirección URL.":::

* Hipervínculo la información de contacto en la pantalla de configuración en lugar de texto sin formato para ayudar a los usuarios a ponerse en contacto con usted para conocer los requisitos de soporte técnico. [*corrección obligatoria*]

* Para una experiencia de usuario de primera ejecución sin problemas, se recomienda hipervínculo la dirección URL de soporte técnico o el correo electrónico en la pantalla de configuración. [*Corrección sugerida*]

</details>
</br>

<details><summary>Vistas</summary>

* The sign in screen area must not use large logos. [*Mandatory Fix*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-applogin.png" alt-text="validation-views-app-login":::

* El contenido se puede simplificar desglosándolo en varias pestañas.

    :::image type="content" source="../../../../assets/images/submission/validation-views-multiple-tabs.png" alt-text="val-views-multiple-tabs":::

* Las pestañas no deben tener un encabezado duplicado. Quite los logotipos duplicados del marco I, ya que el marco de tabulación ya muestra el icono y el nombre de la aplicación. [*Corrección sugerida*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-no-duplicate-header-logo.png" alt-text="El gráfico muestra un ejemplo de una pestaña sin encabezados y logotipos duplicados.":::

    :::image type="content" source="../../../../assets/images/submission/validation-views-duplicate-header-logo.png" alt-text="El gráfico muestra un ejemplo de una pestaña con encabezados y logotipos duplicados.":::

</details>
</br>

<details><summary>Navegación</summary>

Estas son las directrices de navegación:

* Las pestañas no deben proporcionar una navegación que entre en conflicto con la navegación principal de Teams. Si proporciona un panel de navegación izquierdo en la pestaña, no debe incluir solo iconos o iconos con texto apilado. No debe ser un raíl contraíble con la opción de ver iconos con texto apilado (imitando la barra de navegación de Teams). Incluya iconos con texto en línea o solo texto, o use menús de hamburguesa en lugar del raíl izquierdo de la pestaña. [*corrección obligatoria*]

Diseñe su aplicación con componentes de UI Fluent [básicos](~/concepts/design/design-teams-app-basic-ui-components.md) y [avanzados](~\concepts\design\design-teams-app-advanced-ui-components.md).

:::image type="content" source="../../../../assets/images/submission/validation-navigation-static-tab.png" alt-text="El gráfico muestra un ejemplo de navegación en una pestaña que no entra en conflicto con la navegación principal de Teams.":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-left-navigation.png" alt-text="El gráfico muestra un ejemplo de la barra de navegación izquierda que entra en conflicto con la navegación principal de Teams.":::

* Las pestañas con barra de herramientas en el raíl izquierdo deben dejar espaciado de 20 píxeles desde el panel de navegación izquierdo de Teams. [*corrección obligatoria*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-spacing-between-toolbar.png" alt-text="validation-nav-spacing-between-toolbar":::

* Las páginas secundarias y terciarias de una pestaña deben abrirse en una vista de nivel dos (L2) y nivel tres (L3) en el área de tabulación principal, que se navega a través de rutas de navegación o navegación izquierda. También puede usar los siguientes componentes para ayudar a la navegación en una pestaña:
  * Botones Atrás
  * Encabezados de página
  * Menús de hamburguesa

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-improper-navigation-leveles.png" alt-text="Captura de pantalla que muestra un ejemplo de diálogo en reunión con varios niveles de navegación.":::

* Los vínculos profundos de las pestañas no deben vincularse a una página web externa, sino dentro de Teams. Por ejemplo, módulos de tareas u otras pestañas. [*corrección obligatoria*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-view-button-not-linked-static-tab.png" alt-text="validation-nav-view-button-not-linked-static-tab":::

* Las pestañas no deben permitir que los usuarios naveguen fuera de Teams para la experiencia de la aplicación principal. Las pestañas pueden redirigir fuera de Teams para flujos de trabajo no principales. Por ejemplo, para generar una incidencia de soporte técnico. [*corrección obligatoria*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-within-configuration.png" alt-text="validation-nav-core-workflow-within-configuration":::

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-redirects-outside.png" alt-text="validation-nav-core-workflow-redirects-outside":::

* El desplazamiento horizontal no debe estar presente en una pestaña en la reunión. [*Corrección obligatoria*]

* Los diálogos en la reunión que se usan en la aplicación no deben permitir el desplazamiento horizontal. Use diálogos en reuniones con moderación y para escenarios que estén orientados a tareas y a la luz. Puede especificar el ancho del marco I del cuadro de diálogo en la reunión dentro del intervalo de tamaño admitido para tener en cuenta diferentes escenarios. [*corrección obligatoria*]
* Los módulos de tareas usados en la aplicación no deben permitir el desplazamiento horizontal. Los módulos de tareas permiten seleccionar diferentes tamaños para que el contenido responda sin necesidad de desplazamiento horizontal. Si es necesario, puede usar una vista de fase (un componente de interfaz de usuario de pantalla completa para exponer el contenido web) para completar el flujo de trabajo sin desplazamiento horizontal. [*corrección obligatoria*]

* No se permite el desplazamiento horizontal presente en la pestaña de una pestaña de detalles de chat, canal y reunión personales en cualquier ámbito si todo el lienzo de pestaña se puede desplazar, a menos que la pestaña use un lienzo infinito con elementos fijos de la interfaz de usuario. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-allowed-scenarios.png" alt-text="El gráfico muestra ejemplos de todos los escenarios en dispositivos móviles en los que se permite el desplazamiento horizontal.":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-allowed-kanban.png" alt-text="El gráfico muestra un ejemplo de desplazamiento horizontal en el panel Kanban.":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-list-view-components.png" alt-text="El gráfico muestra un ejemplo de vista de lista con muchos componentes.":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-fixed-board.png" alt-text="El gráfico muestra un ejemplo de desplazamiento horizontal en una pizarra blanca con lienzo infinito y placa fija.":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-in-list-view.png" alt-text="El gráfico muestra un ejemplo de desplazamiento horizontal en la vista de lista.":::

* El desplazamiento horizontal en tarjetas adaptables no debe estar presente en Teams. [*corrección obligatoria*]

* La barra inferior que se usa para la navegación en pestañas no debe entrar en conflicto con la navegación de aplicaciones móviles nativas de Teams. [*corrección obligatoria*]

  :::image type="content" source="../../../../assets/images/submission/validation-tab-bottom-rail-conflicts-with-teams-mobile.png" alt-text="El gráfico muestra un ejemplo de una pestaña que entra en conflicto con la navegación nativa de aplicaciones móviles de Teams.":::

</details>
</br>

<details><summary>Facilidad de uso</summary>

* Las pestañas deben proporcionar valor añadido más allá de hospedar un sitio web ya existente. [*corrección obligatoria*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-provides-workflows.png" alt-text="El gráfico muestra un ejemplo de una aplicación con un flujo de trabajo valioso para canalizar miembros dentro de un equipo.":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-website-i-framed.png" alt-text="El gráfico muestra un ejemplo de una aplicación con todo el sitio web en un marco I sin ninguna opción de retroceso.":::

* El contenido no debe truncarse ni superponerse dentro de la pestaña.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-content-truncation.png" alt-text="validation-usability-content-truncations":::

* Los usuarios deben poder deshacer su última acción en la pestaña.

* Las pestañas en un contexto personal pueden agregar contenido de instancias compartidas de la aplicación. Por ejemplo, una aplicación de administración de proyectos con una pestaña configurable que permite a los miembros del canal comentar el proyecto en tarjetas Kanban debe agregar ese contenido y mostrarlo en la aplicación personal. [*Corrección sugerida*]

* Las pestañas deben responder a los temas de Teams. Cuando un usuario cambia el tema, el tema de la aplicación debe reflejar la selección.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-responsive-tabs.png" alt-text="El gráfico muestra un ejemplo de una pestaña que responde a un tema en Teams.":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-unresponsive-tabs.png" alt-text="El gráfico muestra un ejemplo de una pestaña que no responde al tema en Teams.":::

* Las pestañas deben usar componentes con estilo de Teams, como fuentes de Teams, rampas de tipo, paletas de colores, sistema de cuadrícula, movimiento, tono de voz, siempre que sea posible. Para obtener más información, vea [directrices de diseño de pestañas](/microsoftteams/platform/tabs/design/tabs). [*Corrección sugerida*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-uses-diff-font.png" alt-text="Captura de pantalla que muestra un ejemplo de una pestaña con fuente calibri en lugar de una fuente nativa de Teams.":::

* Si la funcionalidad de la aplicación requiere cambios en la configuración, incluya una pestaña de **Configuración**. [*Corrección sugerida*]
* Las pestañas deben seguir el diseño de interacción de Teams, como la navegación en la página, la posición y el uso de diálogos, las jerarquías de información. Para obtener más información, consulte [Kit de interfaz de usuario de Microsoft Teams Fluent](~/concepts/design/design-teams-app-basic-ui-components.md).

* Las experiencias de pestañas deben tener una capacidad de respuesta total en dispositivos móviles (Android e iOS).

   > [!TIP]
   >
   > * Incluir un bot personal junto a una ficha personal.
   > * Permitir a los usuarios compartir contenidos desde su pestaña personal.

* Tab no debe contener elementos que obstruyan o impidan completamente los flujos de trabajo dentro de la pestaña. Por ejemplo, bot dentro de una pestaña que no se puede minimizar.

   :::image type="content" source="../../../../assets/images/submission/validation-tab-elements-impede-workflow.png" alt-text="El gráfico muestra un ejemplo de pestaña con elementos que impiden los flujos de trabajo dentro de la pestaña.":::

* La pestaña no debe tener una funcionalidad rota. Su oferta debe ser una solución de software utilizable y debe proporcionar la funcionalidad, las características y los resultados, tal como se describe en la descripción y otros materiales relacionados. [*corrección obligatoria*]

* Si las pestañas contienen un pie de página, asegúrese de quitar del pie de página todos los vínculos no relacionados con la funcionalidad de la aplicación.

</details>
</br>

<details><summary>Selección de ámbito</summary>

* El contenido de la página de aterrizaje de las pestañas configurables no debe tener como ámbito el uso individual y no incluir contenido personal, como **Mis tareas** o **Mi panel**.

   :::image type="content" source="../../../../assets/images/submission/validation-configurable-tab-content-personal-scope.png" alt-text="El gráfico muestra un ejemplo de contenido en una pestaña configurable con ámbito personal, como Mis tareas o Mi panel.":::

* Después de la experiencia de configuración, la página de aterrizaje debe mostrar una vista de colaboración para todo el equipo.

* Si la aplicación requiere el aprovisionamiento de una vista de ámbito personal para que el usuario mejore la eficacia o la productividad del área de trabajo, use vistas filtradas, vínculos profundos a aplicaciones personales o navegue a las vistas L2 o L3 dentro de la pestaña configurable y mantenga la página de aterrizaje contextualmente igual para todos los usuarios.

* El contenido de la página de aterrizaje de las pestañas configurables debe ser contextualmente el mismo para todos los miembros del canal.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-tab-personal-info.png" alt-text="El gráfico muestra un ejemplo de contenido en la página de aterrizaje de las pestañas configurables contextualmente diferentes para todos los miembros.":::

* Las pestañas configurables deben tener una funcionalidad centrada.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-nested-tabs.png" alt-text="validation-usability-configurable-nested-tab":::

</details>
<br/>

## <a name="bots"></a>Bots

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.3](/legal/marketplace/certification-policies#114043-bots).

Si la aplicación incluye un bot, asegúrese de que cumple estas directrices.

> [!TIP]
> Para obtener más información sobre cómo crear una experiencia de aplicación de alta calidad, consulte [directrices de diseño de bots de Teams](~/bots/design/bots.md).

</br>
<details><summary>Directrices de diseño de bots</summary>

* La aplicación de Teams debe seguir [las directrices de diseño del bot de Teams](../../../../bots/design/bots.md).

* Debe implementar un módulo de tareas para evitar la respuesta del bot de varios turnos cuando el flujo de trabajo implica al usuario realizar tareas repetitivas. Por ejemplo, use un módulo de tareas para capturar de forma repetitiva el nombre, el dob, el lugar y la designación en lugar de usar conversaciones de varios turnos. [*corrección obligatoria*]

* Los vínculos, respuestas o flujos de trabajo rotos de la aplicación deben corregirse. [*corrección obligatoria*]

</details>

</br>
<details><summary>Comandos bot</summary>

Analyzing user input and predicting user intent is difficult. Bot commands provide users a set of words or phrases for your bot to understand.

* Debe enumerar al menos un comando de bot compatible en la `{commandList}` sección del manifiesto de la aplicación. Estos comandos aparecen en el cuadro de redacción cuando un usuario intenta enviar un mensaje a su bot.

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-listed.png" alt-text="El gráfico muestra un ejemplo de comandos de bot enumerados en el manifiesto de la aplicación.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-not-listed.png" alt-text="El gráfico muestra un ejemplo de comandos de bot que no aparecen en el manifiesto de la aplicación.":::

* Todos los comandos que admite el bot deben funcionar correctamente, incluidos los comandos genéricos como **Hi**, **Hello** y **Help**.
  
  :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-generic-response-pass.png" alt-text="El gráfico muestra un ejemplo de bot que responde a comandos genéricos.":::

  :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-generic-no-response.png" alt-text="El gráfico muestra un ejemplo de bot sin respuesta a comandos genéricos.":::

* Los comandos de bot no deben llevar a un usuario a un punto de conexión, los comandos siempre deben proporcionar una forma de avanzar.

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-deadend.png" alt-text="validation-bot-commands-dead-end":::

* Debe enumerar al menos un comando de bot válido en la `items.commands.title` sección del manifiesto y agregar una descripción adecuada que proporcione claridad al usuario sobre el comando del bot y su uso. Los comandos de bot que aparecen en la `commandLists` sección de la superficie del manifiesto como comandos rellenados previamente en el menú de comandos del bot y proporcionan una manera de avanzar para que el nuevo usuario interactúe con el bot. [*corrección obligatoria*]

* La respuesta del bot no debe contener imágenes ni avatares oficiales de productos de Microsoft. Usa tus propios recursos en la aplicación. No se permite el uso de imágenes de producto de Microsoft en la aplicación. Solo puede copiar, modificar, distribuir, mostrar, licenciar o vender imágenes de producto protegidas por derechos de autor de Microsoft si se le concede permiso explícito dentro del contrato de licencia de End-User (CLUF), los términos de licencia que acompañan al contenido o en [las directrices de marca comercial y marca de Microsoft](https://www.microsoft.com/legal/intellectualproperty/trademarks). [*corrección obligatoria*]

* Los bots deben responder a los comandos del usuario sin mostrar un indicador de carga continua. [*corrección obligatoria*]

* La respuesta del comando bot help no debe redirigir al usuario fuera de Teams. La respuesta de comandos de ayuda del bot puede redirigir al usuario a un lienzo dentro de la aplicación teams o proporcionar una respuesta de avance en una tarjeta adaptable. [*corrección obligatoria*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-redirects-user-outside-teams.png" alt-text="El gráfico muestra un ejemplo de respuesta del bot que redirige al usuario fuera de Teams.":::

* Los bots siempre deben proporcionar una respuesta válida a una entrada del usuario, incluso si la entrada es irrelevante o incorrecta. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-valid-improper-input.png" alt-text="El gráfico muestra un ejemplo de una respuesta válida para un comando de bot incorrecto.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-improper-response-invalid-command.png" alt-text="El gráfico muestra un ejemplo de una respuesta no válida para un comando de bot incorrecto.":::

* Los caracteres especiales, como la barra diagonal (**/**), no deben ir precedidos de comandos de bot. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-special-characters.png" alt-text="El gráfico muestra un ejemplo de un escenario con errores en el que los caracteres especiales tienen como prefijo los comandos del bot.":::

* Los bots deben proporcionar una respuesta válida a los comandos de usuario no válidos. Los bots no deben enviar al usuario un error o mostrar un error si un usuario envía un comando de bot no válido. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-way-forward-for-invalid-command.png" alt-text="El gráfico muestra un ejemplo de bot que proporciona una manera de avanzar para un comando no válido.":::

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-bot-dead-end-invalid-command.png" alt-text="El gráfico muestra un ejemplo de un escenario con errores en el que un bot envía una misma respuesta para un comando válido y no válido.":::

* La funcionalidad del bot debe ser relevante para el ámbito en el que está instalado el bot y el bot debe proporcionar valor en el ámbito instalado. [*corrección obligatoria*]

* Los bots no deben contener comandos duplicados. [*corrección obligatoria*]

* Los bots no deben mostrar un indicador de escritura después de responder al comando del usuario, pero pueden mostrar un indicador de escritura mientras responden al comando del usuario. [*corrección obligatoria*]

* Los bots deben proporcionar una respuesta válida al comando **de ayuda** escrito en minúsculas o en mayúsculas que proporcione al usuario una manera de avanzar o permita al usuario acceder al contenido de ayuda relacionado con el uso del bot. Los bots deben proporcionar una respuesta válida incluso cuando el usuario no haya iniciado sesión en la aplicación. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-valid-response-lowercase.png" alt-text="El gráfico muestra un ejemplo de bot que no proporciona una respuesta válida para un comando en minúsculas o en mayúsculas.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-valid-response-logged-app.png" alt-text="El gráfico muestra un ejemplo de un bot sin una respuesta válida cuando el usuario no ha iniciado sesión en la aplicación.":::

* Los bots deben proporcionar una respuesta válida para **ayudar** al comando.

   :::image type="content" source="../../../../assets/images/submission/validation-bot-help-command.png" alt-text="El gráfico muestra un ejemplo de bot que envía una respuesta válida para el comando help.":::

* Las respuestas de bot en dispositivos móviles deben responder sin ningún truncamiento de datos que entorpece el uso del bot del usuario final para completar los flujos de trabajo deseados. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-no-truncate-mobile.png" alt-text="El gráfico muestra un ejemplo de un mensaje de bot sin truncarse en el móvil.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-truncate-mobile.png" alt-text="El gráfico muestra un ejemplo de un mensaje de bot truncado en el móvil.":::

* Todos los vínculos de una tarjeta adaptable de respuesta del bot deben responder. Cualquier vínculo que lleve al usuario fuera de la plataforma de Teams debe tener un texto de redireccionamiento claro, como **Ver en.** o **bien, de esta manera,** un icono emergente en el botón de acción de respuesta del bot o tener un texto de redireccionamiento adecuado en el cuerpo del mensaje de respuesta del bot. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-action-button-redirect-warning.png" alt-text="El gráfico muestra un ejemplo del botón de acción de respuesta del bot con un redireccionamiento.":::

* Por diseño, si el bot no responde ni admite ningún comando de usuario y es un bot unidireccional destinado solo a notificar a los usuarios. Debe establecer en `isNotificationOnly` true en el manifiesto. [*corrección obligatoria*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-command-isnotification-only-true.png" alt-text="El gráfico muestra un ejemplo de la propiedad notification only establecida en true en el manifiesto de la aplicación.":::

  :::image type="content" source="../../../../assets/images/submission/validation-bot-command-isnotification-only-not-true.png" alt-text="El gráfico muestra un ejemplo de bot de notificación solo que no responde para el mensaje de un usuario.":::

* La experiencia del usuario del bot no debe romperse en las plataformas móviles. El bot debe tener una capacidad de respuesta completa en dispositivos móviles. [*corrección obligatoria*]

> [!TIP]
> Para los bots personales, incluye una pestaña de **Ayuda** que describa con más detalle lo que puede hacer su bot.

</details>
</br>

<details><summary>Mensajes de bienvenida de los bots</summary>

* Si la aplicación tiene un flujo de configuración complejo (requiere una licencia de empresa o carece de un flujo de registro intuitivo), los bots de estas aplicaciones siempre deben enviar un mensaje de bienvenida durante la primera ejecución.

  Para obtener la mejor experiencia, el mensaje de bienvenida debe incluir el valor que ofrece el bot a los usuarios, que instalaron el bot en el canal, cómo configurar el bot y describir brevemente todos los comandos de bot admitidos. Puede mostrar el mensaje de bienvenida con una tarjeta adaptable con botones para mejorar la facilidad de uso. Para obtener más información, consulte [cómo activar un mensaje de bienvenida del bot](~/bots/how-to/conversations/send-proactive-messages.md). En el caso de las aplicaciones sin un flujo de configuración complejo, puede elegir desencadenar un mensaje de bienvenida durante la primera experiencia de ejecución del bot. Sin embargo, si se desencadena un mensaje de bienvenida, debe seguir las instrucciones del mensaje de bienvenida.

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message.png" alt-text="El gráfico muestra un ejemplo de bot que envía un mensaje de bienvenida cuando el bot tiene un flujo de trabajo de configuración complejo.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-no-welcome-message.png" alt-text="El gráfico muestra un ejemplo de bot que no envía un mensaje de bienvenida cuando el bot tiene un flujo de trabajo de configuración complejo.":::

* Los mensajes de bienvenida del bot en los canales y chats son opcionales durante la primera ejecución, especialmente si el bot está disponible para uso personal y realiza acciones similares. El bot no debe enviar mensajes de bienvenida a los usuarios individualmente (se considera [correo no deseado](#botmessagespamming)). El mensaje también debe mencionar a la persona que agregó el bot.

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-not-triggered.png" alt-text="validation-bot-welcome-message-not-trigger":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-triggered.png" alt-text="validation-bot-wel-message-trigger":::

* Solo los bots de notificación deben enviar un mensaje de bienvenida que aclara que el bot es un bot de notificación solo y los usuarios no podrán interactuar con él. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-notification-only-welcome-message-pass.png" alt-text="El gráfico muestra un ejemplo de bot que envía un mensaje de bienvenida que indica que es un bot solo de notificación.":::

* El mensaje de bienvenida no debe ser un error del usuario. El mensaje de bienvenida debe incluir el valor que ofrece el bot a los usuarios que instalaron el bot en el canal, cómo configurar el bot y describir brevemente todos los comandos de bot admitidos. Puede mostrar el mensaje de bienvenida con una tarjeta adaptable con botones para mejorar la facilidad de uso. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-no-way-forward.png" alt-text="El gráfico muestra un ejemplo de un escenario con errores en el que el bot no tiene ninguna manera de avanzar para el usuario en un mensaje de bienvenida.":::

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-clear-way-forward.png" alt-text="El gráfico muestra un ejemplo de mensaje de bienvenida del bot con una manera clara de avanzar para que el usuario complete la tarea.":::

* El bot instalado en un ámbito de chat de canal o grupo no debe enviar un mensaje de bienvenida proactivo a todos los miembros del equipo en el chat 1:1. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-send-proactive-message-to-all-members.png" alt-text="El gráfico muestra un ejemplo de bot que envía un mensaje de bienvenida proactivo a todos los miembros del equipo.":::

* Solo el bot de notificación puede enviar un mensaje de bienvenida proactivo en un canal solo si el mensaje contiene información importante para que cualquier usuario complete la configuración del bot o aclare los escenarios en los que se desencadenan las notificaciones. [*corrección obligatoria*]

* El bot instalado en un ámbito de chat de canal o grupo no debe enviar mensajes proactivos (no solo mensajes de bienvenida) que sean irrelevantes para todos los usuarios del chat de canal o grupo, sino que deben enviar mensajes proactivos al usuario a través del chat 1:1. [*corrección obligatoria*]

* El bot instalado en un ámbito de chat de canal o grupo no debe permitir que los usuarios inicien flujos de trabajo individuales. Los bots deben completar flujos de trabajo individuales en el chat 1:1 con el usuario. [*corrección obligatoria*]

* El mensaje de bienvenida del bot debe indicar claramente las limitaciones relacionadas con el uso del bot en el ámbito instalado. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-messahe-with-app-limitation.png" alt-text="El gráfico muestra un ejemplo de limitación de aplicaciones en el mensaje de bienvenida del bot.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-messahe-without-app-limitation.png" alt-text="El gráfico muestra un ejemplo de un bot sin limitación de aplicación en un mensaje de bienvenida.":::

* El mensaje de bienvenida debe desencadenarse automáticamente al instalar la aplicación en un ámbito personal. Si el bot no envía un mensaje de bienvenida en un ámbito personal, el usuario se lleva a un punto muerto. Si la aplicación no incluye un flujo de trabajo de configuración complejo, es opcional que el desarrollador desencadene un mensaje de bienvenida en el ámbito de chat de grupo o canal. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-no-welcome-message-in-personal-scope.png" alt-text="El gráfico muestra un ejemplo de bot que no envía un mensaje de bienvenida automáticamente en el ámbito personal.":::

* Los mensajes de bienvenida solo deben desencadenarse una vez al instalar el bot. Los mensajes de bienvenida no deben desencadenarse cada vez que el usuario invoca el comando de ayuda. La respuesta del comando de ayuda debe centrarse para incluir una manera de que el usuario acceda a la ayuda relacionada con el bot. [*corrección obligatoria*]

* Los mensajes de bienvenida no deben desencadenarse con todos los comandos del bot. Esto se considera spam. [*corrección obligatoria*]

  :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-trigger-for-any-command.png" alt-text="El gráfico muestra un ejemplo para que el bot desencadene un mensaje de bienvenida para cualquier comando.":::

* El contenido del mensaje de bienvenida debe estar relacionado con el flujo de trabajo del bot mencionado en la descripción larga de la aplicación y el ámbito de instalación. El mensaje de bienvenida debe incluir el valor que ofrece el bot a los usuarios que instalaron el bot en el canal, cómo configurar el bot y describir brevemente todos los comandos de bot admitidos. [*corrección obligatoria*]

* El bot no debe enviar varios mensajes de bienvenida cuando se desencadena al instalar la aplicación. [*corrección obligatoria*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-multiple-message-trigger-install.png" alt-text="El gráfico muestra un ejemplo de bot que desencadena varios mensajes de bienvenida durante la instalación de la aplicación.":::

* El nombre de la aplicación en el mensaje de bienvenida debe coincidir con el nombre de la aplicación en el manifiesto. [*corrección obligatoria*]

  :::image type="content" source="../../../../assets/images/submission/validation-app-name-mismatch-manifeast-and-welcome-message.png" alt-text="El gráfico muestra un ejemplo de nombre de aplicación en el mensaje de bienvenida que no coincide con el nombre de la aplicación en el manifiesto de la aplicación.":::

* El mensaje de bienvenida no debe mostrar nombres de plataformas de colaboración basadas en chats de la competencia a menos que la aplicación proporcione interoperabilidad específica.

* El mensaje de bienvenida no debe redirigir al usuario a otra aplicación de Teams, sino que el mensaje de bienvenida debe empujar al usuario para completar su primera tarea y describir brevemente todos los comandos de bot admitidos en la aplicación. [*corrección obligatoria*]

* El mensaje de bienvenida no debe contener vínculos a ningún marketplace de aplicaciones, incluido AppSource. [*corrección obligatoria*]

* Si la aplicación tiene un flujo de trabajo de configuración complejo que requiere la instalación dirigida por el administrador, no tiene un flujo de registro intuitivo y disponible, o requiere que los usuarios completen los pasos de configuración fuera de la experiencia de Teams y vuelvan, el bot debe enviar un mensaje de bienvenida proactivo en un ámbito de chat de grupo o equipo después de la instalación. [*corrección obligatoria*]

* Si el bot envía un mensaje de bienvenida en el canal, no debe enviarlo a los usuarios individualmente (se considera spam). El mensaje de bienvenida también debe mencionar a la persona que agregó el bot. [*Corrección sugerida*]

> [!TIP]
> En los mensajes de bienvenida a usuarios individuales, un paseo por el carrusel puede proporcionar una visión general eficaz del bot y cualquier otra característica de la aplicación para animar a los usuarios a probar los comandos bot. Por ejemplo, **Crear una tarea**.

</details>
</br>

<details><summary><a id="botmessagespamming">Mensajes de correo no deseado de bots</a></summary>

Los bots no deben enviar correo no deseado a los usuarios enviando varios mensajes a corto plazo.

* **Mensajes de bots en canales y chats**: No cree spam, enviando mensajes separados a los usuarios. Crear una publicación única con respuestas en el mismo hilo.

    :::image type="content" source="../../../../assets/images/submission/validation-bot-message-spamming-one-message.png" alt-text="validation-bot-message-spam-one-message":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-message-spamming-multiple-messages.png" alt-text="validation-bot-message-spam-multiple-message":::

* **mensajes de bot en aplicaciones personales**:
  * No envíe varios mensajes en sucesión rápida.

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-multiple-message-quick-succession.png" alt-text="El gráfico muestra un ejemplo de un bot que envía varios mensajes en sucesión rápida.":::

  * Envíe un mensaje con la información completa.
  * Evite las conversaciones de varios turnos para completar un único flujo de trabajo repetitivo.
  * Use un formulario (o módulo de tareas) para recopilar todas las entradas de un usuario a la vez.
  * Los bots de chat conversacionales basados en NLP pueden usar la conversación de varios turnos para que el diálogo sea más atractivo y complete un flujo de trabajo.

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-task-module.png" alt-text="validation-bot-message-using-task-module":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-mutliple-conversation.png" alt-text="El gráfico muestra un bot de ejemplo que usa mensajes de varios turnos para completar una sola conversación.":::

* **Mensajes de bienvenida:** no repita el mismo mensaje de bienvenida en intervalos regulares. Por ejemplo, cuando se agrega un nuevo miembro a un equipo, no hay que enviar un mensaje de bienvenida a los demás miembros. Enviar un mensaje personalmente al nuevo miembro.

   :::image type="icon" source="../../../../assets/images/submission/validation-bot-send-proactive-message-to-all-members.png" alt-text="En el gráfico se muestra un ejemplo de correo no deseado de bot a los usuarios con el mismo mensaje de bienvenida.":::

</details>
</br>

<details><summary>Notificaciones de bot</summary>

Las notificaciones del bot deben incluir contenido relevante para el ámbito que se defina para el bot (equipo, chat o personal).

:::image type="content" source="../../../../assets/images/submission/validation-bot-notifications-relevant.png" alt-text="validation-bot-notification-relevant":::

:::image type="content" source="../../../../assets/images/submission/validation-bot-notifications-not-relevant.png" alt-text="validation-bot-notification-not-relevant":::

</details>
</br>
<details><summary>Bots y tarjetas adaptables</summary>

Las tarjetas adaptativas son una forma muy recomendable de mostrar los mensajes de los bots. Las tarjetas deben ser ligeras y solo deben incluir un máximo de seis acciones. Para mostrar más contenido, considere la posibilidad de usar un módulo de tareas o una pestaña.

Para obtener más información acerca de las tarjetas, consulte:

* [Diseño de tarjetas adaptables](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Referencia de tarjetas](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

La experiencia del bot debe ser totalmente dinámica en dispositivos móviles. Las respuestas del bot deben proporcionar una manera de avanzar cuando corresponda. El bot debe responder y generar un error con un mensaje de error estable para los errores. Los mensajes de bot enviados en el ámbito personal a la base del usuario en los desencadenadores de un ámbito de colaboración deben proporcionar información contextual (incluido el origen del mensaje).

</details>
</br>

<details><summary>Bots de solo notificación</summary>

Las aplicaciones que constan de bots de solo notificación proporcionan valor añadido al usuario mediante el desencadenamiento de notificaciones de usuario basadas en determinados desencadenadores o eventos en la aplicación principal o el back-end. Por ejemplo, se agrega un nuevo cliente potencial para que el equipo de ventas realice un seguimiento. Un bot de solo notificación de alta calidad notifica a los usuarios periódicamente determinadas finalizaciones de eventos, como las finalizaciones de flujo de trabajo o las alertas.

Una notificación proporciona valor añadido en Teams si:

1. La tarjeta o el texto publicados proporcionan detalles adecuados que no requieren ninguna otra acción por parte del usuario.
1. La tarjeta o el texto publicados proporcionan información de vista previa adecuada para que un usuario tome medidas o decida ver más detalles en un vínculo que se abre fuera de Teams.

Las aplicaciones que solo proporcionan notificaciones con contenido como, **Tiene una nueva notificación**, **haga clic para ver** y requiera que el usuario navegue fuera de Teams para todo lo demás no proporciona un valor significativo dentro de Teams.

   :::image type="content" source="../../../../assets/images/submission/validation-bot-notification-only-inadequete-info.png" alt-text="Captura de pantalla que muestra un ejemplo de una notificación solo un poco con información inadecuada en la versión preliminar.":::

> [!TIP]
> Obtenga una vista previa de la información y proporcione acciones de usuario insertadas básicas en la tarjeta publicada para que el usuario no tenga que navegar fuera de Teams para todas las acciones (independientemente de la complejidad).

</details>
<br/>

<details><summary>Información de metadatos del bot</summary>

* La información del bot en el manifiesto de la aplicación (nombre del bot, logotipo, vínculo de privacidad y vínculo de términos de servicio) debe ser coherente con los metadatos de Bot Framework. [*corrección obligatoria*]

* El identificador de bot debe coincidir en el manifiesto de la aplicación y los metadatos de Bot Framework. [*corrección obligatoria*]

* Asegúrese de que el identificador del bot en el manifiesto de la aplicación coincide con el identificador del bot en la última versión publicada de la tienda de la aplicación. El cambio de los identificadores de bot en una actualización de la aplicación conduce a la pérdida permanente de todo el historial de interacción del usuario con el bot para los usuarios existentes de la aplicación e inicia una nueva cadena de conversaciones con el nuevo identificador de bot. [*corrección obligatoria*]

* Cualquier cambio en el nombre de la aplicación, los metadatos, el mensaje de bienvenida del bot o las respuestas del bot debe actualizarse con un nuevo nombre. [*corrección obligatoria*]

* El nombre de la aplicación en el mensaje de bienvenida del bot o las respuestas del bot deben coincidir con el nombre de la aplicación en el manifiesto. [*corrección obligatoria*]

</details>
<br/>

<details><summary>Bot en ámbito de colaboración</summary>

* No se permite la instalación de bots en un ámbito de chat de grupo o canal para obtener la lista de equipos para enviar notificaciones proactivas para los usuarios, ya que no se permiten chats 1:1 para desencadenadores específicos del equipo. Por ejemplo, la aplicación que empareja a personas para una reunión. [*corrección obligatoria*]

* El bot en el chat de canal o grupo solo se usa para obtener los mensajes o las publicaciones en el chat de canal o grupo para enviar notificaciones proactivas para los usuarios, ya que no se permiten los chats 1:1. [*corrección obligatoria*]

* Los bots instalados en el ámbito de colaboración deben proporcionar un valor de usuario en el ámbito de colaboración. [*corrección obligatoria*]

</details>

## <a name="message-extensions"></a>Extensiones de mensajes

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.4](/legal/marketplace/certification-policies#114044-messaging-extensions).

Si la aplicación incluye una extensión de mensaje, asegúrese de que cumple estas directrices.

> [!TIP]
> Para obtener más información sobre cómo crear una experiencia de aplicación de alta calidad, vea las [directrices de diseño de extensiones de mensaje de Teams](~/messaging-extensions/design/messaging-extension-design.md).

<br/>

<details><summary>Instrucciones de diseño de extensiones de mensajería</summary>

* Si la aplicación de Teams usa la funcionalidad de extensión de mensajería, la aplicación debe seguir las [directrices de diseño de la extensión de mensajería](../../../../messaging-extensions/design/messaging-extension-design.md).

   :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-design-guidelines-fail.png" alt-text="El gráfico muestra un ejemplo de una aplicación que no cumple las directrices de extensión.":::

* Las extensiones de mensajería son métodos abreviados para insertar contenido de la aplicación o realizar una acción en un mensaje sin salir de la conversación. Mantenga la extensión de mensajería simple y muestre solo los componentes necesarios para completar la acción de forma eficaz. El sitio web completo no debe estar enmarcado dentro de la extensión de mensajería [*Corrección obligatoria*]

* Las imágenes en versión preliminar en tarjetas adaptables en extensiones de mensajería deben cargarse correctamente. [*corrección obligatoria*]

  :::image type="content" source="../../../../assets/images/submission/validation-preview-image-adaptive-card-loading.png" alt-text="El gráfico muestra un ejemplo de carga de imágenes en versión preliminar en la tarjeta adaptable.":::

  :::image type="content" source="../../../../assets/images/submission/validation-preview-image-adaptive-card-not-loading.png" alt-text="El gráfico muestra un ejemplo de imagen de vista previa que no se carga en la tarjeta adaptable.":::

* La tarjeta de respuesta de la extensión de mensajería debe incluir el icono de aplicación para evitar confusiones del usuario final. [*corrección obligatoria*]

* La aplicación no debe tener ninguna funcionalidad rota. La aplicación no debe ser un punto muerto ni impedir que el usuario complete un flujo de trabajo en una extensión de mensajería. [*corrección obligatoria*]

* Las extensiones de mensajería deben responder o funcionar según lo previsto en los ámbitos de canal y chat en grupo. [*corrección obligatoria*]

* Debe incluir una manera de que el usuario inicie sesión o cierre la sesión desde la extensión de mensajería. [*corrección obligatoria*]

</details>
</br>

<details><summary>Comandos de acción para extensiones de mensaje basadas en acciones</summary>

Las extensiones de mensaje basadas en acciones deben hacer lo siguiente:

* Permitir que los usuarios desencadenen acciones en un mensaje sin completar pasos intermedios, como es el inicio de sesión.

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-no-intermediate-step.png" alt-text="validation-messaging-extension-no-intermediate-steps":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-intermediate-step-available.png" alt-text="validation-messaging-extension-intermediate-steps-available":::

* Pasar el contexto del mensaje al siguiente estado de trabajo. [*corrección obligatoria*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-passes-message.png" alt-text="validation-messaging-extension-app-passes-messages":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-doesnot-pass-message.png" alt-text="validation-messaging-extension-app-doesnot-pass-messages":::

* Incorpore el nombre de la aplicación host en lugar de un verbo genérico para los comandos de acción que se desencadenan desde un mensaje de chat, una publicación de canal o una llamada a la acción dentro de las aplicaciones. Por ejemplo, use **Iniciar un Reunión de Skype** para **Iniciar reunión**, **Cargar archivo en DocuSign** para **Cargar archivo**. [*Corrección sugerida*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-host-name.png" alt-text="El gráfico muestra un ejemplo del nombre de la aplicación host para un comando de acción.":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-verb.png" alt-text="El gráfico muestra un ejemplo de verbo genérico para un comando de acción.":::

* La invocación de una acción de mensaje debe permitir que el usuario complete el flujo de trabajo. Los errores, las respuestas en blanco o los indicadores de carga continua para que la acción del mensaje funcione según lo previsto no deben estar presentes. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-continous-loading-indicator-action-command.png" alt-text="El gráfico muestra un ejemplo de indicador de carga continua cuando un bot invoca un comando de acción.":::

* Los comandos de acción duplicados no deben estar presentes. [*corrección obligatoria*]

* Las acciones de mensaje deben permitir que el usuario complete el flujo de trabajo según lo previsto sin una respuesta no válida. [*corrección obligatoria*]

* Las aplicaciones con solo la extensión de mensajería basada en acciones deben tener el siguiente estado final:

  * Publique una acción pertinente como una notificación en el contexto donde se invoca la extensión de mensaje o en el chat del bot 1:1 en función del escenario de usuario. [*corrección obligatoria*]

  * Permitir a los usuarios compartir tarjetas con otros usuarios en función de la acción realizada. Esto es para asegurarse de que las aplicaciones no realizan acciones silenciosas. Por ejemplo, se crea un vale en función de un mensaje de un canal, pero la aplicación no envía una notificación o no proporciona una manera de solicitar al usuario que comparta los detalles de la incidencia después de crear el vale. [*corrección obligatoria*]

</details>
</br>

<details><summary>Vista previa de los vínculos (despliegue de vínculos)</summary>

[*corrección obligatoria*]

Las extensiones de mensaje deben obtener una vista previa de los vínculos reconocidos en el cuadro de redacción de Teams. No agregue dominios que estén fuera de su control (direcciones URL absolutas o caracteres comodín). Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido. Los dominios de nivel superior también están prohibidos. Por ejemplo, `*.com` o `*.org`. [*corrección obligatoria*]

</details>
</br>

<details><summary>Comandos de búsqueda</summary>

* Las extensiones de mensaje basadas en búsqueda deben proporcionar texto que ayude a los usuarios a buscar de forma eficaz. [*corrección obligatoria*]

    :::image type="content" source="../../../../assets/images/submission/validation-search-commands-text-available.png" alt-text="El gráfico muestra un ejemplo de una extensión de mensaje con texto de ayuda para que los usuarios busquen de forma eficaz.":::

    :::image type="content" source="../../../../assets/images/submission/validation-search-commands-text-not-available.png" alt-text="El gráfico muestra un ejemplo de una extensión de mensaje sin texto de ayuda para que los usuarios busquen de forma eficaz.":::

* Los ejecutables de @mención deben ser claros, fáciles de entender y legibles.

    :::image type="content" source="../../../../assets/images/submission/validation-search-command-unclear-executable.png" alt-text="validation-search-commands-unclear-executable":::

</details>
</br>

<details><summary>Comandos de acción para la extensión de mensaje basada en búsqueda</summary>

[*corrección obligatoria*]

Las aplicaciones que constan de la extensión de mensaje basada en búsqueda proporcionan valor añadido al usuario mediante el uso compartido de tarjetas que permiten conversaciones contextuales sin cambiar de contexto.

Para pasar la validación de una aplicación de extensión de mensaje solo basada en búsqueda, se requieren los siguientes elementos como línea base para asegurarse de que la experiencia del usuario no se interrumpe. Una tarjeta compartida a través de una extensión de mensaje proporciona valor añadido en Teams si:

1. La tarjeta publicada proporciona los detalles adecuados que no requieren ninguna otra acción por parte del usuario.
1. La tarjeta publicada proporciona información de vista previa adecuada para que un usuario tome medidas o decida ver más detalles en un vínculo que se abre fuera de Teams.

    :::image type="content" source="../../../../assets/images/submission/validation-search-based-messaging-ext-adequete-info.png" alt-text="validation-search-base-messaging-ext-adequete-info":::

    :::image type="content" source="../../../../assets/images/submission/validation-search-based-messaging-ext-inadequete-info.png" alt-text="validation-search-base-messaging-ext-inadequete-info":::

El desenlazamiento de vínculos de solo las aplicaciones no proporciona un valor añadido significativo en Teams. Considere la posibilidad de crear flujos de trabajo adicionales en la aplicación, si la aplicación solo admite la apertura de vínculos y no tiene ninguna otra funcionalidad.

</details>

## <a name="task-modules"></a>Módulos de tareas

[*corrección obligatoria*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.5](/legal/marketplace/certification-policies#114045-task-modules).
<br></br>
<details><summary>Expandir para obtener más información</summary>

Un módulo de tarea debe incluir un icono y el nombre corto de la aplicación a la que está asociado. Los módulos de tareas no deben insertar una aplicación completa y mostrar solo los componentes necesarios para completar una acción específica.

Para obtener más información, vea [las directrices de diseño de módulos de tareas de Teams](~\task-modules-and-cards\task-modules\design-teams-task-modules.md).

:::image type="content" source="../../../../assets/images/submission/validation-task-module-displays-components.png" alt-text="validation-task-module-displays-component":::

:::image type="content" source="../../../../assets/images/submission/validation-task-module-embeds-app.png" alt-text="validation-task-module-embed-app":::

> [!TIP]
> Para obtener más información sobre cómo crear una experiencia de aplicación de alta calidad, vea [directrices de diseño de módulos de tareas de Teams](~/task-modules-and-cards/task-modules/design-teams-task-modules.md).

</details>

## <a name="meeting-extensions"></a>Extensiones de reunión

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.6](/legal/marketplace/certification-policies#114046-meeting-extensions).
> [!TIP]
> Para obtener más información sobre cómo crear una experiencia de aplicación de alta calidad, vea las [directrices de diseño de la extensión de reuniones de Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md).

</br>
<details><summary>Directrices de diseño de extensiones de reunión</summary>

* Las aplicaciones de Teams deben seguir [las directrices de diseño de la extensión de reunión](../../../../apps-in-teams-meetings/design/designing-apps-in-meetings.md).

* Con la experiencia de la aplicación en la reunión, puede interactuar con los participantes durante la reunión mediante pestañas, cuadros de diálogo y la característica de uso compartido en la reunión para la fase. Si la aplicación admite la extensión de reunión de Teams, debe proporcionar una experiencia dinámica en la reunión alineada con la experiencia de reunión de Teams. [*corrección obligatoria*]

* Con la experiencia de la aplicación previa a la reunión, los usuarios pueden buscar y agregar aplicaciones de reunión. Los usuarios también pueden realizar tareas previas a la reunión, como desarrollar un sondeo para encuestar a los participantes de la reunión. Una aplicación que proporciona una experiencia previa a la reunión debe ser relevante para el flujo de trabajo de la reunión y ofrecer valor al usuario. [*corrección obligatoria*]

* Con la experiencia de la aplicación posterior a la reunión, los usuarios pueden ver los resultados de la reunión, como, sondear los resultados de la encuesta o los comentarios y otro contenido de la aplicación. Una aplicación que proporciona una experiencia posterior a la reunión debe ser relevante para el flujo de trabajo de la reunión y ofrecer valor al usuario. [*corrección obligatoria*]

* Con la experiencia de la aplicación en la reunión, puede interactuar con los participantes de la reunión durante la reunión y mejorar la experiencia de la reunión para todos los asistentes. Los asistentes no se deben llevar fuera de la reunión de Teams para completar los flujos de trabajo principales de los usuarios de la aplicación. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-outside-teams-core-workflows.png" alt-text="El gráfico muestra un ejemplo de una experiencia en la reunión que redirige al usuario fuera de Teams para completar la funcionalidad básica de la aplicación.":::

* La aplicación debe ofrecer valor más allá de proporcionar solo escenas personalizadas del modo junto en Teams. [*corrección obligatoria*]

* Debe declarar `groupChat` como un ámbito en `configurableTabs` y `meetingDetailsTab`, `meetingChatTab`y `meetingSidePanel` como una propiedad de contexto en el manifiesto para habilitar la aplicación para reuniones en dispositivos móviles de Teams. [*corrección obligatoria*]

* Los lienzos de reunión no deben ser un asistente a la reunión. Los lienzos de reunión deben mostrar un mensaje de error correcto para las limitaciones de la aplicación, como la dependencia específica de la región. [*corrección obligatoria*]

* El encabezado del lienzo de la reunión debe mostrar el nombre correcto de la aplicación para evitar confundir al asistente a la reunión. [*corrección obligatoria*]

* Debe incluir una opción para que el usuario cierre la sesión o cierre la sesión de la extensión de reunión. [*corrección obligatoria*]

* Las pestañas de reunión en plataformas móviles deben incluir flujos de trabajo pertinentes. Las páginas en blanco no deben estar presentes en una pestaña de reunión. [*Corrección obligatoria*]

* La fase de reunión es un lienzo de participación centrada, intuitiva y colaborativa. La fase de reunión no debe insertar la experiencia completa del sitio web. [*corrección obligatoria*]

* La aplicación no debe mostrar la pantalla de carga continua, el error o la funcionalidad interrumpida que impide que el usuario o bloquee la finalización de un flujo de trabajo en un escenario de reunión. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-app-shows-continous-loading-screen.png" alt-text="El gráfico muestra un ejemplo de pantalla de carga continua en una aplicación.":::

* La aplicación no debe abrir una nueva instancia de Teams al iniciar una reunión. Los lienzos de reuniones son una extensión de las funcionalidades de Teams que promueven la colaboración en tiempo real y las nuevas reuniones siempre deben abrirse dentro de la instancia de Teams actualmente activa. [*corrección obligatoria*]

* Las aplicaciones de reunión deben completar flujos de trabajo dentro de la plataforma de Microsoft Teams sin redirigir a plataformas basadas en chats de la competencia. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-apps-redirecting-competitor-chat-platform.png" alt-text="Gráfico que muestra un ejemplo de una aplicación que redirige a la plataforma basada en chat de la competencia.":::

* Si la aplicación admite vistas basadas en roles y determinados flujos de trabajo no están disponibles para todos los participantes, se recomienda implementar la mensajería adecuada para los participantes en la pestaña y el panel lateral, indicando que la aplicación está actualmente para la vista del organizador y proporcionar detalles sobre cómo los asistentes recibirán las notas de la reunión, los elementos de acción y las agendas de actualización. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-way-forward-not-available-for-role-based-views.png" alt-text="El gráfico muestra un ejemplo de una aplicación sin una manera de avanzar para los participantes en una vista basada en roles.":::

</details>
<br/>

<details><summary>General</summary>

Use las siguientes directrices para las extensiones de reuniones:

* Las aplicaciones de extensibilidad de reuniones deben ofrecer una experiencia dinámica en la reunión alineada con la experiencia de reunión de Teams. La experiencia en la reunión es obligatoria para una aplicación de Teams que admite la extensibilidad de reuniones, pero las experiencias previas y posteriores a la reunión no son obligatorias.

  * Con la experiencia de la aplicación previa a la reunión, los usuarios pueden buscar y agregar aplicaciones de reunión. Los usuarios también pueden realizar tareas previas a la reunión, como desarrollar un sondeo para encuestar a los participantes de la reunión. Si la aplicación proporciona una experiencia previa a la reunión, debe ser relevante para el flujo de trabajo de la reunión.

  * Con la experiencia de la aplicación posterior a la reunión, los usuarios pueden ver los resultados de la reunión, como, sondear los resultados de la encuesta o los comentarios y otro contenido de la aplicación. Si la aplicación proporciona una experiencia posterior a la reunión, debe ser relevante para el flujo de trabajo de la reunión.

  * Con la experiencia de la aplicación en la reunión, puede interactuar con los participantes de la reunión durante la reunión y mejorar la experiencia de la reunión para todos los asistentes. Los asistentes no se deben llevar fuera de la reunión de Teams para completar los flujos de trabajo principales de usuario de la aplicación.

* La aplicación debe ofrecer valor añadido que vaya más allá de proporcionar escenas personalizadas en Modo conferencia en Teams.

* La característica de fase de reunión compartida solo se puede iniciar a través de la aplicación de escritorio de Teams. Sin embargo, la experiencia de consumo de la fase de reunión compartida debe ser usable y no interrumpirse cuando se visualiza en dispositivos móviles.

> [!TIP]
> Debe declarar `groupChat` como un ámbito en `configurableTabs` y `meetingDetailsTab`, `meetingChatTab`y `meetingSidePanel` como una propiedad de contexto en el manifiesto para habilitar la aplicación para reuniones en dispositivos móviles de Teams.

</details>
</br>

<details><summary>Experiencia previa y posterior a la reunión</summary>

* Las pantallas previas y posteriores a la reunión deben cumplir las directrices generales de diseño de pestañas. Para obtener más información, vea [las directrices de diseño de Teams](~/tabs/design/tabs.md).
* Las pestañas deben tener un diseño organizado cuando muestren varios elementos. Por ejemplo, más de 10 sondeos o encuestas, vea [diseño de ejemplo](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).
* La aplicación debe notificar a los usuarios cuándo se exportan los resultados de una encuesta o un sondeo indicando **resultados descargados correctamente**.

   :::image type="content" source="../../../../assets/images/submission/validation-meeting-experience-tab-design-guidelines-fail.png" alt-text="El gráfico muestra un ejemplo de tabulación que no sigue las directrices de diseño de pestañas.":::

</details>

</br>
<details><summary>Experiencia en la reunión</summary>

* Las aplicaciones sólo deben utilizar un tema oscuro durante las reuniones. Para obtener más información, vea [las directrices de diseño de Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming).
* Una información sobre herramientas debe mostrar el nombre de la aplicación cuando se mantenga el puntero sobre el icono de la aplicación durante las reuniones.

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-display-app-name.png" alt-text="validation-in-meeting-exp-display-app-names":::

* Las extensiones de mensaje deben funcionar igual durante las reuniones que fuera de ellas.

</details>

</br>
<details><summary>Pestañas en la reunión</summary>

* Debe ser receptivo.
* Debe mantener el relleno y los tamaños de componentes.
* Debe tener un botón Atrás si hay más de una capa de navegación.

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button.png" alt-text="El gráfico muestra un ejemplo de botón Atrás presente.":::

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button-absent.png" alt-text="El gráfico muestra un ejemplo de botón Atrás no presente.":::

* No debe incluir más de un botón cerrar. Puede confundir a los usuarios, ya que ya hay un botón de encabezado integrado para descartar la pestaña.
* No debe tener desplazamiento horizontal.

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-tab-vertical-scroll.png" alt-text="El gráfico muestra un ejemplo de pestaña en reunión con desplazamiento vertical.":::

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-tab-horizontal-scroll.png" alt-text="El gráfico muestra un ejemplo de pestaña en reunión con desplazamiento horizontal.":::

</details>

</br>
<details><summary>Diálogos en las reuniones</summary>

* Debe usarse con moderación y para escenarios que sean ligeros y orientados a tareas.
* Debe mostrar el contenido en una sola columna y no tener varios niveles de navegación.

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-single-column-layout.png" alt-text="El gráfico muestra un ejemplo de diseño de una sola columna para el cuadro de diálogo en la reunión.":::

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-multiple-column-layout.png" alt-text="El gráfico muestra un ejemplo de varios diseños de columna para el cuadro de diálogo en la reunión.":::

* No debe utilizar módulos de tareas.
* Debe alinearse con el centro del escenario de la reunión.

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-dialog-not-aligned.png" alt-text="El gráfico muestra un ejemplo de diálogo en reunión que no se alinea con el centro de la fase de reunión.":::

* Debe descartarse después de que un usuario seleccione un botón o realice una acción.

* **Modo conferencia**: cerciórese de tener en cuenta los siguientes procedimientos recomendados para una experiencia de creación de escenas:
  * Todas las imágenes están en formato .png.
  * El paquete final con todas las imágenes juntas no debe superar la resolución de 1920 x 1080. La resolución es un número par. Esta resolución es un requisito para que las escenas se muestren correctamente.
  * El tamaño máximo de la escena es de 10 MB.
  * El tamaño máximo de cada imagen es de 5 MB. Una escena es una colección de varias imágenes. El límite es para cada imagen individual.
  * Seleccione **Transparente** según sea necesario. Esta casilla está disponible en el panel derecho cuando se selecciona una imagen. Las imágenes superpuestas deben marcarse como transparentes para indicar que se superponen en la escena.

</details>

## <a name="notifications"></a>Notificaciones

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.4.7](/legal/marketplace/certification-policies#114047-notification-apis).

Si la aplicación usa las [API de fuente de actividad proporcionadas por Microsoft Graph](/graph/teams-send-activityfeednotifications), asegúrese de que cumple las siguientes directrices.

> [!TIP]
> Si las aplicaciones admiten escenarios de notificación en los que las notificaciones se desencadenan después de intervalos largos, por ejemplo, después de un día o un mes. Antes de enviarlas para su revisión, asegúrese de desencadenar dichas notificaciones en segundo plano para que podamos probar las notificaciones.

<br></br>

<details><summary>Directrices de diseño de notificaciones</summary>

* Las aplicaciones de Teams deben seguir [las directrices de diseño de notificaciones de fuente de actividad](/graph/teams-send-activityfeednotifications).

* El flujo de trabajo irrelevante, incorrecto, no responde o roto no debe estar presente después de que el usuario seleccione una notificación en la fuente de actividad de Teams. No se debe impedir que los usuarios completen un flujo de trabajo después de seleccionar una notificación de fuente de actividad. [*corrección obligatoria*]

* Incluya el nombre de la aplicación en la notificación de fuente de actividad para que los usuarios finales comprendan el origen o el desencadenador de la notificación sin confusiones. [*corrección obligatoria*]

* La aplicación debe desencadenar notificaciones para todos los escenarios de notificación mencionados en la descripción larga de la aplicación, la experiencia de primera ejecución de la aplicación y en los escenarios declarados `activityTypes` en en el manifiesto. [*corrección obligatoria*]

* Las notificaciones deben aparecer en los cinco segundos siguientes a la acción del usuario. [*corrección obligatoria*]

* Debes llamar a las limitaciones de notificación (si las hubiera) en la descripción larga de la aplicación o en la primera experiencia de ejecución de la aplicación. [*corrección obligatoria*]

</details>
<br/>

<details><summary>General</summary>

* Todos los desencadenadores de notificación especificados en la configuración de la aplicación deben funcionar.
* Las notificaciones deben estar localizadas según los idiomas admitidos configurados para su aplicación.
* Las notificaciones deben aparecer en los cinco segundos siguientes a la acción del usuario.
* Las notificaciones deben localizarse según los idiomas admitidos para todas las plataformas donde la aplicación es compatible. [*corrección obligatoria*]

</details>
</br>

<details><summary>Avatares</summary>

* El avatar de notificación debe coincidir con el icono de color de la aplicación.
* Las notificaciones desencadenadas por un usuario deben incluir el avatar del usuario.

</details>
</br>
<details><summary>Correo no deseado</summary>

* Las aplicaciones no deben enviar más de 10 notificaciones por minuto a un usuario.
* Los bots y la fuente de actividades no deben desencadenar notificaciones duplicadas.
* Las notificaciones deben aportar algún valor a los usuarios y no ser utilizadas para eventos triviales o irrelevantes.

</details>
</br>
<details><summary>Navegación y diseño</summary>

* Las notificaciones deben ceñirse al diseño y la experiencia de la alimentación de la actividad de Teams.
* Al seleccionar una notificación, se debe dirigir al usuario al contenido relevante dentro de Teams.

</details>

## <a name="microsoft-365-app-compliance-program"></a>Programa de cumplimiento de aplicaciones de Microsoft 365

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la[directiva de marketplace comercial de Microsoft 1140.6](/legal/marketplace/certification-policies#11406-publisher-attestation).
<br></br>
<details><summary>Expandir para obtener más información</summary>

El Programa de cumplimiento de aplicaciones de Microsoft 365 está destinado a ayudar a las organizaciones a evaluar y administrar el riesgo mediante la evaluación de la información de seguridad y cumplimiento de su aplicación. Si publica una aplicación en la tienda de Teams, debe completar los siguientes niveles del programa:

* **Verificación de editores**: Ayuda a los administradores y usuarios finales a comprender la autenticidad de los desarrolladores de aplicaciones que se integran en la plataforma de identidad de Microsoft. Cuando haya finalizado, se mostrará un distintivo de **verificado** en el cuadro de diálogo de consentimiento de Azure Active Directory y en otras pantallas. Para obtener más información, consulte [Marcar la aplicación como verificada por el publicador](/azure/active-directory/develop/mark-app-as-publisher-verified).

    :::image type="content" source="../../../../assets/images/submission/validation-365-compliance-publisher-verification.png" alt-text="El gráfico muestra un ejemplo de una notificación verificada azul en el cuadro de diálogo de consentimiento de Azure Active Directory.":::

* **Certificación del editor**: Un proceso en el que usted comparte información general, de manejo de datos y de seguridad y cumplimiento para ayudar a los clientes potenciales a tomar decisiones informadas sobre el uso de su aplicación.

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Si presenta una aplicación que no ha sido incluida en la lista anteriormente, no puede completar oficialmente la certificación de editor hasta que su aplicación esté en la tienda de Teams. Si está actualizando una aplicación de la lista, complete el certificado de editor antes de enviar la última versión de la aplicación.

</details>

## <a name="advertising"></a>Publicidad

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Esta sección está alineada con la [directiva de Marketplace comercial de Microsoft 1140.7](/legal/marketplace/certification-policies#11407-advertising).

Las aplicaciones no deben mostrar publicidad, incluidos anuncios dinámicos, anuncios de banner y anuncios en el mensaje.

:::image type="content" source="../../../../assets/images/submission/validation-advertising-banners.png" alt-text="El gráfico muestra un ejemplo de un escenario con errores de publicidad en Teams.":::

## <a name="cryptocurrency-based-apps"></a>Aplicaciones basadas en criptomonedas

Debe demostrar el cumplimiento de todas las leyes en las que se distribuye la aplicación, si la aplicación:

* Facilita las transacciones o transmisiones criptomoneda dentro de la aplicación.

* Promueve el contenido relacionado con criptomonedas.

* Permite a los usuarios almacenar o acceder a su criptomoneda almacenada.

* Anima o permite a los usuarios completar una transacción o transmisión basada en criptomonedas fuera de la plataforma de Teams.

* Fomenta o facilita la minería de tokens de criptomoneda.

* Facilita la participación del usuario en las ofertas iniciales de monedas.

* Recompensa o incentiva a los usuarios con tokens de criptomoneda para completar una tarea.

Después de una revisión interna de Microsoft, si la demostración de cumplimiento es satisfactoria, Microsoft puede continuar con la certificación adicional de la aplicación. Si la demostración de cumplimiento no es satisfactoria, Microsoft le mantendrá informado de la decisión de no continuar con la certificación de la aplicación.

## <a name="app-functionality"></a>Funcionalidad de la aplicación

* Los flujos de trabajo o el contenido de la aplicación deben estar relacionados con el ámbito. [*corrección obligatoria*]
* Todas las funcionalidades de la aplicación deben ser funcionales y deben funcionar correctamente como se describe en la descripción larga de AppSource o manifiesto. [*corrección obligatoria*]
* Las aplicaciones siempre deben indicar al usuario antes de descargar cualquier archivo o archivo ejecutable en el entorno del usuario. Cualquier llamada a la acción (CTA), ya sea basada en texto o de otro modo, que permita al usuario que se descargue un archivo o ejecutable en la acción del usuario en la aplicación. [*corrección obligatoria*]

## <a name="mobile-experience"></a>Experiencia móvil

* Los complementos móviles deben ser gratuitos. No debe haber contenido ni vínculos desde la aplicación que promuevan ventas al alza, tiendas en línea u otras solicitudes de pago. Las cuentas necesarias para las aplicaciones no deben tener ningún cargo por su uso y, si se limita el tiempo, no deben incluir ningún contenido que indique una necesidad de pago.

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-add-in-charges.png" alt-text="El gráfico muestra un ejemplo de un complemento móvil que solicita el pago.":::

* El uso de la palabra **FREE**, **FREE TRIAL** o **TRY FREE** se permite en la experiencia de aplicación web o de escritorio sin ninguna limitación o consideración.

* Se permite el uso de la palabra **FREE** como texto sin formato en el contexto de una versión de prueba o actualización de la aplicación en el móvil.

* El uso de la palabra **GRATIS** en el contexto de una evaluación o actualización de la aplicación con un vínculo que conduce a una página de aterrizaje sin pago o información de precios está permitido en el móvil. El texto sin formato para indicar que la aplicación es **PAID** se permite en el móvil.

* No se permite el uso de la palabra **FREE** como texto sin formato en el contexto de una actualización de prueba o aplicación y asociada a los detalles de precios en dispositivos móviles.

* No se permite el uso de la palabra **GRATIS** en el contexto de una evaluación o actualización de la aplicación y asociado a un vínculo que conduce a una página de aterrizaje con información de precios o detalles de pago en el móvil.

* No se permiten los detalles de precios en el móvil en cualquier formato, por ejemplo, la imagen, el texto o el vínculo. No se permite la llamada a la acción, como **los planes de visualización** en dispositivos móviles. No se permite la información sobre los planes sin detalles de precios, pero con un vínculo de contacto o un correo electrónico en el móvil. No se permite ningún texto con detalles de contacto que vinculen o aluden a una actualización de pago en el móvil. Pagos para bienes físicos se permiten en el móvil. Por ejemplo, la aplicación puede permitir el pago para reservar un taxi.

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-exp-pricing-details-on-mobile-fail.png" alt-text="El gráfico muestra un ejemplo de detalles de precios en el móvil.":::

* Pagos para productos digitales en la aplicación no se permiten en el móvil. [*corrección obligatoria*]

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-exp-payments-digital-goods.png" alt-text="Gráfico que muestra un ejemplo de pagos por bienes digitales en el móvil.":::

* Las aplicaciones de Teams deben ofrecer una experiencia móvil entre dispositivos adecuada. [*corrección obligatoria*]

* Las funcionalidades que no se admiten en dispositivos móviles no deben ser un usuario sin salida y deben proporcionar un mensaje de error correcto cuando corresponda. [*corrección obligatoria*]

## <a name="next-step"></a>Paso siguiente

> [!div class=*nextstepaction*]
> [Crear una cuenta del Centro de partners](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)

## <a name="see-also"></a>Consulte también

* [Distribuir la aplicación](~/concepts/deploy-and-publish/apps-publish-overview.md)
* [Preparar el envío de la tienda](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [Prueba y depuración de la aplicación](~/concepts/build-and-test/debug.md)
* [Crear una cuenta de desarrollador del Centro de partners](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
