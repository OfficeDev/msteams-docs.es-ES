---
title: Uso de Fluid con Teams
author: timtwang
ms.author: mobajemu
description: Tutorial para integrar características de colaboración en tiempo real con tecnología fluid en una aplicación de pestaña de Microsoft Teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 620e2150ca6300fb8d37bc7c68b965aacb19700b
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615494"
---
# <a name="use-fluid-with-teams"></a>Uso de Fluid con Teams

Al final de este tutorial, puede integrar cualquier aplicación con tecnología Fluid en Teams y colaborar con otros usuarios en tiempo real.

En esta sección puede aprender los siguientes conceptos:

1. Integre un cliente de Fluid en la aplicación de pestaña de Teams.
1. Ejecute y conecte la aplicación de Teams a un servicio Fluid (Azure Fluid Relay).
1. Cree y obtenga contenedores fluidos y páselos a un componente de React.

Para obtener más información sobre cómo compilar aplicaciones complejas, consulte El ejemplo de [Fluid नमस्ते संसार de Teams](https://github.com/microsoft/FluidExamples/tree/main/teams-fluid-hello-world) en nuestro repositorio FluidExamples.

## <a name="prerequisites"></a>Requisitos previos

Este tutorial requiere estar familiarizado con los siguientes conceptos y recursos:

- [Información general sobre Fluid Framework](https://fluidframework.com/docs/)
- [Inicio rápido de Fluid Framework](https://fluidframework.com/docs/start/quick-start/)
- Los conceptos básicos de [los enlaces de React](https://reactjs.org/) y [React](https://reactjs.org/docs/hooks-intro.html)
- Cómo crear una [pestaña de Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs)

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](tab-requirements.md)

## <a name="create-the-project"></a>Cree el proyecto

1. Abra un símbolo del sistema y vaya a la carpeta primaria donde desea crear el proyecto, por ejemplo, `/My Microsoft Teams Projects`.
1. Cree una aplicación de pestaña de Teams ejecutando el siguiente comando y [creando una pestaña de canal](create-channel-group-tab.md#create-a-custom-channel-or-group-tab-with-nodejs):

    ```cmd
    yo teams
    ```

1. Después de crear, vaya al proyecto con el siguiente comando `cd <your project name>`.
1. El proyecto usa las siguientes bibliotecas:

    |Biblioteca |Descripción |
    |---|---|
    | `fluid-framework`    |Contiene IFluidContainer y otras [estructuras de datos distribuidas](https://fluidframework.com/docs/build/dds/) que sincronizan datos entre clientes.|
    | `@fluidframework/azure-client`   |Define el esquema inicial del [contenedor Fluid](https://fluidframework.com/docs/build/containers/).|
    | `@fluidframework/test-client-utils` |Define el `InsecureTokenProvider` necesario para crear la conexión a un servicio Fluid.|

    Ejecute el siguiente comando para instalar las bibliotecas:

    ```cmd
    npm install @fluidframework/azure-client fluid-framework @fluidframework/test-client-utils
    ```

## <a name="code-the-project"></a>Codificar el proyecto

1. Abra el archivo `/src/client/<your tab name>` en el editor de código.
1. Cree un archivo como `Util.ts` y agregue las siguientes instrucciones de importación:

    ```ts
    //`Util.ts

    import { IFluidContainer } from "fluid-framework";
    import { AzureClient, AzureClientProps } from "@fluidframework/azure-client";
    import { InsecureTokenProvider } from "@fluidframework/test-client-utils";
    ```

### <a name="defining-fluid-functions-and-parameters"></a>Definición de funciones y parámetros de Fluid

Esta aplicación está pensada para usarse en el contexto de Microsoft Teams, con todas las importaciones, inicialización y funciones relacionadas con Fluid. Esto proporciona una experiencia mejorada y facilita su uso en el futuro. Puede agregar el código siguiente a las instrucciones import:

```ts
// TODO 1: Define the parameter key(s).
// TODO 2: Define container schema.
// TODO 3: Define connectionConfig (AzureClientProps).
// TODO 4: Create Azure client.
// TODO 5: Define create container function.
// TODO 6: Define get container function.
```

> [!NOTE]
> Los comentarios definen todas las funciones y constantes necesarias para interactuar con el servicio Fluid y el contenedor.

1. Reemplace `TODO 1:` por el código siguiente:

    ```ts
    export const containerIdQueryParamKey = "containerId";
    ```

    La constante se exporta a medida que se anexa a `contentUrl` en la configuración de Microsoft Teams y, posteriormente, para analizar el identificador de contenedor en la página de contenido. Es un patrón común almacenar claves de parámetros de consulta importantes como constantes, en lugar de escribir la cadena sin procesar cada vez.

    Antes de que el cliente pueda crear contenedores, necesita un `containerSchema` que defina los objetos compartidos que se usan en esta aplicación. En este ejemplo se usa SharedMap como `initialObjects`, pero se puede usar cualquier objeto compartido.

    > [!NOTE]
    > `map` es el identificador del `SharedMap` objeto y debe ser único dentro del contenedor como cualquier otro DDS.

1. Reemplace `TODO: 2` por el código siguiente:

    ```ts
    const containerSchema = {
        initialObjects: { map: SharedMap }
    };
    ```

1. Reemplace `TODO: 3` por el código siguiente:

    ```ts
    const connectionConfig : AzureClientProps =
    {
        connection: {
            type: "local",
            tokenProvider: new InsecureTokenProvider("foobar", { id: "user" }),
            endpoint: "http://localhost:7070"
        }
    };
    ```

    Antes de que se pueda usar el cliente, necesita un `AzureClientProps` que defina el tipo de conexión que usa el cliente. La `connectionConfig` propiedad es necesaria para conectarse al servicio. Se usa el modo local del cliente de Azure. Para habilitar la colaboración entre todos los clientes, reemplácela por credenciales de Fluid Relay Service. Para más información, consulte configuración [del servicio Azure Fluid Relay](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal).

1. Reemplace `TODO: 4` por el código siguiente:

    ```ts
    const client = new AzureClient(connectionConfig);
    ```

1. Reemplace `TODO: 5` por el código siguiente:

    ```ts
    export async function createContainer() : Promise<string> {
        const { container } = await client.createContainer(containerSchema);
        const containerId = await container.attach();
        return containerId;
    };
    ```

    A medida que crea el contenedor en la página de configuración y lo anexa a la `contentUrl` configuración de Teams, debe devolver el identificador de contenedor después de adjuntar el contenedor.

1. Reemplace `TODO: 6` por el código siguiente:

    ```ts
    export async function getContainer(id : string) : Promise<IFluidContainer> {
        const { container } = await client.getContainer(id, containerSchema);
        return container;
    };
    ```

    Al capturar el contenedor de Fluid, debe devolver el contenedor, ya que la aplicación debe interactuar con el contenedor y los DDS dentro de él, en la página de contenido.

### <a name="create-fluid-container-in-the-configuration-page"></a>Creación de un contenedor fluid en la página de configuración

1. Abra el archivo `src/client/<your tab name>/<your tab name>Config.tsx` en el editor de código.

    El flujo de aplicación de pestaña estándar de Teams va de la configuración a la página de contenido. Para habilitar la colaboración, es fundamental conservar el contenedor mientras se carga en la página de contenido. La mejor solución para conservar el contenedor es anexar el identificador de contenedor a y `contentUrl` `websiteUrl`, las direcciones URL de la página de contenido, como parámetro de consulta. El botón Guardar de la página de configuración de Teams es la puerta de enlace entre la página de configuración y la página de contenido. Es un lugar para crear el contenedor y anexar el identificador de contenedor en la configuración.

1. Agregue la siguiente instrucción de importación:

    ```ts
    import { createContainer, containerIdQueryParamKey } from "./Util";
    ```

1. Reemplace el método `onSaveHandler` con el siguiente código: Las únicas líneas agregadas aquí son llamar al método create container definido anteriormente en `Utils.ts` y, a continuación, anexar el identificador de contenedor devuelto a `contentUrl` y `websiteUrl` como parámetro de consulta.

    ```ts {linenos=inline,hl_lines=[134,136,137]}
    const onSaveHandler = async (saveEvent: microsoftTeams.settings.SaveEvent) => {
        const host = "https://" + window.location.host;
        const containerId = await createContainer();
        microsoftTeams.settings.setSettings({
            contentUrl: host + "/<your tab name>/?" + containerIdQueryParamKey + "=" + containerId + "&name={loginHint}&tenant={tid}&group={groupId}&theme={theme}",
            websiteUrl: host + "/<your tab name>/?" + containerIdQueryParamKey + "=" + containerId + "&name={loginHint}&tenant={tid}&group={groupId}&theme={theme}",
            suggestedDisplayName: "<your tab name>",
            removeUrl: host + "/<your tab name>/remove.html?theme={theme}",
            entityId: entityId.current
        });
        saveEvent.notifySuccess();
    };
    ```

    Asegúrese de reemplazar por `<your tab name>` el nombre de la pestaña del proyecto.

    > [!WARNING]
    > A medida que se usa la dirección URL de la página de contenido para almacenar el identificador de contenedor, este registro se quita si se elimina la pestaña Teams.
    > Además, cada página de contenido solo puede admitir un identificador de contenedor.

### <a name="refactor-content-page-to-reflect-fluid-application"></a>Página de refactorización de contenido para reflejar la aplicación Fluid

1. Abra el archivo `src/client/<your tab name>/<your tab name>.tsx` en el editor de código. Una aplicación típica con tecnología Fluid consta de una vista y una estructura de datos Fluid. Céntrese en obtener o cargar el contenedor Fluid y deje todas las interacciones relacionadas con Fluid en un componente React.

1. Agregue las siguientes instrucciones de importación en la página de contenido:

    ```ts
    import { IFluidContainer } from "fluid-framework";
    import { getContainer, containerIdQueryParamKey } from "./Util";
    ```

1. Quite todo el código debajo de las instrucciones import de la página de contenido y reemplácelo por lo siguiente:

    ```ts
    export const <your tab name> = () => {
      // TODO 1: Initialize Microsoft Teams.
      // TODO 2: Initialize inTeams boolean.
      // TODO 3: Define container as a React state.
      // TODO 4: Define a method that gets the Fluid container
      // TODO 5: Get Fluid container on content page startup.
      // TODO 6: Pass the container to the React component as argument.
    }
    ```

    Asegúrese de reemplazar por `<your tab name>` el nombre de pestaña que defina para el proyecto.

1. Reemplace `TODO 1` por el código siguiente:

    ```ts
    microsoftTeams.initialize();
    ```

    Para mostrar la página de contenido en Teams, debe incluir el [SDK de cliente javascript de Microsoft Teams](/javascript/api/overview/msteams-client) e incluir una llamada para inicializarla después de que se cargue la página.

1. Reemplace `TODO 2` por el código siguiente:

    ```ts
    const [{ inTeams }] = useTeams();
    ```

    Como la aplicación de Teams es simplemente una inserción de IFrame de una página web, debe inicializar la `inTeams` constante booleana para saber si la aplicación está dentro de Teams o no, y si los recursos de Teams, como `contentUrl`, están disponibles.

1. Reemplace `TODO 3` por el código siguiente:

    ```ts
    const [fluidContainer, setFluidContainer] = useState<IFluidContainer | undefined>(undefined);
    ```

    Use un estado de React para el contenedor, ya que proporciona la capacidad de actualizar dinámicamente el contenedor y los objetos de datos que contiene.

1. Reemplace `TODO 4` por el código siguiente:

    ```ts
    const getFluidContainer = async (url : URLSearchParams) => {
        const containerId = url.get(containerIdQueryParamKey);
        if (!containerId) {
            throw Error("containerId not found in the URL");
        }
        const container = await getContainer(containerId);
        setFluidContainer(container);
    };
    ```

    Analice la dirección URL para obtener la cadena del parámetro de consulta, definida por `containerIdQueryParamKey`y recuperar el identificador de contenedor. Con el identificador de contenedor, puede cargar el contenedor. Una vez que tenga el contenedor, establezca el `fluidContainer` estado React, consulte el paso anterior.

1. Reemplace `TODO 5` por el código siguiente:

    ```ts
    useEffect(() => {
        if (inTeams === true) {
            microsoftTeams.settings.getSettings(async (instanceSettings) => {
                const url = new URL(instanceSettings.contentUrl);
                getFluidContainer(url.searchParams);
            });
            microsoftTeams.appInitialization.notifySuccess();
        }
    }, [inTeams]);
    ```

    Después de definir cómo obtener el contenedor fluid, debe indicar a React que llame `getFluidContainer` a la carga y, a continuación, almacenar el resultado en el estado en función de si la aplicación está dentro de Teams.
    el [enlace useState](https://reactjs.org/docs/hooks-state.html) de React proporciona el almacenamiento necesario y [useEffect](https://reactjs.org/docs/hooks-effect.html) permite llamar `getFluidContainer` a en representación, pasando el valor devuelto a `setFluidContainer`.

    Al agregar `inTeams` en la matriz de dependencias al final de , la aplicación garantiza que esta función solo se llame en la carga de `useEffect`la página de contenido.

1. Reemplace `TODO 6` por el código siguiente:

    ```ts
    if (inTeams === false) {
      return (
          <div>This application only works in the context of Microsoft Teams</div>
      );
    }

    if (fluidContainer !== undefined) {
      return (
          <FluidComponent fluidContainer={fluidContainer} />
      );
    }

    return (
      <div>Loading FluidComponent...</div>
    );
    ```

    > [!NOTE]
    > Es importante asegurarse de que la página de contenido se carga dentro de Teams y de que el contenedor fluid se define antes de pasarlo al componente React (definido como `FluidComponent`, vea a continuación).

### <a name="create-react-component-for-fluid-view-and-data"></a>Creación de un componente de React para la vista y los datos de Fluid

Ha integrado el flujo de creación básico de Teams y Fluid. Ahora puede crear su propio componente de React que controle las interacciones entre la vista de la aplicación y los datos de Fluid. A partir de ahora, la lógica y el flujo se comportan igual que otras aplicaciones con tecnología Fluid. Con la estructura básica configurada, puede crear cualquiera de los [ejemplos de Fluid](https://github.com/microsoft/FluidExamples) como una aplicación de Teams cambiando la interacción de la `ContainerSchema` vista de aplicación y con los objetos DDSes/data de la página de contenido.

## <a name="start-the-fluid-server-and-run-the-application"></a>Iniciar el servidor de Fluid y ejecutar la aplicación

Si ejecuta la aplicación de Teams localmente con el modo local cliente de Azure, asegúrese de ejecutar el siguiente comando en el símbolo del sistema para iniciar el servicio Fluid:

```cmd
npx @fluidframework/azure-local-service@latest
```

Para ejecutar e iniciar la aplicación de Teams, abra otro terminal y siga las [instrucciones para ejecutar el servidor de aplicaciones](create-channel-group-tab.md#upload-your-application-to-teams).

> [!WARNING]
> No se conservan los nombres de host con `ngrok`los túneles gratuitos. Cada ejecución generará una dirección URL diferente. Cuando se crea un nuevo `ngrok` túnel, ya no se podrá acceder al contenedor anterior. Para escenarios de producción, consulte [Uso de AzureClient con Azure Fluid Relay](#use-azureclient-with-azure-fluid-relay).

> [!NOTE]
> Instale una dependencia adicional para que esta demostración sea compatible con Webpack 5. Si recibe un error de compilación relacionado con un paquete de "búfer", ejecute `npm install -D buffer` e inténtelo de nuevo. Esto se resolverá en una versión futura de Fluid Framework.

## <a name="next-steps"></a>Pasos siguientes

### <a name="use-azureclient-with-azure-fluid-relay"></a>Uso de AzureClient con Azure Fluid Relay

Como se trata de una aplicación de pestaña de Teams, la colaboración y la interacción son el foco principal. Reemplace el modo `AzureClientProps` local proporcionado anteriormente por las credenciales no locales de la instancia de servicio de Azure para que otros usuarios puedan unirse e interactuar con usted en la aplicación. Consulte [cómo aprovisionar el servicio Azure Fluid Relay](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal).

> [!IMPORTANT]
> Es importante ocultar las credenciales que se pasan `AzureClientProps` para que no se confirmen accidentalmente en el control de código fuente. El proyecto de Teams incluye un `.env` archivo donde puede almacenar sus credenciales como variables de entorno y el propio archivo ya está incluido en .`.gitignore` Para usar las variables de entorno en Teams, consulte [Establecimiento y obtención de variables de entorno](#set-and-get-environment-variable).

> [!WARNING]
> `InsecureTokenProvider` es una manera cómoda de probar la aplicación localmente. Es su responsabilidad controlar cualquier autenticación de usuario y usar un [token seguro](/azure/azure-fluid-relay/how-tos/connect-fluid-azure-service) para cualquier entorno de producción.

### <a name="set-and-get-environment-variable"></a>Establecimiento y obtención de una variable de entorno

Para establecer una variable de entorno y recuperarla en Teams, puede aprovechar el archivo integrado `.env` . El código siguiente se usa para establecer la variable de entorno en `.env`:

```
# .env

TENANT_KEY=foobar
```

Para pasar el contenido del `.env` archivo a nuestra aplicación del lado cliente, debe configurarlo en `webpack.config.js` para que `webpack` proporcione acceso a ellos en tiempo de ejecución. Use el código siguiente para agregar la variable de entorno de `.env`:

```js
// webpack,config.js

webpack.EnvironmentPlugin({
    PUBLIC_HOSTNAME: undefined,
    TAB_APP_ID: null,
    TAB_APP_URI: null,
    REACT_APP_TENANT_KEY: JSON.stringify(process.env.TENANT_KEY) // Add environment variable here
}),
```

Puede acceder a la variable de entorno en `Util.ts`

```ts
// Util.ts

tokenProvider: new InsecureTokenProvider(JSON.parse(process.env.REACT_APP_TENANT_KEY!), { id: "user" }),
```

> [!TIP]
> Al realizar cambios en el código, el proyecto se vuelve a generar automáticamente y el servidor de aplicaciones se vuelve a cargar. Sin embargo, si realiza cambios en el esquema de contenedor, solo surtirán efecto si cierra y reinicia el servidor de aplicaciones. Para ello, vaya al símbolo del sistema y presione Ctrl-C dos veces. A continuación, ejecute `gulp serve` o `gulp ngrok-serve` de nuevo.

## <a name="see-also"></a>Vea también

- [Documentación de Azure Fluid Relay](/azure/azure-fluid-relay)

- [Documentación de Fluid Framework](https://fluidframework.com/docs/)
- [Repositorio de GitHub de ejemplos fluidos](https://github.com/microsoft/FluidExamples)
