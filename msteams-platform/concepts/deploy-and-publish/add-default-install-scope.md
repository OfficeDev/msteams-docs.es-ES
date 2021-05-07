---
title: Configurar opciones de instalación predeterminadas para la aplicación
description: Describe cómo especificar las opciones de instalación predeterminadas de la aplicación.
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 561a4f2910e703db5ffce6176f6177dfd661d2ce
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230935"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a><span data-ttu-id="2e080-103">Configurar las opciones de instalación predeterminadas para Microsoft Teams aplicación</span><span class="sxs-lookup"><span data-stu-id="2e080-103">Configure default install options for your Microsoft Teams app</span></span>

<span data-ttu-id="2e080-104">Es común que una aplicación admita varios escenarios en Teams, pero es posible que la haya diseñado con un ámbito y capacidad específicos en mente.</span><span class="sxs-lookup"><span data-stu-id="2e080-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="2e080-105">Por ejemplo, si la aplicación es principalmente para uso de equipo o canal, puedes asegurarte de que la primera opción de instalación que los usuarios ven en la tienda es **Agregar a un equipo**.</span><span class="sxs-lookup"><span data-stu-id="2e080-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

:::row:::
   :::column span="2":::

![Agregar un ejemplo desplegable de aplicaciones](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

<span data-ttu-id="2e080-107">Si la funcionalidad principal de la aplicación es un bot, también puedes convertir el bot en la funcionalidad predeterminada cuando un usuario instala la aplicación en un equipo.</span><span class="sxs-lookup"><span data-stu-id="2e080-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span>

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="2e080-108">Configurar el ámbito de instalación predeterminado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2e080-108">Configure your app's default install scope</span></span>

<span data-ttu-id="2e080-109">Configure el ámbito de instalación predeterminado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2e080-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="2e080-110">Solo puede establecer un ámbito a la vez.</span><span class="sxs-lookup"><span data-stu-id="2e080-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="2e080-111">**Para configurar el ámbito de instalación predeterminado en el manifiesto de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="2e080-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="2e080-112">Abre el manifiesto de la aplicación y agrega la `defaultInstallScope` propiedad.</span><span class="sxs-lookup"><span data-stu-id="2e080-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="2e080-113">Establezca el valor de ámbito de instalación predeterminado como `personal` , , , o `team` `groupchat` `meetings` .</span><span class="sxs-lookup"><span data-stu-id="2e080-113">Set default install scope value as, either `personal`, `team`, `groupchat`, or `meetings`.</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="2e080-114">Para obtener más información, consulta el esquema [de manifiesto de la aplicación](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="2e080-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="2e080-115">Configurar la funcionalidad predeterminada para ámbitos compartidos</span><span class="sxs-lookup"><span data-stu-id="2e080-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="2e080-116">Configura la funcionalidad predeterminada cuando la aplicación esté instalada para un equipo, una reunión o un chat de grupo.</span><span class="sxs-lookup"><span data-stu-id="2e080-116">Configure the default capability when your app is installed for a team, meeting, or groupchat.</span></span>

> [!NOTE]
> <span data-ttu-id="2e080-117">`defaultGroupCapability` proporciona la funcionalidad predeterminada que se agregará al equipo, al chat de grupo o a la reunión.</span><span class="sxs-lookup"><span data-stu-id="2e080-117">`defaultGroupCapability` provides the default capability that will be added to the team, groupchat, or meeting.</span></span> <span data-ttu-id="2e080-118">Selecciona una pestaña, bot o conector como la funcionalidad predeterminada de la aplicación, pero debes asegurarte de que has proporcionado la funcionalidad seleccionada en la definición de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2e080-118">Select a tab, bot, or connector as the default capability for your app, but you must ensure that you have provided the selected capability in your app definition.</span></span>

<span data-ttu-id="2e080-119">**Para configurar detalles en el manifiesto de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="2e080-119">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="2e080-120">Abre el manifiesto de la aplicación y agrega la `defaultGroupCapability` propiedad a él.</span><span class="sxs-lookup"><span data-stu-id="2e080-120">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="2e080-121">Establezca un valor `team` de `groupchat` , o `meetings` .</span><span class="sxs-lookup"><span data-stu-id="2e080-121">Set a value of `team`, `groupchat`, or `meetings`.</span></span>
3. <span data-ttu-id="2e080-122">Para la funcionalidad de grupo seleccionada, las capacidades de grupo disponibles `bot` son, `tab` , o `connector` .</span><span class="sxs-lookup"><span data-stu-id="2e080-122">For the selected group capability, the available group capabilities are, `bot`, `tab`, or `connector`.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="2e080-123">Solo puede seleccionar una funcionalidad predeterminada, `bot` , o para la funcionalidad de grupo `tab` `connector` seleccionada.</span><span class="sxs-lookup"><span data-stu-id="2e080-123">You can select only one default capability, `bot`, `tab`, or `connector` for the selected group capability.</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> <span data-ttu-id="2e080-124">Para obtener más información, consulta el esquema [de manifiesto de la aplicación](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="2e080-124">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="2e080-125">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="2e080-125">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e080-126">Crear el paquete de aplicación</span><span class="sxs-lookup"><span data-stu-id="2e080-126">Create your app package</span></span>](~/concepts/build-and-test/apps-package.md)
