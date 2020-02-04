---
title: Referencia del esquema JSON del archivo de localización
description: Describe el esquema de localización compatible con el archivo de localización de Microsoft Teams.
keywords: localización del esquema del manifiesto de Microsoft Teams
ms.date: 05/20/2019
ms.openlocfilehash: 1a800ad514633455da8f4fb116e2a55c46cd39c7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675987"
---
# <a name="reference-localization-file-json-schema"></a>Referencia: esquema JSON del archivo de localización

El archivo de localización de Microsoft Teams describe las traducciones de idiomas que se servirán en función de la configuración de idioma del cliente. El archivo debe ajustarse al esquema hospedado [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json)en. Para obtener más información, consulte localización de la [aplicación](~/concepts/build-and-test/apps-localization.md).

## <a name="sample"></a>Muestra

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
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

## <a name="schema"></a>$schema

**URI**

La dirección URL de https://que hace referencia al esquema JSON del manifiesto.

> [!TIP]
> Especifique el esquema al principio del manifiesto para habilitar IntelliSense o compatibilidad similar desde el editor de código:`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",`

## <a name="nameshort"></a>nombre. Short

**Cadena, longitud máxima 30**

Reemplaza la cadena correspondiente del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="namefull"></a>nombre. Full

**Cadena, longitud máxima 100**

Reemplaza la cadena correspondiente del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="descriptionshort"></a>Descripción. Short

**Cadena, longitud máxima 80**

Reemplaza la cadena correspondiente del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="descriptionfull"></a>Descripción. Full

**Cadena, longitud máxima 4000**

Reemplaza la cadena correspondiente del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="statictabs0-910-5name"></a>staticTabs\\[([0-9] | 1 [0-5])\\]\\. nombre

**Cadena, longitud máxima 128**

Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="bots0commandlists0-2commands0-9title"></a>bots\\[0\\]\\. commandLists\\[[0-2]\\]\\. comandos\\[[0-9]\\]\\. title

**Cadena, longitud máxima 32**

Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="bots0commandlists0-2commands0-9description"></a>bots\\[0\\]\\. commandLists\\[[0-2]\\]\\. comandos\\[[0-9]\\]\\. Descripción

**Cadena, longitud máxima 128**

Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="composeextensions0commands0-9title"></a>composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. title

**Cadena, longitud máxima 32**

Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="composeextensions0commands0-9description"></a>composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. Description

**Cadena, longitud máxima 128**

Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="composeextensions0commands0-9parameters0-4title"></a>composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. Parameters\\[[\\0-4\\]]. title

**Cadena, longitud máxima 32**

Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="composeextensions0commands0-9parameters0-4description"></a>composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. Parameters\\[[\\0-4\\]]. Description

**Cadena, longitud máxima 128**

Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="composeextensions0commands0-9parameters0-4value"></a>composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. Parameters\\[[\\0-4\\]]. Value

**Cadena, longitud máxima 512**

Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. Parameters\\[[\\0-4\\]]\\. Choices [\\[\\0-9]]. title

**Cadena, longitud máxima 128**

Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.

## <a name="composeextensions0commands0-9taskinfotitle"></a>composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. taskInfo\\. title

**Cadena, longitud máxima 64**

Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.