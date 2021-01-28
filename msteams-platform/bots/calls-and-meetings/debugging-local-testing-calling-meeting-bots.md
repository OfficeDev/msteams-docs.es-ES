---
title: Depurar el bot de llamadas y reuniones de forma local
description: Obtén información sobre cómo también puedes usar ngrok para desarrollar llamadas y bots de reunión en línea en tu equipo local.
ms.topic: how-to
keywords: túnel ngrok de desarrollo local
ms.date: 11/18/2018
ms.openlocfilehash: e9b77df18c8d80f02134dc7912b5796023082039
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014309"
---
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="1a7de-104">Cómo desarrollar bots de llamadas y reuniones en línea en el equipo local</span><span class="sxs-lookup"><span data-stu-id="1a7de-104">How to develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="1a7de-105">En [Ejecutar y depurar la aplicación,](../../concepts/build-and-test/debug.md) explicamos cómo usar [ngrok](https://ngrok.com) para crear un túnel entre el equipo local e Internet.</span><span class="sxs-lookup"><span data-stu-id="1a7de-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="1a7de-106">En este tema, obtén información sobre cómo también puedes usar ngrok y el equipo local para desarrollar bots que admitan llamadas y reuniones en línea.</span><span class="sxs-lookup"><span data-stu-id="1a7de-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="1a7de-107">Los bots de mensajería usan HTTP, pero los bots de llamadas y reuniones en línea usan el TCP de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="1a7de-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="1a7de-108">Ngrok admite túneles TCP además de túneles HTTP; aprenderá cómo hacerlo a continuación.</span><span class="sxs-lookup"><span data-stu-id="1a7de-108">Ngrok supports TCP tunnels in addition to HTTP tunnels; you'll learn how, below.</span></span>

## <a name="configuring-ngrokyml"></a><span data-ttu-id="1a7de-109">Configuración de ngrok.yml</span><span class="sxs-lookup"><span data-stu-id="1a7de-109">Configuring ngrok.yml</span></span>

<span data-ttu-id="1a7de-110">Vaya a [ngrok y](https://ngrok.com) regístrese para obtener una cuenta gratuita o inicie sesión en su cuenta existente.</span><span class="sxs-lookup"><span data-stu-id="1a7de-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="1a7de-111">Una vez que haya iniciado sesión, vaya al [panel](https://dashboard.ngrok.com) y obtenga el authtoken.</span><span class="sxs-lookup"><span data-stu-id="1a7de-111">Once you've logged in, go to the [dashboard](https://dashboard.ngrok.com) and get your authtoken.</span></span>

<span data-ttu-id="1a7de-112">Crea un archivo de configuración ngrok (consulta aquí para obtener más información sobre dónde se puede encontrar este archivo) y `ngrok.yml` agrega esta línea: [](https://ngrok.com/docs#config)</span><span class="sxs-lookup"><span data-stu-id="1a7de-112">Create an ngrok configuration file `ngrok.yml` (see [here](https://ngrok.com/docs#config) for more information on where this file can be located) and add this line:</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a><span data-ttu-id="1a7de-113">Configuración de señalización</span><span class="sxs-lookup"><span data-stu-id="1a7de-113">Setting up signaling</span></span>

<span data-ttu-id="1a7de-114">En [los bots de](./calls-meetings-bots-overview.md)llamadas y reuniones en línea, analizamos la señalización de llamadas: cómo los bots detectan y responden a nuevas llamadas y eventos durante una llamada.</span><span class="sxs-lookup"><span data-stu-id="1a7de-114">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling — how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="1a7de-115">Los eventos de señalización de llamadas se envían a través de HTTP POST al extremo de llamada del bot.</span><span class="sxs-lookup"><span data-stu-id="1a7de-115">Call signaling events are sent via HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="1a7de-116">Al igual que con la API de mensajería del bot, para que la plataforma de medios en tiempo real hable con el bot, el bot debe estar accesible a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="1a7de-116">As with the bot's messaging API, in order for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="1a7de-117">Ngrok hace que esto sea sencillo: agregue las siguientes líneas a ngrok.yml:</span><span class="sxs-lookup"><span data-stu-id="1a7de-117">Ngrok makes this simple — add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a><span data-ttu-id="1a7de-118">Configuración de medios locales</span><span class="sxs-lookup"><span data-stu-id="1a7de-118">Setting up local media</span></span>

> [!NOTE]
> <span data-ttu-id="1a7de-119">Esta sección solo es necesaria para los bots multimedia hospedados en la aplicación y se puede omitir si no hospeda medios usted mismo.</span><span class="sxs-lookup"><span data-stu-id="1a7de-119">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="1a7de-120">Los medios hospedados en aplicaciones usan certificados y túneles TCP.</span><span class="sxs-lookup"><span data-stu-id="1a7de-120">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="1a7de-121">Se requieren los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="1a7de-121">The following steps are required:</span></span>

- <span data-ttu-id="1a7de-122">Los extremos TCP públicos de Ngrok tienen direcciones URL fijas.</span><span class="sxs-lookup"><span data-stu-id="1a7de-122">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="1a7de-123">Son, `0.tcp.ngrok.io` `1.tcp.ngrok.io` y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="1a7de-123">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="1a7de-124">Debe tener una entrada CNAME de DNS para el servicio que apunta a estas direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="1a7de-124">You should have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="1a7de-125">En este ejemplo, supongamos que hace referencia a `0.bot.contoso.com` , hace referencia a , y así `0.tcp.ngrok.io` `1.bot.contoso.com` `1.tcp.ngrok.io` sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="1a7de-125">In this example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
- <span data-ttu-id="1a7de-126">Se requiere un certificado SSL para las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="1a7de-126">A SSL certificate is required for your URLs.</span></span> <span data-ttu-id="1a7de-127">Para facilitarlo, use un certificado SSL emitido a un dominio de comodín.</span><span class="sxs-lookup"><span data-stu-id="1a7de-127">To make it easy, use a SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="1a7de-128">En este caso, sería `*.bot.contoso.com` .</span><span class="sxs-lookup"><span data-stu-id="1a7de-128">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="1a7de-129">El SDK de medios valida este certificado SSL, por lo que debe coincidir con la dirección URL pública del bot.</span><span class="sxs-lookup"><span data-stu-id="1a7de-129">This SSL certificate is validated by the media SDK, so it should match your bot's public URL.</span></span> <span data-ttu-id="1a7de-130">Ten en cuenta la huella digital e instálrala en los certificados de la máquina.</span><span class="sxs-lookup"><span data-stu-id="1a7de-130">Note the thumbprint and install it in your machine certificates.</span></span>
- <span data-ttu-id="1a7de-131">Ahora, configure un túnel TCP para reenviar el tráfico a localhost.</span><span class="sxs-lookup"><span data-stu-id="1a7de-131">Now, setup a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="1a7de-132">Escriba las siguientes líneas en ngrok.yml:</span><span class="sxs-lookup"><span data-stu-id="1a7de-132">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="1a7de-133">Iniciar ngrok</span><span class="sxs-lookup"><span data-stu-id="1a7de-133">Start ngrok</span></span>

<span data-ttu-id="1a7de-134">Ahora que la configuración de ngrok está lista, indándala:</span><span class="sxs-lookup"><span data-stu-id="1a7de-134">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="1a7de-135">Esto inicia ngrok y define las direcciones URL públicas que proporcionan los túneles al host local.</span><span class="sxs-lookup"><span data-stu-id="1a7de-135">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="1a7de-136">El resultado es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="1a7de-136">The output looks like the following:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="1a7de-137">Este es el puerto de señalización, es el puerto hospedado por la aplicación y es el puerto multimedia remoto `12345` `8445` expuesto por `12332` ngrok.</span><span class="sxs-lookup"><span data-stu-id="1a7de-137">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="1a7de-138">Tenga en cuenta que tenemos un reenvío de `1.bot.contoso.com` a `1.tcp.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="1a7de-138">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="1a7de-139">Se usará como la dirección URL multimedia del bot.</span><span class="sxs-lookup"><span data-stu-id="1a7de-139">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="1a7de-140">Por supuesto, estos números de puerto son solo ejemplos y puede usar cualquier puerto disponible.</span><span class="sxs-lookup"><span data-stu-id="1a7de-140">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="1a7de-141">Actualización del código</span><span class="sxs-lookup"><span data-stu-id="1a7de-141">Update code</span></span>

<span data-ttu-id="1a7de-142">Una vez que ngrok esté en funcionamiento, actualice el código para usar la configuración que acaba de configurar.</span><span class="sxs-lookup"><span data-stu-id="1a7de-142">Once ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="1a7de-143">Actualizar señalización</span><span class="sxs-lookup"><span data-stu-id="1a7de-143">Update signaling</span></span>

- <span data-ttu-id="1a7de-144">En la llamada de BotBuilder, cambie la dirección URL de señalización `NotificationUrl` proporcionada por ngrok.</span><span class="sxs-lookup"><span data-stu-id="1a7de-144">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="1a7de-145">Reemplace la señal por la que proporciona ngrok y la ruta de acceso `NotificationEndpoint` del controlador que recibe la notificación.</span><span class="sxs-lookup"><span data-stu-id="1a7de-145">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> <span data-ttu-id="1a7de-146">**IMPORTANTE:** La dirección URL debe `SetNotificationUrl` ser HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1a7de-146">**IMPORTANT**: The URL in `SetNotificationUrl` must be HTTPS.</span></span>

> <span data-ttu-id="1a7de-147">**IMPORTANTE:** La instancia local debe estar escuchando el tráfico HTTP en el puerto de señalización.</span><span class="sxs-lookup"><span data-stu-id="1a7de-147">**IMPORTANT**: Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="1a7de-148">Las solicitudes realizadas por la plataforma de llamadas y reuniones en línea llegarán al bot como tráfico HTTP localhost a menos que se configure el cifrado de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="1a7de-148">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="1a7de-149">Actualizar contenido multimedia</span><span class="sxs-lookup"><span data-stu-id="1a7de-149">Update media</span></span>

<span data-ttu-id="1a7de-150">Actualice el `MediaPlatformSettings` archivo a lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="1a7de-150">Update your `MediaPlatformSettings` to the following.</span></span>

```csharp
var mediaPlatform = new MediaPlatformSettings
{
    ApplicationId = <Your application id>
    MediaPlatformInstanceSettings = new MediaPlatformInstanceSettings
    {
        CertificateThumbprint = <Your SSL Cert thumbprint>,
        InstanceInternalPort = <Localhost media port>,
        InstancePublicPort = <Ngrok exposed remote media port>,
        InstancePublicIPAddress = new IPAddress(0x0),
        ServiceFqdn = <Media url for bot (eg: 1.bot.contoso.com)>,
    },
}
```

> [!NOTE]
> <span data-ttu-id="1a7de-151">La huella digital del certificado proporcionada anteriormente debe coincidir con el FQDN del servicio.</span><span class="sxs-lookup"><span data-stu-id="1a7de-151">The certificate thumbprint provided above should match the Service FQDN.</span></span> <span data-ttu-id="1a7de-152">Por eso se requieren las entradas DNS.</span><span class="sxs-lookup"><span data-stu-id="1a7de-152">That is why the DNS entries are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a7de-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a7de-153">Next steps</span></span>

<span data-ttu-id="1a7de-154">El bot ahora puede ejecutarse localmente y todos los flujos funcionan desde el host local.</span><span class="sxs-lookup"><span data-stu-id="1a7de-154">Your bot can now run locally and all the flows work from your localhost.</span></span>

## <a name="caveats"></a><span data-ttu-id="1a7de-155">Advertencias</span><span class="sxs-lookup"><span data-stu-id="1a7de-155">Caveats</span></span>

- <span data-ttu-id="1a7de-156">Las cuentas gratuitas de Ngrok **no proporcionan** cifrado de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="1a7de-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="1a7de-157">Los datos HTTPS terminan en la dirección URL de ngrok y los flujos de datos no cifrados de ngrok a `localhost` .</span><span class="sxs-lookup"><span data-stu-id="1a7de-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="1a7de-158">Si necesita cifrado de un extremo a otro, considere la posibilidad de usar una cuenta de ngrok de pago.</span><span class="sxs-lookup"><span data-stu-id="1a7de-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="1a7de-159">Consulte [los túneles TLS](https://ngrok.com/docs#tls) para ver los pasos para configurar túneles seguros de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="1a7de-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="1a7de-160">Dado que la dirección URL de devolución de llamada del bot es dinámica, los escenarios de llamadas entrantes requieren que actualice con frecuencia los puntos de conexión de ngrok.</span><span class="sxs-lookup"><span data-stu-id="1a7de-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="1a7de-161">Una forma de corregir esto es usar una cuenta de ngrok de pago que proporciona subdominios fijos a los que puede apuntar el bot y la plataforma.</span><span class="sxs-lookup"><span data-stu-id="1a7de-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="1a7de-162">Los túneles de Ngrok también se pueden usar con [Azure Service Fabric.](/azure/service-fabric/service-fabric-overview)</span><span class="sxs-lookup"><span data-stu-id="1a7de-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="1a7de-163">Para obtener un ejemplo de cómo hacerlo, consulta la aplicación [de ejemplo HueBot](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span><span class="sxs-lookup"><span data-stu-id="1a7de-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
