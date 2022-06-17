---
title: Localizar la referencia de esquema JSON
description: Describe el esquema de localización compatible con el archivo de localización para Microsoft Teams mediante un esquema de ejemplo.
ms.topic: reference
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 23d02e845e4fcdc1c2fc76d8e9c376479fe1fa1f
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144281"
---
# <a name="localize-json-schema-reference"></a>Localizar la referencia de esquema JSON

El archivo de localización de Microsoft Teams describe las traducciones de idioma que se proporcionan en función de la configuración del idioma del cliente. El manifiesto debe ajustarse al esquema alojado en [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).

> [!TIP]
> Especifique el esquema al principio del manifiesto para habilitar `IntelliSense` o una compatibilidad similar desde el editor de código: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="example"></a>Ejemplo

El ejemplo de localización de esquema JSON es el siguiente:

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
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
|`$schema`|URI|ND|Dirección URL https:// que hace referencia al esquema JSON para el manifiesto.|
|`name.short`|Cadena|30|Reemplaza la cadena correspondiente del manifiesto de aplicación por el valor proporcionado aquí.|
|`name.full`|Cadena|100|Reemplaza la cadena correspondiente del manifiesto de aplicación por el valor proporcionado aquí.|
|`description.short`|Cadena|80|Reemplaza la cadena correspondiente del manifiesto de aplicación por el valor proporcionado aquí.|
|`description.full`|Cadena|4000|Reemplaza la cadena correspondiente del manifiesto de aplicación por el valor proporcionado aquí.|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|Cadena|128|Reemplaza las cadenas correspondientes del manifiesto de aplicación por el valor proporcionado aquí.|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|Cadena|32|Reemplaza las cadenas correspondientes del manifiesto de aplicación por el valor proporcionado aquí.|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|Cadena|128|Reemplaza las cadenas correspondientes del manifiesto de aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|Cadena|32|Reemplaza las cadenas correspondientes del manifiesto de aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|Cadena|128|Reemplaza las cadenas correspondientes del manifiesto de aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|Cadena|32|Reemplaza la cadena correspondiente del manifiesto de aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|Cadena|128|Reemplaza las cadenas correspondientes del manifiesto de aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|Cadena|512|Reemplaza la cadena correspondiente del manifiesto de aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|Cadena|128|Reemplaza las cadenas correspondientes del manifiesto de aplicación por el valor proporcionado aquí.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|Cadena|64|Reemplaza las cadenas correspondientes del manifiesto de aplicación por el valor proporcionado aquí.|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.description`|Cadena|128|Una breve descripción de la notificación.|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.templateText`|Cadena|128|P. ej.: " {actor} creó la tarea {taskId} para usted"|

## <a name="see-also"></a>Consulte también

[Localizar la aplicación](~/concepts/build-and-test/apps-localization.md)
