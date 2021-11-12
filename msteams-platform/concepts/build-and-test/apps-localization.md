---
title: Localizar la aplicación
description: Describe consideraciones para la localización de la Microsoft Teams aplicación.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams publish store office publishing AppSource localization language
ms.date: 05/15/2018
ms.openlocfilehash: 82174caf6154e78a3cae80640c0b9d1d7fe00a68
ms.sourcegitcommit: 58fe8a87b988850ae6219c55062ac34cd8bdbf66
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2021
ms.locfileid: "60949575"
---
# <a name="localize-your-app"></a>Localizar la aplicación

Ten en cuenta los siguientes factores para encontrar tu Microsoft Teams aplicación:

1. [Localiza la descripción de AppSource](#localize-your-appsource-listing).
1. [Localiza las cadenas en el manifiesto de la aplicación](#localize-strings-in-your-app-manifest). 
1. [Controlar envíos de texto localizados de los usuarios](#handle-localized-text-submissions-from-your-users).

## <a name="localize-your-appsource-listing"></a>Localización de la descripción de AppSource

Si vas a publicar la aplicación en la tienda, debes tener en cuenta que aún no se admite la localización de la descripción de AppSource. Para admitir las listas localizadas en la tienda de aplicaciones, puedes agregar idiomas adicionales a la descripción. La información de idioma predeterminada que proporcionas en [el Centro de partners](/office/dev/store/submit-to-appsource-via-partner-center) para tu descripción aparece en la descripción del sitio web de [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource es un lugar para todas las necesidades de su equipo. reunir todo, incluidos chats, reuniones, llamadas, archivos y herramientas para permitir un trabajo en equipo más productivo.") para tu aplicación. Actualmente, el idioma predeterminado es inglés.

### <a name="configure-localization"></a>Configurar la localización

Para configurar un idioma adicional para la aplicación, en el [Centro de partners,](/office/dev/store/submit-to-appsource-via-partner-center)selecciona inglés y el idioma adicional de la aplicación. El francés se usa como un idioma adicional en el siguiente ejemplo:

1. Agregar idioma inglés
    * Escribe el nombre de la aplicación.
    * Escribe una breve descripción de la aplicación en inglés.
    * Escribe la descripción larga de la aplicación en inglés.
    * En la descripción larga, escribe: **Esta aplicación está disponible en francés**.
    * Upload las imágenes de la interfaz de usuario de la aplicación (en inglés).
2. Agregar francés
    * Escribe el nombre de la aplicación.
    * Escribe una breve descripción de la aplicación en francés.
    * Escribe la descripción larga de la aplicación en francés.
    * Upload las imágenes de la interfaz de usuario de la aplicación (en francés).

Las imágenes que carga con el idioma inglés se usan en AppSource.

## <a name="localize-strings-in-your-app-manifest"></a>Localización de cadenas en el manifiesto de la aplicación

Debes usar el esquema Microsoft Teams aplicación y `v1.5` más adelante para encontrar la aplicación. Para ello, establece el atributo del archivo manifest.json en o superior y actualiza la propiedad a `$schema` version ( en este **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** `manifestVersion` `$schema` `1.5` caso). 

Debe agregar la propiedad `localizationInfo` con el idioma predeterminado que admite la aplicación. El idioma predeterminado se usa como el idioma de reserva final si la configuración del cliente del usuario no coincide con ninguno de los idiomas adicionales.

### <a name="example-manifestjson-change"></a>Cambio de manifest.json de ejemplo

El siguiente manifiesto.json ayuda a agregar la propiedad con el idioma predeterminado que la `localizationInfo` aplicación admite junto con `additionalLanguages` :

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "localizationInfo": {
        "defaultLanguageTag": "en",
        "additionalLanguages": [
            {
                "languageTag": "es-mx",
                "file": "es-mx.json"
            }
        ]
    }
  ...
}
```

### <a name="example-localization-json-change"></a>Ejemplo de cambio .json de localización

A continuación se muestra un ejemplo para la localización .json:

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```


Puede proporcionar archivos .json adicionales con traducciones de todas las cadenas de acceso del usuario en el manifiesto. Estos archivos deben cumplir el esquema JSON del archivo [de](../../resources/schema/localization-schema.md) localización y deben agregarse a la `localizationInfo` propiedad del manifiesto. Cada archivo se correlaciona con una etiqueta de idioma, que Teams cliente usa para seleccionar las cadenas adecuadas. La etiqueta de idioma tiene la forma de, pero puede omitir la parte para dirigirse a todas las `<language>-<region>` `<region>` regiones que admiten el idioma deseado.

El cliente Teams aplica las cadenas en el siguiente orden: cadenas de idioma predeterminadas -> idioma del usuario sólo cadenas -> idioma del usuario + cadenas de región del usuario.

Por ejemplo, proporciona un idioma predeterminado de "fr" (francés, todas las regiones) y archivos de idioma adicionales para "en" (inglés, todas las regiones) y "en-gb" (inglés, Gran Bretaña), el idioma del usuario se establece en "en-gb". Los siguientes cambios se llevan a cabo en función de la selección de idioma:

1. El Teams toma las cadenas 'fr' y las sobrescribe con las cadenas 'en'.
1. Sobrescriba las cadenas 'en' con las cadenas 'en-gb'.

Si el idioma del usuario se establece en "en-ca", se realizarán los siguientes cambios en función de la selección de idioma: 

1. El Teams toma las cadenas 'fr' y las sobrescribe con las cadenas 'en'.
1. Dado que no se proporciona ninguna localización 'en-ca', se usan las localizaciones 'en'.

Si el idioma del usuario se establece en 'es-es', el cliente Teams toma las cadenas 'fr'. El Teams no invalida las cadenas con ninguno de los archivos de idioma, ya que no se proporciona ninguna traducción de 'es' o 'es-es'.

Por lo tanto, debe proporcionar traducciones de nivel superior y solo de idioma en el manifiesto. Por ejemplo, 'en' en lugar de 'en-us'. Debe proporcionar invalidaciones de nivel de región solo para las pocas cadenas que las necesiten. 

### <a name="example-manifestjson-change"></a>Cambio de manifest.json de ejemplo

El cambio manifest.json se muestra en el siguiente ejemplo:

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en",
    "additionalLanguages": [
      {
        "languageTag": "en-gb",
        "file": "en-gb.json"
      },
      {
        "languageTag": "fr",
        "file": "fr.json"
      },
      {
        "languageTag": "pl",
        "file": "pl.json"
      }
    ]
  }
  ...
}
```

### <a name="example-localization-json-file"></a>Archivo .json de localización de ejemplo

 El cambio localization.json se muestra en el siguiente ejemplo:

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "name.short": "Le App",
  "name.full": "App pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

## <a name="handle-localized-text-submissions-from-your-users"></a>Controlar envíos de texto localizados de los usuarios

Si proporciona versiones localizadas de la aplicación, los usuarios responderán con el mismo idioma. Como Teams convierte los envíos de usuario al idioma predeterminado, la aplicación debe controlar las respuestas de idioma localizado. Por ejemplo, si proporciona una localización , las respuestas al bot son el texto localizado del comando, no `commandList` el idioma predeterminado. La aplicación debe responder correctamente.

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | .NET | Node.js |
|-------------|-------------|------|------|
| Localización de aplicaciones | Microsoft Teams localización de aplicaciones mediante bot y pestaña. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>Consulte también

[Localizar la referencia de esquema JSON](~/resources/schema/localization-schema.md)
