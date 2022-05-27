---
title: Depurar el bot de llamadas y reuniones de forma local
description: Obtenga información sobre cómo también puede usar ngrok para desarrollar llamadas y bots de reuniones en línea en su equipo local.
ms.topic: how-to
ms.localizationpriority: medium
keywords: túnel ngrok de desarrollo local
ms.date: 11/18/2018
ms.openlocfilehash: 7f85243e0a5d94711cd303ff542decd3bbc7847a
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757118"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>Desarrolle bots de llamadas y reuniones en línea en su equipo local

En [Ejecutar y depurar la aplicación](../../concepts/build-and-test/debug.md), explicamos cómo usar [ngrok](https://ngrok.com) para crear un túnel entre el equipo local e Internet. En este tema, aprenderá cómo también puede usar ngrok y su equipo local para desarrollar bots que admitan llamadas y reuniones en línea.

Los bots de mensajería usan HTTP, pero las llamadas y los bots de reuniones en línea usan el TCP de nivel inferior. Ngrok admite túneles TCP además de túneles HTTP.

## <a name="configure-ngrokyml"></a>Configurar ngrok.yml

Vaya a [ngrok](https://ngrok.com) y regístrese para obtener una cuenta gratuita o inicie sesión en su cuenta existente. Después de iniciar sesión, vaya a la [dashboard](https://dashboard.ngrok.com) y obtenga el token de autenticación.

Cree un archivo `ngrok.yml` de configuración ngrok y agregue la línea siguiente. Para obtener más información sobre dónde se puede encontrar el archivo, consulte [ngrok](https://ngrok.com/docs#config):

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>Configurar señalización

En [Calls y bots de reuniones en línea](./calls-meetings-bots-overview.md), analizamos la señalización de llamadas sobre cómo los bots detectan y responden a nuevas llamadas y eventos durante una llamada. Los eventos de señalización de llamadas se envían a través de HTTP POST al punto de conexión de llamada del bot.

Al igual que con la API de mensajería del bot, para que la plataforma multimedia en tiempo real hable con el bot, el bot debe ser accesible a través de Internet. Ngrok lo simplifica. Agregue las líneas siguientes a ngrok.yml:

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a>Configurar medios locales

> [!NOTE]
> Esta sección solo es necesaria para los bots multimedia hospedados en la aplicación y se puede omitir si no hospeda medios usted mismo.

Los medios hospedados en la aplicación usan certificados y túneles TCP. Se requieren los pasos siguientes:

1. Los puntos de conexión TCP públicos de Ngrok tienen direcciones URL fijas. `0.tcp.ngrok.io`Son , `1.tcp.ngrok.io`y así sucesivamente. Debe tener una entrada CNAME de DNS para el servicio que apunte a estas direcciones URL. Por ejemplo, supongamos que `0.bot.contoso.com` hace referencia a `0.tcp.ngrok.io`, `1.bot.contoso.com` hace referencia a `1.tcp.ngrok.io`, etc.
2. Se requiere un certificado SSL para las direcciones URL. Para facilitarlo, use un certificado SSL emitido para un dominio comodín. En este caso, sería `*.bot.contoso.com`. El SDK multimedia valida este certificado SSL, por lo que debe coincidir con la dirección URL pública del bot. Anote la huella digital e instálela en los certificados del equipo.
3. Ahora, configure un túnel TCP para reenviar el tráfico a localhost. Escriba las líneas siguientes en el archivo ngrok.yml:

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>Iniciar ngrok

Ahora que la configuración de ngrok está lista, iníciela:

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

Esto inicia ngrok y define las direcciones URL públicas, que proporcionan los túneles a localhost. Este es un ejemplo de la salida:

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

Aquí, `12345` es el puerto de señalización, `8445` es el puerto hospedado por la aplicación y `12332` es el puerto multimedia remoto expuesto por ngrok. Tenga en cuenta que tenemos un reenvío de `1.bot.contoso.com` a `1.tcp.ngrok.io`. Se usará como dirección URL multimedia del bot. Por supuesto, estos números de puerto son solo ejemplos y puede usar cualquier puerto disponible.

### <a name="update-code"></a>Actualización del código

Una vez que ngrok esté en funcionamiento, actualice el código para usar la configuración que acaba de configurar.

#### <a name="update-signaling"></a>Actualizar señalización

En la llamada a BotBuilder, cambie el `NotificationUrl` a la dirección URL de señalización proporcionada por ngrok.

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Reemplace la señal por la proporcionada por ngrok y el `NotificationEndpoint` por la ruta de acceso del controlador que recibe la notificación.

> [!IMPORTANT]
>
> * La dirección URL de `SetNotificationUrl` debe ser HTTPS.
>
> La instancia local debe escuchar el tráfico HTTP en el puerto de señalización. Las solicitudes realizadas por la plataforma de llamadas y reuniones en línea llegarán al bot como tráfico HTTP de localhost a menos que se configure el cifrado de un extremo a otro.

#### <a name="update-media"></a>Actualizar medios

Actualice el `MediaPlatformSettings` como se indica a continuación:

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
> La huella digital del certificado proporcionada en el `MediaPlatformSettings` debe coincidir con el FQDN del servicio. Este es el motivo por el que se requieren las entradas DNS.

## <a name="caveats"></a>Advertencias

* Las cuentas gratuitas de Ngrok **no** proporcionan cifrado de un extremo a otro. Los datos HTTPS terminan en la dirección URL de ngrok y los flujos de datos no se cifran de ngrok a `localhost`. Si necesita cifrado de un extremo a otro, considere la posibilidad de usar una cuenta de ngrok de pago. Consulte [túnelesTLS](https://ngrok.com/docs#tls) para obtener información sobre cómo configurar túneles seguros de un extremo a otro.
* Dado que la dirección URL de devolución de llamada del bot es dinámica, los escenarios de llamada entrante requieren que actualice con frecuencia los puntos de conexión de ngrok. Una manera de corregir esto es usar una cuenta de ngrok de pago, que proporciona subdominios fijos a los que puede apuntar el bot y la plataforma.
* Los túneles Ngrok también se pueden usar con [Azure Service Fabric](/azure/service-fabric/service-fabric-overview). Para obtener un ejemplo de cómo hacerlo, consulte la aplicación de ejemplo [HueBot](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples/HueBot/HueBot).
