---
title: Referencia de esquema de manifiesto de vista previa del desarrollador
description: Describe el esquema admitido por el manifiesto para Microsoft Teams
ms.topic: reference
keywords: equipos manifiestan esquema Developer Preview
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: b52d52f96312dc2978844b07a0f7ebb1d817166d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566708"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="caef6-104">Esquema de manifiesto de vista previa del desarrollador para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="caef6-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="caef6-105">Consulte [Vista previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md) para obtener información sobre el programa y cómo puede unirse.</span><span class="sxs-lookup"><span data-stu-id="caef6-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="caef6-106">Si no está utilizando la vista previa del desarrollador, no debería usar esta versión del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="caef6-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="caef6-107">Consulte [Referencia: esquema de manifiesto para Microsoft Teams](~/resources/schema/manifest-schema.md) para la versión pública del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="caef6-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="caef6-108">El manifiesto Microsoft Teams describe cómo se integra la aplicación en el producto Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="caef6-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="caef6-109">El manifiesto debe ajustarse al esquema hospedado en [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="caef6-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="caef6-110">Para obtener más información sobre las características disponibles, consulte: [Características de la vista previa del desarrollador público para Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span><span class="sxs-lookup"><span data-stu-id="caef6-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="caef6-111">Muestra de manifiesto completo</span><span class="sxs-lookup"><span data-stu-id="caef6-111">Sample full manifest</span></span>

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

<span data-ttu-id="caef6-112">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="caef6-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="caef6-113">$schema</span><span class="sxs-lookup"><span data-stu-id="caef6-113">$schema</span></span>

<span data-ttu-id="caef6-114">*Opcional, pero recomendado* &ndash; cuerda</span><span class="sxs-lookup"><span data-stu-id="caef6-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="caef6-115">La dirección URL https:// que hace referencia al esquema JSON del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="caef6-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="caef6-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="caef6-116">manifestVersion</span></span>

<span data-ttu-id="caef6-117">**Requerido** &ndash; cuerda</span><span class="sxs-lookup"><span data-stu-id="caef6-117">**Required** &ndash; String</span></span>

<span data-ttu-id="caef6-118">La versión del esquema de manifiesto que este manifiesto está utilizando.</span><span class="sxs-lookup"><span data-stu-id="caef6-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="caef6-119">Debe ser "devPreview".</span><span class="sxs-lookup"><span data-stu-id="caef6-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="caef6-120">version</span><span class="sxs-lookup"><span data-stu-id="caef6-120">version</span></span>

<span data-ttu-id="caef6-121">**Requerido** &ndash; cuerda</span><span class="sxs-lookup"><span data-stu-id="caef6-121">**Required** &ndash; String</span></span>

<span data-ttu-id="caef6-122">La versión de la aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="caef6-122">The version of the specific app.</span></span> <span data-ttu-id="caef6-123">Si actualiza algo en el manifiesto, la versión también debe incrementarse.</span><span class="sxs-lookup"><span data-stu-id="caef6-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="caef6-124">De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="caef6-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="caef6-125">Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y volver a validarse.</span><span class="sxs-lookup"><span data-stu-id="caef6-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="caef6-126">A continuación, los usuarios de esta aplicación obtendrán el nuevo manifiesto actualizado automáticamente en unas horas, después de que se apruebe.</span><span class="sxs-lookup"><span data-stu-id="caef6-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="caef6-127">Si cambian los permisos solicitados por la aplicación, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="caef6-128">Esta cadena de versión debe seguir el estándar [de semver](http://semver.org/) (MAJOR. menor. PARCHE).</span><span class="sxs-lookup"><span data-stu-id="caef6-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="caef6-129">id</span><span class="sxs-lookup"><span data-stu-id="caef6-129">id</span></span>

<span data-ttu-id="caef6-130">**Requerido** &ndash; Identificador de aplicación de Microsoft</span><span class="sxs-lookup"><span data-stu-id="caef6-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="caef6-131">El identificador único generado por Microsoft para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="caef6-132">Si ha registrado un bot a través de la Microsoft Bot Framework, o la aplicación web de su pestaña ya inicia sesión con Microsoft, ya debe tener un IDENTIFICADOR y debe introducirlo aquí.</span><span class="sxs-lookup"><span data-stu-id="caef6-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="caef6-133">De lo contrario, debe generar un nuevo identificador en el Portal de registro de aplicaciones de Microsoft ([Mis aplicaciones](https://apps.dev.microsoft.com)), escribirlo aquí y, a continuación, reutilizarlo al agregar [un bot](~/bots/how-to/create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="caef6-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="caef6-134">packageName</span><span class="sxs-lookup"><span data-stu-id="caef6-134">packageName</span></span>

<span data-ttu-id="caef6-135">**Requerido** &ndash; cuerda</span><span class="sxs-lookup"><span data-stu-id="caef6-135">**Required** &ndash; String</span></span>

<span data-ttu-id="caef6-136">Un identificador único para esta aplicación en notación de dominio inverso; por ejemplo, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="caef6-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="caef6-137">developer</span><span class="sxs-lookup"><span data-stu-id="caef6-137">developer</span></span>

<span data-ttu-id="caef6-138">**Required**</span><span class="sxs-lookup"><span data-stu-id="caef6-138">**Required**</span></span>

<span data-ttu-id="caef6-139">Especifica información sobre su empresa.</span><span class="sxs-lookup"><span data-stu-id="caef6-139">Specifies information about your company.</span></span> <span data-ttu-id="caef6-140">Para las aplicaciones enviadas a AppSource (anteriormente Office Store), estos valores deben coincidir con la información de la entrada de AppSource.</span><span class="sxs-lookup"><span data-stu-id="caef6-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="caef6-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-141">Name</span></span>| <span data-ttu-id="caef6-142">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-142">Maximum size</span></span> | <span data-ttu-id="caef6-143">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-143">Required</span></span> | <span data-ttu-id="caef6-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="caef6-145">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-145">32 characters</span></span>|<span data-ttu-id="caef6-146">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-146">✔</span></span>|<span data-ttu-id="caef6-147">El nombre para mostrar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="caef6-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="caef6-148">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-148">2048 characters</span></span>|<span data-ttu-id="caef6-149">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-149">✔</span></span>|<span data-ttu-id="caef6-150">La URL de https:// al sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="caef6-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="caef6-151">Este enlace debe llevar a los usuarios a su empresa o página de destino específica del producto.</span><span class="sxs-lookup"><span data-stu-id="caef6-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="caef6-152">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-152">2048 characters</span></span>|<span data-ttu-id="caef6-153">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-153">✔</span></span>|<span data-ttu-id="caef6-154">La dirección URL de https:// a la política de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="caef6-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="caef6-155">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-155">2048 characters</span></span>|<span data-ttu-id="caef6-156">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-156">✔</span></span>|<span data-ttu-id="caef6-157">La dirección URL https:// a los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="caef6-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="caef6-158">10 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-158">10 characters</span></span>|<span data-ttu-id="caef6-159">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-159">✔</span></span>|<span data-ttu-id="caef6-160">**Opcional** Identificador de red de partners de Microsoft que identifica la organización asociada que compilará la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="caef6-161">localizaciónInfo</span><span class="sxs-lookup"><span data-stu-id="caef6-161">localizationInfo</span></span>

<span data-ttu-id="caef6-162">**Optional**</span><span class="sxs-lookup"><span data-stu-id="caef6-162">**Optional**</span></span>

<span data-ttu-id="caef6-163">Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="caef6-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="caef6-164">Consulte [localización](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="caef6-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="caef6-165">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-165">Name</span></span>| <span data-ttu-id="caef6-166">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-166">Maximum size</span></span> | <span data-ttu-id="caef6-167">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-167">Required</span></span> | <span data-ttu-id="caef6-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="caef6-169">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-169">4 characters</span></span>|<span data-ttu-id="caef6-170">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-170">✔</span></span>|<span data-ttu-id="caef6-171">La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="caef6-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="caef6-172">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="caef6-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="caef6-173">Matriz de objetos que especifica traducciones de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="caef6-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="caef6-174">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-174">Name</span></span>| <span data-ttu-id="caef6-175">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-175">Maximum size</span></span> | <span data-ttu-id="caef6-176">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-176">Required</span></span> | <span data-ttu-id="caef6-177">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="caef6-178">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-178">4 characters</span></span>|<span data-ttu-id="caef6-179">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-179">✔</span></span>|<span data-ttu-id="caef6-180">La etiqueta de idioma de las cadenas del archivo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="caef6-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="caef6-181">4 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-181">4 characters</span></span>|<span data-ttu-id="caef6-182">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-182">✔</span></span>|<span data-ttu-id="caef6-183">Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="caef6-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="caef6-184">name</span><span class="sxs-lookup"><span data-stu-id="caef6-184">name</span></span>

<span data-ttu-id="caef6-185">**Required**</span><span class="sxs-lookup"><span data-stu-id="caef6-185">**Required**</span></span>

<span data-ttu-id="caef6-186">El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia Teams.</span><span class="sxs-lookup"><span data-stu-id="caef6-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="caef6-187">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource.</span><span class="sxs-lookup"><span data-stu-id="caef6-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="caef6-188">Los valores de `short` y no deben ser los `full` mismos.</span><span class="sxs-lookup"><span data-stu-id="caef6-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="caef6-189">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-189">Name</span></span>| <span data-ttu-id="caef6-190">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-190">Maximum size</span></span> | <span data-ttu-id="caef6-191">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-191">Required</span></span> | <span data-ttu-id="caef6-192">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="caef6-193">30 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-193">30 characters</span></span>|<span data-ttu-id="caef6-194">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-194">✔</span></span>|<span data-ttu-id="caef6-195">El nombre para mostrar corto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="caef6-196">100 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-196">100 characters</span></span>||<span data-ttu-id="caef6-197">El nombre completo de la aplicación, utilizado si el nombre completo de la aplicación supera los 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="caef6-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="caef6-198">description</span><span class="sxs-lookup"><span data-stu-id="caef6-198">description</span></span>

<span data-ttu-id="caef6-199">**Required**</span><span class="sxs-lookup"><span data-stu-id="caef6-199">**Required**</span></span>

<span data-ttu-id="caef6-200">Describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="caef6-200">Describes your app to users.</span></span> <span data-ttu-id="caef6-201">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource.</span><span class="sxs-lookup"><span data-stu-id="caef6-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="caef6-202">Asegúrese de que su descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a entender lo que hace su experiencia.</span><span class="sxs-lookup"><span data-stu-id="caef6-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="caef6-203">También debe tener en cuenta, en la descripción completa, si se requiere una cuenta externa para su uso.</span><span class="sxs-lookup"><span data-stu-id="caef6-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="caef6-204">Los valores de `short` y no deben ser los `full` mismos.</span><span class="sxs-lookup"><span data-stu-id="caef6-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="caef6-205">La breve descripción no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="caef6-206">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-206">Name</span></span>| <span data-ttu-id="caef6-207">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-207">Maximum size</span></span> | <span data-ttu-id="caef6-208">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-208">Required</span></span> | <span data-ttu-id="caef6-209">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="caef6-210">80 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-210">80 characters</span></span>|<span data-ttu-id="caef6-211">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-211">✔</span></span>|<span data-ttu-id="caef6-212">Una breve descripción de la experiencia de la aplicación, utilizada cuando el espacio es limitado.</span><span class="sxs-lookup"><span data-stu-id="caef6-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="caef6-213">4000 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-213">4000 characters</span></span>|<span data-ttu-id="caef6-214">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-214">✔</span></span>|<span data-ttu-id="caef6-215">La descripción completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="caef6-216">iconos</span><span class="sxs-lookup"><span data-stu-id="caef6-216">icons</span></span>

<span data-ttu-id="caef6-217">**Required**</span><span class="sxs-lookup"><span data-stu-id="caef6-217">**Required**</span></span>

<span data-ttu-id="caef6-218">Iconos utilizados en la aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="caef6-218">Icons used within the Teams app.</span></span> <span data-ttu-id="caef6-219">Los archivos de icono deben incluirse como parte del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="caef6-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="caef6-220">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-220">Name</span></span>| <span data-ttu-id="caef6-221">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-221">Maximum size</span></span> | <span data-ttu-id="caef6-222">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-222">Required</span></span> | <span data-ttu-id="caef6-223">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="caef6-224">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-224">2048 characters</span></span>|<span data-ttu-id="caef6-225">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-225">✔</span></span>|<span data-ttu-id="caef6-226">Una ruta de acceso de archivo relativa a un icono de contorno PNG 32x32 transparente.</span><span class="sxs-lookup"><span data-stu-id="caef6-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="caef6-227">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-227">2048 characters</span></span>|<span data-ttu-id="caef6-228">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-228">✔</span></span>|<span data-ttu-id="caef6-229">Una ruta de acceso de archivo relativa a un icono PNG 192x192 a todo color.</span><span class="sxs-lookup"><span data-stu-id="caef6-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="caef6-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="caef6-230">accentColor</span></span>

<span data-ttu-id="caef6-231">**Requerido** &ndash; cuerda</span><span class="sxs-lookup"><span data-stu-id="caef6-231">**Required** &ndash; String</span></span>

<span data-ttu-id="caef6-232">Un color para usar junto con y como fondo para los iconos de contorno.</span><span class="sxs-lookup"><span data-stu-id="caef6-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="caef6-233">El valor debe ser un código de color HTML válido que comience por '#', por `#4464ee` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="caef6-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="caef6-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="caef6-234">configurableTabs</span></span>

<span data-ttu-id="caef6-235">**Optional**</span><span class="sxs-lookup"><span data-stu-id="caef6-235">**Optional**</span></span>

<span data-ttu-id="caef6-236">Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de equipo que requiere configuración adicional antes de agregarla.</span><span class="sxs-lookup"><span data-stu-id="caef6-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="caef6-237">Las pestañas configurables solo se admiten en el ámbito de los equipos y actualmente solo se admite una pestaña por aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="caef6-238">El objeto es una matriz con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="caef6-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="caef6-239">Este bloque solo es necesario para soluciones que proporcionan una solución de pestaña de canal configurable.</span><span class="sxs-lookup"><span data-stu-id="caef6-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="caef6-240">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-240">Name</span></span>| <span data-ttu-id="caef6-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="caef6-241">Type</span></span>| <span data-ttu-id="caef6-242">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-242">Maximum size</span></span> | <span data-ttu-id="caef6-243">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-243">Required</span></span> | <span data-ttu-id="caef6-244">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="caef6-245">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-245">String</span></span>|<span data-ttu-id="caef6-246">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-246">2048 characters</span></span>|<span data-ttu-id="caef6-247">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-247">✔</span></span>|<span data-ttu-id="caef6-248">La dirección URL https:// que se usará al configurar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="caef6-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="caef6-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="caef6-249">Boolean</span></span>|||<span data-ttu-id="caef6-250">Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de la creación.</span><span class="sxs-lookup"><span data-stu-id="caef6-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="caef6-251">predeterminado: `true`</span><span class="sxs-lookup"><span data-stu-id="caef6-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="caef6-252">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="caef6-252">Array of enum</span></span>|<span data-ttu-id="caef6-253">1</span><span class="sxs-lookup"><span data-stu-id="caef6-253">1</span></span>|<span data-ttu-id="caef6-254">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-254">✔</span></span>|<span data-ttu-id="caef6-255">Actualmente, las pestañas configurables solo admiten el `team` `groupchat` ámbito.</span><span class="sxs-lookup"><span data-stu-id="caef6-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="caef6-256">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-256">String</span></span>|<span data-ttu-id="caef6-257">2048</span><span class="sxs-lookup"><span data-stu-id="caef6-257">2048</span></span>||<span data-ttu-id="caef6-258">Una ruta de acceso de archivo relativa a una imagen de vista previa de tabulación para su uso en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="caef6-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="caef6-259">Tamaño 1024x768.</span><span class="sxs-lookup"><span data-stu-id="caef6-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="caef6-260">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="caef6-260">Array of enum</span></span>|<span data-ttu-id="caef6-261">1</span><span class="sxs-lookup"><span data-stu-id="caef6-261">1</span></span>||<span data-ttu-id="caef6-262">Define cómo se pondrá a disposición su pestaña en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="caef6-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="caef6-263">Las opciones son `sharePointFullPage` y `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="caef6-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="caef6-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="caef6-264">staticTabs</span></span>

<span data-ttu-id="caef6-265">**Optional**</span><span class="sxs-lookup"><span data-stu-id="caef6-265">**Optional**</span></span>

<span data-ttu-id="caef6-266">Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente.</span><span class="sxs-lookup"><span data-stu-id="caef6-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="caef6-267">Las pestañas estáticas declaradas en `personal` el ámbito siempre están ancladas a la experiencia personal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="caef6-268">Actualmente no se admiten pestañas estáticas declaradas en el `team` ámbito.</span><span class="sxs-lookup"><span data-stu-id="caef6-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="caef6-269">El objeto es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="caef6-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="caef6-270">Este bloque solo es necesario para soluciones que proporcionan una solución de pestaña estática.</span><span class="sxs-lookup"><span data-stu-id="caef6-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="caef6-271">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-271">Name</span></span>| <span data-ttu-id="caef6-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="caef6-272">Type</span></span>| <span data-ttu-id="caef6-273">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-273">Maximum size</span></span> | <span data-ttu-id="caef6-274">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-274">Required</span></span> | <span data-ttu-id="caef6-275">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="caef6-276">String</span><span class="sxs-lookup"><span data-stu-id="caef6-276">String</span></span>|<span data-ttu-id="caef6-277">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-277">64 characters</span></span>|<span data-ttu-id="caef6-278">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-278">✔</span></span>|<span data-ttu-id="caef6-279">Identificador único de la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="caef6-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="caef6-280">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-280">String</span></span>|<span data-ttu-id="caef6-281">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-281">128 characters</span></span>|<span data-ttu-id="caef6-282">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-282">✔</span></span>|<span data-ttu-id="caef6-283">El nombre para mostrar de la pestaña en la interfaz del canal.</span><span class="sxs-lookup"><span data-stu-id="caef6-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="caef6-284">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-284">String</span></span>|<span data-ttu-id="caef6-285">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-285">2048 characters</span></span>|<span data-ttu-id="caef6-286">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-286">✔</span></span>|<span data-ttu-id="caef6-287">La dirección URL de https:// que apunta a la interfaz de usuario de la entidad que se mostrará en el lienzo de Teams.</span><span class="sxs-lookup"><span data-stu-id="caef6-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="caef6-288">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-288">String</span></span>|<span data-ttu-id="caef6-289">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-289">2048 characters</span></span>||<span data-ttu-id="caef6-290">La dirección URL https:// a la que apuntar si un usuario opta por verlo en un explorador.</span><span class="sxs-lookup"><span data-stu-id="caef6-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="caef6-291">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="caef6-291">Array of enum</span></span>|<span data-ttu-id="caef6-292">1</span><span class="sxs-lookup"><span data-stu-id="caef6-292">1</span></span>|<span data-ttu-id="caef6-293">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-293">✔</span></span>|<span data-ttu-id="caef6-294">Actualmente, las pestañas estáticas solo admiten el `personal` ámbito, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.</span><span class="sxs-lookup"><span data-stu-id="caef6-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="caef6-295">Bots</span><span class="sxs-lookup"><span data-stu-id="caef6-295">bots</span></span>

<span data-ttu-id="caef6-296">**Optional**</span><span class="sxs-lookup"><span data-stu-id="caef6-296">**Optional**</span></span>

<span data-ttu-id="caef6-297">Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="caef6-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="caef6-298">El objeto es una matriz (máximo de solo 1 elemento &mdash; actualmente solo se permite un bot por aplicación) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="caef6-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="caef6-299">Este bloque solo es necesario para soluciones que proporcionan una experiencia de bot.</span><span class="sxs-lookup"><span data-stu-id="caef6-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="caef6-300">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-300">Name</span></span>| <span data-ttu-id="caef6-301">Tipo</span><span class="sxs-lookup"><span data-stu-id="caef6-301">Type</span></span>| <span data-ttu-id="caef6-302">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-302">Maximum size</span></span> | <span data-ttu-id="caef6-303">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-303">Required</span></span> | <span data-ttu-id="caef6-304">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="caef6-305">String</span><span class="sxs-lookup"><span data-stu-id="caef6-305">String</span></span>|<span data-ttu-id="caef6-306">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-306">64 characters</span></span>|<span data-ttu-id="caef6-307">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-307">✔</span></span>|<span data-ttu-id="caef6-308">El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="caef6-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="caef6-309">Esto bien puede ser el mismo que el IDENTIFICADOR general de la [aplicación.](#id)</span><span class="sxs-lookup"><span data-stu-id="caef6-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="caef6-310">Booleano</span><span class="sxs-lookup"><span data-stu-id="caef6-310">Boolean</span></span>|||<span data-ttu-id="caef6-311">Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico.</span><span class="sxs-lookup"><span data-stu-id="caef6-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="caef6-312">predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="caef6-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="caef6-313">Booleano</span><span class="sxs-lookup"><span data-stu-id="caef6-313">Boolean</span></span>|||<span data-ttu-id="caef6-314">Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación.</span><span class="sxs-lookup"><span data-stu-id="caef6-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="caef6-315">predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="caef6-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="caef6-316">Booleano</span><span class="sxs-lookup"><span data-stu-id="caef6-316">Boolean</span></span>|||<span data-ttu-id="caef6-317">Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal.</span><span class="sxs-lookup"><span data-stu-id="caef6-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="caef6-318">predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="caef6-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="caef6-319">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="caef6-319">Array of enum</span></span>|<span data-ttu-id="caef6-320">3</span><span class="sxs-lookup"><span data-stu-id="caef6-320">3</span></span>|<span data-ttu-id="caef6-321">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-321">✔</span></span>|<span data-ttu-id="caef6-322">Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`).</span><span class="sxs-lookup"><span data-stu-id="caef6-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="caef6-323">Estas opciones no son exclusivas.</span><span class="sxs-lookup"><span data-stu-id="caef6-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="caef6-324">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="caef6-324">bots.commandLists</span></span>

<span data-ttu-id="caef6-325">Una lista opcional de comandos que el bot puede recomendar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="caef6-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="caef6-326">El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de `object` comandos independiente para cada ámbito que admita el bot.</span><span class="sxs-lookup"><span data-stu-id="caef6-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="caef6-327">Para obtener más información, consulte [menús Bot](~/bots/how-to/create-a-bot-commands-menu.md).</span><span class="sxs-lookup"><span data-stu-id="caef6-327">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="caef6-328">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-328">Name</span></span>| <span data-ttu-id="caef6-329">Tipo</span><span class="sxs-lookup"><span data-stu-id="caef6-329">Type</span></span>| <span data-ttu-id="caef6-330">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-330">Maximum size</span></span> | <span data-ttu-id="caef6-331">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-331">Required</span></span> | <span data-ttu-id="caef6-332">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="caef6-333">matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="caef6-333">array of enum</span></span>|<span data-ttu-id="caef6-334">3</span><span class="sxs-lookup"><span data-stu-id="caef6-334">3</span></span>|<span data-ttu-id="caef6-335">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-335">✔</span></span>|<span data-ttu-id="caef6-336">Especifica el ámbito para el que la lista de comandos es válida.</span><span class="sxs-lookup"><span data-stu-id="caef6-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="caef6-337">Las opciones son `team`, `personal` y `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="caef6-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="caef6-338">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="caef6-338">array of objects</span></span>|<span data-ttu-id="caef6-339">10</span><span class="sxs-lookup"><span data-stu-id="caef6-339">10</span></span>|<span data-ttu-id="caef6-340">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-340">✔</span></span>|<span data-ttu-id="caef6-341">Una matriz de comandos que el bot admite:</span><span class="sxs-lookup"><span data-stu-id="caef6-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="caef6-342">`title`: el nombre del comando bot (cadena, 32).</span><span class="sxs-lookup"><span data-stu-id="caef6-342">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="caef6-343">`description`: una descripción simple o ejemplo de la sintaxis del comando y su argumento (cadena, 128).</span><span class="sxs-lookup"><span data-stu-id="caef6-343">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="caef6-344">Conectores</span><span class="sxs-lookup"><span data-stu-id="caef6-344">connectors</span></span>

<span data-ttu-id="caef6-345">**Optional**</span><span class="sxs-lookup"><span data-stu-id="caef6-345">**Optional**</span></span>

<span data-ttu-id="caef6-346">El `connectors` bloque define un conector de Office 365 para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="caef6-347">El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="caef6-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="caef6-348">Este bloque solo es necesario para las soluciones que proporcionan un conector.</span><span class="sxs-lookup"><span data-stu-id="caef6-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="caef6-349">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-349">Name</span></span>| <span data-ttu-id="caef6-350">Tipo</span><span class="sxs-lookup"><span data-stu-id="caef6-350">Type</span></span>| <span data-ttu-id="caef6-351">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-351">Maximum size</span></span> | <span data-ttu-id="caef6-352">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-352">Required</span></span> | <span data-ttu-id="caef6-353">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="caef6-354">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-354">String</span></span>|<span data-ttu-id="caef6-355">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-355">2048 characters</span></span>|<span data-ttu-id="caef6-356">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-356">✔</span></span>|<span data-ttu-id="caef6-357">La dirección URL https:// que se usará al configurar el conector.</span><span class="sxs-lookup"><span data-stu-id="caef6-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="caef6-358">String</span><span class="sxs-lookup"><span data-stu-id="caef6-358">String</span></span>|<span data-ttu-id="caef6-359">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-359">64 characters</span></span>|<span data-ttu-id="caef6-360">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-360">✔</span></span>|<span data-ttu-id="caef6-361">Identificador único del conector que coincide con su identificador en el [panel de desarrollador de conectores.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="caef6-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="caef6-362">Matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="caef6-362">Array of enum</span></span>|<span data-ttu-id="caef6-363">1</span><span class="sxs-lookup"><span data-stu-id="caef6-363">1</span></span>|<span data-ttu-id="caef6-364">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-364">✔</span></span>|<span data-ttu-id="caef6-365">Especifica si connector ofrece una experiencia en el contexto de un canal en un `team` objeto y una experiencia con ámbito a un usuario individual solo ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="caef6-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="caef6-366">Actualmente, solo se admite el `team` ámbito.</span><span class="sxs-lookup"><span data-stu-id="caef6-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="caef6-367">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="caef6-367">composeExtensions</span></span>

<span data-ttu-id="caef6-368">**Optional**</span><span class="sxs-lookup"><span data-stu-id="caef6-368">**Optional**</span></span>

<span data-ttu-id="caef6-369">Define una extensión de mensajería para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="caef6-370">El nombre de la característica se cambió de "extensión de composición" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="caef6-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="caef6-371">El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="caef6-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="caef6-372">Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="caef6-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="caef6-373">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-373">Name</span></span>| <span data-ttu-id="caef6-374">Tipo</span><span class="sxs-lookup"><span data-stu-id="caef6-374">Type</span></span> | <span data-ttu-id="caef6-375">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-375">Maximum Size</span></span> | <span data-ttu-id="caef6-376">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="caef6-376">Required</span></span> | <span data-ttu-id="caef6-377">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="caef6-378">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-378">String</span></span>|<span data-ttu-id="caef6-379">64</span><span class="sxs-lookup"><span data-stu-id="caef6-379">64</span></span>|<span data-ttu-id="caef6-380">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-380">✔</span></span>|<span data-ttu-id="caef6-381">El identificador único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="caef6-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="caef6-382">Esto bien puede ser el mismo que el IDENTIFICADOR general de la [aplicación.](#id)</span><span class="sxs-lookup"><span data-stu-id="caef6-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="caef6-383">Boolean</span><span class="sxs-lookup"><span data-stu-id="caef6-383">Boolean</span></span>|||<span data-ttu-id="caef6-384">Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="caef6-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="caef6-385">El valor predeterminado es `false`.</span><span class="sxs-lookup"><span data-stu-id="caef6-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="caef6-386">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="caef6-386">Array of object</span></span>|<span data-ttu-id="caef6-387">10</span><span class="sxs-lookup"><span data-stu-id="caef6-387">10</span></span>|<span data-ttu-id="caef6-388">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-388">✔</span></span>|<span data-ttu-id="caef6-389">Matriz de comandos que admite la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="caef6-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="caef6-390">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="caef6-390">composeExtensions.commands</span></span>

<span data-ttu-id="caef6-391">La extensión de mensajería debe declarar uno o varios comandos.</span><span class="sxs-lookup"><span data-stu-id="caef6-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="caef6-392">Cada comando aparece en Microsoft Teams como una interacción potencial desde el punto de entrada basado en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="caef6-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="caef6-393">Hay un máximo de 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="caef6-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="caef6-394">Cada elemento de comando es un objeto con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="caef6-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="caef6-395">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-395">Name</span></span>| <span data-ttu-id="caef6-396">Tipo</span><span class="sxs-lookup"><span data-stu-id="caef6-396">Type</span></span>| <span data-ttu-id="caef6-397">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-397">Maximum size</span></span> | <span data-ttu-id="caef6-398">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-398">Required</span></span> | <span data-ttu-id="caef6-399">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="caef6-400">String</span><span class="sxs-lookup"><span data-stu-id="caef6-400">String</span></span>|<span data-ttu-id="caef6-401">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-401">64 characters</span></span>|<span data-ttu-id="caef6-402">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-402">✔</span></span>|<span data-ttu-id="caef6-403">El ID del comando.</span><span class="sxs-lookup"><span data-stu-id="caef6-403">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="caef6-404">String</span><span class="sxs-lookup"><span data-stu-id="caef6-404">String</span></span>|<span data-ttu-id="caef6-405">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-405">64 characters</span></span>||<span data-ttu-id="caef6-406">Tipo de comando.</span><span class="sxs-lookup"><span data-stu-id="caef6-406">Type of the command.</span></span> <span data-ttu-id="caef6-407">Uno de `query` o `action` .</span><span class="sxs-lookup"><span data-stu-id="caef6-407">One of `query` or `action`.</span></span> <span data-ttu-id="caef6-408">predeterminado: `query`</span><span class="sxs-lookup"><span data-stu-id="caef6-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="caef6-409">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-409">String</span></span>|<span data-ttu-id="caef6-410">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-410">32 characters</span></span>|<span data-ttu-id="caef6-411">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-411">✔</span></span>|<span data-ttu-id="caef6-412">El nombre del comando fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="caef6-412">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="caef6-413">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-413">String</span></span>|<span data-ttu-id="caef6-414">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-414">128 characters</span></span>||<span data-ttu-id="caef6-415">La descripción que aparece a los usuarios para indicar el propósito de este comando.</span><span class="sxs-lookup"><span data-stu-id="caef6-415">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="caef6-416">Boolean</span><span class="sxs-lookup"><span data-stu-id="caef6-416">Boolean</span></span>|||<span data-ttu-id="caef6-417">Un valor booleano que indica si el comando debe ejecutarse inicialmente sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="caef6-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="caef6-418">predeterminado: `false`</span><span class="sxs-lookup"><span data-stu-id="caef6-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="caef6-419">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="caef6-419">Array of Strings</span></span>|<span data-ttu-id="caef6-420">3</span><span class="sxs-lookup"><span data-stu-id="caef6-420">3</span></span>||<span data-ttu-id="caef6-421">Define desde dónde se puede invocar la extensión de mensaje.</span><span class="sxs-lookup"><span data-stu-id="caef6-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="caef6-422">Cualquier combinación de `compose` `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="caef6-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="caef6-423">El valor predeterminado es `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="caef6-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="caef6-424">Boolean</span><span class="sxs-lookup"><span data-stu-id="caef6-424">Boolean</span></span>|||<span data-ttu-id="caef6-425">Valor booleano que indica si debe recuperar el módulo de tareas dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="caef6-425">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="caef6-426">Objeto</span><span class="sxs-lookup"><span data-stu-id="caef6-426">Object</span></span>|||<span data-ttu-id="caef6-427">Especifique el módulo de tareas que se va a precargar al utilizar un comando de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="caef6-427">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="caef6-428">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-428">String</span></span>|<span data-ttu-id="caef6-429">64</span><span class="sxs-lookup"><span data-stu-id="caef6-429">64</span></span>||<span data-ttu-id="caef6-430">Título inicial del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="caef6-430">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="caef6-431">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-431">String</span></span>|||<span data-ttu-id="caef6-432">Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "medio" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="caef6-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="caef6-433">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-433">String</span></span>|||<span data-ttu-id="caef6-434">Altura del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "medio" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="caef6-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="caef6-435">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-435">String</span></span>|||<span data-ttu-id="caef6-436">URL de vista web inicial.</span><span class="sxs-lookup"><span data-stu-id="caef6-436">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="caef6-437">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="caef6-437">Array of Objects</span></span>|<span data-ttu-id="caef6-438">5 </span><span class="sxs-lookup"><span data-stu-id="caef6-438">5</span></span>||<span data-ttu-id="caef6-439">Una lista de controladores que permiten invocar aplicaciones cuando se cumplen ciertas condiciones.</span><span class="sxs-lookup"><span data-stu-id="caef6-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="caef6-440">Los dominios también deben aparecer en `validDomains` .</span><span class="sxs-lookup"><span data-stu-id="caef6-440">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="caef6-441">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-441">String</span></span>|||<span data-ttu-id="caef6-442">El tipo de controlador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="caef6-442">The type of message handler.</span></span> <span data-ttu-id="caef6-443">Debe ser `"link"`.</span><span class="sxs-lookup"><span data-stu-id="caef6-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="caef6-444">Matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="caef6-444">Array of Strings</span></span>|||<span data-ttu-id="caef6-445">Matriz de dominios para los que el controlador de mensajes de vínculo puede registrarse.</span><span class="sxs-lookup"><span data-stu-id="caef6-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="caef6-446">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="caef6-446">Array of object</span></span>|<span data-ttu-id="caef6-447">5 </span><span class="sxs-lookup"><span data-stu-id="caef6-447">5</span></span>|<span data-ttu-id="caef6-448">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-448">✔</span></span>|<span data-ttu-id="caef6-449">La lista de parámetros que toma el comando.</span><span class="sxs-lookup"><span data-stu-id="caef6-449">The list of parameters the command takes.</span></span> <span data-ttu-id="caef6-450">Mínimo: 1; máximo: 5</span><span class="sxs-lookup"><span data-stu-id="caef6-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="caef6-451">String</span><span class="sxs-lookup"><span data-stu-id="caef6-451">String</span></span>|<span data-ttu-id="caef6-452">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-452">64 characters</span></span>|<span data-ttu-id="caef6-453">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-453">✔</span></span>|<span data-ttu-id="caef6-454">El nombre del parámetro tal como aparece en el cliente.</span><span class="sxs-lookup"><span data-stu-id="caef6-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="caef6-455">Esto se incluye en la solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="caef6-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="caef6-456">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-456">String</span></span>|<span data-ttu-id="caef6-457">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-457">32 characters</span></span>|<span data-ttu-id="caef6-458">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-458">✔</span></span>|<span data-ttu-id="caef6-459">Título fácil de usar para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="caef6-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="caef6-460">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-460">String</span></span>|<span data-ttu-id="caef6-461">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-461">128 characters</span></span>||<span data-ttu-id="caef6-462">Cadena fácil de usar que describe el propósito de este parámetro.</span><span class="sxs-lookup"><span data-stu-id="caef6-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="caef6-463">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-463">String</span></span>|<span data-ttu-id="caef6-464">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-464">128 characters</span></span>||<span data-ttu-id="caef6-465">Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="caef6-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="caef6-466">Uno de `text` , , , , , `textarea` `number` `date` `time` `toggle` `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="caef6-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="caef6-467">Matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="caef6-467">Array of Objects</span></span>|<span data-ttu-id="caef6-468">10</span><span class="sxs-lookup"><span data-stu-id="caef6-468">10</span></span>||<span data-ttu-id="caef6-469">Las opciones de elección para el `choiceset` archivo .</span><span class="sxs-lookup"><span data-stu-id="caef6-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="caef6-470">Utilice únicamente cuando `parameter.inputType` sea `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="caef6-470">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="caef6-471">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-471">String</span></span>|<span data-ttu-id="caef6-472">128</span><span class="sxs-lookup"><span data-stu-id="caef6-472">128</span></span>||<span data-ttu-id="caef6-473">Título de la elección.</span><span class="sxs-lookup"><span data-stu-id="caef6-473">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="caef6-474">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-474">String</span></span>|<span data-ttu-id="caef6-475">512</span><span class="sxs-lookup"><span data-stu-id="caef6-475">512</span></span>||<span data-ttu-id="caef6-476">Valor de la elección.</span><span class="sxs-lookup"><span data-stu-id="caef6-476">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="caef6-477">permisos</span><span class="sxs-lookup"><span data-stu-id="caef6-477">permissions</span></span>

<span data-ttu-id="caef6-478">**Optional**</span><span class="sxs-lookup"><span data-stu-id="caef6-478">**Optional**</span></span>

<span data-ttu-id="caef6-479">Una matriz de `string` la que se especifica qué permisos solicita la aplicación, lo que permite a los usuarios finales saber cómo se realizará la extensión.</span><span class="sxs-lookup"><span data-stu-id="caef6-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="caef6-480">Las siguientes opciones no son exclusivas:</span><span class="sxs-lookup"><span data-stu-id="caef6-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="caef6-481">`identity`&emsp;Requiere información de identidad de usuario.</span><span class="sxs-lookup"><span data-stu-id="caef6-481">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="caef6-482">`messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="caef6-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="caef6-483">Cambiar estos permisos al actualizar la aplicación hará que los usuarios repitan el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="caef6-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="caef6-484">dispositivoPermissions</span><span class="sxs-lookup"><span data-stu-id="caef6-484">devicePermissions</span></span>

<span data-ttu-id="caef6-485">**Opcional** Matriz de cuerdas</span><span class="sxs-lookup"><span data-stu-id="caef6-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="caef6-486">Especifica las características nativas en el dispositivo de un usuario al que la aplicación puede solicitar acceso.</span><span class="sxs-lookup"><span data-stu-id="caef6-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="caef6-487">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="caef6-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="caef6-488">validDomains</span><span class="sxs-lookup"><span data-stu-id="caef6-488">validDomains</span></span>

<span data-ttu-id="caef6-489">**Opcional,** excepto **requerido** cuando se indique</span><span class="sxs-lookup"><span data-stu-id="caef6-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="caef6-490">Una lista de dominios válidos desde los que la aplicación espera cargar cualquier contenido.</span><span class="sxs-lookup"><span data-stu-id="caef6-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="caef6-491">Los listados de dominios pueden incluir comodines, por `*.example.com` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="caef6-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="caef6-492">Esto coincide exactamente con un segmento del dominio; si necesita `a.b.example.com` coincidir, utilice `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="caef6-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="caef6-493">Si la configuración de la pestaña o la interfaz de usuario de contenido deben navegar a cualquier otro dominio además del que se usa para la configuración de pestañas, ese dominio debe especificarse aquí.</span><span class="sxs-lookup"><span data-stu-id="caef6-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="caef6-494">Sin embargo, **no** es necesario incluir los dominios de los proveedores de identidades que desea admitir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="caef6-495">Por ejemplo, para autenticarse con un ID de Google, es necesario redirigir a accounts.google.com, pero no debe incluir accounts.google.com en `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="caef6-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="caef6-496">No agregue dominios que estén fuera de su control, ya sea directamente o a través de comodines.</span><span class="sxs-lookup"><span data-stu-id="caef6-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="caef6-497">Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="caef6-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="caef6-498">El objeto es una matriz con todos los elementos del tipo `string` .</span><span class="sxs-lookup"><span data-stu-id="caef6-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="caef6-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="caef6-499">webApplicationInfo</span></span>

<span data-ttu-id="caef6-500">**Optional**</span><span class="sxs-lookup"><span data-stu-id="caef6-500">**Optional**</span></span>

<span data-ttu-id="caef6-501">Especifique el ID de aplicación de AAD y Graph información para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación AAD.</span><span class="sxs-lookup"><span data-stu-id="caef6-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="caef6-502">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-502">Name</span></span>| <span data-ttu-id="caef6-503">Tipo</span><span class="sxs-lookup"><span data-stu-id="caef6-503">Type</span></span>| <span data-ttu-id="caef6-504">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-504">Maximum size</span></span> | <span data-ttu-id="caef6-505">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-505">Required</span></span> | <span data-ttu-id="caef6-506">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="caef6-507">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-507">String</span></span>|<span data-ttu-id="caef6-508">36 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-508">36 characters</span></span>|<span data-ttu-id="caef6-509">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-509">✔</span></span>|<span data-ttu-id="caef6-510">Identificador de aplicación AAD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-510">AAD application id of the app.</span></span> <span data-ttu-id="caef6-511">Este id debe ser un GUID.</span><span class="sxs-lookup"><span data-stu-id="caef6-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="caef6-512">Cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-512">String</span></span>|<span data-ttu-id="caef6-513">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="caef6-513">2048 characters</span></span>|<span data-ttu-id="caef6-514">✔</span><span class="sxs-lookup"><span data-stu-id="caef6-514">✔</span></span>|<span data-ttu-id="caef6-515">Url de recurso de la aplicación para adquirir token de autenticación para SSO.</span><span class="sxs-lookup"><span data-stu-id="caef6-515">Resource url of app for acquiring auth token for SSO.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="caef6-516">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="caef6-516">configurableProperties</span></span>

<span data-ttu-id="caef6-517">**Opcional** - matriz</span><span class="sxs-lookup"><span data-stu-id="caef6-517">**Optional** - array</span></span>

<span data-ttu-id="caef6-518">El `configurableProperties` bloque define las propiedades de la aplicación que Teams administrador puede personalizar.</span><span class="sxs-lookup"><span data-stu-id="caef6-518">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="caef6-519">Para obtener más información, consulte [personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="caef6-519">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="caef6-520">Se debe definir un mínimo de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="caef6-520">A minimum of one property must be defined.</span></span> <span data-ttu-id="caef6-521">Puede definir un máximo de nueve propiedades en este bloque.</span><span class="sxs-lookup"><span data-stu-id="caef6-521">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="caef6-522">Como práctica recomendada, debe proporcionar directrices de personalización para que los usuarios y clientes de la aplicación las sigan al personalizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-522">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> 

<span data-ttu-id="caef6-523">Puede definir cualquiera de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="caef6-523">You can define any of the following properties:</span></span>
* <span data-ttu-id="caef6-524">`name`: Permite al administrador cambiar el nombre para mostrar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-524">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="caef6-525">`shortDescription`: Permite al administrador cambiar la breve descripción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-525">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="caef6-526">`longDescription`: Permite al administrador cambiar la descripción detallada de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-526">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="caef6-527">`smallImageUrl`: Es la `outline` propiedad en el bloque del `icons` manifiesto.</span><span class="sxs-lookup"><span data-stu-id="caef6-527">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="caef6-528">`largeImageUrl`: Es la `color` propiedad en el bloque del `icons` manifiesto.</span><span class="sxs-lookup"><span data-stu-id="caef6-528">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="caef6-529">`accentColor`: Es el color a utilizar junto con y como fondo para sus iconos de contorno.</span><span class="sxs-lookup"><span data-stu-id="caef6-529">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="caef6-530">`websiteUrl`: Es la URL https:// al sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="caef6-530">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="caef6-531">`privacyUrl`: Es la URL https:// a la política de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="caef6-531">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="caef6-532">`termsOfUseUrl`: Es la URL https:// a los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="caef6-532">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="caef6-533">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="caef6-533">defaultInstallScope</span></span>

<span data-ttu-id="caef6-534">**Opcional** - cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-534">**Optional** - string</span></span>

<span data-ttu-id="caef6-535">Especifica el ámbito de instalación definido para esta aplicación de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="caef6-535">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="caef6-536">El ámbito definido será la opción que se muestra en el botón cuando un usuario intenta agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-536">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="caef6-537">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="caef6-537">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="caef6-538">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="caef6-538">defaultGroupCapability</span></span>

<span data-ttu-id="caef6-539">**Opcional** - objeto</span><span class="sxs-lookup"><span data-stu-id="caef6-539">**Optional** - object</span></span>

<span data-ttu-id="caef6-540">Cuando se selecciona un ámbito de instalación de grupo, definirá la funcionalidad predeterminada cuando el usuario instale la aplicación.</span><span class="sxs-lookup"><span data-stu-id="caef6-540">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="caef6-541">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="caef6-541">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="caef6-542">Nombre</span><span class="sxs-lookup"><span data-stu-id="caef6-542">Name</span></span>| <span data-ttu-id="caef6-543">Tipo</span><span class="sxs-lookup"><span data-stu-id="caef6-543">Type</span></span>| <span data-ttu-id="caef6-544">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="caef6-544">Maximum size</span></span> | <span data-ttu-id="caef6-545">Necesario</span><span class="sxs-lookup"><span data-stu-id="caef6-545">Required</span></span> | <span data-ttu-id="caef6-546">Descripción</span><span class="sxs-lookup"><span data-stu-id="caef6-546">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="caef6-547">string</span><span class="sxs-lookup"><span data-stu-id="caef6-547">string</span></span>|||<span data-ttu-id="caef6-548">Cuando se selecciona el ámbito de `team` instalación, este campo especifica la capacidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="caef6-548">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="caef6-549">Opciones: `tab` , `bot` o `connector` .</span><span class="sxs-lookup"><span data-stu-id="caef6-549">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="caef6-550">cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-550">string</span></span>|||<span data-ttu-id="caef6-551">Cuando se selecciona el ámbito de `groupchat` instalación, este campo especifica la capacidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="caef6-551">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="caef6-552">Opciones: `tab` , `bot` o `connector` .</span><span class="sxs-lookup"><span data-stu-id="caef6-552">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="caef6-553">cadena</span><span class="sxs-lookup"><span data-stu-id="caef6-553">string</span></span>|||<span data-ttu-id="caef6-554">Cuando se selecciona el ámbito de `meetings` instalación, este campo especifica la capacidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="caef6-554">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="caef6-555">Opciones: `tab` , `bot` o `connector` .</span><span class="sxs-lookup"><span data-stu-id="caef6-555">Options: `tab`, `bot`, or `connector`.</span></span>|

