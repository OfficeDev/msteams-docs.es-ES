---
title: Enviar la aplicación al Centro de partners
description: Obtén información sobre cómo crear una cuenta del Centro de partners y enviar la aplicación para la validación de la tienda.
author: heath-hamilton
ms.author: lajanuar
ms.topic: how-to
ms.openlocfilehash: 732e283bffc253743e890b0c45dc7b0689108716
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101927"
---
# <a name="submit-your-microsoft-teams-app-to-partner-center"></a>Enviar la aplicación Microsoft Teams al Centro de partners

Después de preparar el envío de la tienda, puedes enviar la aplicación oficialmente para su revisión.

## <a name="create-a-partner-center-account"></a>Crear una cuenta del Centro de partners

Para publicar la aplicación en la tienda Teams y AppSource, primero debes [configurar una cuenta de desarrollador.](https://docs.microsoft.com/office/dev/store/open-a-developer-account)

## <a name="submit-your-app"></a>Enviar la aplicación

Para enviar la aplicación, sigue estas instrucciones de [envío paso a paso del almacén](https://docs.microsoft.com/office/dev/store/add-in-submission-guide). Al crear un nuevo envío, especifica que estás enviando una Teams aplicación.

### <a name="app-category-mapping"></a>Asignación de categorías de aplicaciones

Durante el envío, se te pide que clasifices tu aplicación. En la tabla siguiente se Teams categorías de almacén a las categorías enumeradas en el Centro de partners.

| Teams categorías       | Categorías del Centro de partners  |
|:---------------------|:---------------|
| Análisis e BI | Análisis, visualización de datos e BI |
| Desarrollador y IT | Herramientas para desarrolladores, administrador de TI |
| Educación | Educación |
| Recursos humanos | Recursos humanos y contratación |
| Productividad | Administración de contenido, archivos y documentos, productividad, aprendizaje y tutoriales y utilidades |
| Administración de proyectos | Administración de Project, flujo de trabajo y administración empresarial |
| Ventas y soporte técnico | Administración de clientes y contactos, soporte al cliente, administración financiera, ventas y marketing |
| Social y divertido | Galerías de imágenes y vídeo, Estilo de vida, Noticias y Tiempo, Social, Viajes y Navegación |

### <a name="3-fix-issues-with-your-submission"></a>3. Corregir problemas con el envío

Si la aplicación falla el envío, recibirás un informe de errores para que sepas qué corregir y volver a enviar. Microsoft también proporciona un servicio de guante blanco para ayudar a que la aplicación aparezca en la lista.

## <a name="faqs"></a>Preguntas frecuentes

### <a name="how-do-i-create-a-partner-center-account"></a>¿Cómo puedo crear una cuenta del Centro de partners?

Puede crear una cuenta del Centro de partners de una de las siguientes maneras:

- Si es nuevo en el Centro de partners y no tiene una cuenta en la red de Microsoft, cree una cuenta mediante la página de inscripción del Centro [de partners.](/office/dev/store/open-a-developer-account#create-an-account-using-the-partner-center-enrollment-page)
- Si ya está inscrito en la red de partners, cree una cuenta directamente en el Centro de partners mediante una [página de inscripción existente.](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)

### <a name="what-if-i-cant-find-my-office-store-account-in-partner-center"></a>¿Qué sucede si no puedo encontrar mi cuenta Office store en el Centro de partners?

Abra un [vale de soporte técnico del Centro de partners](https://partner.microsoft.com/support/v2/?stage=1) y seleccione lo siguiente en los menús desplegables:

| Menú | Opción |
| -------   | -------  |
|Categoría| Mercado comercial|
| Tema | Preguntas de ayuda y ayuda general de Marketplace |
| Subtópico| Complemento de Office |

### <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a>¿Dónde puedo obtener soporte técnico para problemas de mi cuenta del Centro de partners?

Visite la [página de soporte técnico de editores](https://aka.ms/marketplacepublishersupport) para buscar el tema del problema y encontrar instrucciones. Si las instrucciones proporcionadas no son útiles, genera un vale de soporte [técnico del Centro de partners.](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)

### <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a>¿Cómo puedo administrar mi cuenta Office store en el Centro de partners?

Visita la [cuenta Administrar tu Office store a través del Centro de partners](/office/dev/store/manage-account-settings-and-profile) para obtener instrucciones.

### <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a>¿Cómo agreto mi número de teléfono a la sección de contacto de perfil de socio?

El número de teléfono tiene tres partes, código de país, código de área y número de teléfono. Si el número de teléfono no incluye un código de área, deje el segundo cuadro vacío y complete el tercer cuadro.

### <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a>¿Cómo puedo administrar la configuración de mi cuenta y el perfil de socio en el Centro de partners?

Visita la [página Administrar la configuración de la cuenta](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) y la información de perfil para obtener instrucciones sobre cómo administrar la configuración de la cuenta del Centro de partners.

### <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-app"></a>¿Por qué recibo el mensaje "Esta cuenta no es apta para publicación" cuando intento enviar mi aplicación?

Recibirá el mensaje de error anterior cuando el estado de comprobación [de la](/partner-center/verification-responses) cuenta esté pendiente. Compruebe el estado de comprobación de su cuenta en el panel del Centro de [partners.](https://partner.microsoft.com/dashboard) Seleccione **Configuración**, el icono de engranaje en la esquina superior derecha del shell de encabezado de página. Elija **Configuración del programador Configuración** de  =>  **cuenta** Configuración de   =>  **cuenta**.

![Página de configuración de la cuenta del Centro de partners](../../../assets/images/partner-center-accts-page.png)

![Estado de comprobación del Centro de partners](../../../assets/images/partner-center-verification-status.png)

El estado de cada paso necesario, como Propiedad del correo **electrónico,** Verificación de empleo y Verificación **empresarial,** se muestra en el proceso de verificación de la cuenta. Una vez completado el proceso de comprobación, el estado de comprobación de la inscripción en la página de perfil cambia de *pendiente* a *autorizado.* Los pasos del proceso ya no se muestran.

![Error de comprobación del Centro de partners](../../../assets/images/partner-center-acct-verification-error.png)

### <a name="what-is-verified-in-the-partner-center-account-verification-process-and-how-to-respond"></a>¿Qué se comprueba en el proceso de verificación de cuentas del Centro de partners y cómo responder?

Hay tres áreas de verificación, **Propiedad de correo** electrónico, **Empleo** y **Empresa.** Para obtener más información sobre el proceso de verificación, vea [What is verified and how to respond](/partner-center/verification-responses#what-is-verified-and-how-to-respond).
Si eres el contacto principal, administrador global o administrador de cuentas, ve a tu perfil de partner para supervisar el estado de verificación y realizar un seguimiento del progreso.

Una vez completado el proceso de comprobación, el estado de comprobación de la inscripción en la página de perfil cambia de *pendiente* a *autorizado.* Después de la autorización, los pasos del proceso y su estado ya no están disponibles en la página. El contacto principal recibe un correo electrónico de Microsoft en unos días laborables después de que se complete la comprobación.

### <a name="my-account-verification-status-hasnt-advanced-beyond-email-ownership-how-should-i-proceed"></a>El estado de comprobación de mi cuenta no ha avanzado más allá de la propiedad del correo electrónico. ¿Cómo debo continuar?

Durante el proceso **de comprobación de** propiedad de correo electrónico, se envía un correo electrónico de verificación a la dirección de correo electrónico de contacto principal. Compruebe en la bandeja de entrada de su contacto principal un correo electrónico de **maccount@<span>microsoft</span>.com** con la línea de asunto Acción *necesaria: Comprobar* su cuenta de correo electrónico con Microsoft . Complete el proceso de verificación de correo electrónico. El correo electrónico de verificación se envía a la dirección de correo electrónico que aparece en la página de configuración de la cuenta en el Centro de partners.

> [!NOTE]
> * El vínculo de verificación de correo electrónico solo es válido durante siete días. 
> * Puede solicitarnos que vuelva a enviar el correo electrónico visitando la página de perfil de socio y seleccionando el vínculo Volver a enviar correo electrónico **de verificación.**
> * Para asegurarse de que se recibe el correo electrónico, enumrá el correo microsoft.com como un dominio seguro y compruebe las carpetas de correo no deseado.

### <a name="how-do-i-get-further-support-for-my-account-related-issues"></a>¿Cómo puedo obtener más soporte técnico para los problemas relacionados con mi cuenta?

Visite la [página Soporte técnico del programa De marketplace](/azure/marketplace/partner-center-portal/support) comercial en el Centro de partners para obtener instrucciones y pasos para crear un vale de soporte técnico.

### <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what-must-i-do-next"></a>He comprobado mis carpetas de correo y no he recibido el correo electrónico de verificación. ¿Qué debo hacer a continuación?

Pruebe a hacer lo siguiente:
* Compruebe la carpeta de correo no deseado o correo no deseado.
* Borra la caché del explorador, ve al panel  de la cuenta del Centro de partners y selecciona el vínculo Volver a enviar el correo electrónico de verificación para que el correo electrónico de verificación se resiente en tu dirección de correo electrónico.
* Intente obtener acceso al vínculo Volver a **enviar correo** electrónico de verificación desde un explorador diferente.
* Trabaje con su departamento de TI para asegurarse de que el servidor de correo electrónico no bloquee los correos electrónicos de verificación.
* Ajuste el filtro de correo no deseado del servidor para permitir o enumerar de forma segura todos los correos electrónicos de **maccount@microsoft. <span></span> com**.

### <a name="how-long-does-the-employment-verification-process-usually-take"></a>¿Cuánto tiempo suele tardar el proceso de verificación de empleo?

Si todos los detalles enviados son correctos, el proceso de verificación de empleo tarda aproximadamente dos horas en completarse.

### <a name="how-long-does-the-business-verification-process-usually-take"></a>¿Cuánto tiempo suele tardar el proceso de verificación empresarial?

Si se envían todos los documentos necesarios, la comprobación empresarial tarda de uno a dos días laborables en completarse.

### <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a>Si me puedo acercar al equipo de soporte técnico, ¿se acelerará mi vale?

Los vales de soporte técnico se resuelven en una semana. Compruebe si hay actualizaciones enviadas al identificador de correo electrónico proporcionado al generar el vale de soporte técnico.

### <a name="my-issue-is-not-listed-here-are-there-other-pages-i-can-reference-for-partner-center-issues"></a>Mi problema no aparece aquí. ¿Hay otras páginas a las que pueda hacer referencia para problemas del Centro de partners?

Consulte la [documentación del mercado comercial](/azure/marketplace/) para obtener más ayuda.

### <a name="ive-created-a-support-ticket-and-i-havent-received-an-update-in-7-business-days-where-can-i-get-help"></a>He creado un vale de soporte técnico y no he recibido una actualización en 7 días laborables. ¿Dónde puedo obtener ayuda?

Envíe un correo electrónico **<teamsubm@microsoft.com>** con los siguientes detalles:

* **Línea de asunto:** Problema de cuenta del Centro de partners <App_Name> (especifique el nombre de la aplicación).
* **Cuerpo del correo** electrónico :
    * Número de vale de soporte técnico
    * Su id. de vendedor
    * Captura de pantalla del problema (si es posible)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Mantener y admitir la aplicación](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
