---
title: Localizar la referencia de esquema JSON
description: Describe el esquema de localización admitido por el archivo de localización para Microsoft Teams
ms.topic: reference
ms.localizationpriority: medium
keywords: localización del esquema de manifiesto de teams
ms.date: 05/20/2019
ms.openlocfilehash: 8c5f32fb8244f70fadc610ed7c193d97f11171f2
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157209"
---
# <a name="localize-json-schema-reference"></a>Localizar la referencia de esquema JSON

El Microsoft Teams de localización describe las traducciones de idioma que se sirven en función de la configuración del idioma del cliente. El archivo debe cumplir con el esquema hospedado en [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json) . 

> [!TIP]
> Especifique el esquema al principio del manifiesto para habilitar o `IntelliSense` compatibilidad similar desde el editor de código: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`

## <a name="example"></a>Ejemplo 

Ejemplo de esquema JSON de localización es el siguiente:

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "name.short": "Le App Studio",
  "name.full": "App Studio pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App Studio.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App Studio.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

El esquema define las siguientes propiedades:

|Propiedad|Tipo|Longitud máxima|Descripción|
|---------------|--------|---------|------------------|
|`$schema`|URI|N/D|La https:// url que hace referencia al esquema JSON para el manifiesto.|
|`name.short`|Cadena|30|Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.|
|`name.full`|Cadena|100|Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.|
|`description.short`|Cadena|80|Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.|
|`description.full`|Cadena|4000|Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|Cadena|128|Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|Cadena|32|Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.|
|`## bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|Cadena|128|Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|Cadena|32|Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|Cadena|128|Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|Cadena|32|Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|Cadena|128|Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|Cadena|512|Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|Cadena|128|Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|Cadena|64|Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.|

## <a name="see-also"></a>Consulte también

> [Localizar la aplicación](~/concepts/build-and-test/apps-localization.md)
