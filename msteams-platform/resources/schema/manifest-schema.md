---
title: Referencia de esquema de manifiesto
description: Describe el esquema del manifiesto para Microsoft Teams
keywords: esquema del manifiesto de Microsoft Teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: c66add190b0492170acf9756980ee16fb1fdf1fd
ms.sourcegitcommit: 5f1d6c12d80d48f403b73586f68bacf15785c855
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/30/2020
ms.locfileid: "49739059"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="56e29-104">Referencia: esquema de manifiesto para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="56e29-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="56e29-105">El manifiesto de Microsoft Teams describe cómo se integra la aplicación en el producto de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="56e29-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="56e29-106">El manifiesto debe cumplir el esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="56e29-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="56e29-107">También se admiten las versiones anteriores 1.0-1.4 (mediante "v1. x" en la dirección URL).</span><span class="sxs-lookup"><span data-stu-id="56e29-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="56e29-108">En el siguiente ejemplo de esquema se muestran todas las opciones de extensibilidad.</span><span class="sxs-lookup"><span data-stu-id="56e29-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="56e29-109">Manifiesto completo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="56e29-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.8",
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
  }
}
```

<span data-ttu-id="56e29-110">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="56e29-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="56e29-111">$schema</span><span class="sxs-lookup"><span data-stu-id="56e29-111">$schema</span></span>

<span data-ttu-id="56e29-112">*Opcional, pero recomendado* , String</span><span class="sxs-lookup"><span data-stu-id="56e29-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="56e29-113">La dirección URL de https://que hace referencia al esquema JSON del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="56e29-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="56e29-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="56e29-114">manifestVersion</span></span>

<span data-ttu-id="56e29-115">**Obligatorio** : String</span><span class="sxs-lookup"><span data-stu-id="56e29-115">**Required** — string</span></span>

<span data-ttu-id="56e29-116">La versión del esquema del manifiesto que está usando este manifiesto.</span><span class="sxs-lookup"><span data-stu-id="56e29-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="56e29-117">Debe ser "1,7".</span><span class="sxs-lookup"><span data-stu-id="56e29-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="56e29-118">version</span><span class="sxs-lookup"><span data-stu-id="56e29-118">version</span></span>

<span data-ttu-id="56e29-119">**Obligatorio** : String</span><span class="sxs-lookup"><span data-stu-id="56e29-119">**Required** — string</span></span>

<span data-ttu-id="56e29-120">La versión de la aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="56e29-120">The version of the specific app.</span></span> <span data-ttu-id="56e29-121">Si actualiza algo en el manifiesto, la versión también debe incrementarse.</span><span class="sxs-lookup"><span data-stu-id="56e29-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="56e29-122">De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="56e29-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="56e29-123">Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y a validarse.</span><span class="sxs-lookup"><span data-stu-id="56e29-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="56e29-124">A continuación, los usuarios de esta aplicación recibirán el nuevo manifiesto actualizado automáticamente en unas pocas horas, después de que se apruebe.</span><span class="sxs-lookup"><span data-stu-id="56e29-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="56e29-125">Si la aplicación ha solicitado un cambio de permisos, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="56e29-126">Esta cadena de versión debe seguir el estándar [SemVer](http://semver.org/) (Major. Secundaria. REVISIÓN).</span><span class="sxs-lookup"><span data-stu-id="56e29-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="56e29-127">id</span><span class="sxs-lookup"><span data-stu-id="56e29-127">id</span></span>

<span data-ttu-id="56e29-128">**Obligatorio** : identificador de aplicación de Microsoft</span><span class="sxs-lookup"><span data-stu-id="56e29-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="56e29-129">El identificador único generado por Microsoft para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="56e29-130">Si ha registrado un bot a través de Microsoft bot Framework o la aplicación Web de su pestaña ya inicia sesión en Microsoft, debe tener ya un identificador y escribirlo aquí.</span><span class="sxs-lookup"><span data-stu-id="56e29-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="56e29-131">De lo contrario, debe generar un nuevo identificador en el portal de registro de aplicaciones de Microsoft ([mis aplicaciones](https://apps.dev.microsoft.com)), escribirlo aquí y volver a usarlo cuando agregue un bot. Nota: Si va a enviar una actualización a su aplicación existente en AppSource, el identificador del manifiesto no debe modificarse.</span><span class="sxs-lookup"><span data-stu-id="56e29-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="56e29-132">developer</span><span class="sxs-lookup"><span data-stu-id="56e29-132">developer</span></span>

<span data-ttu-id="56e29-133">**Obligatorio** : Object</span><span class="sxs-lookup"><span data-stu-id="56e29-133">**Required** — object</span></span>

<span data-ttu-id="56e29-134">Especifica información sobre la compañía.</span><span class="sxs-lookup"><span data-stu-id="56e29-134">Specifies information about your company.</span></span> <span data-ttu-id="56e29-135">Para las aplicaciones enviadas a AppSource (anteriormente tienda Office), estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="56e29-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="56e29-136">Consulte nuestras [directrices de publicación](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="56e29-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="56e29-137">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-137">Name</span></span>| <span data-ttu-id="56e29-138">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-138">Maximum size</span></span> | <span data-ttu-id="56e29-139">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-139">Required</span></span> | <span data-ttu-id="56e29-140">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="56e29-141">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-141">32 characters</span></span>|<span data-ttu-id="56e29-142">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-142">✔</span></span>|<span data-ttu-id="56e29-143">El nombre para mostrar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="56e29-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="56e29-144">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-144">2048 characters</span></span>|<span data-ttu-id="56e29-145">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-145">✔</span></span>|<span data-ttu-id="56e29-146">La dirección URL https://al sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="56e29-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="56e29-147">Este vínculo debe llevar a los usuarios a su compañía o a la página de aterrizaje específica del producto.</span><span class="sxs-lookup"><span data-stu-id="56e29-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="56e29-148">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-148">2048 characters</span></span>|<span data-ttu-id="56e29-149">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-149">✔</span></span>|<span data-ttu-id="56e29-150">La dirección URL de https://a la Directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="56e29-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="56e29-151">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-151">2048 characters</span></span>|<span data-ttu-id="56e29-152">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-152">✔</span></span>|<span data-ttu-id="56e29-153">La dirección URL de https://a las condiciones de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="56e29-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="56e29-154">10 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-154">10 characters</span></span>| |<span data-ttu-id="56e29-155">**Opcional** IDENTIFICADOR de red de los socios de Microsoft que identifica la organización asociada que crea la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="56e29-156">name</span><span class="sxs-lookup"><span data-stu-id="56e29-156">name</span></span>

<span data-ttu-id="56e29-157">**Obligatorio** : Object</span><span class="sxs-lookup"><span data-stu-id="56e29-157">**Required** — object</span></span>

<span data-ttu-id="56e29-158">El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="56e29-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="56e29-159">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="56e29-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="56e29-160">Los valores de `short` y `full` no deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="56e29-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="56e29-161">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-161">Name</span></span>| <span data-ttu-id="56e29-162">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-162">Maximum size</span></span> | <span data-ttu-id="56e29-163">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-163">Required</span></span> | <span data-ttu-id="56e29-164">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="56e29-165">30 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-165">30 characters</span></span>|<span data-ttu-id="56e29-166">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-166">✔</span></span>|<span data-ttu-id="56e29-167">El nombre para mostrar corto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="56e29-168">100 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-168">100 characters</span></span>||<span data-ttu-id="56e29-169">El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="56e29-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="56e29-170">description</span><span class="sxs-lookup"><span data-stu-id="56e29-170">description</span></span>

<span data-ttu-id="56e29-171">**Obligatorio** : Object</span><span class="sxs-lookup"><span data-stu-id="56e29-171">**Required** — object</span></span>

<span data-ttu-id="56e29-172">Describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="56e29-172">Describes your app to users.</span></span> <span data-ttu-id="56e29-173">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="56e29-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="56e29-174">Asegúrese de que la descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia.</span><span class="sxs-lookup"><span data-stu-id="56e29-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="56e29-175">También debe tener en cuenta, en la descripción completa, si se requiere uso de una cuenta externa.</span><span class="sxs-lookup"><span data-stu-id="56e29-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="56e29-176">Los valores de `short` y `full` no deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="56e29-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="56e29-177">La descripción breve no debe repetirse en la descripción larga y no debe incluir ningún otro nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="56e29-178">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-178">Name</span></span>| <span data-ttu-id="56e29-179">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-179">Maximum size</span></span> | <span data-ttu-id="56e29-180">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-180">Required</span></span> | <span data-ttu-id="56e29-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="56e29-182">80 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-182">80 characters</span></span>|<span data-ttu-id="56e29-183">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-183">✔</span></span>|<span data-ttu-id="56e29-184">Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.</span><span class="sxs-lookup"><span data-stu-id="56e29-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="56e29-185">4000 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-185">4000 characters</span></span>|<span data-ttu-id="56e29-186">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-186">✔</span></span>|<span data-ttu-id="56e29-187">La descripción completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="56e29-188">packageName</span><span class="sxs-lookup"><span data-stu-id="56e29-188">packageName</span></span>

<span data-ttu-id="56e29-189">**Opcional** : cadena</span><span class="sxs-lookup"><span data-stu-id="56e29-189">**Optional** — string</span></span>

<span data-ttu-id="56e29-190">Un identificador único para esta aplicación en la notación de dominio inverso; por ejemplo, com. example. myapp.</span><span class="sxs-lookup"><span data-stu-id="56e29-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="56e29-191">Longitud máxima: 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="56e29-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="56e29-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="56e29-192">localizationInfo</span></span>

<span data-ttu-id="56e29-193">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="56e29-193">**Optional** — object</span></span>

<span data-ttu-id="56e29-194">Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="56e29-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="56e29-195">Consulte [localización](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="56e29-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="56e29-196">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-196">Name</span></span>| <span data-ttu-id="56e29-197">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-197">Maximum size</span></span> | <span data-ttu-id="56e29-198">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-198">Required</span></span> | <span data-ttu-id="56e29-199">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="56e29-200">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-200">✔</span></span>|<span data-ttu-id="56e29-201">La etiqueta de idioma de las cadenas en este archivo de manifiesto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="56e29-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="56e29-202">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="56e29-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="56e29-203">Una matriz de objetos que especifica traducciones de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="56e29-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="56e29-204">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-204">Name</span></span>| <span data-ttu-id="56e29-205">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-205">Maximum size</span></span> | <span data-ttu-id="56e29-206">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-206">Required</span></span> | <span data-ttu-id="56e29-207">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="56e29-208">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-208">✔</span></span>|<span data-ttu-id="56e29-209">La etiqueta de idioma de las cadenas en el archivo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="56e29-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="56e29-210">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-210">✔</span></span>|<span data-ttu-id="56e29-211">Una ruta de acceso relativa a un archivo. JSON que contiene las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="56e29-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="56e29-212">iconos</span><span class="sxs-lookup"><span data-stu-id="56e29-212">icons</span></span>

<span data-ttu-id="56e29-213">**Obligatorio** : Object</span><span class="sxs-lookup"><span data-stu-id="56e29-213">**Required** — object</span></span>

<span data-ttu-id="56e29-214">Iconos usados en la aplicación Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="56e29-214">Icons used within the Teams app.</span></span> <span data-ttu-id="56e29-215">Los archivos de icono deben incluirse como parte del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="56e29-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="56e29-216">Vea [iconos](../../concepts/build-and-test/apps-package.md#app-icons) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="56e29-216">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="56e29-217">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-217">Name</span></span>| <span data-ttu-id="56e29-218">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-218">Maximum size</span></span> | <span data-ttu-id="56e29-219">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-219">Required</span></span> | <span data-ttu-id="56e29-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="56e29-221">32 x 32 píxeles</span><span class="sxs-lookup"><span data-stu-id="56e29-221">32 x 32 pixels</span></span>|<span data-ttu-id="56e29-222">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-222">✔</span></span>|<span data-ttu-id="56e29-223">Una ruta de acceso relativa a un icono de esquema PNG transparente de 32x32.</span><span class="sxs-lookup"><span data-stu-id="56e29-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="56e29-224">192 x 192 píxeles</span><span class="sxs-lookup"><span data-stu-id="56e29-224">192 x 192 pixels</span></span>|<span data-ttu-id="56e29-225">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-225">✔</span></span>|<span data-ttu-id="56e29-226">Una ruta de acceso de archivo relativa a un icono PNG 192x192 de color completo.</span><span class="sxs-lookup"><span data-stu-id="56e29-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="56e29-227">accentColor</span><span class="sxs-lookup"><span data-stu-id="56e29-227">accentColor</span></span>

<span data-ttu-id="56e29-228">**Opcional** : código de color hexadecimal HTML</span><span class="sxs-lookup"><span data-stu-id="56e29-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="56e29-229">Color que se va a usar junto con y como fondo de los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="56e29-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="56e29-230">El valor debe ser un código de color HTML válido que empiece por ' # ', por ejemplo `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="56e29-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="56e29-231">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="56e29-231">configurableTabs</span></span>

<span data-ttu-id="56e29-232">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="56e29-232">**Optional** — array</span></span>

<span data-ttu-id="56e29-233">Se usa cuando la experiencia de la aplicación tiene una experiencia de la pestaña de canal de equipo que requiere una configuración adicional antes de que se agregue.</span><span class="sxs-lookup"><span data-stu-id="56e29-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="56e29-234">Las pestañas configurables solo se admiten en el ámbito de Teams (no en personal) y actualmente solo se admite **una** pestaña por aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="56e29-235">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-235">Name</span></span>| <span data-ttu-id="56e29-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="56e29-236">Type</span></span>| <span data-ttu-id="56e29-237">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-237">Maximum size</span></span> | <span data-ttu-id="56e29-238">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-238">Required</span></span> | <span data-ttu-id="56e29-239">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="56e29-240">string</span><span class="sxs-lookup"><span data-stu-id="56e29-240">string</span></span>|<span data-ttu-id="56e29-241">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-241">2048 characters</span></span>|<span data-ttu-id="56e29-242">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-242">✔</span></span>|<span data-ttu-id="56e29-243">Dirección URL de https://que se va a usar al configurar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="56e29-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="56e29-244">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="56e29-244">array of enums</span></span>|<span data-ttu-id="56e29-245">1 </span><span class="sxs-lookup"><span data-stu-id="56e29-245">1</span></span>|<span data-ttu-id="56e29-246">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-246">✔</span></span>|<span data-ttu-id="56e29-247">Actualmente, las pestañas configurables solo admiten los `team` `groupchat` ámbitos y.</span><span class="sxs-lookup"><span data-stu-id="56e29-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="56e29-248">boolean</span><span class="sxs-lookup"><span data-stu-id="56e29-248">boolean</span></span>|||<span data-ttu-id="56e29-249">Un valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de crearla.</span><span class="sxs-lookup"><span data-stu-id="56e29-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="56e29-250">Valor predeterminado: **true**.</span><span class="sxs-lookup"><span data-stu-id="56e29-250">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="56e29-251">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="56e29-251">array of enums</span></span>|<span data-ttu-id="56e29-252">6 </span><span class="sxs-lookup"><span data-stu-id="56e29-252">6</span></span>||<span data-ttu-id="56e29-253">El conjunto de `contextItem` ámbitos en los que se admite una pestaña.</span><span class="sxs-lookup"><span data-stu-id="56e29-253">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="56e29-254">Valor predeterminado: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="56e29-254">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="56e29-255">string</span><span class="sxs-lookup"><span data-stu-id="56e29-255">string</span></span>|<span data-ttu-id="56e29-256">2048</span><span class="sxs-lookup"><span data-stu-id="56e29-256">2048</span></span>||<span data-ttu-id="56e29-257">Una ruta de acceso de archivo relativa a una imagen de vista previa de pestaña para su uso en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="56e29-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="56e29-258">Tamaño 1024x768.</span><span class="sxs-lookup"><span data-stu-id="56e29-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="56e29-259">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="56e29-259">array of enums</span></span>|<span data-ttu-id="56e29-260">1 </span><span class="sxs-lookup"><span data-stu-id="56e29-260">1</span></span>||<span data-ttu-id="56e29-261">Define cómo estará disponible la pestaña en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="56e29-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="56e29-262">Las opciones son `sharePointFullPage` y `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="56e29-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="56e29-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="56e29-263">staticTabs</span></span>

<span data-ttu-id="56e29-264">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="56e29-264">**Optional** — array</span></span>

<span data-ttu-id="56e29-265">Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente.</span><span class="sxs-lookup"><span data-stu-id="56e29-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="56e29-266">Las pestañas estáticas declaradas en `personal` el ámbito siempre están ancladas a la experiencia personal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="56e29-267">Actualmente no se admiten las pestañas estáticas declaradas en el `team` ámbito.</span><span class="sxs-lookup"><span data-stu-id="56e29-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="56e29-268">Este elemento es una matriz (un máximo de 16 elementos) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="56e29-268">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="56e29-269">Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña estática.</span><span class="sxs-lookup"><span data-stu-id="56e29-269">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="56e29-270">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-270">Name</span></span>| <span data-ttu-id="56e29-271">Tipo</span><span class="sxs-lookup"><span data-stu-id="56e29-271">Type</span></span>| <span data-ttu-id="56e29-272">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-272">Maximum size</span></span> | <span data-ttu-id="56e29-273">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-273">Required</span></span> | <span data-ttu-id="56e29-274">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-274">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="56e29-275">string</span><span class="sxs-lookup"><span data-stu-id="56e29-275">string</span></span>|<span data-ttu-id="56e29-276">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-276">64 characters</span></span>|<span data-ttu-id="56e29-277">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-277">✔</span></span>|<span data-ttu-id="56e29-278">Un identificador único para la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="56e29-278">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="56e29-279">string</span><span class="sxs-lookup"><span data-stu-id="56e29-279">string</span></span>|<span data-ttu-id="56e29-280">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-280">128 characters</span></span>|<span data-ttu-id="56e29-281">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-281">✔</span></span>|<span data-ttu-id="56e29-282">El nombre para mostrar de la pestaña en la interfaz de canal.</span><span class="sxs-lookup"><span data-stu-id="56e29-282">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="56e29-283">string</span><span class="sxs-lookup"><span data-stu-id="56e29-283">string</span></span>||<span data-ttu-id="56e29-284">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-284">✔</span></span>|<span data-ttu-id="56e29-285">Dirección URL de https://que señala a la interfaz de usuario de la entidad que se va a mostrar en el lienzo de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="56e29-285">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="56e29-286">string</span><span class="sxs-lookup"><span data-stu-id="56e29-286">string</span></span>|||<span data-ttu-id="56e29-287">Dirección URL de https://para apuntar a si un usuario opta por verlo en un explorador.</span><span class="sxs-lookup"><span data-stu-id="56e29-287">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="56e29-288">string</span><span class="sxs-lookup"><span data-stu-id="56e29-288">string</span></span>|||<span data-ttu-id="56e29-289">Dirección URL de https://para apuntar a las consultas de búsqueda de un usuario.</span><span class="sxs-lookup"><span data-stu-id="56e29-289">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="56e29-290">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="56e29-290">array of enums</span></span>|<span data-ttu-id="56e29-291">1 </span><span class="sxs-lookup"><span data-stu-id="56e29-291">1</span></span>|<span data-ttu-id="56e29-292">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-292">✔</span></span>|<span data-ttu-id="56e29-293">Actualmente, las pestañas estáticas solo admiten el `personal` ámbito, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.</span><span class="sxs-lookup"><span data-stu-id="56e29-293">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="56e29-294">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="56e29-294">array of enums</span></span>| <span data-ttu-id="56e29-295">2 </span><span class="sxs-lookup"><span data-stu-id="56e29-295">2</span></span>|| <span data-ttu-id="56e29-296">El conjunto de `contextItem` ámbitos en los que se admite una pestaña.</span><span class="sxs-lookup"><span data-stu-id="56e29-296">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="56e29-297">Si las pestañas requieren información dependiente del contexto para mostrar contenido relevante o para iniciar un flujo de autenticación, *vea* [obtener contexto para la pestaña de Microsoft Teams](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="56e29-297">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="56e29-298">transferido</span><span class="sxs-lookup"><span data-stu-id="56e29-298">bots</span></span>

<span data-ttu-id="56e29-299">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="56e29-299">**Optional** — array</span></span>

<span data-ttu-id="56e29-300">Define una solución de bot, junto con información opcional como propiedades de comando predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="56e29-300">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="56e29-301">El elemento es una matriz (un máximo solo de un elemento, &mdash; actualmente solo se permite un bot por aplicación) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="56e29-301">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="56e29-302">Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.</span><span class="sxs-lookup"><span data-stu-id="56e29-302">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="56e29-303">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-303">Name</span></span>| <span data-ttu-id="56e29-304">Tipo</span><span class="sxs-lookup"><span data-stu-id="56e29-304">Type</span></span>| <span data-ttu-id="56e29-305">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-305">Maximum size</span></span> | <span data-ttu-id="56e29-306">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-306">Required</span></span> | <span data-ttu-id="56e29-307">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-307">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="56e29-308">string</span><span class="sxs-lookup"><span data-stu-id="56e29-308">string</span></span>|<span data-ttu-id="56e29-309">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-309">64 characters</span></span>|<span data-ttu-id="56e29-310">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-310">✔</span></span>|<span data-ttu-id="56e29-311">El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="56e29-311">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="56e29-312">Puede ser el mismo que el [identificador de aplicación](#id)general.</span><span class="sxs-lookup"><span data-stu-id="56e29-312">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="56e29-313">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="56e29-313">array of enums</span></span>|<span data-ttu-id="56e29-314">3 </span><span class="sxs-lookup"><span data-stu-id="56e29-314">3</span></span>|<span data-ttu-id="56e29-315">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-315">✔</span></span>|<span data-ttu-id="56e29-316">Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`).</span><span class="sxs-lookup"><span data-stu-id="56e29-316">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="56e29-317">Estas opciones no son exclusivas.</span><span class="sxs-lookup"><span data-stu-id="56e29-317">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="56e29-318">boolean</span><span class="sxs-lookup"><span data-stu-id="56e29-318">boolean</span></span>|||<span data-ttu-id="56e29-319">Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico.</span><span class="sxs-lookup"><span data-stu-id="56e29-319">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="56e29-320">Predeterminada **`false`**</span><span class="sxs-lookup"><span data-stu-id="56e29-320">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="56e29-321">boolean</span><span class="sxs-lookup"><span data-stu-id="56e29-321">boolean</span></span>|||<span data-ttu-id="56e29-322">Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación.</span><span class="sxs-lookup"><span data-stu-id="56e29-322">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="56e29-323">Predeterminada **`false`**</span><span class="sxs-lookup"><span data-stu-id="56e29-323">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="56e29-324">boolean</span><span class="sxs-lookup"><span data-stu-id="56e29-324">boolean</span></span>|||<span data-ttu-id="56e29-325">Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal.</span><span class="sxs-lookup"><span data-stu-id="56e29-325">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="56e29-326">Predeterminada **`false`**</span><span class="sxs-lookup"><span data-stu-id="56e29-326">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="56e29-327">boolean</span><span class="sxs-lookup"><span data-stu-id="56e29-327">boolean</span></span>|||<span data-ttu-id="56e29-328">Un valor que indica dónde es compatible un bot con las llamadas de audio.</span><span class="sxs-lookup"><span data-stu-id="56e29-328">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="56e29-329">**Importante**: esta propiedad es experimental actualmente.</span><span class="sxs-lookup"><span data-stu-id="56e29-329">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="56e29-330">Es posible que las propiedades experimentales no estén completas y puedan sufrir cambios antes de que estén completamente disponibles.</span><span class="sxs-lookup"><span data-stu-id="56e29-330">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="56e29-331">Se proporciona solo para fines de prueba y exploración y no debe usarse en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="56e29-331">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="56e29-332">Predeterminada **`false`**</span><span class="sxs-lookup"><span data-stu-id="56e29-332">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="56e29-333">boolean</span><span class="sxs-lookup"><span data-stu-id="56e29-333">boolean</span></span>|||<span data-ttu-id="56e29-334">Un valor que indica dónde es compatible una llamada de vídeo con un bot.</span><span class="sxs-lookup"><span data-stu-id="56e29-334">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="56e29-335">**Importante**: esta propiedad es experimental actualmente.</span><span class="sxs-lookup"><span data-stu-id="56e29-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="56e29-336">Es posible que las propiedades experimentales no estén completas y puedan sufrir cambios antes de que estén completamente disponibles.</span><span class="sxs-lookup"><span data-stu-id="56e29-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="56e29-337">Se proporciona solo para fines de prueba y exploración y no debe usarse en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="56e29-337">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="56e29-338">Predeterminada **`false`**</span><span class="sxs-lookup"><span data-stu-id="56e29-338">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="56e29-339">bots. commandLists</span><span class="sxs-lookup"><span data-stu-id="56e29-339">bots.commandLists</span></span>

<span data-ttu-id="56e29-340">Una lista opcional de comandos que el bot puede recomendar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="56e29-340">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="56e29-341">El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo `object` ; debe definir una lista de comandos independiente para cada ámbito que admita el bot.</span><span class="sxs-lookup"><span data-stu-id="56e29-341">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="56e29-342">Consulte [menús de bot](~/bots/how-to/create-a-bot-commands-menu.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="56e29-342">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="56e29-343">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-343">Name</span></span>| <span data-ttu-id="56e29-344">Tipo</span><span class="sxs-lookup"><span data-stu-id="56e29-344">Type</span></span>| <span data-ttu-id="56e29-345">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-345">Maximum size</span></span> | <span data-ttu-id="56e29-346">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-346">Required</span></span> | <span data-ttu-id="56e29-347">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-347">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="56e29-348">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="56e29-348">array of enums</span></span>|<span data-ttu-id="56e29-349">3 </span><span class="sxs-lookup"><span data-stu-id="56e29-349">3</span></span>|<span data-ttu-id="56e29-350">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-350">✔</span></span>|<span data-ttu-id="56e29-351">Especifica el ámbito para el que la lista de comandos es válida.</span><span class="sxs-lookup"><span data-stu-id="56e29-351">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="56e29-352">Las opciones son `team`, `personal` y `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="56e29-352">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="56e29-353">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="56e29-353">array of objects</span></span>|<span data-ttu-id="56e29-354">10 </span><span class="sxs-lookup"><span data-stu-id="56e29-354">10</span></span>|<span data-ttu-id="56e29-355">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-355">✔</span></span>|<span data-ttu-id="56e29-356">Una matriz de comandos que el bot admite:</span><span class="sxs-lookup"><span data-stu-id="56e29-356">An array of commands the bot supports:</span></span><br><span data-ttu-id="56e29-357">`title`: el nombre de comando del bot (cadena, 32)</span><span class="sxs-lookup"><span data-stu-id="56e29-357">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="56e29-358">`description`: una descripción o un ejemplo sencillo de la sintaxis del comando y su argumento (cadena, 128).</span><span class="sxs-lookup"><span data-stu-id="56e29-358">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="56e29-359">bots. commandLists. Commands</span><span class="sxs-lookup"><span data-stu-id="56e29-359">bots.commandLists.commands</span></span>

|<span data-ttu-id="56e29-360">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-360">Name</span></span>| <span data-ttu-id="56e29-361">Tipo</span><span class="sxs-lookup"><span data-stu-id="56e29-361">Type</span></span>| <span data-ttu-id="56e29-362">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-362">Maximum size</span></span> | <span data-ttu-id="56e29-363">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-363">Required</span></span> | <span data-ttu-id="56e29-364">Description</span><span class="sxs-lookup"><span data-stu-id="56e29-364">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="56e29-365">title</span><span class="sxs-lookup"><span data-stu-id="56e29-365">title</span></span>|<span data-ttu-id="56e29-366">string</span><span class="sxs-lookup"><span data-stu-id="56e29-366">string</span></span>|<span data-ttu-id="56e29-367">12 </span><span class="sxs-lookup"><span data-stu-id="56e29-367">12</span></span>|<span data-ttu-id="56e29-368">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-368">✔</span></span>|<span data-ttu-id="56e29-369">El nombre del comando bot</span><span class="sxs-lookup"><span data-stu-id="56e29-369">The bot command name</span></span>|
|<span data-ttu-id="56e29-370">description</span><span class="sxs-lookup"><span data-stu-id="56e29-370">description</span></span>|<span data-ttu-id="56e29-371">string</span><span class="sxs-lookup"><span data-stu-id="56e29-371">string</span></span>|<span data-ttu-id="56e29-372">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-372">128 characters</span></span>|<span data-ttu-id="56e29-373">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-373">✔</span></span>|<span data-ttu-id="56e29-374">Una descripción de texto simple o un ejemplo de la sintaxis del comando y sus argumentos.</span><span class="sxs-lookup"><span data-stu-id="56e29-374">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="56e29-375">Connector</span><span class="sxs-lookup"><span data-stu-id="56e29-375">connectors</span></span>

<span data-ttu-id="56e29-376">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="56e29-376">**Optional** — array</span></span>

<span data-ttu-id="56e29-377">El `connectors` bloque define un conector de Office 365 para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-377">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="56e29-378">El objeto es una matriz (un máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="56e29-378">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="56e29-379">Este bloque solo es necesario para las soluciones que proporcionan un conector.</span><span class="sxs-lookup"><span data-stu-id="56e29-379">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="56e29-380">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-380">Name</span></span>| <span data-ttu-id="56e29-381">Tipo</span><span class="sxs-lookup"><span data-stu-id="56e29-381">Type</span></span>| <span data-ttu-id="56e29-382">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-382">Maximum size</span></span> | <span data-ttu-id="56e29-383">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-383">Required</span></span> | <span data-ttu-id="56e29-384">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-384">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="56e29-385">string</span><span class="sxs-lookup"><span data-stu-id="56e29-385">string</span></span>|<span data-ttu-id="56e29-386">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-386">2048 characters</span></span>|<span data-ttu-id="56e29-387">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-387">✔</span></span>|<span data-ttu-id="56e29-388">Dirección URL de https://que se va a usar al configurar el conector.</span><span class="sxs-lookup"><span data-stu-id="56e29-388">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="56e29-389">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="56e29-389">array of enums</span></span>|<span data-ttu-id="56e29-390">1 </span><span class="sxs-lookup"><span data-stu-id="56e29-390">1</span></span>|<span data-ttu-id="56e29-391">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-391">✔</span></span>|<span data-ttu-id="56e29-392">Especifica si el conector ofrece una experiencia en el contexto de un canal en un `team` o una experiencia en el ámbito de un solo usuario individual ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="56e29-392">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="56e29-393">Actualmente, solo `team` se admite el ámbito.</span><span class="sxs-lookup"><span data-stu-id="56e29-393">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="56e29-394">string</span><span class="sxs-lookup"><span data-stu-id="56e29-394">string</span></span>|<span data-ttu-id="56e29-395">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-395">64 characters</span></span>|<span data-ttu-id="56e29-396">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-396">✔</span></span>|<span data-ttu-id="56e29-397">Un identificador único para el conector que coincide con su identificador en el [panel del programador de conectores](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="56e29-397">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="56e29-398">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="56e29-398">composeExtensions</span></span>

<span data-ttu-id="56e29-399">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="56e29-399">**Optional** — array</span></span>

<span data-ttu-id="56e29-400">Define una extensión de mensajería para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-400">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="56e29-401">El nombre de la característica se cambió de "redactar extensión" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="56e29-401">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="56e29-402">El elemento es una matriz (un máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="56e29-402">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="56e29-403">Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="56e29-403">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="56e29-404">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-404">Name</span></span>| <span data-ttu-id="56e29-405">Tipo</span><span class="sxs-lookup"><span data-stu-id="56e29-405">Type</span></span> | <span data-ttu-id="56e29-406">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-406">Maximum Size</span></span> | <span data-ttu-id="56e29-407">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="56e29-407">Required</span></span> | <span data-ttu-id="56e29-408">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-408">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="56e29-409">string</span><span class="sxs-lookup"><span data-stu-id="56e29-409">string</span></span>|<span data-ttu-id="56e29-410">64</span><span class="sxs-lookup"><span data-stu-id="56e29-410">64</span></span>|<span data-ttu-id="56e29-411">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-411">✔</span></span>|<span data-ttu-id="56e29-412">IDENTIFICADOR único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, tal como se registró con bot Framework.</span><span class="sxs-lookup"><span data-stu-id="56e29-412">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="56e29-413">Puede ser el mismo que el identificador de aplicación general.</span><span class="sxs-lookup"><span data-stu-id="56e29-413">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="56e29-414">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="56e29-414">array of objects</span></span>|<span data-ttu-id="56e29-415">10 </span><span class="sxs-lookup"><span data-stu-id="56e29-415">10</span></span>|<span data-ttu-id="56e29-416">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-416">✔</span></span>|<span data-ttu-id="56e29-417">matriz de comandos que admite la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="56e29-417">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="56e29-418">boolean</span><span class="sxs-lookup"><span data-stu-id="56e29-418">boolean</span></span>|||<span data-ttu-id="56e29-419">Un valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="56e29-419">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="56e29-420">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="56e29-420">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="56e29-421">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="56e29-421">array of Objects</span></span>|<span data-ttu-id="56e29-422">5 </span><span class="sxs-lookup"><span data-stu-id="56e29-422">5</span></span>||<span data-ttu-id="56e29-423">Una lista de controladores que permiten invocar las aplicaciones cuando se cumplen ciertas condiciones.</span><span class="sxs-lookup"><span data-stu-id="56e29-423">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="56e29-424">Los dominios también deben aparecer en `validDomains`</span><span class="sxs-lookup"><span data-stu-id="56e29-424">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="56e29-425">string</span><span class="sxs-lookup"><span data-stu-id="56e29-425">string</span></span>|||<span data-ttu-id="56e29-426">El tipo de controlador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="56e29-426">The type of message handler.</span></span> <span data-ttu-id="56e29-427">Debe ser `"link"`.</span><span class="sxs-lookup"><span data-stu-id="56e29-427">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="56e29-428">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="56e29-428">array of Strings</span></span>|||<span data-ttu-id="56e29-429">matriz de dominios para los que el controlador de mensajes de vínculo puede registrarse.</span><span class="sxs-lookup"><span data-stu-id="56e29-429">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="56e29-430">composeExtensions. Commands</span><span class="sxs-lookup"><span data-stu-id="56e29-430">composeExtensions.commands</span></span>

<span data-ttu-id="56e29-431">La extensión de mensajería debe declarar uno o más comandos.</span><span class="sxs-lookup"><span data-stu-id="56e29-431">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="56e29-432">Cada comando aparece en Microsoft Teams como una posible interacción desde el punto de entrada basado en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="56e29-432">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="56e29-433">Hay un máximo de 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="56e29-433">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="56e29-434">Cada elemento de comando es un objeto con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="56e29-434">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="56e29-435">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-435">Name</span></span>| <span data-ttu-id="56e29-436">Tipo</span><span class="sxs-lookup"><span data-stu-id="56e29-436">Type</span></span>| <span data-ttu-id="56e29-437">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-437">Maximum size</span></span> | <span data-ttu-id="56e29-438">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-438">Required</span></span> | <span data-ttu-id="56e29-439">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-439">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="56e29-440">string</span><span class="sxs-lookup"><span data-stu-id="56e29-440">string</span></span>|<span data-ttu-id="56e29-441">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-441">64 characters</span></span>|<span data-ttu-id="56e29-442">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-442">✔</span></span>|<span data-ttu-id="56e29-443">IDENTIFICADOR del comando.</span><span class="sxs-lookup"><span data-stu-id="56e29-443">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="56e29-444">string</span><span class="sxs-lookup"><span data-stu-id="56e29-444">string</span></span>|<span data-ttu-id="56e29-445">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-445">32 characters</span></span>|<span data-ttu-id="56e29-446">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-446">✔</span></span>|<span data-ttu-id="56e29-447">Nombre de comando fácil de tener.</span><span class="sxs-lookup"><span data-stu-id="56e29-447">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="56e29-448">string</span><span class="sxs-lookup"><span data-stu-id="56e29-448">string</span></span>|<span data-ttu-id="56e29-449">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-449">64 characters</span></span>||<span data-ttu-id="56e29-450">Tipo del comando.</span><span class="sxs-lookup"><span data-stu-id="56e29-450">Type of the command.</span></span> <span data-ttu-id="56e29-451">Uno de `query` o `action` .</span><span class="sxs-lookup"><span data-stu-id="56e29-451">One of `query` or `action`.</span></span> <span data-ttu-id="56e29-452">Valor predeterminado: **consulta**.</span><span class="sxs-lookup"><span data-stu-id="56e29-452">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="56e29-453">string</span><span class="sxs-lookup"><span data-stu-id="56e29-453">string</span></span>|<span data-ttu-id="56e29-454">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-454">128 characters</span></span>||<span data-ttu-id="56e29-455">La descripción que se muestra a los usuarios para indicar el propósito de este comando.</span><span class="sxs-lookup"><span data-stu-id="56e29-455">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="56e29-456">boolean</span><span class="sxs-lookup"><span data-stu-id="56e29-456">boolean</span></span>|||<span data-ttu-id="56e29-457">Un valor booleano que indica si el comando se debe ejecutar inicialmente sin ningún parámetro.</span><span class="sxs-lookup"><span data-stu-id="56e29-457">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="56e29-458">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="56e29-458">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="56e29-459">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="56e29-459">array of Strings</span></span>|<span data-ttu-id="56e29-460">3 </span><span class="sxs-lookup"><span data-stu-id="56e29-460">3</span></span>||<span data-ttu-id="56e29-461">Define desde dónde se puede invocar la extensión de mensajes.</span><span class="sxs-lookup"><span data-stu-id="56e29-461">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="56e29-462">Cualquier combinación de `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="56e29-462">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="56e29-463">El valor predeterminado es `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="56e29-463">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="56e29-464">boolean</span><span class="sxs-lookup"><span data-stu-id="56e29-464">boolean</span></span>|||<span data-ttu-id="56e29-465">Un valor booleano que indica si debe recuperar el módulo de tarea de forma dinámica.</span><span class="sxs-lookup"><span data-stu-id="56e29-465">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="56e29-466">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="56e29-466">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="56e29-467">object</span><span class="sxs-lookup"><span data-stu-id="56e29-467">object</span></span>|||<span data-ttu-id="56e29-468">Especifique el módulo de tarea que se cargará previamente cuando se use un comando de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="56e29-468">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="56e29-469">string</span><span class="sxs-lookup"><span data-stu-id="56e29-469">string</span></span>|<span data-ttu-id="56e29-470">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-470">64 characters</span></span>||<span data-ttu-id="56e29-471">Título del cuadro de diálogo inicial.</span><span class="sxs-lookup"><span data-stu-id="56e29-471">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="56e29-472">string</span><span class="sxs-lookup"><span data-stu-id="56e29-472">string</span></span>|||<span data-ttu-id="56e29-473">Ancho del cuadro de diálogo, ya sea un número en píxeles o un diseño predeterminado, como "Large", "Medium" o "Small".</span><span class="sxs-lookup"><span data-stu-id="56e29-473">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="56e29-474">string</span><span class="sxs-lookup"><span data-stu-id="56e29-474">string</span></span>|||<span data-ttu-id="56e29-475">Alto del cuadro de diálogo: número en píxeles o diseño predeterminado, como "Large", "Medium" o "Small".</span><span class="sxs-lookup"><span data-stu-id="56e29-475">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="56e29-476">string</span><span class="sxs-lookup"><span data-stu-id="56e29-476">string</span></span>|||<span data-ttu-id="56e29-477">Dirección URL de la WebView inicial.</span><span class="sxs-lookup"><span data-stu-id="56e29-477">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="56e29-478">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="56e29-478">array of object</span></span>|<span data-ttu-id="56e29-479">5 elementos</span><span class="sxs-lookup"><span data-stu-id="56e29-479">5 items</span></span>|<span data-ttu-id="56e29-480">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-480">✔</span></span>|<span data-ttu-id="56e29-481">La lista de parámetros que toma el comando.</span><span class="sxs-lookup"><span data-stu-id="56e29-481">The list of parameters the command takes.</span></span> <span data-ttu-id="56e29-482">Mínimo: 1; máximo: 5.</span><span class="sxs-lookup"><span data-stu-id="56e29-482">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="56e29-483">string</span><span class="sxs-lookup"><span data-stu-id="56e29-483">string</span></span>|<span data-ttu-id="56e29-484">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-484">64 characters</span></span>|<span data-ttu-id="56e29-485">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-485">✔</span></span>|<span data-ttu-id="56e29-486">El nombre del parámetro tal y como aparece en el cliente.</span><span class="sxs-lookup"><span data-stu-id="56e29-486">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="56e29-487">Se incluye en la solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="56e29-487">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="56e29-488">string</span><span class="sxs-lookup"><span data-stu-id="56e29-488">string</span></span>|<span data-ttu-id="56e29-489">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-489">32 characters</span></span>|<span data-ttu-id="56e29-490">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-490">✔</span></span>|<span data-ttu-id="56e29-491">Título descriptivo del parámetro.</span><span class="sxs-lookup"><span data-stu-id="56e29-491">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="56e29-492">string</span><span class="sxs-lookup"><span data-stu-id="56e29-492">string</span></span>|<span data-ttu-id="56e29-493">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-493">128 characters</span></span>||<span data-ttu-id="56e29-494">Cadena descriptiva que describe el propósito de este parámetro.</span><span class="sxs-lookup"><span data-stu-id="56e29-494">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="56e29-495">string</span><span class="sxs-lookup"><span data-stu-id="56e29-495">string</span></span>|<span data-ttu-id="56e29-496">512 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-496">512 characters</span></span>||<span data-ttu-id="56e29-497">Valor inicial del parámetro.</span><span class="sxs-lookup"><span data-stu-id="56e29-497">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="56e29-498">string</span><span class="sxs-lookup"><span data-stu-id="56e29-498">string</span></span>|<span data-ttu-id="56e29-499">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-499">128 characters</span></span>||<span data-ttu-id="56e29-500">Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="56e29-500">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="56e29-501">Uno de `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="56e29-501">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="56e29-502">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="56e29-502">array of objects</span></span>|<span data-ttu-id="56e29-503">10 elementos</span><span class="sxs-lookup"><span data-stu-id="56e29-503">10 items</span></span>||<span data-ttu-id="56e29-504">Las opciones de opción del `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="56e29-504">The choice options for the`choiceset`.</span></span> <span data-ttu-id="56e29-505">Use sólo cuando `parameter.inputType` sea `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="56e29-505">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="56e29-506">string</span><span class="sxs-lookup"><span data-stu-id="56e29-506">string</span></span>|<span data-ttu-id="56e29-507">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-507">128 characters</span></span>|<span data-ttu-id="56e29-508">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-508">✔</span></span>|<span data-ttu-id="56e29-509">Título de la elección.</span><span class="sxs-lookup"><span data-stu-id="56e29-509">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="56e29-510">string</span><span class="sxs-lookup"><span data-stu-id="56e29-510">string</span></span>|<span data-ttu-id="56e29-511">512 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-511">512 characters</span></span>|<span data-ttu-id="56e29-512">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-512">✔</span></span>|<span data-ttu-id="56e29-513">Valor de la elección.</span><span class="sxs-lookup"><span data-stu-id="56e29-513">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="56e29-514">permissions</span><span class="sxs-lookup"><span data-stu-id="56e29-514">permissions</span></span>

<span data-ttu-id="56e29-515">**Opcional** : matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="56e29-515">**Optional** — array of strings</span></span>

<span data-ttu-id="56e29-516">Una matriz de `string` que especifica los permisos que solicita la aplicación, lo que permite a los usuarios finales saber cómo se realizará la extensión.</span><span class="sxs-lookup"><span data-stu-id="56e29-516">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="56e29-517">Las siguientes opciones no son exclusivas:</span><span class="sxs-lookup"><span data-stu-id="56e29-517">The following options are non-exclusive:</span></span>

* <span data-ttu-id="56e29-518">`identity`&emsp;Requiere información de identidad del usuario</span><span class="sxs-lookup"><span data-stu-id="56e29-518">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="56e29-519">`messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="56e29-519">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="56e29-520">Cambiar estos permisos al actualizar la aplicación hará que los usuarios repitan el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="56e29-520">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="56e29-521">Consulte [actualizar la aplicación](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="56e29-521">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="56e29-522">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="56e29-522">devicePermissions</span></span>

<span data-ttu-id="56e29-523">**Opcional** : matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="56e29-523">**Optional** — array of strings</span></span>

<span data-ttu-id="56e29-524">Especifica las características nativas del dispositivo de un usuario al que la aplicación puede solicitar acceso.</span><span class="sxs-lookup"><span data-stu-id="56e29-524">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="56e29-525">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="56e29-525">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="56e29-526">validDomains</span><span class="sxs-lookup"><span data-stu-id="56e29-526">validDomains</span></span>

<span data-ttu-id="56e29-527">**Opcional**, excepto **obligatorio** donde se indica</span><span class="sxs-lookup"><span data-stu-id="56e29-527">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="56e29-528">Una lista de dominios válidos para los sitios web que la aplicación espera que se carguen dentro del cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="56e29-528">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="56e29-529">Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="56e29-529">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="56e29-530">Esto coincide exactamente con un segmento del dominio; Si tiene que hacer coincidir `a.b.example.com` , use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="56e29-530">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="56e29-531">Si la configuración de la pestaña o la interfaz de usuario de contenido debe navegar a cualquier otro dominio además del uso de la configuración de pestañas, dicho dominio debe especificarse aquí.</span><span class="sxs-lookup"><span data-stu-id="56e29-531">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="56e29-532">No obstante, **no** es necesario incluir los dominios de los proveedores de identidades que desea admitir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-532">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="56e29-533">Por ejemplo, para autenticarse con un identificador de Google, es necesario redirigir a accounts.google.com, pero no se debe incluir accounts.google.com en `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="56e29-533">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="56e29-534">Las aplicaciones de Microsoft teams que requieren sus propias direcciones URL de SharePoint para que funcionen correctamente pueden incluir "{teamsitedomain}" en su lista de dominios válidos.</span><span class="sxs-lookup"><span data-stu-id="56e29-534">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56e29-535">No agregue dominios que estén fuera de su control, ya sea directamente o mediante caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="56e29-535">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="56e29-536">Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="56e29-536">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="56e29-537">El objeto es una matriz con todos los elementos del tipo `string` .</span><span class="sxs-lookup"><span data-stu-id="56e29-537">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="56e29-538">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="56e29-538">webApplicationInfo</span></span>

<span data-ttu-id="56e29-539">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="56e29-539">**Optional** — object</span></span>

<span data-ttu-id="56e29-540">Especifique el identificador de aplicación de Azure Active Directory (Azure AD) y la información de Microsoft Graph para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-540">Specify your Azure Active Directory (Azure AD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="56e29-541">Si la aplicación está registrada en Azure AD, debe proporcionar el identificador de la aplicación para que los administradores puedan revisar fácilmente los permisos y conceder el consentimiento en el centro de administración de Teams.</span><span class="sxs-lookup"><span data-stu-id="56e29-541">If your app is registered in Azure AD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="56e29-542">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-542">Name</span></span>| <span data-ttu-id="56e29-543">Tipo</span><span class="sxs-lookup"><span data-stu-id="56e29-543">Type</span></span>| <span data-ttu-id="56e29-544">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-544">Maximum size</span></span> | <span data-ttu-id="56e29-545">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-545">Required</span></span> | <span data-ttu-id="56e29-546">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-546">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="56e29-547">string</span><span class="sxs-lookup"><span data-stu-id="56e29-547">string</span></span>|<span data-ttu-id="56e29-548">36 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-548">36 characters</span></span>|<span data-ttu-id="56e29-549">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-549">✔</span></span>|<span data-ttu-id="56e29-550">Identificador de la aplicación de AAD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56e29-550">AAD application id of the app.</span></span> <span data-ttu-id="56e29-551">Este identificador debe ser un GUID.</span><span class="sxs-lookup"><span data-stu-id="56e29-551">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="56e29-552">string</span><span class="sxs-lookup"><span data-stu-id="56e29-552">string</span></span>|<span data-ttu-id="56e29-553">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-553">2048 characters</span></span>|<span data-ttu-id="56e29-554">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-554">✔</span></span>|<span data-ttu-id="56e29-555">Dirección URL de recurso de la aplicación para adquirir el token de autenticación para el SSO.</span><span class="sxs-lookup"><span data-stu-id="56e29-555">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="56e29-556">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="56e29-556">array of strings</span></span>|<span data-ttu-id="56e29-557">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-557">128 characters</span></span>||<span data-ttu-id="56e29-558">Especificar el [consentimiento específico del recurso](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions) granular</span><span class="sxs-lookup"><span data-stu-id="56e29-558">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="56e29-559">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="56e29-559">showLoadingIndicator</span></span>

<span data-ttu-id="56e29-560">**Opcional** : Boolean</span><span class="sxs-lookup"><span data-stu-id="56e29-560">**Optional** — boolean</span></span>

<span data-ttu-id="56e29-561">Indica si se va a mostrar el indicador de carga cuando se cargue una aplicación o pestaña.</span><span class="sxs-lookup"><span data-stu-id="56e29-561">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="56e29-562">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="56e29-562">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="56e29-563">Si establece "showLoadingIndicator: true" en el manifiesto de la aplicación, para que la página se cargue correctamente, debe modificar las páginas de contenido de sus fichas y módulos de tareas según el protocolo que se describe en [Mostrar un documento de indicador de carga nativo](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) .</span><span class="sxs-lookup"><span data-stu-id="56e29-563">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="56e29-564">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="56e29-564">isFullScreen</span></span>

 <span data-ttu-id="56e29-565">**Opcional** : Boolean</span><span class="sxs-lookup"><span data-stu-id="56e29-565">**Optional** — boolean</span></span>

<span data-ttu-id="56e29-566">Indicar dónde se representa una aplicación personal con o sin una barra de encabezado de pestañas.</span><span class="sxs-lookup"><span data-stu-id="56e29-566">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="56e29-567">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="56e29-567">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="56e29-568">activities</span><span class="sxs-lookup"><span data-stu-id="56e29-568">activities</span></span>

<span data-ttu-id="56e29-569">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="56e29-569">**Optional** — object</span></span>

<span data-ttu-id="56e29-570">Defina las propiedades que usará la aplicación para publicar en una fuente de actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="56e29-570">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="56e29-571">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-571">Name</span></span>| <span data-ttu-id="56e29-572">Tipo</span><span class="sxs-lookup"><span data-stu-id="56e29-572">Type</span></span>| <span data-ttu-id="56e29-573">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-573">Maximum size</span></span> | <span data-ttu-id="56e29-574">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-574">Required</span></span> | <span data-ttu-id="56e29-575">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-575">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="56e29-576">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="56e29-576">array of Objects</span></span>|<span data-ttu-id="56e29-577">de 128 elementos</span><span class="sxs-lookup"><span data-stu-id="56e29-577">128 items</span></span>| | <span data-ttu-id="56e29-578">Especifique los tipos de actividades que la aplicación puede publicar en la fuente de actividades de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="56e29-578">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="56e29-579">Activities. activityTypes</span><span class="sxs-lookup"><span data-stu-id="56e29-579">activities.activityTypes</span></span>

|<span data-ttu-id="56e29-580">Nombre</span><span class="sxs-lookup"><span data-stu-id="56e29-580">Name</span></span>| <span data-ttu-id="56e29-581">Tipo</span><span class="sxs-lookup"><span data-stu-id="56e29-581">Type</span></span>| <span data-ttu-id="56e29-582">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="56e29-582">Maximum size</span></span> | <span data-ttu-id="56e29-583">Necesario</span><span class="sxs-lookup"><span data-stu-id="56e29-583">Required</span></span> | <span data-ttu-id="56e29-584">Descripción</span><span class="sxs-lookup"><span data-stu-id="56e29-584">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="56e29-585">string</span><span class="sxs-lookup"><span data-stu-id="56e29-585">string</span></span>|<span data-ttu-id="56e29-586">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-586">32 characters</span></span>|<span data-ttu-id="56e29-587">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-587">✔</span></span>|<span data-ttu-id="56e29-588">El tipo de notificación.</span><span class="sxs-lookup"><span data-stu-id="56e29-588">The notification type.</span></span> <span data-ttu-id="56e29-589">*Vea a continuación*.</span><span class="sxs-lookup"><span data-stu-id="56e29-589">*See below*.</span></span>|
|`description`|<span data-ttu-id="56e29-590">string</span><span class="sxs-lookup"><span data-stu-id="56e29-590">string</span></span>|<span data-ttu-id="56e29-591">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-591">128 characters</span></span>|<span data-ttu-id="56e29-592">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-592">✔</span></span>|<span data-ttu-id="56e29-593">Una breve descripción de la notificación.</span><span class="sxs-lookup"><span data-stu-id="56e29-593">A brief description of the notification.</span></span> <span data-ttu-id="56e29-594">*Vea a continuación*.</span><span class="sxs-lookup"><span data-stu-id="56e29-594">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="56e29-595">string</span><span class="sxs-lookup"><span data-stu-id="56e29-595">string</span></span>|<span data-ttu-id="56e29-596">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="56e29-596">128 characters</span></span>|<span data-ttu-id="56e29-597">✔</span><span class="sxs-lookup"><span data-stu-id="56e29-597">✔</span></span>|<span data-ttu-id="56e29-598">Ejemplo: "{actor} tarea creada {taskId} para usted"</span><span class="sxs-lookup"><span data-stu-id="56e29-598">Ex: "{actor} created task {taskId} for you"</span></span>|

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
>
>
