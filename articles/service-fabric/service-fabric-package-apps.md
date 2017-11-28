---
title: "приложение Azure Service Fabric aaaPackage | Документы Microsoft"
description: "Как toopackage приложения перед развертыванием tooa кластера Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a><span data-ttu-id="9b95b-103">Создание пакета приложения</span><span class="sxs-lookup"><span data-stu-id="9b95b-103">Package an application</span></span>
<span data-ttu-id="9b95b-104">В этой статье описывается как toopackage приложения Service Fabric и подготовить ее для развертывания.</span><span class="sxs-lookup"><span data-stu-id="9b95b-104">This article describes how toopackage a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="9b95b-105">Макет пакета</span><span class="sxs-lookup"><span data-stu-id="9b95b-105">Package layout</span></span>
<span data-ttu-id="9b95b-106">манифест приложения Hello, один или несколько манифесты службы и другие необходимые пакеты, файлы могут быть организованы в определенном макете для развертывания в кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b95b-106">hello application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="9b95b-107">манифесты пример Hello в этой статье, потребуется toobe организованы в hello следующая структура каталогов:</span><span class="sxs-lookup"><span data-stu-id="9b95b-107">hello example manifests in this article would need toobe organized in hello following directory structure:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

<span data-ttu-id="9b95b-108">Hello папки с именами toomatch hello **имя** атрибуты каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="9b95b-108">hello folders are named toomatch hello **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="9b95b-109">Например, если hello манифест службы содержится два пакета кода с именами hello **MyCodeA** и **MyCodeB**, а затем две папки с одноименными будет содержать hello hello необходимые двоичные файлы для каждого кода пакет.</span><span class="sxs-lookup"><span data-stu-id="9b95b-109">For example, if hello service manifest contained two code packages with hello names **MyCodeA** and **MyCodeB**, then two folders with hello same names would contain hello necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="9b95b-110">Использование SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="9b95b-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="9b95b-111">Типичные сценарии использования **SetupEntryPoint** составляют случаи, когда требуется toorun исполняемый файл до запуска службы hello или требуется tooperform операции с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="9b95b-111">Typical scenarios for using **SetupEntryPoint** are when you need toorun an executable before hello service starts or you need tooperform an operation with elevated privileges.</span></span> <span data-ttu-id="9b95b-112">Например:</span><span class="sxs-lookup"><span data-stu-id="9b95b-112">For example:</span></span>

* <span data-ttu-id="9b95b-113">Настройка и инициализация переменных среды, которые hello исполняемый требованиям службы.</span><span class="sxs-lookup"><span data-stu-id="9b95b-113">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="9b95b-114">Это не исполняемые файлы ограниченный tooonly записано с помощью модели программирования hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b95b-114">It is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="9b95b-115">Например, npm.exe нужны определенные переменные среды, настроенные для развертывания приложения node.js.</span><span class="sxs-lookup"><span data-stu-id="9b95b-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="9b95b-116">Настройка контроля доступа посредством установки сертификатов безопасности.</span><span class="sxs-lookup"><span data-stu-id="9b95b-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="9b95b-117">Дополнительные сведения о том, как tooconfigure hello **SetupEntryPoint**, в разделе [настройки hello политики для точки входа установки службы](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="9b95b-117">For more information on how tooconfigure hello **SetupEntryPoint**, see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="9b95b-118">Настройка</span><span class="sxs-lookup"><span data-stu-id="9b95b-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="9b95b-119">Создание пакета с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9b95b-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="9b95b-120">Если вы используете Visual Studio 2015 toocreate приложения, можно использовать hello пакета tooautomatically команда создания пакета, который соответствует hello макета, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="9b95b-120">If you use Visual Studio 2015 toocreate your application, you can use hello Package command tooautomatically create a package that matches hello layout described above.</span></span>

<span data-ttu-id="9b95b-121">toocreate пакета, щелкните правой кнопкой мыши проект приложения hello в обозревателе решений и выберите команду пакет hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="9b95b-121">toocreate a package, right-click hello application project in Solution Explorer and choose hello Package command, as shown below:</span></span>

![Создание пакета приложения с помощью Visual Studio][vs-package-command]

<span data-ttu-id="9b95b-123">После завершения упаковки hello расположение hello пакета можно найти в hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="9b95b-123">When packaging is complete, you can find hello location of hello package in hello **Output** window.</span></span> <span data-ttu-id="9b95b-124">Привет упаковкой шаг выполняется автоматически при выполнении развертывания или отладки приложения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b95b-124">hello packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="9b95b-125">Создание пакета с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="9b95b-125">Build a package by command line</span></span>
<span data-ttu-id="9b95b-126">Это также возможно tooprogrammatically пакета приложения с помощью `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="9b95b-126">It is also possible tooprogrammatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="9b95b-127">Кулисами hello, Visual Studio выполняется его так же hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9b95b-127">Under hello hood, Visual Studio is running it so hello output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a><span data-ttu-id="9b95b-128">Тестовый пакет hello</span><span class="sxs-lookup"><span data-stu-id="9b95b-128">Test hello package</span></span>
<span data-ttu-id="9b95b-129">Структура пакета hello локально с помощью PowerShell можно проверить с помощью hello [ServiceFabricApplicationPackage тест](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) команды.</span><span class="sxs-lookup"><span data-stu-id="9b95b-129">You can verify hello package structure locally through PowerShell by using hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="9b95b-130">Эта команда проверит манифест на наличие ошибок при анализе, а также все ссылки.</span><span class="sxs-lookup"><span data-stu-id="9b95b-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="9b95b-131">Эта команда проверяет только правильность структурных hello hello каталогов и файлов в пакете hello.</span><span class="sxs-lookup"><span data-stu-id="9b95b-131">This command only verifies hello structural correctness of hello directories and files in hello package.</span></span>
<span data-ttu-id="9b95b-132">Он не проверяет любые hello кода или данных содержимое пакета после проверки того, что имеются все необходимые файлы.</span><span class="sxs-lookup"><span data-stu-id="9b95b-132">It doesn't verify any of hello code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="9b95b-133">Эта ошибка показывает, что hello *MySetup.bat* файла, на который ссылается манифест службы hello **SetupEntryPoint** отсутствует пакет кода hello.</span><span class="sxs-lookup"><span data-stu-id="9b95b-133">This error shows that hello *MySetup.bat* file referenced in hello service manifest **SetupEntryPoint** is missing from hello code package.</span></span> <span data-ttu-id="9b95b-134">После добавления отсутствующего файла hello проверки приложения hello проходит успешно:</span><span class="sxs-lookup"><span data-stu-id="9b95b-134">After hello missing file is added, hello application verification passes:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

<span data-ttu-id="9b95b-135">Если для приложения определены [параметры приложения](service-fabric-manage-multiple-environment-app-configuration.md), их можно передать в командлет [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) для полной проверки.</span><span class="sxs-lookup"><span data-stu-id="9b95b-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="9b95b-136">Если вы знаете hello кластера, где будут развертываться приложения hello, рекомендуется передать hello `ImageStoreConnectionString` параметра.</span><span class="sxs-lookup"><span data-stu-id="9b95b-136">If you know hello cluster where hello application will be deployed, it is recommended you pass in hello `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="9b95b-137">В этом случае пакет hello также проверяется с использованием предыдущих версий приложения hello, которые уже запущены в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="9b95b-137">In this case, hello package is also validated against previous versions of hello application that are already running in hello cluster.</span></span> <span data-ttu-id="9b95b-138">Например, можно обнаружить проверки hello ли пакет с hello же версии, но различное содержимое уже был развернут.</span><span class="sxs-lookup"><span data-stu-id="9b95b-138">For example, hello validation can detect whether a package with hello same version but different content was already deployed.</span></span>  

<span data-ttu-id="9b95b-139">Как только приложение hello упакован должным образом и проходит проверку, оценки на основе размера hello и hello число файлов, при необходимости сжатия.</span><span class="sxs-lookup"><span data-stu-id="9b95b-139">Once hello application is packaged correctly and passes validation, evaluate based on hello size and hello number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="9b95b-140">Сжатие пакета</span><span class="sxs-lookup"><span data-stu-id="9b95b-140">Compress a package</span></span>
<span data-ttu-id="9b95b-141">Если пакет содержит большое число файлов или имеет большой размер, можно выполнить сжатие пакета для более быстрого развертывания.</span><span class="sxs-lookup"><span data-stu-id="9b95b-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="9b95b-142">Сжатие уменьшает число файлов и размер пакета hello hello.</span><span class="sxs-lookup"><span data-stu-id="9b95b-142">Compression reduces hello number of files and hello package size.</span></span>
<span data-ttu-id="9b95b-143">Для пакета приложений сжатые [передача пакета приложения hello](service-fabric-deploy-remove-applications.md#upload-the-application-package) может занять больше по сравнению toouploading hello несжатый пакет (специально сжатия времени с учетом), но [регистрации](service-fabric-deploy-remove-applications.md#register-the-application-package) и [Отмена регистрации типа приложения hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) работают быстрее для пакета сжатых приложений.</span><span class="sxs-lookup"><span data-stu-id="9b95b-143">For a compressed application package, [Uploading hello application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared toouploading hello uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering hello application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="9b95b-144">механизм развертывания Hello же сжатые и несжатые пакетов.</span><span class="sxs-lookup"><span data-stu-id="9b95b-144">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="9b95b-145">Если пакет hello сжаты, таким образом сохраняется в хранилище образов кластера hello и сжимаются на узле hello перед запуском приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9b95b-145">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>
<span data-ttu-id="9b95b-146">Сжатие Hello hello сжатая версия заменяет hello допустимый пакет Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b95b-146">hello compression replaces hello valid Service Fabric package with hello compressed version.</span></span> <span data-ttu-id="9b95b-147">Папка Hello должны разрешать разрешения на запись.</span><span class="sxs-lookup"><span data-stu-id="9b95b-147">hello folder must allow write permissions.</span></span> <span data-ttu-id="9b95b-148">Если выполнить сжатие для уже сжатого пакета, никаких изменений не происходит.</span><span class="sxs-lookup"><span data-stu-id="9b95b-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="9b95b-149">Пакет можно сжать, выполнив команду Powershell hello [копирования ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) с `CompressPackage` переключения.</span><span class="sxs-lookup"><span data-stu-id="9b95b-149">You can compress a package by running hello Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="9b95b-150">Можно распаковать hello пакета с hello же с помощью `UncompressPackage` переключения.</span><span class="sxs-lookup"><span data-stu-id="9b95b-150">You can uncompress hello package with hello same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="9b95b-151">Hello следующая команда сжимает hello пакета, не копируя его toohello хранилище образов.</span><span class="sxs-lookup"><span data-stu-id="9b95b-151">hello following command compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="9b95b-152">Можно скопировать tooone сжатый пакет или несколько кластеров Service Fabric, при необходимости, с помощью [копирования ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) без hello `SkipCopy` флаг.</span><span class="sxs-lookup"><span data-stu-id="9b95b-152">You can copy a compressed package tooone or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without hello `SkipCopy` flag.</span></span>
<span data-ttu-id="9b95b-153">Hello пакет теперь содержит ZIP-файл для hello `code`, `config`, и `data` пакетов.</span><span class="sxs-lookup"><span data-stu-id="9b95b-153">hello package now includes zipped files for hello `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="9b95b-154">манифест приложения Hello и манифесты hello не ZIP-, так как они требуются для многих внутренних операций (например, пакет управления доступом приложения имя и версия извлечения типа для определенных проверок).</span><span class="sxs-lookup"><span data-stu-id="9b95b-154">hello application manifest and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="9b95b-155">Архивировать манифесты hello сделает эти операции неэффективно.</span><span class="sxs-lookup"><span data-stu-id="9b95b-155">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

<span data-ttu-id="9b95b-156">Кроме того, можно сжимать и скопировать hello пакет с [ServiceFabricApplicationPackage копирования](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) за один шаг.</span><span class="sxs-lookup"><span data-stu-id="9b95b-156">Alternatively, you can compress and copy hello package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="9b95b-157">Если hello пакет имеет большой размер, укажите время tooallow достаточно высокое время ожидания для сжатия пакета hello и hello передачи toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="9b95b-157">If hello package is large, provide a high enough timeout tooallow time for both hello package compression and hello upload toohello cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="9b95b-158">На внутреннем уровне Service Fabric вычисляет контрольные суммы для hello пакетов приложений для проверки.</span><span class="sxs-lookup"><span data-stu-id="9b95b-158">Internally, Service Fabric computes checksums for hello application packages for validation.</span></span> <span data-ttu-id="9b95b-159">При использовании сжатия, hello контрольные суммы вычисляются на hello ZIP-версии каждого пакета.</span><span class="sxs-lookup"><span data-stu-id="9b95b-159">When using compression, hello checksums are computed on hello zipped versions of each package.</span></span>
<span data-ttu-id="9b95b-160">Если вы скопировали несжатую версию пакета приложения, и требуется toouse сжатия для hello того же пакета, необходимо изменить hello версий hello `code`, `config`, и `data` пакеты tooavoid ошибка контрольной суммы.</span><span class="sxs-lookup"><span data-stu-id="9b95b-160">If you copied an uncompressed version of your application package, and you want toouse compression for hello same package, you must change hello versions of hello `code`, `config`, and `data` packages tooavoid checksum mismatch.</span></span> <span data-ttu-id="9b95b-161">Если пакеты hello не меняются, вместо изменения версии hello, можно использовать [подготовки diff](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="9b95b-161">If hello packages are unchanged, instead of changing hello version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="9b95b-162">Этот параметр, не включайте hello без изменения пакета вместо ссылок на него манифест службы hello.</span><span class="sxs-lookup"><span data-stu-id="9b95b-162">With this option, do not include hello unchanged package instead reference it from hello service manifest.</span></span>

<span data-ttu-id="9b95b-163">Аналогичным образом Если вы отправили сжатая версия пакета hello и требуется toouse пакет без сжатия, необходимо обновить hello версии tooavoid hello ошибка контрольной суммы.</span><span class="sxs-lookup"><span data-stu-id="9b95b-163">Similarly, if you uploaded a compressed version of hello package and you want toouse an uncompressed package, you must update hello versions tooavoid hello checksum mismatch.</span></span>

<span data-ttu-id="9b95b-164">Hello пакет теперь упакованные правильно, проверяется и сжатые (при необходимости), поэтому она не готова для [развертывания](service-fabric-deploy-remove-applications.md) tooone или дополнительные Service Fabric кластерах.</span><span class="sxs-lookup"><span data-stu-id="9b95b-164">hello package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) tooone or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="9b95b-165">Сжатие пакетов при развертывании с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9b95b-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="9b95b-166">Пакеты toocompress Visual Studio для развертывания, можно настроить путем добавления hello `CopyPackageParameters` tooyour элемент профиль публикации, задайте hello `CompressPackage` атрибут слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="9b95b-166">You can instruct Visual Studio toocompress packages on deployment, by adding hello `CopyPackageParameters` element tooyour publish profile, and set hello `CompressPackage` attribute too`true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="9b95b-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9b95b-167">Next steps</span></span>
<span data-ttu-id="9b95b-168">[Развертывание и удаление приложений] [ 10] описывает как экземпляры приложения toomanage toouse PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b95b-168">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances</span></span>

<span data-ttu-id="9b95b-169">[Управление параметрами приложения для нескольких сред] [ 11] описывает способ tooconfigure параметров и переменных среды для экземпляров другого приложения.</span><span class="sxs-lookup"><span data-stu-id="9b95b-169">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="9b95b-170">[Настройка политик безопасности для приложения] [ 12] описывает, каким образом службы toorun toorestrict политики безопасности доступа.</span><span class="sxs-lookup"><span data-stu-id="9b95b-170">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
