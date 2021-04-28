---
title: Configurar opciones de instalación predeterminadas para la aplicación
description: Describe cómo especificar las opciones de instalación predeterminadas de la aplicación.
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 0afcce50a4779421016c23c4ec4e3d25cc3401d1
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058617"
---
# <a name="add-a-default-install-scope-and-group-capability"></a><span data-ttu-id="506d0-103">Agregar un ámbito de instalación predeterminado y una funcionalidad de grupo</span><span class="sxs-lookup"><span data-stu-id="506d0-103">Add a default install scope and group capability</span></span>

<span data-ttu-id="506d0-104">Es común que una aplicación admita varios escenarios en Teams, pero es posible que la haya diseñado con un ámbito y una funcionalidad específicos en mente.</span><span class="sxs-lookup"><span data-stu-id="506d0-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="506d0-105">Por ejemplo, si la aplicación es principalmente para uso de equipo o canal, puedes asegurarte de que la primera opción de instalación que los usuarios ven en la tienda es **Agregar a un equipo**.</span><span class="sxs-lookup"><span data-stu-id="506d0-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

![Agregar una aplicación](../../assets/images/compose-extensions/addanapp.png)

<span data-ttu-id="506d0-107">Si la funcionalidad principal de la aplicación es un bot, también puedes convertir el bot en la funcionalidad predeterminada cuando un usuario instala la aplicación en un equipo.</span><span class="sxs-lookup"><span data-stu-id="506d0-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span>

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="506d0-108">Configurar el ámbito de instalación predeterminado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="506d0-108">Configure your app's default install scope</span></span>

<span data-ttu-id="506d0-109">Configure el ámbito de instalación predeterminado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="506d0-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="506d0-110">Solo puede establecer un ámbito a la vez.</span><span class="sxs-lookup"><span data-stu-id="506d0-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="506d0-111">**Para configurar el ámbito de instalación predeterminado en el manifiesto de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="506d0-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="506d0-112">Abre el manifiesto de la aplicación y agrega la `defaultInstallScope` propiedad.</span><span class="sxs-lookup"><span data-stu-id="506d0-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="506d0-113">Establezca el valor de ámbito de instalación predeterminado como `personal` , , , o `team` `groupchat` `meetings` .</span><span class="sxs-lookup"><span data-stu-id="506d0-113">Set default install scope value as, either `personal`, `team`, `groupchat`, or `meetings`.</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="506d0-114">Para obtener más información, consulta el esquema [de manifiesto de la aplicación](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="506d0-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="506d0-115">Configurar la funcionalidad predeterminada para ámbitos compartidos</span><span class="sxs-lookup"><span data-stu-id="506d0-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="506d0-116">Configura la funcionalidad predeterminada cuando la aplicación esté instalada para un equipo, una reunión o un chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="506d0-116">Configure the default capability when your app is installed for a team, meeting, or groupchat.</span></span>

> [!NOTE]
> <span data-ttu-id="506d0-117">`defaultGroupCapability` proporciona la funcionalidad predeterminada que se agregará al equipo, al chat de grupo o a la reunión.</span><span class="sxs-lookup"><span data-stu-id="506d0-117">`defaultGroupCapability` provides the default capability that will be added to the team, groupchat, or meeting.</span></span> <span data-ttu-id="506d0-118">Selecciona una pestaña, bot o conector como la funcionalidad predeterminada de la aplicación, pero debes asegurarte de que has proporcionado la funcionalidad seleccionada en la definición de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="506d0-118">Select a tab, bot, or connector as the default capability for your app, but you must ensure that you have provided the selected capability in your app definition.</span></span>

<span data-ttu-id="506d0-119">**Para configurar detalles en el manifiesto de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="506d0-119">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="506d0-120">Abre el manifiesto de la aplicación y agrega la `defaultGroupCapability` propiedad a él.</span><span class="sxs-lookup"><span data-stu-id="506d0-120">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="506d0-121">Establezca un valor `team` de `groupchat` , o `meetings` .</span><span class="sxs-lookup"><span data-stu-id="506d0-121">Set a value of `team`, `groupchat`, or `meetings`.</span></span>
3. <span data-ttu-id="506d0-122">Para la funcionalidad de grupo seleccionada, las capacidades de grupo disponibles `bot` son, `tab` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="506d0-122">For the selected group capability, the available group capabilities are, `bot`, `tab`, or `connector`.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="506d0-123">Solo puede seleccionar una funcionalidad predeterminada, `bot` , o para la funcionalidad de grupo `tab` `connector` seleccionada.</span><span class="sxs-lookup"><span data-stu-id="506d0-123">You can select only one default capability, `bot`, `tab`, or `connector` for the selected group capability.</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> <span data-ttu-id="506d0-124">Para obtener más información, consulta el esquema [de manifiesto de la aplicación](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="506d0-124">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="506d0-125">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="506d0-125">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="506d0-126">Elegir cómo distribuir la aplicación</span><span class="sxs-lookup"><span data-stu-id="506d0-126">Choose how to distribute your app</span></span>](overview.md)
