---
title: Localización de la aplicación
description: Describe consideraciones para la localización de la Microsoft Teams aplicación.
ms.topic: conceptual
localization_priority: Normal
keywords: teams publish store office publishing AppSource localization language
ms.date: 05/15/2018
ms.openlocfilehash: 9a939b1990d1b09410af344f79dd39b8b02c404b
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101712"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="c30c9-104">Localización para Microsoft Teams aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c30c9-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="c30c9-105">Al encontrar la aplicación Microsoft Teams, debes tener en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c30c9-105">When localizing your Microsoft Teams app, you must consider the following:</span></span>

1. <span data-ttu-id="c30c9-106">La Teams de la tienda (si procede).</span><span class="sxs-lookup"><span data-stu-id="c30c9-106">Your Teams store listing (if applicable).</span></span>
1. <span data-ttu-id="c30c9-107">Las cadenas de acceso del usuario final en el manifiesto de la aplicación (por ejemplo, comandos bot).</span><span class="sxs-lookup"><span data-stu-id="c30c9-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="c30c9-108">Responder al texto localizado enviado por los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c30c9-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="c30c9-109">Localización de la descripción de AppSource</span><span class="sxs-lookup"><span data-stu-id="c30c9-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="c30c9-110">Si vas a publicar en la tienda, debes tener en cuenta que aún no se admite la localización de la descripción de AppSource.</span><span class="sxs-lookup"><span data-stu-id="c30c9-110">If you're publishing to the store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="c30c9-111">Sin embargo, como preparación para la compatibilidad con las listas localizadas en la tienda de aplicaciones, puedes agregar idiomas adicionales a tu descripción.</span><span class="sxs-lookup"><span data-stu-id="c30c9-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="c30c9-112">Actualmente, solo la información de idioma predeterminada (inglés) que proporciones en el [Centro](/office/dev/store/submit-to-appsource-via-partner-center) de partners para tu descripción aparecerá en la descripción del sitio web de [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) para tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="c30c9-112">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

### <a name="example-of-configuring-localization"></a><span data-ttu-id="c30c9-113">Ejemplo de configuración de localización</span><span class="sxs-lookup"><span data-stu-id="c30c9-113">Example of configuring localization</span></span>

<span data-ttu-id="c30c9-114">Para configurar un idioma adicional para la aplicación, en el [Centro de partners,](/office/dev/store/submit-to-appsource-via-partner-center)selecciona inglés y el idioma adicional de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c30c9-114">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="c30c9-115">El francés se usa en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c30c9-115">French is used in this example.</span></span>

1. <span data-ttu-id="c30c9-116">Agregar idioma inglés</span><span class="sxs-lookup"><span data-stu-id="c30c9-116">Add English language</span></span>
    * <span data-ttu-id="c30c9-117">Rellene el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c30c9-117">Fill in the app name.</span></span>
    * <span data-ttu-id="c30c9-118">Rellene una breve descripción de la aplicación en inglés.</span><span class="sxs-lookup"><span data-stu-id="c30c9-118">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="c30c9-119">Rellene la descripción larga de la aplicación en inglés.</span><span class="sxs-lookup"><span data-stu-id="c30c9-119">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="c30c9-120">En la descripción larga, agrega también la línea "Esta aplicación está disponible en francés".</span><span class="sxs-lookup"><span data-stu-id="c30c9-120">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="c30c9-121">Upload las imágenes de la interfaz de usuario de la aplicación (en inglés).</span><span class="sxs-lookup"><span data-stu-id="c30c9-121">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="c30c9-122">Agregar francés</span><span class="sxs-lookup"><span data-stu-id="c30c9-122">Add French language</span></span>
    * <span data-ttu-id="c30c9-123">Rellene el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c30c9-123">Fill in the app name.</span></span>
    * <span data-ttu-id="c30c9-124">Rellene una breve descripción de la aplicación en francés.</span><span class="sxs-lookup"><span data-stu-id="c30c9-124">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="c30c9-125">Rellene la descripción larga de la aplicación en francés.</span><span class="sxs-lookup"><span data-stu-id="c30c9-125">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="c30c9-126">Upload las imágenes de la interfaz de usuario de la aplicación (en francés).</span><span class="sxs-lookup"><span data-stu-id="c30c9-126">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="c30c9-127">Las imágenes que cargues con el idioma inglés serán las que se usan en AppSource.</span><span class="sxs-lookup"><span data-stu-id="c30c9-127">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="c30c9-128">Localización de las cadenas en el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c30c9-128">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="c30c9-129">Debes usar el esquema Microsoft Teams aplicación v1.5+ para encontrar la aplicación correctamente.</span><span class="sxs-lookup"><span data-stu-id="c30c9-129">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="c30c9-130">Para ello, establece el atributo en el archivo manifest.jsen ' y actualiza la propiedad `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json 'manifestVersion' en '1,7'.</span><span class="sxs-lookup"><span data-stu-id="c30c9-130">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="c30c9-131">Ejemplo manifest.jsal cambiar</span><span class="sxs-lookup"><span data-stu-id="c30c9-131">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="c30c9-132">A continuación, querrá agregar la propiedad 'localizationInfo' con el idioma predeterminado que admite la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c30c9-132">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="c30c9-133">El idioma predeterminado se usa como el último idioma de reserva si la configuración del cliente del usuario no coincide con ninguno de los idiomas adicionales.</span><span class="sxs-lookup"><span data-stu-id="c30c9-133">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="c30c9-134">Ejemplo manifest.jsal cambiar</span><span class="sxs-lookup"><span data-stu-id="c30c9-134">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="c30c9-135">Puede proporcionar archivos .json adicionales con traducciones de todas las cadenas de acceso del usuario en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="c30c9-135">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="c30c9-136">Estos archivos deben cumplir el esquema [JSON](../../resources/schema/localization-schema.md) del archivo de localización y deben agregarse a la propiedad 'localizationInfo' del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="c30c9-136">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="c30c9-137">Cada archivo se correlaciona con una etiqueta de idioma que Teams cliente usa para elegir las cadenas adecuadas.</span><span class="sxs-lookup"><span data-stu-id="c30c9-137">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="c30c9-138">La etiqueta de idioma tiene la forma de, pero se recomienda omitir la parte para dirigirse a todas las <language> - <region> <region> regiones que admiten el idioma deseado.</span><span class="sxs-lookup"><span data-stu-id="c30c9-138">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="c30c9-139">El cliente Teams aplicará las cadenas en este orden: cadenas de idioma predeterminadas -> solo cadenas de idioma del usuario -> idioma del usuario + cadenas de región del usuario.</span><span class="sxs-lookup"><span data-stu-id="c30c9-139">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="c30c9-140">Por ejemplo, proporciona un idioma predeterminado de 'fr' (francés, todas las regiones) y archivos de idioma adicionales para 'en' (inglés, todas las regiones) y 'en-gb' (inglés, Gran Bretaña).</span><span class="sxs-lookup"><span data-stu-id="c30c9-140">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="c30c9-141">Si el idioma del usuario está establecido en 'en-gb':</span><span class="sxs-lookup"><span data-stu-id="c30c9-141">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="c30c9-142">El Teams tomará las cadenas 'fr' sobrescrituras con las cadenas 'en'.</span><span class="sxs-lookup"><span data-stu-id="c30c9-142">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="c30c9-143">Sobrescriba las cadenas 'en-gb'.</span><span class="sxs-lookup"><span data-stu-id="c30c9-143">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="c30c9-144">Si el idioma del usuario está establecido en 'en-ca':</span><span class="sxs-lookup"><span data-stu-id="c30c9-144">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="c30c9-145">El Teams tomará las cadenas 'fr' sobrescrituras con las cadenas 'en'.</span><span class="sxs-lookup"><span data-stu-id="c30c9-145">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="c30c9-146">Dado que no se proporciona ninguna localización 'en-ca', se usarán las localizaciones 'en'.</span><span class="sxs-lookup"><span data-stu-id="c30c9-146">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="c30c9-147">Si el idioma del usuario se establece en 'es-es', el cliente de Teams tomará las cadenas 'fr' y no las invalidará con ninguno de los archivos de idioma.</span><span class="sxs-lookup"><span data-stu-id="c30c9-147">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="c30c9-148">Por lo tanto, se recomienda encarecidamente proporcionar traducciones de solo idioma de nivel superior en el manifiesto ('en' en lugar de 'en-us') y solo proporcionar invalidaciones de nivel de región para las pocas cadenas que las necesitan.</span><span class="sxs-lookup"><span data-stu-id="c30c9-148">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="c30c9-149">Ejemplo manifest.jsal cambiar</span><span class="sxs-lookup"><span data-stu-id="c30c9-149">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="c30c9-150">Archivo .json de localización de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c30c9-150">Example localization .json file</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="c30c9-151">Controlar envíos de texto localizados de los usuarios</span><span class="sxs-lookup"><span data-stu-id="c30c9-151">Handling localized text submissions from your users</span></span>

<span data-ttu-id="c30c9-152">Si proporciona versiones localizadas de la aplicación, es muy probable que los usuarios respondan con el mismo idioma.</span><span class="sxs-lookup"><span data-stu-id="c30c9-152">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="c30c9-153">Teams convierte los envíos de usuario al idioma predeterminado, por lo que la aplicación tendrá que controlarlo.</span><span class="sxs-lookup"><span data-stu-id="c30c9-153">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="c30c9-154">Por ejemplo, si proporciona una localización , las respuestas al bot serán el texto localizado del comando, no `commandList` el idioma predeterminado.</span><span class="sxs-lookup"><span data-stu-id="c30c9-154">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="c30c9-155">La aplicación tendrá que responder correctamente.</span><span class="sxs-lookup"><span data-stu-id="c30c9-155">Your app will need to respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="c30c9-156">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="c30c9-156">Code sample</span></span>

| <span data-ttu-id="c30c9-157">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c30c9-157">Sample name</span></span> | <span data-ttu-id="c30c9-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="c30c9-158">Description</span></span> | <span data-ttu-id="c30c9-159">.NET</span><span class="sxs-lookup"><span data-stu-id="c30c9-159">.NET</span></span> |
|-------------|-------------|------|
| <span data-ttu-id="c30c9-160">Localización de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c30c9-160">App Localization</span></span> | <span data-ttu-id="c30c9-161">Microsoft Teams localización de aplicaciones mediante bot y pestaña.</span><span class="sxs-lookup"><span data-stu-id="c30c9-161">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="c30c9-162">View</span><span class="sxs-lookup"><span data-stu-id="c30c9-162">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


