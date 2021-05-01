---
title: Localización de la aplicación
description: Describe consideraciones para la localización de la Microsoft Teams aplicación.
ms.topic: conceptual
localization_priority: Normal
keywords: teams publish store office publishing AppSource localization language
ms.date: 05/15/2018
ms.openlocfilehash: 9a939b1990d1b09410af344f79dd39b8b02c404b
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101712"
---
# <a name="localization-for-microsoft-teams-apps"></a>Localización para Microsoft Teams aplicaciones

Al encontrar la aplicación Microsoft Teams, debes tener en cuenta lo siguiente:

1. La Teams de la tienda (si procede).
1. Las cadenas de acceso del usuario final en el manifiesto de la aplicación (por ejemplo, comandos bot).
1. Responder al texto localizado enviado por los usuarios.

## <a name="localizing-your-appsource-listing"></a>Localización de la descripción de AppSource

Si vas a publicar en la tienda, debes tener en cuenta que aún no se admite la localización de la descripción de AppSource. Sin embargo, como preparación para la compatibilidad con las listas localizadas en la tienda de aplicaciones, puedes agregar idiomas adicionales a tu descripción. Actualmente, solo la información de idioma predeterminada (inglés) que proporciones en el [Centro](/office/dev/store/submit-to-appsource-via-partner-center) de partners para tu descripción aparecerá en la descripción del sitio web de [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) para tu aplicación.

### <a name="example-of-configuring-localization"></a>Ejemplo de configuración de localización

Para configurar un idioma adicional para la aplicación, en el [Centro de partners,](/office/dev/store/submit-to-appsource-via-partner-center)selecciona inglés y el idioma adicional de la aplicación. El francés se usa en este ejemplo.

1. Agregar idioma inglés
    * Rellene el nombre de la aplicación.
    * Rellene una breve descripción de la aplicación en inglés.
    * Rellene la descripción larga de la aplicación en inglés.
    * En la descripción larga, agrega también la línea "Esta aplicación está disponible en francés".
    * Upload las imágenes de la interfaz de usuario de la aplicación (en inglés).
2. Agregar francés
    * Rellene el nombre de la aplicación.
    * Rellene una breve descripción de la aplicación en francés.
    * Rellene la descripción larga de la aplicación en francés.
    * Upload las imágenes de la interfaz de usuario de la aplicación (en francés).

Las imágenes que cargues con el idioma inglés serán las que se usan en AppSource.

## <a name="localizing-the-strings-in-your-app-manifest"></a>Localización de las cadenas en el manifiesto de la aplicación

Debes usar el esquema Microsoft Teams aplicación v1.5+ para encontrar la aplicación correctamente. Para ello, establece el atributo en el archivo manifest.jsen ' y actualiza la propiedad `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json 'manifestVersion' en '1,7'.

### <a name="example-manifestjson-change"></a>Ejemplo manifest.jsal cambiar

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

A continuación, querrá agregar la propiedad 'localizationInfo' con el idioma predeterminado que admite la aplicación. El idioma predeterminado se usa como el último idioma de reserva si la configuración del cliente del usuario no coincide con ninguno de los idiomas adicionales.

### <a name="example-manifestjson-change"></a>Ejemplo manifest.jsal cambiar

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

Puede proporcionar archivos .json adicionales con traducciones de todas las cadenas de acceso del usuario en el manifiesto. Estos archivos deben cumplir el esquema [JSON](../../resources/schema/localization-schema.md) del archivo de localización y deben agregarse a la propiedad 'localizationInfo' del manifiesto. Cada archivo se correlaciona con una etiqueta de idioma que Teams cliente usa para elegir las cadenas adecuadas. La etiqueta de idioma tiene la forma de, pero se recomienda omitir la parte para dirigirse a todas las <language> - <region> <region> regiones que admiten el idioma deseado.

El cliente Teams aplicará las cadenas en este orden: cadenas de idioma predeterminadas -> solo cadenas de idioma del usuario -> idioma del usuario + cadenas de región del usuario.

Por ejemplo, proporciona un idioma predeterminado de 'fr' (francés, todas las regiones) y archivos de idioma adicionales para 'en' (inglés, todas las regiones) y 'en-gb' (inglés, Gran Bretaña). Si el idioma del usuario está establecido en 'en-gb':

1. El Teams tomará las cadenas 'fr' sobrescrituras con las cadenas 'en'.
2. Sobrescriba las cadenas 'en-gb'.

Si el idioma del usuario está establecido en 'en-ca': 

1. El Teams tomará las cadenas 'fr' sobrescrituras con las cadenas 'en'.
2. Dado que no se proporciona ninguna localización 'en-ca', se usarán las localizaciones 'en'.

Si el idioma del usuario se establece en 'es-es', el cliente de Teams tomará las cadenas 'fr' y no las invalidará con ninguno de los archivos de idioma.

Por lo tanto, se recomienda encarecidamente proporcionar traducciones de solo idioma de nivel superior en el manifiesto ('en' en lugar de 'en-us') y solo proporcionar invalidaciones de nivel de región para las pocas cadenas que las necesitan.

### <a name="example-manifestjson-change"></a>Ejemplo manifest.jsal cambiar

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

## <a name="handling-localized-text-submissions-from-your-users"></a>Controlar envíos de texto localizados de los usuarios

Si proporciona versiones localizadas de la aplicación, es muy probable que los usuarios respondan con el mismo idioma. Teams convierte los envíos de usuario al idioma predeterminado, por lo que la aplicación tendrá que controlarlo. Por ejemplo, si proporciona una localización , las respuestas al bot serán el texto localizado del comando, no `commandList` el idioma predeterminado. La aplicación tendrá que responder correctamente.

## <a name="code-sample"></a>Ejemplo de código

| Nombre de ejemplo | Descripción | .NET |
|-------------|-------------|------|
| Localización de aplicaciones | Microsoft Teams localización de aplicaciones mediante bot y pestaña. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


