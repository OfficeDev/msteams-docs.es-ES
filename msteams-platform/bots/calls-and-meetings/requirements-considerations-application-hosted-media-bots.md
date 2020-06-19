---
title: Requisitos y consideraciones para los bots de medios hospedados en la aplicación
description: Comprenda los requisitos y las consideraciones importantes relacionados con la creación de bots de medios hospedados en aplicaciones para Microsoft Teams.
keywords: VM de Windows Server Azure media hospedada en la aplicación
ms.date: 11/16/2018
ms.openlocfilehash: f5b721edacb11e867d05c8213b74036cb51f419c
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801450"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>Requisitos y consideraciones para los bots de medios hospedados en la aplicación

No todas las instrucciones para desarrollar bots de mensajería y de respuesta interactiva de voz (IVR) se aplican por igual para crear bots de medios hospedados en la aplicación. En este artículo se describen algunos de los requisitos y consideraciones importantes para desarrollar y ejecutar un bot de medios hospedado por la aplicación.

> [!NOTE]
> Como la plataforma de medios en tiempo real de Microsoft para bots está en vista previa para desarrolladores, las instrucciones de este artículo están sujetas a cambios.

## <a name="application-hosted-media-bot-development-requires-cnet-and-windows-server"></a>El desarrollo de robots de medios hospedados en aplicaciones requiere C#/.NET y Windows Server

- Un bot? s de medios hospedado en aplicaciones requiere la `Microsoft.Graph.Communications.Calls.Media` biblioteca .net ([disponible aquí](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) para obtener acceso a los flujos de medios de audio y vídeo, y el bot debe implementarse en un equipo con Windows Server o en un sistema operativo invitado de Windows Server en Azure). Por lo tanto, el bot debe desarrollarse en C# y en .NET Framework estándar y se puede implementar en Microsoft Azure. No puede usar C++ ni API de Node.js para obtener acceso a medios en tiempo real y .NET Core no se admite para un bot de medios hospedado por la aplicación.

- Un bot de medios hospedados por la aplicación puede alojarse en uno de los siguientes entornos de servicio de Azure:
  - Servicio en la nube.
  - Fabric de servicio con conjuntos de escalas de máquinas virtuales (VMSS).
  - Máquina virtual (VM) de infraestructura como servicio (IaaS).  
  
- Un bot? n de medios hospedado en aplicaciones no se puede implementar como una aplicación Web de Azure.

- Un bot de medios hospedado en la aplicación debe ejecutarse en una versión reciente de la `Microsoft.Graph.Communications.Calls.Media` biblioteca de .net. El bot debe usar la versión más reciente disponible del [paquete NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)o una versión que no tenga más de tres meses de antigüedad. Las versiones anteriores de la biblioteca estarán obsoletas y es posible que no funcionen después de unos meses. Mantener la `Microsoft.Graph.Communications.Calls.Media` biblioteca actualizada, garantizará la mejor interoperabilidad entre el bot y Microsoft Teams.

## <a name="real-time-media-calls-stay-on-the-machine-where-they-were-created"></a>Las llamadas de medios en tiempo real permanecen en el equipo en el que se crearon

- Una llamada a medios en tiempo real está anclada a la instancia de la máquina virtual (VM) que aceptó o inició la llamada. Los medios de una llamada o reunión de Microsoft Teams fluirá a esa instancia de VM y los medios que el bot devuelve a Microsoft Teams también deben originarse desde esa máquina virtual.
- Si hay llamadas de medios en tiempo real en curso cuando se detiene la máquina virtual, esas llamadas se finalizarán de forma abrupta. Si el bot tiene conocimientos previos sobre el cierre de la máquina virtual pendiente, puede intentar "de forma correcta" finalizar las llamadas.

## <a name="application-hosted-media-bots-must-be-directly-accessible-on-the-internet"></a>Los bots de medios hospedados en aplicaciones deben ser accesibles directamente en Internet

- Cada instancia de VM que hospeda un bot de medios hospedado en la aplicación en Azure debe ser accesible directamente desde Internet mediante una dirección IP pública de nivel de instancia (ILPIP).
  - Para obtener y configurar un ILPIP para un servicio de nube de Azure, consulte [información general sobre la IP pública en el nivel de instancia (Classic)](/azure/virtual-network/virtual-networks-instance-level-public-ip).
  - Para configurar un ILPIP para un conjunto de escalaciones de VM, consulte [Public IPv4 per Virtual Machine](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine).
- El servicio que hospeda un Boto multimedia hospedado en la aplicación también debe configurar cada instancia de VM con un puerto de conexión pública que se asigna a la instancia específica.
  - Para un servicio de nube de Azure, esto requiere un punto de conexión de entrada de instancia; consulte [enable Communication for role instances in Azure](/azure/cloud-services/cloud-services-enable-communication-role-instances).
  - Para un conjunto de escalas de máquina virtual, debe configurarse una regla NAT en el equilibrador de carga; vea [redes virtuales y máquinas virtuales en Azure](/azure/virtual-machines/windows/network-overview).
- Los bots de medios hospedados en aplicaciones no son compatibles con el emulador de bot Framework.

## <a name="scalability-and-performance-considerations"></a>Consideraciones de rendimiento y escalabilidad

- Los bots de medios hospedados en aplicaciones requieren más capacidad de cálculo y de red (ancho de banda) que los bots de mensajería y pueden incurrir en costos operativos mucho más altos. Un desarrollador de robots de medios en tiempo real debe medir cuidadosamente la escalabilidad del bot y asegurarse de que el bot no acepta más llamadas simultáneas de las que puede administrar. Un bot habilitado para vídeo puede soportar solo una o dos sesiones de medios simultáneos por núcleo de CPU (si usa los formatos de vídeo "RAW" RGB24 o NV12).
- Actualmente, la plataforma de medios en tiempo real no aprovecha las unidades de procesamiento de gráficos (GPU) disponibles en la máquina virtual para descargar la codificación y descodificación de vídeo H. 264. En su lugar, la codificación y descodificación de vídeo se realiza en el software de la CPU. Si hay disponible una GPU, el bot puede aprovecharla para su propia representación gráfica (por ejemplo, si el bot usa un motor de gráficos 3D).
- La instancia de VM que hospeda el bot de medios en tiempo real debe tener al menos 2 núcleos de CPU. Para Azure, se recomienda una máquina virtual de Dv2-series. Para otros tipos de VM de Azure, un sistema con 4 CPU virtuales (vCPU) es el tamaño mínimo requerido. Encontrará información detallada sobre los tipos de máquinas virtuales de Azure en la [documentación de Azure](/azure/virtual-machines/windows/sizes-general).

## <a name="samples-and-additional-resources"></a>Ejemplos y recursos adicionales

- [Aplicaciones de ejemplo](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [Documentación del SDK de llamadas de Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
