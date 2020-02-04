---
title: Referencia de esquema de manifiesto
description: Describe el esquema admitido por el manifiesto para Microsoft Teams.
keywords: esquema del manifiesto de Microsoft Teams
ms.openlocfilehash: d4a2864c18a5066673bafab42a46733a0ab5f116
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675986"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="a609b-104">Referencia: esquema de manifiesto para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a609b-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="a609b-105">El manifiesto de Microsoft Teams describe cómo se integra la aplicación en el producto de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a609b-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="a609b-106">El manifiesto debe cumplir el esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span><span class="sxs-lookup"><span data-stu-id="a609b-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="a609b-107">También se admiten las versiones anteriores 1.0-1.4 (mediante "v1. x" en la dirección URL).</span><span class="sxs-lookup"><span data-stu-id="a609b-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="a609b-108">En el siguiente ejemplo de esquema se muestran todas las opciones de extensibilidad.</span><span class="sxs-lookup"><span data-stu-id="a609b-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="a609b-109">Manifiesto completo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a609b-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "devicePermissions" : [ "geolocation", "media" ],
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters"
  },
  "description": {
    "short": "Short description of your app",
    "full": "Full description of your app"
  },
  "icons": {
    "outline": "%FILENAME-32x32px%",
    "color": "%FILENAME-192x192px"
  },
  "accentColor": "%HEX-COLOR%",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content?host=msteams",
      "websiteUrl": "https://contoso.com/content",
      "scopes": [ "personal" ]
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
  "connectors": [
    {
      "connectorId": "GUID-FROM-CONNECTOR-DEV-PORTAL%",
      "configurationUrl": "https://contoso.com/teamsconnector/configure",
      "scopes": [ "team"]
    }
  ],
  "composeExtensions": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "type" : "search",
          "context" : ["compose", "commandBox"],
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "description": "Enter the keywords to search for"
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "type" : "action",
          "fetchTask" : true,
          "context" : ["message"],
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType" : "text"
            }
          ]
        }
      ],
      "messageHandlers": [
        {
          "type" : "link",
          "value" : {
            "domains" : [
              "mysite.someplace.com",
              "othersite.someplace.com"
            ]
          }
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ]
}
```

<span data-ttu-id="a609b-110">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="a609b-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="a609b-111">$schema</span><span class="sxs-lookup"><span data-stu-id="a609b-111">$schema</span></span>

<span data-ttu-id="a609b-112">*Opcional, pero* &ndash; la cadena recomendada</span><span class="sxs-lookup"><span data-stu-id="a609b-112">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="a609b-113">La dirección URL de https://que hace referencia al esquema JSON del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="a609b-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="a609b-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="a609b-114">manifestVersion</span></span>

<span data-ttu-id="a609b-115">String **requerida** &ndash;</span><span class="sxs-lookup"><span data-stu-id="a609b-115">**Required** &ndash; String</span></span>

<span data-ttu-id="a609b-116">La versión del esquema del manifiesto que está usando este manifiesto.</span><span class="sxs-lookup"><span data-stu-id="a609b-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="a609b-117">Debe ser "1,5".</span><span class="sxs-lookup"><span data-stu-id="a609b-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="a609b-118">version</span><span class="sxs-lookup"><span data-stu-id="a609b-118">version</span></span>

<span data-ttu-id="a609b-119">String **requerida** &ndash;</span><span class="sxs-lookup"><span data-stu-id="a609b-119">**Required** &ndash; String</span></span>

<span data-ttu-id="a609b-120">La versión de la aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="a609b-120">The version of the specific app.</span></span> <span data-ttu-id="a609b-121">Si actualiza algo en el manifiesto, la versión también debe incrementarse.</span><span class="sxs-lookup"><span data-stu-id="a609b-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="a609b-122">De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="a609b-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="a609b-123">Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y a validarse.</span><span class="sxs-lookup"><span data-stu-id="a609b-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="a609b-124">A continuación, los usuarios de esta aplicación recibirán el nuevo manifiesto actualizado automáticamente en unas pocas horas, después de que se apruebe.</span><span class="sxs-lookup"><span data-stu-id="a609b-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="a609b-125">Si la aplicación ha solicitado un cambio de permisos, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="a609b-126">Esta cadena de versión debe seguir el estándar [SemVer](http://semver.org/) (Major. Secundaria. REVISIÓN).</span><span class="sxs-lookup"><span data-stu-id="a609b-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="a609b-127">id</span><span class="sxs-lookup"><span data-stu-id="a609b-127">id</span></span>

<span data-ttu-id="a609b-128">Identificador de aplicación de Microsoft **necesario** &ndash;</span><span class="sxs-lookup"><span data-stu-id="a609b-128">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="a609b-129">El identificador único generado por Microsoft para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="a609b-130">Si ha registrado un bot a través de Microsoft bot Framework o la aplicación Web de su pestaña ya inicia sesión en Microsoft, debe tener ya un identificador y escribirlo aquí.</span><span class="sxs-lookup"><span data-stu-id="a609b-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="a609b-131">De lo contrario, debe generar un nuevo identificador en el portal de registro de aplicaciones de Microsoft ([mis aplicaciones](https://apps.dev.microsoft.com)), escribirlo aquí y volver a usarlo cuando agregue un bot. Nota: Si va a enviar una actualización a su aplicación existente en AppSource, el identificador del manifiesto no debe modificarse.</span><span class="sxs-lookup"><span data-stu-id="a609b-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="packagename"></a><span data-ttu-id="a609b-132">packageName</span><span class="sxs-lookup"><span data-stu-id="a609b-132">packageName</span></span>

<span data-ttu-id="a609b-133">String **requerida** &ndash;</span><span class="sxs-lookup"><span data-stu-id="a609b-133">**Required** &ndash; String</span></span>

<span data-ttu-id="a609b-134">Un identificador único para esta aplicación en la notación de dominio inverso; por ejemplo, com. example. myapp.</span><span class="sxs-lookup"><span data-stu-id="a609b-134">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="a609b-135">developer</span><span class="sxs-lookup"><span data-stu-id="a609b-135">developer</span></span>

<span data-ttu-id="a609b-136">**Required**</span><span class="sxs-lookup"><span data-stu-id="a609b-136">**Required**</span></span>

<span data-ttu-id="a609b-137">Especifica información sobre la compañía.</span><span class="sxs-lookup"><span data-stu-id="a609b-137">Specifies information about your company.</span></span> <span data-ttu-id="a609b-138">Para las aplicaciones enviadas a AppSource (anteriormente tienda Office), estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="a609b-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="a609b-139">Consulte nuestras [directrices de publicación](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a609b-139">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="a609b-140">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-140">Name</span></span>| <span data-ttu-id="a609b-141">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-141">Maximum size</span></span> | <span data-ttu-id="a609b-142">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-142">Required</span></span> | <span data-ttu-id="a609b-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="a609b-144">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-144">32 characters</span></span>|<span data-ttu-id="a609b-145">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-145">✔</span></span>|<span data-ttu-id="a609b-146">El nombre para mostrar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a609b-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="a609b-147">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-147">2048 characters</span></span>|<span data-ttu-id="a609b-148">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-148">✔</span></span>|<span data-ttu-id="a609b-149">La dirección URL https://al sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a609b-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="a609b-150">Este vínculo debe llevar a los usuarios a su compañía o a la página de aterrizaje específica del producto.</span><span class="sxs-lookup"><span data-stu-id="a609b-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="a609b-151">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-151">2048 characters</span></span>|<span data-ttu-id="a609b-152">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-152">✔</span></span>|<span data-ttu-id="a609b-153">La dirección URL de https://a la Directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a609b-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="a609b-154">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-154">2048 characters</span></span>|<span data-ttu-id="a609b-155">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-155">✔</span></span>|<span data-ttu-id="a609b-156">La dirección URL de https://a las condiciones de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a609b-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="a609b-157">10 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-157">10 characters</span></span>| |<span data-ttu-id="a609b-158">**Opcional** IDENTIFICADOR de red de los socios de Microsoft que identifica la organización asociada que crea la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="a609b-159">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="a609b-159">localizationInfo</span></span>

<span data-ttu-id="a609b-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a609b-160">**Optional**</span></span>

<span data-ttu-id="a609b-161">Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="a609b-161">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="a609b-162">Consulte [localización](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="a609b-162">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="a609b-163">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-163">Name</span></span>| <span data-ttu-id="a609b-164">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-164">Maximum size</span></span> | <span data-ttu-id="a609b-165">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-165">Required</span></span> | <span data-ttu-id="a609b-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-166">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="a609b-167">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-167">✔</span></span>|<span data-ttu-id="a609b-168">La etiqueta de idioma de las cadenas en este archivo de manifiesto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="a609b-168">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="a609b-169">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="a609b-169">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="a609b-170">Una matriz de objetos que especifica traducciones de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="a609b-170">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="a609b-171">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-171">Name</span></span>| <span data-ttu-id="a609b-172">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-172">Maximum size</span></span> | <span data-ttu-id="a609b-173">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-173">Required</span></span> | <span data-ttu-id="a609b-174">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-174">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="a609b-175">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-175">✔</span></span>|<span data-ttu-id="a609b-176">La etiqueta de idioma de las cadenas en el archivo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="a609b-176">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="a609b-177">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-177">✔</span></span>|<span data-ttu-id="a609b-178">Una ruta de acceso relativa a un archivo. JSON que contiene las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="a609b-178">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="a609b-179">name</span><span class="sxs-lookup"><span data-stu-id="a609b-179">name</span></span>

<span data-ttu-id="a609b-180">**Required**</span><span class="sxs-lookup"><span data-stu-id="a609b-180">**Required**</span></span>

<span data-ttu-id="a609b-181">El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a609b-181">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="a609b-182">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="a609b-182">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="a609b-183">Los valores de `short` y `full` no deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="a609b-183">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="a609b-184">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-184">Name</span></span>| <span data-ttu-id="a609b-185">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-185">Maximum size</span></span> | <span data-ttu-id="a609b-186">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-186">Required</span></span> | <span data-ttu-id="a609b-187">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-187">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="a609b-188">30 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-188">30 characters</span></span>|<span data-ttu-id="a609b-189">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-189">✔</span></span>|<span data-ttu-id="a609b-190">El nombre para mostrar corto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-190">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="a609b-191">100 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-191">100 characters</span></span>||<span data-ttu-id="a609b-192">El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="a609b-192">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="a609b-193">description</span><span class="sxs-lookup"><span data-stu-id="a609b-193">description</span></span>

<span data-ttu-id="a609b-194">**Required**</span><span class="sxs-lookup"><span data-stu-id="a609b-194">**Required**</span></span>

<span data-ttu-id="a609b-195">Describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a609b-195">Describes your app to users.</span></span> <span data-ttu-id="a609b-196">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="a609b-196">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="a609b-197">Asegúrese de que la descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia.</span><span class="sxs-lookup"><span data-stu-id="a609b-197">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="a609b-198">También debe tener en cuenta, en la descripción completa, si se requiere uso de una cuenta externa.</span><span class="sxs-lookup"><span data-stu-id="a609b-198">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="a609b-199">Los valores de `short` y `full` no deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="a609b-199">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="a609b-200">La descripción breve no debe repetirse en la descripción larga y no debe incluir ningún otro nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-200">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="a609b-201">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-201">Name</span></span>| <span data-ttu-id="a609b-202">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-202">Maximum size</span></span> | <span data-ttu-id="a609b-203">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-203">Required</span></span> | <span data-ttu-id="a609b-204">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-204">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="a609b-205">80 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-205">80 characters</span></span>|<span data-ttu-id="a609b-206">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-206">✔</span></span>|<span data-ttu-id="a609b-207">Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.</span><span class="sxs-lookup"><span data-stu-id="a609b-207">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="a609b-208">4000 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-208">4000 characters</span></span>|<span data-ttu-id="a609b-209">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-209">✔</span></span>|<span data-ttu-id="a609b-210">La descripción completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-210">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="a609b-211">iconos</span><span class="sxs-lookup"><span data-stu-id="a609b-211">icons</span></span>

<span data-ttu-id="a609b-212">**Required**</span><span class="sxs-lookup"><span data-stu-id="a609b-212">**Required**</span></span>

<span data-ttu-id="a609b-213">Iconos usados en la aplicación Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a609b-213">Icons used within the Teams app.</span></span> <span data-ttu-id="a609b-214">Los archivos de icono deben incluirse como parte del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="a609b-214">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="a609b-215">Vea [iconos](~/concepts/build-and-test/apps-package.md#icons) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a609b-215">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="a609b-216">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-216">Name</span></span>| <span data-ttu-id="a609b-217">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-217">Maximum size</span></span> | <span data-ttu-id="a609b-218">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-218">Required</span></span> | <span data-ttu-id="a609b-219">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-219">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="a609b-220">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-220">2048 characters</span></span>|<span data-ttu-id="a609b-221">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-221">✔</span></span>|<span data-ttu-id="a609b-222">Una ruta de acceso relativa a un icono de esquema PNG transparente de 32x32.</span><span class="sxs-lookup"><span data-stu-id="a609b-222">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="a609b-223">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-223">2048 characters</span></span>|<span data-ttu-id="a609b-224">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-224">✔</span></span>|<span data-ttu-id="a609b-225">Una ruta de acceso de archivo relativa a un icono PNG 192x192 de color completo.</span><span class="sxs-lookup"><span data-stu-id="a609b-225">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="a609b-226">accentColor</span><span class="sxs-lookup"><span data-stu-id="a609b-226">accentColor</span></span>

<span data-ttu-id="a609b-227">String **requerida** &ndash;</span><span class="sxs-lookup"><span data-stu-id="a609b-227">**Required** &ndash; String</span></span>

<span data-ttu-id="a609b-228">Color que se va a usar junto con y como fondo de los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="a609b-228">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="a609b-229">El valor debe ser un código de color HTML válido que empiece por ' # ', `#4464ee`por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a609b-229">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="a609b-230">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="a609b-230">configurableTabs</span></span>

<span data-ttu-id="a609b-231">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a609b-231">**Optional**</span></span>

<span data-ttu-id="a609b-232">Se usa cuando la experiencia de la aplicación tiene una experiencia de la pestaña de canal de equipo que requiere una configuración adicional antes de que se agregue.</span><span class="sxs-lookup"><span data-stu-id="a609b-232">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="a609b-233">Las pestañas configurables solo se admiten en el ámbito de Teams y actualmente solo se admite una pestaña por aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-233">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="a609b-234">El objeto es una matriz con todos los elementos del tipo `object`.</span><span class="sxs-lookup"><span data-stu-id="a609b-234">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="a609b-235">Este bloque solo es necesario para las soluciones que proporcionan una solución de ficha de canal configurable.</span><span class="sxs-lookup"><span data-stu-id="a609b-235">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="a609b-236">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-236">Name</span></span>| <span data-ttu-id="a609b-237">Tipo</span><span class="sxs-lookup"><span data-stu-id="a609b-237">Type</span></span>| <span data-ttu-id="a609b-238">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-238">Maximum size</span></span> | <span data-ttu-id="a609b-239">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-239">Required</span></span> | <span data-ttu-id="a609b-240">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-240">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="a609b-241">String</span><span class="sxs-lookup"><span data-stu-id="a609b-241">String</span></span>|<span data-ttu-id="a609b-242">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-242">2048 characters</span></span>|<span data-ttu-id="a609b-243">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-243">✔</span></span>|<span data-ttu-id="a609b-244">Dirección URL de https://que se va a usar al configurar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a609b-244">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="a609b-245">Boolean</span><span class="sxs-lookup"><span data-stu-id="a609b-245">Boolean</span></span>|||<span data-ttu-id="a609b-246">Un valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de crearla.</span><span class="sxs-lookup"><span data-stu-id="a609b-246">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="a609b-247">Predeterminada`true`</span><span class="sxs-lookup"><span data-stu-id="a609b-247">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="a609b-248">Matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a609b-248">Array of enum</span></span>|<span data-ttu-id="a609b-249">1 </span><span class="sxs-lookup"><span data-stu-id="a609b-249">1</span></span>|<span data-ttu-id="a609b-250">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-250">✔</span></span>|<span data-ttu-id="a609b-251">Actualmente, las pestañas configurables solo admiten los `team` ámbitos y `groupchat` .</span><span class="sxs-lookup"><span data-stu-id="a609b-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="a609b-252">String</span><span class="sxs-lookup"><span data-stu-id="a609b-252">String</span></span>|<span data-ttu-id="a609b-253">2048</span><span class="sxs-lookup"><span data-stu-id="a609b-253">2048</span></span>||<span data-ttu-id="a609b-254">Una ruta de acceso de archivo relativa a una imagen de vista previa de pestaña para su uso en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a609b-254">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="a609b-255">Tamaño 1024x768.</span><span class="sxs-lookup"><span data-stu-id="a609b-255">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="a609b-256">Matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a609b-256">Array of enum</span></span>|<span data-ttu-id="a609b-257">1 </span><span class="sxs-lookup"><span data-stu-id="a609b-257">1</span></span>||<span data-ttu-id="a609b-258">Define cómo estará disponible la pestaña en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a609b-258">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="a609b-259">Las opciones `sharePointFullPage` son y`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="a609b-259">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="a609b-260">staticTabs</span><span class="sxs-lookup"><span data-stu-id="a609b-260">staticTabs</span></span>

<span data-ttu-id="a609b-261">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a609b-261">**Optional**</span></span>

<span data-ttu-id="a609b-262">Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente.</span><span class="sxs-lookup"><span data-stu-id="a609b-262">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="a609b-263">Las pestañas estáticas declaradas en `personal` el ámbito siempre están ancladas a la experiencia personal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-263">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="a609b-264">Actualmente no se admiten `team` las pestañas estáticas declaradas en el ámbito.</span><span class="sxs-lookup"><span data-stu-id="a609b-264">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="a609b-265">El objeto es una matriz (un máximo de 16 elementos) con todos los elementos del `object`tipo.</span><span class="sxs-lookup"><span data-stu-id="a609b-265">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="a609b-266">Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña estática.</span><span class="sxs-lookup"><span data-stu-id="a609b-266">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="a609b-267">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-267">Name</span></span>| <span data-ttu-id="a609b-268">Tipo</span><span class="sxs-lookup"><span data-stu-id="a609b-268">Type</span></span>| <span data-ttu-id="a609b-269">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-269">Maximum size</span></span> | <span data-ttu-id="a609b-270">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-270">Required</span></span> | <span data-ttu-id="a609b-271">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-271">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="a609b-272">String</span><span class="sxs-lookup"><span data-stu-id="a609b-272">String</span></span>|<span data-ttu-id="a609b-273">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-273">64 characters</span></span>|<span data-ttu-id="a609b-274">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-274">✔</span></span>|<span data-ttu-id="a609b-275">Un identificador único para la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a609b-275">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="a609b-276">String</span><span class="sxs-lookup"><span data-stu-id="a609b-276">String</span></span>|<span data-ttu-id="a609b-277">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-277">128 characters</span></span>|<span data-ttu-id="a609b-278">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-278">✔</span></span>|<span data-ttu-id="a609b-279">El nombre para mostrar de la pestaña en la interfaz de canal.</span><span class="sxs-lookup"><span data-stu-id="a609b-279">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="a609b-280">String</span><span class="sxs-lookup"><span data-stu-id="a609b-280">String</span></span>|<span data-ttu-id="a609b-281">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-281">2048 characters</span></span>|<span data-ttu-id="a609b-282">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-282">✔</span></span>|<span data-ttu-id="a609b-283">Dirección URL de https://que señala a la interfaz de usuario de la entidad que se va a mostrar en el lienzo de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a609b-283">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="a609b-284">String</span><span class="sxs-lookup"><span data-stu-id="a609b-284">String</span></span>|<span data-ttu-id="a609b-285">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-285">2048 characters</span></span>||<span data-ttu-id="a609b-286">La dirección URL de https://para apuntar a si un usuario opta por verlo en un explorador.</span><span class="sxs-lookup"><span data-stu-id="a609b-286">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="a609b-287">Matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a609b-287">Array of enum</span></span>|<span data-ttu-id="a609b-288">1 </span><span class="sxs-lookup"><span data-stu-id="a609b-288">1</span></span>|<span data-ttu-id="a609b-289">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-289">✔</span></span>|<span data-ttu-id="a609b-290">Actualmente, las pestañas estáticas `personal` solo admiten el ámbito, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.</span><span class="sxs-lookup"><span data-stu-id="a609b-290">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="a609b-291">transferido</span><span class="sxs-lookup"><span data-stu-id="a609b-291">bots</span></span>

<span data-ttu-id="a609b-292">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a609b-292">**Optional**</span></span>

<span data-ttu-id="a609b-293">Define una solución de bot, junto con información opcional como propiedades de comando predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="a609b-293">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="a609b-294">El objeto es una matriz (un máximo de solo 1&mdash;elemento solo es posible para cada aplicación) con todos los elementos del tipo `object`.</span><span class="sxs-lookup"><span data-stu-id="a609b-294">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="a609b-295">Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.</span><span class="sxs-lookup"><span data-stu-id="a609b-295">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="a609b-296">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-296">Name</span></span>| <span data-ttu-id="a609b-297">Tipo</span><span class="sxs-lookup"><span data-stu-id="a609b-297">Type</span></span>| <span data-ttu-id="a609b-298">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-298">Maximum size</span></span> | <span data-ttu-id="a609b-299">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-299">Required</span></span> | <span data-ttu-id="a609b-300">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-300">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a609b-301">String</span><span class="sxs-lookup"><span data-stu-id="a609b-301">String</span></span>|<span data-ttu-id="a609b-302">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-302">64 characters</span></span>|<span data-ttu-id="a609b-303">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-303">✔</span></span>|<span data-ttu-id="a609b-304">IDENTIFICADOR único de la aplicación de Microsoft para el bot como se registra con bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a609b-304">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="a609b-305">Puede ser el mismo que el [identificador de aplicación](#id)general.</span><span class="sxs-lookup"><span data-stu-id="a609b-305">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="a609b-306">Boolean</span><span class="sxs-lookup"><span data-stu-id="a609b-306">Boolean</span></span>|||<span data-ttu-id="a609b-307">Describe si el bot utiliza o no una sugerencia del usuario para agregar el bot a un canal específico.</span><span class="sxs-lookup"><span data-stu-id="a609b-307">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="a609b-308">Predeterminada`false`</span><span class="sxs-lookup"><span data-stu-id="a609b-308">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="a609b-309">Boolean</span><span class="sxs-lookup"><span data-stu-id="a609b-309">Boolean</span></span>|||<span data-ttu-id="a609b-310">Indica si un bot es un bot? a de solo notificaciones unidireccional, a diferencia de un bot? a de la conversación.</span><span class="sxs-lookup"><span data-stu-id="a609b-310">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="a609b-311">Predeterminada`false`</span><span class="sxs-lookup"><span data-stu-id="a609b-311">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="a609b-312">Boolean</span><span class="sxs-lookup"><span data-stu-id="a609b-312">Boolean</span></span>|||<span data-ttu-id="a609b-313">Indica si el bot admite la capacidad de cargar o descargar archivos en un chat personal.</span><span class="sxs-lookup"><span data-stu-id="a609b-313">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="a609b-314">Predeterminada`false`</span><span class="sxs-lookup"><span data-stu-id="a609b-314">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="a609b-315">Matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a609b-315">Array of enum</span></span>|<span data-ttu-id="a609b-316">3 </span><span class="sxs-lookup"><span data-stu-id="a609b-316">3</span></span>|<span data-ttu-id="a609b-317">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-317">✔</span></span>|<span data-ttu-id="a609b-318">Especifica si bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat en grupo (`groupchat`) o una experiencia en un ámbito específico de un solo usuario (`personal`).</span><span class="sxs-lookup"><span data-stu-id="a609b-318">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a609b-319">Estas opciones no son exclusivas.</span><span class="sxs-lookup"><span data-stu-id="a609b-319">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="a609b-320">bots. commandLists</span><span class="sxs-lookup"><span data-stu-id="a609b-320">bots.commandLists</span></span>

<span data-ttu-id="a609b-321">Una lista opcional de comandos que el bot puede recomendar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a609b-321">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="a609b-322">El objeto es una matriz (un máximo de 2 elementos) con todos los elementos `object`de tipo; debe definir una lista de comandos independiente para cada ámbito que admita el bot.</span><span class="sxs-lookup"><span data-stu-id="a609b-322">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="a609b-323">Consulte [menús de bot](~/bots/how-to/create-a-bot-commands-menu.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a609b-323">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="a609b-324">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-324">Name</span></span>| <span data-ttu-id="a609b-325">Tipo</span><span class="sxs-lookup"><span data-stu-id="a609b-325">Type</span></span>| <span data-ttu-id="a609b-326">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-326">Maximum size</span></span> | <span data-ttu-id="a609b-327">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-327">Required</span></span> | <span data-ttu-id="a609b-328">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-328">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="a609b-329">matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a609b-329">array of enum</span></span>|<span data-ttu-id="a609b-330">3 </span><span class="sxs-lookup"><span data-stu-id="a609b-330">3</span></span>|<span data-ttu-id="a609b-331">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-331">✔</span></span>|<span data-ttu-id="a609b-332">Especifica el ámbito para el que es válida la lista de comandos.</span><span class="sxs-lookup"><span data-stu-id="a609b-332">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="a609b-333">Las opciones `team`son `personal`, y `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="a609b-333">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="a609b-334">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a609b-334">array of objects</span></span>|<span data-ttu-id="a609b-335">10 </span><span class="sxs-lookup"><span data-stu-id="a609b-335">10</span></span>|<span data-ttu-id="a609b-336">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-336">✔</span></span>|<span data-ttu-id="a609b-337">Una matriz de comandos que el bot admite:</span><span class="sxs-lookup"><span data-stu-id="a609b-337">An array of commands the bot supports:</span></span><br><span data-ttu-id="a609b-338">`title`: el nombre del comando Bot (cadena, 32)</span><span class="sxs-lookup"><span data-stu-id="a609b-338">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="a609b-339">`description`: una descripción sencilla o un ejemplo de la sintaxis del comando y su argumento (String, 128)</span><span class="sxs-lookup"><span data-stu-id="a609b-339">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="a609b-340">Connector</span><span class="sxs-lookup"><span data-stu-id="a609b-340">connectors</span></span>

<span data-ttu-id="a609b-341">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a609b-341">**Optional**</span></span>

<span data-ttu-id="a609b-342">El `connectors` bloque define un conector de Office 365 para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-342">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="a609b-343">El objeto es una matriz (un máximo de 1 elemento) con todos los elementos `object`de tipo.</span><span class="sxs-lookup"><span data-stu-id="a609b-343">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="a609b-344">Este bloque solo es necesario para las soluciones que proporcionan un conector.</span><span class="sxs-lookup"><span data-stu-id="a609b-344">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="a609b-345">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-345">Name</span></span>| <span data-ttu-id="a609b-346">Tipo</span><span class="sxs-lookup"><span data-stu-id="a609b-346">Type</span></span>| <span data-ttu-id="a609b-347">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-347">Maximum size</span></span> | <span data-ttu-id="a609b-348">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-348">Required</span></span> | <span data-ttu-id="a609b-349">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-349">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="a609b-350">String</span><span class="sxs-lookup"><span data-stu-id="a609b-350">String</span></span>|<span data-ttu-id="a609b-351">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-351">2048 characters</span></span>|<span data-ttu-id="a609b-352">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-352">✔</span></span>|<span data-ttu-id="a609b-353">Dirección URL de https://que se va a usar al configurar el conector.</span><span class="sxs-lookup"><span data-stu-id="a609b-353">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="a609b-354">String</span><span class="sxs-lookup"><span data-stu-id="a609b-354">String</span></span>|<span data-ttu-id="a609b-355">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-355">64 characters</span></span>|<span data-ttu-id="a609b-356">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-356">✔</span></span>|<span data-ttu-id="a609b-357">Un identificador único para el conector que coincide con su identificador en el [panel del programador de conectores](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="a609b-357">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="a609b-358">Matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a609b-358">Array of enum</span></span>|<span data-ttu-id="a609b-359">1 </span><span class="sxs-lookup"><span data-stu-id="a609b-359">1</span></span>|<span data-ttu-id="a609b-360">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-360">✔</span></span>|<span data-ttu-id="a609b-361">Especifica si el conector ofrece una experiencia en el contexto de un canal en un `team`o una experiencia en el ámbito de un solo usuario individual (`personal`).</span><span class="sxs-lookup"><span data-stu-id="a609b-361">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a609b-362">Actualmente, solo se `team` admite el ámbito.</span><span class="sxs-lookup"><span data-stu-id="a609b-362">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="a609b-363">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="a609b-363">composeExtensions</span></span>

<span data-ttu-id="a609b-364">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a609b-364">**Optional**</span></span>

<span data-ttu-id="a609b-365">Define una extensión de mensajería para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-365">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="a609b-366">El nombre de la característica se cambió de "redactar extensión" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="a609b-366">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="a609b-367">El objeto es una matriz (un máximo de 1 elemento) con todos los elementos `object`de tipo.</span><span class="sxs-lookup"><span data-stu-id="a609b-367">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="a609b-368">Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a609b-368">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="a609b-369">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-369">Name</span></span>| <span data-ttu-id="a609b-370">Tipo</span><span class="sxs-lookup"><span data-stu-id="a609b-370">Type</span></span> | <span data-ttu-id="a609b-371">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-371">Maximum Size</span></span> | <span data-ttu-id="a609b-372">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-372">Required</span></span> | <span data-ttu-id="a609b-373">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-373">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a609b-374">String</span><span class="sxs-lookup"><span data-stu-id="a609b-374">String</span></span>|<span data-ttu-id="a609b-375">64</span><span class="sxs-lookup"><span data-stu-id="a609b-375">64</span></span>|<span data-ttu-id="a609b-376">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-376">✔</span></span>|<span data-ttu-id="a609b-377">IDENTIFICADOR único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, tal como se registró con bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a609b-377">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="a609b-378">Puede ser el mismo que el identificador de aplicación general.</span><span class="sxs-lookup"><span data-stu-id="a609b-378">This may well be the same as the overall App ID.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="a609b-379">Boolean</span><span class="sxs-lookup"><span data-stu-id="a609b-379">Boolean</span></span>|||<span data-ttu-id="a609b-380">Un valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a609b-380">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="a609b-381">El valor predeterminado `false`es.</span><span class="sxs-lookup"><span data-stu-id="a609b-381">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="a609b-382">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a609b-382">Array of object</span></span>|<span data-ttu-id="a609b-383">10 </span><span class="sxs-lookup"><span data-stu-id="a609b-383">10</span></span>|<span data-ttu-id="a609b-384">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-384">✔</span></span>|<span data-ttu-id="a609b-385">Matriz de comandos que admite la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="a609b-385">Array of commands the messaging extension supports</span></span>|
|`messageHandlers`|<span data-ttu-id="a609b-386">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a609b-386">Array of Objects</span></span>|<span data-ttu-id="a609b-387">5 </span><span class="sxs-lookup"><span data-stu-id="a609b-387">5</span></span>||<span data-ttu-id="a609b-388">Una lista de controladores que permiten invocar las aplicaciones cuando se cumplen ciertas condiciones.</span><span class="sxs-lookup"><span data-stu-id="a609b-388">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="a609b-389">Los dominios también deben aparecer en`validDomains`</span><span class="sxs-lookup"><span data-stu-id="a609b-389">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="a609b-390">String</span><span class="sxs-lookup"><span data-stu-id="a609b-390">String</span></span>|||<span data-ttu-id="a609b-391">El tipo de controlador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="a609b-391">The type of message handler.</span></span> <span data-ttu-id="a609b-392">Debe ser `"link"`.</span><span class="sxs-lookup"><span data-stu-id="a609b-392">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="a609b-393">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="a609b-393">Array of Strings</span></span>|||<span data-ttu-id="a609b-394">Matriz de dominios para los que el controlador de mensajes de vínculo puede registrarse.</span><span class="sxs-lookup"><span data-stu-id="a609b-394">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="a609b-395">composeExtensions. Commands</span><span class="sxs-lookup"><span data-stu-id="a609b-395">composeExtensions.commands</span></span>

<span data-ttu-id="a609b-396">La extensión de mensajería debe declarar uno o más comandos.</span><span class="sxs-lookup"><span data-stu-id="a609b-396">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="a609b-397">Cada comando aparece en Microsoft Teams como una posible interacción desde el punto de entrada basado en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="a609b-397">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="a609b-398">Hay un máximo de 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="a609b-398">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="a609b-399">Cada elemento de comando es un objeto con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="a609b-399">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="a609b-400">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-400">Name</span></span>| <span data-ttu-id="a609b-401">Tipo</span><span class="sxs-lookup"><span data-stu-id="a609b-401">Type</span></span>| <span data-ttu-id="a609b-402">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-402">Maximum size</span></span> | <span data-ttu-id="a609b-403">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-403">Required</span></span> | <span data-ttu-id="a609b-404">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-404">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="a609b-405">String</span><span class="sxs-lookup"><span data-stu-id="a609b-405">String</span></span>|<span data-ttu-id="a609b-406">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-406">64 characters</span></span>|<span data-ttu-id="a609b-407">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-407">✔</span></span>|<span data-ttu-id="a609b-408">Identificador del comando.</span><span class="sxs-lookup"><span data-stu-id="a609b-408">The ID for the command</span></span>|
|`type`|<span data-ttu-id="a609b-409">String</span><span class="sxs-lookup"><span data-stu-id="a609b-409">String</span></span>|<span data-ttu-id="a609b-410">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-410">64 characters</span></span>||<span data-ttu-id="a609b-411">Tipo del comando.</span><span class="sxs-lookup"><span data-stu-id="a609b-411">Type of the command.</span></span> <span data-ttu-id="a609b-412">Uno de `query` o `action`.</span><span class="sxs-lookup"><span data-stu-id="a609b-412">One of `query` or `action`.</span></span> <span data-ttu-id="a609b-413">Predeterminada`query`</span><span class="sxs-lookup"><span data-stu-id="a609b-413">Default: `query`</span></span>|
|`title`|<span data-ttu-id="a609b-414">String</span><span class="sxs-lookup"><span data-stu-id="a609b-414">String</span></span>|<span data-ttu-id="a609b-415">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-415">32 characters</span></span>|<span data-ttu-id="a609b-416">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-416">✔</span></span>|<span data-ttu-id="a609b-417">El nombre de comando descriptivo</span><span class="sxs-lookup"><span data-stu-id="a609b-417">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="a609b-418">String</span><span class="sxs-lookup"><span data-stu-id="a609b-418">String</span></span>|<span data-ttu-id="a609b-419">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-419">128 characters</span></span>||<span data-ttu-id="a609b-420">La descripción que se muestra a los usuarios para indicar el propósito de este comando</span><span class="sxs-lookup"><span data-stu-id="a609b-420">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="a609b-421">Boolean</span><span class="sxs-lookup"><span data-stu-id="a609b-421">Boolean</span></span>|||<span data-ttu-id="a609b-422">Un valor booleano que indica si el comando se debe ejecutar inicialmente sin ningún parámetro.</span><span class="sxs-lookup"><span data-stu-id="a609b-422">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="a609b-423">Predeterminada`false`</span><span class="sxs-lookup"><span data-stu-id="a609b-423">Default: `false`</span></span>|
|`context`|<span data-ttu-id="a609b-424">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="a609b-424">Array of Strings</span></span>|<span data-ttu-id="a609b-425">3 </span><span class="sxs-lookup"><span data-stu-id="a609b-425">3</span></span>||<span data-ttu-id="a609b-426">Define desde dónde se puede invocar la extensión de mensajes.</span><span class="sxs-lookup"><span data-stu-id="a609b-426">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="a609b-427">Cualquier combinación de `compose`, `commandBox`, `message`.</span><span class="sxs-lookup"><span data-stu-id="a609b-427">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="a609b-428">El valor predeterminado es`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="a609b-428">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="a609b-429">Boolean</span><span class="sxs-lookup"><span data-stu-id="a609b-429">Boolean</span></span>|||<span data-ttu-id="a609b-430">Un valor booleano que indica si debe recuperar el módulo de tareas de forma dinámica.</span><span class="sxs-lookup"><span data-stu-id="a609b-430">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="a609b-431">Objeto</span><span class="sxs-lookup"><span data-stu-id="a609b-431">Object</span></span>|||<span data-ttu-id="a609b-432">Especificar el módulo de tarea para cargar previamente cuando se usa un comando de extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="a609b-432">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="a609b-433">String</span><span class="sxs-lookup"><span data-stu-id="a609b-433">String</span></span>|<span data-ttu-id="a609b-434">64</span><span class="sxs-lookup"><span data-stu-id="a609b-434">64</span></span>||<span data-ttu-id="a609b-435">Título del cuadro de diálogo inicial</span><span class="sxs-lookup"><span data-stu-id="a609b-435">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="a609b-436">String</span><span class="sxs-lookup"><span data-stu-id="a609b-436">String</span></span>|||<span data-ttu-id="a609b-437">Ancho del cuadro de diálogo, ya sea un número en píxeles o un diseño predeterminado, como "Large", "Medium" o "Small"</span><span class="sxs-lookup"><span data-stu-id="a609b-437">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="a609b-438">String</span><span class="sxs-lookup"><span data-stu-id="a609b-438">String</span></span>|||<span data-ttu-id="a609b-439">Alto del cuadro de diálogo: número en píxeles o diseño predeterminado, como "Large", "Medium" o "Small"</span><span class="sxs-lookup"><span data-stu-id="a609b-439">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="a609b-440">String</span><span class="sxs-lookup"><span data-stu-id="a609b-440">String</span></span>|||<span data-ttu-id="a609b-441">Dirección URL de la WebView inicial</span><span class="sxs-lookup"><span data-stu-id="a609b-441">Initial webview URL</span></span>|
|`parameters`|<span data-ttu-id="a609b-442">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a609b-442">Array of object</span></span>|<span data-ttu-id="a609b-443">5 </span><span class="sxs-lookup"><span data-stu-id="a609b-443">5</span></span>|<span data-ttu-id="a609b-444">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-444">✔</span></span>|<span data-ttu-id="a609b-445">La lista de parámetros que toma el comando.</span><span class="sxs-lookup"><span data-stu-id="a609b-445">The list of parameters the command takes.</span></span> <span data-ttu-id="a609b-446">Mínimo: 1; máximo: 5</span><span class="sxs-lookup"><span data-stu-id="a609b-446">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="a609b-447">String</span><span class="sxs-lookup"><span data-stu-id="a609b-447">String</span></span>|<span data-ttu-id="a609b-448">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-448">64 characters</span></span>|<span data-ttu-id="a609b-449">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-449">✔</span></span>|<span data-ttu-id="a609b-450">El nombre del parámetro tal y como aparece en el cliente.</span><span class="sxs-lookup"><span data-stu-id="a609b-450">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="a609b-451">Se incluye en la solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="a609b-451">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="a609b-452">String</span><span class="sxs-lookup"><span data-stu-id="a609b-452">String</span></span>|<span data-ttu-id="a609b-453">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-453">32 characters</span></span>|<span data-ttu-id="a609b-454">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-454">✔</span></span>|<span data-ttu-id="a609b-455">Título descriptivo del parámetro.</span><span class="sxs-lookup"><span data-stu-id="a609b-455">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="a609b-456">String</span><span class="sxs-lookup"><span data-stu-id="a609b-456">String</span></span>|<span data-ttu-id="a609b-457">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-457">128 characters</span></span>||<span data-ttu-id="a609b-458">Cadena descriptiva que describe el propósito de este parámetro.</span><span class="sxs-lookup"><span data-stu-id="a609b-458">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="a609b-459">String</span><span class="sxs-lookup"><span data-stu-id="a609b-459">String</span></span>|<span data-ttu-id="a609b-460">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-460">128 characters</span></span>||<span data-ttu-id="a609b-461">Define el tipo de control que se muestra en un módulo `fetchTask: true`de tareas para.</span><span class="sxs-lookup"><span data-stu-id="a609b-461">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="a609b-462">Uno de `text`, `textarea`, `number`, `date` `time` `toggle`,,`choiceset`</span><span class="sxs-lookup"><span data-stu-id="a609b-462">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="a609b-463">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a609b-463">Array of Objects</span></span>|<span data-ttu-id="a609b-464">10 </span><span class="sxs-lookup"><span data-stu-id="a609b-464">10</span></span>||<span data-ttu-id="a609b-465">Las opciones de opción del `choiceset`.</span><span class="sxs-lookup"><span data-stu-id="a609b-465">The choice options for the `choiceset`.</span></span> <span data-ttu-id="a609b-466">Use solo cuando `parameter.inputType` sea`choiceset`</span><span class="sxs-lookup"><span data-stu-id="a609b-466">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="a609b-467">String</span><span class="sxs-lookup"><span data-stu-id="a609b-467">String</span></span>|<span data-ttu-id="a609b-468">128</span><span class="sxs-lookup"><span data-stu-id="a609b-468">128</span></span>||<span data-ttu-id="a609b-469">Título de la opción</span><span class="sxs-lookup"><span data-stu-id="a609b-469">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="a609b-470">String</span><span class="sxs-lookup"><span data-stu-id="a609b-470">String</span></span>|<span data-ttu-id="a609b-471">512</span><span class="sxs-lookup"><span data-stu-id="a609b-471">512</span></span>||<span data-ttu-id="a609b-472">Valor de la opción</span><span class="sxs-lookup"><span data-stu-id="a609b-472">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="a609b-473">permissions</span><span class="sxs-lookup"><span data-stu-id="a609b-473">permissions</span></span>

<span data-ttu-id="a609b-474">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a609b-474">**Optional**</span></span>

<span data-ttu-id="a609b-475">Una matriz de `string` que especifica los permisos que solicita la aplicación, lo que permite a los usuarios finales saber cómo se realizará la extensión.</span><span class="sxs-lookup"><span data-stu-id="a609b-475">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="a609b-476">Las siguientes opciones no son exclusivas:</span><span class="sxs-lookup"><span data-stu-id="a609b-476">The following options are non-exclusive:</span></span>

* <span data-ttu-id="a609b-477">`identity`&emsp; Requiere información de identidad del usuario</span><span class="sxs-lookup"><span data-stu-id="a609b-477">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="a609b-478">`messageTeamMembers`&emsp; Requiere permiso para enviar mensajes directos a los miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="a609b-478">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="a609b-479">Cambiar estos permisos al actualizar la aplicación hará que los usuarios repitan el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="a609b-479">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="a609b-480">Consulte [actualizar la aplicación](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a609b-480">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="a609b-481">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="a609b-481">devicePermissions</span></span>

<span data-ttu-id="a609b-482">**Opcional** Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="a609b-482">**Optional** Array of Strings</span></span>

<span data-ttu-id="a609b-483">Especifica las características nativas del dispositivo de un usuario al que la aplicación puede solicitar acceso.</span><span class="sxs-lookup"><span data-stu-id="a609b-483">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="a609b-484">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="a609b-484">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="a609b-485">validDomains</span><span class="sxs-lookup"><span data-stu-id="a609b-485">validDomains</span></span>

<span data-ttu-id="a609b-486">**Opcional**, excepto **obligatorio** donde se indica</span><span class="sxs-lookup"><span data-stu-id="a609b-486">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="a609b-487">Una lista de dominios válidos para los sitios web que la aplicación espera que se carguen dentro del cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="a609b-487">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="a609b-488">Las listas de dominios pueden incluir caracteres comodín, por `*.example.com`ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a609b-488">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="a609b-489">Esto coincide exactamente con un segmento del dominio; Si tiene que hacer coincidir `a.b.example.com` , `*.*.example.com`use.</span><span class="sxs-lookup"><span data-stu-id="a609b-489">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="a609b-490">Si la configuración de la pestaña o la interfaz de usuario de contenido debe navegar a cualquier otro dominio además del uso de la configuración de pestañas, dicho dominio debe especificarse aquí.</span><span class="sxs-lookup"><span data-stu-id="a609b-490">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="a609b-491">No obstante, **no** es necesario incluir los dominios de los proveedores de identidades que desea admitir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-491">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="a609b-492">Por ejemplo, para autenticarse con un identificador de Google, es necesario redirigir a accounts.google.com, pero no se debe incluir accounts.google.com en `validDomains[]`.</span><span class="sxs-lookup"><span data-stu-id="a609b-492">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="a609b-493">Las aplicaciones de Microsoft teams que requieren sus propias direcciones URL de SharePoint para que funcionen correctamente pueden incluir "{teamsitedomain}" en su lista de dominios válidos.</span><span class="sxs-lookup"><span data-stu-id="a609b-493">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a609b-494">No agregue dominios que estén fuera de su control, ya sea directamente o mediante caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="a609b-494">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="a609b-495">Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="a609b-495">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="a609b-496">El objeto es una matriz con todos los elementos del tipo `string`.</span><span class="sxs-lookup"><span data-stu-id="a609b-496">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="a609b-497">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="a609b-497">webApplicationInfo</span></span>

<span data-ttu-id="a609b-498">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a609b-498">**Optional**</span></span>

<span data-ttu-id="a609b-499">Especifique la información del grafo y el identificador de la aplicación de AAD para ayudar a los usuarios a iniciar sesión sin problemas en su aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="a609b-499">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="a609b-500">Nombre</span><span class="sxs-lookup"><span data-stu-id="a609b-500">Name</span></span>| <span data-ttu-id="a609b-501">Tipo</span><span class="sxs-lookup"><span data-stu-id="a609b-501">Type</span></span>| <span data-ttu-id="a609b-502">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a609b-502">Maximum size</span></span> | <span data-ttu-id="a609b-503">Necesario</span><span class="sxs-lookup"><span data-stu-id="a609b-503">Required</span></span> | <span data-ttu-id="a609b-504">Descripción</span><span class="sxs-lookup"><span data-stu-id="a609b-504">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="a609b-505">String</span><span class="sxs-lookup"><span data-stu-id="a609b-505">String</span></span>|<span data-ttu-id="a609b-506">36 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-506">36 characters</span></span>|<span data-ttu-id="a609b-507">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-507">✔</span></span>|<span data-ttu-id="a609b-508">Identificador de la aplicación de AAD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a609b-508">AAD application id of the app.</span></span> <span data-ttu-id="a609b-509">Este identificador debe ser un GUID.</span><span class="sxs-lookup"><span data-stu-id="a609b-509">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="a609b-510">String</span><span class="sxs-lookup"><span data-stu-id="a609b-510">String</span></span>|<span data-ttu-id="a609b-511">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a609b-511">2048 characters</span></span>|<span data-ttu-id="a609b-512">✔</span><span class="sxs-lookup"><span data-stu-id="a609b-512">✔</span></span>|<span data-ttu-id="a609b-513">Dirección URL de recurso de la aplicación para adquirir el token de autenticación para el SSO.</span><span class="sxs-lookup"><span data-stu-id="a609b-513">Resource url of app for acquiring auth token for SSO.</span></span>|
