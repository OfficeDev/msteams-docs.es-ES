---
title: Referencia de esquema de manifiesto de versión preliminar de desarrollador
description: Describe el esquema admitido por el manifiesto para Microsoft Teams
ms.topic: reference
keywords: Vista previa del programador del esquema de manifiesto de teams
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: c2009038341a22664b0f055fa9756a9d1eba87b9
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915093"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="a5104-104">Esquema de manifiesto de vista previa de desarrollador para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a5104-104">Developer preview manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="a5104-105">Para obtener información sobre cómo habilitar la vista previa del desarrollador, vea [public developer preview for Microsoft Teams](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="a5104-105">For information on how to enable developer preview, see [public developer preview for Microsoft Teams](~/resources/dev-preview/developer-preview-intro.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="a5104-106">Si no estás usando las características de vista previa del desarrollador, usa el manifiesto de la aplicación [para las características de GA](~/resources/schema/manifest-schema.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="a5104-106">If you aren't using developer preview features, use the [app manifest for GA features](~/resources/schema/manifest-schema.md) instead.</span></span>

<span data-ttu-id="a5104-107">El Microsoft Teams describe cómo se integra la aplicación en el Microsoft Teams producto.</span><span class="sxs-lookup"><span data-stu-id="a5104-107">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="a5104-108">El manifiesto debe cumplir con el esquema hospedado en [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="a5104-108">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="a5104-109">Para obtener más información sobre las características disponibles, vea: [Características en public developer preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span><span class="sxs-lookup"><span data-stu-id="a5104-109">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="a5104-110">Manifiesto completo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a5104-110">Sample full manifest</span></span>

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

<span data-ttu-id="a5104-111">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="a5104-111">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="a5104-112">$schema</span><span class="sxs-lookup"><span data-stu-id="a5104-112">$schema</span></span>

<span data-ttu-id="a5104-113">*Opcional, pero recomendado* &ndash; String</span><span class="sxs-lookup"><span data-stu-id="a5104-113">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="a5104-114">La https:// url que hace referencia al esquema JSON para el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="a5104-114">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="a5104-115">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="a5104-115">manifestVersion</span></span>

<span data-ttu-id="a5104-116">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="a5104-116">**Required** &ndash; String</span></span>

<span data-ttu-id="a5104-117">La versión del esquema de manifiesto que usa este manifiesto.</span><span class="sxs-lookup"><span data-stu-id="a5104-117">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="a5104-118">Debe ser "devPreview".</span><span class="sxs-lookup"><span data-stu-id="a5104-118">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="a5104-119">version</span><span class="sxs-lookup"><span data-stu-id="a5104-119">version</span></span>

<span data-ttu-id="a5104-120">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="a5104-120">**Required** &ndash; String</span></span>

<span data-ttu-id="a5104-121">La versión de la aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="a5104-121">The version of the specific app.</span></span> <span data-ttu-id="a5104-122">Si actualiza algo en el manifiesto, la versión también debe incrementarse.</span><span class="sxs-lookup"><span data-stu-id="a5104-122">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="a5104-123">De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="a5104-123">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="a5104-124">Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y volver a validarse.</span><span class="sxs-lookup"><span data-stu-id="a5104-124">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="a5104-125">A continuación, los usuarios de esta aplicación recibirán el nuevo manifiesto actualizado automáticamente en unas pocas horas, después de que se apruebe.</span><span class="sxs-lookup"><span data-stu-id="a5104-125">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="a5104-126">Si cambian los permisos solicitados por la aplicación, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-126">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="a5104-127">Esta cadena de versión debe seguir el [estándar de semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="a5104-127">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="a5104-128">id</span><span class="sxs-lookup"><span data-stu-id="a5104-128">id</span></span>

<span data-ttu-id="a5104-129">**Obligatorio** &ndash; Id. de aplicación de Microsoft</span><span class="sxs-lookup"><span data-stu-id="a5104-129">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="a5104-130">Identificador único generado por Microsoft para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-130">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="a5104-131">Si has registrado un bot a través del Microsoft Bot Framework o la aplicación web de la pestaña ya inicia sesión con Microsoft, ya debes tener un identificador y debes escribirlo aquí.</span><span class="sxs-lookup"><span data-stu-id="a5104-131">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="a5104-132">De lo contrario, debe generar un nuevo identificador en el Portal de registro de aplicaciones de Microsoft ([Mis](https://apps.dev.microsoft.com)aplicaciones ), escriba aquí y, a continuación, volver a usarlo cuando [agregue un bot](~/bots/how-to/create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="a5104-132">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="a5104-133">packageName</span><span class="sxs-lookup"><span data-stu-id="a5104-133">packageName</span></span>

<span data-ttu-id="a5104-134">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="a5104-134">**Required** &ndash; String</span></span>

<span data-ttu-id="a5104-135">Un identificador único para esta aplicación en la notación de dominio inverso; por ejemplo, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="a5104-135">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="a5104-136">developer</span><span class="sxs-lookup"><span data-stu-id="a5104-136">developer</span></span>

<span data-ttu-id="a5104-137">**Required**</span><span class="sxs-lookup"><span data-stu-id="a5104-137">**Required**</span></span>

<span data-ttu-id="a5104-138">Especifica información sobre su empresa.</span><span class="sxs-lookup"><span data-stu-id="a5104-138">Specifies information about your company.</span></span> <span data-ttu-id="a5104-139">Para las aplicaciones enviadas a AppSource (anteriormente Office Store), estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="a5104-139">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="a5104-140">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-140">Name</span></span>| <span data-ttu-id="a5104-141">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-141">Maximum size</span></span> | <span data-ttu-id="a5104-142">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-142">Required</span></span> | <span data-ttu-id="a5104-143">Description</span><span class="sxs-lookup"><span data-stu-id="a5104-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="a5104-144">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-144">32 characters</span></span>|<span data-ttu-id="a5104-145">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-145">✔</span></span>|<span data-ttu-id="a5104-146">Nombre para mostrar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a5104-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="a5104-147">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-147">2048 characters</span></span>|<span data-ttu-id="a5104-148">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-148">✔</span></span>|<span data-ttu-id="a5104-149">La https:// url del sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a5104-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="a5104-150">Este vínculo debe llevar a los usuarios a su empresa o página de aterrizaje específica del producto.</span><span class="sxs-lookup"><span data-stu-id="a5104-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="a5104-151">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-151">2048 characters</span></span>|<span data-ttu-id="a5104-152">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-152">✔</span></span>|<span data-ttu-id="a5104-153">La https:// url a la directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a5104-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="a5104-154">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-154">2048 characters</span></span>|<span data-ttu-id="a5104-155">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-155">✔</span></span>|<span data-ttu-id="a5104-156">La https:// url a los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a5104-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="a5104-157">10 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-157">10 characters</span></span>|<span data-ttu-id="a5104-158">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-158">✔</span></span>|<span data-ttu-id="a5104-159">**Opcional** Id. de red de partners de Microsoft que identifica la organización asociada que está creando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-159">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="a5104-160">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="a5104-160">localizationInfo</span></span>

<span data-ttu-id="a5104-161">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a5104-161">**Optional**</span></span>

<span data-ttu-id="a5104-162">Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="a5104-162">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="a5104-163">Vea [localización](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="a5104-163">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="a5104-164">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-164">Name</span></span>| <span data-ttu-id="a5104-165">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-165">Maximum size</span></span> | <span data-ttu-id="a5104-166">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-166">Required</span></span> | <span data-ttu-id="a5104-167">Description</span><span class="sxs-lookup"><span data-stu-id="a5104-167">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="a5104-168">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-168">4 characters</span></span>|<span data-ttu-id="a5104-169">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-169">✔</span></span>|<span data-ttu-id="a5104-170">La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="a5104-170">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="a5104-171">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="a5104-171">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="a5104-172">Una matriz de objetos que especifica traducciones de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="a5104-172">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="a5104-173">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-173">Name</span></span>| <span data-ttu-id="a5104-174">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-174">Maximum size</span></span> | <span data-ttu-id="a5104-175">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-175">Required</span></span> | <span data-ttu-id="a5104-176">Description</span><span class="sxs-lookup"><span data-stu-id="a5104-176">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="a5104-177">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-177">4 characters</span></span>|<span data-ttu-id="a5104-178">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-178">✔</span></span>|<span data-ttu-id="a5104-179">Etiqueta de idioma de las cadenas del archivo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="a5104-179">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="a5104-180">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-180">4 characters</span></span>|<span data-ttu-id="a5104-181">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-181">✔</span></span>|<span data-ttu-id="a5104-182">Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="a5104-182">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="a5104-183">name</span><span class="sxs-lookup"><span data-stu-id="a5104-183">name</span></span>

<span data-ttu-id="a5104-184">**Required**</span><span class="sxs-lookup"><span data-stu-id="a5104-184">**Required**</span></span>

<span data-ttu-id="a5104-185">El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="a5104-185">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="a5104-186">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="a5104-186">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="a5104-187">Los valores de `short` y no deben ser los `full` mismos.</span><span class="sxs-lookup"><span data-stu-id="a5104-187">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="a5104-188">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-188">Name</span></span>| <span data-ttu-id="a5104-189">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-189">Maximum size</span></span> | <span data-ttu-id="a5104-190">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-190">Required</span></span> | <span data-ttu-id="a5104-191">Description</span><span class="sxs-lookup"><span data-stu-id="a5104-191">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="a5104-192">30 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-192">30 characters</span></span>|<span data-ttu-id="a5104-193">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-193">✔</span></span>|<span data-ttu-id="a5104-194">El nombre para mostrar corto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-194">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="a5104-195">100 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-195">100 characters</span></span>||<span data-ttu-id="a5104-196">El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="a5104-196">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="a5104-197">description</span><span class="sxs-lookup"><span data-stu-id="a5104-197">description</span></span>

<span data-ttu-id="a5104-198">**Required**</span><span class="sxs-lookup"><span data-stu-id="a5104-198">**Required**</span></span>

<span data-ttu-id="a5104-199">Describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a5104-199">Describes your app to users.</span></span> <span data-ttu-id="a5104-200">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="a5104-200">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="a5104-201">Asegúrese de que su descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia.</span><span class="sxs-lookup"><span data-stu-id="a5104-201">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="a5104-202">También debe tener en cuenta, en la descripción completa, si se requiere una cuenta externa para su uso.</span><span class="sxs-lookup"><span data-stu-id="a5104-202">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="a5104-203">Los valores de `short` y no deben ser los `full` mismos.</span><span class="sxs-lookup"><span data-stu-id="a5104-203">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="a5104-204">La descripción breve no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-204">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="a5104-205">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-205">Name</span></span>| <span data-ttu-id="a5104-206">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-206">Maximum size</span></span> | <span data-ttu-id="a5104-207">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-207">Required</span></span> | <span data-ttu-id="a5104-208">Description</span><span class="sxs-lookup"><span data-stu-id="a5104-208">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="a5104-209">80 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-209">80 characters</span></span>|<span data-ttu-id="a5104-210">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-210">✔</span></span>|<span data-ttu-id="a5104-211">Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.</span><span class="sxs-lookup"><span data-stu-id="a5104-211">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="a5104-212">4000 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-212">4000 characters</span></span>|<span data-ttu-id="a5104-213">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-213">✔</span></span>|<span data-ttu-id="a5104-214">Descripción completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-214">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="a5104-215">iconos</span><span class="sxs-lookup"><span data-stu-id="a5104-215">icons</span></span>

<span data-ttu-id="a5104-216">**Required**</span><span class="sxs-lookup"><span data-stu-id="a5104-216">**Required**</span></span>

<span data-ttu-id="a5104-217">Iconos usados dentro de la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-217">Icons used within the Teams app.</span></span> <span data-ttu-id="a5104-218">Los archivos de icono deben incluirse como parte del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="a5104-218">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="a5104-219">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-219">Name</span></span>| <span data-ttu-id="a5104-220">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-220">Maximum size</span></span> | <span data-ttu-id="a5104-221">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-221">Required</span></span> | <span data-ttu-id="a5104-222">Description</span><span class="sxs-lookup"><span data-stu-id="a5104-222">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="a5104-223">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-223">2048 characters</span></span>|<span data-ttu-id="a5104-224">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-224">✔</span></span>|<span data-ttu-id="a5104-225">Una ruta de acceso de archivo relativa a un icono de esquema PNG transparente de 32 x 32.</span><span class="sxs-lookup"><span data-stu-id="a5104-225">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="a5104-226">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-226">2048 characters</span></span>|<span data-ttu-id="a5104-227">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-227">✔</span></span>|<span data-ttu-id="a5104-228">Una ruta de acceso de archivo relativa a un icono PNG de color completo de 192 x 192.</span><span class="sxs-lookup"><span data-stu-id="a5104-228">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="a5104-229">accentColor</span><span class="sxs-lookup"><span data-stu-id="a5104-229">accentColor</span></span>

<span data-ttu-id="a5104-230">**Obligatorio** &ndash; String</span><span class="sxs-lookup"><span data-stu-id="a5104-230">**Required** &ndash; String</span></span>

<span data-ttu-id="a5104-231">Color que se usará junto con y como fondo para los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="a5104-231">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="a5104-232">El valor debe ser un código de color HTML válido a partir de '#', por ejemplo `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="a5104-232">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="a5104-233">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="a5104-233">configurableTabs</span></span>

<span data-ttu-id="a5104-234">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a5104-234">**Optional**</span></span>

<span data-ttu-id="a5104-235">Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de grupo que requiere una configuración adicional antes de agregarla.</span><span class="sxs-lookup"><span data-stu-id="a5104-235">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="a5104-236">Las pestañas configurables solo se admiten en el ámbito de teams y actualmente solo se admite una pestaña por aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-236">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="a5104-237">El objeto es una matriz con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="a5104-237">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="a5104-238">Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña de canal configurable.</span><span class="sxs-lookup"><span data-stu-id="a5104-238">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="a5104-239">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-239">Name</span></span>| <span data-ttu-id="a5104-240">Tipo</span><span class="sxs-lookup"><span data-stu-id="a5104-240">Type</span></span>| <span data-ttu-id="a5104-241">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-241">Maximum size</span></span> | <span data-ttu-id="a5104-242">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-242">Required</span></span> | <span data-ttu-id="a5104-243">Descripción</span><span class="sxs-lookup"><span data-stu-id="a5104-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="a5104-244">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-244">String</span></span>|<span data-ttu-id="a5104-245">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-245">2048 characters</span></span>|<span data-ttu-id="a5104-246">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-246">✔</span></span>|<span data-ttu-id="a5104-247">La https:// url que se va a usar al configurar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a5104-247">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="a5104-248">Booleano</span><span class="sxs-lookup"><span data-stu-id="a5104-248">Boolean</span></span>|||<span data-ttu-id="a5104-249">Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de su creación.</span><span class="sxs-lookup"><span data-stu-id="a5104-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="a5104-250">Valor predeterminado: `true`</span><span class="sxs-lookup"><span data-stu-id="a5104-250">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="a5104-251">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="a5104-251">Array of enum</span></span>|<span data-ttu-id="a5104-252">1</span><span class="sxs-lookup"><span data-stu-id="a5104-252">1</span></span>|<span data-ttu-id="a5104-253">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-253">✔</span></span>|<span data-ttu-id="a5104-254">Actualmente, las pestañas configurables solo admiten `team` los `groupchat` ámbitos y.</span><span class="sxs-lookup"><span data-stu-id="a5104-254">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="a5104-255">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-255">String</span></span>|<span data-ttu-id="a5104-256">2048</span><span class="sxs-lookup"><span data-stu-id="a5104-256">2048</span></span>||<span data-ttu-id="a5104-257">Una ruta de acceso de archivo relativa a una imagen de vista previa de tabulación para su uso en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a5104-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="a5104-258">Tamaño 1024x768.</span><span class="sxs-lookup"><span data-stu-id="a5104-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="a5104-259">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="a5104-259">Array of enum</span></span>|<span data-ttu-id="a5104-260">1</span><span class="sxs-lookup"><span data-stu-id="a5104-260">1</span></span>||<span data-ttu-id="a5104-261">Define cómo la pestaña estará disponible en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a5104-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="a5104-262">Las opciones son `sharePointFullPage` y `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="a5104-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="a5104-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="a5104-263">staticTabs</span></span>

<span data-ttu-id="a5104-264">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a5104-264">**Optional**</span></span>

<span data-ttu-id="a5104-265">Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente.</span><span class="sxs-lookup"><span data-stu-id="a5104-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="a5104-266">Las pestañas estáticas declaradas en el ámbito siempre se anclan a la experiencia `personal` personal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="a5104-267">Actualmente no se admiten las pestañas estáticas declaradas `team` en el ámbito.</span><span class="sxs-lookup"><span data-stu-id="a5104-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="a5104-268">Represente las pestañas con tarjetas adaptables especificando en `contentBotId` lugar de en el bloque `contentUrl` **staticTabs.**</span><span class="sxs-lookup"><span data-stu-id="a5104-268">Render tabs with Adaptive Cards by specifying `contentBotId` instead of `contentUrl` in the **staticTabs** block.</span></span>

<span data-ttu-id="a5104-269">El objeto es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="a5104-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="a5104-270">Este bloque solo es necesario para las soluciones que proporcionan una solución de tabulación estática.</span><span class="sxs-lookup"><span data-stu-id="a5104-270">This block is required only for solutions that provide a static tab solution.</span></span>


|<span data-ttu-id="a5104-271">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-271">Name</span></span>| <span data-ttu-id="a5104-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="a5104-272">Type</span></span>| <span data-ttu-id="a5104-273">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-273">Maximum size</span></span> | <span data-ttu-id="a5104-274">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-274">Required</span></span> | <span data-ttu-id="a5104-275">Descripción</span><span class="sxs-lookup"><span data-stu-id="a5104-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="a5104-276">String</span><span class="sxs-lookup"><span data-stu-id="a5104-276">String</span></span>|<span data-ttu-id="a5104-277">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-277">64 characters</span></span>|<span data-ttu-id="a5104-278">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-278">✔</span></span>|<span data-ttu-id="a5104-279">Identificador único para la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="a5104-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="a5104-280">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-280">String</span></span>|<span data-ttu-id="a5104-281">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-281">128 characters</span></span>|<span data-ttu-id="a5104-282">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-282">✔</span></span>|<span data-ttu-id="a5104-283">Nombre para mostrar de la pestaña en la interfaz de canal.</span><span class="sxs-lookup"><span data-stu-id="a5104-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="a5104-284">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-284">String</span></span>|<span data-ttu-id="a5104-285">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-285">2048 characters</span></span>|<span data-ttu-id="a5104-286">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-286">✔</span></span>|<span data-ttu-id="a5104-287">Dirección URL https:// que apunta a la interfaz de usuario de la entidad que se va a mostrar en el Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="a5104-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`contentBotId`|   | | | <span data-ttu-id="a5104-288">El Microsoft Teams de aplicación especificado para el bot en el portal de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a5104-288">The Microsoft Teams app ID specified for the bot in the Bot Framework portal.</span></span> |
|`websiteUrl`|<span data-ttu-id="a5104-289">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-289">String</span></span>|<span data-ttu-id="a5104-290">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-290">2048 characters</span></span>||<span data-ttu-id="a5104-291">La https:// dirección URL para apuntar si un usuario opta por ver en un explorador.</span><span class="sxs-lookup"><span data-stu-id="a5104-291">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="a5104-292">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="a5104-292">Array of enum</span></span>|<span data-ttu-id="a5104-293">1</span><span class="sxs-lookup"><span data-stu-id="a5104-293">1</span></span>|<span data-ttu-id="a5104-294">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-294">✔</span></span>|<span data-ttu-id="a5104-295">Actualmente, las pestañas estáticas solo admiten el ámbito, lo que significa que solo se puede aprovisionar como `personal` parte de la experiencia personal.</span><span class="sxs-lookup"><span data-stu-id="a5104-295">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="a5104-296">bots</span><span class="sxs-lookup"><span data-stu-id="a5104-296">bots</span></span>

<span data-ttu-id="a5104-297">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a5104-297">**Optional**</span></span>

<span data-ttu-id="a5104-298">Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="a5104-298">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="a5104-299">El objeto es una matriz (máximo de solo 1 elemento actualmente solo se permite un bot por aplicación) con todos los &mdash; elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="a5104-299">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="a5104-300">Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.</span><span class="sxs-lookup"><span data-stu-id="a5104-300">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="a5104-301">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-301">Name</span></span>| <span data-ttu-id="a5104-302">Tipo</span><span class="sxs-lookup"><span data-stu-id="a5104-302">Type</span></span>| <span data-ttu-id="a5104-303">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-303">Maximum size</span></span> | <span data-ttu-id="a5104-304">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-304">Required</span></span> | <span data-ttu-id="a5104-305">Descripción</span><span class="sxs-lookup"><span data-stu-id="a5104-305">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a5104-306">String</span><span class="sxs-lookup"><span data-stu-id="a5104-306">String</span></span>|<span data-ttu-id="a5104-307">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-307">64 characters</span></span>|<span data-ttu-id="a5104-308">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-308">✔</span></span>|<span data-ttu-id="a5104-309">El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a5104-309">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="a5104-310">Esto bien puede ser el mismo que el identificador general [de la aplicación](#id).</span><span class="sxs-lookup"><span data-stu-id="a5104-310">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="a5104-311">Booleano</span><span class="sxs-lookup"><span data-stu-id="a5104-311">Boolean</span></span>|||<span data-ttu-id="a5104-312">Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico.</span><span class="sxs-lookup"><span data-stu-id="a5104-312">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="a5104-313">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="a5104-313">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="a5104-314">Booleano</span><span class="sxs-lookup"><span data-stu-id="a5104-314">Boolean</span></span>|||<span data-ttu-id="a5104-315">Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación.</span><span class="sxs-lookup"><span data-stu-id="a5104-315">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="a5104-316">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="a5104-316">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="a5104-317">Booleano</span><span class="sxs-lookup"><span data-stu-id="a5104-317">Boolean</span></span>|||<span data-ttu-id="a5104-318">Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal.</span><span class="sxs-lookup"><span data-stu-id="a5104-318">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="a5104-319">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="a5104-319">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="a5104-320">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="a5104-320">Array of enum</span></span>|<span data-ttu-id="a5104-321">3</span><span class="sxs-lookup"><span data-stu-id="a5104-321">3</span></span>|<span data-ttu-id="a5104-322">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-322">✔</span></span>|<span data-ttu-id="a5104-323">Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`).</span><span class="sxs-lookup"><span data-stu-id="a5104-323">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a5104-324">Estas opciones no son exclusivas.</span><span class="sxs-lookup"><span data-stu-id="a5104-324">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="a5104-325">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="a5104-325">bots.commandLists</span></span>

<span data-ttu-id="a5104-326">Una lista opcional de comandos que el bot puede recomendar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a5104-326">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="a5104-327">El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de comandos independiente para cada ámbito compatible `object` con el bot.</span><span class="sxs-lookup"><span data-stu-id="a5104-327">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="a5104-328">Para obtener más información, vea [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span><span class="sxs-lookup"><span data-stu-id="a5104-328">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="a5104-329">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-329">Name</span></span>| <span data-ttu-id="a5104-330">Tipo</span><span class="sxs-lookup"><span data-stu-id="a5104-330">Type</span></span>| <span data-ttu-id="a5104-331">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-331">Maximum size</span></span> | <span data-ttu-id="a5104-332">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-332">Required</span></span> | <span data-ttu-id="a5104-333">Descripción</span><span class="sxs-lookup"><span data-stu-id="a5104-333">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="a5104-334">matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="a5104-334">array of enum</span></span>|<span data-ttu-id="a5104-335">3</span><span class="sxs-lookup"><span data-stu-id="a5104-335">3</span></span>|<span data-ttu-id="a5104-336">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-336">✔</span></span>|<span data-ttu-id="a5104-337">Especifica el ámbito para el que la lista de comandos es válida.</span><span class="sxs-lookup"><span data-stu-id="a5104-337">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="a5104-338">Las opciones son `team`, `personal` y `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="a5104-338">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="a5104-339">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a5104-339">array of objects</span></span>|<span data-ttu-id="a5104-340">10</span><span class="sxs-lookup"><span data-stu-id="a5104-340">10</span></span>|<span data-ttu-id="a5104-341">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-341">✔</span></span>|<span data-ttu-id="a5104-342">Una matriz de comandos que el bot admite:</span><span class="sxs-lookup"><span data-stu-id="a5104-342">An array of commands the bot supports:</span></span><br><span data-ttu-id="a5104-343">`title`: el nombre del comando bot (cadena, 32).</span><span class="sxs-lookup"><span data-stu-id="a5104-343">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="a5104-344">`description`: una descripción sencilla o un ejemplo de la sintaxis del comando y su argumento (cadena, 128).</span><span class="sxs-lookup"><span data-stu-id="a5104-344">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="a5104-345">conectores</span><span class="sxs-lookup"><span data-stu-id="a5104-345">connectors</span></span>

<span data-ttu-id="a5104-346">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a5104-346">**Optional**</span></span>

<span data-ttu-id="a5104-347">El `connectors` bloque define un Office 365 connector para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-347">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="a5104-348">El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="a5104-348">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="a5104-349">Este bloque solo es necesario para las soluciones que proporcionan un conector.</span><span class="sxs-lookup"><span data-stu-id="a5104-349">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="a5104-350">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-350">Name</span></span>| <span data-ttu-id="a5104-351">Tipo</span><span class="sxs-lookup"><span data-stu-id="a5104-351">Type</span></span>| <span data-ttu-id="a5104-352">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-352">Maximum size</span></span> | <span data-ttu-id="a5104-353">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-353">Required</span></span> | <span data-ttu-id="a5104-354">Descripción</span><span class="sxs-lookup"><span data-stu-id="a5104-354">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="a5104-355">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-355">String</span></span>|<span data-ttu-id="a5104-356">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-356">2048 characters</span></span>|<span data-ttu-id="a5104-357">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-357">✔</span></span>|<span data-ttu-id="a5104-358">La https:// url que se va a usar al configurar el conector.</span><span class="sxs-lookup"><span data-stu-id="a5104-358">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="a5104-359">String</span><span class="sxs-lookup"><span data-stu-id="a5104-359">String</span></span>|<span data-ttu-id="a5104-360">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-360">64 characters</span></span>|<span data-ttu-id="a5104-361">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-361">✔</span></span>|<span data-ttu-id="a5104-362">Identificador único del conector que coincide con su identificador en el [Panel de desarrolladores de conectores.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="a5104-362">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="a5104-363">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="a5104-363">Array of enum</span></span>|<span data-ttu-id="a5104-364">1</span><span class="sxs-lookup"><span data-stu-id="a5104-364">1</span></span>|<span data-ttu-id="a5104-365">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-365">✔</span></span>|<span data-ttu-id="a5104-366">Especifica si connector ofrece una experiencia en el contexto de un canal en un , o una experiencia ámbito a un `team` usuario individual solo ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="a5104-366">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a5104-367">Actualmente, solo se `team` admite el ámbito.</span><span class="sxs-lookup"><span data-stu-id="a5104-367">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="a5104-368">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="a5104-368">composeExtensions</span></span>

<span data-ttu-id="a5104-369">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a5104-369">**Optional**</span></span>

<span data-ttu-id="a5104-370">Define una extensión de mensajería para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-370">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="a5104-371">El nombre de la característica se cambió de "extensión de redacción" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="a5104-371">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="a5104-372">El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="a5104-372">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="a5104-373">Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a5104-373">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="a5104-374">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-374">Name</span></span>| <span data-ttu-id="a5104-375">Tipo</span><span class="sxs-lookup"><span data-stu-id="a5104-375">Type</span></span> | <span data-ttu-id="a5104-376">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-376">Maximum Size</span></span> | <span data-ttu-id="a5104-377">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a5104-377">Required</span></span> | <span data-ttu-id="a5104-378">Descripción</span><span class="sxs-lookup"><span data-stu-id="a5104-378">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a5104-379">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-379">String</span></span>|<span data-ttu-id="a5104-380">64</span><span class="sxs-lookup"><span data-stu-id="a5104-380">64</span></span>|<span data-ttu-id="a5104-381">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-381">✔</span></span>|<span data-ttu-id="a5104-382">El identificador único de la aplicación de Microsoft para el bot que hace una copia de seguridad de la extensión de mensajería, tal como se registró con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a5104-382">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="a5104-383">Esto bien puede ser el mismo que el identificador general [de la aplicación](#id).</span><span class="sxs-lookup"><span data-stu-id="a5104-383">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="a5104-384">Booleano</span><span class="sxs-lookup"><span data-stu-id="a5104-384">Boolean</span></span>|||<span data-ttu-id="a5104-385">Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a5104-385">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="a5104-386">El valor predeterminado es `false`.</span><span class="sxs-lookup"><span data-stu-id="a5104-386">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="a5104-387">Matriz de objeto</span><span class="sxs-lookup"><span data-stu-id="a5104-387">Array of object</span></span>|<span data-ttu-id="a5104-388">10</span><span class="sxs-lookup"><span data-stu-id="a5104-388">10</span></span>|<span data-ttu-id="a5104-389">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-389">✔</span></span>|<span data-ttu-id="a5104-390">Matriz de comandos que admite la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="a5104-390">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="a5104-391">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="a5104-391">composeExtensions.commands</span></span>

<span data-ttu-id="a5104-392">La extensión de mensajería debe declarar uno o más comandos.</span><span class="sxs-lookup"><span data-stu-id="a5104-392">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="a5104-393">Cada comando aparece en Microsoft Teams como una interacción potencial desde el punto de entrada basado en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="a5104-393">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="a5104-394">Hay un máximo de 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="a5104-394">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="a5104-395">Cada elemento de comando es un objeto con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="a5104-395">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="a5104-396">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-396">Name</span></span>| <span data-ttu-id="a5104-397">Tipo</span><span class="sxs-lookup"><span data-stu-id="a5104-397">Type</span></span>| <span data-ttu-id="a5104-398">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-398">Maximum size</span></span> | <span data-ttu-id="a5104-399">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-399">Required</span></span> | <span data-ttu-id="a5104-400">Descripción</span><span class="sxs-lookup"><span data-stu-id="a5104-400">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="a5104-401">String</span><span class="sxs-lookup"><span data-stu-id="a5104-401">String</span></span>|<span data-ttu-id="a5104-402">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-402">64 characters</span></span>|<span data-ttu-id="a5104-403">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-403">✔</span></span>|<span data-ttu-id="a5104-404">El identificador del comando.</span><span class="sxs-lookup"><span data-stu-id="a5104-404">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="a5104-405">String</span><span class="sxs-lookup"><span data-stu-id="a5104-405">String</span></span>|<span data-ttu-id="a5104-406">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-406">64 characters</span></span>||<span data-ttu-id="a5104-407">Tipo del comando.</span><span class="sxs-lookup"><span data-stu-id="a5104-407">Type of the command.</span></span> <span data-ttu-id="a5104-408">Uno de `query` o `action` .</span><span class="sxs-lookup"><span data-stu-id="a5104-408">One of `query` or `action`.</span></span> <span data-ttu-id="a5104-409">Valor predeterminado: `query`</span><span class="sxs-lookup"><span data-stu-id="a5104-409">Default: `query`</span></span>|
|`title`|<span data-ttu-id="a5104-410">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-410">String</span></span>|<span data-ttu-id="a5104-411">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-411">32 characters</span></span>|<span data-ttu-id="a5104-412">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-412">✔</span></span>|<span data-ttu-id="a5104-413">Nombre de comando fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="a5104-413">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="a5104-414">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-414">String</span></span>|<span data-ttu-id="a5104-415">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-415">128 characters</span></span>||<span data-ttu-id="a5104-416">La descripción que se muestra a los usuarios para indicar el propósito de este comando.</span><span class="sxs-lookup"><span data-stu-id="a5104-416">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="a5104-417">Booleano</span><span class="sxs-lookup"><span data-stu-id="a5104-417">Boolean</span></span>|||<span data-ttu-id="a5104-418">Valor booleano que indica si el comando debe ejecutarse inicialmente sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="a5104-418">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="a5104-419">Valor predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="a5104-419">Default: `false`</span></span>|
|`context`|<span data-ttu-id="a5104-420">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="a5104-420">Array of Strings</span></span>|<span data-ttu-id="a5104-421">3</span><span class="sxs-lookup"><span data-stu-id="a5104-421">3</span></span>||<span data-ttu-id="a5104-422">Define desde dónde se puede invocar la extensión de mensaje.</span><span class="sxs-lookup"><span data-stu-id="a5104-422">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="a5104-423">Cualquier combinación de `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="a5104-423">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="a5104-424">El valor predeterminado es `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="a5104-424">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="a5104-425">Booleano</span><span class="sxs-lookup"><span data-stu-id="a5104-425">Boolean</span></span>|||<span data-ttu-id="a5104-426">Valor booleano que indica si debe capturar el módulo de tareas dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="a5104-426">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="a5104-427">Objeto</span><span class="sxs-lookup"><span data-stu-id="a5104-427">Object</span></span>|||<span data-ttu-id="a5104-428">Especifique el módulo de tareas que se debe precargar al usar un comando de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a5104-428">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="a5104-429">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-429">String</span></span>|<span data-ttu-id="a5104-430">64</span><span class="sxs-lookup"><span data-stu-id="a5104-430">64</span></span>||<span data-ttu-id="a5104-431">Título del cuadro de diálogo inicial.</span><span class="sxs-lookup"><span data-stu-id="a5104-431">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="a5104-432">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-432">String</span></span>|||<span data-ttu-id="a5104-433">Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="a5104-433">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="a5104-434">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-434">String</span></span>|||<span data-ttu-id="a5104-435">Alto del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="a5104-435">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="a5104-436">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-436">String</span></span>|||<span data-ttu-id="a5104-437">Dirección URL de vista web inicial.</span><span class="sxs-lookup"><span data-stu-id="a5104-437">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="a5104-438">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a5104-438">Array of Objects</span></span>|<span data-ttu-id="a5104-439">5 </span><span class="sxs-lookup"><span data-stu-id="a5104-439">5</span></span>||<span data-ttu-id="a5104-440">Una lista de controladores que permiten invocar aplicaciones cuando se cumplen determinadas condiciones.</span><span class="sxs-lookup"><span data-stu-id="a5104-440">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="a5104-441">Los dominios también deben aparecer en `validDomains` .</span><span class="sxs-lookup"><span data-stu-id="a5104-441">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="a5104-442">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-442">String</span></span>|||<span data-ttu-id="a5104-443">El tipo de controlador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="a5104-443">The type of message handler.</span></span> <span data-ttu-id="a5104-444">Debe ser `"link"`.</span><span class="sxs-lookup"><span data-stu-id="a5104-444">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="a5104-445">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="a5104-445">Array of Strings</span></span>|||<span data-ttu-id="a5104-446">Matriz de dominios para los que se puede registrar el controlador de mensajes de vínculo.</span><span class="sxs-lookup"><span data-stu-id="a5104-446">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="a5104-447">Matriz de objeto</span><span class="sxs-lookup"><span data-stu-id="a5104-447">Array of object</span></span>|<span data-ttu-id="a5104-448">5 </span><span class="sxs-lookup"><span data-stu-id="a5104-448">5</span></span>|<span data-ttu-id="a5104-449">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-449">✔</span></span>|<span data-ttu-id="a5104-450">La lista de parámetros que toma el comando.</span><span class="sxs-lookup"><span data-stu-id="a5104-450">The list of parameters the command takes.</span></span> <span data-ttu-id="a5104-451">Mínimo: 1; máximo: 5</span><span class="sxs-lookup"><span data-stu-id="a5104-451">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="a5104-452">String</span><span class="sxs-lookup"><span data-stu-id="a5104-452">String</span></span>|<span data-ttu-id="a5104-453">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-453">64 characters</span></span>|<span data-ttu-id="a5104-454">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-454">✔</span></span>|<span data-ttu-id="a5104-455">Nombre del parámetro tal como aparece en el cliente.</span><span class="sxs-lookup"><span data-stu-id="a5104-455">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="a5104-456">Esto se incluye en la solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="a5104-456">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="a5104-457">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-457">String</span></span>|<span data-ttu-id="a5104-458">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-458">32 characters</span></span>|<span data-ttu-id="a5104-459">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-459">✔</span></span>|<span data-ttu-id="a5104-460">Título fácil de usar para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="a5104-460">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="a5104-461">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-461">String</span></span>|<span data-ttu-id="a5104-462">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-462">128 characters</span></span>||<span data-ttu-id="a5104-463">Cadena fácil de usar que describe el propósito de este parámetro.</span><span class="sxs-lookup"><span data-stu-id="a5104-463">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="a5104-464">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-464">String</span></span>|<span data-ttu-id="a5104-465">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-465">128 characters</span></span>||<span data-ttu-id="a5104-466">Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="a5104-466">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="a5104-467">Uno de `text` , , , , , , `textarea` `number` `date` `time` `toggle` `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="a5104-467">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="a5104-468">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="a5104-468">Array of Objects</span></span>|<span data-ttu-id="a5104-469">10</span><span class="sxs-lookup"><span data-stu-id="a5104-469">10</span></span>||<span data-ttu-id="a5104-470">Las opciones de elección para `choiceset` el archivo .</span><span class="sxs-lookup"><span data-stu-id="a5104-470">The choice options for the `choiceset`.</span></span> <span data-ttu-id="a5104-471">Use solo cuando `parameter.inputType` es `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="a5104-471">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="a5104-472">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-472">String</span></span>|<span data-ttu-id="a5104-473">128</span><span class="sxs-lookup"><span data-stu-id="a5104-473">128</span></span>||<span data-ttu-id="a5104-474">Título de la elección.</span><span class="sxs-lookup"><span data-stu-id="a5104-474">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="a5104-475">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-475">String</span></span>|<span data-ttu-id="a5104-476">512</span><span class="sxs-lookup"><span data-stu-id="a5104-476">512</span></span>||<span data-ttu-id="a5104-477">Valor de la elección.</span><span class="sxs-lookup"><span data-stu-id="a5104-477">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="a5104-478">permisos</span><span class="sxs-lookup"><span data-stu-id="a5104-478">permissions</span></span>

<span data-ttu-id="a5104-479">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a5104-479">**Optional**</span></span>

<span data-ttu-id="a5104-480">Una matriz de la que se especifican los permisos que solicita la aplicación, lo que permite a los usuarios finales saber cómo se llevará a cabo `string` la extensión.</span><span class="sxs-lookup"><span data-stu-id="a5104-480">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="a5104-481">Las siguientes opciones no son exclusivas:</span><span class="sxs-lookup"><span data-stu-id="a5104-481">The following options are non-exclusive:</span></span>

* <span data-ttu-id="a5104-482">`identity`&emsp;Requiere información de identidad de usuario.</span><span class="sxs-lookup"><span data-stu-id="a5104-482">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="a5104-483">`messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="a5104-483">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="a5104-484">Al cambiar estos permisos al actualizar la aplicación, los usuarios repetirán el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="a5104-484">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="a5104-485">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="a5104-485">devicePermissions</span></span>

<span data-ttu-id="a5104-486">**Opcional** Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="a5104-486">**Optional** Array of Strings</span></span>

<span data-ttu-id="a5104-487">Especifica las características nativas del dispositivo de un usuario a las que la aplicación puede solicitar acceso.</span><span class="sxs-lookup"><span data-stu-id="a5104-487">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="a5104-488">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="a5104-488">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="a5104-489">validDomains</span><span class="sxs-lookup"><span data-stu-id="a5104-489">validDomains</span></span>

<span data-ttu-id="a5104-490">**Opcional**, excepto **Requerido cuando** se indica</span><span class="sxs-lookup"><span data-stu-id="a5104-490">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="a5104-491">Una lista de dominios válidos desde los que la aplicación espera cargar cualquier contenido.</span><span class="sxs-lookup"><span data-stu-id="a5104-491">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="a5104-492">Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="a5104-492">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="a5104-493">Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="a5104-493">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="a5104-494">Si la interfaz de usuario de contenido o configuración de pestañas necesita navegar a cualquier otro dominio además del uso para la configuración de pestañas, este dominio debe especificarse aquí.</span><span class="sxs-lookup"><span data-stu-id="a5104-494">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="a5104-495">Sin **embargo,** no es necesario incluir los dominios de los proveedores de identidades que quieres admitir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-495">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="a5104-496">Por ejemplo, para autenticar con un id. de Google, es necesario redirigir a accounts.google.com, pero no debe incluir accounts.google.com en `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="a5104-496">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5104-497">No agregue dominios que estén fuera del control, ya sea directamente o a través de caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="a5104-497">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="a5104-498">Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="a5104-498">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="a5104-499">El objeto es una matriz con todos los elementos del tipo `string` .</span><span class="sxs-lookup"><span data-stu-id="a5104-499">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="a5104-500">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="a5104-500">webApplicationInfo</span></span>

<span data-ttu-id="a5104-501">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a5104-501">**Optional**</span></span>

<span data-ttu-id="a5104-502">Especifica tu id. de aplicación de AAD y Graph información para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="a5104-502">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="a5104-503">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-503">Name</span></span>| <span data-ttu-id="a5104-504">Tipo</span><span class="sxs-lookup"><span data-stu-id="a5104-504">Type</span></span>| <span data-ttu-id="a5104-505">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-505">Maximum size</span></span> | <span data-ttu-id="a5104-506">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-506">Required</span></span> | <span data-ttu-id="a5104-507">Descripción</span><span class="sxs-lookup"><span data-stu-id="a5104-507">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="a5104-508">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-508">String</span></span>|<span data-ttu-id="a5104-509">36 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-509">36 characters</span></span>|<span data-ttu-id="a5104-510">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-510">✔</span></span>|<span data-ttu-id="a5104-511">Id. de aplicación de AAD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-511">AAD application id of the app.</span></span> <span data-ttu-id="a5104-512">Este identificador debe ser un GUID.</span><span class="sxs-lookup"><span data-stu-id="a5104-512">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="a5104-513">Cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-513">String</span></span>|<span data-ttu-id="a5104-514">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="a5104-514">2048 characters</span></span>|<span data-ttu-id="a5104-515">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-515">✔</span></span>|<span data-ttu-id="a5104-516">Url de recurso de la aplicación para adquirir token de autenticación para SSO.</span><span class="sxs-lookup"><span data-stu-id="a5104-516">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="a5104-517">Matriz</span><span class="sxs-lookup"><span data-stu-id="a5104-517">Array</span></span>|<span data-ttu-id="a5104-518">Máximo de 100 elementos</span><span class="sxs-lookup"><span data-stu-id="a5104-518">Maximum 100 items</span></span>|<span data-ttu-id="a5104-519">✔</span><span class="sxs-lookup"><span data-stu-id="a5104-519">✔</span></span>|<span data-ttu-id="a5104-520">Permisos de recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-520">Resource permissions for application.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="a5104-521">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="a5104-521">configurableProperties</span></span>

<span data-ttu-id="a5104-522">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="a5104-522">**Optional** - array</span></span>

<span data-ttu-id="a5104-523">El `configurableProperties` bloque define las propiedades de la aplicación que Teams los administradores pueden personalizar.</span><span class="sxs-lookup"><span data-stu-id="a5104-523">The `configurableProperties` block defines the app properties that Teams admins can customize.</span></span> <span data-ttu-id="a5104-524">Para obtener más información, consulta [Habilitar la personalización de la aplicación](~/concepts/design/enable-app-customization.md).</span><span class="sxs-lookup"><span data-stu-id="a5104-524">For more information, see [enable app customization](~/concepts/design/enable-app-customization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a5104-525">Debe definirse un mínimo de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="a5104-525">A minimum of one property must be defined.</span></span> <span data-ttu-id="a5104-526">Puede definir un máximo de nueve propiedades en este bloque.</span><span class="sxs-lookup"><span data-stu-id="a5104-526">You can define a maximum of nine properties in this block.</span></span>

<span data-ttu-id="a5104-527">Puede definir cualquiera de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="a5104-527">You can define any of the following properties:</span></span>

* <span data-ttu-id="a5104-528">`name`: nombre para mostrar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-528">`name`: The app's display name.</span></span>
* <span data-ttu-id="a5104-529">`shortDescription`: descripción breve de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-529">`shortDescription`: The app's short description.</span></span>
* <span data-ttu-id="a5104-530">`longDescription`: descripción detallada de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-530">`longDescription`: The app's detailed description.</span></span>
* <span data-ttu-id="a5104-531">`smallImageUrl`: icono de esquema de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-531">`smallImageUrl`: The app's outline icon.</span></span>
* <span data-ttu-id="a5104-532">`largeImageUrl`: icono de color de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-532">`largeImageUrl`: The app's color icon.</span></span>
* <span data-ttu-id="a5104-533">`accentColor`: color que se usará junto con y como fondo para los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="a5104-533">`accentColor`: The color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="a5104-534">`developerUrl`: la dirección URL HTTPS del sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a5104-534">`developerUrl`: The HTTPS URL of the developer's website.</span></span>
* <span data-ttu-id="a5104-535">`privacyUrl`: la dirección URL HTTPS de la directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a5104-535">`privacyUrl`: The HTTPS URL of the developer's privacy policy.</span></span>
* <span data-ttu-id="a5104-536">`termsOfUseUrl`: la dirección URL HTTPS de los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a5104-536">`termsOfUseUrl`: The HTTPS URL of the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="a5104-537">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="a5104-537">defaultInstallScope</span></span>

<span data-ttu-id="a5104-538">**Opcional** : cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-538">**Optional** - string</span></span>

<span data-ttu-id="a5104-539">Especifica el ámbito de instalación definido para esta aplicación de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a5104-539">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="a5104-540">El ámbito definido será la opción que se muestra en el botón cuando un usuario intente agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-540">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="a5104-541">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="a5104-541">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="a5104-542">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="a5104-542">defaultGroupCapability</span></span>

<span data-ttu-id="a5104-543">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="a5104-543">**Optional** - object</span></span>

<span data-ttu-id="a5104-544">Cuando se selecciona un ámbito de instalación de grupo, se definirá la funcionalidad predeterminada cuando el usuario instale la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5104-544">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="a5104-545">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="a5104-545">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="a5104-546">Nombre</span><span class="sxs-lookup"><span data-stu-id="a5104-546">Name</span></span>| <span data-ttu-id="a5104-547">Tipo</span><span class="sxs-lookup"><span data-stu-id="a5104-547">Type</span></span>| <span data-ttu-id="a5104-548">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="a5104-548">Maximum size</span></span> | <span data-ttu-id="a5104-549">Necesario</span><span class="sxs-lookup"><span data-stu-id="a5104-549">Required</span></span> | <span data-ttu-id="a5104-550">Descripción</span><span class="sxs-lookup"><span data-stu-id="a5104-550">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="a5104-551">string</span><span class="sxs-lookup"><span data-stu-id="a5104-551">string</span></span>|||<span data-ttu-id="a5104-552">Cuando el ámbito de instalación seleccionado es `team` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="a5104-552">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="a5104-553">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="a5104-553">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="a5104-554">cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-554">string</span></span>|||<span data-ttu-id="a5104-555">Cuando el ámbito de instalación seleccionado es `groupchat` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="a5104-555">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="a5104-556">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="a5104-556">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="a5104-557">cadena</span><span class="sxs-lookup"><span data-stu-id="a5104-557">string</span></span>|||<span data-ttu-id="a5104-558">Cuando el ámbito de instalación seleccionado es `meetings` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="a5104-558">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="a5104-559">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="a5104-559">Options: `tab`, `bot`, or `connector`.</span></span>|
