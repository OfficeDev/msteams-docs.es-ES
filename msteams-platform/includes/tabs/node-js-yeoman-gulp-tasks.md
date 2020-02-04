## <a name="create-the-app-package"></a>Crear el paquete de la aplicación

Necesitará un paquete de la aplicación para probar la pestaña en Microsoft Teams. Se trata de una carpeta ZIP que contiene los siguientes archivos necesarios:

- Un **icono de color completo** que mide 192 x 192 píxeles.
- Un **icono de contorno transparente** que mide 32 x 32 píxeles.
- Un archivo **manifest. JSON** que especifica los atributos de la aplicación.

El paquete se crea a través de una tarea de Gulp que valida el archivo manifest. JSON y genera la carpeta zip `./package directory`en el. En el símbolo del sistema, escriba:

```bash
gulp manifest
```

## <a name="build-your-application"></a>Compilar la aplicación

El comando de compilación transpilará la solución a la carpeta *./Dist.* . A continuación, escriba:

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a>Ejecutar la aplicación en localhost

Escriba lo siguiente para iniciar un servidor Web local:

```bash
gulp serve
```

Escriba `http://localhost:3007/<yourDefaultAppNameTab>/` en el explorador y vea la Página principal de la aplicación:

![captura de pantalla de página principal](~/assets/images/tab-images/homePage.png)