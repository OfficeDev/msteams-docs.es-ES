---
title: Localizar la aplicación
description: Describe consideraciones para la localización de la Microsoft Teams aplicación.
ms.topic: conceptual
localization_priority: Normal
keywords: teams publish store office publishing AppSource localization language
ms.date: 05/15/2018
ms.openlocfilehash: 5410d6f829c3fec9b5d631452e459bd276df472e
ms.sourcegitcommit: c145d52b2d4daa7655e6c3ddfa739fa1beeb8d6a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2021
ms.locfileid: "53455216"
---
# <a name="localize-your-app"></a><span data-ttu-id="109ce-104">Localizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="109ce-104">Localize your app</span></span>

<span data-ttu-id="109ce-105">Debes tener en cuenta los siguientes factores para encontrar tu Microsoft Teams aplicación:</span><span class="sxs-lookup"><span data-stu-id="109ce-105">You must consider the following factors to localize your Microsoft Teams app:</span></span>

1. <span data-ttu-id="109ce-106">[Localiza la descripción de AppSource](#localize-your-appsource-listing).</span><span class="sxs-lookup"><span data-stu-id="109ce-106">[Localize your AppSource listing](#localize-your-appsource-listing).</span></span>
1. <span data-ttu-id="109ce-107">[Localiza las cadenas en el manifiesto de la aplicación](#localize-strings-in-your-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="109ce-107">[Localize strings in your app manifest](#localize-strings-in-your-app-manifest).</span></span> 
1. <span data-ttu-id="109ce-108">[Controlar envíos de texto localizados de los usuarios](#handle-localized-text-submissions-from-your-users).</span><span class="sxs-lookup"><span data-stu-id="109ce-108">[Handle localized text submissions from your users](#handle-localized-text-submissions-from-your-users).</span></span>

## <a name="localize-your-appsource-listing"></a><span data-ttu-id="109ce-109">Localización de la descripción de AppSource</span><span class="sxs-lookup"><span data-stu-id="109ce-109">Localize your AppSource listing</span></span>

<span data-ttu-id="109ce-110">Si vas a publicar la aplicación en la tienda, debes tener en cuenta que aún no se admite la localización de la descripción de AppSource.</span><span class="sxs-lookup"><span data-stu-id="109ce-110">If you are publishing the app to the store, you must be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="109ce-111">Para admitir las listas localizadas en la tienda de aplicaciones, puedes agregar idiomas adicionales a la descripción.</span><span class="sxs-lookup"><span data-stu-id="109ce-111">To support localized listings in the app store, you can add additional languages to your listing.</span></span> <span data-ttu-id="109ce-112">La información de idioma predeterminada que proporcionas en [el Centro de partners](/office/dev/store/submit-to-appsource-via-partner-center) para tu descripción aparece en la descripción del sitio web de [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource es un lugar para todas las necesidades de su equipo. reunir todo, incluidos chats, reuniones, llamadas, archivos y herramientas para permitir un trabajo en equipo más productivo.") para tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="109ce-112">The default language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing appears in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource is one place for all your team needs. bring everything together including chats, meetings, calls, files, and tools to enable more productive teamwork.") listing for your app.</span></span> <span data-ttu-id="109ce-113">Actualmente, el idioma predeterminado es inglés.</span><span class="sxs-lookup"><span data-stu-id="109ce-113">Currently, the default language is English.</span></span>

### <a name="configure-localization"></a><span data-ttu-id="109ce-114">Configurar la localización</span><span class="sxs-lookup"><span data-stu-id="109ce-114">Configure localization</span></span>

<span data-ttu-id="109ce-115">Para configurar un idioma adicional para la aplicación, en el [Centro de partners,](/office/dev/store/submit-to-appsource-via-partner-center)selecciona inglés y el idioma adicional de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="109ce-115">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="109ce-116">El francés se usa como un idioma adicional en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="109ce-116">French is used as an additional language in the following example:</span></span>

1. <span data-ttu-id="109ce-117">Agregar idioma inglés</span><span class="sxs-lookup"><span data-stu-id="109ce-117">Add English language</span></span>
    * <span data-ttu-id="109ce-118">Escribe el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="109ce-118">Enter the app name.</span></span>
    * <span data-ttu-id="109ce-119">Escribe una breve descripción de la aplicación en inglés.</span><span class="sxs-lookup"><span data-stu-id="109ce-119">Enter a short description of the app in English.</span></span>
    * <span data-ttu-id="109ce-120">Escribe la descripción larga de la aplicación en inglés.</span><span class="sxs-lookup"><span data-stu-id="109ce-120">Enter the long description of the app in English.</span></span>
    * <span data-ttu-id="109ce-121">En la descripción larga, escribe: **Esta aplicación está disponible en francés**.</span><span class="sxs-lookup"><span data-stu-id="109ce-121">In the long description, enter: **This app is available in French**.</span></span>
    * <span data-ttu-id="109ce-122">Upload las imágenes de la interfaz de usuario de la aplicación (en inglés).</span><span class="sxs-lookup"><span data-stu-id="109ce-122">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="109ce-123">Agregar francés</span><span class="sxs-lookup"><span data-stu-id="109ce-123">Add French language</span></span>
    * <span data-ttu-id="109ce-124">Escribe el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="109ce-124">Enter the app name.</span></span>
    * <span data-ttu-id="109ce-125">Escribe una breve descripción de la aplicación en francés.</span><span class="sxs-lookup"><span data-stu-id="109ce-125">Enter a short description of the app in French.</span></span>
    * <span data-ttu-id="109ce-126">Escribe la descripción larga de la aplicación en francés.</span><span class="sxs-lookup"><span data-stu-id="109ce-126">Enter the long description of the app in French.</span></span>
    * <span data-ttu-id="109ce-127">Upload las imágenes de la interfaz de usuario de la aplicación (en francés).</span><span class="sxs-lookup"><span data-stu-id="109ce-127">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="109ce-128">Las imágenes que carga con el idioma inglés se usan en AppSource.</span><span class="sxs-lookup"><span data-stu-id="109ce-128">The images that you upload with the English language are used in AppSource.</span></span>

## <a name="localize-strings-in-your-app-manifest"></a><span data-ttu-id="109ce-129">Localización de cadenas en el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="109ce-129">Localize strings in your app manifest</span></span>

<span data-ttu-id="109ce-130">Debes usar el esquema Microsoft Teams aplicación y `v1.5` más adelante para encontrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="109ce-130">You must use the Microsoft Teams app schema `v1.5` and later to localize your app.</span></span> <span data-ttu-id="109ce-131">Para ello, establece el atributo en el archivo manifest.jso posterior y actualiza la propiedad a `$schema` la versión ( en este **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** `manifestVersion` `$schema` `1.5` caso).</span><span class="sxs-lookup"><span data-stu-id="109ce-131">You can do this by setting the `$schema` attribute in your manifest.json file to **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** or higher and updating the `manifestVersion` property to `$schema` version (`1.5` in this case).</span></span> 

<span data-ttu-id="109ce-132">Debe agregar la propiedad `localizationInfo` con el idioma predeterminado que admite la aplicación.</span><span class="sxs-lookup"><span data-stu-id="109ce-132">You must add the `localizationInfo` property with the default language that your application supports.</span></span> <span data-ttu-id="109ce-133">El idioma predeterminado se usa como el idioma de reserva final si la configuración del cliente del usuario no coincide con ninguno de los idiomas adicionales.</span><span class="sxs-lookup"><span data-stu-id="109ce-133">The default language is used as the final fallback language if the user's client settings do not match with any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="109ce-134">Ejemplo manifest.jsal cambiar</span><span class="sxs-lookup"><span data-stu-id="109ce-134">Example manifest.json change</span></span>

<span data-ttu-id="109ce-135">La siguiente manifest.jsayuda a agregar la propiedad con el idioma predeterminado que la `localizationInfo` aplicación admite junto con `additionalLanguages` :</span><span class="sxs-lookup"><span data-stu-id="109ce-135">The following manifest.json helps to add the `localizationInfo` property with the default language that your application supports along with `additionalLanguages`:</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "localizationInfo": {
        "defaultLanguageTag": "en",
        "additionalLanguages": [
            {
                "languageTag": "es-mx",
                "file": "es-mx.json"
            }
        ]
    }
  ...
}
```

### <a name="example-localization-json-change"></a><span data-ttu-id="109ce-136">Ejemplo de cambio .json de localización</span><span class="sxs-lookup"><span data-stu-id="109ce-136">Example localization .json change</span></span>

<span data-ttu-id="109ce-137">A continuación se muestra un ejemplo para la localización .json:</span><span class="sxs-lookup"><span data-stu-id="109ce-137">Following is an example for localization .json:</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```


<span data-ttu-id="109ce-138">Puede proporcionar archivos .json adicionales con traducciones de todas las cadenas de acceso del usuario en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="109ce-138">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="109ce-139">Estos archivos deben cumplir el esquema JSON del archivo [de](../../resources/schema/localization-schema.md) localización y deben agregarse a la `localizationInfo` propiedad del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="109ce-139">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the `localizationInfo` property of your manifest.</span></span> <span data-ttu-id="109ce-140">Cada archivo se correlaciona con una etiqueta de idioma, que Teams cliente usa para seleccionar las cadenas adecuadas.</span><span class="sxs-lookup"><span data-stu-id="109ce-140">Each file correlates to a language tag, which the Teams client uses to select the appropriate strings.</span></span> <span data-ttu-id="109ce-141">La etiqueta de idioma tiene la forma de, pero puede omitir la parte para dirigirse a todas las `<language>-<region>` `<region>` regiones que admiten el idioma deseado.</span><span class="sxs-lookup"><span data-stu-id="109ce-141">The language tag takes the form of `<language>-<region>` but you can omit the `<region>` portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="109ce-142">El cliente Teams aplica las cadenas en el siguiente orden: cadenas de idioma predeterminadas -> idioma del usuario sólo cadenas -> idioma del usuario + cadenas de región del usuario.</span><span class="sxs-lookup"><span data-stu-id="109ce-142">The Teams client applies the strings in the following order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="109ce-143">Por ejemplo, proporciona un idioma predeterminado de "fr" (francés, todas las regiones) y archivos de idioma adicionales para "en" (inglés, todas las regiones) y "en-gb" (inglés, Gran Bretaña), el idioma del usuario se establece en "en-gb".</span><span class="sxs-lookup"><span data-stu-id="109ce-143">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain), the user's language is set to 'en-gb'.</span></span> <span data-ttu-id="109ce-144">Los siguientes cambios se llevan a cabo en función de la selección de idioma:</span><span class="sxs-lookup"><span data-stu-id="109ce-144">The following changes take place based on the language selection:</span></span>

1. <span data-ttu-id="109ce-145">El Teams toma las cadenas 'fr' y las sobrescribe con las cadenas 'en'.</span><span class="sxs-lookup"><span data-stu-id="109ce-145">The Teams client takes the 'fr' strings and overwrite them with the 'en' strings.</span></span>
1. <span data-ttu-id="109ce-146">Sobrescriba las cadenas 'en' con las cadenas 'en-gb'.</span><span class="sxs-lookup"><span data-stu-id="109ce-146">Overwrite the 'en' strings with the 'en-gb' strings.</span></span>

<span data-ttu-id="109ce-147">Si el idioma del usuario se establece en "en-ca", se realizarán los siguientes cambios en función de la selección de idioma:</span><span class="sxs-lookup"><span data-stu-id="109ce-147">If the user's language is set to 'en-ca', the following changes take place based on the language selection:</span></span> 

1. <span data-ttu-id="109ce-148">El Teams toma las cadenas 'fr' y las sobrescribe con las cadenas 'en'.</span><span class="sxs-lookup"><span data-stu-id="109ce-148">The Teams client takes the 'fr' strings and overwrite them with the 'en' strings.</span></span>
1. <span data-ttu-id="109ce-149">Dado que no se proporciona ninguna localización 'en-ca', se usan las localizaciones 'en'.</span><span class="sxs-lookup"><span data-stu-id="109ce-149">Since no 'en-ca' localization is supplied, the 'en\` localizations are used.</span></span>

<span data-ttu-id="109ce-150">Si el idioma del usuario se establece en 'es-es', el cliente Teams toma las cadenas 'fr'.</span><span class="sxs-lookup"><span data-stu-id="109ce-150">If the user's language is set to 'es-es', the Teams client takes the 'fr' strings.</span></span> <span data-ttu-id="109ce-151">El Teams no invalida las cadenas con ninguno de los archivos de idioma, ya que no se proporciona ninguna traducción de 'es' o 'es-es'.</span><span class="sxs-lookup"><span data-stu-id="109ce-151">The Teams client does not override the strings with any of the language files as no 'es' or 'es-es' translation is provided.</span></span>

<span data-ttu-id="109ce-152">Por lo tanto, debe proporcionar traducciones de nivel superior y solo de idioma en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="109ce-152">Therefore, you must provide top level, language only translations in your manifest.</span></span> <span data-ttu-id="109ce-153">Por ejemplo, 'en' en lugar de 'en-us'.</span><span class="sxs-lookup"><span data-stu-id="109ce-153">For example, 'en' instead of 'en-us'.</span></span> <span data-ttu-id="109ce-154">Debe proporcionar invalidaciones de nivel de región solo para las pocas cadenas que las necesiten.</span><span class="sxs-lookup"><span data-stu-id="109ce-154">You must provide region level overrides only for the few strings that need them.</span></span> 

### <a name="example-manifestjson-change"></a><span data-ttu-id="109ce-155">Ejemplo manifest.jsal cambiar</span><span class="sxs-lookup"><span data-stu-id="109ce-155">Example manifest.json change</span></span>

<span data-ttu-id="109ce-156">El manifest.jsal cambiar se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="109ce-156">The manifest.json change is shown in the following example:</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="109ce-157">Archivo .json de localización de ejemplo</span><span class="sxs-lookup"><span data-stu-id="109ce-157">Example localization .json file</span></span>

 <span data-ttu-id="109ce-158">El localization.jsal cambiar se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="109ce-158">The localization.json change is shown in the following example:</span></span>

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

## <a name="handle-localized-text-submissions-from-your-users"></a><span data-ttu-id="109ce-159">Controlar envíos de texto localizados de los usuarios</span><span class="sxs-lookup"><span data-stu-id="109ce-159">Handle localized text submissions from your users</span></span>

<span data-ttu-id="109ce-160">Si proporciona versiones localizadas de la aplicación, los usuarios responderán con el mismo idioma.</span><span class="sxs-lookup"><span data-stu-id="109ce-160">If your provide localized versions of your application, the users respond with the same language.</span></span> <span data-ttu-id="109ce-161">Como Teams convierte los envíos de usuario al idioma predeterminado, la aplicación debe controlar las respuestas de idioma localizado.</span><span class="sxs-lookup"><span data-stu-id="109ce-161">As Teams does not translate the user submissions back to the default language, your app must handle the localized language responses.</span></span> <span data-ttu-id="109ce-162">Por ejemplo, si proporciona una localización , las respuestas al bot son el texto localizado del comando, no `commandList` el idioma predeterminado.</span><span class="sxs-lookup"><span data-stu-id="109ce-162">For example, if you provide a localized `commandList`, the responses to your bot are the localized text of the command, not the default language.</span></span> <span data-ttu-id="109ce-163">La aplicación debe responder correctamente.</span><span class="sxs-lookup"><span data-stu-id="109ce-163">Your app must respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="109ce-164">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="109ce-164">Code sample</span></span>

| <span data-ttu-id="109ce-165">Ejemplo de nombre</span><span class="sxs-lookup"><span data-stu-id="109ce-165">Sample name</span></span> | <span data-ttu-id="109ce-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="109ce-166">Description</span></span> | <span data-ttu-id="109ce-167">.NET</span><span class="sxs-lookup"><span data-stu-id="109ce-167">.NET</span></span> | <span data-ttu-id="109ce-168">Node.js</span><span class="sxs-lookup"><span data-stu-id="109ce-168">Node.js</span></span> |
|-------------|-------------|------|------|
| <span data-ttu-id="109ce-169">Localización de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="109ce-169">App Localization</span></span> | <span data-ttu-id="109ce-170">Microsoft Teams localización de aplicaciones mediante bot y pestaña.</span><span class="sxs-lookup"><span data-stu-id="109ce-170">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="109ce-171">Ver</span><span class="sxs-lookup"><span data-stu-id="109ce-171">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[<span data-ttu-id="109ce-172">Ver</span><span class="sxs-lookup"><span data-stu-id="109ce-172">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

