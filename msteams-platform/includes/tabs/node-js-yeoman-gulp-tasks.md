## <a name="create-the-app-package"></a>Crear el paquete de la aplicación

Necesitarás un paquete de aplicación para probar la pestaña en Teams. Es una carpeta zip que contiene los siguientes archivos necesarios:

- Un **icono de color completo** que mide 192 x 192 píxeles.
- Un **icono de esquema transparente** que mide 32 x 32 píxeles.
- Un **manifest.jsen** el archivo que especifica los atributos de la aplicación.

El paquete se crea a través de una tarea gulp que valida el archivo manifest.jsen y genera la carpeta zip en `./package directory` el archivo . En el símbolo del sistema, escriba:

```bash
gulp manifest
```

## <a name="build-your-application"></a>Compilar la aplicación

El comando build transpila la solución en la *carpeta ./dist.* Siguiente,escriba:

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a>Ejecutar la aplicación en localhost

Para iniciar un servidor web local, escriba lo siguiente:

```bash
gulp serve
```

Escriba `http://localhost:3007/<yourDefaultAppNameTab>/` en el explorador y vea la página principal de la aplicación:

![captura de pantalla de la página principal](~/assets/images/tab-images/homePage.png)