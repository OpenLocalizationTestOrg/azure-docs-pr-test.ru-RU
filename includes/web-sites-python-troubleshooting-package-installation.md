<span data-ttu-id="dd647-101">Некоторые пакеты могут не установиться с помощью pip при запуске Azure.</span><span class="sxs-lookup"><span data-stu-id="dd647-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="dd647-102">Просто возможно, этот пакет hello не доступен на hello индекс пакета Python.</span><span class="sxs-lookup"><span data-stu-id="dd647-102">It may simply be that hello package is not available on hello Python Package Index.</span></span>  <span data-ttu-id="dd647-103">Возможно, что компилятор не требуется (компилятора недоступен на hello машины выполняющегося hello веб-приложения в службе приложений Azure).</span><span class="sxs-lookup"><span data-stu-id="dd647-103">It could be that a compiler is required (a compiler is not available on hello machine running hello web app in Azure App Service).</span></span>

<span data-ttu-id="dd647-104">В этом разделе мы рассмотрим способы toodeal с этой проблемой.</span><span class="sxs-lookup"><span data-stu-id="dd647-104">In this section, we'll look at ways toodeal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="dd647-105">Запрос архивов wheel</span><span class="sxs-lookup"><span data-stu-id="dd647-105">Request wheels</span></span>
<span data-ttu-id="dd647-106">Если установка пакета hello требует компилятора, следует обратитесь toorequest владельца пакета hello, колеса доступны для пакета hello.</span><span class="sxs-lookup"><span data-stu-id="dd647-106">If hello package installation requires a compiler, you should try contacting hello package owner toorequest that wheels be made available for hello package.</span></span>

<span data-ttu-id="dd647-107">С hello последних доступность [Microsoft Visual C++ компилятор для Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], теперь стало проще toobuild пакеты, имеющие машинного кода Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="dd647-107">With hello recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier toobuild packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="dd647-108">Сборки wheel (требуется Windows)</span><span class="sxs-lookup"><span data-stu-id="dd647-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="dd647-109">Примечание: При использовании этого параметра, убедитесь, что пакет toocompile hello, с помощью среды Python, который соответствует hello/архитектура и версии платформы, используемой на веб-приложения hello в службе приложений Azure (Windows/32-bit/2.7 или 3.4).</span><span class="sxs-lookup"><span data-stu-id="dd647-109">Note: When using this option, make sure toocompile hello package using a Python environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="dd647-110">Если hello пакет не устанавливается, поскольку компилятору требуется, можно установить компилятора hello на локальном компьютере и сборка колеса для hello пакета, который затем будут включены в репозитории.</span><span class="sxs-lookup"><span data-stu-id="dd647-110">If hello package doesn't install because it requires a compiler, you can install hello compiler on your local machine and build a wheel for hello package, which you will then include in your repository.</span></span>

<span data-ttu-id="dd647-111">Пользователей Mac и Linux: Если у вас нет доступа tooa Windows компьютера, см. раздел [создания виртуальной машины под управлением Windows] [ Create a Virtual Machine Running Windows] как toocreate ВМ в Azure.</span><span class="sxs-lookup"><span data-stu-id="dd647-111">Mac/Linux Users: If you don't have access tooa Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how toocreate a VM on Azure.</span></span>  <span data-ttu-id="dd647-112">Использовать toobuild hello колеса, добавьте их toohello репозитория и при необходимости отменить hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="dd647-112">You can use it toobuild hello wheels, add them toohello repository, and discard hello VM if you like.</span></span> 

<span data-ttu-id="dd647-113">Python 2.7, можно установить [Microsoft Visual C++ компилятор для Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="dd647-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="dd647-114">Python 3.4, можно установить [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="dd647-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="dd647-115">toobuild колеса, вам потребуется hello колесо пакета:</span><span class="sxs-lookup"><span data-stu-id="dd647-115">toobuild wheels, you'll need hello wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="dd647-116">Вы воспользуетесь `pip wheel` toocompile зависимость:</span><span class="sxs-lookup"><span data-stu-id="dd647-116">You'll use `pip wheel` toocompile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="dd647-117">Будет создан файл .whl в папке \wheelhouse hello.</span><span class="sxs-lookup"><span data-stu-id="dd647-117">This creates a .whl file in hello \wheelhouse folder.</span></span>  <span data-ttu-id="dd647-118">Добавьте папку \wheelhouse hello и колесо файлы tooyour репозитория.</span><span class="sxs-lookup"><span data-stu-id="dd647-118">Add hello \wheelhouse folder and wheel files tooyour repository.</span></span>

<span data-ttu-id="dd647-119">Изменить ваш hello tooadd requirements.txt `--find-links` параметр вверху hello.</span><span class="sxs-lookup"><span data-stu-id="dd647-119">Edit your requirements.txt tooadd hello `--find-links` option at hello top.</span></span> <span data-ttu-id="dd647-120">Это заставляет toolook PIP-адрес для точного совпадения в локальной папке hello перед индекс пакета python toohello постоянной.</span><span class="sxs-lookup"><span data-stu-id="dd647-120">This tells pip toolook for an exact match in hello local folder before going toohello python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="dd647-121">Следует tooinclude вообще индексировать все зависимости, в hello \wheelhouse папку и не используйте hello пакет python можно принудительно hello пакета pip tooignore индекс путем добавления `--no-index` toohello верхней части вашего requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="dd647-121">If you want tooinclude all your dependencies in hello \wheelhouse folder and not use hello python package index at all, you can force pip tooignore hello package index by adding `--no-index` toohello top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="dd647-122">Настройка установки</span><span class="sxs-lookup"><span data-stu-id="dd647-122">Customize installation</span></span>
<span data-ttu-id="dd647-123">Можно настроить tooinstall сценария hello развертывания пакета в виртуальной среде hello, с помощью альтернативных установщика, таких как просто\_установки.</span><span class="sxs-lookup"><span data-stu-id="dd647-123">You can customize hello deployment script tooinstall a package in hello virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="dd647-124">Закомментированный пример см. в файле deploy.cmd.  Убедитесь, что эти пакеты не указанные в requirements.txt tooprevent pip из их установки.</span><span class="sxs-lookup"><span data-stu-id="dd647-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, tooprevent pip from installing them.</span></span>

<span data-ttu-id="dd647-125">Добавьте этот сценарий развертывания toohello:</span><span class="sxs-lookup"><span data-stu-id="dd647-125">Add this toohello deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="dd647-126">Также может быть легко может toouse\_установите tooinstall из EXE-файла установщика (некоторые являются ZIP-совместимость, поэтому просто\_их поддерживает установки).</span><span class="sxs-lookup"><span data-stu-id="dd647-126">You may also be able toouse easy\_install tooinstall from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="dd647-127">Добавить репозиторий tooyour установщика hello и просто вызвать\_установить посредством передачи toohello путь hello исполняемый.</span><span class="sxs-lookup"><span data-stu-id="dd647-127">Add hello installer tooyour repository, and invoke easy\_install by passing hello path toohello executable.</span></span>

<span data-ttu-id="dd647-128">Добавьте этот сценарий развертывания toohello:</span><span class="sxs-lookup"><span data-stu-id="dd647-128">Add this toohello deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a><span data-ttu-id="dd647-129">Включить hello виртуальной среды в репозиторий hello (необходима операционная система Windows)</span><span class="sxs-lookup"><span data-stu-id="dd647-129">Include hello virtual environment in hello repository (requires Windows)</span></span>
<span data-ttu-id="dd647-130">Примечание: При использовании этого параметра, убедитесь, что toouse виртуальную среду, которая соответствует hello/архитектура и версии платформы, используемой на веб-приложения hello в службе приложений Azure (Windows/32-bit/2.7 или 3.4).</span><span class="sxs-lookup"><span data-stu-id="dd647-130">Note: When using this option, make sure toouse a virtual environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="dd647-131">При включении виртуальной среды hello в репозитории hello можно предотвратить скрипт развертывания hello выполнив управления виртуальной среды в Azure, создав пустой файл:</span><span class="sxs-lookup"><span data-stu-id="dd647-131">If you include hello virtual environment in hello repository, you can prevent hello deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="dd647-132">Рекомендуется удалять hello существующую виртуальную среду на приложение hello, оставшиеся файлы tooprevent из при автоматически управляет hello виртуальной среды.</span><span class="sxs-lookup"><span data-stu-id="dd647-132">We recommend that you delete hello existing virtual environment on hello app, tooprevent leftover files from when hello virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
