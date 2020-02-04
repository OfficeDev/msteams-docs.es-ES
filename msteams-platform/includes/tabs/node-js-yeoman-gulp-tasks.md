## <a name="create-the-app-package"></a><span data-ttu-id="8a1dc-101">Crear el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="8a1dc-101">Create the app package</span></span>

<span data-ttu-id="8a1dc-102">Necesitará un paquete de la aplicación para probar la pestaña en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8a1dc-102">You'll need an app package to test your tab in Teams.</span></span> <span data-ttu-id="8a1dc-103">Se trata de una carpeta ZIP que contiene los siguientes archivos necesarios:</span><span class="sxs-lookup"><span data-stu-id="8a1dc-103">It's a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="8a1dc-104">Un **icono de color completo** que mide 192 x 192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="8a1dc-104">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="8a1dc-105">Un **icono de contorno transparente** que mide 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="8a1dc-105">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="8a1dc-106">Un archivo **manifest. JSON** que especifica los atributos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a1dc-106">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="8a1dc-107">El paquete se crea a través de una tarea de Gulp que valida el archivo manifest. JSON y genera la carpeta zip `./package directory`en el.</span><span class="sxs-lookup"><span data-stu-id="8a1dc-107">The package is created via a gulp task that validates the manifest.json file and generates the zip folder in the `./package directory`.</span></span> <span data-ttu-id="8a1dc-108">En el símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="8a1dc-108">In the command prompt enter:</span></span>

```bash
gulp manifest
```

## <a name="build-your-application"></a><span data-ttu-id="8a1dc-109">Compilar la aplicación</span><span class="sxs-lookup"><span data-stu-id="8a1dc-109">Build your application</span></span>

<span data-ttu-id="8a1dc-110">El comando de compilación transpilará la solución a la carpeta *./Dist.* .</span><span class="sxs-lookup"><span data-stu-id="8a1dc-110">The build command transpiles your solution into the *./dist* folder.</span></span> <span data-ttu-id="8a1dc-111">A continuación, escriba:</span><span class="sxs-lookup"><span data-stu-id="8a1dc-111">Next,enter:</span></span>

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a><span data-ttu-id="8a1dc-112">Ejecutar la aplicación en localhost</span><span class="sxs-lookup"><span data-stu-id="8a1dc-112">Run your application in localhost</span></span>

<span data-ttu-id="8a1dc-113">Escriba lo siguiente para iniciar un servidor Web local:</span><span class="sxs-lookup"><span data-stu-id="8a1dc-113">Start a local web server by entering the following:</span></span>

```bash
gulp serve
```

<span data-ttu-id="8a1dc-114">Escriba `http://localhost:3007/<yourDefaultAppNameTab>/` en el explorador y vea la Página principal de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="8a1dc-114">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser and view your application's home page:</span></span>

![captura de pantalla de página principal](~/assets/images/tab-images/homePage.png)