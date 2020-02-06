---
title: Lista de comprobación de manifiesto de la aplicación
description: La lista de comprobación del manifiesto de la aplicación para publicar su aplicación de Microsoft Teams en AppSource
keywords: lista de comprobación de publicación de tienda Office de Microsoft Teams
ms.openlocfilehash: 6186daf264f04e04d6037ddfb7d9208994cc3c57
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783881"
---
# <a name="app-manifest-checklist"></a>Lista de comprobación de manifiesto de la aplicación

>[!IMPORTANT]
>Estamos migrando la administración de las soluciones de Office desde el panel de vendedores al centro de Partners. Para más información, vea[la sección moverse del panel de control del vendedor al centro de Partners ](https://developer.microsoft.com/office/blogs/moving-management-of-solutions-from-seller-dashboard-to-partner-center/)y lea el[FAQ](https://docs.microsoft.com/office/dev/store/partner-center-faq).

El manifiesto de la aplicación debe cumplir con las directrices que se describen a continuación.

>[!Tip]
> Use App Studio para que le ayude a compilar el manifiesto de la aplicación. Validará la mayoría de los requisitos que se indican a continuación y mostrará cualquier error o advertencia en la ficha **probar y distribuir** .

## <a name="tips"></a>Sugerencias

* No use "Teams", "Microsoft" o "app" en el nombre de la aplicación.
* El developerName del manifiesto debe ser el mismo que el nombre del proveedor definido en el centro de asociados.
* Asegúrese de que la descripción de la aplicación, las capturas de pantallas, el texto y las imágenes promocionales solo describen la aplicación y que no contienen anuncios, promociones o nombres de marcas protegidos por copyright.
* Si su producto requiere una cuenta en su servicio u otro servicio, enumere la descripción y asegúrese de que hay vínculos para registrarse, iniciar sesión y cerrar sesión.
* Si su producto requiere compras adicionales para funcionar correctamente, enumere la descripción.
* Proporcione los términos y los vínculos de la Directiva de privacidad necesarios en el manifiesto y en el centro del partner o el panel. Compruebe que los vínculos se resuelven correctamente en la documentación correcta, lo ideal es que los equipos sean específicos. Para los bots, debe proporcionar esta misma información en la sección envío de la página de registro de bot Framework.
* Asegúrese de que los metadatos del manifiesto coinciden exactamente con los metadatos del centro del asociado (y, en el caso de los bots, en el registro del marco de bot). Tenga en cuenta que la entrada del centro de asociados puede contener una descripción más detallada y con formato para usarla en la página del producto AppSource.
* Asegúrese de que el título de la aplicación usado en el manifiesto es una **coincidencia exacta** con el título de la aplicación que se especifica en el envío del centro de asociados. *Vea* [crear listas eficaces en Microsoft AppSource y en Office: Use un nombre de complemento coherente ](https://docs.microsoft.com/office/dev/store/create-effective-office-store-listings#use-a-consistent-add-in-name).

## <a name="metadata-requirement"></a>Requisitos de metadatos

Se requieren los siguientes metadatos para la aplicación.

|Datos|Tipo|Size|Manifiesto|Centro para socios|Description|
|---|---|---|---|---|---|
|Paquete de la aplicación|.zip|||✔|El paquete de la aplicación real para la carga o el envío de AppSource.|
|Logotipo-color|.png|192&times;192 píxeles|`icon.color`||El icono para mostrar en la lista de la página del producto en la galería de Teams. Este es su logotipo de color de todo el producto.|
|Contorno de logotipo|.png|32&times;32 píxeles|`icon.outline`||Icono que se va a mostrar en Microsoft Teams, en el canal de chat de Microsoft Teams y en otras ubicaciones. Este es el logotipo representado como un contorno blanco con fondo transparente.|
|Logotipo de la aplicación|. png,. jpg,. JPEG,. gif|300&times;300 píxeles||✔|Icono que se va a mostrar en AppSource. Este es el logotipo de producto de color completo y es un archivo diferente del que se usa en el manifiesto para `icon.color`. debe ser inferior a 512 KB.|
|Vínculo de soporte técnico|URL|||✔|Un vínculo a material de soporte para los usuarios finales que podrían no tener instalada la aplicación. Vínculo disponible públicamente accesible sin ningún inicio de sesión (HTTPS).|
|Vínculo de privacidad|URL||`developer.privacyUrl`|✔|Un vínculo a la Directiva de privacidad (HTTPS).|
|Vínculo a vídeo|URL|||Opcional|Un vínculo a un vídeo sobre la aplicación.|
|FORMALIZA|. doc,. pdf, etc.|||Opcional|AppSource requiere un contrato de licencia para el usuario final (CLUF), que puede proporcionar como datos adjuntos. Si opta por no enviar un CLUF, se proporcionará uno en su nombre.|
|Condiciones de servicio|URL||`developer.termsOfServiceUrl`||Un vínculo a sus términos de servicio (HTTPS).|
|Notas de prueba|Rellenar un vínculo entre líneas o una dirección URL pública|||Notas de prueba detalladas sobre cómo probar la aplicación paso a paso. Incluya dos credenciales de inicio de sesión para probar los escenarios de administrador y no administrador.|

## <a name="localized-content"></a>Contenido localizado

> [!NOTE]
> AppSource planea admitir contenido localizado para los siguientes metadatos. Actualmente, la descripción de la aplicación solo se mostrará en inglés en AppSource, pero se mostrará correctamente en el cliente de Microsoft Teams. Consulte [localización de la aplicación](~/concepts/build-and-test/apps-localization.md) para obtener más información.

|Datos|Tipo|Size|Manifiesto|Centro para socios|Description|
|---|---|---|---|---|---|
|Nombre de la aplicación|Cadena|semestre|`name.short`|✔|El nombre de la aplicación tal como debería aparecer en el escaparate y en el producto.|
|Nombre de aplicación largo|Cadena|semestre|`name.full`|✔|El nombre de la aplicación tal como debería aparecer en el escaparate y en el producto.|
|La descripción breve|Cadena|80|`description.short`|✔|Breve descripción de la aplicación.|
|La descripción larga|Cadena|4000|`description.full`|✔|Una descripción más detallada de la aplicación. En el archivo del manifiesto, es adecuado un resumen preciso. En el centro de Partners, puede usar una descripción con formato y más rica para la página de producto de AppSource.|
|Capturas de pantalla (1-5)|. png,. jpg o. gif|1366w x 768h y menor que 1024 KB||✔|Al menos una captura de pantalla que muestra la experiencia de la aplicación. Se usa en la página de detalles de la aplicación.|

## <a name="submission-extras-for-bots"></a>Extras de envío para bots

Los bots en Microsoft Teams se deben crear con el marco de trabajo. Vea [crear un bot](~/bots/how-to/create-a-bot-for-teams.md) para obtener instrucciones. Use un icono de color 96x96 para el icono de bot en el marco de bot.
