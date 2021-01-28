---
title: Requisitos y consideraciones para bots multimedia hospedados en aplicaciones
description: Comprenda los requisitos y consideraciones importantes relacionados con la creación de bots multimedia hospedados en aplicaciones para Microsoft Teams.
ms.topic: conceptual
keywords: máquina virtual de Azure de Windows Server de medios hospedados en la aplicación
ms.date: 11/16/2018
ms.openlocfilehash: bf75b7f689713f16cb3ff9ff4313ab829b5cc2d6
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014491"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>Requisitos y consideraciones para bots multimedia hospedados en aplicaciones

No todas las instrucciones para desarrollar bots de mensajería y respuesta interactiva de voz (IVR) se aplican por igual a la creación de bots multimedia hospedados en aplicaciones. En este artículo se describen algunos de los requisitos y consideraciones importantes para desarrollar y ejecutar un bot multimedia hospedado en aplicaciones.

> [!NOTE]
> Dado que la Plataforma de medios en tiempo real de Microsoft para bots está en versión preliminar para desarrolladores, las instrucciones de este artículo están sujetas a cambios.

## <a name="application-hosted-media-bot-development-requires-cnet-and-windows-server"></a>El desarrollo de bots multimedia hospedados en aplicaciones requiere C#/.NET y Windows Server

- Un bot de medios hospedado en aplicaciones requiere la biblioteca .NET (disponible aquí para tener acceso a las secuencias multimedia de audio y vídeo, y el bot debe implementarse en un equipo con Windows Server (o el sistema operativo invitado de Windows Server en `Microsoft.Graph.Communications.Calls.Media` Azure).[](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) Por lo tanto, el bot debe desarrollarse en C# y .NET Framework estándar e implementarse en Microsoft Azure. No puedes usar C++ ni Node.js API para acceder a medios en tiempo real y .NET Core no es compatible con un bot de medios hospedado en la aplicación.

- Un bot de medios hospedado por la aplicación se puede hospedar en uno de los siguientes entornos de servicio de Azure:
  - Servicio en la nube.
  - Service Fabric con conjuntos de escalado de máquinas virtuales (VMSS).
  - Máquina virtual (VM) de infraestructura como servicio (IaaS).  
  
- Un bot multimedia hospedado en la aplicación no se puede implementar como una aplicación web de Azure.

- Un bot de medios hospedado en la aplicación debe ejecutarse en una versión reciente de la `Microsoft.Graph.Communications.Calls.Media` biblioteca .NET. El bot debe usar la versión más reciente disponible del paquete [NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)o una versión que no tiene más de tres meses de antigüedad. Las versiones anteriores de la biblioteca estarán en desuso y es posible que no funcionen después de unos meses. Mantener la biblioteca actualizada garantizará la mejor interoperabilidad `Microsoft.Graph.Communications.Calls.Media` entre el bot y Microsoft Teams.

## <a name="real-time-media-calls-stay-on-the-machine-where-they-were-created"></a>Las llamadas multimedia en tiempo real permanecen en el equipo donde se crearon

- Una llamada multimedia en tiempo real se ancla a la instancia de máquina virtual (VM) que aceptó o inició la llamada. Los medios de una llamada o reunión de Microsoft Teams fluirán a esa instancia de máquina virtual, y los medios que el bot envía a Microsoft Teams también deben originarse desde esa máquina virtual.
- Si hay llamadas multimedia en tiempo real en curso cuando se detiene la máquina virtual, dichas llamadas finalizarán bruscamente. Si el bot tiene conocimientos previos del apagado pendiente de la máquina virtual, puede intentar finalizar "correctamente" las llamadas.

## <a name="application-hosted-media-bots-must-be-directly-accessible-on-the-internet"></a>Los bots de medios hospedados en aplicaciones deben ser accesibles directamente en Internet

- Cada instancia de máquina virtual que hospeda un bot de medios hospedado por la aplicación en Azure debe ser accesible directamente desde Internet mediante una dirección IP pública de nivel de instancia (ILPIP).
  - Para obtener y configurar un ILPIP para un servicio en la nube de Azure, vea información general sobre ip pública [(clásica) de nivel de instancia.](/azure/virtual-network/virtual-networks-instance-level-public-ip)
  - Para configurar un ILPIP para un conjunto de escalado de vm, consulte [IPv4 público por máquina virtual.](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine)
- El servicio que hospeda un bot multimedia hospedado en la aplicación también debe configurar cada instancia de máquina virtual con un puerto de acceso público que se asigna a la instancia específica.
  - Para un servicio en la nube de Azure, esto requiere un punto de conexión de entrada de instancia; vea [Habilitar la comunicación para instancias de roles en Azure.](/azure/cloud-services/cloud-services-enable-communication-role-instances)
  - Para un conjunto de escalado de vm, debe configurarse una regla NAT en el equilibrador de carga; vea [Redes virtuales y máquinas virtuales en Azure.](/azure/virtual-machines/windows/network-overview)
- Los bots multimedia hospedados en la aplicación no son compatibles con el emulador de Bot Framework.

## <a name="scalability-and-performance-considerations"></a>Consideraciones de rendimiento y escalabilidad

- Los bots de medios hospedados en aplicaciones requieren más capacidad de proceso y red (ancho de banda) que los bots de mensajería y pueden incurrir en costos operativos significativamente mayores. Un desarrollador de bots multimedia en tiempo real debe medir cuidadosamente la escalabilidad del bot y asegurarse de que el bot no acepta más llamadas simultáneas de las que puede administrar. Un bot habilitado para vídeo puede ser capaz de mantener solo una o dos sesiones multimedia simultáneas por núcleo de CPU (si usa los formatos de vídeo RGB24 o NV12 "sin procesar").
- La plataforma multimedia en tiempo real no aprovecha actualmente ninguna unidades de procesamiento gráfico (GPU) disponibles en la máquina virtual para desactivar la codificación/decodificación de vídeo H.264. En su lugar, la codificación y descodificación de vídeo se realizan en el software de la CPU. Si una GPU está disponible, el bot puede aprovecharlo para su propia representación de gráficos (por ejemplo, si el bot usa un motor de gráficos 3D).
- La instancia de máquina virtual que hospeda el bot multimedia en tiempo real debe tener al menos 2 núcleos de CPU. Para Azure, se recomienda una máquina virtual de la serie Dv2. Para otros tipos de VM de Azure, un sistema con 4 CPU virtuales (vCPU) es el tamaño mínimo necesario. La información detallada sobre los tipos de vm de Azure está disponible en la [documentación de Azure.](/azure/virtual-machines/windows/sizes-general)

## <a name="samples-and-additional-resources"></a>Ejemplos y recursos adicionales

- [Aplicaciones de ejemplo](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [Documentación del SDK de llamadas de Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
