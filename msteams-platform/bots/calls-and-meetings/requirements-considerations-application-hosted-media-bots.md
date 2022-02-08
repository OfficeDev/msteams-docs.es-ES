---
title: Requisitos y consideraciones para bots multimedia hospedados en aplicaciones
description: Comprenda los requisitos y consideraciones importantes, así como las consideraciones de escalabilidad y rendimiento relacionadas con la creación de bots multimedia hospedados en aplicaciones para Microsoft Teams ejemplo de código y ejemplos.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Medios hospedados por la aplicación Windows máquina virtual de Azure del servidor
ms.date: 11/16/2018
ms.openlocfilehash: c3c6f76b5062f003902c9967191be9cd0be336aa
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435715"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>Requisitos y consideraciones para bots multimedia hospedados en aplicaciones

Un bot multimedia hospedado por la aplicación requiere que [la biblioteca`Microsoft.Graph.Communications.Calls.Media` .NET](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) obtenga acceso a las secuencias multimedia de audio y vídeo. El bot debe implementarse en un equipo Windows Server o en un Windows operativo invitado del servidor en Azure.

> [!NOTE]
> * Las instrucciones para desarrollar mensajes y bots de respuesta de voz interactiva (IVR) no se aplican por completo a la creación de bots multimedia hospedados en aplicaciones.
> * Como la Plataforma multimedia en tiempo real de Microsoft para bots está en versión preliminar para desarrolladores, las instrucciones de este documento están sujetas a cambios.

## <a name="c-or-net-and-windows-server-for-development"></a>C# o .NET y Windows Server para desarrollo

Un bot multimedia hospedado por la aplicación requiere lo siguiente:

- El bot debe desarrollarse en C# y la .NET Framework estándar e implementarse en Microsoft Azure. No puede usar las API de C++ o Node.js para obtener acceso a medios en tiempo real y .NET Core no es compatible con un bot de medios hospedado por la aplicación.

- El bot se puede hospedar en uno de los siguientes entornos de servicio de Azure:
    - Servicio en la nube.
    - Service Fabric con conjuntos de escalado de máquinas virtuales (VMSS).
    - Máquina virtual (VM) de infraestructura como servicio (IaaS).  
  
- El bot no se puede implementar como una aplicación web de Azure.

- El bot debe ejecutarse en una versión reciente de la biblioteca `Microsoft.Graph.Communications.Calls.Media` .NET. El bot debe usar la versión disponible más reciente del paquete [NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) o una versión que no tiene más de tres meses de antigüedad. Las versiones anteriores de la biblioteca están en desuso y no funcionan después de unos meses. Mantener la `Microsoft.Graph.Communications.Calls.Media` biblioteca actualizada garantiza la mejor interoperabilidad entre el bot y Microsoft Teams.

En la siguiente sección se proporcionan detalles sobre dónde se encuentran las llamadas multimedia en tiempo real.

## <a name="real-time-media-calls-stay-where-they-are-created"></a>Las llamadas multimedia en tiempo real permanecen donde se crean

Las llamadas multimedia en tiempo real permanecen en el equipo donde se crearon. Una llamada multimedia en tiempo real se ancla a la instancia de máquina virtual (VM) que aceptó o inició la llamada. Los medios de una Microsoft Teams o reunión fluyen a esa instancia de máquina virtual y los medios que el bot envía de vuelta a Microsoft Teams también deben originarse desde esa máquina virtual. Si hay llamadas multimedia en tiempo real en curso cuando se detiene la máquina virtual, dichas llamadas finalizan abruptamente. Si el bot tiene conocimientos previos sobre el apagado de vm pendiente, puede finalizar las llamadas.

En la siguiente sección se proporcionan detalles sobre la accesibilidad de los bots multimedia hospedados en la aplicación.

## <a name="application-hosted-media-bots-accessible-on-the-internet"></a>Bots multimedia hospedados en aplicaciones accesibles en Internet

Los bots multimedia hospedados en aplicaciones deben ser accesibles directamente en Internet. Estos bots deben incluir las siguientes características:

- Cada instancia de máquina virtual que hospeda un bot multimedia hospedado por la aplicación en Azure debe ser accesible directamente desde Internet mediante una dirección IP pública (ILPIP) de nivel de instancia.
    - Para obtener y configurar un ILPIP para un servicio en la nube de Azure, consulte [Instance level public IP classic overview](/azure/virtual-network/virtual-networks-instance-level-public-ip).
    - Para configurar un ILPIP para un conjunto de escalado de vm, consulte [public IPv4 per virtual machine](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine).
- El servicio que hospeda un bot multimedia hospedado por la aplicación también debe configurar cada instancia de máquina virtual con un puerto público que se asigna a la instancia específica.
    - Para un servicio en la nube de Azure, esto requiere un extremo de entrada de instancia. Para obtener más información, vea [Habilitar la comunicación para instancias de roles en Azure](/azure/cloud-services/cloud-services-enable-communication-role-instances).
    - Para un conjunto de escalado de vm, se debe configurar una regla NAT en el equilibrador de carga. Para obtener más información, [vea Redes virtuales y máquinas virtuales en Azure](/azure/virtual-machines/windows/network-overview).
- Los bots multimedia hospedados en aplicaciones no son compatibles con el Bot Framework Emulator.

En la siguiente sección se proporcionan detalles sobre las consideraciones de escalabilidad y rendimiento de los bots multimedia hospedados en la aplicación.

## <a name="scalability-and-performance-considerations"></a>Consideraciones de rendimiento y escalabilidad

Los bots multimedia hospedados en aplicaciones requieren las siguientes consideraciones de escalabilidad y rendimiento:
- Los bots multimedia hospedados en aplicaciones requieren más capacidad de cómputo y red (ancho de banda) que los bots de mensajería y pueden incurrir en costos operativos significativamente más altos. Un desarrollador de bots multimedia en tiempo real debe medir cuidadosamente la escalabilidad del bot y asegurarse de que el bot no acepta más llamadas simultáneas de las que puede administrar. Un bot habilitado para vídeo puede soportar solo una o dos sesiones multimedia simultáneas por núcleo de CPU (si usa los formatos de vídeo RGB24 o NV12 "sin procesar").
- Actualmente, la Plataforma multimedia en tiempo real no aprovecha las unidades de procesamiento de gráficos (GPU) disponibles en la máquina virtual para desactivar la codificación y decodificación de vídeo H.264. En su lugar, la codificación y descodificación de vídeo se realizan en el software de la CPU. Si hay una GPU disponible, el bot puede aprovecharlo para su propia representación de gráficos, por ejemplo, si el bot usa un motor de gráficos 3D.
- La instancia de vm que hospeda el bot multimedia en tiempo real debe tener al menos 2 núcleos de CPU. Para Azure, se recomienda una máquina virtual de la serie Dv2. Para otros tipos de vm de Azure, un sistema con cuatro CPU virtuales (vCPU) es el tamaño mínimo necesario. La documentación de Azure incluye información detallada sobre los tipos de máquina virtual [de Azure](/azure/virtual-machines/windows/sizes-general). 

## <a name="code-sample"></a>Ejemplo de código

Los ejemplos de bots multimedia hospedados en la aplicación son los siguientes:

| **Ejemplo de nombre** | **Descripción** | **Graph** |
|------------|-------------|-----------|
| Ejemplo de medios locales | Ejemplos que ilustran diferentes escenarios de medios locales. | [Ver](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples) |
| Ejemplo de medios remotos | Ejemplos que ilustran diferentes escenarios multimedia remotos. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/RemoteMediaSamples) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Formatos multimedia admitidos](~/resources/media-formats.md)

## <a name="see-also"></a>Vea también

- [Graph documentación del SDK de llamadas](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
- Los bots requieren más capacidad de procesamiento y ancho de banda de red que los bots de mensajería e incurren en costos operativos significativamente más altos. Un desarrollador de bots multimedia en tiempo real debe medir cuidadosamente la escalabilidad del bot y asegurarse de que el bot no acepta más llamadas simultáneas de las que puede administrar. Un bot habilitado para vídeo solo puede soportar una o dos sesiones multimedia simultáneas por núcleo de CPU si usa los formatos de vídeo RGB24 o NV12 sin procesar.
- Actualmente, la Plataforma multimedia en tiempo real no aprovecha las unidades de procesamiento de gráficos (GPU) disponibles en la máquina virtual para desactivar la codificación o decodificación de vídeo H.264. En su lugar, la codificación y descodificación de vídeo se realizan en el software de la CPU. Si hay una GPU disponible, el bot aprovecha para su propia representación gráfica, por ejemplo, si el bot usa un motor de gráficos 3D.
- La instancia de vm que hospeda el bot multimedia en tiempo real debe tener al menos 2 núcleos de CPU. Para Azure, se recomienda una máquina virtual de la serie Dv2. Para otros tipos de vm de Azure, un sistema con 4 CPU virtuales (vCPU) es el tamaño mínimo necesario. Para obtener más información acerca de los tipos de vm de Azure, consulte [documentación de Azure](/azure/virtual-machines/windows/sizes-general).

En la siguiente sección se proporcionan ejemplos que ilustran diferentes escenarios de medios locales.

## <a name="samples-and-additional-resources"></a>Ejemplos y recursos adicionales

- [Aplicaciones de ejemplo](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
- [Graph documentación del SDK de llamada](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)