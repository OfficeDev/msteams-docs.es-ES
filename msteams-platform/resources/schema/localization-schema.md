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
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="f31d8-104">Referencia: esquema JSON del archivo de localización</span><span class="sxs-lookup"><span data-stu-id="f31d8-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="f31d8-105">El archivo de localización de Microsoft Teams describe las traducciones de idiomas que se servirán en función de la configuración de idioma del cliente.</span><span class="sxs-lookup"><span data-stu-id="f31d8-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="f31d8-106">El archivo debe ajustarse al esquema hospedado [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json)en.</span><span class="sxs-lookup"><span data-stu-id="f31d8-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="f31d8-107">Para obtener más información, consulte localización de la [aplicación](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="f31d8-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="f31d8-108">Muestra</span><span class="sxs-lookup"><span data-stu-id="f31d8-108">Sample</span></span>

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

<span data-ttu-id="f31d8-109">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="f31d8-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="f31d8-110">$schema</span><span class="sxs-lookup"><span data-stu-id="f31d8-110">$schema</span></span>

<span data-ttu-id="f31d8-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="f31d8-111">**URI**</span></span>

<span data-ttu-id="f31d8-112">La dirección URL de https://que hace referencia al esquema JSON del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="f31d8-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="f31d8-113">Especifique el esquema al principio del manifiesto para habilitar IntelliSense o compatibilidad similar desde el editor de código:`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="f31d8-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="f31d8-114">nombre. Short</span><span class="sxs-lookup"><span data-stu-id="f31d8-114">name.short</span></span>

<span data-ttu-id="f31d8-115">**Cadena, longitud máxima 30**</span><span class="sxs-lookup"><span data-stu-id="f31d8-115">**String, Max Length 30**</span></span>

<span data-ttu-id="f31d8-116">Reemplaza la cadena correspondiente del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="f31d8-117">nombre. Full</span><span class="sxs-lookup"><span data-stu-id="f31d8-117">name.full</span></span>

<span data-ttu-id="f31d8-118">**Cadena, longitud máxima 100**</span><span class="sxs-lookup"><span data-stu-id="f31d8-118">**String, Max Length 100**</span></span>

<span data-ttu-id="f31d8-119">Reemplaza la cadena correspondiente del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="f31d8-120">Descripción. Short</span><span class="sxs-lookup"><span data-stu-id="f31d8-120">description.short</span></span>

<span data-ttu-id="f31d8-121">**Cadena, longitud máxima 80**</span><span class="sxs-lookup"><span data-stu-id="f31d8-121">**String, Max Length 80**</span></span>

<span data-ttu-id="f31d8-122">Reemplaza la cadena correspondiente del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="f31d8-123">Descripción. Full</span><span class="sxs-lookup"><span data-stu-id="f31d8-123">description.full</span></span>

<span data-ttu-id="f31d8-124">**Cadena, longitud máxima 4000**</span><span class="sxs-lookup"><span data-stu-id="f31d8-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="f31d8-125">Reemplaza la cadena correspondiente del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="f31d8-126">staticTabs\\[([0-9] | 1 [0-5])\\]\\. nombre</span><span class="sxs-lookup"><span data-stu-id="f31d8-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="f31d8-127">**Cadena, longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="f31d8-127">**String, Max Length 128**</span></span>

<span data-ttu-id="f31d8-128">Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="f31d8-129">bots\\[0\\]\\. commandLists\\[[0-2]\\]\\. comandos\\[[0-9]\\]\\. title</span><span class="sxs-lookup"><span data-stu-id="f31d8-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="f31d8-130">**Cadena, longitud máxima 32**</span><span class="sxs-lookup"><span data-stu-id="f31d8-130">**String, Max Length 32**</span></span>

<span data-ttu-id="f31d8-131">Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="f31d8-132">bots\\[0\\]\\. commandLists\\[[0-2]\\]\\. comandos\\[[0-9]\\]\\. Descripción</span><span class="sxs-lookup"><span data-stu-id="f31d8-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="f31d8-133">**Cadena, longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="f31d8-133">**String, Max Length 128**</span></span>

<span data-ttu-id="f31d8-134">Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="f31d8-135">composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. title</span><span class="sxs-lookup"><span data-stu-id="f31d8-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="f31d8-136">**Cadena, longitud máxima 32**</span><span class="sxs-lookup"><span data-stu-id="f31d8-136">**String, Max Length 32**</span></span>

<span data-ttu-id="f31d8-137">Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="f31d8-138">composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. Description</span><span class="sxs-lookup"><span data-stu-id="f31d8-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="f31d8-139">**Cadena, longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="f31d8-139">**String, Max Length 128**</span></span>

<span data-ttu-id="f31d8-140">Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="f31d8-141">composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. Parameters\\[[\\0-4\\]]. title</span><span class="sxs-lookup"><span data-stu-id="f31d8-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="f31d8-142">**Cadena, longitud máxima 32**</span><span class="sxs-lookup"><span data-stu-id="f31d8-142">**String, Max Length 32**</span></span>

<span data-ttu-id="f31d8-143">Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="f31d8-144">composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. Parameters\\[[\\0-4\\]]. Description</span><span class="sxs-lookup"><span data-stu-id="f31d8-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="f31d8-145">**Cadena, longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="f31d8-145">**String, Max Length 128**</span></span>

<span data-ttu-id="f31d8-146">Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="f31d8-147">composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. Parameters\\[[\\0-4\\]]. Value</span><span class="sxs-lookup"><span data-stu-id="f31d8-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="f31d8-148">**Cadena, longitud máxima 512**</span><span class="sxs-lookup"><span data-stu-id="f31d8-148">**String, Max Length 512**</span></span>

<span data-ttu-id="f31d8-149">Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="f31d8-150">composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. Parameters\\[[\\0-4\\]]\\. Choices [\\[\\0-9]]. title</span><span class="sxs-lookup"><span data-stu-id="f31d8-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="f31d8-151">**Cadena, longitud máxima 128**</span><span class="sxs-lookup"><span data-stu-id="f31d8-151">**String, Max Length 128**</span></span>

<span data-ttu-id="f31d8-152">Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="f31d8-153">composeExtensions\\[0\\]\\. comandos\\[[0-9]\\]\\. taskInfo\\. title</span><span class="sxs-lookup"><span data-stu-id="f31d8-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="f31d8-154">**Cadena, longitud máxima 64**</span><span class="sxs-lookup"><span data-stu-id="f31d8-154">**String, Max Length 64**</span></span>

<span data-ttu-id="f31d8-155">Reemplaza la cadena o cadenas correspondientes del manifiesto de la aplicación con el valor proporcionado aquí.</span><span class="sxs-lookup"><span data-stu-id="f31d8-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>