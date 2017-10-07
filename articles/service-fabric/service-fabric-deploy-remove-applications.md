---
title: "развертывание приложения Service Fabric aaaAzure | Документы Microsoft"
description: "Как toodeploy и удаление приложений в Service Fabric, с помощью PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="099e5-103">Развертывание и удаление приложений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="099e5-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="099e5-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="099e5-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="099e5-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="099e5-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="099e5-106">API-интерфейсы FabricClient</span><span class="sxs-lookup"><span data-stu-id="099e5-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="099e5-107">После [создания пакета приложения][10] его можно развернуть в кластере Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="099e5-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="099e5-108">Развертывание включает hello следующие три шага:</span><span class="sxs-lookup"><span data-stu-id="099e5-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="099e5-109">Отправка хранилища образов toohello пакета приложения hello</span><span class="sxs-lookup"><span data-stu-id="099e5-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="099e5-110">Регистрация типа приложения hello</span><span class="sxs-lookup"><span data-stu-id="099e5-110">Register hello application type</span></span>
3. <span data-ttu-id="099e5-111">Создание экземпляра приложения hello</span><span class="sxs-lookup"><span data-stu-id="099e5-111">Create hello application instance</span></span>

<span data-ttu-id="099e5-112">После развертывания приложения и экземпляр работает в кластере hello, можно удалить экземпляр приложения hello и его тип приложения.</span><span class="sxs-lookup"><span data-stu-id="099e5-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="099e5-113">Удаление toocompletely приложение из кластера hello включает в себя hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="099e5-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="099e5-114">Удалить (или) запущен экземпляр приложения hello</span><span class="sxs-lookup"><span data-stu-id="099e5-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="099e5-115">Отмена регистрации типа приложения hello, если оно больше не требуется</span><span class="sxs-lookup"><span data-stu-id="099e5-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="099e5-116">Удаление пакета приложения hello из хранилища образов hello</span><span class="sxs-lookup"><span data-stu-id="099e5-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="099e5-117">Если вы используете [Visual Studio для развертывания и отладки приложений](service-fabric-publish-app-remote-cluster.md) в кластере локальной разработки все hello описанные выше шаги автоматически обрабатываются с помощью сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="099e5-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="099e5-118">Этот скрипт находится в hello *сценариев* папку проекта приложения hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="099e5-119">В этой статье приведены фона действиями этот скрипт, чтобы можно было выполнять hello и те же операции вне Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="099e5-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="099e5-120">Подключите кластер toohello</span><span class="sxs-lookup"><span data-stu-id="099e5-120">Connect toohello cluster</span></span>
<span data-ttu-id="099e5-121">Перед выполнением любых команд PowerShell в этой статье, всегда начинаются с помощью [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) кластера Service Fabric toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="099e5-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric cluster.</span></span> <span data-ttu-id="099e5-122">tooconnect toohello локальному кластеру разработки, выполните hello ниже:</span><span class="sxs-lookup"><span data-stu-id="099e5-122">tooconnect toohello local development cluster, run hello following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="099e5-123">Примеры соединения tooa удаленного кластера или кластера, защищенные с помощью Azure Active Directory, X509 сертификаты или Windows Active Directory см. в разделе [кластера безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="099e5-123">For examples of connecting tooa remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-hello-application-package"></a><span data-ttu-id="099e5-124">Отправить пакет приложения hello</span><span class="sxs-lookup"><span data-stu-id="099e5-124">Upload hello application package</span></span>
<span data-ttu-id="099e5-125">Отправка пакета приложения hello помещает его в расположении, доступном из внутренних компонентов Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="099e5-125">Uploading hello application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="099e5-126">Пакет приложения hello tooverify локально, используйте hello [ServiceFabricApplicationPackage тест](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="099e5-126">If you want tooverify hello application package locally, use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="099e5-127">Hello [ServiceFabricApplicationPackage копирования](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) команда передачи hello хранилище образов кластера toohello пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="099e5-127">hello [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads hello application package toohello cluster image store.</span></span>
<span data-ttu-id="099e5-128">Hello **Get ImageStoreConnectionStringFromClusterManifest** , который является частью модуля Service Fabric SDK PowerShell hello, — используется tooget hello изображение хранение строки подключения.</span><span class="sxs-lookup"><span data-stu-id="099e5-128">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="099e5-129">hello SDK tooimport модуль, запустите:</span><span class="sxs-lookup"><span data-stu-id="099e5-129">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="099e5-130">Предположим, вы собрали и упаковали в Visual Studio 2015 приложение с именем *MyApplication*.</span><span class="sxs-lookup"><span data-stu-id="099e5-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="099e5-131">По умолчанию имя типа приложения hello, перечисленные в hello ApplicationManifest.xml является «MyApplicationType».</span><span class="sxs-lookup"><span data-stu-id="099e5-131">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="099e5-132">Hello пакет приложения, который содержит манифест необходимые приложения hello, манифесты и пакеты кода/config/данные, находится в *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="099e5-132">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="099e5-133">Hello следующая команда перечисляет hello содержимого пакета приложения hello:</span><span class="sxs-lookup"><span data-stu-id="099e5-133">hello following command lists hello contents of hello application package:</span></span>

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

<span data-ttu-id="099e5-134">Если пакет приложения hello большой или имеет большое количество файлов, вы можете [Сжать](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="099e5-134">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="099e5-135">Hello сжатие приводит к уменьшению размера hello и hello количеством файлов.</span><span class="sxs-lookup"><span data-stu-id="099e5-135">hello compression reduces hello size and hello number of files.</span></span>
<span data-ttu-id="099e5-136">Hello побочным эффектом является hello, регистрация и Отмена регистрации типа приложения работают быстрее.</span><span class="sxs-lookup"><span data-stu-id="099e5-136">hello side effect is that registering and un-registering hello application type are faster.</span></span> <span data-ttu-id="099e5-137">Время передачи могут работать медленнее в настоящее время, особенно в том случае, если включен пакет hello toocompress времени hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-137">Upload time may be slower currently, especially if you include hello time toocompress hello package.</span></span> 

<span data-ttu-id="099e5-138">пакет, используйте toocompress hello же [ServiceFabricApplicationPackage копирования](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) команды.</span><span class="sxs-lookup"><span data-stu-id="099e5-138">toocompress a package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="099e5-139">Сжатие может выполняться отдельно в передаче, с помощью hello `SkipCopy` флаг или вместе с hello операции передачи.</span><span class="sxs-lookup"><span data-stu-id="099e5-139">Compression can be done separate from upload, by using hello `SkipCopy` flag, or together with hello upload operation.</span></span> <span data-ttu-id="099e5-140">Применить сжатие к сжатому пакету невозможно.</span><span class="sxs-lookup"><span data-stu-id="099e5-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="099e5-141">toouncompress сжатый пакет, используйте hello же [копирования ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) с hello `UncompressPackage` переключения.</span><span class="sxs-lookup"><span data-stu-id="099e5-141">toouncompress a compressed package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with hello `UncompressPackage` switch.</span></span>

<span data-ttu-id="099e5-142">Hello следующий командлет сжимает hello пакета, не копируя его toohello хранилища образов.</span><span class="sxs-lookup"><span data-stu-id="099e5-142">hello following cmdlet compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="099e5-143">Hello пакет теперь содержит ZIP-файл для hello `Code` и `Config` пакетов.</span><span class="sxs-lookup"><span data-stu-id="099e5-143">hello package now includes zipped files for hello `Code` and `Config` packages.</span></span> <span data-ttu-id="099e5-144">манифесты службы hello приложения Hello и являются не ZIP-, так как они требуются для многих внутренних операций (например, пакет управления доступом приложения имя и версия извлечения типа для определенных проверок).</span><span class="sxs-lookup"><span data-stu-id="099e5-144">hello application and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="099e5-145">Архивировать манифесты hello сделает эти операции неэффективно.</span><span class="sxs-lookup"><span data-stu-id="099e5-145">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

<span data-ttu-id="099e5-146">Для больших пакетов приложений hello сжатие экономит время.</span><span class="sxs-lookup"><span data-stu-id="099e5-146">For large application packages, hello compression takes time.</span></span> <span data-ttu-id="099e5-147">Для получения наилучших результатов используйте быстрый SSD-диск.</span><span class="sxs-lookup"><span data-stu-id="099e5-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="099e5-148">время сжатия Hello и hello размер сжатого пакета hello также зависят от содержимого пакета hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-148">hello compression times and hello size of hello compressed package also differ based on hello package content.</span></span>
<span data-ttu-id="099e5-149">Например вот сжатия статистики для некоторых пакетов, в которых Показать начальной hello и hello размер сжатого пакета с временем сжатия hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-149">For example, here is compression statistics for some packages, which show hello initial and hello compressed package size, with hello compression time.</span></span>

|<span data-ttu-id="099e5-150">Исходный размер (МБ)</span><span class="sxs-lookup"><span data-stu-id="099e5-150">Initial size (MB)</span></span>|<span data-ttu-id="099e5-151">Число файлов</span><span class="sxs-lookup"><span data-stu-id="099e5-151">File count</span></span>|<span data-ttu-id="099e5-152">Время сжатия</span><span class="sxs-lookup"><span data-stu-id="099e5-152">Compression Time</span></span>|<span data-ttu-id="099e5-153">Размер сжатого пакета (МБ)</span><span class="sxs-lookup"><span data-stu-id="099e5-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="099e5-154">100</span><span class="sxs-lookup"><span data-stu-id="099e5-154">100</span></span>|<span data-ttu-id="099e5-155">100</span><span class="sxs-lookup"><span data-stu-id="099e5-155">100</span></span>|<span data-ttu-id="099e5-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="099e5-156">00:00:03.3547592</span></span>|<span data-ttu-id="099e5-157">60</span><span class="sxs-lookup"><span data-stu-id="099e5-157">60</span></span>|
|<span data-ttu-id="099e5-158">512</span><span class="sxs-lookup"><span data-stu-id="099e5-158">512</span></span>|<span data-ttu-id="099e5-159">100</span><span class="sxs-lookup"><span data-stu-id="099e5-159">100</span></span>|<span data-ttu-id="099e5-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="099e5-160">00:00:16.3850303</span></span>|<span data-ttu-id="099e5-161">307</span><span class="sxs-lookup"><span data-stu-id="099e5-161">307</span></span>|
|<span data-ttu-id="099e5-162">1024</span><span class="sxs-lookup"><span data-stu-id="099e5-162">1024</span></span>|<span data-ttu-id="099e5-163">500</span><span class="sxs-lookup"><span data-stu-id="099e5-163">500</span></span>|<span data-ttu-id="099e5-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="099e5-164">00:00:32.5907950</span></span>|<span data-ttu-id="099e5-165">615</span><span class="sxs-lookup"><span data-stu-id="099e5-165">615</span></span>|
|<span data-ttu-id="099e5-166">2048</span><span class="sxs-lookup"><span data-stu-id="099e5-166">2048</span></span>|<span data-ttu-id="099e5-167">1000</span><span class="sxs-lookup"><span data-stu-id="099e5-167">1000</span></span>|<span data-ttu-id="099e5-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="099e5-168">00:01:04.3775554</span></span>|<span data-ttu-id="099e5-169">1231</span><span class="sxs-lookup"><span data-stu-id="099e5-169">1231</span></span>|
|<span data-ttu-id="099e5-170">5012</span><span class="sxs-lookup"><span data-stu-id="099e5-170">5012</span></span>|<span data-ttu-id="099e5-171">100</span><span class="sxs-lookup"><span data-stu-id="099e5-171">100</span></span>|<span data-ttu-id="099e5-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="099e5-172">00:02:45.2951288</span></span>|<span data-ttu-id="099e5-173">3074</span><span class="sxs-lookup"><span data-stu-id="099e5-173">3074</span></span>|

<span data-ttu-id="099e5-174">После сжатия пакета может быть загруженного tooone или несколько Service Fabric кластеров при необходимости.</span><span class="sxs-lookup"><span data-stu-id="099e5-174">Once a package is compressed, it can be uploaded tooone or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="099e5-175">механизм развертывания Hello же сжатые и несжатые пакетов.</span><span class="sxs-lookup"><span data-stu-id="099e5-175">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="099e5-176">Если пакет hello сжаты, таким образом сохраняется в хранилище образов кластера hello и сжимаются на узле hello перед запуском приложения hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-176">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>


<span data-ttu-id="099e5-177">Hello следующий пример передает hello хранилища образов toohello пакета, в папку с именем «MyApplicationV1»:</span><span class="sxs-lookup"><span data-stu-id="099e5-177">hello following example uploads hello package toohello image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="099e5-178">Hello **Get ImageStoreConnectionStringFromClusterManifest** , который является частью модуля Service Fabric SDK PowerShell hello, — используется tooget hello изображение хранение строки подключения.</span><span class="sxs-lookup"><span data-stu-id="099e5-178">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="099e5-179">hello SDK tooimport модуль, запустите:</span><span class="sxs-lookup"><span data-stu-id="099e5-179">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="099e5-180">Если вы не укажете hello *- ApplicationPackagePathInImageStore* параметров пакета приложения hello копируется в папку «Debug» hello в хранилище образов hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-180">If you do not specify hello *-ApplicationPackagePathInImageStore* parameter, hello application package is copied into hello "Debug" folder in hello image store.</span></span>

<span data-ttu-id="099e5-181">Hello время, затрачиваемое tooupload пакета зависит от нескольких факторов.</span><span class="sxs-lookup"><span data-stu-id="099e5-181">hello time it takes tooupload a package differs depending on multiple factors.</span></span> <span data-ttu-id="099e5-182">Некоторые из этих факторов, hello число файлов в пакет hello, размер пакета hello и размеры файлов hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-182">Some of these factors are hello number of files in hello package, hello package size, and hello file sizes.</span></span> <span data-ttu-id="099e5-183">Hello скорость сетевого подключения между исходным компьютером hello и кластер Service Fabric hello также влияет на время передачи hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-183">hello network speed between hello source machine and hello Service Fabric cluster also impacts hello upload time.</span></span> <span data-ttu-id="099e5-184">Здравствуйте, время ожидания по умолчанию для [ServiceFabricApplicationPackage копирования](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) составляет 30 минут.</span><span class="sxs-lookup"><span data-stu-id="099e5-184">hello default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="099e5-185">В зависимости от Здравствуйте описываются факторы, возможно, время ожидания tooincrease hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-185">Depending on hello described factors, you may have tooincrease hello timeout.</span></span> <span data-ttu-id="099e5-186">При сжатии пакета hello в вызове hello копирования необходимо tooalso рассмотрим hello время сжатия.</span><span class="sxs-lookup"><span data-stu-id="099e5-186">If you are compressing hello package in hello copy call, you need tooalso consider hello compression time.</span></span>

<span data-ttu-id="099e5-187">В разделе [понять строка подключения хранилища изображения hello](service-fabric-image-store-connection-string.md) Дополнительные сведения о хранилище образов hello и image хранение строки подключения.</span><span class="sxs-lookup"><span data-stu-id="099e5-187">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="099e5-188">Регистрация пакета приложения hello</span><span class="sxs-lookup"><span data-stu-id="099e5-188">Register hello application package</span></span>
<span data-ttu-id="099e5-189">Тип приложения Hello и версии, объявленные в манифесте приложения hello, становятся доступны для использования при регистрации пакета приложения hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-189">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="099e5-190">Hello система считывает переданный на предыдущем шаге hello пакет hello, проверяет пакет hello, обрабатывает содержимое пакета hello и копирует расположение внутреннего системного tooan hello обработки пакета.</span><span class="sxs-lookup"><span data-stu-id="099e5-190">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="099e5-191">Запустите hello [ServiceFabricApplicationType регистра](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) tooregister командлет hello типа приложения в кластере hello и сделать его доступным для развертывания:</span><span class="sxs-lookup"><span data-stu-id="099e5-191">Run hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello application type in hello cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="099e5-192">«MyApplicationV1» является папкой hello в хранилище образов hello, где находится пакет приложения hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-192">"MyApplicationV1" is hello folder in hello image store where hello application package is located.</span></span> <span data-ttu-id="099e5-193">Тип приложения Hello с именем «MyApplicationType» и версией «1.0.0» (оба находятся в манифесте приложения hello) зарегистрирован в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-193">hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) is now registered in hello cluster.</span></span>

<span data-ttu-id="099e5-194">Hello [ServiceFabricApplicationType регистра](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) команда возвращает только после hello система имеет пакет приложения успешно зарегистрирован hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-194">hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after hello system has successfully registered hello application package.</span></span> <span data-ttu-id="099e5-195">Как долго принимает регистрации зависит от размера hello и содержимого пакета приложения hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-195">How long registration takes depends on hello size and contents of hello application package.</span></span> <span data-ttu-id="099e5-196">При необходимости hello **- TimeoutSec** параметр можно использовать toosupply более длительного времени ожидания (hello время ожидания по умолчанию — 60 секунд).</span><span class="sxs-lookup"><span data-stu-id="099e5-196">If needed, hello **-TimeoutSec** parameter can be used toosupply a longer timeout (hello default timeout is 60 seconds).</span></span>

<span data-ttu-id="099e5-197">При наличии большого приложения пакета или при возникновении тайм-ауты использовать hello **- Async** параметра.</span><span class="sxs-lookup"><span data-stu-id="099e5-197">If you have a large application package or if you are experiencing timeouts, use hello **-Async** parameter.</span></span> <span data-ttu-id="099e5-198">Команда Hello возвращает hello кластера принимает команды hello регистрации и обработки hello продолжается при необходимости.</span><span class="sxs-lookup"><span data-stu-id="099e5-198">hello command returns when hello cluster accepts hello register command, and hello processing continues as needed.</span></span>
<span data-ttu-id="099e5-199">Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) команда выводит список всех версий типа успешно зарегистрированного приложения и состояние их регистрации.</span><span class="sxs-lookup"><span data-stu-id="099e5-199">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="099e5-200">После завершения регистрации hello toodetermine этой команды можно использовать.</span><span class="sxs-lookup"><span data-stu-id="099e5-200">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a><span data-ttu-id="099e5-201">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="099e5-201">Create hello application</span></span>
<span data-ttu-id="099e5-202">Можно создать приложение с любой версии типа приложения, который успешно зарегистрирован с помощью hello [New ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="099e5-202">You can instantiate an application from any application type version that has been registered successfully by using hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="099e5-203">Имя каждого приложения Hello должно начинаться с hello *«fabric: «* схему и должны быть уникальными для каждого экземпляра приложения.</span><span class="sxs-lookup"><span data-stu-id="099e5-203">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="099e5-204">Также создаются все службы по умолчанию, определенных в манифесте приложения hello объекта тип целевого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-204">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="099e5-205">Для каждой версии зарегистрированного типа приложения можно создать несколько экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="099e5-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="099e5-206">Каждый экземпляр выполняется изолированно, используя собственный рабочий каталог и процесс.</span><span class="sxs-lookup"><span data-stu-id="099e5-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="099e5-207">toosee имени приложения и службы работают в кластере hello, запустите hello [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) и [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) командлетов:</span><span class="sxs-lookup"><span data-stu-id="099e5-207">toosee which named apps and services are running in hello cluster, run hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a><span data-ttu-id="099e5-208">Удаление приложения</span><span class="sxs-lookup"><span data-stu-id="099e5-208">Remove an application</span></span>
<span data-ttu-id="099e5-209">При экземпляр приложения больше не нужен, можно окончательно удалить его по имени, используя hello [ServiceFabricApplication удаление](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="099e5-209">When an application instance is no longer needed, you can permanently remove it by name using hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="099e5-210">[Удаление ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) автоматически удаляет все службы, которые принадлежат toohello приложения также, без возможности восстановления, удаляя все состояния службы.</span><span class="sxs-lookup"><span data-stu-id="099e5-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="099e5-211">Эта операция необратима, и вы не сможете восстановить состояние приложения.</span><span class="sxs-lookup"><span data-stu-id="099e5-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="099e5-212">Отмена регистрации типа приложения</span><span class="sxs-lookup"><span data-stu-id="099e5-212">Unregister an application type</span></span>
<span data-ttu-id="099e5-213">При определенной версии типа приложения больше не нужен, необходимо отменить регистрацию с помощью hello тип приложения hello [Unregister ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="099e5-213">When a particular version of an application type is no longer needed, you should unregister hello application type using hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="099e5-214">Отмена регистрации неиспользуемые приложения типы выпуски пространства, используемого хранилища образов hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-214">Unregistering unused application types releases storage space used by hello image store.</span></span> <span data-ttu-id="099e5-215">Регистрацию типа приложения можно отменить в том случае, если на его основе не были созданы экземпляры приложений и нет ссылающихся на него незавершенных обновлений приложений.</span><span class="sxs-lookup"><span data-stu-id="099e5-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="099e5-216">Запустите [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) типы приложения hello toosee в настоящее время зарегистрированы в кластере hello:</span><span class="sxs-lookup"><span data-stu-id="099e5-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello application types currently registered in hello cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="099e5-217">Запустите [Unregister ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister приложения определенного типа:</span><span class="sxs-lookup"><span data-stu-id="099e5-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="099e5-218">Удаление пакета приложения из хранилища образов hello</span><span class="sxs-lookup"><span data-stu-id="099e5-218">Remove an application package from hello image store</span></span>
<span data-ttu-id="099e5-219">Если пакета приложения больше не нужен, его можно удалить из hello образа хранилища toofree системные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="099e5-219">When an application package is no longer needed, you can delete it from hello image store toofree up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="099e5-220">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="099e5-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="099e5-221">Команда Copy-ServiceFabricApplicationPackage запрашивает строку ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="099e5-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="099e5-222">пакет Service Fabric SDK среды Hello должна уже иметь hello правильно настроить значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="099e5-222">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="099e5-223">Но при необходимости hello строка ImageStoreConnectionString для всех команд должны соответствует значению hello, hello кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="099e5-223">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="099e5-224">Hello строка ImageStoreConnectionString можно найти в манифесте кластера hello, полученные при помощи hello [Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) и Get-ImageStoreConnectionStringFromClusterManifest команды:</span><span class="sxs-lookup"><span data-stu-id="099e5-224">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="099e5-225">Hello **Get ImageStoreConnectionStringFromClusterManifest** , который является частью модуля Service Fabric SDK PowerShell hello, — используется tooget hello изображение хранение строки подключения.</span><span class="sxs-lookup"><span data-stu-id="099e5-225">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="099e5-226">hello SDK tooimport модуль, запустите:</span><span class="sxs-lookup"><span data-stu-id="099e5-226">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="099e5-227">Строка ImageStoreConnectionString Hello можно найти в манифесте кластера hello:</span><span class="sxs-lookup"><span data-stu-id="099e5-227">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="099e5-228">В разделе [понять строка подключения хранилища изображения hello](service-fabric-image-store-connection-string.md) Дополнительные сведения о хранилище образов hello и image хранение строки подключения.</span><span class="sxs-lookup"><span data-stu-id="099e5-228">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="099e5-229">Развертывание пакета приложения большего размера</span><span class="sxs-lookup"><span data-stu-id="099e5-229">Deploy large application package</span></span>
<span data-ttu-id="099e5-230">Проблема. Время ожидания выполнения команды [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) истекает для пакета большого приложения (несколько ГБ).</span><span class="sxs-lookup"><span data-stu-id="099e5-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="099e5-231">Попробуйте выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="099e5-231">Try:</span></span>
- <span data-ttu-id="099e5-232">Задайте большее время ожидания для команды [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) с помощью параметра `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="099e5-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="099e5-233">По умолчанию hello время ожидания составляет 30 минут.</span><span class="sxs-lookup"><span data-stu-id="099e5-233">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="099e5-234">Проверьте hello сетевого подключения между исходным компьютером и кластера.</span><span class="sxs-lookup"><span data-stu-id="099e5-234">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="099e5-235">Если используется медленное подключение hello, рассмотрите возможность использования на машине для улучшения подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="099e5-235">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="099e5-236">Если hello клиентский компьютер находится в другом регионе hello кластера, рекомендуется использовать клиентский компьютер в регионе, подробный или же hello кластера.</span><span class="sxs-lookup"><span data-stu-id="099e5-236">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="099e5-237">Проверьте, достигнуто ли внешнее регулирование.</span><span class="sxs-lookup"><span data-stu-id="099e5-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="099e5-238">Например при хранилища azure настроенных toouse hello хранилища образов может регулирование передачи.</span><span class="sxs-lookup"><span data-stu-id="099e5-238">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="099e5-239">Проблема. Загрузка пакета завершена успешно, но время ожидания для выполнения команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) истекает. Попробуйте выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="099e5-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out. Try:</span></span>
- <span data-ttu-id="099e5-240">[Сжатие пакета hello](service-fabric-package-apps.md#compress-a-package) перед копированием toohello хранилища образов.</span><span class="sxs-lookup"><span data-stu-id="099e5-240">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="099e5-241">Hello Сжатие уменьшает размер hello и запускать hello число файлов, который в свою очередь, снижает объем трафика в hello и работать, Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="099e5-241">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="099e5-242">операции выгрузки Hello может требоваться (особенно при включении hello сжатия времени), однако скорости регистрации и отмены регистрации типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="099e5-242">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="099e5-243">Задайте большее время ожидания для выполнения команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) с помощью параметра `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="099e5-243">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="099e5-244">Задайте параметр `Async` для команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="099e5-244">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="099e5-245">Команда Hello возвращает hello кластера принимает команды hello и hello регистрация типа приложения hello продолжается асинхронно.</span><span class="sxs-lookup"><span data-stu-id="099e5-245">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span> <span data-ttu-id="099e5-246">По этой причине нет нет необходимости toospecify большее значение времени ожидания в данном случае.</span><span class="sxs-lookup"><span data-stu-id="099e5-246">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="099e5-247">Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) команда выводит список всех версий типа успешно зарегистрированного приложения и состояние их регистрации.</span><span class="sxs-lookup"><span data-stu-id="099e5-247">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="099e5-248">После завершения регистрации hello toodetermine этой команды можно использовать.</span><span class="sxs-lookup"><span data-stu-id="099e5-248">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="099e5-249">Развертывание пакета приложения с несколькими файлами</span><span class="sxs-lookup"><span data-stu-id="099e5-249">Deploy application package with many files</span></span>
<span data-ttu-id="099e5-250">Проблема. Время ожидания для выполнения команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) истекает для пакета приложения с несколькими файлами (несколько тысяч).</span><span class="sxs-lookup"><span data-stu-id="099e5-250">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="099e5-251">Попробуйте выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="099e5-251">Try:</span></span>
- <span data-ttu-id="099e5-252">[Сжатие пакета hello](service-fabric-package-apps.md#compress-a-package) перед копированием toohello хранилища образов.</span><span class="sxs-lookup"><span data-stu-id="099e5-252">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="099e5-253">Hello Сжатие уменьшает число hello файлов.</span><span class="sxs-lookup"><span data-stu-id="099e5-253">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="099e5-254">Задайте большее время ожидания для выполнения команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) с помощью параметра `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="099e5-254">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="099e5-255">Задайте параметр `Async` для команды [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="099e5-255">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="099e5-256">Команда Hello возвращает hello кластера принимает команды hello и hello регистрация типа приложения hello продолжается асинхронно.</span><span class="sxs-lookup"><span data-stu-id="099e5-256">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span>
<span data-ttu-id="099e5-257">По этой причине нет нет необходимости toospecify большее значение времени ожидания в данном случае.</span><span class="sxs-lookup"><span data-stu-id="099e5-257">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="099e5-258">Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) команда выводит список всех версий типа успешно зарегистрированного приложения и состояние их регистрации.</span><span class="sxs-lookup"><span data-stu-id="099e5-258">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="099e5-259">После завершения регистрации hello toodetermine этой команды можно использовать.</span><span class="sxs-lookup"><span data-stu-id="099e5-259">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="099e5-260">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="099e5-260">Next steps</span></span>
[<span data-ttu-id="099e5-261">Обновление приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="099e5-261">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="099e5-262">Общие сведения о работоспособности Service Fabric</span><span class="sxs-lookup"><span data-stu-id="099e5-262">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="099e5-263">Диагностика и устранение неполадок службы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="099e5-263">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="099e5-264">Моделирование приложения в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="099e5-264">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
