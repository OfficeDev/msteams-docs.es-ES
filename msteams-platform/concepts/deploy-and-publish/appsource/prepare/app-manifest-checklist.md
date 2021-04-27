---
title: Lista de comprobación de manifiesto de la aplicación
description: La lista de comprobación del manifiesto de la aplicación para publicar la aplicación de Microsoft Teams en AppSource
ms.topic: reference
localization_priority: Normal
keywords: Lista de comprobación de publicación de la oficina de la tienda de teams
ms.openlocfilehash: a8fd57d8050530856fa635f59c0a6ce4f8c2a5cf
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019905"
---
# <a name="app-manifest-checklist"></a>Lista de comprobación de manifiesto de la aplicación

>[!IMPORTANT]
>Estamos migrando la administración de las soluciones de Office desde el panel de vendedores al centro de Partners. Para más información, vea[la sección moverse del panel de control del vendedor al centro de Partners ](https://developer.microsoft.com/office/blogs/moving-management-of-solutions-from-seller-dashboard-to-partner-center/)y lea el[FAQ](https://docs.microsoft.com/office/dev/store/partner-center-faq).

El manifiesto de la aplicación debe cumplir las directrices que se describen a continuación.

>[!Tip]
> Usa App Studio para crear el manifiesto de la aplicación. Validará la mayoría de los requisitos siguientes y mostrará cualquier error o advertencia en la pestaña Probar **y** distribuir.

## <a name="tips"></a>Sugerencias

* No use "Teams", "Microsoft" o "app" en el nombre de la aplicación.
* El developerName del manifiesto debe ser el mismo que el nombre del proveedor definido en el Centro de partners.
* Asegúrate de que la descripción de la aplicación, las capturas de pantalla, el texto y las imágenes promocionales describen solo la aplicación y no contienen ninguna publicidad adicional, promociones o nombres de marca con derechos de autor.
* Si el producto requiere una cuenta en el servicio u otro servicio, enuméñalo en la descripción y asegúrate de que hay vínculos para registrarse, iniciar sesión y cerrar sesión.
* Si el producto requiere compras adicionales para funcionar correctamente, enume eso en la descripción.
* Proporcione los vínculos de directiva de privacidad y términos necesarios en el manifiesto y el Centro de partners o panel. Compruebe que los vínculos se resuelven correctamente en la documentación correcta, idealmente específica de Teams. Para los bots, debe proporcionar esta misma información en la sección Envío de la página de registro de Bot Framework.
* Asegúrese de que los metadatos del manifiesto coincidan exactamente con los metadatos del Centro de partners (y, en el caso de los bots, en el registro de Bot Framework). Tenga en cuenta que la entrada del Centro de partners puede contener una descripción más detallada y con formato para su uso en la página del producto AppSource.
* Asegúrate de que el título  de la aplicación usado en el manifiesto coincide exactamente con el título de la aplicación especificado en el envío del Centro de partners. *Vea* [Create effective listings in Microsoft AppSource and within Office : Use a consistent add-in name](https://docs.microsoft.com/office/dev/store/create-effective-office-store-listings#use-a-consistent-add-in-name).

## <a name="metadata-requirement"></a>Requisito de metadatos

Los siguientes metadatos son necesarios para la aplicación.

|Datos|Tipo|Size|Manifiesto|Centro de asociados|Descripción|
|---|---|---|---|---|---|
|Paquete de la aplicación|.zip|||✔|El paquete de la aplicación real para cargar o enviar AppSource.|
|Logotipo de color|.png|192 &times; 192 píxeles|`icon.color`||Icono que se mostrará en la descripción de la página del producto en la galería de Teams. Este es el logotipo del producto a todo color.|
|Esquema del logotipo|.png|32 &times; 32 píxeles|`icon.outline`||Icono que se mostrará en Teams, en el canal de chat de Teams y en otras ubicaciones. Este es el logotipo representado como un esquema blanco con fondo transparente.|
|Logotipo de la aplicación|.png, .jpg, .jpeg, .gif|300 &times; 300 píxeles||✔|Icono que se mostrará en AppSource. Este es el logotipo del producto a todo color y es un archivo diferente del que se usa en el manifiesto para `icon.color` . debe ser inferior a 512 KB.|
|Vínculo de soporte técnico|URL|||✔|Un vínculo para admitir material para usuarios finales que quizás no han instalado la aplicación. Vínculo disponible públicamente accesible sin ningún inicio de sesión (HTTPS).|
|Vínculo privacidad|URL||`developer.privacyUrl`|✔|Un vínculo a la directiva de privacidad (HTTPS).|
|Vínculo a vídeo|URL|||Opcional|Un vínculo a un vídeo sobre la aplicación.|
|CLUF|.doc, .pdf, etc.|||Opcional|AppSource requiere un contrato de licencia de usuario final (CLUF), que puede proporcionar como datos adjuntos. Si decide no enviar un CLUF, se le proporciona uno en su nombre.|
|Términos de servicio|URL||`developer.termsOfServiceUrl`||Un vínculo a sus términos de servicio (HTTPS).|
|Notas de la prueba|Rellenar en línea o vínculo a una dirección URL pública|||Notas de prueba detalladas sobre cómo probar la aplicación paso a paso. Incluya dos credenciales de inicio de sesión para probar escenarios de administrador y no administrador.|

## <a name="localized-content"></a>Contenido localizado

> [!NOTE]
> AppSource planea admitir contenido localizado para los siguientes metadatos. Actualmente, la descripción de la aplicación solo se mostrará en inglés en AppSource, pero se mostrará correctamente localizada en el cliente de Teams. Consulta [Localización de la aplicación](~/concepts/build-and-test/apps-localization.md) para obtener más información.

|Datos|Tipo|Size|Manifiesto|Centro de asociados|Descripción|
|---|---|---|---|---|---|
|Nombre de la aplicación|Cadena|30|`name.short`|✔|El nombre de la aplicación tal como debe aparecer en el escaparate y en el producto.|
|Nombre de la aplicación larga|Cadena|30|`name.full`|✔|El nombre de la aplicación tal como debe aparecer en el escaparate y en el producto.|
|La descripción breve|Cadena|80|`description.short`|✔|Breve descripción de la aplicación.|
|La descripción larga|Cadena|4000|`description.full`|✔|Una descripción más detallada de la aplicación. En el archivo de manifiesto, un resumen preciso es adecuado. En el Centro de partners, puede usar una descripción más enriquecida y con formato para la página del producto AppSource.|
|Capturas de pantalla (1-5)|.png, .jpg o .gif|1366w x 768h y menor que 1024 KB||✔|Al menos una captura de pantalla que muestre la experiencia de la aplicación. Se usa en la página de detalles de la aplicación.|

## <a name="submission-extras-for-bots"></a>Extras de envío para bots

Los bots de Microsoft Teams deben crearse con Bot Framework. Consulta [Crear un bot para](~/bots/how-to/create-a-bot-for-teams.md) obtener instrucciones. Usa un icono de color de 96 x 96 para el icono del bot en Bot Framework.
