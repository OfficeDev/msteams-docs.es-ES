---
title: Requisiciones y consideraciones para bots multimedia hospedados en la aplicación
description: Comprenda los requisitos y consideraciones importantes, así como las consideraciones de escalabilidad y rendimiento relacionadas con la creación de bots multimedia hospedados en aplicaciones para Microsoft Teams mediante ejemplos y ejemplos de código.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: máquina virtual de Azure de Windows Server multimedia hospedada en la aplicación
ms.date: 11/16/2018
ms.openlocfilehash: 987bb26ba7ad91f11228f7072d3e268ebd87dc5a
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756614"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>Requisiciones y consideraciones para bots multimedia hospedados en la aplicación

Un bot multimedia hospedado en la aplicación requiere la [`Microsoft.Graph.Communications.Calls.Media` biblioteca .NET](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) para acceder a las secuencias multimedia de audio y vídeo. El bot debe implementarse en una máquina local de Windows Server o en un sistema operativo (SO) invitado de Windows Server en Azure.

> [!NOTE]
>
> * Las instrucciones para desarrollar bots de mensajería y respuesta interactiva de voz (IVR) no se aplican completamente a la creación de bots multimedia hospedados en aplicaciones.
> * Dado que la plataforma multimedia en tiempo real de Microsoft para bots se encuentra en versión preliminar para desarrolladores, las orientaciones de este documento están sujetas a cambios.

## <a name="c-or-net-and-windows-server-for-development"></a>C# o .NET y Windows Server para desarrollo

Un bot multimedia hospedado en la aplicación requiere lo siguiente:

* El bot debe desarrollarse en C# y .NET Framework estándar e implementarse en Microsoft Azure. No puede usar las API de C++ o Node.js para acceder a elementos multimedia en tiempo real y .NET Core no es compatible con un bot multimedia hospedado en la aplicación.

* El bot se puede hospedar en uno de los siguientes entornos de servicio de Azure:
  * Servicio en la nube.
  * Service Fabric con VMSS (Conjuntos de escalado de máquina virtual).
  * Máquina virtual (VM) de infraestructura como servicio (IaaS).  
  
* El bot no se puede implementar como una aplicación web de Azure.

* El bot debe ejecutarse en una versión reciente de la biblioteca .NET `Microsoft.Graph.Communications.Calls.Media`. El bot debe usar la versión más reciente disponible del [paquete NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) o una versión que no tenga más de tres meses de antigüedad. Las versiones anteriores de la biblioteca están en desuso y no funcionan después de unos meses. Mantener actualizada la biblioteca `Microsoft.Graph.Communications.Calls.Media` garantiza la mejor interoperabilidad entre el bot y Microsoft Teams.

En la sección siguiente se proporcionan detalles sobre dónde se encuentran las llamadas multimedia en tiempo real.

## <a name="real-time-media-calls-stay-where-theyre-created"></a>Las llamadas multimedia en tiempo real permanecen donde se crean

Las llamadas multimedia en tiempo real permanecen en el equipo donde se crearon. Se ancla una llamada multimedia en tiempo real a la instancia de máquina virtual (VM) que aceptó o inició la llamada. Los elementos multimedia de una llamada o reunión de Microsoft Teams fluyen a esa instancia de máquina virtual y los elementos multimedia que el bot devuelve a Microsoft Teams también deben originarse desde esa máquina virtual. Si hay llamadas multimedia en tiempo real en curso cuando se detiene la máquina virtual, esas llamadas finalizan repentinamente. Si el bot tiene conocimiento previo del apagado de la máquina virtual pendiente, puede finalizar las llamadas.

En la próxima sección se proporcionan detalles sobre la accesibilidad de los bots multimedia hospedados en la aplicación.

## <a name="application-hosted-media-bots-accessible-on-the-internet"></a>Bots multimedia hospedados en la aplicación accesibles en Internet

Los bots multimedia hospedados en la aplicación deben ser accesibles directamente en Internet. Estos bots deben incluir las siguientes características:

* Cada instancia de máquina virtual que hospeda un bot multimedia hospedado en la aplicación en Azure debe ser accesible directamente desde Internet mediante una dirección IP pública de nivel de instancia (ILPIP).
  * Para obtener y configurar una ILPIP para un servicio en la nube de Azure, consulte [introducción a la IP pública a nivel de instancia clásica](/azure/virtual-network/virtual-networks-instance-level-public-ip).
  * Para configurar una ILPIP para un conjunto de escalado de máquina virtual, consulte [IPv4 público por máquina virtual](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine).
* El servicio que hospeda un bot multimedia hospedado en la aplicación también debe configurar cada instancia de máquina virtual con un puerto de acceso público que se asigne a la instancia específica.
  * Para un servicio en la nube de Azure, esto requiere un punto de conexión de entrada de instancia. Para obtener más información, consulte [habilitar la comunicación para instancias de rol en Azure](/azure/cloud-services/cloud-services-enable-communication-role-instances).
  * Para un conjunto de escalado de máquina virtual, se debe configurar una regla NAT en el equilibrador de carga. Para obtener más información, consulte [redes virtuales y máquinas virtuales en Azure](/azure/virtual-machines/windows/network-overview).

* El Bot Framework Emulator no admite bots multimedia hospedados en la aplicación.

En la sección siguiente se proporcionan detalles sobre las consideraciones de escalabilidad y rendimiento de los bots multimedia hospedados en la aplicación.

## <a name="scalability-and-performance-considerations"></a>Consideraciones de rendimiento y escalabilidad

Los bots multimedia hospedados en la aplicación requieren las siguientes consideraciones de escalabilidad y rendimiento:

* Los bots multimedia hospedados en la aplicación requieren más capacidad de proceso y red (ancho de banda) que los bots de mensajería y pueden incurrir en mayores costos operativos. Un desarrollador de bots multimedia en tiempo real debe medir cuidadosamente la escalabilidad del bot y asegurarse de que el bot no acepta más llamadas simultáneas de las que puede administrar. Un bot habilitado para vídeo puede admitir solo una o dos sesiones multimedia simultáneas por núcleo de CPU (si usa formatos de vídeo "raw" RGB24 o NV12).
* La plataforma multimedia en tiempo real no aprovecha actualmente ninguna unidad de procesamiento gráfico (GPU) disponible en la máquina virtual para descargar la codificación o descodificación de vídeo H.264. En su lugar, la codificación y descodificación de vídeo se realizan en el software de la CPU. Si hay una GPU disponible, el bot puede aprovecharla para su propia representación gráfica, por ejemplo, si el bot usa un motor de gráficos 3D.
* La instancia de máquina virtual que hospeda el bot multimedia en tiempo real debe tener al menos 2 núcleos de CPU. Para Azure, se recomienda una máquina virtual de la serie Dv2. Para otros tipos de máquina virtual de Azure, un sistema con cuatro CPU virtuales (vCPU) es el tamaño mínimo necesario. Puede encontrar información detallada sobre los tipos de máquina virtual de Azure en la [documentación de Azure](/azure/virtual-machines/windows/sizes-general).

## <a name="code-sample"></a>Ejemplo de código

Los ejemplos de bots multimedia hospedados en la aplicación son los siguientes:

| **Ejemplo de nombre** | **Descripción** | **Graph** |
|------------|-------------|-----------|
| Ejemplo de elementos multimedia locales | Ejemplo que muestra diferentes escenarios de medios locales. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples) |
| Ejemplo de elementos multimedia remotos | Ejemplo que muestra diferentes escenarios de medios remotos. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/RemoteMediaSamples) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Formatos multimedia admitidos](~/resources/media-formats.md)

## <a name="see-also"></a>Consulte también

* [Documentación del SDK de llamadas de Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
* Los bots requieren más capacidad de ancho de banda de red y proceso que los bots de mensajería y generan mayores costos operativos. Un desarrollador de bots multimedia en tiempo real debe medir cuidadosamente la escalabilidad del bot y asegurarse de que el bot no acepta más llamadas simultáneas de las que puede administrar. Un bot habilitado para vídeo puede admitir solo una o dos sesiones multimedia simultáneas por núcleo de CPU si usa formatos de vídeo "raw" RGB24 o NV12.
* La plataforma multimedia en tiempo real no aprovecha actualmente las unidades de procesamiento de gráficos (GPU) disponibles en la máquina virtual para desactivar la carga de codificación o descodificación de vídeo H.264. En su lugar, la codificación y descodificación de vídeo se realizan en el software de la CPU. Si hay una GPU disponible, el bot la aprovecha para su propia representación gráfica, por ejemplo, si el bot usa un motor de gráficos 3D.
* La instancia de máquina virtual que hospeda el bot multimedia en tiempo real debe tener al menos 2 núcleos de CPU. Para Azure, se recomienda una máquina virtual de la serie Dv2. Para otros tipos de máquina virtual de Azure, un sistema con 4 CPU virtuales (vCPU) es el tamaño mínimo necesario. Para obtener más información sobre los tipos de máquina virtual de Azure, consulte [documentación de Azure](/azure/virtual-machines/windows/sizes-general).

En la sección siguiente se proporcionan ejemplos que ilustran diferentes escenarios de elementos multimedia locales.

## <a name="samples-and-additional-resources"></a>Ejemplos y recursos adicionales

* [Aplicaciones de ejemplo](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
* [Documentación del SDK de llamadas de Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
