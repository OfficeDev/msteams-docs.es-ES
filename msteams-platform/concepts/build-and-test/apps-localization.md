---
title: Localización de la aplicación
description: Describe consideraciones para la localización de la aplicación de Microsoft Teams.
ms.topic: conceptual
localization_priority: Normal
keywords: teams publish store office publishing AppSource localization language
ms.date: 05/15/2018
ms.openlocfilehash: 6c63bd5c71934d0a3342b31bc10feda38b8ae0d1
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075748"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="5957b-104">Localización de aplicaciones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5957b-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="5957b-105">Al encontrar la aplicación de Microsoft Teams, hay tres áreas principales que debes tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="5957b-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="5957b-106">La descripción de AppSource (si estás publicando en la tienda de aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="5957b-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="5957b-107">Las cadenas de acceso del usuario final en el manifiesto de la aplicación (por ejemplo, comandos bot).</span><span class="sxs-lookup"><span data-stu-id="5957b-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="5957b-108">Responder al texto localizado enviado por los usuarios.</span><span class="sxs-lookup"><span data-stu-id="5957b-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="5957b-109">Localización de la descripción de AppSource</span><span class="sxs-lookup"><span data-stu-id="5957b-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="5957b-110">Si vas a publicar en la tienda de aplicaciones, debes tener en cuenta que aún no se admite la localización de la descripción de AppSource.</span><span class="sxs-lookup"><span data-stu-id="5957b-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="5957b-111">Sin embargo, como preparación para la compatibilidad con las listas localizadas en la tienda de aplicaciones, puedes agregar idiomas adicionales a tu descripción.</span><span class="sxs-lookup"><span data-stu-id="5957b-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="5957b-112">Actualmente, solo la información de idioma predeterminada (inglés) que proporciones en el [Centro](/office/dev/store/submit-to-appsource-via-partner-center) de partners para tu descripción aparecerá en la descripción del sitio web de [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) para tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="5957b-112">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="5957b-113">Para configurar un idioma adicional para la aplicación, en el [Centro de partners,](/office/dev/store/submit-to-appsource-via-partner-center)selecciona inglés y el idioma adicional de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5957b-113">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="5957b-114">El francés se usa en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5957b-114">French is used in this example.</span></span>

1. <span data-ttu-id="5957b-115">Agregar idioma inglés</span><span class="sxs-lookup"><span data-stu-id="5957b-115">Add English language</span></span>
    * <span data-ttu-id="5957b-116">Rellene el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5957b-116">Fill in the app name.</span></span>
    * <span data-ttu-id="5957b-117">Rellene una breve descripción de la aplicación en inglés.</span><span class="sxs-lookup"><span data-stu-id="5957b-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="5957b-118">Rellene la descripción larga de la aplicación en inglés.</span><span class="sxs-lookup"><span data-stu-id="5957b-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="5957b-119">En la descripción larga, agrega también la línea "Esta aplicación está disponible en francés".</span><span class="sxs-lookup"><span data-stu-id="5957b-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="5957b-120">Cargue las imágenes de la interfaz de usuario de la aplicación (en inglés).</span><span class="sxs-lookup"><span data-stu-id="5957b-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="5957b-121">Agregar francés</span><span class="sxs-lookup"><span data-stu-id="5957b-121">Add French language</span></span>
    * <span data-ttu-id="5957b-122">Rellene el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5957b-122">Fill in the app name.</span></span>
    * <span data-ttu-id="5957b-123">Rellene una breve descripción de la aplicación en francés.</span><span class="sxs-lookup"><span data-stu-id="5957b-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="5957b-124">Rellene la descripción larga de la aplicación en francés.</span><span class="sxs-lookup"><span data-stu-id="5957b-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="5957b-125">Cargue las imágenes de la interfaz de usuario de la aplicación (en francés).</span><span class="sxs-lookup"><span data-stu-id="5957b-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="5957b-126">Las imágenes que cargues con el idioma inglés serán las que se usan en AppSource.</span><span class="sxs-lookup"><span data-stu-id="5957b-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="5957b-127">Localización de las cadenas en el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5957b-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="5957b-128">Debes usar el esquema de aplicación de Microsoft Teams v1.5+ para encontrarla correctamente.</span><span class="sxs-lookup"><span data-stu-id="5957b-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="5957b-129">Para ello, establece el atributo en el archivo manifest.jsen ' y actualiza la propiedad `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json 'manifestVersion' en '1,7'.</span><span class="sxs-lookup"><span data-stu-id="5957b-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="5957b-130">Ejemplo manifest.jsal cambiar</span><span class="sxs-lookup"><span data-stu-id="5957b-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="5957b-131">A continuación, querrá agregar la propiedad 'localizationInfo' con el idioma predeterminado que admite la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5957b-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="5957b-132">El idioma predeterminado se usa como el último idioma de reserva si la configuración del cliente del usuario no coincide con ninguno de los idiomas adicionales.</span><span class="sxs-lookup"><span data-stu-id="5957b-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="5957b-133">Ejemplo manifest.jsal cambiar</span><span class="sxs-lookup"><span data-stu-id="5957b-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="5957b-134">Puede proporcionar archivos .json adicionales con traducciones de todas las cadenas de acceso del usuario en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="5957b-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="5957b-135">Estos archivos deben cumplir el esquema [JSON](../../resources/schema/localization-schema.md) del archivo de localización y deben agregarse a la propiedad 'localizationInfo' del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="5957b-135">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="5957b-136">Cada archivo se correlaciona con una etiqueta de idioma que el cliente de Teams usa para elegir las cadenas adecuadas.</span><span class="sxs-lookup"><span data-stu-id="5957b-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="5957b-137">La etiqueta de idioma tiene la forma de, pero se recomienda omitir la parte para dirigirse a todas las <language> - <region> <region> regiones que admiten el idioma deseado.</span><span class="sxs-lookup"><span data-stu-id="5957b-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="5957b-138">El cliente de Teams aplicará las cadenas en este orden: cadenas de idioma predeterminadas -> idioma del usuario sólo cadenas -> idioma del usuario + cadenas de región del usuario.</span><span class="sxs-lookup"><span data-stu-id="5957b-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="5957b-139">Por ejemplo, proporciona un idioma predeterminado de 'fr' (francés, todas las regiones) y archivos de idioma adicionales para 'en' (inglés, todas las regiones) y 'en-gb' (inglés, Gran Bretaña).</span><span class="sxs-lookup"><span data-stu-id="5957b-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="5957b-140">Si el idioma del usuario está establecido en 'en-gb':</span><span class="sxs-lookup"><span data-stu-id="5957b-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="5957b-141">El cliente de Teams tomará las cadenas 'fr' sobrescrituras con las cadenas 'en'.</span><span class="sxs-lookup"><span data-stu-id="5957b-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="5957b-142">Sobrescriba las cadenas 'en-gb'.</span><span class="sxs-lookup"><span data-stu-id="5957b-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="5957b-143">Si el idioma del usuario está establecido en 'en-ca':</span><span class="sxs-lookup"><span data-stu-id="5957b-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="5957b-144">El cliente de Teams tomará las cadenas 'fr' sobrescrituras con las cadenas 'en'.</span><span class="sxs-lookup"><span data-stu-id="5957b-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="5957b-145">Dado que no se proporciona ninguna localización 'en-ca', se usarán las localizaciones 'en'.</span><span class="sxs-lookup"><span data-stu-id="5957b-145">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="5957b-146">Si el idioma del usuario se establece en 'es-es', el cliente de Teams tomará las cadenas 'fr' y no las invalidará con ninguno de los archivos de idioma.</span><span class="sxs-lookup"><span data-stu-id="5957b-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="5957b-147">Por lo tanto, se recomienda encarecidamente proporcionar traducciones de solo idioma de nivel superior en el manifiesto ('en' en lugar de 'en-us') y solo proporcionar invalidaciones de nivel de región para las pocas cadenas que las necesitan.</span><span class="sxs-lookup"><span data-stu-id="5957b-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="5957b-148">Ejemplo manifest.jsal cambiar</span><span class="sxs-lookup"><span data-stu-id="5957b-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="5957b-149">Archivo .json de localización de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5957b-149">Example localization .json file</span></span>

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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="5957b-150">Controlar envíos de texto localizados de los usuarios</span><span class="sxs-lookup"><span data-stu-id="5957b-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="5957b-151">Si proporciona versiones localizadas de la aplicación, es muy probable que los usuarios respondan con el mismo idioma.</span><span class="sxs-lookup"><span data-stu-id="5957b-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="5957b-152">Teams no traduce los envíos de los usuarios al idioma predeterminado, por lo que la aplicación tendrá que controlarlo.</span><span class="sxs-lookup"><span data-stu-id="5957b-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="5957b-153">Por ejemplo, si proporciona una localización , las respuestas al bot serán el texto localizado del comando, no `commandList` el idioma predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5957b-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="5957b-154">La aplicación tendrá que responder correctamente.</span><span class="sxs-lookup"><span data-stu-id="5957b-154">Your app will need to respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="5957b-155">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="5957b-155">Code sample</span></span>

| <span data-ttu-id="5957b-156">Nombre de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5957b-156">Sample name</span></span> | <span data-ttu-id="5957b-157">Description</span><span class="sxs-lookup"><span data-stu-id="5957b-157">Description</span></span> | <span data-ttu-id="5957b-158">.NET</span><span class="sxs-lookup"><span data-stu-id="5957b-158">.NET</span></span> |
|-------------|-------------|------|
| <span data-ttu-id="5957b-159">Localización de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="5957b-159">App Localization</span></span> | <span data-ttu-id="5957b-160">Localización de aplicaciones de Microsoft Teams mediante bot y pestaña.</span><span class="sxs-lookup"><span data-stu-id="5957b-160">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="5957b-161">View</span><span class="sxs-lookup"><span data-stu-id="5957b-161">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


