---
title: Descripción del proceso de envío del almacén de Teams
description: Describe el proceso de envío de aprobación para publicar la aplicación en la tienda de aplicaciones de Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: teams publish store office publishing publish AppSource partner center account verification apps account account not publish eligible app submission
ms.openlocfilehash: 79584ae1eb0be24b4a66e2421f23dd694f8d610f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019898"
---
# <a name="submit-your-app-to-appsource"></a>Enviar la aplicación a AppSource

## <a name="teams-app-submission"></a>Envío de aplicaciones de Teams

Haga que la aplicación esté disponible en el catálogo de aplicaciones de Microsoft Teams y en la web publicandola en [AppSource](https://appsource.microsoft.com). En un nivel alto, el proceso para enviar la aplicación a AppSource es el siguiente:

1. Desarrolla tu aplicación siguiendo las [directrices de diseño.](~/concepts/design/understand-use-cases.md) Las pestañas deben seguir las directrices de diseño de pestañas para dispositivos [de escritorio y web](~/tabs/design/tabs.md) y [móviles.](~/tabs/design/tabs-mobile.md) Los bots deben seguir las [directrices de diseño del bot](~/bots/design/bots.md).
1. Asegúrate de que la aplicación cumple las directivas [de validación de aplicaciones](/legal/marketplace/certification-policies) para Microsoft Teams. 
1. Pruebe la aplicación con la [herramienta de validación manifiesto](prepare/submission-checklist.md#teams-app-validation-tool).
1. Configurar una cuenta [de desarrollador en](/office/dev/store/open-a-developer-account) el Centro de [partners](https://support.microsoft.com/help/4499930/partner-center-overview). *Consulta también* [Cómo crear una cuenta del Centro de partners en](#how-do-i-create-a-partner-center-account) la sección preguntas más frecuentes.
1. Prepare la aplicación para el envío siguiendo la lista [de comprobación de envío.](prepare/submission-checklist.md)
1. Revise los [casos de prueba más fallidos para obtener una aprobación de calidad de la aplicación más rápida.](prepare/frequently-failed-cases.md)
1. Enviar el paquete a [AppSource a través del Centro de partners](/office/dev/store/use-partner-center-to-submit-to-appsource).
1. Realice un seguimiento del proceso de aprobación en el panel del Centro de partners. *Vea* [Información general del Centro de partners](https://support.microsoft.com/help/4499930/partner-center-overview).
1. Después del envío, revisa las instrucciones para mantener y [admitir la aplicación publicada.](post-publish/overview.md)

>[!NOTE]
>
>- La aplicación de Teams debe ser compatible con dispositivos móviles y no cumplir con [los](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment) requisitos de ventas emergentes en el sistema operativo móvil (iOS y Android). 
>- Si la aplicación de Teams contiene un bot, debes cumplir con el Código de conducta [de](https://aka.ms/bf-conduct)Bot Developer Framework .
>- Si la aplicación contiene un conector de Office 365, pueden aplicarse términos adicionales. Vea [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard) y App Developer [Agreement](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm).
>- Para que la aplicación esté disponible para los usuarios de La nube de la comunidad gubernamental (GCC) y para evitar las listas de aplicaciones duplicadas en la tienda, el proceso o flujo de autenticación debe identificar y enrutar al usuario a la dirección URL de contenido especificada o esperada para los usuarios de GCC.

## <a name="faqs--teams-apps-and-partner-account-verification-process-in-partner-center"></a>Preguntas frecuentes: aplicaciones de Teams y proceso de verificación de cuentas de partners en el Centro de partners

## <a name="how-do-i-create-a-partner-center-account"></a>¿Cómo puedo crear una cuenta del Centro de partners?

Hay dos formas de crear una cuenta del Centro de partners:

- Si es nuevo en el Centro de partners y no tiene una cuenta en la red de Microsoft, cree una cuenta mediante la página de inscripción del Centro [de partners](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment).
- Si ya está inscrito en la red de partners, cree una cuenta directamente en el Centro de partners mediante una [página de inscripción existente.](/office/dev/store/)

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a>¿Qué ocurre si no puedo encontrar mi cuenta de la Tienda Office en el Centro de partners?

Abra un [vale de soporte técnico del Centro de partners](https://partner.microsoft.com/support/v2/?stage=1) y seleccione lo siguiente en los menús desplegables:

| Menú | Opción |
| -------   | -------  |
|Categoría| Mercado comercial|
| Tema | Preguntas de ayuda y ayuda general de Marketplace |
| Subtópico| Complemento de Office |

## <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a>¿Dónde puedo obtener soporte técnico para problemas de mi cuenta del Centro de partners?

Visite la [página de soporte técnico de editores](https://aka.ms/marketplacepublishersupport) para buscar el tema del problema y encontrar instrucciones. Si las instrucciones proporcionadas no son útiles, genera un vale de soporte [técnico del Centro de partners.](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)

## <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a>¿Cómo puedo administrar mi cuenta de la Tienda Office en el Centro de partners?

Visite la [cuenta Administrar su cuenta de la Tienda Office a través del Centro de partners](/office/dev/store/manage-account-settings-and-profile) para obtener instrucciones.

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a>¿Cómo agreto mi número de teléfono a la sección de contacto de perfil de socio?

El número de teléfono tiene tres partes, código de país, código de área y número de teléfono. Si el número de teléfono no incluye un código de área, deje el segundo cuadro vacío y complete el tercer cuadro.

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a>¿Cómo puedo administrar la configuración de mi cuenta y el perfil de socio en el Centro de partners?

Visita la [página Administrar la configuración de la cuenta](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) y la información de perfil para obtener instrucciones sobre cómo administrar la configuración de la cuenta del Centro de partners.

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>¿Por qué recibo el mensaje "Esta cuenta no es apta para publicación", cuando intento enviar mi complemento a través del Centro de partners?

Recibirá el mensaje de error anterior cuando el estado de comprobación [de la](/partner-center/verification-responses) cuenta esté pendiente. Compruebe el estado de comprobación de su cuenta en el panel del Centro de [partners.](https://partner.microsoft.com/dashboard) Seleccione **Configuración**, el icono de engranaje en la esquina superior derecha del shell de encabezado de página. Elija **Configuración del programador Configuración** de  =>  **cuenta** Configuración de   =>  **cuenta**.

![Página de configuración de la cuenta del Centro de partners](../../../assets/images/partner-center-accts-page.png)

![Estado de comprobación del Centro de partners](../../../assets/images/partner-center-verification-status.png)

El estado de cada paso necesario, como Propiedad del correo **electrónico,** Verificación de empleo y Verificación **empresarial,** se muestra en el proceso de verificación de la cuenta. Una vez completado el proceso de comprobación, el estado de comprobación de la inscripción en la página de perfil cambia de *pendiente* a *autorizado.* Los pasos del proceso ya no se muestran.

![Error de comprobación del Centro de partners](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="what-is-verified-in-the-partner-center-account-verification-process-and-how-to-respond"></a>¿Qué se comprueba en el proceso de verificación de cuentas del Centro de partners y cómo responder?
Hay tres áreas de verificación, **Propiedad de correo** electrónico, **Empleo** y **Empresa.** Para obtener más información sobre el proceso de verificación, vea [What is verified and how to respond](/partner-center/verification-responses#what-is-verified-and-how-to-respond).
Si eres el contacto principal, administrador global o administrador de cuentas, ve a tu perfil de partner para supervisar el estado de verificación y realizar un seguimiento del progreso.

Una vez completado el proceso de comprobación, el estado de comprobación de la inscripción en la página de perfil cambia de *pendiente* a *autorizado.* Después de la autorización, los pasos del proceso y su estado ya no están disponibles en la página. El contacto principal recibe un correo electrónico de Microsoft en unos días laborables después de que se complete la comprobación.

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-in-the-partner-center-how-should-i-proceed"></a>El estado de comprobación de mi cuenta no ha avanzado más allá de la propiedad del correo electrónico en el Centro de partners. ¿Cómo debo continuar?

Durante el proceso **de comprobación de** propiedad de correo electrónico, se envía un correo electrónico de verificación a la dirección de correo electrónico de contacto principal. Compruebe en la bandeja de entrada de su contacto principal un correo electrónico de **maccount@<span>microsoft</span>.com** con la línea de asunto Acción *necesaria: Comprobar* su cuenta de correo electrónico con Microsoft . Complete el proceso de verificación de correo electrónico. El correo electrónico de verificación se envía a la dirección de correo electrónico que aparece en la página de configuración de la cuenta en el Centro de partners.

> [!NOTE]
> * El vínculo de verificación de correo electrónico solo es válido durante siete días. 
> * Puede solicitarnos que vuelva a enviar el correo electrónico visitando la página de perfil de socio y seleccionando el vínculo Volver a enviar correo electrónico **de verificación.**
> * Para asegurarse de que se recibe el correo electrónico, enumrá el correo microsoft.com como un dominio seguro y compruebe las carpetas de correo no deseado.

## <a name="how-do-i-get-further-support-for-my-account-related-issues"></a>¿Cómo puedo obtener soporte técnico adicional para problemas relacionados con mi cuenta?

Visite la [página Soporte técnico del programa De marketplace](/azure/marketplace/partner-center-portal/support) comercial en el Centro de partners para obtener instrucciones y pasos para crear un vale de soporte técnico.

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what-must-i-do-next"></a>He comprobado mis carpetas de correo y no he recibido el correo electrónico de verificación. ¿Qué debo hacer a continuación?

Pruebe a hacer lo siguiente:
* Compruebe la carpeta de correo no deseado o correo no deseado.
* Borra la caché del explorador, ve al panel  de la cuenta del Centro de partners y selecciona el vínculo Volver a enviar el correo electrónico de verificación para que el correo electrónico de verificación se resiente en tu dirección de correo electrónico.
* Intente obtener acceso al vínculo Volver a **enviar correo** electrónico de verificación desde un explorador diferente.
* Trabaje con su departamento de TI para asegurarse de que el servidor de correo electrónico no bloquee los correos electrónicos de verificación.
* Ajuste el filtro de correo no deseado del servidor para permitir o enumerar de forma segura todos los correos electrónicos de **maccount@microsoft. <span></span> com**.

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>¿Cuánto tiempo suele tardar el proceso de verificación de empleo?

Si todos los detalles enviados son correctos, el proceso de verificación de empleo tarda aproximadamente dos horas en completarse.

## <a name="how-long-does-the-business-verification-process-usually-take"></a>¿Cuánto tiempo suele tardar el proceso de verificación empresarial?

Si se envían todos los documentos necesarios, la comprobación empresarial tarda de uno a dos días laborables en completarse.

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a>Si me puedo acercar al equipo de soporte técnico, ¿se acelerará mi vale?

Los vales de soporte técnico se resuelven en una semana. Compruebe si hay actualizaciones enviadas al identificador de correo electrónico proporcionado al generar el vale de soporte técnico.

## <a name="my-issue-is-not-listed-here-are-there-other-pages-i-can-reference-for-partner-center-issues"></a>Mi problema no aparece aquí. ¿Hay otras páginas a las que pueda hacer referencia para problemas del Centro de partners?

Consulte la [documentación del mercado comercial](/azure/marketplace/) para obtener más ayuda.

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>He creado un vale de soporte técnico, han pasado 7 días laborables y no he recibido ninguna actualización. ¿Dónde puedo obtener ayuda adicional?

Envíe un correo electrónico **<teamsubm@microsoft.com>** con los siguientes detalles:

* **Línea de asunto:** Problema de cuenta del Centro de partners <App_Name> (especifique el nombre de la aplicación).
* **Cuerpo del correo** electrónico :
    * Número de vale de soporte técnico
    * Su id. de vendedor
    * Captura de pantalla del problema (si es posible)
    
## <a name="app-category-mapping"></a>Asignación de categorías de aplicaciones

| Categoría Teams       | Categorías de PC  |
|:---------------------|:---------------|
| Análisis e BI | Análisis, visualización de datos e BI |
| Desarrollador y IT | Herramientas para desarrolladores, administrador de TI |
| Educación | Educación |
| Recursos humanos | Recursos humanos y contratación |
| Productividad | Administración de contenido, archivos y documentos, productividad, aprendizaje y tutoriales y utilidades |
| Administración de proyectos | Comunicación, Administración de proyectos, Flujo de trabajo y Administración de empresas |
| Ventas y soporte técnico | Administración de clientes y contactos, soporte al cliente, administración financiera, ventas y marketing |
| Social y divertido | Galerías de imágenes y vídeo, Estilo de vida, Noticias y Tiempo, Social, Viajes y Navegación |

>
> [!div class="nextstepaction"]
> [Más información sobre las directivas de validación de aplicaciones para Microsoft Teams](/legal/marketplace/certification-policies)
