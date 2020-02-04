---
title: Referencia del esquema del manifiesto de vista previa para desarrolladores
description: Describe el esquema admitido por el manifiesto para Microsoft Teams.
keywords: Vista previa para desarrolladores de esquema de manifiesto de Teams
ms.date: 05/20/2019
ms.openlocfilehash: b99e1ae99b7fd1edd4c695f43f3ac25270f0c710
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675733"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="a9c5f-104">Esquema del manifiesto de vista previa para desarrolladores de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a9c5f-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="a9c5f-105">Consulte la [vista previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md) para obtener información sobre el programa y cómo puede unirse.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="a9c5f-106">Si no usa la vista previa para desarrolladores, no debe usar esta versión del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="a9c5f-107">Consulte [Reference: manifest Schema for Microsoft Teams](~/resources/schema/manifest-schema.md) para obtener la versión pública del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="a9c5f-108">El manifiesto de Microsoft Teams describe cómo se integra la aplicación en el producto de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="a9c5f-109">El manifiesto debe cumplir el esquema hospedado en [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span><span class="sxs-lookup"><span data-stu-id="a9c5f-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="a9c5f-110">Para obtener más información sobre las características disponibles, consulte: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span><span class="sxs-lookup"><span data-stu-id="a9c5f-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="a9c5f-111">Manifiesto completo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-111">Sample full manifest</span></span>

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "devPreview",
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
    "defaultLanguageTag": "es-es",
    "additionalLanguages": [
      {
        "languageTag": "en-us",
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
        },
        {
          "id": "exampleMessageHandler",
          "title": "Message Handler",
          "description": "Domains that will create a preview when pasted into the compose box",
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
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers",
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ]
}
```

<span data-ttu-id="a9c5f-112">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="a9c5f-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="a9c5f-113">$schema</span><span class="sxs-lookup"><span data-stu-id="a9c5f-113">$schema</span></span>

<span data-ttu-id="a9c5f-114">*Opcional, pero* &ndash; la cadena recomendada</span><span class="sxs-lookup"><span data-stu-id="a9c5f-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="a9c5f-115">La dirección URL de https://que hace referencia al esquema JSON del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="a9c5f-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="a9c5f-116">manifestVersion</span></span>

<span data-ttu-id="a9c5f-117">String **requerida** &ndash;</span><span class="sxs-lookup"><span data-stu-id="a9c5f-117">**Required** &ndash; String</span></span>

<span data-ttu-id="a9c5f-118">La versión del esquema del manifiesto que está usando este manifiesto.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="a9c5f-119">Debe ser "devPreview".</span><span class="sxs-lookup"><span data-stu-id="a9c5f-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="a9c5f-120">version</span><span class="sxs-lookup"><span data-stu-id="a9c5f-120">version</span></span>

<span data-ttu-id="a9c5f-121">String **requerida** &ndash;</span><span class="sxs-lookup"><span data-stu-id="a9c5f-121">**Required** &ndash; String</span></span>

<span data-ttu-id="a9c5f-122">La versión de la aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-122">The version of the specific app.</span></span> <span data-ttu-id="a9c5f-123">Si actualiza algo en el manifiesto, la versión también debe incrementarse.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="a9c5f-124">De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="a9c5f-125">Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y a validarse.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="a9c5f-126">A continuación, los usuarios de esta aplicación recibirán el nuevo manifiesto actualizado automáticamente en unas pocas horas, después de que se apruebe.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="a9c5f-127">Si la aplicación ha solicitado un cambio de permisos, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="a9c5f-128">Esta cadena de versión debe seguir el estándar [SemVer](http://semver.org/) (Major. Secundaria. REVISIÓN).</span><span class="sxs-lookup"><span data-stu-id="a9c5f-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="a9c5f-129">id</span><span class="sxs-lookup"><span data-stu-id="a9c5f-129">id</span></span>

<span data-ttu-id="a9c5f-130">Identificador de aplicación de Microsoft **necesario** &ndash;</span><span class="sxs-lookup"><span data-stu-id="a9c5f-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="a9c5f-131">El identificador único generado por Microsoft para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="a9c5f-132">Si ha registrado un bot a través de Microsoft bot Framework o la aplicación Web de su pestaña ya inicia sesión en Microsoft, debe tener ya un identificador y escribirlo aquí.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="a9c5f-133">De lo contrario, debe generar un nuevo identificador en el portal de registro de aplicaciones de Microsoft ([mis aplicaciones](https://apps.dev.microsoft.com)), escribirlo aquí y volver a usarlo cuando [agregue un bot](~/bots/how-to/create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="a9c5f-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="a9c5f-134">packageName</span><span class="sxs-lookup"><span data-stu-id="a9c5f-134">packageName</span></span>

<span data-ttu-id="a9c5f-135">String **requerida** &ndash;</span><span class="sxs-lookup"><span data-stu-id="a9c5f-135">**Required** &ndash; String</span></span>

<span data-ttu-id="a9c5f-136">Un identificador único para esta aplicación en la notación de dominio inverso; por ejemplo, com. example. myapp.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="a9c5f-137">developer</span><span class="sxs-lookup"><span data-stu-id="a9c5f-137">developer</span></span>

<span data-ttu-id="a9c5f-138">**Required**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-138">**Required**</span></span>

<span data-ttu-id="a9c5f-139">Especifica información sobre la compañía.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-139">Specifies information about your company.</span></span> <span data-ttu-id="a9c5f-140">Para las aplicaciones enviadas a AppSource (anteriormente tienda Office), estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="a9c5f-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-141">Name</span></span>| <span data-ttu-id="a9c5f-142">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-142">Maximum size</span></span> | <span data-ttu-id="a9c5f-143">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-143">Required</span></span> | <span data-ttu-id="a9c5f-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="a9c5f-145">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-145">32 characters</span></span>|<span data-ttu-id="a9c5f-146">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-146">✔</span></span>|<span data-ttu-id="a9c5f-147">El nombre para mostrar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="a9c5f-148">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-148">2048 characters</span></span>|<span data-ttu-id="a9c5f-149">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-149">✔</span></span>|<span data-ttu-id="a9c5f-150">La dirección URL https://al sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="a9c5f-151">Este vínculo debe llevar a los usuarios a su compañía o a la página de aterrizaje específica del producto.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="a9c5f-152">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-152">2048 characters</span></span>|<span data-ttu-id="a9c5f-153">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-153">✔</span></span>|<span data-ttu-id="a9c5f-154">La dirección URL de https://a la Directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="a9c5f-155">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-155">2048 characters</span></span>|<span data-ttu-id="a9c5f-156">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-156">✔</span></span>|<span data-ttu-id="a9c5f-157">La dirección URL de https://a las condiciones de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="a9c5f-158">10 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-158">10 characters</span></span>|<span data-ttu-id="a9c5f-159">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-159">✔</span></span>|<span data-ttu-id="a9c5f-160">**Opcional** IDENTIFICADOR de red de los socios de Microsoft que identifica la organización asociada que crea la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="a9c5f-161">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-161">localizationInfo</span></span>

<span data-ttu-id="a9c5f-162">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-162">**Optional**</span></span>

<span data-ttu-id="a9c5f-163">Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="a9c5f-164">Consulte [localización](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="a9c5f-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="a9c5f-165">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-165">Name</span></span>| <span data-ttu-id="a9c5f-166">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-166">Maximum size</span></span> | <span data-ttu-id="a9c5f-167">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-167">Required</span></span> | <span data-ttu-id="a9c5f-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="a9c5f-169">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-169">4 characters</span></span>|<span data-ttu-id="a9c5f-170">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-170">✔</span></span>|<span data-ttu-id="a9c5f-171">La etiqueta de idioma de las cadenas en este archivo de manifiesto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="a9c5f-172">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="a9c5f-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="a9c5f-173">Una matriz de objetos que especifica traducciones de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="a9c5f-174">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-174">Name</span></span>| <span data-ttu-id="a9c5f-175">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-175">Maximum size</span></span> | <span data-ttu-id="a9c5f-176">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-176">Required</span></span> | <span data-ttu-id="a9c5f-177">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="a9c5f-178">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-178">4 characters</span></span>|<span data-ttu-id="a9c5f-179">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-179">✔</span></span>|<span data-ttu-id="a9c5f-180">La etiqueta de idioma de las cadenas en el archivo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="a9c5f-181">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-181">4 characters</span></span>|<span data-ttu-id="a9c5f-182">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-182">✔</span></span>|<span data-ttu-id="a9c5f-183">Una ruta de acceso relativa a un archivo. JSON que contiene las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="a9c5f-184">name</span><span class="sxs-lookup"><span data-stu-id="a9c5f-184">name</span></span>

<span data-ttu-id="a9c5f-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-185">**Required**</span></span>

<span data-ttu-id="a9c5f-186">El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="a9c5f-187">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="a9c5f-188">Los valores de `short` y `full` no deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="a9c5f-189">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-189">Name</span></span>| <span data-ttu-id="a9c5f-190">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-190">Maximum size</span></span> | <span data-ttu-id="a9c5f-191">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-191">Required</span></span> | <span data-ttu-id="a9c5f-192">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="a9c5f-193">30 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-193">30 characters</span></span>|<span data-ttu-id="a9c5f-194">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-194">✔</span></span>|<span data-ttu-id="a9c5f-195">El nombre para mostrar corto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="a9c5f-196">100 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-196">100 characters</span></span>||<span data-ttu-id="a9c5f-197">El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="a9c5f-198">description</span><span class="sxs-lookup"><span data-stu-id="a9c5f-198">description</span></span>

<span data-ttu-id="a9c5f-199">**Required**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-199">**Required**</span></span>

<span data-ttu-id="a9c5f-200">Describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-200">Describes your app to users.</span></span> <span data-ttu-id="a9c5f-201">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="a9c5f-202">Asegúrese de que la descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="a9c5f-203">También debe tener en cuenta, en la descripción completa, si se requiere uso de una cuenta externa.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="a9c5f-204">Los valores de `short` y `full` no deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="a9c5f-205">La descripción breve no debe repetirse en la descripción larga y no debe incluir ningún otro nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="a9c5f-206">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-206">Name</span></span>| <span data-ttu-id="a9c5f-207">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-207">Maximum size</span></span> | <span data-ttu-id="a9c5f-208">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-208">Required</span></span> | <span data-ttu-id="a9c5f-209">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="a9c5f-210">80 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-210">80 characters</span></span>|<span data-ttu-id="a9c5f-211">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-211">✔</span></span>|<span data-ttu-id="a9c5f-212">Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="a9c5f-213">4000 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-213">4000 characters</span></span>|<span data-ttu-id="a9c5f-214">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-214">✔</span></span>|<span data-ttu-id="a9c5f-215">La descripción completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="a9c5f-216">iconos</span><span class="sxs-lookup"><span data-stu-id="a9c5f-216">icons</span></span>

<span data-ttu-id="a9c5f-217">**Required**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-217">**Required**</span></span>

<span data-ttu-id="a9c5f-218">Iconos usados en la aplicación Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-218">Icons used within the Teams app.</span></span> <span data-ttu-id="a9c5f-219">Los archivos de icono deben incluirse como parte del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="a9c5f-220">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-220">Name</span></span>| <span data-ttu-id="a9c5f-221">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-221">Maximum size</span></span> | <span data-ttu-id="a9c5f-222">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-222">Required</span></span> | <span data-ttu-id="a9c5f-223">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="a9c5f-224">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-224">2048 characters</span></span>|<span data-ttu-id="a9c5f-225">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-225">✔</span></span>|<span data-ttu-id="a9c5f-226">Una ruta de acceso relativa a un icono de esquema PNG transparente de 32x32.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="a9c5f-227">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-227">2048 characters</span></span>|<span data-ttu-id="a9c5f-228">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-228">✔</span></span>|<span data-ttu-id="a9c5f-229">Una ruta de acceso de archivo relativa a un icono PNG 192x192 de color completo.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="a9c5f-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="a9c5f-230">accentColor</span></span>

<span data-ttu-id="a9c5f-231">String **requerida** &ndash;</span><span class="sxs-lookup"><span data-stu-id="a9c5f-231">**Required** &ndash; String</span></span>

<span data-ttu-id="a9c5f-232">Color que se va a usar junto con y como fondo de los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="a9c5f-233">El valor debe ser un código de color HTML válido que empiece por ' # ', `#4464ee`por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="a9c5f-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="a9c5f-234">configurableTabs</span></span>

<span data-ttu-id="a9c5f-235">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-235">**Optional**</span></span>

<span data-ttu-id="a9c5f-236">Se usa cuando la experiencia de la aplicación tiene una experiencia de la pestaña de canal de equipo que requiere una configuración adicional antes de que se agregue.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="a9c5f-237">Las pestañas configurables solo se admiten en el ámbito de Teams y actualmente solo se admite una pestaña por aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="a9c5f-238">El objeto es una matriz con todos los elementos del tipo `object`.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="a9c5f-239">Este bloque solo es necesario para las soluciones que proporcionan una solución de ficha de canal configurable.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="a9c5f-240">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-240">Name</span></span>| <span data-ttu-id="a9c5f-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-241">Type</span></span>| <span data-ttu-id="a9c5f-242">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-242">Maximum size</span></span> | <span data-ttu-id="a9c5f-243">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-243">Required</span></span> | <span data-ttu-id="a9c5f-244">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="a9c5f-245">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-245">String</span></span>|<span data-ttu-id="a9c5f-246">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-246">2048 characters</span></span>|<span data-ttu-id="a9c5f-247">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-247">✔</span></span>|<span data-ttu-id="a9c5f-248">Dirección URL de https://que se va a usar al configurar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="a9c5f-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="a9c5f-249">Boolean</span></span>|||<span data-ttu-id="a9c5f-250">Un valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de crearla.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="a9c5f-251">Predeterminada`true`</span><span class="sxs-lookup"><span data-stu-id="a9c5f-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="a9c5f-252">Matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a9c5f-252">Array of enum</span></span>|<span data-ttu-id="a9c5f-253">1 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-253">1</span></span>|<span data-ttu-id="a9c5f-254">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-254">✔</span></span>|<span data-ttu-id="a9c5f-255">Actualmente, las pestañas configurables solo admiten los `team` ámbitos y `groupchat` .</span><span class="sxs-lookup"><span data-stu-id="a9c5f-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="a9c5f-256">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-256">String</span></span>|<span data-ttu-id="a9c5f-257">2048</span><span class="sxs-lookup"><span data-stu-id="a9c5f-257">2048</span></span>||<span data-ttu-id="a9c5f-258">Una ruta de acceso de archivo relativa a una imagen de vista previa de pestaña para su uso en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="a9c5f-259">Tamaño 1024x768.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="a9c5f-260">Matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a9c5f-260">Array of enum</span></span>|<span data-ttu-id="a9c5f-261">1 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-261">1</span></span>||<span data-ttu-id="a9c5f-262">Define cómo estará disponible la pestaña en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="a9c5f-263">Las opciones `sharePointFullPage` son y`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="a9c5f-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="a9c5f-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="a9c5f-264">staticTabs</span></span>

<span data-ttu-id="a9c5f-265">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-265">**Optional**</span></span>

<span data-ttu-id="a9c5f-266">Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="a9c5f-267">Las pestañas estáticas declaradas en `personal` el ámbito siempre están ancladas a la experiencia personal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="a9c5f-268">Actualmente no se admiten `team` las pestañas estáticas declaradas en el ámbito.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="a9c5f-269">El objeto es una matriz (un máximo de 16 elementos) con todos los elementos del `object`tipo.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="a9c5f-270">Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña estática.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="a9c5f-271">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-271">Name</span></span>| <span data-ttu-id="a9c5f-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-272">Type</span></span>| <span data-ttu-id="a9c5f-273">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-273">Maximum size</span></span> | <span data-ttu-id="a9c5f-274">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-274">Required</span></span> | <span data-ttu-id="a9c5f-275">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="a9c5f-276">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-276">String</span></span>|<span data-ttu-id="a9c5f-277">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-277">64 characters</span></span>|<span data-ttu-id="a9c5f-278">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-278">✔</span></span>|<span data-ttu-id="a9c5f-279">Un identificador único para la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="a9c5f-280">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-280">String</span></span>|<span data-ttu-id="a9c5f-281">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-281">128 characters</span></span>|<span data-ttu-id="a9c5f-282">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-282">✔</span></span>|<span data-ttu-id="a9c5f-283">El nombre para mostrar de la pestaña en la interfaz de canal.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="a9c5f-284">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-284">String</span></span>|<span data-ttu-id="a9c5f-285">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-285">2048 characters</span></span>|<span data-ttu-id="a9c5f-286">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-286">✔</span></span>|<span data-ttu-id="a9c5f-287">Dirección URL de https://que señala a la interfaz de usuario de la entidad que se va a mostrar en el lienzo de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="a9c5f-288">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-288">String</span></span>|<span data-ttu-id="a9c5f-289">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-289">2048 characters</span></span>||<span data-ttu-id="a9c5f-290">La dirección URL de https://para apuntar a si un usuario opta por verlo en un explorador.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="a9c5f-291">Matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a9c5f-291">Array of enum</span></span>|<span data-ttu-id="a9c5f-292">1 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-292">1</span></span>|<span data-ttu-id="a9c5f-293">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-293">✔</span></span>|<span data-ttu-id="a9c5f-294">Actualmente, las pestañas estáticas `personal` solo admiten el ámbito, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="a9c5f-295">transferido</span><span class="sxs-lookup"><span data-stu-id="a9c5f-295">bots</span></span>

<span data-ttu-id="a9c5f-296">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-296">**Optional**</span></span>

<span data-ttu-id="a9c5f-297">Define una solución de bot, junto con información opcional como propiedades de comando predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="a9c5f-298">El objeto es una matriz (un máximo de solo 1&mdash;elemento solo es posible para cada aplicación) con todos los elementos del tipo `object`.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="a9c5f-299">Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="a9c5f-300">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-300">Name</span></span>| <span data-ttu-id="a9c5f-301">Tipo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-301">Type</span></span>| <span data-ttu-id="a9c5f-302">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-302">Maximum size</span></span> | <span data-ttu-id="a9c5f-303">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-303">Required</span></span> | <span data-ttu-id="a9c5f-304">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a9c5f-305">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-305">String</span></span>|<span data-ttu-id="a9c5f-306">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-306">64 characters</span></span>|<span data-ttu-id="a9c5f-307">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-307">✔</span></span>|<span data-ttu-id="a9c5f-308">IDENTIFICADOR único de la aplicación de Microsoft para el bot como se registra con bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="a9c5f-309">Puede ser el mismo que el [identificador de aplicación](#id)general.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="a9c5f-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="a9c5f-310">Boolean</span></span>|||<span data-ttu-id="a9c5f-311">Describe si el bot utiliza o no una sugerencia del usuario para agregar el bot a un canal específico.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="a9c5f-312">Predeterminada`false`</span><span class="sxs-lookup"><span data-stu-id="a9c5f-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="a9c5f-313">Boolean</span><span class="sxs-lookup"><span data-stu-id="a9c5f-313">Boolean</span></span>|||<span data-ttu-id="a9c5f-314">Indica si un bot es un bot? a de solo notificaciones unidireccional, a diferencia de un bot? a de la conversación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="a9c5f-315">Predeterminada`false`</span><span class="sxs-lookup"><span data-stu-id="a9c5f-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="a9c5f-316">Boolean</span><span class="sxs-lookup"><span data-stu-id="a9c5f-316">Boolean</span></span>|||<span data-ttu-id="a9c5f-317">Indica si el bot admite la capacidad de cargar o descargar archivos en un chat personal.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="a9c5f-318">Predeterminada`false`</span><span class="sxs-lookup"><span data-stu-id="a9c5f-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="a9c5f-319">Matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a9c5f-319">Array of enum</span></span>|<span data-ttu-id="a9c5f-320">3 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-320">3</span></span>|<span data-ttu-id="a9c5f-321">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-321">✔</span></span>|<span data-ttu-id="a9c5f-322">Especifica si bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat en grupo (`groupchat`) o una experiencia en un ámbito específico de un solo usuario (`personal`).</span><span class="sxs-lookup"><span data-stu-id="a9c5f-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a9c5f-323">Estas opciones no son exclusivas.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="a9c5f-324">bots. commandLists</span><span class="sxs-lookup"><span data-stu-id="a9c5f-324">bots.commandLists</span></span>

<span data-ttu-id="a9c5f-325">Una lista opcional de comandos que el bot puede recomendar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="a9c5f-326">El objeto es una matriz (un máximo de 2 elementos) con todos los elementos `object`de tipo; debe definir una lista de comandos independiente para cada ámbito que admita el bot.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="a9c5f-327">Consulte [menús de bot](~/bots/how-to/create-a-bot-commands-menu.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-327">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="a9c5f-328">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-328">Name</span></span>| <span data-ttu-id="a9c5f-329">Tipo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-329">Type</span></span>| <span data-ttu-id="a9c5f-330">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-330">Maximum size</span></span> | <span data-ttu-id="a9c5f-331">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-331">Required</span></span> | <span data-ttu-id="a9c5f-332">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="a9c5f-333">matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a9c5f-333">array of enum</span></span>|<span data-ttu-id="a9c5f-334">3 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-334">3</span></span>|<span data-ttu-id="a9c5f-335">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-335">✔</span></span>|<span data-ttu-id="a9c5f-336">Especifica el ámbito para el que es válida la lista de comandos.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="a9c5f-337">Las opciones `team`son `personal`, y `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="a9c5f-338">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a9c5f-338">array of objects</span></span>|<span data-ttu-id="a9c5f-339">10 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-339">10</span></span>|<span data-ttu-id="a9c5f-340">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-340">✔</span></span>|<span data-ttu-id="a9c5f-341">Una matriz de comandos que el bot admite:</span><span class="sxs-lookup"><span data-stu-id="a9c5f-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="a9c5f-342">`title`: el nombre del comando Bot (cadena, 32)</span><span class="sxs-lookup"><span data-stu-id="a9c5f-342">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="a9c5f-343">`description`: una descripción sencilla o un ejemplo de la sintaxis del comando y su argumento (String, 128)</span><span class="sxs-lookup"><span data-stu-id="a9c5f-343">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="a9c5f-344">Connector</span><span class="sxs-lookup"><span data-stu-id="a9c5f-344">connectors</span></span>

<span data-ttu-id="a9c5f-345">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-345">**Optional**</span></span>

<span data-ttu-id="a9c5f-346">El `connectors` bloque define un conector de Office 365 para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="a9c5f-347">El objeto es una matriz (un máximo de 1 elemento) con todos los elementos `object`de tipo.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="a9c5f-348">Este bloque solo es necesario para las soluciones que proporcionan un conector.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="a9c5f-349">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-349">Name</span></span>| <span data-ttu-id="a9c5f-350">Tipo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-350">Type</span></span>| <span data-ttu-id="a9c5f-351">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-351">Maximum size</span></span> | <span data-ttu-id="a9c5f-352">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-352">Required</span></span> | <span data-ttu-id="a9c5f-353">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="a9c5f-354">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-354">String</span></span>|<span data-ttu-id="a9c5f-355">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-355">2048 characters</span></span>|<span data-ttu-id="a9c5f-356">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-356">✔</span></span>|<span data-ttu-id="a9c5f-357">Dirección URL de https://que se va a usar al configurar el conector.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="a9c5f-358">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-358">String</span></span>|<span data-ttu-id="a9c5f-359">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-359">64 characters</span></span>|<span data-ttu-id="a9c5f-360">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-360">✔</span></span>|<span data-ttu-id="a9c5f-361">Un identificador único para el conector que coincide con su identificador en el [panel del programador de conectores](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="a9c5f-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="a9c5f-362">Matriz de enum</span><span class="sxs-lookup"><span data-stu-id="a9c5f-362">Array of enum</span></span>|<span data-ttu-id="a9c5f-363">1 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-363">1</span></span>|<span data-ttu-id="a9c5f-364">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-364">✔</span></span>|<span data-ttu-id="a9c5f-365">Especifica si el conector ofrece una experiencia en el contexto de un canal en un `team`o una experiencia en el ámbito de un solo usuario individual (`personal`).</span><span class="sxs-lookup"><span data-stu-id="a9c5f-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a9c5f-366">Actualmente, solo se `team` admite el ámbito.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="a9c5f-367">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="a9c5f-367">composeExtensions</span></span>

<span data-ttu-id="a9c5f-368">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-368">**Optional**</span></span>

<span data-ttu-id="a9c5f-369">Define una extensión de mensajería para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="a9c5f-370">El nombre de la característica se cambió de "redactar extensión" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="a9c5f-371">El objeto es una matriz (un máximo de 1 elemento) con todos los elementos `object`de tipo.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="a9c5f-372">Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="a9c5f-373">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-373">Name</span></span>| <span data-ttu-id="a9c5f-374">Tipo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-374">Type</span></span> | <span data-ttu-id="a9c5f-375">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-375">Maximum Size</span></span> | <span data-ttu-id="a9c5f-376">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-376">Required</span></span> | <span data-ttu-id="a9c5f-377">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a9c5f-378">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-378">String</span></span>|<span data-ttu-id="a9c5f-379">64</span><span class="sxs-lookup"><span data-stu-id="a9c5f-379">64</span></span>|<span data-ttu-id="a9c5f-380">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-380">✔</span></span>|<span data-ttu-id="a9c5f-381">IDENTIFICADOR único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, tal como se registró con bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="a9c5f-382">Puede ser el mismo que el [identificador de aplicación](#id)general.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="a9c5f-383">Boolean</span><span class="sxs-lookup"><span data-stu-id="a9c5f-383">Boolean</span></span>|||<span data-ttu-id="a9c5f-384">Un valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="a9c5f-385">El valor predeterminado `false`es.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="a9c5f-386">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a9c5f-386">Array of object</span></span>|<span data-ttu-id="a9c5f-387">10 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-387">10</span></span>|<span data-ttu-id="a9c5f-388">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-388">✔</span></span>|<span data-ttu-id="a9c5f-389">Matriz de comandos que admite la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="a9c5f-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="a9c5f-390">composeExtensions. Commands</span><span class="sxs-lookup"><span data-stu-id="a9c5f-390">composeExtensions.commands</span></span>

<span data-ttu-id="a9c5f-391">La extensión de mensajería debe declarar uno o más comandos.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="a9c5f-392">Cada comando aparece en Microsoft Teams como una posible interacción desde el punto de entrada basado en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="a9c5f-393">Hay un máximo de 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="a9c5f-394">Cada elemento de comando es un objeto con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="a9c5f-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="a9c5f-395">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-395">Name</span></span>| <span data-ttu-id="a9c5f-396">Tipo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-396">Type</span></span>| <span data-ttu-id="a9c5f-397">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-397">Maximum size</span></span> | <span data-ttu-id="a9c5f-398">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-398">Required</span></span> | <span data-ttu-id="a9c5f-399">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="a9c5f-400">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-400">String</span></span>|<span data-ttu-id="a9c5f-401">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-401">64 characters</span></span>|<span data-ttu-id="a9c5f-402">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-402">✔</span></span>|<span data-ttu-id="a9c5f-403">Identificador del comando.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-403">The ID for the command</span></span>|
|`type`|<span data-ttu-id="a9c5f-404">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-404">String</span></span>|<span data-ttu-id="a9c5f-405">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-405">64 characters</span></span>||<span data-ttu-id="a9c5f-406">Tipo del comando.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-406">Type of the command.</span></span> <span data-ttu-id="a9c5f-407">Uno de `query` o `action`.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-407">One of `query` or `action`.</span></span> <span data-ttu-id="a9c5f-408">Predeterminada`query`</span><span class="sxs-lookup"><span data-stu-id="a9c5f-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="a9c5f-409">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-409">String</span></span>|<span data-ttu-id="a9c5f-410">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-410">32 characters</span></span>|<span data-ttu-id="a9c5f-411">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-411">✔</span></span>|<span data-ttu-id="a9c5f-412">El nombre de comando descriptivo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-412">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="a9c5f-413">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-413">String</span></span>|<span data-ttu-id="a9c5f-414">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-414">128 characters</span></span>||<span data-ttu-id="a9c5f-415">La descripción que se muestra a los usuarios para indicar el propósito de este comando</span><span class="sxs-lookup"><span data-stu-id="a9c5f-415">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="a9c5f-416">Boolean</span><span class="sxs-lookup"><span data-stu-id="a9c5f-416">Boolean</span></span>|||<span data-ttu-id="a9c5f-417">Un valor booleano que indica si el comando se debe ejecutar inicialmente sin ningún parámetro.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="a9c5f-418">Predeterminada`false`</span><span class="sxs-lookup"><span data-stu-id="a9c5f-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="a9c5f-419">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="a9c5f-419">Array of Strings</span></span>|<span data-ttu-id="a9c5f-420">3 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-420">3</span></span>||<span data-ttu-id="a9c5f-421">Define desde dónde se puede invocar la extensión de mensajes.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="a9c5f-422">Cualquier combinación de `compose`, `commandBox`, `message`.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="a9c5f-423">El valor predeterminado es`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="a9c5f-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="a9c5f-424">Boolean</span><span class="sxs-lookup"><span data-stu-id="a9c5f-424">Boolean</span></span>|||<span data-ttu-id="a9c5f-425">Un valor booleano que indica si debe recuperar el módulo de tareas de forma dinámica.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-425">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="a9c5f-426">Objeto</span><span class="sxs-lookup"><span data-stu-id="a9c5f-426">Object</span></span>|||<span data-ttu-id="a9c5f-427">Especificar el módulo de tarea para cargar previamente cuando se usa un comando de extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="a9c5f-427">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="a9c5f-428">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-428">String</span></span>|<span data-ttu-id="a9c5f-429">64</span><span class="sxs-lookup"><span data-stu-id="a9c5f-429">64</span></span>||<span data-ttu-id="a9c5f-430">Título del cuadro de diálogo inicial</span><span class="sxs-lookup"><span data-stu-id="a9c5f-430">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="a9c5f-431">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-431">String</span></span>|||<span data-ttu-id="a9c5f-432">Ancho del cuadro de diálogo, ya sea un número en píxeles o un diseño predeterminado, como "Large", "Medium" o "Small"</span><span class="sxs-lookup"><span data-stu-id="a9c5f-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="a9c5f-433">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-433">String</span></span>|||<span data-ttu-id="a9c5f-434">Alto del cuadro de diálogo: número en píxeles o diseño predeterminado, como "Large", "Medium" o "Small"</span><span class="sxs-lookup"><span data-stu-id="a9c5f-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="a9c5f-435">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-435">String</span></span>|||<span data-ttu-id="a9c5f-436">Dirección URL de la WebView inicial</span><span class="sxs-lookup"><span data-stu-id="a9c5f-436">Initial webview URL</span></span>|
|`messageHandlers`|<span data-ttu-id="a9c5f-437">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a9c5f-437">Array of Objects</span></span>|<span data-ttu-id="a9c5f-438">5 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-438">5</span></span>||<span data-ttu-id="a9c5f-439">Una lista de controladores que permiten invocar las aplicaciones cuando se cumplen ciertas condiciones.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="a9c5f-440">Los dominios también deben aparecer en`validDomains`</span><span class="sxs-lookup"><span data-stu-id="a9c5f-440">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="a9c5f-441">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-441">String</span></span>|||<span data-ttu-id="a9c5f-442">El tipo de controlador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-442">The type of message handler.</span></span> <span data-ttu-id="a9c5f-443">Debe ser `"link"`.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="a9c5f-444">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="a9c5f-444">Array of Strings</span></span>|||<span data-ttu-id="a9c5f-445">Matriz de dominios para los que el controlador de mensajes de vínculo puede registrarse.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="a9c5f-446">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a9c5f-446">Array of object</span></span>|<span data-ttu-id="a9c5f-447">5 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-447">5</span></span>|<span data-ttu-id="a9c5f-448">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-448">✔</span></span>|<span data-ttu-id="a9c5f-449">La lista de parámetros que toma el comando.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-449">The list of parameters the command takes.</span></span> <span data-ttu-id="a9c5f-450">Mínimo: 1; máximo: 5</span><span class="sxs-lookup"><span data-stu-id="a9c5f-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="a9c5f-451">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-451">String</span></span>|<span data-ttu-id="a9c5f-452">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-452">64 characters</span></span>|<span data-ttu-id="a9c5f-453">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-453">✔</span></span>|<span data-ttu-id="a9c5f-454">El nombre del parámetro tal y como aparece en el cliente.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="a9c5f-455">Se incluye en la solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="a9c5f-456">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-456">String</span></span>|<span data-ttu-id="a9c5f-457">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-457">32 characters</span></span>|<span data-ttu-id="a9c5f-458">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-458">✔</span></span>|<span data-ttu-id="a9c5f-459">Título descriptivo del parámetro.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="a9c5f-460">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-460">String</span></span>|<span data-ttu-id="a9c5f-461">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-461">128 characters</span></span>||<span data-ttu-id="a9c5f-462">Cadena descriptiva que describe el propósito de este parámetro.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="a9c5f-463">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-463">String</span></span>|<span data-ttu-id="a9c5f-464">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-464">128 characters</span></span>||<span data-ttu-id="a9c5f-465">Define el tipo de control que se muestra en un módulo `fetchTask: true`de tareas para.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="a9c5f-466">Uno de `text`, `textarea`, `number`, `date` `time` `toggle`,,`choiceset`</span><span class="sxs-lookup"><span data-stu-id="a9c5f-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="a9c5f-467">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a9c5f-467">Array of Objects</span></span>|<span data-ttu-id="a9c5f-468">10 </span><span class="sxs-lookup"><span data-stu-id="a9c5f-468">10</span></span>||<span data-ttu-id="a9c5f-469">Las opciones de opción del `choiceset`.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="a9c5f-470">Use solo cuando `parameter.inputType` sea`choiceset`</span><span class="sxs-lookup"><span data-stu-id="a9c5f-470">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="a9c5f-471">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-471">String</span></span>|<span data-ttu-id="a9c5f-472">128</span><span class="sxs-lookup"><span data-stu-id="a9c5f-472">128</span></span>||<span data-ttu-id="a9c5f-473">Título de la opción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-473">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="a9c5f-474">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-474">String</span></span>|<span data-ttu-id="a9c5f-475">512</span><span class="sxs-lookup"><span data-stu-id="a9c5f-475">512</span></span>||<span data-ttu-id="a9c5f-476">Valor de la opción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-476">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="a9c5f-477">permissions</span><span class="sxs-lookup"><span data-stu-id="a9c5f-477">permissions</span></span>

<span data-ttu-id="a9c5f-478">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-478">**Optional**</span></span>

<span data-ttu-id="a9c5f-479">Una matriz de `string` que especifica los permisos que solicita la aplicación, lo que permite a los usuarios finales saber cómo se realizará la extensión.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="a9c5f-480">Las siguientes opciones no son exclusivas:</span><span class="sxs-lookup"><span data-stu-id="a9c5f-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="a9c5f-481">`identity`&emsp; Requiere información de identidad del usuario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-481">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="a9c5f-482">`messageTeamMembers`&emsp; Requiere permiso para enviar mensajes directos a los miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="a9c5f-483">Cambiar estos permisos al actualizar la aplicación hará que los usuarios repitan el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="a9c5f-484">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="a9c5f-484">devicePermissions</span></span>

<span data-ttu-id="a9c5f-485">**Opcional** Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="a9c5f-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="a9c5f-486">Especifica las características nativas del dispositivo de un usuario al que la aplicación puede solicitar acceso.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="a9c5f-487">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="a9c5f-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="a9c5f-488">validDomains</span><span class="sxs-lookup"><span data-stu-id="a9c5f-488">validDomains</span></span>

<span data-ttu-id="a9c5f-489">**Opcional**, excepto **obligatorio** donde se indica</span><span class="sxs-lookup"><span data-stu-id="a9c5f-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="a9c5f-490">Una lista de dominios válidos de los que la aplicación espera cargar contenido.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="a9c5f-491">Las listas de dominios pueden incluir caracteres comodín, por `*.example.com`ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="a9c5f-492">Esto coincide exactamente con un segmento del dominio; Si tiene que hacer coincidir `a.b.example.com` , `*.*.example.com`use.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="a9c5f-493">Si la configuración de la pestaña o la interfaz de usuario de contenido debe navegar a cualquier otro dominio además del uso de la configuración de pestañas, dicho dominio debe especificarse aquí.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="a9c5f-494">No obstante, **no** es necesario incluir los dominios de los proveedores de identidades que desea admitir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="a9c5f-495">Por ejemplo, para autenticarse con un identificador de Google, es necesario redirigir a accounts.google.com, pero no se debe incluir accounts.google.com en `validDomains[]`.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9c5f-496">No agregue dominios que estén fuera de su control, ya sea directamente o mediante caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="a9c5f-497">Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="a9c5f-498">El objeto es una matriz con todos los elementos del tipo `string`.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="a9c5f-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-499">webApplicationInfo</span></span>

<span data-ttu-id="a9c5f-500">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a9c5f-500">**Optional**</span></span>

<span data-ttu-id="a9c5f-501">Especifique la información del grafo y el identificador de la aplicación de AAD para ayudar a los usuarios a iniciar sesión sin problemas en su aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="a9c5f-502">Nombre</span><span class="sxs-lookup"><span data-stu-id="a9c5f-502">Name</span></span>| <span data-ttu-id="a9c5f-503">Tipo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-503">Type</span></span>| <span data-ttu-id="a9c5f-504">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a9c5f-504">Maximum size</span></span> | <span data-ttu-id="a9c5f-505">Necesario</span><span class="sxs-lookup"><span data-stu-id="a9c5f-505">Required</span></span> | <span data-ttu-id="a9c5f-506">Descripción</span><span class="sxs-lookup"><span data-stu-id="a9c5f-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="a9c5f-507">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-507">String</span></span>|<span data-ttu-id="a9c5f-508">36 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-508">36 characters</span></span>|<span data-ttu-id="a9c5f-509">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-509">✔</span></span>|<span data-ttu-id="a9c5f-510">Identificador de la aplicación de AAD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-510">AAD application id of the app.</span></span> <span data-ttu-id="a9c5f-511">Este identificador debe ser un GUID.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="a9c5f-512">String</span><span class="sxs-lookup"><span data-stu-id="a9c5f-512">String</span></span>|<span data-ttu-id="a9c5f-513">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a9c5f-513">2048 characters</span></span>|<span data-ttu-id="a9c5f-514">✔</span><span class="sxs-lookup"><span data-stu-id="a9c5f-514">✔</span></span>|<span data-ttu-id="a9c5f-515">Dirección URL de recurso de la aplicación para adquirir el token de autenticación para el SSO.</span><span class="sxs-lookup"><span data-stu-id="a9c5f-515">Resource url of app for acquiring auth token for SSO.</span></span>|