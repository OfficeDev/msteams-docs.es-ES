---
title: Razones comunes del error de validación de la aplicación
description: Obtenga información sobre las razones más comunes para el error de validación de aplicaciones, como vínculos rotos, errores inesperados, bloqueos, infracción de directrices de dominio válidas, errores funcionales.
ms.topic: overview
author: v-ypalikila
ms.author: v-ypalikila
ms.localizationpriority: high
ms.openlocfilehash: 006fe6d9e939d9578fa84c61daaa4c404a10d5f6
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791730"
---
# <a name="common-reasons-for-app-validation-failure"></a>Razones comunes del error de validación de la aplicación

La mayoría de las aplicaciones no pasan el proceso de envío a la tienda debido a problemas durante su desarrollo. Los problemas o razones más comunes se tratarán en este artículo para ayudarle a preparar mejor la aplicación antes de [enviarla para su revisión](/office/dev/store/add-in-submission-guide?toc=/microsoftteams/platform/toc.json&bc=/microsoftteams/platform/breadcrumb/toc.json). Evite estos errores comunes y siga las [directrices de validación de la tienda de Microsoft Teams](prepare/teams-store-validation-guidelines.md) y las [directivas de Certificación de marketplace comercial](/legal/marketplace/certification-policies) para aumentar las posibilidades de que la aplicación supere el proceso de envío a la tienda de Microsoft Teams.

Estas son las razones más comunes por las que se puede rechazar tu aplicación:

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/broken-links-errors-icon-1.png" link="#broken-links-functional-bugs-app-crashes-and-unexpected-errors":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/app-description-icon.png" link="#app-description":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/trademark-icon.png" link="#violation-of-microsoft-trademark-and-brand-guidelines":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/testability-icon.png" link="#testability":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/compliance-icon.png" link="#microsoft-365-app-compliance-program":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/app-guideline-icon.png" link="#violation-of-app-icon-guidelines":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/app-name-icon.png" link="#app-name":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/support-link-icon.png" link="#support-link":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/schema-icon.png" link="#manifest-schema":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/app-ui-icon.png" link="#app-ui":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/domain-icon.png" link="#valid-domains":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/localization-icon.png" link="#localization-information":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/developer-name-icon.png" link="#provider-or-developer-name-mismatch":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/privacy-policy-icon.png" link="#privacy-policy":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/terms-of-use-icon.png" link="#terms-of-use":::
   :::column-end:::
:::row-end:::

## <a name="broken-links-functional-bugs-app-crashes-and-unexpected-errors"></a>Vínculos rotos, errores funcionales, bloqueos de aplicaciones y errores inesperados

Pruebe la aplicación para comprobar la corrección, la funcionalidad y el uso de la aplicación. Asegúrese de que prueba la aplicación de manera exhaustiva, compruebe todos los flujos de trabajo que admite la aplicación sin olvidarse de ninguno, pruebe la compatibilidad de la aplicación en los sistemas operativos y exploradores según las [directivas de Certificación de marketplace comercial](/legal/marketplace/certification-policies) y corrija todos los errores. Debe evitar los siguientes errores en la aplicación antes de enviarlos para su revisión:

* Vínculos rotos en la aplicación.

* Errores funcionales que bloquean el uso de la aplicación.

* Bloqueos de la aplicación.

* Carga continua de superficies de aplicación que impiden la finalización de los flujos de trabajo indicados que admite la aplicación.

* Mensajes de error inesperados durante la experiencia de uso, inicio de sesión y registro de la aplicación, y para escenarios en los que las características de la aplicación no funcionan según lo esperado.

* Asegúrese de que la aplicación está completa y lista para publicarse antes de enviarla para su revisión.

## <a name="app-description"></a>Descripción de la aplicación

Una buena descripción puede hacer que la aplicación destaque en la tienda de Microsoft Teams y sirva para animar a los clientes a descargarla. Debe evitar cometer los siguientes errores en la descripción de la aplicación:

* En el manifiesto y en la descripción completa de AppSource no se incluye la información de reenvío de información para nuevos usuarios como, por ejemplo, Registrarse o Introducción, o los vínculos Ayuda y Contacte con nosotros.

* El nombre o la funcionalidad de la aplicación específica de la región no se denominó en las descripciones de manifiesto y Centro de partners de la aplicación.

* Las limitaciones o la dependencia de la cuenta en cuentas o servicios externos para completar la experiencia de inicio de sesión, cierre de sesión y registro no se indican en el manifiesto de la aplicación ni en una descripción larga.

* La descripción breve y completa del manifiesto de la aplicación no resalta la propuesta de valor de la aplicación.

* Las características de aplicaciones admitidas no se actualizan.

* Comparación de la aplicación con otra.

* Referencias a las integraciones, que no forman parte de la funcionalidad de la aplicación.

* Errores gramaticales.

* La descripción breve y completa de la aplicación es la misma.

## <a name="violation-of-microsoft-trademark-and-brand-guidelines"></a>Infracción de las directrices de marca comercial y marca de Microsoft

Los activos de marca de Microsoft, incluidos logotipos, iconos, diseños, identidad corporativa, fuentes, nombres de productos, servicios, sonidos, emojis y otras características y elementos de la marca, estén o no registrados, son activos propiedad de Microsoft y su grupo de empresas.

Al hacer referencia a marcas comerciales, nombres de productos y servicios de Microsoft, debe seguir [las Directrices de marca comercial y marca de Microsoft](https://www.microsoft.com/legal/intellectualproperty/trademarks). Debe evitar las siguientes infracciones comunes que provocan el rechazo de la aplicación:

* Abreviar Microsoft como MS o MSFT en la lista de ofertas o hacer referencia a la primera instancia de Microsoft Teams en la lista de ofertas como **Teams** en lugar de **Microsoft Teams**.

* Usar activos de la marca de Microsoft en el contenido de la oferta sin una licencia rápida de Microsoft.

* Crear una descripción de la oferta (incluida la descripción de la oferta, el título, el icono, las capturas de pantalla y los vídeos) que suplanta o da la impresión de que es una aplicación oficial de Microsoft para la tienda de Microsoft Teams.

## <a name="testability"></a>Capacidad de prueba  

 [Instrucciones de prueba detalladas](prepare/teams-store-validation-guidelines.md#app-package-and-store-listing) y credenciales que le ayudarán a revisar correctamente la aplicación.

Asegúrese de proporcionar todos los detalles necesarios para revisar la aplicación en la sección Notas de la sección de Información sobre la certificación del Centro de partners, credenciales de demostración válidas para las características que requieren inicio de sesión e instrucciones para establecer cualquier configuración especial, un vídeo de demostración o hardware para las características que requieren un entorno difícil de replicar y conseguir. Además, asegúrese de proporcionar la información de contacto más reciente.

Debe evitar los siguientes problemas que se producen en el 20 % de las aplicaciones que se rechazan durante la revisión de las aplicaciones:

* No hay instrucciones de prueba ni credenciales para probar la aplicación.

* Solo se proporciona una cuenta de prueba cuando hay una dependencia con dos cuentas de prueba para probar escenarios de colaboración.

* Las instrucciones de prueba y las credenciales proporcionadas no son suficientes para completar las pruebas de funcionamiento de la aplicación.

## <a name="microsoft-365-app-compliance-program"></a>Programa de cumplimiento de aplicaciones de Microsoft 365  

El programa de cumplimiento de aplicaciones de Microsoft 365 ayuda a las organizaciones a evaluar y administrar los riesgos mediante la evaluación de la información de seguridad y cumplimiento de una aplicación. **Debe completar** la [Verificación del editor](/azure/active-directory/develop/mark-app-as-publisher-verified) antes de enviar la aplicación para su revisión para poder publicarla en la tienda de Microsoft Teams.

## <a name="violation-of-app-icon-guidelines"></a>Infracción de las directrices del icono de la aplicación

Los iconos son uno de los principales elementos que la gente ve cuando navega por la tienda de Microsoft Teams. Los iconos deben comunicar la marca y el propósito de la aplicación y cumplir [las directrices de iconos de aplicación](../../build-and-test/apps-package.md#app-icons). Debe evitar las siguientes infracciones que provocan el rechazo de la aplicación:

* Envíos de aplicaciones que contienen paquetes de aplicación con iconos de color y contorno diferentes o iconos de contorno no blancos y no transparentes.

* Envíos de aplicaciones con logotipos diferentes en Centro de partners y en el paquete de la aplicación enviado para su revisión.

## <a name="app-name"></a>Nombre de la aplicación

El nombre de la aplicación desempeña un papel fundamental para que los usuarios encuentren la aplicación en la tienda de Microsoft Teams. Asegúrese de que el nombre de la aplicación cumple las[directrices de nombre de aplicación](prepare/teams-store-validation-guidelines.md#app-name) y no infringe las [directrices de marca comercial y marca de Microsoft](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks). Debe evitar las siguientes infracciones que provocan el rechazo de la aplicación:

* Uso incoherente del nombre de la aplicación en toda la funcionalidad de la aplicación.
* Error de coincidencia entre el nombre de la aplicación mencionado en el manifiesto de la aplicación enviado como parte del paquete de la aplicación y en el Centro de partners.
* Nombres de aplicación que incluyen *Beta*, *Dev* y *Prod* para indicar que la aplicación no está lista para producción.
* Envíos de aplicaciones en los que el desarrollador ha cambiado el nombre de la aplicación, pero el nombre de la aplicación anterior se sigue usando dentro de la aplicación.

## <a name="support-link"></a>Vínculos de soporte técnico

 Los vínculos de soporte técnico no deben pedir autenticación a los usuarios y deben conducir directamente a la información de soporte técnico adecuada. Debe asegurarse de que la aplicación incluye un vínculo de soporte técnico válido para que los usuarios se ponga en contacto con ellos.

## <a name="manifest-schema"></a>Esquema del manifiesto

El manifiesto de la aplicación de Teams describe cómo se integra la aplicación en el producto de Microsoft Teams. El manifiesto debe cumplir con un [esquema de manifiesto](../../../resources/schema/manifest-schema.md) publicado de forma pública. Si la aplicación admite la localización, asegúrese de usar un esquema de manifiesto de localización versión 1.5 o posterior. Los paquetes de aplicaciones que contienen esquemas de vista previa (no publicados públicamente) no se pueden revisar.

Debe actualizar la versión de la aplicación declarada en el manifiesto si va a enviar una actualización de la aplicación. Se recomienda usar siempre el esquema de manifiesto publicado más reciente al enviar una nueva aplicación o una actualización de la aplicación y asegurarse de que la versión del esquema de manifiesto en la tienda de Microsoft Teams y Microsoft AppSource es la misma.

El paquete de la aplicación solo debe contener el manifiesto, el icono de color y el icono de esquema de la aplicación. Los paquetes de aplicaciones que contienen otros archivos o carpetas adicionales no se revisan.

## <a name="app-ui"></a>App UI

La interfaz de usuario de la aplicación no debe parecer inacabada y debe ser intuitiva. Asegúrese de que los usuarios no se encuentran con una pantalla en blanco al realizar una acción en la interfaz de usuario de la aplicación. Las aplicaciones que han truncado o superpuesto contenido y las aplicaciones que muestran imágenes rotas no pasan la revisión de la aplicación.

## <a name="valid-domains"></a>Dominios válidos

El envío de la aplicación debe cumplir las directrices de [dominios externos](/legal/marketplace/certification-policies) según lo previsto en la directiva de Certificación de marketplace comercial de Microsoft. Para que la aplicación pase la revisión, asegúrese de que los dominios válidos enumerados en el manifiesto de la aplicación estén bajo el control directo de su organización.

## <a name="localization-information"></a>Información sobre la localización

Debe incluir los archivos de idioma localizados en el paquete de la aplicación si la aplicación admite la localización. Los archivos de localización deben ajustarse al [esquema de localización de Teams](../../build-and-test/apps-localization.md). Las aplicaciones que admiten la localización pero a las que les falta información de localización en el manifiesto de la aplicación no pasan la revisión de la aplicación.

## <a name="provider-or-developer-name-mismatch"></a>El nombre del proveedor o desarrollador no coincide

Debe asegurarse de proporcionar el mismo nombre de desarrollador en la descripción de la oferta en ambos escaparates para evitar la confusión del usuario final durante la adquisición de la aplicación desde la tienda de Microsoft Teams o Microsoft AppSource. Las ofertas con incoherencias en el nombre del desarrollador suelen suspender la revisión de la aplicación.

## <a name="privacy-policy"></a>Directiva de privacidad

La descripción de la oferta debe incluir un vínculo de directiva de privacidad válido. Las ofertas con vínculos de directiva de privacidad no válidos, no seguros o rotos no pasan la revisión de la aplicación. La directiva de privacidad debe seguir las [directrices de directiva de privacidad](prepare/teams-store-validation-guidelines.md#privacy-policy).

## <a name="terms-of-use"></a>Términos de uso

La descripción de la oferta debe incluir un vínculo de Condiciones de uso válido. Las ofertas con vínculos de Condiciones de uso no válidos, no seguros o rotos no pasan la revisión de la aplicación. Debe seguir las [directrices de Condiciones de uso](prepare/teams-store-validation-guidelines.md#terms-of-use).

## <a name="see-also"></a>Consulte también

* [Directrices de validación de la tienda de Microsoft Teams](prepare/teams-store-validation-guidelines.md)
* [Directivas de Certificación de marketplace comercial](/legal/marketplace/certification-policies)
* [Directrices de marca comercial y marca de Microsoft](https://www.microsoft.com/legal/intellectualproperty/trademarks)
