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
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="0c5fd-104">Referencia: esquema JSON del archivo de localización</span><span class="sxs-lookup"><span data-stu-id="0c5fd-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="0c5fd-105">El archivo de localización de Microsoft Teams describe las traducciones de idioma que se ofrecerán en función de la configuración de idioma del cliente.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="0c5fd-106">El archivo debe cumplir con el esquema hospedado en [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="0c5fd-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="0c5fd-107">Para obtener información adicional, consulta [localización de la aplicación.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="0c5fd-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="0c5fd-108">Muestra</span><span class="sxs-lookup"><span data-stu-id="0c5fd-108">Sample</span></span>

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

<span data-ttu-id="0c5fd-109">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="0c5fd-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="0c5fd-110">$schema</span><span class="sxs-lookup"><span data-stu-id="0c5fd-110">$schema</span></span>

<span data-ttu-id="0c5fd-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-111">**URI**</span></span>

<span data-ttu-id="0c5fd-112">La https:// URL que hace referencia al esquema JSON del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="0c5fd-113">Especifique el esquema al principio del manifiesto para habilitar la compatibilidad IntelliSense o similar desde el editor de código: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="0c5fd-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="0c5fd-114">name.short</span><span class="sxs-lookup"><span data-stu-id="0c5fd-114">name.short</span></span>

<span data-ttu-id="0c5fd-115">**Cadena, longitud máxima 30**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-115">**String, Max Length 30**</span></span>

<span data-ttu-id="0c5fd-116">Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="0c5fd-117">name.full</span><span class="sxs-lookup"><span data-stu-id="0c5fd-117">name.full</span></span>

<span data-ttu-id="0c5fd-118">**Cadena, longitud máxima 100**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-118">**String, Max Length 100**</span></span>

<span data-ttu-id="0c5fd-119">Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="0c5fd-120">description.short</span><span class="sxs-lookup"><span data-stu-id="0c5fd-120">description.short</span></span>

<span data-ttu-id="0c5fd-121">**Cadena, longitud máxima 80**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-121">**String, Max Length 80**</span></span>

<span data-ttu-id="0c5fd-122">Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="0c5fd-123">description.full</span><span class="sxs-lookup"><span data-stu-id="0c5fd-123">description.full</span></span>

<span data-ttu-id="0c5fd-124">**Cadena, longitud máxima 4000**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="0c5fd-125">Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="0c5fd-126">staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name</span><span class="sxs-lookup"><span data-stu-id="0c5fd-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="0c5fd-127">**Cadena, longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-127">**String, Max Length 128**</span></span>

<span data-ttu-id="0c5fd-128">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="0c5fd-129">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="0c5fd-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="0c5fd-130">**Cadena, longitud máxima 32**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-130">**String, Max Length 32**</span></span>

<span data-ttu-id="0c5fd-131">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="0c5fd-132">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="0c5fd-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="0c5fd-133">**Cadena, longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-133">**String, Max Length 128**</span></span>

<span data-ttu-id="0c5fd-134">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="0c5fd-135">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="0c5fd-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="0c5fd-136">**Cadena, longitud máxima 32**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-136">**String, Max Length 32**</span></span>

<span data-ttu-id="0c5fd-137">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="0c5fd-138">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="0c5fd-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="0c5fd-139">**Cadena, longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-139">**String, Max Length 128**</span></span>

<span data-ttu-id="0c5fd-140">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="0c5fd-141">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="0c5fd-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="0c5fd-142">**Cadena, longitud máxima 32**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-142">**String, Max Length 32**</span></span>

<span data-ttu-id="0c5fd-143">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="0c5fd-144">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="0c5fd-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="0c5fd-145">**Cadena, longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-145">**String, Max Length 128**</span></span>

<span data-ttu-id="0c5fd-146">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="0c5fd-147">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value</span><span class="sxs-lookup"><span data-stu-id="0c5fd-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="0c5fd-148">**Cadena, longitud máxima 512**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-148">**String, Max Length 512**</span></span>

<span data-ttu-id="0c5fd-149">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="0c5fd-150">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="0c5fd-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="0c5fd-151">**Cadena, longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-151">**String, Max Length 128**</span></span>

<span data-ttu-id="0c5fd-152">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="0c5fd-153">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title</span><span class="sxs-lookup"><span data-stu-id="0c5fd-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="0c5fd-154">**Cadena, longitud máxima 64**</span><span class="sxs-lookup"><span data-stu-id="0c5fd-154">**String, Max Length 64**</span></span>

<span data-ttu-id="0c5fd-155">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor que se proporciona aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5fd-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
