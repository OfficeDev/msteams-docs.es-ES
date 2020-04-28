---
title: Guía del proceso de aprobación de aplicaciones de Microsoft Teams
description: Describe el proceso de aprobación para publicar la aplicación en la tienda de aplicaciones de Microsoft Teams
keywords: publicación de la tienda Office de tienda de AppSource
ms.openlocfilehash: 70f81f40ff424ab28e7129da7b947be0b1fcf469
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914549"
---
# <a name="submit-your-app-to-appsource"></a>Enviar la aplicación a AppSource

## <a name="teams-app-submission"></a>Envío de aplicación de Teams

La publicación de la aplicación en [AppSource](https://appsource.microsoft.com) hace que esté disponible en el catálogo de aplicaciones de Microsoft Teams y en la Web. En un nivel alto, el proceso para enviar la aplicación a AppSource es:

1. Desarrolle su aplicación siguiendo nuestras [pautas de diseño](~/concepts/design/understand-use-cases.md). Las pestañas deben seguir nuestras [instrucciones de diseño de pestañas](~/tabs/design/tabs.md). Los bots deben seguir las [directrices de diseño de bot](~/bots/design/bots.md).
1. [Configure una cuenta de Desarrollador en el](/office/dev/store/open-a-developer-account) [centro de Partners](https://support.microsoft.com/help/4499930/partner-center-overview).
1. Prepare la aplicación para el envío siguiendo nuestra [lista de comprobación de envío](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).
1. Revise nuestras [sugerencias para obtener un envío de aplicación correcto](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md).
1. Envíe el paquete a [AppSource a través del centro de asociados](/office/dev/store/use-partner-center-to-submit-to-appsource).
1. Realice un seguimiento del proceso de aprobación en el panel del centro de asociados. *Consulte* [información general sobre el centro de Partners](https://support.microsoft.com/help/4499930/partner-center-overview).
1. Post subenvío: revise nuestras instrucciones para [mantener y dar soporte a su aplicación publicada](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).

>[!NOTE]
>
> * Si la aplicación de Microsoft Teams contiene un bot, debe cumplir con el [código de conducta del marco del desarrollador de](https://aka.ms/bf-conduct)bot? n.
> * Si la aplicación contiene un conector de Office 365, es posible que se apliquen términos adicionales. *Vea* [Connector Dashboard Developer's Dashboard](https://aka.ms/connectorsdashboard) and [App Developer Agreement](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm).

## <a name="faqs--teams-apps-and-partner-accounts"></a>Preguntas más frecuentes: las aplicaciones de Microsoft Teams y las cuentas de asociados

## <a name="how-do-i-create-a-partner-center-account"></a>¿Cómo se crea una cuenta del centro del asociado?

Hay dos formas de crear una cuenta del centro de asociados:

* Si no está familiarizado con el centro de Partners y no tiene una cuenta en Microsoft Network, [cree una cuenta con la página de inscripción del centro de asociados](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment).
* Si ya está inscrito en la red del asociado, [cree una cuenta directamente en el centro de asociados con una inscripción existente](/office/dev/store/).

## <a name="how-do-i-add-my-phone-number-to-the-contact-info-section"></a>¿Cómo agrego mi número de teléfono a la sección información de contacto?

El número de teléfono tiene tres partes: el código de país, el código de área y el número de teléfono. Si alguna sección no es aplicable, escriba el número `0`.

## <a name="why-do-i-get-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>¿Por qué recibo el mensaje? "esta cuenta no es elegible para publicación" cuando intento enviar mi complemento a través del centro de asociados?

Recibirá el mensaje de error anterior cuando el [Estado de verificación de cuenta](/partner-center/verification-responses) esté pendiente. Puede comprobar el estado de verificación de la cuenta en el [Panel](https://partner.microsoft.com/dashboard) del centro de asociados seleccionando la opción de **configuración** (el icono de engranaje) en la esquina superior derecha del shell de encabezado de página y eligiendo opciones de configuración de**cuenta** de**la cuenta de**  =>  **configuración** => de desarrollador.

![Página configuración de la cuenta del centro asociado](../../../assets/images/partner-center-accts-page.png)

![Estado de comprobación del centro de asociados](../../../assets/images/partner-center-verification-status.png)

Durante el proceso de verificación de la cuenta, se mostrará el estado de cada paso necesario (propiedad del correo electrónico, verificación del empleo e comprobación de la empresa). Una vez que el proceso de comprobación se haya completado correctamente, el estado de verificación de la inscripción en la página de perfil cambiará de "pendiente" a "autorizado" y los pasos del proceso ya no se mostrarán.

![Error de comprobación del centro del asociado](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="how-i-do-get-further-support-for-my-account-related-issues"></a>¿Cómo puedo obtener más soporte para mis problemas relacionados con la cuenta?

Visite la [Página ayuda y soporte técnico para partners](https://aka.ms/marketplacepublishersupport) y busque soluciones útiles para la documentación relacionada con su problema. Si las soluciones o documentos autoservicios proporcionados no son útiles para resolver el problema, seleccione **proporcionar detalles de asunto** en la sección **siguiente paso** . Puede buscar el tema del problema en el cuadro de búsqueda o seleccionar **examinar temas**, debajo del cuadro de búsqueda, para profundizar más.

> [!TIP]
> Si está buscando ayuda con un problema de **verificación** de la cuenta:
>
>1. Debajo del **cuadro de búsqueda**, seleccione **examinar temas**.
>1. Seleccione **todos los programas** en el menú desplegable **categoría** .
> 1. Seleccione **cuenta, incorporación y acceso** en el menú desplegable **tema** .
>1. **Seleccione una opción** en el menú desplegable **subtopic** .
>1. Para obtener más ayuda. Seleccione **proporcionar detalles del problema** en la sección **paso siguiente** .
>

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what--should-i-do-next"></a>He revisado mis carpetas de correo y no he recibido el correo electrónico de verificación. ¿Qué debo hacer a continuación?

Intente lo siguiente:

1. Compruebe la carpeta correo no deseado o correo no deseado.
1. Borre la memoria caché del explorador, vaya a su panel de cuenta del centro de asociados y seleccione el vínculo **reenviar correo electrónico de comprobación** para que el correo electrónico de verificación vuelva a enviarse a su dirección de correo electrónico.
1. Intente acceder al vínculo **reenviar correo electrónico de comprobación** desde otro explorador.
1. Trabaje con su Departamento de TI para asegurarse de que el servidor de correo electrónico no bloquea los correos electrónicos de verificación.
1. Ajuste el filtro de correo no deseado del servidor para permitir o lista blanca de todos los correos electrónicos de **maccount@microsoft.<span> </span> com**.

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>¿Cuánto tiempo tarda el proceso de verificación de empleo?

Si todos los detalles se proporcionan correctamente, la verificación del empleo finaliza en 1 a 2 horas.

## <a name="ive-already-reached-out-to-support-is-there-a-way-to-expedite-my-case"></a>Ya he llegado a soporte técnico, ¿hay alguna forma de agilizar mi caso?

Los vales de soporte técnico se resolverán en el plazo de una semana. Busque las actualizaciones que se enviarán al correo electrónico proporcionado cuando se haya producido el vale de soporte técnico.

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>He creado un vale de soporte técnico, tiene 7 días laborables y no he recibido ninguna actualización. ¿Dónde puedo obtener ayuda adicional?

Envíe un correo electrónico a **<teamsubm@microsoft.com>** con los siguientes detalles:

1. **Línea de asunto**. *Problema en la cuenta del centro asociado para <>de App_Name* (especifique el nombre de la aplicación).
2. **Cuerpo del correo electrónico:**
    * Número de incidencia de soporte técnico:
    * Tu identificador de vendedor:
    * Captura de pantalla del problema.

> [!div class="nextstepaction"]
> [Obtenga más información sobre las directivas de validación de aplicaciones para Microsoft Teams](https://docs.microsoft.com/legal/marketplace/certification-policies)
