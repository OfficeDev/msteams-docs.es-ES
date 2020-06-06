---
title: Localización para las aplicaciones de equipo
description: Describe problemas relacionados con la localización de la aplicación
keywords: Microsoft Teams publicar AppSource de localización de Office Publishing idioma
ms.date: 05/15/2018
ms.openlocfilehash: 30e4a2589bf5c1093723406c78cff2258554c486
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2020
ms.locfileid: "44590861"
---
# <a name="localization-for-microsoft-teams-apps"></a>Localización de aplicaciones de Microsoft Teams

Al localizar la aplicación de Microsoft Teams, hay tres áreas principales que debe tener en cuenta.

1. La lista de AppSource (si está publicando en la tienda de aplicaciones).
1. Las cadenas que se enfrentan al usuario final en el manifiesto de la aplicación (por ejemplo, comandos de bot).
1. Responder al texto localizado que envían los usuarios.

## <a name="localizing-your-appsource-listing"></a>Localización de la lista de AppSource

Si está publicando en la tienda de aplicaciones, debe tener en cuenta que la localización de la lista de AppSource todavía no es compatible. Sin embargo, para preparar la compatibilidad con las listas localizadas en la tienda de aplicaciones, puede agregar idiomas adicionales a la lista. Actualmente, en la lista de [sitios web de AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) de su aplicación solo se mostrará la información del idioma predeterminado (Inglés) que proporcione al [Centro para socios](/dev/store/use-partner-center-to-submit-to-appsource) .

Para configurar un idioma adicional para la aplicación, en [centro de asociados](/dev/store/use-partner-center-to-submit-to-appsource), seleccione inglés y el idioma adicional de la aplicación. En este ejemplo se usa el francés.

1. Agregar al idioma inglés
    * Rellene el nombre de la aplicación.
    * Rellene una breve descripción de la aplicación en inglés.
    * Rellene la descripción larga de la aplicación en inglés.
    * En la descripción larga, agregue también la línea "esta aplicación está disponible en" francés ".
    * Cargue las imágenes de la interfaz de usuario de la aplicación (en inglés).
2. Agregar idioma francés
    * Rellene el nombre de la aplicación.
    * Rellene una breve descripción de la aplicación en francés.
    * Rellene la descripción larga de la aplicación en francés.
    * Cargue las imágenes de la interfaz de usuario de la aplicación (en francés).

Las imágenes que cargue con el idioma inglés serán las que se usan en AppSource.

## <a name="localizing-the-strings-in-your-app-manifest"></a>Localización de las cadenas en el manifiesto de la aplicación

Debe usar el esquema de aplicación de Microsoft Teams v 1.5 + para localizar correctamente la aplicación. Para ello, establezca el atributo del `$schema` archivo manifest. JSON en ' https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json ' y actualice la propiedad ' manifestVersion ' a ' 1,5 '.

### <a name="example-manifestjson-change"></a>Cambio de manifiesto de ejemplo. JSON

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

A continuación, querrá agregar la propiedad ' localizationInfo ' con el idioma predeterminado que admite la aplicación. El idioma predeterminado se usa como idioma final de reserva si la configuración de cliente del usuario no coincide con ninguno de los idiomas adicionales.

### <a name="example-manifestjson-change"></a>Cambio de manifiesto de ejemplo. JSON

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

Puede proporcionar archivos. JSON adicionales con traducciones de todas las cadenas a las que se enfrente el usuario en el manifiesto. Estos archivos deben adherirse al [esquema JSON del archivo de localización](../../resources/schema/localization-schema.md) y deben agregarse a la propiedad ' localizationInfo ' del manifiesto. Cada archivo se correlaciona con una etiqueta de idioma que el cliente de Microsoft Teams usa para elegir las cadenas adecuadas. La etiqueta Language tiene la forma de <language> - <region> , pero se recomienda omitir la <region> parte para todas las regiones que admitan el idioma deseado.

El cliente de Microsoft Teams aplicará las cadenas en este orden: cadenas de idioma predeterminadas-> cadenas de idioma del usuario solo cadenas-> idioma del usuario + cadenas de región del usuario.

Por ejemplo, proporciona un idioma predeterminado de ' fr ' (Francés, todas las regiones) y archivos de idioma adicionales para ' en ' (Inglés, todas las regiones) y "en-GB" (Inglés, Gran Bretaña). Si el idioma del usuario se establece en "en-GB":

1. El cliente de Microsoft Teams tomará las cadenas ' fr ' para sobrescribirlas con las cadenas ' en '.
2. Sobrescriba los con las cadenas "en-GB".

Si el idioma del usuario se establece en "en-CA": 

1. El cliente de Microsoft Teams tomará las cadenas ' fr ' para sobrescribirlas con las cadenas ' en '.
2. Dado que no se proporciona localización de "en-CA", se usarán las localizaciones "en".

Si el idioma del usuario se establece en "es-es", el cliente de Microsoft Teams tomará las cadenas "fr" y no las invalidará con ninguno de los archivos de idioma.

Por lo tanto, se recomienda encarecidamente proporcionar traducciones de nivel superior solo de idioma en el manifiesto (' en ' en lugar de ' en-US ') y solo proporcionar invalidaciones a nivel de región para las pocas cadenas que las necesitan.

### <a name="example-manifestjson-change"></a>Cambio de manifiesto de ejemplo. JSON

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

### <a name="example-localization-json-file"></a>Ejemplo de archivo localización. JSON

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a>Tratamiento de envíos de texto localizados de los usuarios

Si proporciona versiones localizadas de la aplicación, es muy probable que los usuarios respondan con el mismo idioma. Microsoft Teams no traduce los envíos de usuario al idioma predeterminado, por lo que la aplicación necesitará controlarlo. Por ejemplo, si proporciona un localizado `commandList` , las respuestas a su bot serán el texto localizado del comando, no el idioma predeterminado. La aplicación tendrá que responder correctamente.
