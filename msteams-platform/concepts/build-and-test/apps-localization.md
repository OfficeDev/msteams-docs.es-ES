---
title: Localización de la aplicación
description: Describe las consideraciones para localizar la aplicación Microsoft Teams.
ms.topic: conceptual
localization_priority: Normal
keywords: equipos publican la oficina de la tienda publicando el idioma de localización de AppSource
ms.date: 05/15/2018
ms.openlocfilehash: a55b8af97e5306843858e5844a017dd402ab3516
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566050"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="33d66-104">Localización de aplicaciones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="33d66-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="33d66-105">Al localizar la aplicación Microsoft Teams, debe tener en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="33d66-105">When localizing your Microsoft Teams app, you must consider the following:</span></span>

1. <span data-ttu-id="33d66-106">Su Teams lista de la tienda (si corresponde).</span><span class="sxs-lookup"><span data-stu-id="33d66-106">Your Teams store listing (if applicable).</span></span>
1. <span data-ttu-id="33d66-107">Las cadenas orientadas al usuario final en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="33d66-107">The end-user facing strings in your app manifest.</span></span> <span data-ttu-id="33d66-108">Por ejemplo, comandos bot.</span><span class="sxs-lookup"><span data-stu-id="33d66-108">For example bot commands.</span></span>
1. <span data-ttu-id="33d66-109">Responder al texto localizado enviado por los usuarios.</span><span class="sxs-lookup"><span data-stu-id="33d66-109">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="33d66-110">Localización de su anuncio de AppSource</span><span class="sxs-lookup"><span data-stu-id="33d66-110">Localizing your AppSource listing</span></span>

<span data-ttu-id="33d66-111">Si va a publicar en la tienda, debe tener en cuenta que aún no se admite la localización de la lista de AppSource.</span><span class="sxs-lookup"><span data-stu-id="33d66-111">If you're publishing to the store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="33d66-112">Sin embargo, en preparación para la compatibilidad con anuncios localizados en la tienda de aplicaciones, puede agregar idiomas adicionales a su anuncio.</span><span class="sxs-lookup"><span data-stu-id="33d66-112">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="33d66-113">Actualmente solo aparecerá la información predeterminada (en inglés) que proporciones en [el Centro de partners](/office/dev/store/submit-to-appsource-via-partner-center) para tu anuncio en la lista del sitio web de [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) para tu aplicación.</span><span class="sxs-lookup"><span data-stu-id="33d66-113">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

### <a name="example-of-configuring-localization"></a><span data-ttu-id="33d66-114">Ejemplo de configuración de la localización</span><span class="sxs-lookup"><span data-stu-id="33d66-114">Example of configuring localization</span></span>

<span data-ttu-id="33d66-115">Para configurar un idioma adicional para la aplicación, en [el Centro de partners,](/office/dev/store/submit-to-appsource-via-partner-center)seleccione inglés y el idioma adicional de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="33d66-115">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="33d66-116">El francés se utiliza en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="33d66-116">French is used in this example:</span></span>

1. <span data-ttu-id="33d66-117">Añadir idioma inglés</span><span class="sxs-lookup"><span data-stu-id="33d66-117">Add English language</span></span>
    * <span data-ttu-id="33d66-118">Rellene el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="33d66-118">Fill in the app name.</span></span>
    * <span data-ttu-id="33d66-119">Rellene una breve descripción de la aplicación en inglés.</span><span class="sxs-lookup"><span data-stu-id="33d66-119">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="33d66-120">Rellene la larga descripción de la aplicación en inglés.</span><span class="sxs-lookup"><span data-stu-id="33d66-120">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="33d66-121">En la larga descripción, por favor agregue también la línea "Esta aplicación está disponible en "Francés".</span><span class="sxs-lookup"><span data-stu-id="33d66-121">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="33d66-122">Upload las imágenes de la interfaz de usuario de la aplicación (en inglés).</span><span class="sxs-lookup"><span data-stu-id="33d66-122">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="33d66-123">Añadir idioma francés</span><span class="sxs-lookup"><span data-stu-id="33d66-123">Add French language</span></span>
    * <span data-ttu-id="33d66-124">Rellene el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="33d66-124">Fill in the app name.</span></span>
    * <span data-ttu-id="33d66-125">Rellene una breve descripción de la aplicación en francés.</span><span class="sxs-lookup"><span data-stu-id="33d66-125">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="33d66-126">Rellene la larga descripción de la aplicación en francés.</span><span class="sxs-lookup"><span data-stu-id="33d66-126">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="33d66-127">Upload las imágenes de la interfaz de usuario de la aplicación (en francés).</span><span class="sxs-lookup"><span data-stu-id="33d66-127">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="33d66-128">Las imágenes que cargues con el idioma inglés serán las utilizadas en AppSource.</span><span class="sxs-lookup"><span data-stu-id="33d66-128">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="33d66-129">Localización de las cadenas en el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="33d66-129">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="33d66-130">Debe usar el esquema de aplicación Microsoft Teams v1.5+ para localizar correctamente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="33d66-130">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="33d66-131">Puede hacerlo estableciendo el atributo de la `$schema` manifest.jsen archivo ' ' y https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json actualizando la propiedad 'manifestVersion' a '1.7'.</span><span class="sxs-lookup"><span data-stu-id="33d66-131">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="33d66-132">Ejemplo manifest.jssobre el cambio</span><span class="sxs-lookup"><span data-stu-id="33d66-132">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="33d66-133">A continuación, deseará agregar la propiedad 'localizationInfo' con el idioma predeterminado que admite la aplicación.</span><span class="sxs-lookup"><span data-stu-id="33d66-133">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="33d66-134">El idioma predeterminado se utiliza como el idioma de reserva final si la configuración del cliente del usuario no coincide con ninguno de los idiomas adicionales.</span><span class="sxs-lookup"><span data-stu-id="33d66-134">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="33d66-135">Ejemplo manifest.jssobre el cambio</span><span class="sxs-lookup"><span data-stu-id="33d66-135">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="33d66-136">Puede proporcionar archivos .json adicionales con traducciones de todas las cadenas orientadas al usuario en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="33d66-136">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="33d66-137">Estos archivos deben adherirse al esquema JSON del [archivo de localización](../../resources/schema/localization-schema.md) y deben agregarse a la propiedad 'localizationInfo' del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="33d66-137">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="33d66-138">Cada archivo se correlaciona con una etiqueta de idioma que el cliente Teams utiliza para elegir las cadenas adecuadas.</span><span class="sxs-lookup"><span data-stu-id="33d66-138">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="33d66-139">La etiqueta de idioma toma la forma de <language> - <region> pero se recomienda omitir la <region> parte para dirigirse a todas las regiones que admiten el idioma deseado.</span><span class="sxs-lookup"><span data-stu-id="33d66-139">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="33d66-140">El cliente Teams aplicará las cadenas en este orden: cadenas de lenguaje predeterminadas -> lenguaje del usuario solo cadenas -> idioma del usuario + cadenas de región de usuario.</span><span class="sxs-lookup"><span data-stu-id="33d66-140">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="33d66-141">Por ejemplo, proporciona un idioma predeterminado de 'fr' (francés, todas las regiones) y archivos de idioma adicionales para 'en' (inglés, todas las regiones) y 'en-gb' (inglés, Gran Bretaña).</span><span class="sxs-lookup"><span data-stu-id="33d66-141">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="33d66-142">Si el idioma del usuario está establecido en 'en-gb':</span><span class="sxs-lookup"><span data-stu-id="33d66-142">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="33d66-143">El cliente Teams tomará las cadenas 'fr' sobrescribirlas con las cadenas 'en'.</span><span class="sxs-lookup"><span data-stu-id="33d66-143">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="33d66-144">Sobrescriba aquellos con las cadenas 'en-gb'.</span><span class="sxs-lookup"><span data-stu-id="33d66-144">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="33d66-145">Si el idioma del usuario se establece en 'en-ca':</span><span class="sxs-lookup"><span data-stu-id="33d66-145">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="33d66-146">El cliente Teams tomará las cadenas 'fr' sobrescribirlas con las cadenas 'en'.</span><span class="sxs-lookup"><span data-stu-id="33d66-146">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="33d66-147">Dado que no se suministra ninguna localización 'en-ca', se utilizarán las localizaciones 'en'.</span><span class="sxs-lookup"><span data-stu-id="33d66-147">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="33d66-148">Si el idioma del usuario se establece en 'es-es', el cliente Teams tomará las cadenas 'fr' y no las invalidará con ninguno de los archivos de idioma.</span><span class="sxs-lookup"><span data-stu-id="33d66-148">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="33d66-149">Por lo tanto, se recomienda encarecidamente proporcionar traducciones de nivel superior solo de idioma en el manifiesto ('en' en lugar de 'en-us') y proporcionar solo invalidaciones a nivel de región para las pocas cadenas que las necesitan.</span><span class="sxs-lookup"><span data-stu-id="33d66-149">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="33d66-150">Ejemplo manifest.jssobre el cambio</span><span class="sxs-lookup"><span data-stu-id="33d66-150">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="33d66-151">Ejemplo de localización del archivo .json</span><span class="sxs-lookup"><span data-stu-id="33d66-151">Example localization .json file</span></span>

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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="33d66-152">Manejo de envíos de texto localizados de los usuarios</span><span class="sxs-lookup"><span data-stu-id="33d66-152">Handling localized text submissions from your users</span></span>

<span data-ttu-id="33d66-153">Si proporciona versiones localizadas de la aplicación, es muy probable que los usuarios respondan con el mismo idioma.</span><span class="sxs-lookup"><span data-stu-id="33d66-153">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="33d66-154">Teams no traduce los envíos de usuario al idioma predeterminado, por lo que la aplicación tendrá que controlarlo.</span><span class="sxs-lookup"><span data-stu-id="33d66-154">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="33d66-155">Por ejemplo, si proporciona un localizado `commandList` , las respuestas al bot serán el texto localizado del comando, no el idioma predeterminado.</span><span class="sxs-lookup"><span data-stu-id="33d66-155">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="33d66-156">La aplicación tendrá que responder adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="33d66-156">Your app will need to respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="33d66-157">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="33d66-157">Code sample</span></span>

| <span data-ttu-id="33d66-158">Nombre de la muestra</span><span class="sxs-lookup"><span data-stu-id="33d66-158">Sample name</span></span> | <span data-ttu-id="33d66-159">Descripción</span><span class="sxs-lookup"><span data-stu-id="33d66-159">Description</span></span> | <span data-ttu-id="33d66-160">.NET</span><span class="sxs-lookup"><span data-stu-id="33d66-160">.NET</span></span> |
|-------------|-------------|------|
| <span data-ttu-id="33d66-161">Localización de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="33d66-161">App Localization</span></span> | <span data-ttu-id="33d66-162">Microsoft Teams localización de aplicaciones mediante bot y pestaña.</span><span class="sxs-lookup"><span data-stu-id="33d66-162">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="33d66-163">View</span><span class="sxs-lookup"><span data-stu-id="33d66-163">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


