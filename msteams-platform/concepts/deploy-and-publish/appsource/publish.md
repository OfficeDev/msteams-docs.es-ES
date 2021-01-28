---
title: Descripción del proceso de envío al almacén de Teams
description: Describe el proceso de envío de aprobación para publicar la aplicación en la tienda de aplicaciones de Microsoft Teams
ms.topic: overview
keywords: Teams publicar la publicación de la tienda de publicación de la cuenta del Centro de partners de AppSource cuenta de aplicaciones de verificación no publicar envío de aplicación elegible
ms.openlocfilehash: d2dc624c6dd13896397041c5c69ce5c5eb471a5b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014414"
---
# <a name="submit-your-app-to-appsource"></a>Enviar la aplicación a AppSource

## <a name="teams-app-submission"></a>Envío de aplicaciones de Teams

Haga que la aplicación esté disponible en el catálogo de aplicaciones de Microsoft Teams y en la web publicando en [AppSource.](https://appsource.microsoft.com) En un nivel alto, el proceso para enviar la aplicación a AppSource es el siguiente:

1. Desarrolle la aplicación siguiendo las [directrices de diseño.](~/concepts/design/understand-use-cases.md) Las pestañas deben seguir las directrices de [](~/tabs/design/tabs-mobile.md)diseño de pestañas para dispositivos móviles y [de escritorio.](~/tabs/design/tabs.md) Los bots deben seguir las [directrices de diseño del bot.](~/bots/design/bots.md)
1. Asegúrese de que la aplicación cumple las directivas [de validación de](/legal/marketplace/certification-policies) aplicaciones para Microsoft Teams. 
1. Pruebe la aplicación con la herramienta [de validación de manifiesto.](prepare/submission-checklist.md#teams-app-validation-tool)
1. Configura una cuenta [de desarrollador en](/office/dev/store/open-a-developer-account) el Centro de [partners.](https://support.microsoft.com/help/4499930/partner-center-overview) *Consulta también* [Cómo crear una cuenta del Centro de partners](#how-do-i-create-a-partner-center-account) en la sección preguntas más frecuentes.
1. Prepara la aplicación para el envío siguiendo la lista [de comprobación de envío.](prepare/submission-checklist.md)
1. Revisa los [casos de prueba más fallidos para obtener una aprobación de calidad de la](prepare/frequently-failed-cases.md)aplicación más rápida.
1. Envía el paquete a [AppSource a través del Centro de partners.](/office/dev/store/use-partner-center-to-submit-to-appsource)
1. Realiza un seguimiento del proceso de aprobación en el panel del Centro de partners. *Consulta Información* [general del Centro de partners.](https://support.microsoft.com/help/4499930/partner-center-overview)
1. Después del envío, revisa las instrucciones para mantener y [admitir la aplicación publicada.](post-publish/overview.md)

>[!NOTE]
>
>- La aplicación de Teams debe ser dinámica para dispositivos móviles y no cumplir con [los](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment) requisitos de ventas en el sistema operativo móvil (iOS y Android). 
>- Si la aplicación de Teams contiene un bot, debe cumplir con el código de conducta de Bot Developer [Framework.](https://aka.ms/bf-conduct)
>- Si la aplicación contiene un conector de Office 365, pueden aplicarse términos adicionales. Vea [El panel del programador de conectores](https://aka.ms/connectorsdashboard) y el acuerdo para [desarrolladores de aplicaciones.](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)
>- Para que la aplicación esté disponible para los usuarios de Government Community Cloud (GCC) y para evitar des listados de aplicaciones duplicados en la tienda, el flujo o proceso de autenticación debe identificar y enrutar al usuario a la dirección URL de contenido especificada o esperada para los usuarios de GCC.

## <a name="faqs--teams-apps-and-partner-account-verification-process-in-partner-center"></a>Preguntas más frecuentes: proceso de comprobación de aplicaciones de Teams y cuenta de partner en el Centro de partners

## <a name="how-do-i-create-a-partner-center-account"></a>¿Cómo puedo crear una cuenta del Centro de partners?

Hay dos formas de crear una cuenta del Centro de partners:

- Si no estás en el Centro de partners y no tienes una cuenta en la red de Microsoft, crea una cuenta con la página de inscripción del [Centro de partners.](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)
- Si ya estás inscrito en la Red de partners, crea una cuenta directamente en el Centro de partners mediante una [página de inscripción existente.](/office/dev/store/)

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a>¿Qué ocurre si no puedo encontrar mi cuenta de la Tienda Office en el Centro de partners?

Abre un [vale de soporte técnico del Centro](https://partner.microsoft.com/support/v2/?stage=1) de partners y selecciona lo siguiente en los menús desplegables:

| Menú | Opción |
| -------   | -------  |
|Categoría| Mercado comercial|
| Tema | Preguntas generales sobre ayuda y ayuda del catálogo de soluciones |
| Subtopic| Complemento de Office |

## <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a>¿Dónde puedo obtener soporte técnico para los problemas de mi cuenta del Centro de partners?

Visite la [página de soporte técnico de los](https://aka.ms/marketplacepublishersupport) editores para buscar el tema del problema y encontrar instrucciones. Si las instrucciones proporcionadas no son útiles, genera un vale de soporte [técnico del Centro de partners.](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)

## <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a>¿Cómo puedo administrar mi cuenta de la Tienda Office en el Centro de partners?

Visite la [cuenta Administrar la Tienda Office a través del Centro de partners](/office/dev/store/manage-account-settings-and-profile) para obtener instrucciones.

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a>¿Cómo agrero mi número de teléfono a la sección de contacto de perfil de partner?

El número de teléfono tiene tres partes, código de país, código de área y número de teléfono. Si el número de teléfono no incluye un código de área, deje el segundo cuadro vacío y complete el tercer cuadro.

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a>¿Cómo puedo administrar la configuración de mi cuenta y mi perfil de partner en el Centro de partners?

Visita la [página Administrar la configuración de la](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) cuenta y la información de perfil para obtener instrucciones sobre cómo administrar la configuración de la cuenta del Centro de partners.

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>¿Por qué recibo el mensaje "Esta cuenta no es apta para la publicación" cuando intento enviar el complemento a través del Centro de partners?

Recibirá el mensaje de error anterior cuando el estado [de comprobación de su](/partner-center/verification-responses) cuenta esté pendiente. Comprueba el estado de comprobación de tu cuenta en el panel del Centro de [partners.](https://partner.microsoft.com/dashboard) Seleccione **Configuración**, el icono de engranaje en la esquina superior derecha del shell de encabezado de página. Elija configuración **de la cuenta de la** cuenta de configuración del  =>     =>  **desarrollador.**

![Página de configuración de la cuenta del Centro de partners](../../../assets/images/partner-center-accts-page.png)

![Estado de verificación del Centro de partners](../../../assets/images/partner-center-verification-status.png)

El estado de cada paso necesario, como propiedad del correo **electrónico,** verificación de empleo y verificación **empresarial,** se muestra en el proceso de comprobación de la cuenta. Una vez completado el proceso de verificación, el estado de comprobación de la inscripción en la página de perfil cambia de *pendiente* a *autorizado.* Los pasos del proceso ya no se muestran.

![Error de verificación del Centro de partners](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="what-is-verified-in-the-partner-center-account-verification-process-and-how-to-respond"></a>¿Qué se comprueba en el proceso de verificación de la cuenta del Centro de partners y cómo responder?
Hay tres áreas de verificación: **Propiedad del** correo electrónico, **Empleo** y **Empresa.** Para obtener más información sobre el proceso de comprobación, vea [Qué se comprueba y cómo responder.](/partner-center/verification-responses#what-is-verified-and-how-to-respond)
Si eres el contacto principal, el administrador global o el administrador de la cuenta, ve a tu perfil de partner para supervisar el estado de comprobación y realizar un seguimiento del progreso.

Una vez completado el proceso de verificación, el estado de comprobación de la inscripción en la página de perfil cambia de *pendiente* a *autorizado.* Después de la autorización, los pasos del proceso y su estado ya no están disponibles en la página. El contacto principal recibe un correo electrónico de Microsoft en unos días laborables después de que se complete la comprobación.

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-in-the-partner-center-how-should-i-proceed"></a>El estado de comprobación de mi cuenta no ha avanzado más allá de la propiedad del correo electrónico en el Centro de partners. ¿Cómo debo continuar?

Durante el proceso **de comprobación de la** propiedad del correo electrónico, se envía un correo electrónico de verificación a la dirección de correo electrónico de contacto principal. Compruebe su bandeja de entrada de contacto principal para obtener un correo electrónico de **maccount@<span>microsoft</span>.com** con la línea de asunto Acción *necesaria: Compruebe* su cuenta de correo electrónico con Microsoft . Complete el proceso de comprobación de correo electrónico. El correo electrónico de verificación se envía a la dirección de correo electrónico que aparece en la página de configuración de tu cuenta en el Centro de partners.

> [!NOTE]
> * El vínculo de verificación de correo electrónico solo es válido durante siete días. 
> * Puedes solicitarnos que vuelvas a enviar el correo electrónico visitando la página de perfil de tu partner y seleccionando el **vínculo** de correo electrónico de comprobación volver a enviar.
> * Para asegurarse de que se recibe el correo electrónico, enume el correo electrónico de microsoft.com como dominio seguro y compruebe las carpetas de correo no deseado.

## <a name="how-do-i-get-further-support-for-my-account-related-issues"></a>¿Cómo puedo obtener soporte técnico adicional para problemas relacionados con mi cuenta?

Visita la [página Soporte técnico del programa Mercado comercial](/azure/marketplace/partner-center-portal/support) en el Centro de partners para obtener instrucciones y pasos para crear un vale de soporte técnico.

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what-must-i-do-next"></a>He comprobado mis carpetas de correo y no he recibido el correo electrónico de verificación. ¿Qué debo hacer a continuación?

Pruebe a hacer lo siguiente:
* Compruebe su carpeta de correo no deseado o correo no deseado.
* Borra la memoria caché del explorador, ve al  panel de la cuenta del Centro de partners y selecciona el vínculo de correo electrónico volver a enviar la verificación para que el correo electrónico de verificación se reenvia a tu dirección de correo electrónico.
* Intente obtener acceso al **vínculo de correo electrónico de verificación Volver** a enviar desde otro explorador.
* Trabaje con su departamento de TI para asegurarse de que el servidor de correo electrónico no bloquee los correos electrónicos de verificación.
* Ajuste el filtro de correo no deseado del servidor para permitir o enumerar de forma segura todos los correos electrónicos de **maccount@microsoft. <span></span> com**.

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>¿Cuánto tiempo suele tardar el proceso de verificación de empleo?

Si todos los detalles enviados son correctos, el proceso de comprobación del empleo tarda aproximadamente dos horas en completarse.

## <a name="how-long-does-the-business-verification-process-usually-take"></a>¿Cuánto tiempo suele tardar el proceso de verificación empresarial?

Si se envían todos los documentos necesarios, la verificación empresarial tarda de uno a dos días laborables en completarse.

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a>If I reach out to the support team, will my ticket be expedited?

Los vales de soporte técnico se resuelven en una semana. Compruebe si hay actualizaciones enviadas al identificador de correo electrónico proporcionado al generar el vale de soporte técnico.

## <a name="my-issue-is-not-listed-here-are-there-other-pages-i-can-reference-for-partner-center-issues"></a>Mi problema no aparece aquí. ¿Hay otras páginas a las que pueda hacer referencia para problemas del Centro de partners?

Consulte la documentación [del mercado comercial](/azure/marketplace/) para obtener más ayuda.

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>He creado un vale de soporte técnico, han pasado 7 días laborables y no he recibido ninguna actualización. ¿Dónde puedo obtener ayuda adicional?

Envíe un correo **<teamsubm@microsoft.com>** electrónico con los siguientes detalles:

* **Línea de asunto:** problema de cuenta del Centro de partners <App_Name> (especifica el nombre de la aplicación).
* **Cuerpo del correo** electrónico:
    * Número de vale de soporte técnico
    * Su id. de vendedor
    * Captura de pantalla del problema (si es posible)
    
## <a name="app-category-mapping"></a>Asignación de categorías de aplicaciones

| Categoría teams       | Categorías de PC  |
|:---------------------|:---------------|
| Análisis e BI | Análisis, visualización de datos e BI |
| Desarrollador e IT | Herramientas de desarrollo, administrador de TI |
| Educación | Educación |
| Recursos humanos | Recursos humanos y contratación |
| Productividad | Administración de contenido, archivos y documentos, productividad, aprendizaje y tutoriales, y utilidades |
| Administración de proyectos | Comunicación, administración de proyectos, flujo de trabajo y administración empresarial |
| Ventas y soporte técnico | Administración de clientes y contactos, soporte al cliente, administración financiera, ventas y marketing |
| Social y divertido | Galerías de imágenes y vídeos, estilo de vida, noticias y tiempo, redes sociales, viajes y navegación |

>
> [!div class="nextstepaction"]
> [Más información sobre las directivas de validación de aplicaciones para Microsoft Teams](/legal/marketplace/certification-policies)
