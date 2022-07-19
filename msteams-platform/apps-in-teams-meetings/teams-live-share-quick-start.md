---
title: Inicio rápido de Live Share
author: surbhigupta
description: En este módulo, aprenderá a probar de forma rápida el ejemplo de Lanzamiento de dados
ms.topic: conceptual
ms.localizationpriority: high
ms.author: stevenic
ms.date: 04/07/2022
ms.openlocfilehash: 10bf4b3ce67322c25517d82af2d06a654a4d8668
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841788"
---
# <a name="quick-start-guide"></a>Guía de inicio rápido

Introducción al SDK de Live Share mediante el ejemplo de lanzamiento de dados es una evolución del [Inicio rápido de Fluid Framework](https://fluidframework.com/docs/start/quick-start/) y está diseñado para ejecutar rápidamente una [muestra de lanzamiento de dados](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller) basada en el SDK de Live Share en el host local del equipo.

:::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="Ejemplo de Lanzamiento de dados":::

> [!NOTE]
> En esta guía se explica cómo usar Live Share localmente en un explorador. Para más información sobre el uso del SDK en una reunión de Teams, pruebe nuestro [tutorial de Agile Poker](../sbs-teams-live-share.yml).

## <a name="set-up-your-development-environment"></a>Configurar el entorno de desarrollo

Para empezar, instale lo siguiente:

* [Node.js](https://nodejs.org/en/download): el SDK de Live Share admite Node.js LTS versiones 12.17 y posteriores.
* [Versión más reciente de Visual Studio Code](https://code.visualstudio.com/).
* [Git](https://git-scm.com/downloads)

## <a name="build-and-run-the-dice-roller-app"></a>Compilar y ejecutar la aplicación Lanzamiento de dados

1. Vaya a la aplicación de ejemplo [Lanzamiento de dados](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller).

1. Clone el repositorio del [SDK de Live Share](https://github.com/microsoft/live-share-sdk) para probar la aplicación de ejemplo:

    ```bash
    git clone https://github.com/microsoft/live-share-sdk.git
    ```

1. Ejecute el siguiente comando para ir a la carpeta de la aplicación de ejemplo Lanzamiento de dados:

   ```bash
    cd live-share-sdk\samples\01.dice-roller
   ```

1. Ejecute el siguiente comando para instalar el paquete de dependencias:

    ```bash
    npm install
    ```

1. Ejecute el comando siguiente para iniciar el cliente y el servidor local:

   ```bash
   npm start
   ```
  
     Una nueva pestaña del explorador abrirá una dirección URL `http://localhost:8080` y aparecerá el juego Lanzamiento de dados.

1. Copie la dirección URL completa en el explorador, incluyendo el identificador, y pegue la dirección URL en una nueva ventana o en otro explorador.

   Se abrirá un segundo cliente para la aplicación Lanzamiento de dados.

1. Abra ambas ventanas y seleccione el botón **Revertir** en una ventana. El estado de los dados cambiará en ambos clientes.

    :::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="Múltiples pestañas de Lanzamiento de dados":::
  
   **Enhorabuena**, ha aprendido a compilar y ejecutar una aplicación mediante el SDK de Live Share.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Tutorial de Lanzamiento de dados](teams-live-share-tutorial.md)

## <a name="see-also"></a>Vea también

* [Repositorio de GitHub](https://github.com/microsoft/live-share-sdk)
* [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
* [Documentos de referencia del SDK multimedia de Live Share](/javascript/api/@microsoft/live-share-media/)
* [Capacidades de Live Share](teams-live-share-capabilities.md)
* [Preguntas más frecuentes sobre Live Share](teams-live-share-faq.md)
* [Aplicaciones de Teams en las reuniones](teams-apps-in-meetings.md)
