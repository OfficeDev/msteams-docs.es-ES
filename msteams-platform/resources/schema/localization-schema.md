---
title: Referencia del esquema JSON del archivo de localización
description: Describe el esquema de localización admitido por el archivo de localización para Microsoft Teams
ms.topic: reference
keywords: localización del esquema de manifiesto de teams
ms.date: 05/20/2019
ms.openlocfilehash: 696a65de70a63e767f8fcdb040364fe90cde8716
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014603"
---
# <a name="reference-localization-file-json-schema"></a>Referencia: esquema JSON del archivo de localización

El archivo de localización de Microsoft Teams describe las traducciones de idioma que se ofrecerán en función de la configuración de idioma del cliente. El archivo debe cumplir con el esquema hospedado en [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) . Para obtener información adicional, consulta [localización de la aplicación.](~/concepts/build-and-test/apps-localization.md)

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

La https:// URL que hace referencia al esquema JSON del manifiesto.

> [!TIP]
> Especifique el esquema al principio del manifiesto para habilitar la compatibilidad IntelliSense o similar desde el editor de código: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>name.short

**Cadena, longitud máxima 30**

Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="namefull"></a>name.full

**Cadena, longitud máxima 100**

Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="descriptionshort"></a>description.short

**Cadena, longitud máxima 80**

Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="descriptionfull"></a>description.full

**Cadena, longitud máxima 4000**

Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="statictabs0-910-5name"></a>staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name

**Cadena, longitud máxima 128**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="bots0commandlists0-2commands0-9title"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title

**Cadena, longitud máxima 32**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="bots0commandlists0-2commands0-9description"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**Cadena, longitud máxima 128**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="composeextensions0commands0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title

**Cadena, longitud máxima 32**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="composeextensions0commands0-9description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**Cadena, longitud máxima 128**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="composeextensions0commands0-9parameters0-4title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title

**Cadena, longitud máxima 32**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="composeextensions0commands0-9parameters0-4description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description

**Cadena, longitud máxima 128**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="composeextensions0commands0-9parameters0-4value"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value

**Cadena, longitud máxima 512**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title

**Cadena, longitud máxima 128**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.

## <a name="composeextensions0commands0-9taskinfotitle"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title

**Cadena, longitud máxima 64**

Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.
