---
title: Guía del proceso de aprobación de aplicaciones de Microsoft Teams
description: Describe el proceso de aprobación para publicar la aplicación en la tienda de aplicaciones de Microsoft Teams
keywords: publicación de la tienda Office de tienda de AppSource
ms.openlocfilehash: b3efdf81aa4ecf79fb19375cb4ee5377fcad2f7f
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652200"
---
# <a name="understanding-the-appsource-submission-process"></a>Descripción del proceso de envío de AppSource

## <a name="teams-app-submission"></a>Envío de aplicación de Teams

La publicación de la aplicación en [Microsoft AppSource](https://appsource.microsoft.com) hace que esté disponible en el catálogo de aplicaciones de Microsoft Teams y en la Web. En un nivel alto, el proceso para enviar la aplicación a AppSource es:

1. Desarrolle su aplicación siguiendo nuestras [pautas de diseño](~/concepts/design/understand-use-cases.md). Las pestañas deben seguir nuestras [instrucciones de diseño de pestañas](~/tabs/design/tabs.md). Los bots deben seguir las [directrices de diseño de bot](~/bots/design/bots.md).
1. Asegúrese de que su aplicación cumple las [directivas de validación](/legal/marketplace/certification-policies) de aplicaciones de Microsoft Teams.
1. [Configure una cuenta de Desarrollador en el](/office/dev/store/open-a-developer-account) [centro de Partners](https://support.microsoft.com/help/4499930/partner-center-overview). *Consulte también* [Cómo crear una cuenta del centro de asociados](#how-do-i-create-a-partner-center-account) en la sección Preguntas más frecuentes, a continuación.
1. Prepare la aplicación para el envío siguiendo nuestra [lista de comprobación de envío](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).
1. Revise nuestras [sugerencias para obtener un envío de aplicación correcto](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md).
1. Envíe el paquete a [AppSource a través del centro de asociados](/office/dev/store/use-partner-center-to-submit-to-appsource).
1. Realice un seguimiento del proceso de aprobación en el panel del centro de asociados. *Consulte* [información general sobre el centro de Partners](https://support.microsoft.com/help/4499930/partner-center-overview).
1. Post subenvío: revise nuestras instrucciones para [mantener y dar soporte a su aplicación publicada](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).

>[!NOTE]
>
>- Si la aplicación de Microsoft Teams contiene un bot, debe cumplir con el [código de conducta del marco del desarrollador de](https://aka.ms/bf-conduct)bot? n.
>- Si la aplicación contiene un conector de Office 365, es posible que se apliquen términos adicionales. *Vea* [Connector Dashboard Developer's Dashboard](https://aka.ms/connectorsdashboard) and [App Developer Agreement](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm).

## <a name="faqs--teams-apps-and-partner-accounts"></a>Preguntas más frecuentes: las aplicaciones de Microsoft Teams y las cuentas de asociados

## <a name="how-do-i-create-a-partner-center-account"></a>¿Cómo se crea una cuenta del centro del asociado?

Hay dos formas de crear una cuenta del centro de asociados:

- Si no está familiarizado con el centro de Partners y no tiene una cuenta en Microsoft Network, [cree una cuenta con la página de inscripción del centro de asociados](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment).
- Si ya está inscrito en la red del asociado, [cree una cuenta directamente en el centro de asociados con una inscripción existente](/office/dev/store/).

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a>¿Qué ocurre si no encuentro mi cuenta de la tienda Office en el centro para socios?

Abra un [vale de soporte técnico del centro de asociados](https://partner.microsoft.com/support/v2/?stage=1) y seleccione lo siguiente en los menús desplegables:

| Menú | Opción |
| -------   | -------  |
|Categoría| Mercado comercial|
| Tema | Ayuda general de Marketplace y preguntas sobre procedimientos |
| Tema secundario| Complemento de Office |

## <a name="where-can-i-get-support-for-my-partner-center-issues"></a>¿Dónde puedo obtener soporte para mis problemas con el centro de Partners?

Visite nuestra [Página de soporte técnico de Publishers](https://aka.ms/marketplacepublishersupport) para buscar su tema de problemas y buscar instrucciones. Si las instrucciones proporcionadas no le resultan útiles, [abra un vale de soporte técnico del centro de asociados](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket).

## <a name="how-do-i-manage-my-office-store-account"></a>¿Cómo puedo administrar mi cuenta de la tienda Office?

Visite nuestra  [cuenta de administración de la tienda Office en el centro de Partners](/office/dev/store/manage-account-settings-and-profile) para obtener instrucciones sobre cómo administrar la cuenta de la tienda Office a través del centro de asociados.

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a>¿Cómo agrego mi número de teléfono a la sección de contacto del perfil del socio?

El número de teléfono tiene tres partes: el código de país, el código de área y el número de teléfono. Si su número de teléfono no incluye un código de área, deje el segundo cuadro vacío y rellene el tercer cuadro.

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a>¿Cómo puedo administrar la configuración de mi cuenta y el perfil de asociados en el centro de Partners?

Visite nuestra página [administrar la configuración de la cuenta y la información del perfil](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) para obtener instrucciones sobre cómo administrar la configuración de la cuenta del centro de asociados.

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>¿Por qué recibo el mensaje "esta cuenta no es elegible para publicación" cuando intento enviar mi complemento a través del centro de asociados?

Recibirá el mensaje de error anterior cuando el [Estado de verificación de cuenta](/partner-center/verification-responses) esté pendiente. Puede comprobar el estado de verificación de la cuenta en el [Panel](https://partner.microsoft.com/dashboard) del centro de asociados seleccionando la opción de **configuración** (el icono de engranaje) en la esquina superior derecha del shell de encabezado de página y eligiendo opciones de configuración de cuenta de la cuenta de **configuración de desarrollador**  =>  **Account**   =>  **Account settings** .

![Página configuración de la cuenta del centro asociado](../../assets/images/partner-center-accts-page.png)

![Estado de comprobación del centro de asociados](../../assets/images/partner-center-verification-status.png)

Durante el proceso de verificación de la cuenta, se mostrará el estado de cada paso necesario (propiedad del correo electrónico, verificación del empleo e comprobación de la empresa). Una vez que el proceso de comprobación se haya completado correctamente, el estado de verificación de la inscripción en la página de perfil cambiará de "pendiente" a "autorizado" y los pasos del proceso ya no se mostrarán.

![Error de comprobación del centro del asociado](../../assets/images/partner-center-acct-verification-error.png)

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-how-should-i-proceed"></a>El estado de comprobación de mi cuenta no se ha avanzado más allá de la propiedad del correo electrónico. ¿Cómo debo continuar?

Durante el proceso de comprobación de la **propiedad del correo electrónico** , se envía un correo electrónico de verificación a la dirección de correo electrónico de contacto principal. Consulte la bandeja de entrada del contacto principal para ver si hay un correo electrónico de **maccount@<span>Microsoft</span>. com** con la acción de línea de asunto *necesaria: Compruebe su cuenta de correo electrónico con Microsoft*y solicite que complete el proceso de comprobación de correo electrónico. El correo electrónico de comprobación se enviará a la dirección de correo electrónico que aparece en la página Configuración de la cuenta del centro de asociados.

> [!NOTE]
 >El vínculo de comprobación de correo electrónico solo es válido durante 7 días. Puede solicitar que se le reenvíe el correo electrónico visitando la página de Perfil de socio y seleccionar el vínculo **reenviar correo electrónico de verificación** . Para asegurarse de que se recibe el correo electrónico, consulte el correo electrónico de la lista blanca de microsoft.com como un dominio seguro y compruebe las carpetas de correo no deseado.

## <a name="how-i-do-get-further-support-for-my-account-related-issues"></a>¿Cómo puedo obtener más soporte para mis problemas relacionados con la cuenta?

Para obtener instrucciones y pasos para crear un vale de soporte, visite nuestra página de [soporte técnico para el servicio de catálogo de soluciones comerciales en el centro de Partners](/azure/marketplace/partner-center-portal/support) .

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what--should-i-do-next"></a>He revisado mis carpetas de correo y no he recibido el correo electrónico de verificación. ¿Qué debo hacer a continuación?

Intente lo siguiente:

1. Compruebe la carpeta correo no deseado o correo no deseado.
1. Borre la memoria caché del explorador, vaya a su panel de cuenta del centro de asociados y seleccione el vínculo **reenviar correo electrónico de comprobación** para que el correo electrónico de verificación vuelva a enviarse a su dirección de correo electrónico.
1. Intente acceder al vínculo  **reenviar correo electrónico de comprobación** desde otro explorador.
1. Trabaje con su Departamento de TI para asegurarse de que el servidor de correo electrónico no bloquea los correos electrónicos de verificación.
1. Ajuste el filtro de correo no deseado del servidor para permitir o lista blanca de todos los correos electrónicos de **maccount@microsoft. <span></span> com**.

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>¿Cuánto tiempo tarda el proceso de verificación de empleo?

Si todos los detalles enviados son correctos, la verificación del empleo finaliza en 1 a 2 horas.

## <a name="how-long-does-the-business-verification-process-usually-take"></a>¿Cuánto tiempo tarda el proceso de "comprobación empresarial"?

La comprobación de la empresa tarda de 1 a 2 días laborales en completarse, siempre que se hayan enviado todos los documentos necesarios.

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a>Si me pongo en contacto con el equipo de soporte técnico, ¿se le proporcionará la solicitud rápida?

Los vales de soporte técnico se resolverán en el plazo de una semana. Busque las actualizaciones que se enviarán al correo electrónico proporcionado cuando se haya producido el vale de soporte técnico.

## <a name="my-issue-is-not-listed-here--are-there-other-pages-i-can-reference-for-partner-center-issues"></a>Mi problema no aparece aquí.  ¿Hay otras páginas a las que pueda hacer referencia para los problemas del centro de asociados?

Para obtener más ayuda, consulte nuestra [documentación de mercado comercial](/azure/marketplace/) .

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>He creado un vale de soporte técnico, tiene 7 días laborables y no he recibido ninguna actualización. ¿Dónde puedo obtener ayuda adicional?

Envíe un correo electrónico a **<teamsubm@microsoft.com>** con los siguientes detalles:

1. **Línea de asunto**. *Problema en la cuenta del centro asociado para <>de App_Name * (especifique el nombre de la aplicación).
1. **Cuerpo del correo electrónico:**
    * Número de incidencia de soporte técnico:
    * Tu identificador de vendedor:
    * Captura de pantalla del problema (si es posible):

>
> [!div class="nextstepaction"]
> [Obtenga más información sobre las directivas de validación de aplicaciones para Microsoft Teams](/legal/marketplace/certification-policies)