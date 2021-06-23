---
title: Crear una extensión de mensajería usando App Studio
author: surbhigupta
description: Obtén información sobre cómo crear una Microsoft Teams de mensajería con App Studio.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 61bfed969b981bd5000bdb6eca0bbd77196e8086
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069222"
---
# <a name="create-a-messaging-extension-using-app-studio"></a><span data-ttu-id="8c823-103">Crear una extensión de mensajería usando App Studio</span><span class="sxs-lookup"><span data-stu-id="8c823-103">Create a messaging extension using App Studio</span></span>

> [!TIP]
> <span data-ttu-id="8c823-104">¿Está buscando una forma más rápida de empezar?</span><span class="sxs-lookup"><span data-stu-id="8c823-104">Looking for a faster way to get started?</span></span> <span data-ttu-id="8c823-105">Cree una [extensión de mensajería](../build-your-first-app/build-messaging-extension.md) mediante el Microsoft Teams Toolkit.</span><span class="sxs-lookup"><span data-stu-id="8c823-105">Create a [messaging extension](../build-your-first-app/build-messaging-extension.md) using the Microsoft Teams Toolkit.</span></span>

<span data-ttu-id="8c823-106">En un nivel alto, deberá completar los siguientes pasos para crear una extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8c823-106">At a high level, you'll need to complete the following steps to create a messaging extension.</span></span>

1. <span data-ttu-id="8c823-107">Preparar el entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="8c823-107">Prepare your development environment</span></span>
2. <span data-ttu-id="8c823-108">Crear e implementar el servicio web (mientras se desarrolla, use un servicio de túnel como ngrok para ejecutarlo localmente)</span><span class="sxs-lookup"><span data-stu-id="8c823-108">Create and deploy your web service (while developing use a tunneling service like ngrok to run it locally)</span></span>
3. <span data-ttu-id="8c823-109">Registrar el servicio web con Bot Framework</span><span class="sxs-lookup"><span data-stu-id="8c823-109">Register your web service with the Bot Framework</span></span>
4. <span data-ttu-id="8c823-110">Crear el paquete de aplicación</span><span class="sxs-lookup"><span data-stu-id="8c823-110">Create your app package</span></span>
5. <span data-ttu-id="8c823-111">Cargar el paquete en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8c823-111">Upload your package to Microsoft Teams</span></span>

<span data-ttu-id="8c823-112">La creación del servicio web, la creación del paquete de la aplicación y el registro del servicio web con Bot Framework se pueden realizar en cualquier orden.</span><span class="sxs-lookup"><span data-stu-id="8c823-112">Creating your web service, creating your app package, and registering your web service with the Bot Framework can be done in any order.</span></span> <span data-ttu-id="8c823-113">Dado que estas tres piezas están entrelazadas, independientemente del orden en el que las realice, tendrá que volver a actualizar las otras.</span><span class="sxs-lookup"><span data-stu-id="8c823-113">Because those three pieces are so intertwined, no matter which order you do them in you'll need return to update the others.</span></span> <span data-ttu-id="8c823-114">El registro necesita el extremo de mensajería del servicio web implementado y el servicio web necesita el identificador y la contraseña creados a partir del registro.</span><span class="sxs-lookup"><span data-stu-id="8c823-114">Your registration needs the messaging endpoint from your deployed web service, and your web service needs the Id and password created from your registration.</span></span> <span data-ttu-id="8c823-115">El manifiesto de la aplicación también necesita ese identificador para conectarse Teams al servicio web.</span><span class="sxs-lookup"><span data-stu-id="8c823-115">Your app manifest also needs that Id to connect Teams to your web service.</span></span>

<span data-ttu-id="8c823-116">Al crear la extensión de mensajería, se mueve regularmente entre cambiar el manifiesto de la aplicación e implementar código en el servicio web.</span><span class="sxs-lookup"><span data-stu-id="8c823-116">As you're building your messaging extension, you'll regularly be moving between changing your app manifest, and deploying code to your web service.</span></span> <span data-ttu-id="8c823-117">Al trabajar con el manifiesto de la aplicación, ten en cuenta que puedes manipular manualmente el archivo JSON o realizar cambios a través de App Studio.</span><span class="sxs-lookup"><span data-stu-id="8c823-117">When working with the app manifest, keep in mind that you can either manually manipulate the JSON file, or make changes through App Studio.</span></span> <span data-ttu-id="8c823-118">En cualquier caso, tendrás que volver a implementar (cargar) la aplicación en Teams cuando realices un cambio en el manifiesto, pero no es necesario hacerlo al implementar cambios en el servicio web.</span><span class="sxs-lookup"><span data-stu-id="8c823-118">Either way, you'll need to re-deploy (upload) your app in Teams when you make a change to the manifest, but there's no need to do so when you deploy changes to your web service.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a><span data-ttu-id="8c823-119">Crear su servicio web</span><span class="sxs-lookup"><span data-stu-id="8c823-119">Create your web service</span></span>

<span data-ttu-id="8c823-120">El corazón de la extensión de mensajería es el servicio web.</span><span class="sxs-lookup"><span data-stu-id="8c823-120">The heart of your messaging extension is your web service.</span></span> <span data-ttu-id="8c823-121">Definirá una sola ruta, normalmente `/api/messages` , para recibir todas las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="8c823-121">It will define a single route, typically `/api/messages`, to receive all requests on.</span></span> <span data-ttu-id="8c823-122">Si estás empezando desde cero, tienes algunas opciones entre las que elegir.</span><span class="sxs-lookup"><span data-stu-id="8c823-122">If you're getting started from scratch, you have a few options to choose from.</span></span>

* <span data-ttu-id="8c823-123">Use uno de nuestros [tutoriales de inicio rápido](#learn-more) que le guiará a través de la creación de su servicio web.</span><span class="sxs-lookup"><span data-stu-id="8c823-123">Use one of our [quickstarts](#learn-more) tutorials that will guide you through the creation of your web service.</span></span>
* <span data-ttu-id="8c823-124">Elija uno de los ejemplos de extensión de mensajería disponibles en el repositorio de ejemplo [de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples) desde el que empezar.</span><span class="sxs-lookup"><span data-stu-id="8c823-124">Choose one of the messaging extension samples available in the [Bot Framework sample repository](https://github.com/Microsoft/BotBuilder-Samples) to start from.</span></span>
* <span data-ttu-id="8c823-125">Si usa JavaScript, use el generador [de Yeoman](https://github.com/OfficeDev/generator-teams) para Microsoft Teams scaffolding de la aplicación Teams, incluido el servicio web.</span><span class="sxs-lookup"><span data-stu-id="8c823-125">If you're using JavaScript, use the [Yeoman generator for Microsoft Teams](https://github.com/OfficeDev/generator-teams) to scaffold your Teams app, including your web service.</span></span>
* <span data-ttu-id="8c823-126">Crear su servicio web desde cero.</span><span class="sxs-lookup"><span data-stu-id="8c823-126">Create your web service from scratch.</span></span> <span data-ttu-id="8c823-127">Puede optar por agregar el SDK de Bot Framework para su idioma, o bien puede trabajar directamente con las cargas JSON.</span><span class="sxs-lookup"><span data-stu-id="8c823-127">You can choose to add the Bot Framework SDK for your language, or you can work directly with the JSON payloads.</span></span>

## <a name="register-your-web-service-with-the-bot-framework"></a><span data-ttu-id="8c823-128">Registrar el servicio web con Bot Framework</span><span class="sxs-lookup"><span data-stu-id="8c823-128">Register your web service with the Bot Framework</span></span>

<span data-ttu-id="8c823-129">Las extensiones de mensajería aprovechan el esquema de mensajería del Bot Framework y el protocolo de comunicación segura; si aún no tiene uno, deberá registrar el servicio web en Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="8c823-129">Messaging extensions take advantage of the Bot Framework's messaging schema and secure communication protocol; if you don't already have one you'll need to register your web service on the Bot Framework.</span></span> <span data-ttu-id="8c823-130">El Id. de aplicación de Microsoft (nos referiremos a esto como el Identificador de bot desde dentro de Teams, para identificarlo desde otros identificadores de aplicación con los que podría estar trabajando) y el extremo de mensajería con el que se registrará con Bot Framework se usará en la extensión de mensajería para recibir y responder a las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="8c823-130">The Microsoft App Id (we'll refer to this as your Bot Id from inside of Teams, to identify it from other App Id's you might be working with) and the messaging endpoint your register with the Bot Framework will be used in your messaging extension to receive and respond to requests.</span></span> <span data-ttu-id="8c823-131">Si usa un registro existente, asegúrese de habilitar el canal [Microsoft Teams .](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8c823-131">If you're using an existing registration, make sure you [enable the Microsoft Teams channel](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="8c823-132">Si sigue uno de los inicios rápidos o empieza desde uno de los ejemplos disponibles, se le guiará a través del registro del servicio web.</span><span class="sxs-lookup"><span data-stu-id="8c823-132">If you follow one of the quickstarts or start from one of the available samples you'll be guided through registering your web service.</span></span> <span data-ttu-id="8c823-133">Si desea registrar manualmente el servicio, tiene tres opciones para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="8c823-133">If you want to manually register your service you have three options to do so.</span></span> <span data-ttu-id="8c823-134">Si decide registrarse sin usar una suscripción de Azure, no podrá aprovechar el flujo simplificado de autenticación de OAuth proporcionado por Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="8c823-134">If you choose to register without using an Azure subscription you will not be able to take advantage of the simplified OAuth authentication flow provided by the Bot Framework.</span></span> <span data-ttu-id="8c823-135">Podrás migrar el registro a Azure después de la creación.</span><span class="sxs-lookup"><span data-stu-id="8c823-135">You will be able to migrate your registration to Azure after creation.</span></span>

* <span data-ttu-id="8c823-136">Si tiene una suscripción de Azure (o desea crear una nueva), puede registrar el servicio web manualmente mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8c823-136">If you have an Azure subscription (or want to create a new one), you can register your web service manually using the Azure Portal.</span></span> <span data-ttu-id="8c823-137">Cree un recurso "Registro de canales de bot".</span><span class="sxs-lookup"><span data-stu-id="8c823-137">Create a "Bot Channels Registration" resource.</span></span> <span data-ttu-id="8c823-138">Puedes elegir el nivel de precios gratuito, ya que los mensajes de Microsoft Teams no cuentan para el total de mensajes permitidos al mes.</span><span class="sxs-lookup"><span data-stu-id="8c823-138">You can choose the free pricing tier, as messages from Microsoft Teams do not count towards your total allowable messages per month.</span></span>
* <span data-ttu-id="8c823-139">Si no desea usar una suscripción de Azure, puede usar el [portal de registro heredado](https://dev.botframework.com/bots/new).</span><span class="sxs-lookup"><span data-stu-id="8c823-139">If you do not wish to use an Azure subscription, you can use the [legacy registration portal](https://dev.botframework.com/bots/new).</span></span>
* <span data-ttu-id="8c823-140">App Studio también puede ayudarte a registrar el servicio web (bot).</span><span class="sxs-lookup"><span data-stu-id="8c823-140">App Studio can also help you register your web service (bot).</span></span> <span data-ttu-id="8c823-141">Los servicios web registrados a través de App Studio no están registrados en Azure.</span><span class="sxs-lookup"><span data-stu-id="8c823-141">Web services registered through App Studio are not registered in Azure.</span></span> <span data-ttu-id="8c823-142">Puede usar el [portal heredado para](https://dev.botframework.com/bots) ver, administrar y migrar los registros.</span><span class="sxs-lookup"><span data-stu-id="8c823-142">You can use the [legacy portal](https://dev.botframework.com/bots) to view, manage, and migrate your registrations.</span></span>

## <a name="create-your-app-manifest"></a><span data-ttu-id="8c823-143">Crear el manifiesto de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8c823-143">Create your app manifest</span></span>

<span data-ttu-id="8c823-144">Puede usar App Studio para ayudarle a crear el manifiesto de la aplicación, o bien crearlo de forma manual.</span><span class="sxs-lookup"><span data-stu-id="8c823-144">You can either use App Studio to help you create your app manifest, or create it manually.</span></span>

### <a name="create-your-app-manifest-using-app-studio"></a><span data-ttu-id="8c823-145">Crear el manifiesto de la aplicación con App Studio</span><span class="sxs-lookup"><span data-stu-id="8c823-145">Create your app manifest using App Studio</span></span>

<span data-ttu-id="8c823-146">Puedes usar la aplicación app Studio desde el cliente Microsoft Teams para ayudar a crear el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8c823-146">You can use the App Studio app from within the Microsoft Teams client to help create your app manifest.</span></span>

1. <span data-ttu-id="8c823-147">En el cliente de Teams, abra App Studio en el menú de desbordamiento **...** del raíl de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="8c823-147">In the Teams client, open App Studio from the **...** overflow menu on the left navigation rail.</span></span> <span data-ttu-id="8c823-148">Si aún no está instalado, puede hacerlo buscándolo.</span><span class="sxs-lookup"><span data-stu-id="8c823-148">If it isn't already installed, you can do so by searching for it.</span></span>
2. <span data-ttu-id="8c823-149">En la **pestaña Editor de manifiestos,** selecciona **Crear** una nueva aplicación (o si estás agregando una extensión de mensajería a una aplicación existente, puedes importar el paquete de la aplicación)</span><span class="sxs-lookup"><span data-stu-id="8c823-149">On the **Manifest editor** tab select **Create a new app** (or if you're adding a messaging extension to an existing app, you can import your app package)</span></span>
3. <span data-ttu-id="8c823-150">Agregue los detalles de la aplicación (consulte [definición de esquema de manifiesto](~/resources/schema/manifest-schema.md) para obtener las descripciones completas de cada campo).</span><span class="sxs-lookup"><span data-stu-id="8c823-150">Add your app details (see [manifest schema definition](~/resources/schema/manifest-schema.md) for full descriptions of each field).</span></span>
4. <span data-ttu-id="8c823-151">En la **pestaña Extensiones de mensajería,** haga clic en **el botón Configurar.**</span><span class="sxs-lookup"><span data-stu-id="8c823-151">On the **Messaging extensions** tab click the **Setup** button.</span></span>
5. <span data-ttu-id="8c823-152">Puede crear un nuevo servicio web (bot) para que la extensión de mensajería lo use, o si ya ha registrado un select/add it aquí.</span><span class="sxs-lookup"><span data-stu-id="8c823-152">You can either create a new web service (bot) for your messaging extension to use, or if you've already registered one select/add it here.</span></span>
6. <span data-ttu-id="8c823-153">Si es necesario, actualice la dirección del extremo del bot para que apunte a su bot.</span><span class="sxs-lookup"><span data-stu-id="8c823-153">If necessary, update your bot endpoint address to point to your bot.</span></span> <span data-ttu-id="8c823-154">Debería tener un aspecto similar a `https://someplace.com/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="8c823-154">It should look something like `https://someplace.com/api/messages`.</span></span>
7. <span data-ttu-id="8c823-155">El **botón** Agregar de la **sección Comando** le guiará a través de la adición de comandos a la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8c823-155">The **Add** button in the **Command** section will guide you through adding commands to your messaging extension.</span></span> <span data-ttu-id="8c823-156">Vea la [sección Más información](#learn-more) para obtener vínculos a más información sobre cómo agregar comandos.</span><span class="sxs-lookup"><span data-stu-id="8c823-156">See the [Learn more](#learn-more) section for links to more information on adding commands.</span></span> <span data-ttu-id="8c823-157">Recuerde que puede definir hasta 10 comandos para la extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8c823-157">Remember you can define up to 10 commands for your messaging extension.</span></span>
8. <span data-ttu-id="8c823-158">La **sección Controladores de mensajes** le permite agregar un dominio en el que se desencadenará la mensajería.</span><span class="sxs-lookup"><span data-stu-id="8c823-158">The **Message Handlers** section allows you to add a domain that your messaging will trigger on.</span></span> <span data-ttu-id="8c823-159">Vea [deshacer vínculos para](~/messaging-extensions/how-to/link-unfurling.md) obtener más información.</span><span class="sxs-lookup"><span data-stu-id="8c823-159">See [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) for more information.</span></span>

<span data-ttu-id="8c823-160">En la pestaña **Finalizar =>** Probar  y distribuir puedes descargar el paquete de la aplicación (que incluye el manifiesto de la aplicación, así como los iconos de la aplicación) o **Instalar** el paquete.</span><span class="sxs-lookup"><span data-stu-id="8c823-160">From the **Finish => Test and distribute** tab you can **Download** your app package (which includes your app manifest as well as your app icons), or **Install** the package.</span></span>

### <a name="create-your-app-manifest-manually"></a><span data-ttu-id="8c823-161">Crear el manifiesto de la aplicación manualmente</span><span class="sxs-lookup"><span data-stu-id="8c823-161">Create your app manifest manually</span></span>

<span data-ttu-id="8c823-162">Al igual que con los bots y las pestañas, actualizas [el](~/resources/schema/manifest-schema.md#composeextensions) manifiesto de la aplicación para incluir las propiedades de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8c823-162">As with bots and tabs, you update the [app manifest](~/resources/schema/manifest-schema.md#composeextensions) of your app to include the messaging extension properties.</span></span> <span data-ttu-id="8c823-163">Estas propiedades rigen cómo aparece y se comporta la extensión de mensajería en el Microsoft Teams cliente.</span><span class="sxs-lookup"><span data-stu-id="8c823-163">These properties govern how your messaging extension appears and behaves in the Microsoft Teams client.</span></span> <span data-ttu-id="8c823-164">Las extensiones de mensajería se admiten a partir de la versión 1.0 del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="8c823-164">Messaging extensions are supported beginning with v1.0 of the manifest.</span></span>

#### <a name="declare-your-messaging-extension"></a><span data-ttu-id="8c823-165">Declarar la extensión de mensajería</span><span class="sxs-lookup"><span data-stu-id="8c823-165">Declare your messaging extension</span></span>

<span data-ttu-id="8c823-166">Para agregar una extensión de mensajería, incluya una nueva estructura JSON de nivel superior en el manifiesto de la aplicación con la `composeExtensions` propiedad.</span><span class="sxs-lookup"><span data-stu-id="8c823-166">To add a messaging extension, include a new top-level JSON structure in your app manifest with the `composeExtensions` property.</span></span> <span data-ttu-id="8c823-167">Creas una sola extensión de mensajería para la aplicación, con hasta 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="8c823-167">You create a single messaging extension for your app, with up to 10 commands.</span></span>

> [!NOTE]
> <span data-ttu-id="8c823-168">El manifiesto hace referencia a las extensiones de mensajería como `composeExtensions` .</span><span class="sxs-lookup"><span data-stu-id="8c823-168">The manifest refers to messaging extensions as `composeExtensions`.</span></span> <span data-ttu-id="8c823-169">Esto es para mantener la compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="8c823-169">This is to maintain backward compatibility.</span></span>

<span data-ttu-id="8c823-170">La definición de extensión es un objeto que tiene la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="8c823-170">The extension definition is an object that has the following structure:</span></span>

| <span data-ttu-id="8c823-171">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="8c823-171">Property name</span></span> | <span data-ttu-id="8c823-172">Objetivo</span><span class="sxs-lookup"><span data-stu-id="8c823-172">Purpose</span></span> | <span data-ttu-id="8c823-173">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="8c823-173">Required?</span></span> |
|---|---|---|
| `botId` | <span data-ttu-id="8c823-174">El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="8c823-174">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="8c823-175">Normalmente, debería ser el mismo que el identificador de la aplicación Teams general.</span><span class="sxs-lookup"><span data-stu-id="8c823-175">This should typically be the same as the ID for your overall Teams app.</span></span> | <span data-ttu-id="8c823-176">Sí</span><span class="sxs-lookup"><span data-stu-id="8c823-176">Yes</span></span> |
| `canUpdateConfiguration` | <span data-ttu-id="8c823-177">Habilita **Configuración** elemento de menú.</span><span class="sxs-lookup"><span data-stu-id="8c823-177">Enables **Settings** menu item.</span></span> | <span data-ttu-id="8c823-178">No</span><span class="sxs-lookup"><span data-stu-id="8c823-178">No</span></span> |
| `commands` | <span data-ttu-id="8c823-179">Matriz de comandos compatibles con esta extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8c823-179">Array of commands that this messaging extension supports.</span></span> <span data-ttu-id="8c823-180">Está limitado a 10 comandos.</span><span class="sxs-lookup"><span data-stu-id="8c823-180">You are limited to 10 commands.</span></span> | <span data-ttu-id="8c823-181">Sí</span><span class="sxs-lookup"><span data-stu-id="8c823-181">Yes</span></span> |

#### <a name="define-your-commands"></a><span data-ttu-id="8c823-182">Definir los comandos</span><span class="sxs-lookup"><span data-stu-id="8c823-182">Define your commands</span></span>

<span data-ttu-id="8c823-183">La extensión de mensajería debe declarar uno o varios comandos, que definen dónde los usuarios pueden desencadenar la extensión de mensajería y el tipo de interacción.</span><span class="sxs-lookup"><span data-stu-id="8c823-183">Your messaging extension should declare one or more commands, which define where your users can trigger your messaging extension, and the type of interaction.</span></span> <span data-ttu-id="8c823-184">Vea [más información para](#learn-more) obtener más información sobre los comandos de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8c823-184">See [learn more](#learn-more) for more information on messaging extension commands.</span></span>

#### <a name="simple-manifest-example"></a><span data-ttu-id="8c823-185">Ejemplo de manifiesto simple</span><span class="sxs-lookup"><span data-stu-id="8c823-185">Simple manifest example</span></span>

<span data-ttu-id="8c823-186">El siguiente ejemplo es un objeto de extensión de mensajería simple en el manifiesto de la aplicación con un comando de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="8c823-186">The following example is a simple messaging extension object in the app manifest with a search command.</span></span> <span data-ttu-id="8c823-187">Este no es el archivo de manifiesto de la aplicación completo, solo la parte específica para las extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="8c823-187">This is not the entire app manifest file, just the part specific to messaging extensions.</span></span> <span data-ttu-id="8c823-188">Consulta [esquema de manifiesto de aplicación](~/resources/schema/manifest-schema.md) para ver un ejemplo completo.</span><span class="sxs-lookup"><span data-stu-id="8c823-188">See [app manifest schema](~/resources/schema/manifest-schema.md) for a complete example.</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "abcd1234-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "searchCmd",
        "description": "Search you ToDo's",
        "title": "Search",
        "initialRun": true,
        "parameters": [
          {
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }
        ]
      }
    ]
  }
]
...
```

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="8c823-189">Ejemplo de manifiesto de aplicación completa</span><span class="sxs-lookup"><span data-stu-id="8c823-189">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

## <a name="add-your-invoke-message-handlers"></a><span data-ttu-id="8c823-190">Agregar los controladores de mensajes de invocación</span><span class="sxs-lookup"><span data-stu-id="8c823-190">Add your invoke message handlers</span></span>

<span data-ttu-id="8c823-191">Cuando los usuarios desencadene la extensión de mensajería, deberá controlar el mensaje de invocación inicial, recopilar información del usuario y, a continuación, procesar esa información y responder correctamente.</span><span class="sxs-lookup"><span data-stu-id="8c823-191">When your users trigger your messaging extension you'll need to handle the initial invoke message, collect some information from the user, then process that information and respond appropriately.</span></span> <span data-ttu-id="8c823-192">Para ello, primero tendrá que decidir qué tipo de comandos desea agregar a [](~/messaging-extensions/how-to/action-commands/define-action-command.md) la extensión de mensajería y agregar comandos de acción o agregar comandos [de búsqueda.](~/messaging-extensions/how-to/search-commands/define-search-command.md)</span><span class="sxs-lookup"><span data-stu-id="8c823-192">To do that, you'll first need to decide what kind of commands you want to add to your messaging extension and either [add an action commands](~/messaging-extensions/how-to/action-commands/define-action-command.md) or [add a search commands](~/messaging-extensions/how-to/search-commands/define-search-command.md).</span></span>

## <a name="messaging-extensions-in-teams-meetings"></a><span data-ttu-id="8c823-193">Extensiones de mensajería en Teams reuniones</span><span class="sxs-lookup"><span data-stu-id="8c823-193">Messaging extensions in Teams meetings</span></span>

> [!NOTE]
> <span data-ttu-id="8c823-194">Si una reunión o un chat de grupo tiene usuarios federados en la lista, Teams elimina el acceso a extensiones de mensajería para todos los usuarios, incluido el organizador.</span><span class="sxs-lookup"><span data-stu-id="8c823-194">If a meeting or group chat has federated users in the roster, Teams suppresses access to messaging extensions for all users, including the organizer.</span></span>

<span data-ttu-id="8c823-195">Una vez que se inicia una reunión, Teams participantes pueden interactuar directamente con la extensión de mensajería durante una llamada en directo.</span><span class="sxs-lookup"><span data-stu-id="8c823-195">Once a meeting begins, Teams participants can interact directly with your messaging extension during a live call.</span></span> <span data-ttu-id="8c823-196">Tenga en cuenta lo siguiente al crear la extensión de mensajería en la reunión:</span><span class="sxs-lookup"><span data-stu-id="8c823-196">Consider the following when building your in-meeting messaging extension:</span></span>

1. <span data-ttu-id="8c823-197">**Location**.</span><span class="sxs-lookup"><span data-stu-id="8c823-197">**Location**.</span></span> <span data-ttu-id="8c823-198">La extensión de mensajería se puede invocar desde el área del mensaje de redacción, el cuadro de comandos o @mentioned en el chat de la reunión.</span><span class="sxs-lookup"><span data-stu-id="8c823-198">Your messaging extension can be invoked from the compose message area, the command box, or @mentioned in the meeting chat.</span></span>

1. <span data-ttu-id="8c823-199">**Metadatos**.</span><span class="sxs-lookup"><span data-stu-id="8c823-199">**Metadata**.</span></span> <span data-ttu-id="8c823-200">Cuando se invoca la extensión de mensajería, puede identificar el usuario y el inquilino `userId` desde y `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="8c823-200">When your messaging extension is invoked it can identify the user and tenant from `userId` and `tenantId`.</span></span> <span data-ttu-id="8c823-201">Se puede encontrar `meetingId` como parte del objeto `channelData`.</span><span class="sxs-lookup"><span data-stu-id="8c823-201">The `meetingId` can be found as part of the `channelData` object.</span></span> <span data-ttu-id="8c823-202">La aplicación puede usar la `userId` solicitud y para la API para recuperar roles de `meetingId` `GetParticipant` usuario.</span><span class="sxs-lookup"><span data-stu-id="8c823-202">Your app can use the `userId` and `meetingId`  for the `GetParticipant` API request to retrieve user roles.</span></span>

1. <span data-ttu-id="8c823-203">**Tipo de comando**.</span><span class="sxs-lookup"><span data-stu-id="8c823-203">**Command type**.</span></span> <span data-ttu-id="8c823-204">Si la extensión de mensaje usa [comandos basados](../messaging-extensions/what-are-messaging-extensions.md#action-commands)en acciones, debe seguir la autenticación de inicio [de sesión único de pestañas.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="8c823-204">If your message extension uses [action-based commands](../messaging-extensions/what-are-messaging-extensions.md#action-commands), it should follow tabs [single sign-on](../tabs/how-to/authentication/auth-aad-sso.md) authentication.</span></span>

1. <span data-ttu-id="8c823-205">**Experiencia del usuario**.</span><span class="sxs-lookup"><span data-stu-id="8c823-205">**User experience**.</span></span> <span data-ttu-id="8c823-206">La extensión de mensajería debe tener el mismo aspecto y comportamiento que fuera de una reunión.</span><span class="sxs-lookup"><span data-stu-id="8c823-206">You messaging extension should look and behave the same as it would outside a meeting.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c823-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c823-207">Next steps</span></span>

* [<span data-ttu-id="8c823-208">Crear comandos de acción</span><span class="sxs-lookup"><span data-stu-id="8c823-208">Create action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="8c823-209">Crear comandos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="8c823-209">Create search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [<span data-ttu-id="8c823-210">Apertura de vínculos</span><span class="sxs-lookup"><span data-stu-id="8c823-210">Link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a><span data-ttu-id="8c823-211">Más información</span><span class="sxs-lookup"><span data-stu-id="8c823-211">Learn more</span></span>

<span data-ttu-id="8c823-212">Pruébalo en un inicio rápido:</span><span class="sxs-lookup"><span data-stu-id="8c823-212">Try it out in a quickstart:</span></span>

* <span data-ttu-id="8c823-213">Inicios rápidos para C #</span><span class="sxs-lookup"><span data-stu-id="8c823-213">Quickstarts for C#</span></span>
  * [<span data-ttu-id="8c823-214">Extensión de mensajería con comandos basados en acciones</span><span class="sxs-lookup"><span data-stu-id="8c823-214">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="8c823-215">Extensión de mensajería con comandos basados en búsqueda</span><span class="sxs-lookup"><span data-stu-id="8c823-215">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* <span data-ttu-id="8c823-216">Inicios rápidos para JavaScript</span><span class="sxs-lookup"><span data-stu-id="8c823-216">Quickstarts for JavaScript</span></span>
  * [<span data-ttu-id="8c823-217">Extensión de mensajería con comandos basados en acciones</span><span class="sxs-lookup"><span data-stu-id="8c823-217">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="8c823-218">Extensión de mensajería con comandos basados en búsqueda</span><span class="sxs-lookup"><span data-stu-id="8c823-218">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

<span data-ttu-id="8c823-219">Obtenga más información sobre Teams de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="8c823-219">Learn more about Teams development concepts:</span></span>

* [<span data-ttu-id="8c823-220">Comprender Teams funcionalidades de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8c823-220">Understand Teams app capabilities</span></span>](../concepts/capabilities-overview.md)
* [<span data-ttu-id="8c823-221">¿Qué son las extensiones de mensajería?</span><span class="sxs-lookup"><span data-stu-id="8c823-221">What are messaging extensions?</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
