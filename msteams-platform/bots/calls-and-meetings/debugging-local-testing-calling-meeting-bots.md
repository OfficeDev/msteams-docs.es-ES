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
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a>Cómo desarrollar bots de llamadas y reuniones en línea en el equipo local

En [Ejecutar y depurar la aplicación,](../../concepts/build-and-test/debug.md) explicamos cómo usar [ngrok](https://ngrok.com) para crear un túnel entre el equipo local e Internet. En este tema, obtén información sobre cómo también puedes usar ngrok y el equipo local para desarrollar bots que admitan llamadas y reuniones en línea.

Los bots de mensajería usan HTTP, pero los bots de llamadas y reuniones en línea usan el TCP de nivel inferior. Ngrok admite túneles TCP además de túneles HTTP; aprenderá cómo hacerlo a continuación.

## <a name="configuring-ngrokyml"></a>Configuración de ngrok.yml

Vaya a [ngrok y](https://ngrok.com) regístrese para obtener una cuenta gratuita o inicie sesión en su cuenta existente. Una vez que haya iniciado sesión, vaya al [panel](https://dashboard.ngrok.com) y obtenga el authtoken.

Crea un archivo de configuración ngrok (consulta aquí para obtener más información sobre dónde se puede encontrar este archivo) y `ngrok.yml` agrega esta línea: [](https://ngrok.com/docs#config)

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a>Configuración de señalización

En [los bots de](./calls-meetings-bots-overview.md)llamadas y reuniones en línea, analizamos la señalización de llamadas: cómo los bots detectan y responden a nuevas llamadas y eventos durante una llamada. Los eventos de señalización de llamadas se envían a través de HTTP POST al extremo de llamada del bot.

Al igual que con la API de mensajería del bot, para que la plataforma de medios en tiempo real hable con el bot, el bot debe estar accesible a través de Internet. Ngrok hace que esto sea sencillo: agregue las siguientes líneas a ngrok.yml:

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a>Configuración de medios locales

> [!NOTE]
> Esta sección solo es necesaria para los bots multimedia hospedados en la aplicación y se puede omitir si no hospeda medios usted mismo.

Los medios hospedados en aplicaciones usan certificados y túneles TCP. Se requieren los siguientes pasos:

- Los extremos TCP públicos de Ngrok tienen direcciones URL fijas. Son, `0.tcp.ngrok.io` `1.tcp.ngrok.io` y así sucesivamente. Debe tener una entrada CNAME de DNS para el servicio que apunta a estas direcciones URL. En este ejemplo, supongamos que hace referencia a `0.bot.contoso.com` , hace referencia a , y así `0.tcp.ngrok.io` `1.bot.contoso.com` `1.tcp.ngrok.io` sucesivamente.
- Se requiere un certificado SSL para las direcciones URL. Para facilitarlo, use un certificado SSL emitido a un dominio de comodín. En este caso, sería `*.bot.contoso.com` . El SDK de medios valida este certificado SSL, por lo que debe coincidir con la dirección URL pública del bot. Ten en cuenta la huella digital e instálrala en los certificados de la máquina.
- Ahora, configure un túnel TCP para reenviar el tráfico a localhost. Escriba las siguientes líneas en ngrok.yml:

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>Iniciar ngrok

Ahora que la configuración de ngrok está lista, indándala:

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

Esto inicia ngrok y define las direcciones URL públicas que proporcionan los túneles al host local. El resultado es similar al siguiente:

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

Este es el puerto de señalización, es el puerto hospedado por la aplicación y es el puerto multimedia remoto `12345` `8445` expuesto por `12332` ngrok. Tenga en cuenta que tenemos un reenvío de `1.bot.contoso.com` a `1.tcp.ngrok.io` . Se usará como la dirección URL multimedia del bot. Por supuesto, estos números de puerto son solo ejemplos y puede usar cualquier puerto disponible.

### <a name="update-code"></a>Actualización del código

Una vez que ngrok esté en funcionamiento, actualice el código para usar la configuración que acaba de configurar.

#### <a name="update-signaling"></a>Actualizar señalización

- En la llamada de BotBuilder, cambie la dirección URL de señalización `NotificationUrl` proporcionada por ngrok.

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Reemplace la señal por la que proporciona ngrok y la ruta de acceso `NotificationEndpoint` del controlador que recibe la notificación.

> **IMPORTANTE:** La dirección URL debe `SetNotificationUrl` ser HTTPS.

> **IMPORTANTE:** La instancia local debe estar escuchando el tráfico HTTP en el puerto de señalización. Las solicitudes realizadas por la plataforma de llamadas y reuniones en línea llegarán al bot como tráfico HTTP localhost a menos que se configure el cifrado de un extremo a otro.

#### <a name="update-media"></a>Actualizar contenido multimedia

Actualice el `MediaPlatformSettings` archivo a lo siguiente.

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
> La huella digital del certificado proporcionada anteriormente debe coincidir con el FQDN del servicio. Por eso se requieren las entradas DNS.

## <a name="next-steps"></a>Pasos siguientes

El bot ahora puede ejecutarse localmente y todos los flujos funcionan desde el host local.

## <a name="caveats"></a>Advertencias

- Las cuentas gratuitas de Ngrok **no proporcionan** cifrado de un extremo a otro. Los datos HTTPS terminan en la dirección URL de ngrok y los flujos de datos no cifrados de ngrok a `localhost` . Si necesita cifrado de un extremo a otro, considere la posibilidad de usar una cuenta de ngrok de pago. Consulte [los túneles TLS](https://ngrok.com/docs#tls) para ver los pasos para configurar túneles seguros de un extremo a otro.
- Dado que la dirección URL de devolución de llamada del bot es dinámica, los escenarios de llamadas entrantes requieren que actualice con frecuencia los puntos de conexión de ngrok. Una forma de corregir esto es usar una cuenta de ngrok de pago que proporciona subdominios fijos a los que puede apuntar el bot y la plataforma.
- Los túneles de Ngrok también se pueden usar con [Azure Service Fabric.](/azure/service-fabric/service-fabric-overview) Para obtener un ejemplo de cómo hacerlo, consulta la aplicación [de ejemplo HueBot](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).
