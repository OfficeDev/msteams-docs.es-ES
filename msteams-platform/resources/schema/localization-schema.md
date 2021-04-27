---
title: Referencia del esquema JSON del archivo de localización
description: Describe el esquema de localización admitido por el archivo de localización para Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: localización del esquema de manifiesto de teams
ms.date: 05/20/2019
ms.openlocfilehash: 3e4207fb3e862eac18c80ffc49e7c5648ae05c28
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019709"
---
# <a name="reference-localization-file-json-schema"></a>Referencia: esquema JSON del archivo de localización

El archivo de localización de Microsoft Teams describe las traducciones de idioma que se van a servir en función de la configuración del idioma del cliente. El archivo debe cumplir con el esquema hospedado en [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) . Para obtener información adicional, consulta [Localización de aplicaciones](~/concepts/build-and-test/apps-localization.md).

## <a name="sample"></a>Muestra

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

## <a name="schema"></a>$schema

**URI**

La https:// url que hace referencia al esquema JSON para el manifiesto.

> [!TIP]
> Especifique el esquema al principio del manifiesto para habilitar la IntelliSense o similar desde el editor de código: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>name.short

**String, Max Length 30**

Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="namefull"></a>name.full

**String, Max Length 100**

Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="descriptionshort"></a>description.short

**String, Max Length 80**

Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="descriptionfull"></a>description.full

**String, Longitud máxima 4000**

Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="statictabs0-910-5name"></a>staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name

**String, Longitud máxima 128**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="bots0commandlists0-2commands0-9title"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title

**String, Max Length 32**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="bots0commandlists0-2commands0-9description"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**String, Longitud máxima 128**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="composeextensions0commands0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title

**String, Max Length 32**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="composeextensions0commands0-9description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**String, Longitud máxima 128**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="composeextensions0commands0-9parameters0-4title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title

**String, Max Length 32**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="composeextensions0commands0-9parameters0-4description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description

**String, Longitud máxima 128**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="composeextensions0commands0-9parameters0-4value"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value

**String, Longitud máxima 512**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title

**String, Longitud máxima 128**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.

## <a name="composeextensions0commands0-9taskinfotitle"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title

**String, Max Length 64**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.
