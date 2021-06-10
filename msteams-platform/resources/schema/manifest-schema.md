---
title: Referencia de esquema de manifiesto
description: Describe el esquema de manifiesto para Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: esquema de manifiesto de teams
ms.openlocfilehash: 75c29a1cf9c2897d7b419b45bfc1a4f0447c7aa3
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853532"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="16d0b-104">Referencia: esquema de manifiesto para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="16d0b-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="16d0b-105">El Teams describe cómo se integra la aplicación en el Microsoft Teams producto.</span><span class="sxs-lookup"><span data-stu-id="16d0b-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="16d0b-106">El manifiesto debe cumplir con el esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="16d0b-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="16d0b-107">También se admiten las versiones anteriores 1.0, 1.1,..., 1.6, y así sucesivamente (con "v1.x" en la dirección URL).</span><span class="sxs-lookup"><span data-stu-id="16d0b-107">Previous versions 1.0, 1.1,..., 1.6, and so on are also supported (using "v1.x" in the URL).</span></span>
<span data-ttu-id="16d0b-108">Para obtener más información sobre los cambios realizados en cada versión, vea [registro de cambios de manifiesto](https://github.com/OfficeDev/microsoft-teams-app-schema/releases).</span><span class="sxs-lookup"><span data-stu-id="16d0b-108">For more information on the changes made in each version, see [manifest change log](https://github.com/OfficeDev/microsoft-teams-app-schema/releases).</span></span>

<span data-ttu-id="16d0b-109">En el ejemplo de esquema siguiente se muestran todas las opciones de extensibilidad:</span><span class="sxs-lookup"><span data-stu-id="16d0b-109">The following schema sample shows all extensibility options:</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="16d0b-110">Manifiesto completo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="16d0b-110">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json",
  "manifestVersion": "1.10",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters (<=100 chars)"
  },
  "description": {
    "short": "Short description of your app (<= 80 chars)",
    "full": "Full description of your app (<= 4000 chars)"
  },
  "icons": {
    "outline": "A relative path to a transparent .png icon — 32px X 32px",
    "color": "A relative path to a full color .png icon — 192px X 192px"
  },
  "accentColor": "A valid HTML color code.",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "scopes": [
        "team",
        "groupchat"
      ],
      "canUpdateConfiguration": true,
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
      ],
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": [
         "sharePointFullPage",
         "sharePointWebPart"
      ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "context":[
        "personalTab",
        "channelTab"
        ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser)",
       "searchUrl":  "https://contoso.com/content (displayed in web browser)"
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "scopes": [
        "team",
        "personal",
        "groupchat"
      ],
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "supportsFiles": true,
      "supportsCalling": false,
      "supportsVideo": true,
      "commandLists": [
        {
          "scopes": [
            "team",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command 2",
              "description": "Description of Command 2"
            }
          ]
        },
        {
          "scopes": [
            "personal",
            "groupchat"
          ],
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
      "scopes": [
        "team"
      ],
      "configurationUrl": "https://contoso.com/teamsconnector/configure"
    }
  ],
  "composeExtensions": [
    {
      "canUpdateConfiguration": true,
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "type": "query",
          "context": [
            "compose",
            "commandBox"
          ],
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "fetchTask": false,
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "inputType": "text",
              "description": "Enter the keywords to search for",
              "value": "Initial value for the parameter",
              "choices": [
                {
                  "title": "Title of the choice",
                  "value": "Value of the choice"
                }
              ]
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "type": "action",
          "context": [
            "message"
          ],
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "fetchTask": true,
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType": "text"
            }
          ]
        }
      ],
      "taskInfo": {
        "title": "Initial dialog title",
        "width": "Dialog width",
        "height": "Dialog height",
        "url": "Initial webview URL"
      },
      "messageHandlers": [
        {
          "type": "link",
          "value": {
            "domains": [
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
  "devicePermissions": [
    "geolocation",
    "media",
    "notifications",
    "midi",
    "openExternal"
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
  "showLoadingIndicator": false,
  "isFullScreen": false,
  "activities": {
    "activityTypes": [
      {
        "type": "taskCreated",
        "description": "Task created activity",
        "templateText": "<team member> created task <taskId> for you"
      },
      {
        "type": "userMention",
        "description": "Personal mention activity",
        "templateText": "<team member> mentioned you"
      }
    ]
  },
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
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
  ]              
}
```

<span data-ttu-id="16d0b-111">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="16d0b-111">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="16d0b-112">$schema</span><span class="sxs-lookup"><span data-stu-id="16d0b-112">$schema</span></span>

<span data-ttu-id="16d0b-113">Opcional, pero recomendado: cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-113">Optional, but recommended — string</span></span>

<span data-ttu-id="16d0b-114">La https:// url que hace referencia al esquema JSON para el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="16d0b-114">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="16d0b-115">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="16d0b-115">manifestVersion</span></span>

<span data-ttu-id="16d0b-116">**Obligatorio:** cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-116">**Required** — string</span></span>

<span data-ttu-id="16d0b-117">La versión del esquema de manifiesto que usa este manifiesto.</span><span class="sxs-lookup"><span data-stu-id="16d0b-117">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="16d0b-118">Debe ser 1.10.</span><span class="sxs-lookup"><span data-stu-id="16d0b-118">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="16d0b-119">version</span><span class="sxs-lookup"><span data-stu-id="16d0b-119">version</span></span>

<span data-ttu-id="16d0b-120">**Obligatorio:** cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-120">**Required** — string</span></span>

<span data-ttu-id="16d0b-121">La versión de una aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="16d0b-121">The version of a specific app.</span></span> <span data-ttu-id="16d0b-122">Si actualiza algo en el manifiesto, la versión también debe incrementarse.</span><span class="sxs-lookup"><span data-stu-id="16d0b-122">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="16d0b-123">De este modo, cuando se instala el nuevo manifiesto, se sobrescribe el existente y el usuario recibe la nueva funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="16d0b-123">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="16d0b-124">Si esta aplicación se envió a la tienda, el nuevo manifiesto debe volver a enviarse y volver a validarse.</span><span class="sxs-lookup"><span data-stu-id="16d0b-124">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="16d0b-125">Los usuarios de la aplicación reciben el nuevo manifiesto actualizado automáticamente en pocas horas después de que se apruebe el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="16d0b-125">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="16d0b-126">Si cambian las solicitudes de permisos de la aplicación, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-126">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="16d0b-127">Esta cadena de versión debe seguir el [estándar de semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="16d0b-127">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="16d0b-128">id</span><span class="sxs-lookup"><span data-stu-id="16d0b-128">id</span></span>

<span data-ttu-id="16d0b-129">**Obligatorio:** id. de aplicación de Microsoft</span><span class="sxs-lookup"><span data-stu-id="16d0b-129">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="16d0b-130">El identificador es un identificador único generado por Microsoft para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-130">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="16d0b-131">Tienes un identificador si el bot está registrado a través del Microsoft Bot Framework o la aplicación web de la pestaña ya inicia sesión con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="16d0b-131">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="16d0b-132">Debe escribir el identificador aquí.</span><span class="sxs-lookup"><span data-stu-id="16d0b-132">You must enter the ID here.</span></span> <span data-ttu-id="16d0b-133">De lo contrario, debe generar un nuevo identificador en el Portal de [registro de aplicaciones de Microsoft](https://aka.ms/appregistrations).</span><span class="sxs-lookup"><span data-stu-id="16d0b-133">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="16d0b-134">Use el mismo identificador si agrega un bot.</span><span class="sxs-lookup"><span data-stu-id="16d0b-134">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="16d0b-135">Si vas a enviar una actualización a la aplicación existente en AppSource, no se debe modificar el identificador del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="16d0b-135">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="16d0b-136">developer</span><span class="sxs-lookup"><span data-stu-id="16d0b-136">developer</span></span>

<span data-ttu-id="16d0b-137">**Obligatorio** : objeto</span><span class="sxs-lookup"><span data-stu-id="16d0b-137">**Required** — object</span></span>

<span data-ttu-id="16d0b-138">Especifica información sobre su empresa.</span><span class="sxs-lookup"><span data-stu-id="16d0b-138">Specifies information about your company.</span></span> <span data-ttu-id="16d0b-139">Para las aplicaciones enviadas a la Teams, estos valores deben coincidir con la información de la descripción de la tienda.</span><span class="sxs-lookup"><span data-stu-id="16d0b-139">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="16d0b-140">Para obtener más información, consulte [las Teams de publicación del almacén de almacenamiento.](~/concepts/deploy-and-publish/appsource/publish.md)</span><span class="sxs-lookup"><span data-stu-id="16d0b-140">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="16d0b-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-141">Name</span></span>| <span data-ttu-id="16d0b-142">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-142">Maximum size</span></span> | <span data-ttu-id="16d0b-143">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-143">Required</span></span> | <span data-ttu-id="16d0b-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="16d0b-145">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-145">32 characters</span></span>|<span data-ttu-id="16d0b-146">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-146">✔</span></span>|<span data-ttu-id="16d0b-147">Nombre para mostrar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="16d0b-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="16d0b-148">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-148">2048 characters</span></span>|<span data-ttu-id="16d0b-149">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-149">✔</span></span>|<span data-ttu-id="16d0b-150">La https:// url del sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="16d0b-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="16d0b-151">Este vínculo debe llevar a los usuarios a su empresa o página de aterrizaje específica del producto.</span><span class="sxs-lookup"><span data-stu-id="16d0b-151">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="16d0b-152">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-152">2048 characters</span></span>|<span data-ttu-id="16d0b-153">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-153">✔</span></span>|<span data-ttu-id="16d0b-154">La https:// url a la directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="16d0b-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="16d0b-155">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-155">2048 characters</span></span>|<span data-ttu-id="16d0b-156">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-156">✔</span></span>|<span data-ttu-id="16d0b-157">La https:// url a los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="16d0b-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="16d0b-158">10 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-158">10 characters</span></span>| |<span data-ttu-id="16d0b-159">**Opcional** Id. de red de partners de Microsoft que identifica la organización asociada que está creando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-159">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="16d0b-160">name</span><span class="sxs-lookup"><span data-stu-id="16d0b-160">name</span></span>

<span data-ttu-id="16d0b-161">**Obligatorio** : objeto</span><span class="sxs-lookup"><span data-stu-id="16d0b-161">**Required** — object</span></span>

<span data-ttu-id="16d0b-162">El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="16d0b-162">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="16d0b-163">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="16d0b-163">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="16d0b-164">Los valores de `short` y `full` deben ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="16d0b-164">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="16d0b-165">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-165">Name</span></span>| <span data-ttu-id="16d0b-166">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-166">Maximum size</span></span> | <span data-ttu-id="16d0b-167">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-167">Required</span></span> | <span data-ttu-id="16d0b-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-168">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="16d0b-169">30 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-169">30 characters</span></span>|<span data-ttu-id="16d0b-170">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-170">✔</span></span>|<span data-ttu-id="16d0b-171">El nombre para mostrar corto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-171">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="16d0b-172">100 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-172">100 characters</span></span>||<span data-ttu-id="16d0b-173">El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="16d0b-173">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="16d0b-174">description</span><span class="sxs-lookup"><span data-stu-id="16d0b-174">description</span></span>

<span data-ttu-id="16d0b-175">**Obligatorio** : objeto</span><span class="sxs-lookup"><span data-stu-id="16d0b-175">**Required** — object</span></span>

<span data-ttu-id="16d0b-176">Describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="16d0b-176">Describes your app to users.</span></span> <span data-ttu-id="16d0b-177">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="16d0b-177">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="16d0b-178">Asegúrese de que su descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia.</span><span class="sxs-lookup"><span data-stu-id="16d0b-178">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="16d0b-179">Debe tener en cuenta en la descripción completa, si se requiere una cuenta externa para su uso.</span><span class="sxs-lookup"><span data-stu-id="16d0b-179">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="16d0b-180">Los valores de `short` y `full` deben ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="16d0b-180">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="16d0b-181">La descripción breve no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-181">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="16d0b-182">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-182">Name</span></span>| <span data-ttu-id="16d0b-183">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-183">Maximum size</span></span> | <span data-ttu-id="16d0b-184">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-184">Required</span></span> | <span data-ttu-id="16d0b-185">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-185">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="16d0b-186">80 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-186">80 characters</span></span>|<span data-ttu-id="16d0b-187">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-187">✔</span></span>|<span data-ttu-id="16d0b-188">Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.</span><span class="sxs-lookup"><span data-stu-id="16d0b-188">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="16d0b-189">4000 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-189">4000 characters</span></span>|<span data-ttu-id="16d0b-190">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-190">✔</span></span>|<span data-ttu-id="16d0b-191">Descripción completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-191">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="16d0b-192">packageName</span><span class="sxs-lookup"><span data-stu-id="16d0b-192">packageName</span></span>

<span data-ttu-id="16d0b-193">**Opcional:** cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-193">**Optional** — string</span></span>

<span data-ttu-id="16d0b-194">Un identificador único para la aplicación en la notación de dominio inverso; por ejemplo, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="16d0b-194">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="16d0b-195">Longitud máxima: 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="16d0b-195">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="16d0b-196">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="16d0b-196">localizationInfo</span></span>

<span data-ttu-id="16d0b-197">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="16d0b-197">**Optional** — object</span></span>

<span data-ttu-id="16d0b-198">Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="16d0b-198">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="16d0b-199">Para obtener más información, vea [localización](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="16d0b-199">For more information, see [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="16d0b-200">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-200">Name</span></span>| <span data-ttu-id="16d0b-201">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-201">Maximum size</span></span> | <span data-ttu-id="16d0b-202">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-202">Required</span></span> | <span data-ttu-id="16d0b-203">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-203">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="16d0b-204">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-204">✔</span></span>|<span data-ttu-id="16d0b-205">La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="16d0b-205">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="16d0b-206">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="16d0b-206">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="16d0b-207">Una matriz de objetos que especifica traducciones de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="16d0b-207">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="16d0b-208">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-208">Name</span></span>| <span data-ttu-id="16d0b-209">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-209">Maximum size</span></span> | <span data-ttu-id="16d0b-210">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-210">Required</span></span> | <span data-ttu-id="16d0b-211">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-211">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="16d0b-212">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-212">✔</span></span>|<span data-ttu-id="16d0b-213">Etiqueta de idioma de las cadenas del archivo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="16d0b-213">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="16d0b-214">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-214">✔</span></span>|<span data-ttu-id="16d0b-215">Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="16d0b-215">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="16d0b-216">iconos</span><span class="sxs-lookup"><span data-stu-id="16d0b-216">icons</span></span>

<span data-ttu-id="16d0b-217">**Obligatorio** : objeto</span><span class="sxs-lookup"><span data-stu-id="16d0b-217">**Required** — object</span></span>

<span data-ttu-id="16d0b-218">Iconos usados dentro de la Teams aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-218">Icons used within the Teams app.</span></span> <span data-ttu-id="16d0b-219">Los archivos de icono deben incluirse como parte del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="16d0b-219">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="16d0b-220">Consulta [Iconos](../../concepts/build-and-test/apps-package.md#app-icons) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="16d0b-220">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="16d0b-221">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-221">Name</span></span>| <span data-ttu-id="16d0b-222">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-222">Maximum size</span></span> | <span data-ttu-id="16d0b-223">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-223">Required</span></span> | <span data-ttu-id="16d0b-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-224">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="16d0b-225">32 x 32 píxeles</span><span class="sxs-lookup"><span data-stu-id="16d0b-225">32 x 32 pixels</span></span>|<span data-ttu-id="16d0b-226">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-226">✔</span></span>|<span data-ttu-id="16d0b-227">Una ruta de acceso de archivo relativa a un icono de esquema PNG transparente de 32 x 32.</span><span class="sxs-lookup"><span data-stu-id="16d0b-227">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="16d0b-228">192 x 192 píxeles</span><span class="sxs-lookup"><span data-stu-id="16d0b-228">192 x 192 pixels</span></span>|<span data-ttu-id="16d0b-229">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-229">✔</span></span>|<span data-ttu-id="16d0b-230">Una ruta de acceso de archivo relativa a un icono PNG de color completo de 192 x 192.</span><span class="sxs-lookup"><span data-stu-id="16d0b-230">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="16d0b-231">accentColor</span><span class="sxs-lookup"><span data-stu-id="16d0b-231">accentColor</span></span>

<span data-ttu-id="16d0b-232">**Opcional:** código de color Hexadecimal HTML</span><span class="sxs-lookup"><span data-stu-id="16d0b-232">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="16d0b-233">Color que se usará junto con y como fondo para los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="16d0b-233">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="16d0b-234">El valor debe ser un código de color HTML válido a partir de '#', por ejemplo `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-234">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="16d0b-235">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="16d0b-235">configurableTabs</span></span>

<span data-ttu-id="16d0b-236">**Opcional:** matriz</span><span class="sxs-lookup"><span data-stu-id="16d0b-236">**Optional** — array</span></span>

<span data-ttu-id="16d0b-237">Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de grupo que requiere una configuración adicional antes de agregarla.</span><span class="sxs-lookup"><span data-stu-id="16d0b-237">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="16d0b-238">Las pestañas configurables solo se admiten en el ámbito de teams y puede configurar las mismas pestañas varias veces.</span><span class="sxs-lookup"><span data-stu-id="16d0b-238">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="16d0b-239">Sin embargo, solo puede definirlo en el manifiesto una vez.</span><span class="sxs-lookup"><span data-stu-id="16d0b-239">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="16d0b-240">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-240">Name</span></span>| <span data-ttu-id="16d0b-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-241">Type</span></span>| <span data-ttu-id="16d0b-242">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-242">Maximum size</span></span> | <span data-ttu-id="16d0b-243">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-243">Required</span></span> | <span data-ttu-id="16d0b-244">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="16d0b-245">string</span><span class="sxs-lookup"><span data-stu-id="16d0b-245">string</span></span>|<span data-ttu-id="16d0b-246">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-246">2048 characters</span></span>|<span data-ttu-id="16d0b-247">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-247">✔</span></span>|<span data-ttu-id="16d0b-248">La https:// url que se va a usar al configurar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="16d0b-248">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="16d0b-249">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="16d0b-249">array of enums</span></span>|<span data-ttu-id="16d0b-250">1</span><span class="sxs-lookup"><span data-stu-id="16d0b-250">1</span></span>|<span data-ttu-id="16d0b-251">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-251">✔</span></span>|<span data-ttu-id="16d0b-252">Actualmente, las pestañas configurables solo admiten `team` los `groupchat` ámbitos y.</span><span class="sxs-lookup"><span data-stu-id="16d0b-252">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="16d0b-253">boolean</span><span class="sxs-lookup"><span data-stu-id="16d0b-253">boolean</span></span>|||<span data-ttu-id="16d0b-254">Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de su creación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-254">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="16d0b-255">Valor predeterminado: **true**.</span><span class="sxs-lookup"><span data-stu-id="16d0b-255">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="16d0b-256">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="16d0b-256">array of enums</span></span>|<span data-ttu-id="16d0b-257">6 </span><span class="sxs-lookup"><span data-stu-id="16d0b-257">6</span></span>||<span data-ttu-id="16d0b-258">Conjunto de `contextItem` ámbitos donde se admite [una pestaña](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="16d0b-258">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="16d0b-259">Valor predeterminado: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="16d0b-259">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="16d0b-260">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-260">string</span></span>|<span data-ttu-id="16d0b-261">2048</span><span class="sxs-lookup"><span data-stu-id="16d0b-261">2048</span></span>||<span data-ttu-id="16d0b-262">Una ruta de acceso de archivo relativa a una imagen de vista previa de tabulación para su uso en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="16d0b-262">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="16d0b-263">Tamaño 1024x768.</span><span class="sxs-lookup"><span data-stu-id="16d0b-263">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="16d0b-264">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="16d0b-264">array of enums</span></span>|<span data-ttu-id="16d0b-265">1</span><span class="sxs-lookup"><span data-stu-id="16d0b-265">1</span></span>||<span data-ttu-id="16d0b-266">Define cómo la pestaña está disponible en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="16d0b-266">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="16d0b-267">Las opciones son `sharePointFullPage` y `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="16d0b-267">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="16d0b-268">staticTabs</span><span class="sxs-lookup"><span data-stu-id="16d0b-268">staticTabs</span></span>

<span data-ttu-id="16d0b-269">**Opcional:** matriz</span><span class="sxs-lookup"><span data-stu-id="16d0b-269">**Optional** — array</span></span>

<span data-ttu-id="16d0b-270">Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente.</span><span class="sxs-lookup"><span data-stu-id="16d0b-270">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="16d0b-271">Las pestañas estáticas declaradas en el ámbito siempre se anclan a la experiencia `personal` personal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-271">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="16d0b-272">Actualmente no se admiten las pestañas estáticas declaradas `team` en el ámbito.</span><span class="sxs-lookup"><span data-stu-id="16d0b-272">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="16d0b-273">Este elemento es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-273">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="16d0b-274">Este bloque solo es necesario para las soluciones que proporcionan una solución de tabulación estática.</span><span class="sxs-lookup"><span data-stu-id="16d0b-274">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="16d0b-275">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-275">Name</span></span>| <span data-ttu-id="16d0b-276">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-276">Type</span></span>| <span data-ttu-id="16d0b-277">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-277">Maximum size</span></span> | <span data-ttu-id="16d0b-278">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-278">Required</span></span> | <span data-ttu-id="16d0b-279">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-279">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="16d0b-280">string</span><span class="sxs-lookup"><span data-stu-id="16d0b-280">string</span></span>|<span data-ttu-id="16d0b-281">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-281">64 characters</span></span>|<span data-ttu-id="16d0b-282">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-282">✔</span></span>|<span data-ttu-id="16d0b-283">Identificador único para la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="16d0b-283">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="16d0b-284">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-284">string</span></span>|<span data-ttu-id="16d0b-285">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-285">128 characters</span></span>|<span data-ttu-id="16d0b-286">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-286">✔</span></span>|<span data-ttu-id="16d0b-287">Nombre para mostrar de la pestaña en la interfaz de canal.</span><span class="sxs-lookup"><span data-stu-id="16d0b-287">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="16d0b-288">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-288">string</span></span>||<span data-ttu-id="16d0b-289">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-289">✔</span></span>|<span data-ttu-id="16d0b-290">Dirección URL https:// que apunta a la interfaz de usuario de la entidad que se va a mostrar en el Teams usuario.</span><span class="sxs-lookup"><span data-stu-id="16d0b-290">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="16d0b-291">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-291">string</span></span>|||<span data-ttu-id="16d0b-292">La https:// dirección URL que se debe apuntar si un usuario opta por ver en un explorador.</span><span class="sxs-lookup"><span data-stu-id="16d0b-292">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="16d0b-293">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-293">string</span></span>|||<span data-ttu-id="16d0b-294">La https:// dirección URL que se va a apuntar a las consultas de búsqueda de un usuario.</span><span class="sxs-lookup"><span data-stu-id="16d0b-294">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="16d0b-295">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="16d0b-295">array of enums</span></span>|<span data-ttu-id="16d0b-296">1</span><span class="sxs-lookup"><span data-stu-id="16d0b-296">1</span></span>|<span data-ttu-id="16d0b-297">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-297">✔</span></span>|<span data-ttu-id="16d0b-298">Actualmente, las pestañas estáticas solo admiten el ámbito, lo que significa que solo se puede aprovisionar como `personal` parte de la experiencia personal.</span><span class="sxs-lookup"><span data-stu-id="16d0b-298">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="16d0b-299">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="16d0b-299">array of enums</span></span>| <span data-ttu-id="16d0b-300">2</span><span class="sxs-lookup"><span data-stu-id="16d0b-300">2</span></span>|| <span data-ttu-id="16d0b-301">Conjunto de `contextItem` ámbitos donde se admite una pestaña.</span><span class="sxs-lookup"><span data-stu-id="16d0b-301">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="16d0b-302">La característica searchUrl no está disponible para los desarrolladores de terceros.</span><span class="sxs-lookup"><span data-stu-id="16d0b-302">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="16d0b-303">Si las pestañas requieren información dependiente del contexto para mostrar contenido relevante o para iniciar un flujo de autenticación, para obtener más información, vea [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="16d0b-303">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="16d0b-304">bots</span><span class="sxs-lookup"><span data-stu-id="16d0b-304">bots</span></span>

<span data-ttu-id="16d0b-305">**Opcional:** matriz</span><span class="sxs-lookup"><span data-stu-id="16d0b-305">**Optional** — array</span></span>

<span data-ttu-id="16d0b-306">Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="16d0b-306">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="16d0b-307">El elemento es una matriz (máximo de solo 1 elemento actualmente solo se permite un bot por aplicación) con todos los &mdash; elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-307">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="16d0b-308">Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.</span><span class="sxs-lookup"><span data-stu-id="16d0b-308">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="16d0b-309">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-309">Name</span></span>| <span data-ttu-id="16d0b-310">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-310">Type</span></span>| <span data-ttu-id="16d0b-311">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-311">Maximum size</span></span> | <span data-ttu-id="16d0b-312">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-312">Required</span></span> | <span data-ttu-id="16d0b-313">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-313">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="16d0b-314">string</span><span class="sxs-lookup"><span data-stu-id="16d0b-314">string</span></span>|<span data-ttu-id="16d0b-315">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-315">64 characters</span></span>|<span data-ttu-id="16d0b-316">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-316">✔</span></span>|<span data-ttu-id="16d0b-317">El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="16d0b-317">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="16d0b-318">Esto bien puede ser el mismo que el identificador general [de la aplicación](#id).</span><span class="sxs-lookup"><span data-stu-id="16d0b-318">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="16d0b-319">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="16d0b-319">array of enums</span></span>|<span data-ttu-id="16d0b-320">3</span><span class="sxs-lookup"><span data-stu-id="16d0b-320">3</span></span>|<span data-ttu-id="16d0b-321">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-321">✔</span></span>|<span data-ttu-id="16d0b-322">Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`).</span><span class="sxs-lookup"><span data-stu-id="16d0b-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="16d0b-323">Estas opciones no son exclusivas.</span><span class="sxs-lookup"><span data-stu-id="16d0b-323">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="16d0b-324">boolean</span><span class="sxs-lookup"><span data-stu-id="16d0b-324">boolean</span></span>|||<span data-ttu-id="16d0b-325">Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico.</span><span class="sxs-lookup"><span data-stu-id="16d0b-325">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="16d0b-326">Valor predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="16d0b-326">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="16d0b-327">boolean</span><span class="sxs-lookup"><span data-stu-id="16d0b-327">boolean</span></span>|||<span data-ttu-id="16d0b-328">Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-328">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="16d0b-329">Valor predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="16d0b-329">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="16d0b-330">boolean</span><span class="sxs-lookup"><span data-stu-id="16d0b-330">boolean</span></span>|||<span data-ttu-id="16d0b-331">Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal.</span><span class="sxs-lookup"><span data-stu-id="16d0b-331">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="16d0b-332">Valor predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="16d0b-332">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="16d0b-333">boolean</span><span class="sxs-lookup"><span data-stu-id="16d0b-333">boolean</span></span>|||<span data-ttu-id="16d0b-334">Valor que indica dónde un bot admite llamadas de audio.</span><span class="sxs-lookup"><span data-stu-id="16d0b-334">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="16d0b-335">**IMPORTANTE:** Esta propiedad es actualmente experimental.</span><span class="sxs-lookup"><span data-stu-id="16d0b-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="16d0b-336">Es posible que las propiedades experimentales no estén completas y que se someten a cambios antes de estar totalmente disponibles.</span><span class="sxs-lookup"><span data-stu-id="16d0b-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="16d0b-337">Se proporciona solo con fines de prueba y exploración y no debe usarse en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="16d0b-337">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="16d0b-338">Valor predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="16d0b-338">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="16d0b-339">boolean</span><span class="sxs-lookup"><span data-stu-id="16d0b-339">boolean</span></span>|||<span data-ttu-id="16d0b-340">Valor que indica dónde un bot admite videollamadas.</span><span class="sxs-lookup"><span data-stu-id="16d0b-340">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="16d0b-341">**IMPORTANTE:** Esta propiedad es actualmente experimental.</span><span class="sxs-lookup"><span data-stu-id="16d0b-341">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="16d0b-342">Es posible que las propiedades experimentales no estén completas y que se someten a cambios antes de estar totalmente disponibles.</span><span class="sxs-lookup"><span data-stu-id="16d0b-342">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="16d0b-343">Se proporciona solo con fines de prueba y exploración y no debe usarse en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="16d0b-343">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="16d0b-344">Valor predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="16d0b-344">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="16d0b-345">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="16d0b-345">bots.commandLists</span></span>

<span data-ttu-id="16d0b-346">Una lista opcional de comandos que el bot puede recomendar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="16d0b-346">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="16d0b-347">El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de comandos independiente para cada ámbito compatible `object` con el bot.</span><span class="sxs-lookup"><span data-stu-id="16d0b-347">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="16d0b-348">Consulta [Menús bot para](~/bots/how-to/create-a-bot-commands-menu.md) obtener más información.</span><span class="sxs-lookup"><span data-stu-id="16d0b-348">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="16d0b-349">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-349">Name</span></span>| <span data-ttu-id="16d0b-350">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-350">Type</span></span>| <span data-ttu-id="16d0b-351">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-351">Maximum size</span></span> | <span data-ttu-id="16d0b-352">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-352">Required</span></span> | <span data-ttu-id="16d0b-353">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-353">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="16d0b-354">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="16d0b-354">array of enums</span></span>|<span data-ttu-id="16d0b-355">3</span><span class="sxs-lookup"><span data-stu-id="16d0b-355">3</span></span>|<span data-ttu-id="16d0b-356">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-356">✔</span></span>|<span data-ttu-id="16d0b-357">Especifica el ámbito para el que la lista de comandos es válida.</span><span class="sxs-lookup"><span data-stu-id="16d0b-357">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="16d0b-358">Las opciones son `team`, `personal` y `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="16d0b-358">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="16d0b-359">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="16d0b-359">array of objects</span></span>|<span data-ttu-id="16d0b-360">10</span><span class="sxs-lookup"><span data-stu-id="16d0b-360">10</span></span>|<span data-ttu-id="16d0b-361">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-361">✔</span></span>|<span data-ttu-id="16d0b-362">Una matriz de comandos que el bot admite:</span><span class="sxs-lookup"><span data-stu-id="16d0b-362">An array of commands the bot supports:</span></span><br><span data-ttu-id="16d0b-363">`title`: el nombre de comando del bot (cadena, 32)</span><span class="sxs-lookup"><span data-stu-id="16d0b-363">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="16d0b-364">`description`: una descripción sencilla o un ejemplo de la sintaxis del comando y su argumento (cadena, 128).</span><span class="sxs-lookup"><span data-stu-id="16d0b-364">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="16d0b-365">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="16d0b-365">bots.commandLists.commands</span></span>

|<span data-ttu-id="16d0b-366">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-366">Name</span></span>| <span data-ttu-id="16d0b-367">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-367">Type</span></span>| <span data-ttu-id="16d0b-368">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-368">Maximum size</span></span> | <span data-ttu-id="16d0b-369">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-369">Required</span></span> | <span data-ttu-id="16d0b-370">Description</span><span class="sxs-lookup"><span data-stu-id="16d0b-370">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="16d0b-371">title</span><span class="sxs-lookup"><span data-stu-id="16d0b-371">title</span></span>|<span data-ttu-id="16d0b-372">string</span><span class="sxs-lookup"><span data-stu-id="16d0b-372">string</span></span>|<span data-ttu-id="16d0b-373">12 </span><span class="sxs-lookup"><span data-stu-id="16d0b-373">12</span></span>|<span data-ttu-id="16d0b-374">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-374">✔</span></span>|<span data-ttu-id="16d0b-375">Nombre del comando bot.</span><span class="sxs-lookup"><span data-stu-id="16d0b-375">The bot command name.</span></span>|
|<span data-ttu-id="16d0b-376">description</span><span class="sxs-lookup"><span data-stu-id="16d0b-376">description</span></span>|<span data-ttu-id="16d0b-377">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-377">string</span></span>|<span data-ttu-id="16d0b-378">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-378">128 characters</span></span>|<span data-ttu-id="16d0b-379">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-379">✔</span></span>|<span data-ttu-id="16d0b-380">Una descripción de texto simple o un ejemplo de la sintaxis del comando y sus argumentos.</span><span class="sxs-lookup"><span data-stu-id="16d0b-380">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="16d0b-381">conectores</span><span class="sxs-lookup"><span data-stu-id="16d0b-381">connectors</span></span>

<span data-ttu-id="16d0b-382">**Opcional:** matriz</span><span class="sxs-lookup"><span data-stu-id="16d0b-382">**Optional** — array</span></span>

<span data-ttu-id="16d0b-383">El `connectors` bloque define un Office 365 connector para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-383">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="16d0b-384">El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-384">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="16d0b-385">Este bloque solo es necesario para las soluciones que proporcionan un conector.</span><span class="sxs-lookup"><span data-stu-id="16d0b-385">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="16d0b-386">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-386">Name</span></span>| <span data-ttu-id="16d0b-387">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-387">Type</span></span>| <span data-ttu-id="16d0b-388">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-388">Maximum size</span></span> | <span data-ttu-id="16d0b-389">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-389">Required</span></span> | <span data-ttu-id="16d0b-390">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-390">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="16d0b-391">string</span><span class="sxs-lookup"><span data-stu-id="16d0b-391">string</span></span>|<span data-ttu-id="16d0b-392">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-392">2048 characters</span></span>|<span data-ttu-id="16d0b-393">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-393">✔</span></span>|<span data-ttu-id="16d0b-394">La https:// url que se va a usar al configurar el conector.</span><span class="sxs-lookup"><span data-stu-id="16d0b-394">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="16d0b-395">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="16d0b-395">array of enums</span></span>|<span data-ttu-id="16d0b-396">1</span><span class="sxs-lookup"><span data-stu-id="16d0b-396">1</span></span>|<span data-ttu-id="16d0b-397">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-397">✔</span></span>|<span data-ttu-id="16d0b-398">Especifica si connector ofrece una experiencia en el contexto de un canal en un , o una experiencia ámbito a un `team` usuario individual solo ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="16d0b-398">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="16d0b-399">Actualmente, solo se `team` admite el ámbito.</span><span class="sxs-lookup"><span data-stu-id="16d0b-399">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="16d0b-400">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-400">string</span></span>|<span data-ttu-id="16d0b-401">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-401">64 characters</span></span>|<span data-ttu-id="16d0b-402">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-402">✔</span></span>|<span data-ttu-id="16d0b-403">Identificador único del conector que coincide con su identificador en el [Panel de desarrolladores de conectores.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="16d0b-403">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="16d0b-404">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="16d0b-404">composeExtensions</span></span>

<span data-ttu-id="16d0b-405">**Opcional:** matriz</span><span class="sxs-lookup"><span data-stu-id="16d0b-405">**Optional** — array</span></span>

<span data-ttu-id="16d0b-406">Define una extensión de mensajería para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-406">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="16d0b-407">El nombre de la característica se cambió de "extensión de redacción" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="16d0b-407">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="16d0b-408">El elemento es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-408">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="16d0b-409">Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="16d0b-409">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="16d0b-410">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-410">Name</span></span>| <span data-ttu-id="16d0b-411">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-411">Type</span></span> | <span data-ttu-id="16d0b-412">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-412">Maximum Size</span></span> | <span data-ttu-id="16d0b-413">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="16d0b-413">Required</span></span> | <span data-ttu-id="16d0b-414">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-414">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="16d0b-415">string</span><span class="sxs-lookup"><span data-stu-id="16d0b-415">string</span></span>|<span data-ttu-id="16d0b-416">64</span><span class="sxs-lookup"><span data-stu-id="16d0b-416">64</span></span>|<span data-ttu-id="16d0b-417">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-417">✔</span></span>|<span data-ttu-id="16d0b-418">El identificador único de la aplicación de Microsoft para el bot que hace una copia de seguridad de la extensión de mensajería, tal como se registró con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="16d0b-418">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="16d0b-419">Esto bien puede ser el mismo que el identificador general de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-419">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="16d0b-420">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="16d0b-420">array of objects</span></span>|<span data-ttu-id="16d0b-421">10</span><span class="sxs-lookup"><span data-stu-id="16d0b-421">10</span></span>|<span data-ttu-id="16d0b-422">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-422">✔</span></span>|<span data-ttu-id="16d0b-423">Matriz de comandos que admite la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="16d0b-423">Array of commands the messaging extension supports.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="16d0b-424">boolean</span><span class="sxs-lookup"><span data-stu-id="16d0b-424">boolean</span></span>|||<span data-ttu-id="16d0b-425">Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="16d0b-425">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="16d0b-426">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="16d0b-426">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="16d0b-427">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="16d0b-427">array of Objects</span></span>|<span data-ttu-id="16d0b-428">5 </span><span class="sxs-lookup"><span data-stu-id="16d0b-428">5</span></span>||<span data-ttu-id="16d0b-429">Una lista de controladores que permiten invocar aplicaciones cuando se cumplen determinadas condiciones.</span><span class="sxs-lookup"><span data-stu-id="16d0b-429">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="16d0b-430">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-430">string</span></span>|||<span data-ttu-id="16d0b-431">El tipo de controlador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="16d0b-431">The type of message handler.</span></span> <span data-ttu-id="16d0b-432">Debe ser `"link"`.</span><span class="sxs-lookup"><span data-stu-id="16d0b-432">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="16d0b-433">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="16d0b-433">array of Strings</span></span>|||<span data-ttu-id="16d0b-434">Matriz de dominios para los que se puede registrar el controlador de mensajes de vínculo.</span><span class="sxs-lookup"><span data-stu-id="16d0b-434">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="16d0b-435">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="16d0b-435">composeExtensions.commands</span></span>

<span data-ttu-id="16d0b-436">La extensión de mensajería debe declarar uno o varios comandos.</span><span class="sxs-lookup"><span data-stu-id="16d0b-436">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="16d0b-437">Cada comando aparece en Microsoft Teams como una interacción potencial desde el punto de entrada basado en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="16d0b-437">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="16d0b-438">Hay un máximo de 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="16d0b-438">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="16d0b-439">Cada elemento de comando es un objeto con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="16d0b-439">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="16d0b-440">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-440">Name</span></span>| <span data-ttu-id="16d0b-441">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-441">Type</span></span>| <span data-ttu-id="16d0b-442">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-442">Maximum size</span></span> | <span data-ttu-id="16d0b-443">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-443">Required</span></span> | <span data-ttu-id="16d0b-444">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-444">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="16d0b-445">string</span><span class="sxs-lookup"><span data-stu-id="16d0b-445">string</span></span>|<span data-ttu-id="16d0b-446">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-446">64 characters</span></span>|<span data-ttu-id="16d0b-447">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-447">✔</span></span>|<span data-ttu-id="16d0b-448">El identificador del comando.</span><span class="sxs-lookup"><span data-stu-id="16d0b-448">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="16d0b-449">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-449">string</span></span>|<span data-ttu-id="16d0b-450">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-450">32 characters</span></span>|<span data-ttu-id="16d0b-451">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-451">✔</span></span>|<span data-ttu-id="16d0b-452">Nombre de comando fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="16d0b-452">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="16d0b-453">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-453">string</span></span>|<span data-ttu-id="16d0b-454">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-454">64 characters</span></span>||<span data-ttu-id="16d0b-455">Tipo del comando.</span><span class="sxs-lookup"><span data-stu-id="16d0b-455">Type of the command.</span></span> <span data-ttu-id="16d0b-456">Uno de `query` o `action` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-456">One of `query` or `action`.</span></span> <span data-ttu-id="16d0b-457">Valor predeterminado: **consulta**.</span><span class="sxs-lookup"><span data-stu-id="16d0b-457">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="16d0b-458">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-458">string</span></span>|<span data-ttu-id="16d0b-459">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-459">128 characters</span></span>||<span data-ttu-id="16d0b-460">La descripción que se muestra a los usuarios para indicar el propósito de este comando.</span><span class="sxs-lookup"><span data-stu-id="16d0b-460">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="16d0b-461">boolean</span><span class="sxs-lookup"><span data-stu-id="16d0b-461">boolean</span></span>|||<span data-ttu-id="16d0b-462">Un valor booleano indica si el comando se ejecuta inicialmente sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="16d0b-462">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="16d0b-463">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="16d0b-463">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="16d0b-464">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="16d0b-464">array of Strings</span></span>|<span data-ttu-id="16d0b-465">3</span><span class="sxs-lookup"><span data-stu-id="16d0b-465">3</span></span>||<span data-ttu-id="16d0b-466">Define desde dónde se puede invocar la extensión de mensaje.</span><span class="sxs-lookup"><span data-stu-id="16d0b-466">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="16d0b-467">Cualquier combinación de `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-467">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="16d0b-468">El valor predeterminado es `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="16d0b-468">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="16d0b-469">boolean</span><span class="sxs-lookup"><span data-stu-id="16d0b-469">boolean</span></span>|||<span data-ttu-id="16d0b-470">Valor booleano que indica si debe capturar el módulo de tareas dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="16d0b-470">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="16d0b-471">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="16d0b-471">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="16d0b-472">object</span><span class="sxs-lookup"><span data-stu-id="16d0b-472">object</span></span>|||<span data-ttu-id="16d0b-473">Especifique el módulo de tareas que se debe cargar previamente al usar un comando de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="16d0b-473">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="16d0b-474">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-474">string</span></span>|<span data-ttu-id="16d0b-475">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-475">64 characters</span></span>||<span data-ttu-id="16d0b-476">Título del cuadro de diálogo inicial.</span><span class="sxs-lookup"><span data-stu-id="16d0b-476">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="16d0b-477">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-477">string</span></span>|||<span data-ttu-id="16d0b-478">Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="16d0b-478">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="16d0b-479">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-479">string</span></span>|||<span data-ttu-id="16d0b-480">Alto del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="16d0b-480">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="16d0b-481">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-481">string</span></span>|||<span data-ttu-id="16d0b-482">Dirección URL de vista web inicial.</span><span class="sxs-lookup"><span data-stu-id="16d0b-482">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="16d0b-483">matriz de objeto</span><span class="sxs-lookup"><span data-stu-id="16d0b-483">array of object</span></span>|<span data-ttu-id="16d0b-484">5 elementos</span><span class="sxs-lookup"><span data-stu-id="16d0b-484">5 items</span></span>|<span data-ttu-id="16d0b-485">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-485">✔</span></span>|<span data-ttu-id="16d0b-486">La lista de parámetros que toma el comando.</span><span class="sxs-lookup"><span data-stu-id="16d0b-486">The list of parameters the command takes.</span></span> <span data-ttu-id="16d0b-487">Mínimo: 1; máximo: 5.</span><span class="sxs-lookup"><span data-stu-id="16d0b-487">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="16d0b-488">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-488">string</span></span>|<span data-ttu-id="16d0b-489">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-489">64 characters</span></span>|<span data-ttu-id="16d0b-490">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-490">✔</span></span>|<span data-ttu-id="16d0b-491">Nombre del parámetro tal como aparece en el cliente.</span><span class="sxs-lookup"><span data-stu-id="16d0b-491">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="16d0b-492">Esto se incluye en la solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="16d0b-492">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="16d0b-493">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-493">string</span></span>|<span data-ttu-id="16d0b-494">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-494">32 characters</span></span>|<span data-ttu-id="16d0b-495">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-495">✔</span></span>|<span data-ttu-id="16d0b-496">Título fácil de usar para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="16d0b-496">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="16d0b-497">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-497">string</span></span>|<span data-ttu-id="16d0b-498">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-498">128 characters</span></span>||<span data-ttu-id="16d0b-499">Cadena fácil de usar que describe el propósito de este parámetro.</span><span class="sxs-lookup"><span data-stu-id="16d0b-499">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="16d0b-500">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-500">string</span></span>|<span data-ttu-id="16d0b-501">512 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-501">512 characters</span></span>||<span data-ttu-id="16d0b-502">Valor inicial del parámetro.</span><span class="sxs-lookup"><span data-stu-id="16d0b-502">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="16d0b-503">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-503">string</span></span>|<span data-ttu-id="16d0b-504">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-504">128 characters</span></span>||<span data-ttu-id="16d0b-505">Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-505">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="16d0b-506">Uno de `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-506">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="16d0b-507">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="16d0b-507">array of objects</span></span>|<span data-ttu-id="16d0b-508">10 elementos</span><span class="sxs-lookup"><span data-stu-id="16d0b-508">10 items</span></span>||<span data-ttu-id="16d0b-509">Las opciones de elección para `choiceset` el archivo .</span><span class="sxs-lookup"><span data-stu-id="16d0b-509">The choice options for the`choiceset`.</span></span> <span data-ttu-id="16d0b-510">Use solo cuando `parameter.inputType` es `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-510">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="16d0b-511">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-511">string</span></span>|<span data-ttu-id="16d0b-512">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-512">128 characters</span></span>|<span data-ttu-id="16d0b-513">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-513">✔</span></span>|<span data-ttu-id="16d0b-514">Título de la elección.</span><span class="sxs-lookup"><span data-stu-id="16d0b-514">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="16d0b-515">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-515">string</span></span>|<span data-ttu-id="16d0b-516">512 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-516">512 characters</span></span>|<span data-ttu-id="16d0b-517">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-517">✔</span></span>|<span data-ttu-id="16d0b-518">Valor de la elección.</span><span class="sxs-lookup"><span data-stu-id="16d0b-518">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="16d0b-519">permisos</span><span class="sxs-lookup"><span data-stu-id="16d0b-519">permissions</span></span>

<span data-ttu-id="16d0b-520">**Opcional:** matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="16d0b-520">**Optional** — array of strings</span></span>

<span data-ttu-id="16d0b-521">Una matriz de los cuales especifica qué permisos solicita la aplicación, lo que permite a los usuarios `string` finales saber cómo funciona la extensión.</span><span class="sxs-lookup"><span data-stu-id="16d0b-521">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="16d0b-522">Las siguientes opciones no son exclusivas:</span><span class="sxs-lookup"><span data-stu-id="16d0b-522">The following options are non-exclusive:</span></span>

* <span data-ttu-id="16d0b-523">`identity`&emsp;Requiere información de identidad de usuario.</span><span class="sxs-lookup"><span data-stu-id="16d0b-523">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="16d0b-524">`messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="16d0b-524">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="16d0b-525">Al cambiar estos permisos durante la actualización de la aplicación, los usuarios repiten el proceso de consentimiento después de ejecutar la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="16d0b-525">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="16d0b-526">Consulta [Actualizar la aplicación para](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) obtener más información.</span><span class="sxs-lookup"><span data-stu-id="16d0b-526">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="16d0b-527">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="16d0b-527">devicePermissions</span></span>

<span data-ttu-id="16d0b-528">**Opcional:** matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="16d0b-528">**Optional** — array of strings</span></span>

<span data-ttu-id="16d0b-529">Proporciona las características nativas en el dispositivo de un usuario al que la aplicación solicita acceso.</span><span class="sxs-lookup"><span data-stu-id="16d0b-529">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="16d0b-530">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="16d0b-530">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="16d0b-531">validDomains</span><span class="sxs-lookup"><span data-stu-id="16d0b-531">validDomains</span></span>

<span data-ttu-id="16d0b-532">**Opcional**, excepto **Requerido cuando** se indica.</span><span class="sxs-lookup"><span data-stu-id="16d0b-532">**Optional**, except **Required** where noted.</span></span>

<span data-ttu-id="16d0b-533">Una lista de dominios válidos para sitios web que la aplicación espera cargar en el Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="16d0b-533">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="16d0b-534">Las listas de dominios pueden incluir caracteres comodín, por ejemplo, `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-534">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="16d0b-535">Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-535">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="16d0b-536">Si la interfaz de usuario de contenido o configuración de pestañas necesita navegar a cualquier otro dominio además del uso para la configuración de pestañas, este dominio debe especificarse aquí.</span><span class="sxs-lookup"><span data-stu-id="16d0b-536">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="16d0b-537">No es **necesario** incluir los dominios de los proveedores de identidades que quieres admitir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-537">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="16d0b-538">Por ejemplo, para autenticar con un identificador de Google, es necesario redirigir a accounts.google.com, sin embargo, no debe incluir accounts.google.com en `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-538">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="16d0b-539">Teams aplicaciones que requieren que sus propias direcciones URL de sharepoint funcionen correctamente, incluye "{teamsitedomain}" en su lista de dominios válida.</span><span class="sxs-lookup"><span data-stu-id="16d0b-539">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16d0b-540">No agregue dominios que estén fuera del control, ya sea directamente o a través de caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="16d0b-540">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="16d0b-541">Por ejemplo, `yourapp.onmicrosoft.com` es válido, sin embargo, `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="16d0b-541">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="16d0b-542">El objeto es una matriz con todos los elementos del tipo `string` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-542">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="16d0b-543">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="16d0b-543">webApplicationInfo</span></span>

<span data-ttu-id="16d0b-544">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="16d0b-544">**Optional** — object</span></span>

<span data-ttu-id="16d0b-545">Proporcione su Azure Active Directory de aplicación (AAD) y microsoft Graph información para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-545">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="16d0b-546">Si la aplicación está registrada en AAD, debes proporcionar el identificador de la aplicación, para que los administradores puedan revisar fácilmente los permisos y conceder el consentimiento en Teams centro de administración.</span><span class="sxs-lookup"><span data-stu-id="16d0b-546">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="16d0b-547">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-547">Name</span></span>| <span data-ttu-id="16d0b-548">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-548">Type</span></span>| <span data-ttu-id="16d0b-549">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-549">Maximum size</span></span> | <span data-ttu-id="16d0b-550">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-550">Required</span></span> | <span data-ttu-id="16d0b-551">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-551">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="16d0b-552">string</span><span class="sxs-lookup"><span data-stu-id="16d0b-552">string</span></span>|<span data-ttu-id="16d0b-553">36 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-553">36 characters</span></span>|<span data-ttu-id="16d0b-554">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-554">✔</span></span>|<span data-ttu-id="16d0b-555">Id. de aplicación de AAD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-555">AAD application id of the app.</span></span> <span data-ttu-id="16d0b-556">Este identificador debe ser un GUID.</span><span class="sxs-lookup"><span data-stu-id="16d0b-556">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="16d0b-557">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-557">string</span></span>|<span data-ttu-id="16d0b-558">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-558">2048 characters</span></span>|<span data-ttu-id="16d0b-559">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-559">✔</span></span>|<span data-ttu-id="16d0b-560">Dirección URL de recurso de la aplicación para adquirir token de autenticación para SSO.</span><span class="sxs-lookup"><span data-stu-id="16d0b-560">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="16d0b-561">**NOTA:** Si no usa SSO, asegúrese de escribir un valor de cadena ficticia en este campo en el manifiesto de la aplicación, por ejemplo, para evitar https://notapplicable una respuesta de error.</span><span class="sxs-lookup"><span data-stu-id="16d0b-561">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="16d0b-562">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="16d0b-562">array of strings</span></span>|<span data-ttu-id="16d0b-563">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-563">128 characters</span></span>||<span data-ttu-id="16d0b-564">Especifique el consentimiento [específico del recurso pormenorizados](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span><span class="sxs-lookup"><span data-stu-id="16d0b-564">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="16d0b-565">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="16d0b-565">showLoadingIndicator</span></span>

<span data-ttu-id="16d0b-566">**Opcional:** booleano</span><span class="sxs-lookup"><span data-stu-id="16d0b-566">**Optional** — boolean</span></span>

<span data-ttu-id="16d0b-567">Indica si se va a mostrar el indicador de carga cuando se carga una aplicación o una pestaña.</span><span class="sxs-lookup"><span data-stu-id="16d0b-567">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="16d0b-568">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="16d0b-568">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="16d0b-569">Si seleccionas como true en el manifiesto de la aplicación, para cargar la página correctamente, modifica las páginas de contenido de las pestañas y los módulos de tareas como se describe en Mostrar un documento de indicador de carga `showLoadingIndicator` nativo. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="16d0b-569">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="16d0b-570">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="16d0b-570">isFullScreen</span></span>

 <span data-ttu-id="16d0b-571">**Opcional:** booleano</span><span class="sxs-lookup"><span data-stu-id="16d0b-571">**Optional** — boolean</span></span>

<span data-ttu-id="16d0b-572">Indica dónde se representa una aplicación personal con o sin una barra de encabezado de pestaña.</span><span class="sxs-lookup"><span data-stu-id="16d0b-572">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="16d0b-573">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="16d0b-573">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="16d0b-574">activities</span><span class="sxs-lookup"><span data-stu-id="16d0b-574">activities</span></span>

<span data-ttu-id="16d0b-575">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="16d0b-575">**Optional** — object</span></span>

<span data-ttu-id="16d0b-576">Define las propiedades que usa la aplicación para publicar una fuente de actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="16d0b-576">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="16d0b-577">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-577">Name</span></span>| <span data-ttu-id="16d0b-578">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-578">Type</span></span>| <span data-ttu-id="16d0b-579">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-579">Maximum size</span></span> | <span data-ttu-id="16d0b-580">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-580">Required</span></span> | <span data-ttu-id="16d0b-581">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-581">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="16d0b-582">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="16d0b-582">array of Objects</span></span>|<span data-ttu-id="16d0b-583">128 elementos</span><span class="sxs-lookup"><span data-stu-id="16d0b-583">128 items</span></span>| | <span data-ttu-id="16d0b-584">Proporciona los tipos de actividades que la aplicación puede publicar en una fuente de actividad de usuarios.</span><span class="sxs-lookup"><span data-stu-id="16d0b-584">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="16d0b-585">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="16d0b-585">activities.activityTypes</span></span>

|<span data-ttu-id="16d0b-586">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-586">Name</span></span>| <span data-ttu-id="16d0b-587">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-587">Type</span></span>| <span data-ttu-id="16d0b-588">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-588">Maximum size</span></span> | <span data-ttu-id="16d0b-589">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-589">Required</span></span> | <span data-ttu-id="16d0b-590">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-590">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="16d0b-591">string</span><span class="sxs-lookup"><span data-stu-id="16d0b-591">string</span></span>|<span data-ttu-id="16d0b-592">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-592">32 characters</span></span>|<span data-ttu-id="16d0b-593">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-593">✔</span></span>|<span data-ttu-id="16d0b-594">Tipo de notificación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-594">The notification type.</span></span> <span data-ttu-id="16d0b-595">*Vea a continuación*.</span><span class="sxs-lookup"><span data-stu-id="16d0b-595">*See below*.</span></span>|
|`description`|<span data-ttu-id="16d0b-596">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-596">string</span></span>|<span data-ttu-id="16d0b-597">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-597">128 characters</span></span>|<span data-ttu-id="16d0b-598">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-598">✔</span></span>|<span data-ttu-id="16d0b-599">Breve descripción de la notificación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-599">A brief description of the notification.</span></span> <span data-ttu-id="16d0b-600">*Vea a continuación*.</span><span class="sxs-lookup"><span data-stu-id="16d0b-600">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="16d0b-601">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-601">string</span></span>|<span data-ttu-id="16d0b-602">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="16d0b-602">128 characters</span></span>|<span data-ttu-id="16d0b-603">✔</span><span class="sxs-lookup"><span data-stu-id="16d0b-603">✔</span></span>|<span data-ttu-id="16d0b-604">Ex: "{actor} created task {taskId} for you"</span><span class="sxs-lookup"><span data-stu-id="16d0b-604">Ex: "{actor} created task {taskId} for you"</span></span>|

```json
{
   "activities":{
      "activityTypes":[
         {
            "type":"taskCreated",
            "description":"Task Created Activity",
            "templateText":"{actor} created task {taskId} for you"
         },
         {
            "type":"teamMention",
            "description":"Team Mention Activity",
            "templateText":"{actor} mentioned team"
         },
         {
            "type":"channelMention",
            "description":"Channel Mention Activity",
            "templateText":"{actor} mentioned channel"
         },
         {
            "type":"userMention",
            "description":"Personal Mention Activity",
            "templateText":"{actor} mentioned user"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"creatorTaskCreated",
            "description":"Created Task Created",
            "templateText":"The Creator created task {taskId} for you"
         }
      ]
   }
}
```

***

## <a name="defaultinstallscope"></a><span data-ttu-id="16d0b-605">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="16d0b-605">defaultInstallScope</span></span>

<span data-ttu-id="16d0b-606">**Opcional** : cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-606">**Optional** - string</span></span>

<span data-ttu-id="16d0b-607">Especifica el ámbito de instalación definido para esta aplicación de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="16d0b-607">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="16d0b-608">El ámbito definido será la opción que se muestra en el botón cuando un usuario intente agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-608">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="16d0b-609">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="16d0b-609">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="16d0b-610">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="16d0b-610">defaultGroupCapability</span></span>

<span data-ttu-id="16d0b-611">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="16d0b-611">**Optional** - object</span></span>

<span data-ttu-id="16d0b-612">Cuando se selecciona un ámbito de instalación de grupo, se definirá la funcionalidad predeterminada cuando el usuario instale la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-612">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="16d0b-613">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="16d0b-613">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="16d0b-614">Nombre</span><span class="sxs-lookup"><span data-stu-id="16d0b-614">Name</span></span>| <span data-ttu-id="16d0b-615">Tipo</span><span class="sxs-lookup"><span data-stu-id="16d0b-615">Type</span></span>| <span data-ttu-id="16d0b-616">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="16d0b-616">Maximum size</span></span> | <span data-ttu-id="16d0b-617">Necesario</span><span class="sxs-lookup"><span data-stu-id="16d0b-617">Required</span></span> | <span data-ttu-id="16d0b-618">Descripción</span><span class="sxs-lookup"><span data-stu-id="16d0b-618">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="16d0b-619">string</span><span class="sxs-lookup"><span data-stu-id="16d0b-619">string</span></span>|||<span data-ttu-id="16d0b-620">Cuando el ámbito de instalación seleccionado es `team` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="16d0b-620">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="16d0b-621">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-621">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="16d0b-622">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-622">string</span></span>|||<span data-ttu-id="16d0b-623">Cuando el ámbito de instalación seleccionado es `groupchat` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="16d0b-623">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="16d0b-624">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-624">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="16d0b-625">cadena</span><span class="sxs-lookup"><span data-stu-id="16d0b-625">string</span></span>|||<span data-ttu-id="16d0b-626">Cuando el ámbito de instalación seleccionado es `meetings` , este campo especifica la funcionalidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="16d0b-626">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="16d0b-627">Opciones: `tab` `bot` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="16d0b-627">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="16d0b-628">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="16d0b-628">configurableProperties</span></span>

<span data-ttu-id="16d0b-629">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="16d0b-629">**Optional** - array</span></span>

<span data-ttu-id="16d0b-630">El `configurableProperties` bloque define las propiedades de la aplicación que Teams los administradores pueden personalizar.</span><span class="sxs-lookup"><span data-stu-id="16d0b-630">The `configurableProperties` block defines the app properties that Teams admins can customize.</span></span> <span data-ttu-id="16d0b-631">Para obtener más información, consulta [Habilitar la personalización de la aplicación](~/concepts/design/enable-app-customization.md).</span><span class="sxs-lookup"><span data-stu-id="16d0b-631">For more information, see [enable app customization](~/concepts/design/enable-app-customization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="16d0b-632">Debe definirse un mínimo de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="16d0b-632">A minimum of one property must be defined.</span></span> <span data-ttu-id="16d0b-633">Puede definir un máximo de nueve propiedades en este bloque.</span><span class="sxs-lookup"><span data-stu-id="16d0b-633">You can define a maximum of nine properties in this block.</span></span>

<span data-ttu-id="16d0b-634">Puede definir cualquiera de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="16d0b-634">You can define any of the following properties:</span></span>

* <span data-ttu-id="16d0b-635">`name`: nombre para mostrar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-635">`name`: The app's display name.</span></span>
* <span data-ttu-id="16d0b-636">`shortDescription`: descripción breve de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-636">`shortDescription`: The app's short description.</span></span>
* <span data-ttu-id="16d0b-637">`longDescription`: descripción detallada de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-637">`longDescription`: The app's detailed description.</span></span>
* <span data-ttu-id="16d0b-638">`smallImageUrl`: icono de esquema de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-638">`smallImageUrl`: The app's outline icon.</span></span>
* <span data-ttu-id="16d0b-639">`largeImageUrl`: icono de color de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16d0b-639">`largeImageUrl`: The app's color icon.</span></span>
* <span data-ttu-id="16d0b-640">`accentColor`: color que se usará junto con y como fondo para los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="16d0b-640">`accentColor`: The color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="16d0b-641">`developerUrl`: la dirección URL HTTPS del sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="16d0b-641">`developerUrl`: The HTTPS URL of the developer's website.</span></span>
* <span data-ttu-id="16d0b-642">`privacyUrl`: la dirección URL HTTPS de la directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="16d0b-642">`privacyUrl`: The HTTPS URL of the developer's privacy policy.</span></span>
* <span data-ttu-id="16d0b-643">`termsOfUseUrl`: la dirección URL HTTPS de los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="16d0b-643">`termsOfUseUrl`: The HTTPS URL of the developer's terms of use.</span></span>
