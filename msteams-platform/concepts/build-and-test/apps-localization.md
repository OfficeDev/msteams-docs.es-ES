---
title: Localización de la aplicación
description: Describe las consideraciones para localizar la aplicación Microsoft Teams.
ms.topic: conceptual
localization_priority: Normal
keywords: equipos publican la oficina de la tienda publicando el idioma de localización de AppSource
ms.date: 05/15/2018
ms.openlocfilehash: a55b8af97e5306843858e5844a017dd402ab3516
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566050"
---
# <a name="localization-for-microsoft-teams-apps"></a>Localización de aplicaciones de Microsoft Teams

Al localizar la aplicación Microsoft Teams, debe tener en cuenta lo siguiente:

1. Su Teams lista de la tienda (si corresponde).
1. Las cadenas orientadas al usuario final en el manifiesto de la aplicación. Por ejemplo, comandos bot.
1. Responder al texto localizado enviado por los usuarios.

## <a name="localizing-your-appsource-listing"></a>Localización de su anuncio de AppSource

Si va a publicar en la tienda, debe tener en cuenta que aún no se admite la localización de la lista de AppSource. Sin embargo, en preparación para la compatibilidad con anuncios localizados en la tienda de aplicaciones, puede agregar idiomas adicionales a su anuncio. Actualmente solo aparecerá la información predeterminada (en inglés) que proporciones en [el Centro de partners](/office/dev/store/submit-to-appsource-via-partner-center) para tu anuncio en la lista del sitio web de [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) para tu aplicación.

### <a name="example-of-configuring-localization"></a>Ejemplo de configuración de la localización

Para configurar un idioma adicional para la aplicación, en [el Centro de partners,](/office/dev/store/submit-to-appsource-via-partner-center)seleccione inglés y el idioma adicional de la aplicación. El francés se utiliza en este ejemplo:

1. Añadir idioma inglés
    * Rellene el nombre de la aplicación.
    * Rellene una breve descripción de la aplicación en inglés.
    * Rellene la larga descripción de la aplicación en inglés.
    * En la larga descripción, por favor agregue también la línea "Esta aplicación está disponible en "Francés".
    * Upload las imágenes de la interfaz de usuario de la aplicación (en inglés).
2. Añadir idioma francés
    * Rellene el nombre de la aplicación.
    * Rellene una breve descripción de la aplicación en francés.
    * Rellene la larga descripción de la aplicación en francés.
    * Upload las imágenes de la interfaz de usuario de la aplicación (en francés).

Las imágenes que cargues con el idioma inglés serán las utilizadas en AppSource.

## <a name="localizing-the-strings-in-your-app-manifest"></a>Localización de las cadenas en el manifiesto de la aplicación

Debe usar el esquema de aplicación Microsoft Teams v1.5+ para localizar correctamente la aplicación. Puede hacerlo estableciendo el atributo de la `$schema` manifest.jsen archivo ' ' y https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json actualizando la propiedad 'manifestVersion' a '1.7'.

### <a name="example-manifestjson-change"></a>Ejemplo manifest.jssobre el cambio

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

A continuación, deseará agregar la propiedad 'localizationInfo' con el idioma predeterminado que admite la aplicación. El idioma predeterminado se utiliza como el idioma de reserva final si la configuración del cliente del usuario no coincide con ninguno de los idiomas adicionales.

### <a name="example-manifestjson-change"></a>Ejemplo manifest.jssobre el cambio

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

Puede proporcionar archivos .json adicionales con traducciones de todas las cadenas orientadas al usuario en el manifiesto. Estos archivos deben adherirse al esquema JSON del [archivo de localización](../../resources/schema/localization-schema.md) y deben agregarse a la propiedad 'localizationInfo' del manifiesto. Cada archivo se correlaciona con una etiqueta de idioma que el cliente Teams utiliza para elegir las cadenas adecuadas. La etiqueta de idioma toma la forma de <language> - <region> pero se recomienda omitir la <region> parte para dirigirse a todas las regiones que admiten el idioma deseado.

El cliente Teams aplicará las cadenas en este orden: cadenas de lenguaje predeterminadas -> lenguaje del usuario solo cadenas -> idioma del usuario + cadenas de región de usuario.

Por ejemplo, proporciona un idioma predeterminado de 'fr' (francés, todas las regiones) y archivos de idioma adicionales para 'en' (inglés, todas las regiones) y 'en-gb' (inglés, Gran Bretaña). Si el idioma del usuario está establecido en 'en-gb':

1. El cliente Teams tomará las cadenas 'fr' sobrescribirlas con las cadenas 'en'.
2. Sobrescriba aquellos con las cadenas 'en-gb'.

Si el idioma del usuario se establece en 'en-ca': 

1. El cliente Teams tomará las cadenas 'fr' sobrescribirlas con las cadenas 'en'.
2. Dado que no se suministra ninguna localización 'en-ca', se utilizarán las localizaciones 'en'.

Si el idioma del usuario se establece en 'es-es', el cliente Teams tomará las cadenas 'fr' y no las invalidará con ninguno de los archivos de idioma.

Por lo tanto, se recomienda encarecidamente proporcionar traducciones de nivel superior solo de idioma en el manifiesto ('en' en lugar de 'en-us') y proporcionar solo invalidaciones a nivel de región para las pocas cadenas que las necesitan.

### <a name="example-manifestjson-change"></a>Ejemplo manifest.jssobre el cambio

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

### <a name="example-localization-json-file"></a>Ejemplo de localización del archivo .json

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

## <a name="handling-localized-text-submissions-from-your-users"></a>Manejo de envíos de texto localizados de los usuarios

Si proporciona versiones localizadas de la aplicación, es muy probable que los usuarios respondan con el mismo idioma. Teams no traduce los envíos de usuario al idioma predeterminado, por lo que la aplicación tendrá que controlarlo. Por ejemplo, si proporciona un localizado `commandList` , las respuestas al bot serán el texto localizado del comando, no el idioma predeterminado. La aplicación tendrá que responder adecuadamente.

## <a name="code-sample"></a>Ejemplo de código

| Nombre de la muestra | Descripción | .NET |
|-------------|-------------|------|
| Localización de aplicaciones | Microsoft Teams localización de aplicaciones mediante bot y pestaña. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


