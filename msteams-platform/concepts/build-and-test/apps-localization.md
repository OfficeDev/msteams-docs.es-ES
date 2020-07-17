---
title: Localización para las aplicaciones de equipo
description: Describe problemas relacionados con la localización de la aplicación
keywords: Microsoft Teams publicar AppSource de localización de Office Publishing idioma
ms.date: 05/15/2018
ms.openlocfilehash: 138b6d66808fc5ed212f1cb0eed8579faea6f764
ms.sourcegitcommit: bac0226d9048c363d96bbaf6f5395388c5f5c45a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "45039275"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="bbf0f-104">Localización de aplicaciones de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bbf0f-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="bbf0f-105">Al localizar la aplicación de Microsoft Teams, hay tres áreas principales que debe tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="bbf0f-106">La lista de AppSource (si está publicando en la tienda de aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="bbf0f-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="bbf0f-107">Las cadenas que se enfrentan al usuario final en el manifiesto de la aplicación (por ejemplo, comandos de bot).</span><span class="sxs-lookup"><span data-stu-id="bbf0f-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="bbf0f-108">Responder al texto localizado que envían los usuarios.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="bbf0f-109">Localización de la lista de AppSource</span><span class="sxs-lookup"><span data-stu-id="bbf0f-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="bbf0f-110">Si está publicando en la tienda de aplicaciones, debe tener en cuenta que la localización de la lista de AppSource todavía no es compatible.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="bbf0f-111">Sin embargo, para preparar la compatibilidad con las listas localizadas en la tienda de aplicaciones, puede agregar idiomas adicionales a la lista.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="bbf0f-112">Actualmente, en la lista de [sitios web de AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) de su aplicación solo se mostrará la información del idioma predeterminado (Inglés) que proporcione al [Centro para socios](/dev/store/use-partner-center-to-submit-to-appsource) .</span><span class="sxs-lookup"><span data-stu-id="bbf0f-112">Currently only the default (English) language information you provide in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="bbf0f-113">Para configurar un idioma adicional para la aplicación, en [centro de asociados](/dev/store/use-partner-center-to-submit-to-appsource), seleccione inglés y el idioma adicional de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-113">To configure an additional language for your app, in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource), select both English and the additional language of the app.</span></span> <span data-ttu-id="bbf0f-114">En este ejemplo se usa el francés.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-114">French is used in this example.</span></span>

1. <span data-ttu-id="bbf0f-115">Agregar al idioma inglés</span><span class="sxs-lookup"><span data-stu-id="bbf0f-115">Add English language</span></span>
    * <span data-ttu-id="bbf0f-116">Rellene el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-116">Fill in the app name.</span></span>
    * <span data-ttu-id="bbf0f-117">Rellene una breve descripción de la aplicación en inglés.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="bbf0f-118">Rellene la descripción larga de la aplicación en inglés.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="bbf0f-119">En la descripción larga, agregue también la línea "esta aplicación está disponible en" francés ".</span><span class="sxs-lookup"><span data-stu-id="bbf0f-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="bbf0f-120">Cargue las imágenes de la interfaz de usuario de la aplicación (en inglés).</span><span class="sxs-lookup"><span data-stu-id="bbf0f-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="bbf0f-121">Agregar idioma francés</span><span class="sxs-lookup"><span data-stu-id="bbf0f-121">Add French language</span></span>
    * <span data-ttu-id="bbf0f-122">Rellene el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-122">Fill in the app name.</span></span>
    * <span data-ttu-id="bbf0f-123">Rellene una breve descripción de la aplicación en francés.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="bbf0f-124">Rellene la descripción larga de la aplicación en francés.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="bbf0f-125">Cargue las imágenes de la interfaz de usuario de la aplicación (en francés).</span><span class="sxs-lookup"><span data-stu-id="bbf0f-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="bbf0f-126">Las imágenes que cargue con el idioma inglés serán las que se usan en AppSource.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="bbf0f-127">Localización de las cadenas en el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="bbf0f-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="bbf0f-128">Debe usar el esquema de aplicación de Microsoft Teams v 1.5 + para localizar correctamente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="bbf0f-129">Para ello, establezca el `$schema` atributo de la manifest.jsen archivo en ' https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json ' y actualice la propiedad ' manifestVersion ' a ' 1,7 '.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="bbf0f-130">Ejemplo manifest.jsel cambio</span><span class="sxs-lookup"><span data-stu-id="bbf0f-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="bbf0f-131">A continuación, querrá agregar la propiedad ' localizationInfo ' con el idioma predeterminado que admite la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="bbf0f-132">El idioma predeterminado se usa como idioma final de reserva si la configuración de cliente del usuario no coincide con ninguno de los idiomas adicionales.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="bbf0f-133">Ejemplo manifest.jsel cambio</span><span class="sxs-lookup"><span data-stu-id="bbf0f-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="bbf0f-134">Puede proporcionar archivos. JSON adicionales con traducciones de todas las cadenas a las que se enfrente el usuario en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="bbf0f-135">Estos archivos deben adherirse al [esquema JSON del archivo de localización](../../resources/schema/localization-schema.md) y deben agregarse a la propiedad ' localizationInfo ' del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-135">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="bbf0f-136">Cada archivo se correlaciona con una etiqueta de idioma que el cliente de Microsoft Teams usa para elegir las cadenas adecuadas.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="bbf0f-137">La etiqueta Language tiene la forma de <language> - <region> , pero se recomienda omitir la <region> parte para todas las regiones que admitan el idioma deseado.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="bbf0f-138">El cliente de Microsoft Teams aplicará las cadenas en este orden: cadenas de idioma predeterminadas-> cadenas de idioma del usuario solo cadenas-> idioma del usuario + cadenas de región del usuario.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="bbf0f-139">Por ejemplo, proporciona un idioma predeterminado de ' fr ' (Francés, todas las regiones) y archivos de idioma adicionales para ' en ' (Inglés, todas las regiones) y "en-GB" (Inglés, Gran Bretaña).</span><span class="sxs-lookup"><span data-stu-id="bbf0f-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="bbf0f-140">Si el idioma del usuario se establece en "en-GB":</span><span class="sxs-lookup"><span data-stu-id="bbf0f-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="bbf0f-141">El cliente de Microsoft Teams tomará las cadenas ' fr ' para sobrescribirlas con las cadenas ' en '.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="bbf0f-142">Sobrescriba los con las cadenas "en-GB".</span><span class="sxs-lookup"><span data-stu-id="bbf0f-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="bbf0f-143">Si el idioma del usuario se establece en "en-CA":</span><span class="sxs-lookup"><span data-stu-id="bbf0f-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="bbf0f-144">El cliente de Microsoft Teams tomará las cadenas ' fr ' para sobrescribirlas con las cadenas ' en '.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="bbf0f-145">Dado que no se proporciona localización de "en-CA", se usarán las localizaciones "en".</span><span class="sxs-lookup"><span data-stu-id="bbf0f-145">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="bbf0f-146">Si el idioma del usuario se establece en "es-es", el cliente de Microsoft Teams tomará las cadenas "fr" y no las invalidará con ninguno de los archivos de idioma.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="bbf0f-147">Por lo tanto, se recomienda encarecidamente proporcionar traducciones de nivel superior solo de idioma en el manifiesto (' en ' en lugar de ' en-US ') y solo proporcionar invalidaciones a nivel de región para las pocas cadenas que las necesitan.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="bbf0f-148">Ejemplo manifest.jsel cambio</span><span class="sxs-lookup"><span data-stu-id="bbf0f-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="bbf0f-149">Ejemplo de archivo localización. JSON</span><span class="sxs-lookup"><span data-stu-id="bbf0f-149">Example localization .json file</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="bbf0f-150">Tratamiento de envíos de texto localizados de los usuarios</span><span class="sxs-lookup"><span data-stu-id="bbf0f-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="bbf0f-151">Si proporciona versiones localizadas de la aplicación, es muy probable que los usuarios respondan con el mismo idioma.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="bbf0f-152">Microsoft Teams no traduce los envíos de usuario al idioma predeterminado, por lo que la aplicación necesitará controlarlo.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="bbf0f-153">Por ejemplo, si proporciona un localizado `commandList` , las respuestas a su bot serán el texto localizado del comando, no el idioma predeterminado.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="bbf0f-154">La aplicación tendrá que responder correctamente.</span><span class="sxs-lookup"><span data-stu-id="bbf0f-154">Your app will need to respond appropriately.</span></span>
