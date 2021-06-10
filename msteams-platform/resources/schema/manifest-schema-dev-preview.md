---
title: Referencia de esquema de manifiesto de versión preliminar de desarrollador
description: Describe el esquema admitido por el manifiesto para Microsoft Teams
ms.topic: reference
keywords: Vista previa del programador del esquema de manifiesto de teams
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: c582a6af0505680b9843c86be7fc800fab12129d
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853539"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="0eee4-104">Esquema de manifiesto de vista previa de desarrollador para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0eee4-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="0eee4-105">Para obtener más información sobre el programa y cómo puede unirse, vea [Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="0eee4-105">For more information on the program and how you can join,see [Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
> <span data-ttu-id="0eee4-106">Si no usa la vista previa del desarrollador, no debe usar esta versión del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0eee4-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="0eee4-107">Vea [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) para la versión pública del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0eee4-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="0eee4-108">El Microsoft Teams describe cómo se integra la aplicación en el Microsoft Teams producto.</span><span class="sxs-lookup"><span data-stu-id="0eee4-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="0eee4-109">El manifiesto debe cumplir con el esquema hospedado en [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="0eee4-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="0eee4-110">Para obtener más información sobre las características disponibles, vea: [Características en public developer preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span><span class="sxs-lookup"><span data-stu-id="0eee4-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="0eee4-111">Manifiesto completo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0eee4-111">Sample full manifest</span></span>

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
      "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
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
  ],
  "webApplicationInfo": {
    "id": "AAD App ID",
    "resource": "Resource URL for acquiring auth token for SSO",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelSettings.Read.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "ChannelMessage.Read.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group",
      "Member.ReadWrite.Group",
      "Owner.ReadWrite.Group"
    ],
  },
   "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "developerUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ],
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  }
}
```

<span data-ttu-id="0eee4-112">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="0eee4-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="0eee4-113">$schema</span><span class="sxs-lookup"><span data-stu-id="0eee4-113">$schema</span></span>

<span data-ttu-id="0eee4-114">*Opcional, pero recomendado* &ndash; String</span><span class="sxs-lookup"><span data-stu-id="0eee4-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="0eee4-115">La https:// url que hace referencia al esquema JSON para el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0eee4-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="0eee4-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="0eee4-116">manifestVersion</span></span>

<span data-ttu-id="0eee4-117">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="0eee4-117">**Required** &ndash; String</span></span>

<span data-ttu-id="0eee4-118">La versión del esquema de manifiesto que usa este manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0eee4-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="0eee4-119">Debe ser "devPreview".</span><span class="sxs-lookup"><span data-stu-id="0eee4-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="0eee4-120">version</span><span class="sxs-lookup"><span data-stu-id="0eee4-120">version</span></span>

<span data-ttu-id="0eee4-121">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="0eee4-121">**Required** &ndash; String</span></span>

<span data-ttu-id="0eee4-122">La versión de la aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="0eee4-122">The version of the specific app.</span></span> <span data-ttu-id="0eee4-123">Si actualiza algo en el manifiesto, la versión también debe incrementarse.</span><span class="sxs-lookup"><span data-stu-id="0eee4-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="0eee4-124">De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="0eee4-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="0eee4-125">Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y volver a validarse.</span><span class="sxs-lookup"><span data-stu-id="0eee4-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="0eee4-126">A continuación, los usuarios de esta aplicación recibirán el nuevo manifiesto actualizado automáticamente en unas pocas horas, después de que se apruebe.</span><span class="sxs-lookup"><span data-stu-id="0eee4-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="0eee4-127">Si cambian los permisos solicitados por la aplicación, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="0eee4-128">Esta cadena de versión debe seguir el [estándar de semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="0eee4-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="0eee4-129">id</span><span class="sxs-lookup"><span data-stu-id="0eee4-129">id</span></span>

<span data-ttu-id="0eee4-130">**Obligatorio** &ndash; Id. de aplicación de Microsoft</span><span class="sxs-lookup"><span data-stu-id="0eee4-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="0eee4-131">Identificador único generado por Microsoft para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="0eee4-132">Si has registrado un bot a través del Microsoft Bot Framework o la aplicación web de la pestaña ya inicia sesión con Microsoft, ya debes tener un identificador y debes escribirlo aquí.</span><span class="sxs-lookup"><span data-stu-id="0eee4-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="0eee4-133">De lo contrario, debe generar un nuevo identificador en el Portal de registro de aplicaciones de Microsoft ([Mis](https://apps.dev.microsoft.com)aplicaciones ), escriba aquí y, a continuación, volver a usarlo cuando [agregue un bot](~/bots/how-to/create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="0eee4-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="0eee4-134">packageName</span><span class="sxs-lookup"><span data-stu-id="0eee4-134">packageName</span></span>

<span data-ttu-id="0eee4-135">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="0eee4-135">**Required** &ndash; String</span></span>

<span data-ttu-id="0eee4-136">Un identificador único para esta aplicación en la notación de dominio inverso; por ejemplo, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="0eee4-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="0eee4-137">developer</span><span class="sxs-lookup"><span data-stu-id="0eee4-137">developer</span></span>

<span data-ttu-id="0eee4-138">**Required**</span><span class="sxs-lookup"><span data-stu-id="0eee4-138">**Required**</span></span>

<span data-ttu-id="0eee4-139">Especifica información sobre su empresa.</span><span class="sxs-lookup"><span data-stu-id="0eee4-139">Specifies information about your company.</span></span> <span data-ttu-id="0eee4-140">Para las aplicaciones enviadas a AppSource (anteriormente Office Store), estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="0eee4-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="0eee4-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-141">Name</span></span>| <span data-ttu-id="0eee4-142">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-142">Maximum size</span></span> | <span data-ttu-id="0eee4-143">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-143">Required</span></span> | <span data-ttu-id="0eee4-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="0eee4-145">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-145">32 characters</span></span>|<span data-ttu-id="0eee4-146">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-146">✔</span></span>|<span data-ttu-id="0eee4-147">Nombre para mostrar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0eee4-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="0eee4-148">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-148">2048 characters</span></span>|<span data-ttu-id="0eee4-149">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-149">✔</span></span>|<span data-ttu-id="0eee4-150">La https:// url del sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0eee4-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="0eee4-151">Este vínculo debe llevar a los usuarios a su empresa o página de aterrizaje específica del producto.</span><span class="sxs-lookup"><span data-stu-id="0eee4-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="0eee4-152">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-152">2048 characters</span></span>|<span data-ttu-id="0eee4-153">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-153">✔</span></span>|<span data-ttu-id="0eee4-154">La https:// url a la directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0eee4-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="0eee4-155">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-155">2048 characters</span></span>|<span data-ttu-id="0eee4-156">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-156">✔</span></span>|<span data-ttu-id="0eee4-157">La https:// url a los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0eee4-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="0eee4-158">10 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-158">10 characters</span></span>|<span data-ttu-id="0eee4-159">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-159">✔</span></span>|<span data-ttu-id="0eee4-160">**Opcional** Id. de red de partners de Microsoft que identifica la organización asociada que está creando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="0eee4-161">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="0eee4-161">localizationInfo</span></span>

<span data-ttu-id="0eee4-162">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0eee4-162">**Optional**</span></span>

<span data-ttu-id="0eee4-163">Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="0eee4-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="0eee4-164">Vea [localización](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="0eee4-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="0eee4-165">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-165">Name</span></span>| <span data-ttu-id="0eee4-166">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-166">Maximum size</span></span> | <span data-ttu-id="0eee4-167">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-167">Required</span></span> | <span data-ttu-id="0eee4-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="0eee4-169">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-169">4 characters</span></span>|<span data-ttu-id="0eee4-170">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-170">✔</span></span>|<span data-ttu-id="0eee4-171">La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="0eee4-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="0eee4-172">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="0eee4-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="0eee4-173">Una matriz de objetos que especifica traducciones de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="0eee4-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="0eee4-174">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-174">Name</span></span>| <span data-ttu-id="0eee4-175">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-175">Maximum size</span></span> | <span data-ttu-id="0eee4-176">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-176">Required</span></span> | <span data-ttu-id="0eee4-177">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="0eee4-178">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-178">4 characters</span></span>|<span data-ttu-id="0eee4-179">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-179">✔</span></span>|<span data-ttu-id="0eee4-180">Etiqueta de idioma de las cadenas del archivo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="0eee4-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="0eee4-181">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-181">4 characters</span></span>|<span data-ttu-id="0eee4-182">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-182">✔</span></span>|<span data-ttu-id="0eee4-183">Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="0eee4-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="0eee4-184">name</span><span class="sxs-lookup"><span data-stu-id="0eee4-184">name</span></span>

<span data-ttu-id="0eee4-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="0eee4-185">**Required**</span></span>

<span data-ttu-id="0eee4-186">El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="0eee4-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="0eee4-187">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="0eee4-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="0eee4-188">Los valores de `short` y no deben ser los `full` mismos.</span><span class="sxs-lookup"><span data-stu-id="0eee4-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="0eee4-189">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-189">Name</span></span>| <span data-ttu-id="0eee4-190">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-190">Maximum size</span></span> | <span data-ttu-id="0eee4-191">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-191">Required</span></span> | <span data-ttu-id="0eee4-192">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="0eee4-193">30 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-193">30 characters</span></span>|<span data-ttu-id="0eee4-194">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-194">✔</span></span>|<span data-ttu-id="0eee4-195">El nombre para mostrar corto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="0eee4-196">100 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-196">100 characters</span></span>||<span data-ttu-id="0eee4-197">El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0eee4-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="0eee4-198">description</span><span class="sxs-lookup"><span data-stu-id="0eee4-198">description</span></span>

<span data-ttu-id="0eee4-199">**Required**</span><span class="sxs-lookup"><span data-stu-id="0eee4-199">**Required**</span></span>

<span data-ttu-id="0eee4-200">Describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0eee4-200">Describes your app to users.</span></span> <span data-ttu-id="0eee4-201">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="0eee4-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="0eee4-202">Asegúrese de que su descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia.</span><span class="sxs-lookup"><span data-stu-id="0eee4-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="0eee4-203">También debe tener en cuenta, en la descripción completa, si se requiere una cuenta externa para su uso.</span><span class="sxs-lookup"><span data-stu-id="0eee4-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="0eee4-204">Los valores de `short` y no deben ser los `full` mismos.</span><span class="sxs-lookup"><span data-stu-id="0eee4-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="0eee4-205">La descripción breve no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="0eee4-206">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-206">Name</span></span>| <span data-ttu-id="0eee4-207">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-207">Maximum size</span></span> | <span data-ttu-id="0eee4-208">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-208">Required</span></span> | <span data-ttu-id="0eee4-209">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="0eee4-210">80 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-210">80 characters</span></span>|<span data-ttu-id="0eee4-211">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-211">✔</span></span>|<span data-ttu-id="0eee4-212">Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.</span><span class="sxs-lookup"><span data-stu-id="0eee4-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="0eee4-213">4000 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-213">4000 characters</span></span>|<span data-ttu-id="0eee4-214">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-214">✔</span></span>|<span data-ttu-id="0eee4-215">Descripción completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="0eee4-216">iconos</span><span class="sxs-lookup"><span data-stu-id="0eee4-216">icons</span></span>

<span data-ttu-id="0eee4-217">**Required**</span><span class="sxs-lookup"><span data-stu-id="0eee4-217">**Required**</span></span>

<span data-ttu-id="0eee4-218">Iconos usados dentro de la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-218">Icons used within the Teams app.</span></span> <span data-ttu-id="0eee4-219">Los archivos de icono deben incluirse como parte del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="0eee4-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="0eee4-220">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-220">Name</span></span>| <span data-ttu-id="0eee4-221">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-221">Maximum size</span></span> | <span data-ttu-id="0eee4-222">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-222">Required</span></span> | <span data-ttu-id="0eee4-223">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="0eee4-224">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-224">2048 characters</span></span>|<span data-ttu-id="0eee4-225">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-225">✔</span></span>|<span data-ttu-id="0eee4-226">Una ruta de acceso de archivo relativa a un icono de esquema PNG transparente de 32 x 32.</span><span class="sxs-lookup"><span data-stu-id="0eee4-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="0eee4-227">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-227">2048 characters</span></span>|<span data-ttu-id="0eee4-228">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-228">✔</span></span>|<span data-ttu-id="0eee4-229">Una ruta de acceso de archivo relativa a un icono PNG de color completo de 192 x 192.</span><span class="sxs-lookup"><span data-stu-id="0eee4-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="0eee4-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="0eee4-230">accentColor</span></span>

<span data-ttu-id="0eee4-231">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="0eee4-231">**Required** &ndash; String</span></span>

<span data-ttu-id="0eee4-232">Color que se usará junto con y como fondo para los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="0eee4-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="0eee4-233">El valor debe ser un código de color HTML válido a partir de '#', por ejemplo `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="0eee4-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="0eee4-234">configurableTabs</span></span>

<span data-ttu-id="0eee4-235">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0eee4-235">**Optional**</span></span>

<span data-ttu-id="0eee4-236">Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de grupo que requiere una configuración adicional antes de agregarla.</span><span class="sxs-lookup"><span data-stu-id="0eee4-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="0eee4-237">Las pestañas configurables solo se admiten en el ámbito de teams y actualmente solo se admite una pestaña por aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="0eee4-238">El objeto es una matriz con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="0eee4-239">Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña de canal configurable.</span><span class="sxs-lookup"><span data-stu-id="0eee4-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="0eee4-240">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-240">Name</span></span>| <span data-ttu-id="0eee4-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="0eee4-241">Type</span></span>| <span data-ttu-id="0eee4-242">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-242">Maximum size</span></span> | <span data-ttu-id="0eee4-243">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-243">Required</span></span> | <span data-ttu-id="0eee4-244">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="0eee4-245">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-245">String</span></span>|<span data-ttu-id="0eee4-246">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-246">2048 characters</span></span>|<span data-ttu-id="0eee4-247">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-247">✔</span></span>|<span data-ttu-id="0eee4-248">La https:// url que se va a usar al configurar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0eee4-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="0eee4-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="0eee4-249">Boolean</span></span>|||<span data-ttu-id="0eee4-250">Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de su creación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="0eee4-251">Valor predeterminado: `true`</span><span class="sxs-lookup"><span data-stu-id="0eee4-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="0eee4-252">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0eee4-252">Array of enum</span></span>|<span data-ttu-id="0eee4-253">1</span><span class="sxs-lookup"><span data-stu-id="0eee4-253">1</span></span>|<span data-ttu-id="0eee4-254">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-254">✔</span></span>|<span data-ttu-id="0eee4-255">Actualmente, las pestañas configurables solo admiten `team` los `groupchat` ámbitos y.</span><span class="sxs-lookup"><span data-stu-id="0eee4-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="0eee4-256">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-256">String</span></span>|<span data-ttu-id="0eee4-257">2048</span><span class="sxs-lookup"><span data-stu-id="0eee4-257">2048</span></span>||<span data-ttu-id="0eee4-258">Una ruta de acceso de archivo relativa a una imagen de vista previa de tabulación para su uso en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0eee4-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="0eee4-259">Tamaño 1024x768.</span><span class="sxs-lookup"><span data-stu-id="0eee4-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="0eee4-260">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0eee4-260">Array of enum</span></span>|<span data-ttu-id="0eee4-261">1</span><span class="sxs-lookup"><span data-stu-id="0eee4-261">1</span></span>||<span data-ttu-id="0eee4-262">Define cómo la pestaña estará disponible en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0eee4-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="0eee4-263">Las opciones son `sharePointFullPage` y `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="0eee4-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="0eee4-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="0eee4-264">staticTabs</span></span>

<span data-ttu-id="0eee4-265">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0eee4-265">**Optional**</span></span>

<span data-ttu-id="0eee4-266">Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente.</span><span class="sxs-lookup"><span data-stu-id="0eee4-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="0eee4-267">Las pestañas estáticas declaradas en el ámbito siempre se anclan a la experiencia `personal` personal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="0eee4-268">Actualmente no se admiten las pestañas estáticas declaradas `team` en el ámbito.</span><span class="sxs-lookup"><span data-stu-id="0eee4-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="0eee4-269">Represente las pestañas con tarjetas adaptables especificando en `contentBotId` lugar de en el bloque `contentUrl` **staticTabs.**</span><span class="sxs-lookup"><span data-stu-id="0eee4-269">Render tabs with Adaptive Cards by specifying `contentBotId` instead of `contentUrl` in the **staticTabs** block.</span></span>

<span data-ttu-id="0eee4-270">El objeto es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-270">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="0eee4-271">Este bloque solo es necesario para las soluciones que proporcionan una solución de tabulación estática.</span><span class="sxs-lookup"><span data-stu-id="0eee4-271">This block is required only for solutions that provide a static tab solution.</span></span>


|<span data-ttu-id="0eee4-272">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-272">Name</span></span>| <span data-ttu-id="0eee4-273">Tipo</span><span class="sxs-lookup"><span data-stu-id="0eee4-273">Type</span></span>| <span data-ttu-id="0eee4-274">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-274">Maximum size</span></span> | <span data-ttu-id="0eee4-275">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-275">Required</span></span> | <span data-ttu-id="0eee4-276">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-276">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="0eee4-277">String</span><span class="sxs-lookup"><span data-stu-id="0eee4-277">String</span></span>|<span data-ttu-id="0eee4-278">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-278">64 characters</span></span>|<span data-ttu-id="0eee4-279">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-279">✔</span></span>|<span data-ttu-id="0eee4-280">Identificador único para la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0eee4-280">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="0eee4-281">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-281">String</span></span>|<span data-ttu-id="0eee4-282">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-282">128 characters</span></span>|<span data-ttu-id="0eee4-283">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-283">✔</span></span>|<span data-ttu-id="0eee4-284">Nombre para mostrar de la pestaña en la interfaz de canal.</span><span class="sxs-lookup"><span data-stu-id="0eee4-284">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="0eee4-285">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-285">String</span></span>|<span data-ttu-id="0eee4-286">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-286">2048 characters</span></span>|<span data-ttu-id="0eee4-287">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-287">✔</span></span>|<span data-ttu-id="0eee4-288">Dirección URL https:// que apunta a la interfaz de usuario de la entidad que se va a mostrar en el Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="0eee4-288">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`contentBotId`|   | | | <span data-ttu-id="0eee4-289">El Microsoft Teams de aplicación especificado para el bot en el portal de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="0eee4-289">The Microsoft Teams app ID specified for the bot in the Bot Framework portal.</span></span> |
|`websiteUrl`|<span data-ttu-id="0eee4-290">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-290">String</span></span>|<span data-ttu-id="0eee4-291">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-291">2048 characters</span></span>||<span data-ttu-id="0eee4-292">La https:// dirección URL para apuntar si un usuario opta por ver en un explorador.</span><span class="sxs-lookup"><span data-stu-id="0eee4-292">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="0eee4-293">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0eee4-293">Array of enum</span></span>|<span data-ttu-id="0eee4-294">1</span><span class="sxs-lookup"><span data-stu-id="0eee4-294">1</span></span>|<span data-ttu-id="0eee4-295">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-295">✔</span></span>|<span data-ttu-id="0eee4-296">Actualmente, las pestañas estáticas solo admiten el ámbito, lo que significa que solo se puede aprovisionar como `personal` parte de la experiencia personal.</span><span class="sxs-lookup"><span data-stu-id="0eee4-296">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="0eee4-297">bots</span><span class="sxs-lookup"><span data-stu-id="0eee4-297">bots</span></span>

<span data-ttu-id="0eee4-298">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0eee4-298">**Optional**</span></span>

<span data-ttu-id="0eee4-299">Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="0eee4-299">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="0eee4-300">El objeto es una matriz (máximo de solo 1 elemento actualmente solo se permite un bot por aplicación) con todos los &mdash; elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-300">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="0eee4-301">Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.</span><span class="sxs-lookup"><span data-stu-id="0eee4-301">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="0eee4-302">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-302">Name</span></span>| <span data-ttu-id="0eee4-303">Tipo</span><span class="sxs-lookup"><span data-stu-id="0eee4-303">Type</span></span>| <span data-ttu-id="0eee4-304">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-304">Maximum size</span></span> | <span data-ttu-id="0eee4-305">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-305">Required</span></span> | <span data-ttu-id="0eee4-306">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-306">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="0eee4-307">String</span><span class="sxs-lookup"><span data-stu-id="0eee4-307">String</span></span>|<span data-ttu-id="0eee4-308">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-308">64 characters</span></span>|<span data-ttu-id="0eee4-309">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-309">✔</span></span>|<span data-ttu-id="0eee4-310">El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="0eee4-310">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="0eee4-311">Esto bien puede ser el mismo que el identificador general [de la aplicación](#id).</span><span class="sxs-lookup"><span data-stu-id="0eee4-311">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="0eee4-312">Booleano</span><span class="sxs-lookup"><span data-stu-id="0eee4-312">Boolean</span></span>|||<span data-ttu-id="0eee4-313">Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico.</span><span class="sxs-lookup"><span data-stu-id="0eee4-313">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="0eee4-314">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="0eee4-314">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="0eee4-315">Booleano</span><span class="sxs-lookup"><span data-stu-id="0eee4-315">Boolean</span></span>|||<span data-ttu-id="0eee4-316">Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-316">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="0eee4-317">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="0eee4-317">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="0eee4-318">Booleano</span><span class="sxs-lookup"><span data-stu-id="0eee4-318">Boolean</span></span>|||<span data-ttu-id="0eee4-319">Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal.</span><span class="sxs-lookup"><span data-stu-id="0eee4-319">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="0eee4-320">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="0eee4-320">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="0eee4-321">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0eee4-321">Array of enum</span></span>|<span data-ttu-id="0eee4-322">3</span><span class="sxs-lookup"><span data-stu-id="0eee4-322">3</span></span>|<span data-ttu-id="0eee4-323">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-323">✔</span></span>|<span data-ttu-id="0eee4-324">Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`).</span><span class="sxs-lookup"><span data-stu-id="0eee4-324">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="0eee4-325">Estas opciones no son exclusivas.</span><span class="sxs-lookup"><span data-stu-id="0eee4-325">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="0eee4-326">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="0eee4-326">bots.commandLists</span></span>

<span data-ttu-id="0eee4-327">Una lista opcional de comandos que el bot puede recomendar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0eee4-327">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="0eee4-328">El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de comandos independiente para cada ámbito compatible `object` con el bot.</span><span class="sxs-lookup"><span data-stu-id="0eee4-328">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="0eee4-329">Para obtener más información, vea [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span><span class="sxs-lookup"><span data-stu-id="0eee4-329">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="0eee4-330">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-330">Name</span></span>| <span data-ttu-id="0eee4-331">Tipo</span><span class="sxs-lookup"><span data-stu-id="0eee4-331">Type</span></span>| <span data-ttu-id="0eee4-332">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-332">Maximum size</span></span> | <span data-ttu-id="0eee4-333">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-333">Required</span></span> | <span data-ttu-id="0eee4-334">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-334">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="0eee4-335">matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0eee4-335">array of enum</span></span>|<span data-ttu-id="0eee4-336">3</span><span class="sxs-lookup"><span data-stu-id="0eee4-336">3</span></span>|<span data-ttu-id="0eee4-337">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-337">✔</span></span>|<span data-ttu-id="0eee4-338">Especifica el ámbito para el que la lista de comandos es válida.</span><span class="sxs-lookup"><span data-stu-id="0eee4-338">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="0eee4-339">Las opciones son `team`, `personal` y `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="0eee4-339">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="0eee4-340">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="0eee4-340">array of objects</span></span>|<span data-ttu-id="0eee4-341">10</span><span class="sxs-lookup"><span data-stu-id="0eee4-341">10</span></span>|<span data-ttu-id="0eee4-342">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-342">✔</span></span>|<span data-ttu-id="0eee4-343">Una matriz de comandos que el bot admite:</span><span class="sxs-lookup"><span data-stu-id="0eee4-343">An array of commands the bot supports:</span></span><br><span data-ttu-id="0eee4-344">`title`: el nombre del comando bot (cadena, 32).</span><span class="sxs-lookup"><span data-stu-id="0eee4-344">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="0eee4-345">`description`: una descripción sencilla o un ejemplo de la sintaxis del comando y su argumento (cadena, 128).</span><span class="sxs-lookup"><span data-stu-id="0eee4-345">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="0eee4-346">conectores</span><span class="sxs-lookup"><span data-stu-id="0eee4-346">connectors</span></span>

<span data-ttu-id="0eee4-347">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0eee4-347">**Optional**</span></span>

<span data-ttu-id="0eee4-348">El `connectors` bloque define un Office 365 connector para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-348">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="0eee4-349">El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-349">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="0eee4-350">Este bloque solo es necesario para las soluciones que proporcionan un conector.</span><span class="sxs-lookup"><span data-stu-id="0eee4-350">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="0eee4-351">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-351">Name</span></span>| <span data-ttu-id="0eee4-352">Tipo</span><span class="sxs-lookup"><span data-stu-id="0eee4-352">Type</span></span>| <span data-ttu-id="0eee4-353">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-353">Maximum size</span></span> | <span data-ttu-id="0eee4-354">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-354">Required</span></span> | <span data-ttu-id="0eee4-355">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-355">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="0eee4-356">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-356">String</span></span>|<span data-ttu-id="0eee4-357">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-357">2048 characters</span></span>|<span data-ttu-id="0eee4-358">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-358">✔</span></span>|<span data-ttu-id="0eee4-359">La https:// url que se va a usar al configurar el conector.</span><span class="sxs-lookup"><span data-stu-id="0eee4-359">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="0eee4-360">String</span><span class="sxs-lookup"><span data-stu-id="0eee4-360">String</span></span>|<span data-ttu-id="0eee4-361">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-361">64 characters</span></span>|<span data-ttu-id="0eee4-362">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-362">✔</span></span>|<span data-ttu-id="0eee4-363">Identificador único del conector que coincide con su identificador en el [Panel de desarrolladores de conectores.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="0eee4-363">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="0eee4-364">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0eee4-364">Array of enum</span></span>|<span data-ttu-id="0eee4-365">1</span><span class="sxs-lookup"><span data-stu-id="0eee4-365">1</span></span>|<span data-ttu-id="0eee4-366">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-366">✔</span></span>|<span data-ttu-id="0eee4-367">Especifica si connector ofrece una experiencia en el contexto de un canal en un , o una experiencia ámbito a un `team` usuario individual solo ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="0eee4-367">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="0eee4-368">Actualmente, solo se `team` admite el ámbito.</span><span class="sxs-lookup"><span data-stu-id="0eee4-368">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="0eee4-369">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="0eee4-369">composeExtensions</span></span>

<span data-ttu-id="0eee4-370">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0eee4-370">**Optional**</span></span>

<span data-ttu-id="0eee4-371">Define una extensión de mensajería para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-371">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="0eee4-372">El nombre de la característica se cambió de "extensión de redacción" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="0eee4-372">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="0eee4-373">El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-373">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="0eee4-374">Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0eee4-374">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="0eee4-375">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-375">Name</span></span>| <span data-ttu-id="0eee4-376">Tipo</span><span class="sxs-lookup"><span data-stu-id="0eee4-376">Type</span></span> | <span data-ttu-id="0eee4-377">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-377">Maximum Size</span></span> | <span data-ttu-id="0eee4-378">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0eee4-378">Required</span></span> | <span data-ttu-id="0eee4-379">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-379">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="0eee4-380">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-380">String</span></span>|<span data-ttu-id="0eee4-381">64</span><span class="sxs-lookup"><span data-stu-id="0eee4-381">64</span></span>|<span data-ttu-id="0eee4-382">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-382">✔</span></span>|<span data-ttu-id="0eee4-383">El identificador único de la aplicación de Microsoft para el bot que hace una copia de seguridad de la extensión de mensajería, tal como se registró con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="0eee4-383">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="0eee4-384">Esto bien puede ser el mismo que el identificador general [de la aplicación](#id).</span><span class="sxs-lookup"><span data-stu-id="0eee4-384">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="0eee4-385">Boolean</span><span class="sxs-lookup"><span data-stu-id="0eee4-385">Boolean</span></span>|||<span data-ttu-id="0eee4-386">Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0eee4-386">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="0eee4-387">El valor predeterminado es `false`.</span><span class="sxs-lookup"><span data-stu-id="0eee4-387">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="0eee4-388">Matriz de objeto</span><span class="sxs-lookup"><span data-stu-id="0eee4-388">Array of object</span></span>|<span data-ttu-id="0eee4-389">10</span><span class="sxs-lookup"><span data-stu-id="0eee4-389">10</span></span>|<span data-ttu-id="0eee4-390">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-390">✔</span></span>|<span data-ttu-id="0eee4-391">Matriz de comandos que admite la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="0eee4-391">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="0eee4-392">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="0eee4-392">composeExtensions.commands</span></span>

<span data-ttu-id="0eee4-393">La extensión de mensajería debe declarar uno o más comandos.</span><span class="sxs-lookup"><span data-stu-id="0eee4-393">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="0eee4-394">Cada comando aparece en Microsoft Teams como una interacción potencial desde el punto de entrada basado en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="0eee4-394">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="0eee4-395">Hay un máximo de 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="0eee4-395">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="0eee4-396">Cada elemento de comando es un objeto con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="0eee4-396">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="0eee4-397">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-397">Name</span></span>| <span data-ttu-id="0eee4-398">Tipo</span><span class="sxs-lookup"><span data-stu-id="0eee4-398">Type</span></span>| <span data-ttu-id="0eee4-399">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-399">Maximum size</span></span> | <span data-ttu-id="0eee4-400">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-400">Required</span></span> | <span data-ttu-id="0eee4-401">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-401">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="0eee4-402">String</span><span class="sxs-lookup"><span data-stu-id="0eee4-402">String</span></span>|<span data-ttu-id="0eee4-403">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-403">64 characters</span></span>|<span data-ttu-id="0eee4-404">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-404">✔</span></span>|<span data-ttu-id="0eee4-405">El identificador del comando.</span><span class="sxs-lookup"><span data-stu-id="0eee4-405">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="0eee4-406">String</span><span class="sxs-lookup"><span data-stu-id="0eee4-406">String</span></span>|<span data-ttu-id="0eee4-407">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-407">64 characters</span></span>||<span data-ttu-id="0eee4-408">Tipo del comando.</span><span class="sxs-lookup"><span data-stu-id="0eee4-408">Type of the command.</span></span> <span data-ttu-id="0eee4-409">Uno de `query` o `action` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-409">One of `query` or `action`.</span></span> <span data-ttu-id="0eee4-410">Valor predeterminado: `query`</span><span class="sxs-lookup"><span data-stu-id="0eee4-410">Default: `query`</span></span>|
|`title`|<span data-ttu-id="0eee4-411">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-411">String</span></span>|<span data-ttu-id="0eee4-412">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-412">32 characters</span></span>|<span data-ttu-id="0eee4-413">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-413">✔</span></span>|<span data-ttu-id="0eee4-414">Nombre de comando fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="0eee4-414">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="0eee4-415">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-415">String</span></span>|<span data-ttu-id="0eee4-416">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-416">128 characters</span></span>||<span data-ttu-id="0eee4-417">La descripción que se muestra a los usuarios para indicar el propósito de este comando.</span><span class="sxs-lookup"><span data-stu-id="0eee4-417">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="0eee4-418">Boolean</span><span class="sxs-lookup"><span data-stu-id="0eee4-418">Boolean</span></span>|||<span data-ttu-id="0eee4-419">Valor booleano que indica si el comando debe ejecutarse inicialmente sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="0eee4-419">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="0eee4-420">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="0eee4-420">Default: `false`</span></span>|
|`context`|<span data-ttu-id="0eee4-421">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="0eee4-421">Array of Strings</span></span>|<span data-ttu-id="0eee4-422">3</span><span class="sxs-lookup"><span data-stu-id="0eee4-422">3</span></span>||<span data-ttu-id="0eee4-423">Define desde dónde se puede invocar la extensión de mensaje.</span><span class="sxs-lookup"><span data-stu-id="0eee4-423">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="0eee4-424">Cualquier combinación de `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-424">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="0eee4-425">El valor predeterminado es `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="0eee4-425">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="0eee4-426">Boolean</span><span class="sxs-lookup"><span data-stu-id="0eee4-426">Boolean</span></span>|||<span data-ttu-id="0eee4-427">Valor booleano que indica si debe capturar el módulo de tareas dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="0eee4-427">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="0eee4-428">Objeto</span><span class="sxs-lookup"><span data-stu-id="0eee4-428">Object</span></span>|||<span data-ttu-id="0eee4-429">Especifique el módulo de tareas que se debe precargar al usar un comando de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0eee4-429">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="0eee4-430">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-430">String</span></span>|<span data-ttu-id="0eee4-431">64</span><span class="sxs-lookup"><span data-stu-id="0eee4-431">64</span></span>||<span data-ttu-id="0eee4-432">Título del cuadro de diálogo inicial.</span><span class="sxs-lookup"><span data-stu-id="0eee4-432">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="0eee4-433">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-433">String</span></span>|||<span data-ttu-id="0eee4-434">Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="0eee4-434">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="0eee4-435">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-435">String</span></span>|||<span data-ttu-id="0eee4-436">Alto del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="0eee4-436">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="0eee4-437">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-437">String</span></span>|||<span data-ttu-id="0eee4-438">Dirección URL de vista web inicial.</span><span class="sxs-lookup"><span data-stu-id="0eee4-438">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="0eee4-439">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="0eee4-439">Array of Objects</span></span>|<span data-ttu-id="0eee4-440">5 </span><span class="sxs-lookup"><span data-stu-id="0eee4-440">5</span></span>||<span data-ttu-id="0eee4-441">Una lista de controladores que permiten invocar aplicaciones cuando se cumplen determinadas condiciones.</span><span class="sxs-lookup"><span data-stu-id="0eee4-441">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="0eee4-442">Los dominios también deben aparecer en `validDomains` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-442">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="0eee4-443">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-443">String</span></span>|||<span data-ttu-id="0eee4-444">El tipo de controlador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="0eee4-444">The type of message handler.</span></span> <span data-ttu-id="0eee4-445">Debe ser `"link"`.</span><span class="sxs-lookup"><span data-stu-id="0eee4-445">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="0eee4-446">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="0eee4-446">Array of Strings</span></span>|||<span data-ttu-id="0eee4-447">Matriz de dominios para los que se puede registrar el controlador de mensajes de vínculo.</span><span class="sxs-lookup"><span data-stu-id="0eee4-447">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="0eee4-448">Matriz de objeto</span><span class="sxs-lookup"><span data-stu-id="0eee4-448">Array of object</span></span>|<span data-ttu-id="0eee4-449">5 </span><span class="sxs-lookup"><span data-stu-id="0eee4-449">5</span></span>|<span data-ttu-id="0eee4-450">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-450">✔</span></span>|<span data-ttu-id="0eee4-451">La lista de parámetros que toma el comando.</span><span class="sxs-lookup"><span data-stu-id="0eee4-451">The list of parameters the command takes.</span></span> <span data-ttu-id="0eee4-452">Mínimo: 1; máximo: 5</span><span class="sxs-lookup"><span data-stu-id="0eee4-452">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="0eee4-453">String</span><span class="sxs-lookup"><span data-stu-id="0eee4-453">String</span></span>|<span data-ttu-id="0eee4-454">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-454">64 characters</span></span>|<span data-ttu-id="0eee4-455">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-455">✔</span></span>|<span data-ttu-id="0eee4-456">Nombre del parámetro tal como aparece en el cliente.</span><span class="sxs-lookup"><span data-stu-id="0eee4-456">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="0eee4-457">Esto se incluye en la solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="0eee4-457">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="0eee4-458">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-458">String</span></span>|<span data-ttu-id="0eee4-459">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-459">32 characters</span></span>|<span data-ttu-id="0eee4-460">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-460">✔</span></span>|<span data-ttu-id="0eee4-461">Título fácil de usar para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="0eee4-461">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="0eee4-462">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-462">String</span></span>|<span data-ttu-id="0eee4-463">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-463">128 characters</span></span>||<span data-ttu-id="0eee4-464">Cadena fácil de usar que describe el propósito de este parámetro.</span><span class="sxs-lookup"><span data-stu-id="0eee4-464">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="0eee4-465">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-465">String</span></span>|<span data-ttu-id="0eee4-466">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-466">128 characters</span></span>||<span data-ttu-id="0eee4-467">Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-467">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="0eee4-468">Uno de `text` , , , , , , `textarea` `number` `date` `time` `toggle` `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-468">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="0eee4-469">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="0eee4-469">Array of Objects</span></span>|<span data-ttu-id="0eee4-470">10</span><span class="sxs-lookup"><span data-stu-id="0eee4-470">10</span></span>||<span data-ttu-id="0eee4-471">Las opciones de elección para `choiceset` el archivo .</span><span class="sxs-lookup"><span data-stu-id="0eee4-471">The choice options for the `choiceset`.</span></span> <span data-ttu-id="0eee4-472">Use solo cuando `parameter.inputType` es `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-472">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="0eee4-473">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-473">String</span></span>|<span data-ttu-id="0eee4-474">128</span><span class="sxs-lookup"><span data-stu-id="0eee4-474">128</span></span>||<span data-ttu-id="0eee4-475">Título de la elección.</span><span class="sxs-lookup"><span data-stu-id="0eee4-475">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="0eee4-476">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-476">String</span></span>|<span data-ttu-id="0eee4-477">512</span><span class="sxs-lookup"><span data-stu-id="0eee4-477">512</span></span>||<span data-ttu-id="0eee4-478">Valor de la elección.</span><span class="sxs-lookup"><span data-stu-id="0eee4-478">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="0eee4-479">permisos</span><span class="sxs-lookup"><span data-stu-id="0eee4-479">permissions</span></span>

<span data-ttu-id="0eee4-480">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0eee4-480">**Optional**</span></span>

<span data-ttu-id="0eee4-481">Una matriz de la que se especifican los permisos que solicita la aplicación, lo que permite a los usuarios finales saber cómo se llevará a cabo `string` la extensión.</span><span class="sxs-lookup"><span data-stu-id="0eee4-481">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="0eee4-482">Las siguientes opciones no son exclusivas:</span><span class="sxs-lookup"><span data-stu-id="0eee4-482">The following options are non-exclusive:</span></span>

* <span data-ttu-id="0eee4-483">`identity`&emsp;Requiere información de identidad de usuario.</span><span class="sxs-lookup"><span data-stu-id="0eee4-483">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="0eee4-484">`messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="0eee4-484">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="0eee4-485">Al cambiar estos permisos al actualizar la aplicación, los usuarios repetirán el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="0eee4-485">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="0eee4-486">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="0eee4-486">devicePermissions</span></span>

<span data-ttu-id="0eee4-487">**Opcional** Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="0eee4-487">**Optional** Array of Strings</span></span>

<span data-ttu-id="0eee4-488">Especifica las características nativas del dispositivo de un usuario a las que la aplicación puede solicitar acceso.</span><span class="sxs-lookup"><span data-stu-id="0eee4-488">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="0eee4-489">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="0eee4-489">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="0eee4-490">validDomains</span><span class="sxs-lookup"><span data-stu-id="0eee4-490">validDomains</span></span>

<span data-ttu-id="0eee4-491">**Opcional**, excepto **Requerido cuando** se indica</span><span class="sxs-lookup"><span data-stu-id="0eee4-491">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="0eee4-492">Una lista de dominios válidos desde los que la aplicación espera cargar cualquier contenido.</span><span class="sxs-lookup"><span data-stu-id="0eee4-492">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="0eee4-493">Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-493">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="0eee4-494">Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-494">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="0eee4-495">Si la interfaz de usuario de contenido o configuración de pestañas necesita navegar a cualquier otro dominio además del uso para la configuración de pestañas, este dominio debe especificarse aquí.</span><span class="sxs-lookup"><span data-stu-id="0eee4-495">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="0eee4-496">Sin **embargo,** no es necesario incluir los dominios de los proveedores de identidades que quieres admitir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-496">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="0eee4-497">Por ejemplo, para autenticar con un id. de Google, es necesario redirigir a accounts.google.com, pero no debe incluir accounts.google.com en `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-497">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0eee4-498">No agregue dominios que estén fuera del control, ya sea directamente o a través de caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="0eee4-498">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="0eee4-499">Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="0eee4-499">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="0eee4-500">El objeto es una matriz con todos los elementos del tipo `string` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-500">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="0eee4-501">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="0eee4-501">webApplicationInfo</span></span>

<span data-ttu-id="0eee4-502">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0eee4-502">**Optional**</span></span>

<span data-ttu-id="0eee4-503">Especifica tu id. de aplicación de AAD y Graph información para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="0eee4-503">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="0eee4-504">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-504">Name</span></span>| <span data-ttu-id="0eee4-505">Tipo</span><span class="sxs-lookup"><span data-stu-id="0eee4-505">Type</span></span>| <span data-ttu-id="0eee4-506">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-506">Maximum size</span></span> | <span data-ttu-id="0eee4-507">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-507">Required</span></span> | <span data-ttu-id="0eee4-508">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-508">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="0eee4-509">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-509">String</span></span>|<span data-ttu-id="0eee4-510">36 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-510">36 characters</span></span>|<span data-ttu-id="0eee4-511">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-511">✔</span></span>|<span data-ttu-id="0eee4-512">Id. de aplicación de AAD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-512">AAD application id of the app.</span></span> <span data-ttu-id="0eee4-513">Este identificador debe ser un GUID.</span><span class="sxs-lookup"><span data-stu-id="0eee4-513">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="0eee4-514">Cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-514">String</span></span>|<span data-ttu-id="0eee4-515">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0eee4-515">2048 characters</span></span>|<span data-ttu-id="0eee4-516">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-516">✔</span></span>|<span data-ttu-id="0eee4-517">Url de recurso de la aplicación para adquirir token de autenticación para SSO.</span><span class="sxs-lookup"><span data-stu-id="0eee4-517">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="0eee4-518">Matriz</span><span class="sxs-lookup"><span data-stu-id="0eee4-518">Array</span></span>|<span data-ttu-id="0eee4-519">Máximo de 100 elementos</span><span class="sxs-lookup"><span data-stu-id="0eee4-519">Maximum 100 items</span></span>|<span data-ttu-id="0eee4-520">✔</span><span class="sxs-lookup"><span data-stu-id="0eee4-520">✔</span></span>|<span data-ttu-id="0eee4-521">Permisos de recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-521">Resource permissions for application.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="0eee4-522">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="0eee4-522">configurableProperties</span></span>

<span data-ttu-id="0eee4-523">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="0eee4-523">**Optional** - array</span></span>

<span data-ttu-id="0eee4-524">El `configurableProperties` bloque define las propiedades de la aplicación que Teams los administradores pueden personalizar.</span><span class="sxs-lookup"><span data-stu-id="0eee4-524">The `configurableProperties` block defines the app properties that Teams admins can customize.</span></span> <span data-ttu-id="0eee4-525">Para obtener más información, consulta [Habilitar la personalización de la aplicación](~/concepts/design/enable-app-customization.md).</span><span class="sxs-lookup"><span data-stu-id="0eee4-525">For more information, see [enable app customization](~/concepts/design/enable-app-customization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0eee4-526">Debe definirse un mínimo de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="0eee4-526">A minimum of one property must be defined.</span></span> <span data-ttu-id="0eee4-527">Puede definir un máximo de nueve propiedades en este bloque.</span><span class="sxs-lookup"><span data-stu-id="0eee4-527">You can define a maximum of nine properties in this block.</span></span>

<span data-ttu-id="0eee4-528">Puede definir cualquiera de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="0eee4-528">You can define any of the following properties:</span></span>

* <span data-ttu-id="0eee4-529">`name`: nombre para mostrar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-529">`name`: The app's display name.</span></span>
* <span data-ttu-id="0eee4-530">`shortDescription`: descripción breve de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-530">`shortDescription`: The app's short description.</span></span>
* <span data-ttu-id="0eee4-531">`longDescription`: descripción detallada de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-531">`longDescription`: The app's detailed description.</span></span>
* <span data-ttu-id="0eee4-532">`smallImageUrl`: icono de esquema de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-532">`smallImageUrl`: The app's outline icon.</span></span>
* <span data-ttu-id="0eee4-533">`largeImageUrl`: icono de color de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-533">`largeImageUrl`: The app's color icon.</span></span>
* <span data-ttu-id="0eee4-534">`accentColor`: color que se usará junto con y como fondo para los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="0eee4-534">`accentColor`: The color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="0eee4-535">`developerUrl`: la dirección URL HTTPS del sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0eee4-535">`developerUrl`: The HTTPS URL of the developer's website.</span></span>
* <span data-ttu-id="0eee4-536">`privacyUrl`: la dirección URL HTTPS de la directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0eee4-536">`privacyUrl`: The HTTPS URL of the developer's privacy policy.</span></span>
* <span data-ttu-id="0eee4-537">`termsOfUseUrl`: la dirección URL HTTPS de los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0eee4-537">`termsOfUseUrl`: The HTTPS URL of the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="0eee4-538">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="0eee4-538">defaultInstallScope</span></span>

<span data-ttu-id="0eee4-539">**Opcional** : cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-539">**Optional** - string</span></span>

<span data-ttu-id="0eee4-540">Especifica el ámbito de instalación definido para esta aplicación de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0eee4-540">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="0eee4-541">El ámbito definido será la opción que se muestra en el botón cuando un usuario intente agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-541">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="0eee4-542">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="0eee4-542">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="0eee4-543">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="0eee4-543">defaultGroupCapability</span></span>

<span data-ttu-id="0eee4-544">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="0eee4-544">**Optional** - object</span></span>

<span data-ttu-id="0eee4-545">Cuando se selecciona un ámbito de instalación de grupo, se definirá la funcionalidad predeterminada cuando el usuario instale la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eee4-545">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="0eee4-546">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="0eee4-546">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="0eee4-547">Nombre</span><span class="sxs-lookup"><span data-stu-id="0eee4-547">Name</span></span>| <span data-ttu-id="0eee4-548">Tipo</span><span class="sxs-lookup"><span data-stu-id="0eee4-548">Type</span></span>| <span data-ttu-id="0eee4-549">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0eee4-549">Maximum size</span></span> | <span data-ttu-id="0eee4-550">Necesario</span><span class="sxs-lookup"><span data-stu-id="0eee4-550">Required</span></span> | <span data-ttu-id="0eee4-551">Descripción</span><span class="sxs-lookup"><span data-stu-id="0eee4-551">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="0eee4-552">string</span><span class="sxs-lookup"><span data-stu-id="0eee4-552">string</span></span>|||<span data-ttu-id="0eee4-553">Cuando el ámbito de instalación seleccionado es `team` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="0eee4-553">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="0eee4-554">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-554">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="0eee4-555">cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-555">string</span></span>|||<span data-ttu-id="0eee4-556">Cuando el ámbito de instalación seleccionado es `groupchat` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="0eee4-556">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="0eee4-557">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-557">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="0eee4-558">cadena</span><span class="sxs-lookup"><span data-stu-id="0eee4-558">string</span></span>|||<span data-ttu-id="0eee4-559">Cuando el ámbito de instalación seleccionado es `meetings` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="0eee4-559">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="0eee4-560">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="0eee4-560">Options: `tab`, `bot`, or `connector`.</span></span>|
