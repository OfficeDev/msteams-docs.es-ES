---
title: Recibir todos los mensajes de canal con RSC
author: surbhigupta12
description: Recibir todos los mensajes de canal con permisos de RSC
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 833bdbc015cf852fcd899ce4e75f742448b89978
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631415"
---
# <a name="receive-all-channel-messages-with-rsc"></a><span data-ttu-id="9a4a9-103">Recibir todos los mensajes de canal con RSC</span><span class="sxs-lookup"><span data-stu-id="9a4a9-103">Receive all channel messages with RSC</span></span>

> [!NOTE]
> <span data-ttu-id="9a4a9-104">Esta característica está disponible actualmente solo en [la versión preliminar del desarrollador](../../../resources/dev-preview/developer-preview-intro.md) público.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-104">This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="9a4a9-105">El modelo de permisos de consentimiento específico de recursos (RSC), desarrollado originalmente para Teams Graph API, ahora se extiende a escenarios de bots.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-105">The resource-specific consent (RSC) permissions model, originally developed for Teams Graph APIs, is now extended to bot scenarios.</span></span>

<span data-ttu-id="9a4a9-106">Actualmente, los bots solo pueden recibir mensajes de canal de usuario cuando se @mentioned.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-106">Currently, bots can only receive user channel messages when they are @mentioned.</span></span> <span data-ttu-id="9a4a9-107">Con RSC, ahora puedes solicitar a los propietarios del equipo que consienten que un bot reciba mensajes de usuario en los canales estándar de un equipo sin que se @mentioned.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-107">Using RSC, you can now request team owners to consent for a bot to receive user messages across standard channels in a team without being @mentioned.</span></span> <span data-ttu-id="9a4a9-108">Esta funcionalidad se habilita especificando el permiso en el `ChannelMessage.Read.Group` manifiesto de una aplicación Teams RSC habilitada.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-108">This capability is enabled by specifying the `ChannelMessage.Read.Group` permission in the manifest of an RSC enabled Teams app.</span></span> <span data-ttu-id="9a4a9-109">Después de la configuración, los propietarios del equipo pueden conceder su consentimiento durante el proceso de instalación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-109">After configuration, team owners can grant consent during the app installation process.</span></span>

<span data-ttu-id="9a4a9-110">Para obtener más información acerca de cómo habilitar RSC para tu aplicación, consulta el consentimiento específico de los [recursos en Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="9a4a9-110">For more information about enabling RSC for your app, see [resource-specific consent in Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).</span></span>

## <a name="enable-bots-to-receive-all-channel-messages"></a><span data-ttu-id="9a4a9-111">Habilitar bots para recibir todos los mensajes de canal</span><span class="sxs-lookup"><span data-stu-id="9a4a9-111">Enable bots to receive all channel messages</span></span>

<span data-ttu-id="9a4a9-112">El `ChannelMessage.Read.Group` permiso RSC se extiende a los bots.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-112">The `ChannelMessage.Read.Group` RSC permission is extended to bots.</span></span> <span data-ttu-id="9a4a9-113">Con el consentimiento del usuario, este permiso permite que las aplicaciones de gráficos obtengan todos los mensajes de una conversación y que los bots reciban todos los mensajes de canal sin que se @mentioned.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-113">With user consent, this permission allows graph applications to get all messages in a conversation and bots to receive all channel messages without being @mentioned.</span></span>

## <a name="update-app-manifest"></a><span data-ttu-id="9a4a9-114">Actualizar manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="9a4a9-114">Update app manifest</span></span>

<span data-ttu-id="9a4a9-115">Para que el bot reciba todos los mensajes de canal, RSC debe configurarse en el manifiesto Teams aplicación con el permiso `ChannelMessage.Read.Group` especificado en la `webApplicationInfo` propiedad.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-115">For your bot to receive all channel messages, RSC must be configured in the Teams app manifest with the `ChannelMessage.Read.Group` permission specified in the `webApplicationInfo` property.</span></span>

![Actualizar manifiesto de la aplicación](~/bots/how-to/conversations/Media/appmanifest.png)

<span data-ttu-id="9a4a9-117">A continuación se muestra un ejemplo del `webApplicationInfo` objeto:</span><span class="sxs-lookup"><span data-stu-id="9a4a9-117">The following is an example of the `webApplicationInfo` object:</span></span>

* <span data-ttu-id="9a4a9-118">**id:** el Azure Active Directory de aplicación (AAD).</span><span class="sxs-lookup"><span data-stu-id="9a4a9-118">**id**: Your Azure Active Directory (AAD) app ID.</span></span> <span data-ttu-id="9a4a9-119">Puede ser el mismo que el identificador del bot.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-119">This can be the same as your bot ID.</span></span>
* <span data-ttu-id="9a4a9-120">**resource**: Any string.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-120">**resource**: Any string.</span></span> <span data-ttu-id="9a4a9-121">Este campo no tiene ninguna operación en RSC, pero debe agregarse y tener un valor para evitar la respuesta de error.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-121">This field has no operation in RSC, but must be added and have a value to avoid error response.</span></span>
* <span data-ttu-id="9a4a9-122">**applicationPermissions:** se deben especificar los permisos de RSC para `ChannelMessage.Read.Group` la aplicación con.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-122">**applicationPermissions**: RSC permissions for your app with `ChannelMessage.Read.Group` must be specified.</span></span> <span data-ttu-id="9a4a9-123">Para obtener más información, [consulte resource-specific permissions](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).</span><span class="sxs-lookup"><span data-stu-id="9a4a9-123">For more information, see [resource-specific permissions](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).</span></span>

<span data-ttu-id="9a4a9-124">El código siguiente proporciona un ejemplo del manifiesto de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="9a4a9-124">The following code provides an example of the app manifest:</span></span>

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team-to-test"></a><span data-ttu-id="9a4a9-125">Instalación local en un equipo para probar</span><span class="sxs-lookup"><span data-stu-id="9a4a9-125">Sideload in a team to test</span></span>

<span data-ttu-id="9a4a9-126">Para realizar la instalación local en un equipo para probar, si todos los mensajes de canal de un equipo con RSC se reciben sin que se @mentioned:</span><span class="sxs-lookup"><span data-stu-id="9a4a9-126">To sideload in a team to test, whether all channel messages in a team with RSC are received without being @mentioned:</span></span>

1. <span data-ttu-id="9a4a9-127">Seleccione o cree un equipo.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-127">Select or create a team.</span></span>
1. <span data-ttu-id="9a4a9-128">Seleccione los puntos suspensivos &#x25CF;&#x25CF;&#x25CF; en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-128">Select the ellipses &#x25CF;&#x25CF;&#x25CF; from the left pane.</span></span> <span data-ttu-id="9a4a9-129">Aparece el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-129">The drop-down menu appears.</span></span>
1. <span data-ttu-id="9a4a9-130">Seleccione **Administrar equipo** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-130">Select **Manage team** from the drop-down menu.</span></span> <span data-ttu-id="9a4a9-131">Aparecen los detalles.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-131">The details appear.</span></span>

   ![Administración de aplicaciones en equipo](~/bots/how-to/conversations/Media/managingteam.png)

1. <span data-ttu-id="9a4a9-133">Seleccione **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-133">Select **Apps**.</span></span> <span data-ttu-id="9a4a9-134">Aparecen varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-134">Multiple apps appear.</span></span>
1. <span data-ttu-id="9a4a9-135">Selecciona **Upload una aplicación personalizada** en la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-135">Select **Upload a custom app** from the lower right corner.</span></span>

    ![Cargar una aplicación personalizada](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. <span data-ttu-id="9a4a9-137">Selecciona el paquete de la aplicación en el **cuadro de diálogo** Abrir.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-137">Select the app package from the **Open** dialog box.</span></span>
1. <span data-ttu-id="9a4a9-138">Seleccione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-138">Select **Open**.</span></span>

    ![Selección del paquete de la aplicación](~/bots/how-to/conversations/Media/selectapppackage.png)

1. <span data-ttu-id="9a4a9-140">Selecciona **Agregar** en la ventana emergente detalles de la aplicación para agregar el bot al equipo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-140">Select **Add** from the app details pop-up, to add the bot to your selected team.</span></span>

    ![Agregar el bot](~/bots/how-to/conversations/Media/addingbot.png)

1. <span data-ttu-id="9a4a9-142">Seleccione un canal e introduzca un mensaje en el canal del bot.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-142">Select a channel and enter a message in the channel for your bot.</span></span>

    <span data-ttu-id="9a4a9-143">El bot recibe el mensaje sin que se @mentioned.</span><span class="sxs-lookup"><span data-stu-id="9a4a9-143">The bot receives the message without being @mentioned.</span></span>

    ![Bot recibe mensaje](~/bots/how-to/conversations/Media/botreceivingmessage.png)

## <a name="see-also"></a><span data-ttu-id="9a4a9-145">Vea también</span><span class="sxs-lookup"><span data-stu-id="9a4a9-145">See also</span></span>

* [<span data-ttu-id="9a4a9-146">Conversaciones de bot</span><span class="sxs-lookup"><span data-stu-id="9a4a9-146">Bot conversations</span></span>](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [<span data-ttu-id="9a4a9-147">Consentimiento específico del recurso</span><span class="sxs-lookup"><span data-stu-id="9a4a9-147">Resource-specific consent</span></span>](/microsoftteams/resource-specific-consent)
* [<span data-ttu-id="9a4a9-148">Probar el consentimiento específico de los recursos</span><span class="sxs-lookup"><span data-stu-id="9a4a9-148">Test resource-specific consent</span></span>](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [<span data-ttu-id="9a4a9-149">Upload aplicación personalizada en Teams</span><span class="sxs-lookup"><span data-stu-id="9a4a9-149">Upload custom app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
