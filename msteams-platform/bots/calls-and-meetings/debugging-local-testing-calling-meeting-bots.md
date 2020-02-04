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
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a>Cómo desarrollar los bots de llamada y reunión en línea en su equipo local

En [Ejecutar y depurar la aplicación](../../concepts/build-and-test/debug.md) , explicamos cómo usar [ngrok](https://ngrok.com) para crear un túnel entre el equipo local e Internet. En este tema, aprenderá cómo puede usar ngrok y su PC local para desarrollar bots que admitan llamadas y reuniones en línea.

Los bots de mensajería usan HTTP, pero las llamadas y los bots de reuniones en línea usan el TCP de nivel inferior. Ngrok admite túneles TCP además de túneles HTTP; aprenderá cómo hacerlo más adelante.

## <a name="configuring-ngrokyml"></a>Configuración de ngrok. yml

Vaya a [ngrok](https://ngrok.com) y regístrese para obtener una cuenta gratuita o inicie sesión en su cuenta existente. Una vez que haya iniciado sesión, vaya al [Panel](https://dashboard.ngrok.com) y obtenga sus authtoken.

Cree un archivo `ngrok.yml` de configuración de ngrok (vea [aquí](https://ngrok.com/docs#config) para obtener más información acerca de dónde se puede encontrar este archivo) y agregue esta línea:

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a>Configuración de la señalización

En las [llamadas y los bots de reuniones en línea](./calls-meetings-bots-overview.md), analizamos la señalización de llamadas: cómo los bots detectan y responden a nuevas llamadas y eventos durante una llamada. Los eventos de señalización de llamadas se envían a través de HTTP POST al extremo de llamada del bot.

Al igual que con la API de mensajería del bot, para que la plataforma de medios en tiempo real hable a su bot, el bot debe ser accesible a través de Internet. Ngrok hace esto sencillo: Agregue las siguientes líneas a su Ngrok. yml:

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a>Configuración de medios locales

> [!NOTE]
> Esta sección solo es necesaria para los bots de medios hospedados en aplicaciones y se puede omitir si no hospeda medios por su cuenta.

Los medios hospedados en la aplicación usan certificados y túneles TCP. Se requieren los pasos siguientes:

- Los extremos TCP públicos de Ngrok tienen direcciones URL fijas. Son `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, y así sucesivamente. Debe tener una entrada CNAME de DNS para el servicio que apunte a estas direcciones URL. En este ejemplo, supongamos `0.bot.contoso.com` que hace `0.tcp.ngrok.io`referencia `1.bot.contoso.com` a `1.tcp.ngrok.io`, y así sucesivamente.
- Se necesita un certificado SSL para las direcciones URL. Para que sea más fácil, use un certificado SSL emitido para un dominio comodín. En este caso, sería `*.bot.contoso.com`. El SDK de media valida este certificado SSL, por lo que debe coincidir con la dirección URL pública de su bot. Anote la huella digital e instálela en los certificados del equipo.
- Ahora, configure un túnel TCP para reenviar el tráfico a localhost. Escriba las líneas siguientes en el ngrok. yml:

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>Iniciar ngrok

Ahora que la configuración de ngrok está lista, iníciela:

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

Esto inicia ngrok y define las direcciones URL públicas que proporcionan los túneles a su host local. El resultado tiene un aspecto similar al siguiente:

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

Aquí, `12345` es el puerto de señalización `8445` , es el puerto hospedado por la `12332` aplicación y es el puerto de medios remotos expuesto por ngrok. Tenga en cuenta que tenemos que reenviar `1.bot.contoso.com` desde `1.tcp.ngrok.io`a. Se utilizará como la dirección URL del medio para el bot. Por supuesto, estos números de puerto son solo ejemplos y puede usar cualquier puerto disponible.

### <a name="update-code"></a>Actualización del código

Una vez que ngrok está en funcionamiento, actualice el código para usar la configuración que acaba de configurar.

#### <a name="update-signaling"></a>Señalización de actualizaciones

- En la llamada BotBuilder, cambie el `NotificationUrl` a la dirección URL de señalización proporcionada por ngrok.

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Reemplace la señal con la proporcionada por ngrok y la `NotificationEndpoint` por la ruta de acceso del controlador que recibe la notificación.

> **Importante**: la dirección URL `SetNotificationUrl` de debe ser https.

> **Importante**: la instancia local debe estar escuchando el tráfico http en el puerto de señalización. Las solicitudes realizadas por las llamadas y la plataforma de reuniones en línea alcanzarán el bot como tráfico HTTP localhost a menos que se configure el cifrado de un extremo a otro.

#### <a name="update-media"></a>Actualizar medios

Actualice el `MediaPlatformSettings` a los siguientes.

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
> La huella digital de certificado proporcionada anteriormente debe coincidir con el FQDN de servicio. Esa es la razón por la que se necesitan las entradas DNS.

## <a name="next-steps"></a>Siguientes pasos

Ahora, el bot puede ejecutarse de forma local y todos los flujos de trabajo de su host local.

## <a name="caveats"></a>ADVERTENCIAS

- Las cuentas gratuitas de Ngrok **no** proporcionan cifrado de un extremo a otro. Los datos HTTPS finalizan en la dirección URL de ngrok y los flujos de datos no `localhost`cifrados de ngrok a. Si requiere un cifrado de un extremo a otro, considere una cuenta de ngrok de pago. Consulte [túneles TLS](https://ngrok.com/docs#tls) para conocer los pasos sobre la configuración de túneles de extremo a extremo seguros.
- Debido a que la dirección URL de devolución de llamada de bot es dinámica, los escenarios de llamadas entrantes requieren que actualice con frecuencia los puntos de conexión de ngrok. Una forma de solucionar esto es usar una cuenta de ngrok de pago que proporcione subdominios fijos a los que puede apuntar el bot y la plataforma.
- Los túneles de Ngrok también pueden usarse con [Azure Service fabric](/azure/service-fabric/service-fabric-overview). Para obtener un ejemplo de cómo hacerlo, vea la [aplicación de ejemplo HueBot](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).
