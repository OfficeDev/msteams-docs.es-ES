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
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="5fdd5-104">Referencia: esquema JSON del archivo de localización</span><span class="sxs-lookup"><span data-stu-id="5fdd5-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="5fdd5-105">El Microsoft Teams de localización describe las traducciones de idioma que se van a servir en función de la configuración del idioma del cliente.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="5fdd5-106">El archivo debe cumplir con el esquema hospedado en [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="5fdd5-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="5fdd5-107">Para obtener información adicional, consulta [Localización de aplicaciones](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="5fdd5-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="5fdd5-108">Muestra</span><span class="sxs-lookup"><span data-stu-id="5fdd5-108">Sample</span></span>

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

<span data-ttu-id="5fdd5-109">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="5fdd5-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="5fdd5-110">$schema</span><span class="sxs-lookup"><span data-stu-id="5fdd5-110">$schema</span></span>

<span data-ttu-id="5fdd5-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-111">**URI**</span></span>

<span data-ttu-id="5fdd5-112">La https:// url que hace referencia al esquema JSON para el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="5fdd5-113">Especifique el esquema al principio del manifiesto para habilitar la IntelliSense o similar desde el editor de código:`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="5fdd5-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="5fdd5-114">name.short</span><span class="sxs-lookup"><span data-stu-id="5fdd5-114">name.short</span></span>

<span data-ttu-id="5fdd5-115">**String, Max Length 30**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-115">**String, Max Length 30**</span></span>

<span data-ttu-id="5fdd5-116">Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="5fdd5-117">name.full</span><span class="sxs-lookup"><span data-stu-id="5fdd5-117">name.full</span></span>

<span data-ttu-id="5fdd5-118">**String, Max Length 100**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-118">**String, Max Length 100**</span></span>

<span data-ttu-id="5fdd5-119">Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="5fdd5-120">description.short</span><span class="sxs-lookup"><span data-stu-id="5fdd5-120">description.short</span></span>

<span data-ttu-id="5fdd5-121">**String, Max Length 80**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-121">**String, Max Length 80**</span></span>

<span data-ttu-id="5fdd5-122">Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="5fdd5-123">description.full</span><span class="sxs-lookup"><span data-stu-id="5fdd5-123">description.full</span></span>

<span data-ttu-id="5fdd5-124">**String, Longitud máxima 4000**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="5fdd5-125">Reemplaza la cadena correspondiente del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="5fdd5-126">staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name</span><span class="sxs-lookup"><span data-stu-id="5fdd5-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="5fdd5-127">**String, Longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-127">**String, Max Length 128**</span></span>

<span data-ttu-id="5fdd5-128">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="5fdd5-129">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="5fdd5-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="5fdd5-130">**String, Max Length 32**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-130">**String, Max Length 32**</span></span>

<span data-ttu-id="5fdd5-131">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="5fdd5-132">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="5fdd5-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="5fdd5-133">**String, Longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-133">**String, Max Length 128**</span></span>

<span data-ttu-id="5fdd5-134">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="5fdd5-135">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="5fdd5-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="5fdd5-136">**String, Max Length 32**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-136">**String, Max Length 32**</span></span>

<span data-ttu-id="5fdd5-137">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="5fdd5-138">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="5fdd5-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="5fdd5-139">**String, Longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-139">**String, Max Length 128**</span></span>

<span data-ttu-id="5fdd5-140">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="5fdd5-141">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="5fdd5-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="5fdd5-142">**String, Max Length 32**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-142">**String, Max Length 32**</span></span>

<span data-ttu-id="5fdd5-143">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="5fdd5-144">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="5fdd5-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="5fdd5-145">**String, Longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-145">**String, Max Length 128**</span></span>

<span data-ttu-id="5fdd5-146">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="5fdd5-147">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value</span><span class="sxs-lookup"><span data-stu-id="5fdd5-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="5fdd5-148">**String, Longitud máxima 512**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-148">**String, Max Length 512**</span></span>

<span data-ttu-id="5fdd5-149">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="5fdd5-150">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="5fdd5-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="5fdd5-151">**String, Longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-151">**String, Max Length 128**</span></span>

<span data-ttu-id="5fdd5-152">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="5fdd5-153">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title</span><span class="sxs-lookup"><span data-stu-id="5fdd5-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="5fdd5-154">**String, Max Length 64**</span><span class="sxs-lookup"><span data-stu-id="5fdd5-154">**String, Max Length 64**</span></span>

<span data-ttu-id="5fdd5-155">Reemplaza las cadenas correspondientes del manifiesto de la aplicación por el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="5fdd5-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
