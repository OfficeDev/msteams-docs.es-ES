---
title: Referencia de esquema de manifiesto
description: Describe el esquema de manifiesto de Microsoft Teams
ms.topic: reference
ms.author: lajanuar
keywords: esquema de manifiesto de teams
ms.openlocfilehash: 291d748d546dec16fa4bf748318b8749b7d0275d
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479861"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="302dd-104">Referencia: esquema de manifiesto para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="302dd-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="302dd-105">El manifiesto de Teams describe cómo se integra la aplicación en el producto de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="302dd-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="302dd-106">El manifiesto debe cumplir con el esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="302dd-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="302dd-107">Las versiones anteriores 1.0-1.4 también son compatibles (con "v1.x" en la dirección URL).</span><span class="sxs-lookup"><span data-stu-id="302dd-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="302dd-108">En el ejemplo de esquema siguiente se muestran todas las opciones de extensibilidad.</span><span class="sxs-lookup"><span data-stu-id="302dd-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="302dd-109">Manifiesto completo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="302dd-109">Sample full manifest</span></span>

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
  },
  "defaultInstallScope": {
     "type": "string",
     "enum": [
        "personal",
        "team",
        "groupchat",
        "meetings"
      ],
      "description": "The install scope is defined for this app by default. It is the option displayed on the button when a user tries to add the app."
    },
  "defaultGroupCapability": {
      "type": "object",
      "properties": {
        "team": {
          "type": "string",
          "enum": [
            "tab",
            "bot",
            "connector"
          ],
          "description": "When the selected install scope is Team, this field specifies the default capability available."
    },
    "groupchat": {
      "type": "string",
      "enum": [
            "tab",
            "bot",
            "connector"
      ],
      "description": "When the selected install scope is Group Chat, this field specifies the default capability available."
    },
    "meetings": {
      "type": "string",
      "enum": [
            "tab",
            "bot",
            "connector"
      ],
      "description": "When the selected install scope is Meetings, this field specifies the default capability available."
      }
    },
    "description": "When a group install scope is selected, this defines the default capability when the user installs the app.",
    "additionalProperties": false

}
```

<span data-ttu-id="302dd-110">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="302dd-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="302dd-111">$schema</span><span class="sxs-lookup"><span data-stu-id="302dd-111">$schema</span></span>

<span data-ttu-id="302dd-112">Opcional, pero recomendado: cadena</span><span class="sxs-lookup"><span data-stu-id="302dd-112">Optional, but recommended — string</span></span>

<span data-ttu-id="302dd-113">La https:// url que hace referencia al esquema JSON para el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="302dd-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="302dd-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="302dd-114">manifestVersion</span></span>

<span data-ttu-id="302dd-115">**Obligatorio:** cadena</span><span class="sxs-lookup"><span data-stu-id="302dd-115">**Required** — string</span></span>

<span data-ttu-id="302dd-116">La versión del esquema de manifiesto que usa este manifiesto.</span><span class="sxs-lookup"><span data-stu-id="302dd-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="302dd-117">Debe ser 1.7.</span><span class="sxs-lookup"><span data-stu-id="302dd-117">It must be 1.7.</span></span>

## <a name="version"></a><span data-ttu-id="302dd-118">version</span><span class="sxs-lookup"><span data-stu-id="302dd-118">version</span></span>

<span data-ttu-id="302dd-119">**Obligatorio:** cadena</span><span class="sxs-lookup"><span data-stu-id="302dd-119">**Required** — string</span></span>

<span data-ttu-id="302dd-120">La versión de una aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="302dd-120">The version of a specific app.</span></span> <span data-ttu-id="302dd-121">Si actualiza algo en el manifiesto, la versión también debe incrementarse.</span><span class="sxs-lookup"><span data-stu-id="302dd-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="302dd-122">De este modo, cuando se instala el nuevo manifiesto, se sobrescribe el existente y el usuario recibe la nueva funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="302dd-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="302dd-123">Si esta aplicación se envió a la tienda, el nuevo manifiesto debe volver a enviarse y volver a validarse.</span><span class="sxs-lookup"><span data-stu-id="302dd-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="302dd-124">Los usuarios de la aplicación reciben el nuevo manifiesto actualizado automáticamente en pocas horas después de que se apruebe el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="302dd-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="302dd-125">Si cambian las solicitudes de permisos de la aplicación, se pedirá a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="302dd-126">Esta cadena de versión debe seguir el [estándar de semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="302dd-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="302dd-127">id</span><span class="sxs-lookup"><span data-stu-id="302dd-127">id</span></span>

<span data-ttu-id="302dd-128">**Obligatorio:** id. de aplicación de Microsoft</span><span class="sxs-lookup"><span data-stu-id="302dd-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="302dd-129">El identificador es un identificador único generado por Microsoft para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="302dd-130">Tienes un identificador si el bot está registrado a través de Microsoft Bot Framework o la aplicación web de la pestaña ya inicia sesión con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="302dd-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="302dd-131">Debe escribir el identificador aquí.</span><span class="sxs-lookup"><span data-stu-id="302dd-131">You must enter the ID here.</span></span> <span data-ttu-id="302dd-132">De lo contrario, debe generar un nuevo identificador en el Portal de registro de aplicaciones de Microsoft ([Mis aplicaciones](https://apps.dev.microsoft.com)).</span><span class="sxs-lookup"><span data-stu-id="302dd-132">Otherwise, you must generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)).</span></span> <span data-ttu-id="302dd-133">Use el mismo identificador si agrega un bot.</span><span class="sxs-lookup"><span data-stu-id="302dd-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="302dd-134">Si vas a enviar una actualización a la aplicación existente en AppSource, no se debe modificar el identificador del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="302dd-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="302dd-135">developer</span><span class="sxs-lookup"><span data-stu-id="302dd-135">developer</span></span>

<span data-ttu-id="302dd-136">**Obligatorio** : objeto</span><span class="sxs-lookup"><span data-stu-id="302dd-136">**Required** — object</span></span>

<span data-ttu-id="302dd-137">Proporciona información sobre su empresa.</span><span class="sxs-lookup"><span data-stu-id="302dd-137">Gives information about your company.</span></span> <span data-ttu-id="302dd-138">Para las aplicaciones enviadas a AppSource (anteriormente Tienda Office), estos valores deben coincidir con la información de la entrada de AppSource.</span><span class="sxs-lookup"><span data-stu-id="302dd-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="302dd-139">Consulte las [directrices de publicación](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) para obtener información adicional.</span><span class="sxs-lookup"><span data-stu-id="302dd-139">See the [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="302dd-140">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-140">Name</span></span>| <span data-ttu-id="302dd-141">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-141">Maximum size</span></span> | <span data-ttu-id="302dd-142">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-142">Required</span></span> | <span data-ttu-id="302dd-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="302dd-144">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-144">32 characters</span></span>|<span data-ttu-id="302dd-145">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-145">✔</span></span>|<span data-ttu-id="302dd-146">Nombre para mostrar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="302dd-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="302dd-147">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-147">2048 characters</span></span>|<span data-ttu-id="302dd-148">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-148">✔</span></span>|<span data-ttu-id="302dd-149">La https:// url del sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="302dd-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="302dd-150">Este vínculo debe llevar a los usuarios a su empresa o página de aterrizaje específica del producto.</span><span class="sxs-lookup"><span data-stu-id="302dd-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="302dd-151">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-151">2048 characters</span></span>|<span data-ttu-id="302dd-152">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-152">✔</span></span>|<span data-ttu-id="302dd-153">La https:// url a la directiva de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="302dd-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="302dd-154">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-154">2048 characters</span></span>|<span data-ttu-id="302dd-155">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-155">✔</span></span>|<span data-ttu-id="302dd-156">La https:// url a los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="302dd-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="302dd-157">10 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-157">10 characters</span></span>| |<span data-ttu-id="302dd-158">**Opcional** Id. de red de partners de Microsoft que identifica la organización asociada que está creando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="302dd-159">name</span><span class="sxs-lookup"><span data-stu-id="302dd-159">name</span></span>

<span data-ttu-id="302dd-160">**Obligatorio** : objeto</span><span class="sxs-lookup"><span data-stu-id="302dd-160">**Required** — object</span></span>

<span data-ttu-id="302dd-161">El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia de Teams.</span><span class="sxs-lookup"><span data-stu-id="302dd-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="302dd-162">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="302dd-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="302dd-163">Los valores de `short` y `full` deben ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="302dd-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="302dd-164">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-164">Name</span></span>| <span data-ttu-id="302dd-165">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-165">Maximum size</span></span> | <span data-ttu-id="302dd-166">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-166">Required</span></span> | <span data-ttu-id="302dd-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="302dd-168">30 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-168">30 characters</span></span>|<span data-ttu-id="302dd-169">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-169">✔</span></span>|<span data-ttu-id="302dd-170">El nombre para mostrar corto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="302dd-171">100 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-171">100 characters</span></span>||<span data-ttu-id="302dd-172">El nombre completo de la aplicación, que se usa si el nombre completo de la aplicación supera los 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="302dd-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="302dd-173">description</span><span class="sxs-lookup"><span data-stu-id="302dd-173">description</span></span>

<span data-ttu-id="302dd-174">**Obligatorio** : objeto</span><span class="sxs-lookup"><span data-stu-id="302dd-174">**Required** — object</span></span>

<span data-ttu-id="302dd-175">Describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="302dd-175">Describes your app to users.</span></span> <span data-ttu-id="302dd-176">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada AppSource.</span><span class="sxs-lookup"><span data-stu-id="302dd-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="302dd-177">Asegúrese de que su descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a comprender lo que hace su experiencia.</span><span class="sxs-lookup"><span data-stu-id="302dd-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="302dd-178">Debe tener en cuenta en la descripción completa, si se requiere una cuenta externa para su uso.</span><span class="sxs-lookup"><span data-stu-id="302dd-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="302dd-179">Los valores de `short` y `full` deben ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="302dd-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="302dd-180">La descripción breve no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="302dd-181">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-181">Name</span></span>| <span data-ttu-id="302dd-182">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-182">Maximum size</span></span> | <span data-ttu-id="302dd-183">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-183">Required</span></span> | <span data-ttu-id="302dd-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="302dd-185">80 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-185">80 characters</span></span>|<span data-ttu-id="302dd-186">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-186">✔</span></span>|<span data-ttu-id="302dd-187">Una breve descripción de la experiencia de la aplicación, que se usa cuando el espacio es limitado.</span><span class="sxs-lookup"><span data-stu-id="302dd-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="302dd-188">4000 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-188">4000 characters</span></span>|<span data-ttu-id="302dd-189">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-189">✔</span></span>|<span data-ttu-id="302dd-190">Descripción completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="302dd-191">packageName</span><span class="sxs-lookup"><span data-stu-id="302dd-191">packageName</span></span>

<span data-ttu-id="302dd-192">**Opcional:** cadena</span><span class="sxs-lookup"><span data-stu-id="302dd-192">**Optional** — string</span></span>

<span data-ttu-id="302dd-193">Un identificador único para la aplicación en la notación de dominio inverso; por ejemplo, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="302dd-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="302dd-194">Longitud máxima: 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="302dd-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="302dd-195">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="302dd-195">localizationInfo</span></span>

<span data-ttu-id="302dd-196">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="302dd-196">**Optional** — object</span></span>

<span data-ttu-id="302dd-197">Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="302dd-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="302dd-198">Vea [localización](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="302dd-198">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="302dd-199">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-199">Name</span></span>| <span data-ttu-id="302dd-200">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-200">Maximum size</span></span> | <span data-ttu-id="302dd-201">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-201">Required</span></span> | <span data-ttu-id="302dd-202">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="302dd-203">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-203">✔</span></span>|<span data-ttu-id="302dd-204">La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="302dd-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="302dd-205">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="302dd-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="302dd-206">Una matriz de objetos que especifica traducciones de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="302dd-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="302dd-207">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-207">Name</span></span>| <span data-ttu-id="302dd-208">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-208">Maximum size</span></span> | <span data-ttu-id="302dd-209">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-209">Required</span></span> | <span data-ttu-id="302dd-210">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="302dd-211">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-211">✔</span></span>|<span data-ttu-id="302dd-212">Etiqueta de idioma de las cadenas del archivo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="302dd-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="302dd-213">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-213">✔</span></span>|<span data-ttu-id="302dd-214">Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="302dd-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="302dd-215">iconos</span><span class="sxs-lookup"><span data-stu-id="302dd-215">icons</span></span>

<span data-ttu-id="302dd-216">**Obligatorio** : objeto</span><span class="sxs-lookup"><span data-stu-id="302dd-216">**Required** — object</span></span>

<span data-ttu-id="302dd-217">Iconos usados dentro de la aplicación de Teams.</span><span class="sxs-lookup"><span data-stu-id="302dd-217">Icons used within the Teams app.</span></span> <span data-ttu-id="302dd-218">Los archivos de icono deben incluirse como parte del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="302dd-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="302dd-219">Consulta [Iconos](../../concepts/build-and-test/apps-package.md#app-icons) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="302dd-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="302dd-220">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-220">Name</span></span>| <span data-ttu-id="302dd-221">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-221">Maximum size</span></span> | <span data-ttu-id="302dd-222">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-222">Required</span></span> | <span data-ttu-id="302dd-223">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="302dd-224">32 x 32 píxeles</span><span class="sxs-lookup"><span data-stu-id="302dd-224">32 x 32 pixels</span></span>|<span data-ttu-id="302dd-225">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-225">✔</span></span>|<span data-ttu-id="302dd-226">Una ruta de acceso de archivo relativa a un icono de esquema PNG transparente de 32 x 32.</span><span class="sxs-lookup"><span data-stu-id="302dd-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="302dd-227">192 x 192 píxeles</span><span class="sxs-lookup"><span data-stu-id="302dd-227">192 x 192 pixels</span></span>|<span data-ttu-id="302dd-228">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-228">✔</span></span>|<span data-ttu-id="302dd-229">Una ruta de acceso de archivo relativa a un icono PNG de color completo de 192 x 192.</span><span class="sxs-lookup"><span data-stu-id="302dd-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="302dd-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="302dd-230">accentColor</span></span>

<span data-ttu-id="302dd-231">**Opcional:** código de color Hexadecimal HTML</span><span class="sxs-lookup"><span data-stu-id="302dd-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="302dd-232">Color que se usará junto con y como fondo para los iconos de esquema.</span><span class="sxs-lookup"><span data-stu-id="302dd-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="302dd-233">El valor debe ser un código de color HTML válido a partir de '#', por ejemplo `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="302dd-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="302dd-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="302dd-234">configurableTabs</span></span>

<span data-ttu-id="302dd-235">**Opcional:** matriz</span><span class="sxs-lookup"><span data-stu-id="302dd-235">**Optional** — array</span></span>

<span data-ttu-id="302dd-236">Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de grupo que requiere una configuración adicional antes de agregarla.</span><span class="sxs-lookup"><span data-stu-id="302dd-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="302dd-237">Las pestañas configurables solo se admiten en el ámbito de teams (no personal) y actualmente **solo** se admite una pestaña por aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-237">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="302dd-238">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-238">Name</span></span>| <span data-ttu-id="302dd-239">Tipo</span><span class="sxs-lookup"><span data-stu-id="302dd-239">Type</span></span>| <span data-ttu-id="302dd-240">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-240">Maximum size</span></span> | <span data-ttu-id="302dd-241">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-241">Required</span></span> | <span data-ttu-id="302dd-242">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-242">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="302dd-243">string</span><span class="sxs-lookup"><span data-stu-id="302dd-243">string</span></span>|<span data-ttu-id="302dd-244">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-244">2048 characters</span></span>|<span data-ttu-id="302dd-245">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-245">✔</span></span>|<span data-ttu-id="302dd-246">La https:// url que se va a usar al configurar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="302dd-246">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="302dd-247">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="302dd-247">array of enums</span></span>|<span data-ttu-id="302dd-248">1 </span><span class="sxs-lookup"><span data-stu-id="302dd-248">1</span></span>|<span data-ttu-id="302dd-249">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-249">✔</span></span>|<span data-ttu-id="302dd-250">Actualmente, las pestañas configurables solo admiten `team` los `groupchat` ámbitos y.</span><span class="sxs-lookup"><span data-stu-id="302dd-250">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="302dd-251">boolean</span><span class="sxs-lookup"><span data-stu-id="302dd-251">boolean</span></span>|||<span data-ttu-id="302dd-252">Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de su creación.</span><span class="sxs-lookup"><span data-stu-id="302dd-252">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="302dd-253">Valor predeterminado: **true**.</span><span class="sxs-lookup"><span data-stu-id="302dd-253">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="302dd-254">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="302dd-254">array of enums</span></span>|<span data-ttu-id="302dd-255">6 </span><span class="sxs-lookup"><span data-stu-id="302dd-255">6</span></span>||<span data-ttu-id="302dd-256">Conjunto de `contextItem` ámbitos donde se admite una pestaña.</span><span class="sxs-lookup"><span data-stu-id="302dd-256">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="302dd-257">Valor predeterminado: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="302dd-257">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="302dd-258">string</span><span class="sxs-lookup"><span data-stu-id="302dd-258">string</span></span>|<span data-ttu-id="302dd-259">2048</span><span class="sxs-lookup"><span data-stu-id="302dd-259">2048</span></span>||<span data-ttu-id="302dd-260">Una ruta de acceso de archivo relativa a una imagen de vista previa de tabulación para su uso en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="302dd-260">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="302dd-261">Tamaño 1024x768.</span><span class="sxs-lookup"><span data-stu-id="302dd-261">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="302dd-262">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="302dd-262">array of enums</span></span>|<span data-ttu-id="302dd-263">1 </span><span class="sxs-lookup"><span data-stu-id="302dd-263">1</span></span>||<span data-ttu-id="302dd-264">Define cómo la pestaña está disponible en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="302dd-264">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="302dd-265">Las opciones son `sharePointFullPage` y `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="302dd-265">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="302dd-266">staticTabs</span><span class="sxs-lookup"><span data-stu-id="302dd-266">staticTabs</span></span>

<span data-ttu-id="302dd-267">**Opcional:** matriz</span><span class="sxs-lookup"><span data-stu-id="302dd-267">**Optional** — array</span></span>

<span data-ttu-id="302dd-268">Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente.</span><span class="sxs-lookup"><span data-stu-id="302dd-268">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="302dd-269">Las pestañas estáticas declaradas en el ámbito siempre se anclan a la experiencia `personal` personal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-269">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="302dd-270">Actualmente no se admiten las pestañas estáticas declaradas `team` en el ámbito.</span><span class="sxs-lookup"><span data-stu-id="302dd-270">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="302dd-271">Este elemento es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="302dd-271">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="302dd-272">Este bloque solo es necesario para las soluciones que proporcionan una solución de tabulación estática.</span><span class="sxs-lookup"><span data-stu-id="302dd-272">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="302dd-273">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-273">Name</span></span>| <span data-ttu-id="302dd-274">Tipo</span><span class="sxs-lookup"><span data-stu-id="302dd-274">Type</span></span>| <span data-ttu-id="302dd-275">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-275">Maximum size</span></span> | <span data-ttu-id="302dd-276">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-276">Required</span></span> | <span data-ttu-id="302dd-277">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-277">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="302dd-278">string</span><span class="sxs-lookup"><span data-stu-id="302dd-278">string</span></span>|<span data-ttu-id="302dd-279">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-279">64 characters</span></span>|<span data-ttu-id="302dd-280">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-280">✔</span></span>|<span data-ttu-id="302dd-281">Identificador único para la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="302dd-281">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="302dd-282">string</span><span class="sxs-lookup"><span data-stu-id="302dd-282">string</span></span>|<span data-ttu-id="302dd-283">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-283">128 characters</span></span>|<span data-ttu-id="302dd-284">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-284">✔</span></span>|<span data-ttu-id="302dd-285">Nombre para mostrar de la pestaña en la interfaz de canal.</span><span class="sxs-lookup"><span data-stu-id="302dd-285">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="302dd-286">string</span><span class="sxs-lookup"><span data-stu-id="302dd-286">string</span></span>||<span data-ttu-id="302dd-287">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-287">✔</span></span>|<span data-ttu-id="302dd-288">Dirección HTTPS:// que apunta a la interfaz de usuario de la entidad que se va a mostrar en el lienzo de Teams.</span><span class="sxs-lookup"><span data-stu-id="302dd-288">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="302dd-289">string</span><span class="sxs-lookup"><span data-stu-id="302dd-289">string</span></span>|||<span data-ttu-id="302dd-290">La https:// dirección URL que se debe apuntar si un usuario opta por ver en un explorador.</span><span class="sxs-lookup"><span data-stu-id="302dd-290">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="302dd-291">string</span><span class="sxs-lookup"><span data-stu-id="302dd-291">string</span></span>|||<span data-ttu-id="302dd-292">La https:// dirección URL que se va a apuntar a las consultas de búsqueda de un usuario.</span><span class="sxs-lookup"><span data-stu-id="302dd-292">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="302dd-293">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="302dd-293">array of enums</span></span>|<span data-ttu-id="302dd-294">1 </span><span class="sxs-lookup"><span data-stu-id="302dd-294">1</span></span>|<span data-ttu-id="302dd-295">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-295">✔</span></span>|<span data-ttu-id="302dd-296">Actualmente, las pestañas estáticas solo admiten el ámbito, lo que significa que solo se puede aprovisionar como `personal` parte de la experiencia personal.</span><span class="sxs-lookup"><span data-stu-id="302dd-296">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="302dd-297">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="302dd-297">array of enums</span></span>| <span data-ttu-id="302dd-298">2 </span><span class="sxs-lookup"><span data-stu-id="302dd-298">2</span></span>|| <span data-ttu-id="302dd-299">Conjunto de `contextItem` ámbitos donde se admite una pestaña.</span><span class="sxs-lookup"><span data-stu-id="302dd-299">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="302dd-300">Si las pestañas requieren información dependiente del contexto para mostrar contenido  relevante o para iniciar un flujo de autenticación, consulte [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="302dd-300">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="302dd-301">bots</span><span class="sxs-lookup"><span data-stu-id="302dd-301">bots</span></span>

<span data-ttu-id="302dd-302">**Opcional:** matriz</span><span class="sxs-lookup"><span data-stu-id="302dd-302">**Optional** — array</span></span>

<span data-ttu-id="302dd-303">Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="302dd-303">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="302dd-304">El elemento es una matriz (máximo de solo 1 elemento actualmente solo se permite un bot por aplicación) con todos los &mdash; elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="302dd-304">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="302dd-305">Este bloque solo es necesario para las soluciones que proporcionan una experiencia de bot.</span><span class="sxs-lookup"><span data-stu-id="302dd-305">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="302dd-306">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-306">Name</span></span>| <span data-ttu-id="302dd-307">Tipo</span><span class="sxs-lookup"><span data-stu-id="302dd-307">Type</span></span>| <span data-ttu-id="302dd-308">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-308">Maximum size</span></span> | <span data-ttu-id="302dd-309">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-309">Required</span></span> | <span data-ttu-id="302dd-310">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-310">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="302dd-311">string</span><span class="sxs-lookup"><span data-stu-id="302dd-311">string</span></span>|<span data-ttu-id="302dd-312">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-312">64 characters</span></span>|<span data-ttu-id="302dd-313">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-313">✔</span></span>|<span data-ttu-id="302dd-314">El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="302dd-314">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="302dd-315">Esto bien puede ser el mismo que el identificador general [de la aplicación](#id).</span><span class="sxs-lookup"><span data-stu-id="302dd-315">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="302dd-316">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="302dd-316">array of enums</span></span>|<span data-ttu-id="302dd-317">3 </span><span class="sxs-lookup"><span data-stu-id="302dd-317">3</span></span>|<span data-ttu-id="302dd-318">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-318">✔</span></span>|<span data-ttu-id="302dd-319">Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`).</span><span class="sxs-lookup"><span data-stu-id="302dd-319">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="302dd-320">Estas opciones no son exclusivas.</span><span class="sxs-lookup"><span data-stu-id="302dd-320">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="302dd-321">boolean</span><span class="sxs-lookup"><span data-stu-id="302dd-321">boolean</span></span>|||<span data-ttu-id="302dd-322">Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico.</span><span class="sxs-lookup"><span data-stu-id="302dd-322">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="302dd-323">Valor predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="302dd-323">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="302dd-324">boolean</span><span class="sxs-lookup"><span data-stu-id="302dd-324">boolean</span></span>|||<span data-ttu-id="302dd-325">Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación.</span><span class="sxs-lookup"><span data-stu-id="302dd-325">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="302dd-326">Valor predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="302dd-326">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="302dd-327">boolean</span><span class="sxs-lookup"><span data-stu-id="302dd-327">boolean</span></span>|||<span data-ttu-id="302dd-328">Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal.</span><span class="sxs-lookup"><span data-stu-id="302dd-328">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="302dd-329">Valor predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="302dd-329">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="302dd-330">boolean</span><span class="sxs-lookup"><span data-stu-id="302dd-330">boolean</span></span>|||<span data-ttu-id="302dd-331">Valor que indica dónde un bot admite llamadas de audio.</span><span class="sxs-lookup"><span data-stu-id="302dd-331">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="302dd-332">**IMPORTANTE:** Esta propiedad es actualmente experimental.</span><span class="sxs-lookup"><span data-stu-id="302dd-332">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="302dd-333">Es posible que las propiedades experimentales no estén completas y que se someten a cambios antes de estar totalmente disponibles.</span><span class="sxs-lookup"><span data-stu-id="302dd-333">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="302dd-334">Se proporciona solo con fines de prueba y exploración y no debe usarse en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="302dd-334">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="302dd-335">Valor predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="302dd-335">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="302dd-336">boolean</span><span class="sxs-lookup"><span data-stu-id="302dd-336">boolean</span></span>|||<span data-ttu-id="302dd-337">Valor que indica dónde un bot admite videollamadas.</span><span class="sxs-lookup"><span data-stu-id="302dd-337">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="302dd-338">**IMPORTANTE:** Esta propiedad es actualmente experimental.</span><span class="sxs-lookup"><span data-stu-id="302dd-338">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="302dd-339">Es posible que las propiedades experimentales no estén completas y que se someten a cambios antes de estar totalmente disponibles.</span><span class="sxs-lookup"><span data-stu-id="302dd-339">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="302dd-340">Se proporciona solo con fines de prueba y exploración y no debe usarse en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="302dd-340">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="302dd-341">Valor predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="302dd-341">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="302dd-342">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="302dd-342">bots.commandLists</span></span>

<span data-ttu-id="302dd-343">Una lista opcional de comandos que el bot puede recomendar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="302dd-343">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="302dd-344">El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de comandos independiente para cada ámbito compatible `object` con el bot.</span><span class="sxs-lookup"><span data-stu-id="302dd-344">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="302dd-345">Consulta [Menús bot para](~/bots/how-to/create-a-bot-commands-menu.md) obtener más información.</span><span class="sxs-lookup"><span data-stu-id="302dd-345">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="302dd-346">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-346">Name</span></span>| <span data-ttu-id="302dd-347">Tipo</span><span class="sxs-lookup"><span data-stu-id="302dd-347">Type</span></span>| <span data-ttu-id="302dd-348">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-348">Maximum size</span></span> | <span data-ttu-id="302dd-349">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-349">Required</span></span> | <span data-ttu-id="302dd-350">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-350">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="302dd-351">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="302dd-351">array of enums</span></span>|<span data-ttu-id="302dd-352">3 </span><span class="sxs-lookup"><span data-stu-id="302dd-352">3</span></span>|<span data-ttu-id="302dd-353">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-353">✔</span></span>|<span data-ttu-id="302dd-354">Especifica el ámbito para el que la lista de comandos es válida.</span><span class="sxs-lookup"><span data-stu-id="302dd-354">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="302dd-355">Las opciones son `team`, `personal` y `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="302dd-355">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="302dd-356">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="302dd-356">array of objects</span></span>|<span data-ttu-id="302dd-357">10  </span><span class="sxs-lookup"><span data-stu-id="302dd-357">10</span></span>|<span data-ttu-id="302dd-358">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-358">✔</span></span>|<span data-ttu-id="302dd-359">Una matriz de comandos que el bot admite:</span><span class="sxs-lookup"><span data-stu-id="302dd-359">An array of commands the bot supports:</span></span><br><span data-ttu-id="302dd-360">`title`: el nombre de comando del bot (cadena, 32)</span><span class="sxs-lookup"><span data-stu-id="302dd-360">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="302dd-361">`description`: una descripción o un ejemplo sencillo de la sintaxis del comando y su argumento (cadena, 128).</span><span class="sxs-lookup"><span data-stu-id="302dd-361">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="302dd-362">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="302dd-362">bots.commandLists.commands</span></span>

|<span data-ttu-id="302dd-363">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-363">Name</span></span>| <span data-ttu-id="302dd-364">Tipo</span><span class="sxs-lookup"><span data-stu-id="302dd-364">Type</span></span>| <span data-ttu-id="302dd-365">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-365">Maximum size</span></span> | <span data-ttu-id="302dd-366">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-366">Required</span></span> | <span data-ttu-id="302dd-367">Description</span><span class="sxs-lookup"><span data-stu-id="302dd-367">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="302dd-368">title</span><span class="sxs-lookup"><span data-stu-id="302dd-368">title</span></span>|<span data-ttu-id="302dd-369">string</span><span class="sxs-lookup"><span data-stu-id="302dd-369">string</span></span>|<span data-ttu-id="302dd-370">12 </span><span class="sxs-lookup"><span data-stu-id="302dd-370">12</span></span>|<span data-ttu-id="302dd-371">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-371">✔</span></span>|<span data-ttu-id="302dd-372">Nombre del comando bot</span><span class="sxs-lookup"><span data-stu-id="302dd-372">The bot command name</span></span>|
|<span data-ttu-id="302dd-373">description</span><span class="sxs-lookup"><span data-stu-id="302dd-373">description</span></span>|<span data-ttu-id="302dd-374">string</span><span class="sxs-lookup"><span data-stu-id="302dd-374">string</span></span>|<span data-ttu-id="302dd-375">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-375">128 characters</span></span>|<span data-ttu-id="302dd-376">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-376">✔</span></span>|<span data-ttu-id="302dd-377">Una descripción de texto simple o un ejemplo de la sintaxis del comando y sus argumentos.</span><span class="sxs-lookup"><span data-stu-id="302dd-377">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="302dd-378">conectores</span><span class="sxs-lookup"><span data-stu-id="302dd-378">connectors</span></span>

<span data-ttu-id="302dd-379">**Opcional:** matriz</span><span class="sxs-lookup"><span data-stu-id="302dd-379">**Optional** — array</span></span>

<span data-ttu-id="302dd-380">El `connectors` bloque define un conector de Office 365 para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-380">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="302dd-381">El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="302dd-381">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="302dd-382">Este bloque solo es necesario para las soluciones que proporcionan un conector.</span><span class="sxs-lookup"><span data-stu-id="302dd-382">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="302dd-383">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-383">Name</span></span>| <span data-ttu-id="302dd-384">Tipo</span><span class="sxs-lookup"><span data-stu-id="302dd-384">Type</span></span>| <span data-ttu-id="302dd-385">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-385">Maximum size</span></span> | <span data-ttu-id="302dd-386">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-386">Required</span></span> | <span data-ttu-id="302dd-387">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-387">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="302dd-388">string</span><span class="sxs-lookup"><span data-stu-id="302dd-388">string</span></span>|<span data-ttu-id="302dd-389">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-389">2048 characters</span></span>|<span data-ttu-id="302dd-390">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-390">✔</span></span>|<span data-ttu-id="302dd-391">La https:// url que se va a usar al configurar el conector.</span><span class="sxs-lookup"><span data-stu-id="302dd-391">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="302dd-392">matriz de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="302dd-392">array of enums</span></span>|<span data-ttu-id="302dd-393">1 </span><span class="sxs-lookup"><span data-stu-id="302dd-393">1</span></span>|<span data-ttu-id="302dd-394">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-394">✔</span></span>|<span data-ttu-id="302dd-395">Especifica si connector ofrece una experiencia en el contexto de un canal en un , o una experiencia ámbito a un `team` usuario individual solo ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="302dd-395">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="302dd-396">Actualmente, solo se `team` admite el ámbito.</span><span class="sxs-lookup"><span data-stu-id="302dd-396">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="302dd-397">string</span><span class="sxs-lookup"><span data-stu-id="302dd-397">string</span></span>|<span data-ttu-id="302dd-398">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-398">64 characters</span></span>|<span data-ttu-id="302dd-399">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-399">✔</span></span>|<span data-ttu-id="302dd-400">Identificador único del conector que coincide con su identificador en el [Panel de desarrolladores de conectores.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="302dd-400">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="302dd-401">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="302dd-401">composeExtensions</span></span>

<span data-ttu-id="302dd-402">**Opcional:** matriz</span><span class="sxs-lookup"><span data-stu-id="302dd-402">**Optional** — array</span></span>

<span data-ttu-id="302dd-403">Define una extensión de mensajería para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-403">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="302dd-404">El nombre de la característica se cambió de "extensión de redacción" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="302dd-404">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="302dd-405">El elemento es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="302dd-405">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="302dd-406">Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="302dd-406">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="302dd-407">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-407">Name</span></span>| <span data-ttu-id="302dd-408">Tipo</span><span class="sxs-lookup"><span data-stu-id="302dd-408">Type</span></span> | <span data-ttu-id="302dd-409">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-409">Maximum Size</span></span> | <span data-ttu-id="302dd-410">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="302dd-410">Required</span></span> | <span data-ttu-id="302dd-411">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-411">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="302dd-412">string</span><span class="sxs-lookup"><span data-stu-id="302dd-412">string</span></span>|<span data-ttu-id="302dd-413">64</span><span class="sxs-lookup"><span data-stu-id="302dd-413">64</span></span>|<span data-ttu-id="302dd-414">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-414">✔</span></span>|<span data-ttu-id="302dd-415">El identificador único de la aplicación de Microsoft para el bot que hace una copia de seguridad de la extensión de mensajería, tal como se registró con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="302dd-415">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="302dd-416">Esto bien puede ser el mismo que el identificador general de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-416">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="302dd-417">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="302dd-417">array of objects</span></span>|<span data-ttu-id="302dd-418">10  </span><span class="sxs-lookup"><span data-stu-id="302dd-418">10</span></span>|<span data-ttu-id="302dd-419">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-419">✔</span></span>|<span data-ttu-id="302dd-420">Matriz de comandos que admite la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="302dd-420">Array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="302dd-421">boolean</span><span class="sxs-lookup"><span data-stu-id="302dd-421">boolean</span></span>|||<span data-ttu-id="302dd-422">Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="302dd-422">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="302dd-423">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="302dd-423">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="302dd-424">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="302dd-424">array of Objects</span></span>|<span data-ttu-id="302dd-425">5 </span><span class="sxs-lookup"><span data-stu-id="302dd-425">5</span></span>||<span data-ttu-id="302dd-426">Una lista de controladores que permiten invocar aplicaciones cuando se cumplen determinadas condiciones.</span><span class="sxs-lookup"><span data-stu-id="302dd-426">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="302dd-427">string</span><span class="sxs-lookup"><span data-stu-id="302dd-427">string</span></span>|||<span data-ttu-id="302dd-428">El tipo de controlador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="302dd-428">The type of message handler.</span></span> <span data-ttu-id="302dd-429">Debe ser `"link"`.</span><span class="sxs-lookup"><span data-stu-id="302dd-429">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="302dd-430">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="302dd-430">array of Strings</span></span>|||<span data-ttu-id="302dd-431">Matriz de dominios para los que se puede registrar el controlador de mensajes de vínculo.</span><span class="sxs-lookup"><span data-stu-id="302dd-431">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="302dd-432">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="302dd-432">composeExtensions.commands</span></span>

<span data-ttu-id="302dd-433">La extensión de mensajería debe declarar uno o varios comandos.</span><span class="sxs-lookup"><span data-stu-id="302dd-433">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="302dd-434">Cada comando aparece en Microsoft Teams como una interacción potencial desde el punto de entrada basado en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="302dd-434">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="302dd-435">Hay un máximo de 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="302dd-435">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="302dd-436">Cada elemento de comando es un objeto con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="302dd-436">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="302dd-437">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-437">Name</span></span>| <span data-ttu-id="302dd-438">Tipo</span><span class="sxs-lookup"><span data-stu-id="302dd-438">Type</span></span>| <span data-ttu-id="302dd-439">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-439">Maximum size</span></span> | <span data-ttu-id="302dd-440">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-440">Required</span></span> | <span data-ttu-id="302dd-441">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-441">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="302dd-442">string</span><span class="sxs-lookup"><span data-stu-id="302dd-442">string</span></span>|<span data-ttu-id="302dd-443">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-443">64 characters</span></span>|<span data-ttu-id="302dd-444">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-444">✔</span></span>|<span data-ttu-id="302dd-445">El identificador del comando.</span><span class="sxs-lookup"><span data-stu-id="302dd-445">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="302dd-446">string</span><span class="sxs-lookup"><span data-stu-id="302dd-446">string</span></span>|<span data-ttu-id="302dd-447">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-447">32 characters</span></span>|<span data-ttu-id="302dd-448">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-448">✔</span></span>|<span data-ttu-id="302dd-449">Nombre de comando fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="302dd-449">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="302dd-450">string</span><span class="sxs-lookup"><span data-stu-id="302dd-450">string</span></span>|<span data-ttu-id="302dd-451">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-451">64 characters</span></span>||<span data-ttu-id="302dd-452">Tipo del comando.</span><span class="sxs-lookup"><span data-stu-id="302dd-452">Type of the command.</span></span> <span data-ttu-id="302dd-453">Uno de `query` o `action` .</span><span class="sxs-lookup"><span data-stu-id="302dd-453">One of `query` or `action`.</span></span> <span data-ttu-id="302dd-454">Valor predeterminado: **consulta**.</span><span class="sxs-lookup"><span data-stu-id="302dd-454">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="302dd-455">string</span><span class="sxs-lookup"><span data-stu-id="302dd-455">string</span></span>|<span data-ttu-id="302dd-456">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-456">128 characters</span></span>||<span data-ttu-id="302dd-457">La descripción que se muestra a los usuarios para indicar el propósito de este comando.</span><span class="sxs-lookup"><span data-stu-id="302dd-457">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="302dd-458">boolean</span><span class="sxs-lookup"><span data-stu-id="302dd-458">boolean</span></span>|||<span data-ttu-id="302dd-459">Un valor booleano indica si el comando se ejecuta inicialmente sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="302dd-459">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="302dd-460">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="302dd-460">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="302dd-461">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="302dd-461">array of Strings</span></span>|<span data-ttu-id="302dd-462">3 </span><span class="sxs-lookup"><span data-stu-id="302dd-462">3</span></span>||<span data-ttu-id="302dd-463">Define desde dónde se puede invocar la extensión de mensaje.</span><span class="sxs-lookup"><span data-stu-id="302dd-463">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="302dd-464">Cualquier combinación de `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="302dd-464">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="302dd-465">El valor predeterminado es `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="302dd-465">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="302dd-466">boolean</span><span class="sxs-lookup"><span data-stu-id="302dd-466">boolean</span></span>|||<span data-ttu-id="302dd-467">Valor booleano que indica si debe capturar el módulo de tareas dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="302dd-467">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="302dd-468">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="302dd-468">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="302dd-469">object</span><span class="sxs-lookup"><span data-stu-id="302dd-469">object</span></span>|||<span data-ttu-id="302dd-470">Especifique el módulo de tareas que se debe cargar previamente al usar un comando de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="302dd-470">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="302dd-471">string</span><span class="sxs-lookup"><span data-stu-id="302dd-471">string</span></span>|<span data-ttu-id="302dd-472">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-472">64 characters</span></span>||<span data-ttu-id="302dd-473">Título del cuadro de diálogo inicial.</span><span class="sxs-lookup"><span data-stu-id="302dd-473">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="302dd-474">string</span><span class="sxs-lookup"><span data-stu-id="302dd-474">string</span></span>|||<span data-ttu-id="302dd-475">Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="302dd-475">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="302dd-476">string</span><span class="sxs-lookup"><span data-stu-id="302dd-476">string</span></span>|||<span data-ttu-id="302dd-477">Alto del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "mediano" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="302dd-477">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="302dd-478">string</span><span class="sxs-lookup"><span data-stu-id="302dd-478">string</span></span>|||<span data-ttu-id="302dd-479">Dirección URL de vista web inicial.</span><span class="sxs-lookup"><span data-stu-id="302dd-479">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="302dd-480">matriz de objeto</span><span class="sxs-lookup"><span data-stu-id="302dd-480">array of object</span></span>|<span data-ttu-id="302dd-481">5 elementos</span><span class="sxs-lookup"><span data-stu-id="302dd-481">5 items</span></span>|<span data-ttu-id="302dd-482">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-482">✔</span></span>|<span data-ttu-id="302dd-483">La lista de parámetros que toma el comando.</span><span class="sxs-lookup"><span data-stu-id="302dd-483">The list of parameters the command takes.</span></span> <span data-ttu-id="302dd-484">Mínimo: 1; máximo: 5.</span><span class="sxs-lookup"><span data-stu-id="302dd-484">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="302dd-485">string</span><span class="sxs-lookup"><span data-stu-id="302dd-485">string</span></span>|<span data-ttu-id="302dd-486">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-486">64 characters</span></span>|<span data-ttu-id="302dd-487">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-487">✔</span></span>|<span data-ttu-id="302dd-488">Nombre del parámetro tal como aparece en el cliente.</span><span class="sxs-lookup"><span data-stu-id="302dd-488">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="302dd-489">Esto se incluye en la solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="302dd-489">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="302dd-490">string</span><span class="sxs-lookup"><span data-stu-id="302dd-490">string</span></span>|<span data-ttu-id="302dd-491">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-491">32 characters</span></span>|<span data-ttu-id="302dd-492">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-492">✔</span></span>|<span data-ttu-id="302dd-493">Título fácil de usar para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="302dd-493">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="302dd-494">string</span><span class="sxs-lookup"><span data-stu-id="302dd-494">string</span></span>|<span data-ttu-id="302dd-495">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-495">128 characters</span></span>||<span data-ttu-id="302dd-496">Cadena fácil de usar que describe el propósito de este parámetro.</span><span class="sxs-lookup"><span data-stu-id="302dd-496">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="302dd-497">string</span><span class="sxs-lookup"><span data-stu-id="302dd-497">string</span></span>|<span data-ttu-id="302dd-498">512 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-498">512 characters</span></span>||<span data-ttu-id="302dd-499">Valor inicial del parámetro.</span><span class="sxs-lookup"><span data-stu-id="302dd-499">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="302dd-500">string</span><span class="sxs-lookup"><span data-stu-id="302dd-500">string</span></span>|<span data-ttu-id="302dd-501">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-501">128 characters</span></span>||<span data-ttu-id="302dd-502">Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="302dd-502">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="302dd-503">Uno de `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="302dd-503">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="302dd-504">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="302dd-504">array of objects</span></span>|<span data-ttu-id="302dd-505">10 elementos</span><span class="sxs-lookup"><span data-stu-id="302dd-505">10 items</span></span>||<span data-ttu-id="302dd-506">Las opciones de elección para `choiceset` el archivo .</span><span class="sxs-lookup"><span data-stu-id="302dd-506">The choice options for the`choiceset`.</span></span> <span data-ttu-id="302dd-507">Use solo cuando `parameter.inputType` es `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="302dd-507">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="302dd-508">string</span><span class="sxs-lookup"><span data-stu-id="302dd-508">string</span></span>|<span data-ttu-id="302dd-509">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-509">128 characters</span></span>|<span data-ttu-id="302dd-510">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-510">✔</span></span>|<span data-ttu-id="302dd-511">Título de la elección.</span><span class="sxs-lookup"><span data-stu-id="302dd-511">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="302dd-512">string</span><span class="sxs-lookup"><span data-stu-id="302dd-512">string</span></span>|<span data-ttu-id="302dd-513">512 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-513">512 characters</span></span>|<span data-ttu-id="302dd-514">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-514">✔</span></span>|<span data-ttu-id="302dd-515">Valor de la elección.</span><span class="sxs-lookup"><span data-stu-id="302dd-515">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="302dd-516">permisos</span><span class="sxs-lookup"><span data-stu-id="302dd-516">permissions</span></span>

<span data-ttu-id="302dd-517">**Opcional:** matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="302dd-517">**Optional** — array of strings</span></span>

<span data-ttu-id="302dd-518">Una matriz de los cuales especifica qué permisos solicita la aplicación, lo que permite a los usuarios `string` finales saber cómo funciona la extensión.</span><span class="sxs-lookup"><span data-stu-id="302dd-518">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="302dd-519">Las siguientes opciones no son exclusivas:</span><span class="sxs-lookup"><span data-stu-id="302dd-519">The following options are non-exclusive:</span></span>

* <span data-ttu-id="302dd-520">`identity`&emsp;Requiere información de identidad de usuario</span><span class="sxs-lookup"><span data-stu-id="302dd-520">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="302dd-521">`messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a miembros del equipo</span><span class="sxs-lookup"><span data-stu-id="302dd-521">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="302dd-522">Al cambiar estos permisos durante la actualización de la aplicación, los usuarios repiten el proceso de consentimiento después de ejecutar la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="302dd-522">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="302dd-523">Consulta [Actualizar la aplicación para](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) obtener más información.</span><span class="sxs-lookup"><span data-stu-id="302dd-523">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="302dd-524">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="302dd-524">devicePermissions</span></span>

<span data-ttu-id="302dd-525">**Opcional:** matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="302dd-525">**Optional** — array of strings</span></span>

<span data-ttu-id="302dd-526">Proporciona las características nativas en el dispositivo de un usuario al que la aplicación solicita acceso.</span><span class="sxs-lookup"><span data-stu-id="302dd-526">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="302dd-527">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="302dd-527">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="302dd-528">validDomains</span><span class="sxs-lookup"><span data-stu-id="302dd-528">validDomains</span></span>

<span data-ttu-id="302dd-529">**Opcional**, excepto **Requerido cuando** se indica</span><span class="sxs-lookup"><span data-stu-id="302dd-529">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="302dd-530">Una lista de dominios válidos para sitios web que la aplicación espera cargar en el cliente de Teams.</span><span class="sxs-lookup"><span data-stu-id="302dd-530">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="302dd-531">Las listas de dominios pueden incluir caracteres comodín, por ejemplo, `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="302dd-531">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="302dd-532">Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="302dd-532">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="302dd-533">Si la interfaz de usuario de contenido o configuración de pestañas necesita navegar a cualquier otro dominio además del uso para la configuración de pestañas, este dominio debe especificarse aquí.</span><span class="sxs-lookup"><span data-stu-id="302dd-533">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="302dd-534">No es **necesario** incluir los dominios de los proveedores de identidades que quieres admitir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-534">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="302dd-535">Por ejemplo, para autenticar con un identificador de Google, es necesario redirigir a accounts.google.com, sin embargo, no debe incluir accounts.google.com en `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="302dd-535">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="302dd-536">Las aplicaciones de Teams que requieren que sus propias direcciones URL de sharepoint funcionen correctamente, incluyen "{teamsitedomain}" en su lista de dominios válida.</span><span class="sxs-lookup"><span data-stu-id="302dd-536">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="302dd-537">No agregue dominios que estén fuera del control, ya sea directamente o a través de caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="302dd-537">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="302dd-538">Por ejemplo, `yourapp.onmicrosoft.com` es válido, sin embargo, `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="302dd-538">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="302dd-539">El objeto es una matriz con todos los elementos del tipo `string` .</span><span class="sxs-lookup"><span data-stu-id="302dd-539">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="302dd-540">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="302dd-540">webApplicationInfo</span></span>

<span data-ttu-id="302dd-541">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="302dd-541">**Optional** — object</span></span>

<span data-ttu-id="302dd-542">Proporcione el identificador de aplicación de Azure Active Directory (AAD) y la información de Microsoft Graph para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-542">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="302dd-543">Si la aplicación está registrada en AAD, debes proporcionar el identificador de la aplicación para que los administradores puedan revisar fácilmente los permisos y conceder el consentimiento en el Centro de administración de Teams.</span><span class="sxs-lookup"><span data-stu-id="302dd-543">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="302dd-544">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-544">Name</span></span>| <span data-ttu-id="302dd-545">Tipo</span><span class="sxs-lookup"><span data-stu-id="302dd-545">Type</span></span>| <span data-ttu-id="302dd-546">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-546">Maximum size</span></span> | <span data-ttu-id="302dd-547">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-547">Required</span></span> | <span data-ttu-id="302dd-548">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-548">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="302dd-549">string</span><span class="sxs-lookup"><span data-stu-id="302dd-549">string</span></span>|<span data-ttu-id="302dd-550">36 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-550">36 characters</span></span>|<span data-ttu-id="302dd-551">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-551">✔</span></span>|<span data-ttu-id="302dd-552">Id. de aplicación de AAD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="302dd-552">AAD application id of the app.</span></span> <span data-ttu-id="302dd-553">Este identificador debe ser un GUID.</span><span class="sxs-lookup"><span data-stu-id="302dd-553">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="302dd-554">string</span><span class="sxs-lookup"><span data-stu-id="302dd-554">string</span></span>|<span data-ttu-id="302dd-555">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-555">2048 characters</span></span>|<span data-ttu-id="302dd-556">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-556">✔</span></span>|<span data-ttu-id="302dd-557">Dirección URL de recurso de la aplicación para adquirir token de autenticación para SSO.</span><span class="sxs-lookup"><span data-stu-id="302dd-557">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="302dd-558">**NOTA:** Si no usa SSO, asegúrese de escribir un valor de cadena ficticia en este campo en el manifiesto de la aplicación, por ejemplo, para evitar https://notapplicable una respuesta de error.</span><span class="sxs-lookup"><span data-stu-id="302dd-558">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="302dd-559">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="302dd-559">array of strings</span></span>|<span data-ttu-id="302dd-560">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-560">128 characters</span></span>||<span data-ttu-id="302dd-561">Especifique el consentimiento [específico del recurso pormenorizados](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span><span class="sxs-lookup"><span data-stu-id="302dd-561">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="302dd-562">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="302dd-562">showLoadingIndicator</span></span>

<span data-ttu-id="302dd-563">**Opcional:** booleano</span><span class="sxs-lookup"><span data-stu-id="302dd-563">**Optional** — boolean</span></span>

<span data-ttu-id="302dd-564">Indica si se va a mostrar el indicador de carga cuando se carga una aplicación o una pestaña.</span><span class="sxs-lookup"><span data-stu-id="302dd-564">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="302dd-565">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="302dd-565">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="302dd-566">Si seleccionas como true en el manifiesto de la aplicación, para cargar la página correctamente, modifica las páginas de contenido de las pestañas y los módulos de tareas como se describe en Mostrar un documento de indicador de carga `showLoadingIndicator` nativo. [](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="302dd-566">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="302dd-567">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="302dd-567">isFullScreen</span></span>

 <span data-ttu-id="302dd-568">**Opcional:** booleano</span><span class="sxs-lookup"><span data-stu-id="302dd-568">**Optional** — boolean</span></span>

<span data-ttu-id="302dd-569">Indica dónde se representa una aplicación personal con o sin una barra de encabezado de pestaña.</span><span class="sxs-lookup"><span data-stu-id="302dd-569">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="302dd-570">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="302dd-570">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="302dd-571">activities</span><span class="sxs-lookup"><span data-stu-id="302dd-571">activities</span></span>

<span data-ttu-id="302dd-572">**Opcional** : objeto</span><span class="sxs-lookup"><span data-stu-id="302dd-572">**Optional** — object</span></span>

<span data-ttu-id="302dd-573">Define las propiedades que usa la aplicación para publicar una fuente de actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="302dd-573">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="302dd-574">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-574">Name</span></span>| <span data-ttu-id="302dd-575">Tipo</span><span class="sxs-lookup"><span data-stu-id="302dd-575">Type</span></span>| <span data-ttu-id="302dd-576">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-576">Maximum size</span></span> | <span data-ttu-id="302dd-577">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-577">Required</span></span> | <span data-ttu-id="302dd-578">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-578">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="302dd-579">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="302dd-579">array of Objects</span></span>|<span data-ttu-id="302dd-580">128 elementos</span><span class="sxs-lookup"><span data-stu-id="302dd-580">128 items</span></span>| | <span data-ttu-id="302dd-581">Proporciona los tipos de actividades que la aplicación puede publicar en una fuente de actividad de usuarios.</span><span class="sxs-lookup"><span data-stu-id="302dd-581">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="302dd-582">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="302dd-582">activities.activityTypes</span></span>

|<span data-ttu-id="302dd-583">Nombre</span><span class="sxs-lookup"><span data-stu-id="302dd-583">Name</span></span>| <span data-ttu-id="302dd-584">Tipo</span><span class="sxs-lookup"><span data-stu-id="302dd-584">Type</span></span>| <span data-ttu-id="302dd-585">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="302dd-585">Maximum size</span></span> | <span data-ttu-id="302dd-586">Necesario</span><span class="sxs-lookup"><span data-stu-id="302dd-586">Required</span></span> | <span data-ttu-id="302dd-587">Descripción</span><span class="sxs-lookup"><span data-stu-id="302dd-587">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="302dd-588">string</span><span class="sxs-lookup"><span data-stu-id="302dd-588">string</span></span>|<span data-ttu-id="302dd-589">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-589">32 characters</span></span>|<span data-ttu-id="302dd-590">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-590">✔</span></span>|<span data-ttu-id="302dd-591">Tipo de notificación.</span><span class="sxs-lookup"><span data-stu-id="302dd-591">The notification type.</span></span> <span data-ttu-id="302dd-592">*Vea a continuación*.</span><span class="sxs-lookup"><span data-stu-id="302dd-592">*See below*.</span></span>|
|`description`|<span data-ttu-id="302dd-593">string</span><span class="sxs-lookup"><span data-stu-id="302dd-593">string</span></span>|<span data-ttu-id="302dd-594">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-594">128 characters</span></span>|<span data-ttu-id="302dd-595">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-595">✔</span></span>|<span data-ttu-id="302dd-596">Breve descripción de la notificación.</span><span class="sxs-lookup"><span data-stu-id="302dd-596">A brief description of the notification.</span></span> <span data-ttu-id="302dd-597">*Vea a continuación*.</span><span class="sxs-lookup"><span data-stu-id="302dd-597">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="302dd-598">string</span><span class="sxs-lookup"><span data-stu-id="302dd-598">string</span></span>|<span data-ttu-id="302dd-599">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="302dd-599">128 characters</span></span>|<span data-ttu-id="302dd-600">✔</span><span class="sxs-lookup"><span data-stu-id="302dd-600">✔</span></span>|<span data-ttu-id="302dd-601">Ex: "{actor} created task {taskId} for you"</span><span class="sxs-lookup"><span data-stu-id="302dd-601">Ex: "{actor} created task {taskId} for you"</span></span>|

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
