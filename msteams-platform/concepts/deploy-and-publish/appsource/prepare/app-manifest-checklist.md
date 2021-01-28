---
title: Lista de comprobación de manifiesto de la aplicación
description: La lista de comprobación del manifiesto de la aplicación para publicar la aplicación de Microsoft Teams en AppSource
ms.topic: reference
keywords: Lista de comprobación de publicación de office de la tienda de teams
ms.openlocfilehash: f07c0d2693d12d56d6717724e1ef402cf79d5fff
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014400"
---
# <a name="app-manifest-checklist"></a>Lista de comprobación de manifiesto de la aplicación

>[!IMPORTANT]
>Estamos migrando la administración de las soluciones de Office desde el panel de vendedores al centro de Partners. Para más información, vea[la sección moverse del panel de control del vendedor al centro de Partners ](https://developer.microsoft.com/office/blogs/moving-management-of-solutions-from-seller-dashboard-to-partner-center/)y lea el[FAQ](https://docs.microsoft.com/office/dev/store/partner-center-faq).

El manifiesto de la aplicación debe cumplir con las directrices que se describen a continuación.

>[!Tip]
> Usa App Studio para ayudarte a crear el manifiesto de la aplicación. Validará la mayoría de los requisitos siguientes y mostrará cualquier error o advertencia en la pestaña Probar **y** distribuir.

## <a name="tips"></a>Sugerencias

* No use "Teams", "Microsoft" o "app" en el nombre de la aplicación.
* El developerName del manifiesto debe ser el mismo que el nombre del proveedor definido en el Centro de partners.
* Asegúrate de que la descripción de la aplicación, las capturas de pantalla, el texto y las imágenes promocionales describen solo la aplicación y no contienen publicidad adicional, promociones o nombres de marca protegidos por derechos de autor.
* Si el producto requiere una cuenta en el servicio u otro servicio, enumédalo en la descripción y asegúrese de que hay vínculos para registrarse, iniciar sesión y cerrar sesión.
* Si el producto requiere compras adicionales para funcionar correctamente, enumeralo en la descripción.
* Proporciona los vínculos a términos y directivas de privacidad necesarios en el manifiesto y en el Centro de partners o panel. Compruebe que los vínculos se resuelven correctamente en la documentación correcta, lo ideal es específico de Teams. Para los bots, debe proporcionar esta misma información en la sección Envío de la página de registro de Bot Framework.
* Asegúrate de que los metadatos del manifiesto coincidan exactamente con los metadatos del Centro de partners (y, para los bots, en el registro de Bot Framework). Ten en cuenta que la entrada del Centro de partners puede contener una descripción más detallada y con formato para usarla en la página del producto AppSource.
* Asegúrate de que el título  de la aplicación usado en el manifiesto coincide exactamente con el título de la aplicación especificado en el envío del Centro de partners. *Vea* [Crear listas eficaces en Microsoft AppSource](https://docs.microsoft.com/office/dev/store/create-effective-office-store-listings#use-a-consistent-add-in-name)y en Office: use un nombre de complemento coherente.

## <a name="metadata-requirement"></a>Requisito de metadatos

Los siguientes metadatos son necesarios para la aplicación.

|Datos|Tipo|Size|Manifiesto|Centro de asociados|Descripción|
|---|---|---|---|---|---|
|Paquete de la aplicación|.zip|||✔|El paquete de la aplicación real para cargar o enviar AppSource.|
|Logotipo de color|.png|192 &times; 192 píxeles|`icon.color`||Icono que se mostrará en la lista de páginas de productos de la galería de Teams. Este es el logotipo del producto a todo color.|
|Esquema del logotipo|.png|32 &times; 32 píxeles|`icon.outline`||El icono que se mostrará en Teams, en el canal de chat de Teams y en otras ubicaciones. Este es el logotipo representado como un esquema blanco con fondo transparente.|
|Logotipo de la aplicación|.png, .jpg, .jpeg, .gif|300 &times; 300 píxeles||✔|Icono que se mostrará en AppSource. Este es el logotipo del producto a todo color y es un archivo diferente del que se usa en el manifiesto para `icon.color` . debe ser inferior a 512 KB.|
|Vínculo de soporte técnico|URL|||✔|Un vínculo a material de soporte técnico para los usuarios finales que quizás no tengan instalada la aplicación. Vínculo disponible públicamente accesible sin ningún inicio de sesión (HTTPS).|
|Vínculo de privacidad|URL||`developer.privacyUrl`|✔|Un vínculo a la directiva de privacidad (HTTPS).|
|Vínculo a vídeo|URL|||Opcional|Un vínculo a un vídeo sobre la aplicación.|
|CLUF|.doc, .pdf, etc.|||Opcional|AppSource requiere un contrato de licencia para el usuario final (CLUF), que puede proporcionar como datos adjuntos. Si decide no enviar un CLUF, se le proporciona uno en su nombre.|
|Términos de servicio|URL||`developer.termsOfServiceUrl`||Un vínculo a los términos de servicio (HTTPS).|
|Notas de prueba|Rellenar en línea o vínculo a una dirección URL pública|||Notas de prueba detalladas sobre cómo probar la aplicación paso a paso. Incluya dos credenciales de inicio de sesión para probar escenarios de administrador y no administrador.|

## <a name="localized-content"></a>Contenido localizado

> [!NOTE]
> AppSource planea admitir contenido localizado para los siguientes metadatos. Actualmente, la descripción de la aplicación solo se mostrará en inglés en AppSource, pero se mostrará correctamente localizada en el cliente de Teams. Consulta [la localización de la aplicación](~/concepts/build-and-test/apps-localization.md) para obtener más información.

|Datos|Tipo|Size|Manifiesto|Centro de asociados|Descripción|
|---|---|---|---|---|---|
|Nombre de la aplicación|Cadena|30|`name.short`|✔|El nombre de la aplicación tal como debe aparecer en el frente de la tienda y en el producto.|
|Nombre largo de la aplicación|Cadena|30|`name.full`|✔|El nombre de la aplicación tal como debería aparecer en la tienda y en el producto.|
|La descripción breve|Cadena|80|`description.short`|✔|Breve descripción de la aplicación.|
|La descripción larga|Cadena|4000|`description.full`|✔|Una descripción más detallada de la aplicación. En el archivo de manifiesto, un resumen preciso es adecuado. En el Centro de partners, puedes usar una descripción más completa y con formato para la página del producto AppSource.|
|Capturas de pantalla (1-5)|.png, .jpg o .gif|1366 w x 768h y menos de 1024 KB||✔|Al menos una captura de pantalla que muestre la experiencia de la aplicación. Se usa en la página de detalles de la aplicación.|

## <a name="submission-extras-for-bots"></a>Extras de envío para bots

Los bots de Microsoft Teams deben crearse con Bot Framework. Vea [Crear un bot para](~/bots/how-to/create-a-bot-for-teams.md) obtener instrucciones. Use un icono de color de 96 x 96 para el icono del bot en Bot Framework.
