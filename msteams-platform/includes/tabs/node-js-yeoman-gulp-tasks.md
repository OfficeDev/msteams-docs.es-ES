## <a name="create-the-app-package"></a><span data-ttu-id="23796-101">Crear el paquete de la aplicación</span><span class="sxs-lookup"><span data-stu-id="23796-101">Create the app package</span></span>

<span data-ttu-id="23796-102">Necesitarás un paquete de aplicación para probar la pestaña en Teams.</span><span class="sxs-lookup"><span data-stu-id="23796-102">You'll need an app package to test your tab in Teams.</span></span> <span data-ttu-id="23796-103">Es una carpeta zip que contiene los siguientes archivos necesarios:</span><span class="sxs-lookup"><span data-stu-id="23796-103">It's a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="23796-104">Un **icono de color completo** que mide 192 x 192 píxeles.</span><span class="sxs-lookup"><span data-stu-id="23796-104">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="23796-105">Un **icono de esquema transparente** que mide 32 x 32 píxeles.</span><span class="sxs-lookup"><span data-stu-id="23796-105">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="23796-106">Un **manifest.jsen** el archivo que especifica los atributos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="23796-106">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="23796-107">El paquete se crea a través de una tarea gulp que valida el archivo manifest.jsen y genera la carpeta zip en `./package directory` el archivo .</span><span class="sxs-lookup"><span data-stu-id="23796-107">The package is created via a gulp task that validates the manifest.json file and generates the zip folder in the `./package directory`.</span></span> <span data-ttu-id="23796-108">En el símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="23796-108">In the command prompt enter:</span></span>

```bash
gulp manifest
```

## <a name="build-your-application"></a><span data-ttu-id="23796-109">Compilar la aplicación</span><span class="sxs-lookup"><span data-stu-id="23796-109">Build your application</span></span>

<span data-ttu-id="23796-110">El comando build transpila la solución en la *carpeta ./dist.*</span><span class="sxs-lookup"><span data-stu-id="23796-110">The build command transpiles your solution into the *./dist* folder.</span></span> <span data-ttu-id="23796-111">Siguiente,escriba:</span><span class="sxs-lookup"><span data-stu-id="23796-111">Next,enter:</span></span>

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a><span data-ttu-id="23796-112">Ejecutar la aplicación en localhost</span><span class="sxs-lookup"><span data-stu-id="23796-112">Run your application in localhost</span></span>

<span data-ttu-id="23796-113">Para iniciar un servidor web local, escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="23796-113">Start a local web server by entering the following:</span></span>

```bash
gulp serve
```

<span data-ttu-id="23796-114">Escriba `http://localhost:3007/<yourDefaultAppNameTab>/` en el explorador y vea la página principal de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="23796-114">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser and view your application's home page:</span></span>

![captura de pantalla de la página principal](~/assets/images/tab-images/homePage.png)