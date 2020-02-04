---
title: Cómo desarrollar los bots de llamada y reunión en línea en su equipo local
description: Obtenga información acerca de cómo puede usar ngrok para desarrollar llamadas y bots de reuniones en línea en su equipo local.
keywords: túnel de ngrok de desarrollo local
ms.date: 11/18/2018
ms.openlocfilehash: b6cd2ba5a3866da8085b3da42377ab9e21f12f5f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676128"
---
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="5fbe3-104">Cómo desarrollar los bots de llamada y reunión en línea en su equipo local</span><span class="sxs-lookup"><span data-stu-id="5fbe3-104">How to develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="5fbe3-105">En [Ejecutar y depurar la aplicación](../../concepts/build-and-test/debug.md) , explicamos cómo usar [ngrok](https://ngrok.com) para crear un túnel entre el equipo local e Internet.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="5fbe3-106">En este tema, aprenderá cómo puede usar ngrok y su PC local para desarrollar bots que admitan llamadas y reuniones en línea.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="5fbe3-107">Los bots de mensajería usan HTTP, pero las llamadas y los bots de reuniones en línea usan el TCP de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="5fbe3-108">Ngrok admite túneles TCP además de túneles HTTP; aprenderá cómo hacerlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-108">Ngrok supports TCP tunnels in addition to HTTP tunnels; you'll learn how, below.</span></span>

## <a name="configuring-ngrokyml"></a><span data-ttu-id="5fbe3-109">Configuración de ngrok. yml</span><span class="sxs-lookup"><span data-stu-id="5fbe3-109">Configuring ngrok.yml</span></span>

<span data-ttu-id="5fbe3-110">Vaya a [ngrok](https://ngrok.com) y regístrese para obtener una cuenta gratuita o inicie sesión en su cuenta existente.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="5fbe3-111">Una vez que haya iniciado sesión, vaya al [Panel](https://dashboard.ngrok.com) y obtenga sus authtoken.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-111">Once you've logged in, go to the [dashboard](https://dashboard.ngrok.com) and get your authtoken.</span></span>

<span data-ttu-id="5fbe3-112">Cree un archivo `ngrok.yml` de configuración de ngrok (vea [aquí](https://ngrok.com/docs#config) para obtener más información acerca de dónde se puede encontrar este archivo) y agregue esta línea:</span><span class="sxs-lookup"><span data-stu-id="5fbe3-112">Create an ngrok configuration file `ngrok.yml` (see [here](https://ngrok.com/docs#config) for more information on where this file can be located) and add this line:</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a><span data-ttu-id="5fbe3-113">Configuración de la señalización</span><span class="sxs-lookup"><span data-stu-id="5fbe3-113">Setting up signaling</span></span>

<span data-ttu-id="5fbe3-114">En las [llamadas y los bots de reuniones en línea](./calls-meetings-bots-overview.md), analizamos la señalización de llamadas: cómo los bots detectan y responden a nuevas llamadas y eventos durante una llamada.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-114">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling — how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="5fbe3-115">Los eventos de señalización de llamadas se envían a través de HTTP POST al extremo de llamada del bot.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-115">Call signaling events are sent via HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="5fbe3-116">Al igual que con la API de mensajería del bot, para que la plataforma de medios en tiempo real hable a su bot, el bot debe ser accesible a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-116">As with the bot's messaging API, in order for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="5fbe3-117">Ngrok hace esto sencillo: Agregue las siguientes líneas a su Ngrok. yml:</span><span class="sxs-lookup"><span data-stu-id="5fbe3-117">Ngrok makes this simple — add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a><span data-ttu-id="5fbe3-118">Configuración de medios locales</span><span class="sxs-lookup"><span data-stu-id="5fbe3-118">Setting up local media</span></span>

> [!NOTE]
> <span data-ttu-id="5fbe3-119">Esta sección solo es necesaria para los bots de medios hospedados en aplicaciones y se puede omitir si no hospeda medios por su cuenta.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-119">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="5fbe3-120">Los medios hospedados en la aplicación usan certificados y túneles TCP.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-120">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="5fbe3-121">Se requieren los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5fbe3-121">The following steps are required:</span></span>

- <span data-ttu-id="5fbe3-122">Los extremos TCP públicos de Ngrok tienen direcciones URL fijas.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-122">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="5fbe3-123">Son `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-123">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="5fbe3-124">Debe tener una entrada CNAME de DNS para el servicio que apunte a estas direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-124">You should have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="5fbe3-125">En este ejemplo, supongamos `0.bot.contoso.com` que hace `0.tcp.ngrok.io`referencia `1.bot.contoso.com` a `1.tcp.ngrok.io`, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-125">In this example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
- <span data-ttu-id="5fbe3-126">Se necesita un certificado SSL para las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-126">A SSL certificate is required for your URLs.</span></span> <span data-ttu-id="5fbe3-127">Para que sea más fácil, use un certificado SSL emitido para un dominio comodín.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-127">To make it easy, use a SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="5fbe3-128">En este caso, sería `*.bot.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-128">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="5fbe3-129">El SDK de media valida este certificado SSL, por lo que debe coincidir con la dirección URL pública de su bot.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-129">This SSL certificate is validated by the media SDK, so it should match your bot's public URL.</span></span> <span data-ttu-id="5fbe3-130">Anote la huella digital e instálela en los certificados del equipo.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-130">Note the thumbprint and install it in your machine certificates.</span></span>
- <span data-ttu-id="5fbe3-131">Ahora, configure un túnel TCP para reenviar el tráfico a localhost.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-131">Now, setup a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="5fbe3-132">Escriba las líneas siguientes en el ngrok. yml:</span><span class="sxs-lookup"><span data-stu-id="5fbe3-132">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="5fbe3-133">Iniciar ngrok</span><span class="sxs-lookup"><span data-stu-id="5fbe3-133">Start ngrok</span></span>

<span data-ttu-id="5fbe3-134">Ahora que la configuración de ngrok está lista, iníciela:</span><span class="sxs-lookup"><span data-stu-id="5fbe3-134">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="5fbe3-135">Esto inicia ngrok y define las direcciones URL públicas que proporcionan los túneles a su host local.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-135">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="5fbe3-136">El resultado tiene un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="5fbe3-136">The output looks like the following:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="5fbe3-137">Aquí, `12345` es el puerto de señalización `8445` , es el puerto hospedado por la `12332` aplicación y es el puerto de medios remotos expuesto por ngrok.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-137">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="5fbe3-138">Tenga en cuenta que tenemos que reenviar `1.bot.contoso.com` desde `1.tcp.ngrok.io`a.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-138">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="5fbe3-139">Se utilizará como la dirección URL del medio para el bot.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-139">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="5fbe3-140">Por supuesto, estos números de puerto son solo ejemplos y puede usar cualquier puerto disponible.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-140">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="5fbe3-141">Actualización del código</span><span class="sxs-lookup"><span data-stu-id="5fbe3-141">Update code</span></span>

<span data-ttu-id="5fbe3-142">Una vez que ngrok está en funcionamiento, actualice el código para usar la configuración que acaba de configurar.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-142">Once ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="5fbe3-143">Señalización de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="5fbe3-143">Update signaling</span></span>

- <span data-ttu-id="5fbe3-144">En la llamada BotBuilder, cambie el `NotificationUrl` a la dirección URL de señalización proporcionada por ngrok.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-144">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="5fbe3-145">Reemplace la señal con la proporcionada por ngrok y la `NotificationEndpoint` por la ruta de acceso del controlador que recibe la notificación.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-145">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> <span data-ttu-id="5fbe3-146">**Importante**: la dirección URL `SetNotificationUrl` de debe ser https.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-146">**IMPORTANT**: The URL in `SetNotificationUrl` must be HTTPS.</span></span>

> <span data-ttu-id="5fbe3-147">**Importante**: la instancia local debe estar escuchando el tráfico http en el puerto de señalización.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-147">**IMPORTANT**: Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="5fbe3-148">Las solicitudes realizadas por las llamadas y la plataforma de reuniones en línea alcanzarán el bot como tráfico HTTP localhost a menos que se configure el cifrado de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-148">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="5fbe3-149">Actualizar medios</span><span class="sxs-lookup"><span data-stu-id="5fbe3-149">Update media</span></span>

<span data-ttu-id="5fbe3-150">Actualice el `MediaPlatformSettings` a los siguientes.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-150">Update your `MediaPlatformSettings` to the following.</span></span>

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
> <span data-ttu-id="5fbe3-151">La huella digital de certificado proporcionada anteriormente debe coincidir con el FQDN de servicio.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-151">The certificate thumbprint provided above should match the Service FQDN.</span></span> <span data-ttu-id="5fbe3-152">Esa es la razón por la que se necesitan las entradas DNS.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-152">That is why the DNS entries are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fbe3-153">Siguientes pasos</span><span class="sxs-lookup"><span data-stu-id="5fbe3-153">Next steps</span></span>

<span data-ttu-id="5fbe3-154">Ahora, el bot puede ejecutarse de forma local y todos los flujos de trabajo de su host local.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-154">Your bot can now run locally and all the flows work from your localhost.</span></span>

## <a name="caveats"></a><span data-ttu-id="5fbe3-155">ADVERTENCIAS</span><span class="sxs-lookup"><span data-stu-id="5fbe3-155">Caveats</span></span>

- <span data-ttu-id="5fbe3-156">Las cuentas gratuitas de Ngrok **no** proporcionan cifrado de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="5fbe3-157">Los datos HTTPS finalizan en la dirección URL de ngrok y los flujos de datos no `localhost`cifrados de ngrok a.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="5fbe3-158">Si requiere un cifrado de un extremo a otro, considere una cuenta de ngrok de pago.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="5fbe3-159">Consulte [túneles TLS](https://ngrok.com/docs#tls) para conocer los pasos sobre la configuración de túneles de extremo a extremo seguros.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="5fbe3-160">Debido a que la dirección URL de devolución de llamada de bot es dinámica, los escenarios de llamadas entrantes requieren que actualice con frecuencia los puntos de conexión de ngrok.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="5fbe3-161">Una forma de solucionar esto es usar una cuenta de ngrok de pago que proporcione subdominios fijos a los que puede apuntar el bot y la plataforma.</span><span class="sxs-lookup"><span data-stu-id="5fbe3-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="5fbe3-162">Los túneles de Ngrok también pueden usarse con [Azure Service fabric](/azure/service-fabric/service-fabric-overview).</span><span class="sxs-lookup"><span data-stu-id="5fbe3-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="5fbe3-163">Para obtener un ejemplo de cómo hacerlo, vea la [aplicación de ejemplo HueBot](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span><span class="sxs-lookup"><span data-stu-id="5fbe3-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
