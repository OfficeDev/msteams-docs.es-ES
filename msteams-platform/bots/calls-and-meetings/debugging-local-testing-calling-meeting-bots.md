---
title: Depurar el bot de llamadas y reuniones de forma local
description: Obtenga información sobre cómo también puede usar ngrok para desarrollar llamadas y bots de reunión en línea en su equipo local.
ms.topic: how-to
keywords: túnel ngrok de desarrollo local
ms.date: 11/18/2018
ms.openlocfilehash: b764e41302ab569e40c9dacd374a31e6abb1d642
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654289"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="eb0fd-104">Desarrollar bots de llamadas y reuniones en línea en el equipo local</span><span class="sxs-lookup"><span data-stu-id="eb0fd-104">Develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="eb0fd-105">En [Ejecutar y depurar la aplicación](../../concepts/build-and-test/debug.md) te explicamos cómo usar [ngrok](https://ngrok.com) para crear un túnel entre tu equipo local e Internet.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="eb0fd-106">En este tema, obtenga información sobre cómo también puede usar ngrok y su equipo local para desarrollar bots compatibles con llamadas y reuniones en línea.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="eb0fd-107">Los bots de mensajería usan HTTP, pero las llamadas y los bots de reunión en línea usan el TCP de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="eb0fd-108">Ngrok admite túneles TCP además de túneles HTTP.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-108">Ngrok supports TCP tunnels in addition to HTTP tunnels.</span></span> 

## <a name="configure-ngrokyml"></a><span data-ttu-id="eb0fd-109">Configurar ngrok.yml</span><span class="sxs-lookup"><span data-stu-id="eb0fd-109">Configure ngrok.yml</span></span>

<span data-ttu-id="eb0fd-110">Vaya a [ngrok](https://ngrok.com) y regístrese para obtener una cuenta gratuita o inicie sesión en su cuenta existente.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="eb0fd-111">Después de haber iniciado sesión, vaya al [panel y](https://dashboard.ngrok.com) obtenga el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-111">After you've signed in, go to the [dashboard](https://dashboard.ngrok.com) and get your auth token.</span></span>

<span data-ttu-id="eb0fd-112">Cree un archivo de configuración de ngrok `ngrok.yml` y agregue la siguiente línea.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-112">Create an ngrok configuration file `ngrok.yml` and add the following line.</span></span> <span data-ttu-id="eb0fd-113">Para obtener más información sobre dónde se puede encontrar el archivo, [vea ngrok](https://ngrok.com/docs#config):</span><span class="sxs-lookup"><span data-stu-id="eb0fd-113">For more information on where the file can be located, see [ngrok](https://ngrok.com/docs#config):</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a><span data-ttu-id="eb0fd-114">Configurar la señalización</span><span class="sxs-lookup"><span data-stu-id="eb0fd-114">Set up signaling</span></span>

<span data-ttu-id="eb0fd-115">En [bots de llamadas](./calls-meetings-bots-overview.md)y reuniones en línea, hablamos sobre la señalización de llamadas sobre cómo los bots detectan y responden a nuevas llamadas y eventos durante una llamada.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-115">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling on how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="eb0fd-116">Los eventos de señalización de llamadas se envían a través de HTTP POST al extremo de llamada del bot.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-116">Call signaling events are sent through HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="eb0fd-117">Al igual que con la API de mensajería del bot, para que la Plataforma multimedia en tiempo real hable con el bot, el bot debe ser accesible a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-117">As with the bot's messaging API, for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="eb0fd-118">Ngrok hace que esto sea sencillo.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-118">Ngrok makes this simple.</span></span> <span data-ttu-id="eb0fd-119">Agregue las siguientes líneas a su ngrok.yml:</span><span class="sxs-lookup"><span data-stu-id="eb0fd-119">Add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a><span data-ttu-id="eb0fd-120">Configurar medios locales</span><span class="sxs-lookup"><span data-stu-id="eb0fd-120">Set up local media</span></span>

> [!NOTE]
> <span data-ttu-id="eb0fd-121">Esta sección solo es necesaria para los bots multimedia hospedados en aplicaciones y se puede omitir si no hospeda los medios usted mismo.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-121">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="eb0fd-122">Los medios hospedados en aplicaciones usan certificados y túneles TCP.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-122">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="eb0fd-123">Se requieren los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="eb0fd-123">The following steps are required:</span></span>

1. <span data-ttu-id="eb0fd-124">Los puntos de conexión TCP públicos de Ngrok tienen direcciones URL fijas.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-124">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="eb0fd-125">Son `0.tcp.ngrok.io` , `1.tcp.ngrok.io` y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-125">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="eb0fd-126">Debe tener una entrada CNAME DNS para el servicio que apunta a estas direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-126">You must have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="eb0fd-127">Por ejemplo, supongamos que hace `0.bot.contoso.com` referencia a , hace referencia a , y así `0.tcp.ngrok.io` `1.bot.contoso.com` `1.tcp.ngrok.io` sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-127">For example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
2. <span data-ttu-id="eb0fd-128">Se requiere un certificado SSL para las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-128">An SSL certificate is required for your URLs.</span></span> <span data-ttu-id="eb0fd-129">Para facilitarlo, use un certificado SSL emitido a un dominio de comodín.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-129">To make it easy, use an SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="eb0fd-130">En este caso, sería `*.bot.contoso.com` .</span><span class="sxs-lookup"><span data-stu-id="eb0fd-130">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="eb0fd-131">El SDK multimedia valida este certificado SSL, por lo que debe coincidir con la dirección URL pública del bot.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-131">This SSL certificate is validated by the media SDK, so it must match your bot's public URL.</span></span> <span data-ttu-id="eb0fd-132">Tenga en cuenta la huella digital e instálesla en los certificados de la máquina.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-132">Note the thumbprint and install it in your machine certificates.</span></span>
3. <span data-ttu-id="eb0fd-133">Ahora, configure un túnel TCP para reenviar el tráfico a localhost.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-133">Now, set up a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="eb0fd-134">Escriba las siguientes líneas en su ngrok.yml:</span><span class="sxs-lookup"><span data-stu-id="eb0fd-134">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="eb0fd-135">Iniciar ngrok</span><span class="sxs-lookup"><span data-stu-id="eb0fd-135">Start ngrok</span></span>

<span data-ttu-id="eb0fd-136">Ahora que la configuración de ngrok está lista, inicie:</span><span class="sxs-lookup"><span data-stu-id="eb0fd-136">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="eb0fd-137">Esto inicia ngrok y define las direcciones URL públicas que proporcionan los túneles al host local.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-137">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="eb0fd-138">A continuación se muestra un ejemplo de la salida:</span><span class="sxs-lookup"><span data-stu-id="eb0fd-138">Following is an example of the output:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="eb0fd-139">Aquí, es el puerto de señalización, es el puerto hospedado por la aplicación y es el puerto multimedia remoto `12345` `8445` expuesto por `12332` ngrok.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-139">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="eb0fd-140">Tenga en cuenta que tenemos un reenvío de `1.bot.contoso.com` a `1.tcp.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="eb0fd-140">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="eb0fd-141">Se usará como la dirección URL multimedia del bot.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-141">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="eb0fd-142">Por supuesto, estos números de puerto son solo ejemplos y puede usar cualquier puerto disponible.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-142">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="eb0fd-143">Actualización del código</span><span class="sxs-lookup"><span data-stu-id="eb0fd-143">Update code</span></span>

<span data-ttu-id="eb0fd-144">Después de que ngrok esté en funcionamiento, actualice el código para usar la configuración que acaba de configurar.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-144">After ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="eb0fd-145">Actualizar señalización</span><span class="sxs-lookup"><span data-stu-id="eb0fd-145">Update signaling</span></span>

<span data-ttu-id="eb0fd-146">En la llamada a BotBuilder, cambie la dirección URL de señalización `NotificationUrl` proporcionada por ngrok.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-146">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="eb0fd-147">Reemplace la señal por la proporcionada por ngrok y la ruta de acceso `NotificationEndpoint` del controlador que recibe la notificación.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-147">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="eb0fd-148">La dirección URL en `SetNotificationUrl` debe ser HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-148">The URL in `SetNotificationUrl` must be HTTPS.</span></span>
> 
> <span data-ttu-id="eb0fd-149">La instancia local debe estar escuchando el tráfico HTTP en el puerto de señalización.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-149">Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="eb0fd-150">Las solicitudes realizadas por la plataforma de llamadas y reuniones en línea llegarán al bot como tráfico HTTP localhost a menos que se configure el cifrado de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-150">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="eb0fd-151">Actualizar medios</span><span class="sxs-lookup"><span data-stu-id="eb0fd-151">Update media</span></span>

<span data-ttu-id="eb0fd-152">Actualice el `MediaPlatformSettings` siguiente:</span><span class="sxs-lookup"><span data-stu-id="eb0fd-152">Update your `MediaPlatformSettings` as following:</span></span>

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
> <span data-ttu-id="eb0fd-153">La huella digital del certificado proporcionada en el `MediaPlatformSettings` debe coincidir con el FQDN de servicio.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-153">The certificate thumbprint provided in the `MediaPlatformSettings` must match the Service FQDN.</span></span> <span data-ttu-id="eb0fd-154">Es por eso que se requieren las entradas DNS.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-154">That is why the DNS entries are required.</span></span>

## <a name="caveats"></a><span data-ttu-id="eb0fd-155">Advertencias</span><span class="sxs-lookup"><span data-stu-id="eb0fd-155">Caveats</span></span>

- <span data-ttu-id="eb0fd-156">Las cuentas gratuitas de Ngrok **no proporcionan** cifrado de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="eb0fd-157">Los datos HTTPS terminan en la dirección URL de ngrok y los flujos de datos sin cifrar de ngrok a `localhost` .</span><span class="sxs-lookup"><span data-stu-id="eb0fd-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="eb0fd-158">Si necesita cifrado de extremo a extremo, considere la posibilidad de una cuenta de ngrok de pago.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="eb0fd-159">Consulte [Túneles TLS para](https://ngrok.com/docs#tls) ver los pasos para configurar túneles seguros de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="eb0fd-160">Dado que la dirección URL de devolución de llamada del bot es dinámica, los escenarios de llamadas entrantes requieren que actualices con frecuencia los puntos de conexión de ngrok.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="eb0fd-161">Una forma de solucionar esto es usar una cuenta de ngrok de pago que proporciona subdominios fijos a los que puede apuntar el bot y la plataforma.</span><span class="sxs-lookup"><span data-stu-id="eb0fd-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="eb0fd-162">Los túneles Ngrok también se pueden usar con [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span><span class="sxs-lookup"><span data-stu-id="eb0fd-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="eb0fd-163">Para ver un ejemplo de cómo hacerlo, consulta la aplicación [de ejemplo HueBot](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span><span class="sxs-lookup"><span data-stu-id="eb0fd-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
