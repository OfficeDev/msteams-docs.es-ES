---
title: Configurar opciones de instalación predeterminadas para la aplicación
description: Describe cómo especificar las opciones de instalación predeterminadas de la aplicación.
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a4b70df70c7b9442e29953dae8a8c4e892cb72c1
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946493"
---
# <a name="add-a-default-install-scope-and-group-capability"></a><span data-ttu-id="4183d-103">Agregar un ámbito de instalación predeterminado y una funcionalidad de grupo</span><span class="sxs-lookup"><span data-stu-id="4183d-103">Add a default install scope and group capability</span></span>

<span data-ttu-id="4183d-104">Es común que una aplicación admita varios escenarios en Teams, pero es posible que la haya diseñado con un ámbito y una funcionalidad específicos en mente.</span><span class="sxs-lookup"><span data-stu-id="4183d-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="4183d-105">Por ejemplo, si la aplicación es principalmente para uso de equipo o canal, puedes asegurarte de que la primera opción de instalación que los usuarios ven en la tienda es **Agregar a un equipo**.</span><span class="sxs-lookup"><span data-stu-id="4183d-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

![Agregar una aplicación](../../assets/images/compose-extensions/addanapp.png)

<span data-ttu-id="4183d-107">Si la funcionalidad principal de la aplicación es un bot, también puedes convertir el bot en la funcionalidad predeterminada cuando un usuario instala la aplicación en un equipo.</span><span class="sxs-lookup"><span data-stu-id="4183d-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span> 

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="4183d-108">Configurar el ámbito de instalación predeterminado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4183d-108">Configure your app's default install scope</span></span>

<span data-ttu-id="4183d-109">Configure el ámbito de instalación predeterminado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4183d-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="4183d-110">Solo puede establecer un ámbito a la vez.</span><span class="sxs-lookup"><span data-stu-id="4183d-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="4183d-111">**Para configurar el ámbito de instalación predeterminado en el manifiesto de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="4183d-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="4183d-112">Abre el manifiesto de la aplicación y agrega la `defaultInstallScope` propiedad.</span><span class="sxs-lookup"><span data-stu-id="4183d-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="4183d-113">Establezca un valor de `personal` , `team` , o `groupchat` `meetings` (vea un ejemplo a continuación).</span><span class="sxs-lookup"><span data-stu-id="4183d-113">Set a value of `personal`, `team`, `groupchat`, or `meetings` (see an example below).</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="4183d-114">Para obtener más información, consulta el esquema [de manifiesto de la aplicación](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="4183d-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="4183d-115">Configurar la funcionalidad predeterminada para ámbitos compartidos</span><span class="sxs-lookup"><span data-stu-id="4183d-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="4183d-116">Configura la funcionalidad predeterminada cuando la aplicación esté instalada para un equipo, una reunión o un chat.</span><span class="sxs-lookup"><span data-stu-id="4183d-116">Configure the default capability when your app is installed for a team, meeting, or chat.</span></span>

<span data-ttu-id="4183d-117">**Para configurar detalles en el manifiesto de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="4183d-117">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="4183d-118">Abre el manifiesto de la aplicación y agrega la `defaultGroupCapability` propiedad a él.</span><span class="sxs-lookup"><span data-stu-id="4183d-118">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="4183d-119">Guarde las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="4183d-119">Save the updates.</span></span>

    <span data-ttu-id="4183d-120">A continuación se muestra un ejemplo json:</span><span class="sxs-lookup"><span data-stu-id="4183d-120">Following is a JSON example:</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```
> [!NOTE]
> <span data-ttu-id="4183d-121">Para obtener información sobre el esquema completo, vea [esquema de manifiesto](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="4183d-121">For information on full schema, see [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="4183d-122">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="4183d-122">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4183d-123">Elegir cómo distribuir la aplicación</span><span class="sxs-lookup"><span data-stu-id="4183d-123">Choose how to distribute your app</span></span>](overview.md)
