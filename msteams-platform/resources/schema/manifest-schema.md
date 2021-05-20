---
title: Referencia de esquema manifiesto
description: Describe el esquema de manifiesto para Microsoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: equipos manifiestan esquema
ms.openlocfilehash: 6c7cd02480f78d19aed269b5d78d0c6f470621d2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566449"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="54f4e-104">Referencia: Esquema de manifiesto para Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="54f4e-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="54f4e-105">El manifiesto Teams describe cómo se integra la aplicación en el producto Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="54f4e-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="54f4e-106">El manifiesto debe ajustarse al esquema hospedado en [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="54f4e-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="54f4e-107">Las versiones anteriores 1.0, 1.1,..., 1.6, etc., también son compatibles (usando "v1.x" en la DIRECCIÓN URL).</span><span class="sxs-lookup"><span data-stu-id="54f4e-107">Previous versions 1.0, 1.1,..., 1.6, and so on are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="54f4e-108">En el ejemplo de esquema siguiente se muestran todas las opciones de extensibilidad:</span><span class="sxs-lookup"><span data-stu-id="54f4e-108">The following schema sample shows all extensibility options:</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="54f4e-109">Muestra de manifiesto completo</span><span class="sxs-lookup"><span data-stu-id="54f4e-109">Sample full manifest</span></span>

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
     "websiteUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ]              
}
```

<span data-ttu-id="54f4e-110">El esquema define las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="54f4e-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="54f4e-111">$schema</span><span class="sxs-lookup"><span data-stu-id="54f4e-111">$schema</span></span>

<span data-ttu-id="54f4e-112">Opcional, pero recomendado — cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-112">Optional, but recommended — string</span></span>

<span data-ttu-id="54f4e-113">La dirección URL https:// que hace referencia al esquema JSON del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="54f4e-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="54f4e-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="54f4e-114">manifestVersion</span></span>

<span data-ttu-id="54f4e-115">**Requerido** — cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-115">**Required** — string</span></span>

<span data-ttu-id="54f4e-116">La versión del esquema de manifiesto que este manifiesto está utilizando.</span><span class="sxs-lookup"><span data-stu-id="54f4e-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="54f4e-117">Debe ser 1.10.</span><span class="sxs-lookup"><span data-stu-id="54f4e-117">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="54f4e-118">version</span><span class="sxs-lookup"><span data-stu-id="54f4e-118">version</span></span>

<span data-ttu-id="54f4e-119">**Requerido** — cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-119">**Required** — string</span></span>

<span data-ttu-id="54f4e-120">La versión de una aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="54f4e-120">The version of a specific app.</span></span> <span data-ttu-id="54f4e-121">Si actualiza algo en el manifiesto, la versión también debe incrementarse.</span><span class="sxs-lookup"><span data-stu-id="54f4e-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="54f4e-122">De esta manera, cuando se instala el nuevo manifiesto, sobrescribe el existente y el usuario recibe la nueva funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="54f4e-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="54f4e-123">Si esta aplicación se envió a la tienda, el nuevo manifiesto debe volver a enviarse y volver a validarse.</span><span class="sxs-lookup"><span data-stu-id="54f4e-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="54f4e-124">Los usuarios de la aplicación reciben el nuevo manifiesto actualizado automáticamente dentro de las pocas horas después de la aprobación del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="54f4e-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="54f4e-125">Si las solicitudes de permisos de la aplicación cambian, se pide a los usuarios que actualicen y vuelvan a dar su consentimiento a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="54f4e-126">Esta cadena de versión debe seguir el estándar [de semver](http://semver.org/) (MAJOR. menor. PARCHE).</span><span class="sxs-lookup"><span data-stu-id="54f4e-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="54f4e-127">id</span><span class="sxs-lookup"><span data-stu-id="54f4e-127">id</span></span>

<span data-ttu-id="54f4e-128">**Obligatorio** : identificador de aplicación de Microsoft</span><span class="sxs-lookup"><span data-stu-id="54f4e-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="54f4e-129">El identificador es un identificador único generado por Microsoft para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="54f4e-130">Tienes un identificador si el bot está registrado a través de la Microsoft Bot Framework o la aplicación web de tu pestaña ya inicia sesión con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54f4e-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="54f4e-131">Debe introducir el ID aquí.</span><span class="sxs-lookup"><span data-stu-id="54f4e-131">You must enter the ID here.</span></span> <span data-ttu-id="54f4e-132">De lo contrario, debe generar un nuevo identificador en el [Portal de registro de aplicaciones de Microsoft.](https://aka.ms/appregistrations)</span><span class="sxs-lookup"><span data-stu-id="54f4e-132">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="54f4e-133">Utilice el mismo ID si agrega un bot.</span><span class="sxs-lookup"><span data-stu-id="54f4e-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="54f4e-134">Si va a enviar una actualización a la aplicación existente en AppSource, el identificador del manifiesto no debe modificarse.</span><span class="sxs-lookup"><span data-stu-id="54f4e-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="54f4e-135">developer</span><span class="sxs-lookup"><span data-stu-id="54f4e-135">developer</span></span>

<span data-ttu-id="54f4e-136">**Requerido** — objeto</span><span class="sxs-lookup"><span data-stu-id="54f4e-136">**Required** — object</span></span>

<span data-ttu-id="54f4e-137">Especifica información sobre su empresa.</span><span class="sxs-lookup"><span data-stu-id="54f4e-137">Specifies information about your company.</span></span> <span data-ttu-id="54f4e-138">Para las aplicaciones enviadas a la tienda Teams, estos valores deben coincidir con la información de la lista de la tienda.</span><span class="sxs-lookup"><span data-stu-id="54f4e-138">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="54f4e-139">Para obtener más información, consulte las [directrices de publicación de Teams tienda.](~/concepts/deploy-and-publish/appsource/publish.md)</span><span class="sxs-lookup"><span data-stu-id="54f4e-139">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="54f4e-140">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-140">Name</span></span>| <span data-ttu-id="54f4e-141">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-141">Maximum size</span></span> | <span data-ttu-id="54f4e-142">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-142">Required</span></span> | <span data-ttu-id="54f4e-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="54f4e-144">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-144">32 characters</span></span>|<span data-ttu-id="54f4e-145">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-145">✔</span></span>|<span data-ttu-id="54f4e-146">El nombre para mostrar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="54f4e-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="54f4e-147">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-147">2048 characters</span></span>|<span data-ttu-id="54f4e-148">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-148">✔</span></span>|<span data-ttu-id="54f4e-149">La URL de https:// al sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="54f4e-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="54f4e-150">Este enlace debe llevar a los usuarios a su empresa o página de destino específica del producto.</span><span class="sxs-lookup"><span data-stu-id="54f4e-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="54f4e-151">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-151">2048 characters</span></span>|<span data-ttu-id="54f4e-152">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-152">✔</span></span>|<span data-ttu-id="54f4e-153">La dirección URL de https:// a la política de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="54f4e-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="54f4e-154">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-154">2048 characters</span></span>|<span data-ttu-id="54f4e-155">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-155">✔</span></span>|<span data-ttu-id="54f4e-156">La dirección URL https:// a los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="54f4e-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="54f4e-157">10 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-157">10 characters</span></span>| |<span data-ttu-id="54f4e-158">**Opcional** Identificador de red de partners de Microsoft que identifica la organización asociada que compilará la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="54f4e-159">name</span><span class="sxs-lookup"><span data-stu-id="54f4e-159">name</span></span>

<span data-ttu-id="54f4e-160">**Requerido** — objeto</span><span class="sxs-lookup"><span data-stu-id="54f4e-160">**Required** — object</span></span>

<span data-ttu-id="54f4e-161">El nombre de la experiencia de la aplicación, que se muestra a los usuarios en la experiencia Teams.</span><span class="sxs-lookup"><span data-stu-id="54f4e-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="54f4e-162">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource.</span><span class="sxs-lookup"><span data-stu-id="54f4e-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="54f4e-163">Los valores de `short` y `full` debe ser diferente.</span><span class="sxs-lookup"><span data-stu-id="54f4e-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="54f4e-164">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-164">Name</span></span>| <span data-ttu-id="54f4e-165">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-165">Maximum size</span></span> | <span data-ttu-id="54f4e-166">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-166">Required</span></span> | <span data-ttu-id="54f4e-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="54f4e-168">30 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-168">30 characters</span></span>|<span data-ttu-id="54f4e-169">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-169">✔</span></span>|<span data-ttu-id="54f4e-170">El nombre para mostrar corto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="54f4e-171">100 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-171">100 characters</span></span>||<span data-ttu-id="54f4e-172">El nombre completo de la aplicación, utilizado si el nombre completo de la aplicación supera los 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="54f4e-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="54f4e-173">description</span><span class="sxs-lookup"><span data-stu-id="54f4e-173">description</span></span>

<span data-ttu-id="54f4e-174">**Requerido** — objeto</span><span class="sxs-lookup"><span data-stu-id="54f4e-174">**Required** — object</span></span>

<span data-ttu-id="54f4e-175">Describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="54f4e-175">Describes your app to users.</span></span> <span data-ttu-id="54f4e-176">Para las aplicaciones enviadas a AppSource, estos valores deben coincidir con la información de la entrada de AppSource.</span><span class="sxs-lookup"><span data-stu-id="54f4e-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="54f4e-177">Asegúrese de que su descripción describe con precisión su experiencia y proporciona información para ayudar a los clientes potenciales a entender lo que hace su experiencia.</span><span class="sxs-lookup"><span data-stu-id="54f4e-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="54f4e-178">Debe tener en cuenta en la descripción completa, si se requiere una cuenta externa para su uso.</span><span class="sxs-lookup"><span data-stu-id="54f4e-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="54f4e-179">Los valores de `short` y `full` debe ser diferente.</span><span class="sxs-lookup"><span data-stu-id="54f4e-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="54f4e-180">La breve descripción no debe repetirse dentro de la descripción larga y no debe incluir ningún otro nombre de aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="54f4e-181">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-181">Name</span></span>| <span data-ttu-id="54f4e-182">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-182">Maximum size</span></span> | <span data-ttu-id="54f4e-183">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-183">Required</span></span> | <span data-ttu-id="54f4e-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="54f4e-185">80 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-185">80 characters</span></span>|<span data-ttu-id="54f4e-186">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-186">✔</span></span>|<span data-ttu-id="54f4e-187">Una breve descripción de la experiencia de la aplicación, utilizada cuando el espacio es limitado.</span><span class="sxs-lookup"><span data-stu-id="54f4e-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="54f4e-188">4000 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-188">4000 characters</span></span>|<span data-ttu-id="54f4e-189">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-189">✔</span></span>|<span data-ttu-id="54f4e-190">La descripción completa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="54f4e-191">packageName</span><span class="sxs-lookup"><span data-stu-id="54f4e-191">packageName</span></span>

<span data-ttu-id="54f4e-192">**Opcional** — cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-192">**Optional** — string</span></span>

<span data-ttu-id="54f4e-193">Un identificador único para la aplicación en notación de dominio inverso; por ejemplo, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="54f4e-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="54f4e-194">Longitud máxima: 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="54f4e-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="54f4e-195">localizaciónInfo</span><span class="sxs-lookup"><span data-stu-id="54f4e-195">localizationInfo</span></span>

<span data-ttu-id="54f4e-196">**Opcional** — objeto</span><span class="sxs-lookup"><span data-stu-id="54f4e-196">**Optional** — object</span></span>

<span data-ttu-id="54f4e-197">Permite la especificación de un idioma predeterminado, así como punteros a archivos de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="54f4e-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="54f4e-198">Para obtener más información, consulte [localización](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="54f4e-198">For more information, see [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="54f4e-199">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-199">Name</span></span>| <span data-ttu-id="54f4e-200">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-200">Maximum size</span></span> | <span data-ttu-id="54f4e-201">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-201">Required</span></span> | <span data-ttu-id="54f4e-202">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="54f4e-203">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-203">✔</span></span>|<span data-ttu-id="54f4e-204">La etiqueta de idioma de las cadenas de este archivo de manifiesto de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="54f4e-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="54f4e-205">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="54f4e-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="54f4e-206">Matriz de objetos que especifica traducciones de idioma adicionales.</span><span class="sxs-lookup"><span data-stu-id="54f4e-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="54f4e-207">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-207">Name</span></span>| <span data-ttu-id="54f4e-208">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-208">Maximum size</span></span> | <span data-ttu-id="54f4e-209">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-209">Required</span></span> | <span data-ttu-id="54f4e-210">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="54f4e-211">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-211">✔</span></span>|<span data-ttu-id="54f4e-212">La etiqueta de idioma de las cadenas del archivo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="54f4e-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="54f4e-213">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-213">✔</span></span>|<span data-ttu-id="54f4e-214">Una ruta de acceso de archivo relativa a un archivo .json que contiene las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="54f4e-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="54f4e-215">iconos</span><span class="sxs-lookup"><span data-stu-id="54f4e-215">icons</span></span>

<span data-ttu-id="54f4e-216">**Requerido** — objeto</span><span class="sxs-lookup"><span data-stu-id="54f4e-216">**Required** — object</span></span>

<span data-ttu-id="54f4e-217">Iconos utilizados en la aplicación Teams.</span><span class="sxs-lookup"><span data-stu-id="54f4e-217">Icons used within the Teams app.</span></span> <span data-ttu-id="54f4e-218">Los archivos de icono deben incluirse como parte del paquete de carga.</span><span class="sxs-lookup"><span data-stu-id="54f4e-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="54f4e-219">Consulte [Iconos](../../concepts/build-and-test/apps-package.md#app-icons) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="54f4e-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="54f4e-220">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-220">Name</span></span>| <span data-ttu-id="54f4e-221">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-221">Maximum size</span></span> | <span data-ttu-id="54f4e-222">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-222">Required</span></span> | <span data-ttu-id="54f4e-223">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="54f4e-224">32 x 32 píxeles</span><span class="sxs-lookup"><span data-stu-id="54f4e-224">32 x 32 pixels</span></span>|<span data-ttu-id="54f4e-225">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-225">✔</span></span>|<span data-ttu-id="54f4e-226">Una ruta de acceso de archivo relativa a un icono de contorno PNG 32x32 transparente.</span><span class="sxs-lookup"><span data-stu-id="54f4e-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="54f4e-227">192 x 192 píxeles</span><span class="sxs-lookup"><span data-stu-id="54f4e-227">192 x 192 pixels</span></span>|<span data-ttu-id="54f4e-228">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-228">✔</span></span>|<span data-ttu-id="54f4e-229">Una ruta de acceso de archivo relativa a un icono PNG 192x192 a todo color.</span><span class="sxs-lookup"><span data-stu-id="54f4e-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="54f4e-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="54f4e-230">accentColor</span></span>

<span data-ttu-id="54f4e-231">**Opcional** — Código de color HTML Hexagonal</span><span class="sxs-lookup"><span data-stu-id="54f4e-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="54f4e-232">Un color para usar junto con y como fondo para los iconos de contorno.</span><span class="sxs-lookup"><span data-stu-id="54f4e-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="54f4e-233">El valor debe ser un código de color HTML válido que comience por '#', por `#4464ee` ejemplo.</span><span class="sxs-lookup"><span data-stu-id="54f4e-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="54f4e-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="54f4e-234">configurableTabs</span></span>

<span data-ttu-id="54f4e-235">**Opcional** — matriz</span><span class="sxs-lookup"><span data-stu-id="54f4e-235">**Optional** — array</span></span>

<span data-ttu-id="54f4e-236">Se usa cuando la experiencia de la aplicación tiene una experiencia de pestaña de canal de equipo que requiere configuración adicional antes de agregarla.</span><span class="sxs-lookup"><span data-stu-id="54f4e-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="54f4e-237">Las pestañas configurables solo se admiten en el ámbito de los equipos y puede configurar las mismas pestañas varias veces.</span><span class="sxs-lookup"><span data-stu-id="54f4e-237">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="54f4e-238">Sin embargo, solo puede definirlo en el manifiesto una sola vez.</span><span class="sxs-lookup"><span data-stu-id="54f4e-238">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="54f4e-239">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-239">Name</span></span>| <span data-ttu-id="54f4e-240">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-240">Type</span></span>| <span data-ttu-id="54f4e-241">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-241">Maximum size</span></span> | <span data-ttu-id="54f4e-242">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-242">Required</span></span> | <span data-ttu-id="54f4e-243">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="54f4e-244">string</span><span class="sxs-lookup"><span data-stu-id="54f4e-244">string</span></span>|<span data-ttu-id="54f4e-245">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-245">2048 characters</span></span>|<span data-ttu-id="54f4e-246">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-246">✔</span></span>|<span data-ttu-id="54f4e-247">La dirección URL https:// que se usará al configurar la pestaña.</span><span class="sxs-lookup"><span data-stu-id="54f4e-247">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="54f4e-248">variedad de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="54f4e-248">array of enums</span></span>|<span data-ttu-id="54f4e-249">1</span><span class="sxs-lookup"><span data-stu-id="54f4e-249">1</span></span>|<span data-ttu-id="54f4e-250">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-250">✔</span></span>|<span data-ttu-id="54f4e-251">Actualmente, las pestañas configurables solo admiten el `team` `groupchat` ámbito.</span><span class="sxs-lookup"><span data-stu-id="54f4e-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="54f4e-252">boolean</span><span class="sxs-lookup"><span data-stu-id="54f4e-252">boolean</span></span>|||<span data-ttu-id="54f4e-253">Valor que indica si el usuario puede actualizar una instancia de la configuración de la pestaña después de la creación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-253">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="54f4e-254">Predeterminado: **true**.</span><span class="sxs-lookup"><span data-stu-id="54f4e-254">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="54f4e-255">variedad de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="54f4e-255">array of enums</span></span>|<span data-ttu-id="54f4e-256">6 </span><span class="sxs-lookup"><span data-stu-id="54f4e-256">6</span></span>||<span data-ttu-id="54f4e-257">El conjunto de `contextItem` ámbitos donde se admite una [pestaña.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="54f4e-257">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="54f4e-258">Valor predeterminado: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="54f4e-258">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="54f4e-259">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-259">string</span></span>|<span data-ttu-id="54f4e-260">2048</span><span class="sxs-lookup"><span data-stu-id="54f4e-260">2048</span></span>||<span data-ttu-id="54f4e-261">Una ruta de acceso de archivo relativa a una imagen de vista previa de tabulación para su uso en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="54f4e-261">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="54f4e-262">Tamaño 1024x768.</span><span class="sxs-lookup"><span data-stu-id="54f4e-262">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="54f4e-263">variedad de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="54f4e-263">array of enums</span></span>|<span data-ttu-id="54f4e-264">1</span><span class="sxs-lookup"><span data-stu-id="54f4e-264">1</span></span>||<span data-ttu-id="54f4e-265">Define cómo la pestaña está disponible en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="54f4e-265">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="54f4e-266">Las opciones son `sharePointFullPage` y `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="54f4e-266">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="54f4e-267">staticTabs</span><span class="sxs-lookup"><span data-stu-id="54f4e-267">staticTabs</span></span>

<span data-ttu-id="54f4e-268">**Opcional** — matriz</span><span class="sxs-lookup"><span data-stu-id="54f4e-268">**Optional** — array</span></span>

<span data-ttu-id="54f4e-269">Define un conjunto de pestañas que se pueden "anclar" de forma predeterminada, sin que el usuario las agregue manualmente.</span><span class="sxs-lookup"><span data-stu-id="54f4e-269">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="54f4e-270">Las pestañas estáticas declaradas en `personal` el ámbito siempre están ancladas a la experiencia personal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-270">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="54f4e-271">Actualmente no se admiten pestañas estáticas declaradas en el `team` ámbito.</span><span class="sxs-lookup"><span data-stu-id="54f4e-271">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="54f4e-272">Este elemento es una matriz (máximo de 16 elementos) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-272">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="54f4e-273">Este bloque solo es necesario para soluciones que proporcionan una solución de pestaña estática.</span><span class="sxs-lookup"><span data-stu-id="54f4e-273">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="54f4e-274">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-274">Name</span></span>| <span data-ttu-id="54f4e-275">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-275">Type</span></span>| <span data-ttu-id="54f4e-276">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-276">Maximum size</span></span> | <span data-ttu-id="54f4e-277">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-277">Required</span></span> | <span data-ttu-id="54f4e-278">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-278">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="54f4e-279">string</span><span class="sxs-lookup"><span data-stu-id="54f4e-279">string</span></span>|<span data-ttu-id="54f4e-280">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-280">64 characters</span></span>|<span data-ttu-id="54f4e-281">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-281">✔</span></span>|<span data-ttu-id="54f4e-282">Identificador único de la entidad que muestra la pestaña.</span><span class="sxs-lookup"><span data-stu-id="54f4e-282">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="54f4e-283">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-283">string</span></span>|<span data-ttu-id="54f4e-284">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-284">128 characters</span></span>|<span data-ttu-id="54f4e-285">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-285">✔</span></span>|<span data-ttu-id="54f4e-286">El nombre para mostrar de la pestaña en la interfaz del canal.</span><span class="sxs-lookup"><span data-stu-id="54f4e-286">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="54f4e-287">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-287">string</span></span>||<span data-ttu-id="54f4e-288">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-288">✔</span></span>|<span data-ttu-id="54f4e-289">La dirección URL de https:// que apunta a la interfaz de usuario de la entidad que se mostrará en el lienzo de Teams.</span><span class="sxs-lookup"><span data-stu-id="54f4e-289">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="54f4e-290">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-290">string</span></span>|||<span data-ttu-id="54f4e-291">La dirección URL https:// a la que apuntar si un usuario opta por verlo en un explorador.</span><span class="sxs-lookup"><span data-stu-id="54f4e-291">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="54f4e-292">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-292">string</span></span>|||<span data-ttu-id="54f4e-293">La dirección URL https:// a la que se debe apuntar para las consultas de búsqueda de un usuario.</span><span class="sxs-lookup"><span data-stu-id="54f4e-293">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="54f4e-294">variedad de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="54f4e-294">array of enums</span></span>|<span data-ttu-id="54f4e-295">1</span><span class="sxs-lookup"><span data-stu-id="54f4e-295">1</span></span>|<span data-ttu-id="54f4e-296">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-296">✔</span></span>|<span data-ttu-id="54f4e-297">Actualmente, las pestañas estáticas solo admiten el `personal` ámbito, lo que significa que solo se puede aprovisionar como parte de la experiencia personal.</span><span class="sxs-lookup"><span data-stu-id="54f4e-297">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="54f4e-298">variedad de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="54f4e-298">array of enums</span></span>| <span data-ttu-id="54f4e-299">2</span><span class="sxs-lookup"><span data-stu-id="54f4e-299">2</span></span>|| <span data-ttu-id="54f4e-300">El conjunto de `contextItem` ámbitos donde se admite una pestaña.</span><span class="sxs-lookup"><span data-stu-id="54f4e-300">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="54f4e-301">La característica searchUrl no está disponible para los desarrolladores de terceros.</span><span class="sxs-lookup"><span data-stu-id="54f4e-301">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="54f4e-302">Si las pestañas requieren información dependiente del contexto para mostrar contenido relevante o para iniciar un flujo de autenticación, para obtener más información, consulte [Obtener contexto para la pestaña Microsoft Teams](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="54f4e-302">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="54f4e-303">Bots</span><span class="sxs-lookup"><span data-stu-id="54f4e-303">bots</span></span>

<span data-ttu-id="54f4e-304">**Opcional** — matriz</span><span class="sxs-lookup"><span data-stu-id="54f4e-304">**Optional** — array</span></span>

<span data-ttu-id="54f4e-305">Define una solución de bot, junto con información opcional, como las propiedades de comando predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="54f4e-305">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="54f4e-306">El elemento es una matriz (máximo de solo 1 elemento &mdash; actualmente solo se permite un bot por aplicación) con todos los elementos del tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-306">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="54f4e-307">Este bloque solo es necesario para soluciones que proporcionan una experiencia de bot.</span><span class="sxs-lookup"><span data-stu-id="54f4e-307">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="54f4e-308">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-308">Name</span></span>| <span data-ttu-id="54f4e-309">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-309">Type</span></span>| <span data-ttu-id="54f4e-310">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-310">Maximum size</span></span> | <span data-ttu-id="54f4e-311">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-311">Required</span></span> | <span data-ttu-id="54f4e-312">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-312">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="54f4e-313">string</span><span class="sxs-lookup"><span data-stu-id="54f4e-313">string</span></span>|<span data-ttu-id="54f4e-314">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-314">64 characters</span></span>|<span data-ttu-id="54f4e-315">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-315">✔</span></span>|<span data-ttu-id="54f4e-316">El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="54f4e-316">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="54f4e-317">Esto bien puede ser el mismo que el IDENTIFICADOR general de la [aplicación.](#id)</span><span class="sxs-lookup"><span data-stu-id="54f4e-317">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="54f4e-318">variedad de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="54f4e-318">array of enums</span></span>|<span data-ttu-id="54f4e-319">3</span><span class="sxs-lookup"><span data-stu-id="54f4e-319">3</span></span>|<span data-ttu-id="54f4e-320">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-320">✔</span></span>|<span data-ttu-id="54f4e-321">Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`).</span><span class="sxs-lookup"><span data-stu-id="54f4e-321">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="54f4e-322">Estas opciones no son exclusivas.</span><span class="sxs-lookup"><span data-stu-id="54f4e-322">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="54f4e-323">boolean</span><span class="sxs-lookup"><span data-stu-id="54f4e-323">boolean</span></span>|||<span data-ttu-id="54f4e-324">Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico.</span><span class="sxs-lookup"><span data-stu-id="54f4e-324">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="54f4e-325">predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="54f4e-325">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="54f4e-326">boolean</span><span class="sxs-lookup"><span data-stu-id="54f4e-326">boolean</span></span>|||<span data-ttu-id="54f4e-327">Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-327">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="54f4e-328">predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="54f4e-328">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="54f4e-329">boolean</span><span class="sxs-lookup"><span data-stu-id="54f4e-329">boolean</span></span>|||<span data-ttu-id="54f4e-330">Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal.</span><span class="sxs-lookup"><span data-stu-id="54f4e-330">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="54f4e-331">predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="54f4e-331">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="54f4e-332">boolean</span><span class="sxs-lookup"><span data-stu-id="54f4e-332">boolean</span></span>|||<span data-ttu-id="54f4e-333">Valor que indica dónde un bot admite llamadas de audio.</span><span class="sxs-lookup"><span data-stu-id="54f4e-333">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="54f4e-334">**IMPORTANTE**: Esta propiedad es actualmente experimental.</span><span class="sxs-lookup"><span data-stu-id="54f4e-334">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="54f4e-335">Es posible que las propiedades experimentales no estén completas y puedan sufrir cambios antes de estar completamente disponibles.</span><span class="sxs-lookup"><span data-stu-id="54f4e-335">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="54f4e-336">Se proporciona únicamente con fines de pruebas y exploración y no debe utilizarse en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="54f4e-336">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="54f4e-337">predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="54f4e-337">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="54f4e-338">boolean</span><span class="sxs-lookup"><span data-stu-id="54f4e-338">boolean</span></span>|||<span data-ttu-id="54f4e-339">Valor que indica dónde un bot admite videollamadas.</span><span class="sxs-lookup"><span data-stu-id="54f4e-339">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="54f4e-340">**IMPORTANTE**: Esta propiedad es actualmente experimental.</span><span class="sxs-lookup"><span data-stu-id="54f4e-340">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="54f4e-341">Es posible que las propiedades experimentales no estén completas y puedan sufrir cambios antes de estar completamente disponibles.</span><span class="sxs-lookup"><span data-stu-id="54f4e-341">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="54f4e-342">Se proporciona únicamente con fines de pruebas y exploración y no debe utilizarse en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="54f4e-342">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="54f4e-343">predeterminado: **`false`**</span><span class="sxs-lookup"><span data-stu-id="54f4e-343">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="54f4e-344">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="54f4e-344">bots.commandLists</span></span>

<span data-ttu-id="54f4e-345">Una lista opcional de comandos que el bot puede recomendar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="54f4e-345">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="54f4e-346">El objeto es una matriz (máximo de 2 elementos) con todos los elementos de tipo; debe definir una lista de `object` comandos independiente para cada ámbito que admita el bot.</span><span class="sxs-lookup"><span data-stu-id="54f4e-346">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="54f4e-347">Consulte [menús bot](~/bots/how-to/create-a-bot-commands-menu.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="54f4e-347">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="54f4e-348">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-348">Name</span></span>| <span data-ttu-id="54f4e-349">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-349">Type</span></span>| <span data-ttu-id="54f4e-350">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-350">Maximum size</span></span> | <span data-ttu-id="54f4e-351">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-351">Required</span></span> | <span data-ttu-id="54f4e-352">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-352">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="54f4e-353">variedad de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="54f4e-353">array of enums</span></span>|<span data-ttu-id="54f4e-354">3</span><span class="sxs-lookup"><span data-stu-id="54f4e-354">3</span></span>|<span data-ttu-id="54f4e-355">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-355">✔</span></span>|<span data-ttu-id="54f4e-356">Especifica el ámbito para el que la lista de comandos es válida.</span><span class="sxs-lookup"><span data-stu-id="54f4e-356">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="54f4e-357">Las opciones son `team`, `personal` y `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="54f4e-357">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="54f4e-358">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="54f4e-358">array of objects</span></span>|<span data-ttu-id="54f4e-359">10</span><span class="sxs-lookup"><span data-stu-id="54f4e-359">10</span></span>|<span data-ttu-id="54f4e-360">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-360">✔</span></span>|<span data-ttu-id="54f4e-361">Una matriz de comandos que el bot admite:</span><span class="sxs-lookup"><span data-stu-id="54f4e-361">An array of commands the bot supports:</span></span><br><span data-ttu-id="54f4e-362">`title`: el nombre de comando del bot (cadena, 32)</span><span class="sxs-lookup"><span data-stu-id="54f4e-362">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="54f4e-363">`description`: una descripción simple o ejemplo de la sintaxis del comando y su argumento (cadena, 128).</span><span class="sxs-lookup"><span data-stu-id="54f4e-363">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="54f4e-364">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="54f4e-364">bots.commandLists.commands</span></span>

|<span data-ttu-id="54f4e-365">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-365">Name</span></span>| <span data-ttu-id="54f4e-366">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-366">Type</span></span>| <span data-ttu-id="54f4e-367">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-367">Maximum size</span></span> | <span data-ttu-id="54f4e-368">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-368">Required</span></span> | <span data-ttu-id="54f4e-369">Description</span><span class="sxs-lookup"><span data-stu-id="54f4e-369">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="54f4e-370">title</span><span class="sxs-lookup"><span data-stu-id="54f4e-370">title</span></span>|<span data-ttu-id="54f4e-371">string</span><span class="sxs-lookup"><span data-stu-id="54f4e-371">string</span></span>|<span data-ttu-id="54f4e-372">12 </span><span class="sxs-lookup"><span data-stu-id="54f4e-372">12</span></span>|<span data-ttu-id="54f4e-373">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-373">✔</span></span>|<span data-ttu-id="54f4e-374">El nombre del comando bot.</span><span class="sxs-lookup"><span data-stu-id="54f4e-374">The bot command name.</span></span>|
|<span data-ttu-id="54f4e-375">description</span><span class="sxs-lookup"><span data-stu-id="54f4e-375">description</span></span>|<span data-ttu-id="54f4e-376">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-376">string</span></span>|<span data-ttu-id="54f4e-377">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-377">128 characters</span></span>|<span data-ttu-id="54f4e-378">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-378">✔</span></span>|<span data-ttu-id="54f4e-379">Una descripción de texto simple o un ejemplo de la sintaxis del comando y sus argumentos.</span><span class="sxs-lookup"><span data-stu-id="54f4e-379">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="54f4e-380">Conectores</span><span class="sxs-lookup"><span data-stu-id="54f4e-380">connectors</span></span>

<span data-ttu-id="54f4e-381">**Opcional** — matriz</span><span class="sxs-lookup"><span data-stu-id="54f4e-381">**Optional** — array</span></span>

<span data-ttu-id="54f4e-382">El `connectors` bloque define un conector de Office 365 para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-382">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="54f4e-383">El objeto es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-383">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="54f4e-384">Este bloque solo es necesario para las soluciones que proporcionan un conector.</span><span class="sxs-lookup"><span data-stu-id="54f4e-384">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="54f4e-385">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-385">Name</span></span>| <span data-ttu-id="54f4e-386">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-386">Type</span></span>| <span data-ttu-id="54f4e-387">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-387">Maximum size</span></span> | <span data-ttu-id="54f4e-388">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-388">Required</span></span> | <span data-ttu-id="54f4e-389">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-389">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="54f4e-390">string</span><span class="sxs-lookup"><span data-stu-id="54f4e-390">string</span></span>|<span data-ttu-id="54f4e-391">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-391">2048 characters</span></span>|<span data-ttu-id="54f4e-392">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-392">✔</span></span>|<span data-ttu-id="54f4e-393">La dirección URL https:// que se usará al configurar el conector.</span><span class="sxs-lookup"><span data-stu-id="54f4e-393">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="54f4e-394">variedad de enumeraciones</span><span class="sxs-lookup"><span data-stu-id="54f4e-394">array of enums</span></span>|<span data-ttu-id="54f4e-395">1</span><span class="sxs-lookup"><span data-stu-id="54f4e-395">1</span></span>|<span data-ttu-id="54f4e-396">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-396">✔</span></span>|<span data-ttu-id="54f4e-397">Especifica si connector ofrece una experiencia en el contexto de un canal en un `team` objeto y una experiencia con ámbito a un usuario individual solo ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="54f4e-397">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="54f4e-398">Actualmente, solo se admite el `team` ámbito.</span><span class="sxs-lookup"><span data-stu-id="54f4e-398">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="54f4e-399">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-399">string</span></span>|<span data-ttu-id="54f4e-400">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-400">64 characters</span></span>|<span data-ttu-id="54f4e-401">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-401">✔</span></span>|<span data-ttu-id="54f4e-402">Identificador único del conector que coincide con su identificador en el [panel de desarrollador de conectores.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="54f4e-402">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="54f4e-403">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="54f4e-403">composeExtensions</span></span>

<span data-ttu-id="54f4e-404">**Opcional** — matriz</span><span class="sxs-lookup"><span data-stu-id="54f4e-404">**Optional** — array</span></span>

<span data-ttu-id="54f4e-405">Define una extensión de mensajería para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-405">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="54f4e-406">El nombre de la característica se cambió de "extensión de composición" a "extensión de mensajería" en noviembre de 2017, pero el nombre del manifiesto sigue siendo el mismo para que las extensiones existentes sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="54f4e-406">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="54f4e-407">El elemento es una matriz (máximo de 1 elemento) con todos los elementos de tipo `object` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-407">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="54f4e-408">Este bloque solo es necesario para las soluciones que proporcionan una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="54f4e-408">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="54f4e-409">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-409">Name</span></span>| <span data-ttu-id="54f4e-410">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-410">Type</span></span> | <span data-ttu-id="54f4e-411">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-411">Maximum Size</span></span> | <span data-ttu-id="54f4e-412">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="54f4e-412">Required</span></span> | <span data-ttu-id="54f4e-413">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-413">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="54f4e-414">string</span><span class="sxs-lookup"><span data-stu-id="54f4e-414">string</span></span>|<span data-ttu-id="54f4e-415">64</span><span class="sxs-lookup"><span data-stu-id="54f4e-415">64</span></span>|<span data-ttu-id="54f4e-416">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-416">✔</span></span>|<span data-ttu-id="54f4e-417">El identificador único de la aplicación de Microsoft para el bot que respalda la extensión de mensajería, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="54f4e-417">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="54f4e-418">Esto bien puede ser el mismo que el ID de aplicación general.</span><span class="sxs-lookup"><span data-stu-id="54f4e-418">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="54f4e-419">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="54f4e-419">array of objects</span></span>|<span data-ttu-id="54f4e-420">10</span><span class="sxs-lookup"><span data-stu-id="54f4e-420">10</span></span>|<span data-ttu-id="54f4e-421">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-421">✔</span></span>|<span data-ttu-id="54f4e-422">Matriz de comandos que admite la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="54f4e-422">Array of commands the messaging extension supports.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="54f4e-423">boolean</span><span class="sxs-lookup"><span data-stu-id="54f4e-423">boolean</span></span>|||<span data-ttu-id="54f4e-424">Valor que indica si el usuario puede actualizar la configuración de una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="54f4e-424">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="54f4e-425">Valor predeterminado: **false**.</span><span class="sxs-lookup"><span data-stu-id="54f4e-425">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="54f4e-426">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="54f4e-426">array of Objects</span></span>|<span data-ttu-id="54f4e-427">5 </span><span class="sxs-lookup"><span data-stu-id="54f4e-427">5</span></span>||<span data-ttu-id="54f4e-428">Una lista de controladores que permiten invocar aplicaciones cuando se cumplen ciertas condiciones.</span><span class="sxs-lookup"><span data-stu-id="54f4e-428">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="54f4e-429">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-429">string</span></span>|||<span data-ttu-id="54f4e-430">El tipo de controlador de mensajes.</span><span class="sxs-lookup"><span data-stu-id="54f4e-430">The type of message handler.</span></span> <span data-ttu-id="54f4e-431">Debe ser `"link"`.</span><span class="sxs-lookup"><span data-stu-id="54f4e-431">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="54f4e-432">matriz de cuerdas</span><span class="sxs-lookup"><span data-stu-id="54f4e-432">array of Strings</span></span>|||<span data-ttu-id="54f4e-433">Matriz de dominios para los que el controlador de mensajes de vínculo puede registrarse.</span><span class="sxs-lookup"><span data-stu-id="54f4e-433">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="54f4e-434">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="54f4e-434">composeExtensions.commands</span></span>

<span data-ttu-id="54f4e-435">La extensión de mensajería debe declarar uno o varios comandos.</span><span class="sxs-lookup"><span data-stu-id="54f4e-435">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="54f4e-436">Cada comando aparece en Microsoft Teams como una interacción potencial desde el punto de entrada basado en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="54f4e-436">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="54f4e-437">Hay un máximo de 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="54f4e-437">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="54f4e-438">Cada elemento de comando es un objeto con la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="54f4e-438">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="54f4e-439">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-439">Name</span></span>| <span data-ttu-id="54f4e-440">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-440">Type</span></span>| <span data-ttu-id="54f4e-441">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-441">Maximum size</span></span> | <span data-ttu-id="54f4e-442">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-442">Required</span></span> | <span data-ttu-id="54f4e-443">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-443">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="54f4e-444">string</span><span class="sxs-lookup"><span data-stu-id="54f4e-444">string</span></span>|<span data-ttu-id="54f4e-445">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-445">64 characters</span></span>|<span data-ttu-id="54f4e-446">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-446">✔</span></span>|<span data-ttu-id="54f4e-447">El ID del comando.</span><span class="sxs-lookup"><span data-stu-id="54f4e-447">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="54f4e-448">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-448">string</span></span>|<span data-ttu-id="54f4e-449">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-449">32 characters</span></span>|<span data-ttu-id="54f4e-450">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-450">✔</span></span>|<span data-ttu-id="54f4e-451">El nombre del comando fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="54f4e-451">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="54f4e-452">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-452">string</span></span>|<span data-ttu-id="54f4e-453">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-453">64 characters</span></span>||<span data-ttu-id="54f4e-454">Tipo de comando.</span><span class="sxs-lookup"><span data-stu-id="54f4e-454">Type of the command.</span></span> <span data-ttu-id="54f4e-455">Uno de `query` o `action` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-455">One of `query` or `action`.</span></span> <span data-ttu-id="54f4e-456">Predeterminado: **consulta**.</span><span class="sxs-lookup"><span data-stu-id="54f4e-456">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="54f4e-457">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-457">string</span></span>|<span data-ttu-id="54f4e-458">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-458">128 characters</span></span>||<span data-ttu-id="54f4e-459">La descripción que aparece a los usuarios para indicar el propósito de este comando.</span><span class="sxs-lookup"><span data-stu-id="54f4e-459">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="54f4e-460">boolean</span><span class="sxs-lookup"><span data-stu-id="54f4e-460">boolean</span></span>|||<span data-ttu-id="54f4e-461">Un valor booleano indica si el comando se ejecuta inicialmente sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="54f4e-461">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="54f4e-462">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="54f4e-462">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="54f4e-463">matriz de cuerdas</span><span class="sxs-lookup"><span data-stu-id="54f4e-463">array of Strings</span></span>|<span data-ttu-id="54f4e-464">3</span><span class="sxs-lookup"><span data-stu-id="54f4e-464">3</span></span>||<span data-ttu-id="54f4e-465">Define desde dónde se puede invocar la extensión de mensaje.</span><span class="sxs-lookup"><span data-stu-id="54f4e-465">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="54f4e-466">Cualquier combinación de `compose` `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-466">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="54f4e-467">El valor predeterminado es `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="54f4e-467">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="54f4e-468">boolean</span><span class="sxs-lookup"><span data-stu-id="54f4e-468">boolean</span></span>|||<span data-ttu-id="54f4e-469">Valor booleano que indica si debe capturar el módulo de tareas dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="54f4e-469">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="54f4e-470">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="54f4e-470">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="54f4e-471">object</span><span class="sxs-lookup"><span data-stu-id="54f4e-471">object</span></span>|||<span data-ttu-id="54f4e-472">Especifique el módulo de tareas que se va a cargar previamente cuando utilice un comando de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="54f4e-472">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="54f4e-473">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-473">string</span></span>|<span data-ttu-id="54f4e-474">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-474">64 characters</span></span>||<span data-ttu-id="54f4e-475">Título inicial del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="54f4e-475">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="54f4e-476">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-476">string</span></span>|||<span data-ttu-id="54f4e-477">Ancho del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "medio" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="54f4e-477">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="54f4e-478">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-478">string</span></span>|||<span data-ttu-id="54f4e-479">Altura del cuadro de diálogo: un número en píxeles o un diseño predeterminado como "grande", "medio" o "pequeño".</span><span class="sxs-lookup"><span data-stu-id="54f4e-479">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="54f4e-480">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-480">string</span></span>|||<span data-ttu-id="54f4e-481">URL de vista web inicial.</span><span class="sxs-lookup"><span data-stu-id="54f4e-481">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="54f4e-482">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="54f4e-482">array of object</span></span>|<span data-ttu-id="54f4e-483">5 artículos</span><span class="sxs-lookup"><span data-stu-id="54f4e-483">5 items</span></span>|<span data-ttu-id="54f4e-484">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-484">✔</span></span>|<span data-ttu-id="54f4e-485">La lista de parámetros que toma el comando.</span><span class="sxs-lookup"><span data-stu-id="54f4e-485">The list of parameters the command takes.</span></span> <span data-ttu-id="54f4e-486">Mínimo: 1; máximo: 5.</span><span class="sxs-lookup"><span data-stu-id="54f4e-486">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="54f4e-487">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-487">string</span></span>|<span data-ttu-id="54f4e-488">64 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-488">64 characters</span></span>|<span data-ttu-id="54f4e-489">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-489">✔</span></span>|<span data-ttu-id="54f4e-490">El nombre del parámetro tal como aparece en el cliente.</span><span class="sxs-lookup"><span data-stu-id="54f4e-490">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="54f4e-491">Esto se incluye en la solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="54f4e-491">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="54f4e-492">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-492">string</span></span>|<span data-ttu-id="54f4e-493">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-493">32 characters</span></span>|<span data-ttu-id="54f4e-494">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-494">✔</span></span>|<span data-ttu-id="54f4e-495">Título fácil de usar para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="54f4e-495">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="54f4e-496">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-496">string</span></span>|<span data-ttu-id="54f4e-497">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-497">128 characters</span></span>||<span data-ttu-id="54f4e-498">Cadena fácil de usar que describe el propósito de este parámetro.</span><span class="sxs-lookup"><span data-stu-id="54f4e-498">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="54f4e-499">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-499">string</span></span>|<span data-ttu-id="54f4e-500">512 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-500">512 characters</span></span>||<span data-ttu-id="54f4e-501">Valor inicial para el parámetro.</span><span class="sxs-lookup"><span data-stu-id="54f4e-501">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="54f4e-502">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-502">string</span></span>|<span data-ttu-id="54f4e-503">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-503">128 characters</span></span>||<span data-ttu-id="54f4e-504">Define el tipo de control que se muestra en un módulo de tareas para `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-504">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="54f4e-505">Uno de `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-505">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="54f4e-506">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="54f4e-506">array of objects</span></span>|<span data-ttu-id="54f4e-507">10 artículos</span><span class="sxs-lookup"><span data-stu-id="54f4e-507">10 items</span></span>||<span data-ttu-id="54f4e-508">Las opciones de elección para el `choiceset` archivo .</span><span class="sxs-lookup"><span data-stu-id="54f4e-508">The choice options for the`choiceset`.</span></span> <span data-ttu-id="54f4e-509">Utilice únicamente cuando `parameter.inputType` sea `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-509">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="54f4e-510">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-510">string</span></span>|<span data-ttu-id="54f4e-511">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-511">128 characters</span></span>|<span data-ttu-id="54f4e-512">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-512">✔</span></span>|<span data-ttu-id="54f4e-513">Título de la elección.</span><span class="sxs-lookup"><span data-stu-id="54f4e-513">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="54f4e-514">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-514">string</span></span>|<span data-ttu-id="54f4e-515">512 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-515">512 characters</span></span>|<span data-ttu-id="54f4e-516">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-516">✔</span></span>|<span data-ttu-id="54f4e-517">Valor de la elección.</span><span class="sxs-lookup"><span data-stu-id="54f4e-517">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="54f4e-518">permisos</span><span class="sxs-lookup"><span data-stu-id="54f4e-518">permissions</span></span>

<span data-ttu-id="54f4e-519">**Opcional** — matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="54f4e-519">**Optional** — array of strings</span></span>

<span data-ttu-id="54f4e-520">Una matriz de `string` la que se especifica qué permisos solicita la aplicación, lo que permite a los usuarios finales saber cómo funciona la extensión.</span><span class="sxs-lookup"><span data-stu-id="54f4e-520">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="54f4e-521">Las siguientes opciones no son exclusivas:</span><span class="sxs-lookup"><span data-stu-id="54f4e-521">The following options are non-exclusive:</span></span>

* <span data-ttu-id="54f4e-522">`identity`&emsp;Requiere información de identidad de usuario.</span><span class="sxs-lookup"><span data-stu-id="54f4e-522">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="54f4e-523">`messageTeamMembers`&emsp;Requiere permiso para enviar mensajes directos a los miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="54f4e-523">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="54f4e-524">Cambiar estos permisos durante la actualización de la aplicación, hace que los usuarios repitan el proceso de consentimiento después de ejecutar la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="54f4e-524">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="54f4e-525">Consulta [Actualización de la aplicación](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="54f4e-525">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="54f4e-526">dispositivoPermissions</span><span class="sxs-lookup"><span data-stu-id="54f4e-526">devicePermissions</span></span>

<span data-ttu-id="54f4e-527">**Opcional** — matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="54f4e-527">**Optional** — array of strings</span></span>

<span data-ttu-id="54f4e-528">Proporciona las características nativas en el dispositivo de un usuario al que la aplicación solicita acceso.</span><span class="sxs-lookup"><span data-stu-id="54f4e-528">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="54f4e-529">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="54f4e-529">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="54f4e-530">validDomains</span><span class="sxs-lookup"><span data-stu-id="54f4e-530">validDomains</span></span>

<span data-ttu-id="54f4e-531">**Opcional,** excepto **Obligatorio** cuando se indique.</span><span class="sxs-lookup"><span data-stu-id="54f4e-531">**Optional**, except **Required** where noted.</span></span>

<span data-ttu-id="54f4e-532">Una lista de dominios válidos para los sitios web que la aplicación espera cargar dentro del cliente Teams.</span><span class="sxs-lookup"><span data-stu-id="54f4e-532">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="54f4e-533">Los listados de dominios pueden incluir comodines, por ejemplo, `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-533">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="54f4e-534">Esto coincide exactamente con un segmento del dominio; si necesita `a.b.example.com` coincidir, utilice `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-534">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="54f4e-535">Si la configuración de la pestaña o la interfaz de usuario de contenido deben navegar a cualquier otro dominio además del que se usa para la configuración de pestañas, ese dominio debe especificarse aquí.</span><span class="sxs-lookup"><span data-stu-id="54f4e-535">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="54f4e-536">**No** es necesario incluir los dominios de los proveedores de identidades que desea admitir en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-536">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="54f4e-537">Por ejemplo, para autenticarse con un ID de Google, es necesario redirigir a accounts.google.com, sin embargo, no debe incluir accounts.google.com en `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-537">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="54f4e-538">Teams aplicaciones que requieren que sus propias direcciones URL de sharepoint funcionen bien, incluye "{teamsitedomain}" en su lista de dominios válida.</span><span class="sxs-lookup"><span data-stu-id="54f4e-538">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54f4e-539">No agregue dominios que estén fuera del control, ya sea directamente o a través de comodines.</span><span class="sxs-lookup"><span data-stu-id="54f4e-539">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="54f4e-540">Por ejemplo, `yourapp.onmicrosoft.com` es válido, sin embargo, `*.onmicrosoft.com` no es válido.</span><span class="sxs-lookup"><span data-stu-id="54f4e-540">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="54f4e-541">El objeto es una matriz con todos los elementos del tipo `string` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-541">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="54f4e-542">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="54f4e-542">webApplicationInfo</span></span>

<span data-ttu-id="54f4e-543">**Opcional** — objeto</span><span class="sxs-lookup"><span data-stu-id="54f4e-543">**Optional** — object</span></span>

<span data-ttu-id="54f4e-544">Proporcione el identificador de aplicación de Azure Active Directory (AAD) y microsoft Graph información para ayudar a los usuarios a iniciar sesión sin problemas en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-544">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="54f4e-545">Si la aplicación está registrada en AAD, debe proporcionar el IDENTIFICADOR de aplicación para que los administradores puedan revisar fácilmente los permisos y conceder su consentimiento en Teams centro de administración.</span><span class="sxs-lookup"><span data-stu-id="54f4e-545">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="54f4e-546">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-546">Name</span></span>| <span data-ttu-id="54f4e-547">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-547">Type</span></span>| <span data-ttu-id="54f4e-548">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-548">Maximum size</span></span> | <span data-ttu-id="54f4e-549">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-549">Required</span></span> | <span data-ttu-id="54f4e-550">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-550">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="54f4e-551">string</span><span class="sxs-lookup"><span data-stu-id="54f4e-551">string</span></span>|<span data-ttu-id="54f4e-552">36 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-552">36 characters</span></span>|<span data-ttu-id="54f4e-553">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-553">✔</span></span>|<span data-ttu-id="54f4e-554">Identificador de aplicación AAD de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-554">AAD application id of the app.</span></span> <span data-ttu-id="54f4e-555">Este id debe ser un GUID.</span><span class="sxs-lookup"><span data-stu-id="54f4e-555">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="54f4e-556">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-556">string</span></span>|<span data-ttu-id="54f4e-557">2048 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-557">2048 characters</span></span>|<span data-ttu-id="54f4e-558">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-558">✔</span></span>|<span data-ttu-id="54f4e-559">Dirección URL de recursos de la aplicación para adquirir token de autenticación para SSO.</span><span class="sxs-lookup"><span data-stu-id="54f4e-559">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="54f4e-560">**NOTA:** Si no usa SSO, asegúrese de introducir un valor de cadena ficticio en este campo en el manifiesto de la aplicación, por ejemplo, https://notapplicable para evitar una respuesta de error.</span><span class="sxs-lookup"><span data-stu-id="54f4e-560">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="54f4e-561">matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="54f4e-561">array of strings</span></span>|<span data-ttu-id="54f4e-562">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-562">128 characters</span></span>||<span data-ttu-id="54f4e-563">Especifique el [consentimiento específico del recurso](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)granular.</span><span class="sxs-lookup"><span data-stu-id="54f4e-563">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="54f4e-564">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="54f4e-564">showLoadingIndicator</span></span>

<span data-ttu-id="54f4e-565">**Opcional** — booleano</span><span class="sxs-lookup"><span data-stu-id="54f4e-565">**Optional** — boolean</span></span>

<span data-ttu-id="54f4e-566">Indica si se debe mostrar o no el indicador de carga cuando se carga una aplicación o pestaña.</span><span class="sxs-lookup"><span data-stu-id="54f4e-566">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="54f4e-567">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="54f4e-567">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="54f4e-568">Si selecciona `showLoadingIndicator` como true en el manifiesto de la aplicación, para cargar la página correctamente, modifique las páginas de contenido de las pestañas y los módulos de tareas como se describe en Mostrar un documento indicador de carga [nativo.](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)</span><span class="sxs-lookup"><span data-stu-id="54f4e-568">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="54f4e-569">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="54f4e-569">isFullScreen</span></span>

 <span data-ttu-id="54f4e-570">**Opcional** — booleano</span><span class="sxs-lookup"><span data-stu-id="54f4e-570">**Optional** — boolean</span></span>

<span data-ttu-id="54f4e-571">Indique dónde se representa una aplicación personal con o sin una barra de encabezado de tabulación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-571">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="54f4e-572">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="54f4e-572">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="54f4e-573">activities</span><span class="sxs-lookup"><span data-stu-id="54f4e-573">activities</span></span>

<span data-ttu-id="54f4e-574">**Opcional** — objeto</span><span class="sxs-lookup"><span data-stu-id="54f4e-574">**Optional** — object</span></span>

<span data-ttu-id="54f4e-575">Defina las propiedades que usa la aplicación para publicar una fuente de actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="54f4e-575">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="54f4e-576">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-576">Name</span></span>| <span data-ttu-id="54f4e-577">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-577">Type</span></span>| <span data-ttu-id="54f4e-578">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-578">Maximum size</span></span> | <span data-ttu-id="54f4e-579">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-579">Required</span></span> | <span data-ttu-id="54f4e-580">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-580">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="54f4e-581">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="54f4e-581">array of Objects</span></span>|<span data-ttu-id="54f4e-582">128 artículos</span><span class="sxs-lookup"><span data-stu-id="54f4e-582">128 items</span></span>| | <span data-ttu-id="54f4e-583">Proporcione los tipos de actividades que la aplicación puede publicar en una fuente de actividades de usuarios.</span><span class="sxs-lookup"><span data-stu-id="54f4e-583">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="54f4e-584">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="54f4e-584">activities.activityTypes</span></span>

|<span data-ttu-id="54f4e-585">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-585">Name</span></span>| <span data-ttu-id="54f4e-586">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-586">Type</span></span>| <span data-ttu-id="54f4e-587">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-587">Maximum size</span></span> | <span data-ttu-id="54f4e-588">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-588">Required</span></span> | <span data-ttu-id="54f4e-589">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-589">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="54f4e-590">string</span><span class="sxs-lookup"><span data-stu-id="54f4e-590">string</span></span>|<span data-ttu-id="54f4e-591">32 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-591">32 characters</span></span>|<span data-ttu-id="54f4e-592">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-592">✔</span></span>|<span data-ttu-id="54f4e-593">El tipo de notificación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-593">The notification type.</span></span> <span data-ttu-id="54f4e-594">*Vea a continuación*.</span><span class="sxs-lookup"><span data-stu-id="54f4e-594">*See below*.</span></span>|
|`description`|<span data-ttu-id="54f4e-595">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-595">string</span></span>|<span data-ttu-id="54f4e-596">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-596">128 characters</span></span>|<span data-ttu-id="54f4e-597">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-597">✔</span></span>|<span data-ttu-id="54f4e-598">Una breve descripción de la notificación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-598">A brief description of the notification.</span></span> <span data-ttu-id="54f4e-599">*Vea a continuación*.</span><span class="sxs-lookup"><span data-stu-id="54f4e-599">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="54f4e-600">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-600">string</span></span>|<span data-ttu-id="54f4e-601">128 caracteres</span><span class="sxs-lookup"><span data-stu-id="54f4e-601">128 characters</span></span>|<span data-ttu-id="54f4e-602">✔</span><span class="sxs-lookup"><span data-stu-id="54f4e-602">✔</span></span>|<span data-ttu-id="54f4e-603">Por ejemplo: "{actor} creó la tarea {taskId} para usted"</span><span class="sxs-lookup"><span data-stu-id="54f4e-603">Ex: "{actor} created task {taskId} for you"</span></span>|

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

## <a name="defaultinstallscope"></a><span data-ttu-id="54f4e-604">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="54f4e-604">defaultInstallScope</span></span>

<span data-ttu-id="54f4e-605">**Opcional** - cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-605">**Optional** - string</span></span>

<span data-ttu-id="54f4e-606">Especifica el ámbito de instalación definido para esta aplicación de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="54f4e-606">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="54f4e-607">El ámbito definido será la opción que se muestra en el botón cuando un usuario intenta agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-607">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="54f4e-608">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="54f4e-608">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="54f4e-609">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="54f4e-609">defaultGroupCapability</span></span>

<span data-ttu-id="54f4e-610">**Opcional** - objeto</span><span class="sxs-lookup"><span data-stu-id="54f4e-610">**Optional** - object</span></span>

<span data-ttu-id="54f4e-611">Cuando se selecciona un ámbito de instalación de grupo, definirá la funcionalidad predeterminada cuando el usuario instale la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-611">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="54f4e-612">Las opciones son:</span><span class="sxs-lookup"><span data-stu-id="54f4e-612">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="54f4e-613">Nombre</span><span class="sxs-lookup"><span data-stu-id="54f4e-613">Name</span></span>| <span data-ttu-id="54f4e-614">Tipo</span><span class="sxs-lookup"><span data-stu-id="54f4e-614">Type</span></span>| <span data-ttu-id="54f4e-615">Tamaño máximo</span><span class="sxs-lookup"><span data-stu-id="54f4e-615">Maximum size</span></span> | <span data-ttu-id="54f4e-616">Necesario</span><span class="sxs-lookup"><span data-stu-id="54f4e-616">Required</span></span> | <span data-ttu-id="54f4e-617">Descripción</span><span class="sxs-lookup"><span data-stu-id="54f4e-617">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="54f4e-618">string</span><span class="sxs-lookup"><span data-stu-id="54f4e-618">string</span></span>|||<span data-ttu-id="54f4e-619">Cuando se selecciona el ámbito de `team` instalación, este campo especifica la capacidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="54f4e-619">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="54f4e-620">Opciones: `tab` , `bot` o `connector` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-620">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="54f4e-621">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-621">string</span></span>|||<span data-ttu-id="54f4e-622">Cuando se selecciona el ámbito de `groupchat` instalación, este campo especifica la capacidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="54f4e-622">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="54f4e-623">Opciones: `tab` , `bot` o `connector` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-623">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="54f4e-624">cadena</span><span class="sxs-lookup"><span data-stu-id="54f4e-624">string</span></span>|||<span data-ttu-id="54f4e-625">Cuando se selecciona el ámbito de `meetings` instalación, este campo especifica la capacidad predeterminada disponible.</span><span class="sxs-lookup"><span data-stu-id="54f4e-625">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="54f4e-626">Opciones: `tab` , `bot` o `connector` .</span><span class="sxs-lookup"><span data-stu-id="54f4e-626">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="54f4e-627">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="54f4e-627">configurableProperties</span></span>

<span data-ttu-id="54f4e-628">**Opcional** - matriz</span><span class="sxs-lookup"><span data-stu-id="54f4e-628">**Optional** - array</span></span>

<span data-ttu-id="54f4e-629">El `configurableProperties` bloque define las propiedades de la aplicación que Teams administrador puede personalizar.</span><span class="sxs-lookup"><span data-stu-id="54f4e-629">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="54f4e-630">Para obtener más información, consulte [personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="54f4e-630">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="54f4e-631">Se debe definir un mínimo de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="54f4e-631">A minimum of one property must be defined.</span></span> <span data-ttu-id="54f4e-632">Puede definir un máximo de nueve propiedades en este bloque.</span><span class="sxs-lookup"><span data-stu-id="54f4e-632">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="54f4e-633">Como práctica recomendada, debe proporcionar directrices de personalización para que los usuarios y clientes de la aplicación las sigan al personalizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-633">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span>

<span data-ttu-id="54f4e-634">Puede definir cualquiera de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="54f4e-634">You can define any of the following properties:</span></span>
* <span data-ttu-id="54f4e-635">`name`: Permite al administrador cambiar el nombre para mostrar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-635">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="54f4e-636">`shortDescription`: Permite al administrador cambiar la breve descripción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-636">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="54f4e-637">`longDescription`: Permite al administrador cambiar la descripción detallada de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="54f4e-637">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="54f4e-638">`smallImageUrl`: Es la `outline` propiedad en el bloque del `icons` manifiesto.</span><span class="sxs-lookup"><span data-stu-id="54f4e-638">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="54f4e-639">`largeImageUrl`: Es la `color` propiedad en el bloque del `icons` manifiesto.</span><span class="sxs-lookup"><span data-stu-id="54f4e-639">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="54f4e-640">`accentColor`: Es el color a utilizar junto con y como fondo para sus iconos de contorno.</span><span class="sxs-lookup"><span data-stu-id="54f4e-640">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="54f4e-641">`websiteUrl`: Es la URL https:// al sitio web del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="54f4e-641">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="54f4e-642">`privacyUrl`: Es la URL https:// a la política de privacidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="54f4e-642">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="54f4e-643">`termsOfUseUrl`: Es la URL https:// a los términos de uso del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="54f4e-643">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>


