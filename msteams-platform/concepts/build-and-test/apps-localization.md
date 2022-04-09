---
title: Localizar la aplicación
description: Describe las consideraciones para localizar la aplicación Microsoft Teams.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Los equipos publican el lenguaje de localización appSource de publicación de office de la tienda
ms.date: 05/15/2018
ms.openlocfilehash: 25a7694017cc8002ac23cf7075c59488ceb9773d
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737039"
---
# <a name="localize-your-app"></a>Localizar la aplicación

Tenga en cuenta los siguientes factores para localizar la aplicación de Microsoft Teams:

1. [Localiza tu lista de AppSource](#localize-your-appsource-listing).
1. [Localiza las cadenas en el manifiesto de la aplicación](#localize-strings-in-your-app-manifest).
1. [Controlar envíos de texto localizados de los usuarios](#handle-localized-text-submissions-from-your-users).

## <a name="localize-your-appsource-listing"></a>Localización de la lista de AppSource

Si va a publicar la aplicación en la tienda, proporcione metadatos (descripciones, capturas de pantalla, nombre) en los idiomas en los que desea que aparezca la aplicación y especifique explícitamente estos idiomas en la página **de listas de Marketplace** del Centro de partners. Para obtener más información, vea [Frentes localizados de Microsoft AppSource](/office/dev/store/prepare-localized-solutions#localized-microsoft-appsource-fronts). Para admitir descripciones localizadas en la tienda de aplicaciones, puede agregar idiomas adicionales a la descripción. La información de idioma predeterminada que proporcione en el [Centro de partners](/office/dev/store/submit-to-appsource-via-partner-center) para la descripción aparece en la lista del [sitio web de AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource es un lugar para todas las necesidades del equipo. reunir todo, incluidos chats, reuniones, llamadas, archivos y herramientas para permitir un trabajo en equipo más productivo.") de la aplicación. Actualmente, el idioma predeterminado es inglés.

### <a name="configure-localization"></a>Configuración de la localización

Para configurar un idioma adicional para la aplicación, en el [Centro de partners](/office/dev/store/submit-to-appsource-via-partner-center), seleccione inglés y el idioma adicional de la aplicación. El francés se usa como idioma adicional en el ejemplo siguiente:

1. Agregar idioma inglés
    * Escriba el nombre de la aplicación.
    * Escriba una breve descripción de la aplicación en inglés.
    * Escriba la descripción larga de la aplicación en inglés.
    * En la descripción larga, escriba: **Esta aplicación está disponible en francés**.
    * Upload las imágenes de la interfaz de usuario de la aplicación (en inglés).
2. Agregar idioma francés
    * Escriba el nombre de la aplicación.
    * Escriba una breve descripción de la aplicación en francés.
    * Escriba la descripción larga de la aplicación en francés.
    * Upload las imágenes de la interfaz de usuario de la aplicación (en francés).

Las imágenes que se cargan con el idioma inglés se usan en AppSource.

## <a name="localize-strings-in-your-app-manifest"></a>Localización de cadenas en el manifiesto de la aplicación

Usa el esquema `v1.5` de la aplicación Microsoft Teams y versiones posteriores para localizar la aplicación. Para ello, establezca el `$schema` atributo del archivo `https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json` manifest.json en o superior y actualice la propiedad a `$schema` la `manifestVersion` versión (`1.5` en este caso).

Agregue la `localizationInfo` propiedad con el idioma predeterminado que admite la aplicación. El idioma predeterminado se usa como idioma de reserva final si la configuración de cliente del usuario no coincide con ninguno de los idiomas adicionales.

### <a name="example-manifestjson-change"></a>Ejemplo de cambio de manifest.json

Lo siguiente `manifest.json` ayuda a agregar la `localizationInfo` propiedad con el idioma predeterminado que admite la aplicación junto con `additionalLanguages`:

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

### <a name="example-localization-json-change"></a>Cambio de .json de localización de ejemplo

A continuación se muestra un ejemplo de localización .json:

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```

Puede proporcionar archivos .json adicionales con traducciones de todas las cadenas orientadas al usuario en el manifiesto. Estos archivos deben cumplir el [esquema JSON del archivo de localización](../../resources/schema/localization-schema.md) y deben agregarse a la `localizationInfo` propiedad del manifiesto. Cada archivo se correlaciona con una etiqueta de idioma, que el cliente de Teams usa para seleccionar las cadenas adecuadas. La etiqueta de idioma tiene la forma de `<language>-<region>` , pero puede omitir la `<region>` parte para dirigirse a todas las regiones que admiten el idioma deseado.

El cliente de Teams aplica las cadenas en el orden siguiente: cadenas de idioma predeterminadas -> solo cadenas de idioma del usuario -> idioma del usuario + cadenas de región del usuario.

Por ejemplo, proporciona un idioma predeterminado de "fr" (francés, todas las regiones) y archivos de idioma adicionales para "en" (inglés, todas las regiones) y "en-gb" (inglés, Gran Bretaña), el idioma del usuario se establece en "en-gb". Los siguientes cambios tienen lugar en función de la selección de idioma:

1. El cliente Teams toma las cadenas "fr" y las sobrescribe con las cadenas "en".
1. Sobrescriba las cadenas "en" con las cadenas "en-gb".

Si el idioma del usuario está establecido en "en-ca", se producen los siguientes cambios en función de la selección de idioma:

1. El cliente Teams toma las cadenas "fr" y las sobrescribe con las cadenas "en".
1. Dado que no se proporciona ninguna localización "en-ca", se usan las localizaciones "en".

Si el idioma del usuario está establecido en "es-es", el cliente de Teams toma las cadenas "fr". El cliente de Teams no invalida las cadenas con ninguno de los archivos de idioma, ya que no se proporciona ninguna traducción "es" o "es-es".

Por lo tanto, debe proporcionar traducciones de nivel superior solo de idioma en el manifiesto. Por ejemplo, `en` en lugar de `en-us`. Debe proporcionar invalidaciones de nivel de región solo para las pocas cadenas que las necesitan.

### <a name="example-manifestjson-change"></a>Ejemplo de cambio de manifest.json

El `manifest.json` cambio se muestra en el ejemplo siguiente:

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

### <a name="example-localization-json-file"></a>Ejemplo de archivo .json de localización

 El `localization.json` cambio se muestra en el ejemplo siguiente:

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
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

## <a name="handle-localized-text-submissions-from-your-users"></a>Controlar envíos de texto localizado de los usuarios

Si proporciona versiones localizadas de la aplicación, los usuarios responderán con el mismo idioma. Como Teams no convierte los envíos de usuario al idioma predeterminado, la aplicación debe controlar las respuestas de idioma localizadas. Por ejemplo, si proporciona un elemento localizado `commandList`, las respuestas al bot son el texto localizado del comando, no el idioma predeterminado. La aplicación debe responder correctamente.

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | .NET | Node.js |
|-------------|-------------|------|------|
| Localización de aplicaciones | Microsoft Teams localización de aplicaciones mediante bot y pestaña. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[Ver](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>Consulte también

[Localizar la referencia de esquema JSON](~/resources/schema/localization-schema.md)
