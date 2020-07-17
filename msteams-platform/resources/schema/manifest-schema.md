---
title: Referencia de esquema de manifiesto
description: Describe el esquema admitido por el manifiesto para Microsoft Teams.
keywords: esquema del manifiesto de Microsoft Teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: b67b23278a2d2bbb2b24c0e828f01cf1789c6191
ms.sourcegitcommit: bac0226d9048c363d96bbaf6f5395388c5f5c45a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "45039289"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="8a740-104">Referencia: esquema de manifiesto para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8a740-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="8a740-105">El manifiesto de Microsoft Teams describe cómo se integra la aplicación en el producto de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8a740-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="8a740-106">El manifiesto debe cumplir el esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="8a740-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="8a740-107">También se admiten las versiones anteriores 1.0-1.4 (mediante "v1. x" en la dirección URL).</span><span class="sxs-lookup"><span data-stu-id="8a740-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="8a740-108">En el siguiente ejemplo de esquema se muestran todas las opciones de extensibilidad.</span><span class="sxs-lookup"><span data-stu-id="8a740-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="8a740-109">Manifiesto completo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a740-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.7",
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
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": "Define how your tab wil be made available in SharePoint (full page or web part)"
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser"
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

<span data-ttu-id="8a740-110">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="8a740-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="8a740-111">$schema</span><span class="sxs-lookup"><span data-stu-id="8a740-111">$schema</span></span>

<span data-ttu-id="8a740-112">*Opcional, pero recomendado* , String</span><span class="sxs-lookup"><span data-stu-id="8a740-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="8a740-113">La dirección URL de https://que hace referencia al esquema JSON del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="8a740-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="8a740-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="8a740-114">manifestVersion</span></span>

<span data-ttu-id="8a740-115">**Obligatorio** : String</span><span class="sxs-lookup"><span data-stu-id="8a740-115">**Required** — string</span></span>

<span data-ttu-id="8a740-116">La versión del esquema del manifiesto que está usando este manifiesto.</span><span class="sxs-lookup"><span data-stu-id="8a740-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="8a740-117">Debe ser "1,5".</span><span class="sxs-lookup"><span data-stu-id="8a740-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="8a740-118">version</span><span class="sxs-lookup"><span data-stu-id="8a740-118">version</span></span>

<span data-ttu-id="8a740-119">**Obligatorio** : String</span><span class="sxs-lookup"><span data-stu-id="8a740-119">**Required** — string</span></span>

<span data-ttu-id="8a740-120">La versión de la aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="8a740-120">The version of the specific app.</span></span> <span data-ttu-id="8a740-121">Si actualiza algo en el manifiesto, la versión también debe incrementarse.</span><span class="sxs-lookup"><span data-stu-id="8a740-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="8a740-122">De este modo, cuando se instale el nuevo manifiesto, se sobrescribirá el anterior y el usuario podrá disfrutar de las funciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="8a740-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="8a740-123">Si esta aplicación se envió a la tienda, el nuevo manifiesto tendrá que volver a enviarse y a validarse.</span><span class="sxs-lookup"><span data-stu-id="8a740-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="8a740-124">A continuación, los usuarios de esta aplicación recibirán el nuevo manifiesto actualizado automáticamente en unas pocas horas, después de que se apruebe.</span><span class="sxs-lookup"><span data-stu-id="8a740-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="8a740-125">Si la aplicación ha solicitado un cambio de permisos, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="8a740-126">Esta cadena de versión debe seguir el estándar [SemVer](http://semver.org/) (Major. Secundaria. REVISIÓN).</span><span class="sxs-lookup"><span data-stu-id="8a740-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="8a740-127">id</span><span class="sxs-lookup"><span data-stu-id="8a740-127">id</span></span>

<span data-ttu-id="8a740-128">**Obligatorio** : identificador de aplicación de Microsoft</span><span class="sxs-lookup"><span data-stu-id="8a740-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="8a740-129">El identificador único generado por Microsoft para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="8a740-130">Si ha registrado un bot a través de Microsoft bot Framework o la aplicación Web de su pestaña ya inicia sesión en Microsoft, debe tener ya un identificador y escribirlo aquí.</span><span class="sxs-lookup"><span data-stu-id="8a740-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="8a740-131">De lo contrario, debe generar un nuevo identificador en el portal de registro de aplicaciones de Microsoft ([mis aplicaciones](https://apps.dev.microsoft.com)), escribirlo aquí y volver a usarlo cuando agregue un bot. Nota: Si va a enviar una actualización a su aplicación existente en AppSource, el identificador del manifiesto no debe modificarse.</span><span class="sxs-lookup"><span data-stu-id="8a740-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="8a740-132">developer</span><span class="sxs-lookup"><span data-stu-id="8a740-132">developer</span></span>

<span data-ttu-id="8a740-133">**Obligatorio** : Object</span><span class="sxs-lookup"><span data-stu-id="8a740-133">**Required** — object</span></span>

<span data-ttu-id="8a740-134">Especifica información sobre la compañía.</span><span class="sxs-lookup"><span data-stu-id="8a740-134">Specifies information about your company.</span></span> <span data-ttu-id="8a740-135">Para las aplicaciones enviadas a AppSource (anteriormente tienda Office), estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="8a740-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="8a740-136">Consulte nuestras [directrices de publicación](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="8a740-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="8a740-137">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-137">Name</span></span>| <span data-ttu-id="8a740-138">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-138">Maximum size</span></span> | <span data-ttu-id="8a740-139">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-139">Required</span></span> | <span data-ttu-id="8a740-140">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="8a740-141">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-141">32 characters</span></span>|<span data-ttu-id="8a740-142">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-142">✔</span></span>|<span data-ttu-id="8a740-143">El nombre para mostrar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="8a740-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="8a740-144">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-144">2048 characters</span></span>|<span data-ttu-id="8a740-145">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-145">✔</span></span>|<span data-ttu-id="8a740-146">La dirección URL https://al sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="8a740-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="8a740-147">Este vínculo debe llevar a los usuarios a su compañía o a la página de aterrizaje específica del producto.</span><span class="sxs-lookup"><span data-stu-id="8a740-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="8a740-148">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-148">2048 characters</span></span>|<span data-ttu-id="8a740-149">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-149">✔</span></span>|<span data-ttu-id="8a740-150">La dirección URL de https://a la Directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="8a740-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="8a740-151">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-151">2048 characters</span></span>|<span data-ttu-id="8a740-152">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-152">✔</span></span>|<span data-ttu-id="8a740-153">La dirección URL de https://a las condiciones de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="8a740-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="8a740-154">10 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-154">10 characters</span></span>| |<span data-ttu-id="8a740-155">**Opcional** IDENTIFICADOR de red de los socios de Microsoft que identifica la organización asociada que crea la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="8a740-156">name</span><span class="sxs-lookup"><span data-stu-id="8a740-156">name</span></span>

<span data-ttu-id="8a740-157">**Obligatorio** : Object</span><span class="sxs-lookup"><span data-stu-id="8a740-157">**Required** — object</span></span>

<span data-ttu-id="8a740-158">El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8a740-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="8a740-159">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="8a740-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="8a740-160">Los valores de `short` y `full` no deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="8a740-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="8a740-161">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-161">Name</span></span>| <span data-ttu-id="8a740-162">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-162">Maximum size</span></span> | <span data-ttu-id="8a740-163">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-163">Required</span></span> | <span data-ttu-id="8a740-164">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="8a740-165">30 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-165">30 characters</span></span>|<span data-ttu-id="8a740-166">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-166">✔</span></span>|<span data-ttu-id="8a740-167">El nombre para mostrar corto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="8a740-168">100 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-168">100 characters</span></span>||<span data-ttu-id="8a740-169">El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="8a740-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="8a740-170">description</span><span class="sxs-lookup"><span data-stu-id="8a740-170">description</span></span>

<span data-ttu-id="8a740-171">**Obligatorio** : Object</span><span class="sxs-lookup"><span data-stu-id="8a740-171">**Required** — object</span></span>

<span data-ttu-id="8a740-172">Describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8a740-172">Describes your app to users.</span></span> <span data-ttu-id="8a740-173">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="8a740-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="8a740-174">Asegúrese de que la descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia.</span><span class="sxs-lookup"><span data-stu-id="8a740-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="8a740-175">También debe tener en cuenta, en la descripción completa, si se requiere uso de una cuenta externa.</span><span class="sxs-lookup"><span data-stu-id="8a740-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="8a740-176">Los valores de `short` y `full` no deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="8a740-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="8a740-177">La descripción breve no debe repetirse en la descripción larga y no debe incluir ningún otro nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="8a740-178">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-178">Name</span></span>| <span data-ttu-id="8a740-179">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-179">Maximum size</span></span> | <span data-ttu-id="8a740-180">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-180">Required</span></span> | <span data-ttu-id="8a740-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="8a740-182">80 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-182">80 characters</span></span>|<span data-ttu-id="8a740-183">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-183">✔</span></span>|<span data-ttu-id="8a740-184">Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.</span><span class="sxs-lookup"><span data-stu-id="8a740-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="8a740-185">4000 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-185">4000 characters</span></span>|<span data-ttu-id="8a740-186">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-186">✔</span></span>|<span data-ttu-id="8a740-187">La descripción completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="8a740-188">packageName</span><span class="sxs-lookup"><span data-stu-id="8a740-188">packageName</span></span>

<span data-ttu-id="8a740-189">**Opcional** : cadena</span><span class="sxs-lookup"><span data-stu-id="8a740-189">**Optional** — string</span></span>

<span data-ttu-id="8a740-190">Un identificador único para esta aplicación en la notación de dominio inverso; por ejemplo, com. example. myapp.</span><span class="sxs-lookup"><span data-stu-id="8a740-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="8a740-191">Longitud máxima: 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="8a740-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="8a740-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="8a740-192">localizationInfo</span></span>

<span data-ttu-id="8a740-193">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="8a740-193">**Optional** — object</span></span>

<span data-ttu-id="8a740-194">Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="8a740-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="8a740-195">Consulte [localización](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="8a740-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="8a740-196">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-196">Name</span></span>| <span data-ttu-id="8a740-197">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-197">Maximum size</span></span> | <span data-ttu-id="8a740-198">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-198">Required</span></span> | <span data-ttu-id="8a740-199">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="8a740-200">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-200">✔</span></span>|<span data-ttu-id="8a740-201">La etiqueta de idioma de las cadenas en este archivo de manifiesto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="8a740-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="8a740-202">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="8a740-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="8a740-203">Una matriz de objetos que especifica traducciones de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="8a740-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="8a740-204">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-204">Name</span></span>| <span data-ttu-id="8a740-205">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-205">Maximum size</span></span> | <span data-ttu-id="8a740-206">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-206">Required</span></span> | <span data-ttu-id="8a740-207">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="8a740-208">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-208">✔</span></span>|<span data-ttu-id="8a740-209">La etiqueta de idioma de las cadenas en el archivo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="8a740-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="8a740-210">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-210">✔</span></span>|<span data-ttu-id="8a740-211">Una ruta de acceso relativa a un archivo. JSON que contiene las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="8a740-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="8a740-212">iconos</span><span class="sxs-lookup"><span data-stu-id="8a740-212">icons</span></span>

<span data-ttu-id="8a740-213">**Obligatorio** : Object</span><span class="sxs-lookup"><span data-stu-id="8a740-213">**Required** — object</span></span>

<span data-ttu-id="8a740-214">Iconos usados en la aplicación Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8a740-214">Icons used within the Teams app.</span></span> <span data-ttu-id="8a740-215">Los archivos de icono deben incluirse como parte del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="8a740-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="8a740-216">Vea [iconos](~/concepts/build-and-test/apps-package.md#icons) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="8a740-216">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="8a740-217">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-217">Name</span></span>| <span data-ttu-id="8a740-218">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-218">Maximum size</span></span> | <span data-ttu-id="8a740-219">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-219">Required</span></span> | <span data-ttu-id="8a740-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="8a740-221">32 x 32 píxeles</span><span class="sxs-lookup"><span data-stu-id="8a740-221">32 x 32 pixels</span></span>|<span data-ttu-id="8a740-222">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-222">✔</span></span>|<span data-ttu-id="8a740-223">Una ruta de acceso relativa a un icono de esquema PNG transparente de 32x32.</span><span class="sxs-lookup"><span data-stu-id="8a740-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="8a740-224">192 x 192 píxeles</span><span class="sxs-lookup"><span data-stu-id="8a740-224">192 x 192 pixels</span></span>|<span data-ttu-id="8a740-225">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-225">✔</span></span>|<span data-ttu-id="8a740-226">Una ruta de acceso de archivo relativa a un icono PNG 192x192 de color completo.</span><span class="sxs-lookup"><span data-stu-id="8a740-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="8a740-227">accentColor</span><span class="sxs-lookup"><span data-stu-id="8a740-227">accentColor</span></span>

<span data-ttu-id="8a740-228">**Opcional** : código de color hexadecimal HTML</span><span class="sxs-lookup"><span data-stu-id="8a740-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="8a740-229">Color que se va a usar junto con y como fondo de los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="8a740-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="8a740-230">El valor debe ser un código de color HTML válido que empiece por ' # ', por ejemplo `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="8a740-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="8a740-231">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="8a740-231">configurableTabs</span></span>

<span data-ttu-id="8a740-232">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="8a740-232">**Optional** — array</span></span>

<span data-ttu-id="8a740-233">Se usa cuando la experiencia de la aplicación tiene una experiencia de la pestaña de canal de equipo que requiere una configuración adicional antes de que se agregue.</span><span class="sxs-lookup"><span data-stu-id="8a740-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="8a740-234">Las pestañas configurables solo se admiten en el ámbito de Teams (no en personal) y actualmente solo se admite **una** pestaña por aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="8a740-235">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-235">Name</span></span>| <span data-ttu-id="8a740-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a740-236">Type</span></span>| <span data-ttu-id="8a740-237">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-237">Maximum size</span></span> | <span data-ttu-id="8a740-238">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-238">Required</span></span> | <span data-ttu-id="8a740-239">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="8a740-240">string</span><span class="sxs-lookup"><span data-stu-id="8a740-240">string</span></span>|<span data-ttu-id="8a740-241">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-241">2048 characters</span></span>|<span data-ttu-id="8a740-242">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-242">✔</span></span>|<span data-ttu-id="8a740-243">Dirección URL de https://que se va a usar al configurar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="8a740-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="8a740-244">matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="8a740-244">array of enum</span></span>|<span data-ttu-id="8a740-245">1 </span><span class="sxs-lookup"><span data-stu-id="8a740-245">1</span></span>|<span data-ttu-id="8a740-246">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-246">✔</span></span>|<span data-ttu-id="8a740-247">Actualmente, las pestañas configurables solo admiten los `team` `groupchat` ámbitos y.</span><span class="sxs-lookup"><span data-stu-id="8a740-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="8a740-248">boolean</span><span class="sxs-lookup"><span data-stu-id="8a740-248">boolean</span></span>|||<span data-ttu-id="8a740-249">Un valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de crearla.</span><span class="sxs-lookup"><span data-stu-id="8a740-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="8a740-250">Valor predeterminado: **true**.</span><span class="sxs-lookup"><span data-stu-id="8a740-250">Default: **true**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="8a740-251">string</span><span class="sxs-lookup"><span data-stu-id="8a740-251">string</span></span>|<span data-ttu-id="8a740-252">2048</span><span class="sxs-lookup"><span data-stu-id="8a740-252">2048</span></span>||<span data-ttu-id="8a740-253">Una ruta de acceso de archivo relativa a una imagen de vista previa de pestaña para su uso en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8a740-253">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="8a740-254">Tamaño 1024x768.</span><span class="sxs-lookup"><span data-stu-id="8a740-254">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="8a740-255">matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="8a740-255">array of enum</span></span>|<span data-ttu-id="8a740-256">1 </span><span class="sxs-lookup"><span data-stu-id="8a740-256">1</span></span>||<span data-ttu-id="8a740-257">Define cómo estará disponible la pestaña en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8a740-257">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="8a740-258">Las opciones son `sharePointFullPage` y`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="8a740-258">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="8a740-259">staticTabs</span><span class="sxs-lookup"><span data-stu-id="8a740-259">staticTabs</span></span>

<span data-ttu-id="8a740-260">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="8a740-260">**Optional** — array</span></span>

<span data-ttu-id="8a740-261">Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente.</span><span class="sxs-lookup"><span data-stu-id="8a740-261">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="8a740-262">Las pestañas estáticas declaradas en `personal` el ámbito siempre están ancladas a la experiencia personal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-262">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="8a740-263">Actualmente no se admiten las pestañas estáticas declaradas en el `team` ámbito.</span><span class="sxs-lookup"><span data-stu-id="8a740-263">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="8a740-264">Este elemento es una matriz (un máximo de 16 elementos) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="8a740-264">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="8a740-265">Este bloque solo es necesario para las soluciones que proporcionan una solución de pestaña estática.</span><span class="sxs-lookup"><span data-stu-id="8a740-265">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="8a740-266">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-266">Name</span></span>| <span data-ttu-id="8a740-267">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a740-267">Type</span></span>| <span data-ttu-id="8a740-268">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-268">Maximum size</span></span> | <span data-ttu-id="8a740-269">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-269">Required</span></span> | <span data-ttu-id="8a740-270">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-270">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="8a740-271">string</span><span class="sxs-lookup"><span data-stu-id="8a740-271">string</span></span>|<span data-ttu-id="8a740-272">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-272">64 characters</span></span>|<span data-ttu-id="8a740-273">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-273">✔</span></span>|<span data-ttu-id="8a740-274">Un identificador único para la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="8a740-274">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="8a740-275">string</span><span class="sxs-lookup"><span data-stu-id="8a740-275">string</span></span>|<span data-ttu-id="8a740-276">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-276">128 characters</span></span>|<span data-ttu-id="8a740-277">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-277">✔</span></span>|<span data-ttu-id="8a740-278">El nombre para mostrar de la pestaña en la interfaz de canal.</span><span class="sxs-lookup"><span data-stu-id="8a740-278">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="8a740-279">string</span><span class="sxs-lookup"><span data-stu-id="8a740-279">string</span></span>|<span data-ttu-id="8a740-280">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-280">2048 characters</span></span>|<span data-ttu-id="8a740-281">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-281">✔</span></span>|<span data-ttu-id="8a740-282">Dirección URL de https://que señala a la interfaz de usuario de la entidad que se va a mostrar en el lienzo de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8a740-282">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="8a740-283">string</span><span class="sxs-lookup"><span data-stu-id="8a740-283">string</span></span>|<span data-ttu-id="8a740-284">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-284">2048 characters</span></span>||<span data-ttu-id="8a740-285">La dirección URL de https://para apuntar a si un usuario opta por verlo en un explorador.</span><span class="sxs-lookup"><span data-stu-id="8a740-285">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="8a740-286">matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="8a740-286">array of enum</span></span>|<span data-ttu-id="8a740-287">1 </span><span class="sxs-lookup"><span data-stu-id="8a740-287">1</span></span>|<span data-ttu-id="8a740-288">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-288">✔</span></span>|<span data-ttu-id="8a740-289">Actualmente, las pestañas estáticas solo admiten el `personal` ámbito, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.</span><span class="sxs-lookup"><span data-stu-id="8a740-289">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

> [!NOTE]
> <span data-ttu-id="8a740-290">Si las pestañas requieren información dependiente del contexto para mostrar contenido relevante o para iniciar un flujo de autenticación, *vea* [obtener contexto para la pestaña de Microsoft Teams](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="8a740-290">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="8a740-291">transferido</span><span class="sxs-lookup"><span data-stu-id="8a740-291">bots</span></span>

<span data-ttu-id="8a740-292">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="8a740-292">**Optional** — array</span></span>

<span data-ttu-id="8a740-293">Define una solución de bot, junto con información opcional como propiedades de comando predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="8a740-293">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="8a740-294">El elemento es una matriz (un máximo solo de un elemento, &mdash; actualmente solo se permite un bot por aplicación) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="8a740-294">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="8a740-295">Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.</span><span class="sxs-lookup"><span data-stu-id="8a740-295">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="8a740-296">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-296">Name</span></span>| <span data-ttu-id="8a740-297">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a740-297">Type</span></span>| <span data-ttu-id="8a740-298">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-298">Maximum size</span></span> | <span data-ttu-id="8a740-299">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-299">Required</span></span> | <span data-ttu-id="8a740-300">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-300">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="8a740-301">string</span><span class="sxs-lookup"><span data-stu-id="8a740-301">string</span></span>|<span data-ttu-id="8a740-302">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-302">64 characters</span></span>|<span data-ttu-id="8a740-303">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-303">✔</span></span>|<span data-ttu-id="8a740-304">El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="8a740-304">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="8a740-305">Puede ser el mismo que el [identificador de aplicación](#id)general.</span><span class="sxs-lookup"><span data-stu-id="8a740-305">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="8a740-306">matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="8a740-306">array of enum</span></span>|<span data-ttu-id="8a740-307">3 </span><span class="sxs-lookup"><span data-stu-id="8a740-307">3</span></span>|<span data-ttu-id="8a740-308">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-308">✔</span></span>|<span data-ttu-id="8a740-309">Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`).</span><span class="sxs-lookup"><span data-stu-id="8a740-309">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="8a740-310">Estas opciones no son exclusivas.</span><span class="sxs-lookup"><span data-stu-id="8a740-310">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="8a740-311">boolean</span><span class="sxs-lookup"><span data-stu-id="8a740-311">boolean</span></span>|||<span data-ttu-id="8a740-312">Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico.</span><span class="sxs-lookup"><span data-stu-id="8a740-312">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="8a740-313">Predeterminada**`false`**</span><span class="sxs-lookup"><span data-stu-id="8a740-313">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="8a740-314">boolean</span><span class="sxs-lookup"><span data-stu-id="8a740-314">boolean</span></span>|||<span data-ttu-id="8a740-315">Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación.</span><span class="sxs-lookup"><span data-stu-id="8a740-315">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="8a740-316">Predeterminada`**false**`</span><span class="sxs-lookup"><span data-stu-id="8a740-316">Default: `**false**`</span></span>|
|`supportsFiles`|<span data-ttu-id="8a740-317">boolean</span><span class="sxs-lookup"><span data-stu-id="8a740-317">boolean</span></span>|||<span data-ttu-id="8a740-318">Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal.</span><span class="sxs-lookup"><span data-stu-id="8a740-318">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="8a740-319">Predeterminada**`false`**</span><span class="sxs-lookup"><span data-stu-id="8a740-319">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="8a740-320">bots. commandLists</span><span class="sxs-lookup"><span data-stu-id="8a740-320">bots.commandLists</span></span>

<span data-ttu-id="8a740-321">Una lista opcional de comandos que el bot puede recomendar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8a740-321">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="8a740-322">El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo `object` ; debe definir una lista de comandos independiente para cada ámbito que admita el bot.</span><span class="sxs-lookup"><span data-stu-id="8a740-322">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="8a740-323">Consulte [menús de bot](~/bots/how-to/create-a-bot-commands-menu.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="8a740-323">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="8a740-324">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-324">Name</span></span>| <span data-ttu-id="8a740-325">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a740-325">Type</span></span>| <span data-ttu-id="8a740-326">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-326">Maximum size</span></span> | <span data-ttu-id="8a740-327">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-327">Required</span></span> | <span data-ttu-id="8a740-328">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-328">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="8a740-329">matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="8a740-329">array of enum</span></span>|<span data-ttu-id="8a740-330">3 </span><span class="sxs-lookup"><span data-stu-id="8a740-330">3</span></span>|<span data-ttu-id="8a740-331">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-331">✔</span></span>|<span data-ttu-id="8a740-332">Especifica el ámbito para el que la lista de comandos es válida.</span><span class="sxs-lookup"><span data-stu-id="8a740-332">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="8a740-333">Las opciones son `team`, `personal` y `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="8a740-333">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="8a740-334">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="8a740-334">array of objects</span></span>|<span data-ttu-id="8a740-335">10 </span><span class="sxs-lookup"><span data-stu-id="8a740-335">10</span></span>|<span data-ttu-id="8a740-336">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-336">✔</span></span>|<span data-ttu-id="8a740-337">Una matriz de comandos que el bot admite:</span><span class="sxs-lookup"><span data-stu-id="8a740-337">An array of commands the bot supports:</span></span><br><span data-ttu-id="8a740-338">`title`: el nombre de comando del bot (cadena, 32)</span><span class="sxs-lookup"><span data-stu-id="8a740-338">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="8a740-339">`description`: una descripción o un ejemplo sencillo de la sintaxis del comando y su argumento (cadena, 128).</span><span class="sxs-lookup"><span data-stu-id="8a740-339">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="8a740-340">bots. commandLists. Commands</span><span class="sxs-lookup"><span data-stu-id="8a740-340">bots.commandLists.commands</span></span>

|<span data-ttu-id="8a740-341">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-341">Name</span></span>| <span data-ttu-id="8a740-342">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a740-342">Type</span></span>| <span data-ttu-id="8a740-343">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-343">Maximum size</span></span> | <span data-ttu-id="8a740-344">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-344">Required</span></span> | <span data-ttu-id="8a740-345">Description</span><span class="sxs-lookup"><span data-stu-id="8a740-345">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="8a740-346">title</span><span class="sxs-lookup"><span data-stu-id="8a740-346">title</span></span>|<span data-ttu-id="8a740-347">string</span><span class="sxs-lookup"><span data-stu-id="8a740-347">string</span></span>|<span data-ttu-id="8a740-348">12 </span><span class="sxs-lookup"><span data-stu-id="8a740-348">12</span></span>|<span data-ttu-id="8a740-349">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-349">✔</span></span>|<span data-ttu-id="8a740-350">El nombre del comando bot</span><span class="sxs-lookup"><span data-stu-id="8a740-350">The bot command name</span></span>|
|<span data-ttu-id="8a740-351">description</span><span class="sxs-lookup"><span data-stu-id="8a740-351">description</span></span>|<span data-ttu-id="8a740-352">cadena</span><span class="sxs-lookup"><span data-stu-id="8a740-352">string</span></span>|<span data-ttu-id="8a740-353">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-353">128 characters</span></span>|<span data-ttu-id="8a740-354">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-354">✔</span></span>|<span data-ttu-id="8a740-355">Una descripción de texto simple o un ejemplo de la sintaxis del comando y sus argumentos.</span><span class="sxs-lookup"><span data-stu-id="8a740-355">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="8a740-356">Connector</span><span class="sxs-lookup"><span data-stu-id="8a740-356">connectors</span></span>

<span data-ttu-id="8a740-357">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="8a740-357">**Optional** — array</span></span>

<span data-ttu-id="8a740-358">El `connectors` bloque define un conector de Office 365 para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-358">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="8a740-359">El objeto es una matriz (un máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="8a740-359">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="8a740-360">Este bloque solo es necesario para las soluciones que proporcionan un conector.</span><span class="sxs-lookup"><span data-stu-id="8a740-360">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="8a740-361">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-361">Name</span></span>| <span data-ttu-id="8a740-362">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a740-362">Type</span></span>| <span data-ttu-id="8a740-363">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-363">Maximum size</span></span> | <span data-ttu-id="8a740-364">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-364">Required</span></span> | <span data-ttu-id="8a740-365">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-365">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="8a740-366">string</span><span class="sxs-lookup"><span data-stu-id="8a740-366">string</span></span>|<span data-ttu-id="8a740-367">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-367">2048 characters</span></span>|<span data-ttu-id="8a740-368">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-368">✔</span></span>|<span data-ttu-id="8a740-369">Dirección URL de https://que se va a usar al configurar el conector.</span><span class="sxs-lookup"><span data-stu-id="8a740-369">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="8a740-370">matriz de enumeración</span><span class="sxs-lookup"><span data-stu-id="8a740-370">array of enum</span></span>|<span data-ttu-id="8a740-371">1 </span><span class="sxs-lookup"><span data-stu-id="8a740-371">1</span></span>|<span data-ttu-id="8a740-372">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-372">✔</span></span>|<span data-ttu-id="8a740-373">Especifica si el conector ofrece una experiencia en el contexto de un canal en un `team` o una experiencia en el ámbito de un solo usuario individual ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="8a740-373">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="8a740-374">Actualmente, solo `team` se admite el ámbito.</span><span class="sxs-lookup"><span data-stu-id="8a740-374">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="8a740-375">string</span><span class="sxs-lookup"><span data-stu-id="8a740-375">string</span></span>|<span data-ttu-id="8a740-376">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-376">64 characters</span></span>|<span data-ttu-id="8a740-377">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-377">✔</span></span>|<span data-ttu-id="8a740-378">Un identificador único para el conector que coincide con su identificador en el [panel del programador de conectores](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="8a740-378">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="8a740-379">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="8a740-379">composeExtensions</span></span>

<span data-ttu-id="8a740-380">**Opcional** : matriz</span><span class="sxs-lookup"><span data-stu-id="8a740-380">**Optional** — array</span></span>

<span data-ttu-id="8a740-381">Define una extensión de mensajería para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-381">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="8a740-382">El nombre de la característica se cambió de "redactar extensión" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="8a740-382">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="8a740-383">El elemento es una matriz (un máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="8a740-383">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="8a740-384">Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8a740-384">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="8a740-385">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-385">Name</span></span>| <span data-ttu-id="8a740-386">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a740-386">Type</span></span> | <span data-ttu-id="8a740-387">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-387">Maximum Size</span></span> | <span data-ttu-id="8a740-388">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8a740-388">Required</span></span> | <span data-ttu-id="8a740-389">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-389">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="8a740-390">string</span><span class="sxs-lookup"><span data-stu-id="8a740-390">string</span></span>|<span data-ttu-id="8a740-391">64</span><span class="sxs-lookup"><span data-stu-id="8a740-391">64</span></span>|<span data-ttu-id="8a740-392">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-392">✔</span></span>|<span data-ttu-id="8a740-393">IDENTIFICADOR único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, tal como se registró con bot Framework.</span><span class="sxs-lookup"><span data-stu-id="8a740-393">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="8a740-394">Puede ser el mismo que el identificador de aplicación general.</span><span class="sxs-lookup"><span data-stu-id="8a740-394">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="8a740-395">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="8a740-395">array of objects</span></span>|<span data-ttu-id="8a740-396">10 </span><span class="sxs-lookup"><span data-stu-id="8a740-396">10</span></span>|<span data-ttu-id="8a740-397">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-397">✔</span></span>|<span data-ttu-id="8a740-398">matriz de comandos que admite la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="8a740-398">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="8a740-399">boolean</span><span class="sxs-lookup"><span data-stu-id="8a740-399">boolean</span></span>|||<span data-ttu-id="8a740-400">Un valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8a740-400">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="8a740-401">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="8a740-401">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="8a740-402">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="8a740-402">array of Objects</span></span>|<span data-ttu-id="8a740-403">5 </span><span class="sxs-lookup"><span data-stu-id="8a740-403">5</span></span>||<span data-ttu-id="8a740-404">Una lista de controladores que permiten invocar las aplicaciones cuando se cumplen ciertas condiciones.</span><span class="sxs-lookup"><span data-stu-id="8a740-404">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="8a740-405">Los dominios también deben aparecer en`validDomains`</span><span class="sxs-lookup"><span data-stu-id="8a740-405">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="8a740-406">string</span><span class="sxs-lookup"><span data-stu-id="8a740-406">string</span></span>|||<span data-ttu-id="8a740-407">El tipo de controlador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="8a740-407">The type of message handler.</span></span> <span data-ttu-id="8a740-408">Debe ser `"link"`.</span><span class="sxs-lookup"><span data-stu-id="8a740-408">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="8a740-409">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="8a740-409">array of Strings</span></span>|||<span data-ttu-id="8a740-410">matriz de dominios para los que el controlador de mensajes de vínculo puede registrarse.</span><span class="sxs-lookup"><span data-stu-id="8a740-410">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="8a740-411">composeExtensions. Commands</span><span class="sxs-lookup"><span data-stu-id="8a740-411">composeExtensions.commands</span></span>

<span data-ttu-id="8a740-412">La extensión de mensajería debe declarar uno o más comandos.</span><span class="sxs-lookup"><span data-stu-id="8a740-412">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="8a740-413">Cada comando aparece en Microsoft Teams como una posible interacción desde el punto de entrada basado en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="8a740-413">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="8a740-414">Hay un máximo de 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="8a740-414">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="8a740-415">Cada elemento de comando es un objeto con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="8a740-415">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="8a740-416">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-416">Name</span></span>| <span data-ttu-id="8a740-417">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a740-417">Type</span></span>| <span data-ttu-id="8a740-418">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-418">Maximum size</span></span> | <span data-ttu-id="8a740-419">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-419">Required</span></span> | <span data-ttu-id="8a740-420">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-420">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="8a740-421">string</span><span class="sxs-lookup"><span data-stu-id="8a740-421">string</span></span>|<span data-ttu-id="8a740-422">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-422">64 characters</span></span>|<span data-ttu-id="8a740-423">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-423">✔</span></span>|<span data-ttu-id="8a740-424">IDENTIFICADOR del comando.</span><span class="sxs-lookup"><span data-stu-id="8a740-424">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="8a740-425">string</span><span class="sxs-lookup"><span data-stu-id="8a740-425">string</span></span>|<span data-ttu-id="8a740-426">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-426">32 characters</span></span>|<span data-ttu-id="8a740-427">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-427">✔</span></span>|<span data-ttu-id="8a740-428">Nombre de comando fácil de tener.</span><span class="sxs-lookup"><span data-stu-id="8a740-428">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="8a740-429">string</span><span class="sxs-lookup"><span data-stu-id="8a740-429">string</span></span>|<span data-ttu-id="8a740-430">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-430">64 characters</span></span>||<span data-ttu-id="8a740-431">Tipo del comando.</span><span class="sxs-lookup"><span data-stu-id="8a740-431">Type of the command.</span></span> <span data-ttu-id="8a740-432">Uno de `query` o `action` .</span><span class="sxs-lookup"><span data-stu-id="8a740-432">One of `query` or `action`.</span></span> <span data-ttu-id="8a740-433">Valor predeterminado: **consulta**.</span><span class="sxs-lookup"><span data-stu-id="8a740-433">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="8a740-434">string</span><span class="sxs-lookup"><span data-stu-id="8a740-434">string</span></span>|<span data-ttu-id="8a740-435">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-435">128 characters</span></span>||<span data-ttu-id="8a740-436">La descripción que se muestra a los usuarios para indicar el propósito de este comando.</span><span class="sxs-lookup"><span data-stu-id="8a740-436">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="8a740-437">boolean</span><span class="sxs-lookup"><span data-stu-id="8a740-437">boolean</span></span>|||<span data-ttu-id="8a740-438">Un valor booleano que indica si el comando se debe ejecutar inicialmente sin ningún parámetro.</span><span class="sxs-lookup"><span data-stu-id="8a740-438">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="8a740-439">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="8a740-439">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="8a740-440">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="8a740-440">array of Strings</span></span>|<span data-ttu-id="8a740-441">3 </span><span class="sxs-lookup"><span data-stu-id="8a740-441">3</span></span>||<span data-ttu-id="8a740-442">Define desde dónde se puede invocar la extensión de mensajes.</span><span class="sxs-lookup"><span data-stu-id="8a740-442">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="8a740-443">Cualquier combinación de `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="8a740-443">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="8a740-444">El valor predeterminado es `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="8a740-444">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="8a740-445">boolean</span><span class="sxs-lookup"><span data-stu-id="8a740-445">boolean</span></span>|||<span data-ttu-id="8a740-446">Un valor booleano que indica si debe recuperar el módulo de tarea de forma dinámica.</span><span class="sxs-lookup"><span data-stu-id="8a740-446">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="8a740-447">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="8a740-447">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="8a740-448">object</span><span class="sxs-lookup"><span data-stu-id="8a740-448">object</span></span>|||<span data-ttu-id="8a740-449">Especifique el módulo de tarea que se cargará previamente cuando se use un comando de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8a740-449">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="8a740-450">string</span><span class="sxs-lookup"><span data-stu-id="8a740-450">string</span></span>|<span data-ttu-id="8a740-451">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-451">64 characters</span></span>||<span data-ttu-id="8a740-452">Título del cuadro de diálogo inicial.</span><span class="sxs-lookup"><span data-stu-id="8a740-452">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="8a740-453">string</span><span class="sxs-lookup"><span data-stu-id="8a740-453">string</span></span>|||<span data-ttu-id="8a740-454">Ancho del cuadro de diálogo, ya sea un número en píxeles o un diseño predeterminado, como "Large", "Medium" o "Small".</span><span class="sxs-lookup"><span data-stu-id="8a740-454">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="8a740-455">string</span><span class="sxs-lookup"><span data-stu-id="8a740-455">string</span></span>|||<span data-ttu-id="8a740-456">Alto del cuadro de diálogo: número en píxeles o diseño predeterminado, como "Large", "Medium" o "Small".</span><span class="sxs-lookup"><span data-stu-id="8a740-456">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="8a740-457">string</span><span class="sxs-lookup"><span data-stu-id="8a740-457">string</span></span>|||<span data-ttu-id="8a740-458">Dirección URL de la WebView inicial.</span><span class="sxs-lookup"><span data-stu-id="8a740-458">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="8a740-459">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="8a740-459">array of object</span></span>|<span data-ttu-id="8a740-460">5 elementos</span><span class="sxs-lookup"><span data-stu-id="8a740-460">5 items</span></span>|<span data-ttu-id="8a740-461">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-461">✔</span></span>|<span data-ttu-id="8a740-462">La lista de parámetros que toma el comando.</span><span class="sxs-lookup"><span data-stu-id="8a740-462">The list of parameters the command takes.</span></span> <span data-ttu-id="8a740-463">Mínimo: 1; máximo: 5.</span><span class="sxs-lookup"><span data-stu-id="8a740-463">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="8a740-464">string</span><span class="sxs-lookup"><span data-stu-id="8a740-464">string</span></span>|<span data-ttu-id="8a740-465">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-465">64 characters</span></span>|<span data-ttu-id="8a740-466">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-466">✔</span></span>|<span data-ttu-id="8a740-467">El nombre del parámetro tal y como aparece en el cliente.</span><span class="sxs-lookup"><span data-stu-id="8a740-467">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="8a740-468">Se incluye en la solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="8a740-468">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="8a740-469">string</span><span class="sxs-lookup"><span data-stu-id="8a740-469">string</span></span>|<span data-ttu-id="8a740-470">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-470">32 characters</span></span>|<span data-ttu-id="8a740-471">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-471">✔</span></span>|<span data-ttu-id="8a740-472">Título descriptivo del parámetro.</span><span class="sxs-lookup"><span data-stu-id="8a740-472">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="8a740-473">string</span><span class="sxs-lookup"><span data-stu-id="8a740-473">string</span></span>|<span data-ttu-id="8a740-474">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-474">128 characters</span></span>||<span data-ttu-id="8a740-475">Cadena descriptiva que describe el propósito de este parámetro.</span><span class="sxs-lookup"><span data-stu-id="8a740-475">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="8a740-476">string</span><span class="sxs-lookup"><span data-stu-id="8a740-476">string</span></span>|<span data-ttu-id="8a740-477">512 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-477">512 characters</span></span>||<span data-ttu-id="8a740-478">Valor inicial del parámetro.</span><span class="sxs-lookup"><span data-stu-id="8a740-478">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="8a740-479">string</span><span class="sxs-lookup"><span data-stu-id="8a740-479">string</span></span>|<span data-ttu-id="8a740-480">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-480">128 characters</span></span>||<span data-ttu-id="8a740-481">Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="8a740-481">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="8a740-482">Uno de `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="8a740-482">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="8a740-483">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="8a740-483">array of objects</span></span>|<span data-ttu-id="8a740-484">10 elementos</span><span class="sxs-lookup"><span data-stu-id="8a740-484">10 items</span></span>||<span data-ttu-id="8a740-485">Las opciones de opción del `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="8a740-485">The choice options for the`choiceset`.</span></span> <span data-ttu-id="8a740-486">Use sólo cuando `parameter.inputType` sea `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="8a740-486">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="8a740-487">string</span><span class="sxs-lookup"><span data-stu-id="8a740-487">string</span></span>|<span data-ttu-id="8a740-488">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-488">128 characters</span></span>|<span data-ttu-id="8a740-489">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-489">✔</span></span>|<span data-ttu-id="8a740-490">Título de la elección.</span><span class="sxs-lookup"><span data-stu-id="8a740-490">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="8a740-491">string</span><span class="sxs-lookup"><span data-stu-id="8a740-491">string</span></span>|<span data-ttu-id="8a740-492">512 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-492">512 characters</span></span>|<span data-ttu-id="8a740-493">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-493">✔</span></span>|<span data-ttu-id="8a740-494">Valor de la elección.</span><span class="sxs-lookup"><span data-stu-id="8a740-494">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="8a740-495">permissions</span><span class="sxs-lookup"><span data-stu-id="8a740-495">permissions</span></span>

<span data-ttu-id="8a740-496">**Opcional** : matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="8a740-496">**Optional** — array of strings</span></span>

<span data-ttu-id="8a740-497">Una matriz de `string` que especifica los permisos que solicita la aplicación, lo que permite a los usuarios finales saber cómo se realizará la extensión.</span><span class="sxs-lookup"><span data-stu-id="8a740-497">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="8a740-498">Las siguientes opciones no son exclusivas:</span><span class="sxs-lookup"><span data-stu-id="8a740-498">The following options are non-exclusive:</span></span>

* <span data-ttu-id="8a740-499">`identity`&emsp;Requiere información de identidad del usuario</span><span class="sxs-lookup"><span data-stu-id="8a740-499">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="8a740-500">`messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="8a740-500">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="8a740-501">Cambiar estos permisos al actualizar la aplicación hará que los usuarios repitan el proceso de consentimiento la primera vez que ejecuten la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="8a740-501">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="8a740-502">Consulte [actualizar la aplicación](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="8a740-502">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="8a740-503">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="8a740-503">devicePermissions</span></span>

<span data-ttu-id="8a740-504">**Opcional** : matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="8a740-504">**Optional** — array of strings</span></span>

<span data-ttu-id="8a740-505">Especifica las características nativas del dispositivo de un usuario al que la aplicación puede solicitar acceso.</span><span class="sxs-lookup"><span data-stu-id="8a740-505">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="8a740-506">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="8a740-506">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="8a740-507">validDomains</span><span class="sxs-lookup"><span data-stu-id="8a740-507">validDomains</span></span>

<span data-ttu-id="8a740-508">**Opcional**, excepto **obligatorio** donde se indica</span><span class="sxs-lookup"><span data-stu-id="8a740-508">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="8a740-509">Una lista de dominios válidos para los sitios web que la aplicación espera que se carguen dentro del cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="8a740-509">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="8a740-510">Las listas de dominios pueden incluir caracteres comodín, por ejemplo `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="8a740-510">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="8a740-511">Esto coincide exactamente con un segmento del dominio; Si tiene que hacer coincidir `a.b.example.com` , use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="8a740-511">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="8a740-512">Si la configuración de la pestaña o la interfaz de usuario de contenido debe navegar a cualquier otro dominio además del uso de la configuración de pestañas, dicho dominio debe especificarse aquí.</span><span class="sxs-lookup"><span data-stu-id="8a740-512">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="8a740-513">No obstante, **no** es necesario incluir los dominios de los proveedores de identidades que desea admitir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-513">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="8a740-514">Por ejemplo, para autenticarse con un identificador de Google, es necesario redirigir a accounts.google.com, pero no se debe incluir accounts.google.com en `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="8a740-514">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="8a740-515">Las aplicaciones de Microsoft teams que requieren sus propias direcciones URL de SharePoint para que funcionen correctamente pueden incluir "{teamsitedomain}" en su lista de dominios válidos.</span><span class="sxs-lookup"><span data-stu-id="8a740-515">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a740-516">No agregue dominios que estén fuera de su control, ya sea directamente o mediante caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="8a740-516">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="8a740-517">Por ejemplo, `yourapp.onmicrosoft.com` es válido, pero `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="8a740-517">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="8a740-518">El objeto es una matriz con todos los elementos del tipo `string` .</span><span class="sxs-lookup"><span data-stu-id="8a740-518">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="8a740-519">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="8a740-519">webApplicationInfo</span></span>

<span data-ttu-id="8a740-520">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="8a740-520">**Optional** — object</span></span>

<span data-ttu-id="8a740-521">Especifique la información del grafo y el identificador de la aplicación de AAD para ayudar a los usuarios a iniciar sesión sin problemas en su aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="8a740-521">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="8a740-522">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-522">Name</span></span>| <span data-ttu-id="8a740-523">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a740-523">Type</span></span>| <span data-ttu-id="8a740-524">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-524">Maximum size</span></span> | <span data-ttu-id="8a740-525">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-525">Required</span></span> | <span data-ttu-id="8a740-526">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-526">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="8a740-527">string</span><span class="sxs-lookup"><span data-stu-id="8a740-527">string</span></span>|<span data-ttu-id="8a740-528">36 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-528">36 characters</span></span>|<span data-ttu-id="8a740-529">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-529">✔</span></span>|<span data-ttu-id="8a740-530">Identificador de la aplicación de AAD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a740-530">AAD application id of the app.</span></span> <span data-ttu-id="8a740-531">Este identificador debe ser un GUID.</span><span class="sxs-lookup"><span data-stu-id="8a740-531">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="8a740-532">string</span><span class="sxs-lookup"><span data-stu-id="8a740-532">string</span></span>|<span data-ttu-id="8a740-533">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-533">2048 characters</span></span>||<span data-ttu-id="8a740-534">Dirección URL de recurso de la aplicación para adquirir el token de autenticación para el SSO.</span><span class="sxs-lookup"><span data-stu-id="8a740-534">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="8a740-535">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="8a740-535">array of strings</span></span>|<span data-ttu-id="8a740-536">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-536">128 characters</span></span>||<span data-ttu-id="8a740-537">Especificar el [consentimiento específico del recurso](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions) granular</span><span class="sxs-lookup"><span data-stu-id="8a740-537">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="8a740-538">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="8a740-538">showLoadingIndicator</span></span>

<span data-ttu-id="8a740-539">**Opcional** : Boolean</span><span class="sxs-lookup"><span data-stu-id="8a740-539">**Optional** — boolean</span></span>

<span data-ttu-id="8a740-540">Indica dónde mostrar o no el indicador de carga cuando se carga una aplicación o pestaña.</span><span class="sxs-lookup"><span data-stu-id="8a740-540">Indicate where or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="8a740-541">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="8a740-541">Default: **false**.</span></span>

## <a name="isfullscreen"></a><span data-ttu-id="8a740-542">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="8a740-542">isFullScreen</span></span>

 <span data-ttu-id="8a740-543">**Opcional** : Boolean</span><span class="sxs-lookup"><span data-stu-id="8a740-543">**Optional** — boolean</span></span>

<span data-ttu-id="8a740-544">Indicar dónde se representa una aplicación personal con o sin una barra de encabezado de pestañas.</span><span class="sxs-lookup"><span data-stu-id="8a740-544">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="8a740-545">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="8a740-545">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="8a740-546">activities</span><span class="sxs-lookup"><span data-stu-id="8a740-546">activities</span></span>

<span data-ttu-id="8a740-547">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="8a740-547">**Optional** — object</span></span>

<span data-ttu-id="8a740-548">Defina las propiedades que usará la aplicación para publicar en una fuente de actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="8a740-548">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="8a740-549">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-549">Name</span></span>| <span data-ttu-id="8a740-550">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a740-550">Type</span></span>| <span data-ttu-id="8a740-551">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-551">Maximum size</span></span> | <span data-ttu-id="8a740-552">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-552">Required</span></span> | <span data-ttu-id="8a740-553">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-553">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="8a740-554">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="8a740-554">array of Objects</span></span>|<span data-ttu-id="8a740-555">de 128 elementos</span><span class="sxs-lookup"><span data-stu-id="8a740-555">128 items</span></span>| | <span data-ttu-id="8a740-556">Especifique los tipos de actividades que la aplicación puede publicar en la fuente de actividades de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8a740-556">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="8a740-557">Activities. activityTypes</span><span class="sxs-lookup"><span data-stu-id="8a740-557">activities.activityTypes</span></span>

|<span data-ttu-id="8a740-558">Nombre</span><span class="sxs-lookup"><span data-stu-id="8a740-558">Name</span></span>| <span data-ttu-id="8a740-559">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a740-559">Type</span></span>| <span data-ttu-id="8a740-560">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="8a740-560">Maximum size</span></span> | <span data-ttu-id="8a740-561">Necesario</span><span class="sxs-lookup"><span data-stu-id="8a740-561">Required</span></span> | <span data-ttu-id="8a740-562">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a740-562">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="8a740-563">string</span><span class="sxs-lookup"><span data-stu-id="8a740-563">string</span></span>|<span data-ttu-id="8a740-564">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-564">32 characters</span></span>|<span data-ttu-id="8a740-565">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-565">✔</span></span>|<span data-ttu-id="8a740-566">El tipo de notificación.</span><span class="sxs-lookup"><span data-stu-id="8a740-566">The notification type.</span></span> <span data-ttu-id="8a740-567">*Vea a continuación*.</span><span class="sxs-lookup"><span data-stu-id="8a740-567">*See below*.</span></span>|
|`description`|<span data-ttu-id="8a740-568">string</span><span class="sxs-lookup"><span data-stu-id="8a740-568">string</span></span>|<span data-ttu-id="8a740-569">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-569">128 characters</span></span>|<span data-ttu-id="8a740-570">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-570">✔</span></span>|<span data-ttu-id="8a740-571">Una breve descripción de la notificación.</span><span class="sxs-lookup"><span data-stu-id="8a740-571">A brief description of the notification.</span></span> <span data-ttu-id="8a740-572">*Vea a continuación*.</span><span class="sxs-lookup"><span data-stu-id="8a740-572">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="8a740-573">string</span><span class="sxs-lookup"><span data-stu-id="8a740-573">string</span></span>|<span data-ttu-id="8a740-574">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="8a740-574">128 characters</span></span>|<span data-ttu-id="8a740-575">✔</span><span class="sxs-lookup"><span data-stu-id="8a740-575">✔</span></span>|<span data-ttu-id="8a740-576">Ejemplo: "{actor} tarea creada {taskId} para usted"</span><span class="sxs-lookup"><span data-stu-id="8a740-576">Ex: "{actor} created task {taskId} for you"</span></span>|

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
