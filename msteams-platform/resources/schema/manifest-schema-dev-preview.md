---
title: Referencia de esquema de manifiesto de versión preliminar de desarrollador
description: Describe el esquema admitido por el manifiesto para Microsoft Teams
ms.topic: reference
keywords: Vista previa del programador del esquema de manifiesto de teams
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: 333ed556ba8ba59c66f66d7eaa41dd0ea66dca0a
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629868"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="0d480-104">Esquema de manifiesto de vista previa de desarrollador para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0d480-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="0d480-105">Consulta [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) para obtener información sobre el programa y cómo puedes unirte.</span><span class="sxs-lookup"><span data-stu-id="0d480-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="0d480-106">Si no usa la vista previa del desarrollador, no debe usar esta versión del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0d480-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="0d480-107">Vea [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) para la versión pública del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0d480-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="0d480-108">El Microsoft Teams describe cómo se integra la aplicación en el Microsoft Teams producto.</span><span class="sxs-lookup"><span data-stu-id="0d480-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="0d480-109">El manifiesto debe cumplir con el esquema hospedado en [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="0d480-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="0d480-110">Para obtener más información sobre las características disponibles, vea: [Características en public developer preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span><span class="sxs-lookup"><span data-stu-id="0d480-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="0d480-111">Manifiesto completo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0d480-111">Sample full manifest</span></span>

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
     "websiteUrl",
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

<span data-ttu-id="0d480-112">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="0d480-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="0d480-113">$schema</span><span class="sxs-lookup"><span data-stu-id="0d480-113">$schema</span></span>

<span data-ttu-id="0d480-114">*Opcional, pero recomendado* &ndash; String</span><span class="sxs-lookup"><span data-stu-id="0d480-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="0d480-115">La https:// url que hace referencia al esquema JSON para el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0d480-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="0d480-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="0d480-116">manifestVersion</span></span>

<span data-ttu-id="0d480-117">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="0d480-117">**Required** &ndash; String</span></span>

<span data-ttu-id="0d480-118">La versión del esquema de manifiesto que usa este manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0d480-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="0d480-119">Debe ser "devPreview".</span><span class="sxs-lookup"><span data-stu-id="0d480-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="0d480-120">version</span><span class="sxs-lookup"><span data-stu-id="0d480-120">version</span></span>

<span data-ttu-id="0d480-121">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="0d480-121">**Required** &ndash; String</span></span>

<span data-ttu-id="0d480-122">La versión de la aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="0d480-122">The version of the specific app.</span></span> <span data-ttu-id="0d480-123">Si actualiza algo en el manifiesto, la versión también debe incrementarse.</span><span class="sxs-lookup"><span data-stu-id="0d480-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="0d480-124">De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="0d480-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="0d480-125">Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y volver a validarse.</span><span class="sxs-lookup"><span data-stu-id="0d480-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="0d480-126">A continuación, los usuarios de esta aplicación recibirán el nuevo manifiesto actualizado automáticamente en unas pocas horas, después de que se apruebe.</span><span class="sxs-lookup"><span data-stu-id="0d480-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="0d480-127">Si cambian los permisos solicitados por la aplicación, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="0d480-128">Esta cadena de versión debe seguir el [estándar de semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="0d480-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="0d480-129">id</span><span class="sxs-lookup"><span data-stu-id="0d480-129">id</span></span>

<span data-ttu-id="0d480-130">**Obligatorio** &ndash; Id. de aplicación de Microsoft</span><span class="sxs-lookup"><span data-stu-id="0d480-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="0d480-131">Identificador único generado por Microsoft para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="0d480-132">Si has registrado un bot a través del Microsoft Bot Framework o la aplicación web de la pestaña ya inicia sesión con Microsoft, ya debes tener un identificador y debes escribirlo aquí.</span><span class="sxs-lookup"><span data-stu-id="0d480-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="0d480-133">De lo contrario, debe generar un nuevo identificador en el Portal de registro de aplicaciones de Microsoft ([Mis](https://apps.dev.microsoft.com)aplicaciones ), escriba aquí y, a continuación, volver a usarlo cuando [agregue un bot](~/bots/how-to/create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="0d480-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="0d480-134">packageName</span><span class="sxs-lookup"><span data-stu-id="0d480-134">packageName</span></span>

<span data-ttu-id="0d480-135">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="0d480-135">**Required** &ndash; String</span></span>

<span data-ttu-id="0d480-136">Un identificador único para esta aplicación en la notación de dominio inverso; por ejemplo, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="0d480-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="0d480-137">developer</span><span class="sxs-lookup"><span data-stu-id="0d480-137">developer</span></span>

<span data-ttu-id="0d480-138">**Required**</span><span class="sxs-lookup"><span data-stu-id="0d480-138">**Required**</span></span>

<span data-ttu-id="0d480-139">Especifica información sobre su empresa.</span><span class="sxs-lookup"><span data-stu-id="0d480-139">Specifies information about your company.</span></span> <span data-ttu-id="0d480-140">Para las aplicaciones enviadas a AppSource (anteriormente Office Store), estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="0d480-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="0d480-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-141">Name</span></span>| <span data-ttu-id="0d480-142">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-142">Maximum size</span></span> | <span data-ttu-id="0d480-143">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-143">Required</span></span> | <span data-ttu-id="0d480-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="0d480-145">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-145">32 characters</span></span>|<span data-ttu-id="0d480-146">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-146">✔</span></span>|<span data-ttu-id="0d480-147">Nombre para mostrar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0d480-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="0d480-148">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-148">2048 characters</span></span>|<span data-ttu-id="0d480-149">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-149">✔</span></span>|<span data-ttu-id="0d480-150">La https:// url del sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0d480-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="0d480-151">Este vínculo debe llevar a los usuarios a su empresa o página de aterrizaje específica del producto.</span><span class="sxs-lookup"><span data-stu-id="0d480-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="0d480-152">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-152">2048 characters</span></span>|<span data-ttu-id="0d480-153">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-153">✔</span></span>|<span data-ttu-id="0d480-154">La https:// url a la directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0d480-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="0d480-155">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-155">2048 characters</span></span>|<span data-ttu-id="0d480-156">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-156">✔</span></span>|<span data-ttu-id="0d480-157">La https:// url a los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0d480-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="0d480-158">10 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-158">10 characters</span></span>|<span data-ttu-id="0d480-159">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-159">✔</span></span>|<span data-ttu-id="0d480-160">**Opcional** Id. de red de partners de Microsoft que identifica la organización asociada que está creando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="0d480-161">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="0d480-161">localizationInfo</span></span>

<span data-ttu-id="0d480-162">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0d480-162">**Optional**</span></span>

<span data-ttu-id="0d480-163">Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="0d480-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="0d480-164">Vea [localización](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="0d480-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="0d480-165">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-165">Name</span></span>| <span data-ttu-id="0d480-166">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-166">Maximum size</span></span> | <span data-ttu-id="0d480-167">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-167">Required</span></span> | <span data-ttu-id="0d480-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="0d480-169">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-169">4 characters</span></span>|<span data-ttu-id="0d480-170">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-170">✔</span></span>|<span data-ttu-id="0d480-171">La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="0d480-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="0d480-172">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="0d480-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="0d480-173">Una matriz de objetos que especifica traducciones de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="0d480-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="0d480-174">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-174">Name</span></span>| <span data-ttu-id="0d480-175">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-175">Maximum size</span></span> | <span data-ttu-id="0d480-176">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-176">Required</span></span> | <span data-ttu-id="0d480-177">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="0d480-178">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-178">4 characters</span></span>|<span data-ttu-id="0d480-179">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-179">✔</span></span>|<span data-ttu-id="0d480-180">Etiqueta de idioma de las cadenas del archivo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="0d480-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="0d480-181">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-181">4 characters</span></span>|<span data-ttu-id="0d480-182">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-182">✔</span></span>|<span data-ttu-id="0d480-183">Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="0d480-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="0d480-184">name</span><span class="sxs-lookup"><span data-stu-id="0d480-184">name</span></span>

<span data-ttu-id="0d480-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="0d480-185">**Required**</span></span>

<span data-ttu-id="0d480-186">El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="0d480-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="0d480-187">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="0d480-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="0d480-188">Los valores de `short` y no deben ser los `full` mismos.</span><span class="sxs-lookup"><span data-stu-id="0d480-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="0d480-189">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-189">Name</span></span>| <span data-ttu-id="0d480-190">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-190">Maximum size</span></span> | <span data-ttu-id="0d480-191">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-191">Required</span></span> | <span data-ttu-id="0d480-192">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="0d480-193">30 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-193">30 characters</span></span>|<span data-ttu-id="0d480-194">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-194">✔</span></span>|<span data-ttu-id="0d480-195">El nombre para mostrar corto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="0d480-196">100 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-196">100 characters</span></span>||<span data-ttu-id="0d480-197">El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0d480-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="0d480-198">descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-198">description</span></span>

<span data-ttu-id="0d480-199">**Required**</span><span class="sxs-lookup"><span data-stu-id="0d480-199">**Required**</span></span>

<span data-ttu-id="0d480-200">Describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0d480-200">Describes your app to users.</span></span> <span data-ttu-id="0d480-201">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="0d480-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="0d480-202">Asegúrese de que su descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia.</span><span class="sxs-lookup"><span data-stu-id="0d480-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="0d480-203">También debe tener en cuenta, en la descripción completa, si se requiere una cuenta externa para su uso.</span><span class="sxs-lookup"><span data-stu-id="0d480-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="0d480-204">Los valores de `short` y no deben ser los `full` mismos.</span><span class="sxs-lookup"><span data-stu-id="0d480-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="0d480-205">La descripción breve no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="0d480-206">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-206">Name</span></span>| <span data-ttu-id="0d480-207">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-207">Maximum size</span></span> | <span data-ttu-id="0d480-208">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-208">Required</span></span> | <span data-ttu-id="0d480-209">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="0d480-210">80 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-210">80 characters</span></span>|<span data-ttu-id="0d480-211">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-211">✔</span></span>|<span data-ttu-id="0d480-212">Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.</span><span class="sxs-lookup"><span data-stu-id="0d480-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="0d480-213">4000 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-213">4000 characters</span></span>|<span data-ttu-id="0d480-214">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-214">✔</span></span>|<span data-ttu-id="0d480-215">Descripción completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="0d480-216">iconos</span><span class="sxs-lookup"><span data-stu-id="0d480-216">icons</span></span>

<span data-ttu-id="0d480-217">**Required**</span><span class="sxs-lookup"><span data-stu-id="0d480-217">**Required**</span></span>

<span data-ttu-id="0d480-218">Iconos usados dentro de la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-218">Icons used within the Teams app.</span></span> <span data-ttu-id="0d480-219">Los archivos de icono deben incluirse como parte del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="0d480-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="0d480-220">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-220">Name</span></span>| <span data-ttu-id="0d480-221">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-221">Maximum size</span></span> | <span data-ttu-id="0d480-222">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-222">Required</span></span> | <span data-ttu-id="0d480-223">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="0d480-224">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-224">2048 characters</span></span>|<span data-ttu-id="0d480-225">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-225">✔</span></span>|<span data-ttu-id="0d480-226">Una ruta de acceso de archivo relativa a un icono de esquema PNG transparente de 32 x 32.</span><span class="sxs-lookup"><span data-stu-id="0d480-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="0d480-227">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-227">2048 characters</span></span>|<span data-ttu-id="0d480-228">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-228">✔</span></span>|<span data-ttu-id="0d480-229">Una ruta de acceso de archivo relativa a un icono PNG de color completo de 192 x 192.</span><span class="sxs-lookup"><span data-stu-id="0d480-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="0d480-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="0d480-230">accentColor</span></span>

<span data-ttu-id="0d480-231">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="0d480-231">**Required** &ndash; String</span></span>

<span data-ttu-id="0d480-232">Color que se usará junto con y como fondo para los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="0d480-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="0d480-233">El valor debe ser un código de color HTML válido a partir de '#', por ejemplo `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="0d480-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="0d480-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="0d480-234">configurableTabs</span></span>

<span data-ttu-id="0d480-235">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0d480-235">**Optional**</span></span>

<span data-ttu-id="0d480-236">Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de grupo que requiere una configuración adicional antes de agregarla.</span><span class="sxs-lookup"><span data-stu-id="0d480-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="0d480-237">Las pestañas configurables solo se admiten en el ámbito de teams y actualmente solo se admite una pestaña por aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="0d480-238">El objeto es una matriz con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="0d480-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="0d480-239">Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña de canal configurable.</span><span class="sxs-lookup"><span data-stu-id="0d480-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="0d480-240">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-240">Name</span></span>| <span data-ttu-id="0d480-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d480-241">Type</span></span>| <span data-ttu-id="0d480-242">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-242">Maximum size</span></span> | <span data-ttu-id="0d480-243">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-243">Required</span></span> | <span data-ttu-id="0d480-244">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="0d480-245">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-245">String</span></span>|<span data-ttu-id="0d480-246">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-246">2048 characters</span></span>|<span data-ttu-id="0d480-247">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-247">✔</span></span>|<span data-ttu-id="0d480-248">La https:// url que se va a usar al configurar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0d480-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="0d480-249">Booleano</span><span class="sxs-lookup"><span data-stu-id="0d480-249">Boolean</span></span>|||<span data-ttu-id="0d480-250">Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de su creación.</span><span class="sxs-lookup"><span data-stu-id="0d480-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="0d480-251">Valor predeterminado: `true`</span><span class="sxs-lookup"><span data-stu-id="0d480-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="0d480-252">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0d480-252">Array of enum</span></span>|<span data-ttu-id="0d480-253">1</span><span class="sxs-lookup"><span data-stu-id="0d480-253">1</span></span>|<span data-ttu-id="0d480-254">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-254">✔</span></span>|<span data-ttu-id="0d480-255">Actualmente, las pestañas configurables solo admiten `team` los `groupchat` ámbitos y.</span><span class="sxs-lookup"><span data-stu-id="0d480-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="0d480-256">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-256">String</span></span>|<span data-ttu-id="0d480-257">2048</span><span class="sxs-lookup"><span data-stu-id="0d480-257">2048</span></span>||<span data-ttu-id="0d480-258">Una ruta de acceso de archivo relativa a una imagen de vista previa de tabulación para su uso en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0d480-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="0d480-259">Tamaño 1024x768.</span><span class="sxs-lookup"><span data-stu-id="0d480-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="0d480-260">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0d480-260">Array of enum</span></span>|<span data-ttu-id="0d480-261">1</span><span class="sxs-lookup"><span data-stu-id="0d480-261">1</span></span>||<span data-ttu-id="0d480-262">Define cómo la pestaña estará disponible en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0d480-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="0d480-263">Las opciones son `sharePointFullPage` y `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="0d480-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="0d480-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="0d480-264">staticTabs</span></span>

<span data-ttu-id="0d480-265">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0d480-265">**Optional**</span></span>

<span data-ttu-id="0d480-266">Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente.</span><span class="sxs-lookup"><span data-stu-id="0d480-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="0d480-267">Las pestañas estáticas declaradas en el ámbito siempre se anclan a la experiencia `personal` personal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="0d480-268">Actualmente no se admiten las pestañas estáticas declaradas `team` en el ámbito.</span><span class="sxs-lookup"><span data-stu-id="0d480-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="0d480-269">El objeto es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="0d480-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="0d480-270">Este bloque solo es necesario para las soluciones que proporcionan una solución de tabulación estática.</span><span class="sxs-lookup"><span data-stu-id="0d480-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="0d480-271">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-271">Name</span></span>| <span data-ttu-id="0d480-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d480-272">Type</span></span>| <span data-ttu-id="0d480-273">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-273">Maximum size</span></span> | <span data-ttu-id="0d480-274">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-274">Required</span></span> | <span data-ttu-id="0d480-275">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="0d480-276">String</span><span class="sxs-lookup"><span data-stu-id="0d480-276">String</span></span>|<span data-ttu-id="0d480-277">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-277">64 characters</span></span>|<span data-ttu-id="0d480-278">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-278">✔</span></span>|<span data-ttu-id="0d480-279">Identificador único para la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="0d480-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="0d480-280">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-280">String</span></span>|<span data-ttu-id="0d480-281">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-281">128 characters</span></span>|<span data-ttu-id="0d480-282">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-282">✔</span></span>|<span data-ttu-id="0d480-283">Nombre para mostrar de la pestaña en la interfaz de canal.</span><span class="sxs-lookup"><span data-stu-id="0d480-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="0d480-284">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-284">String</span></span>|<span data-ttu-id="0d480-285">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-285">2048 characters</span></span>|<span data-ttu-id="0d480-286">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-286">✔</span></span>|<span data-ttu-id="0d480-287">Dirección URL https:// que apunta a la interfaz de usuario de la entidad que se va a mostrar en el Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="0d480-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="0d480-288">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-288">String</span></span>|<span data-ttu-id="0d480-289">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-289">2048 characters</span></span>||<span data-ttu-id="0d480-290">La https:// dirección URL para apuntar si un usuario opta por ver en un explorador.</span><span class="sxs-lookup"><span data-stu-id="0d480-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="0d480-291">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0d480-291">Array of enum</span></span>|<span data-ttu-id="0d480-292">1</span><span class="sxs-lookup"><span data-stu-id="0d480-292">1</span></span>|<span data-ttu-id="0d480-293">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-293">✔</span></span>|<span data-ttu-id="0d480-294">Actualmente, las pestañas estáticas solo admiten el ámbito, lo que significa que solo se puede aprovisionar como `personal` parte de la experiencia personal.</span><span class="sxs-lookup"><span data-stu-id="0d480-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="0d480-295">bots</span><span class="sxs-lookup"><span data-stu-id="0d480-295">bots</span></span>

<span data-ttu-id="0d480-296">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0d480-296">**Optional**</span></span>

<span data-ttu-id="0d480-297">Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="0d480-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="0d480-298">El objeto es una matriz (máximo de solo 1 elemento actualmente solo se permite un bot por aplicación) con todos los &mdash; elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="0d480-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="0d480-299">Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.</span><span class="sxs-lookup"><span data-stu-id="0d480-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="0d480-300">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-300">Name</span></span>| <span data-ttu-id="0d480-301">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d480-301">Type</span></span>| <span data-ttu-id="0d480-302">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-302">Maximum size</span></span> | <span data-ttu-id="0d480-303">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-303">Required</span></span> | <span data-ttu-id="0d480-304">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="0d480-305">String</span><span class="sxs-lookup"><span data-stu-id="0d480-305">String</span></span>|<span data-ttu-id="0d480-306">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-306">64 characters</span></span>|<span data-ttu-id="0d480-307">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-307">✔</span></span>|<span data-ttu-id="0d480-308">El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="0d480-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="0d480-309">Esto bien puede ser el mismo que el identificador general [de la aplicación](#id).</span><span class="sxs-lookup"><span data-stu-id="0d480-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="0d480-310">Booleano</span><span class="sxs-lookup"><span data-stu-id="0d480-310">Boolean</span></span>|||<span data-ttu-id="0d480-311">Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico.</span><span class="sxs-lookup"><span data-stu-id="0d480-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="0d480-312">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="0d480-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="0d480-313">Booleano</span><span class="sxs-lookup"><span data-stu-id="0d480-313">Boolean</span></span>|||<span data-ttu-id="0d480-314">Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación.</span><span class="sxs-lookup"><span data-stu-id="0d480-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="0d480-315">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="0d480-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="0d480-316">Booleano</span><span class="sxs-lookup"><span data-stu-id="0d480-316">Boolean</span></span>|||<span data-ttu-id="0d480-317">Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal.</span><span class="sxs-lookup"><span data-stu-id="0d480-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="0d480-318">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="0d480-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="0d480-319">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0d480-319">Array of enum</span></span>|<span data-ttu-id="0d480-320">3</span><span class="sxs-lookup"><span data-stu-id="0d480-320">3</span></span>|<span data-ttu-id="0d480-321">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-321">✔</span></span>|<span data-ttu-id="0d480-322">Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`).</span><span class="sxs-lookup"><span data-stu-id="0d480-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="0d480-323">Estas opciones no son exclusivas.</span><span class="sxs-lookup"><span data-stu-id="0d480-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="0d480-324">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="0d480-324">bots.commandLists</span></span>

<span data-ttu-id="0d480-325">Una lista opcional de comandos que el bot puede recomendar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0d480-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="0d480-326">El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de comandos independiente para cada ámbito compatible `object` con el bot.</span><span class="sxs-lookup"><span data-stu-id="0d480-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="0d480-327">Para obtener más información, vea [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span><span class="sxs-lookup"><span data-stu-id="0d480-327">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="0d480-328">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-328">Name</span></span>| <span data-ttu-id="0d480-329">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d480-329">Type</span></span>| <span data-ttu-id="0d480-330">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-330">Maximum size</span></span> | <span data-ttu-id="0d480-331">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-331">Required</span></span> | <span data-ttu-id="0d480-332">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="0d480-333">matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0d480-333">array of enum</span></span>|<span data-ttu-id="0d480-334">3</span><span class="sxs-lookup"><span data-stu-id="0d480-334">3</span></span>|<span data-ttu-id="0d480-335">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-335">✔</span></span>|<span data-ttu-id="0d480-336">Especifica el ámbito para el que la lista de comandos es válida.</span><span class="sxs-lookup"><span data-stu-id="0d480-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="0d480-337">Las opciones son `team`, `personal` y `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="0d480-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="0d480-338">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="0d480-338">array of objects</span></span>|<span data-ttu-id="0d480-339">10</span><span class="sxs-lookup"><span data-stu-id="0d480-339">10</span></span>|<span data-ttu-id="0d480-340">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-340">✔</span></span>|<span data-ttu-id="0d480-341">Una matriz de comandos que el bot admite:</span><span class="sxs-lookup"><span data-stu-id="0d480-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="0d480-342">`title`: el nombre del comando bot (cadena, 32).</span><span class="sxs-lookup"><span data-stu-id="0d480-342">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="0d480-343">`description`: una descripción sencilla o un ejemplo de la sintaxis del comando y su argumento (cadena, 128).</span><span class="sxs-lookup"><span data-stu-id="0d480-343">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="0d480-344">conectores</span><span class="sxs-lookup"><span data-stu-id="0d480-344">connectors</span></span>

<span data-ttu-id="0d480-345">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0d480-345">**Optional**</span></span>

<span data-ttu-id="0d480-346">El `connectors` bloque define un Office 365 connector para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="0d480-347">El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="0d480-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="0d480-348">Este bloque solo es necesario para las soluciones que proporcionan un conector.</span><span class="sxs-lookup"><span data-stu-id="0d480-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="0d480-349">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-349">Name</span></span>| <span data-ttu-id="0d480-350">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d480-350">Type</span></span>| <span data-ttu-id="0d480-351">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-351">Maximum size</span></span> | <span data-ttu-id="0d480-352">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-352">Required</span></span> | <span data-ttu-id="0d480-353">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="0d480-354">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-354">String</span></span>|<span data-ttu-id="0d480-355">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-355">2048 characters</span></span>|<span data-ttu-id="0d480-356">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-356">✔</span></span>|<span data-ttu-id="0d480-357">La https:// url que se va a usar al configurar el conector.</span><span class="sxs-lookup"><span data-stu-id="0d480-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="0d480-358">String</span><span class="sxs-lookup"><span data-stu-id="0d480-358">String</span></span>|<span data-ttu-id="0d480-359">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-359">64 characters</span></span>|<span data-ttu-id="0d480-360">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-360">✔</span></span>|<span data-ttu-id="0d480-361">Identificador único del conector que coincide con su identificador en el [Panel de desarrolladores de conectores.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="0d480-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="0d480-362">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="0d480-362">Array of enum</span></span>|<span data-ttu-id="0d480-363">1</span><span class="sxs-lookup"><span data-stu-id="0d480-363">1</span></span>|<span data-ttu-id="0d480-364">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-364">✔</span></span>|<span data-ttu-id="0d480-365">Especifica si connector ofrece una experiencia en el contexto de un canal en un , o una experiencia ámbito a un `team` usuario individual solo ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="0d480-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="0d480-366">Actualmente, solo se `team` admite el ámbito.</span><span class="sxs-lookup"><span data-stu-id="0d480-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="0d480-367">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="0d480-367">composeExtensions</span></span>

<span data-ttu-id="0d480-368">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0d480-368">**Optional**</span></span>

<span data-ttu-id="0d480-369">Define una extensión de mensajería para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="0d480-370">El nombre de la característica se cambió de "extensión de redacción" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="0d480-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="0d480-371">El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="0d480-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="0d480-372">Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0d480-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="0d480-373">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-373">Name</span></span>| <span data-ttu-id="0d480-374">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d480-374">Type</span></span> | <span data-ttu-id="0d480-375">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-375">Maximum Size</span></span> | <span data-ttu-id="0d480-376">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0d480-376">Required</span></span> | <span data-ttu-id="0d480-377">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="0d480-378">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-378">String</span></span>|<span data-ttu-id="0d480-379">64</span><span class="sxs-lookup"><span data-stu-id="0d480-379">64</span></span>|<span data-ttu-id="0d480-380">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-380">✔</span></span>|<span data-ttu-id="0d480-381">El identificador único de la aplicación de Microsoft para el bot que hace una copia de seguridad de la extensión de mensajería, tal como se registró con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="0d480-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="0d480-382">Esto bien puede ser el mismo que el identificador general [de la aplicación](#id).</span><span class="sxs-lookup"><span data-stu-id="0d480-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="0d480-383">Booleano</span><span class="sxs-lookup"><span data-stu-id="0d480-383">Boolean</span></span>|||<span data-ttu-id="0d480-384">Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0d480-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="0d480-385">El valor predeterminado es `false`.</span><span class="sxs-lookup"><span data-stu-id="0d480-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="0d480-386">Matriz de objeto</span><span class="sxs-lookup"><span data-stu-id="0d480-386">Array of object</span></span>|<span data-ttu-id="0d480-387">10</span><span class="sxs-lookup"><span data-stu-id="0d480-387">10</span></span>|<span data-ttu-id="0d480-388">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-388">✔</span></span>|<span data-ttu-id="0d480-389">Matriz de comandos que admite la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="0d480-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="0d480-390">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="0d480-390">composeExtensions.commands</span></span>

<span data-ttu-id="0d480-391">La extensión de mensajería debe declarar uno o más comandos.</span><span class="sxs-lookup"><span data-stu-id="0d480-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="0d480-392">Cada comando aparece en Microsoft Teams como una interacción potencial desde el punto de entrada basado en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="0d480-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="0d480-393">Hay un máximo de 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="0d480-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="0d480-394">Cada elemento de comando es un objeto con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="0d480-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="0d480-395">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-395">Name</span></span>| <span data-ttu-id="0d480-396">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d480-396">Type</span></span>| <span data-ttu-id="0d480-397">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-397">Maximum size</span></span> | <span data-ttu-id="0d480-398">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-398">Required</span></span> | <span data-ttu-id="0d480-399">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="0d480-400">String</span><span class="sxs-lookup"><span data-stu-id="0d480-400">String</span></span>|<span data-ttu-id="0d480-401">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-401">64 characters</span></span>|<span data-ttu-id="0d480-402">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-402">✔</span></span>|<span data-ttu-id="0d480-403">El identificador del comando.</span><span class="sxs-lookup"><span data-stu-id="0d480-403">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="0d480-404">String</span><span class="sxs-lookup"><span data-stu-id="0d480-404">String</span></span>|<span data-ttu-id="0d480-405">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-405">64 characters</span></span>||<span data-ttu-id="0d480-406">Tipo del comando.</span><span class="sxs-lookup"><span data-stu-id="0d480-406">Type of the command.</span></span> <span data-ttu-id="0d480-407">Uno de `query` o `action` .</span><span class="sxs-lookup"><span data-stu-id="0d480-407">One of `query` or `action`.</span></span> <span data-ttu-id="0d480-408">Valor predeterminado: `query`</span><span class="sxs-lookup"><span data-stu-id="0d480-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="0d480-409">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-409">String</span></span>|<span data-ttu-id="0d480-410">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-410">32 characters</span></span>|<span data-ttu-id="0d480-411">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-411">✔</span></span>|<span data-ttu-id="0d480-412">Nombre de comando fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="0d480-412">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="0d480-413">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-413">String</span></span>|<span data-ttu-id="0d480-414">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-414">128 characters</span></span>||<span data-ttu-id="0d480-415">La descripción que se muestra a los usuarios para indicar el propósito de este comando.</span><span class="sxs-lookup"><span data-stu-id="0d480-415">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="0d480-416">Booleano</span><span class="sxs-lookup"><span data-stu-id="0d480-416">Boolean</span></span>|||<span data-ttu-id="0d480-417">Valor booleano que indica si el comando debe ejecutarse inicialmente sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="0d480-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="0d480-418">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="0d480-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="0d480-419">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="0d480-419">Array of Strings</span></span>|<span data-ttu-id="0d480-420">3</span><span class="sxs-lookup"><span data-stu-id="0d480-420">3</span></span>||<span data-ttu-id="0d480-421">Define desde dónde se puede invocar la extensión de mensaje.</span><span class="sxs-lookup"><span data-stu-id="0d480-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="0d480-422">Cualquier combinación de `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="0d480-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="0d480-423">El valor predeterminado es `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="0d480-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="0d480-424">Booleano</span><span class="sxs-lookup"><span data-stu-id="0d480-424">Boolean</span></span>|||<span data-ttu-id="0d480-425">Valor booleano que indica si debe capturar el módulo de tareas dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="0d480-425">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="0d480-426">Objeto</span><span class="sxs-lookup"><span data-stu-id="0d480-426">Object</span></span>|||<span data-ttu-id="0d480-427">Especifique el módulo de tareas que se debe precargar al usar un comando de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0d480-427">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="0d480-428">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-428">String</span></span>|<span data-ttu-id="0d480-429">64</span><span class="sxs-lookup"><span data-stu-id="0d480-429">64</span></span>||<span data-ttu-id="0d480-430">Título del cuadro de diálogo inicial.</span><span class="sxs-lookup"><span data-stu-id="0d480-430">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="0d480-431">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-431">String</span></span>|||<span data-ttu-id="0d480-432">Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="0d480-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="0d480-433">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-433">String</span></span>|||<span data-ttu-id="0d480-434">Alto del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="0d480-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="0d480-435">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-435">String</span></span>|||<span data-ttu-id="0d480-436">Dirección URL de vista web inicial.</span><span class="sxs-lookup"><span data-stu-id="0d480-436">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="0d480-437">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="0d480-437">Array of Objects</span></span>|<span data-ttu-id="0d480-438">5 </span><span class="sxs-lookup"><span data-stu-id="0d480-438">5</span></span>||<span data-ttu-id="0d480-439">Una lista de controladores que permiten invocar aplicaciones cuando se cumplen determinadas condiciones.</span><span class="sxs-lookup"><span data-stu-id="0d480-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="0d480-440">Los dominios también deben aparecer en `validDomains` .</span><span class="sxs-lookup"><span data-stu-id="0d480-440">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="0d480-441">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-441">String</span></span>|||<span data-ttu-id="0d480-442">El tipo de controlador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="0d480-442">The type of message handler.</span></span> <span data-ttu-id="0d480-443">Debe ser `"link"`.</span><span class="sxs-lookup"><span data-stu-id="0d480-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="0d480-444">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="0d480-444">Array of Strings</span></span>|||<span data-ttu-id="0d480-445">Matriz de dominios para los que se puede registrar el controlador de mensajes de vínculo.</span><span class="sxs-lookup"><span data-stu-id="0d480-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="0d480-446">Matriz de objeto</span><span class="sxs-lookup"><span data-stu-id="0d480-446">Array of object</span></span>|<span data-ttu-id="0d480-447">5 </span><span class="sxs-lookup"><span data-stu-id="0d480-447">5</span></span>|<span data-ttu-id="0d480-448">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-448">✔</span></span>|<span data-ttu-id="0d480-449">La lista de parámetros que toma el comando.</span><span class="sxs-lookup"><span data-stu-id="0d480-449">The list of parameters the command takes.</span></span> <span data-ttu-id="0d480-450">Mínimo: 1; máximo: 5</span><span class="sxs-lookup"><span data-stu-id="0d480-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="0d480-451">String</span><span class="sxs-lookup"><span data-stu-id="0d480-451">String</span></span>|<span data-ttu-id="0d480-452">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-452">64 characters</span></span>|<span data-ttu-id="0d480-453">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-453">✔</span></span>|<span data-ttu-id="0d480-454">Nombre del parámetro tal como aparece en el cliente.</span><span class="sxs-lookup"><span data-stu-id="0d480-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="0d480-455">Esto se incluye en la solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="0d480-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="0d480-456">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-456">String</span></span>|<span data-ttu-id="0d480-457">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-457">32 characters</span></span>|<span data-ttu-id="0d480-458">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-458">✔</span></span>|<span data-ttu-id="0d480-459">Título fácil de usar para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="0d480-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="0d480-460">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-460">String</span></span>|<span data-ttu-id="0d480-461">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-461">128 characters</span></span>||<span data-ttu-id="0d480-462">Cadena fácil de usar que describe el propósito de este parámetro.</span><span class="sxs-lookup"><span data-stu-id="0d480-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="0d480-463">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-463">String</span></span>|<span data-ttu-id="0d480-464">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-464">128 characters</span></span>||<span data-ttu-id="0d480-465">Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="0d480-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="0d480-466">Uno de `text` , , , , , , `textarea` `number` `date` `time` `toggle` `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="0d480-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="0d480-467">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="0d480-467">Array of Objects</span></span>|<span data-ttu-id="0d480-468">10</span><span class="sxs-lookup"><span data-stu-id="0d480-468">10</span></span>||<span data-ttu-id="0d480-469">Las opciones de elección para `choiceset` el archivo .</span><span class="sxs-lookup"><span data-stu-id="0d480-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="0d480-470">Use solo cuando `parameter.inputType` es `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="0d480-470">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="0d480-471">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-471">String</span></span>|<span data-ttu-id="0d480-472">128</span><span class="sxs-lookup"><span data-stu-id="0d480-472">128</span></span>||<span data-ttu-id="0d480-473">Título de la elección.</span><span class="sxs-lookup"><span data-stu-id="0d480-473">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="0d480-474">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-474">String</span></span>|<span data-ttu-id="0d480-475">512</span><span class="sxs-lookup"><span data-stu-id="0d480-475">512</span></span>||<span data-ttu-id="0d480-476">Valor de la elección.</span><span class="sxs-lookup"><span data-stu-id="0d480-476">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="0d480-477">permisos</span><span class="sxs-lookup"><span data-stu-id="0d480-477">permissions</span></span>

<span data-ttu-id="0d480-478">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0d480-478">**Optional**</span></span>

<span data-ttu-id="0d480-479">Una matriz de la que se especifican los permisos que solicita la aplicación, lo que permite a los usuarios finales saber cómo se llevará a cabo `string` la extensión.</span><span class="sxs-lookup"><span data-stu-id="0d480-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="0d480-480">Las siguientes opciones no son exclusivas:</span><span class="sxs-lookup"><span data-stu-id="0d480-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="0d480-481">`identity`&emsp;Requiere información de identidad de usuario.</span><span class="sxs-lookup"><span data-stu-id="0d480-481">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="0d480-482">`messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="0d480-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="0d480-483">Al cambiar estos permisos al actualizar la aplicación, los usuarios repetirán el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="0d480-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="0d480-484">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="0d480-484">devicePermissions</span></span>

<span data-ttu-id="0d480-485">**Opcional** Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="0d480-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="0d480-486">Especifica las características nativas del dispositivo de un usuario a las que la aplicación puede solicitar acceso.</span><span class="sxs-lookup"><span data-stu-id="0d480-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="0d480-487">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="0d480-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="0d480-488">validDomains</span><span class="sxs-lookup"><span data-stu-id="0d480-488">validDomains</span></span>

<span data-ttu-id="0d480-489">**Opcional**, excepto **Requerido cuando** se indica</span><span class="sxs-lookup"><span data-stu-id="0d480-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="0d480-490">Una lista de dominios válidos desde los que la aplicación espera cargar cualquier contenido.</span><span class="sxs-lookup"><span data-stu-id="0d480-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="0d480-491">Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="0d480-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="0d480-492">Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="0d480-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="0d480-493">Si la interfaz de usuario de contenido o configuración de pestañas necesita navegar a cualquier otro dominio además del uso para la configuración de pestañas, este dominio debe especificarse aquí.</span><span class="sxs-lookup"><span data-stu-id="0d480-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="0d480-494">Sin **embargo,** no es necesario incluir los dominios de los proveedores de identidades que quieres admitir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="0d480-495">Por ejemplo, para autenticar con un id. de Google, es necesario redirigir a accounts.google.com, pero no debe incluir accounts.google.com en `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="0d480-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d480-496">No agregue dominios que estén fuera del control, ya sea directamente o a través de caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="0d480-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="0d480-497">Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="0d480-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="0d480-498">El objeto es una matriz con todos los elementos del tipo `string` .</span><span class="sxs-lookup"><span data-stu-id="0d480-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="0d480-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="0d480-499">webApplicationInfo</span></span>

<span data-ttu-id="0d480-500">**Optional**</span><span class="sxs-lookup"><span data-stu-id="0d480-500">**Optional**</span></span>

<span data-ttu-id="0d480-501">Especifica tu id. de aplicación de AAD y Graph información para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="0d480-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="0d480-502">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-502">Name</span></span>| <span data-ttu-id="0d480-503">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d480-503">Type</span></span>| <span data-ttu-id="0d480-504">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-504">Maximum size</span></span> | <span data-ttu-id="0d480-505">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-505">Required</span></span> | <span data-ttu-id="0d480-506">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="0d480-507">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-507">String</span></span>|<span data-ttu-id="0d480-508">36 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-508">36 characters</span></span>|<span data-ttu-id="0d480-509">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-509">✔</span></span>|<span data-ttu-id="0d480-510">Id. de aplicación de AAD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-510">AAD application id of the app.</span></span> <span data-ttu-id="0d480-511">Este identificador debe ser un GUID.</span><span class="sxs-lookup"><span data-stu-id="0d480-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="0d480-512">Cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-512">String</span></span>|<span data-ttu-id="0d480-513">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="0d480-513">2048 characters</span></span>|<span data-ttu-id="0d480-514">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-514">✔</span></span>|<span data-ttu-id="0d480-515">Url de recurso de la aplicación para adquirir token de autenticación para SSO.</span><span class="sxs-lookup"><span data-stu-id="0d480-515">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="0d480-516">Matriz</span><span class="sxs-lookup"><span data-stu-id="0d480-516">Array</span></span>|<span data-ttu-id="0d480-517">Máximo de 100 elementos</span><span class="sxs-lookup"><span data-stu-id="0d480-517">Maximum 100 items</span></span>|<span data-ttu-id="0d480-518">✔</span><span class="sxs-lookup"><span data-stu-id="0d480-518">✔</span></span>|<span data-ttu-id="0d480-519">Permisos de recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-519">Resource permissions for application.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="0d480-520">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="0d480-520">configurableProperties</span></span>

<span data-ttu-id="0d480-521">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="0d480-521">**Optional** - array</span></span>

<span data-ttu-id="0d480-522">El `configurableProperties` bloque define las propiedades de la aplicación que Teams puede personalizar el administrador.</span><span class="sxs-lookup"><span data-stu-id="0d480-522">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="0d480-523">Para obtener más información, consulta [Personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="0d480-523">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="0d480-524">Debe definirse un mínimo de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="0d480-524">A minimum of one property must be defined.</span></span> <span data-ttu-id="0d480-525">Puede definir un máximo de nueve propiedades en este bloque.</span><span class="sxs-lookup"><span data-stu-id="0d480-525">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="0d480-526">Como práctica recomendada, debes proporcionar directrices de personalización para que los usuarios de la aplicación y los clientes puedan seguir al personalizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-526">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> 

<span data-ttu-id="0d480-527">Puede definir cualquiera de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="0d480-527">You can define any of the following properties:</span></span>
* <span data-ttu-id="0d480-528">`name`: permite al administrador cambiar el nombre para mostrar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-528">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="0d480-529">`shortDescription`: permite al administrador cambiar la descripción breve de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-529">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="0d480-530">`longDescription`: permite al administrador cambiar la descripción detallada de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-530">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="0d480-531">`smallImageUrl`: es la `outline` propiedad del bloque del `icons` manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0d480-531">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="0d480-532">`largeImageUrl`: es la `color` propiedad del bloque del `icons` manifiesto.</span><span class="sxs-lookup"><span data-stu-id="0d480-532">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="0d480-533">`accentColor`: es el color que se debe usar junto con y como fondo para los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="0d480-533">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="0d480-534">`websiteUrl`: es la dirección HTTPS:// url del sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0d480-534">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="0d480-535">`privacyUrl`: es la dirección URL https:// a la directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0d480-535">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="0d480-536">`termsOfUseUrl`: es la dirección URL https:// los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="0d480-536">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="0d480-537">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="0d480-537">defaultInstallScope</span></span>

<span data-ttu-id="0d480-538">**Opcional** : cadena</span><span class="sxs-lookup"><span data-stu-id="0d480-538">**Optional** - string</span></span>

<span data-ttu-id="0d480-539">Especifica el ámbito de instalación definido para esta aplicación de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0d480-539">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="0d480-540">El ámbito definido será la opción que se muestra en el botón cuando un usuario intente agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-540">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="0d480-541">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="0d480-541">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="0d480-542">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="0d480-542">defaultGroupCapability</span></span>

<span data-ttu-id="0d480-543">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="0d480-543">**Optional** - object</span></span>

<span data-ttu-id="0d480-544">Cuando se selecciona un ámbito de instalación de grupo, se definirá la funcionalidad predeterminada cuando el usuario instale la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d480-544">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="0d480-545">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="0d480-545">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="0d480-546">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d480-546">Name</span></span>| <span data-ttu-id="0d480-547">Tipo</span><span class="sxs-lookup"><span data-stu-id="0d480-547">Type</span></span>| <span data-ttu-id="0d480-548">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="0d480-548">Maximum size</span></span> | <span data-ttu-id="0d480-549">Necesario</span><span class="sxs-lookup"><span data-stu-id="0d480-549">Required</span></span> | <span data-ttu-id="0d480-550">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d480-550">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="0d480-551">string</span><span class="sxs-lookup"><span data-stu-id="0d480-551">string</span></span>|||<span data-ttu-id="0d480-552">Cuando el ámbito de instalación seleccionado es `team` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="0d480-552">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="0d480-553">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="0d480-553">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="0d480-554">string</span><span class="sxs-lookup"><span data-stu-id="0d480-554">string</span></span>|||<span data-ttu-id="0d480-555">Cuando el ámbito de instalación seleccionado es `groupchat` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="0d480-555">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="0d480-556">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="0d480-556">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="0d480-557">string</span><span class="sxs-lookup"><span data-stu-id="0d480-557">string</span></span>|||<span data-ttu-id="0d480-558">Cuando el ámbito de instalación seleccionado es `meetings` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="0d480-558">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="0d480-559">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="0d480-559">Options: `tab`, `bot`, or `connector`.</span></span>|

