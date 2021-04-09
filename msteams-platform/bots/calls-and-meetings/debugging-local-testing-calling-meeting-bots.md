---
title: Depurar el bot de llamadas y reuniones de forma local
description: Obtenga información sobre cómo también puede usar ngrok para desarrollar llamadas y bots de reunión en línea en su equipo local.
ms.topic: how-to
keywords: túnel ngrok de desarrollo local
ms.date: 11/18/2018
ms.openlocfilehash: d61c380fda941618a769ad3fffa053b2a4800de9
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634730"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>Desarrollar bots de llamadas y reuniones en línea en el equipo local

En [Ejecutar y depurar la aplicación](../../concepts/build-and-test/debug.md) te explicamos cómo usar [ngrok](https://ngrok.com) para crear un túnel entre tu equipo local e Internet. En este tema, obtenga información sobre cómo también puede usar ngrok y su equipo local para desarrollar bots compatibles con llamadas y reuniones en línea.

Los bots de mensajería usan HTTP, pero las llamadas y los bots de reunión en línea usan el TCP de nivel inferior. Ngrok admite túneles TCP además de túneles HTTP. 

## <a name="configure-ngrokyml"></a>Configurar ngrok.yml

Vaya a [ngrok](https://ngrok.com) y regístrese para obtener una cuenta gratuita o inicie sesión en su cuenta existente. Después de haber iniciado sesión, vaya al [panel](https://dashboard.ngrok.com) y obtenga el authtoken.

Cree un archivo de configuración de ngrok `ngrok.yml` y agregue la siguiente línea. Para obtener más información sobre dónde se puede encontrar el archivo, [vea ngrok](https://ngrok.com/docs#config):

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>Configurar la señalización

En [bots de llamadas](./calls-meetings-bots-overview.md)y reuniones en línea, hablamos sobre la señalización de llamadas sobre cómo los bots detectan y responden a nuevas llamadas y eventos durante una llamada. Los eventos de señalización de llamadas se envían a través de HTTP POST al extremo de llamada del bot.

Al igual que con la API de mensajería del bot, para que la Plataforma multimedia en tiempo real hable con el bot, el bot debe ser accesible a través de Internet. Ngrok hace que esto sea sencillo. Agregue las siguientes líneas a su ngrok.yml:

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a>Configurar medios locales

> [!NOTE]
> Esta sección solo es necesaria para los bots multimedia hospedados en aplicaciones y se puede omitir si no hospeda los medios usted mismo.

Los medios hospedados en aplicaciones usan certificados y túneles TCP. Se requieren los siguientes pasos:

1. Los puntos de conexión TCP públicos de Ngrok tienen direcciones URL fijas. Son `0.tcp.ngrok.io` , `1.tcp.ngrok.io` y así sucesivamente. Debe tener una entrada CNAME DNS para el servicio que apunta a estas direcciones URL. Por ejemplo, supongamos que hace `0.bot.contoso.com` referencia a , hace referencia a , y así `0.tcp.ngrok.io` `1.bot.contoso.com` `1.tcp.ngrok.io` sucesivamente.
2. Se requiere un certificado SSL para las direcciones URL. Para facilitar la tarea, use un certificado SSL emitido a un dominio de comodín. En este caso, sería `*.bot.contoso.com` . El SDK multimedia valida este certificado SSL, por lo que debe coincidir con la dirección URL pública del bot. Tenga en cuenta la huella digital e instálesla en los certificados de la máquina.
3. Ahora, configure un túnel TCP para reenviar el tráfico a localhost. Escriba las siguientes líneas en su ngrok.yml:

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>Iniciar ngrok

Ahora que la configuración de ngrok está lista, inicie:

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

Esto inicia ngrok y define las direcciones URL públicas que proporcionan los túneles al host local. A continuación se muestra un ejemplo de la salida:

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

Aquí, es el puerto de señalización, es el puerto hospedado por la aplicación y es el puerto multimedia remoto `12345` `8445` expuesto por `12332` ngrok. Tenga en cuenta que tenemos un reenvío de `1.bot.contoso.com` a `1.tcp.ngrok.io` . Se usará como la dirección URL multimedia del bot. Por supuesto, estos números de puerto son solo ejemplos y puede usar cualquier puerto disponible.

### <a name="update-code"></a>Actualización del código

Después de que ngrok esté en funcionamiento, actualice el código para usar la configuración que acaba de configurar.

#### <a name="update-signaling"></a>Actualizar señalización

En la llamada a BotBuilder, cambie la dirección URL de señalización `NotificationUrl` proporcionada por ngrok.

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Reemplace la señal por la proporcionada por ngrok y la ruta de acceso `NotificationEndpoint` del controlador que recibe la notificación.

> [!IMPORTANT]
> * La dirección URL en `SetNotificationUrl` debe ser HTTPS.
> 
> La instancia local debe estar escuchando el tráfico HTTP en el puerto de señalización. Las solicitudes realizadas por la plataforma de llamadas y reuniones en línea llegarán al bot como tráfico HTTP localhost a menos que se configure el cifrado de extremo a extremo.

#### <a name="update-media"></a>Actualizar medios

Actualice el `MediaPlatformSettings` siguiente:

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
> La huella digital del certificado proporcionada en el `MediaPlatformSettings` debe coincidir con el FQDN de servicio. Es por eso que se requieren las entradas DNS.

## <a name="caveats"></a>Advertencias

- Las cuentas gratuitas de Ngrok **no proporcionan** cifrado de extremo a extremo. Los datos HTTPS terminan en la dirección URL de ngrok y los flujos de datos sin cifrar de ngrok a `localhost` . Si necesita cifrado de extremo a extremo, considere la posibilidad de una cuenta de ngrok de pago. Consulte [Túneles TLS para](https://ngrok.com/docs#tls) ver los pasos para configurar túneles seguros de extremo a extremo.
- Dado que la dirección URL de devolución de llamada del bot es dinámica, los escenarios de llamadas entrantes requieren que actualices con frecuencia los puntos de conexión de ngrok. Una forma de solucionar esto es usar una cuenta de ngrok de pago que proporciona subdominios fijos a los que puede apuntar el bot y la plataforma.
- Los túneles Ngrok también se pueden usar con [Azure Service Fabric](/azure/service-fabric/service-fabric-overview). Para ver un ejemplo de cómo hacerlo, consulta la aplicación [de ejemplo HueBot](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).
